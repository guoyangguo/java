# Java 面试题

## 什么是JDk JRE JVM

1. JDK  java development kit java 开发工具
2. JRE java runtime environment java 运行时环境
3. JVM java virtual machine java虚拟机

## 什么是字节码，有什么好处

1. 字节码，Java源码文件通过Javac命令编译后生成的class文件，class文件中的文件内容就是字节码
2. 字节码可以实现Java程序的跨平台运行，因为字节码文件是运行在JVM中的，JVM是运行在操作系统上的，所以只需要关心JDK在不同操作系统上的实现即可。

## 面向对象的三大特性

1. 封装，将类的属性对外隐藏，开放方法访问
2. 继承，子类继承父类
3. 多态，父类调用子类的实现

## hashcode 与 equals之间的关系

1. 两个对象相同，那么hashcode一定相同
2. hashcode相同，不一定是同一个对象
3. 两个对象相等，hashcode一定相同
4. 重写hashcode方法，一定要重写equals方法
5. equals的特性
   1. 对称性，对于任何引用x和y，当且仅当y.equals(x)返回true，x.equals(y)也应该返回true
   2. 自反性，对于任何非空引用x，x.equals(x)应该返回true。
   3. 传递性, 对于任何引用x、y和z，如果x.equals(y)返回true，y.equals(z)返回true，x.equals(z)也应该返回true
   4. 一致性，如果x和y引用的对象没有没有发生变化，反复调用x.equals(y)应该返回相同的结果
   5. 对于任何非空引用x，x.equals(null)应该返回false
6. 在比较2个引用对象时候相等的时候，通过会先通过hashcode比较，如果hashcode相同，再通过euqals比较

## equals 与 ==

1. 对于基础数据类型使用只能使用==，此处 == 比较的是值
2. 对于引用类型，要看有没有重写equals方法，默认的equals方法就是 == ，比较的就是内存地址，但是**String重写了equals方法**

## String StringBuffer StringBuild

1. String 
   1. String 是final修饰的，是不可变类，线程安全，对String的每个操作都会产生一个新的对象；
2. StringBuffer 
   1. StringBuffer解决了String频繁出现新对象的问题，StringBuilder的底层是一个char[]，默认的容量是 str.length+16
   2. StringBuffer是线程安全的，相应的方法都加上了sync关键字
   3. 扩容机制
      1. 当追加的字符串的长度超过当前容量，扩容为当前capactiy *2+2
      2. 当追加字符串的长度超过当前capacity *2+2，直接扩容到当前追加字符串的长度
   4. 每次扩容都涉及到创建新的数组和数组之间的copy,所以在能够预知字符串长度的情况下，初始化的设置capacity
3. StringBuilder
   1. StringBuilder的实现与StringBuffer相同，只是StringBuilder是非线程安全的，单线程环境下使用

## 泛型中 extends 和 super的区别

1. extends 是上界通配符，来限制具体类的类型，只能是extends指定类及其子类，在添加的时候会导致有多个具体类型
2. super 是下界通配符，来限制具体的类型只能是指定类和及其父类，在取数据的时候必须要强转成Object

## 泛型的类型擦除

1. 泛型的类型擦除是为了向下兼容，jdk5后才出现的泛型
2. 泛型的出现是为了将参数更好的类型化
3. 泛型只存在源码阶段，编译后会消除,替换成对应的上下届类型，没有则是Object类型

## 重载和重写的区别

1. 重载是同一个类中存在多个名称相同，参数不同的方法

   1. 参数不同可分为 参数类型不同，参数个数不同
   2. 返回值不同不能称之为重载

2. 重写是指子类对父类方法的重写

   1. 子类对父类方法的重写有以下规则

      1. 子类方法的返回值范围小于等于父类
      2. 子类方法抛出的异常要小于等于父类
      3. 子类访问修饰符要大于等于等于父类

      ```java
      //父类的方法
      protected Integer say() throws RuntimeException {
              return 0;
          }
      // 子类的方法
      public Integer say() throws ArrayIndexOutOfBoundsException{
              return 0 ;
          }
      ```

## List 与Set的区别

1. List
   1. List 是有序的,通过插入的顺序排序
   2. List允许重复值
   3. List可以通过下表取元素
2. Set
   1. Set是无序的
   2. Set不允许有重复值值
   3. Set只能通过遍历

## ArrayList 与 LinkedList的区别

1. ArrayList 与LinkedList都是Java的集合类，都实现了List接口
2. LinkedList还实现的Deque的接口，有双向队列的操作方法
3. ArrayList的底层是数组实现的
   1. ArrayList的查询速度比较快，插入删除操作比较慢，适合读多写少的操作
   2. ArrayList的默认大小是10，每次扩容为原来的50%
4. LinkedList的底层是双向列表实现的
   1. LinnkedList查询速度比较慢，插入和删除速度比较快，适合写多读少的操作

## ConcurrentHashMap的扩容机制

ConcurrentHash采用的是分段思想，但是在JDK7 与 JDK8中的实现机制不同

1. JDK7中每个segment

## JDK7 JDK8之间HashMap的变化

## 黑红树

## HashMap的Put方法

## HashMap的扩容机制

## CopyOnWriteArrayList的底层原理

1. CopyOnWriteArrayList底层的数据结构是数组
2. 对于多个线程操作的时候，每个线程都能访问到底层的数组(get 方法，调用getArray())，当某个线程需要写操作的时候，会先加锁,然后创建新的数组，进行数组拷贝，最后释放锁；此过程不影响读操作，读的数据会有延迟，对数据实时性要求高的不能采用此数据结构

