## 1 make与new的差别，引用类型的意义？
2 逃逸分析？
3 channel的实现？
## 4 gmp与gc?
常见的gc有四种：
1. 引用计数：优点是回收快，实现简单，不需要stw;缺点是无法解决循环引用问题，对cache不友好，使用典型object-c
2. 标记-清除：mark-sweep。古老但有效，如果不可达先标记，到达阈值再stw进行清除。奠定了大部分gc算法的基础。
3. 节点复制 copying: java也用到了，只要是分代回收，不连续分配，在代划分时都会用到copy
4. 分代回收：比如java。



5 网络io等待队列？
6 读写屏障
7 map的实现，sync.map的实现，map实现随机的方法

大部分在《go语言设计与实现里》


## 参考

[Golang 垃圾回收剖析](http://legendtkl.com/2017/04/28/golang-gc/)