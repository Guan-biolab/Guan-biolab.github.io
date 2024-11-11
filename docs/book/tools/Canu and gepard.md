# Canu and gepard

分享者：bio0013

---

###### 更新时间：20241030

Canu 专门组装 PacBio 或 Oxford Nanopore 序列。Canu 分为三个阶段：校正、修剪和组装。校正阶段将提高读取中碱基的准确性。修剪阶段将修剪读取到看似高质量序列的部分，删除可疑区域（例如剩余的 SMRTbell 适配器）。组装阶段将把读取排序为重叠群，生成一致序列并创建替代路径图。

 

对于真核基因组，20 倍以上的覆盖率足以超越当前的混合方法，但建议的最低覆盖率应为 30 倍至 60 倍。更高的覆盖率将允许 Canu 使用更长的读取进行组装，从而实现更好的组装。

 

输入序列可以是 FASTA 或 FASTQ 格式，未压缩或使用 gzip (.gz)、bzip2 (.bz2) 或 xz (.xz) 压缩。请注意，不支持 zip 文件 (.zip)。

 



```
 canu \

\>  -p 1_assembly -d 1_output \

\>  genomeSize=5.2m \

\>  -pacbio-raw 1.subreads.fastq.gz \

\>  useGrid=false maxThreads=16

-- canu 2.2


```





#### Canu和gepard 看三代结果是否环形

Canu

```
conda activate canu

canu   -p 1_assembly -d 1_output   genomeSize=5.2m   -pacbio-raw 1.subreads.fastq.gz   useGrid=false maxThreads=16
```

Gepard

```
conda activate gepard

java -cp /platform_data/Software/miniconda3/envs/gepard/share/gepard/dist/Gepard-2.1.jar org.gepard.client.cmdline.CommandLine -seq /platform_data/User/bio0013/tig00000002.fasta /platform_data/User/bio0013/tig00000002.fasta -matrix /platform_data/Software/miniconda3/envs/gepard/share/gepard/resources/matrices/edna.mat -outfile /platform_data/User/bio0013/1tig2_circular_test.png**
```

