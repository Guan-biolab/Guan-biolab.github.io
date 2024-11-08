# tree

分享者：bio0015

---

###### 更新时间：20241025

\#!/bin/bash



\# 激活 trimal 环境

conda activate trimal



\# 设定输入和输出文件

input_fasta="artical_ncbi_own.fasta"

mafft_output="mafft_RSVA_artical_ncbi_own.fasta"

trimal_output="trimal_mafft_RSVA_artical_ncbi_own.fasta"



\# 运行 MAFFT 进行序列比对

echo "Running MAFFT alignment..."

mafft --thread 20 --auto $input_fasta > $mafft_output



\# 运行 trimAl 进行序列修剪

echo "Running trimAl..."

trimal -in $mafft_output -out $trimal_output -automated1



\# 运行 IQ-TREE2 进行系统发育分析并生成进化树

echo "Running IQ-TREE2..."

iqtree2 -s $trimal_output -T AUTO -B 10000

