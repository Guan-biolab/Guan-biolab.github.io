# hmmer

分享者：乙文静

---

###### 更新时间：20241018

hmmer

2024年1月26日

20:27

 

安装：

conda create -n hmmer

conda install bioconda::hmmer 或者conda install bioconda/label/cf201901::hmmer

 

使用说明：

Usage: hmmsearch [options] <hmmfile> <seqdb>

用法：hmmsearch 参数 hmm文件 序列数据库

例：

hmmsearch --tblout 17978_result_out -E 0.0000001 vgrG.hmm 17978_protein.faa

-o <f> : direct output to file <f>, not stdout 

输出到文件中，而不是到标准输出

 

-A <f> : save multiple alignment of all hits to file <f> 

将所有命中的多序列比对输出到文件

 

--tblout <f> : save parseable table of per-sequence hits to file <f> 

保存每个序列的命中结果的解析表到文件中

 

--domtblout <f> : save parseable table of per-domain hits to file <f> 

保存每个结构域的命中结果的解析表到文件中

 

--pfamtblout <f> : save table of hits and domains to file, in Pfam format <f>

保存命中和结构域的表格到文件，Pfam形式

 

--acc : prefer accessions over names in output

在输出文件中将登录号覆盖名字

 

--noali : don't output alignments, so output is smaller

不要输出比对，这样输出会变得更小

 

--notextw : unlimit ASCII text output line width

不限制ASCII文本输出行的宽度

 

--textw <n> : set max width of ASCII text output lines [120] (n>=120)

设置ASCII文本输出行的最大宽度

 