## 深拷贝浅拷贝

1. 浅拷贝，对于基础数据类型直接拷贝值，对于引用类型，拷贝引用地址
2. 深拷贝，对于基础数据类型直接拷贝值，对于引用类型，同样拷贝一个新的对象
   1. 实现深拷贝的三种方式：
      1. 通过new一个新的对象
      2. 实现Cloneable接口，并重写clone()方法，通过 Parent parent2 = (Parent) parent.clone();每个类都需要实现；
      3. 通过序列化和反序列化

## Java异常体系

1. Java的异常的父类是 Throwable
2. Java异常分为 Error和Exception
3. Error 是程序遇到的不可恢复的错误，代码中无法控制的，比如 OutOfMemoryError StackOverfolwError
4. Exception 
   1. 检查时异常，编译期能检测的异常，IOException 
   2. 运行时异常，运行时发生的异常，ArrayIndexOutOfBoundsException NPE
5. 不能生吞异常
6. 异常的捕获应当遵循从小的大的规则
7. 避免打印堆栈信息，printStackTrace()里加锁

## Java中的类加载器

1. 根加载器 BootStrapClassLoader 加载 JAVA_HOME/lib
2. 扩展类加载器 ExtClassLoader 加载 JAVA_HOME/lib/ext/lib
3. 应用类加载器 AppClassLoader
4. 自定义类加载器
   1. 继承ClassLoader
   2. 重写findClass方法
5. 类加载器有缓存加载功能，如果发现已经加载过了，就不在加载
6. 类加载器有命名空间隔离，父类加载器无法加载子类空间的类

## 类加载的双亲委派模型

1. 类加载器在加载一个类的时候，会将这个类一直向上委托给他的父加载器，如果父加载器加载过了就不再加载，反之返回到当前加载器自己加载
2. 双亲委派模型，保证JDK核心类的优先加载
3. 双亲委派模型，保证Java自己内部lib的安全性
4. 双亲委派模型，保证JVM只有一份相同的字节码

## 自定义加载器

1. 自定义类继承ClassLoader
2. 重写loadClass方法

## 什么是SPI

1. SPI S ervice Provider Interface 接口提供商
2. SPI 可以破坏双亲委派模型

## SPI原理

1. 通过 ServiceLoader.class 传入当前线程的类加载器，和加载的class，构建一个ServicerLaoder对象

2. new 一个LazyIterator，扫描META-INF下指定的services 

3. 将配置文件中的所有配置类的全定限名，通过反射加载，并实例化到缓存中去

4. SPI每次加载就会加载所有配置文件中指定的类

   ```java
   // 1. 定义一个com.autumnin.Uploade接口
   // 并构造好实现类
   
   // 2. resouces/META-INF/com.autumnin.Uploader
   com.autumnin.spi.AliUpload
   com.autumnin.spi.BaiduUpload
   // 3.通过ServiceLoader加载
   ServiceLoader<Upload> uploads = ServiceLoader.load(Upload.class);
           uploads.forEach(it-> {
               it.upload();
           });
   ```

## 破坏双亲委派模型

1. 自定义类加载器，重写ClassLoader方法（只要不是类加载向上传递就是打破双亲委派）(Tomcat)
2. 使用SPI（JDBC）

## Tomcat 是如何打破双亲委派模型的

1. Tomcat给每个Webapp 都分配了一个WebAppClassLoader,优先加载当前应用目录下的类，如果当前应用找不到在一层层的向上
2. 如果Web应用的依赖不需要隔离的话，将应用程序之间需要共享的lib放到同一个目录下，使用SharedClassLoader进行加载
3. 为了隔绝Tomcat本身与Web应用之间的依赖，Tomcat使用CatalinaClassLoader来加载自身的类

## JDBC 是如何打破双亲委派模型的

1. JDBC定义了接口，由各个厂商去是实现具体的类
2. 类加载的规则：如果一个类是由类加载器A加载的，那么该类的依赖类也是由A加载器加载
3. 使用JDBC的时候是通过DriverManager类操作的，该类处于JAVA_HOME/lib下根Bootstrap加载器加载，所以，具体的实现类也应该由根加载器加载，
4. 但是类加载有命名空间隔离性，无法加载到具体的实现类，（除非放到对应的命名空间中）
5. JDBC的解决方案是，在DriverMananger初始化的时候，得到上下文加载器，由当前的上下文加载器去加载

## 一个类从加载到JVM到被GC清除经历了什么

## 怎么判断一个对象是不是垃圾对象

1. 引用计数法
   1. 每个对象会额外保存一个引用计数，如果有一个对象引用了它，计数器就+1
   2. 存在循环引用问题
2. 可达性分析

## 哪些对象是根对象

## JVM GC 算法

## 什么是STW

## 线程安全的理解

## 守护线程

## ThreadLocal的底层原理

## ThreadLocal有什么隐藏问题

## 并发 并行 串行

## 死锁

## java中查看死锁

jstatck 

## 使用锁的要素

锁的粒度要可能的小



## 线程池的底层原理

## 线程池为什么是先创建队列，而不是先创建最大线程

## AQS



## ReentrantLock

## synchronized

## synchronized 的偏向锁、轻量级锁、重量级锁

## synchronized 与ReentrantLock的区别



## Sych

## 公平锁非公平锁的底层原理

## tryLock() lock()的区别

## countDownLatch

## Semaphore 信号量





## 













# JVM

## JVM 模型

