# RAxML

分享者：bio0015

---

###### 更新时间：20241025



```
conda activate kraken2
```



```
kraken2 --threads 60 --paired **--db /platform_data/Database/kraken2** --report JX1JX2.kreport --output JX1JX2.kraken /platform_data/User/bio0015/respiratory_tract_data/clean_data/Human_lsussu_clean_JX_1-JX_2_1.fq.gz /platform_data/User/bio0015/respiratory_tract_data/clean_data/Human_lsussu_clean_JX_1-JX_2_2.fq.gz
```

\###bracken,用kraken2 report文件作为输入

```
 bracken -d /platform_data/Database/kraken2 -i HT3.kreport -o ./bracken_out/HT3.bracken.G -w ./bracken_out/HT3.bracken.G.kreport -l G -t 60
```

