

## Directories for everything in this manual
click on the links for details.

### Part 1. Prerequisites & Setup
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


# Prerequisites

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

# `parse_allc_by_genotype.sh`

This shell script takes in a directory containing multiple `...allc_paths.txt`, each containing `allc.tsv.gz` files and parses them by cluster (clst0, clst1...) and genotype (`col`, `rdd`, `met`) using `mct_x_y` identifiers embedded in the file paths.

## Example Directory Structure

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
## How It Classifies
The script classifies genotype based on the `mct_x_y` portion:

* `mct_1_y` → `col`
* `mct_2_y` → `rdd`
* `mct_3_y` → `met`

*insightful quote from jimmy:*

> -1 is 2C -2 is 4C -3 is 8C and -4 is 16C but that doesn’t matter like we talked about.
>
> ---James walker, 2025

## Running the Script

1. Make sure the output directory exists:

   ```bash
   mkdir -p /ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/path_allc_bam_genotype_clst/
   ```

2. Run the script:
   ```bash
   chmod +x parse_allc_by_genotype.sh
   ./parse_allc_by_genotype.sh
   ```

## Output

Creates 3 files per cluster in `path_allc_bam_genotype_clst/`, e.g.:

* `clst0_col_allc_paths.txt`
* `clst0_rdd_allc_paths.txt`
* `clst0_met_allc_paths.txt`

## Notes

* Lines without an `mct_x_y` pattern are skipped with a warning.
* Make sure all file paths and formats follow the expected conventions.

---


# `allc_merge.sh`
*Jimmy's legacy code.*

This shell script runs `allcools merge-allc` to merge `.allc.tsv.gz` files for 16 clusters using input path files (e.g., `clst0_allc_paths.txt`). **If you need parallel processing via the cluster or merge with specififc genotypes see `allc_merge_per_genotype.sh` and `allc_submit.sh`.**

# `allc_merge_per_genotype.sh`

This script merges `.allc.tsv.gz` files for a **single cluster per each of the three genotype\* (specified below)** using `allcools merge-allc`. It is designed to be callable with `allc_submit.sh` as batch jobs.

## Usage

if you need to just process a single cluster, pass the cluster number via the `CLST` environment variable:

```bash
qsub -N NAME -V -cwd -l mem_free=10G,h_vmem=10G,qname=gale.q -v YOUR_VARIABLE=X YOUR_SCRIPT.sh
````

The script will:

* Check for the presence of `clstX_allc_paths.txt` under `./path_allc_bam_each_clst`
* Create the output directory (if missing)
* Run `allcools merge-allc`
* Log the output to ./logs

---

Chromosome data: `  /gale/raidix/rdx-7/tnobori/tools/YAP/reference_files/Arabidopsis_thaliana.TAIR10.dna.toplevel_chrL_appended_sizes.genome`

**\*** Genotypes: col, met, rdd


> *insightful quote from ChatGPT's interpretive hallucination of Jimmy:*
>
> "One cluster, one shot, one genome — no retries."
>
> — *Not James Walker, 2025*

---

# `allc_submit.sh`

This script submits **one job per cluster** to merge `.allc.tsv.gz` files using `allc_merge_per_genotype.sh`. Of course, you can automate other scripts by changing the script to run. 

## What It Does

- Loops over clusters and submits a job (`qsub`) for each cluster
- Passes the cluster ID to the script via the `CLST` environment variable

## Outputs

- Merged `.allc.tsv.gz` files saved to:  
  `/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/merged_allc_by_clst_genotype/clstX.GENOTYPE.allc.tsv.gz`

- Logs:  
  Written per inner job to the `logs/` directory

---

# `gff_creator.sh`

## What it does
- takes all allc files from e.g. `$MERGED_DIR`
- creates w1 and w100 windowed gff files per methylation context per genotype.

## Outputs
- gff files saved to `./gffs_by_clst_genotype`

---

# `gff_submit.sh`

This script submits **one job per cluster** to create gff files using `gff_creator.sh`. Of course, you can automate other scripts by changing the script to run. 

## What It Does

- Loops over clusters and submits a job (`qsub`) for each cluster
- Passes the cluster ID to the script via the `CLST` environment variable

## Outputs
- follows the script ran.


# Other Miscellaneous useful life hacks

## qsub:
- check task ID with certain keyword: `qstat -u $USER | grep KEYWORD | awk '{print $1}'`
- delete task ID with certain keyword:`qstat -u $USER | grep mrg | awk '{print $1}' | xargs qdel` (*Do not delete all tasks or Jimmy will be mad!!!*)
