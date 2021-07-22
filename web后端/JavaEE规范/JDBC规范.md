- JDBC

  > - JDBC规范下接口介绍(JDK中java.sql包下)
  >
  >   > - java.sql.DriverManager类：这个类负责将数据库厂商提供的Driver接口实现进行注册，负责在Java工程与Mysql服务器之间建立一个【连接通道】
  >   > - java.sql.connection接口：负责管理Java工程与数据库服务器之间【连接通道】
  >   > - java.sql.Preparedstatement接口：负责管理在【连接通道】上进行往返交通的【交通工具】 
  >   > - java.sql.Resultset接口：负责管理数据库服务器返回【临时表】
  >
  > - JDBC流程
  >
  >   ![image-20210325191503841](/Users/jackiez/学海/Java开发笔记/picture/jdbc.png)
  >
  > - JDBC与mysql数据库连接例子1:
  >
  >   ```java
  >   // "jdbc:mysql://服务器所在计算机IP地址:服务器端口号/数据库"
  >   String url = "jdbc:mysqL://ocalhost:3306/bjpowernode"
  >   //sql命令
  >   String sql = "insert into dept（deptno，dname，loc） values（90，'小额贷款部门'，'上海'）"
  >   //1.将MySqL服务器提供的jar包中Driver接口实现类，注册到JVM 
  >   /*Driver driver = new com.mysql.jdbc.Driver();
  >   DriverManager.registerDriver(driver);此种方法没有Class.forName常用*/
  >   Class.forName("com.mysql.jdbc.Driver");
  >   //2.通过DriverManager在Java工程与MySqL服务器之间建立一个连接通道
  >   Connection con= DriverManager.getconnection(url, user:"root" password:"123")
  >   //3.在通道上创建一个交通工具
  >   PreparedStatement ps = con.prepareStatement("");
  >   //4.通过交通工具将SQL命令推送到MySqL服务器上来执行并带回处理结果
  >   int result = ps.executeUpdate(sql);//当sql为查询命令时，使用executeQuery，返回ResultSet对象。  
  >   //5. 销毁相关资源
  >   /*如果是数据库查询操作，则还有此步骤
  >   if(rs != null){
  >     rs.close();
  >   }*/
  >   if(ps != null){
  >     ps.close();
  >   }
  >   if(con != null){
  >   ```
>     con.close();
  >   }
  >   ```java
  >   
  > - JDBC与mysql数据库连接例子2(预编译):
  >
  >   ​```java
  >   String url = "jdbc:mysqL://ocalhost:3306/bjpowernode"
  >   String sql = "insert into dept（deptno，dname，loc） values（？，？，？）"
  >   Class.forName("com.mysql.jdbc.Driver");
  >   Connection con= DriverManager.getconnection(url, user:"root" password:"123")
  >   PreparedStatement ps = con.prepareStatement(sql);
  >   //向Mysql服务器推送100条数据
  >   for(int i=1;i<=100;i++){
  >     ps.setInt(1, i);
  >     ps.setString(2, "dept_"+i);
  >     ps.setString(3, "北京")；
  >     ps.addBatch();//在新的sql语句生成之后，将sql语句作为子弹添加到ps的弹夹。
  >   }
  >   ps.executeBatch();//一次性将100条sql命令推送到mysql服务器执行
  >   //销毁资源
  >   if(ps != null){
  >     ps.close();
  >   }
  >   if(con != null){
  >     con.close();
  >   }
  >   ```
  >   
  > - JDBC与mysql数据库连接例子3(事务控制):
  >
  >   ```java
  >   String url = "jdbc:mysqL://ocalhost:3306/bjpowernode"
  >   String sql = "insert into dept（deptno，dname，loc） values（？，？，？）"
  >   Class.forName("com.mysql.jdbc.Driver");
  >   Connection con= DriverManager.getconnection(url, user:"root" password:"123")
  >   con.setAutoCommit(false);//通过「连接通道」向mysql服务器发送命令“start transaction”
  >   PreparedStatement ps = con.prepareStatement(sql);
  >   for(int i=1;i<=100;i++){
  >     ps.setInt(1, i);
  >     ps.setString(2, "dept_"+i);
  >     ps.setString(3, "北京")；
  >     ps.addBatch();//在新的sql语句生成之后，将sql语句作为子弹添加到ps的弹夹。
  >   }
  >   try{
  >     ps.executeBatch();
  >     con.commit();//所有sql命令都能正常执行，此时提交,删除备份表文件。
  >   }catch(SQLException ex){
  >     //由connection通知mysql服务器将本次操作中所有表文件备份覆盖表文件，取消本次操作。
  >     con.rollback();//向mysql服务器推送“rollback”命令
  >   }
  >   ```
  >


