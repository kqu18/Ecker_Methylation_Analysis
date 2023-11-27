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

### Step 1. mapping_config.ini

change input and output directories to fit for specific project by modifying `.ini` file via nano.

### Step 2. Demultiplex


