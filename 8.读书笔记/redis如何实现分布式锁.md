# redis 如何实现分布式锁

## strategy 1

SETNX lock 1 //set if not exist 
EXPIRE lock 10  // 10s后自动过期
DEL lock

问题： setnx与expire不是原子操作，会出现不同步的情况，导致死锁

解决方案：SET lock 1 EX 10 NX 原子操作

问题2： 客户1操作超时，lock被释放掉，客户2加锁，客户1操作完成释放了客户2的锁

## strategy 2
>解锁strategy1锁的权限问题，以及锁超时的续期问题

* 死锁：设置过期时间
* 过期时间评估不好，锁提前过期：守护线程，自动续期
* 锁被别人释放：锁写入唯一标识，释放锁先检查标识，再释放

# 锁的分类与区别

* 可重入锁
* 乐观锁
* 公平锁
* 读写锁
* Redlock