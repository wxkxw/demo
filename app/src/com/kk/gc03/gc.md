
### 概述

·哪些内存需要回收？ 
·什么时候回收？ 
·如何回收？


程序计数器、虚拟机栈、本地方法栈3个区域随线程而生，随线程而灭，基本不需要去管。

堆：
    
### 对象已死

失去引用的对象需要回收

#### 引用计数法

算法简单

需要额外空间
容易造成相互引用，造成内存泄露

#### 可达性分析算法

生存还是死亡：
    标记两次才判断 是否回收
    第一次标记，
    为F-Queue的
    第二次如果 finalize()执行了 
    则也不回收

#### 回收方法区：

《Java虚 拟机规范》中提到过可以不要求虚拟机在方法区中实现垃圾收集，事实上也确实有未实现或
未能完整 实现方法区类型卸载的收集器存在（如JDK 11时期的ZGC收集器就不支持类卸载），方法区垃
圾收集 的“性价比”通常也是比较低的

在大量使用反射、动态代理、CGLib等字节码框架，动态生成JSP以及OSGi这类频繁自定义类加载
器的场景中，通常都需要Java虚拟机具备类型卸载的能力，以保证不会对方法区造成过大的内存压力。

### 垃圾收集算法

追踪式垃圾收集的范畴。

#### 1. 分代收集理论

1. 弱分代假说
2. 强分代假说

基于堆的分代的，才有了对应的分代类型，才有了“Minor GC”“Major GC”“Full GC”这样的回收类型的划分；

也才能够针对不同的区域安 排与里面存储对象存亡特征相匹配的垃圾收集算法——因而发展出了“标记-复制算法”
“标记-清除算 法”“标记-整理算法”等针对性的垃圾收集算法。
3. 跨代引用假说

注意 刚才我们已经提到了“Minor GC”，后续文中还会出现其他针对不同分代的类似名词， 为避免读者产生混淆，在这里统一定义： ·部分收集（Partial GC）：指目标不是完整收集整个Java堆的垃圾收集，其中又分为： ■新生代收集（Minor GC/Young GC）：指目标只是新生代的垃圾收集。 ■老年代收集（Major GC/Old GC）：指目标只是老年代的垃圾收集。目前只有CMS收集器会有单 独收集老年代的行为。另外请注意“Major GC”这个说法现在有点混淆，在不同资料上常有不同所指， 读者需按上下文区分到底是指老年代的收集还是整堆收集。 ■混合收集（Mixed GC）：指目标是收集整个新生代以及部分老年代的垃圾收集。目前只有G1收 集器会有这种行为。 ·整堆收集（Full GC）：收集整个Java堆和方法区的垃圾收集。

#### 常用垃圾收集算法

1. 标记-清除算法

2. 标记-复制算法

3. 标记-整理算法

#### 经典垃圾回收器

### 内存分配与回收策略

Java技术体系的自动内存管理，最根本的目标是自动化地解决两个问题：
自动给对象分配内存以及自动回收分配给对象的内存。

#### 对象优先在Eden分配

#### 大对象直接进入老年代

#### 长期存活的对象将进入老年代

#### 动态对象年龄判定

#### 空间分配担保
