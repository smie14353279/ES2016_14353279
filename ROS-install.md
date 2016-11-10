##ROS安装##


### 一、ROS简介 ###
ROS（Robot Operating System） 是一个在计算机上对机器人进行操作的一个开源系统。ROS系统通常由大量节点组成，其中任何一个节点均可以通过发布/订阅的方式与其他节点进行通信。举例来说，机器人上的一个位置传感器如雷达单元就可以作为ROS的一个节点，雷达单元可以以信息流的方式发布雷达获得的信息，发布的信息可以被其他节点如导航单元、路径规划单元获得。

使用ROS的原因：ROS作为一个灵活的操作系统，其上的节点具有很大的随意性，它们可以位于不同的计算机上，甚至可以位于不同的网络上。而且ROS还是一个开源的系统，由专门的社区维护。

### 二、在Ubuntu上安装ROS###

**1.**配置你的 Ubuntu 软件仓库(repositories) 以允许 "restricted"、"universe" 和 "multiverse"这三种安装模式。

<center>![image](https://cloud.githubusercontent.com/assets/22726648/20171129/44b9ef86-a76a-11e6-95d1-5d5b982bff75.png)</center>
<br />
**2.**添加sources.list：配置你的电脑使其能够安装来自 packages.ros.org的软件包

<center>![image](https://cloud.githubusercontent.com/assets/22726648/20171275/e0c46852-a76a-11e6-9cb7-f892deef43e1.png)</center>
<br />
**3.**添加keys

<center>![image](https://cloud.githubusercontent.com/assets/22726648/20171336/1f2ca884-a76b-11e6-8e21-da5e3332ea9d.png)</center>
<br />
**4.**安装ros

<center>![image](https://cloud.githubusercontent.com/assets/22726648/20171362/44b9a9bc-a76b-11e6-8b2c-ca27bf0291c0.png)

![image](https://cloud.githubusercontent.com/assets/22726648/20171366/48e87982-a76b-11e6-896d-887ac8bcf3ad.png)</center><br />
**5.**初始化rosdep: rosdep可以方便在需要编译某些源码的时候为其安装一些系统依赖，同时也是某些ROS核心功能组件所必需用到的工具。

<center>
![image](https://cloud.githubusercontent.com/assets/22726648/20171433/93cea26e-a76b-11e6-9483-d95ba1361bc6.png)

![image](https://cloud.githubusercontent.com/assets/22726648/20171435/95ca0766-a76b-11e6-90e5-1958f6c91571.png)</center>
<br />
**6.**环境配置: 每次打开一个新的终端时ROS环境变量都能够自动配置好。

<center>![image](https://cloud.githubusercontent.com/assets/22726648/20171503/e9bf7bee-a76b-11e6-9d1b-cc48214ded86.png)</center><br />
**7.**安装 rosinstall: rosinstall 是ROS中一个独立分开的常用命令行工具，它可以方便让你通过一条命令就可以给某个ROS软件包下载很多源码树。

<center>
![image](https://cloud.githubusercontent.com/assets/22726648/20171548/197f08ea-a76c-11e6-80a6-80ec2e5b6e31.png)

![image](https://cloud.githubusercontent.com/assets/22726648/20171549/1b8730fe-a76c-11e6-9526-8498528bfa53.png)
</center><br />
### 三、问题与思考 ###
　　本次实验中，安装教程那里推荐换源来加快下载速度，所以我也参照网上提供的方法去source center那里换成中科大的源，然后在命令行通过apt-get update来更新，发现报错说我无法取得锁，后来去网上查找了下原因，发现是我在它换源更新的时候不知何原因终止了它的更新操作，导致出现问题，网上提供的解决方法是列出当前进程表（命令：ps aux），记录被锁住的进程的PID，然后终止它（命令：sudo kill PID）即可，然后就解决了问题。
