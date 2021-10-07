- ## git使用教程

  https://git-scm.com/book/zh/v2/
  
  Git ssh免密登录设置：https://blog.csdn.net/w15321271041/article/details/80535135
  
- ## 常用命令

  > - git init ：在对应目录进入命令行，执行该命令初始化仓库
  > - git add xxx : 将xxx添加到暂存区
  > - git commit -m "versionx" xxx: 将xxx提交到本地仓库
  > - git remote add javanote https://github.com/Eleven-J/java-interview-note.git：给github仓库链接创建别名为javanote
  > - git branch xxx: 创建分支xxx
  > - git branch -v: 查看所有分支
  > - git checkout xxx：切换到xxx分支
  > - git merge xxx：将xxx分支合并到当前分支
  > - git push javanote master ：将本地仓库的master分支push到github远程仓库，javanote为链接别名
  > - git pull javanote master : 将远程库的资源拉取到本地
  > - git clone https://github.com/Eleven-J/java-interview-note.git : 将该链接的资源克隆到本地
  > - git status: 查看本地库状态

- ## idea 使用git

  > - 使用VCS—>Create git Respository—>会创建一个本地git仓库（.git文件夹），默认路径就在项目路径下
  >
  > - .git文件夹里有相关文件指针，用于切换版本
  >
  > - .gitignore文件：用于在提交时过滤掉一些集成环境相关的文件（与项目无关）
  >
  > - Github 中创建一个远程库（一般跟自己项目名称一样）
  >
  >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722154159725.png" alt="image-20210722154159725" style="zoom:33%;" />
  >
  > - 远程库链接
  >
  >   ![image-20210722154239163](/Users/jackiez/学海/Java开发笔记/picture/image-20210722154239163-6939763.png)
  >
  > - 如果嫌这个链接太长不好记，可以创建别名
  >
  >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722154551088.png" alt="image-20210722154551088" style="zoom:50%;" />
  >
  > - 切换分支命令
  >
  >   ```java
  >   git checkout master  //将当前指针切换到主分支，即将主分支的版本设为当前版本
  >   ```
  >
  > - 每次进行commit后，可以查看git日志（log），以及相关版本的变化
  >
  >   ![image-20210722160218682](/Users/jackiez/学海/Java开发笔记/picture/image-20210722160218682-6940941.png)
  >
  > - 从version4切回version3:
  >
  >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722160748137.png" alt="image-20210722160748137" style="zoom:50%;" />
  >
  >   **头指针指向了version3（头指针指向哪个版本，哪个版本就是当前用户使用的版本)**
  >
  >   ![image-20210722160914536](/Users/jackiez/学海/Java开发笔记/picture/image-20210722160914536.png)
  >
  > - 新建分支
  >
  >   > - 新建一个分支
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722161457050.png" alt="image-20210722161457050" style="zoom:50%;" />
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午5.07.50.png" alt="截屏2021-07-22 下午5.07.50" style="zoom:50%;" />
  >   >
  >   >   ![截屏2021-07-22 下午4.54.17](/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午4.54.17.png)
  >   >
  >   > - idea右下角有当前分支的标识
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午4.59.28.png" alt="截屏2021-07-22 下午4.59.28" style="zoom:50%;" />
  >   >
  >   > - 可以点击当前标识，来切换不同分支
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午5.01.03.png" alt="截屏2021-07-22 下午5.01.03" style="zoom:50%;" />
  >
  > - 在hot-fix分支上修改代码，再跟master分支合并
  >
  >   > - 在hot-fix分支上修改后提交version5
  >   >
  >   >   ![image-20210722171537109](/Users/jackiez/学海/Java开发笔记/picture/image-20210722171537109-6945342.png)
  >   >
  >   >   ![image-20210722171614188](/Users/jackiez/学海/Java开发笔记/picture/image-20210722171614188-6945375.png)
  >   >
  >   > - 在master分支上操作：合并hot-fix分支
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午5.20.40.png" alt="截屏2021-07-22 下午5.20.40" style="zoom:50%;" />
  >   >
  >   > - 由于我在version3创建的hot-fix分支，随后我在master分支又提交了version4，在hot-fix分支提交了version5，此时就会产生合并冲突，需要手动解决。（如果我master分支一直没变，也就是没有提交version5，那么合并是不会有冲突的）
  >   >
  >   > - <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722173051082.png" alt="image-20210722173051082" style="zoom:50%;" />
  >   >
  >   >   ![截屏2021-07-22 下午5.31.25](/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午5.31.25.png)
  >   >
  >   >   ![image-20210722173618939](/Users/jackiez/学海/Java开发笔记/picture/image-20210722173618939-6946581.png)
  >   >
  >   >   ![image-20210722174017448](/Users/jackiez/学海/Java开发笔记/picture/image-20210722174017448-6946818.png)
  >
  > - ## idea使用github
  >
  >   > - 将项目上传到github
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722175051448.png" alt="image-20210722175051448" style="zoom:50%;" />
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午6.02.35.png" alt="截屏2021-07-22 下午6.02.35" style="zoom:50%;" />
  >   >
  >   > - 此时在github上自动创建了mytest仓库，并且自动将项目代码push到了github仓库
  >   >
  >   > - 随后便可以使用push，pull来操作远程库
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722181054919.png" alt="image-20210722181054919" style="zoom:50%;" />
  >   >
  >   > - 注意：在pull后，idea中会显示Remote，即从github pull下来的资源将会在Remote中，标记如：origin/master
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722201419738.png" alt="image-20210722201419738" style="zoom:50%;" />
  >   >
  >   > - 具体工作流程可以是：程序员每天工作第一件事情——从github中pull代码，被放在origin/master分支；然后你用你本地的master分支（昨天写的代码）去合并今天刚pull下来的origin/master，然后开始在合并的分支上进行今天的代码工作编写，到了晚上要下班的时候，再把这个分支push到github远程仓库中。
  >   >
  >   > - Clone（克隆:直接把项目代码拉到本地，并在指定地址创建出项目）
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午6.51.16.png" alt="截屏2021-07-22 下午6.51.16" style="zoom:50%;" />
  >   >
  >   >   <img src="/Users/jackiez/学海/Java开发笔记/picture/image-20210722185250934.png" alt="image-20210722185250934" style="zoom:50%;" />
  >   >
  >   >   ![截屏2021-07-22 下午6.53.52](/Users/jackiez/学海/Java开发笔记/picture/截屏2021-07-22 下午6.53.52.png)
  >   >
  >   >   
  >
  > 
  >
  > 
  >
  > 

