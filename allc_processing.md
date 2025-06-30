
# ALLC Merge Pipeline (SGE Batch Submission)

This repository contains scripts to batch-merge single-cell ALLC files using `allcools merge-allc` across multiple cell clusters, submitted as parallel jobs on an SGE (Sun Grid Engine) cluster using `qsub`.

---

## 📁 Project Layout

```

project\_dir/
├── allc\_merge.sh               # Per-cluster merge script (run on the cluster)
├── submit\_allc\_merges.sh       # Master job submission script
├── log/                        # Stdout/stderr logs for each job
├── merged\_allc\_by\_clst/        # Output merged ALLC files per cluster
├── path\_allc\_bam\_each\_clst/    # Input: file lists for each cluster (clst0\_allc\_paths.txt, etc.)

````

---

## 🚀 How to Use

### 1. Activate the environment

Ensure `allcools` is installed and accessible:

```bash
conda activate allcools
````

### 2. Submit the jobs

```bash
./submit_allc_merges.sh
```

This script will:

* Loop through clusters 0 to 16
* Submit one job per cluster (`clstX`)
* Log outputs to `./log/clstX.out` and `clstX.err`

---

## ⚙️ Configuration

Edit the following paths in `submit_allc_merges.sh`:

```bash
ChromSizePath="/path/to/your/Arabidopsis.chrom.sizes"
InPath="/.../path_allc_bam_each_clst"
OutPath="/.../merged_allc_by_clst"
LogPath="./log"
```

Each input file should be named:

```
clst0_allc_paths.txt
clst1_allc_paths.txt
...
clst16_allc_paths.txt
```

Each file should list the paths to individual `.allc.tsv.gz` files that belong to the cluster.

---

## 📡 Monitoring Jobs

Check job status:

```bash
qstat
```

Inspect log output:

```bash
tail -f log/clst3.out
```

---

## 🧹 Cleanup & Retry

Cancel all submitted jobs:

```bash
qselect -N mrg_clst | xargs qdel
```

Clean up logs and outputs:

```bash
rm -f log/clst* merged_allc_by_clst/clst*.tsv.gz
```

To re-run only failed clusters, you can modify the loop in `submit_allc_merges.sh` to check if output files already exist:

```bash
if [[ ! -s ${OutPath}/clst${clst}.allc.tsv.gz ]]; then
    # submit job
fi
```

---

## 🐛 Troubleshooting

* **FileNotFoundError: `.chrom.sizes`**
  → Check that the file exists and the path is correct.

* **Job stuck in `qw` (queue waiting)**
  → May indicate cluster load. Use a different queue or retry later.

* **Output `.tsv.gz` file is empty**
  → Check that the input path file for that cluster is not empty or corrupted.

---

## 👤 Author & Acknowledgments

Maintained by \[Your Name or Lab Name]
Created June 2025
Tested on the Salk `gale.q` cluster

---

## 📌 Notes

* This pipeline is tailored for **Arabidopsis thaliana** data using `allcools >= 0.5.1`.
* Modify `qsub` flags (memory, queue, job name) in `submit_allc_merges.sh` to match your cluster's configuration.

```

Let me know if you'd like this turned into a GitHub wiki, webpage, or if you'd like a LaTeX or PDF version for internal documentation.
```
