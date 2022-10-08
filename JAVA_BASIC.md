# JAVA Basic

## JDK JRE JVM

- JDK  Java Development Kit Java开发工具
- JRE Java Runtime Environment Java运行时环境
- JVM Java Virtual Machine Java 虚拟机啊

## JavaSE JavaME JavaEE

- JavaSE Java Platform Standard Edition
- JavaME Java Platform Micro Edition
- JavaEE  Java Platform Enterprise Edition

## Java 命令

- java 运行java程序
- java 编译.java文件

## Java 注释

- 单行注释 

  ```java
  // 单行注释
  ```

- 多行注释 

  ```java
  /*
  多行注释
  可以同时注释多行
  */
  ```

- 文档注释

  ```java
  /**
  @Description 文档注释
  @Author guoyang
  */
  ```

## Java 命令规则

Java变量的规则

- 所有标识符都应该以字母（A-Z或者a-z），美元符（$），或者下划线（_）开始;
- 首字母之后的字符可以任意组合；
- Java区分大小写；
- 不能使用Java的关键字;

##  Java 数据类型

Java是强类型语言，变量必须先定义后才能使用；

`[修饰符] 变量类型 变量名称`

Java 数据类型分为两种：

1. 基础数据类型
2. 引用数据类型

### Java 基本数据类型

| 数据类型 | 范围                                 | 字节大小 | 对应的包装类型 |
| -------- | ------------------------------------ | -------- | -------------- |
| byte     | -128-127  (-2^7~2^7-1)               | 1byte    | Byte           |
| short    | -32768-32767 (-2^15~2^15-1)          | 2byte    | Short          |
| int      | (-2^31~2^31-1) 2147483648~2147483647 | 4byte    | Integer        |
| Long     | (-2^63~2^63-1)                       | 8byte    |                |
| flaot    |                                      | 4byte    | Float          |
| double   |                                      | 8byte    | Double         |
| char     |                                      | 2byte    | Character      |
| boolean  | true \| false                        | 1byte    | Boolean        |

 Java中8进制 10进制 16进制的表示

```java

public class Main {
    public static void main(String[] args) {
        // 8进制
        int num1 = 010;
        // 10进制
        int num2 = 10;
        // 16进制
        int num3 = 0x10;
        System.out.println(String.format("8进制：%d,10进制：%d,16进制：%d",num1,num2,num3));
    }
}

```

Java中尽量不要受用浮点型进行比较，因为精度不准确

```java
```



#### 基础类型之间的类型转换

Java 类型之间的转换优先级

byte ,short,char --> int --> long --> float --> double 

Java的类型存在两种类型转换

- 强类型转换；高优先级 ---- > 低优先级的，位数不够容易产生内容泄露问题
- 自动转换（隐式类型转换）; 低优先级 ----> 高优先级

  

### Java 引用数据类型

Java的引用数据类型有类，数组，接口



## Java Doc

## 方法

方法重载的规则

1. 方法的名称必须相同；
2. 方法的参数必须不同（参数的类型、参数的个数）；
3. 方法的返回类型可以相等，也可以不相等；
4. 仅仅返回值不相等，无法成为方法的重载

  ```java
      // 方法的重载
      public void Say(String name) {
          System.out.println(name);
      }
  
      public void Say(int age) {
          System.out.println(age);
      }
  
      public String Say(String firstname, String lastname) {
          return firstname + lastname;
      }
  ```

方法重载的原理：方法名称相同时，编译器会根据调用方法的参数个数，参数类型去逐个匹配，以选择对应的方法，如果匹配失败，则编译出错。

## 数组

数组是相同类型数据的有序集合

数组的特点：

1. 数组的长度是固定的，数组一旦创建，数组的大小就不可改变；
2. 数组的元素必须是相同类型的；
3. 数组的元素可以是任何数据类型，包括基本类型和引用类型；
4. 数组属于引用类型
5. 数组的本身就是对象，Java的对象是在堆中的，所以数组的元素类型无论是基本类型还是引用类型，数组对象本身都是在堆中的；

数组的使用：

稀虚数组



## 面向对象 OOP

### 什么是面向对象

OOP：Object-Oriented Programming

面向对象的本质是：以类的方式组织代码，以对象的方式封装数据

面向对象的三大特性：

- 封装
- 继承
- 多态

