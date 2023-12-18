# First-time setup:
- login to br1, then `qlogin`
- install `conda` or set env $PATH through your supervisor's conda (Jimmy's conda was used for this example)
- if conda fails to self-boot, use `source ./bashrc`


# location: (temp)

`/gale/netapp/home2/jwalker/`


# qlogin

1. `qlogin -l h_vmem=120G -l h=gale-10`

2. `screen -S Jptr_gale-10`

3. `reset`

4. `conda activate <env>`

5. `cd /gale/`

6. `jupyter notebook --ip 0.0.0.0 --no-browser --port 8886 --NotebookApp.max_buffer_size=66843545600`

jupyter lab --port=8886 --no-browser --ip `hostname`
