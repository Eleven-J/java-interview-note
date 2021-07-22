##### 1. 注解（annotation）：

- 主要在编译阶段起作用，可以帮助程序员在编写程序时少犯些低级错误

- 自定义注解代码实现：

  ```java
  public @interface MyAnnotation{
    //jdk8之后才支持这种写法，注解可以跟参数。（自定义注解时可以什么都不写，也可以写上参数内容。一旦写上参数了，使用注解时就必须带上参数，否则会报错，除非参数在自定义是设置了默认值，如下面的number）
    String value(); 
    int number() defult 10; //默认值为10，注解被使用时可以不写number
  }
  /********使用时***********/
  @MyAnnotation(value = "eleven") //这里value可以省略（当且仅当只有一个参数，且参数名为value时）
  ```

##### 2. Java jdk中常见的注解：

> - @Override: 标记重写的方法
>
> - @Deprecated: 标记过时的类、属性、方法等
>
> - @Target: 此为元注解，指定被注解的注解可以标注的对象（类？方法？属性？...）
>
>   ```java
>   // Target参数名为value，下面省略了。参数类型时枚举类型
>   @Target({ElementType.TYPE,ElementType.METHOD,...})//表示@MyAnnotation只能注解类、方法、...
>   @MyAnnotation
>   ```
>
> - @Retention：此为元注解，指定被注解的注解可以标记存储的位置及是否可以被反射的权利。
>
>   ```java
>   // Retention参数名为value，下面省略了。参数类型时枚举类型
>   @Retention(RetentionPolicy.CLASS)  //表示@MyAnnotation可以存储（生成）.class文件
>   //@Retention(RetentionPolicy.RUNTIME) ——>表示@MyAnnotation可以存储（生成）.class文件，并且支持反射机制
>   //@Retention(RetentionPolicy.SOURCE) ——>表示@MyAnnotation只可以存储源文件（.java），不能生成.class文件
>   @MyAnnotation
>   ```
>
>   

```java

```