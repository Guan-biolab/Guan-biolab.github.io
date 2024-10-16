# FastQC



---

当二代测序的原始数据拿到手之后，第一步要做的就是看一看原始reads的质量。常用的工具就是FastQC。

### 安装：

 用conda 安装

```bash
$ conda install fastqc
```

下载压缩包安装：

  FastQC的官网：http://www.bioinformatics.babraham.ac.uk/projects/fastqc/

 

  FastQC的下载地址：http://www.bioinformatics.babraham.ac.uk/projects/download.html#fastqc

最新版

https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.12.1.zip

 linux命令：nohup wget -c http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.12.1.zip 1>fastqc.o 2>fastqc.e

 

  得到压缩包：fastqc_v0.12.1.zip 

 

  解压：unzip fastqc_v0.12.1.zip



 进入FastQC

  查看help文档：fastqc -h

 

  增加可执行权限：chmod 754 fastqc

 

  无需编译，直接运行

###  使用

  运行命令：

```bash
$ fastqc -f fastq -o result/ clean_r1.fq clean_r2.fq
```



## 