1. 程序计数器 Progrom Counter Register
   1. 当前线程执行字节码的行号指示器
   2. 每个线程私有的
   3. 是JVM中唯一没有规定OOM的区域
   4. Java中的多线程是通过线程轮流切换，分配处理器执行时间的方式实现的
2. 虚拟机栈 Stack
   1. 虚拟机栈是Java方法执行的线程内存模型，每一个方法的调用到执行结束就对应一个栈帧的出栈入栈的过程
   2. 栈帧由局部变量表 操作数栈 方法的返回信息 动态链接组成
      1. 局部变量表，存储编译期可知各种基础数据类型和对象的引用
   3. 线程私有的
      1. 当线程所申请的栈的深度大于虚拟机所允许的最大深度产生 StackOverflowError
      2. 当栈扩展时无法申请到更多的内存，就会产生OOM
   4. 默认单个线程栈的大小是1M
   5. 通过 Xss指定大小
3. 本地方法栈 Native Stack
   1. 本地方法栈与虚拟机栈基本一致，只不过是用来执行本地方法的
   2. JVM会将所有的本地方法列在本地方法栈中，然后通过JNI去调用
   3. HotSpot中将虚拟机栈和本地方法栈合二为一了
4. 元空间（方法区）Meta-Space (Method Area)
   1. 用于存放虚拟机加载的类型信息，常量，静态变量，和JIT产生的代码缓存
   2. 线程共享的区域
   3. 内存回收的目标是 常量池的回收和对象的卸载
   4. 逻辑上属于堆，物理上不属于堆
   5. 没有足够多的内存就会产生OOM
5. 堆 Heap
   1. 堆是JVM中内存分配最大的一块
   2. 是线程共享的
   3. 堆中存放的是对象的实例，new关键字产生的实例都在这
   4. 堆中又分为 新生代（Eden区，S0,S1 8:1:1） 老年代
   5. -Xmx512m -Xms512m 指定最大可申请内存是512M,最低要求内存是512M,
   6. -Xmx512m -Xms512m 相同表示堆内存不可动态扩展
   7. 默认的Xmx是物理内存的1/4，Xms是1/64
   8. 无法有足够多的内存分配给新的对象实例就会产生OOM
6. 直接内存 Direct Memory
   1. 不属于JVM内存模型的一部分
   2. 当JVM内存+直接内存超过物理内存时就会OOM

## 对象的组成

1. Java中对象由 对象头 实例数据 对齐填充组成
   1. 对象头
      1. 对象hashcode 
      2. GC分代年龄
      3. 锁状态标志
      4. 线程持有的锁
      5. 偏向线程ID
      6. 偏向时间戳
      7. 32位JVM的Mark word为32位，64位JVM为64位
   2. 实例数据
   3. 对齐填充
      1. 对象的大小必须是8字节的整数倍
2. Java对象的内存分配方式
   1. 指针配置
   2. 空闲列表

## 对象的访问定位

1. 句柄访问
2. 指针访问

### 如何判断对象已死

1. 引用计数法
   1. 对象中添加引用计数器，一个对象被引用一次计数器就+1，引用失效就-1，为0则没有引用；
   2. 引用计数法无法解决循环引用问题
2. 可达性分析算法
   1. 以GCRoots为根，从GCRoots到目标对象间不存在引用链则对象不可达，可进行回收
   2. 可作为GCRoots的对象
      1. 局部变量表的引用对象
      2. 方法区的静态变量
      3. 常量池中的引用对象
      4. JNI引用的对象
      5. JVM内部的引用
   3. 一个对象被真正回收的时候会经过2次标记，一次是GCRoots不可达时，另一次是finalize方法没有被重写或者finalize重写但已经被执行过

## 4种引用

1. 强引用 ，Java中new的对象都属于强引用，只要引用还在GC就不会回收，宁愿OOM
2. 软引用，软引用通常描述还有用但非必要的对象，在将要OOM之前会对象软引用对象进行一次回收，属于内存后留着，内存不够就回收
3. 弱引用，同样描述还有用但非必要的对象但是程度比软引用要弱，无论内存是否还够，GC开始后都会被回收
4. 虚引用，虚引用不会对象对象的生存周期产生影响，GC都会回收，但是虚引用的对象在回收的时候，会收到系统通知

### finalize方法

1. 重写了finalize，可以对即将回收的对象进行一次抢救，对对象重新赋值（加上引用）
2. finalize方法只会被执行一次
3. JVM对finalize的执行，是开启一个优先级比较低的线程去执行的，不会等待结果

## 方法区如何回收

1. 方法区的回收主要面临两个方面
   1. 回收不在使用的类型，类的卸载（ 没有引用了就可以卸载了）
   2. 回收常量池中没有引用的常量，没有任何字符串对象引用引用常量池中的变量

## JVM 相关的命令

1. jps 查看当前用户下的所有java进程
   1. jps -l 输出启动类
   2. jps -v 输出jvm参数
   3. jps -m 输出Main.class参数

```shell
guoyang@Guoyangs-mbp ~ % jps
18931 Launcher
17605 RemoteMavenServer36
17575 
19549 Jps
```

2. jinfo ${pid} 查看JVM的运行参数
3. jstat 查看java应用程序的资源和性能

### JVM中有哪些是线程共享的区域

1. 线程中堆（heap）是每个线程共享的区域
2. 方法区（method area）是每个线程共享的
3. 方法栈，本地方栈，程序计数器都是每个线程私有的

## 垃圾回收算法

