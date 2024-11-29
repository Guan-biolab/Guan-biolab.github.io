# MrBayes

分享者：labstd02

---

###### 更新时间：20241025



①  激活环境: 

```
conda activate phylophlan
```

②  配置文件：

```
phylophlan_write_config_file -d a -o phylophlan.cfg --db_aa diamond --map_aa diamond --msa mafft --trim trimal --tree1 iqtree --tree2 raxml --verbose > log.cfg
```

产生两个文件：phylophlan.cfg 和 log.cfg。

③  首先使用细菌基因组氨基酸序列通过phylophlan获得核心基因的比对文件：

```
phylophlan -i faa_file -d phylophlan -f phylophlan.cfg --diversity low -o result --nproc 20 –verbose
```

注意：--diversity这个参数

"low": for genus-/species-/strain-level phylogenies
 "medium": for class-/order-level phylogenies
 "high": for phylum-/tree-of-life size phylogenies

④  在比对文件的基础上使用iqtree绘制全基因组进化树（使用的使最大似然法）

iqtree -s faa_file_concatenated.aln -T AUTO -B 10000

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png) 



MrBayes构建进化树的方法：

①  使用phylophlan获得核心基因组的对齐文件（faa_file_concatenated.aln）

②  需要将faa_file_concatenated.aln转换成Nexus格式

python format.py faa_file_concatenated.aln

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image003.jpg)

最终产生一个alignment.nex文件 

③  需要对alignment.nex进行修改：

文件的尾部添加相应的参数：

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image005.jpg)

其中ngen代表迭代的次数，ngen=500000，表示分析总共迭代**五万代**，对于小数据集一般只需几万代就可以收敛，而大数据集可能则要至少数百万代才能收敛。

samplefreq=100，表示每一百代采一次样，对于需要长时间才能收敛的大数据集而言可以将该值调高以降低采样频率，避免最终文件包含的树和参数信息过多。

nruns=8，表示进行八个独立的分析，用于判断收敛情况。有时，提升该值会对有效样本大小（ESS）增加有奇效。

其余参数详见：[贝叶斯建树之 Mrbayes 篇 | Juse's Blog](https://biojuse.com/2023/07/06/贝叶斯建树之 Mrbayes 篇/)

④  运行数据

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image007.jpg)

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)

建议酌情使用线程以及使用较大的memory空间的节点，否则容易被kill。

运行的结果文件：

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

最终将结果文件alignment1.nex.con.tre上传至itol可视化！