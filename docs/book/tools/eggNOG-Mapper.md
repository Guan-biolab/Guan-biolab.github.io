# eggNOG-Mapper

分享者：乙文静

---

###### 更新时间：20241018

2024年3月14日记录

 

```shell
conda install -c bioconda eggnog-mapper

emapper.py -i all_fre100.faa --output emapper_result -d bact --usemem --cpu 80
```

 

- - query_name: 检索的基因名或者其他ID
  - sedd_eggNOG_ortholog: eggNOG中最佳的蛋白匹配
  - seed_orholog_evalue: 最佳匹配的e-value
  - seed_ortolog_evalu: 最佳匹配的bit-score
  - predicted_gene_name: 预测的基因名，特别指的是类似AP2有一定含义的基因名，而不是AT2G17950这类编号
  - GO_term: 推测的GO的词条， 未必最新
  - KEGG_KO: 推测的KEGG KO词条，      未必最新
  - BiGG_Reactions: BiGG代谢反应的预测结果
  - Annotation_tax_scope: 对该序列在分类范围的注释
  - Matching_OGs: 匹配的eggNOG Orthologous Groups
  - best_OG|evalue|score: 最佳匹配的OG(HMM模式才有)
  - COG functional categories: 从最佳匹配的OG中推测出的COG功能分类
  - eggNOG_HMM_model_annotation: 从最佳匹配的OG中推测出eggNOG功能描述
