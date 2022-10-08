# JAVA Reflection

## Annation 注解

### 内置注解

Java中定义好的注解称之为内置注解

@Override @OVerWite @PostConstruct

### 元注解

Java中用来定义注解的注解称之为元注解，meta-annation

- @Target 注解作用的类型，TYPE METHOD FIELD CONSTRUCTOR .... 
- @Retention 注解作用的范围 runtime(运行时) > class(编译后的class文件) > source(源码时期)
- @Inherited 子类可以继承父类的注解 
- @Docment 将注解生成到Java中

## 反射

### 什么是反射

反射是JAVA代码中，在运行时获取类信息的一种机制。

### 获取Class的方式

```Java
public class Main {
    public static void main(String[] args) throws ClassNotFoundException {
        // 获取Class的几种方式
        // 1. 通过Class.forName("path")获取
        Class c1 = Class.forName("demo.Student");
        System.out.println("c1 hashcode:" + c1.hashCode());
        // 2. 通过对象获取
        Student student = new Student();
        Class c2 = student.getClass();
        System.out.println("c2 hashcode:" + c2.hashCode());
        // 通过类名.class获取
        Class<Student> c3 = Student.class;
        System.out.println("c3 hashcode:" + c3.hashCode());
        // 基本类型的包装类
        Class<Integer> c4 = Integer.TYPE;
        System.out.println("c4 hashcode:" + c4.hashCode());
        // 与c4并不是同一个class
        Class<Integer> c5 = Integer.class;
        System.out.println("c5 hashcode:" + c5.hashCode());

    }
}
```

### 类的加载过程

1. 加载，通过classloader将编译好的class加载到JVM中，并在heap中生成对应的Java Class对象,此过程由类加载器完成；
2. 链接，链接又分为3个过程
   1. 验证，验证Class对象是否符合JVM标准
   2. 准备：准备过程中实现对类变量（static变量）的内存分配和分配零值，只要是 static类型都会在这个阶段完成
   3. 解析：将常量池中的符号引用（常量名）替换成直接引用（地址）
3. 初始化，这个阶段是执行类构造器<clint>方法的过程（**类构造器是指构造类的过程，并不是类对象的构造器**），此过程会将static变量的赋值动作和static代码块语句合并产生(按照先后代码的顺序进行整合)；

### 类什么时候会初始化

1. 类的主动引用会触发类的初始化
   1. 虚拟机启动的Main方法所在的类一定会初始化
   2. 使用new关键字进行实例化
   3. 通过反射的方法对类进行反射调用
   4. 当一个类的父类还没有被初始化的时候，会先对父类进行初始化
2. 类的被动引用不会触发类的初始化
   1. 引用类的常量不会触发类的初始化，因为常量在链接的准备阶段就已经放入来常量池中；
   2. 当访问一个静态域时，只有真正声明这个域的类才会被初始化，子类调用父类的静态变量，只有父类会初始化，子类并不会初始化；
   3. 通过数组定义类的引用，不会触发类的初始化，个人理解此过程只是引用类类的定义

### 类加载器的作用

1. JAVA 类加载器的类型
2. 自定义类加载器

### 双亲委派机制

### 类加载器的加载路径

### 泛型擦除



