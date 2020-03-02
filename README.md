## 书单

《亿级流量网站架构核心技术》
《微观经济学》
《精通比特币》
《etcd 技术内幕》
《Kubernetes in Action》
《小岛经济学》
《Elixir 程序设计》

### 游戏开发

[《Unity shader入门精要》](/1.Unity+Shader入门精要/Unity+Shader入门精要.pdf)

[《Unity shader入门精要》读书笔记](/1.Unity+Shader入门精要/读书笔记.md)

### C#语法

[CLR via C#]()

### 设计模式

[设计模式与游戏完美开发 读书笔记](/3.设计模式与完美开发/读书笔记.md)


### 阅读汇总

#### nodejs

node单进程的问题要靠代理进程解决，还是负载均衡的问题。
同时也是微服务的问题，即业务与业务的服务分离，区别于传统的单体架构。
其实react的flux单向数据流也是这样的思想，即数据的读权限与写权限分离。Flux架构其实来源于后端的CQRS，即Command Query Responsibility Segregation，命令与查询职责分离。

#### mvc

* 标准版本mvc
vc都依赖于m: v获得输入调用c进行操作，c进行数据更新m层，然后回调v层更新，v层再向m层要数据