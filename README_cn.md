# 单元化架构
单元化架构是基于单元进行大规模业务系统的整体设计、开发、部署、运维的架构实践。


# AlphaOne-CellArchitecture

## 介绍
AlphaOne 是一个生产级、企业级、金融级的，基于单元化架构和微服务架构的分布式技术平台，可以作为大型金融类型企业的数字化转型改造的技术基座。

- **生产级**：production-ready（生产就绪），区别于demo/poc级以及小规模应用系统，各类组件都经过了大规模生产环境的验证。
- **企业级**：区别于支撑单个系统的技术或组件，各类组件都可以实现对企业内几百上千个业务系统的接入使用，成为企业的基础分布式能力。
- **金融级**：在稳定性、可靠性、可用性、性能、一致性等非功能要求上，满足大规模高并发金融场景的业务需要、运维需要、监管需要。

### 单元化架构
**Cell Architecture**，简称CA，是将整个大规模分布式业务系统划分成多个不同类型不同数据的单元进行设计和部署的架构模式，从而实现容量和流量的分配调拨、运维管控的统一管理，灾难恢复和故障切换等高可用特性。

### 微服务架构
**MicroServices Architecture**，简称MSA，是将企业的业务系统和业务数据按照服务进行拆分，独立设计、开发、部署、运维和演进的架构模式，从而在借助大规模自动化手段的情况下，提升整个系统的研发效能、降低业务复杂度。（从设计上考虑同时兼容spring cloud和dubbo）

### 分布式技术平台
**分布式技术平台**（Distributed Technical Platform，DTP）在传统的云基础架构划分里，偏向于PaaS层，由大量的分布式组件组成，向下需要适配不同的底层IaaS能力，向上需要支撑大规模应用开发，从而作为整个企业迈向下一代分布式技术（甚至云原生容器化）的技术底座。

## 软件架构

### 分布式组件
#### 1.微服务组件
- 远程过程调用 RPC（Remote Procedure Call）：兼容主流协议Dubbo、Spring Cloud、GRPC等
- 微服务网关 MGW（Microservices GateWay）：配合单元化，以及注册中心，可考虑Spring Cloud Gateway，Zuul2，Shenyu，Kong，APISIX等
- 分布式注册中心 DRC（Distributed Registry Center）：应用级注册、多机房同步，企业级能力，可考虑Nacos/ZooKeeper/Consul/etcd等
- 分布式配置中心 DCC（Distributed Configuration Center）：多机房同步，企业级能力，可考虑Apollo/Nacos/Disconf/Spring Cloud Config等

其他能力：
- 流量控制：针对线程资源，调用方和调用次数，进行流量控制，Resilient4j/Sentinel
- 故障隔离：针对故障节点进行隔离，从服务到中间件，到数据库
- 灰度发布：实现灰度节点，灰度单元，以及流量的调拨
- 超时重试：全链路的超时控制，以及部分节点的重试机制
- 优雅启停：启动和停机，尽量不对正在处理的业务产生影响
- 异常处理：全局的异常处理机制，异常码，区分技术异常和业务异常
- 日志监控：日志记录和跟踪，用于排查业务运维问题，监控系统状态, ELK, Promethus+Grafana
- 链路跟踪：全链路的调用跟踪分析，用于分析和优化性能，Skywalking
- 服务挡板：直接为制定服务提供mock信息，不执行实际调用
- 多环境支持：针对多套测试环境，可以基于基准环境实现增量服务模式，降低资源消耗

#### 2.数据组件
- 数据访问层 DAL，Data Access Layer，druid/hikari/Mybatis
- 分库分表 DSS，Data Sharding Service，ShardingSphere-JDBC
- 读写分离 RWS，Read-Write Splitting，ShardingSphere-JDBC
- 分布式事务 DTX，Distributed Transaction，Seata/hmily/XA
- 数据库高可用 DHA，Database High-Availability，MGR or else?
- 数据代理服务（运维侧）DAP，Data Access Proxy，ShardingSphere-Proxy
- 数据聚合服务（业务侧）DAS，Data Aggregation Service，ElasticSearche

#### 3.单元化组件
- 全局路由服务 GRS, Global Router Service
- 单元架构设计 CAD, Cell Architecture Design
- 单元故障转移 CFO, Cell FailOver
- 单元流量调拨 CTA, Cell Traffic Allocation


#### 4.分布式组件
- 分布式消息队列 DMQ，Distributed Message Queue，RocketMQ/Kafka
- 分布式缓存服务 DCS，Distributed Cache Service，Redis/Hazelcast/Ignite
- 分布式文件系统 DFS，Distributed File System，DFS/HDFS/Ceph/GlusterFS/MooseFS/TFS/GridFS
- 分布式序号服务 DSS，Distributed Sequence Service，
- 分布式锁服务    DLS，Distributed Lock Service，Redisson/Hazelcast/Ignite
- 分布式数据结构 DDS，Distributed Data Structure，Redisson/Hazelcast/Ignite

#### 9.联机交易组件
TODO

#### 10.批量处理组件
TODO

#### 11.容器化能力 -- 2期
- 镜像管理
- 网络配置
- 资源调度
- 弹性扩缩容

#### 12.企业级能力 -- 2期
- xxx

#### 13.多租户能力 -- 2期
- xxx



- xxx


