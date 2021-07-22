- webstorm环境搭建

  > - Nodejs: 它其实就是google浏览器v8引擎，可以提供javascript代码运行环境，使得脱离浏览器也能运行js。
  >
  > - npm：前端的包管理器，管理前端js依赖，联网下载js依赖，如jquery。相当于后端的maven。
  >
  >   > - 执行npm init -y对项目进行初始化后，项目会自动生成一个package.json文件，类似于maven的pom.xml文件。
  >   >
  >   > - Npm可添加淘宝镜像。
  >   >
  >   > - 执行npm install xxx后，项目会产生一个nodeMoudle文件夹和package-lock.json文件；nodeMoudle文件夹中存放install的xxx依赖，而package-lock.json文件里限定了你要下载的依赖版本。
  >   > - 对一个项目而言，不可能一个依赖一个依赖的手动用命令去下载，所以一般是在package.json文件中罗列需要的依赖，然后用命令“npm install”去执行下载所有依赖，存放到nodeMoudle中。
  >
  > - babel：转码器——将es6的代码转换成es5，再去运行。
  > - elimentUI

- 数据库

  > 插入和修改更新数据库时注意 事务的运用！！！