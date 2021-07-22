##### 1. 集合中存储的都是引用（对象的内存地址），不能存储基本数据类型，即使`list.add(100)`, “100”也是先进行自动装箱成Integer对象，再存入list

##### 2. 在java中，集合本身是一个容器，是一个对象。

##### 3. 在java中集合分为两大类：

> 一类是单个方式存储元素：这一类集合的超级父接口：java.util.collection；
>
> 一类是以键值对的方式存储元素，这一类集合的超级父接口：java.util.Map；

##### 4. 集合继承结构图：

![image-20210118102243152](/Users/jackiez/学海/Java开发笔记/picture/集合继承结构图.png)

![image-20210118105505222](/Users/jackiez/学海/Java开发笔记/picture/集合继承结构图2.png)

![image-20210118110650957](/Users/jackiez/学海/Java开发笔记/picture/集合继承结构图3.png)

##### 5. Collection中的常用方法

> boolean add（object e）：向集合中添加元素
> int size( )：获取集合中元素的个数
> void clear（）：清空集合
> boolean contains（objecto）：判断当前集合中是否包含元素o，包含返回true，不包含返回falseboolean remove（0bject o）删除集合中的某个元素。
> boolean isEmpty( )：判断该集合中元素的个数是否为0
> 0bject[ ] toArray（）:调用这个方法可以把集合转换成数组。
>
> > Collection的遍历方法（**Iterator it = new list.iterator( )** ）：
> >
> > > **.hasnext( ):** 返回类型boolean，判断下一个元素是否为空，并将光标移到下一元素。
> > >
> > > **.next( )：**返回类型object，取出光标所指元素。

> > ​		it对象是指获取当前集合的一个快照，可用来遍历集合（集合状态改变时，需要重新获取新的快照），但是在遍历循环过程中使用list.remove方法删除元素后，集合发生了改变，先前的快照并不会随之改变，此时快照与集合不同，用先前的快照再继续遍历集合会出现异常。
​        解决办法：删除时使用**it.remove( )**,此时删除集合元素的同时，也自动改变了快照，快照和集合在删除操作后仍然一致。

##### 5.1. ArrayList

- Add( )方法触发自动扩容时，默认扩容为原数组列表的1.5倍。
- 创建Arraylist时，无参数构造方法默认容量为10（jdk源码表示：其实创建时容量为0，添加第一个元素时，容量自动默认为10）。

##### 5.2. 泛型机制：

```java
/************************************************************
//未使用泛型
public class Test{
    public static void main(String arg[]){
        Cat cat = new Cat();
        Bird bird = new Bird();
        List mylist = new ArrayList();
        mylist.add(cat);
        mylist.add(bird);
        Iterator it = mylist.iterator();
        while(it.hasNext()){
            Object obj = it.next();
            if(obj instanceof Animal){    //obj运行时是Cat或Bird,Animal是他俩的父类，所以instansof判别为true
                Animal animal = (Animal)obj; //向下转型
                animal.move();
            }
        }
    }
}
*************************************************************/
//使用泛型
public class Test{
    public static void main(String arg[]){
        Cat cat = new Cat();
        Bird bird = new Bird();
        List<Animal> mylist = new ArrayList<Animal>();//这里由于类型自动推断，ArrayList<>中的Animal可以省略。
        mylist.add(cat);
        mylist.add(bird);
        Iterator<Animal> it = mylist.iterator();
        while(it.hasNext()){
          //使用泛型后，mylist中只能存储Animal及它的子类对象，因此，it.next()返回的不再是object，而是Animal
            Animal animal = it.next(); 
            animal.move();
        }
    }
}
class Animal{
    public void move(){
        System.out.println("动物在移动");
    }
}
class Cat extends Animal{
    @Override
    public void move() {
        System.out.println("猫抓老鼠");
    }
}

class Bird extends Animal{
    @Override
    public void move() {
        System.out.println("鸟儿飞翔");
    }
}
/**********************************************************************/
//自定义泛型，note随便写，它只是个标识符。
public class Test1<note> { 
    //public note doSome(note x){   
    //note可以用在方法参数类型位置上（一般写E），也可以用在返回值类型上（一般写T），它类似于一个占位符。
    public void doSome(note x){     
        System.out.println(x);
    }

    public static void main(String[] args) {
        Test1<String> test1 = new Test1<>();  //这里Test1中只能是类，如Integer可以而int不行
        test1.doSome("hello world");
        test1.doSome(100);//编译器报错，100不符合String类型
    }
}
```

##### 6. map是引用数据类型，是以key、value键值对形式存储数据的。Map接口中常用方法：

