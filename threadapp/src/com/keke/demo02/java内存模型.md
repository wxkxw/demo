
1. Java内存模型基础

####  并发编程模型的两个关键问题
线程通讯
线程同步

如何解决的：
    
    共享内存
    同步快
    
#### Java内存模型的抽象结构

Java线程之间的通信由Java内存模型（本文简称为JMM）控制。
JMM决定一个线程对共享 变量的写入何时对另一个线程可见。

JMM通过控制主内存与每个线程的本地内存之间的交互，来为Java程序员提供 内存可见性保证。

JMM属于语言级的内存模型，它确保在不同的编译器和不同的处理器平台之上，通过禁
止特定类型的编译器重排序和处理器重排序，为程序员提供一致的内存可见性保证。

#### happens-before
happens-before仅仅要求前一个操作（执行的结果）对后一个操作可见，且前一

个操作按顺序排在第二个操作之前（the first is visible to and ordered before the second）。

#### 重排序

