**1. 共享资源文件**

- 静态资源文件：

  > 1）如果文件内容是固定，这种文件可以被称为【静态资源文件】（文档，图片，视频）
  >
  > 2）如果文件存放不是内容而是命令，这些命令只能在浏览器编译与执行这种文件可以被称为【静态资源文件】(.html,.css,.js)

- 动态资源文件：

  > 如果文件存放命令，并且命令不能在浏览器编译与执行；只能在服务端计算机编译执行，这样的文件可以被称为【动态资源文件】(.class)

- 静态资源文件与动态资源文件调用区别:
      静态文件被索要时，Http服务器直接通过【输出流】将静态文件中内容或则命令以【二进制形式】推送给发起请求浏览器。
      动态文件被索要时，Http服务器需要创建当前class文件的实例对象（），通过实例对象调用对应的方法处理用户请求。

**2. http请求协议包**（浏览器根据请求信息打包成http协议包用于传输）

![image-20210326125950775](/Users/jackiez/学海/Java开发笔记/picture/http请求协议包.png)

**3.http响应协议包**（服务器根据响应内容打包成http协议包传回浏览器）

![image-20210326130954893](/Users/jackiez/学海/Java开发笔记/picture/http响应协议包.png)

**4. http请求方式**

![image-20210320141306516](/Users/jackiez/学海/Java开发笔记/picture/http请求方式.png)

![image-20210320142014938](/Users/jackiez/学海/Java开发笔记/picture/http请求方式适用场景.png)

**5. http请求的参数**

![image-20210321101058200](/Users/jackiez/学海/Java开发笔记/picture/html请求参数.png)

- 表单域标签分类：

> - (1)<input/>和<textarea></textarea>
>
>   ![image-20210321104323878](/Users/jackiez/学海/Java开发笔记/picture/html表单域标签.png)
>
> - (2)<select></select>
>
>   ![image-20210321104507164](/Users/jackiez/学海/Java开发笔记/picture/html表单域标签select.png)
>
> - note：
>
>   ![image-20210321105143765](/Users/jackiez/Library/Application Support/typora-user-images/image-20210321105143765.png)
>
>   并且，radio和checkbox必须要被选中才能作为参数提交。

- 表单域标签作为请求参数条件：

  ![image-20210321110321349](/Users/jackiez/学海/Java开发笔记/picture/表单域标签作为请求参数条件.png)

**6. http状态码**

![image-20210329221205325](/Users/jackiez/学海/Java开发笔记/picture/http状态码2.png)

![image-20210329221051728](/Users/jackiez/学海/Java开发笔记/picture/http状态码1.png)

**7.HTML标签属性分类：**

![image-20210321113818393](/Users/jackiez/学海/Java开发笔记/picture/html标签属性分类.png)

![image-20210321114506051](/Users/jackiez/学海/Java开发笔记/picture/html标签属性分类2.png)

