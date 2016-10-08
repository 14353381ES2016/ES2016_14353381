# DOL--The distributed operation layer

## DOL概述：
> 分布式操作层（DOL）是一个程序的并行应用软件开发框架，使得应用程序自动映射到多处理器体系结构平台上。DOL基本上由三个部分：

>* DOL的应用程序编程接口：DOL定义了一组计算和通信的程序，是一种应用于形状平台的分布式的编程和并行应用程序。使用这些程序，程序员就可以编写程序，而不必对底层的架构有详细的了解。事实上，在硬件相关的软件这些程序有待进一步细化（HDS）层。

>* DOL功能模拟：为程序员提供一个可能性来测试他们的应用程序，功能仿真框架已经形成。除了应用程序的功能验证，该框架是用来获得在应用程序级的性能参数。

>* DOL的DOL映射映射优化：优化的目标是计算一组应用程序的最佳映射到图形架构平台。在第一步骤中，基于XML的规范格式已被定义，允许描述的应用程序和在一个抽象的水平的体系结构。当然，所有必要的获得准确的性能的信息，都必须包含在内。

## DOL安装笔记

#### 安装一些必要的环境(以ubuntu为例)：

* 更新并安装ant

        sudo apt-get update
        sudo apt-get install ant
        
* 安装jdk和unzip

 	    sudo apt-get install openjdk-7-jdk
	    sudo apt-get install unzip
	   
##### 实验截图：
![](http://p1.bqimg.com/4851/ff200aa451098543.jpg)

1.1 由此安装好实验环境，之后进入DOL的配置。当然，在配置DOL前，还要下载好相应的文件，可以使用Vmware虚拟机，也可以从主机拷贝到虚拟机中去，下载代码为：
    
    sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz
    sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

2.1 解压文件

* 新建dol的文件夹 

        mkdir dol
    
* 将dolethz.zip解压到 dol文件夹中
	   
        unzip dol_ethz.zip -d dol

* 解压systemc
	    
        tar -zxvf systemc-2.3.1.tgz

##### 实验截图：
![](http://p1.bqimg.com/4851/7876735cfb3009ef.jpg)

* 1、这是解压后的dol文件夹（旁边的DOL文件夹是我临时存放数据的，跟本次实验无关）
* 2、这是我新建的仓库，之后会有说明。
* 3、这是解压后的systemc-2.3.1文件夹。
* 4和5、这是1.1中下载的压缩包。

2.2 编译systemc

* 解压后进入systemc-2.3.1的目录下

	    cd systemc-2.3.1
 	
* 新建一个临时文件夹objdir

	    mkdir objdir
	
* 进入该文件夹objdir

	    cd objdir
	
* 运行configure(能根据系统的环境设置一下参数，用于编译)

	    ../configure CXX=g++ --disable-async-updates

2.3 编译systemc
* 编译
    
        sudo make install

* 打开文件目录列表
* 记录当前的工作路径(会输出当前所在路径，记下来，待会有用)

        pwd

##### 实验截图:
![](http://p1.bpimg.com/4851/91ce151473a7589e.jpg)

实验截图中，cd命令打开了systemc-2.3.1这个文件夹，而ls命令则显示了文件夹内的所有内容，因为之后要修改路径，所以，使用pwd命令显示当前路径并记录下来，为/home/zengwp5/systemc-2.3.1。

3.1 编译dol

* 进入dol的文件夹

    	cd ../dol
    	
* 修改build_zip.xml文件

##### 实验截图:
![](http://p1.bqimg.com/4851/bad56499d389ddc0.jpg)

在实验截图中，用红色方框标志的就是上面编译的systemc位置在哪里，即路径。

##### 修改原理:

    <property name="systemc.inc" value="YYY/include"/>
    <property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
把YYY改成上页pwd的结果（注意，对于64位系统的机器，lib-linux要改成lib-linux64）

* 编译xml文件 

    	ant -f build_zip.xml all
    	
* 若成功会显示build successful，之后进入build/bin/mian路径下

    	cd build/bin/main
    	
* 然后运行第一个例子

    	ant -f runexample.xml -Dnumber=1
    
##### 实验截图:
![](http://p1.bqimg.com/4851/d3a54146441d5242.jpg)

由实验截图可知，运行成功。至此DOL配置完成

## 实验感想与心得
1、 本次实验过程中，配置DOL环境还是很简单的，跟着步骤走就好。但是过程还是觉得比较繁琐，需要比较多的时间和耐心，毕竟要输入很多命令，一旦打错了一个字母，有可能要重新再来，在配置仓库时，就试过删掉一切重新再来的感觉。

2、然后是实验截图, 一开始不知道截什么图，在配置好之后才重新进行截图的，导致截图比较少，然后我去下载了markdown的软件，发现插入图片需要生成URL，又不得不找一个图床软件，进行上传并生成截图的URL。

3、通过本次实验，我学习到了很多，不仅仅是初步了解了DOL框架，认识了仓库的创建，更解除了很多好玩的软件，例如markdown，图床工具等。一步步努力，尽量学得更多吧。
