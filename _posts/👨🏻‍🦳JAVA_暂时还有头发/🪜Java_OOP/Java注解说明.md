## 注解

- **注释：一般用于说明“//”、“/\*...*/"等符号**

- **注解：以符号@开头，如@Override**



> 注解可以用元数据这个词来描述，**即一种描述数据的数据**。

```java
@Override
public String toString() {
    return "C语言中文网Java教程";
}
```

上面的代码**重写**了 Object 类的 toString() 方法并使用了 @Override 注解。如果不使用 @Override 注解标记代码，程序也能够正常执行。

那么这么写有什么好处吗？事实上，使用 @Override 注解就相当于告诉编译器这个方法是一个重写方法，**如果父类中不存在该方法，编译器便会报错**，提示该方法没有重写父类中的方法。这样可以防止不小心拼写错误造成麻烦。

例如，在没有使用 @Override 注解的情况下，将 toString() 写成了 toStrring()，这时程序依然能编译运行，但运行结果会和所期望的结果大不相同。



**注解常见的作用有以下几种：**

1. **生成帮助文档**。这是最常见的，也是 Java 最早提供的注解。常用的有 @see、@param 和 @return 等；
2. 跟踪代码依赖性，实现替代配置文件功能。比较常见的是 [Spring](http://c.biancheng.net/spring/) 2.5 开始的基于注解配置。作用就是减少配置。现在的框架基本都使用了这种配置来减少配置文件的数量；
3. 在编译时进行格式检查。如把 @Override 注解放在方法前，如果这个方法并不是重写了父类方法，则编译时就能检查出。


**无论是哪一种注解，本质上都一种数据类型，是一种接口类型。**到 Java 8 为止 Java SE 提供了 11 个内置注解。其中有 5 个是基本注解，它们来自于 java.lang 包。有 6 个是元注解，它们来自于 java.lang.annotation 包，自定义注解会用到元注解。



## @Override注解

> @Override 注解是用来**指定方法重写**的，只能修饰方法并且只能用于方法重写，不能修饰其它的元素。它可以强制一个子类必须重写父类方法或者实现接口的方法。



```JAVA
public class Person {
    private String name = "";
    private int age;
    ...
    @Override
    public String t0String() { //toString()
        return "Person [name=" + name + ", age=" + age + "]";
    }
}
```

上述代码第 6 行是重写 Object 类的 toString() 方法，该方法使用 @Override 注解。如果 toString() 不小心写成了 t0String()，那么程序会发生编译错误。会有如下的代码提示：

`类型为 Person 的方法t0String()必须覆盖或实现超类型方法`

所以 @Override 的作用是告诉编译器检查这个方法，保证父类要包含一个被该方法重写的方法，否则就会编译出错。这样可以帮助程序员避免一些低级错误。