# super()关键字

**由于子类不能继承父类的构造方法，因此，如果要调用父类的构造方法，可以使用 super 关键字。**super 可以用来访问父类的构造方法、普通方法和属性。

super 关键字的功能：

- 在子类的构造方法中显式的调用父类构造方法
- 访问父类的成员方法和变量。

## super调用父类构造方法

super 关键字可以在子类的构造方法中显式地调用父类的构造方法，基本格式如下：

```
super(parameter-list);
```

其中，parameter-list 指定了父类构造方法中的所有参数。**super( ) 必须是在子类<u>构造方法的方法体</u>的第一行。**

#### 例1

声明父类 Person 和子类 Student，在 Person 类中定义一个带有参数的构造方法，代码如下：

```java
public class Person {
		public Person(String name) {    }
}

public class Student extends Person {}
```

会发现 Student 类出现编译错误，提示必须显式定义构造方法，错误信息如下：

`Implicit super constructor Person() is undefined for default constructor. Must define an explicit constructor`



**==在子类的构造方法调用之前会先调用父类的构造方法。==**

在本例中 JVM 默认给 Student 类加了一个无参构造方法，而在这个方法中默认调用了 super()，但是 Person 类中并不存在该构造方法，所以会编译错误。



如果一个类中没有写任何的构造方法，JVM 会生成一个默认的无参构造方法。在继承关系中，由于在子类的构造方法中，第一条语句默认为调用父类的无参构造方法（即默认为 super()，一般这行代码省略了）。所以当在父类中定义了有参构造方法，但是没有定义无参构造方法时，编译器会强制要求我们定义一个相同参数类型的构造方法。

#### 例2

声明父类 Person，类中定义两个构造方法。示例代码如下：

```java
public class Person {    
		public Person(String name, int age) {    }    
		public Person(String name, int age, String sex) {    }
	}
```

子类 Student 继承了 Person 类，使用 super 语句来定义 Student 类的构造方法。示例代码如下：

```java
public class Student extends Person {    
		public Student(String name, int age, String birth) {        
			super(name, age); // 调用父类中含有2个参数的构造方法    
		}    
		public Student(String name, int age, String sex, String birth) {        
			super(name, age, sex); // 调用父类中含有3个参数的构造方法    
		}
}
```

从上述 Student 类构造方法代码可以看出，super 可以用来直接调用父类中的构造方法，使编写代码也更加简洁方便。

编译器会自动在子类构造方法的第一句加上`super();`来调用父类的无参构造方法，必须写在子类构造方法的第一句，也可以省略不写。通过 super 来调用父类其它构造方法时，只需要把相应的参数传过去。

## super访问父类成员

当子类的成员变量或方法与父类同名时，可以使用 super 关键字来访问。如果子类重写了父类的某一个方法，即子类和父类有相同的方法定义，但是有不同的方法体，此时，我们可以通过 super 来调用父类里面的这个方法。

使用 super 访问父类中的成员与 this 关键字的使用相似，只不过它引用的是子类的父类，语法格式如下：

```
super.member
```

其中，member 是父类中的属性或方法。使用 super 访问父类的属性和方法时不用位于第一行。

#### super调用成员属性

当父类和子类具有相同的数据成员时，JVM 可能会模糊不清。我们可以使用以下代码片段更清楚地理解它。

```
class Person {    int age = 12;}class Student extends Person {    int age = 18;    void display() {        System.out.println("学生年龄：" + super.age);    }}class Test {    public static void main(String[] args) {        Student stu = new Student();        stu.display();    }}
```

输出结果为：

学生年龄：12

在上面的例子中，父类和子类都有一个成员变量 age。我们可以使用 super 关键字访问 Person 类中的 age 变量。

#### super调用成员方法

当父类和子类都具有相同的方法名时，可以使用 super 关键字访问父类的方法。具体如下代码所示。

```
class Person {    void message() {        System.out.println("This is person class");    }}class Student extends Person {    void message() {        System.out.println("This is student class");    }    void display() {        message();        super.message();    }}class Test {    public static void main(String args[]) {        Student s = new Student();        s.display();    }}
```

输出结果为：

This is student class
This is person class

在上面的例子中，可以看到如果只调用方法 message( )，是当前的类 message( ) 被调用，使用 super 关键字时，是父类的 message( ) 被调用。

## super和this的区别

==**this 指的是当前对象的引用，super 是当前对象的父对象的引用。**==下面先简单介绍一下 super 和 this 关键字的用法。

super 关键字的用法：

- super.父类属性名：调用父类中的属性
- super.父类方法名：调用父类中的方法
- super()：调用父类的无参构造方法
- super(参数)：调用父类的有参构造方法


如果构造方法的第一行代码不是 this() 和 super()，则系统会默认添加 super()。


this 关键字的用法：

- this.属性名：表示当前对象的属性
- this.方法名(参数)：表示调用当前对象的方法


当局部变量和成员变量发生冲突时，使用`this.`进行区分。

关于 [Java](http://c.biancheng.net/java/) super 和 this 关键字的异同，可简单总结为以下几条。

1. 子类和父类中变量或方法名称相同时，用 super 关键字来访问。可以理解为 super 是指向自己父类对象的一个指针。在子类中调用父类的构造方法。
2. this 是自身的一个对象，代表对象本身，可以理解为 this 是指向对象本身的一个指针。在同一个类中调用其它方法。
3. this 和 super 不能同时出现在一个构造方法里面，因为 this 必然会调用其它的构造方法，其它的构造方法中肯定会有 super 语句的存在，所以在同一个构造方法里面有相同的语句，就失去了语句的意义，编译器也不会通过。
4. this( ) 和 super( ) 都指的是对象，所以，均不可以在 static 环境中使用，包括 static 变量、static 方法和 static 语句块。
5. 从本质上讲，this 是一个指向对象本身的指针, 然而 super 是一个 Java 关键字。

#### 例 3

在 Animal 类和 Cat 类中分别定义了 public 类型的 name 属性和 private 类型的 name 属性，并且 Cat 类继承 Animal 类。那么，我们可以在 Cat 类中通过 super 关键字来访问父类 Animal 中的 name 属性，通过 this 关键字来访问本类中的 name 属性，如下面的代码：

```
// 父类Animal的定义
public class Animal {    
		public String name; // 动物名字}
//子类Cat的定义
public class Cat extends Animal {    private String name; // 名字    public Cat(String aname, String dname) {        super.name = aname; // 通过super关键字来访问父类中的name属性        this.name = dname; // 通过this关键字来访问本类中的name属性    }    public String toString() {        return "我是" + super.name + "，我的名字叫" + this.name;    }    public static void main(String[] args) {        Animal cat = new Cat("动物", "喵星人");        System.out.println(cat);    }}
```

上述代码演示了使用 super 关键字访问父类中与子类同名的成员变量 name，this 关键字访问本类的 name 变量。运行程序，输出结果如下：

```
我是动物，我的名字叫喵星人
```