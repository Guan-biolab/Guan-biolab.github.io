# 基因组公共数据库

---

!!! Abstract "内容简介"
    测序的数据如原始 reads 数据我们可以上传到 NCBI 或 EBI 的公共数据库，发表的文章中可以使用。此外公共数据库中的数据也可以为我们的研究提供帮助。本节我们就来了解一下如何上传和下载基因组测序数据。首先让我们来了解一下网络上的测序公共数据库：

**常见的高通量测序数据的公共数据库：**

- [SRA][] 短序列数据库：由 [NCBI][] 负责维护
- [ENA][] 欧洲核酸数据库：由 [EBI][] 负责维护
- [GSA][] 中国组学数据库：由[中科院北京基因研究所](http://www.big.ac.cn)负责维护

[SRA][] 是 [NCBI][] 为了应对越来越多的高通量测序数据而在 2007 年底推出的测序数据库，用于存储、显示、提取和分析高通量测序数据。而 [ENA][] 则是由 [EBI][] 负责维护的功能类似的数据库，同时作为 [Ensembl](http://www.ensembl.org)、[UniProt](http://www.uniprot.org) 和 [ArrayExpress](http://www.ebi.ac.uk/arrayexpress) 等服务的底层基础。2者在主要功能方面非常类似，同时数据互通。

---

## 1.SRA 数据库

### 1.1 简介

[SRA][] 是 Sequence Read Archive 的首字母缩写。[SRA][] 与 Trace 最大的区别是将实验数据与 metadata（元数据）分离。metadata 是指与测序实验及其实验样品相关的数据，如实验目的、实验设计、测序平台、样本数据(物种，菌株，个体表型等)。metadata可以分为以下几类：

* Study：accession number 以 DRP，SRP，ERP 开头，表示的是一个特定目的的研究课题，可以包含多个研究机构和研究类型等。study 包含了项目的所有 metadata，并有一个 NCBI 和 EBI 共同承认的项目编号（universal project id），一个 study 可以包含多个实验（experiment）。
* Sample：accession number以 DRS，SRS，ERS 开头，表示的是样品信息。样本信息可以包括物种信息、菌株(品系) 信息、家系信息、表型数据、临床数据,组织类型等。可以通过[Trace](http://www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=search_obj) 来查询。
* Experiment：accession number 以 DRX，SRX，ERX 开头。表示一个实验记载的实验设计（Design），实验平台（Platform）和结果处理（processing）三部分信息。实验是 [SRA][] 数据库的最基本单元，一个实验信息可以同时包含多个结果集（run）。
* Run：accession number 以DRR，SRR，ERR 开头。一个 Run 包括测序序列及质量数据。
* Submission：一个 study 的数据，可以分多次递交至 SRA 数据库。比如在一个项目启动前期，就可以把 study，experiment 的数据递交上去，随着项目的进展，逐批递交 run 数据。study 等同于项目，submission 等同于批次的概念。




## [BIG(中国科学院北京基因组所)](http://bigd.big.ac.cn)

几个数据库入口：

- [Bioproject](http://bigd.big.ac.cn/bioproject)
- [Biosample](http://bigd.big.ac.cn/biosample)
- [GSA](http://bigd.big.ac.cn/gsa)

一般可以通过FTP方式下载:w


## [复制起点数据库](http://tubic.org/doric)

细菌、真菌和质粒的复制起始位点数据库


## [质粒数据库](http://www.patlas.site)

## [plsdb质粒数据库](http://ccb-microbes.cs.unisaarland.de/plsdb)

## [eggNOG](http://eggnog.embl.de)

## [GO](http://geneontology.org)


## Reference

1. [NCBI上传数据文档](http://www.ncbi.nlm.nih.gov/books/NBK47529/)
2. 熊筱晶, NCBI高通量测序数据库SRA介绍, 生命的化学[J], 2010:6, 959-963.
3. http://blog.sciencenet.cn/blog-656335-908140.html
4. https://www.biostars.org/p/139422/
5. https://www.youtube.com/watch?v=NSIkUHKRPpo

[NCBI]: http://www.ncbi.nlm.nih.gov
[SRA]: http://www.ncbi.nlm.nih.gov/sra
[EBI]: http://www.ebi.ac.uk
[ENA]: http://www.ebi.ac.uk/ena
[Aspera]: http://asperasoft.com
[Aspera Connect]: http://download.asperasoft.com/download/docs/connect/3.6.1/user_linux/webhelp/index.html#dita/introduction.html
[Aspera Desktop Client]: http://downloads.asperasoft.com/en/downloads/2
[GSA]: http://gsa.big.ac.cn/
[sratoolkit]: (https://github.com/ncbi/sra-tools)
