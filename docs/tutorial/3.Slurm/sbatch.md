# sbatch提交作业模板



---

###### 更新时间：20241016

\#test.sh



```bash
\#!/bin/bash

\#SBATCH -J name        #指定作业名称name

\#SBATCH -o %j.out       #指定使用作业号作为作业标准输出文件的名称

\#SBATCH -e %j.err       #指定使用作业号作为作业标准错误输出文件的名称

\#SBATCH -D /platform_data/User/用户名/......   **#****指定工作目录**

\#SBATCH -p compute_nodes    #指定分区名称 计算节点分区名compute_nodes，GPU节点分区名GPU_nodes

\#SBATCH -N 1          #**指定节点数量****  （请先查看剩余可用节点及对应核。目前集群共5个计算节点，bioinfolab121，bioinfolab122,bioinfolab123,bioinfolab124,bioinfolab-training，前两个节点各开放80核，后两个节点各120核，培训节点150核。)

\#SBATCH -n 60         #**指定总核数****   （目前集群共550核，单用户使用请不要超过60核）

\#SBATCH --mail-user=......@... #指定通知邮箱地址 【可选用】

\#SBATCH --mail-type=END    #通知类型，BEGIN作业开始通知，END作业结束通知，FAIL作业失败通知，ALL全类型通知 【可选用】

\#SBATCH --nodelist=......   #指定使用某节点 （例如，--nodelist=bioinfolab123)【暂可不做指定】

\#SBATCH --exclude=......    #指定避免使用某节点 【暂可不做指定】

\#SBATCH -t 1-12:00       #运行总时间，天数-小时数-分钟，D-HH:MM 【暂可不做指定】

\#SBATCH --gres=gpu:1    #单用户可使用1块GPU卡

\# 运行程序
 ......具体命令行  *（注意命令行里使用的核数，要于上面申请的-n数量一致。）*

###### 执行 sbatch 命令前，可先通过 [conda activate 环境名称] 先激活软件对应环境
```

