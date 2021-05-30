
`java`除了8个基本数据类型，还有一个引用数据类型，其实就是对象，最主要的代表类就是`Object`。

# 对象的组成
- 字段
- 函数

## 函数
### 值传递
函数调用参数永远都是传值；（复制后传值）

# 对象的构造顺序
- 父类的静态代码快、静态成员字段【只在第一次加载类执行，优先级相同先后顺序执行】
- 子类的静态代码快、静态成员字段
- 父类的普通代码块、普通成员字段
- 父类的构造函数
- 子类的普通代码块、普通成员字段
- 子类的构造函数

验证程序：
```java 
class Log {
    public static String baseFieldInit() {
        System.out.println("Base Normal Field");
        return "";
    }

    public static String baseStaticFieldInit() {
        System.out.println("Base Static Field");
        return "";
    }

    public static String fieldInit() {
        System.out.println("Normal Field");
        return "";
    }

    public static String staticFieldInit() {
        System.out.println("Static Field");
        return "";
    }
}

class Base {
    static {
        System.out.println("Base Static Block 1");
    }

    private static String staticValue = Log.baseStaticFieldInit();

    static {
        System.out.println("Base Static Block 2");
    }

    {
        System.out.println("Base Normal Block 1");
    }

    private String value = Log.baseFieldInit();

    {
        System.out.println("Base Normal Block 2");
    }

    Base() {
        System.out.println("Base Constructor");
    }
}

public class Derived extends Base {
    static {
        System.out.println("Static Block 1");
    }

    private static String staticValue = Log.staticFieldInit();

    static {
        System.out.println("Static Block 2");
    }

    {
        System.out.println("Normal Block 1");
    }

    private String value = Log.fieldInit();

    {
        System.out.println("Normal Block 2");
    }

    {
        System.out.println("Normal Block 2");
    }

    public static void main(String[] args) {
        Derived d = new Derived();
    }
}
```

# 对象三大约定
equals
- 自反性
- 对称性
- 传递性
- 一致性

hashCode
- 终生不变性
- `equals`相同则`hashCode`必须相同
- `equals`不同`hashCode`可以不同

Comparable

# Object有哪些方法，都是做什么的？
- equals()、hashCode()：
- finalize()：
- notify()、notifyAll()、wait()
- getClass()
- toString()
- clone()