##   java——数据类型

1. ##### java语言中，整数默认为 ***int型***（4字节），小数默认为***Double*型**，例：

   ```java
   """错误示例"""
   float a = 3.14;  //3.14默认为double型，double型赋值给float型会出现数据损失，因此报错
   """正确示例"""
   float a = float(3.14);  //强制转换
   
   //123333333333默认为int型，但是它超出了int表示范围（溢出），所以需要在后面加上L，告诉系统它是long
   long b = 123333333333L; 
   ```

2. ##### 在某些情况下，java可实现自动数据类型转换

   ```java
   short c = 128;  //128本来默认为int类型，但是128在short范围内，所以可自动转换
   byte d = 56;  //原理同上
   ```

3. ##### 引用以及java内存情况（引用在c++中其实就是指针）

   ![对象引用内存图](/Users/jackiez/学海/Java开发笔记/picture/对象引用内存图.png)
   

##### 4. 包装数据类型（Integer, Character, Byte，Short, Long, Boolean, Float, Double）

> 自动装箱与拆箱：
>
> ```java
> Integer x = 100;//基本数据类型int——>包装数据类型Integer
> int y = x;//包装数据类型——>基本数据类型
> System.out.println(x + 1)//这里会进行自动拆箱操作，转换成基本数据类型，再加1
> ```

> ```java
> Integer a = 1000;  //自动装箱，相当于 Integer a = new Integer(1000),a是个引用，指向对应对象的内存地址
> Integer b = 1000;  //自动装箱，相当于 Integer b = new Integer(1000),b是个引用，指向对应对象的内存地址
> System.out.println(a == b)//flase,只有“+-*/”运算是会触发自动转型，“==”不会自动转型，所以此时比较的是两个对象的内存地址
> //注：当a和b在[-128~127]事，上述打印输出为true
> /*java中为了提高程序的执行效率，将【-128到127】之间所有的包装对象提前创建好，放到了一个方法区的“整数型常量池”当中了，目的是只要用这个区间的数据不需要再new了，直接从整数型常量池当中取出来。
> 原理：x变量中保存的对象的内存地址和y变量中保存的对象的内存地址是一样的。*/
> ```
>
> ![image-20210115232228285](/Users/jackiez/学海/Java开发笔记/picture/包装类的内存空间.png)

##### 5. Integer、int和String之间的转换

```java
//String——>int
int i1 = Integer.parseInt("100");//i1是数字100
System.out.println(i1 + 1);//101，数字相加
//int——>String
String s2 = i1 + "";//字符串拼接，i1被自动转成字符串和""拼接
//int——>Integer
Integer x = 1000;//自动装箱
//Integer——>int
int y = x;//自动拆箱
//String——>Integer
Integer k = Integer.valueOf("123");
//Integer——>String
String e = String.valueOf(k);
```

![image-20210116000011762](/Users/jackiez/学海/Java开发笔记/picture/Integer和int和String的转换关系.png)

##### 6. 数字xx（二进制）右移一位相当于“xx/2” , 左移一位相当于“xx*2”(两倍)。