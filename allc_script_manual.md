
# AllCools Processing Pipeline Manual

## Directories

### Part 1. Background and Environment Setup
- [AllCools and its data structures](#background---allcools)
- [Setup Instructions](#prerequisites)  
  → SSH, qlogin, and working directory setup.

---

### Part 2. Scripts

#### 🔁 Processing Scripts
- [`parse_allc_by_genotype.sh`](#parse_allc_by_genotypesh)  
  → Parses `allc.tsv.gz` paths by cluster and genotype.

- [`allc_merge.sh`](#allc_mergesh)  
  → Merges all `.allc.tsv.gz` files per cluster using `allcools merge-allc`.

- [`allc_merge_per_genotype.sh`](#allc_merge_per_genotypesh)  
  → Merges `.allc.tsv.gz` by **genotype** within a single cluster.

#### 📤 Submission Wrappers
- [`allc_submit.sh`](#allc_submitsh)  
  → Submits one job per cluster for genotype-specific merges.

- [`gff_submit.sh`](#gff_submitsh)  
  → Submits one job per cluster to run `gff_creator.sh`.

#### 🧬 Output Generators
- [`gff_creator.sh`](#gff_creatorsh)  
  → Generates `.gff` files (w1 and w100) per context and genotype.

---

### 🧷 Miscellaneous & Tips

- [Qsub Command Tips](#other-miscellaneous-useful-life-hacks)  
  → Filter or delete SGE tasks using `qstat`, `grep`, and `qdel`.

- [Helpful Quotes](#how-it-classifies)  
  → Wisdom from Jimmy (real and imagined).



---
# Background - AllCools
## 📦 What is `allcools`?

[`allcools`](https://github.com/methylgrammarlab/allcools) is a command-line toolkit for efficient and scalable processing of **single-cell and bulk DNA methylation data** in the `allc` file format. It is designed to support workflows for:

- Parsing and merging `.allc.tsv.gz` files
- Genome-wide methylation aggregation
- GFF file generation for visualization and analysis
- Integration with downstream tools (e.g., methylation clocks, clustering, etc.)

It supports parallelization and large-scale processing using cluster computing environments like SGE or SLURM.

---

## 📄 What are `.allc.tsv.gz` Files?

`.allc.tsv.gz` files (referred to as **allc files**) are the output of single-cell or bulk methylation processing pipelines (e.g., from `methylpy`). Each file contains **per-cytosine** methylation information across the genome for a given sample or cell.

These files are **tab-separated**, compressed with `gzip`, and are structured for fast aggregation and filtering.

---

## 🧬 Format of a Typical `.allc` File

Each `.allc.tsv.gz` file typically contains the following **6 columns**:

| Column # | Name                  | Description |
|----------|-----------------------|-------------|
| 1        | `chrom`               | Chromosome name (e.g., `chr1`, `chr3`, `chrM`) |
| 2        | `pos`                 | 1-based genomic coordinate of the cytosine |
| 3        | `strand`              | DNA strand: `+` or `-` |
| 4        | `context`             | Sequence context of the cytosine site (e.g., `CG`, `CHG`, `CHH`) |
| 5        | `mc`                  | Number of **methylated** reads at this position |
| 6        | `cov`                 | Total number of reads covering this position (methylated + unmethylated) |

---

### 📝 Example Row

```tsv
chr1    10468   +   CG  3   5
```

This means:

- Chromosome: `chr1`
- Position: `10468`
- Strand: `+`
- Context: `CG`
- 3 methylated reads out of 5 total reads at that cytosine site

---

## 🧪 Notes

- We use the three contexts (`CG`, `CHG`, `CHH`) but allcools files might contain raw nucleobases which requires conversion.

---


## 📂 What are GFF Files?

GFF stands for **General Feature Format** — a standard tab-delimited format used to describe features (e.g., genes, regions, windows) on a genome. In the context of **DNA methylation analysis**, especially when using [`allcools`](https://github.com/methylgrammarlab/allcools), GFF files are used to represent **binned or windowed methylation levels** across the genome for visualization and analysis.

These files are typically generated using `allcools gff-create`, and are compatible with genome browsers or plotting tools.

---

## 🗂️ Structure of a Typical GFF File

Each GFF file line represents a **genomic window** (e.g., 100bp or 1000bp) with aggregated methylation statistics. `allcools`-generated GFF files often use a **custom GFF-like format** optimized for methylation.

A typical `.gff` file contains the following **9 columns**:

| Column # | Name         | Description |
|----------|--------------|-------------|
| 1        | `seqname`    | Chromosome or scaffold name (e.g., `chr1`) |
| 2        | `source`     | Source of annotation (commonly `allcools`) |
| 3        | `feature`    | Feature type (e.g., `methylation`) |
| 4        | `start`      | Start position of the window (1-based) |
| 5        | `end`        | End position of the window |
| 6        | `score`      | Methylation score (e.g., methylation ratio) |
| 7        | `strand`     | Strand (`+` or `.` — often strandless for methylation) |
| 8        | `frame`      | Always `.` — unused |
| 9        | `attribute`  | Key-value pairs (e.g., `context=CG;mc=25;cov=50`) |

---

### 📝 Example Row

```tsv
chr1    allcools    methylation    1000    1100    0.5    .    .    context=CG;mc=25;cov=50
```

This describes:

- A 100bp window on `chr1`, from position 1000 to 1100
- Aggregated **CG methylation** ratio of `0.5` (25/50 reads methylated)
- Metadata in `attribute` field: context type, methylated count (`mc`), total coverage (`cov`)

---

## 🧪 Common Use Cases

- Visualizing genome-wide methylation in tools like IGV or UCSC Genome Browser
- Comparing methylation patterns between cell types or genotypes
- Feeding into downstream analysis pipelines (e.g., DMR calling)

---

## 🏷️ GFF File Variants

When generating GFFs with `allcools`, you might see variations like:

- `w100.gff` → 100bp windows  
- `w1.gff` → single-base resolution  
- Context-specific GFFs: `CG.gff`, `CHG.gff`, `CHH.gff`

These are usually generated **per cluster and genotype** using `gff_creator.sh`.

---


# Prerequisites/setup

To start having fun with allc data processing, you'd have to follow some steps to get started. 

1. connect to a Salk domain Wi-Fi.

      *Note: use Cisco Anyconnect 4.X outside of salk for server access.*
   
2. `ssh` login with your credentials.

      This gives you access to salk server.
   
3. `qlogin -l h_vmem=30G`

   This connects you to a login node for lightweight tasks and file access. Use `qsub` to connect to SGE 8.1.6 — Sun Grid Engine for heavy computation tasks.

4. `cd /ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/`

5.  `qsub -N NAME -V -cwd -l mem_free=10G,h_vmem=10G,qname=gale.q -v YOUR_VARIABLE=X YOUR_SCRIPT.sh` (for heavy tasks)

---

**for the remaining manual, refer to current working directory as `/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/`*


---
# Shell scripts

## Cluster CSV to Path TXT (Shell Script)

This shell script (`clst_csv_to_path_txt.sh`) reads a CSV file containing Cell IDs and cluster assignments. It generates a separate text file for each cluster, listing the full paths to each cell's `allc.tsv.gz` file.

## Features
* **Mode Support:** Accepts optional arguments (e.g., `SS`, `WW`) to process specific input files (e.g., `cell_cluster_assignment.SS.csv`).
* **Windows Compatibility:** Automatically strips hidden Windows carriage return (`\r`) characters from input files to prevent path errors.

## Input Requirements

### 1. Cluster Assignment File
The script looks for a CSV file in the same directory. The filename depends on how you run the script:

* **Default Mode:** Looks for `cell_cluster_assignment.csv`.
* **Argument Mode (e.g., "SS"):** Looks for `cell_cluster_assignment.SS.csv`.

**CSV Format:**
Must contain a header row, followed by two columns:
1. `cell_id`: The unique cell identifier.
2. `merged_cluster`: The cluster number.

**Example:**
```csv
cell_id,merged_cluster
NJ_221007_P1-2-K15-J3,0
NJ_221007_P1-2-K15-E16,1
```

### 2. `allc` File Directory Structure
The script assumes the data resides in a specific root directory defined by the `BASE_PATH` variable inside the script.

**Default Base Path:** `/ceph/MethDev/Arab6_with_TE/mCT_with_TE`

**Assumed Structure:**
```text
/ceph/MethDev/Arab6_with_TE/mCT_with_TE/
├── NJ_221007_P1-2-K15/              <-- Derived Directory Name
│   └── allc/
│       ├── NJ_221007_P1-2-K15-J3.allc.tsv.gz
│       └── ...
└── ...
```

## How It Constructs Paths

The script generates the full file path by combining components:

1. **`base_path`**: Hardcoded in the script.
2. **`dir_name`**: Derived from `cell_id` by removing the text after the last hyphen.
   * *Example:* `NJ_221007_P1-2-K15-J3` → `NJ_221007_P1-2-K15`
3. **`cell_id`**: The full ID from the CSV.

**Final Path Format:**
`{base_path}/{dir_name}/allc/{cell_id}.allc.tsv.gz`

## Running the Script

First, ensure the script is executable:
```bash
chmod +x clst_csv_to_path_txt.sh
```

### Option A: Default Behavior
Processes `cell_cluster_assignment.csv` and outputs standard text files.
```bash
./clst_csv_to_path_txt.sh
```

### Option B: With Optional Argument (e.g., SS or WW)
Processes `cell_cluster_assignment.SS.csv` and adds `.SS` to the output filenames.
```bash
./clst_csv_to_path_txt.sh SS
```
*(You can replace `SS` with `WW` or any other suffix).*

## Output

The script outputs to the directory: `path_allc_bam_each_clst/`.

**Example Output (Default Run):**
```text
./path_allc_bam_each_clst/
├── clst0_allc_paths.txt
├── clst1_allc_paths.txt
└── ...
```

**Example Output (Run with "SS" argument):**
```text
./path_allc_bam_each_clst/
├── clst0_allc_paths.SS.txt
├── clst1_allc_paths.SS.txt
└── ...
```

**Example File Content:**
```text
/ceph/MethDev/Arab6_with_TE/mCT_with_TE/NJ_221007_P1-2-K15/allc/NJ_221007_P1-2-K15-J3.allc.tsv.gz
/ceph/MethDev/Arab6_with_TE/mCT_with_TE/NJ_221007_P1-2-K15/allc/NJ_221007_P1-2-K15-C15.allc.tsv.gz
```

## Notes
1. **Edit Base Path:** If your server directory changes, you must edit the `BASE_PATH` variable at the top of `clst_csv_to_path_txt.sh`.
2. **Windows Fix:** The script includes a safety feature (`gsub(/\r/, "")`) to handle CSV files created on Windows, preventing errors with file paths containing hidden return characters.

## `parse_allc_by_genotype.sh`

This shell script takes in a directory containing multiple `...allc_paths.txt`, each containing `allc.tsv.gz` files and parses them by cluster (clst0, clst1...) and genotype (`col`, `rdd`, `met`) using `mct_x_y` identifiers embedded in the file paths.

### Example Directory Structure

```
/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/
├── path_allc_bam_each_clst/
│   ├── clst0_allc_paths.txt
│   ├── clst1_allc_paths.txt
│   ├── clst2_allc_paths.txt
│   └── ... (current script set to 16)
└── path_allc_bam_genotype_clst/   # (output folder created before script)
```

Each line in the .txt files is a full path like:

```
/.../mCT_with_TE/240614_mct_1_2_P1-2-O5/allc/240614_mct_1_2_P1-2-O5-H3.allc.tsv.gz
```
### How It Classifies
The script classifies genotype based on the `mct_x_y` portion:

* `mct_1_y` → `col`
* `mct_2_y` → `rdd`
* `mct_3_y` → `met`

*insightful quote from jimmy:*

> -1 is 2C -2 is 4C -3 is 8C and -4 is 16C but that doesn’t matter like we talked about.
>
> ---James walker, 2025

### Running the Script

1. Make sure the output directory exists:

   ```bash
   mkdir -p /ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/path_allc_bam_genotype_clst/
   ```

2. Run the script:
   ```bash
   chmod +x parse_allc_by_genotype.sh
   ./parse_allc_by_genotype.sh
   ```

### Output

Creates 3 files per cluster in `path_allc_bam_genotype_clst/`, e.g.:

* `clst0_col_allc_paths.txt`
* `clst0_rdd_allc_paths.txt`
* `clst0_met_allc_paths.txt`

### Notes

* Lines without an `mct_x_y` pattern are skipped with a warning.
* Make sure all file paths and formats follow the expected conventions.

---


## `allc_merge.sh`
*Jimmy's legacy code.*

This shell script runs `allcools merge-allc` to merge `.allc.tsv.gz` files for 16 clusters using input path files (e.g., `clst0_allc_paths.txt`). **If you need parallel processing via the cluster or merge with specififc genotypes see `allc_merge_per_genotype.sh` and `allc_submit.sh`.**

## `allc_merge_per_genotype.sh`

This script merges `.allc.tsv.gz` files for a **single cluster per each of the three genotype\* (specified below)** using `allcools merge-allc`. It is designed to be callable with `allc_submit.sh` as batch jobs.

### Usage

if you need to just process a single cluster, pass the cluster number via the `CLST` environment variable:

```bash
qsub -N NAME -V -cwd -l mem_free=10G,h_vmem=10G,qname=gale.q -v YOUR_VARIABLE=X YOUR_SCRIPT.sh
````

The script will:

* Check for the presence of `clstX_allc_paths.txt` under `./path_allc_bam_each_clst`
* Create the output directory (if missing)
* Run `allcools merge-allc`
* Log the output to ./logs

### Notes

Chromosome data: `  /gale/raidix/rdx-7/tnobori/tools/YAP/reference_files/Arabidopsis_thaliana.TAIR10.dna.toplevel_chrL_appended_sizes.genome`

**\*** Genotypes: col, met, rdd


*insightful quote from ChatGPT's interpretive hallucination of Jimmy:*
>
> "One cluster, one shot, one genome — no retries."
>
> — *Not James Walker, 2025*

---

## `allc_submit.sh`

This script submits **one job per cluster** to merge `.allc.tsv.gz` files using `allc_merge_per_genotype.sh`. Of course, you can automate other scripts by changing the script to run. 

### What It Does

- Loops over clusters and submits a job (`qsub`) for each cluster
- Passes the cluster ID to the script via the `CLST` environment variable

### Outputs

- Merged `.allc.tsv.gz` files saved to:  
  `/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/merged_allc_by_clst_genotype/clstX.GENOTYPE.allc.tsv.gz`

- Logs:  
  Written per inner job to the `logs/` directory

---

## `gff_creator.sh`

### What it does
- takes all allc files from e.g. `$MERGED_DIR`
- creates w1 and w100 windowed gff files per methylation context per genotype.

### Outputs
- gff files saved to `./gffs_by_clst_genotype`

---

## `gff_submit.sh`

This script submits **one job per cluster** to create gff files using `gff_creator.sh`. Of course, you can automate other scripts by changing the script to run. 

### What It Does

- Loops over clusters and submits a job (`qsub`) for each cluster
- Passes the cluster ID to the script via the `CLST` environment variable

### Outputs
- follows the script ran.

---

## `create_intersect.sh`

This script runs `bedtools intersect` on each mutants and each contexts

### Outputs
- gff files with overlapping regional information under ./master_gffs/intersects

---


## `filter_w100_gffs_by_ctx_meth_ct.sh`

### What it does
filters gff files in bulk gff paths and categorizes w100 gffs in `./gffs_by_clst_genotype` with:
 -  certain c+t threshold (set to c+t>=5)
 -  methylation score respective to the context
       thresholds["CG"]=0.2
       thresholds["CHG"]=0.1
       thresholds["CHH"]=0.05

### Outputs
- results saved to `~/filtered_w100_gffs_by_clst_genotype/filtered_CONTEXT_w100_gffs_by_clst_genotype` directory
- 
## `aggregate_gffs.sh`

### What it does
keeps unique location of gffs after aggregation by rounding postional information to the nearest 100s (in accordance with w100 windows) and only keeps chr1-5.

## Input

```
/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/
├── filtered_w100_gffs_by_clst_genotype/
│   ├── filtered_CG_w100_gffs_by_clst_genotype/
│   ├── filtered_CHG_w100_gffs_by_clst_genotype/
│   ├── filtered_CHH_w100_gffs_by_clst_genotype/
└── 
```

## Output 
Yields outer-joined UNIQUE location information of the input folders as `master_{mutant}.{context}.JW.gff` under `~/master_gffs/`

## Note
submit as cluster job per context by `submit_aggregation.sh`

---

## `run_intersect.sh`

### What it does
- performs `bedtools intersect` on master gffs and gene segment of interest (e.g. euchromatic/heterochromatic regions)
- left outer join (-wa) so all location matching on master gff will be kept (-a, first argument)

### Input
- master gffs in `~/master_gffs/`
- gene regions gffs in `~/master_gffs/andy_lowercase/`

### Outputs
- intersect_x_and_y.gff under `~/master_gffs/intersects/`

## `meth_hist_ct5.ipynb`

### what it does
- plots methylation profile per cluster per context as a histogram for w100 gff files in a specified directory.
- note: adding grid will slow down generation in notebook
  
### Outputs
- directly print out graphs, optionally use parallel processing

---


## Other Miscellaneous useful life hacks

### qsub:
- check task ID with certain keyword: `qstat -u $USER | grep KEYWORD | awk '{print $1}'`
- delete task ID with certain keyword:`qstat -u $USER | grep mrg | awk '{print $1}' | xargs qdel` (*Do not delete all tasks or Jimmy will be mad!!!*)

- hetero genes - CHG, dont care.
- euchro gene - CG, euchro transposons - CHG, hetero trans - CHG
