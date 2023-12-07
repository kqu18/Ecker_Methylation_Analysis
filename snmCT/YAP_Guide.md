# YAP tutorial
This document will be a walkthrough of how to process snmCT data with [YAP](https://hq-1.gitbook.io/mc/). 

YAP is a full pipeline designed for raw sequencing data (BCL files and raw FASTQ files before demultiplex) generated in the Ecker Lab.

You should work within `/ceph/MethDev/` after `qlogin` but you will still be able to access `gale`.

---

## Directories for directories

Arabidopsis: `/gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/`

Marchantia: `/gale/raidix/rdx-7/jwalker/Marchantia_reference/`

*Processed* Novaseq data: `/gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/`

Arabidopsis reference files: `/gale/raidix/rdx-7/jwalker/YAP/reference_files/`

demux script: `/gale/raidix/rdx-7/jwalker/Marchantia_reference/miseq_demux.sh`

---

## Useful commands
``
`zcat`
`| less`
`grep`
`ls -lsat`
`history`
`| head`

---

## File Formats

For background on file formats (FASTA, FASTQ, SAM) check [here](https://bioinformatics.stackexchange.com/questions/14/what-is-the-difference-between-fasta-fastq-and-sam-file-formats).

### 1. FAST-A format

Here are some key points to keep in mind when working with FASTA files:

- Each entry begins with a header line starting with ">".
- The header line is followed by the identifier of sequence data.
- Sequences can be represented in uppercase or lowercase letters.
- Whitespace, including spaces and line breaks, can be present in the sequence data, but it's often ignored by most sequence analysis tools.

*FASTA Example: *
```
>Mus_musculus_tRNA-Ala-AGC-1-1 (chr13.trna34-AlaAGC)
GGGGGTGTAGCTCAGTGGTAGAGCGCGTGCTTAGCATGCACGAGGcCCTGGGTTCGATCC
CCAGCACCTCCA
>Mus_musculus_tRNA-Ala-AGC-10-1 (chr13.trna457-AlaAGC)
GGGGGATTAGCTCAAATGGTAGAGCGCTCGCTTAGCATGCAAGAGGtAGTGGGATCGATG
CCCACATCCTCCA
```

### 1. FAST-Q format

Here are some key points to keep in mind when working with FASTA files:
- A sequence identifier or header line begins with the "@" symbol. It provides a unique identifier for the sequence.
- then sequenced data is provided
- A line starts with the "+" symbol and is often a repeat of the header line. It serves as a separator between the sequence and the quality scores.
- Lastly, quality scores. The quality scores are encoded using ASCII characters, with each character representing a numerical value that indicates the confidence or accuracy of the base call.
  

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
**
[ALLC](https://hq-1.gitbook.io/mc/tech-background/file-formats#allc-file)

### Step 1. Obtain FASTQ files

Several options. Download from internet, use pre-existing dataset, etc.

`samtools view novaseq_demux/NJ_221007_P1-1-K15/bam/NJ_221007_P1-1-K15-E2.dna_reads.bam | less`

For NovaSeq, each set has 2 * N_lane files, N_lane depends on the flowcell used and the way of loading.

[EdgeTurbo](https://ngdc.cncb.ac.cn/ettrans/files/edgeturbo%E5%AE%A2%E6%88%B7%E7%AB%AF%EF%BC%88linux%E7%89%88%EF%BC%89%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97.pdf)

---

### Step 2. Login
`qlogin -l h_vmem=4G`

---

### Step. 3 Demultiplex

`yap demultiplex` 

Purpose:
This step further demultiplex random index on the 5' of R1, generating cell-level R1 and R2 FASTQ files.
The random index is trimmed after demultiplex. The random index name occurs at the FASTQ file name, which combines with previous information to form the cell id.

This step also prepares Snakefiles that contain all the commands for mapping (using [snakemake](https://snakemake.github.io)).

Result:

Each cell will have two FASTQ files in the output directory, with a fixed name pattern:
{cell_id}-R1.fq.gz for R1
{cell_id}-R2.fq.gz for R2

```
output_dir
├── CEMBA200709_9E_4-1-E18  # a set of FASTQ files
│   ├── fastq
|   |   ├──{cell1}-R1.fq.gz
|   |   ├──{cell1}-R2.fq.gz
|   |   ├──{cell2}-R1.fq.gz
|   |   ├──{cell2}-R2.fq.gz
|   |   ├──...
|   |   ├── skipped  # some FASTQ files may be skipped due to too less or too much reads
|   |   |   ├──...
│   └── Snakefile  # command files for snakemake
├── (Other sets)
│   ├── fastq
|   |   ├──...
|   |   ├── skipped
|   |   |   ├──...
│   └── Snakefile
├── mapping_config.ini  # mapping config copied here
├── snakemake  # this only occur when using yap in Ecker Lab server
│   ├── qsub  # job script for qsub on gale
│   └── sbatch  # job script for sbatch on stampede2
└── stats  # place for summary stats
    ├── demultiplex.stats.csv
    ├── fastq_dataframe.csv
    └── UIDTotalCellInputReadPairs.csv

```

---

### Step 3. Setup mapping config and run script for mapping

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





