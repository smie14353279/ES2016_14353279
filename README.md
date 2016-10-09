## lab1DOL配置 ##


### 一、DOL描述 ###

分布式操作系统是独立的多，网络，通信和物理上独立计算节点的集合软件。每个节点包含全局骨料操作系统的特定的软件子集。每个子集是两个不同的服务置备的复合物。第一个是一个普遍存在的最小的内核，或微内核，直接控制该节点的硬件。第二个是，坐标节点的独立和协同活动系统管理组件的更高级别的集合。这些组件抽象的微核功能，支持用户应用程序。



### 二、DOL安装笔记###

**1.**
下载文件并将下载的两个文件放进虚拟机的某个目录里面，然后将这两个文件解压。

![y 8onx4f inq 1m76ge8yi](https://cloud.githubusercontent.com/assets/22726648/19221673/95668f06-8e7a-11e6-990b-5ebf760d9c81.png)

**2.**
编译systemc：首先进入systemc-2.3.1的目录，创建objdir文件夹并进入该文件夹，然后运行configure。

![w n5b 3g bixy0a fku 3ya](https://cloud.githubusercontent.com/assets/22726648/19221691/fd92edea-8e7a-11e6-9255-6246867d0ca5.png)

运行结果：![5obftl 994ibp8jqyr wi](https://cloud.githubusercontent.com/assets/22726648/19221716/2f15d648-8e7b-11e6-949e-2d5550109a2a.jpg)
 
编译安装![t m mlk4e y njx jw obx](https://cloud.githubusercontent.com/assets/22726648/19221736/80f9069c-8e7b-11e6-9063-21e1e2ab8983.png)

运行结果：


![5obftl 994ibp8jqyr wi](https://cloud.githubusercontent.com/assets/22726648/19221741/9c28e69e-8e7b-11e6-9d68-7de1d0e260d3.jpg)



**3.**在上一步的基础上记录当前工作路径，修改dol文件夹里的build_zip.xml。

修改YYY里的内容变为当前工作路径:![es ftzsavdq88 q5ih2 5f5](https://cloud.githubusercontent.com/assets/22726648/19221761/fa8f443a-8e7b-11e6-965e-69a3550a5504.png)

**4.**最后编译dol

![mw8rna 0 7bkc rf e57b i](https://cloud.githubusercontent.com/assets/22726648/19221776/40365230-8e7c-11e6-926c-0d183a300f31.png)

运行结果：
![oofsq j vtf l tf8cj 86](https://cloud.githubusercontent.com/assets/22726648/19221779/52eb0ed4-8e7c-11e6-9c75-8e0ddbd0165b.jpg)



### 三、实验感想 ###

第一次配置dol的实验总体来说步骤不多，前面解压的操作两句话就完成了，主要是编译systemc出现了一点问题，编译那句话一直执行不成功，最后复制PPT上的语句在终端上执行就成功了，感觉是哪里语句打错了，其它就没什么问题了。