1. 标记-清除算法，分为标记和清除2步
   1. 标记，利用可达性分析算法，标记出不可达的对象
   2. 清除，标记完成后，清除所有的不可达的对象
   3. 随着对象的数量增长而效率降低
   4. 标记清除后会产生大量不连续的内存碎片 
   5. 内存碎片太多导致分配大对象的时候找不到足够的内存，就会触发另一次GC
   6. 已经淘汰不使用了
2. 标记-复制算法，解决标记-清除算法面对大量对象时效率低的问题
   1. 将内存分成大小相同的两块，每次使用其中的一块
   2. 当使用的这一块内存快用完的时候，就将对象转移到另外一块，然后对使用过的进行GC
   3. 对于大部分都是可回收的对象，每次复制都是少量存活的对象
   4. 每次都是整个半区进行清理，内存比较完整
   5. 缺点是，可用的内存变成了原来的一半
   6. 新生代采用的GC算法就是 标记-复制 算法
3. 标记-整理算法，标记-复制算法在存活的对象比较多的时候，效率比较低，每次需要复制大量的数据
   1. 整理，将存活的对象移动到内存的一端，移动完成后，清除边界以外的内存
   2. 每次移动存活的对象都需要暂停所有的用户进程（需要重新更新引用），这会产生STW
   3. STW,Stoping The World 程序会暂停服务
   4. 老年代采用的GC算法

## JVM的垃圾收集器

1. Serial 收集器
   1. 串行收集器，GC线程工作时3，必须暂停所有用户线程，直到GC结束
   2. 频繁的GC会导致频繁的STW
2. Par New 收集器
   1. 本质上是 Serial 收集器的多线程版本
3. Parallel Scavenge 收集器
   1. 并行清楚收集器，采用标记-清除算法实现的，并行多线程垃圾收集器
   2. 自适应调节策略，通过可控制的吞吐量近可能的缩短垃圾收集时用户线程的停顿时间
4. CMS 收集器
   1. Concurrent Mark Sweep 并发-标记-扫描 基于 标记-清除 算法的收集器
   2. 四个步骤
      1. 初始标记
      2. 并发标记
      3. 重新标记
      4. 并发清除
   3. 存在‘浮动垃圾’
      1. 浮动垃圾：CMS的GC线程与用户线程同时工作，所以GC的同时会有新的垃圾产生，只能等到下次GC再次清理
   4. G1 收集器
      1. G1 Garbage Frist收集器
      2. 采用分区的方式进行垃圾回收

## JDK8默认的垃圾收集器

1. 使用`java -XX:+PrintCommandLineFlags`查看回显-XX:+UseParallelGC

## 内存分配与回收策略

1. 优先分配到Eden区
   1. 大多数情况下对象在新生代的Eden区分配，当Eden区没有足够的空间，就进行一次Minor GC
   2. 新生代 Eden 与 s0 s1 的默认分配比例是 8:1:1
   3. 通过-Xmn设置新生代的大小
   4. -XX:+SurvivorRatio==8指定Eden与Survivor的比例
2. 大对象直接分配到老年代
   1. 占用大量连续的内存空间的对象称之为大对象
   2. 超过- XX:PretenureSizeThreshold设置的值就会直接分配到老年代
3. 长期存活的对象将进入老年代
   1. 在对象头中有GC分代年龄标识
   2. 每经过一次minorGC并转移到Survivor区存活下来年龄就+1
   3. 当超过年龄限制（默认是15）就会转移到老年代
   4. -XX:MaxTenuringThreadhold=15设置分代年龄
4. 动态对象年龄判断
   1. 如果Survivor中所有年龄相同的对象大小之和超过Survivor内存空间的一半就会转移到老年代
5. 空间分配担保
   1. 在发生MinorGC之前，JVM会先检查老年代最大可用的连续空间是否是大于新生代所有对象的内存大小之和
   2. 避免极端情况下新生代的所有对象都需要转移到老年代



### 项目中如何排查JVM的问题

1. 项目baking阶段
   1. 
2. 已经发生了OOM的情况
   1. 先增加点内存确定是不是内存设置的太小
   2. 

### JVM 参数

-XX:AutoBoxCacheMax=N Integer类型缓存值的大小

-XX:+PrintGCDetails 打印GC的详细信息

-XX:+HeapDumpOnOutOfMemoryError 发生OOM时候生成dump文件

# Spring 面试题

## 什么是IoC

1. IoC，控制反转，将对象的实例化操作交给了容器（Spring）
2. 避免了太多的new代码和赋值操作
3. DI（依赖注入只是实现IoC的一种方式）

## Spring 容器的启动流程

1. 

## Spring的循环依赖

1. Spring的循环依赖是指两个以上都没有创建的Bean互相依赖，在创建的过程中就会出现循环依赖

## 单例模式和单例Bean

1. 单例模式是指在JVM中只存在这个类的一个实例
2. 单例Bean是在Spring容器只存在这个类一个Bean

## Spring中的事物是如何实现的

1. Spring中事务是基于AOP和数据库的事物实现的
2. 对于使用了@Transation注解的Bean，Spring会使用cglib动态代理生成一个代理Bean
3. 

## Spring 的事物传播机制

1. 

## Spring事物什么时候会失效

## Spring Bean的生命周期

## Spring Bean是线程安全的吗

1. Bean的本质还是Java的类
2. Bean时候是线程安全的主要看Bean提供的一些方法操纵是不是线程安全的
3. Bean的作用域与线程安全没有关系

## ApplicationContext 和 BeanFactory有什么区别

1. ApplicationContext
2. BeanFactory

## Spring中使用到的设计模式

## SpringBoot 如何启动Tomacat的

