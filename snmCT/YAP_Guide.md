# YAP tutorial
This document will be a walkthrough of how to process snmCT data with [YAP](https://hq-1.gitbook.io/mc/). 

You should work within `/ceph/MethDev/` after `qlogin` but you will still be able to access `gale`.

---

### Directories for directories

Arabidopsis: `/gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/`

Marchantia: `/gale/raidix/rdx-7/jwalker/Marchantia_reference/`

*Processed* Novaseq data: `/gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/`

Arabidopsis reference files: `/gale/raidix/rdx-7/jwalker/YAP/reference_files/`

demux script: `/gale/raidix/rdx-7/jwalker/Marchantia_reference/miseq_demux.sh`

---

### Useful commands
``
`zcat`
`| less`
`grep`
`ls -lsat`
`history`
`| head`

---

### File Formats

For background on file formats (FASTA, FASTQ, SAM) check [here](https://bioinformatics.stackexchange.com/questions/14/what-is-the-difference-between-fasta-fastq-and-sam-file-formats).

*FASTA Example: *
```
>Mus_musculus_tRNA-Ala-AGC-1-1 (chr13.trna34-AlaAGC)
GGGGGTGTAGCTCAGTGGTAGAGCGCGTGCTTAGCATGCACGAGGcCCTGGGTTCGATCC
CCAGCACCTCCA
>Mus_musculus_tRNA-Ala-AGC-10-1 (chr13.trna457-AlaAGC)
GGGGGATTAGCTCAAATGGTAGAGCGCTCGCTTAGCATGCAAGAGGtAGTGGGATCGATG
CCCACATCCTCCA
```
*FASTQ Example:  (Q for Quality)*
```
@071112_SLXA-EAS1_s_7:5:1:817:345
GGGTGATGGCCGCTGCCGATGGCGTC
AAATCCCACC
+
IIIIIIIIIIIIIIIIIIIIIIIIII
IIII9IG9IC
@071112_SLXA-EAS1_s_7:5:1:801:338
GTTCAGGGATACGACGTTTGTATTTTAAGAATCTGA
+
IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII6IBI
```

*BAM (SAM )Exaple: (B for Binary)*
```
r001  99  chr1  7 30  17M         =  37  39  TTAGATAAAGGATACTG   IIIIIIIIIIIIIIIII
r002  0   chrX  9 30  3S6M1P1I4M  *  0   0   AAAAGATAAGGATA      IIIIIIIIII6IBI    NM:i:1
```

### Step 1. Obtain FASTQ files

Several options. Download from internet, use pre-existing dataset, etc.

`samtools view novaseq_demux/NJ_221007_P1-1-K15/bam/NJ_221007_P1-1-K15-E2.dna_reads.bam | less`

### Step 2. Login
`qlogin -l h_vmem=4G`

### Step 3. Setup mapping config and run script for demultiplexing

before running, change input and output directories to fit for specific project by modifying `.ini` file via nano.


`qsub -V -cwd -l mem_free=100G,h_vmem=100G,qname=gale.q miseq_demux.sh`

miseq_demux.sh:

`yap demultiplex -fq "/gale/netapp/seq12/illumina_runs/230523_A00280_0656_AH7CLYDSX7_230525125757678577423/Pool_arab_7/*.fastq.gz" -config ./mappingconfig_marchantia_mCT_Nova.ini -o Novaseq_demux_mCT  -j 16`

check status by:
`qstat -u jwalker`

### mapping via qsub

After demultiplexing, all the snakemake command is also summarized in the `{output_dir}/snakemake/qsub` directory. 

```
conda activate mapping
qsub qsub.sh
```

The hallmark of successful snakemake execution is the existence of an MappingSummary.csv.gz in that sub-directory. Because this file is the final target of the snakemake. This file will only occur when all the previous mapping commands are executed successfully.

### check result

Each cell will have two FASTQ files in the output directory, with a fixed name pattern:

{cell_id}-R1.fq.gz for R1
{cell_id}-R2.fq.gz for R2

If error, check `Novaseq_demux_mCT_0.error.log`.

If error with Snakefile, make updates with `yap update-snakemake`[ref](https://snakemake.readthedocs.io/en/stable/).





