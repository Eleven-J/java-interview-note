##### 1. 反射机制：可用来操作字节码文件（“.class”文件），相关类在java.lang.reflect.* 。它主要与配置文件配合使用，可使代码更灵活。

```java
/*获取Class的三种方式*/
1. className = Class.forName("类的全名");
2. 对象.getclass(): Class className = "abc".getClass();//"abc"对象是String类型，所以得到的className为"java.lang.String"
3. 类型.class: Class i = int.class
```

##### 2. 反射机制重要类：

> - java.lang.Class: 代表整个字节码，代表一个类型。（代表整个类）
> - java.lang.reflect.Method: 代表字节码中的方法字节码（代表类中的方法）
> - java.lang.reflect.Constructor: 代表字节码中的构造方法字节码（代表类中的构造方法）
> - java.lang.reflect.Filed: 代表字节码中的属性字节码（代表类中的属性，即成员变量）

```java
//配置文件内容：className=java.lang.Object（这里的类名一定要写全称，带包名的那种）
public class Test8 {
    public static void main (String[] args) throws Exception {
        //通过IO流读取user.properties配置文件，这种方式可适应不同操作系统
        String path = Thread.currentThread().getContextClassLoader()
                      .getResource("com/company/user.properties").getPath();
        FileReader reader = new FileReader(path); //相对路径："src/com/company/user.properties"
        //创建属性类对象map
        Properties pro = new Properties();
        //加载
        pro.load(reader);
        //关闭流
        reader.close();
        //通过key获取value
        String className = pro.getProperty("className");
        //通过反射机制实例化对象,代码无须改变，只需要修改配置文件即可更改创建的对象。
        Class c = Class.forName(className);
        Object obj = c.newInstance();//使用无参数构造方法
        System.out.println(obj);
    }
}
/******************************************************************************************************/
/*使用资源绑定器可以方便地获取配置文件内容：使用资源绑定器重写以上代码，更简便*/
public class Test8 {
    public static void main (String[] args) throws Exception {
        //文件路径必须是类路径下的配置文件,且不用写后缀.properties
        ResourceBundle bundle = ResourceBundle.getBundle("com/company/user");
        String userName = bundle.getString("className");
        Class c = Class.forName(className);
        Object obj = c.newInstance();
        System.out.println(obj);
    }
}

```

##### 3. 若希望一个类的静态代码块执行，其余代码不执行，可使用Class.forName("完整类名")，不要返回值，此方法导致类加载，类加载是静态代码块执行。

##### 4. 通过反射机制访问对象属性

```java
public class Test8 {
    public static void main (String[] args) throws Exception {
      String userName = bundle.getString("className");
      Class c = Class.forName(className);
      Object obj = c.newInstance();
      Field info = c.getDeclaredField("属性名");//此方法无法访问私有属性，用info.setAccessible(true)语句设置后可访问
      info.set(obj,"对应属性值") //给info属性赋值
      s = info.get(obj)  //获取info属性的值
       
    }
}      

```

##### 5. 通过反射机制调用对象的方法（其中部分注释里面包含了反射机制调用构造方法）：

```java
public class Test10 {
    public static void main(String[] args) throws Exception {
        Class userServiceClass = Class.forName("com/company/UserService.java");//加载类
        Object obj = userServiceClass.newInstance();//创建对象，默认使用无参数构造方法
      	/*若用有参数构造方法：
      			Constructor con = userServiceClass.getDeclaredConstructor(int.class);//先获取有参数的构造方法
      			Object obj = con.newInstance(100); //使用获取到的构造方法创建对象
      	*/
        //获取login方法
        Method loginMethod = userServiceClass.getDeclaredMethod("login",String.class,String.class);
        //调用login方法
        loginMethod.invoke(obj,"admin","123");
    }
}
```

```java
public class UserService {
    int i;
    public boolean login(String userName, String password){
        if ("admin".equals(userName) && "123".equals(password)){
            return true;
        }
        return false;
    }
    public void logout(){
        System.out.println("系统安全退出");
    }

}
```

- 反射应用

  > - 动态加载
  > - 集成环境IDE开发
  > - 框架开发