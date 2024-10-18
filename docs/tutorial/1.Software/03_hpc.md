# 集群使用常见问题



---

###### 更新时间：20241009



**软件使用常见问题：**

1、先查阅集群软件说明文件，找准软件安装位置，以确定调用方式；

2、注意区分各软件具体所需参数；

3、从单节点登录的用户，同样可以使用集群共享软件，需注意直接调用时 使用绝对路径；使用conda调用时，请注意先激活/platform_data/Software/miniconda3/。



**数据库使用常见问题：**

1、使用数据库时，每个软件对应使用参数不同，请注意区分。
例如：                                                                                  （易错点）

```shell
emapper.py   --data_dir    /platform_data/Database/eggnog_5.0
pfam_scan.pl  -dir  /platform_data/Database/Pfam
```



**提交作业常见问题：**

1、具体程序命令行中-c、-t等表示使用核数的参数，要与作业申请使用核数（-N*-n)保持一致！

2、#SBATCH -p: 选择分区   计算分区名：compute_nodes；GPU分区名：GPU_nodes；

3、#SBATCH -D: 指定工作目录 需检查无误。
