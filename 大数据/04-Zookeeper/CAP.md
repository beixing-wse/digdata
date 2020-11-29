# CAP原则

## 概念

​		CAP原则是指在一个分布式文件系统中，<font color ="red">一致性（Consistency），可用性（Availability）和分区容错性（Partition tolerance）三个特性中只能同时实现其中两个。</font>

## CAP的定义

- <font color ="red">Consistency (一致性)</font>：所有节点同一时间的数据是完全一致的。对于服务端来说，如何将数据更新复制到所有的节点上。对于客户端来说，并发访问更新后的数据如何获取。一致性的问题是分布式系统中不可避免的。
- Availability（可用性）：“Reads and writes always succeed”，即服务一直可用，而且是正常的访问速度。好的的可用性是指系统能够很好的为用户服务，不会出现用户操作失败，访问超时的情况。
- Partition tolerance（分区容错性）：可靠性，即分布式系统中某个节点不可用或网络分区故障，仍然能够对外提供一致性和可用性的服务。



