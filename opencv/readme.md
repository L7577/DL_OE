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
*比较繁琐，持续更新中*
### 依赖包安装
需要安装部分依赖包
```
sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```
其中在安装libjasper-dev时可能会报错，需要解决安装包找不到等问题！
```
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
sudo apt update
sudo apt install libjasper1 libjasper-dev
```
参考：[unable-to-locate-package-libjasper-dev](https://stackoverflow.com/questions/44468081/unable-to-locate-package-libjasper-dev)

### 下载源码
官方主页：[https://opencv.org/](https://opencv.org/)
官方[github](https://github.com/opencv/opencv)
官网安装说明：[linux_install](https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html)
eg:下载源码包到本地目录
```
mkdir opencv
cd opencv
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
```
下载完成之后进入opencv目录中，创建build目录，准备编译
```
cd opencv
mkdir build
cd build
```
配置cmake选项及命令
```
cmake -D CMAKE_BUILD_TYPE=Release \
 -D CMAKE_INSTALL_PREFIX=/usr/local/opencv \
 -D OPENCV_GENERATE_PKGCONFIG=ON \
 ..
```
*对于opencv4以后的版本默认不会开启，生成pkgconfig目录及其对应文件，所以针对后续开发工作，需要看需求而定，比如本文后续的darknet安装，就是需要opencv支持，读取的配置文件就是需要开启生成的opencv.pc文件*

配置好cmake选项后，会在build目录下生成对应的编译配置文件，包括Makefile文件
执行
`make -j8`
*-j<数字>表示同时开启的线程数，并行编译会节省很多时间*
使用`nproc`命令查看cpu支持的线程数！

编译完成之后，执行
`sudo make install`
拷贝到对应的目录中！
注意：对于之前生成的pkgconfig目录，需要将其加入到系统环境变量中去
```
vim ~/.bashrc
#添加
	PKG_CONFIG_PATH=$PKG_CONFIG_PATH:<pkgconfig目录> 
	export PKG_CONFIG_PATH
#重新启动
source ~/.bashrc
#测试安装是否成功,执行
pkg-config --cflags --libs opencv
#输出对应信息即为安装成功！
```
也可以安装官方示例进行测试
```
git clone https://github.com/opencv/opencv_extra.git
#加入此路径到系统环境变量中
#cmake编译生成相应文件即可
```




