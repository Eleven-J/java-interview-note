#####      1. IO流：通过IO可以完成对硬盘文件的读写。（读：硬盘——>内存；写：内存——>硬盘）

##### 2. 流的分类（流的四大家族：java.io.InputStream、java.io.OutputStream、java.io.Reader、java.io.Writer）：

- 按流的方向进行分类：

  > - 输入流： 硬盘——>内存（读）                
  > - 输出流： 内存——>硬盘（写）  

- 按流的读取方式分类

  > - 字节流：按照字节的方式读取数据，一次读取一个字节（byte），即一次读取 8个二进制位。通过这种流，什么类型的文件都能读取，包括：文本文件，视频文件，音频文件，图片等等。    **[java.io.InputStream]**、 **[java.io.OutputStream]**
  > - 字符流：按照字符的方式读取数据，一次读取一个字符，主要是为了方便读取普通纯文本文件（.txt）而存在的，无法读取其他如音视频的文件。    **[java.io.Reader]、[java.io.Writer]**
  > - note：在java中，类名以“Steam”结尾的都是字节流；类名以“Reader/Writer”结尾的都是字符流。

##### 3. java.io包下需要掌握的流（16个）：

> 文件专属：java.io.FileInputStream、java.io.FileOutputStream、java.io.Reader、java.io.Writer
>
> 转换流（将字节流转换为字符流）：java.InputStreamReader、java.io.OutputStreamWriter
>
> 缓冲流专属：java.io.BufferedWriter、java.io.BufferedReader、java.io.BufferedInputStream、java.io.BufferedOutputStream
>
> 数据流专属：java.io.DataInputStream、java.io.DataOutputStream（数据连带数据类型一起存储）
>
> 标准输出流：java.io.PrintWriter、java.io.PrintStream
>
> 对象专属流：java.io.ObjectInputStream（反序列化）、java.io.ObjectOutputStream（序列化）

##### 4. 在idea中，当前路径就是该项目工程的根目录。

##### 5. FileInputStream读文件（byte[]方式）:

```java
public class Test2 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("test");
            byte[] bytes = new byte[5]; //一次读5个byte
            int readCount = 0;
            while((readCount = fis.read(bytes)) != -1){
                System.out.print(new String(bytes,0, readCount)); //利用String的构造方法将byte数组转换为String
            }
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (fis != null){
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

##### 6. FileInputStream复制文件（含byte[]方式读写文件）：

```java
//文件copy：先将文件读入内存，再将内存中的文件数据写入目标文件。note：一边读，一边写。而不是整个读完了再写（效率太低）
//以追加的方式在文件末尾写入fos = new FileOutputStream("test1",true); 若换成false，则是先清空文件再写入。
public static void main(String[] args) {
        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            fis = new FileInputStream("test");
          	//fos = new FileOutputStream("test1",true); 
            fos = new FileOutputStream("test1");
            byte[] bytes = new byte[100];
            int readCount = 0;
            while ((readCount = fis.read(bytes)) != -1){
                fos.write(bytes,0, readCount);//这里循环写入是不必使用追加，因为循环写入过程中fos并没有close，每写一次，文件光标自动就在文件末尾。但是如果是写已有数据的文件，又不想覆盖文件已有的数据，则可使用上述追加写文件操作。
                fos.flush(); //刷新，把流管道里残余的数据写完
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (fis == null){
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fos == null){
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

```

##### 7.BufferedReader：带有缓冲区的字符输入流，使用时不需要自定义byte[]或char[]，自带缓冲。

```java
//note1:FileReader类的对象是BufferedReader类中的一个实例变量,因此FileReader称为节点流，BufferedReader称为包装流。它们是   相对的。
//note2:bis.readLine()不读取换行符。
    public static void main(String[] args) {
        FileReader fr = null;
        BufferedReader bis = null;
        try {
            fr = new FileReader("test1");
            bis = new BufferedReader(fr);
            String lineData = null;
            while ((lineData = bis.readLine()) != null){
                System.out.println(lineData);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (bis != null){
                try {
                    bis.close();   //fr是节点流，bis是包装流，源码表示：关闭bis时会自动关闭fr。因此代码中不需要另外关闭fr。
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

##### 8. File类：文件或目录的路径的抽象表示。它有很多有用的方法，判断文件与目录、获取文件容量、获取父路径、操作目录的子目录、获取一个目录下所有的文件名等等，可查文档了解。

```java
File类的常用方法（以“C:\\file”为例）：
  1. File f = new File("C:\\file");  //获取“C盘下file文件或文件夹”的File对象
	2. if(f.exists()){ //判断file文件或文件夹是否存在
    		f.creatNewFile(); //创建上述路径下创建file文件
    		f.mkdir(); //在上述路径下创建file目录
    		f.mkdirs(); //按照上述路径创建多重目录（若给的路径时一个多重目录，且file的上级目录不存在）
  };   
	3. f.getAbsolutePath(); //获取file的绝对路径
	4. f.getParentFile(); //获取file上一级的File对象
	5. f.getParent(); //获取file的父路径，即它上一级的路径。<=> f.getParentFile().getAbsolutePath
	6. f.getName(); //获取file的文件名
	7. f.isFile(); / f.isDirectory(); //判断file是否为文件 / 判断file是否为目录
	8. f.lastModified(); //获取文件或目录的最后一次修改时间。返回值为long,距1970年的毫秒数。
					Date time = new Date(f.lastModified());
					SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
					String strTime = sdf.format(time)
	9. f.lenth(); //获取文件的大小（容量）
	10. f.listFiles(); //获取当前file目录下的所有子目录和子文件，返回File数组。
```





##### 9. ObjectOutputStream/ObjectInputStream作用：将内存中的对象存储到硬盘文件/将硬盘文件中的对象取出到内存中。

- 存储的对象所属的类需要实现Serializable接口，java虚拟机看到某类实现了该接口时，会自动给该类生成一个序列化版本号。note：建议手动生成序列化版本号（若自动生成，该类的代码修改后再编译，又会自动生成一个新的序列化版本号，导致java虚拟机认为代码修改前后是不同的两个类）

```java
private static final long serialVersionUID = 123456789L;//可以用idea工具自动生成全球唯一化的UID
```

- java区分类：首先比较类名；若类名相同，则进一步比较序列化版本号

##### 10. IO+Properties的联合应用:
非常好的一个设计理念：
    经常改变的数据，可以单独写到一个文件中，使用程序动态读取。将来只需要修改这个文件的内容，java代码不需要改动，不需要重新编译，服务器也不需要重启。就可以拿到动态的信息。
    类似于以上机制的这种文件被称为配置文件。并且当配置文件中的内容格式是：
key1=value
key2=value
的时候，我们把这种配置文件叫做属性配置文件。
    java规范中有要求：属性配置文件建议以.properties结尾，但这不是必须的。这种以.properties结尾的文件在java中被称为：属性配置文件。其中`Properties`是专门存放属性配置文件内容的一个类。

```java
public static void main(String[] args) {
        //新建一个输入流对象
        try {
            FileReader reader = new FileReader("user.properties");
            //新建一个map集合
            Properties pro = new Properties();
            //调用Properties对象的load方法将文件中的数据加载到Map集合中
            pro.load(reader);
            //通过key获取value
            System.out.println(pro.getProperty("username"));
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

