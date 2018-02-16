Zookeeper集群：Master/Slave模式

基本概念：
- Master选举
- Node：树形目录结构，可存放数据的节点，每个目录是一个Node，Node一共有四种状态
  - 持久化节点
  - 序列化持久化节点
  - 临时节点
  - 序列化临时节点
- Watches：每个节点以及子节点被数据发生变化或被删除，或创建时所触发的事件


分布式系统可将数据信息存储在Zookeeper Node节点.