> `V put（K key，V value）`：向Map集合中添加键值对
> `V get（object key）`：通过key获取value
> `void clear( )`：清空Map集合
> `boolean containsKey（0bject key）`：判断Map中是否包含某key
> `boolean containsValue（object value）`：判断Map中是否包含某个value
> `boolean isEmpty()`：判断Map集合中元素个数是否为0
> `Set<K> keySet（）`：获取Map集合所有的key（所有的键是一个set集合）
> `V remove（object key）`：通过key删除键值对
> `int size（）`：获取Map集合中键值对的个数。
> `Collection<V>  values( )`：获取Map集合中所有的value，返回-个Collection
> `Set<Map.Entry<K,V> entrySet()`:返回Map.Entry类型（其key是K型的，value是V型的）的set集合（Map.Entry类型是将key和value组合起来，形如“key=value”），Map.Entry是一个内部类，<K,V>是泛型。

```java
    public static void main(String[] args) {
        Map<Integer,String> myMap = new HashMap<>();
        myMap.put(1,"zhangsan");
        myMap.put(2,"lisi");
        myMap.put(3, "wangwu");
       //这里原本返回的是object元素的set集合，使用了泛型后，mykey变成了Integer元素的set集合
        Set<Integer> myKey = myMap.keySet();   
        for(Integer key : myKey){
            System.out.println(key);//输出1，2，3

        }
    }
```

- #####  map在遍历时一般有两种方法：


- 先使用Map.keySet( )方法获取key集合，再通过key集合获取相应的value。
- 先使用Map.entrySet( )方法将Map转换为Map.Entry<K,V>类型的set集合，再遍历set集合，使用get方法获取相应的key，value。（此方式效率较高）

##### 6.1 HashMap(哈希表): 它是一种数组和单向链表结合的数据结构。

- HashMap底层实际上就是一个数組。（一维数组,每个元素为单向链表）Node<K,V>[ ] table;

```java
    static class Node<K,V>{
        final int hash;//哈希值（哈希值是key的hashcode方法的执行结果。hash值通过哈希算法/函数可转换为数组下标）
        final K key;   //存储到Map集合的key
        V value;       //存储到Map集合的value
        Node<K,V> next;//下一个节点的内存地址
    }
```

- HashMap集合的默认初始化容量是16，默认加载因子是0.75
  这个默认加载因子是当HashMap集合底层数组的容量达到75%的时候，数组开始扩容，扩容后时原容量的2倍。
  注意：HashMap集合初始化容量必须是2的倍数，这也是官方推荐的，为了达到散列均匀，提高HashMap集合的存取效率。
- 放在HashMap集合key部分的，以及放在HashSet集合中的元素所属的类，需要同时重写hashCode方法和equals方法（直接用IDEA生成）。（重写hashcode方法是为了让相同的多个元素只存一个）
- 若HashMap单向链表中元素超过8个，单向链表数据结构会自动变成红黑**树**数据结构。当红黑树的元素低于6时，红黑树数据结构会自动变成单向链表。  这种机制主要是为了提高效率，毕竟链表元素多了检索效率很低。

- 放在HashSet里的元素等同于放到HashMap的key中了，放在TreeSet里的元素等同于放到TreeMap的key中了。（HashSet底层时HashMap，TreeSet底层时TreeMap）

##### 6.2 TreeSet

- TreeSet是无序（添加和取出的顺序不一样）的，但是它会自动排序（比如：元素是String，就会按首字母顺序排序；元素是Integer，就会按数字大小排序，这是因为String,Integer类都实现了java.lang.Comparable接口；若元素为自定义的类，则需要在此类中实现java.lang.Comarable接口，如此才能排序）。

- 放在TreeSet里的元素所属的类需要实现`java.lang.Comparable`接口（实现compareTo方法，该方法就是TreeSet里元素排序的规则）。**另外一种方法**是给TreeSet构造方法传入比较器对象：TreeSet<Cat> cat = new TreeSet<>(new AnimalComparator( ) ) ,再写出比较器（AnimalComparator类）实现`java.util.comparator`接口。

  note：当比较规则不会发生改变或比较规则只有一个是，建议实现comparable接口；当比较规则有多个，且需要在多个规则中来回切换时，建议实现comparator接口。**服从OCP原则**。

- TreeSet是自平衡二叉树。存放的时候遵循左小右大原则，取出的时候采用中序遍历方式。

##### 7 Collections是一个工具类，里面几乎都是静态方法，主要用来对list对象排序、比较等等。

- 对list集合中元素进行排序时，需要保证list中元素所属的类实现了`java.util.comparator`接口。
- 将ArrayList变成线程安全的：`Collections.synchronizedList(list)`