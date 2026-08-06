# blast

分享者：labstd02  vs bio0013

---

###### 更新时间：20241025

一、 将目的核苷酸序列和nt数据库进行比较：

```
cat B8_100_100_name.txt | while read name; do blastn -query ./B8_100_ffn/$name.fasta -db /platform_data/Database/blastdb/v5/nt/nt -negative_taxids 470 -num_threads 50 -outfmt "7 qaccver saccver pident qcovs length evalue sscinames" -out ./blastn_ming/$name.result; done
```

二、 将目的氨基酸序列和nr数据库进行比较：

```
cat B8_100_100_name.txt | while read name; do blastp -query ./B8_100_ffn/$name.fasta -db /platform_data/Database/blastdb/v5/nr/nr -negative_taxids 470 -num_threads 50 -outfmt "7 qaccver saccver pident qcovs length evalue sscinames" -out ./blastn_ming/$name.result; done

```

详见https://www.ncbi.nlm.nih.gov/books/NBK279684/

三将目的基因的核苷酸和某个细菌基因组进行比较：

①  将基因组构建数据库：

```
makeblastdb -in S2_1.fasta -dbtype nucl -out S2_1_database
```

②  进行比对：

```
blastn -db S2_1_database -query pEGE267.fasta -out pEGE267_S21_blast -outfmt 7
```

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

四将目的基因的氨基酸和某个细菌的基因组进行比较

①  makeblastdb -in S2_1.fasta -dbtype prot -out S2_1_database

②  blastp -db S2_1_database -query pEGE267.fasta -out pEGE267_S21_blast -outfmt 7

################################################



BlastN

```
  blastn -query "${i}p_scaffolds.fasta" -db "/platform_data/Database/blastdb/v5/nt/nt" -out "./reblastn_out_${i}" -outfmt "7 qaccver saccver pident qcovs length evalue" -evalue 1e-3 -num_threads 60
```

