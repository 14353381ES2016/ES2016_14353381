# ROS--Robot operation system

## ROS安装笔记
> 本次安装的环境是Ubantu 14.04，并且要下载相应的包和库，方便之后的环境配置和指令执行。所以过程中要保证系统是连接着互联网的，并且在安装的步骤中，等待时间会很长，自己注意调整时间。

## 实验步骤
1.  添加source.list：

        sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

2. 添加keys：
   
        sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116

3. 安装与初始化
    
    3.1. 更新虚拟机的Debian软件包的索引，输入指令：

        sudo apt-get update 
    
    3.2.安装： 包含ROS、rqt、rviz、通用机器人函数库、2D/3D仿真器、导航以及2D/3D感知功能等的包，输入指令：
    
        sudo apt-get install ros-jade-desktop-full
    
    3.3.初始化rosdep，输入两条指令:
    
        sudo rosdep init
        rosdep update 

    3.4.环境配置：
    
        echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
        source ~/.bashrc
    
    3.5.如果你安装有多个ROS版本, ~/.bashrc 必须只能 source 你当 前使用版本所对应的 setup.bash。 如果你只想改变当前终端下的环境变量，可以执行以下命令：
        
        source /opt/ros/jade/setup.bash 
    
    3.6. 安装rosinatall，输入指令：
    
        sudo apt-get install python-rosinstall
        
## 测试ROS（实验结果）
1. 打开一个终端，输入指令：
    
        roscore
##### 实验截图：
> 当生成实验的网址时，指令成功。

![image](https://github.com/14353381ES2016/ES2016_14353381/blob/5a4f7b4a3a4f45ba9d62ebd853469e8e0ea42553/QQ%E6%88%AA%E5%9B%BE20161109213817.jpg?raw=true)

2. 打开第二个终端，输入指令：
        
        rosrun turtlesim turtlesim_node

##### 实验截图：
> 开启一个小乌龟界面

![image](https://raw.githubusercontent.com/14353381ES2016/ES2016_14353381/5a4f7b4a3a4f45ba9d62ebd853469e8e0ea42553/QQ%E6%88%AA%E5%9B%BE20161109213457.jpg)

3. 打开第三个终端，输入指令：
        
        rosrun turtlesim turtle_teleop_key

##### 实验截图：
> 接收键盘输入，控制小乌龟移动，并在第二个终端打印小乌龟的位置信息

![image](https://github.com/14353381ES2016/ES2016_14353381/blob/5a4f7b4a3a4f45ba9d62ebd853469e8e0ea42553/QQ%E6%88%AA%E5%9B%BE20161109213642.jpg?raw=true)

![image](https://github.com/14353381ES2016/ES2016_14353381/blob/5a4f7b4a3a4f45ba9d62ebd853469e8e0ea42553/QQ%E6%88%AA%E5%9B%BE20161109213739.jpg?raw=true)

4. 打开第四个终端，输入指令：
        
        rosrun rqt_graph rqt_graph

##### 实验截图：
> 左右两边矩形为ROS node，中间连线上是Topic名称

![](https://github.com/14353381ES2016/ES2016_14353381/blob/5a4f7b4a3a4f45ba9d62ebd853469e8e0ea42553/QQ%E6%88%AA%E5%9B%BE20161110123746.jpg?raw=true)

## Cartographer配置
> 到这里ROS配置完成了，接着我们来配置cartographer，我们需要安装3个软件包，ceres solver、cartographer和cartographer_ros，如下是安装过程。

1. 安装所需库和依赖项，输入指令：

        sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev

2. 首先安装ceres solver，选择的版本是1.11，需要新建build文件夹，存放makefile文件
    
        git clone https://github.com/hitcm/ceres-solver-1.11.0.git

        cd ceres-solver-1.11.0/build

        cmake ..

        make –j

        sudo make install
        
3.然后安装 cartographer,路径随意

        git clone https://github.com/hitcm/cartographer.git

        cd cartographer/build

        cmake .. -G Ninja

        ninja

        ninja test

        sudo ninja install
        
4.安装cartographer_ros，下载到catkin_ws下面的src文件夹下面，执行完毕后，到catkin_ws下面运行catkin_make即可

        git clone https://github.com/hitcm/cartographer_ros.git



5.数据下载测试
    
2d数据，大概500M，用迅雷下载，点击
[link1](https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag)

3d数据，8G左右，同样用迅雷下载，点击
[link2](https://storage.googleapis.com/cartographer-public-data/bags/backpack_3d/cartographer_3d_deutsches_museum.bag
)

然后运行launch文件即可，输入指令：

        roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
    roslaunch cartographer_ros demo_backpack_3d.launch bag_filename:=${HOME}/Downloads/cartographer_3d_deutsches_museum.bag
    
##### 实验截图：
> 
![image](https://github.com/14353381ES2016/ES2016_14353381/blob/master/QQ%E5%9B%BE%E7%89%8720161110130832.png?raw=true)

## 感想与心得
本次实验也是主要是配置工作，找到配置教程，安装好环境，其实就很流畅的做出来，但实际情况确实很复杂多变的，例如，ubantu的环境配置里无法更新你的指令里的包，或者没办法翻墙下载需要的数据，更有奇怪的就是他无端端就卡在一个地方，使得结果出不来，我的ubantu还好，过程没有遇到很大的困难，唯一一个地方就是安装ceres solver时，他一直报错说找不到对应的包文件，我仔细检查了好几次也不知道问题出在哪里，后来才发现是第一步的安装环境配置有一个包没有完全下载，估计是下载的时候网络停了或者是什么的，导致没有下载完全，最后重新执行了一次就可以了，这次实验因为要下载很多东西，所以一定要保证网络的连通。