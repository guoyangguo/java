# JAVA Thread

## 线程的创建

1. 继承Thread
2. 实现Runnable
3. 实现Callable
   1. 有返回值
   2. 可以捕获异常

### 线程不一定立即执行，听从CPU的安排调度

### thread.run() thread.start()

1. Thread run 方法只是Thread类中的一个方法，在main线程中执行
2. Thread start 方法才会开始一个新的线程去执行代码，start底层是通过JNI调用的start0()

## 静态代理

 真实对象和代理对象都要实现同一个接口

将真实对象，交给代理对象去执行

好处：

代理对象可以代替真实对象在目标方法的执行前后实现不同的逻辑

真实对象只实现目标方法的逻辑

## Lambda表达式

为什么要有Lambda表达式

1. 避免匿名内部类定义过多
2. 去除无意义的代码，留下核心逻辑，代码起来更加的简洁

## 函数是接口

一个接口中只有一个方法，就是函数式接口

## 多线程的停止

使用外部标志位停止线程，不建议使用过时的stop destory

## sleep

线程休眠

Sleep 不会释放锁

## yield

线程礼让，当前线程让出cpu时间片，重新开始竞争cpu,有可能再次获取到cpu的时间片，所以yield不一定成功

## join

myThread.join();当前线程阻塞，优先执行myThread线程，等myThread线程执行结束后，才执行原来的线程，相当于插队

## 线程状态

- NEW
- RUNNABLE
- BLOCKED
- WATING
- TIMED_WAITING
- TREMINATED

线程只能启动一次；线程一旦TREMINATED，就不能再启动

### 性能倒置：优先级低的线程优先执行