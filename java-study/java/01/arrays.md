数组类型是`JVM`原生提供的定长数据结构，你看不到它的定义，但仍然可以使用它。它是由`jdk`根据特殊的指令来创建的。它主要特性有：
- 长度不可变
- 类型安全
- 只有一个`length`属性
- 可以使用`for`循环迭代它

```java
    public static void main(String[] args) {
        int[] a = new int[]{1,2,3};
    }
```
> 可以理解成`jdk`在`JVM`中为你创建`int[]`类型的字节码文件，这个类型有length属性。只不过它是由`jdk`为你创建的。

1、为什么我从来没有见过数组的定义？
数组是`JVM`提供的虚拟机级别的支持，有对应的字节码，但无`java`源码；比如说在字节码层面上，数组也是一个对象，也有`length`属性。

2、为什么说数组是真泛型，而泛型是假泛型？
- 真泛型是指在运行时，会有类型信息；
- 假泛型是指在运行时，没有类型信息；
```java
String[] a = new String[10];
Object[] b = a;
b[0] = new Object();//这里就会因为类型不同，而抛出异常
```

