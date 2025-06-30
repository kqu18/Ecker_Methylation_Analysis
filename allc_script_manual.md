
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

