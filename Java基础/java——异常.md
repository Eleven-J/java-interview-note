##### 1. 异常在java中以类的形式存在，每个异常类都可以创建异常对象。

##### 2. 当程序出现异常时，会new一个对应的异常对象，并把这个异常对象打印到控制台上。

##### 3. 异常类的继承结构关系：

【所有异常（包括编译时异常和运行时异常）都发生在运行阶段】

> **Object;**
>
> > **Throwable;**(可抛出的异常)
>
> > > **Error**(不可处理，直接退出JVM);  
> > >
> > > **Exception**(可处理)
> > >
> > > > **Exception的直接子类：**编译时异常(要求在编写程序时必须对这些异常进行处理，否则编译器报错。集成环境idea会标红)
> > > >
> > > > **RuntimeException:运行时异常：**（在编写程序阶段程序员可以处理，也可以不处理）

##### 4. java处理异常有两种机制：

> - Throw: 将异常抛给调用它（出现异常的java语句）的那一级
>
> - Try...Catch... : 捕获异常，并进行处理。

```java
/*
程序执行到此处发生ArithmeticException异常，底层new了-个ArithmeticException异常对象，然后抛出了，由于是main方法调用了100/0，所以这个异常ArithmeticException抛给了main方法，main方法没有处理，将这个异常自动抛给了JVM。JVM最终终止程序的执行。
ArithmeticException继承RuntimeException，属于运行时异常。在编写程序阶段不需要对这种异常进行预先的处理。
*/
public static void main(String[] args){ 
  //main方法不用使用throws，发生异常会自动上报给JVM——>JVM终止。所以main方法中一般用try...catch捕捉异常，提高程序健壮性。
  System.out.println(100/0);
	System.out.println("hello world")
//这里的Helloworld没有输出，没有执行律System.out.println("Hello World!");
}
```

```java
public class Test(){
  //main方法
  public static void main(String[] args){
    try{                            // 这里会捕捉到来自m1()抛上来的异常。
      m1();
    }catch(FileNotFoundException e){// e是一个引用，保存的是FileNotFoundException异常对象的内存地址
      e.printStackTrace()// 打印异常堆栈追踪信息
      System.out.println("文件不存在！！！")
    } 
    finally{
      System.out.println("finally中的语句一定会执行，无论是否出现异常")//即使try或catch中出现return，执行到return时也会             					                                                        //自动先把finally中的语句执行完再return
    }
  }
 //m1()方法
  public void m1() throws FileNotFoundException{ //如果发成异常，throws会将该异常向调用该方法的目标抛出
    new FileInputStream("/Users/jackiez/Downloads/Surfboard.conf")//如果没有这个文件名或路径，就会抛出异常。
    
  }
}


```

##### 5. 自定义异常在java中的应用：

- 第一、按自己需求新建一个异常类xxx

- 第二、在要发生异常的地方新建一个异常对象并把它抛出。`throw new xxx`

  (jdk自带的异常也是这种机制)

- `throw`与`throws`: throw是手动抛异常的关键字，throws是方法上抛的关键字，别搞混。

