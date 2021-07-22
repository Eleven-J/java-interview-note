##### 1. 获取文件绝对路径（兼容各种操作系统）：

```java
//下面代码会过去文件的绝对路径，可动态适应不同的操作系统。
String path = Thread.currentThread().getContextClassLoader().getResource("文件的类路径").getPath();
//note:类路径是指在src文件下，类路径是以src为根。(这里是为了好记，准确来说类路径的根是在out文件下的项目文件夹下——>去项目文件夹看看就知道了)
```

##### 2. 

