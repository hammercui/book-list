# ESC
>结合知乎话题与云风blog

Entity是抽象表达，挂载了一堆具体的component，表达为一个具体事物，比如Player {MovementComponent,ConnectionComponent,StatsComponent}

1.不同的实体，在不同的观察者眼里，行为是不一样的
2.数据行为彻底分离。


数据行为的分离带来的好处，是可以区分读写行为，来并行读，优化代码。

System之间的解耦，通过event，或者共享代码，这个共享代码是utility。

component上层还有一个抽象tuple，元组。

状态的修改要少并集中，修改越少，依赖越少。

system的update可以通过delay one frame缓和。

## 优点：

1 解决了oop老问题，a atack b，是a打了b，还是b被a打了。ecs就拆分为healthComponet,attackSystem，statsComponet两个层次的东西了，被揍的人就是healthComponet减少了，攻击者的statsConpont的击杀增加。

2 一个system只关心固定的component组合，这个组合叫tuple。如果新增游戏玩法，新增system即可，与就system完全隔离，新增完全没有负担。极大地提高了灵活性和可扩展行，以及维护的心智负担。

3 方便做回放，可以拆分为live world，replay world

4 方便读写分离。

## 心得

1. 优先设计system，抽象出component，最后由component组合为entity，componet逻辑要足够简单

2. a,b系统共享的数据，存放于单例，不易debug，加上堆栈信息，比如时间戳，地点，原因等

3. utility要为纯函数，不能更改状态，更改状态只能system来做

4. 一个world只维护一个singleton管理状态。

## 云风blog的总结

本质是解决网络同步问题，模块的拆分。提高子任务的内聚性。

E的作用是生命周期管理。

S只筛选出自己关心的组件就行了，slibing

C组合在一起成为System的筛选标准，我们把system要求的必须包含一组component的组合，叫元组，一个system要解决这一组元组的数据更新。


### 更好的entity集合维护
>原因：现实中可能不需要system中遍历所有component，有对component剔除的需求。


可选的方式是使用观察者模式，对component贴上或撕掉标签，把这个标签的变化通知给对应的system，告知system是否需要update。


system订阅指定的component变更事件，更新一个单件中的entity集合。system在迭代时取单件中的数组，检查是否需要对entity进行update。



## 守望先锋网络同步

>帧同步的变种，同步的指令，同时由状态同步

玩家关注的是过程一致，而不是时间一致。

客户端：服务端下发结果，客户端预测失败了，就回到服务端时刻，之后的一段操作重新作用。

服务端：定期接受客户端的信息，客户端提前，所以服务端会缓存，应对网络波动。缓冲为空，服务端预测客户端，等真正操作到达，基于分歧计算下一个状态。服务器通知客户端卡了，客户端更快发包，服务端的预读队列，就能读到更多的值了。
处理丢包。每次都将服务端未确认的包，重新发送。

命中判定：

hitSystem->筛选->ModifyHeathQueueComponet->计算血量治疗量->MovementState组件->找到两者位置，预测错误回退。

只用了回滚和计算的component。