1. 

## SpringBoot的配置文件加载顺序

## #{} 和${} 的区别



# MySQL

## MySQL的三范式

1. 1NF，表中的每一列都不不可分割的，都是原子性的
2. 2NF，在满足第一范式的基础上，每一列都是完整的依赖于主键列，不能依赖于主键的一部分
3. 3NF，在满足第二范式的基础上，非主键列只能依赖于主键列，不能依赖于非主键列

## MySQL的引擎

1. Innodb，
   1. 支持事务
   2. 支持外键
   3. 支持行锁
   4. v5.5之后MySQL的默认存储引擎
2. MyISAM
   1. ISAM Indexed Sequential Access Method 有索引的循序访问方法
   2. 不支持事务
   3. 不支持索引
   4. 支持表锁
3. Memory
   1. 基友内存的索引

## 索引的基本原理

1. 索引是一种数据结构
2. 数据库索引是数据库管理系统中一个排序后的一个数据结构，可以协助快速查询，更新表中数据
3. 通常使用B树或者B+树实现
4. 索引类似于目录，通过对内容建立索引形成目录，索引是一个文件，需要占用物理空间的

## 索引有哪些优缺点

1. 优点
   1. 可以加快数据的查找速度
2. 缺点
   1. 增大了维护成本，索引需要经过业务需求的分析最终确定如何建立索引
   2. 占用存储空间

## 索引有哪些类型

1. 主键索引
   1. 主键索引的列具有唯一性，不能重复
   2. 主键索引的列不能为null
   3. 一张表只有一个字段是主键
2. 唯一索引 
   1. 数据列的值是唯一的
   2. 可以有null值
   3. 一张表可以有多个唯一索引
3. 普通索引
   1. 可以为null，可以重复，没有限制
4. 全文索引

## MySQL中有几种锁

1. 表锁：锁的对象是整张表，在表锁定的期间其他事务不能访问，表锁响应的是非索引字段查询，即全表查询
2. 行锁：行锁响应的是主键，因为Innodb，行的数据会存储在聚簇索引上的

## 乐观锁 被关锁

1. 乐观锁认为不会并发的修改数据，默认不会上锁，只有在更新操作的时候才会上锁
   1. 采用CAS方式 Compare And Swap，容易产生ABA问题
   2. 版本号机制
2. 悲观锁认为，无论什么时候操作都会发生并发问题，所以操作的时候会加上锁

## MVCC 多版本并发控制

## 脏读 幻读 不可重复读

1. 脏读，B事务能读到A事务中修改还没提交的数据，如果A事务回滚了，那么B事务就产生了脏读
2. 幻读，在一个事务中，多次select的结果数目不一样
   1. A事务第一次select结果10，但是B事务在期间insert了5条并提交事务，A事务第二次select的结果就是15了
3. 不可重复读，在一个事务中多次读取同一条数据，读取的结果不一致
   1. 在A事务中，第一读取了值为8000，然后B事务修改了值为5000并提交事务，A事务再次读取的事务，就会发生2次读取的结果不一样

## Innodb的隔离级别

1. read uncommit：读未提交
   1. B事务能读到A事务的已经修改但是还没提交的数据
   2. 产生脏读，幻读，不可重复读
2. read commited: 读提交
   1. B事务能读到A事务已经提交的数据
   2. 产生幻读，不可重复读
3. read repeated: 可重复读
   1. 在一个事务内对同一个数据的读取，每次读取的结果都与第一次是一样的
   2. 产生幻读
4. serializable: 串行化
   1. 事务只能一个一个的去执行，串行，是最安全的，但是效率是最低的

## char varchar text

1. char 是定长的，不论字符串的长度为多少都会按照预定的长度算，超过最大长度会报错
2. varchar 是不定场的，按照字符串的实际长度算，超过最大长度会报错
3. text 系统自动计算长度，由于不确定性，所以建立索引的时候需要指定长度

## 超键 后选键 主键 外键

1. 超键：在关系中能唯一标识一条数据的属性集合称之为超键
   1. 比如学号能唯一标识一个学生，那么学号就是超键
   2. 但是姓名（假设没有重名）+班级+性别 也能确定一个学生，那么 姓名（假设没有重名）+班级+性别 这三个字段也称之为超键
2. 候选键：不含多于属性的超键称之为候选键，也就是只有一个字段的超键
   1. 学号就是一个超键，姓名（假设没有重名）+班级+性别 就不是
3. 主键：最终选择作为该关系的唯一标识的元组，就是主键
   1. 最后选择了哪个候选键作为唯一标识的主键，那个键就是主键
4. 外键：两张表之间，A的主键存在于B表中，那么这个字段就是B的外键

## 联合索引

1. 联合索引是指多个字段联合组成的索引
2. 联合索引瞒足最左匹配原则
3. (A,B,C)为联合索引，where A="",B="",C=""   where A="",B="" where A=""  会走索引
4. (A,B,C)为联合索引，where A="",C=""，不满足左匹配原则，发生索引中断
5. (A,B,C)为联合索引，where C="",B="",A=""，where C="",A="" 满足左匹配原则，会走索引

## 聚簇索引 非聚簇索引

1. 聚簇索引，索引的叶子叶子结点上存储着索引和当前行的数据
   1. 一般是以主键为聚簇索引
   2. 如果没有设置主键，就以不为null的唯一索引为聚簇索引
   3. 如果还没，Innodb，会自己建立一个隐藏的聚簇索引
2. 非聚簇索引，索引的叶子结点上存储的是当前索引和聚簇索引，会产生回表查询，也叫二级索引

