##### 1. 同一个进程中的不同线程：各自的栈内存空间独立，各自的堆内存和方法区共享。

##### 2. 创建线程并执行(建议使用第二种方式，若需要获取线程的执行结果可使用第三种方式)：

- 第一种方式：新建一个类并继承java.lang.Thread，重写run( )方法：

```java
public class Test6 {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();//创建线程对象
        //myThread.run();   //.run()方法相当于调用线程myThread里的程序，执行完再顺序执行main栈里的程序，并没有开发出分支栈。
        myThread.start();   //.start()方法执行后会开发出分支栈，MyThread里写的程序会以线程的形式与main栈并行执行。
        
    }
}
//定义线程类
class MyThread extends Thread{
    @Override
    public void run() {
        //这里写分支线程的程序
    }
}
```

- 第二种方式：编写一个类实现java.lang.Runnable接口，实现run方法。**（推荐）**

```java
public class Test6 {
    public static void main(String[] args) {
       Thread t = new Thread(new MyRunnable());
       t.start();
    }
}
class MyRunnable implements Runnable{

    @Override
    public void run() {
        //这里写分支线程的程序
    }
}
/**************************可用匿名内部类简化上述代码*****************/
    public static void main(String[] args) {
       Thread t = new Thread(new Runnable() {     //Runnable是一个接口
           @Override
           public void run() {
               //这里写分支线程的线程
           }
       });
       t.start();
    }
```

- 第三种方式：实现Callable接口（优点：可以获取到线程的执行结果）

  ```java
  public class Test7 {
      public static void main(String[] args) {
          //FutureTask构造函数需要一个Callable参数，这里使用匿名内部类方式创建对象
          FutureTask task = new FutureTask(new Callable<Integer>() {
              @Override
              //这里的call()方法相当于run方法，只不过这里有返回值（代表线程实行结果）
              public Integer call() throws Exception {
                  System.out.println("call method begin");
                  Thread.sleep(1000*5);
                  System.out.println("call method end");
                  int a = 100,b = 100;
                  return a + b; //自动装箱，返回Integer对象
              }
          });
          Thread t = new Thread(task);
          t.start();
          try {
              Object obj = task.get(); //在主线程mian中获取t线程的执行结果，note：这里会阻塞。
              System.out.println(obj);
          } catch (InterruptedException e) {
              e.printStackTrace();
          } catch (ExecutionException e) {
              e.printStackTrace();
          }
          System.out.println(Thread.currentThread().getName()+"——>"+"helloworld");
      }
  }
  ```

  

##### 3. 线程的生命周期

![线程生命周期图](/Users/jackiez/学海/Java开发笔记/picture/线程生命周期图-3924949.png)

##### 4. 获取当前线程对象：Thread currentThread = Thread.currentThread();

##### 5. 线程的睡眠与唤醒：

- 睡眠：`t.sleep(1000)`——>睡眠1000ms
- 唤醒：`t.interrupt()`——>依靠Try……Catch异常处理机制完成的
- 强行终止线程：`t.stop()`——>已过时（这种方法杀死线程可能会丢失数据）推荐使用flag方案如下：

```java
public class Test6 {
    public static void main(String[] args) {
        MyRunnable r = new MyRunnable();
        Thread t = new Thread(r);
        t.start();
        r.setRun(false);  //终止线程
    }
}
class MyRunnable implements Runnable{
    boolean run = true;

    public boolean isRun() {
        return run;
    }
    public void setRun(boolean run) {
        this.run = run;
    }

    @Override
    public void run() {
        if (run){
            //这里写分支线程的程序
        }else {
            //这里可以保存你需要保存的
            return;//到这里return线程就结束了，有什么需要在线程结束前保存的可以在return前保存。
        }

    }
}
```

##### 6. 线程调度

- 线程优先级：最低为1，最高为10，默认为5。线程优先级越大，大概率抢占到的时间片相对越多。

> `t.setPriority(10)`:设置线程优先级
>
> `t.getPriorty()`:获取线程优先级

- 线程让位：当前线程暂停，回到就绪状态，让给其他线程（自己有可能刚让出去又抢回来，但是概率很低）。

> `Thread.yield()`:该行代码所在的线程让位。

- 线程合并（协调）：

  > `t.join()`:假设`t.join()`这行代码在线程A中，A执行到这行代码时，A线程阻塞，等待`t`线程执行完，A再回到就绪状态。

##### 7. 线程同步机制

- 同步代码块——>`synchronized(共享对象){ }`代码块：传入的参数为所需要同步的线程的共享对象。`synchronized`获取并判断该对象的对象锁的状态，来决定是执行还是等待（相当于一种阻塞）。

- 在实例方法上添加`synchronized`关键字，如`public synchronized void xxx(){ }`，表示共享对象一定是`this`,且同步代码块是整个方法体
- 在静态方法上使用`synchronized`关键字，表示找类锁，类锁永远只有一把，就算创建了100个对象，也只有一把类锁。

- `synchronized`在开发中尽量不要嵌套使用，容易形成死锁，死锁调试起来很困难。

##### 8. 开发中如何选择合适的方案解决线程安全问题：
​		synchronized会让程序的执行效率降低，系统的用户吞吐量降低，用户体验差。在不得已的情况下再选择线程同步（`synchronized`）机制。

> **Fisrt方案：**尽量使用局部变量代替实例变量和静态变量。
> **Second方案：**如果必须是实例变量，那么可以考虑创建多个对象，这样实例变量的内存就不共享了。（一个线程对应1个对象，100个线程对应100个对象，对象不共享，就没有数据安全问题了。）
> **Third方案：**如果不能使用局部变量，对象也不能创建多个，这个时候就只能选择synchronized(线程同步机制)了。

##### 9. 线程分类：

> - 用户线程
>
> - 守护线程：一般是死循环，在后台运行着。在所有用户线程结束后，守护线程会自动结束。
>
>   > 将A线程设置为守护线程：在`A.start()`前执行`A.setDaemon(true)`

##### 10. 定时器：间隔特定的时间，执行特定的程序。

​		java类中已经写好了一个定时器：java.util.Timer。（目前开发中主要使用框架中的定时功能，如Spring框架提供的SpringTask框架，只要加以简单的配置，就可以实现定时器任务，不过它底层实现也是java.util.Timer）

##### 11. 生产与消费模式解读`o.wait()`与`o.notify()`方法：

- `o.wait()`：让活动正在o对象上的线程t进出等待状态，并且释放t线程之前占用的o对象锁。
- `o.notify()`：唤醒正在o对象上等待的线程，但不会释放被占用o对象的锁，与`o.wait()`配套使用。

![image-20210123230413725](/Users/jackiez/学海/Java开发笔记/picture/生产与消费模式.png)

12. sleep() 可能会抛出 InterruptedException，因为异常不能跨线程传播回 main() 中，因此必须在本地进行处理。线程 中抛出的其它异常也同样需要在本地进行处理。
