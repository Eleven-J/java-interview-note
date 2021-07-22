##### 1. java中知支持单继承，不支持多继承（c++）。支持间接继承，如：A继承B, B继承C，则A间接继承C。

##### 2. 子类继承父类，除构造方法外，其余都可以继承，但是私有的属性无法在子类中直接访问。

##### 3. "System.out.println( )"语句分析：

```java
		System是jdk中写好的类（可在jdk中的src.zip中查看），out是System类中的静态变量，该静态变量是一个对象，println( )就是这个对象的方法。
  	System.out.println( 引用 )：默认调用toString方法，输出为：“该引用的类”@“该引用在堆内存中的地址”
```

##### 4. super与this

- super：**super不是引用**，super也不保存内存地址，也不指向任何对象，它只代表当前对象的那一块父类型的特征。
- super( )与this( ):

   ```java
   //this()和super()不能共存，他们都只能出现在构造方法第一行
   //super()：通过子类的构造方法调用父类的构造方法
   //结论1：当一个构造方法第一行既没有this()也没有super()时，默认隐式会有一个super();表示通过当前子类的构造方法调用父类的无参数构造方法。所以必须保证父类的无参数构造方法时存在的————这也是为什么建议最好显式写出类的无参数构造方法。
   //结论2:无论如何，在创建子类对象时，父类的构造方法一定会执行，但是执行父类众多构造方法中哪一个构造方法取决于this()或super()
   public class SuperTest {
       public static void main(String[] args) {
           B b = new B();
       }
   }
   
   class A{
       public A(){
           System.out.println("A类的无参数构造方法");
       }
       public A(int i){
           //super();
           System.out.println("A类的有参数构造方法");
       }
   }
   
   class B extends A{
       public B(){
           this("Jack"); //调用该类的有参数构造方法public B(String name){ }
           //super(100);   调用父类中的有参数构造方法,this和super两者只有其中一个能出现在构造方法第一行
           System.out.println("B类的无参数构造方法");
       }
       public B(String name){
           //super();//默认有这一行代码，未显示
           System.out.println("B类的有参数构造方法");
       }
   }
   ```

- “super. ”与“this. ":  

> super.name: 当前对象的父类型特征中的name属性
>
> this.name: 当前对象的name属性。

​		所以，两者在大多数情况下可以省略，如下特殊情况不能省略：

​        当子类中也出现name属性（父类中也有name属性，“java是允许父类和子类具有相同名字的特征”），此时需要用super.name和this.name来区分，直接写name则默认为this.name。（即此时要访问父类的name属性，则super不能省略）













