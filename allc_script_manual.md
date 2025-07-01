# Prerequisites

To start having fun with allc data processing, you'd have to follow some steps to get started. 

1. connect to a Salk domain Wi-Fi.

      *Note: use vpn outside of salk for server access.*
   
2. `ssh` login with your credentials.

      This gives you access to salk server.
   
3. `qlogin -l h_vmem=30G`

   This connects you to a login node for lightweight tasks and file access. Use `qsub` to connect to SGE 8.1.6 — Sun Grid Engine for heavy computation tasks.

4. `cd /ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/`

5.  `qsub -N NAME -V -cwd -l mem_free=10G,h_vmem=10G,qname=gale.q -v YOUR_VARIABLE=X YOUR_SCRIPT.sh` (for heavy tasks)

---

**for the remaining manual, refer to current working directory as `/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/`*


---


# `allc_merge.sh`

This shell script runs `allcools merge-allc` to merge `.allc.tsv.gz` files for 16 clusters using input path files (e.g., `clst0_allc_paths.txt`). **If you need parallel processing via the cluster see `allc_singular.sh` and `allc_submit.sh`.**

# `allc_merge_singular.sh`

This script merges `.allc.tsv.gz` files for a **single cluster** using `allcools merge-allc`. It is designed to be callable with `allc_submit.sh` as batch jobs.

## Usage

if you need to just process a single cluster, pass the cluster number via the `CLST` environment variable:

```bash
qsub -v CLST=X allc_merge_singular.sh
````

The script will:

* Check for the presence of `clstX_allc_paths.txt` under `./path_allc_bam_each_clst`
* Create the output directory (if missing)
* Run `allcools merge-allc`
* Log the output to ./logs

## Chromosome data:

`  /gale/raidix/rdx-7/tnobori/tools/YAP/reference_files/Arabidopsis_thaliana.TAIR10.dna.toplevel_chrL_appended_sizes.genome`

* Output directory: `merged_allc_by_clst_debug/` (custom for debugging)

```

> *insightful quote from jimmy:*
>
> "One cluster, one shot, one genome — no retries."
>
> — *James Walker, 2025*

```
# `allc_submit.sh`

This script submits **one job per cluster** to merge `.allc.tsv.gz` files using `allc_merge_singular.sh`.

## What It Does

- Loops over clusters
- Submits a job (`qsub`) for each cluster
- Passes the cluster ID to the script via the `CLST` environment variable

## Inputs

- `allc_merge_singular.sh` – the job script for merging
- Input paths:  
  `./path_allc_bam_each_clst/clstX_allc_paths.txt`

- Chromosome size file:  
  `/gale/raidix/rdx-7/tnobori/tools/YAP/reference_files/Arabidopsis_thaliana.TAIR10.dna.toplevel.chrom.sizes`

## Outputs

- Merged `.allc.tsv.gz` files saved to:  
  `/ceph/MethDev/JW240627--at-snmCT_with_TE/mCT_with_TE/merged_allc_by_clst_debug/clstX.allc.tsv.gz`

- Logs:  
  Written per job by `allc_merge_singular.sh` to the `logs/` directory


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

