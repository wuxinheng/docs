## 入门

### 概念

> 模型其实就是标准。

cnn模型：cnn也叫convnet，中文名称为卷积神经网络，是计算机视觉领域常用的一种深度学习模型

mobilenet模型：一个轻量级的深层神经网络，训练快，运行起来也不卡。

> 包管理、环境管理

Anaconda包括Conda、Python以及一大堆安装好的工具包，比如：[numpy](https://baike.baidu.com/item/numpy/5678437)、[pandas](https://baike.baidu.com/item/pandas/17209606)等

conda是一个开源的包、环境管理器，可以用于在同一个机器上安装不同版本的软件包及其依赖，并能够在不同的环境之间切换

> 交互式笔记

Jupyter Notebook（此前被称为 IPython notebook）是一个交互式笔记本，支持运行 40 多种编程语言。

### 安装类库

#### 使用pip安装光速安装

如果安装太慢，可替换国内的下载源`-i https://pypi.tuna.tsinghua.edu.cn/simple`

```text
pip install matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 使用conda安装光速安装matplotlib

```text
#添加国内源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

#安装matplotlib
conda install matplotlib
```



### 类库

> Python常用模板库

#### tensorflow

tensorflow是一个 端到端开源机器学习平台。

安装

#### matplotlib

matplotlib是一个Python 的 2D绘图库，它以各种硬拷贝格式和跨平台的交互式环境生成出版质量级别的图形

#### numpy

numpy是Python 科学计算基础库，可以对数组进行高效的数学运算;

#### requests

requests是一个Python第三方库，处理URL资源特别方便

#### re

re模块提供了正则表达式相关操作。

#### os

os模块是Python标准库中的一个用于访问操作系统功能的模块。

#### sys

sys让你能够访问与Python解释器紧密相关的变量和函数

#### cv2

cv2 是 opencv 的 C++ [命名空间](https://so.csdn.net/so/search?q=命名空间&spm=1001.2101.3001.7020)名称，使用它来表示调用的是 C++ 开发的 opencv 的接口。所以安装时，不是用 pip install cv2 来安装，正确的安装语句

`pip install opencv-python`

#### PIL

PIL 是 Python Image Library 的简称。

PIL 库中提供了诸多用来处理图片的模块，可以对图片做类似于 PS（Photoshop） 的编辑。比如：改变图像大小、旋转图像、图像格式转换，转换颜色通道，图像增强，直方图处理，插值和滤波等等。

PIL 是第三方库，使用之前需要先安装。`pip install pillow`

#### shutil

shutil是 篇python 中的高级文件操作模块，与os模块形成互补的关系，os主要提供了文件或文件夹的新建、删除、查看等方法，还提供了对文件以及目录的路径操作。shutil模块提供了移动、复制、 压缩、解压等操作，恰好与os互补，共同一起使用，基本能完成所有文件的操作。是一个非常重要的模块。

#### Qt家族

QtCore 包含了核心的非GUI的功能。主要和时间、文件与文件夹、各种数据、流、URLs、mime类文件、进程与线程一起使用。

QtGui 包含了窗口系统、事件处理、2D图像、基本绘画、字体和文字类。

QtWidgets类包含了一系列创建桌面应用的UI元素。

QtMultimedia包含了处理多媒体的内容和调用摄像头API的类。 

QtBluetooth模块包含了查找和连接蓝牙的类。 

QtNetwork包含了网络编程的类，这些工具能让TCP/IP和UDP开发变得更加方便和可靠。 

QtPositioning包含了定位的类，可以使用卫星、WiFi甚至文本。 Engine包含了通过客户端进入和管理Qt Cloud的类。 

QtWebSockets包含了WebSocket协议的类。 

QtWebKit包含了一个基WebKit2的web浏览器。

 QtWebKitWidgets包含了基于QtWidgets的WebKit1的类。 

QtXml包含了处理xml的类，提供了SAX和DOM API的工具。 

QtSvg提供了显示SVG内容的类，Scalable Vector Graphics (SVG)是一种是一种基于可扩展标记语言（XML），用于描述二维矢量图形的图形格式（这句话来自于维基百科）。 

QtSql提供了处理数据库的工具。 QtTest提供了测试PyQt5应用的工具。



