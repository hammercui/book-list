# go程序语言设计

## 1 sync/atomic
>原子操作,通过cpu指令完成，同步技术的基础，避免goroutine之间的race condition

atomic.AddInt32(&n, 1),提供了五中函数，int拥有全部，指针类型不能不支持算术运算，没有AddT方法，只拥有

* LoadT
* StoreT
* SwapT
* CompareAndSwapT


StoreT和LoadT原子操作函数经常被用来需要并发运行的实现setter和getter方法。


## 2 内存对齐

受操作系统限制，比如32位和64位操作系统，寻址一次分别是4个字节与8个字节，而原子类型是不可分割的，必须要对齐
比如
```
type T1 struct {
    int8 a;
    int64 b;
    int16 c; 
}
type T2 struct {
    int8 a;
    int16 c; 
    int64 b;
}
```

T1在64位系统，为了内存对齐，需要的字节数1+7+8+2+6 = 24个字节，
T2在64位系统，只需要1+1+2+2+8 = 16个字节，这在多人游戏设计里，可以作为优化的考虑方向。

如何检测内存对齐：

1. golangci-lint run --disable-all -E maligned 发现可优化的struct。

### 3 并发编程 concurrency synchronization

def延迟函数会推入栈，执行时按照堆栈逆序执行。

* 对于一个延迟函数调用，它的实参是在此调用被推入延迟调用堆栈的时候被估值的。意思是调用被推入栈，还未执行时，入参就确定了
* 对于一个协程调用，它的实参是在此协程被创建的时候估值的。意思是goroutine创建时入参就确定了，不一定是调用时。

panic在当前协程退出之前，不会蔓延到其他协同程序，退出后会导致进程停止，需要用recovery消除

### 4 sync.Pool

sync.Pool 可以将暂时不用的对象缓存起来，待下次需要的时候直接使用，不用再次经过内存分配，复用对象的内存，减轻 GC 的压力，提升系统的性能。

sync.Pool 是协程安全的，这对于使用者来说是极其方便的。使用前，设置好对象的 New 函数，用于在 Pool 里没有缓存的对象时，创建一个。之后，在程序的任何地方、任何时候仅通过 Get()、Put() 方法就可以取、还对象了。

