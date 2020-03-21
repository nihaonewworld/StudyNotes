# RNA-seq Upstream Analysis Script
## install conda
```shell
# download miniconda3 from tuna mirrors
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-$(uname -m).sh
# install miniconda3
bash Miniconda3-latest-Linux-x86_64.sh
# update environment variables
source /root/.bashrc
# change conda mirrors
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda
conda config --set show_channel_urls yes
# create a new working environment by conda, some RNAseq analysis tools uses python2
conda create -n rna_seq python=2
# qurey all working environment
conda info —envs
# activate this working environment. if you want to use conda, please activating working environment
conda activate rna_seq
# quit working environment. if you want to quit conda, please deactivating working environment
conda deactivate
```
## install analysis tools by conda
```shell
conda install -y sra-tools
conda install -y bwa
conda install -y trimmomatic cutadapt trim-galore
conda install -y multiqc
conda install -y star hisat2 bowtie2 subread tophat
conda install -y htseq bedtools deeptools salmon
```
## download Sequencing Data and Reference Genome
### method(1)
[download data from FTP][1]

[Filezilla](https://filezilla-project.org/) is a tool to download from FTP site.

* [NCBI](ftp://ftp.ncbi.nlm.nih.gov)

* [EMBI](ftp://ftp.ensembl.org/pub)

### method(2)
[download data by sra-tools][2]

```shell
# query PRJNA257197 infomation
esearch -db sra -query PRJNA257197 | efetch -format runinfo > info.csv
# download SRA data
prefetch SRRXXXXXXX
cd ~/ncbi/public/
fastq-dump --gzip --split-3 SRRXXXXXXX.sra
# you can download data by fastq-dump, but I don't recommend it
fastq-dump --split-files SRRXXXXXXX
```












# Appendix
## sra-tools
tools | function
-|-
fastq-dump | SRA转换为fastq(**常用**)
prefetch | 下载sra数据(**常用**)
sam-dump | 将 SRA 转换为sam格式
sra-pileup | 生成 pileup统计结果
abi-dump | 处理abi格式数据
sff-dump | 处理454测序数据
illumina-dump | 将sra转换为illumina原始的qseq文件；
sra-stat | 统计sra文件
vdb-config，vdb-decrypt，vdb-dump，vdb-encrypt，vdb-validate | 处理vdb格式数据。

# Reference
[1]: https://mp.weixin.qq.com/s?__biz=MzI2MjA1MDQxMg==&mid=2649708801&idx=1&sn=ad33d5befa01abf95ac2fc75cd508d11&chksm=f24afe02c53d7714dc948196ad4a8a53729e68bf8f0ad387b5d2872d8302d8567827e06ca0e4&scene=21#wechat_redirect/
[2]: https://mp.weixin.qq.com/s?__biz=MzI2MjA1MDQxMg==&mid=2649708833&idx=1&sn=2d294025c37e0b963d1c8ed00490a9c6&chksm=f24afe22c53d7734c394c748177db7d6cb4fde8a5957937b24d31122ea1cb7122e8702cbdcc1&scene=21#wechat_redirect
