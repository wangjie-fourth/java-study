所有的包装类都是不可变对象，都是`final`的。

# Integer内部优化
在`int`基本数据类型数据会自动装箱到`Integer`，而每次装箱都`new`一个对象的话，可能有点浪费空间。
所以，`JDK`默认基本数据为`-128 ~ 127`之间的数据，装箱到一个缓存中，如果以后还有相同的数字想转成`Integer`的话，就默认从缓存中获取。
```java 
public static void main(String[] args) {
      Integer a = 1;
      Integer b = 1;
      System.out.println(a);
}
```


# 为啥需要自动拆装箱
在`java`的范型系统中，是不支持基本数据类型的，比如：`List<int>`，而这种实现会很麻烦，所以干脆就不支持基本数据类型，所以就搞成`List<Integer>`。

