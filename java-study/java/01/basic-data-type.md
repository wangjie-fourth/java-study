
# 基本数据类型
`Java`一共有四大种、8小种基本数据类型，即：
- 4种整型：`byte`、`short`、`int`、`long`
- 2种浮点型：`float`、`double`
- 1种布尔类型：`boolean`
- 1种字符类型：`char`

## 整数类型
1、大概范围

| 类型  | 所占字节 | 取值范围 |     
| -- | -- | -- | -- |
| byte  |  1字节   |  -2^7 至 2^7 - 1  |
| short |  2字节   | -2^15 至 2^15 - 1 |
| int  |  4字节   |   正负20亿左右      |
| long  |  8字节   | -2^63 至 2^63 - 1 |

2、写法
有时候能看到代码中这样写：
```java
int a = 10_0000_0000;
long b = 22_0000_0000L;
```
> L可加可不加

## 浮点类型
1、大概范围

|  类型  | 所占字节 |   取值范围   |
| -- | -- | -- |
| float  |  4字节   | 有效位数6位  |
| double |  8字节   | 有效位数15位 |
> `double`有时候被称为双精度数值，是因为它表示的数值精度是`float`的俩倍

2、写法
```java
float a = 0.1f;
double b = 0.01d;
```
> d可加可不加

3、近似表示
十进制中，许多小数是无法用二进制来表示的，只能用近似表示。比如计算机在计算：
```java
0.1 + 0.2 = 0.30000000000000004； // 这就是因为近似表示的原因
```
由于近似表示，我们需要注意浮点数可以比较大小，但不能使用 `==`来比较相等。原因就是由于近似表示，可能会使我们程序逻辑失效。这时候，需要使用`Math`类来比较：
```java
float a = 0.1f;
float b = 0.1f;

if (Math.abs(a - b) < 0.0000001){
	System.out.println("a 与 b 相等");
}
```

4、其他解决办法 - `BigDecimal`对象
由于浮点数类型不适合比较、不适合出现舍入误差计算中。比如说：`System.out.println(2.0-1.1)`结果是`0.8999999999999999`，而不是`0.9`。主要原因是浮点数值是采用二进制系统表示，而在二进制系统中无法精确表示分数`1/10`。就好像十进制中无法精确表示`1/3`。如果数值计算中需要不含任何的舍入误差，应使用`BigDecimal`类。

## 布尔类型
1、布尔类型所占范围
当作为一个普通变量时，编译后使用`int`存储；所以占4个字节；当作为一个数组变量时，每个`boolean`只占1个字节；

2、注意
- 在`java`中，布尔类型不能与整型值进行相互转换

https://juejin.im/post/6844903912877588494

## 字符类型
1、所占范围
因为`java`中`char`是采用`Unicode`字符集来表示字符的，所以一个`char`占俩个字节。

2、注意：
- 字符类型可以当作数字来比较

3、`java`中的`char`可以存储汉字，并且大小是2个字节。如果某个汉字是三个字节呢？
显示不出来。`Unicode`早期设计的时候，认为2个字节完全可以存储世界上所有的字符。所以，`Java`设计的时候，`char`就是按照`Unicode`的俩个字节来存储。后面变成三个字节、四个字节都是后面的事了。最好的证明方式是：
```java
    public static void main(String[] args) {
        char demo = '\uffff';
        System.out.println("demo = " + demo);
    }
```
你在多加1，编译就会报错了。





## 基本数据类型默认赋值

- 如果是整数类型，默认为`0`；
- 如果是浮点类型，默认为`0.0`；
- 如果是字符类型，默认为`\u0000`；
- 如果是布尔类型，默认为`false`；

## 基本数据类型转换

`8`种基本数据类型中除了`boolean`类型数据，其他数据类型可以相互转换。
数据类型转换分为俩种：

- 自动类型转换（隐式）：低精度类型 转 高精度类型；小范围转大范围；
- 强制类型转换（显示）：高精度类型 转 低精度类型；大范围转小范围；

### 自动类型转换

自动类型转换发生在低精度类型 转 高精度类型，比如说：`int`转`double`。在俩个不同基本类型的值操作的时候，有时就发生转换：

- 如果其中有一个操作数是`double`，另一个操作数要先转换为`double`；
- 否则，如果其中有一个操作数是`float`，另一个操作数要先转换为 `float`；
- 否则，如果其中有一个操作数是`long`，另一个操作数要先转换为 `long`；
- 否则，俩个操作数都会转换为`int`类型；

常见的坑有：
```java
public static void main(String[] args) throws IOException {
     System.out.println("result = " + divide(3,2));//1.0
}
static double divide(int a,int b){
      /*
       * 等价于：
       *        double result = a / b;
       *        return result;
       */
      return a/b;
      // return 1.0 * a / b;
}
```

### 强制类型转换

强制类型转换发生在将大的数据类型转换为小的数据类型。比如说：`double`转`int`。这时候，可能会发生**数据溢出**。