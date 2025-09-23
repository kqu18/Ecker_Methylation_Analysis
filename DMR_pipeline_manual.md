# DMR pipeline manual
this markdown will serve as the tutorial for the DMR analysis after curating the gff files via steps from `allcools_pipeline.md`. This pipeline attempts to:
- merge gff files in to a dataframe
- annotate euc/het gene/TE regions
- perform EDA
- calculate custom χ² test statistic for generating individual DMWs and "chunks" of DMRs

---

## 0805_recreate_master.ipynb
iteratively gets all gffs from `gff_dir` matching certain `pattern` param to be merged into one master dataframe, then exported as a tsv, e.g.`master_col.CG.chr1-5.fast.tsv` or pkl, e.g. `./data/gffs_sorted.pkl`.

## 0805_recreate_annotation.ipynb
uses boolean overlap to add four boolean flag columns to master dataframe to indicate whether the window overlaps with `euc/het gene/TE regions`. Writes to a file named like `annotated_full_col.CG_2.fast.tsv`. This will be the **master df** to be refered in the later context.

## 0806_filter_annotated.ipynb
checks across-cluster methylation level. In this example, if a window has below `<0.2` window for every cluster, then it will be removed from the master dataframe. `annotated_filtered_col.CG_2.fast.tsv`

## 



## 0914_get_chunks_with_chisquare.ipynb
