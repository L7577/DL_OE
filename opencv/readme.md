# 如何安装opencv
在图像处理领域，opencv库是必不可少的支持工具，其最新版本已经集成了很多重要的算法，包括对DNN的支持！

*当然安装配置编译opencv库是非常麻烦的，若是我们只需要python支持，只需使用pip一行命令解决，但若是需要更多语言的接口，如C 、C++等，就需要源码编译*


## python单独版
只安装python支持包，需要提前安装好其他的支持包，如numpy、matplotlib等
```
#保证pip是最新的版本
#使用命令  pip install <需要的包>  #安装需要的包
pip install opencv-python
```
若是使用anaconda，需保证conda也是最新版本
`conda upgrade conda`
```
#可以使用search命令,搜索可用支持包
conda install opencv
```
安装完成以后可以简单的测试
```
#命令行输入
python
#进入python环境
import cv2
#没有报错，则是安装成功！
```

##  源码编译
*比较繁琐，稍后在更新*

需要安装部分依赖包
```
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```
其中在安装libjasper-dev时可能会报错，需要解决安装包找不到等问题！

