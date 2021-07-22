IDEA只是一个编写程序的集成环境，它需要和JDK关联起来才能达到程序编译、运行的目的。（IDEA中编译和运行的操作可以通过命令行调用javac.exe和java.exe来实现）

JDK里边包含了JRE，而JRE内包含了JVM。

![image-20210108184155930](/Users/jackiez/学海/Java开发笔记/picture/JDK:JRE:JVM三者关系图.png)

- JDK中包含了许多java类的源代码（库），供我们写自己的项目程序的时候调用。

- JVM虚拟机主要负责代码的编译和运行：它会把我们写的代码编译成“.class”字节码文件，然后交给底层去执行/运行。（JVM里面有javac.exe和java.exe，分别为编译和运行的可执行程序）

- 在编译的时候，编译器知道java.lang里边的所有文件，所以在我们写程序时，像lang中String.java等不需要import。

而java.util里边的文件编译器不知道，所以像util里边的scanner.java需要import，可这样写：import java.util.scanner, 这样编译器就能找到scanner.java文件了。

- IDEA创建的项目模板：com.company.(...), 在不同级的目录/包之间需要调用时，要用到imort，此时编译器默认的根目录是com，所以你需要从com这一级往下写，例：import com.company.test.test01.
- 真正的类名是包含了包名的。
- 我们在用javac.exe和java.exe来去编译和运行我们写的程序是，我需要先在命令行中进入到我们程序的位置（路径），然后再执行javac.exe和java.exe。 而在IDEA中编译和运行时，IDEA会自动告诉JVM我们所写程序的位置（路径）。