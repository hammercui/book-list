#### nodejs

node单进程的问题要靠代理进程解决，还是负载均衡的问题。
同时也是微服务的问题，即业务与业务的服务分离，区别于传统的单体架构。
其实react的flux单向数据流也是这样的思想，即数据的读权限与写权限分离。Flux架构其实来源于后端的CQRS，即Command Query Responsibility Segregation，命令与查询职责分离。

#### mvc

* 标准版本mvc
vc都依赖于m: v获得输入调用c进行操作，c进行数据更新m层，然后回调v层更新，v层再向m层要数据