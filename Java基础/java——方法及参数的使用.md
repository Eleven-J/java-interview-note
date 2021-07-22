##### 1. 可变长参数：

```java
public class Test9 {

    public void myFunction1(String... args){

    }

    public static void main(String[] args) {
        myFunction2(1,"hello","world");

    }
    public static void myFunction2(int i, String... args){//变长参数只能放在参数列表的末尾，
        for(String myString : args){   //可变长参数可看作是一个数组，可以用操作数组的方式去操作它,同样传参的时候也可传数组
            System.out.println(myString);
        }
    }
}
```

