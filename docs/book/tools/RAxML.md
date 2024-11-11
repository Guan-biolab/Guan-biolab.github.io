# RAxML

分享者：labstd02

---

###### 更新时间：20241025

**RAxML构建最大似然法进化树**

**同样是基于phylophlan产生的对齐文件：faa_file_concatenated.aln**

**①**  **简单快速方式**

**raxmlHPC ­-f a ­-x 1234 ­-p 1234 ­-# 10000 ­-m PROTGAMMALGX ­-s faa_file_concatenated.aln ­-n ex -T 150**

**②**  **并行化软件支持，能最快速计算。并行化20个任务，每个任务使用8线程，能使用全部160线程计算资源：**

**mpirun -np 20 raxmlHPC ­-f a ­-x 1234 ­-p 1234 ­-# 10000 ­-m PROTGAMMALGX ­-s faa_file_concatenated.aln ­-n ex -T 8**

 

**其中：** 

**--f a   a表示执行快速 Bootstrap 分析并搜索最佳得分的 ML 树。**

**--x 1234指定一个 int 数作为随机种子，以启用快速 Bootstrap 算法。**

**--p 1234 指定一个随机数作为 parsimony inferences 的种子。**

**--# 10000指定 bootstrap 的次数。**

**--m PROTGAMMALGX**

**指定核苷酸或氨基酸替代模型。PROTGAMMALGX 的解释： "PROT" 表示氨基酸替代模型； GAMMA 表示使用 GAMMA 模型； X 表示使用最大似然法估计碱基频率。**

**结果文件：**

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)

**最终将结果文件RAxML_bestTree.ex上传至itol。**