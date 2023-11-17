# EDA on DNA Methylation
This is a private repository dedicated to various data anlysis tasks related to DNA methylation, under James Walker's supervision, Ecker Lab. There will (estimated) be four parts to this repository: 

- Nanopore genome sequencing data for 5mC and 6mA
- Processing Single Nucleus Methylatyed Cytosine and Transcriptome (snmCT) seqencing data via Yet Another Pipeline ([YAP](https://hq-1.gitbook.io/mc/))
- Creating a heatmap of expression (and optimizing performance) for groups of genes.
- Gene methylation / RNA correlation analysis from ore-existing scripts.

Within each task folder, there will be a rough overview of the task, tools or pipelines necessary, and raw data required to perform analysis and plotting. 

---
# First-time Setup 
Here is a guide to running a Jupyter Notebook on the compute nodes instead using the log-in cluster:

1. Ensure Internet connection is routed via Salk Wifi or Salk VPN.
2. start a new screen using:  `screen -R jbn`
3. Request an interactive login to a compute cluster: `qlogin -l h_vmem=5G -q gale.q@gale-cluster-*.salk.edu -pe smp 5` (*replace asterisk (***) with username*)
4. Activate desired conda environment
   *(You can visualize all environments by `conda env list`)*
5. Start your jupyter notebook by entering:  `jupyter notebook --ip 0.0.0.0 --no-browser --port 445928 --NotebookApp.max_buffer_size=26843545600`

\
*Note:\
`--ip` must be 0.0.0.0 in order to work (localhost doesn't).\
`--NotebookApp.max_buffer_size= 26843545600` is the number of bytes of memory requested.\
R kernel in jupyter is a bit clunky so this must be specified or else the default max memory setting in R is very small.*

# Globus File Manager
A platform enabling file transfers between servers, e.g. from local to GAL-E.
![image](https://github.com/kqu18/Ecker_Methylation_Analysis/assets/104349171/11b953ee-c54b-49b1-b115-679c0f512821)



# Known Issues

## Unable to use `qlogin` (no command called `qlogin`):

1. Open up terminal
2. Enter text editor by command `sudo vi /etc/ssh/ssh_config` (or other text editor of your choice)
3. insert new line at bottom (Press O)
4. Copy and Paste the following:
```
HostkeyAlgorithms +ssh-rsa
PubkeyAcceptedAlgorithms +ssh-rsa
```
5. Press `Esc` to exit insert mode then save your changes with `ZZ` or `:wq`.

## jupyter environment launch issue

Due to difference in conda environmets, sometimes there will be missing dependencies leading to error starting jupyter lab or jupyter notebook. 

In this scenario, you should first try swapping between jupyter lab and jupyter notebook. 

e.g. between \
`jupyter lab --ip 0.0.0.0 --no-browser --port 65535 --NotebookApp.max_buffer_size=26843545600` \
and \
`jupyter notebook --ip 0.0.0.0 --no-browser --port 65535 --NotebookApp.max_buffer_size=26843545600`



