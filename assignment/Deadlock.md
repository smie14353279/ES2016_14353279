##Deadlock##


### 一、死锁产生的截图 ###


下图为产生死锁的截图<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19731399/d78a0f9a-9bcf-11e6-89a8-9d822fb3ecb5.png)<br />


### 二、产生死锁的4个必要条件###

**1.**互斥条件：一个资源每次只能被一个进程使用<br />
**2.**请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放<br />
**3.**不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺<br />
**4.**循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系<br />

### 三、死锁产生的解释 ###

**1.synchronized：**只要在同一个class里面有被synchronized所修饰的函数，那么在同一时间，最多只有一个线程执行被synchronized所修饰的函数，其它被synchronized所修饰的函数将被阻塞。<br />

**2.class A和class B：**它们各自的子函数都被被synchronized所修饰，所以说class A或class B最多只能执行一个子函数，其它子函数将会被阻塞。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19731817/421cddbe-9bd1-11e6-918c-92a4942d1cff.png)<br />

**3.产生死锁的程序：**
首先runnable是一个线程，每次执行它时将自动执行run里面的语句，但因为这个线程里面还有main函数，而main函数的优先级应该比run的优先级高，所以main就抢占run执行，执行里面的Deadlock程序。在上面的函数中，我们可以通过调节Deadlock程序里面的count值来使其优先级下降，以便其被run程序所抢占。<br />
![image](https://cloud.githubusercontent.com/assets/22726648/19731980/d2cf5f6c-9bd1-11e6-9859-27b6837a22e1.png)<br />

**4.死锁产生的原因：**
只有在Deadlock程序和run程序优先级相等时，陷入轮转调度的时候才有可能产生死锁，即a.methodA(b)和b.methodB(a)的优先级相等，此时当执行a.methodA(b)还没执行里面的b.last()时，b.methodB(a)抢占执行。因为a.methodA(b)和b.methodB(a)都被synchronized所修饰，而且a.methodA(b)和b.methodB(a)已经同时执行，class A和class B的last函数都被阻塞，所以两个程序都陷入无限等待的过程中，死锁产生了。<br />

所以产生死锁的可能是将count值调为当run程序在将要执行b.methodB(a)和Deadlock程序将要执行a.methodA(b)的情况下，它们两个的优先级相等，这样的话便于a.methodA(b)和b.methodB(a)互相轮转抢占，发生上面那种产生死锁的情况。<br />
