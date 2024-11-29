# Exonerate

分享者：bio0011

---

###### 更新时间：20241030

```
Exonerate 是一款常用于比对 DNA 和蛋白质序列的生物信息学工具，特别适合从基因组数据中比对蛋白质或核酸序列以找到相似或同源区域。它支持多种模式，能够执行序列比对、转录本与基因组的比对、蛋白质与核酸的比对等，是基因注释过程中常用的软件之一。
我的应用
基因预测：通过将参考序列比对到基因组序列上，用于注释真菌基因或外显子区域。
脚本：
#!/bin/bash
#SBATCH -J exonerate
#SBATCH -o %j.out
#SBATCH -e %j.err
#SBATCH -D /platform_data/User/bio0011/fungi/Data/Candida_albicans_masked/
#SBATCH -p compute_nodes
#SBATCH -N 1
#SBATCH -n 60
#SBATCH --nodelist=bioinfolab123
 
reference="/platform_data/User/bio0011/fungi/reference/Candida_albicans_ref"
input_dir="/platform_data/User/bio0011/fungi/Data/Candida_albicans_masked"
output_dir="/platform_data/User/bio0011/fungi/Data/Candida_albicans_results"
 
mkdir -p "$output_dir"
 
for fna_file in "$input_dir"/*.fna; do
    filename=$(basename "$fna_file")
    base=$(basename "$fna_file" .fna)
    output_file="$output_dir/$base.txt"
 
    exonerate --model protein2genome -c 60 --query "$reference" --target "$fna_file" \
        --showtargetgff > "$output_file"
 
    echo "Processed $filename"
done
```

 

**reference**：定义参考基因组文件的路径

**input_dir**：定义输入目录的路径

**output_dir**：定义输出目录路径

**mkdir -p "$output_dir"**：创建输出目录

**output_file**：定义输出文件路径

**--model protein2genome**：指定模型

**--query "$reference"**：指定查询文件（即参考基因组）路径

**--target "$fna_file"**：指定目标文件路径（即每个`*.fna`文件）

**--showtargetgff**：输出GFF格式的目标序列注释信息，将结果以GFF格式显示并存储到输出文件中

 