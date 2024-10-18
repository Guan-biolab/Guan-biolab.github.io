# foldseek

分享者：乙文静

---

###### 更新时间：20241018

foldseek结果解析

2024年9月26日

11:16



**安装：**conda install bioconda::foldseek

**原理：**

Foldseek 是一种用于快速比较蛋白质结构的工具，能够有效地评估不同蛋白质结构之间的相似性。Foldseek 提供了多个关键指标，包括 **TM score**、**Fident** 和 **QCov**，这些指标分别从不同角度反映了蛋白质结构对齐的质量和相似性。以下是这三个指标的详细解释及其相互关系和计算方法：

**1. TM score****（模板建模分数）**

**定义与意义：**

- **TM     score** 是衡量两个蛋白质结构整体相似性的标准化分数，范围通常在 0 到 1 之间。值越接近     1，表示结构相似性越高。
- TM     score 考虑了蛋白质长度的影响，因此能够公平地比较不同长度的蛋白质结构。

**计算方法：** TM score 的计算基于对齐后对应残基之间的距离，公式如下：

TM score=1Ltarget∑i=1L11+(did0)2\text{TM score} = \frac{1}{L_{\text{target}}} \sum_{i=1}^{L} \frac{1}{1 + \left(\frac{d_i}{d_0}\right)^2}TM score=Ltarget1i=1∑L1+(d0di)21

其中：

- LLL     是对齐的残基数量。
- did_idi 是第 iii 个对应残基之间的距离。
- d0d_0d0 是一个归一化参数，通常取 1.2 Å，用于标准化距离。
- LtargetL_{\text{target}}Ltarget 是目标蛋白质的长度。

**特点：**

- 归一化处理使得 TM score 不受蛋白质长度影响，适用于不同长度蛋白质的比较。
- 对于同源蛋白质，通常 TM score 高于 0.5 表示具有显著的结构相似性。

**2. Fident****（Foldseek 序列同一性分数）**

**定义与意义：**

- **Fident** 表示在对齐区域内的序列同一性，即对齐部分中相同氨基酸残基的比例。
- 它反映了在对齐过程中，序列层面的相似程度。

**计算方法：** Fident 的计算公式为：

Fident=相同残基数量对齐残基总数×100%\text{Fident} = \frac{\text{相同残基数量}}{\text{对齐残基总数}} \times 100\%Fident=对齐残基总数相同残基数量×100%

**特点：**

- Fident     关注序列层面的保守性，序列同一性高通常预示着结构上的相似性，但不绝对。
- 在结构相似性高但序列同一性低的情况下，可能存在进化上不同路径但保留了相似结构的蛋白质。

**3. QCov****（Query Coverage）**

**定义与意义：**

- **QCov** 表示查询蛋白质序列在对齐中的覆盖比例，即有多少比例的查询残基参与了对齐。
- 它衡量了对齐过程中查询序列被覆盖的程度。

**计算方法：** QCov 的计算公式为：

QCov=对齐中的查询残基数查询蛋白质总残基数×100%\text{QCov} = \frac{\text{对齐中的查询残基数}}{\text{查询蛋白质总残基数}} \times 100\%QCov=查询蛋白质总残基数对齐中的查询残基数×100%

**特点：**

- 高 QCov 表示大部分查询蛋白质序列被有效对齐，适用于全面评估结构相似性。
- 低 QCov 可能意味着仅部分结构区域具有相似性，或存在局部相似性。

**三者之间的关系与综合评估**

- **互补性：** TM score、Fident 和 QCov 分别从结构相似性、序列同一性和覆盖范围三个方面评估蛋白质对齐的质量，彼此互补。单一指标可能无法全面反映对齐质量，而结合三个指标可以提供更全面的评估。

- **关联性：**

- - 通常情况下，高 Fident 和高 QCov 会促使 TM score 也较高，因为更多的残基参与对齐且序列同一性高，往往意味着结构相似性较高。
  - 然而，也存在例外情况，例如某些蛋白质可能在特定区域高度保守，导致 Fident 和 TM score 高，但整体 QCov 低，因为只有部分区域被对齐。

**具体计算步骤**

1. **结构对齐：** 使用 Foldseek 对两个蛋白质结构进行快速对齐，找到最佳匹配的结构片段。
2. **计算 TM score：**     根据对齐后的残基对应位置，计算 TM score 以评估整体结构匹配度。
3. **计算 Fident：**     在对齐区域内统计相同的氨基酸残基数量，除以对齐区域的总残基数，得到 Fident。
4. **计算 QCov：**     统计参与对齐的查询蛋白质残基数，除以查询蛋白质的总残基数，得到 QCov。

**应用与意义**

- **结构预测与验证：** 在蛋白质结构预测中，Foldseek     通过这些指标帮助研究人员评估预测模型与已知结构的相似性，提高预测的可靠性。
- **功能推断：** 高度结构相似的蛋白质通常具有相似的功能，通过这些指标可以辅助功能推断和蛋白质家族分类。
- **进化研究：** 分析不同物种中蛋白质结构的保守性，理解蛋白质进化过程中的结构保留机制。

**总结**

TM score、Fident 和 QCov 是 Foldseek 中用于评估蛋白质结构对齐质量的三个重要指标。TM score 主要衡量结构相似性，Fident 关注序列同一性，QCov 则评估对齐覆盖范围。通过综合这三个指标，Foldseek 能够提供全面、准确的蛋白质结构比较结果，辅助生物信息学研究和实验设计。

 

**使用：**

1、建立搜索数据库：

foldseek createdb ./df_alphafold_r/ known_ds_database

2、检索未知数据

foldseek easy-search known_ds_database pre_df_alphafold_r/ known_ds_database result_pre_known_df_foldseek_TM_score_id.tsv tmp/ --format-output "query,target,alntmscore,qtmscore,ttmscore,fident,alnlen,mismatch,gapopen,qstart,qend,tstart,tend,evalue,bits" --threads 100

 

The default output fields are: query,target,fident,alnlen,mismatch,gapopen,qstart,qend,tstart,tend,evalue,bits but they can be customized with the --format-output option e.g., --format-output "query,target,qaln,taln" returns the query and target accessions and the pairwise alignments in tab-separated format. You can choose many different output columns.

| **Code**   | **Description**                                              |
| ---------- | ------------------------------------------------------------ |
| query      | Query sequence identifier                                    |
| target     | Target sequence identifier                                   |
| qca        | Calpha coordinates of the query                              |
| tca        | Calpha coordinates of the target                             |
| alntmscore | TM-score of the alignment                                    |
| qtmscore   | TM-score normalized by the query length                      |
| ttmscore   | TM-score normalized by the target length                     |
| u          | Rotation matrix (computed to by TM-score)                    |
| t          | Translation vector (computed to by TM-score)                 |
| lddt       | Average LDDT of the alignment                                |
| lddtfull   | LDDT per aligned position                                    |
| prob       | Estimated probability for query and target to be homologous  (e.g. being within the same SCOPe superfamily) |

 

3、生成网页版的结果

foldseek easy-search known_ds_database pre_df_alphafold_r/ result.html tmp1 --format-mode 3

 
