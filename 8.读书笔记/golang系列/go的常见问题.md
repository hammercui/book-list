### 1 make与new的差别，引用类型的意义？
2 逃逸分析？
3 channel的实现？
### 4 gmp与gc?
常见的gc有四种：
1. 引用计数：优点是回收快，实现简单，不需要stw;缺点是无法解决循环引用问题，对cache不友好，使用典型object-c
2. 标记-清除：mark-sweep。古老但有效，如果不可达先标记，到达阈值再stw进行清除。奠定了大部分gc算法的基础。
3. 节点复制 copying: java也用到了，只要是分代回收，不连续分配，在代划分时都会用到copy
4. 分代回收：比如java。



5 网络io等待队列？
> io input,output,输入输出，信息交换的流程。
五种io模型：
* 阻塞io:应用进程向内核发起recfrom请求数据，准备数据报，进程阻塞，从内核复制数据到进程，解除阻塞。
* 非阻塞io:应用向内核recfrom申请时，缓冲区没有数据，直接返回应用，应用不断尝试。
* io复用模型：进程将多个fd传递给select，阻塞，等待fd就绪；就绪后通知进程调用recfrom函数，读取数据。核心是一个线程监控多个fd,减少线程分配。
* 信号驱动模型：

参考：
* [epoll nio区别_一篇文章带你彻底搞懂NIO](https://blog.csdn.net/weixin_39888943/article/details/112014207)
* [通俗理解BIO NIO select epoll并图解举例](https://cloud.tencent.com/developer/article/1773847)
* [bio,nio,aio的区别 select,poll,epoll的区别](https://www.cnblogs.com/eryun/p/12040508.html)
* [深入理解NIO select&epoll](https://zhuanlan.zhihu.com/p/150635981)
* [100%弄明白5种IO模型](100%弄明白5种IO模型)
* [5种网络IO模型](https://zhuanlan.zhihu.com/p/54580385)

6 读写屏障
7 map的实现，sync.map的实现，map实现随机的方法

大部分在《go语言设计与实现里》


## 参考

[Golang 垃圾回收剖析](http://legendtkl.com/2017/04/28/golang-gc/)