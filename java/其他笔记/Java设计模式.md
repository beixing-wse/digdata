# Java设计模式

面试题中的知识点：

- 原型设计模式问题
  - 原型设计模式问题中的深拷贝和浅拷贝是什么
  - Spring中的原型bean的创建解释原型模式的应用
- 设计模式的七大原则
  - 单一职责原则
  - 接口隔离原则
  -  依赖倒转原则
  -  里氏替换原则
  -  开闭原则 ocp
  -  迪米特法则
  - 合成复用原则
- 状态设计模式
  - 订单平台，有审核-发布-抢单-等等步骤，岁操作得不同会改变订单的状态，项目中这个模块会使用到<font color="red">状态模式</font>，原因：如果每种状态都使用if/else,进行判断，代码就会越发臃肿，并且一旦没有处理某个状态，便会发生极其严重的BUG，难以维护。
- 解释器设计模式
  - 解释器设计模式是什么
  - Spring的框架中哪里用到了解释器设计模式，源码分析
  -  Spring框架中 SpelExpressionParser就使用到解释器模式
  - 分析设计模式的各个角色是什么
- 单例设计模式共有几种实现方式，（8）种
  - 恶汉式，两种
  - 懒汉式，三种
  - 双重检查
  - 静态内部类
  - 枚举

# 1、设计模式的重要性

​		①软件工程中，**设计模式**（design pattern）是对软件设计中**普遍存在（反复出现）**的各种问题，所提出的**解决方案**，设计模式是由建筑设计领域引入到计算机科学的。

​		②大厦是一个复杂的工程，而简易房是一个简单地工程，简易房就不需要设计模式。

​		③在实际项目工程中，当一个项目开发完后，如果客户提出新的功能，怎么办？（可扩展性，实用设计模式，软件就具有很好的扩展性）。

​		④如果项目开发完，原来的程序员离职，你接手维护的该项目怎么办？（维护性【可读性，规范性】）

​		⑤面试中会经常提问到设计模式，如何使用，在哪里使用，使用设计模式解决了什么问题？

​		⑥设计模式在软件中哪里？面向对象（oo）=> 功能模块【设计模式+算法（数据结构）】=>框架【使用到多种设计模式】=>架构【服务器集群】

​		⑦如果想成为合格的软件工程师，那就花时间研究下设计模式还是十分必要的。

# 2、设计模式七大原则

## 2.1设计模式的目的

​		编写软件过程中，程序员面临着来自耦合性，内聚性以及可维护性，可扩展性，重用性，灵活性等多方面的挑战，设计模式是为了让程序(软件)，具有更好

- 代码重用性（即相同的功能能够重复使用，而不需要重复编写）。
- 可读性（即：变成规范性，便于其他程序员的阅读和理解）。
- 可扩展性（即：在原来的基础上添加新的功能时，非常方便，称为可维护性）。
- 可靠性（即：当我们添加新的功能时，对原来的功能没有影响）。

以上4点使程序呈现高内聚，低耦合的特性。