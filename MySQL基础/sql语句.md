##### 1. SQL语句主要分类：

> - DQL（数据查询语言）：查询语句，凡是select语句都是DQL。
> - DML（数据操作语言）：insert delete update，对表当中的数据进行增删改。
> - DDL（数据定义语言）create drop alter，对表结构的增删改。
> - TCL（事务控制语言）：commit提交事务，rollback回滚事务。（TCI中的T是Transaction）
> - DCL（数据控制语言）grant授权、revoke撤销权限等。

**2. 高级插入命令**

![image-20210324000330940](/Users/jackiez/学海/Java开发笔记/picture/高级插入命令.png)

Note1：表文件备份命令(将A表的数据备份到B表中)—— create table B select * from A

Note2:  mysql中“Null”值不表示空，而是表示“不确定的值”，无法进行任何运算。

**3. 临时表概念**

![image-20210324181301054](/Users/jackiez/学海/Java开发笔记/picture/临时表1.png)

![image-20210324181430981](/Users/jackiez/学海/Java开发笔记/picture/临时表2.png)

![image-20210324181520366](/Users/jackiez/学海/Java开发笔记/picture/临时表3.png)

**4. 查询命令详解**

- SELECT执行原理

![image-20210324190228273](/Users/jackiez/学海/Java开发笔记/picture/groupby与select.png)

- WHERE命令

  ![image-20210324222315198](/Users/jackiez/学海/Java开发笔记/picture/where.png)

- GROUP BY命令

  ![image-20210324222537460](/Users/jackiez/学海/Java开发笔记/picture/groupby.png)

- HAVING命令

![image-20210324213154240](/Users/jackiez/学海/Java开发笔记/picture/Having.png)

- LIMIT命令

  ![image-20210324224147291](/Users/jackiez/学海/Java开发笔记/picture/limit.png)

  Note：mysql服务器中，表文件字段位置从1开始计算，而表文件数据行位置从0开始计算。

- LIKE模糊查询、is null、is not null、通配符 % 和  _

  ![image-20210324223137240](/Users/jackiez/学海/Java开发笔记/picture/like模糊查询.png)

![image-20210324223241810](/Users/jackiez/学海/Java开发笔记/picture/通配符.png)

- JOIN命令：多表查询命令（内链接）

  ![image-20210324231604167](/Users/jackiez/学海/Java开发笔记/picture/join.png)

![image-20210324231710655](/Users/jackiez/学海/Java开发笔记/picture/joinon.png)

- JOIN多表查询（外连接）

  ![image-20210325092134497](/Users/jackiez/学海/Java开发笔记/picture/外连接.png)

- COUNT(字段)与COUNT(*)

  ![image-20210325091701356](/Users/jackiez/学海/Java开发笔记/picture/count.png)

- 子查询

  从当前数据表的临时表中得不到某些数据（如下图中的薪水平均值）时，可通过完整sql语句嵌套来帮助查询。

  ![image-20210325095609198](/Users/jackiez/学海/Java开发笔记/picture/子查询场景.png)

  ![image-20210325095758716](/Users/jackiez/学海/Java开发笔记/picture/子查询select.png)

  ![image-20210325094102503](/Users/jackiez/学海/Java开发笔记/picture/子查询.png)

![image-20210325094951881](/Users/jackiez/学海/Java开发笔记/picture/子查询from定位.png)

![image-20210325095406340](/Users/jackiez/学海/Java开发笔记/picture/子查询groupby.png)

- 索引管理 

  ![image-20210325154128540](/Users/jackiez/学海/Java开发笔记/picture/索引.png)

- 视图

  ![image-20210325164431056](/Users/jackiez/学海/Java开发笔记/picture/视图.png)

![image-20210325164523899](/Users/jackiez/学海/Java开发笔记/picture/视图作用.png)

- 事务（transaaction）

  > - 介绍：
  >   事务是MySql服务器提供一个管理对象，用于对当前表文件备份进行管理
  >
  > - 使用
  >
  >   > **start transaction；**#通知Mysq1服务器提供一个事务对象，这个事务对象对  接下来操作产生所有备份进行管理
  >   >
  >   > **delete from emp where deptno=30**#生成emp.bak
  >   > **delete from dept where deptno=30**#生成dept.bak
  >   > **rollback；**#通知mysq1服务器将本次操作中所有备份信息覆盖到表文件，来取消本次操作
  >   > **commit；**#通知mysq1服务器将本次操作中生成所有备份信息进行删除，称之为提交操作