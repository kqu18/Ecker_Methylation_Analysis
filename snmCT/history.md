  402  cd edgeturbo-client/
  403  ./edgeturbo download /gsa2/CRA008945/CRR793703/CRR793703.fastq.gz
  404  ./edgeturbo download /gsa2/CRA008945/CRR793705/CRR793705.fastq.gz
  405  ./edgeturbo download /gsa2/CRA008945/CRR611524/CRR611524.fastq.gz
  406  ./edgeturbo download /gsa2/CRA008945/CRR793702/CRR793702.fastq.gz
  407  ./edgeturbo download /gsa2/CRA008945/CRR793706/CRR793706.fastq.gz
  408  ./edgeturbo download /gsa2/CRA008945/CRR793704/CRR793704.fastq.gz
  409  pwd
  410  cd ../../../raidix/rdx-7/jwa
  411  cd ../../../raidix/rdx-7/jwalker/
  412  ls
  413  ls Marchantia_reference/
  414  ls Marchantia_test/
  415  ls Marchantia_test/JW_230314_mct_P1-1-D6/
  416  ls Marchantia_Late_Antheridiophore_Novaseq/
  417  pwd
  418  cd Novaseq_Natanella/
  419  ls
  420  ls novaseq_demux/
  421  ls novaseq_demux/NJ_221007_P1-1-K15/
  422  ls novaseq_demux/NJ_221007_P1-1-K15/fastq/
  423  zcat novaseq_demux/NJ_221007_P1-1-K15/fastq/NJ_221007_P1-1-K15-D2-R1.fq.gz | less
  424  ls novaseq_demux/NJ_221007_P1-1-K15/fastq/
  425  zcat novaseq_demux/NJ_221007_P1-1-K15/fastq/NJ_221007_P1-1-K15-D2-R1.fq.gz | less
  426  ls novaseq_demux/NJ_221007_P1-1-K15/fastq/
  427  ls'
  428  q
  429  ls
  430  ls novaseq_demux/
  431  ls novaseq_demux/NJ_221007_P1-1-K15/
  432  ls novaseq_demux/NJ_221007_P1-1-K15/bam/
  433  ls novaseq_demux/NJ_221007_P1-1-K15/
  434  ls novaseq_demux/NJ_221007_P1-1-K15/allc/
  435  zcat novaseq_demux/NJ_221007_P1-1-K15/allc/NJ_221007_P1-1-K15-E2.allc.tsv.gz | less
  436  conda list envs
  437  conda info --envs
  438  conda activate mapping
  439  samtools view novaseq_demux/NJ_221007_P1-1-K15/bam/NJ_221007_P1-1-K15-E2.dna_reads.bam | less
  440  conda deactivate
  441  screen -R jbn
  442  cd ../../../raidix/rdx-7/jwalker/
  443  cd Marchantia_test/
  444  ls
  445  ls JW_230314_mct_P1-D6
  446  ls /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110
  447  ls /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/
  448  qlogin -l h_vmem=4G
  449  cd /ceph/MethDev/
  450  ls
  451  mkdir SRR_files
  452  mv SRR9* SRR_files/
  453  ls
  454  mkdir Misc
  455  mv MpTak1v5.* Misc/
  456  mv output_log_file Misc/
  457  mv error_log_file Misc/
  458  ls
  459  mv bamCompare-Mp_ATAC.sh Misc/
  460  ls
  461  mv output_log_file_bamcompare Misc/
  462  ls
  463  mv error_log_file_bamcompare Misc/
  464  mv allc_merge.sh Misc/
  465  ls
  466  ls Kay_*
  467  ls Kay_Nanopore/
  468  ls Kay_Nanopore/CRA008945/
  469  rm Kay_nanopore/*
  470  rm -r Kay_nanopore/
  471  ls
  472  ls /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110
  473  ls /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/
  474  ls -lath /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/
  475  mkdir Novaseq_files
  476  cd Novaseq_files/
  477  mkdir 230907
  478  cd 230907/
  479  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  480  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  481  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/
  482  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  483  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  484  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/
  485  less /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/mapping_config.ini 
  486  ls
  487  less /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/
  488  ls /gale/raidix/rdx-7/jwalker/
  489  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/
  490  ls /gale/raidix/rdx-7/jwalker/
  491  ls /gale/raidix/rdx-7/jwalker/Natanella_drought/
  492  less /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/mapping_config.ini 
  493  less /gale/raidix/rdx-7/jwalker/YAP/
  494  ls /gale/raidix/rdx-7/jwalker/YAP/
  495  ls /gale/raidix/rdx-7/jwalker/YAP/reference_files/
  496  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  497  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/miseq_demux.sh
  498  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/mappingconfig_marchantia_mCT.ini 
  499  ls /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/
  500  zcat /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/230926-snmCT_seq-NovaSeq-pe-150-JW_230907_1_2-1-J12_S1_L003_R1_001.fastq.gz | less
  501  cd /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  502  ls
  503  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/*fasta
  504  cat /gale/raidix/rdx-7/jwalker/Marchantia_reference/*fasta | grep ">"
  505  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/*fasta
  506  ls
  507  less MpTak1v5.1_and_plastids.genome
  508  less MpTak1v5.1_r1.gtf
  509  ls bismark/
  510  ls bismark/Bisulfite_Genome/
  511  ls
  512  less miseq_demux.sh
  513  less mappingconfig_marchantia_mCT.ini
  514  less miseq_demux.sh
  515  less Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/
  516  less Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/
  517  zcat Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-H1-R1.fq.gz  | less
  518  ssh jwalker@br1.salk.edu
  519  ls
  520  pwd
  521  cd ../../
  522  ls
  523  pwd
  524  cd ../raidix/rdx-7/
  525  ls
  526  ls jswift/
  527  ls qlogin -l h_vmem=4G
  528  qlogin -l h_vmem=4G
  529  cd /ceph
  530  ls
  531  ls ethylene/
  532  ls gale-1/
  533  ls gale-1/manoj/
  534  cd gale-1/manoj/
  535  cd ../
  536  ls
  537  cd ../
  538  ls
  539  ls /ceph/MethDev/
  540  pwd
  541  qlogin -l h_vmem=4G
  542  cd /ceph/
  543  pwd
  544  cd ceph/MethDev
  545  cd ../
  546  pwd
  547  ls
  548  cd /ceph/
  549  qlogin -l h_vmem=4G
  550  cd /ceph/
  551  cd MethDev/
  552  ls
  553  pwd
  554  cd YAP/
  555  less miseq_demux.sh 
  556  ls /gale/netapp/seq12/illumina_runs/231018_A00280_0684_AHMVJJDSX7_231020150849695149110/Pool_arab_9/
  557  less miseq_demux.sh 
  558  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  559  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/mappingconfig_marchantia_mCT.ini 
  560  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/mappingconfig_marchantia_mCT.ini 
  561  ls
  562  less miseq_demux.sh 
  563  qstat
  564  qlogin -l h_vmem=100G
  565  ls
  566  cd /ceph/
  567  pwd
  568  cd /
  569  pwd
  570  qlogin -l h_vmem=10G
  571  cd /ceph/
  572  pwd
  573  cd /ceph/
  574  logout
  575  qlogin -l h_vmem=4G 
  576  cd /ceph/
  577  pwd
  578  ls
  579  cd MethDev/
  580  mkdir YAP
  581  ls
  582  cd YAP/
  583  cp /gale/raidix/rdx-7/jwalker/Marchantia_reference/miseq_demux.sh .
  584  ls
  585  less miseq_demux.sh 
  586  nano miseq_demux.sh 
  587  cp /gale/raidix/rdx-7/jwalker/Marchantia_reference/mappingconfig_marchantia_mCT_Nova.ini .
  588  ls
  589  less mappingconfig_marchantia_mCT_Nova.ini 
  590  qlogin -l h_vmem=100G
  591  conda activate mapping
  592  qsub -V -cwd -l mem_free=100G,h_vmem=100G,qname=gale.q miseq_demux.sh
  593  ls
  594  cd /ceph/MethDev/YAP/
  595  ls
  596  qsub -V -cwd -l mem_free=100G,h_vmem=100G,qname=gale.q miseq_demux.sh
  597  qstat -u jwalker
  598  ls
  599  lsth
  600  ls -lath
  601  qstat -u jwalker
  602  ls -lath
  603  cd Novaseq_demux_mCT/
  604  ls
  605  cd JW_230907_1_2-1-J12/
  606  ls
  607  ls lanes/
  608  ls
  609  ls -lath
  610  cd ..
  611  ls
  612  cd ..
  613  less *sh*e*
  614  less *sh*o*
  615  less *sh*e*
  616  jupyter notebook
  617  jupyter notebook --ip 0.0.0.0 --no-browser --port 445928 --NotebookApp.max_buffer_size=26843545600
  618  jupyter lab --ip 0.0.0.0 --no-browser --port 445928 --NotebookApp.max_buffer_size=26843545600
  619  jupyterlab --ip 0.0.0.0 --no-browser --port 445928 --NotebookApp.max_buffer_size=26843545600
  620  jupyter notebook --ip 0.0.0.0 --no-browser --port 65535 --NotebookApp.max_buffer_size=26843545600
  621  pwd
  622  ls
  623  cd ..
  624  ls
  625  cd Kay_Nanopore/
  626  ls
  627  git clone https://github.com/kqu18/STAM-seq.git
  628  conda search git
  629  conda 
  630  conda install --name mapping git
  631  stat -u jwalker
  632  qstat -u jwalker
  633  qlogin -l h_vmem=4G
  634  cd /ceph/MethDev/
  635  ls
  636  cd YAP/
  637  ls
  638  ls -lath
  639  less miseq_demux.sh.e7841887 
  640  less miseq_demux.sh.o7841887 
  641  ls Novaseq_demux_mCT/
  642  ls
  643  ls Novaseq_demux_mCT/JW_230907_1_2-1-J12/
  644  ls Novaseq_demux_mCT/JW_230907_1_2-1-J12/raw/
  645  ls Novaseq_demux_mCT/JW_230907_1_2-1-J12/lanes/
  646  ls Novaseq_demux_mCT/JW_230907_1_2-1-J12/lanes/Snakefile 
  647  less Novaseq_demux_mCT/JW_230907_1_2-1-J12/lanes/Snakefile 
  648  ls Novaseq_demux_mCT/JW_230907_1_2-1-J12/
  649  ls -lath
  650  qstat -u jwalker
  651  ls -lath
  652  qstat -u jwalker
  653  ls -lath
  654  ls Novaseq_demux_mCT/
  655  ls Novaseq_demux_mCT/JW_230907_1_2-1-J12/
  656  ls Novaseq_demux_mCT/JW_230907_3_4-1-A6/
  657  ls
  658  cd ..
  659  ls
  660  cd Kay_Nanopore/
  661  ls
  662  cd CRA008945/
  663  ls
  664  cat CRR611524.fastq.gz | head
  665  zcat CRR611524.fastq.gz | head
  666  zcat CRR611524.fastq.gz | less
  667  ls
  668  pwd
  669  ls -lath
  670  zcat CRR793701.fastq.gz | less
  671  qlogin -l h_vmem=10G
  672  qlogin -l h_vmem=5G -q gale.q@gale-cluster-*.salk.edu -pe smp 5
  673  ls
  674  cd /ceph/
  675  cd MethDev/
  676  ls
  677  cd YAP
  678  ls
  679  cd Novaseq_demux_mCT/
  680  ls
  681  cd JW_230907_1_2-1-J12/
  682  ls
  683  qstat -u jwalker
  684  ls
  685  ls lanes/
  686  ls -lat lanes/
  687  ls -lath lanes/
  688  cd /ceph/
  689  cd MethDev/
  690  cd YAP
  691  ls
  692  qstat -u jwalker
  693  cd Novaseq_demux_mCT/
  694  ls
  695  ls JW_230907_1_2-1-J12/
  696  ls JW_230907_1_2-1-J12/fastq/
  697  ls
  698  ls JW_230907_1_2-1-J12/
  699  ls JW_230907_1_2-1-J12/fastq/
  700  ls -lath JW_230907_1_2-1-J12/fastq/
  701  ls
  702  cd ..
  703  tail miseq_demux.sh.o7841887 
  704  less miseq_demux.sh.o7841887 
  705  less miseq_demux.sh.e7841887 
  706  ls
  707  cd Novaseq_demux_mCT/
  708  ls
  709  less mapping_config.ini 
  710  ls ..
  711  ls ../../../../gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  712  less ../../../../gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/mapping_config.ini 
  713  ls
  714  ls snakemake/
  715  ls snakemake/qsub/
  716  less snakemake/qsub/qsub.sh 
  717  less mapping_config.ini 
  718  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  719  less mapping_config.ini 
  720  nano mapping_config.ini 
  721  pwd
  722  ls 
  723  cd snakemake/
  724  ls
  725  cd qsub/
  726  ls
  727  less snakemake_cmd.txt 
  728  qsub -V -cwd -l mem_free=100G,h_vmem=100G,qname=gale.q qsub.sh
  729  qstat
  730  qstat -u jwalker
  731  ls
  732  less qsub.error.log 
  733  conda activate mapping
  734  pwd
  735  ls
  736  qsub -V -cwd -l mem_free=100G,h_vmem=100G,qname=gale.q qsub.sh
  737  qstat
  738  ls
  739  ls yNovaseq_demux_mCT_qsub/
  740  ls -lath yNovaseq_demux_mCT_qsub/
  741  pwd
  742  less yNovaseq_demux_mCT_qsub/yNovaseq_demux_mCT_0.error.log
  743  ls
  744  cd ..
  745  ls
  746  cd ..
  747  ls
  748  cd stats/
  749  ls
  750  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/
  751  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-D2-R1.fq.gz | less
  752  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-
  753  samtools view /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/bam/JW_230314_mct_P1-1-D6-H1.dna_reads.bam | 
  754  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-D2-R1.fq.gz | less
  755  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-D3-R1.fq.gz | less
  756  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-L13-R1.fq.gz | less
  757  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-D3-R1.fq.gz | less
  758  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-1-D6/fastq/JW_230314_mct_P1-1-D6-D2-R1.fq.gz | less
  759  zcat /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-2-D6/fastq/JW_230314_mct_P1-2-D6-E15-R1.fq.gz 
  760  qqqqq
  761  ls
  762  cd /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  763  ls
  764  zcat JW_230314_mct_P1-6-D6/fastq/JW_230314_mct_P1-6-D6-E11-R1.fq.gz | less
  765  zcat JW_230314_mct_P2-1-F6/fastq/JW_230314_mct_P2-1-F6-E13-R1.fq.gz | less
  766  ls
  767  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-2-D6/
  768  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-2-D6/bam/
  769  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/JW_230314_mct_P1-2-D6/rna_bam/
  770  qstat -u jwalker
  771  ls
  772  pwd
  773  qlogin -l h_vmem=10G
  774  cd /ceph/MethDev/YAP/
  775  ls
  776  cd Novaseq_demux_mCT/
  777  ls
  778  cd snakemake/
  779  ls
  780  cd qsub/
  781  ls
  782  less qsub.error.log 
  783  cd yNovaseq_demux_mCT_qsub/
  784  ls
  785  less yNovaseq_demux_mCT_0.error.log 
  786  tail yNovaseq_demux_mCT_0.error.log 
  787  less yNovaseq_demux_mCT_0.error.log 
  788  ls
  789  cd ..
  790  ;s
  791  ls
  792  cd ..
  793  ls
  794  cd /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  795  ls
  796  cd JW_230314_mct_P1-5-D6/
  797  ls
  798  less Snakefile 
  799  pwd
  800  cd /ceph/MethDev/YAP/Novaseq_demux_mCT/JW_230907_1_2-2-J12/
  801  ls
  802  less Snakefile 
  803  ls ../
  804  conda activate mapping
  805  yap --h
  806  ls
  807  cd ..
  808  ls
  809  yap update-snakemake --h
  810  yap update-snakemake --output_dir .
  811  pwd
  812  ls
  813  cd JW_230907_1_2-1-J12/
  814  ls
  815  less Snakefile 
  816  pwd
  817  cd ..
  818  cd snakemake/
  819  ls
  820  cd qsub/
  821  ls
  822  rm -r yNovaseq_demux_mCT_qsub/
  823  ls
  824  rm -r qsub.error.log
  825  rm -r qsub.output.log
  826  ls
  827  qsub -V -cwd -l mem_free=100G,h_vmem=100G,qname=gale.q qsub.sh
  828  qstat
  829  ls
  830  cd yNovaseq_demux_mCT_qsub/
  831  ls
  832  cd ..
  833  ls
  834  less qsub.error.log 
  835  pwd
  836  cd ..
  837  ls
  838  cd JW_230907_1_2-1-J12
  839  ls
  840  cd fastq/
  841  ls
  842  zcat JW_230907_1_2-1-J12-I14-R1.fq.gc | less
  843  zcat JW_230907_1_2-1-J12-I14-R1.fq.gz | less
  844  qstat
  845  qlogin -l h_vmem=10G
  846  cd /ceph/MethDev/YAP/
  847  ls
  848  cd Novaseq_demux_mCT/
  849  qstat
  850  ls
  851  ls JW_230907_1_2-1-J12/
  852  ls JW_230907_1_2-1-J12/bam/
  853  ls JW_230907_1_2-1-J12/rna_bam/
  854  qstat -u jwalker
  855  qstat
  856  qlogin -l h_vmem=4G
  857  cd /ceph/
  858  cd MethDev/YAP/
  859  ls
  860  cd Novaseq_demux_mCT/
  861  ls
  862  ls JW_230907_1_2-1-J12/
  863  ls -lath JW_230907_1_2-1-J12/
  864  ls JW_230907_1_2-1-J12/bam/
  865  ls -lath JW_230907_1_2-1-J12/bam/
  866  ls -lath JW_230907_1_2-1-J12/MappingSummary.csv.gz 
  867  ls
  868  cd snakemake/
  869  ls
  870  cd qsub/
  871  ls
  872  less qsub.error.log 
  873  ls -lath
  874  less qsub.output.log 
  875  tail qsub.output.log 
  876  ls
  877  conda activate mapping
  878  ls
  879  cd ..
  880  ls
  881  cd ..
  882  ls
  883  yap summary --output_dir .
  884  ls
  885  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  886  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/snakemake/
  887  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/
  888  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/
  889  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/stats/
  890  ls
  891  ls stats/
  892  yap summary --output_dir ./stats/
  893  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/stats/
  894  ls /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/*sh
  895  less /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/allc_merge.sh
  896  less /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/allc_mcds_10k.sh
  897  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/stats/
  898  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  899  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/allc_merge.sh 
  900  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/
  901  ls
  902  cd ..
  903  ls
  904  cp miseq_demux.sh summary.sh
  905  nano summary.sh 
  906  nano miseq_demux.sh
  907  qsub -V -cwd -l mem_free=10G,h_vmem=10G,qname=gale.q summary.sh 
  908  qstat -u jwalker
  909  ls -lath | head
  910  less summary.sh.e7842118 
  911  nano summary.sh
  912  qsub -V -cwd -l mem_free=10G,h_vmem=10G,qname=gale.q summary.sh 
  913  qstat -u jwalker
  914  ls -lath
  915  rm summary.sh.e7842118
  916  rm summary.sh.o7842118
  917  ls -lath
  918  qstat
  919  less summary.sh.e7842119
  920  less summary.sh.o7842119
  921  qstat
  922  less summary.sh.e7842119
  923  qstat
  924  less summary.sh.e7842119
  925  qstat
  926  ls -lath
  927  qstat
  928  less summary.sh.e7842119
  929  qstat
  930  ls
  931  ls Novaseq_demux_mCT/
  932  cd stats
  933  cd Novaseq_demux_mCT/stats/
  934  ls
  935  cp MappingSummary.html /gale/raidix/rdx-7/jwalker/
  936  ls
  937  cd ..
  938  ls
  939  cd JW_230907_1_2-1-J12/
  940  ls
  941  less allc/
  942  zcat allc/JW_230907_1_2-1-J12-D1.allc.tsv.gz | less
  943  ls
  944  ls -lath allc/
  945  ls /allc/*gz | wc -l
  946  ls allc/*gz | wc -l
  947  pwd
  948  cd ..
  949  ls
  950  ls JW_230907_1_2-*/allc/*gz | wc -l
  951  ls JW_230907_3_4--*/allc/*gz | wc -l
  952  ls JW_230907_3_4-
  953  ls JW_230907_3_4-*
  954  ls JW_230907_3_4-*/allc/
  955  ls JW_230907_1_2-*/allc/*gz | wc -l
  956  ls JW_230907_3_4-*/allc/*gz | wc -l
  957  cat JW_230907_1_2-*/allc/*gz > plate1.allc.tsv.gz
  958  rm plate1.allc.tsv.gz 
  959  ls /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/
  960  less /gale/raidix/rdx-7/jwalker/Marchantia_reference/Novaseq_demux_mCT/allc_merge.sh 
  961  cat JW_230907_1_2-*/allc/*gz > plate1.allc.tsv.gz &
  962  cat JW_230907_3_4-*/allc/*gz > plate2.allc.tsv.gz &
  963  /gale/raidix/rdx-7/jwalker/w50_creator/w50_creator -i
  964  ls
  965  zcat plate1.allc.tsv.gz | less
  966  zcat plate1.allc.tsv.gz | awk '{print $1}' | head
  967  zcat plate1.allc.tsv.gz | awk '{print $1 "\t.\t.\t"$2"\t"$2"\t"}' | head
  968  zcat plate1.allc.tsv.gz | awk '{print $1 "\t.\t.\t"$2"\t"$2"\t"$3"\t.\t.\tc="$5";t="$6-$5}' | head
  969  zcat plate1.allc.tsv.gz | awk '{print $1 "\t.\t.\t"$2"\t"$2"\t"$3"\t.\t.\tc="$5";t="$6-$5}' | sprt -k1,1 -k4,4n > plate1.gff
  970  zcat plate1.allc.tsv.gz | awk '{print $1 "\t.\t.\t"$2"\t"$2"\t"$3"\t.\t.\tc="$5";t="$6-$5}' | sort -k1,1 -k4,4n > plate1.gff
  971  ls
  972  cd JW_230907_1_2-1-J12/
  973  ls
  974  cd fastq/
  975  ls
  976  zcat JW_230907_1_2-1-J12-F1-R1.fq.gz | less
  977  zcat /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/NJ_221007_P1-1-K15/fastq/NJ_221007_P1-1-K15-D14-R1.fq.gz | less
  978  ls
  979  cd ..
  980  ls
  981  cd ..
  982  ls
  983  less plate1.
  984  less plate1.gff 
  985  /gale/raidix/rdx-7/jwalker/w50_creator/w50_creator -i plate1.gff -s 100 > plate1.w100.gff
  986  zcat plate1.allc.tsv.gz | awk '{print $1 "\t.\t.\t"$2"\t"$2"\t.\t"$3"\t.\tc="$5";t="$6-$5}' | sort -k1,1 -k4,4n > plate1.gff
  987  /gale/raidix/rdx-7/jwalker/w50_creator/w50_creator -i plate1.gff -s 100 > plate1.w100.gff
  988  less plate1.w100.gff 
  989  zcat plate2.allc.tsv.gz | awk '{print $1 "\t.\t.\t"$2"\t"$2"\t.\t"$3"\t.\tc="$5";t="$6-$5}' | sort -k1,1 -k4,4n > plate2.gff
  990  ls -lath
  991  /gale/raidix/rdx-7/jwalker/w50_creator/w50_creator -i plate2.gff -s 100 > plate2.w100.gff
  992  ls
  993  ls -lath
  994  less plate2.w100.gff 
  995  wc -l plate2.w100.gff 
  996  cp *w100.gff /gale/raidix/rdx-7/jwalker/
  997  history | grep plate
  998  pwd
  999  cd /ceph/MethDev/YAP/
 1000  ls
 1001  pwd
 1002  ls
 1003  cd Novaseq_demux_mCT/
 1004  ks
 1005  ls
 1006  pwd
 1007  cat history > history.txt
 1008  history > history.txt
 1009  less history.txt 
 1010  wc -l history.txt 
 1011  cat history.txt | tail -n 150 | head
 1012  cat history.txt | tail -n 155 | head
 1013  cat history.txt | tail -n 153 | head
 1014  cat history.txt | tail -n 153 > history_for_Kay.txt
 1015  rm history.txt 
 1016  ls
 1017  less history_for_Kay.txt 
 1018  cd ..
 1019  ls
 1020  less summary.sh
 1021  ls
 1022  cd Novaseq_demux_mCT/
 1023  ls
 1024  ls JW_230907_1_2-1-J12/
 1025  ls JW_230907_1_2-1-J12/bam/
 1026  ls -lath JW_230907_1_2-1-J12/bam/
 1027  ls -lath JW_230907_1_2-1-J12/rna_bam/
 1028  less JW_230907_1_2-1-J12/rna_bam/TotalRNAAligned.rna_reads.feature_count.tsv 
 1029  ls -lath JW_230907_1_2-1-J12/
 1030  ls -lath JW_230907_1_2-1-J12/allc/
 1031  zcat JW_230907_1_2-1-J12/allc/JW_230907_1_2-1-J12-I14.allc.tsv.gz | less
 1032  ls
 1033  ls -lath JW_230907_1_2-1-J12/
 1034  zcat JW_230907_1_2-1-J12/MappingSummary.csv.gz | less
 1035  ls
 1036  cd ..
 1037  ls
 1038  less summary.sh.o7842119 
 1039  ls Novaseq_demux_mCT/stats/
 1040  pwd
 1041  ls
 1042  cd Novaseq_demux_mCT/stats/
 1043  ls
 1044  pwd
 1045  cp MappingSummary.html /gale/raidix/rdx-7/jwalker/
 1046  cd /gale/raidix/rdx-7/jwalker/Novaseq_Natanella/novaseq_demux/
 1047  ls
 1048  cd stats/
 1049  ls
 1050  cp MappingSummary.html MappingSummary.Nat.html
 1051  pwd
 1052  ls
 1053  cd ..
 1054  ls
 1055  pwd
 1056  cd merged_allc_by_clst/
 1057  ls
 1058  ls *gff
 1059  ls -lath WW.CG.w100.gff 
 1060  ls -lath WW.CG.w1.gff 
 1061  ls -lath WW.CHG.w100.gff 
 1062  ls -lath WW.CHH.w100.gff 
 1063  less WW.CG.w1.gff
 1064  less WW.CG.w100.gff
 1065  less WW.CG.w1.gff
 1066  less WW.CG.w100.gff
 1067  cd /ceph/MethDev/YAP/Novaseq_demux_mCT/
 1068  ls
 1069  ls -lath plate*gff
 1070  less plate1.w100.gff 
 1071  pwd
 1072  cd ..
 1073  ls
 1074  cd /gale/raidix/rdx-7/jwalker/Marchantia_reference/
 1075  ls
 1076  history
