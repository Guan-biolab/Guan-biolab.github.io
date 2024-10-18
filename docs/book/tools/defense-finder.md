# defense-finder安装及使用

分享者：乙文静

---

###### 更新时间：20241018

安装：

```shell
conda create -name defensefinder

conda activate defensefinder

pip install mdmparis-defense-finder
```

安装完成后，虽然显示是正常，但是要把macsyfinder 卸载重装装macsyfinder 2.12版本

卸载macsyfinder：whereis macsyfinder -->进入路径删除：rm macsyfinder

安装新的macsyfinder：conda install -c bioconda:macsyfinder==2.1.2

如果还是不成功，运行：defense-finder update

 

即：

```shell
conda create –n defensefinder

conda activate defensefinder

pip install mdmparis-defense-finder

whereis macsyfinder
```

cd 路径

```shell
rm macsyfinder

conda install -c bioconda macsyfinder==2.1.2

defense-finder update
```

 

 

使用方法：

defense-finder run genome.faa

Input.

The input file, here “genome.faa” can be a protein fasta file or a nucleotide fasta file.

A run on a genome (few thousand proteins) should take less than two minutes on a standard laptop. If more, make sure everything is installed properly. In this configuration, all the replicon will be named UserReplicon. ATTENTION, If you want to run DefenseFinder on a larger set of genomes you need to format your dataset as described in "Larger dataset and Gembase Format".

 

Outputs

DefenseFinder will generate three types of files (and an option to conserve MacSyFinder options). All the files are described below.

 

defense_finder_systems.tsv : In this file, each line corresponds to a system found in the given genomes. This is a summary of what was found and gives the following information

 

sys_id : Each system detected by DefenseFinder have a unique ID based on the replicon where it was found and the type of systems

type: Type of the anti-phage system found (such as RM, Cas...)

subtype : Subtype of the anti-phage system found (such as RM_type_I, CAS_Class1-Subtype-I-E)

sys_beg : Protein where the system begins (name found in the input file)

sys_end : Protein where the system ends (name found in the input file)

protein_in_syst : List of all protein(s) present in this system (name found in the input file)

genes_count : Number of genes found in the system

name_of_profiles_in_sys: List of the protein profiles that hit the protein of the system (name from the HMM).

defense_finder_genes.tsv : In this file, each line corresponds to a gene found in a system. For each gene, there is several information such as the replicon, the position, the system.. All the information comes from MacSyFinder and follows MacSyFinder nomenclature (best_solution.tsv) and more can be found in the MacSyFinder Ma documentation.

 

defense_finder_hmmer.tsv : In this file, each line corresponds to an HMM hit. This file show all hit of HMM regardless if they are in a complete system or not. Those results have to be used cautiously for deep inspection. Indeed, biologically, it was shown that only a full system will be anti phage. This function can be used to found defense gene in small portion of genomes. Beware, a single protein can have several hits. The output is a part of the result of HMMer results table.

 

hit_id : the protein name (name found in the input file)

replicon : The name of the replicon

position_hit: The position in the input file

Gene_name : the name of the HMM

 