## 什么是回表查询

1. 回表查询，通过非聚簇索引查询得到聚簇索引，然后再根据聚簇索引查询得到数据，这个过程称之为聚簇索引
2. 解决回表查询的方法是，索引覆盖

## 索引覆盖

1. 索引覆盖就是查询的字段信息，正好都在索引上，直接能拿到想要的数据，就不需要进行回表查询了
2. select name,sex from student where name='zhangsan'，发生回表查询，因为name字段上没有 sex的数据
3. 如果(name,sex)为联合索引，就不会发生回表查询，索引覆盖了

## 临时表

1. 临时表是数据库中是一种特需的表，用来存储查询的中间结果，临时随着连接的断开而销毁

2. 临时表具有连接隔离性，不同连接可以创建同名的临时表

3. 临时表分为2种

   1. 内存临时表，需要存储引擎是memory，速度快，但是占用内存
   2. 磁盘临时表

4. 产生临时表的情况

   1. 使用了union查询
   2. distinct查询，并且加上group by

5. 临时表是可以建立索引的

6. ```SQl
   --创建临时表
   create temporary table <tablename>
   (
     ...
   );
   ```

## 视图

1. 视图是以查询语句为纽带与表建立的一种特需关系的结构，视图是用来简化复杂查询的

2. 如果视图中的字段与表中的字段不是一一对应的，那么视图就只能用来查询

3. 如果建立视图的查询语句字段含有索引字段，那么视图就可以通过索引查询

4. 优点：简化复杂的查询，不存储数据，不占用存储空间

5. 缺点：添加了维护成本

   ```SQL
   -- 创建视图
   create [or replace] view <viewname>
   [(字段列表)]
   as 查询语句;	
   
   -- 修改视图
   alter view <viewname>
   as 查询语句;
   
   -- 查看视图
   describe <viewname>
   ```

   

## 临时表与视图的区别

1. 作用范围不同
   1. 临时表是基于基于连接的，在连接过程中会占用存储（内存还是磁盘取决使用的类别），连接断开就会销毁
   2. 视图是基于查询语句建立的，是多个连接共享的，用来简化复杂查询，过程期间不存储数据

## SQL优化经验

1. 使用精准的字段
   1. 建立主键
   2. 对于能确定的列使用，精准的类型，减少存储空间，利用查询
   3. 合理的建立索引
      1. 对于查询频率高的字段建立索引
      2. 对于联合索引，要将查询频率最高的放在最左侧，等值查询的放在最左侧
      3. 字段设计尽量加上非空约束（Not Null），减少空值判断
      4. 使用like 关键字的时候 只有'**%'才会走索引
   4. 对于复杂的SQL使用explain进行查询计划分析
   5. 分库分表

## 分库分表

1. 垂直分库分表
   1. 垂直分库分表是基于业务上的操作
   2. 垂直分表，将一张大表分成小表，按照查询频率分成不同的表
   3. 垂直分库，将数据库按照不同模块分成多个数据库，只有用到这个模块的时候才连接这个数据库进行操作，相当于对数据库进行了流量拆分
2. 水平分库分表
   1. 水平分库分表是数量级上的
   2. 水平分表，将数据量比较大的表按照一定的规则将数据迁移到另外一张相同结构的新表中
   3. 水平分裤，按照一定的规则，将数据库中的数据拆分出去，存储到另外一个数据库中
3. 分库分表需要在设计阶段完成，在代码中使用使用正则等一定规则的方式去访问数据库和表

## MySQL的日志类型

1. 通用查询日志
   1. 默认是关闭的，需要手动开启
   2. 开启后记录数据库的每个操作
2. 慢SQL日志
   1. 记录数据库中操作比较慢的日志
   2. 通过限制的时间和行数来确定是否是慢SQL
3. 错误日志
   1. MySQL服务本身运行出现异常的日志
4. 二进制日志 bin log
   1. 进行MySQL更新操作的日志
   2. 与relay log配合进行主从数据同步
5. 中继日志 relay log
   1. 从服务上读取主服务上的bin log数据，并存储到relay log
6. 回滚日志 undo log
   1. 记录数据的事务，可通过此日志文件进行事务回滚
   2. 保障其他事务读取到当前事务对这条数据更改之前的值，确保其他事务不受这个事务的影响
7. 重做日志 redo log
   1. MySQL为了保障数据的读取效率，并不会把每次都把数据写到磁盘上，而是将数数据先保存到内存上，积累到一定的程度然后在写到磁盘上，这样带来的问题就是，当MySQL的服务器出现宕机的时候会丢失数据，这个时候就可以从redo log中得到还未写入到磁盘上的操作，更新到磁盘上，保证数据的完整性

## MySQL的主从同步



# Redis

## Redis的数据类型和应用场景

1. 字符串 String
   1. String 的最大值是512M
   2. 通常用来保存session id，计数
2. 列表 List
   1. Reidis List是有序的
   2. Redis List 支持从两端插入（push）和弹出（pop）数据，所以可以用来当作对列
3. 哈希 Hash
   1. hash是key-value结构的，用来存储对象
4. 集合 Set
   1. Redis Set是无序且不重复的数据类型
   2. 可以用来实现收藏夹（收藏的东西是唯一的）
   3. 共同好友，因为set提供交集，差集计算
5. 有序集合 zset
   1. zset是有序不重复集合，会根据分值进行排序
   2. 通常用来做排行榜
   3. 做有权重的队列

## 什么是RDB和AOF

