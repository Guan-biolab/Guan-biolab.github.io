# parallel程序并行 

分享者：bioinfo02

---

###### 更新时间：20241010

**软件安装**

CentOS安装

```shell
sudo yum install parallel
```

Ubuntu安装

```shell
sudo apt-get update

sudo apt-get install parallel
```

本地编译安装

```shell
wget https://ftpmirror.gnu.org/parallel/parallel-latest.tar.bz2

tar xjf parallel-latest.tar.bz2

cd parallel*

./configure

make

sudo make install
```



**基本用法**

parallel command1 ::: arg1 arg2 arg3

command1为需要并行执行的命令，:::符号表示传递参数arg1、arg2和arg3

 

**软件参数**

–jobs / -j：指定要并行执行的作业数量 –load / -l：指定要使用的系统负载 –memfree / -m：指定要保留的系统内存量 –noswap：禁用交换空间 –nice：指定要使用的进程优先级 –timeout / -t：指定作业的超时时间

 

**运行示例**

使用管道符和文件来执行并行任务

```shell
 

# 同时执行6个Fastqc任务，--outdir参数为结果数量目录

find *.fq | parallel -j 6 "fastqc {} --outdir ."

 

# 同时执行samtools index任务，--dry-run显示任务命令但不实际执行，可用于命令检查

find *.bam | parallel --dry-run 'samtools index {}'

find *.bam | parallel 'samtools index {}'

 

# vi run.sh

echo aaa

echo bbb

echo ccc

echo ddd

 

# 同时执行4个任务，生信中常通过这种方式并行执行多个任务

###### cat run.sh | parallel -j 4
```





```shell
#集群上运行例子
#同时执行15个结果

cat ../length/all_genome_first_end.txt |parallel --max-args=1 -j 15 sh ../script/mobile_island_v1.sh & ##&--表示后台运行
```

