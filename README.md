# EDA on DNA Methylation
This is a private repository dedicated to various data anlysis tasks related to DNA methylation, under James Walker's supervision, Ecker Lab. There will (estimated) be four parts to this repository: 

- Nanopore genome sequencing data for 5mC and 6mA
- Processing Single Nucleus Methylatyed Cytosine and Transcriptome (snmCT) seqencing data via Yet Another Pipeline ([YAP](https://hq-1.gitbook.io/mc/))
- Creating a heatmap of expression (and optimizing performance) for groups of genes.
- Gene methylation / RNA correlation analysis from ore-existing scripts.

Within each task folder, there will be a rough overview of the task, tools or pipelines necessary, and raw data required to perform analysis and plotting. 

---
# First-time Setup 

## Connect to SSH

1. Open up terminal
2. Enter text editor by command `sudo vi /etc/ssh/ssh_config` (or other text editor of your choice)
3. insert new line at bottom (Press O)
4. Copy and Paste the following:
```
HostkeyAlgorithms +ssh-rsa
PubkeyAcceptedAlgorithms +ssh-rsa
```
5. Press `Esc` to exit insert mode then save your changes with `ZZ` or `:wq`.

# Known Issues

## jupyter environment launch issue

Due to difference in conda environmets, sometimes there will be missing dependencies leading to error starting jupyter lab or jupyter notebook. 

In this scenario, you should first try swapping between jupyter lab and jupyter notebook. 

e.g. between \
`jupyter lab --ip 0.0.0.0 --no-browser --port 65535 --NotebookApp.max_buffer_size=26843545600` \
and \
`jupyter notebook --ip 0.0.0.0 --no-browser --port 65535 --NotebookApp.max_buffer_size=26843545600`