1. RDB， Redis Database 通过快照的方式将指定间隔内的Redis内存中的数据写入到磁盘文件上

   1. BGSAVE命令开始一个子进程，现将数据写入临时文件，写入成功后在替换原来的文件

   2. 优点

      1. 只有dump.rdb文件方便备份恢复
      2. 性能最大化，通过BGSAVE开启子进程来进行持久化，不会阻塞主进程的IO操作
      3. 数据量比较大的时候，比AOF启动效率更高

   3. 缺点

   4. 可能会丢失数据，RDB是间隔一段时间进行持久化的，如果两次之间redis发生故障，数据会丢失

   5. RDB是通过fork子进程来完成数据持久化的，当数据集比较大时，可能会导致整个服务器停止几百毫秒

   6. 配置

      ```conf
      save 60 1000 // 60秒之内有1000次写入操作就触发BGSAVE命令，进行RDB备份
      stop-writes-on-bgsave-error yes 创建快照失败后是否继续执行写命令
      rdbcompression yes 是否对快照文件进行压缩
      dbfilename dump.rdb rdb文件名称
      dir rdb文件路径
      ```

2. AOF，Append Only File，以日志的形式，记录Redis Server所处理的每一写操作和删除操作，查询操作不会记录

   1. 优点
      1. 数据安全，Redis提供了3种同步策略，每秒同步，每修改同步，和 不同步
         1. 每秒同步，异步完成，每秒同步一次，即使故障也只会丢失一次
         2. 每修改同步，同步机制完成，每修改就同步
         3. 不同步，有系统决定什么时候同步
      2. 中途宕机不会影响已经存在的AOF文件
      3. 可以通过refis-check-aof解决数据一致性问题
      4. 通过AOF rewrite模式，定期对AOF文件进行重写，以达到压缩目的AOF文件大小的目的
   2. 缺点
      1. AOF文件比RDB文件大，恢复速度慢
      2. 数据量大的时候，启动效率比AOF低
      3. 运行效率没有RDB高

## Redis的持久化机制

1. RDB
2. AOF
3. 默认是RDB
4. 同时开启RDB和AOF会使用AOF

## Redis过期键的删除策略

1. 惰性过期
   1. 当访问一个key的时候，才会去判断key是否过期，过期则清除，占用内存
2. 定期过期
   1. 每隔一定的时间就去扫描一定expires字典中一定数量的key，并清除其中已经过期的key，对CPU不友好，占用CPU时间
3. 定时过期（redis没用到）
   1. 创建过期键的时候，同时创建一个定时器，进行管理

## flushall 和 flushdb的区别

1. flushall 清空所有db(0-15)内存数据并进行持久化
2. flushdb 清空当前db的内存数据，并不会立即进行持久化，但是等触发bgsave还还是会持久化的

## Redis事务的实现方式

1. redis事务是将多个命令请求打包，然后一次性按顺序的执行的一种机制
2. redis会等事务执行完成后才会去执行其他客户端的命令请求
3. 事务的实现
   1. 事务开启，通过multi关键字打开REDIS_MULTI标识
   2. 命令入队，redis会将非 multi watch exec discard 的命令缓存到队列中，否则就立即执行
   3. 事务执行，exec命令开始执行事务，按照队列的先进先出的命令开始执行
      1. Watch 命令用于监测任意数量的key，如果在exec执行的时候，发现被watch的key发生了改动，那么事务将被拒绝执行，并将结果返回到客户端
      2. discard 命令放弃事务，不执行了
4. redis的事务不支持回滚，要么执行，要么不执行

## redis的watch机制

1. watch 命令不能在multi中执行

2. watch的字段如果在事务exec的时候发生改动，那么事务就不会执行，并返回nil

   ```shell
   # 操作之间key username hello的value
   127.0.0.1:6379> get username
   "zhangsan"
   127.0.0.1:6379> get hello
   "redis"
   127.0.0.1:6379> 
   127.0.0.1:6379> 
   ## watch username hello
   127.0.0.1:6379> watch username hello
   OK
   ## 开始事务，并对key username hello重新赋值
   127.0.0.1:6379> multi
   OK
   127.0.0.1:6379(TX)> set username lisi
   QUEUED
   127.0.0.1:6379(TX)> set hello java
   QUEUED
   ##执行事务，发现key username有改动，终止事务返回nil
   127.0.0.1:6379(TX)> exec
   (nil)
   ## 验证key username hello 的value，并没有被修改
   127.0.0.1:6379> get username
   "wangwu"
   127.0.0.1:6379> get hello
   "redis"
   127.0.0.1:6379> 
   ```

   3. redis每个db中有一个watch dict来维护watch的信息

## Redis是单进程单线程，单线程为什么那么快

1. redis所说的单线程是指redis的键值对的读写是一个线程来完成的
2. 持久化，异步删除，集群同步都是采用其他线程执行的
3. redis操作的数据都在内存之中，使用一个线程避免了多个线程之间CPU上下文切换和竞争资源之间保护问题的开销
4. redis采用的是IO多路复用的机制，一个线程监听多个文件事件

## Redis的分布式锁是如何实现的

