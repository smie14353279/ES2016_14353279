## lab2 DOL实例分析&编程##


### 一、修改后的dot截图 ###


**1.**下图为example1修改前后的dot图<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19724912/5dad6da8-9bb5-11e6-8a2a-a85204f66ae4.png)<br />

**2.**下图为example2修改前后的dot图<br />

修改前：<br />
![1](https://cloud.githubusercontent.com/assets/22726648/19725363/ac38ce34-9bb7-11e6-93c0-7e7b5342ad3a.png)<br />

修改后：<br />
![2](https://cloud.githubusercontent.com/assets/22726648/19725468/311953d0-9bb8-11e6-9654-16b3dba9aadb.png)<br />

### 二、DOL安装笔记###

**（一）.EXPAMPLE2分析**<br />
目的是将原来的3个平方模块变为2个，所以分析xml，里面是定义和连接模块的内容。<br />

1.各组件的定义：<br />
 定义变量N=3：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19725646/59efc284-9bb9-11e6-9743-f6c53e25c5d8.png)<br />
进程生产者和进程消费者的定义，生产者定义一个名为10的输出端口，而消费者则定义一个名为100的输入端口，下面则是引入这个端口的函数的实现。<br />
生产者：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19725652/5e1e2e04-9bb9-11e6-8c04-d108fbffdd8c.png)<br />
消费者：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19725655/6179923c-9bb9-11e6-8359-3d27f21be900.png)<br />
平方模块的定义，这里使用了迭代器来创建平方模块，因为N为3，所以创建了3个平方模块，通过append function来实现一个索引值来区分，索引为从0到2的3个整数。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726268/a35e40be-9bbc-11e6-8249-d5cbf0f43880.png)<br />
通过迭代器创建4条名为C2通道，通过append function来实现一个索引值来区分，索引为从0到3的4个整数，每条通道一端名为0的输入端和另一端名为1的输出端。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726274/ad1bea2a-9bbc-11e6-89f2-38ddf865ce49.png)<br />

2.各组件的连接<br />
首先是平方模块的链接。先看上面to-square的部分，顾名思义即将线连进平方模块：用变量i来代替迭代器从0到2的三个整数，将名为C2且索引为i的通道的端口1（即输出端）作为源头连接到目标段名为square且索引为i的平方模块。至于下面名为from-square部分则是把平方模块的输出端连进通道的输入端，与上面类似，用变量i来代替迭代器从0到2的三个整数，将名为square且索引为i的平方模块的端口1（输出端）作为源头连接到目标通道名为C2且索引为i+1的通道的端口0（输入端）。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726277/b1becc82-9bbc-11e6-906d-5eac5e35315c.png)<br />
生产者和消费者与通道C2的连接。名为g_的连接是将生产者的名为10的输出端作为源头连接到C2且索引为0的通道的端口0（输入端）；将名为C2且索引为3的通道的端口1（输出端）连接到消费者名为100的输入端。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726287/baa0a0dc-9bbc-11e6-873d-00a277fc60a1.png)<br />

3.dot图<br />
修改前：<br />
![1](https://cloud.githubusercontent.com/assets/22726648/19725363/ac38ce34-9bb7-11e6-93c0-7e7b5342ad3a.png)<br />
而我们的目的是减少一个平方模块，因为上面平方模块的生成和端口的生成都是通过迭代器来完成的，而且部分连接connection也是通过迭代器来实现的，这里涉及的最重要的一个地方就是迭代变量N，只需将N的取值从3改为2即可实现减少一个平方模块的要求。<br />

修改如下：将N的变量值改为2<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726605/44c3e78c-9bbe-11e6-801f-4792b87c852d.png)<br />
编译运行后的结果以及dot图：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726645/7d7300f4-9bbe-11e6-9618-8b700890e8f5.png)<br />
![2](https://cloud.githubusercontent.com/assets/22726648/19725468/311953d0-9bb8-11e6-9654-16b3dba9aadb.png)<br />

**（二）.EXPAMPLE1分析**<br />
目的是将平方模块变为立方模块，即使平方变为立方模块的构建以及连接这里就不多说了，直接分析模块里面的函数。<br />
下图为example1的dot图：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19724912/5dad6da8-9bb5-11e6-8a2a-a85204f66ae4.png)<br />

1.生产者：第一个是初始化函数，只会执行一次，目的是初始化数据以防受影响，然后是下面的fire函数，它将会在p指向local的索引小于LENGTH（20，从global.h处得到）执行上面的if语句，即将索引从0到19的20个整数以及对应的DOLProcess p从端口处输出到C1通道。local的索引大于LENGTH则会执行下面那条if语句，即销毁本程序。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726866/9cf8d420-9bbf-11e6-81ba-c2507dba496c.png)<br />
2.平方模块：大致类型与上面生产者一致，仅仅少部分内容不同。这里与上面不同之处在于有从输入端读取数据的操作，将读取进的数据赋值到i和DOLProcess p，对i进行平方操作后，在将i和DOLProcess p从端口处输出到C2通道。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726870/a025df94-9bbf-11e6-92e3-eb5ae46f7483.png)<br />
3.消费者：这里与平方模块的不同是多了一个打印功能以及少了一个将数据从端口的功能。这里将读取的进的数据赋值到c和DOLProcess p，然后打印c。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726876/a41d39b2-9bbf-11e6-9537-93d637047076.png)<br />

上面3个函数就是dot图3个模块的功能，其中只有中间的平方模块对传入的数据进行了修改，实现了整数的平方，为了实现我们的立方，只需在平方模块将数据的平方改为立方，这里就完成了。<br />

修改如下：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726881/a9bf9626-9bbf-11e6-9a0a-2d1267e6f0c4.png)<br />

结果如下：<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19726889/ae5ccf6e-9bbf-11e6-9062-7c8cbe10dfbb.png)<br />
### 三、实验感想 ###

本次实验虽然修改的只有两个部分，但是整个流程和里面的细节还是有点难理解的，而且我对实验example2中的那个p有点困惑，感觉不需要这个p也能完成这个过程，只需要那个索引即可，其它就没什么大问题了。
