# alphafold2安装

分享者：乙文静

---

###### 更新时间：20241018

**alphafold2安装**

 

**在工作站配置**

先下载alphafold2：

```bush
git clone https://github.com/deepmind/alphafold.git

cd ./alphafold
```

安装aria2：

```shell
sudo apt install aria2
```

下载alphafold2的database：

法一：使用命令的代码：scripts/download_all_data.sh /data1/program/alphafold/alphafold_data > download.log 2> download_all.log &

法二：wget -c （这个download_all_data.sh里面的所有软件包）

法三：是用迅雷快一些

安装docker

 

docker安装alphafold2（失败，下不了显卡驱动）

```shell
sudo docker build -f docker/Dockerfile -t alphafold .
```

 

 

使用conda安装：

**Create a new conda environment and update**

```shell
conda create --name alphafold python==3.8
 conda update -n base conda 
```

 

**Activate conda environment**

```shell
conda activate alphafold
```

 

**Install dependencies**

c

```shell
onda install -y -c conda-forge openmm==7.5.1 cudatoolkit==11.2.2 pdbfixer

conda install -y -c bioconda hmmer hhsuite==3.3.0 kalign2

pip install absl-py==1.0.0 biopython==1.79 chex==0.0.7 dm-haiku==0.0.9 dm-tree==0.1.6 immutabledict==2.0.0 jax==0.3.25 ml-collections==0.1.0 numpy==1.21.6 pandas==1.3.4 protobuf==3.20.1 scipy==1.7.0 tensorflow-cpu==2.9.0

pip install --upgrade --no-cache-dir jax==0.3.25 jaxlib==0.3.25+cuda11.cudnn805 -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html
```

 

**Download alphafold release v2.3.1**

```shell
wget https://github.com/deepmind/alphafold/archive/refs/tags/v2.3.1.tar.gz && tar -xzf v2.3.1.tar.gz && export alphafold_path="$(pwd)/alphafold-2.3.1"

 
```

**Download chemical properties to the common folder**

```shell
wget -q -P $alphafold_path/alphafold/common/ https://git.scicore.unibas.ch/schwede/openstructure/-/raw/7102c63615b64735c4941278d92b554ec94415f8/modules/mol/alg/src/stereo_chemical_props.txt

 
```

**Apply OpenMM patch**

```shell
cd ~/anaconda3/envs/alphafold/lib/python3.8/site-packages/ && patch -p0 < $alphafold_path/docker/openmm.patch

 
```

**Download all databases**

使用迅雷更快一些

 

**Download run script**

run_alphafold.sh

 

**Run alphafold2**

```shell
bash run_alphafold.sh -d ../../alphafold2_database/ -o ./dummy_test/ -f ../test.fasta -t 2020-05-14
```

 

 **但是运行的时候报错了jaxlib问题：**

解决方法：

安装cuda12.2：

使用以下命令卸载旧版本的CUDA：

```shell
sudo apt-get --purge remove "cuda*"

sudo apt-get --purge remove "libcudnn*"

sudo apt-get autoremove
```

**2.** **添加新的CUDA存储库**

根据需要的CUDA版本，访问NVIDIA的[CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)页面，找到对应版本的安装命令或下载链接。

```shell
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub

sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
```

如果使用的是其他Ubuntu版本，请根据版本调整存储库地址。例如：

- Ubuntu 22.04: ubuntu2204
- Ubuntu 18.04: ubuntu1804

 

**3.** **安装CUDA 12.2**

更新包列表并安装CUDA 12.2：

sudo apt-get update

sudo apt-get -y install cuda-12-2（**报错啦**）

 

if报错：（hello上的问题（2024/9/16））

错误一：W: 无法下载 http://dell.archive.canonical.com/dists/focal/InRelease 无法连接上 dell.archive.canonical.com:80 (185.125.189.10)，连接超时 [IP: 185.125.189.10 80]

解决方法：

sudo vim /etc/apt/sources.list.d/dell.sources.list

找到相关的dell存储库文件，然后编辑它，注释掉该行（在行前加#）：

\# deb http://dell.archive.canonical.com/…

sudo apt-get update

 

又遇到了一个错误：E: 仓库 “https://download.docker.com/linux/ubuntu focal Release” 不再含有 Release 文件。

sudo vim /etc/apt/sources.list.d/docker.list

找到以下行：

deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable

将focal改为bionic或jammy（具体取决于你当前的系统兼容性），例如：

deb [arch=amd64] https://download.docker.com/linux/ubuntu jammy stable (失败)

sudo apt-get update (失败)

换成：

deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable (**成功啦**)

sudo apt-get update (**成功啦**)

 

if 报错：（gpu集群（2024/9/17））

错误：The following packages have unmet dependencies: cuda-12-2 : Depends: cuda-runtime-12-2 (>= 12.2.2) but it is not going to be installed Depends: cuda-demo-suite-12-2 (>= 12.2.140) but it is not going to be installed E: Unable to correct problems, you have held broken packages.

解决方法：

法1：

sudo apt-get install -f

sudo apt-get clean

sudo apt-get autoremove

sudo apt-get update

sudo apt-get install cuda-12-2

sudo apt-get install cuda-runtime-12-2 cuda-demo-suite-12-2（又失败啦）

法2：如果问题仍然存在，手动安装缺失的依赖项：

sudo apt-get install cuda-runtime-12-2 cuda-demo-suite-12-2（**又失败啦**）

法3：使用aptitude来解决依赖问题**（成功啦 (￣▽￣)）**

aptitude可以提供更多的解决依赖问题的选项。首先安装aptitude：

sudo apt-get install aptitude

sudo aptitude install cuda-12-2

**4.** **更新环境变量**

安装完成后，修改~/.bashrc文件中的环境变量：

vim ~/.bashrc

export PATH=/usr/local/cuda-12.2/bin${PATH:+:${PATH}}

export LD_LIBRARY_PATH=/usr/local/cuda-12.2/lib64\

​             ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

source ~/.bashrc

**5.** **验证安装**

使用以下命令验证CUDA 12.2是否安装成功：

nvcc --version

 

使用：（路径/platform_data/Software/alphafold-2.3.1/）

在github上下载：https://github.com/kalininalab/alphafold_non_docker/blob/main/run_alphafold.sh

for i in $(cat pro_name.txt);do bash run_alphafold.sh -d /data1/program/alphafold/alphafold_data/ -o ./dummy_test/ -f /data1/program/alphafold/alphafold_pro/${i} -t 2020-05-14 -g true;done

 

 

 

 

 

 

 

 
