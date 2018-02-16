官网：http://storm.apache.org

Storm常见场景
- 推荐系统: 实时推荐
- 金融系统:
- 预警系统:
- 网站统计: 实时统计，流量计算，如双11的成交额

Storm关键特性
- 适合场景广泛
- 可伸缩性高：基于Zookeeper协调集群内的各种配置
- 保证无数据丢失：Storm可以保证每条数据都能得到处理
- 健壮性高：基于Zookeeper进行管理
- 容错性好：支持消息异常进行重试
- 语言无关性：Storm的topology和消息处理组件Bolt可以用任何语言定义

Storm提供实时计算框架，用户仅关注业务开发即可。

---
## 1、Storm集群架构
参考：https://www.w3cschool.cn/apache_storm/

|主节点|工作节点|作业
:----|:-----:|:-----:| :-----:|
Storm  |Nimbus| Supervisor|Topology（内部是死循环，流式计算）
Hadoop  |ResourceManager |NodeManager|MapReduce Job

主节点 Nimbus和工作节点SuperVisor是不耦合的，所有状态信息存储在ZK中。以临时目录判断工作节点是否在线。

基本概念：
- Nimbus：topo只能在nimbus机器上提交，负责集群分发代码，将任务分发到其他机器，故障监控；
- Supervisor: 监听分配给它的节点，根据nimbus的委派在必要时执行启停进程，每个工作进程执行topology的一个子集，一个运行中的topo，由很多机器上的工作进程组成；
- Streams: 消息流，是一个无界的连续tuple；
- Tuple：在Storm是对于流Stream的抽象，**流** 是一个无间断的无界的连续tuple，流中的事件抽象为Tuple（元组）；Tuple是值列表（value list）；list中的每个value都有一个name，该value可以是任意序列化的类型。
- Spout：获取并消费数据源，认为是Stream的源头，自己不产生数据，对接其他数据源；
- Bolt：处理Tuple的处理器；可以多个Bolt串行处理；同个Spout可以发给多个Bolt，消息处理的逻辑，里面有execute方法进行死循环处理。

**备注**

topo的每个节点都要说明它发射出的元组的字段的name，其他节点只需要订阅name就可以接受处理，storm只对可靠的spout调用ack和fail。

---
## 2、Storm集群安装
---
## 3、Storm API
