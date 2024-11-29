# BUSCO

分享者：bio0011

---

###### 更新时间：20241030

```
BUSCO（Benchmarking Universal Single-Copy Orthologs）是一款生物信息学软件工具，用于评估基因组、转录组和蛋白质组数据的完整性。它通过搜索进化保守的单拷贝直系同源基因（单拷贝基因）来衡量数据的完整性，广泛用于基因组装的质量评估。
我的应用：
基因组完整性评估：BUSCO 使用一组进化保守的单拷贝直系同源基因来检测基因组数据是否包含这些基因，从而评估基因组的完整性。
脚本：
#!/bin/bash
#SBATCH -J busco
#SBATCH -o %j.out
#SBATCH -e %j.err
#SBATCH -D /platform_data/User/bio0011/fungi/Candida_albicans/
#SBATCH -p compute_nodes
#SBATCH -N 1
#SBATCH -n 60
#SBATCH --nodelist=bioinfolab121
busco -i genome.fa -o busco_result --out_path /platform_data/User/bio0011/fungi/Candida_albicans -m genome -l /platform_data/User/bio0011/fungi/fungi_odb10  -c 60 --offline
 
```

`**-i** `指定输入文件。（通常为 **FASTA** 格式）

`**-o** `指定输出结果的前缀。

`**--out_path** `指定输出结果存储的路径。

`**-m genome**`：指定分析模式。

`**genome**` 表示输入的是基因组数据。BUSCO 支持多个模式，包括 `**genome**`（基因组）、`**transcriptome**`（转录组）、`**proteins**`（蛋白质序列）。

`**-l /platform_data/User/bio0011/fungi/fungi_odb10**`：指定 BUSCO 数据库路径。

`**-c 60**`：指定使用的 CPU 核心数量。

`**--offline**`：启用离线模式。

启用此参数时，BUSCO 不会尝试连接互联网以下载数据库。它只会使用本地指定的数据库（这里指定的是 `**/platform_data/User/bio0011/fungi/fungi_odb10**`），适合在没有网络连接的环境中使用。