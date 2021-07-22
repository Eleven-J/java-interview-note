##### 1. 方法覆盖：

      条件一：两个类必须要有继承关系
    
      条件二：充血之后的方法和之前的方法具有相同的返回值类型，相同的方法名，相同的形式参数列表。
    
      条件三：访问权限不能更低，可以更高，如：父类的方法关键字为protected，子类重写时关键字可以为public，反之则不行。
    
      条件四：重写之后的方法不能比之前的方法抛出更多的异常，只能更少或相等。

##### 2. 多态是指：多种形态，多种状态，编译和运行有两个不同的状态。

      多态的典型代码：父类型引用指向子类型对象，它包括编译阶段和运行阶段。
      		编译阶段：绑定父类的方法。
          运行阶段：动态绑定子类型对象的方法。多种形态。
      多态在开发中的作用：
      		降低程序的耦合度，提高程序的扩展力（面向父类编程）

##### 3.  向上转型、向下转型：

```java
  向上转型：子——>父    Animal a = new Cat()

  向下转型：父——>子    Cat c = (Cat)a ，需要调用或者执行子类对象中特有的方法时使用。向下转型容易出现ClassCastException类型转换异常，通常使用 instanceof 运算符提前进行判断。( 注意： instanceof 判断时，“本类”或“本类的父类”或“本类实现的接口”甚至“接口的父类接口”都可以通过)
```

##### 4. 接口与类的向上、向下转型分析：

- （父类A：a）——>（子类B：b）向下转型时，两者必须要有继承关系，否则编译器会报错。其次，运行时是否报ClassCastException类型转换异常，主要看a实际指向的是否为B。

  ```java
  /***前提条件：B extends A*****/
  //此情况，两者有继承关系，且在代码运行时a指向的是B类的对象，可成功编译且运行
      A a = new B()  //若A和B无继承关系，则编译器会报错
      B b = (B)a     //若运行时a指向的不是B类对象，则运行会报错——ClassCastException类型转换异常
  ```

- （接口A：a）——>（接口B：b）向下转型时，两者无须继承关系，编译器会通过。但是，运行时是否报ClassCastException类型转换异常，原理跟类的向下转型一样。

  

  

##### 4. 抽象类

![image-20210108104526042](/Users/jackiez/学海/Java开发笔记/picture/抽象类.png)

- 抽象类不能实例化，他是用来被继承的。

- 抽象类中不一定有抽象方法，抽象方法必须出现在抽象类中。

- 重要结论：一个非抽象的类继承抽象类，必须将抽象类中的抽象方法实现了。

  ```java
  abstract class Animal{
      public abstract void move();  // 抽象方法不能有方法体（即{ }）,且抽象方法只能出现在抽象类中。
  }
  
  class Bird{
      public void move(){           // 一定要有这个"方法重写"，因为Bird会继承Animal的抽象方法，但是Bird却不是抽象类。
  
      }
  }
  ```

- 抽象类作用：降低接口实现类与接口之间的实现难度。如：

  ```java
  /*Fruit.java*/
  public interface Fruit{
    public void eat();
    public void drink();
  }
  
  /*YichangFruit.java*/
  //抽象类中可以声明抽象方法，也可以生成具体方法
  //抽象类声明的抽象方法必须由子类进行重写
  //抽象类实现接口时，可以不对接口方法进行重写
  public abstract class YichangFruit implements Fruit{
    //此时YichangFruit只实现了Fruit的eat()方法，那么剩下的继承Fruit的方法就要靠Orange这个类来实现了
    public void eat(){
      //方法重写内容省略
    }
  }
  
  /*Orange.java*/
  //YichangFruit这个抽象类作为Orange和Fruit之间的桥梁，使得Orange不用实现Fruit接口中所有的方法。 如果Orange直接实现Fruit接口，则必须实现Orange全部的方法。
  public class Orange extends YichangFruit{
    public void drink(){
      //方法重写内容省略
    }
  }
  ```

  


##### 5. 接口：

- 接口也是一种引用数据类型"。编译之后也是一个class字节码文件。
- 接口是完全抽象的。（抽象类是半抽象。）或者也可以说接口是特殊的抽象类。
- 接口怎么定义，语法是什么？【修饰符列表】interface 接口名{ }
- 接口支持多继承，一个接口可以继承多个接口。本质上，类对接口的继承就是对该接口的实现。
- 接口中只包含两部分内容，一部分是：常量。一部分是：抽象方法。
- 接口中所有的元素都是public修饰的。（都是公开的)。
- 接口中的方法都是抽象方法，不能有方法体。
- 接口中的方法的public abstract可以省略；接口中的常量的publicstatic final可以省略。



​     



#### import、pakage与.java文件路径（文件结构树）是一个道理、同目录级的.java相互调用不需要imort