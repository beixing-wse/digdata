# Flume参数调优

先简单总结一下Flume，Flume由3组件（Source，Channel，Sink），2个事务（put事务，take事务）,3个器（拦截器，选择器和监控器）共同构成。

通过3个组件来说一下Flume的调优

1. **Source**

    *增加Source个数*（使用Tair Dir Source时可以增大FileGroups个数），可以通过增加Source个数的方法增大读取数据的能力。如：当某一个目录产生的文件过多时，可以将这个文件目录进行拆分成多个目录。同时配置多个Source保证Source有足够的能力获取新产生的数据。

    *调大batchSize*，batchSize参数决定Source一次批量运输到Channel的event条数，适当调大这个参数可以提高Source搬运event到Channel时的性能。

2. **Channel**

    type 选择memory时Channel的性能最好，但是如果Flume进程意外挂掉可能会丢失数据。type选择file时Channel的容错性更好，但是性能上会比memory channel差。

    使用file Channel时*dataDirs配置多个不同盘下的目录*可以提高性能。

    Capacity 参数决定Channel可容纳最大的event条数。transactionCapacity 参数决定每次Source往channel里面写的最大event条数和每次Sink从channel里面读的最大event条数。**transactionCapacity需要大于Source和Sink的batchSize参数。**

3. **Sink**

    增加Sink的个数可以增加Sink消费event的能力。Sink也不是越多越好够用就行，过多的Sink会占用系统资源，造成系统资源不必要的浪费。

    batchSize参数决定Sink一次批量从Channel读取的event条数，适当调大这个参数可以提高Sink从Channel搬出event的性能。