从认知的角度看，先有对象，后有类，类是对对象的抽象

从代码的角度看，先有类，后有对象，类是对象的模板

### 继承

Java类中都是单继承

### Java中的值传递和引用传递

- Java中都是值传递，所谓的引用传递只不过传递的是引用

### 类与对象的创建

### new关键字

### 类的构造器

- 无参构造器
- 有餐构造器
- 没有显示的指定构造器，默认会生成一个无参构造器

### this 与 super 关键字

- this 关键字指代的是当前类
- super关键字指代的是父类
  - spuer关键字在子类的构造方法中调用，一定要放在第一位，

### static 关键字

### 代码块、静态代码块、构造函数的执行顺序

静态代码块是跟随类产生的，类加载的时候就触发，只会执行一次，因为类只会加载一次；

内部方法块，随着类的实例话产生，每实例话一次，就触发一次；

构造方法，与内部方法一样，随着类的实例话产生，每实例话一次，就触发一次，不过是在内部方法块后触发；

```SQL
public class Student {
    // 内部代码块
    {
        System.out.println("1.内部代码块");
    }

    // 静态代码块
    static {
        System.out.println("2.静态代码块");
    }

    // 构造函数
    public Student() {
        System.out.println("3.构造函数");
    }

    public static void main(String[] args) {
       // 当Student类没有初始化的时候，只能输出 2.静态代码
       // Student stu1 = new Student();
       
       // new Student()输出的结果是：
       // 2.静态代码块 -> 3.内部代码块 -> 3.构造函数
       
       Student stu1 = new Student();
    }
}
```

### Java 修饰符

| 访问修饰符 | 所在类 | 同包子类 | 同包非子类 | 非同包子类 | 非同包非子类 |
| ---------- | ------ | -------- | ---------- | ---------- | ------------ |
| private    | 可以   | 不可以   | 不可以     | 不可以     | 不可以       |
| default    | 可以   | 可以     | 可以       | 不可以     | 不可以       |
| protected  | 可以   | 可以     | 可以       | 可以       | 不可以       |
| public     | 可以   | 可以     | 可以       | 可以       | 可以         |

## 抽象类

### 抽象类的规则

1. 抽象类必须使用 abstract关键字修饰
2. 抽象类不能被实例化，也就是不能new
3. 抽象类可以有抽象方法也可以有成员方法，抽象方法不能是私有的
4. 抽象类用有构造器的，也可以拥有成员方法

### 抽象类有构造器吗,为什么

抽象类是有构造器的，因为子类在实例化的时候需要调用父类的构造函数

### 为什么要有抽象类

为了更好的实现代码的OOP,将现实的事物，抽象成一个类

## 接口

### 接口的规则

- 接口的关键字是implents
- 接口中方法的默认修饰符都是 public abstract

- 接口中可以有变量，变量的默认修饰符都是 public final static

## 内部类

1. 成员内部类：作为外部类的成员变量，需要实例化外部类才能访问
2. 静态内部类：使用static 修饰的类，可以直接通过外部类来访问
3. 方法内部类：定义在方法内部的类。类似于局部变量
4. 匿名内部类: 没有名称的内部类

```SQL
public class Student {
    private String className;

    public Student(String className) {
        this.className = className;
    }

    // 成员内部类
    class Tom {
        public void Say() {
            System.out.println("I'm Tom from " + className);
        }

    }

    public static void main(String[] args) {
        // 调用内部类
        Student student = new Student(" class 7");
        Tom tom = student.new Tom();
        tom.Say();
    }

}
```

```java
public class Student {
    private String className;
    private static String school = "168 High School";

    public Student(String className) {
        this.className = className;
    }

    // 静态内部类
    static class Tom {
        public static void Say() {
            // 不能访问外部类的成员变量，因为static的声明周期与成员变量不一致
            // System.out.println("I'm Tom from " + className);
            // 只能访问静态变量
            System.out.println("I'm Tom from " + school);
        }
    }

    public static void main(String[] args) {
        Student.Tom.Say();
    }
}
```





## 异常机制

异常的父类是Throwable

异常分为：

1. Error

   程序运行时遇到的不可抗拒的因素导致的宕机，如OOM,StackOverflowError

2. Exception

   1. 编译时异常：程序在编译期就能检测到的异常：ClassNotFoundException
   2. 运行时异常：NPE ArrayIndexOutofBoundException