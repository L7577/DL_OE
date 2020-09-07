# 深度学习系统运行环境配置
此页为简单介绍，以及如何使用本仓库，可以选择点击进入具体目录，查看如何操作！
## 目录 
- [cuda和cuDNN安装](https://github.com/L7577/Deeplearning_Basic_env/tree/master/CUDA_cuDNN)
- [安装opencv](https://github.com/L7577/Deeplearning_Basic_env/tree/master/opencv)
- [安装tensorflow](https://github.com/L7577/Deeplearning_Basic_env/tree/master/tensorflow)
- [安装pytorch](https://github.com/L7577/Deeplearning_Basic_env/tree/master/pytorch)
- [安装Darknet](https://github.com/L7577/Deeplearning_Basic_env/tree/master/darknet)
- [demo](#demo)
---
|系统或软件名称  | 版本号简述|
|--------------|--------|
|ubuntu        |   18.04|
|python        |>=3.6   |
|Tensorflow    |>=1.13  |
|Pytorch       |>=1.4   |
|darknet       |yolov4  |
|opencv        |>=3.4   |
|CUDA          |>=9.0   |
|cuDNN         |7.6     |
---
本文以NVIDIA公司的GPU产品为主要硬件计算设备，对一些基本的深度学习应用程序的运行环境配置进行简单说明，并使用一些简单的测试案例进行验证。*后面可能也会有其他厂商的深度学习处理器安装配置更新加入，敬请期待*

**首先是进行驱动程序安装及基础工具配置，建议直接由root用户完成！！**
若是自己在官网安装的linux系统版本，需要自行换源到国内镜像，简单命令如下：
*若是需要详细了解相关内容，请自行搜索相关资料*

以ubuntu18.04为例
**`vim /etc/apt/sources.list`**
以阿里源为例，添加如下内容：
```
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse 
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```
保存后退出即可

----


nvidia驱动程序及 CUDA与cuDNN安装，具体请参考相应目录

官方下载地址如下：
[CUDA:  https://developer.nvidia.com/cuda-toolkit](https://developer.nvidia.com/cuda-toolkit)

CUDA 是NVIDIA官方开发的专用GPU计算的工具，目的是更好的支持GPU做大量的并行计算任务，并且进一步优化内存使用，提高设备利用率！

[cuDNN: https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn)

cuDNN 库则是官方开发人员应对深度学习的深度神经网络所开发的专用加速库，内置了非常多的加速支持，如各种高效的卷积运算实现方式等。

目前的CUDA 版本已经到了11.0，对应的cuDNN也已经到了8.0.1,由于发展比较快速，我们使用之前的稳定版本进行测试。

本文测试版本为：cuda10.0 、cuDNN 7.6.5

----
## 单独准备python环境
确认自己的系统中内置的python版本，目前python2已经不再更新维护，python3已经到了3.8，使用者应该根据自己的编程习惯，合理选择版本号以便更好的进行开发工作！
### 更新pip
[说明文档 https://pip.pypa.io/en/stable/installing/](https://pip.pypa.io/en/stable/installing/)
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
```
### pip换源
```bash
# 清华源为例
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

### 安装conda支持
直接安装对应的anaconda版本

[下载地址：https://www.anaconda.com/products/individual#linux](https://www.anaconda.com/products/individual#linux)

[安装说明：https://docs.anaconda.com/anaconda/install/linux/](https://docs.anaconda.com/anaconda/install/linux/)

### conda换源

`vim ~/.condarc`
写入以下配置，以清华源为例：
```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
ssl_verify: true
```
保存后提出！！

------
**注：后文使用pip或者conda都需要保证其是最新版本，关于如何更新，请自行查阅相关资料升级工具包**

## demo
本文寻找了一些有趣的案例，他们基于Tensorflow或PyTorch等其他框架，当然基于什么并不重要，目前的框架基本大同小异，熟悉框架，可以让我们更好的使用它实现我们自己的网络结构及算法思路，并且借助框架的力量，使得对计算和数据资源的使用更加高效可靠！

*持续更新*

[谷歌colab](https://colab.research.google.com/github/tensorflow/docs-l10n/blob/master/site/zh-cn/tutorials/quickstart/beginner.ipynb?hl=zh-cn#scrollTo=0trJmd6DjqBZ)

[colab_yolov4](https://colab.research.google.com/drive/12QusaaRj_lUwCGDvQNfICpa7kA7_a2dE?hl=zh-cn#scrollTo=O2w9w1Ye_nk1)

[Tinker With a Neural Network ](http://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=spiral&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=8,8,8,8,8,8&seed=0.32223&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=true&xSquared=true&ySquared=true&cosX=false&sinX=true&cosY=false&sinY=true&collectStats=false&problem=classification&initZero=false&hideText=false)
