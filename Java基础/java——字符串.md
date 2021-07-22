##### 1. 字符串存在方法区的字符串常量池中，双引号括起来的字符串如“abc”自出生到死亡都是不可变的。

```java
//如常量池已存在“xy”，再新建“xy”的对象或者调用“xy”，都无需再常量池中新建，它默认会自动检索到已存在的“xy”
String s1 = "abcdef";
String s2 = "abcdef" + "xy";
String s3 = new String("xy")//new方法产生的对象都存在堆内存中（这是法则）
```

![image-20210115094634230](/Users/jackiez/学海/Java开发笔记/picture/字符串内存图.png)

##### 2. 字符串的比较

```java
String s1 = "hello";
String s2 = "hello";
System.out.println(s1 == s2);//Ture,因为s2不会再在方法区新建一个“hello”对象，而是直接指向已有的“hello”对象。
String s3 = new String("xyz");//在堆内存中新建一个String对象。
String s4 = new String("xyz");//在堆内存中新建另一个String对象。
Soutem.out.println(s3 == s4);//False，因为它比较的是堆内存中两个String对象的内存地址。

```

##### 3. 打印在控制台上的信息都是字符串形式，都调用了String.valueOf().

##### 4. String  vs  StringBuffer

> **StringBuffer**: 底层实现是byte[ ]（无final），可扩展，涉及到字符串拼接、扩容、追加的情况，尽量用StringBuffer，节省内存空间。扩容具体过程：*新建一个更大的字符串对象，将字符串copy过去，在添加当前需要添加的字符串内容，最后垃圾回收器回收原字符串对象内存空间。*StringBuffer使用方法：
>
> ```java
> StringBuffer stringBuffer = new StringBuffer(N);//默认初始化容量为16，可人为初始化值N。
> stringBuffer.append("abc");
> ```
>
> **String**: 底层实现是final byte[ ]，一旦初始化就不能更改