1. 通过setnx命名来实现
   1. setnx，set if not exist 如果key不存在就设置value,返回1，如果存在就不设置，返回0
   2. setnx，单个命令在redis中是原子性的，不会有并发问题
   3. 通过删除key来释放锁
   4. 存在的问题，如果删除锁失败，锁就会被一直占有，所以需要加上过期时间
   5. 先通过setnx，再通过expire 设置key的过期时间，此过程非原子性的，可通过lua脚本保证原子性，Redssion已经实现
   6. 通过setnx+expire产生的问题
      1. 锁过期
         1. 锁的过期时间小于业务实际的处理时间，导致业务还在处理，锁已经被释放了
         2. 通‘看门狗机制’，开始一个守护线程，对过期时间计时，在即将过时，业务还没处理好的时候，自动续时,Redssion实现了
      2. 释放其他服务的锁
         1. 锁超时带来的衍生问题，因为锁提前自动释放了，可能被其他服务获取到锁，当业务真正执行结束的时候释放锁的时候，就释放了其他业务的锁
         2. setnx key value 的时候，对value的值，加上业务的唯一标识，在删除的时候，先get value查看是否本业务的，在进行删除，此过程非原子性，可通过lua脚本实现

## 缓存穿透 缓存击穿 缓存雪崩的含义

1. 缓存穿透，缓存中不存在，直接访问数据库
   1. 恶意攻击，发起没有的请求，对参数进行校验
   2. 对查询不到的数据，也放到缓存中，value=null(不推荐，会占用大量的内存)
   3. 使用布隆过滤器进行过滤
2. 缓存击穿，某个key过期，直接访问数据库
   1. 这个key是否有设置过期时间的必要
3. 缓存雪崩，某个时间，大量的热点数据key同时过期，压力直接到数据库
   1. 对每个key的过期时间加上随机数，分散过期时间

## 如何保证数据库与缓存的数据一致

1. 更新的时候，先更新数据库再更新缓存，如果redis更新失败，仍存在不一致的问题
2. 先删除再更新，每次先删除缓存中的数据，在更新数据库，这样第二次查询的时候，就会重新加载数据到缓存
   1. 数据操作比较频繁的时候，性能比较低
   2. 多线程操作的时候，会产生数据不一致
3. 延迟双删（闪电缓存）
   1. 先删除缓存再更新数据库，延迟N ms后再删除缓存数据

## Redis回收策略

1. 当redis的内存满了会触发回收策略
2. 回收策略，lru，ttl，random
   1. volatile-lru：从已经设置过期时间的数据中淘汰最近最少使用的数据
   2. volatile-ttl：从已经设置过期时间的数据中淘汰将要过期的数据
   3. volatile-random：从设置了过期时间的数据中，随机淘汰数据
   4. allkeys-lru：从所有数据中淘汰最近最少使用的数据
   5. allkeys-random：从所有数据中随机淘汰
   6. no-enviction: 进制驱逐数据

## Redis内存满了怎么办

1. redis内存满了，首先如果内存淘汰策略为 no-enviction，redis写操作会无法成功，读操作不影响
2. 增加可用内存，默认情况下redis不限制可用内存大小，可通过redis.conf->maxmemory设置
3. Redis会跟内存淘汰策略自身淘汰数据，释放内存空间

## Redis hash槽

1. redis有16384个hash槽，每个key对16384进行取模，决定存放的位置
2. 集群的每个节点负责一部分hash槽

## Redis主从复制

1. 通过replicaof <host> <port> masterauth masteruser 将一台redis服务连上主服务器，成为一台从服务器
2. slave连接上master之后，向master发送sync命令
3. master接收到sync后，执行bgsave命令，生成快照
4. slave 根据replica-serve-stale-data yes来决定在同步过程中是正常响应客户端请求还是返回 ‘SYNC with master in progress’
5. master bgsave 生成快照之后，开始向slave发送快照，此过程中使用缓冲区来记录写命令
6. slave开始接收快照，接受master的快照文件之前先丢弃自己原来的数据
7. master发送完快照文件后，开始向slave同步缓冲区的写命令
8. slave接受完master快照，并解析加载到内存中，开始接受读请求
9. salve 接收maser缓冲区的命令
10. master salve 开始正常的数据同步
11. 优点：读写分离，减轻负载，数据多机备份
12. 缺点：redis的数据容量大小还是取决master单机的大小，数据量并没有平分，无法故障转移

## Redis哨兵机制

1. redis的哨兵机制用来实现master的自动故障转移，但是仍然只有一个主节点用来写
2. 哨兵的作用，监控 选举 通知
   1. 监控：哨兵会向集群中的master和salve节点发送ping命令，如果超过了down-after-milliseconds 的值，则哨兵认为此节点下线（主观下线），此过程可能会出现误判，比如网络的延迟，所以需要多个哨兵（超过一半的哨兵节点（N/2+1））都判定主观下线，那么这个节点就会被客观下线
   2. 选举
      1. 在master节点被客观下线后，哨兵就需要开始选举新的master，通过打分机制在剩下的salve节点中，选择得分最高的选举为master，并通知其他salve节点（类似于webhook)，开始同步新的master的数据，通知应用程序使用新的master IP
      2. 选举得分机制
         1. 根据设置的优先级选择，slave-priority值的高优先选择为master
         2. 如果优先级一样，选择根原master同步进度最高的为slave(丢失的数据最少)
         3. ID号最小，如果优先级和同步进度一样，默认选择ID号最小的为master
   3. 通知，master节点发生改变后，哨兵会通知salve节点开始同步新的master，修改了replicaof的配置

## Redis集群

1. 采用无中心节点的方式实现，将数据分布在不同的节点上存储
2. 每个集群中有多个节点，每个节点中存储中其他节点的信息
3. 通过hash 槽将16384个槽位分部到不同的节点上，根据key的hash对16384进行取模也可以通过 CLUSTER ADDSLOTS <slot> [slot...]指定
4. 每个节点也可以是 主从复制结构的



# RabbitMQ

1. 