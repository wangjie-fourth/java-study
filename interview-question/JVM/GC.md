2、对象一定在堆上分配的吗？
不一定。栈上分配

# GC
## 简单的说一下GC算法？
不同于`C++`语言来说，`java`语言是自动的回收垃圾，并不需要手动释放来及。`GC`就是`Garbage Collectors`垃圾回收器，用于**自动回收堆中**垃圾数据。

## 如何判断某个对象的是垃圾？
`java`有俩种方法判断：
- 引用计数法
- 可达性分析

### 引用计数法
这种方法就是一个对象A如果引用另一个对象B，那么对象B的引用计数就+1；垃圾回收的时候，根据每个对象的引用计算器如果是0的话，就说这个对象是垃圾。
这种方法的缺点是可能产生**循环引用**的问题，可能会导致这些对象就没法被回收，导致内存泄露问题
### 可达性分析
我们将一些对象视为`GC Root`对象，如果某个对象通过引用链可以达到`GC Root`对象得话，就认为这个对象是活对象。反之，认为它是垃圾对象。

## GC Root有哪些？
- 所有的`Thread`对象
- 栈帧中局部变量表中的对象
- 静态的变量，比如说静态变量、常量
- `JNI`持有得引用，比如说native方法中引用的变量
- 其他`JVM`持有得`GC Root`：比如说：如果年轻代在`GC`时，老年代里面得所有对象都是`GC Root`
> [参考信息](https://www.yourkit.com/docs/java/help/gc_roots.jsp)

## 有哪些GC算法？你了解哪些GC回收器？
## GC算法有：
### 引用计数法，
现在基本不用了，因为有**循环引用**的问题

### `Mark-and-Sweep`：标记清除
这种`GC`算法分成俩个阶段：第一个阶段用于标记内存中的有用数据；第二个阶段就是来清除内存没有标记的数据。这种算法会在内存中产生**内存碎片**问题。

### `Mark-Sweep-Compact`：标记、清除、压缩
这种`GC`算法分成三个阶段：前俩个阶段就是上面的；第三个阶段是把内存中的数据压缩一下，让他们尽量在某一块内存，解决**内存碎片**问题。这种算法的缺点就是如果标记数据的数量很多的话，第三阶段的效率比较低。

### `Mark-and-Copy`：标记、拷贝
这种`GC`算法分成俩个阶段：第一个阶段标记内存中的有用数据；第二个阶段就是将这些有用的数据拷贝到另一块内存中。
这种算法的好处是：解决了**内存碎片**问题；在某些情况下，他比前俩个算法效率更高，因为工作线程没有必要等待原来垃圾被回收，只要数据拷贝到另一块内存中，工作线程就可以工作了。
这种算法的缺点是：
（1）占用更多的内存
（2）如果有效数据很多的话，拷贝数据可能会浪费时间；

### 分代假设算法


### 分区算法

## GC回收器
### 串行垃圾回收器
### 并行垃圾回收器
### 并发垃圾回收器
### G1垃圾回收器





---
如何破坏双亲委派模型