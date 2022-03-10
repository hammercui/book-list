可以通过debug.PrintStack()打印堆栈信息。

编译器追求高性能原则，一般会分配在stack的函数里。但是当返回返回后，无法证明变量未被引用，
就必须分配在heap上由gc回收，或者变量非常大，也会分配在heap上。
如果变量已经有地址了，也会分配到heap。
逃逸分析也可以找出生命周期不超过函数返回值的变量，分配在stack。


## 小内存分配

需要小于32kb的内存时，从mcache本地缓存分配，包含多个mspan链表，mspan的链表按存储的object大小，分为67个等级，容量从8字节到32kib,如果span用完，则从mcentral重启申请span，并追加到mcache。

+ mcache
 - span链表8字节，可分配1024个object
 - span链表16字节，可分配512个object
 - ...
 - span链表32k字节，可分配1个object

如果向 OS 申请的内存过多，heap 还会分配一块足够大的连续内存 arena，对于 64 位处理器的 OS 而言，起步价为 64 MB。

## 大内存分配
大于32kb，不再缓存分配，而是在Page分配至heap。