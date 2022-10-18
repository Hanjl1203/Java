# Java入门

## Java简介

Java最早是由SUN公司（已被Oracle收购）的詹姆斯·高斯林（高司令，人称Java之父）在上个世纪90年代初开发的一种编程语言，最初被命名为Oak，目标是针对小型家电设备的嵌入式应用，结果市场没啥反响。互联网的崛起，让Oak重新焕发了生机，于是SUN公司改造了Oak，在1995年以Java的名称正式发布，原因是Oak已经被人注册了，因此SUN注册了Java这个商标。随着互联网的高速发展，Java逐渐成为最重要的网络编程语言。

Java介于编译型语言和解释型语言之间。

- 编译型语言：如C、C++，代码是**直接编译成机器码执行**，但是不同的平台（x86、ARM等）CPU的指令集不同，因此，需要编译出每一种平台的对应机器码。
- 解释型语言如：Python、Ruby，可以由**解释器直接加载源码然后运行**，代价是运行效率太低。
- 而 Java是将代码编译成一种“字节码”，它类似于抽象的CPU指令，然后，针对不同平台编写虚拟机，不同平台的虚拟机负责加载字节码并执行，这样就实现了“一次编写，到处运行”的效果。对于虚拟机，需要为每个平台分别开发。为了保证不同平台、不同公司开发的虚拟机都能正确执行Java字节码，SUN公司制定了一系列的Java虚拟机规范。从实践的角度看，JVM的兼容性做得非常好，低版本的Java字节码完全可以正常运行在高版本的JVM上。

随着 Java的发展，SUN给 Java又分出了三个不同版本：

- Java SE：Standard Edition
- Java EE：Enterprise Edition
- Java ME：Micro Edition

简单来说

- Java SE就是标准版，包含标准的JVM和标准库
- Java EE是企业版，它只是在Java SE的基础上加上了大量的API和库，以便方便开发Web应用、数据库、消息服务等，Java EE的应用使用的虚拟机和Java SE完全相同。
- Java ME是一个针对嵌入式设备的“瘦身版”，Java SE的标准库无法在Java ME上使用，Java ME的虚拟机也是“瘦身版”。


Java SE是整个Java平台的核心，而 Java EE是进一步学习Web应用所必须的。Spring等框架都是Java EE开源生态系统的一部分。没有特殊需求，不建议学习Java ME。



### JDK环境配置

JDK与JRE：

- JRE：Java Runtime Environment，运行Java字节码的虚拟机

- JDK：Java Development Kit，如果只有Java源码，要编译成Java字节码，就需要JDK，因为JDK除了包含JRE，还提供了编译器、调试器等开发工具

  

安装完 JDK后，需要设置一个`JAVA_HOME`的环境变量，它指向JDK的安装目录

- 在Windows下，它是安装目录

  ```bash
  C:\Program Files\Java\jdk-18
  ```

- 在Mac下，它在`~/.bash_profile`或`~/.zprofile`里

  ```bash
  export JAVA_HOME=`/usr/libexec/java_home -v 18`
  ```




然后把`JAVA_HOME`的`bin`目录附加到系统环境变量`PATH`上

- 在Windows下

  ```bash
  Path=%JAVA_HOME%\bin;<现有的其他路径>
  ```

- 在Mac下，它在`~/.bash_profile`或`~/.zprofile`里

  ```bash
  export PATH=$JAVA_HOME/bin:$PATH
  ```




把`JAVA_HOME`的`bin`目录添加到`PATH`中是为了在任意文件夹下都可以运行`java`。打开命令提示符窗口，输入命令`java -version`，如果一切正常，会看到版本输出

- 如果看到的版本号不是`18`，而是`15`、`1.8`之类，说明系统存在多个JDK，且默认JDK不是JDK 18

- 如果得到一个错误输出：这是因为系统无法找到Java虚拟机的程序`java.exe`，需要检查JAVA_HOME和PATH的配置。




### 编译运行步骤

编写第一个Java程序

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

把代码保存为文件时，文件名必须是`Hello.java`，而且文件名也要注意大小写：要和定义的类名`Hello`完全保持一致。

Java源码本质上是一个文本文件

- 先用`javac`把`Hello.java`编译成字节码文件`Hello.class`
- 然后用`java`命令执行这个字节码文件
- 可执行文件`javac`是编译器
- 可执行文件`java`就是虚拟机



**具体步骤：**

第一步，在保存`Hello.java`的目录下执行命令`javac Hello.java`：

```shell
$ javac Hello.java
```

如果源代码无误，上述命令不会有任何输出，而当前目录下会产生一个`Hello.class`文件：

```shell
$ ls
Hello.class	Hello.java
```

第二步，执行`Hello.class`，使用命令`java Hello`：

```shell
$ java Hello
Hello, world!
```

注意：给虚拟机传递的参数`Hello`是定义的类名，虚拟机自动查找对应的`class文件`并执行。



直接运行`java Hello.java`也是可以的：

```shell
$ java Hello.java 
Hello, world!
```

这是Java 11新增的一个功能，它可以直接运行一个单文件源码，但在实际项目中，单个不依赖第三方库的Java源码是非常罕见的，所以，绝大多数情况下，无法直接运行一个Java源码文件，原因是**它需要依赖其他的库**。



### IDEA

IDE是集成开发环境：Integrated Development Environment的缩写。

使用IDE的好处在于，可以把编写代码、组织项目、编译、运行、调试等放到一个环境中运行，能极大地提高开发效率。

IDE提升开发效率主要靠以下几点：

- 编辑器的自动提示，可以大大提高敲代码的速度；
- 代码修改后可以自动重新编译，并直接运行；
- 可以方便地进行断点调试。

**IntelliJ Idea**是由JetBrains公司开发的一个功能强大的IDE，分为免费版和商用付费版。JetBrains公司的IDE平台也是基于IDE平台+语言插件的模式，支持Python开发环境、Ruby开发环境、PHP开发环境等，这些开发环境也分为免费版和付费版。

| 常用快捷键              | 功能                                                         |
| ----------------------- | ------------------------------------------------------------ |
| Ctrl + Z                | 撤销 （必备）                                                |
| Ctrl + Y                | 删除光标所在行 或 删除选中的行 （必备）                      |
| Ctrl + /                | 注释光标所在行代码，会根据当前不同文件类型使用不同的注释符号 （必备） |
| Ctrl + F                | 在当前文件进行文本查找 （必备）                              |
| Ctrl + R                | 在当前文件进行文本替换 （必备）                              |
| Ctrl + Y                | 删除光标所在行 或 删除选中的行 （必备）                      |
| Ctrl + X                | 剪切光标所在行 或 剪切选择内容                               |
| Ctrl + C                | 复制光标所在行 或 复制选择内容                               |
| Ctrl + D                | 复制光标所在行 或 复制选择内容，并把复制内容插入光标位置下面 （必备） |
| Ctrl + 光标             | 按 Ctrl 不要松开，会显示光标所在的类信息摘要                 |
| Shift + Tab             | 取消缩进                                                     |
| Ctrl + Alt + L          | 格式化代码，可以对当前文件和整个包目录使用 （必备）          |
| Ctrl + Alt + O          | 优化导入的类，可以对当前文件和整个包目录使用 （必备）        |
| Ctrl + Alt + B          | 在某个调用的方法名上使用会跳到具体的实现处，可以跳过接口     |
| Alt + Shift + 前方向键  | 移动光标所在行向上移动                                       |
| Alt + Shift + 后方向键  | 移动光标所在行向下移动                                       |
| Ctrl + Shift + 前方向键 | 光标放在方法名上，将方法移动到上一个方法前面，调整方法排序   |
| Ctrl + Shift + 后方向键 | 光标放在方法名上，将方法移动到下一个方法前面，调整方法排序   |
| Ctrl + Shift + Space    | 智能代码提示                                                 |
| Ctrl + Shift + Enter    | 自动结束代码，行末自动添加分号 （必备）                      |
| Alt + Enter             | IntelliJ IDEA 根据光标所在问题，提供快速修复选择，光标放在的位置不同提示的结果也不同 （必备） |
| Alt + Insert            | 代码自动生成，如生成对象的 set / get 方法，构造函数，toString() 等 |



### Debug

Debug 是供程序员使用的程序调试工具，它可以用于查看程序的执行流程，也可以用于追踪程序执行过程来调试程序。

加断点 → Debug 运行 → 单步运行 → 看 Debugger 窗口 → 看 Console 窗口

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/Debug%E6%8C%89%E9%94%AE%E8%AF%B4%E6%98%8E-16652942700731.png" style="zoom: 67%;" />

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/Debug%E6%9D%A1%E4%BB%B6%E6%96%AD%E7%82%B9-16652942700742.png" alt="Debug条件断点" style="zoom: 67%;" />





## class文件管理

### classpath

因为Java是编译型语言，源码文件编译后的`.class`文件才是真正可以被JVM执行的字节码。因此JVM需要知道，如果要加载一个`abc.xyz.Hello`的类，应该去哪搜索对应的`Hello.class`文件

`classpath`： JVM用到的一个环境变量，它用来指示 JVM如何搜索`class`

- `classpath`就是一组目录的集合，它设置的搜索路径与操作系统相关

- 在Windows系统上，用`;`分隔，带空格的目录用`""`括起来

  ```
  C:\work\project1\bin;C:\shared;"D:\My Documents\project1\bin"
  ```

- 在Linux系统上，用`:`分隔

  ```
  /usr/shared:/usr/local/bin:/home/liaoxuefeng/bin
  ```


假设`classpath`是`.;C:\work\project1\bin;C:\shared`，当JVM在加载`abc.xyz.Hello`这个类时，会依次查找：

- <当前目录>\abc\xyz\Hello.class
- C:\work\project1\bin\abc\xyz\Hello.class
- C:\shared\abc\xyz\Hello.class

注意到`.`代表当前目录。如果JVM在某个路径下找到了对应的`class`文件，就不再往后继续搜索。如果所有路径下都没有找到，就报错。



`classpath`的设定方法有两种：

- 在系统环境变量中设置`classpath`环境变量，不推荐
- 在启动JVM时设置`classpath`变量，推荐

强烈不推荐在系统环境变量中设置`classpath`，那样会污染整个系统环境。在启动JVM时设置`classpath`才是推荐的做法。实际上就是给`java`命令传入`-classpath`或`-cp`参数：

```bash
java -cp .;C:\work\project1\bin;C:\shared abc.xyz.Hello
```

没有设置系统环境变量，也没有传入`-cp`参数，JVM默认的`classpath`为`.`

在IDE中运行Java程序，IDE自动传入的`-cp`参数是当前工程的`bin`目录和引入的jar包



在自己编写的`class`中，会引用Java核心库的`class`，例如，`String`、`ArrayList`等。这些`class`应该上哪去找？

- 不需要告诉JVM如何去Java核心库查找`class`，不要把任何Java核心库添加到classpath中，JVM根本不依赖classpath加载核心库

- 更好的做法是，不要设置`classpath`，默认的当前目录`.`对于绝大多数情况都够用


假设有一个编译后的`Hello.class`，它的包名是`com.example`，当前目录是`C:\work`，那么，目录结构必须如下：

```ascii
C:\work
└─ com
   └─ example
      └─ Hello.class
```

运行这个`Hello.class`必须在当前目录下使用如下命令：

```
C:\work> java -cp . com.example.Hello
```

JVM根据classpath设置的`.`在当前目录下查找`com.example.Hello`，即实际搜索文件必须位于`com/example/Hello.class`。如果指定的`.class`文件不存在，或者目录结构和包名对不上，均会报错。



### jar包

如果有很多`.class`文件，散落在各层目录中，肯定不便于管理。把目录打一个包就方便多了

jar包可以把`package`组织的目录层级，以及各个目录下的所有文件（包括`.class`文件和其他文件）都打成一个jar文件

jar包实际上就是一个zip格式的压缩文件，而jar包相当于目录。如果要执行一个jar包的`class`，就可以把jar包放到`classpath`中：

```shell
java -cp ./hello.jar abc.xyz.Hello
```



如何创建jar包？

- 制作一个zip文件，把后缀从`.zip`改为`.jar`即可


假设编译输出的目录结构是这样：

```ascii
package_sample
└─ bin
   ├─ hong
   │  └─ Person.class
   │  ming
   │  └─ Person.class
   └─ mr
      └─ jun
         └─ Arrays.class
```

这里需要特别注意的是，jar包里的第一层目录，不能是`bin`，而应该是`hong`、`ming`、`mr`。

`hong.Person`必须按`hong/Person.class`存放，而不是`bin/hong/Person.class`。



jar包还可以包含一个特殊的`/META-INF/MANIFEST.MF`文件，`MANIFEST.MF`是纯文本，可以指定`Main-Class`和其它信息。JVM会自动读取这个`MANIFEST.MF`文件，如果存在`Main-Class`，就不必在命令行指定启动的类名，而是用更方便的命令：

```
java -jar hello.jar
```

jar包还可以包含其它jar包，这个时候，就需要在`MANIFEST.MF`文件里配置`classpath`了。

在大型项目中，不可能手动编写`MANIFEST.MF`文件，再手动创建zip包。Java社区提供了大量的开源构建工具，例如[Maven](https://www.liaoxuefeng.com/wiki/1252599548343744/1255945359327200)，可以非常方便地创建jar包。



### class版本

通常说的Java 8，Java 11，Java 17，是指JDK的版本，也就是JVM的版本，更确切地说，就是`java.exe`这个程序的版本：

```shell
$ java -version
java version "17" 2021-09-14 LTS
```

而每个版本的JVM，它能执行的class文件版本也不同。例如，Java 11对应的class文件版本是55，而Java 17对应的class文件版本是61。

- 如果用Java 11编译一个Java程序，输出的class文件版本默认就是55，这个class既可以在Java 11上运行，也可以在Java 17上运行，因为Java 17支持的class文件版本是61，表示“最多支持到版本61”。

- 如果用Java 17编译一个Java程序，输出的class文件版本默认就是61，它可以在Java 17、Java 18上运行，但不可能在Java 11上运行，因为Java 11支持的class版本最多到55。如果使用低于Java 17的JVM运行，会得到一个`UnsupportedClassVersionError`




可以用Java 17编译一个Java程序，指定输出的class版本要兼容Java 11（即class版本55），这样编译生成的class文件就可以在Java >=11的环境中运行。指定编译输出有两种方式：

- 在`javac`命令行中用参数`--release`设置：参数`--release 11`表示源码兼容Java 11，编译的class输出版本为Java 11兼容，即class版本55。

  ```shell
  $ javac --release 11 Main.java
  ```

- 用参数`--source`指定源码版本，用参数`--target`指定输出class版本：如下命令如果使用Java 17的JDK编译，它会把源码视为Java 9兼容版本，并输出class为Java 11兼容版本。

  ```shell
  $ javac --source 9 --target 11 Main.java
  ```


- `--release`参数和`--source --target`参数只能二选一，不能同时设置。



指定版本如果低于当前的JDK版本，会有一些潜在的问题。例如用Java 17编译`Hello.java`，参数设置`--source 9`和`--target 11`：

```java
public class Hello {
    public static void hello(String name) {
        System.out.println("hello".indent(4));
    }
}
```

问题：

- 用低于Java 11的JVM运行`Hello`会得到一个`LinkageError`，因为无法加载`Hello.class`文件
- 用Java 11运行`Hello`会得到一个`NoSuchMethodError`，因为`String.indent()`方法是从Java 12才添加进来的



如果使用--release 11则会在编译时检查该方法是否在Java 11中存在。因此如果运行时的JVM版本是Java 11，则编译时也最好使用Java 11

- 如果使用`javac`编译时不指定任何版本参数，那么相当于使用`--release 当前版本`编译

- 在开发阶段，多个版本的JDK可以同时安装，当前使用的JDK版本可由`JAVA_HOME`环境变量切换

- 在编写源代码的时候，通常会预设一个源码的版本。在编译的时候，如果用`--source`或`--release`指定源码版本，则使用指定的源码版本检查语法。
- 例如：使用了lambda表达式的源码版本至少要为8才能编译，使用了`var`关键字的源码版本至少要为10才能编译，使用`switch`表达式的源码版本至少要为12才能编译，且12和13版本需要启用`--enable-preview`参数。



### 模块

从Java 9开始，JDK又引入了模块（Module）。

在Java 9之前，一个大型Java程序会生成自己的jar文件，同时引用依赖的第三方jar文件，而JVM自带的Java标准库，实际上也是以jar文件形式存放的，这个文件叫`rt.jar`，一共有60多M。

如果是自己开发的程序，除了一个自己的`app.jar`以外，还需要一堆第三方的jar包，运行一个Java程序，一般来说，命令行写这样：

```bash
java -cp app.jar:a.jar:b.jar:c.jar com.liaoxuefeng.sample.Main
```

 注意：JVM自带的标准库rt.jar不要写到classpath中，写了反而会干扰JVM的正常运行。

如果漏写了某个运行时需要用到的jar，那么在运行期极有可能抛出`ClassNotFoundException`。

所以，jar只是用于存放class的容器，它并不关心class之间的依赖。



从Java 9开始引入的模块，主要是为了解决“依赖”这个问题。如果`a.jar`必须依赖另一个`b.jar`才能运行，那我们应该给`a.jar`加点说明啥的，让程序在编译和运行的时候能自动定位到`b.jar`，这种自带“依赖关系”的class容器就是模块。

为了表明Java模块化的决心，从Java 9开始，原有的Java标准库已经由一个单一巨大的`rt.jar`分拆成了几十个模块，这些模块以`.jmod`扩展名标识，可以在`$JAVA_HOME/jmods`目录下找到它们：

- java.base.jmod
- java.compiler.jmod
- java.datatransfer.jmod
- java.desktop.jmod
- ...

这些`.jmod`文件每一个都是一个模块，模块名就是文件名。例如：模块`java.base`对应的文件就是`java.base.jmod`。模块之间的依赖关系已经被写入到模块内的`module-info.class`文件了。所有的模块都直接或间接地依赖`java.base`模块，只有`java.base`模块不依赖任何模块，它可以被看作是“根模块”，好比所有的类都是从`Object`直接或间接继承而来。

把一堆class封装为jar仅仅是一个打包的过程，而把一堆class封装为模块则不但需要打包，还需要写入依赖关系，并且还可以包含二进制代码（通常是JNI扩展）。此外，模块支持多版本，即在同一个模块中可以为不同的JVM提供不同的版本。



## 关键字与标识符

### 关键字

定义：被Java赋予了特殊的含义，用作专门用途的字符串（单词）

特点：关键字的字母都是小写

保留字：现有Java版本尚未使用， 但以后版本可能会作为关键字使用，命名标识符时要避免使用这些保留字  

### 标识符

定义：Java 对各种变量、 方法和类等要素命名时使用的字符序列称为标识符

技巧：凡是自己可以起名字的地方都叫标识符  

举例：类名、方法名、变量名、常量名、包名、接口名...

定义合法**标识符规则**：

- 由26个英文字母大小写， 0-9 ， _或 $ 组成
- 数字不可以开头
- 不可以使用关键字和保留字，但能包含关键字和保留字
- Java中严格区分大小写，长度无限制
- 标识符不能包含空格  

如果不遵守规则，编译将无法通过

Java中的名称**命名规范**：

- 包名：多单词组成时所有字母**都小写**： xxxyyyzzz
- 类名、接口名：多单词组成时，所有单词的**首字母大写**： XxxYyyZzz
- 变量名、方法名：多单词组成时，**第一个单词首字母小写**，第二个单词开始每个单词首字母大写： xxxYyyZzz
- 常量名：所有字母**都大写**。多单词时每个单词用下划线连接： XXX_YYY_ZZZ

注意1：在起名字时，为了提高阅读性，要尽量有意义，“见名知意”

注意2： Java采用unicode字符集，因此标识符也可以使用汉字声明，但是不建议使用

### 三种注释

在Java程序中，注释是一种给人阅读的文本，不是程序的一部分，所以编译器会自动忽略注释。

Java有3种注释，第一种是单行注释，以双斜线开头，直到这一行的结尾结束：

```java
// 这是注释...
```

而多行注释以`/*`星号开头，以`*/`结束，可以有多行：

```java
/*
这是注释
blablabla...
这也是注释
*/
```

还有一种特殊的多行注释，以`/**`开头，以`*/`结束，如果有多行，每行通常以星号开头：

```java
/**
 * 可以用来自动创建文档的注释
 * 
 * @auther han
 */
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

这种特殊的多行注释需要写在类和方法的定义处，可以用于自动创建文档。

------



## 变量

### 定义

概念：

- 内存中的一个`存储区域`
- 该区域的数据可以在**同一类型范围**内不断变化
- 变量是程序中最基本的存储单元。包含**变量类型、变量名、存储的值**  

作用：用于在内存中保存数据

注意：

- Java中每个变量必须先声明，后使用
- 使用变量名来访问这块区域的数据
- 变量的作用域：其定义所在的一对{ }内
- 变量只有在其作用域内才有效
- 同一个作用域内，不能定义重名的变量  

声明变量

语法： `<数据类型> <变量名称>`

```java
 int var;
```

变量的赋值

语法： `<变量名称> = <值>`

```java
var = 10;
```

声明和赋值变量

语法： `<数据类型> <变量名> = <初始化值>`

```java
int var = 10;  
```

```java
class VariableTest{
    public static void main(String[] args){
        //变量的定义
        int myAge=12;
        //变量的使用
        System.out.println(myAge);
        
        //变量的声明
        int myNumber;
        //变量的赋值
        myNumber=1000;
        //变量的使用
        System.out.println(myNumber)
    }
}
```



### 分类

对于每一种数据都定义了明确的具体数据类型（强类型语言），在内存中分配了不同大小的内存空间  

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220117145838821-16652942700743.png" alt="image-20220117145838821" style="zoom:50%;" />

**基本数据类型**：CPU可以直接进行运算的类型

Java定义了以下几种基本数据类型：

- 整数类型：byte，short，int，long
- 浮点数类型：float，double
- 字符类型：char
- 布尔类型：boolean

**不同的数据类型占用的字节数不一样。**

除了上述基本类型的变量，剩下的都是**引用类型**。引用类型最常用的就是`String`字符串：

```java
String s = "hello";
```

引用类型的变量类似于C语言的指针，它内部存储一个“地址”，指向某个对象在内存的位置



### 整数类型

Java各整数类型有固定的表数范围和字段长度，不受具体OS的影响，以保证java程序的可移植性

Java的整型常量默认为 `int` 型，**声明long型常量须后加‘l’或‘L’**

Java程序中变量**通常声明为int型**，除非不足以表示较大的数，才使用long  

| 类 型 | 占用存储空间 | 表数范围                |
| ----- | ------------ | ----------------------- |
| byte  | 1字节=8bit位 | -128 ~ 127              |
| short | 2字节        | -2^15 ~2^15-1           |
| int   | 4字节        | -2^31 ~ 2^31-1 (约21亿) |
| long  | 8字节        | -2^63 ~ 2^63-1          |

bit：计算机中的最小存储单位     byte：计算机中基本存储单元 

```java
byte numble1=12; 
short number2=123;
int number3=1234;
long number4=12345L;
```



### 浮点类型

Java 浮点类型也有固定的表数范围和字段长度，不受具体操作系统的影响。

浮点型常量有两种表示形式：

- 十进制数形式：如： 5.12，512.0f，.512 (必须有小数点）
- 科学计数法形式:如： 5.12e2，512E2，100E-2

浮点数可以分为两类：

- `float`：单精度，尾数可以精确到7位有效数字。很多情况下，精度很难满足需求。
- `double`：双精度，精度是float的两倍。通常采用此类型。

Java 的浮点型常量默认为`double`型， **声明float型常量，须后加‘f’或‘F**’

- 对于float型数值，第1位是符号位，接下来8位表示指数，再接下来的23位表示尾数
- 对于double类型数值，**第1位也是符号位，接下来的11位表示指数，再接下来的52位表示尾数**

| 类 型        | 占用存储空间 | 表数范围               |
| ------------ | ------------ | ---------------------- |
| 单精度float  | 4字节        | -3.403E38 ~ 3.403E38   |
| 双精度double | 8字节        | -1.798E308 ~ 1.798E308 |



### 字符类型

char 型数据用来表示通常意义上“字符”(2字节)

Java中的所有字符都使用Unicode编码，故一个字符可以存储一个字母，一个汉字，或其他书面语的一个字符。

字符型变量的三种表现形式：

- 字符常量是用**单引号(‘ ’)**括起来的单个字符。 例如： char c1 = 'a'; char c2= '中'; char c3 = '9';
- Java中还允许使用转义字符‘\’来将其后的字符转变为特殊字符型常量。例如： char c3 = ‘\n’; // '\n'表示换行
- 直接使用 Unicode 值来表示字符型常量：‘\uXXXX’。其中， XXXX代表一个**十六进制整数**。如： \u000a 表示 \n

char类型是可以进行运算的，因为它都对应有Unicode码  

![image-20220117154857995](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220117154857995-16652942700744.png)

> **了解： ASCII 码**
>
> 在计算机内部， 所有数据都使用二进制表示。 每一个二进制位（bit） 有 0 和 1 两种状态，因此 8 个二进制位就可以组合出 256 种状态， 这被称为一个字节（byte）。 一个字节一共可以用来表示 256 种不同的状态， 每一个状态对应一个符号， 就是 256 个符号， 从0000000 到 11111111。
>
> ASCII码： 上个世纪60年代， 美国制定了一套字符编码， 对英语字符与二进制位之间的关系， 做了统一规定。 这被称为ASCII码。 ASCII码一共规定了128个字符的编码， 比如空格“SPACE”是32（二进制00100000）， 大写的字母A是65（二进制01000001）。 这128个符号（包括32个不能打印出来的控制符号）， 只占用了一个字节的后面7位， **最前面的1位统一规定为0**。
>
> 缺点：
>
> - 不能表示所有字符。
> - 相同的编码表示的字符不一样： 比如， 130在法语编码中代表了é， 在希伯来语编码中却代表
>   了字母Gimel   
>
> **了解： Unicode 编码**
>
> 乱码：世界上存在着多种编码方式，同一个二进制数字可以被解释成不同的符号。因此，要想打开一个文本文件，就必须知道它的编码方式，否则用错误的编码方式解读，就会出现乱码。
>
> Unicode： 一种编码，将世界上所有的符号都纳入其中。每一个符号都给予一个独一无二的编码，使用 Unicode 没有乱码的问题。
>
> Unicode 的缺点： 
>
> Unicode 只规定了符号的二进制代码，却没有规定这个二进制代码应该如何存储：无法区别Unicode 和 ASCII：计算机无法区分三个字节表示一个符号还是分别表示三个符号。另外， 我们知道，英文字母只用一个字节表示就够了，如果unicode统一规定，每个符号用三个或四个字节表示，那么每个英文字母前都必然有二到三个字节是0，这对于存储空间来说是极大的浪费。  
>
> **了解： UTF-8**
>
> UTF-8 是在互联网上使用最广的一种 Unicode 的实现方式。
>
> UTF-8 是一种变长的编码方式。它可以使用 1-6 个字节表示一个符号，根据不同的符号而变化字节长度。
>
> UTF-8的编码规则：
>
> - 对于单字节的UTF-8编码，该字节的最高位为0，其余7位用来对字符进行编码（等同于ASCII码）。
> - 对于多字节的UTF-8编码，如果编码包含 n 个字节，那么第一个字节的前 n 位为1，第一个字节的第 n+1 位为0，该字节的剩余各位用来对字符进行编码。在第一个字节之后的所有的字节，都是最高两位为"10"，其余6位用来对字符进行编码。  



### 布尔类型

boolean 类型用来判断逻辑条件，一般用于程序流程控制：

- if条件控制语句；
- while循环控制语句；
- do-while循环控制语句；
- for循环控制语句；

boolean类型数据只允许取值true和false，无null。

**不可以使用0或非 0 的整数替代false和true，这点和C语言不同**。

Java虚拟机中没有任何供boolean值专用的字节码指令， Java语言表达所操作的boolean值，在编译之后都使用Java虚拟机中的int数据类型来代替： true用1表示， false用0表示。  



### 字符串类型

String**不是基本数据类型**，属于引用数据类型

声明String时，使用`" "`，使用方式与基本数据类型一致。例如： `String str = “abcd”;`

一个字符串可以串接另一个字符串，也可以直接串接其他类型的数据。例如：  

- 当“+”的两端有String时，为连接符
- 当两端都不是String时，为加法
- 当＋两端为字符时，变为ASCII码数字相加

```java
int no = 10;
String str = "abcdef";
String str1 = str + "xyz" + no;

str1 = str1 + "123";
char c = '国';//里面的字符数有且仅有1个，而字符串可以为0个

double pi = 3.1416;
str1 = str1 + pi;

boolean b = false;
str1 = str1 + b;
str1 = str1 + c;

System.out.println("str1 = " + str1);
```



如果要表示多行字符串，使用+号连接会非常不方便：

```java
String s = "first line \n"
         + "second line \n"
         + "end";
```

从Java 13开始，字符串可以用`"""..."""`表示多行字符串（Text Blocks）：

```java
// 多行字符串
public class Main {
    public static void main(String[] args) {
        String s = """
                   SELECT * FROM
                     users
                   WHERE id > 100
                   ORDER BY name DESC
                   """;
        System.out.println(s);
    }
}
```

上述多行字符串实际上是5行，在最后一个`DESC`后面还有一个`\n`。如果不想在字符串末尾加一个`\n`，就需要这么写：

```java
String s = """ 
           SELECT * FROM
             users
           WHERE id > 100
           ORDER BY name DESC""";
```

还需要注意到，多行字符串前面共同的空格会被去掉，即：

```java
String s = """
...........SELECT * FROM
...........  users
...........WHERE id > 100
...........ORDER BY name DESC
...........""";
```

用`.`标注的空格都会被去掉。

如果多行字符串的排版不规则，那么，去掉的空格就会变成这样：

```java
String s = """
.........  SELECT * FROM
.........    users
.........WHERE id > 100
.........  ORDER BY name DESC
.........  """;
```

即总是以最短的行首空格为基准。



### 变量的作用范围

在Java中，多行语句用`{ }`括起来。很多控制语句，例如条件判断和循环，都以{ }作为它们自身的范围，只要正确地嵌套这些`{ }`，编译器就能识别出语句块的开始和结束。而在语句块中定义的变量，它有一个作用域，就是从定义处开始，到语句块结束。超出了作用域引用这些变量，编译器会报错。举个例子：

```java
{
    ...
    int i = 0; // 变量i从这里开始定义
    ...
    {
        ...
        int x = 1; // 变量x从这里开始定义
        ...
        {
            ...
            String s = "hello"; // 变量s从这里开始定义
            ...
        } // 变量s作用域到此结束
        ...
        // 注意，这是一个新的变量s，它和上面的变量同名，
        // 但是因为作用域不同，它们是两个不同的变量:
        String s = "hi";
        ...
    } // 变量x和s作用域到此结束
    ...
} // 变量i作用域到此结束
```

定义变量时，要遵循作用域最小化原则，尽量将变量定义在尽可能小的作用域，并且，不要重复使用变量名。



### 基本数据类型转换

**自动类型提升：容量小的类型自动转换为容量大的数据类型。**

容量大小指的是表示数的范围大小

数据类型按容量大小排序为：  

![image-20220117161441567](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220117161441567-16652942700755.png)

有多种类型的数据混合运算时，系统首先自动将所有数据转换成**容量最大的**那种数据类型，然后再进行计算。

**byte,short,char之间不会相互转换，他们三者在计算时首先转换为int类型**

**boolean类型不能与其它数据类型运算**

当把**任何基本数据类型的值和字符串(String)进行连接运算时(+)， 基本数据类型的值将自动转化为字符串(String）类型**。  



**强制类型转换：自动类型提升的逆运算，可能导致精度损失**

自动类型转换的逆过程， 将容量大的数据类型转换为容量小的数据类型。 使用时要加上强制转换符： `()`

```java
double d1=12.3;
int i1=(int)d1;//截断操作，精度损失
int i2=128;
byte b=(byte)i2//结果为-128，也属于精度损失

long l1=123;
short s1=(short)l1;//没有精度损失
```

通常， 字符串不能直接转换为基本类型， 但通过基本类型对应的包装类则可以实现把字符串转换成基本类型。

如： `String a = “43”; int i = Integer.parseInt(a);`

boolean类型不可以转换为其它的数据类型。  

两个编码情况：

```java
//情况1
long l=1234;
System.out.println(l);//此时正常输出，右边没加l,默认右边为int，再自动提升为long
long l1=1234567890;
system.out.print(l1);//此时右边超过int表示范围，报错

//情况2
float f1=12.3;//编译失败，右边默认为double，大转小，失败
```



### var关键字

有些时候，类型的名字太长，写起来比较麻烦。例如：

```java
StringBuilder sb = new StringBuilder();
```

这个时候，如果想省略变量类型，可以使用`var`关键字：

```java
var sb = new StringBuilder();
```

编译器会根据赋值语句自动推断出变量`sb`的类型是`StringBuilder`。对编译器来说，语句：

```java
var sb = new StringBuilder();
```

实际上会自动变成：

```java
StringBuilder sb = new StringBuilder();
```

因此，使用`var`定义变量，仅仅是少写了变量类型而已。



## 数据运算

运算符是一种特殊的符号，用以表示数据的运算、赋值和比较等  

- 算术运算符
- 赋值运算符
- 比较运算符（关系运算符）
- 逻辑运算符
- 位运算符
- 三元运算符  



### 算术运算符

| 运算符  | 运算                                                | 范例                      | 结果                     |
| ------- | --------------------------------------------------- | ------------------------- | ------------------------ |
| +       | 正号                                                | +3                        | 3                        |
| -       | 负号                                                | b=4; -b                   | -4                       |
| +       | 加                                                  | 5+5                       | 10                       |
| -       | 减                                                  | 6-4                       | 2                        |
| *       | 乘                                                  | 3*4                       | 12                       |
| /       | 除                                                  | 5/5                       | 1                        |
| %       | 取模(取余)                                          | 7%5                       | 2                        |
| ++ ++   | 自增（前）：先自增后取值   自增（后）：先取值后自增 | a=2;b=++a;<br/>a=2;b=a++; | **a=3;b=3 <br/>a=3;b=2** |
| - - - - | 自减（前）：先自减后取值 自减（后）：先取值后自减   | a=2;b=- -a a=2;b=a- -     | a=1;b=1 a=1;b=2          |
| +       | 字符串连接                                          | “He”+”llo”                | “Hello”                  |



### 赋值运算符  

符号： =。当“=”两侧数据类型不一致时， 可以使用自动类型转换或使用强制类型转换原则进行处理。支持连续赋值。

扩展赋值运算符： +=, -=, *=, /=, %  

```java
public class Compute{
    public static void main(String[] args){
		short s = 3;
		//s = s+2;//编译无法通过
        short t = 3;
        t += 2;//不会改变变量本身的数据类型，编译可以通过
 		System.out.println(s);
        System.out.println(t);
        
        int i = 1;
        i *= 0.1;//数据类型还是整型，因此i为0
        System.out.println(i);//
        i++;
        System.out.println(i);//
        
        int m = 2;
        int n = 3;
        n *= m++;//先取值m=2，后自增运算m++
        System.out.println("m=" + m);
        System.out.println("n=" + n);
        
        int n = 10;
        n += (n++) + (++n);
        System.out.println(n);
    }
}
//运行结果:3 5 0 1 m=3 n=6 32
```



### 比较运算符  

| 运算符     | 运算                 范例             结果          |
| ---------- | --------------------------------------------------- |
| ==         | 相等于             4==3            false            |
| !=         | 不等于             4!=3              true           |
| <          | 小于                  4<3              false        |
| >          | 大于                  4>3              true         |
| <=         | 小于等于          4<=3            false             |
| >=         | 大于等于          4>=3             true             |
| instanceof | 检查是否是类的对象  “Hello” instanceof String  true |

- 比较运算符的结果都是boolean型，也就是要么是true，要么是false
- 比较运算符“==”不能误写成“=”   



### 逻辑运算符  

&逻辑与        | 逻辑或       ！ 逻辑非
&& 短路与    || 短路或     ^ 逻辑异或  

| a     | b     | a&b   | a&&b  | a\|b  | a\|\|b | !a    | a^b   |
| ----- | ----- | ----- | ----- | ----- | ------ | ----- | ----- |
| true  | true  | true  | true  | true  | true   | false | false |
| true  | false | false | false | true  | true   | false | true  |
| false | true  | false | false | true  | true   | true  | true  |
| false | false | false | false | false | false  | true  | false |

逻辑运算符用于连接布尔型表达式，在Java中不可以写成3<x<6，应该写成x>3 & x<6  

“&”和“&&”的区别：

- 单&时，左边无论真假，右边都进行运算；
- 双&时，如果左边为真，右边参与运算，如果左边为假，那么右边不参与运算

“|”和“||”的区别同理， ||表示：当左边为真，右边不参与运算  

异或( ^ )与或( | )的不同之处是：当左右都为true时，结果为false。



### 位运算符  

位运算是**直接对整数的二进制位**进行的运算  

位运算操作的都是整型数据

| 位运算符 |            |                              |
| -------- | ---------- | ---------------------------- |
| 运算符   | 运算       | 范例                         |
| <<       | 左移       | 3 << 2 = 12 --> 3 * 2 * 2=12 |
| >>       | 右移       | 3 >> 1 = 1 --> 3/2=1         |
| >>>      | 无符号右移 | 3 >>> 1 = 1 --> 3/2=1        |
| &        | 与运算     | 6 & 3 = 2                    |
| \|       | 或运算     | 6 \| 3 = 7                   |
| ^        | 异或运算   | 6 ^ 3 = 5                    |
| ~        | 取反运算   | ~6 = -7                      |

细节处理：

| 位运算符的细节 |                                                              |
| -------------- | ------------------------------------------------------------ |
| <<             | 空位补0，被移除的高位丢弃，空缺位补0。                       |
| >>             | 被移位的二进制最高位是0，右移后，空缺位补0； 最高位是1，空缺位补1。 |
| >>>            | 被移位二进制最高位无论是0或者是1，空缺位都用0补。            |
| &              | 二进制位进行&运算，只有1&1时结果是1，否则是0;                |
| \|             | 二进制位进行 \| 运算，只有0 \| 0时结果是0，否则是1;          |
| ^              | 相同二进制位进行 ^ 运算，结果是0； 1^1=0 , 0^0=0 不相同二进制位 ^ 运算结果是1。 1^0=1 , 0^1=1 |
| ~              | 正数取反，各二进制码按补码各位取反    负数取反，各二进制码按补码各位取反 |



### 三元运算符

格式：`(条件表达式)?表达式1：表达式2；  `

条件表达式的结果为boolean变量，条件表达式的结果：

- 为true， 运算后的结果是表达式1；
- 为false， 运算后的结果是表达式2；  

**表达式1和表达式2为同种类型**

三元运算符与if-else的联系与区别：

- 三元运算符可简化if-else语句
- 三元运算符要求必须返回一个结果。
- if后的代码块可有多个语句  



### 运算符的优先级  

运算符有不同的优先级，所谓优先级就是表达式运算中的运算顺序。如右表，**上一行运算符总优先于下一行**。

只有单目运算符、三元运算符、赋值运算符是从右向左运算的  

|      | .   ()   {}   ;   ,      |
| ---- | ------------------------ |
| R—>L | ++  --  ~  !(data type)  |
| L—>R | *  /  %                  |
| L—>R | +  -                     |
| L—>R | <<  >>  >>>              |
| L—>R | <  >  <=  >=  instanceof |
| L—>R | ==  !=                   |
| L—>R | &                        |
| L—>R | ^                        |
| L—>R | \|                       |
| L—>R | &&                       |
| L—>R | \|\|                     |
| R—>L | ? :                      |
| R—>L | =  *=  /=  %=            |
|      | +=  -=  <<=  >>=         |
|      | >>>=  &=  ^=  \|=        |



## 流程控制

流程控制语句是用来控制程序中各语句执行顺序的语句，可以把语句组合成能完成一定功能的小逻辑模块  

其流程控制方式采用结构化程序设计中规定的三种基本流程结构，即：

- 顺序结构：程序从上到下逐行地执行，中间没有任何判断和跳转。  
- 分支结构：根据条件，选择性地执行某段代码。有if…else和switch-case两种分支语句  
- 循环结构  ：根据循环条件，重复性的执行某段代码。有while、 do…while、 for三种循环语句  

### 输入与输出

在前面的代码中，总是使用`System.out.println()`来向屏幕输出一些内容。

`println`是print line的缩写，表示输出并换行。因此，如果输出后不想换行，可以用`print()`：

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("A,");
        System.out.print("B,");
        System.out.print("C.");
        System.out.println();
        System.out.println("END");
    }
}
```



如果要把数据显示成期望的格式，就需要使用格式化输出的功能。

格式化输出使用`System.out.printf()`，通过使用占位符`%?`，`printf()`可以把后面的参数格式化成指定格式：

```java
// 格式化输出
public class Main {
    public static void main(String[] args) {
        double d = 3.1415926;
        System.out.printf("%.2f\n", d); // 显示两位小数3.14
        System.out.printf("%.4f\n", d); // 显示4位小数3.1416
    }
}
```

Java的格式化功能提供了多种占位符，可以把各种数据类型“格式化”成指定的字符串：

| 占位符 | 说明                             |
| :----- | :------------------------------- |
| %d     | 格式化输出整数                   |
| %x     | 格式化输出十六进制整数           |
| %f     | 格式化输出浮点数                 |
| %e     | 格式化输出科学计数法表示的浮点数 |
| %s     | 格式化字符串                     |

注意，由于%表示占位符，因此，连续两个%%表示一个%字符本身。

占位符本身还可以有更详细的格式化参数。下面的例子把一个整数格式化成十六进制，并用0补足8位：

```java
// 格式化输出
public class Main {
    public static void main(String[] args) {
        int n = 12345000;
        System.out.printf("n=%d, hex=%08x", n, n); // 注意，两个%占位符必须传入两个数
    }
}
```



和输出相比，Java的输入就要复杂得多。

从键盘获取不同类型的变量：需要使用Scanner类

1. 导包：`import java.util.Scanner`
2. Scanner的实例化
3. 调用Scanner类的相关方法，获取指定类型的变量

```java
import java.util.Scanner;//1.导包

public class ScannerTest{
    public static void main(String[] args){
        Scanner scan=new Scanner(System.in);//2.实例化
        
        //3.调用Scanner类相关方法
        String name=scan.next();
        
        String gender=scan.next();
        char genderChar=gender.charAt(0);//获取索引为0位置上的字符
        
        int age=scan.nextInt();

        double weight=scan.nextDouble();

        boolean isLove=scan.nextBoolean();
    }
}    
```



### if-else结构

格式1

```java
if(条件表达式){
	执行代码块；
}
```

格式2

```java
if(条件表达式){
	执行代码块1;
}
else{
	执行代码块2;
}
```

格式3

```java
if(条件表达式1){
	执行代码块1;
}
else if (条件表达式2){
	执行代码块2;
}
……
else{
	执行代码块n;
}
```

使用说明

- 条件表达式必须是布尔表达式（关系表达式或逻辑表达式）、布尔变量
- 语句块只有一条执行语句时，一对{}可以省略，但建议保留
- if-else语句结构，根据需要可以嵌套使用
- 当if-else结构是“多选一”时，最后的else是可选的，根据需要可以省略
- 当多个条件是“互斥”关系时，条件判断语句及执行语句间顺序无所谓
- 当多个条件是“包含”关系时，“小上大下 / 子上父下”  



### switch-case结构

```java
switch(表达式){
case 常量1:
	语句1;
	// break;
case 常量2:
	语句2;
	// break;
… …
case 常量N:
	语句N;
	// break;
default:
	语句;
	// break;
}
```

- switch(表达式)中表达式的值必须是下述几种类型之一： **byte， short，char， int， 枚举 (jdk 5.0)， String (jdk 7.0)；**
- case子句中的值必须是**常量**，不能是变量名或不确定的表达式值；
- 同一个switch语句，所有case子句中的常量值互不相同；
- break语句用来在执行完一个case分支后使程序跳出switch语句块；**如果没有break，程序会顺序执行到switch结尾**
- default子句是可任选的。同时，**位置也是灵活的**。当没有匹配的case时，执行default  

例题：编写程序：从键盘上输入2019年的“month”和“day”，要求通过程序输出输入的日期为2019年的第几天  

```java
import java.util.Scanner;
class DayNumber{
    public static void main(String[] args){
        Scanner scan=new Scanner(System.in);
        System.out.println("请输入2019的month：");
        int month=scan.nextInt();
        System.out.println("请输入2019的day：");
        int day=scan.nextInt();
        
        //在没有break的情况下，会将case后续所有的天数加进去
        int sumDays=0;
        switch(month){
        case 12:
                sumDays+=31;
        case 11:
                sumDays+=30;
                ......
        case 1:
                sumDays+=day;
        }
        System.out.println("2019年"+month+"月"+day+"日是第"+sumDays+"天");
    }
}
```



**switch和if语句的对比**

- 如果判断的具体数值不多，而且符合byte、 short 、 char、 int、 String、枚举等几种类型。虽然两个语句都可以使用，建议使用swtich语句。因为效率稍高。
- 其他情况：对区间判断，对结果为boolean类型判断，使用if， if的使用范围更广。也就是说， 使用switch-case的，都可以改写为if-else。反之不成立  



### 循环结构

在某些条件满足的情况下，反复执行特定代码的功能  

- for 循环
- while 循环
- do-while 循环  

循环语句的四个组成部分

- 初始化部分(init_statement)
- 循环条件部分(test_exp)
- 循环体部分(body_statement)
- 迭代部分(alter_statement)  

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220120151503765-16652942700756.png" alt="image-20220120151503765" style="zoom:50%;" />

### for循环

语法格式

```java
for (①初始化部分; ②循环条件部分; ④迭代部分)｛
	③循环体部分;
｝
```

执行过程：

①-②-③-④-②-③-④-②-③-④-.....-②

说明：

②循环条件部分为boolean类型表达式，当值为false时，退出循环

①初始化部分可以声明多个变量，但**必须是同一个类型**，用逗号分隔

④可以有**多个变量更新，用逗号分隔**  

例题

编写程序从1循环到150，并在每行打印一个值，另外在每个3的倍数行上打印出“foo”,在每个5的倍数行上打印“biz”,在每个7的倍数行上打印出“baz”  

```java
class ForTest{
    public static void main(String[] args){
        for(int i=1;i<=150;i++){
            System.out.print(i+" ")
            if(i % 3==0){
                System.out.print("foo ");
            }
            if(i % 5==0){
                System.out.print("biz ");
            }
            if(i % 7==0){
                System.out.print("baz");
            }
            System.out.println();
        }
    }
}
```

### while循环

语法格式

```java
①初始化部分
while(②循环条件部分)｛
	③循环体部分;
	④迭代部分;
}
```

执行过程：
①-②-③-④-②-③-④-②-③-④-...-②

说明：

- 不要忘记声明④迭代部分，否则循环将不能结束， 变成死循环。
- for循环和while循环可以相互转换  

```java
public class WhileLoop {
	public static void main(String args[]) {
        int result = 0;
        int i = 1;
        while (i <= 100) {
            result += i;
            i++;
        }
        System.out.println("result=" + result);
	}
}
```

最简单“无限” 循环格式：` while(true)` , `for(;;)`,无限循环存在的原因是并不知道循环多少次， 需要根据循环体内部某些条件，来控制循环的结束  

### do-while循环  

语法格式

```java
①初始化部分;
do{
    ③循环体部分
    ④迭代部分
}while(②循环条件部分);
```

执行过程：

①-③-④-②-③-④-②-③-④-...②

**do-while循环至少执行一次循环体**  

```java
public class DoWhileLoop {
	public static void main(String args[]) {
		int result = 0, i = 1;
		do {
			result += i;
			i++;
		} while (i <= 100);
		System.out.println("result=" + result);
	}
}  
```



### 嵌套循环

将一个循环放在另一个循环体内，就形成了嵌套循环。其中，for ,while ,do…while均可以作为外层循环或内层循环。

实质上，嵌套循环就是把内层循环当成外层循环的循环体。当只有内层循环的循环条件为false时，才会**完全跳出内层循环，才可结束外层的当次循环**，开始下一次的循环。设外层循环次数为m次，内层为n次，则内层循环体实际上需要执行m*n次。  

例题：九九乘法表的实现

```java
class NineNineTable{
    public static void main(String[] args){
        for(int i=1;i<=9;i++){
            for(int j=1;j<=i;j++){
                System.out.print(i+"*"+j+"="+i*j+" ");
            }
            System.out.println();
        }
    }
}
```



### break与continue

break 语句用于终止某个语句块的执行，默认是包裹此关键字最近的一层循环

```java
{ ……
	break;
	……
}
```

break语句出现在多层嵌套的语句块中时，可以通过标签指明要终止的是哪一层语句块  

```java
label1: { ……
label2: 	{ ……
label3: 		{ ……
					break label2;
					……
				}
			}
		}
```



continue只能使用在循环结构中，用于跳过其所在循环语句块的**一次执行，继续下一次循环**。continue语句出现在多层嵌套的循环语句体中时，可以通过标签指明要跳过的是哪一层循环  

return：并非专门用于结束循环的，它的功能是结束一个方法。当一个方法执行到一个return语句时，这个方法将被结束。与break和continue不同的是， **return直接结束整个方法，不管这个return处于多少层循环之内**  

使用注意：

- break只能用于switch语句和循环语句中。
- continue 只能用于循环语句中。
- 二者功能类似，但continue是终止本次循环， break是终止本层循环。
- break、 continue之后不能有其他的语句，因为程序永远不会执行其后的语句。
- 标号语句必须紧接在循环的头部。标号语句不能用在非循环语句的前面。
- 很多语言都有goto语句， goto语句可以随意将控制转移到程序中的任意一条语句上，然后执行它。但使程序容易出错。 Java中的break和continue是不同于goto的  。



## 数组

数组(Array)， 是多个相同类型数据按一定顺序排列的集合， 并使用一个名字命名， 并通过编号的方式对这些数据进行统一管理。

数组的常见概念

- 数组名
- 下标(或索引)
- 元素
- 数组的长度 （元素个数） 

数组本身是**引用数据类型**， 而数组中的**元素可以是任何数据类型**， 包括基本数据类型和引用数据类型（可以是String）。

创建数组对象会在内存中开辟一整块**连续的**空间， 而数组名中引用的是**这块连续空间的首地址**。数组的长度一旦确定， 就不能修改。

数组元素是有序的，可以直接通过下标(或索引)的方式调用指定位置的元素， 速度很快。

数组的分类：

- 按照维度：一维数组、 二维数组、 三维数组、 …
- 按照元素的数据类型分：基本数据类型元素的数组、 引用数据类型元素的数组(即对象数组)  



### 一维数组

#### 声明方式

`type var[] `或 `type[] var；`

例如：

```java
int a[];
int[] a1;
double b[];
String[] c; //引用类型变量数组
```

Java语言中**声明数组时不能指定其长度**(数组中元素的数)， 例如：` int a[5]; //非法  `



#### 初始化

静态初始化： 在定义数组的同时就为数组元素分配空间并赋值。  

```java
int arr[] = new int[]{ 3, 9, 8};
int[] arr = {3,9,8};//声明与初始化在一行时，new int[]可以被省略，称为类型推断

String names[] = {“李四光”,“茅以升” ,“华罗庚”}
```

动态初始化： 数组声明且为数组元素**分配空间与赋值的操作分开进行**  

```java
int[] arr = new int[3];
arr[0] = 3;
arr[1] = 9;
arr[2] = 8;

String names[];
names = new String[3];
names[0] = “钱学森”;
names[1] = “邓稼先”;
names[2] = “袁隆平”;
```



#### 元素的引用

定义并用运算符new为之分配空间后，才可以引用数组中的每个元素；

数组元素的引用方式：`数组名[数组元素下标]`

- 数组元素下标可以是整型常量或整型表达式。如`a[3] , b[i] , c[6*i];`
- 数组元素下标从0开始；长度为n的数组合法下标取值范围: `0 —>n-1`； 如`int a[]=new int[3]`; 可引用的数组元素为`a[0]、 a[1]、 a[2]`

每个数组都有一个属性length指明它的长度，例如： `a.length` 指明数组a的长度(元素个数)。数组一旦初始化，其长度是不可变的  



#### 元素的默认初始化值  

数组是引用类型，它的元素相当于类的成员变量，因此数组一经分配空间，其中的每个元素也被按照成员变量同样的方式被隐式初始化。

- 对于基本数据类型而言，默认初始化值各有不同
- 对于引用数据类型而言，默认初始化值为null(注意与0不同！ )  

| 数组元素类型 | 元素默认初始值              |
| ------------ | --------------------------- |
| byte         | 0                           |
| short        | 0                           |
| int          | 0                           |
| long         | 0L                          |
| float        | 0.0F                        |
| double       | 0.0                         |
| char         | 0 或写为:’\u0000’(表现为空) |
| boolean      | false                       |
| 引用类型     | null                        |



#### 数组内存解析

```java
int[] arr = new int[]{1,2,3};
String[] arr1 = new String[4];
arr1[1] = “刘德华”;
arr1[2] = “张学友”;
arr1 = new String[3];
sysout(arr1[1]);//null
```

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220121142233311-16652942700757.png" alt="image-20220121142233311" style="zoom: 50%;" />

左边为**栈**（`stack`），存放地址

右边为**堆**，存放`new`出来的结构：对象、数组  

如果使用语句`System.out.println(arr);`，**得到的是地址而不是数组**



### 多维数组

如果说可以把一维数组当成几何中的线性图形，那么二维数组就相当于是一个表格。对于二维数组的理解，可以看成是一维数组`array1`又作为另一个一维数组`array2`的元素。其实， **从数组底层的运行机制来看，其实没有多维数组**。  

#### 初始化

**静态初始化** ： `int[][] arr = new int[][]{{3,8,2},{2,7},{9,0,1,6}};`

定义一个名称为`arr`的二维数组，**二维数组中有三个一维数组** ，每一个一维数组中具体元素也都已初始化 

- 第一个一维数组 `arr[0] = {3,8,2};` 
- 第二个一维数组 `arr[1] = {2,7};` 
- 第三个一维数组 `arr[2] = {9,0,1,6};` 
- 二维数组`arr`的长度`arr.length`为3
- 第三个一维数组的长度表示方式： `arr[2].length;`

特殊写法情况： `int[] x,y[];`

- x是一维数组， y是二维数组
- Java中多维数组不必都是规则矩阵形式

**动态初始化1** ： `int[][] arr = new int[3][2];`

定义了名称为arr的二维数组，**二维数组中有3个一维数组，每一个一维数组中有2个元素** 

- 一维数组的名称分别为`arr[0], arr[1], arr[2]` 
- 给第一个一维数组1脚标位赋值为78写法是： `arr[0][1] = 78;`

**动态初始化2**： `int[][] arr = new int[3][];`

二维数组中有3个一维数组，每个一维数组都是**默认初始化值null** (注意：区别于格式1） 

- 可以对这个三个一维数组**分别进行初始化**
- `arr[0] = new int[3]; arr[1] = new int[1]; arr[2] = new int[2];` 
- `int[][]arr = new int[][3]; //非法`

#### **默认初始值**

针对初始化方法1

- 内层元素默认初始值：数据类型对应的一维默认初始值
- **外层元素默认初始值：地址值**

针对初始化方法2：

- 内层元素默认初始值：不能调用，否则报错
- 外层元素默认初始值：`null`



### Arrays工具类的使用  

java.util.Arrays类即为操作数组的工具类， 包含了用来操作数组（比如排序和搜索）的各种方法  

| 方法                                  | 作用                                   |
| ------------------------------------- | -------------------------------------- |
| boolean -`equals(int[] a,int[] b) `   | 判断两个数组是否相等。                 |
| String -`toString(int[] a) `          | 输出数组信息。                         |
| void -`fill(int[] a,int val) `        | 将指定值填充到数组之中。               |
| void -`sort(int[] a) `                | 对数组进行排序。                       |
| int -`binarySearch(int[] a,int key) ` | 对排序后的数组进行二分法检索指定的值。 |

```java
import java.util.Arrays
//1.判断是否相等
int[] arr1=new int[]{1,2,3,4};
int[] arr2=new int[]{1,3,2,4};
boolean isEqual=Arrays.equals(arr1,arr2);

//2.输出数组信息
System.out.println(Arrays.toString(arr1));

//3.将指定数值填充到数组中
Arrays.fill(arr1,10);

//4.对数组进行排序
Array.sort(arr2);

//5.对排序后的数组进行二分法检索
int[] arr3=new int[]{10,23,32,45,67};
int index=Arrays.binarySearch(arr3,210);
if(index>=0){
    System.out.println(index)
}else{
    System.out.println("未找到")//索引为负数时表示未找到
}
```



# 面向对象

面向过程(POP) 与 面向对象(OOP)：二者都是一种思想，面向对象是相对于面向过程而言的。

- 面向过程， 强调的是功能行为，以函数为最小单位，考虑怎么做。 
- 面向对象，**将功能封装进对象， 强调具备了功能的对象，以类/对象为最小单位，考虑谁来做**。

面向对象更加强调运用人类在日常的思维逻辑中采用的思想方法与原则，如抽象、分类、继承、聚合、多态等。

面向对象的三大特征

- **封装 (Encapsulation)**
- **继承 (Inheritance)**
- **多态 (Polymorphism)**  

面向对象分析方法分析问题的思路和步骤：

- 根据问题需要，选择问题所针对的现实世界中的实体。
- 从实体中寻找解决问题相关的属性和功能，这些属性和功能就形成了概念世界中的类。
- 把抽象的实体用计算机语言进行描述， 形成计算机世界中类的定义。即借助某种程序语言，把类构造成计算机能够识别和处理的数据结构。
- 将类实例化成计算机世界中的对象。对象是计算机世界中解决问题的最终工具  



## 类及类的成员  

类(Class)和对象(Object)是面向对象的核心概念。

- 类是对一类事物的描述，是抽象的、概念上的定义
- 对象是实际存在的**该类事物的每个个体**，因而也称为实例(instance)。
- “万事万物皆对象”  

可以理解为： 类 = 抽象概念的人； 对象 = 实实在在的某个人

面向对象程序设计的重点是类的设计，类的设计， 其实就是**类的成员的设计**  

常见的**类的成员**有：

- 属性：对应类中的**成员变量**；Field = 属性 = 成员变量  
- 行为：对应类中的成员方法；Method = 成员方法 = 函数      



### 对象的创建与使用

java类的实例化，即创建类的对象，一般有三个步骤 

**1.创建Java自定义类**

- 定义类（考虑修饰符、类名）
- 编写类的属性（考虑修饰符、属性类型、属性名、 初始化值）
- 编写类的方法（考虑修饰符、返回值类型、方法名、形参等）

定义类的语法格式  

```java
修饰符 class 类名 {
	属性声明;
	方法声明;
}
```

说明：修饰符public：类可以被任意访问；类的正文要用{ }括起来

**2.创建对象语法**： `类名 对象名 = new 类名();`

**3.访问对象成员**：`对象名.对象成员`（包括属性和方法）  

```java
public class PersonTest{
    public static void main(String[] args){
        //2.创建Person类的对象=类的实例化
        Person p1=new Person();
        
        //3.调用对象的结构：属性、方法
        //(1)调用属性：对象.属性
        p1.name="韩金陵";
        p1.age=22;
        p1.isMale=true;//由于在类中已经为isHandsome赋值，因此此处可以不赋值
        System.out.println(p1.name);
        //(2)调用方法：对象.方法
        p1.eat();
        p1.sleep();
        p1.talk();  
    }
}

//1.创建类，设计类的成员
//(1)定义类
class Person{
    //(2)编写类的属性，或成员变量
    String name;
    int age;
    boolean isMale;
    boolean isHandsome=true;
    
    //(3)编写类的方法，或函数
    public void eat(){
        System.out.println(name+"在吃饭");
    }
    public void sleep(){
        System.out.println(name+"在睡觉");
    }
    public void talk(){
        System.out.println(name+"在说话");
    }
}
```

如果创建了一个类的多个对象，对于类中定义的属性，每个对象都拥有各自的一套类的属性（非static的），且互不干扰 



###  对象内存解析

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122094617050-16652942700758.png" alt="image-20220122094617050" style="zoom: 67%;" />

堆（ Heap）：此内存区域的唯一目的就是**存放对象实例**， 所有的对象实例以及数组都要在堆上分配

通常所说的栈（ Stack） ：是指虚拟机栈。 虚拟机栈用于**存储局部变量**等。局部变量表存放了编译期可知长度的各种基本数据类型（ boolean、 byte、char 、 short 、 int 、 float 、 long 、double） 、 对象引用（ reference类型，它不等同于对象本身， 是对象在堆内存的首地址） 。 方法执行完， 自动释放。

方法区（Method Area）：用于存储已被虚拟机加载的**类信息、 常量、 静态变量**、 即时编译器编译后的代码等数据。  



## 属性

属性：对应类中的**成员变量**

语法格式：`修饰符 数据类型 属性名 = 初始化值;`

- 修饰符—常用的权限修饰符： private、缺省、protected、 public；其他修饰符：(static、 final ，暂不考虑)
- 数据类型—任何基本数据类型(如int、 Boolean) 或任何引用数据类型。
- 属性名—属于标识符，符合命名规则和规范即可。  

变量的分类：成员变量与局部变量  

- 在**方法体外，类体内**声明的变量称为成员变量。
- 在**方法体内部**声明的变量称为局部变量。  

![image-20220122100146691](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122100146691-16652942700759.png)

成员变量与局部变量异同

同：变量的共同点，如定义格式、先声明后使用、有对应的作用域

异：

|              | 成员变量                            | 局部变量                                                     |
| ------------ | ----------------------------------- | ------------------------------------------------------------ |
| 声明的位置   | 直接声明在类中                      | 方法的形参或内部、代码块内、构造器内等                       |
| 修饰符       | private、 public、 static、 final等 | 不能用权限修饰符修饰，可以用final修饰                        |
| 初始化值     | 有默认初始化值                      | 没有默认初始化值，**必须显式赋值，方可使用**，特别的，**形参在调用时赋值** |
| 内存加载位置 | 堆空间或静态域内                    | 栈空间                                                       |



## 方法

方法(method、函数)：方法是类或对象**行为特征的抽象**，用来完成某个功能操作。在某些语言中也称为函数或过程。将功能封装为方法的目的是，可以实现代码重用，简化代码。Java里的方法不能独立存在，所有的方法必须定义在类里。  

### 方法的声明

```java
修饰符 返回值类型 方法名（参数类型 形参1, 参数类型 形参2, ….）｛
	方法体程序代码
	return 返回值;
｝  
```

修饰符： public、缺省、private、 protected等

返回值类型：

- 没有返回值： void。
- 有返回值，声明出返回值的类型。与方法体中“return 返回值” 搭配使用

方法名：属于标识符，命名时遵循标识符命名规则和规范，“见名知意”

形参列表：可以包含零个，一个或多个参数。多个参数时，中间用“,”隔开

返回值：方法在执行完毕后返还给调用它的程序的数据。  



### 方法的分类  

|        | 无返回值                     | 有返回值                             |
| ------ | ---------------------------- | ------------------------------------ |
| 无形参 | `void 方法名（） {}`         | `返回值的类型 方法名（） {}`         |
| 有形参 | `void 方法名（形参列表） {}` | `返回值的类型 方法名（形参列表） {}` |

```java
public void eat(){}//无返回值，无形参
public void sleep(int hour){}//无返回值，有形参
public String getName(){}//有返回值，无形参
public String getNation(String nation)//有返回值，有形参
```



### 方法的调用

方法通过方法名被调用，且只有被调用才会执行  

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122103803092-166529427007510.png" alt="image-20220122103803092" style="zoom: 67%;" />

注意：

- 方法被调用一次，就会执行一次
- 没有具体返回值的情况，返回值类型用关键字void表示，方法体中可以不必使用return语句。如果使用，仅用来结束方法。
- 定义方法时，方法的结果应该返回给调用者，交由调用者处理。
- 方法中只**能调用方法或属性**， 不可以在方法内部定义方法  

例题：利用面向对象的编程方法，设计类Circle计算圆的面积

```java
public class CircleTest{
    public static void main(String[] args){
        Circle c=new Circle();
        c.radius=2;
        double area=c.computeArea();//局部变量需要重新声明
        System.out.println(area);
    }
}
class Circle{
    double radius;
    public double computeArea(){
        double area=Math.PI*radius*radius;
        return area;
    }
}
```



### 匿名对象调用方法

可以不定义对象的对象名，而直接调用这个对象的方法。这样的对象叫做匿名对象。

如：`new Person().shout();`

使用情况

- 如果对一个对象只需要进行一次方法调用，那么就可以使用匿名对象。
- 经常将匿名对象作为实参传递给一个方法调用  

```Java
public class ObjectTest{
    public static void main(String[] args){
        //匿名对象
        new Phone().price=1999;
        new Phone().showPrice;//0.0
        PhoneMall mall=new PhoneMall();
        mall.show(new Phone());//此时PhoneMall中两方法调用的是同一对象
    }
}
class PhoneMall{
    public void show(Phone phone){
        phone.sendEmail();
        phone.playGame();
    }
}
class Phone{
    double price;
    public void sendEmail(){
        System.out.println("发送邮件");
    }
    public void playGame(){
        System.out.println("玩游戏");
    }
    public void showPrice(){
        System.out.println(price);
    }
}
```



### 方法的重载

概念：在同一个类中，**允许存在一个以上的同名方法**，只要它们的**参数个数或者参数类型不同**即可

特点：**与返回值类型无关，只看参数列表**，且参数列表必须不同。 (参数**个数或类型**)。调用时， 根据方法参数列表的不同来区别。

重载示例：

```java
//返回两个整数的和
int add(int x,int y){return x+y;}
//返回三个整数的和
int add(int x,int y,int z){return x+y+z;}
//返回两个小数的和
double add(double x,double y){return x+y;}
```

使用重载方法，可以为编程带来方便。

例如， `System.out.println()`方法就是典型的重载方法，其内部的声明形式如下：

```java
public void println(byte x)
public void println(short x)
public void println(int x)
public void println(long x)
public void println(float x)
public void println(double x)
public void println(char x)
public void println(double x)
public void println()
……  
```



### 可变个数形参

JavaSE 5.0 中提供了Varargs(variable number of arguments)机制，允许直接定义**能和多个实参相匹配的形参**。从而，可以用一种更简单的方式，来传递个数可变的实参  

- JDK 5.0以前： 采用数组形参来定义方法，传入多个同一类型变量
  `public static void test(int a ,String[] books);`
- JDK5.0： 采用可变个数形参来定义方法，传入多个同一类型变量
  `public static void test(int a ,String…books);`  

说明：

- 声明格式： `方法名(参数的类型名 ...参数名)`
- 可变参数：方法参数部分指定类型的参数个数是可变多个
- 可变个数形参的方法与本类中方法名相同、**形参个数不同**的方法之间构成重载
- 可变个数形参的方法与本类中方法名相同、**形参类型也相同的数组之间不构成重载**，即**新旧方法不能共存**
- 可变参数方法的使用与方法参数部分使用数组是一致的
- 方法的参数部分有**可变形参，需要放在形参声明的最后**
- 在一个方法的**形参位置，最多只能声明一个可变形参**  

```java
public class Test{
	public static void main(String[] args){
		TestOverload to = new TestOverload();
		//下面两次调用将执行第二个test方法
		to.test1();
		to.test1("aa" ,"bb");
		//下面将执行第一个test方法
		to.test(new String[]{"aa"});
		
	}
}	
class TestOverload{
	public void test(String[] msg){
		System.out.println("含字符串数组参数的test方法 ");
	}
	public void test1(String book){
		System.out.println("与可变形参方法构成重载的test1方法");
	}
	public void test1(String ... books){
		System.out.println("形参长度可变的test1");
	}
}
```



### 值传递机制  

关于变量赋值

- 如果变量是基本数据类型，此时赋值的是变量所保存的数据值
- 如果变量是引用数据类型，此时赋值的是变量所保存的数据的地址值

方法，必须由其所在类或对象调用才有意义。若方法含有参数：

- 形参：方法**声明时**的参数
- 实参：方法**调用时**实际传给形参的参数值

Java的实参值如何传入方法：

Java里方法的参数传递方式只有一种： **值传递**。 即将**实际参数值的副本**（复制品）传入方法内，而**参数本身不受影响**。

- 形参是**基本**数据类型：将实参基本数据类型变量的**“数据值”**传递给形参
- 形参是**引用**数据类型：将实参引用数据类型变量的**“地址值”**传递给形参



**基本数据类型**

```java
public static void main(String[] args) {
	int x = 5;
	System.out.println("修改之前x = " + x);// 5
	// x是实参
	change(x);
	System.out.println("修改之后x = " + x);// 5
}
public static void change(int x) {
	System.out.println("change:修改之前x = " + x);
	x = 3;
	System.out.println("change:修改之后x = " + x);
}
```

![image-20220122162850499](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122162850499-166529427007512.png)



**引用数据类型**

```java
public static void main(String[] args) {
	Person obj = new Person();
	obj.age = 5;
	System.out.println("修改之前age = " + obj.age);// 5
	change(obj);
	System.out.println("修改之后age = " + obj.age);// 3
}
public static void change(Person obj) {
    System.out.println("change:修改之前age = " + obj.age);
	obj.age = 3;
	System.out.println("change:修改之后age = " + obj.age);
}
class Person{
	int age;
}
```

![image-20220122163100116](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122163100116-166529427007513.png)

![image-20220122163108800](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122163108800-166529427007511.png)

```java
public static void main(String[] args) {
	Person obj = new Person();
	obj.age = 5;
	System.out.println("修改之前age = " + obj.age);// 5
	change(obj);
	System.out.println("修改之后age = " + obj.age);// 5
}
public static void change(Person obj) {
	obj = new Person();//相比较上个程序修改的地方，即新创建了一个对象
    System.out.println("change:修改之前age = " + obj.age);
	obj.age = 3;
	System.out.println("change:修改之后age = " + obj.age);
}
class Person{
	int age;
}
```

![image-20220122164757245](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122164757245-166529427007514.png)

![image-20220122164811820](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122164811820-166529427007615.png)

![image-20220122164830499](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122164830499-166529427007616.png)

![image-20220122164839729](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220122164839729-166529427007617.png)



例题1

定义一个int型的数组： `int[] arr = new int[]{12,3,3,34,56,77,432};`让数组的每个位置上的值去除以首位置的元素，得到的结果，作为该位置上的新值。遍历新的数组  

```java
//错误写法
for(int i= 0； i < arr.length;i++){
	arr[i] = arr[i] / arr[0];
}
//正确写法1
for(int i = arr.length – 1;i >= 0;i--){
	arr[i] = arr[i] / arr[0];
}
//正确写法2
int temp = arr[0];
for(int i= 0； i < arr.length;i++){
	arr[i] = arr[i] / temp;
}
```

例题2

```java
int[] arr = new int[10];
System.out.println(arr);//地址值

char[] arr1 = new char[]{'a','b','c'};
System.out.println(arr1); //abc
```



### 递归方法

递归方法：一个方法体内调用它自身。

- 方法递归包含了一种隐式的循环，它会重复执行某段代码，但这种重复执行无须循环控制。
- 递归一定要向已知方向递归，否则这种递归就变成了无穷递归，类似于死循环。

```java
//计算1-100之间所有自然数的和
public int sum(int num){
	if(num == 1){
		return 1;
	}else{
		return num + sum(num - 1);
	}
}  
```



## 封装性

### 封装的引入

程序设计追求“高内聚，低耦合”。

- 高内聚 ：类的内部数据操作细节自己完成，不允许外部干涉；
- 低耦合 ： 仅对外暴露少量的方法用于使用。

隐藏对象内部的复杂性，只对外公开简单的接口。便于外界调用，从而提高系统的可扩展性、可维护性。通俗的说， 把该隐藏的隐藏起来，该暴露的暴露出来。 这就是封装性的设计思想。  

使用者对类内部定义的属性(对象的成员变量)的直接操作会导致数据的错误、混乱或安全性问题 。Java中通过将数据**声明为私有的**(**private**)， 再提供公共的（ public）方法：`getXxx()`和`setXxx()`实现对该属性的操作， 以实现下述目的：

- 隐藏一个类中不需要对外提供的实现细节；
- 使用者只能通过事先定制好的方法来访问数据， 可以方便地加入控制逻辑，限制对属性的不合理操作；
- 便于修改， 增强代码的可维护性；

封装性体现：

- **属性私有**
- **方法私有**

```java
class Animal {
	private int legs;// 将属性legs定义为private，只能被Animal类内部访问
	public void setLegs(int i) { // 在这里定义方法 eat()和move()
		if (i != 0 && i != 2 && i != 4) {
			System.out.println("Wrong number of legs!");
			return;
		}
		legs = i;
	}
	public int getLegs() {
		return legs;
	}
}
public class Zoo {
	public static void main(String args[]) {
		Animal xb = new Animal();
		xb.setLegs(4); // xb.setLegs(-1000);
		//xb.legs = -1000; // 非法
		System.out.println(xb.getLegs());
	}
}
```



### 访问权限修饰符  

Java权限修饰符public、 protected、 (缺省)、 private置于类的成员定义前，用来限定对象对该类成员的访问权限。  

| 修饰符    | 类内部 | 同一个包 | 不同包的子类 | 同一个工程 |
| --------- | ------ | -------- | ------------ | ---------- |
| private   | Yes    |          |              |            |
| (缺省)    | Yes    | Yes      |              |            |
| protected | Yes    | Yes      | Yes          |            |
| public    | Yes    | Yes      | Yes          | Yes        |

对于class的权限修饰只可以用public和default(缺省)

- public类可以在任意地方被访问。
- default类只可以被同一个包内部的类访问。  



### JavaBean

在Java中，有很多`class`的定义都符合这样的规范：

- 若干`private`实例字段；
- 通过`public`方法来读写实例字段。

例如：

```java
public class Person {
    private String name;
    private int age;

    public String getName() { return this.name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return this.age; }
    public void setAge(int age) { this.age = age; }
}
```

如果读写方法符合以下这种命名规范：

```java
// 读方法:
public Type getXyz()
// 写方法:
public void setXyz(Type value)
```

那么这种`class`被称为`JavaBean`：



#### 属性的读写

上面的字段是`xyz`，那么读写方法名分别以`get`和`set`开头，并且后接大写字母开头的字段名`Xyz`，因此两个读写方法名分别是`getXyz()`和`setXyz()`。

`boolean`字段比较特殊，它的读方法一般命名为`isXyz()`：

```java
// 读方法:
public boolean isChild()
// 写方法:
public void setChild(boolean value)
```

通常把一组对应的读方法（`getter`）和写方法（`setter`）称为属性（`property`）。例如，`name`属性：

- 对应的读方法是`String getName()`
- 对应的写方法是`setName(String)`

只有`getter`的属性称为只读属性（read-only），例如，定义一个age只读属性：

- 对应的读方法是`int getAge()`
- 无对应的写方法`setAge(int)`

只有`setter`的属性称为只写属性（write-only）。只读属性很常见，只写属性不常见。

属性只需要定义`getter`和`setter`方法，不一定需要对应的字段。例如，`child`只读属性定义如下：

```java
public class Person {
    private String name;
    private int age;

    public String getName() { return this.name; }
    public void setName(String name) { this.name = name; }

    public int getAge() { return this.age; }
    public void setAge(int age) { this.age = age; }

    public boolean isChild() {
        return age <= 6;
    }
}
```

可以看出，`getter`和`setter`也是一种数据封装的方法。

JavaBean主要用来传递数据，即把一组数据组合成一个JavaBean便于传输。此外，JavaBean可以方便地被IDE工具分析，生成读写属性的代码，主要用在图形界面的可视化设计中。

通过IDE，可以快速生成`getter`和`setter`。



#### 枚举JavaBean属性

要枚举一个JavaBean的所有属性，可以直接使用Java核心库提供的`Introspector`：

```java
import java.beans.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BeanInfo info = Introspector.getBeanInfo(Person.class);
        for (PropertyDescriptor pd : info.getPropertyDescriptors()) {
            System.out.println(pd.getName());
            System.out.println("  " + pd.getReadMethod());
            System.out.println("  " + pd.getWriteMethod());
        }
    }
}

class Person {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

运行上述代码，可以列出所有的属性，以及对应的读写方法。注意`class`属性是从`Object`继承的`getClass()`方法带来的。



## 构造器

构造器的特征

- 它**具有与类相同的名称**
- 它不声明返回值类型(与声明为void不同)
- 不能被static、 final、 synchronized、 abstract、 native修饰，不能有return语句返回值  

构造器的作用： 

- **创建对象**
- **给对象进行初始化**

```Java
Order o = new Order(); 
Person p = new Person(“Peter”,15);
```

`Order()`与`Person("Peter",15)`都是构造器



### 语法格式

```java
修饰符 类名 (参数列表) {
	初始化语句；
}  
```

举例

```java
public class Animal {
	private int legs;
	// 构造器
	public Animal(int n) {
		legs = n;//初始化属性
	}
	public void setLegs(int i) {
		legs = i;
	}
	public int getLegs() {
		return legs;
	}
}
```

创建Animal类的实例： `Animal a = new Animal(4);`，调用构造器， 将legs初始化为4

根据参数不同，构造器可以分为如下两类：

- 隐式无参构造器（系统默认提供）
- 显式定义一个或多个构造器（无参、有参）

注 意：

- Java语言中，每个类都至少有一个构造器
- 默认构造器的修饰符与所属类的修饰符一致
- 一旦显式定义了构造器， 则系统不再提供默认构造器
- 一个类可以创建多个重载的构造器
- 父类的构造器不可被子类继承  



### 构造器重载

构造器一般用来创建对象的同时初始化对象

```java
class Person{
	String name;
	int age;
	public Person(String n , int a){
        name=n; age=a;
    }
} 
```

构造器重载使得对象的创建更加灵活，方便创建各种不同的对象。

构造器重载举例：

```java
public class Person{
	public Person(String name, int age, Date d){
        this(name,age);
        ......
    }
	public Person(String name, int age) {…}
	public Person(String name, Date d) {…}
	public Person(){…}
}
```

构造器重载，参数列表必须不同  



### 属性赋值

赋值的位置：

- ① 默认初始化
- ② 显式初始化
- ③ 构造器中初始化
- ④ 通过“对象.属性“或“对象.方法”的方式赋值

赋值的先后顺序：
① - ② - ③ - ④



### this关键字

this关键字的作用和其词义很接近。

- 它在方法内部使用，即这个方法**所属对象的引用**；
- 它在构造器内部使用，表示**该构造器正在初始化的对象**。

this 可以调用类的属性、方法和构造器

**当在方法内需要用到调用该方法的对象时，就用this。**

具体的：可以用this来区分属性和局部变量。比如： `this.name = name;`  

```java
class Person{ // 定义Person类
	private String name ;
	private int age ;
	public Person(String name,int age){
		this.name = name ;//this使得前面的name是属性，后面的name是形参，否则认为二者都是形参
		this.age = age ; 
    }
	public void getInfo(){
		System.out.println("姓名：" + name) ;
		this.speak();
	}
	public void speak(){
		System.out.println("年龄：" + this.age);
	}
}  
```

在任意方法或构造器内，如果使用当前类的成员变量或成员方法可以在其前面添加this，增强程序的阅读性。不过，通常省略this。

当**形参与成员变量同名**时，如果在方法内或构造器内需要使用成员变量，必须添加this来表明该变量是类的成员变量

使用this访问属性和方法时，如果**在本类中未找到，会从父类中查找**  

使用this调用本类的构造器  

```java
class Person{ // 定义Person类
	private String name ;
	private int age ;
	public Person(){ // 无参构造器
		System.out.println("新对象实例化") ;
	}
	public Person(String name){
		this(); // 调用本类中的无参构造器
		this.name = name ;
	}
	public Person(String name,int age){
		this(name) ; // 调用有一个参数的构造器
		this.age = age;
	}
	public String getInfo(){
		return "姓名： " + name + "，年龄： " + age ;
	}
}
```

this可以作为一个类中构造器相互调用的特殊格式  

注意：

- 可以在类的构造器中使用"`this(形参列表)`"的方式，调用**本类中重载的其他的构造器**
- 明确：构造器中**不能**通过"`this(形参列表)`"的方式**调用自身构造器**
- 如果一个类中声明了n个构造器，则最多有 n - 1个构造器中使用了"`this(形参列表)`"
- "`this(形参列表)`"必须**声明在类的构造器的首行**！
- 在类的一个构造器中，**最多只能声明一个**"`this(形参列表)`"  



## 包(package)

### 什么是包

问题引入：

- 如果小明写了一个`Person`类，小红也写了一个`Person`类，现在，小白既想用小明的`Person`，也想用小红的`Person`，怎么办？
- 如果小军写了一个`Arrays`类，恰好JDK也自带了一个`Arrays`类，如何解决类名冲突？

在Java中使用`package`来解决名字冲突：一个类总是属于某个包，类名（比如`Person`）只是一个简写，完整类名是`包名.类名`。

例如：

- 小明的`Person`类存放在包`ming`下面，因此，完整类名是`ming.Person`；
- 小军的`Arrays`类存放在包`mr.jun`下面，因此，完整类名是`mr.jun.Arrays`；
- JDK的`Arrays`类存放在包`java.util`下面，因此，完整类名是`java.util.Arrays`。

在定义`class`的时候，需要在第一行声明这个`class`属于哪个包，如小明的`Person.java`文件：

```Java
package ming; // 申明包名ming

public class Person {
}
```

在Java虚拟机执行的时候，JVM只看完整类名，只要包名不同，类就不同。没有定义包名的`class`，它使用的是默认包，非常容易引起名字冲突，因此，不推荐不写包名的做法。

包可以是多层结构，彼此用`.`隔开，如：`java.util`。

但包没有父子关系：`java.util`和`java.util.zip`是不同的包，两者没有任何继承关系。

我们还需要按照包结构把上面的Java文件组织起来。假设以`package_sample`作为根目录，`src`作为源码目录，那么所有文件结构就是：

```ascii
package_sample
└─ src
    ├─ hong
    │  └─ Person.java
    │  ming
    │  └─ Person.java
    └─ mr
       └─ jun
          └─ Arrays.java
```

即所有Java文件对应的目录层次要和包的层次一致。

编译后的`.class`文件也需要按照包结构存放。如果使用IDE，把编译后的`.class`文件放到`bin`目录下，那么，编译的文件结构就是：

```ascii
package_sample
└─ bin
   ├─ hong
   │  └─ Person.class
   │  ming
   │  └─ Person.class
   └─ mr
      └─ jun
         └─ Arrays.class
```

编译的命令相对比较复杂，需要在`src`目录下执行`javac`命令：

```shell
javac -d ../bin ming/Person.java hong/Person.java mr/jun/Arrays.java
```

在IDE中，会自动根据包结构编译所有Java源码，所以不必担心使用命令行编译的复杂命令。



### 包作用域

**位于同一个包的类，可以访问包作用域的字段和方法。**不用`public`、`protected`、`private`修饰的字段和方法就是包作用域。例如，`Person`类定义在`hello`包下面：

```java
package hello;

public class Person {
    // 包作用域:
    void hello() {
        System.out.println("Hello!");
    }
}
```

`Main`类也定义在`hello`包下面：

```java
package hello;

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.hello(); // 可以调用，因为Main和Person在同一个包
    }
}
```



### import

在一个`class`中，总会引用其他的`class`。

例如，小明的`ming.Person`类，如果要引用小军的`mr.jun.Arrays`类，有三种写法：

第一种，直接写出完整类名，例如：

```java
// Person.java
package ming;

public class Person {
    public void run() {
        mr.jun.Arrays arrays = new mr.jun.Arrays();
    }
}
```

第二种，用`import`语句导入小军的`Arrays`，然后写简单类名：

```java
// Person.java
package ming;

// 导入完整类名:
import mr.jun.Arrays;

public class Person {
    public void run() {
        Arrays arrays = new Arrays();
    }
}
```

在写`import`的时候，可以使用`*`，表示把这个包下面的所有`class`都导入进来**（但不包括子包的`class`）**：

```java
// Person.java
package ming;

// 导入mr.jun包的所有class:
import mr.jun.*;

public class Person {
    public void run() {
        Arrays arrays = new Arrays();
    }
}
```

一般不推荐这种写法，因为在导入了多个包后，很难看出`Arrays`类属于哪个包。



还有一种`import static`的语法，它可以导入可以导入一个类的静态字段和静态方法：

```java
package main;

// 导入System类的所有静态字段和静态方法:
import static java.lang.System.*;

public class Main {
    public static void main(String[] args) {
        // 相当于调用System.out.println(…)
        out.println("Hello, world!");
    }
}
```

`import static`很少使用。



Java编译器最终编译出的`.class`文件只使用完整类名，因此，在代码中，当编译器遇到一个`class`名称时：

- 如果是完整类名，就直接根据完整类名查找这个`class`；
- 如果是简单类名，按下面的顺序依次查找：
  - 查找当前`package`是否存在这个`class`；
  - 查找`import`的包是否包含这个`class`；
  - 查找`java.lang`包是否包含这个`class`。

如果按照上面的规则还无法确定类名，则编译报错。

```java
// Main.java
package test;

import java.text.Format;

public class Main {
    public static void main(String[] args) {
        java.util.List list; // ok，使用完整类名 -> java.util.List
        Format format = null; // ok，使用import的类 -> java.text.Format
        String s = "hi"; // ok，使用java.lang包的String -> java.lang.String
        System.out.println(s); // ok，使用java.lang包的System -> java.lang.System
        MessageFormat mf = null; // 编译错误：无法找到MessageFormat: MessageFormat cannot be resolved to a type
    }
}
```

因此，编写class的时候，编译器会自动帮我们做两个import动作：

- 默认自动`import`当前`package`的其他`class`；
- 默认自动`import java.lang.*`。

 注意：自动导入的是java.lang包，但类似java.lang.reflect这些包仍需要手动导入。

如果有两个`class`名称相同，例如，`mr.jun.Arrays`和`java.util.Arrays`，那么只能`import`其中一个，另一个必须写完整类名。



### 最佳实践

为了避免名字冲突，需要确定唯一的包名。推荐的做法是使用倒置的域名来确保唯一性。例如：

- org.apache
- org.apache.commons.log
- com.liaoxuefeng.sample

子包就可以根据功能自行命名。注意不要和`java.lang`包的类重名，即自己的类不要使用这些名字：

- String
- System
- Runtime
- ...

要注意也不要和JDK常用类重名：

- java.util.List
- java.text.Format
- java.math.BigInteger
- ...



## 继承性

### 继承的引入

在前面的章节中，已经定义了`Person`类：

```java
class Person {
    private String name;
    private int age;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
}
```

现在，假设需要定义一个`Student`类，字段如下：

```java
class Student {
    private String name;
    private int age;
    private int score;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
    public int getScore() { … }
    public void setScore(int score) { … }
}
```

`Student`类包含了`Person`类已有的字段和方法，只是多出了一个`score`字段和相应的`getScore()`、`setScore()`方法。能不能在`Student`中不要写重复的代码？这个时候，继承就派上用场了。

继承是面向对象编程中非常强大的一种机制，它首先可以复用代码。当我们让`Student`从`Person`继承时，`Student`就获得了`Person`的所有功能，我们只需要为`Student`编写新增的功能。

Java使用`extends`关键字来实现继承：

```java
class Person {
    private String name;
    private int age;

    public String getName() {...}
    public void setName(String name) {...}
    public int getAge() {...}
    public void setAge(int age) {...}
}

class Student extends Person {
    // 不要重复name和age字段/方法,
    // 只需要定义新增score字段/方法:
    private int score;

    public int getScore() { … }
    public void setScore(int score) { … }
}
```

通过继承，`Student`只需要编写额外的功能，不再需要重复代码。

注意：**子类自动获得了父类的所有字段，严禁定义与父类重名的字段**

在OOP的术语中，把`Person`称为超类（super class），父类（parent class），基类（base class），把`Student`称为子类（subclass），扩展类（extended class）。

作用：

- 继承的出现减少了代码冗余，提高了代码的复用性。
- 继承的出现，更有利于功能的扩展。
- 继承的出现让类与类之间产生了关系，提供了多态的前提。  

注意：不要仅为了获取其他类中某个功能而去继承  

- 子类继承了父类，就继承了父类的**方法和属性**。
- 在子类中，可以使用父类中定义的方法和属性，也可以创建新的数据和方法。
- 在Java 中，继承的关键字用的是“extends”，即子类不是父类的子集，而是对父类的“**扩展**” 。
- 子类**不能直接访问父类中私有的(private)的成员变量和方法**，但是仍然认为获取了父类中私有的结构，只是因为封装性的影响，使得子类不能直接调用父类的结构而已

Java只支持单继承和多层继承， 不允许多重继承

- 一个子类只能有一个父类(单继承)
- 一个父类可以派生出多个子类，父类可以有自己的父类(多层继承)
- 当一个类没有显式继承父类时，则此类继承于`java.lang.Object`类

![image-20220123104809453](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220123104809453-166529427007618.png)



### protected

继承特点：子类无法访问父类的`private`字段或者方法。

为了让子类可以访问父类的字段，需要把`private`改为`protected`。用`protected`修饰的字段可以被子类访问：

```java
class Person {
    protected String name;
    protected int age;
}

class Student extends Person {
    public String hello() {
        return "Hello, " + name; // OK!
    }
}
```

`protected`关键字把字段和方法的访问权限控制在继承树内部，一个`protected`字段和方法可以被其子类以及子类的子类所访问



### super

`super`关键字表示父类（超类）。

在Java类中使用super来调用父类中的指定操作：

- super可用于访问父类中定义的属性
- super可用于调用父类中定义的成员方法
- super可用于在子类构造器中调用父类的构造器

注意：

- 尤其当**子父类出现同名成员时， 可以用super表明调用的是父类中的成员**
- super的追溯**不仅限于直接父类**
- super和this的用法相像， **this代表本类对象的引用， super代表父类的内存空间的标识**  

子类引用父类的字段时，可以用`super.fieldName`。例如：

```java
class Student extends Person {
    public String hello() {
        return "Hello, " + super.name;
    }
}
```



调用父类的构造器

- 子类中所有的构造器**默认**都会访问父类中**空参数**的构造器
- 当父类中没有空参数的构造器时， 子类的构造器必须通过`this(参数列表)`或者`super(参数列表)`语句指定调用本类或者父类中相应的构造器。 同时， **只能”二选一”**， 且必须放在构造器的首行
- 如果子类构造器中既未显式调用父类或本类的构造器， 且父类中又没有无参的构造器， 则**编译出错**  



**子类不会继承任何父类的构造方法。子类默认的构造方法是编译器自动生成的，不是继承的。**

super与this区别

| 区别点     | this                                                   | super                                     |
| ---------- | ------------------------------------------------------ | ----------------------------------------- |
| 访问属性   | 访问本类中的属性，如果本类没有此属性则从父类中继续查找 | 直接访问父类中的属性                      |
| 调用方法   | 访问本类中的方法，如果本类没有此方法则从父类中继续查找 | 直接访问父类中的方法                      |
| 调用构造器 | 调用本类构造器，必须放在构造器的首行                   | 调用父类构造器，必须 放在子类构造器的首行 |



### 阻止继承

正常情况下，只要某个class没有`final`修饰符，那么任何类都可以从该class继承。

从Java 15开始，允许使用`sealed`修饰class，并通过`permits`明确写出能够从该class继承的子类名称。例如，定义一个`Shape`类：

```java
public sealed class Shape permits Rect, Circle, Triangle {
    ...
}
```

上述`Shape`类就是一个`sealed`类，它只允许指定的3个类继承它。如果写：

```java
public final class Rect extends Shape {...}
```

是没问题的，因为`Rect`出现在`Shape`的`permits`列表中。但是，如果定义一个`Ellipse`就会报错：

```
public final class Ellipse extends Shape {...}
// Compile error: class is not allowed to extend sealed class: Shape
```

原因是`Ellipse`并未出现在`Shape`的`permits`列表中。这种`sealed`类主要用于一些框架，防止继承被滥用。

`sealed`类在Java 15中目前是预览状态，要启用它，必须使用参数`--enable-preview`和`--source 15`。



### 向上转型

如果一个引用变量的类型是`Student`，那么它可以指向一个`Student`类型的实例：

```java
Student s = new Student();
```

如果一个引用类型的变量是`Person`，那么它可以指向一个`Person`类型的实例：

```java
Person p = new Person();
```

如果`Student`是从`Person`继承下来的，一个引用类型为`Person`的变量可以指向`Student`类型的实例

```java
Person p = new Student(); 
```

这种把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）。

向上转型实际上是把一个子类型安全地变为更加抽象的父类型：

```java
Student s = new Student();
Person p = s; // upcasting, ok
Object o1 = p; // upcasting, ok
Object o2 = s; // upcasting, ok
```

注意到继承树是`Student > Person > Object`，所以，可以把`Student`类型转型为`Person`，或者更高层次的`Object`。



### 向下转型

和向上转型相反，如果把一个父类类型强制转型为子类类型，就是向下转型（downcasting）。例如：

```java
Person p1 = new Student(); // upcasting, ok
Person p2 = new Person();  
Student s1 = (Student) p1; // ok
Student s2 = (Student) p2; // runtime error! ClassCastException!
```

如果测试上面的代码，可以发现：

`Person`类型`p1`实际指向`Student`实例，`Person`类型变量`p2`实际指向`Person`实例。

在向下转型的时候，把`p1`转型为`Student`会成功，因为`p1`确实指向`Student`实例，把`p2`转型为`Student`会失败，因为`p2`的实际类型是`Person`，不能把父类变为子类，因为子类功能比父类多，多的功能无法凭空变出来。

因此，向下转型很可能会失败。失败的时候，Java虚拟机会报`ClassCastException`。为了避免向下转型出错，Java提供了`instanceof`操作符，可以先判断一个实例究竟是不是某种类型：

```java
Person p = new Person();
System.out.println(p instanceof Person); // true
System.out.println(p instanceof Student); // false

Student s = new Student();
System.out.println(s instanceof Person); // true
System.out.println(s instanceof Student); // true

Student n = null;
System.out.println(n instanceof Student); // false
```

`instanceof`实际上判断一个变量所指向的实例是否是指定类型，或者这个类型的子类。如果一个引用变量为`null`，那么对任何`instanceof`的判断都为`false`。

利用`instanceof`，在向下转型前可以先判断：

```java
Person p = new Student();
if (p instanceof Student) {
    // 只有判断成功才会向下转型:
    Student s = (Student) p; // 一定会成功
}
```

从Java 14开始，判断`instanceof`后，可以直接转型为指定变量，避免再次强制转型。例如，对于以下代码：

```java
Object obj = "hello";
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.toUpperCase());
}
```

可以改写如下：

```java
// instanceof variable:
public class Main {
    public static void main(String[] args) {
        Object obj = "hello";
        if (obj instanceof String s) {
            // 可以直接使用变量s:
            System.out.println(s.toUpperCase());
        }
    }
}
```

这种使用`instanceof`的写法更加简洁。



### 方法的重写 

定义：在子类中可以根据需要**对从父类中继承来的方法进行改造**。在程序执行时，**子类的方法将覆盖父类的方法**。

要求：

- 子类重写的方法必须和父类被重写的方法具有**相同的方法名称、 参数列表**
- 父类被重写的方法的返回值类型是A类，则子类重写的方法的返回值类型可以是A类或者A类的子类
- 父类被重写的方法的返回值类型是基本数据类型，则子类重写的方法的返回值类型必须是相同的基本数据类型
- 子类重写的方法的权限修饰符不能小于父类被重写的方法的权限修饰符
- 子类**不能重写父类中声明为private权限**的方法
- 子类方法抛出的异常不能大于父类被重写方法的异常

注意：

子类与父类中**同名同参数**的方法必须**同时声明**为**非static**的(即为重写)，或者同时声明为static的（不是重写） 。因为static方法是属于类的，子类无法覆盖父类的方法  

```java
public class Person { 
    public String name; 
    public int age; //重写方法举例(1)
	
    public String getInfo() {
		return "Name: "+ name;
	}
}

public class Student extends Person {
	public String school;
	public String getInfo() { //重写方法
		return "Name: "+ name + "\nschool: "+ school;
	}
    
	public static void main(String args[]){
		Student s1=new Student();
		s1.name="Bob";
		s1.age=20;
		s1.school="school2";
		System.out.println(s1.getInfo()); //Name:Bob age:20 school:school2
	}
}
```



### 子类对象实例化全过程

![image-20220123151553343](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220123151553343-166529427007619.png)

从结果上看：(继承性)

子类继承父类后，就获取了父类声明中的属性或方法

创建子类的对象，在堆空间中就会加载所有父类中声明的属性

从过程上看：

当通过子类的构造器创建子类对象时，一定会直接或间接的调用其父类的构造器，进而调用父类的父类的构造器，直到调用了`java.lang.Object`类中的空参构造器为止，正因为加载过所有的父类的结构，所有才可以看到内存中有父类中的结构，子类对象才可以考虑进行调用

创建子类对象时虽然调用了父类构造器，但是从始至终都只创建过一个对象，即为new的子对象



## 多态性

```java
//多态性展示
public class Test{
    public static void main(String[] args){
        //父类的引用、指向子类的对象
        Person p1=new Man();
        Person p2=new Woman();
        
        //多态的使用————虚拟方法调用
        //当调用子父类同名同参数的方法时，实际执行的是子类重写父类的方法
        p1.eat();//执行前查看eat，会指向父类
        p1.walk();//运行时会按照子类的方法执行
        p1.earnMoney//调用子类特有的方法时编译会报错
        
        
    }
}
```

多态性，是面向对象中最重要的概念， 在Java中的体现：

对象的多态性：**父类的引用、指向子类的对象**

### 多态的使用

- 编译时：只能调用父类中声明的方法
- 执行时：实际执行的是子类重写父类的方法

简称： 编译时， 看左边；运行时， 看右边。

- 若编译时类型和运行时类型不一致， 就出现了对象的多态性
- “看左边” ： 看的是父类的引用（父类中不具备子类特有的方法）
- “看右边” ： 看的是子类的对象（**实际运行的是子类重写父类的方法**）  

**对象的多态性只适用于方法，不适用于属性，属性编译与运行都看左边**

一个引用类型变量如果声明为父类的类型，但实际引用的是子类对象，那么**该变量就不能再访问子类中添加的属性和方法**

```java
Student m = new Student();
m.school = “pku”; //合法,Student类有school成员变量
Person e = new Student();
e.school = “pku”; //非法,Person类没有school成员变量
```

多态的使用前提：

- 类的继承关系
- 子类要有方法的重写

在Java中,子类的对象可以替代父类的对象使用。子类可看做是特殊的父类， 所以父类类型的引用可以指向子类的对象：向上转型(upcasting)。

- 一个变量只能有一种确定的数据类型
- 一个引用类型变量可能指向(引用)多种不同类型的对象

```java
Person p = new Student();
Object o = new Person();//Object类型的变量o， 指向Person类型的对象
o = new Student(); //Object类型的变量o， 指向Student类型的对象
```

 方法声明的形参类型为父类类型，可以使用子类的对象作为实参调用该方法  

```java
public class Test {
	public void method(Person e) {
		// ……
		e.getInfo();
	}
	public static void main(Stirng args[]) {
		Test t = new Test();
		Student m = new Student();
		t.method(m); // 子类的对象m传送给父类类型的参数e
	}
}
```



### 虚拟方法调用

正常的方法调用

```java
Person e = new Person();
e.getInfo();

Student e = new Student();
e.getInfo();
```

虚拟方法调用(多态情况下)

子类中定义了与父类同名同参数的方法，在多态情况下，将此时**父类的方法称为虚拟方法**，父类**根据赋给它的不同子类对象，动态调用属于子类的该方法**。这样的方法调用在编译期是无法确定的。

```java
Person e = new Student();
e.getInfo(); //调用Student类的getInfo()方法
```

编译时类型和运行时类型

编译时e为Person类型，而**方法的调用是在运行时确定的**，所以调用的是Student类的getInfo()方法 ——动态绑定  



### 方法的重载与重写

从编译和运行的角度看：

重载，是指允许存在多个同名方法，而这些方法的参数不同。 编译器根据方法不同的参数表， 对同名方法的名称做修饰。对于编译器而言，这些**同名方法就成了不同的方法**。 它们的调用地址在编译期就绑定了。 Java的重载是可以包括父类和子类的，即子类可以重载父类的同名不同参数的方法。

所以： 对于重载而言，在方法调用之前，编译器就已经确定了所要调用的方法，这称为“早绑定”或“静态绑定” ；

而对于多态，只有等到方法调用的那一刻， 解释运行器才会确定所要调用的具体方法，这称为“晚绑定”或“动态绑定” 。

引用一句Bruce Eckel的话： “不要犯傻，如果它不是晚绑定， 它就不是多态。”  



## static

编写一个类其实就是在描述其对象的属性和行为，而并没有产生实质上的对象，只有通过new关键字才会产生出对象，这时系统才会分配内存空间给对象，其方法才可以供外部调用。

有时候希望**无论是否产生了对象或无论产生了多少对象的情况下**， **某些特定的数据在内存空间里只有一份**，例如所有的中国人都有个国家名称，每一个中国人都共享这个国家名称，不必在每一个中国人的实例对象中都单独分配一个用于代表国家名称的变量。

### 实例变量与静态变量  

```java
class Circle{
	private double radius;
	public Circle(double radius){
        this.radius=radius;
    }
	public double findArea(){
        return Math.PI*radius*radius;
    }
}

//创建两个Circle对象
Circle c1=new Circle(2.0); //c1.radius=2.0
Circle c2=new Circle(3.0); //c2.radius=3.0
```

Circle类中的变量`radius`是一个**实例变量**(instance variable)， 它属于类的每一个对象， **不能被同一个类的不同对象所共享**。

上例中`c1`的`radius`独立于`c2`的`radius`， 存储在不同的空间。 `c1`中的`radius`变化不会影响`c2`的`radius`， 反之亦然。

如果想让一个类的所有实例共享数据，就用**类变量（静态变量）** 



### 类属性

类属性作为该类**各个对象之间共享的变量**。 在设计类时,分析哪些**属性不因对象的不同而改变**，将这些属性设置为类属性。相应的方法设置为类方法。

当通过某个对象修改静态变量，利用其它对象去调用此静态变量时，得到的是修改后的静态变量

使用范围：在Java类中， 可用static修饰属性、 方法、 代码块、 内部类

被修饰后的成员具备以下特点：

- 随着类的加载而加载，由于类只加载一次，则静态变量在内存中仅存在一份，存在于方法的静态域中
- 优先于对象存在
- 修饰的成员，被所有对象所共享
- 访问权限允许时，可不创建对象，直接被类调用  

```java
class Person {
	private int id;
	public static int total = 0;
	
    public Person() {
		total++;
		id = total;
	}
    
	public static void main(String args[]){
		Person Tom=new Person();
		Tom.id=0;
		total=100; // 不用创建对象就可以访问静态成员
	}
}

public class StaticDemo {
	public static void main(String args[]) {
		Person.total = 100; // 不用创建对象就可以访问静态成员
		//访问方式：类名.类属性
		System.out.println(Person.total);
		Person c = new Person();
		System.out.println(c.total); //输出101
	}
}
```



### 类方法

如果**方法与调用者无关，则这样的方法通常被声明为类方法（静态方法）**，由于**不需要创建对象就可以调用类方法**，从而简化了方法的调用  

没有对象的实例时，可以用`类名.方法名()`的形式访问由static修饰的类方法。

在**static方法内部只能访问类的static修饰的属性或方法**， 不能访问类的非static的结构。  

```java
class Person {
	private int id;
	private static int total = 0;
	public static int getTotalPerson() {
		//id++; //非法
		return total;
    }
	public Person() {
		total++;
		id = total;
	}
}

public class PersonTest {
	public static void main(String[] args) {
		System.out.println("Number of total is " + Person.getTotalPerson());
		//没有创建对象也可以访问静态方法
		Person p1 = new Person();
		System.out.println( "Number of total is "+ Person.getTotalPerson());
	}
} 

//输出:Number of total is 0;Number of total is 1
```

因为不需要实例就可以访问static方法，因此static方法内部不能有this。 (也不能有super )，static修饰的方法不能被重写

```java
class Person {
	private int id;
	private static int total = 0;
	public static void setTotalPerson(int total){
		this.total=total; 
        //非法，在static方法中不能有this，也不能有super
	}
	public Person() {
		total++;
		id = total;
	}
}

public class PersonTest {
	public static void main(String[] args) {
		Person.setTotalPerson(3);
	} 
}  
```



### main方法

由于Java虚拟机需要调用类的`main()`方法，所以该方法的访问权限必须是public；

又因为Java虚拟机在执行`main()`方法时不必创建对象，所以该方法必须是static的；

该方法接收一个String类型的数组参数，该数组中保存**执行Java命令时传递给所运行的类的参数**。

又因为`main()` 方法是静态的，不能直接访问该类中的非静态成员，**必须创建该类的一个实例对象后，才能通过这个对象去访问类中的非静态成员**



## 代码块  

代码块(或初始化块)的作用：对Java类或对象进行初始化

代码块(或初始化块)的分类：

一个类中代码块**若有修饰符， 则只能被static修饰**， 称为静态代码块(static block)， 没有使用static修饰的， 为非静态代码块。

static代码块通常用于初始化static的属性

```java
class Person {
	public static int total;
	static {
		total = 100;//为total赋初值
	}
	…… //其它属性或方法声明
}  
```

### 静态代码块

用static 修饰的代码块

- 可以有输出语句。
- 可以对类的属性、类的声明进行初始化操作。
- **不可以对非静态的属性初始化**。即：**不可以调用非静态的属性和方法。**
- 若有多个静态的代码块，那么按照从上到下的顺序依次执行。
- **静态代码块的执行要先于非静态代码块。**
- 静态代码块**随着类的加载而加载并执行**，且**只执行一次**  

```java
class Person {
	public static int total;
	static {
		total = 100;
		System.out.println("in static block!");
	}
}

public class PersonTest {
	public static void main(String[] args) {
		System.out.println("total = " + Person.total);
		System.out.println("total = " + Person.total);
	}
}
//输出：in static block    total=100    total=100
```



### 非静态代码块

没有static修饰的代码块

- 可以有输出语句。
- 可以对类的属性、 类的声明进行初始化操作。
- 除了调用非静态的结构外， 还**可以调用静态的变量或方法。**
- 若有多个非静态的代码块， 那么按照从上到下的顺序依次执行。
- 每次**创建对象的时候， 都会执行一次**。 **且先于构造器执行**。  

### 成员变量赋值的执行顺序  

![image-20220124160140752](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220124160140752-166529427007620.png)



## final关键字

在Java中声明**类、 变量和方法**时， 可使用关键字final来修饰,表示“最终的” 。



### 修饰类  

**final标记的类不能被继承**。 提高安全性， 提高程序的可读性。

- String类、 System类、 StringBuffer类

```java
final class A{
}
class B extends A{ //错误，不能被继承。
}
```



### 修饰方法  

**final标记的方法不能被子类重写**。

- Object类中的`getClass()`。

```java
class A {
	public final void print() {
		System.out.println("A");
	}
}

class B extends A {
	public void print() { // 错误，不能被重写。
		System.out.println("尚硅谷");
	}
}  
```



### 修饰变量——常量  

**final标记的变量**(**成员变量或局部变量**)即称**为常量**。 名称**大写**， 且只能被赋值一次。

- final标记的成员变量**必须**在**声明时**或在**每个构造器中或代码块中显式赋值**， 然后才能使用。
- `final double MY_PI = 3.14;`  

```java
class A {
	private final String INFO = "atguigu"; //声明常量
	public void print() {
		//The final field A.INFO cannot be assigned
		//INFO = "尚硅谷";
	}
}  
```

`static final`用来修饰属性：全局常量  

```java
public final class Test {
	public static int totalNumber = 5;
	public final int ID;
	
    public Test() {
		ID = ++totalNumber; // 可在构造器中给final修饰的“变量”赋值
	}
	
    public static void main(String[] args) {
		Test t = new Test();
		System.out.println(t.ID);
		final int I = 10;
		final int J;
		J = 20;
		J = 30; // 非法
	}
}
```



## 抽象类与抽象方法  

随着继承层次中一个个新子类的定义，类变得越来越具体，而父类则更一般，更通用。

类的设计应该保证父类和子类能够共享特征。有时将一个父类设计得非常抽象，以至于它**没有具体的实例**，这样的类叫做抽象类。  

用abstract来修饰一个方法， 该方法叫做抽象方法。

- 抽象方法：**只有方法的声明，没有方法的实现**。以分号结束，比如： `public abstract void talk();`

用abstract关键字来修饰一个类， 这个类叫做抽象类。

- 含有抽象方法的类必须被声明为抽象类。

- 抽象类不能被实例化。
- 抽象类是用来被继承的，抽象类的子类必须重写父类的抽象方法，并提供方法体。
- 子类若没有重写全部的抽象方法，仍为抽象类，不能被实例化。
- 不能用abstract修饰变量、代码块、构造器；
- 不能用abstract修饰私有方法、静态方法、 final的方法、 final的类。  



### 抽象类的匿名子类

如果Person是个抽象类，Worker是它的可实例化子类

```java
public class PersonTest{
    public static void main(String[] args){
        
        Worker worker=new Worker();
        
        method1(worker);//1.非匿名子类的非匿名对象
        method1(new Worker);//2.非匿名子类的匿名对象
        
        /*
        抽象类的匿名子类：
        创建一个匿名子类的对象：p
        需要使用子类的重写方法，但是只用一次
        因此不去创建子类，而是使用匿名的方法
        */
        
        Person p=new Person(){
            public void eat(){
                System.out.println("重写");
            }
            public void walk(){
                System.out.println("重写");
            }
        }
        method1(p);//3.匿名子类的非匿名对象
        method1(new Person()){//4.匿名子类的匿名对象
            //重写方法
        }
        
        
    }
    public static void method1(Person p){
        p.eat();
        p.walk();
    }
    public static void method(Student s){
        
    }
}
```



### 模板方法设计模式  

抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式  

解决的问题：

- 当功能内部一部分实现是确定的， 一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。
- 换句话说，在软件开发中实现一个算法时，整体步骤很固定、通用，这些步骤已经在父类中写好了。但是某些部分易变，**易变部分可以抽象出来，供不同子类实现**。这就是一种模板模式。  

```java
abstract class Template {
	public final void getTime() {
		long start = System.currentTimeMillis();
		code();//抽象方法，需要测试代码的执行时间，但是代码不确定
		long end = System.currentTimeMillis();
		System.out.println("执行时间是： " + (end - start));
	}
	public abstract void code();
}

class SubTemplate extends Template {
	public void code() {
		for (int i = 0; i < 10000; i++) {
			System.out.println(i);
		}
	}
}
```

模板方法设计模式是编程中经常用得到的模式。 各个框架、 类库中都有他的
影子， 比如常见的有：

- 数据库访问的封装
- Junit单元测试
- JavaWeb的Servlet中关于doGet/doPost方法调用
- Hibernate中模板程序
- Spring中JDBCTemlate、 HibernateTemplate等  



## 接口

### 定义

一方面， 有时必须从几个类中派生出一个子类， 继承它们所有的属性和方法。 但是， Java不支持多重继承。 有了接口， 就可以得到多重继承的效果。

另一方面， 有时必须从几个类中抽取出一些共同的行为特征，而它们之间又没有is-a的关系，仅仅是具有相同的行为特征而已。例如：鼠标、键盘等都支持USB连接。

接口就是规范，定义的是一组规则，体现了现实世界中“如果你是/要...则必须能...”的思想。 继承是一个"是不是"的关系，而接口实现则是 "能不能"的关系。

接口的本质是契约，标准，规范，就像我们的法律一样。制定好后大家都要遵守。  

![image-20220125102017779](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220125102017779-166529427007621.png)

![image-20220125102148122](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220125102148122-166529427007622.png)

接口(interface)是抽象方法和常量值定义的集合。



### 使用

接口的特点：

- 用**interface**来定义。
- 接口中的所有**成员变量都默认**是由`public static final`修饰的(全局常量)。
- 接口中的所有抽象方法都默认是由`public abstract`修饰的(没有方法体)。
- 接口中没有构造器。
- 接口采用多继承机制。  

```java
public interface Runner {
	int ID = 1;
	void start();
	public void run();
	void stop();
}
//等价于
public interface Runner {
	public static final int ID = 1;
	public abstract void start();
	public abstract void run();
	public abstract void stop();
}
```

定义Java类的语法格式： **先写extends，后写implements**

```java
class SubClass extends SuperClass implements InterfaceA{ }
```

- 一个类可以实现多个接口， 接口也可以继承其它接口。
- 接口中不能定义构造器，所以接口不可以实例化
- **实现接口的类中必须提供接口中所有方法的具体实现内容，方可实例化**。否则，仍为抽象类。
- 接口的主要用途就是被实现类实现（面向接口编程）
- 与继承关系类似，接口与实现类之间存在多态性
- 接口和类是并列关系， 或者可以理解为一种特殊的类。 从本质上讲，接口是一种特殊的抽象类，这种抽象类中只包含常量和方法的定义(JDK7.0及之前)， 而没有变量和方法的实现。  

![image-20220125103817060](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220125103817060-166529427007624.png)

```java
interface publicRunner { void start(); 
	public void run();
	public void stop();
}

class Person implements Runner {
	public void start() {
		// 准备工作：弯腰、蹬腿、咬牙、瞪眼
		// 开跑
	}
	public void run() {
		// 摆动手臂
		// 维持直线方向
	}
	public void stop() {
		// 减速直至停止、喝水。
	}
}
```

一个类可以实现多个无关的接口  

```java
interface Runner { public void run();}
interface Swimmer {public double swim();}

class Creator{public int eat(){…}}

class Man extends Creator implements Runner ,Swimmer{
	public void run() {……}
	public double swim() {……}
	public int eat() {……}
}
```

与继承关系类似，接口与实现类之间存在多态性  

```java
public class Test{
	public static void main(String args[]){
		Test t = new Test();
		Man m = new Man();
        //m1-m2的形参是接口，接口不能实例化
        //可以用实现了接口的类的实例来调用
		t.m1(m);
		t.m2(m);
		t.m3(m);
	}
	public String m1(Runner f) { f.run(); }
	public void m2(Swimmer s) {s.swim();}
    
	public void m3(Creator a) {a.eat();}
}
```

接口与接口之间可以相互继承，且可以多继承（因为不涉及实例化）

实现类SubAdapter必须给出接口SubInterface以及父接口MyInterface中所有方法的实现。否则， SubAdapter仍需声明为abstract的。  

```java
interface MyInterface{
	String s=“MyInterface”;
	public void absM1();
}
interface SubInterface extends MyInterface{
	public void absM2();
}

public class SubAdapter implements SubInterface{
	public void absM1(){System.out.println("absM1");}
	public void absM2(){System.out.println("absM2");}
}
```



### 接口的匿名实现类

```java
public class Test{
	public static void main(String args[]){
		Test t = new Test();
        //1.创建接口的非匿名实现类的非匿名对象
        Person p=new Person();
        t.m1.run(p);
		//2.创建接口的非匿名实现类的匿名对象
        t.m1(new Person());
        //3.创建接口匿名实现类的非匿名对象
        Runner p=new Runner(){
            //重写方法
        }
		t.m1(p);
        //4.创建接口匿名实现类的匿名对象
        t.m1(new Runner){
            //重写方法
        }
	}
	public String m1(Runner f) { f.run(); }
}
```



### 接口和抽象类之间的对比  

| 区别点       | 抽象类                                                       | 接口                                         |
| ------------ | ------------------------------------------------------------ | -------------------------------------------- |
| 定义         | 包含抽象方法的类                                             | 主要是抽象方法和全局常量的集合               |
| 组成         | 构造方法、抽象方法、普通方法、 常量、变量                    | 常量、抽象方法、 (jdk8.0:默认方法、静态方法) |
| 使用         | 子类继承抽象类(extends)                                      | 子类实现接口(implements)                     |
| 关系         | 抽象类可以实现多个接口                                       | 接口不能继承抽象类，但允许继承多个接口       |
| 常见设计模式 | 模板方法                                                     | 简单工厂、工厂方法、代理模式                 |
| 对象         | 都通过对象的多态性产生实例化对象                             |                                              |
| 局限         | 抽象类有单继承的局限                                         | 接口没有此局限                               |
| 实际         | 作为一个模板                                                 | 是作为一个标准或是表示一种能力               |
| 选择         | 如果抽象类和接口都可以使用的话，优先使用接口，因为避免单继承的局限 |                                              |

例题

```java
interface A {
	int x = 0;//全局常量
}
class B {
	int x = 1;
}
class C extends B implements A {
	public void pX() {
		System.out.println(super.x);//1
        System.out.println(A.x);//0
	}
	public static void main(String[] args) {
		new C().pX();
	}
}


interface Playable {
	void play();
}

interface Bounceable {
	void play();
}

interface Rollable extends Playable,Bounceable {
	Ball ball = new Ball("PingPang");//public static final，不能再实例化
}

class Ball implements Rollable {
	private String name;
	public String getName() {
		return name;
	}
	public Ball(String name) {
		this.name = name;
	}
    //会同时重写两个接口中的方法
	public void play() {
		ball = new Ball("Football");//违反final，报错
		System.out.println(ball.getName());
	}
}
```



### Java 8中关于接口的改进  

Java 8中，可以为接口添加静态方法和默认方法。从技术角度来说，这是完全合法的，只是它看起来违反了接口作为一个抽象定义的理念。

#### 静态方法

静态方法使用 static 关键字修饰。 **可以通过接口直接调用静态方法**，并执行其方法体。我们经常在相互一起使用的类中使用静态方法。可以在标准库中找到像Collection/Collections或者Path/Paths这样成对的接口和类。  

```java
public interface AA {
	double PI = 3.14;
	public default void method() {
		System.out.println("北京");
	}
	default String method1() {
		return "上海";
	}
	public static void method2() {
		System.out.println(“hello lambda!");
	}
}  
```

#### 默认方法

默认方法使用 default 关键字修饰。可以通过**实现类对象来调用**。我们在已有的接口中提供新方法的同时，还保持了与旧版本代码的兼容性。比如： java 8 API中对Collection、 List、 Comparator等接口提供了丰富的默认方法 

若一个接口中定义了一个默认方法，而另外一个接口中也定义了一个同名同参数的方法（不管此方法是否是默认方法），在实现类同时实现了这两个接口时，会出现： 接口冲突。

解决办法：**实现类必须覆盖接口中同名同参数的方法，来解决冲突**。  

若一个接口中定义了一个默认方法，而父类中也定义了一个同名同参数的非抽象方法，则不会出现冲突问题。因为此时遵守： **类优先原则。 接口中具有相同名称和参数的默认方法会被忽略**  

```java
interface Filial {// 孝顺的
	default void help() {
		System.out.println("老妈，我来救你了");
	}
}
interface Spoony {// 痴情的
	default void help() {
		System.out.println("媳妇， 别怕，我来了");
	}
}

class Man implements Filial, Spoony {
	@Override
	public void help() {
		System.out.println("我该怎么办呢？ ");
		//接口冲突的解决方式
        Filial.super.help();
		Spoony.super.help();
	}
}
```

## 内部类  

当一个事物的内部，还有一个部分需要一个完整的结构进行描述，而这个内部的完整的结构又只为外部事物提供服务(如人类与大脑)，那么整个内部的完整结构最好使用内部类。

- 在Java中，允许一个类的定义位于另一个类的内部，前者称为内部类，后者称为外部类。
- Inner class一般用在定义它的类或语句块之内，**在外部引用它时必须给出完整的名称**。
- Inner class的名字不能与包含它的外部类类名相同；

分类： 

- 成员内部类（static成员内部类和非static成员内部类）
- 局部内部类（不谈修饰符）、匿名内部类  

### 成员内部类

成员内部类作为外部类的成员：

- 和外部类不同， Inner class还可以声明为private或protected；
- 可以调用外部类的结构
- Inner class 可以声明为static的， 但此时就不能再使用外层类的非static的成员变量  

成员内部类作为类：

- 可以在内部定义属性、 方法、 构造器等结构
- 可以声明为abstract类 ， 因此可以被其它的内部类继承
- 可以声明为final的
- 编译以后生成OuterClass$InnerClass.class字节码文件（ 也适用于局部内部类  

【注意】

- 非static的成员内部类中的成员不能声明为static的， 只有在外部类或static的成员内部类中才可声明static成员。
- 外部类访问成员内部类的成员， 需要“内部类.成员”或“内部类对象.成员”的方式
- 成员内部类可以直接使用外部类的所有成员， 包括私有的数据
- 当想要在外部类的静态成员部分使用内部类时， 可以考虑内部类声明为静态的  

```java
//示例1
class Outer {
	private int s;
	public class Inner {
		public void mb() {
			s = 100;
			System.out.println("在内部类Inner中s=" + s);
		}
	}
	public void ma() {
		Inner i = new Inner();
		i.mb();
	}
}
public class InnerTest {
	public static void main(String args[]) {
		Outer o = new Outer();
		o.ma();
	}
}

//示例2
public class Outer {
	private int s = 111;
	public class Inner {
		private int s = 222;
		public void mb(int s) {
			System.out.println(s); // 局部变量s
			System.out.println(this.s); // 内部类对象的属性s
			System.out.println(Outer.this.s); // 外部类对象属性s
		}
	}
	public static void main(String args[]) {
		Outer a = new Outer();
		Outer.Inner b = a.new Inner();
		b.mb(333);
	}
}
```

### 局部内部类

声明局部内部类  

```java
class 外部类{
	方法(){
		class 局部内部类{
		}
	} 
    {
		class 局部内部类{
		}
	}
}
```

如何使用局部内部类

- 只能在声明它的方法或代码块中使用，而且是**先声明后使用**。除此之外的任何地方都不能使用该类
- 但是它的**对象可以通过外部方法的返回值返回使用，返回值类型只能是局部内部类的父类或父接口类型**  

局部内部类的特点

- 内部类仍然是一个独立的类，在编译之后内部类会被编译成独立的.class文件，但是前面冠以外部类的类名和$符号，以及数字编号。
- 只能在声明它的方法或代码块中使用，而且是先声明后使用。除此之外的任何地方都不能使用该类。
- 局部内部类可以使用外部类的成员，包括私有的。
- **局部内部类可以使用外部方法的局部变量，但是必须是final的**。 由局部内部类和局部变量的声明周期不同所致。
- 局部内部类和局部变量地位类似，不能使用public,protected,缺省,private
- 局部内部类不能使用static修饰，因此也不能包含静态成员  

### 匿名内部类  

匿名内部类不能定义任何静态成员、方法和类，只能创建匿名内部类的一个实例。一个匿名内部类一定是在new的后面，用其隐含实现一个接口或实现一个类。

格式：

```java
new 父类构造器（实参列表）|实现接口(){
	//匿名内部类的类体部分
}
```

匿名内部类的特点

- 匿名内部类必须继承父类或实现接口
- 匿名内部类只能有一个对象
- 匿名内部类对象只能使用多态形式引用  

```java
interface A{
	public abstract void fun1();
}

public class Outer{
	public static void main(String[] args) {
		new Outer().callInner(new A(){
		//接口不能new但此处比较特殊是子类对象实现接口，不过没有为对象取名
			public void fun1() {
				System.out.println(“implement for fun1");
			}
		});// 两步写成一步了
	}
	public void callInner(A a) {
		a.fun1();
	}
}  
```



## λ

### lambda

#### 基本介绍

Lambda 表达式是 JDK1.8 开始之后的新技术，是一种代码的新语法，一种特殊写法

作用：为了简化匿名内部类的代码写法

Lambda 表达式的格式:

```java
(匿名内部类被重写方法的形参列表) -> {
	//被重写方法的方法体代码。
}
```

Lambda 表达式并不能简化所有匿名内部类的写法，只能简化**函数式接口的匿名内部类**

简化条件：首先必须是接口，接口中只能有一个抽象方法

@FunctionalInterface 函数式接口注解：一旦某个接口加上了这个注解，这个接口只能有且仅有一个抽象方法



***



#### 简化方法

Lambda 表达式的省略写法（进一步在 Lambda 表达式的基础上继续简化）

* 如果 Lambda 表达式的方法体代码只有一行代码，可以省略大括号不写，同时要省略分号；如果这行代码是 return 语句，必须省略 return 不写
* 参数类型可以省略不写
* 如果只有一个参数，参数类型可以省略，同时()也可以省略

```java
List<String> names = new ArrayList<>();
names.add("胡");
names.add("甘");
names.add("洪");

names.forEach(new Consumer<String>() {
    @Override
    public void accept(String s) {
        System.out.println(s);
    }
});

names.forEach((String s) -> {
        System.out.println(s);
});

names.forEach((s) -> {
    System.out.println(s);
});

names.forEach(s -> {
    System.out.println(s);
});

names.forEach(s -> System.out.println(s) );
```



***



#### 常用简化

Comparator

```java
public class CollectionsDemo {
    public static void main(String[] args) {
        List<Student> lists = new ArrayList<>();//...s1 s2 s3
        Collections.addAll(lists , s1 , s2 , s3);
        Collections.sort(lists, new Comparator<Student>() {
            @Override
            public int compare(Student s1, Student s2) {
                return s1.getAge() - s2.getAge();
            }
        });
        
        // 简化写法
        Collections.sort(lists ,(Student t1, Student t2) -> {
                return t1.getAge() - t2.getAge();
        });
        // 参数类型可以省略,最简单的
        Collections.sort(lists ,(t1,t2) -> t1.getAge()-t2.getAge());
    }
}
```





***



### 方法引用

#### 基本介绍

方法引用：方法引用是为了进一步简化 Lambda 表达式的写法

方法引用的格式：类型或者对象::引用的方法

关键语法是：`::`

```java
lists.forEach( s -> System.out.println(s));
// 方法引用！
lists.forEach(System.out::println);
```



***



#### 静态方法

引用格式：`类名::静态方法`

简化步骤：定义一个静态方法，把需要简化的代码放到一个静态方法中去

静态方法引用的注意事项：被引用的方法的参数列表要和函数式接口中的抽象方法的参数列表一致,才能引用简化

```java
//定义集合加入几个Student元素
// 使用静态方法进行简化！
Collections.sort(lists, (o1, o2) -> Student.compareByAge(o1 , o2));
// 如果前后参数是一样的，而且方法是静态方法，既可以使用静态方法引用
Collections.sort(lists, Student::compareByAge);

public class Student {
    private String name ;
    private int age ;

    public static int compareByAge(Student o1 , Student o2){
        return  o1.getAge() - o2.getAge();
    }
}
```



***



#### 实例方法

引用格式：`对象::实例方法`

简化步骤：定义一个实例方法，把需要的代码放到实例方法中去

实例方法引用的注意事项：被引用的方法的参数列表要和函数式接口中的抽象方法的参数列表一致。

```java
public class MethodDemo {
    public static void main(String[] args) {
        List<String> lists = new ArrayList<>();
        lists.add("java1");
        lists.add("java2");
        lists.add("java3");
        // 对象是 System.out = new PrintStream();
        // 实例方法：println()
        // 前后参数正好都是一个
        lists.forEach(s -> System.out.println(s));
        lists.forEach(System.out::println);
    }
}
```



***



#### 特定类型

特定类型：String，任何类型

引用格式：`特定类型::方法`

注意事项：如果第一个参数列表中的形参中的第一个参数作为了后面的方法的调用者，并且其余参数作为后面方法的形参，那么就可以用特定类型方法引用了

```java
public class MethodDemo{
    public static void main(String[] args) {
        String[] strs = new String[]{"James", "AA", "John",
                "Patricia","Dlei" , "Robert","Boom", "Cao" ,"black" ,
                "Michael", "Linda","cao","after","sa"};

        // public static <T> void sort(T[] a, Comparator<? super T> c)
        // 需求：按照元素的首字符(忽略大小写)升序排序！！！
        Arrays.sort(strs, new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return s1.compareToIgnoreCase(s2);//按照元素的首字符(忽略大小写)
            }
        });

        Arrays.sort(strs, ( s1,  s2 ) ->  s1.compareToIgnoreCase(s2));

        // 特定类型的方法引用：
        Arrays.sort(strs,  String::compareToIgnoreCase);
        System.out.println(Arrays.toString(strs));
    }
}
```



***



#### 构造器

格式：`类名::new`

注意事项：前后参数一致的情况下，又在创建对象，就可以使用构造器引用

```java
public class ConstructorDemo {
    public static void main(String[] args) {
        List<String> lists = new ArrayList<>();
        lists.add("java1");
        lists.add("java2");
        lists.add("java3");

        // 集合默认只能转成Object类型的数组。
        Object[] objs = lists.toArray();

        // 我们想指定转换成字符串类型的数组！最新的写法可以结合构造器引用实现 
        String[] strs = lists.toArray(new IntFunction<String[]>() {
            @Override
            public String[] apply(int value) {
                return new String[value];
            }
        });
        String[] strs1 = lists.toArray(s -> new String[s]);
        String[] strs2 = lists.toArray(String[]::new);

        System.out.println("String类型的数组："+ Arrays.toString(strs2));
    }
}
```





# 常用类

## Object

Object类是所有Java类的根父类

如果在类的声明中未使用extends关键字指明其父类， 则默认父类为`java.lang.Object`类  

```java
public class Person {
	...
}
//等价于：
public class Person extends Object {
	...
}
method(Object obj){…} //可以接收任何类作为其参数
Person o=new Person();
method(o)
```

Object类中的主要结构  

| 方法名称                            | 类型 | 描述           |
| ----------------------------------- | ---- | -------------- |
| `public Object()`                   | 构造 | 构造器         |
| `public boolean equals(Object obj)` | 普通 | 对象比较       |
| `public int hashCode()`             | 普通 | 取得Hash码     |
| `public String toString()`          | 普通 | 对象打印时调用 |

### ==操作符与equals方法  

**= =：**

基本类型比较值:只要两个变量的值相等， 即为true。

```java
int a=5; 
if(a==6){…}
```

引用类型比较引用(是否指向同一个对象)：**只有指向同一个对象时**， ==才返回true。(是不是指向堆中同一个位置)

```java
Person p1=new Person();
Person p2=new Person();
if (p1==p2){…}
```

用“==”进行比较时， 符号两边的数据类型必须兼容(可自动转换的基本数据类型除外)， 否则编译出错 

**equals()**：

所有类都继承了Object， 也就获得了equals()方法。 还可以重写。

- 只能比较**引用类型**， 其作用与“==”相同,比较是否指向同一个对象。
- 格式:`obj1.equals(obj2)`

特例：当用equals()方法进行比较时， 对类File、 String、 Date及包装类（Wrapper Class）来说， 是比较**类型及内容而不考虑引用的是否是同一个对象**；原因：在这些类中重写了Object类的equals()方法。

当自定义使用equals()时， 可以重写。 用于比较两个对象的**“内容” 是否都相等** 

重写equals()方法的原则  

- 对称性： 如果x.equals(y)返回是“ true” ， 那么y.equals(x)也应该返回是“true” 。
- 自反性： x.equals(x)必须返回是“true” 。
- 传递性： 如果x.equals(y)返回是“true” ， 而且y.equals(z)返回是“true” ，那么z.equals(x)也应该返回是“true” 。
- 一致性： 如果x.equals(y)返回是“true” ， 只要x和y内容一直不变， 不管你重复x.equals(y)多少次， 返回都是“true” 。
- 任何情况下， x.equals(null)， 永远返回是“false” ；x.equals(和x不同类型的对象)永远返回是“false” 。  

### toString() 方法

`toString()`方法在Object类中定义， 其返回值是String类型， **返回类名和它的引用地址**。

在进行String与其它类型数据的连接操作时， 自动调用`toString()`方法

```java
Date now=new Date();
System.out.println(“now=”+now); //相当于
System.out.println(“now=”+now.toString());
```

可以根据需要在用户自定义类型中重写toString()方法，如String 类重写了toString()方法， **返回字符串的值**。

```java
s1=“hello”;
System.out.println(s1);//相当于System.out.println(s1.toString());
```

基本类型数据转换为String类型时， 调用了对应包装类的toString()方法

```java
int a=10; 
System.out.println(“a=”+a);  
```

**==和equals的区别**

- == 既可以比较基本类型也可以比较引用类型。对于基本类型就是比较值，对于引用类型就是比较内存地址
- equals的话，它是属于java.lang.Object类里面的方法，如果该方法没有被重写过默认也是==;我们可以看到String等类的equals方法是被重写过的，而且String类在日常开发中用的比较多，久而久之，形成了equals是比较值的错误观点。
- 具体要看自定义类里有没有重写Object的equals方法来判断。
- 通常情况下，重写equals方法，会比较类中的相应属性是否都相等。  



## 包装类

针对八种基本数据类型定义相应的引用类型—包装类（封装类）

有了类的特点，就可以调用类中的方法， Java才是真正的面向对象 

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| byte         | Byte      |
| short        | Short     |
| int          | Integer   |
| long         | Long      |
| float        | Float     |
| double       | Double    |
| boolean      | Boolean   |
| char         | Character |

### 装箱与拆箱

装箱：把基本数据类型包装成包装类

通过包装类的构造器实现：

```java
int i = 500; 
Integer t = new Integer(i);
```

还可以通过字符串参数构造包装类对象：

```java
Float f = new Float("4.56");
Long l = new Long("asdf");//NumberFormatException
```

拆箱：获得包装类对象中包装的基本类型变量

调用包装类的`.xxxValue()`方法：

```java
boolean b = bObj.booleanValue();
```

### 自动装箱与拆箱

因为`int`和`Integer`可以互相转换：

```
int i = 100;
Integer n = Integer.valueOf(i);
int x = n.intValue();
```

所以，Java编译器可以帮助我们自动在`int`和`Integer`之间转型：

```java
Integer n = 100; // 编译器自动使用Integer.valueOf(int)
int x = n; // 编译器自动使用Integer.intValue()
```

这种直接把`int`变为`Integer`的赋值写法，称为自动装箱（Auto Boxing），反过来，把`Integer`变为`int`的赋值写法，称为自动拆箱（Auto Unboxing）。

注意：自动装箱和自动拆箱只发生在编译阶段，目的是为了少写代码。

装箱和拆箱会影响代码的执行效率，因为编译后的`class`代码是严格区分基本类型和引用类型的。并且，自动拆箱执行时可能会报`NullPointerException`

JDK1.5之后，支持自动装箱，自动拆箱。但**类型必须匹配** 

### **字符串转换成基本数据类型**

通过包装类的构造器实现：

```java
int i = new Integer("12");
```

通过包装类的`parseXxx(String s)`静态方法：

```java
Float f = Float.parseFloat("12.1"); 
```

### **基本数据类型转换成字符串**

调用字符串重载的`valueOf()`方法：

```java
String fstr = String.valueOf(2.34f);
```

更直接的方式

```java
String intStr = 5 + ""  ;
```

![image-20220123211753949](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220123211753949-166529427007623.png)

## String 

代表字符串。 Java 程序中的所有字符串字面值（如 "abc" ）都作为此类的实例实现

- 字符串是常量，用双引号引起来表示。 它们的值在创建之后不能更改。
- String对象的字符内容是存储在一个字符数组value[]中的。  

### 对象的创建  

String是一个final类，代表**不可变的字符序列**。

#### 字面量方式 

区别于new，此时字符串值声明在字符串常量池中，**字符串常量池中不会存储相同内容的字符串**

- 对字符串重新赋值时
- 对现有的字符串进行连接操作时
- 当调用String的replace()方法修改指定字符串/字符时

均需要重新指定内存区域赋值，不能使用原有的value进行赋值

```java
public void test1(){
    String s1="abc";//字面量的定义方式
    String s2="abc";
    //s1="hello";

    System.out.println(s1);//abc
    System.out.println(s2);//abc
    System.out.println(s1==s2);//true

    String s3="abc";
    s3+="def";
    System.out.println(s2);//abc
    System.out.println(s3);//abcdef

    String s4="abc";
    String s5=s4.replace('a','m');
    System.out.println(s4);//abc
    System.out.println(s5);//mbc
}
```

![image-20220128091113755](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128091113755-166529427007738.png)

![image-20220128091134239](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128091134239-166529427007625.png)

#### new+构造器方式

给一个字符串赋值，此时s2、s3保存的地址值，是数据在堆空间中开辟空间以后对应的地址值

```java
	public void test2(){
		String s1 = "abc";
		String s2 = new String("abc");
		String s3 = new String("abc");

        System.out.println(s1==s2);//false
        System.out.println(s1==s3);//false
        System.out.println(s2==s3);//false,新的对象

        Person p1=new Person("Tom");
        Person p2=new Person("Tom");
        System.out.println(p1.name.equals(p2.name));//true
        System.out.println(p1.name==p2.name);//true

        p1.name="Jack";
        System.out.println(p2.name);//Tom
	}

class Person{
    String name;

    public Person(String name){
        this.name=name;
    }
}
```

![image-20220128100527587](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128100527587-166529427007726.png)

3. 内存探究

![image-20220128100658215](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128100658215-166529427007728.png)

结论

- 常量与常量的拼接结果在常量池。 且常量池中不会存在相同内容的常量。
- 只要其中有一个是变量， 结果就在堆中
- 如果拼接的结果调用intern()方法， 返回值就在常量池中 

### String使用陷阱  

```java
String s1 = "a";
```

说明：在字符串常量池中创建了一个字面量为"a"的字符串。

```java
s1 = s1 + "b";
```

说明：实际上原来的“a”字符串对象已经丢弃了， 现在在堆空间中产生了一个字符串s1+"b"（也就是"ab")。如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大影响程序的性能。

```java
String s2 = "ab";
```

说明：直接在字符串常量池中创建一个字面量为"ab"的字符串。

```java
String s3 = "a" + "b";
```

说明： s3指向字符串常量池中已经创建的"ab"的字符串。

```java
String s4 = s1.intern();
```

说明：堆空间的s1对象在调用intern()之后，会将常量池中已经存在的"ab"字符串赋值给s4。  

```java
public class StringTest {
	String str = new String("good");
	char[] ch = { 't', 'e', 's', 't' };
    
	public void change(String str, char ch[]) {
		str = "test ok";
		ch[0] = 'b';
	}
    
	public static void main(String[] args) {
		StringTest ex = new StringTest();
		ex.change(ex.str, ex.ch);
		System.out.println(ex.str);//good
		System.out.println(ex.ch);//best
	}
}
```

说明：考察的是值传递，当ex.str作为参数传递到函数中时，实际是把地址给了第一个形参，由于String不可变，所以在试图更改对应字符串的内容时，地址所指的内容不变



### String常用方法

常用 API：

* `public boolean equals(String s)`：比较两个字符串内容是否相同、区分大小写

* `public boolean equalsIgnoreCase(String anotherString)`：比较字符串的内容，忽略大小写
* `public int length()`：返回此字符串的长度
* `public String trim()`：返回一个字符串，其值为此字符串，并删除任何前导和尾随空格
* `public String[] split(String regex)`：将字符串按给定的正则表达式分割成字符串数组
* `public char charAt(int index)`：取索引处的值
* `public char[] toCharArray()`：将字符串拆分为字符数组后返回
* `public boolean startsWith(String prefix)`：测试此字符串是否以指定的前缀开头
* `public int indexOf(String str)`：返回指定子字符串第一次出现的字符串内的索引，没有返回 -1
* `public int lastIndexOf(String str)`：返回字符串最后一次出现 str 的索引，没有返回 -1
* `public String substring(int beginIndex)`：返回子字符串，以原字符串指定索引处到结尾
* `public String substring(int i, int j)`：指定索引处扩展到 j - 1 的位置，字符串长度为 j - i
* `public String toLowerCase()`：将此 String 所有字符转换为小写，使用默认语言环境的规则
* `public String toUpperCase()`：使用默认语言环境的规则将此 String 所有字符转换为大写
* `public String replace(CharSequence target, CharSequence replacement)`：使用新值，将字符串中的旧值替换，得到新的字符串

```java
String s = 123-78;
s.replace("-","");//12378
```



### String与基本数据类型转换  

字符串——>基本数据类型、包装类

- Integer包装类的`public static int parseInt(String s)`：可以将由“数字”字符组成的**字符串转换为整型**
- 类似地,使用java.lang包中的Byte、 Short、 Long、 Float、 Double类调相应的类方法可以将由“数字”字符组成的字符串，转化为相应的基本数据类型

基本数据类型、包装类——>字符串

- 调用String类的`public String valueOf(int n)`可将**int型转换为字符串**
- 相应的`valueOf(byte b)、 valueOf(long l)、 valueOf(float f)、valueOf(doubled)、 valueOf(boolean b)`可由参数的相应类型到字符串的转换  

### String与字符数组转换  

字符数组——>字符串

String 类的构造器： `String(char[])` 和 `String(char[]， int offset， int length)` 分别用字符数组中的全部字符和部分字符创建字符串对象。

字符串——>字符数组

- public char[] `toCharArray()`： 将字符串中的全部字符存放在一个字符数组中的方法。
- public void `getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin)`： 提供了将指定索引范围内的字符串存放到数组中的方法。  

### String与字节数组转换

字节数组——>字符串

- `String(byte[])`： 通过使用平台的默认字符集解码指定的 byte 数组，构造一个新的 String。
- `String(byte[]， int offset， int length)` ： 用指定的字节数组的一部分，即从数组起始位置offset开始取length个字节构造一个字符串对象。

字符串——>字节数组

- public byte[] `getBytes()` ： 使用平台的默认字符集将此 String 编码为byte 序列，并将结果存储到一个新的 byte 数组中。
- public byte[] `getBytes(String charsetName)` ： 使用**指定的字符集**将此 String 编码到 byte 序列，并将结果存储到新的 byte 数组。  



## StringBuffer类  

`java.lang.StringBuffer`代表可变的字符序列， JDK1.0中声明，可以对字符串内容进行增删，此时**不会产生新的对象**。

- 很多方法与String相同。
- 作为参数传递时，方法内部可以改变值。  

### 创建对象

StringBuffer类不同于String，其对象必须使用构造器生成。有三个构造器：  

- `StringBuffer()`：初始容量为16的字符串缓冲区
- `StringBuffer(int size)`：构造指定容量的字符串缓冲区
- `StringBuffer(String str)`：将内容初始化为指定字符串内容  

```java
String s = new String("我喜欢学习");
StringBuffer buffer = new StringBuffer("我喜欢学习");
buffer.append("数学");  
```

![image-20220128132111654](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128132111654-166529427007727.png)

![image-20220128132123399](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128132123399-166529427007729.png)

### 常用方法  

`StringBuffer append(xxx)`：提供了很多的append()方法， 用于进行字符串拼接

`StringBuffer delete(int start,int end)`：删除指定位置的内容

`StringBuffer replace(int start, int end, String str)`：把`[start,end)`位置替换为str

`StringBuffer insert(int offset, xxx)`：在指定位置插入xxx

`StringBuffer reverse() `：把当前字符序列逆转  

- 当append和insert时，如果原来value数组长度不够，可扩容。
- 如上这些方法支持方法链操作。

方法链的原理  

![image-20220128133435513](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128133435513-166529427007730.png)

此外，还定义了如下的方法  

```java
public int indexOf(String str)
public String substring(int start,int end)
public int length()
public char charAt(int n )
public void setCharAt(int n ,char ch)
```



## StringBuilder类  

StringBuilder 和 StringBuffer 非常类似，均代表可变的字符序列， 而且提供相关功能的方法也一样

面试题：对比String、 StringBuffer、 StringBuilder

- String(JDK1.0)： 不可变字符序列
- StringBuffer(JDK1.0)： 可变字符序列、效率低、线程安全
- StringBuilder(JDK 5.0)：可变字符序列、效率高、 线程不安全

注意：作为参数传递的话，**方法内部String不会改变其值， StringBuffer和StringBuilder会改变其值**  

```java
//初始设置
long startTime = 0L
long endTime = 0L;
String text = "";
StringBuffer buffer = new StringBuffer("");
StringBuilder builder = new StringBuilder("");

//开始对比
startTime = System.currentTimeMillis();
for (int i = 0; i < 20000; i++) {
	buffer.append(String.valueOf(i));
}
endTime = System.currentTimeMillis();
System.out.println("StringBuffer的执行时间： " + (endTime - startTime));

startTime = System.currentTimeMillis();
for (int i = 0; i < 20000; i++) {
	builder.append(String.valueOf(i));
}
endTime = System.currentTimeMillis();
System.out.println("StringBuilder的执行时间： " + (endTime - startTime));

startTime = System.currentTimeMillis();
for (int i = 0; i < 20000; i++) {
	text = text + i;
}
endTime = System.currentTimeMillis();
System.out.println("String的执行时间： " + (endTime - startTime));
```



## JDK8之前日期时间API  

### java.lang.System类  

System类提供的public static long `currentTimeMillis()`用来返回当前时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差。此方法适于计算时间差

计算世界时间的主要标准有：

- UTC(Coordinated Universal Time)
- GMT(Greenwich Mean Time)
- CST(Central Standard Time)

### java.util.Date类  

表示特定的瞬间，精确到**毫秒**

- 构造器：
   `Date()`： 使用无参构造器创建的对象可以获取本地当前时间。
   `Date(long date)`：创建指定毫秒数的Date，形参是毫秒数，可以使用`对象.getTime()`

- 常用方法
   `getTime()`:返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象
  表示的毫秒数。
   `toString()`:把此 Date 对象转换为以下形式的 String： `dow mon dd hh:mm:ss zzz yyyy` 其中： `dow` 是一周中的某一天 `(Sun, Mon, Tue,Wed, Thu, Fri, Sat)`， `zzz`是时间标准。
   其它很多方法都过时了。  

```java
import java.util.Date;
Date date = new Date();

System.out.println(date);
System.out.println(System.currentTimeMillis());
System.out.println(date.getTime());

Date date1 = new Date(date.getTime());

System.out.println(date1.getTime());
System.out.println(date1.toString());
```

### java.text.SimpleDateFormat类  

Date类的API不易于国际化，大部分被废弃了,`java.text.SimpleDateFormat`类是一个不与语言环境有关的方式来格式化和解析日期的具体类。它允许进行格式化：日期——>文本、解析：文本——>日期

格式化：

- `SimpleDateFormat()` ：默认的模式和语言环境创建对象
- `public SimpleDateFormat(String pattern)`： 该**构造器**可以用参数pattern指定的格式创建一个对象，该对象调用：
- public String `format(Date date)`： 方法格式化时间对象date

解析：

- public Date `parse(String source)`： 从给定字符串的开始解析文本，以生成一个日期  

```java
import org.junit.Test;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class DataTest {

    @Test
    public void testSimpleDateFormat() throws ParseException {
        //实例化1:使用默认构造器
        SimpleDateFormat sdf=new SimpleDateFormat();
        //格式化日期：日期——>字符串
        Date date=new Date();
        System.out.println(date);
        String format=sdf.format(date);
        System.out.println(format);
        //解析：格式化的逆过程，字符串——>日期
        String str="22-1-28 下午3:03";
        Date date1=sdf.parse(str);
        System.out.println(date1);

        ////实例化2:指定格式创造对象
        SimpleDateFormat sdf1=new SimpleDateFormat("yyyy-MM-dd GGG hh:mm:ss aa");
        //格式化
        String format1=sdf1.format(date);
        System.out.println(format1);
        //解析
        Date date2=sdf1.parse("2022-01-28 公元 03:24:03 下午");
        System.out.println(date2);
    }
}

/*
输出结果：
Fri Jan 28 15:28:47 CST 2022
22-1-28 下午3:28
Fri Jan 28 15:03:00 CST 2022
2022-01-28 公元 03:28:47 下午
Fri Jan 28 15:24:03 CST 2022
*/
```

解析时要求字符串必须是符合SimpleDateFormat识别的格式，否则抛异常，见函数声明

关于pattern中字母的含义

![image-20220128153049425](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220128153049425-166529427007731.png)

### java.util.Calendar(日历)类  

Calendar是一个**抽象**基类，主用用于完成日期字段之间相互操作的功能。

获取Calendar实例的方法

- 使用`Calendar.getInstance()`方法
- 调用它的子类`GregorianCalendar`的构造器

一个Calendar的实例是系统时间的抽象表示，通过`get(int field)`方法来取得想要的时间信息。比如YEAR、 MONTH、 DAY_OF_WEEK、 HOUR_OF_DAY 、MINUTE、 SECOND

- public void set(int field,int value)
- public void add(int field,int amount)
- public final Date getTime()
- public final void setTime(Date date)  

```java
import org.junit.Test;

import java.util.Calendar;
import java.util.Date;

public class CalendarTest {

    @Test
    public void testCalendar(){
        //1.实例化
        //方式1：创建其子类(GregorianCalendar)的对象
        //方式2：调用其静态方法getInstance()
        Calendar calendar=Calendar.getInstance();
        System.out.println(calendar.getClass());

        //2.常用方法
        //get()
        int days1=calendar.get(Calendar.DAY_OF_MONTH);
        int days2=calendar.get(Calendar.DAY_OF_YEAR);
        System.out.println(days1);
        System.out.println(days2);
        //set()
        calendar.set(Calendar.DAY_OF_MONTH,22);
        int days3=calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println(days3);
        //add()
        calendar.add(Calendar.DAY_OF_MONTH,3);
        int days4=calendar.get(Calendar.DAY_OF_MONTH);
        System.out.println(days4);
        //getTime()
        Date date=calendar.getTime();
        System.out.println(date);
        //setTime
        Date date1=new Date();
        calendar.setTime(date1);
    }
}

/*
输出结果：
class java.util.GregorianCalendar
28
28
22
25
Tue Jan 25 15:58:20 CST 2022
*/
```

注意:

- 获取月份时： 一月是0，二月是1，以此类推， 12月是11
- 获取星期时： 周日是1，周二是2 ， 。 。。。周六是7  

## JDK8中新日期时间API  

### 新日期时间API出现的背景

如果我们可以跟别人说：“我们在1502643933071见面，别晚了！”那么就再简单不过了。但是我们希望时间与昼夜和四季有关，于是事情就变复杂了。 JDK 1.0中包含了一个java.util.Date类，但是它的大多数方法已经在JDK 1.1引入Calendar类之后被弃用了。而Calendar并不比Date好多少。它们面临的问题是：

- 可变性：像日期和时间这样的类应该是不可变的。
- 偏移性： Date中的年份是从1900开始的，而月份都从0开始。
- 格式化：格式化只对Date有用， Calendar则不行。
- 此外，它们也不是线程安全的；不能处理闰秒等。

### 新时间日期API  

第三次引入的API是成功的， 并且Java 8中引入的java.time API 已经纠正了过去的缺陷，将来很长一段时间内它都会为我们服务。

Java 8 吸收了 Joda-Time 的精华，以一个新的开始为 Java 创建优秀的 API。新的 java.time 中包含了所有关于本地日期（LocalDate）、本地时间（LocalTime）、本地日期时间（LocalDateTime）、时区（ZonedDateTime）和持续时间（Duration）的类。历史悠久的 Date 类新增了 `toInstant()` 方法，用于把 Date 转换成新的表示形式。这些新增的本地化时间日期 API 大大简化了日期时间和本地化的管理。  

新时间日期API  

- java.time – 包含值对象的基础包
- java.time.chrono – 提供对不同的日历系统的访问
- java.time.format – 格式化和解析时间和日期
- java.time.temporal – 包括底层框架和扩展特性
- java.time.zone – 包含时区支持的类  

大多数开发者只会用到基础包和format包，也可能会用到temporal包。因此，尽管有68个新的公开类型，大多数开发者，大概将只会用到其中的三分之一  

LocalDate、 LocalTime、 LocalDateTime 类是其中较重要的几个类，它们的实例是不可变的对象，分别表示使用 ISO-8601日历系统的日期、时间、日期和时间。它们提供了简单的本地日期或时间，并不包含当前的时间信息，也不包含与时区相关的信息。

- LocalDate代表IOS格式（yyyy-MM-dd）的日期,可以存储生日、纪念日等日期。
- LocalTime表示一个时间，而不是日期。
- LocalDateTime是用来表示日期和时间的， 这是一个最常用的类之一。  

ISO-8601日历系统是国际标准化组织制定的现代公民的日期和时间的表示法，也就是公历。  

| 方法                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `now() / * now(ZoneId zone)`                                 | 静态方法， 根据当前时间**创建对象**/指定时区的对象           |
| `of()`                                                       | 静态方法， 根据指定日期/时间创建对象                         |
| `getDayOfMonth()/getDayOfYear()`                             | 获得月份天数(1-31) /获得年份天数(1-366)                      |
| `getDayOfWeek()`                                             | 获得星期几(返回一个 DayOfWeek 枚举值)                        |
| `getMonth()`                                                 | 获得月份, 返回一个 Month 枚举值                              |
| `getMonthValue() / getYear()`                                | 获得月份(1-12) /获得年份                                     |
| `getHour()/getMinute()/getSecond()`                          | 获得当前对象对应的小时、 分钟、 秒                           |
| `withDayOfMonth()/withDayOfYear()/ withMonth()/withYear()`   | 将月份天数、 年份天数、 月份、 年份修改为指定的值并返回**新的对象** |
| `plusDays(), plusWeeks(), plusMonths(), plusYears(),plusHours()` | 向当前对象添加几天、 几周、 几个月、 几年、 几小时           |
| `minusMonths() / minusWeeks()/ minusDays()/minusYears()/minusHours()` | 从当前对象减去几月、 几周、 几天、 几年、 几小时             |

```java
import org.junit.Test;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

public class NewTimeTest {
    @Test
    public void test1(){
        //now：获取当前的日期、时间、日期时间
        LocalDate localDate = LocalDate.now();
        LocalTime localTime = LocalTime.now();
        LocalDateTime localDateTime = LocalDateTime.now();

        System.out.println(localDate);
        System.out.println(localTime);
        System.out.println(localDateTime);

        //of：设置指定时间的年月日时分秒，没有偏移量
        LocalDateTime localDateTime1 = localDateTime.of(2022, 01,20,15,38);
        System.out.println(localDateTime1);

        //getXxx：获取相关信息
        System.out.println(localDateTime1.getDayOfMonth());
        System.out.println(localDateTime1.getDayOfWeek());
        System.out.println(localDateTime1.getHour());

        //with：修改日期
        System.out.println(localDateTime1.withYear(2019));
        System.out.println(localDateTime1.withMonth(10));
        System.out.println(localDateTime1.withDayOfMonth(12));
        System.out.println(localDateTime1);//不可变性

        //minus、plus
        System.out.println(localDateTime1.plusDays(2));
        System.out.println(localDateTime1.minusDays(2));
        System.out.println(localDateTime1);//不可变性
    }
}
/*
输出结果：
2022-01-29
15:56:53.826
2022-01-29T15:56:53.826

2022-01-20T15:38

20
THURSDAY
15

2019-01-20T15:38
2022-10-20T15:38
2022-01-12T15:38
2022-01-20T15:38

2022-01-22T15:38
2022-01-18T15:38
2022-01-20T15:38
*/
```

### 瞬时： Instant  

Instant：时间线上的一个瞬时点。 这可能被用来记录应用程序中的事件时间戳。

在处理时间和日期的时候，我们通常会想到年,月,日,时,分,秒。然而，这只是时间的一个模型，是面向人类的。第二种通用模型是面向机器的，或者说是连续的。在此模型中，时间线中的一个点表示为一个很大的数，这有利于计算机处理。 在UNIX中，这个数从1970年开始，以秒为的单位；同样的，在Java中，也是从1970年开始，但以**毫秒**为单位。

java.time包通过值类型Instant提供机器视图，不提供处理人类意义上的时间单位。Instant表示时间线上的一点，而不需要任何上下文信息，例如，时区。概念上讲， 它只是简单的表示自1970年1月1日0时0分0秒（ UTC）开始的**秒数**。 因为java.time包是基于纳秒计算的，所以Instant的**精度可以达到纳秒级**。

| 方法                            | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| `now()`                         | **静态方法**， **返回**默认UTC时区的Instant类的**对象**      |
| `ofEpochMilli(long epochMilli)` | **静态方法**，返回在1970-01-01 00:00:00基础上加上指定毫秒的Instant类的对象 |
| `atOffset(ZoneOffset offset)`   | 结合即时的偏移来创建一个 OffsetDateTime对象                  |
| `toEpochMilli()`                | 返回1970-01-01 00:00:00到当前时间的毫秒数， 即为时间戳       |

时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数。  

```java
import org.junit.Test;

import java.time.Instant;
import java.time.OffsetDateTime;
import java.time.ZoneOffset;

public class InstantTest {

    @Test
    public void test2(){
        //获取本初子午线对应标准时间
        Instant instant = Instant.now();
        System.out.println(instant);//与北京时间差8h

        //添加当前时区对应的偏移量
        OffsetDateTime offsetDateTime = instant.atOffset(ZoneOffset.ofHours(8));
        System.out.println(offsetDateTime);

        //返回1970-01-01 00:00:00到当前时间的毫秒数， 即为时间戳
        System.out.println(instant.toEpochMilli());

        //静态方法，返回在1970-01-01 00:00:00基础上加上指定毫秒的Instant类的对象
        System.out.println(Instant.ofEpochMilli(1643444093400L));
    }
}
/*
输出结果
2022-01-29T09:03:54.745Z
2022-01-29T17:03:54.745+08:00
1643447034745
2022-01-29T08:14:53.400Z
```

### 格式化与解析日期或时间  

java.time.format.DateTimeFormatter 类：该类提供了**三种格式化方法**：

预定义的标准格式。如：

- `ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME`
- 本地化相关的格式。如：`ofLocalizedDateTime(FormatStyle.LONG)`
- 自定义的格式。如：`ofPattern(“yyyy-MM-dd hh:mm:ss”)`  

| 方 法                        | 描 述                                                        |
| ---------------------------- | ------------------------------------------------------------ |
| `ofPattern(String pattern)`  | 静 态 方 法 ， 返 回 一 个 指 定 字 符 串 格 式 的 DateTimeFormatter |
| `format(TemporalAccessor t)` | 格式化一个日期、 时间， 返回字符串                           |
| `parse(CharSequence text)`   | 将指定格式的字符序列解析为一个日期、 时间                    |

```java
import org.junit.Test;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.format.FormatStyle;
import java.time.temporal.TemporalAccessor;

public class FormatTest {
@Test
    public void test3(){
        //方式1：预定义的标准格式
        DateTimeFormatter formatter=DateTimeFormatter.ISO_LOCAL_DATE_TIME;
        String str1=formatter.format(LocalDateTime.now());
        System.out.println(str1);

        //解析：字符串——>日期
        TemporalAccessor parse=formatter.parse("2019-02-18T15:42:18.789");
        System.out.println(parse);

        //方式2：本地化相关的格式
        DateTimeFormatter formatter1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG);
        String str2=formatter1.format(LocalDateTime.now());
        System.out.println(str2);

        //方式3：自定义格式
        DateTimeFormatter formatter2 = DateTimeFormatter.ofPattern("yyyy-mm-dd");
        String str3=formatter2.format(LocalDateTime.now());
        System.out.println(str3);
    }
}
/*
输出结果
2022-01-29T17:04:37.103
{},ISO resolved to 2019-02-18T15:42:18.789
2022年1月29日 下午05时04分37秒
2022-04-29
```

### 其它API

ZoneId： 该类中包含了所有的时区信息， 一个时区的ID， 如 Europe/Paris

ZonedDateTime： 一个在ISO-8601日历系统时区的日期时间， 如 2007-12-03T10:15:30+01:00 Europe/Paris。

其中每个时区都对应着ID， 地区ID都为“ {区域}/{城市}” 的格式， 例如：Asia/Shanghai等

Clock： 使用时区提供对当前即时、 日期和时间的访问的时钟。

持续时间： Duration， 用于计算两个“时间” 间隔

日期间隔： Period， 用于计算两个“日期” 间隔

TemporalAdjuster : 时间校正器。有时我们可能需要获取例如：将日期调整到“下一个工作日”等操作。

TemporalAdjusters : 该类通过静态方法(firstDayOfXxx()/lastDayOfXxx()/nextXxx())提供了大量的常用TemporalAdjuster 的实现。  

### 与传统日期处理的转换  

| 类                                                        | To 遗留类                             | From 遗留类                 |
| --------------------------------------------------------- | ------------------------------------- | --------------------------- |
| java.time.Instant与java.util.Date                         | Date.from(instant)                    | date.toInstant()            |
| java.time.Instant与java.sql.Timestamp                     | Timestamp.from(instant)               | timestamp.toInstant()       |
| java.time.ZonedDateTime与 java.util.GregorianCalendar     | GregorianCalendar.from(zonedDateTime) | cal.toZonedDateTime()       |
| java.time.LocalDate与java.sql.Time                        | Date.valueOf(localDate)               | date.toLocalDate()          |
| java.time.LocalTime与java.sql.Time                        | Date.valueOf(localDate)               | date.toLocalTime()          |
| java.time.LocalDateTime与 java.sql.Timestamp              | Timestamp.valueOf(localDateTime)      | timestamp.toLocalDateTime() |
| java.time.ZoneId与java.util.TimeZone                      | Timezone.getTimeZone(id)              | timeZone.toZoneId()         |
| java.time.format.DateTimeFormatter与 java.text.DateFormat | formatter.toFormat()                  | 无                          |

## Java比较器  

在Java中经常会涉及到对象数组的排序问题，那么就涉及到对象之间的比较问题。Java实现对象排序的方式有两种：

- 自然排序： java.lang.Comparable
- 定制排序： java.util.Comparator  



### 自然排序  

Comparable**接口**强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序。

**对于自定义类：**实现 Comparable接口的类必须实现 `compareTo(Object obj)` 方法，该类的两个对象可通过 `compareTo(Object obj)` 方法的返回值来**比较大小**。 **如果当前对象this大于形参对象obj， 则返回正整数**，如果当前对象this小于形参对象obj， 则返回负整数，如果当前对象this等于形参对象obj， 则返回零。

实现Comparable接口的对象的**列表、数组**可以通过 `Collections.sort(Object[] o)` 或`Arrays.sort(Object[] o)`进行**自动排序**。实现此接口的对象可以用作**有序映射中的键或有序集合中的元素**，无需指定比较器。

```java
class Goods implements Comparable{
    private String name;
    private double price;

    Goods(String name, double price) {
        this.name = name;
        this.price = price;
    }

    @Override
    public int compareTo(Object o) {
        if(o instanceof Goods){
            Goods goods=(Goods)o;
            if(this.price>goods.price){
                return 1;
            }else if(this.price<goods.price){
                return -1;
            }else{
                return 0;
            }
        }else{
        throw new RuntimeException("输入数据类型异常");
        }
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public double getPrice() {
        return price;
    }
    public void setPrice(double price) {
        this.price = price;
    }
}

public class CompareTest {
    @Test
    public void test1(){
        Goods[] arr=new Goods[4];
        arr[0]= new Goods("HUAWEI", 5000);
        arr[1]= new Goods("APPLE", 8000);
        arr[2]= new Goods("OPPO", 3000);
        arr[3]= new Goods("XIAOMI", 2000);
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));
    }
}
```

对于类 C 的每一个 e1 和 e2 来说，当且仅当 `e1.compareTo(e2) == 0` 与`e1.equals(e2)` 具有相同的 boolean 值时，类 C 的自然排序才叫做与 equals一致。 建议（虽然不是必需的） 最好使自然排序与 equals 一致。  

**对于Comparable 的典型实现**： (默认都是从小到大排列的)

- String：按照字符串中**字符的Unicode值**进行比较
- Character：按照**字符的Unicode值**来进行比较
- 数值类型对应的包装类以及BigInteger、 BigDecimal：按照它们**对应的数值大小**进行比较
- Boolean： true 对应的包装类实例大于 false 对应的包装类实例
- Date、 Time等：后面的日期时间比前面的日期时间大  



### 定制排序  

当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码，或者实现了java.lang.Comparable接口的排序规则不适合当前的操作(比如对String等类以其他规则进行排序)，可以考虑使用**实现了Comparator的类的对象**来排序， 强行对多个对象进行整体排序的比较。

- 重写`compare(Object o1,Object o2)`方法（**此处有两个对象形参，与Comparable相区别，所以更加灵活**），比较o1和o2的大小： 如果方法返回正整数，则表示o1大于o2；如果返回0，表示相等；返回负整数，表示o1小于o2。
- 可以将 Comparator 传递给 sort 方法（如 `Collections.sort` 或`Arrays.sort`），从而允许在排序顺序上实现精确控制。
- 还可以使用 Comparator 来控制某些数据结构（如有序 set或有序映射）的顺序，或者为那些没有自然顺序的对象 collection 提供排序  

## System类  

System类代表系统，系统级的很多属性和控制方法都放置在该类的内部。该类位于java.lang包。由于该类的构造器是private的，所以无法创建该类的对象，也就是无法实例化该类。其内部的成员变量和成员方法都是static的， 所以也可以很方便的进行调用。

成员变量

System类内部包含`in、 out、err`三个成员变量，分别代表标准输入流(键盘输入)，标准输出流(显示器)和标准错误输出流(显示器)。

成员方法

- native long `currentTimeMillis()`：该方法的作用是返回当前的计算机时间，时间的表达格式为当前计算机时间和GMT时间(格林威治时间)1970年1月1号0时0分0秒所差的毫秒数。

- void `exit(int status)`：该方法的作用是退出程序。其中status的值为0代表正常退出，非零代表异常退出。 使用该方法可以在图形界面编程中实现程序的退出功能等。  

- void `gc()`：该方法的作用是请求系统进行垃圾回收。至于系统是否立刻回收，则取决于系统中垃圾回收算法的实现以及系统执行时的情况。

- String `getProperty(String key)` ：该方法的作用是获得系统中属性名为key的属性对应的值。系统中常见的属性名以及属性的作用如下表所示：  

  ![image-20220129190822818](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220129190822818-166529427007732.png)

## Math类  

java.lang.Math提供了一系列静态方法用于科学计算。其方法的参数和返回值类型一般为double型。

顾名思义，`Math`类就是用来进行数学计算的，它提供了大量的静态方法来便于我们实现数学计算：

求绝对值：

```java
Math.abs(-100); // 100
Math.abs(-7.8); // 7.8
```

取最大或最小值：

```java
Math.max(100, 99); // 100
Math.min(1.2, 2.3); // 1.2
```

计算x的y次方：

```java
Math.pow(2, 10); // 2的10次方=1024
```

计算√x：

```java
Math.sqrt(2); // 1.414...
```

计算e的x次方：

```java
Math.exp(2); // 7.389...
```

计算以e为底的对数：

```java
Math.log(4); // 1.386...
```

计算以10为底的对数：

```java
Math.log10(100); // 2
```

三角函数：

```java
Math.sin(3.14); // 0.00159...
Math.cos(3.14); // -0.9999...
Math.tan(3.14); // -0.0015...
Math.asin(1.0); // 1.57079...
Math.acos(1.0); // 0.0
```

Math还提供了几个数学常量：

```java
double pi = Math.PI; // 3.14159...
double e = Math.E; // 2.7182818...
Math.sin(Math.PI / 6); // sin(π/6) = 0.5
```

**获取随机数**

`Math.random()`随机产生一个数属于`[0.0,1.0)`

想要在[a,b]中获取随机数，则使用`Math.random()*(b-a+1)+a`

```java
double value=Math.random()*90+10;
```

Java标准库还提供了一个`StrictMath`，它提供了和`Math`几乎一模一样的方法。这两个类的区别在于，由于浮点数计算存在误差，不同的平台（例如x86和ARM）计算的结果可能不一致（指误差不同），因此，`StrictMath`保证所有平台计算结果都是完全相同的，而`Math`会尽量针对平台优化计算速度，所以，绝大多数情况下，使用`Math`就足够了。

## BigInteger与BigDecimal

## BigInteger类

Integer类作为int的包装类，能存储的最大整型值为231-1， Long类也是有限的，最大为263-1。 如果要表示再大的整数，不管是基本数据类型还是他们的包装类都无能为力，更不用说进行运算了。

java.math包的BigInteger可以表示**不可变的**任意精度的**整数**。 BigInteger 提供所有 Java 的基本整数操作符的对应物，并提供 java.lang.Math 的所有相关方法。另外，BigInteger 还提供以下运算：模算术、 GCD 计算、质数测试、素数生成、位操作以及一些其他操作。

构造器：`BigInteger(String val)`根据**字符串**构建BigInteger对象  

常用方法

public BigInteger `abs()`：返回此 BigInteger 的绝对值的 BigInteger。

BigInteger `add(BigInteger val)` ：返回其值为 (this + val) 的 BigInteger

BigInteger `subtract(BigInteger val)` ：返回其值为 (this - val) 的 BigInteger

BigInteger `multiply(BigInteger val)` ：返回其值为 (this * val) 的 BigInteger

BigInteger `divide(BigInteger val)` ：返回其值为 (this / val) 的 BigInteger。整数相除只保留整数部分。

BigInteger `remainder(BigInteger val)` ：返回其值为 (this % val) 的BigInteger。

BigInteger[] `divideAndRemainder(BigInteger val)`：返回包含 (this / val) 后跟(this % val) 的两个 BigInteger 的数组。

BigInteger `pow(int exponent)` ：返回其值为 (thisexponent) 的 BigInteger。  

### BigDecimal类

一般的Float类和Double类可以用来做科学计算或工程计算，但在商业计算中，要求数字精度比较高，故用到java.math.BigDecimal类。BigDecimal类支持不可变的、任意精度的有符号十进制定点数。

构造器

`public BigDecimal(double val)`

`public BigDecimal(String val)`

常用方法

public BigDecimal `add(BigDecimal augend)`

public BigDecimal `subtract(BigDecimal subtrahend)`

public BigDecimal `multiply(BigDecimal multiplicand)`

public BigDecimal `divide(BigDecimal divisor, int scale, int roundingMode)`  

## 枚举类的使用

**类的对象只有有限个，确定的**。 举例如下  

- 星期： Monday(星期一)、 ......、 Sunday(星期天)
- 性别： Man(男)、 Woman(女)
- 季节： Spring(春节)......Winter(冬天)
- 支付方式： Cash（现金）、 WeChatPay（微信）、 Alipay(支付宝)、 BankCard(银行卡)、 CreditCard(信用卡)
- 就职状态： Busy、 Free、 Vocation、 Dimission
- 订单状态： Nonpayment（未付款）、 Paid（已付款） 、 Delivered（已发货）、Return（退货）、 Checked（已确认） Fulfilled（已配货）、
- 线程状态：创建、就绪、运行、阻塞、死亡  

当需要定义一组常量时，强烈建议使用枚举类    

若枚举只有一个对象, 则可以作为一种单例模式的实现方式  

### 枚举类的属性

- 枚举类对象的**属性不应允许被改动**, 所以应该使用 `private final` 修饰
- 枚举类的使用 `private final` 修饰的属性应该在**构造器**中为其赋值
- 若枚举类显式的定义了带参数的构造器, 则在列出枚举值时也必须对应的传入参数  

### 枚举类的实现

- JDK1.5之前需要自定义枚举类
- JDK 1.5 新增的 enum 关键字用于定义枚举类

#### 自定义枚举类 

- 私有化类的构造器，保证不能在类的外部创建其对象
- 在类的内部创建枚举类的实例。声明为： `public static final`
- 对象如果有实例变量，应该声明为`private final`，并在构造器中初始化  

```java
class Season{
	private final String SEASONNAME;//季节的名称
	private final String SEASONDESC;//季节的描述
	private Season(String seasonName,String seasonDesc){
		this.SEASONNAME = seasonName;
		this.SEASONDESC = seasonDesc;
	}
	public static final Season SPRING = new Season("春天", "春暖花开");
	public static final Season SUMMER = new Season("夏天", "夏日炎炎");
	public static final Season AUTUMN = new Season("秋天", "秋高气爽");
	public static final Season WINTER = new Season("冬天", "白雪皑皑");
}
```

#### 使用enum定义枚举类

使用说明

- 使用 enum 定义的枚举类默认继承了 java.lang.Enum类，因此**不能再继承其他类**
- 枚举类的**构造器只能使用 private** 权限修饰符
- 枚举类的所有实例必须在枚举类中显式列出(, 分隔   ; 结尾)。列出的实例系统会自动添加 public static final 修饰
- 必须在枚举类的第一行声明枚举类对象  

```java
enum SeasonEnum {
	SPRING("春天","春风又绿江南岸"),
	SUMMER("夏天","映日荷花别样红"),
	AUTUMN("秋天","秋水共长天一色"),
	WINTER("冬天","窗含西岭千秋雪");
	private final String seasonName;
	private final String seasonDesc;
	private SeasonEnum(String seasonName, String seasonDesc) {
		this.seasonName = seasonName;
		this.seasonDesc = seasonDesc;
	}
	public String getSeasonName() {
		return seasonName;
	}
	public String getSeasonDesc() {
		return seasonDesc;
	}
}
```

```java
public class Test2 {
    public static void main(String[] args) {
        EnumTest color=EnumTest.BLANK;
        switch (color) {
            case RED:
                color = EnumTest.GREEN;
                break;
            case YELLOW:
                color = EnumTest.RED;
                break;
            case GREEN:
                color = EnumTest.YELLOW;
                break;
        }
    }
}
```

### Enum类的主要方法

![image-20220129234516585](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220129234516585-166529427007734.png)

Enum类的主要方法：

- values()方法：返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值。
- valueOf(String str)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。
- toString()：返回当前枚举类对象常量的名称  

和普通 Java 类一样，枚举类可以实现一个或多个接口

- 若每个枚举值在调用实现的接口方法呈现相同的行为方式，则只要统一实现该方法即可
- 若需要每个枚举值在调用实现的接口方法呈现出不同的行为方式,则可以让每个枚举值分别来实现该方法  

JDK 1.5 中可以在 switch 表达式中**使用Enum定义的枚举类的对象作为表达式, case 子句可以直接使用枚举值的名字**, 无需添加枚举类作为限定。  

```java
import org.junit.Test;
/**
 * @author HanJL
 * @create 2022/1/30 9:56
 * @description
 */
interface Info{
    void show();
}

enum Season implements Info{
    SPRING("春天","春风又绿江南岸"){
        public void show(){
            System.out.println("春天在哪里");
        }
    },
    SUMMER("夏天","映日荷花别样红"){
        public void show(){
            System.out.println("宁夏");
        }
    },
    AUTUMN("秋天","秋水共长天一色"){
        public void show(){
            System.out.println("秋天不回来");
        }
    },
    WINTER("冬天","窗含西岭千秋雪"){
        public void show(){
            System.out.println("大约在冬季");
        }
    };
    private final String seasonName;
    private final String seasonDesc;
    private Season(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
    public String getSeasonName() {
        return seasonName;
    }
    public String getSeasonDesc() {
        return seasonDesc;
    }
}

public class EnumTest {
    @Test
    public void test1() {
        Season summer = Season.SUMMER;
        //toString()
        System.out.println(summer);
        System.out.println(summer.toString());
        //values()
        Season[] values = Season.values();
        //实现接口的方法
        for (int i = 0; i < values.length; i++) {
            System.out.println(values[i]);
            values[i].show();
        }
        //valueOf
        Season winter = Season.valueOf("WINTER");
        System.out.println(winter);
        //switch case
        Season season1 = Season.valueOf("SPRING");
        switch(season1){
            case SPRING:
                System.out.println("season1是SPRING");
                break;
            case SUMMER:
                System.out.println("season1是SUMMER");
                break;
            case AUTUMN:
                System.out.println("season1是AUTUMN");
                break;
            case WINTER:
                System.out.println("season1是AUTUMN");
                break;
        }
    }
}

/*输出结果
SUMMER
SUMMER
SPRING
春天在哪里
SUMMER
宁夏
AUTUMN
秋天不回来
WINTER
大约在冬季
WINTER
season1是SPRING
*/
```



## Regex

### 概述

正则表达式的作用：是一些特殊字符组成的校验规则，可以校验信息的正确性，校验邮箱、电话号码、金额等。

比如检验 qq 号：

```java
public static boolean checkQQRegex(String qq){
    return qq!=null && qq.matches("\\d{4,}");//即是数字 必须大于4位数
}// 用\\d  是因为\用来告诉它是一个校验类，不是普通的字符 比如 \t \n
```

java.util.regex 包主要包括以下三个类：

- Pattern 类：

  Pattern 对象是一个正则表达式的编译表示。Pattern 类没有公共构造方法，要创建一个 Pattern 对象，必须首先调用其公共静态编译方法，返回一个 Pattern 对象。该方法接受一个正则表达式作为它的第一个参数

- Matcher 类：

  Matcher 对象是对输入字符串进行解释和匹配操作的引擎。与Pattern 类一样，Matcher 也没有公共构造方法，需要调用 Pattern 对象的 matcher 方法来获得一个 Matcher 对象

- PatternSyntaxException：

  PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误。



***



### 字符匹配

#### 普通字符

字母、数字、汉字、下划线、以及没有特殊定义的标点符号，都是“普通字符”。表达式中的普通字符，在匹配一个字符串的时候，匹配与之相同的一个字符。其他统称**元字符**



***



#### 特殊字符

\r\n 是 Windows 中的文本行结束标签，在 Unix/Linux 则是 \n

| 元字符 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| \      | 将下一个字符标记为一个特殊字符或原义字符，告诉它是一个校验类，不是普通字符 |
| \f     | 换页符                                                       |
| \n     | 换行符                                                       |
| \r     | 回车符                                                       |
| \t     | 制表符                                                       |
| \\     | 代表 \ 本身                                                  |
| ()     | 使用 () 定义一个子表达式。子表达式的内容可以当成一个独立元素 |



***



#### 标准字符

能够与多种字符匹配的表达式，注意区分大小写，大写是相反的意思，只能校验**单**个字符。

| 元字符 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| .      | 匹配任意一个字符（除了换行符），如果要匹配包括 \n 在内的所有字符，一般用 [\s\S] |
| \d     | 数字字符，0~9 中的任意一个，等价于 [0-9]                     |
| \D     | 非数字字符，等价于  [ ^0-9]                                  |
| \w     | 大小写字母或数字或下划线，等价于[a-zA-Z_0-9_]                |
| \W     | 对\w取非，等价于[ ^\w]                                       |
| \s     | 空格、制表符、换行符等空白字符的其中任意一个，等价于[\f\n\r\t\v] |
| \S     | 对 \s 取非                                                   |

\x 匹配十六进制字符，\0 匹配八进制，例如 \xA 对应值为 10 的 ASCII 字符 ，即 \n



***



#### 自定义符

自定义符号集合，[ ] 方括号匹配方式，能够匹配方括号中**任意一个**字符

| 元字符       | 说明                                      |
| ------------ | ----------------------------------------- |
| [ab5@]       | 匹配 "a" 或 "b" 或 "5" 或 "@"             |
| [^abc]       | 匹配 "a","b","c" 之外的任意一个字符       |
| [f-k]        | 匹配 "f"~"k" 之间的任意一个字母           |
| [^A-F0-3]    | 匹配 "A","F","0"~"3" 之外的任意一个字符   |
| [a-d[m-p]]   | 匹配 a 到 d 或者 m 到 p：[a-dm-p]（并集） |
| [a-z&&[m-p]] | 匹配 a 到 z 并且 m 到 p：[a-dm-p]（交集） |
| [^]          | 取反                                      |

* 正则表达式的特殊符号，被包含到中括号中，则失去特殊意义，除了 ^,- 之外，需要在前面加 \

* 标准字符集合，除小数点外，如果被包含于中括号，自定义字符集合将包含该集合。
  比如：[\d. \ -+] 将匹配：数字、小数点、+、-



***



#### 量词字符

修饰匹配次数的特殊符号。

* 匹配次数中的贪婪模式(匹配字符越多越好，默认 ！)，\* 和 + 都是贪婪型元字符。
* 匹配次数中的非贪婪模式（匹配字符越少越好，修饰匹配次数的特殊符号后再加上一个 ? 号）

| 元字符 | 说明                              |
| ------ | --------------------------------- |
| X?     | X 一次或一次也没，有相当于 {0,1}  |
| X*     | X 不出现或出现任意次，相当于 {0,} |
| X+     | X 至少一次，相当于 {1,}           |
| X{n}   | X 恰好 n 次                       |
| {n,}   | X 至少 n 次                       |
| {n,m}  | X 至少 n 次，但是不超过 m 次      |



***



### 位置匹配

#### 字符边界

本组标记匹配的不是字符而是位置，符合某种条件的位置

| 元字符 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| ^      | 与字符串开始的地方匹配（在字符集合中用来求非，在字符集合外用作匹配字符串的开头） |
| $      | 与字符串结束的地方匹配                                       |
| \b     | 匹配一个单词边界                                             |



***



#### 捕获组

捕获组是把多个字符当一个单独单元进行处理的方法，它通过对括号内的字符分组来创建。

在表达式 `((A)(B(C)))`，有四个这样的组：((A)(B(C)))、(A)、(B(C))、(C)（按照括号从左到右依次为 group(1)...）

* 调用 matcher 对象的 groupCount 方法返回一个 int 值，表示 matcher 对象当前有多个捕获组。
* 特殊的组 group(0)、group()，代表整个表达式，该组不包括在 groupCount 的返回值中。 

| 表达式                    | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| \|  (分支结构)            | 左右两边表达式之间 "或" 关系，匹配左边或者右边               |
| ()  (捕获组)              | (1) 在被修饰匹配次数的时候，括号中的表达式可以作为整体被修饰<br/>(2) 取匹配结果的时候，括号中的表达式匹配到的内容可以被单独得到<br/>(3) 每一对括号分配一个编号,()的捕获根据左括号的顺序从 1 开始自动编号。捕获元素编号为零的第一个捕获是由整个正则表达式模式匹配的文本 |
| (?:Expression)   非捕获组 | 一些表达式中，不得不使用( )，但又不需要保存 () 中子表达式匹配的内容，这时可以用非捕获组来抵消使用( )带来的副作用。 |



***



#### 反向引用

反向引用（\number），又叫回溯引用：

* 每一对()会分配一个编号，使用 () 的捕获根据左括号的顺序从1开始自动编号

* 通过反向引用，可以对分组已捕获的字符串进行引用，继续匹配

* **把匹配到的字符重复一遍在进行匹配**

* 应用 1：

  ```java
  String regex = "((\d)3)\1[0-9](\w)\2{2}";
  ```

  * 首先匹配 ((\d)3)，其次 \1 匹配 ((\d)3) 已经匹配到的内容，\2 匹配 (\d)， {2} 指的是 \2 的值出现两次
  * 实例：23238n22（匹配到 2 未来就继续匹配 2）
  * 实例：43438n44

* 应用 2：爬虫

  ```java
  String regex = "<(h[1-6])>\w*?<\/\1>";
  ```

  匹配结果

  ```java
  <h1>x</h1>//匹配
  <h2>x</h2>//匹配
  <h3>x</h1>//不匹配
  ```

  

***



#### 零宽断言

预搜索（零宽断言）（环视）

* 只进行子表达式的匹配，匹配内容不计入最终的匹配结果，是零宽度

* 判断当前位置的前后字符，是否符合指定的条件，但不匹配前后的字符，**是对位置的匹配**

* 正则表达式匹配过程中，如果子表达式匹配到的是字符内容，而非位置，并被保存到最终的匹配结果中，那么就认为这个子表达式是占有字符的；如果子表达式匹配的仅仅是位置，或者匹配的内容并不保存到最终的匹配结果中，那么就认为这个子表达式是**零宽度**的。占有字符还是零宽度，是针对匹配的内容是否保存到最终的匹配结果中而言的

  | 表达式   | 说明                                    |
  | -------- | --------------------------------------- |
  | (?=exp)  | 断言自身出现的位置的后面能匹配表达式exp |
  | (?<=exp) | 断言自身出现的位置的前面能匹配表达式exp |
  | (?!exp)  | 断言此位置的后面不能匹配表达式exp       |
  | (?<!exp) | 断言此位置的前面不能匹配表达式exp       |




***



### 匹配模式

正则表达式的匹配模式：

* IGNORECASE 忽略大小写模式
  * 匹配时忽略大小写。
  * 默认情况下，正则表达式是要区分大小写的。
* SINGLELINE 单行模式
  * 整个文本看作一个字符串，只有一个开头，一个结尾。
  * 使小数点 "." 可以匹配包含换行符（\n）在内的任意字符。
* MULTILINE 多行模式
  * 每行都是一个字符串，都有开头和结尾。
  * 在指定了 MULTILINE 之后，如果需要仅匹配字符串开始和结束位置，可以使用 \A 和 \Z



***



### 分组匹配

Pattern 类：

* `static Pattern compile(String regex)`：将给定的正则表达式编译为模式
* `Matcher matcher(CharSequence input)`：创建一个匹配器，匹配给定的输入与此模式
* `static boolean matches(String regex, CharSequence input)`：编译正则表达式，并匹配输入

Matcher 类：

* `boolean find()`：扫描输入的序列，查找与该模式匹配的下一个子序列
* `String group()`：返回与上一个匹配的输入子序列，同 group(0)，匹配整个表达式的子字符串
* `String group(int group)`：返回在上一次匹配操作期间由给定组捕获的输入子序列 
* `int groupCount()`：返回此匹配器模式中捕获组的数量

```java
public class Demo01{
	public static void main(String[] args) {
		//表达式对象
		Pattern p = Pattern.compile("\\w+");
		//创建Matcher对象
		Matcher m = p.matcher("asfsdf2&&3323");
		//boolean b = m.matches();//尝试将整个字符序列与该模式匹配
		//System.out.println(b);//false
		//boolean b2 = m.find();//该方法扫描输入的序列，查找与该模式匹配的下一个子序列
		//System.out.println(b2);//true
		
		//System.out.println(m.find());
		//System.out.println(m.group());//asfsdf2
		//System.out.println(m.find());
		//System.out.println(m.group());//3323
		
		while(m.find()){
			System.out.println(m.group());	//group(),group(0)匹配整个表达式的子字符串
			System.out.println(m.group(0));
		}
		
	}
}
```

```java
public class Demo02 {
	public static void main(String[] args) {
		//在这个字符串：asfsdf23323，是否符合指定的正则表达式：\w+
		//表达式对象
        Pattern p = Pattern.compile("(([a-z]+)([0-9]+))");//不需要加多余的括号
		//创建Matcher对象
		Matcher m = p.matcher("aa232**ssd445");
	
		while(m.find()){
			System.out.println(m.group());//aa232  ssd445
			System.out.println(m.group(1));//aa232  ssd445
			System.out.println(m.group(2));//aa     ssd
            System.out.println(m.group(3));//232    445 
		}
	}
}
```

* 正则表达式改为 `"(([a-z]+)(?:[0-9]+))"`   没有 group(3) 因为是非捕获组
* 正则表达式改为 `"([a-z]+)([0-9]+)"`  没有 group(3)    aa232  - aa  --232



***



### 应用

#### 基本验证

```java
public static void main(String[] args){
	System.out.println("a".matches("[abc]"));//true判断a是否在abc
    System.out.println("a".matches("[^abc]"));//false 判断a是否在abc之外的
    System.out.println("a".matches("\\d")); //false 是否a是整数
    System.out.println("a".matches("\\w")); //true 是否是字符
    System.out.println("你".matches("\\w")); // false
    System.out.println("aa".matches("\\w"));//false 只能检验单个字符
    
    // 密码 必须是数字 字母 下划线 至少 6位
	System.out.println("ssds3c".matches("\\w{6,}")); // true
    // 验证。必须是数字和字符  必须是4位
    System.out.println("dsd22".matches("[a-zA-Z0-9]{4}")); // false
    System.out.println("A3dy".matches("[a-zA-Z0-9]{4}")); // true
}
```



***



#### 验证号码

```java
//1开头 第二位是2-9的数字
public static void checkPhone(String phone){
    if(phone.matches("1[3-9]\\d{9}")){
        System.out.println("手机号码格式正确！");
    } else {.......}
}
//1111@qq.com  zhy@pic.com.cn
public static void checkEmail(String email){
    if(email.matches("\\w{1,}@\\w{1,}(\\.\\w{2,5}){1,2}")){
        System.out.println("邮箱格式正确！");
    }// .是任意字符 \\.就是点
}
```



***



#### 查找替换

* `public String[] split(String regex)`：按照正则表达式匹配的内容进行分割字符串，反回一个字符串数组
* `public String replaceAll(String regex,String newStr)`：按照正则表达式匹配的内容进行替换

```java
//数组分割
public static void main(String[] args) {
	// 1.split的基础用法
	String names = "风清扬,张无忌,周芷若";
	// 以“，”分割成字符串数组
    String[] nameArrs = names.split(",");

    // 2.split集合正则表达式做分割
    String names1 = "风清扬lv434fda324张无忌87632fad2342423周芷若";
    // 以匹配正则表达式的内容为分割点分割成字符串数组
	String[] nameArrs1 = names1.split("\\w+");
    
	// 使用正则表达式定位出内容，替换成/
	System.out.println(names1.replaceAll("\\w+","/"));//风清扬/张无忌/周芷若

	String names3 = "风清扬,张无忌,周芷若";
	System.out.println(names3.replaceAll(",","-"));//风清扬-张无忌-周芷若
}
```



***



#### 搜索号码

找出所有 189 和 132 开头的手机号

```java
public class RegexDemo {
    public static void main(String[] args) {
        String rs = "189asjk65as1891898777745gkkkk189745612318936457894";
        String regex = "(?=((189|132)\\d{8}))";
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(rs);
        while (matcher.find()) {
            System.out.println(matcher.group(1));
        }
    }
}
```





***











# 异常与日志

## 异常概述

### 异常体系

在计算机程序运行的过程中，总是会出现各种各样的错误。

有一些错误是用户造成的，比如，希望用户输入一个`int`类型的年龄，但是用户的输入是`abc`：

```java
// 假设用户输入了abc：
String s = "abc";
int n = Integer.parseInt(s); // NumberFormatException!
```

程序想要读写某个文件的内容，但是用户已经把它删除了：

```java
// 用户删除了该文件：
String t = readFile("C:\\abc.txt"); // FileNotFoundException!
```

还有一些错误是随机出现，并且永远不可能避免的。比如：

- 网络突然断了，连接不到远程服务器；
- 内存耗尽，程序崩溃了；
- 用户点“打印”，但根本没有打印机；
- ……

所以，一个健壮的程序必须处理各种各样的错误。

所谓错误，就是程序调用某个函数的时候，如果失败了，就表示出错。

调用方如何获知调用失败的信息？有两种方法：

**方法一：约定返回错误码。**

例如，处理一个文件，如果返回`0`，表示成功，返回其他整数，表示约定的错误码：

```java
int code = processFile("C:\\test.txt");
if (code == 0) {
    // ok:
} else {
    // error:
    switch (code) {
    case 1:
        // file not found:
    case 2:
        // no read permission:
    default:
        // unknown error:
    }
}
```

因为使用`int`类型的错误码，想要处理就非常麻烦。这种方式常见于底层C函数。

**方法二：在语言层面上提供一个异常处理机制。**

Java内置了一套异常处理机制，总是使用异常来表示错误。

异常是一种`class`，因此它本身带有类型信息。异常可以在任何地方抛出，但只需要在上层捕获，这样就和方法调用分离了：

```java
try {
    String s = processFile(“C:\\test.txt”);
    // ok:
} catch (FileNotFoundException e) {
    // file not found:
} catch (SecurityException e) {
    // no read permission:
} catch (IOException e) {
    // io error:
} catch (Exception e) {
    // other error:
}
```

因为Java的异常是`class`，它的继承关系如下：

```ascii
                     ┌───────────┐
                     │  Object   │
                     └───────────┘
                           ▲
                           │
                     ┌───────────┐
                     │ Throwable │
                     └───────────┘
                           ▲
                 ┌─────────┴─────────┐
                 │                   │
           ┌───────────┐       ┌───────────┐
           │   Error   │       │ Exception │
           └───────────┘       └───────────┘
                 ▲                   ▲
         ┌───────┘              ┌────┴──────────┐
         │                      │               │
┌─────────────────┐    ┌─────────────────┐┌───────────┐
│OutOfMemoryError │... │RuntimeException ││IOException│...
└─────────────────┘    └─────────────────┘└───────────┘
                                ▲
                    ┌───────────┴─────────────┐
                    │                         │
         ┌─────────────────────┐ ┌─────────────────────────┐
         │NullPointerException │ │IllegalArgumentException │...
         └─────────────────────┘ └─────────────────────────┘
```

从继承关系可知：

`Throwable`是异常体系的根，它继承自`Object`。`Throwable`有两个体系：`Error`和`Exception`

``Error`表示严重的错误，程序对此一般无能为力，例如：

- `OutOfMemoryError`：内存耗尽
- `NoClassDefFoundError`：无法加载某个Class
- `StackOverflowError`：栈溢出

而`Exception`则是运行时的错误，它可以被捕获并处理。

某些异常是应用程序逻辑处理的一部分，应该捕获并处理。例如：

- `NumberFormatException`：数值类型的格式错误
- `FileNotFoundException`：未找到文件
- `SocketException`：读取网络失败

还有一些异常是程序逻辑编写不对造成的，应该修复程序本身。例如：

- `NullPointerException`：对某个`null`的对象调用方法或字段
- `IndexOutOfBoundsException`：数组索引越界

`Exception`又分为两大类：

1. `RuntimeException`以及它的子类；
2. 非`RuntimeException`（包括`IOException`、`ReflectiveOperationException`等等）

Java规定：

- 必须捕获的异常，包括`Exception`及其子类，但不包括`RuntimeException`及其子类，这种类型的异常称为Checked Exception。
- 不需要捕获的异常，包括`Error`及其子类，`RuntimeException`及其子类。

注意：编译器对RuntimeException及其子类不做强制捕获要求，不是指应用程序本身不应该捕获并处理RuntimeException。是否需要捕获，具体问题具体分析。

### 常见异常

`java.lang.RuntimeException`

- `ClassCastException`
- `ArrayIndexOutOfBoundsException`
- `NullPointerException`
- `ArithmeticException`
- `NumberFormatException`
- `InputMismatchException`

`java.io.IOExeption`

- `FileNotFoundException`
- `EOFException`

`java.lang.ClassNotFoundException`

`java.lang.InterruptedException`

`java.io.FileNotFoundException`

`java.sql.SQLException`  

```java
//NullPointerException空指针异常
public class NullRef {
	int i = 1;
	public static void main(String[] args) {
		NullRef t = new NullRef();
        t = null;
		System.out.println(t.i);
	}
}

//ArrayIndexOutOfBoundsException数组角标越界异常
public class IndexOutExp {
	public static void main(String[] args) {
		String friends[] = { "lisa", "bily", "kessy" };
		for (int i = 0; i < 5; i++) {
			System.out.println(friends[i]); // friends[4]?
		}
		System.out.println("\nthis is the end");
	}
}

//ClassCastException类型转换异常
public class Order {
	public static void main(String[] args) {
		Object obj = new Date();
		Order order;
		order = (Order) obj;
		System.out.println(order);
	}
}

//NumberFormatException数值转换异常
public class NumberTest{
	public void test(){
		String str="abc";
        int num=Integer.parseInt(str);
	}
}

//InputMismatchException
public class InputTest{
	public void test(){
		Scanner scan=new Scanner();
        int num=scanner.nextInt();
        //输入abc
        System.out.println(num);
	}
}

//ArithmeticException算数异常
public class DivideZero {
	int x;
	public static void main(String[] args) {
		int y;
		DivideZero c=new DivideZero();
		y=3/c.x;
		System.out.println("program ends ok!");
	}
}
```



## 异常处理机制

在编写程序时，经常要在可能出现错误的地方加上检测的代码，如进行x/y运算时，要检测分母为0，数据为空，输入的不是数据而是字符等。 过多的if-else分支会导致程序的代码加长、臃肿，可读性差。因此采用异常处理机制。

Java采用的异常处理机制，是将异常处理的程序代码集中在一起，与正常的程序代码分开，使得程序简洁、优雅， 并易于维护。  

Java异常处理的方式：  

- 方式一： try-catch-finally
- 方式二： throws + 异常类型

Java提供的是异常处理的**抓抛模型**：Java程序的执行过程中**如出现异常， 会生成一个异常类对象**，该异常对象将被**提交给Java运行时系统， 这个过程称为抛出(throw)异常**，一旦抛出，其后的代码就不再执行



### 异常对象的生成

- 由虚拟机自动生成：程序运行过程中，虚拟机检测到程序发生了问题，如果在当前代码中没有找到相应的处理程序，就会在**后台自动创建一个对应异常类的实例对象**并抛出——自动抛出
- 由开发人员手动创建： `Exception exception = new ClassCastException();`创建好的异常对象不抛出对程序没有任何影响，和创建一个普通对象一样  

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220126110945667-166529427007735.png" alt="image-20220126110945667" style="zoom:50%;" />

为保证程序正常执行，代码必须对可能出现的异常进行处理  

- 如果一个方法内抛出异常， 该异常对象会被抛给**调用者方法**中处理。 如果异常没有在调用者方法中处理， 它继续被抛给这个调用方法的上层方法。 这个过程将一直继续下去， 直到异常被处理。这一过程称为捕获(catch)异常。

- 如果一个异常回到main()方法， 并且main()也不处理， 则程序运行终止

程序员通常只能处理Exception， 而对Error无能为力  



### try-catch-finally  

```java
try{
	...... //可能产生异常的代码
}
catch( ExceptionName1 e ){
	...... //当产生ExceptionName1型异常时的处置措施
}
catch( ExceptionName2 e ){
	...... //当产生ExceptionName2型异常时的处置措施
} [
finally{
	...... //无论是否发生异常， 都无条件执行的语句
} ]
```

try：捕获异常的第一步是用try{…}语句块选定捕获异常的范围， 将可能出现异常的代码放在try语句块中。在执行过程中，一旦出现异常，就会生成一个对应异常类的对象，根据此对象的类型，去catch中进行匹配。在try中声明的变量，在出了try结构后不能再被调用

catch (Exceptiontype e)：在catch语句块中是对异常对象进行处理的代码。 每个try语句块可以伴随一个或多个catch语句， 用于处理可能产生的不同类型的异常对象。一旦try中的异常对象匹配到某一个catch时，则进入catch中进行异常处理，一旦处理完成，跳出当前try-catch结构(在没有finally的情况下)，继续执行后面的代码

catch中的异常类型

- 如果没有子父类关系，则声明顺序无所谓；
- 如果存在子父类关系，则子类必须声明在上面，否则报错——**如果明确知道产生的是何种异常， 可以用该异常类作为catch的参数；也可以用其父类作为catch的参数。**

比 如 ： 可以用 ArithmeticException类作为参数的地方 ， 就可以用RuntimeException类作为参数， 或者用所有异常的父类Exception类作为参数。但不能是与ArithmeticException类无关的异常， 如NullPointerException（ catch中的语句将不会执行） 。  

捕获异常的有关信息：与其它对象一样，可以访问一个异常对象的成员变量或调用它的方法。

- `getMessage()` 获取异常信息，返回字符串
- `printStackTrace()` 获取异常类名和异常信息，以及异常出现在程序中的位置。返回值void。  

![image-20220126115234250](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220126115234250-166529427007733.png)

```java
public class TryTest{
	public void test(){
		String str="abc";
        try{
			int num=Integer.parseInt(str);
        }catch(NumberFormatException e){
            System.out.println("出现数值转换异常");
			System.out.println(e.getMessage());
            e.printStackTrace();
        }catch(NullPointerException e){
            System.out.println("出现空指针异常");
        }
	}
}
```

finally的使用

- 捕获异常的最后一步是通过finally语句为异常处理提供一个统一的出口，使得在控制流转到程序的其它部分以前，能够对程序的状态作统一的管理。
- 不论在try代码块中是否发生了异常事件， catch语句是否执行， **catch语句是否有异常**， catch语句中是否有return，finally块中的语句都会被执行。
- finally语句和catch语句是任选的  

```java
public class FinallyTest{
	public void test(){
		String str="abc";
        public int method(){
            try{
                int num=Integer.parseInt(str);
                return 1;
            }catch(NumberFormatException e){
                System.out.println("出现数值转换异常");
				return 2;
            }catch(NullPointerException e){
                System.out.println("出现空指针异常");
            }finally{
                return 3;
            }
	}
}
```

对于上述代码，无论try和catch中是否有异常，是否return，最终都会return 3

像数据库连接、输入输出流、网络编程Socket等资源，JVM是不能自动回收的，需要自行进行资源的回收，此时的资源释放就需要声明在finally中

不捕获异常时的情况  

- 使用try-catch-finally处理编译时异常，使得程序在编译时不再报错，但在运行时仍可能报错。相当于使用try-catch-finally将一个编译时可能出现的异常延迟到运行时再出现
- 前面使用的异常都是RuntimeException类或是它的子类，这些类的异常的特点是：即使没有使用try和catch捕获， Java自己也能捕获，并且编译通过(但运行时会发生异常使得程序运行终止)。
- 如果抛出的异常是IOException等类型的非运行时异常，则必须捕获，否则编译错误。也就是说，我们必须处理编译时异常，将异常进行捕捉，转化为运行时异常  

### throws +异常类型

声明抛出异常是Java中处理异常的第二种方式

如果一个**方法**(中的语句执行时)可能生成某种异常， 但是并不能确定如何处理这种异常， 则**此方法应显示地声明抛出异常， 表明该方法将不对这些异常进行处理，而由该方法的调用者负责处理**。

在方法声明中用throws语句可以声明抛出异常的列表， throws后面的异常类型可以是**方法中产生的异常类型， 也可以是它的父类**。

声明抛出异常举例：

```java
import java.io.*;
public class ThrowsTest {
	public static void main(String[] args) {
		ThrowsTest t = new ThrowsTest();
		//此处调用readFile,并对它进行异常处理
        //在非main方法中可以选择异常处理或者继续往上抛，直到main方法
        try {
			t.readFile();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	public void readFile() throws IOException {
		FileInputStream in = new FileInputStream("atguigushk.txt");
		int b;
		b = in.read();
		while (b != -1) {
			System.out.print((char) b);
			b = in.read();
		}
		in.close();
	}
}
```

由此例可以看出，throws+异常类型 只是将异常抛给了方法的调用者，并没有真正处理异常，真正处理异常的是try-catch-finally

重写方法声明抛出异常的原则

重写方法不能抛出比被重写方法范围更大的异常类型。 在多态的情况下，对methodA()方法的调用-异常的捕获 按父类声明的异常处理  

```java
public class A {
	public void methodA() throws IOException {
	……
	} 
}

public class B1 extends A {
	public void methodA() throws FileNotFoundException {
		……
	} 
}

public class B2 extends A {
	public void methodA() throws Exception { //报错
	……
	} 
}
```

两种异常处理方式的选择

- 如果父类中被重写的方法没有throws方式处理异常，则子类重写的方法也不能使用throws，意味着如果子类重写的方法如果有异常，则必须使用try-catch-finally方式处理
- 执行的方法a中，先后调用了另外的几个方法，而这几个方法是递进关系执行的，建议这几个方法使用throws的方式处理，而a使用try-catch-finally处理

### 手动抛出异常  

Java异常类对象除在程序执行过程中出现异常时由系统自动生成并抛出，也可根据需要使用人工创建并抛出。

首先要生成异常类对象， 然后通过throw语句实现抛出操作(提交给Java运行环境)。

```java
IOException e = new IOException();
throw e;
```

可以抛出的异常必须是**Throwable或其子类的实例**。 下面的语句在编译时将会产生语法错误：

```java
throw new String("want to throw");  
```

### 用户自定义异常类  

一般地，用户自定义异常类都是RuntimeException的子类。

- 自定义异常类通常需要编写几个重载的构造器。
- 自定义异常需要提供serialVersionUID
- 自定义的异常通过throw抛出。
- 自定义异常最重要的是异常类的名字，当异常出现时，可以根据名字判断异常类型。  

用户自定义异常类MyException，用于描述数据取值范围错误信息。用户自己的异常类必须继承现有的异常类  

```java
class MyException extends Exception {
	static final long serialVersionUID = 13465653435L;
	private int idnumber;
	public MyException(String message, int id) {
		super(message);
		this.idnumber = id;
	}
	public int getId() {
		return idnumber;
	}
}

public class MyExpTest {
	public void regist(int num) throws MyException {
		if (num < 0)
			throw new MyException("人数为负值，不合理", 3);
		else
			System.out.println("登记人数" + num);
	}
    public void manager() {
        try {
            regist(100);
        } catch (MyException e) {
            System.out.print("登记失败，出错种类" + e.getId());
        }
        System.out.print("本次登记操作结束");
    }
	public static void main(String args[]) {
		MyExpTest t = new MyExpTest();
		t.manager();
	}
}
```

## 日志

在编写程序的过程中，发现程序运行结果与预期不符，需要用`System.out.println()`打印出执行过程中的某些变量，观察每一步的结果与代码逻辑是否符合，然后有针对性地修改代码。

日志就是Logging，它的目的是为了取代`System.out.println()`。

输出日志，而不是用`System.out.println()`，有以下几个好处：

1. 可以设置输出样式，避免自己每次都写`"ERROR: " + var`；
2. 可以设置输出级别，禁止某些级别输出。例如，只输出错误日志；
3. 可以被重定向到文件，这样可以在程序运行结束后查看日志；
4. 可以按包名控制日志级别，只输出某些包打的日志；
5. ……

### JDK Logging

Java标准库内置了日志包`java.util.logging`

```java
// logging
import java.util.logging.Level;
import java.util.logging.Logger;

public class Hello {
    public static void main(String[] args) {
        Logger logger = Logger.getGlobal();
        logger.info("start process...");
        logger.warning("memory is running out...");
        logger.fine("ignored.");
        logger.severe("process will be terminated...");
    }
}
```

运行上述代码，得到类似如下的输出：

```java
Mar 02, 2019 6:32:13 PM Hello main
INFO: start process...
Mar 02, 2019 6:32:13 PM Hello main
WARNING: memory is running out...
Mar 02, 2019 6:32:13 PM Hello main
SEVERE: process will be terminated...
```

对比可见，使用日志最大的好处是，它自动打印了时间、调用类、调用方法等很多有用的信息。

4条日志，只打印了3条，`logger.fine()`没有打印。这是因为，日志的输出可以设定级别。

JDK的Logging定义了7个日志级别，从严重到普通：

- SEVERE
- WARNING
- INFO
- CONFIG
- FINE
- FINER
- FINEST

因为默认级别是INFO，因此，INFO级别以下的日志，不会被打印出来。使用日志级别的好处在于，调整级别，就可以屏蔽掉很多调试相关的日志输出。

使用Java标准库内置的Logging有以下局限：

- Logging系统在JVM启动时读取配置文件并完成初始化，一旦开始运行`main()`方法，就无法修改配置；

- 配置不太方便，需要在JVM启动时传递参数`-Djava.util.logging.config.file=<config-file-name>`。


因此，Java标准库内置的Logging使用并不是非常广泛

### Commons Logging

和Java标准库提供的日志不同，Commons Logging是一个第三方日志库，它是由Apache创建的日志模块。

Commons Logging的特色是，**它可以挂接不同的日志系统，并通过配置文件指定挂接的日志系统**。默认情况下，Commons Loggin自动搜索并使用Log4j（Log4j是另一个流行的日志系统），如果没有找到Log4j，再使用JDK Logging。

使用Commons Logging只需要和两个类打交道，并且只有两步：

- 第一步，通过`LogFactory`获取`Log`类的实例；
- 第二步，使用`Log`实例的方法打日志

示例代码如下：

```java
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;

public class Main {
    public static void main(String[] args) {
        Log log = LogFactory.getLog(Main.class);
        log.info("start...");
        log.warn("end.");
    }
}
```

因为Commons Logging是一个第三方提供的库，所以，必须先把它下载下来。**该过程在IDEA中可以通过项目管理快捷完成**

运行结果如下：

```java
Mar 02, 2019 7:15:31 PM Main main
INFO: start...
Mar 02, 2019 7:15:31 PM Main main
WARNING: end.
```

Commons Logging定义了6个日志级别：

- FATAL
- ERROR
- WARNING
- INFO
- DEBUG
- TRACE

默认级别是`INFO`。

使用Commons Logging时，如果在静态方法中引用`Log`，通常直接定义一个静态类型变量：

```java
// 在静态方法中引用Log:
public class Main {
    static final Log log = LogFactory.getLog(Main.class);

    static void foo() {
        log.info("foo");
    }
}
```

在实例方法中引用`Log`，通常定义一个实例变量：

```java
// 在实例方法中引用Log:
public class Person {
    protected final Log log = LogFactory.getLog(getClass());

    void foo() {
        log.info("foo");
    }
}
```

注意到实例变量log的获取方式是`LogFactory.getLog(getClass())`，虽然也可以用`LogFactory.getLog(Person.class)`，但是前一种方式有个非常大的好处：**子类可以直接使用该log实例**

```java
// 在子类中使用父类实例化的log:
public class Student extends Person {
    void bar() {
        log.info("bar");
    }
}
```

由于Java类的动态特性，子类获取的`log`字段实际上相当于`LogFactory.getLog(Student.class)`，但却是从父类继承而来

此外，Commons Logging的日志方法，例如`info()`，除了标准的`info(String)`外，还提供了一个非常有用的重载方法：`info(String, Throwable)`，这使得记录异常更加简单：

```java
try {
    ...
} catch (Exception e) {
    log.error("got exception!", e);
}
```

### Log4j

Commons Logging可以作为“日志接口”来使用。而真正的“日志实现”可以使用Log4j。

Log4j是一种非常流行的日志框架，最新版本是2.x。

Log4j是一个组件化设计的日志系统，它的架构大致如下：

```ascii
log.info("User signed in.");
 │
 │   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 ├──>│ Appender │───>│  Filter  │───>│  Layout  │───>│ Console  │
 │   └──────────┘    └──────────┘    └──────────┘    └──────────┘
 │
 │   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 ├──>│ Appender │───>│  Filter  │───>│  Layout  │───>│   File   │
 │   └──────────┘    └──────────┘    └──────────┘    └──────────┘
 │
 │   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 └──>│ Appender │───>│  Filter  │───>│  Layout  │───>│  Socket  │
     └──────────┘    └──────────┘    └──────────┘    └──────────┘
```

使用Log4j输出一条日志时

- 自动通过不同的Appender把同一条日志输出到不同的目的地。例如：

  - console：输出到屏幕；

  - file：输出到文件；

  - socket：通过网络输出到远程计算机；

  - jdbc：输出到数据库


- 通过Filter来过滤哪些log需要被输出，哪些log不需要被输出。例如，仅输出`ERROR`级别的日志。

- 通过Layout来格式化日志信息，例如，自动添加日期、时间、方法名称等信息。


上述结构虽然复杂，但在实际使用的时候，并不需要关心Log4j的API，而是通过配置文件来配置它。

以XML配置为例，使用Log4j的时候，把一个`log4j2.xml`的文件放到`classpath`下就可以让Log4j读取配置文件并按照配置来输出日志

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
	<Properties>
        <!-- 定义日志格式 -->
		<Property name="log.pattern">%d{MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36}%n%msg%n%n</Property>
        <!-- 定义文件名变量 -->
		<Property name="file.err.filename">log/err.log</Property>
		<Property name="file.err.pattern">log/err.%i.log.gz</Property>
	</Properties>
    <!-- 定义Appender，即目的地 -->
	<Appenders>
        <!-- 定义输出到屏幕 -->
		<Console name="console" target="SYSTEM_OUT">
            <!-- 日志格式引用上面定义的log.pattern -->
			<PatternLayout pattern="${log.pattern}" />
		</Console>
        <!-- 定义输出到文件,文件名引用上面定义的file.err.filename -->
		<RollingFile name="err" bufferedIO="true" fileName="${file.err.filename}" filePattern="${file.err.pattern}">
			<PatternLayout pattern="${log.pattern}" />
			<Policies>
                <!-- 根据文件大小自动切割日志 -->
				<SizeBasedTriggeringPolicy size="1 MB" />
			</Policies>
            <!-- 保留最近10份 -->
			<DefaultRolloverStrategy max="10" />
		</RollingFile>
	</Appenders>
	<Loggers>
		<Root level="info">
            <!-- 对info级别的日志，输出到console -->
			<AppenderRef ref="console" level="info" />
            <!-- 对error级别的日志，输出到err，即上面定义的RollingFile -->
			<AppenderRef ref="err" level="error" />
		</Root>
	</Loggers>
</Configuration>
```

虽然配置Log4j比较繁琐，但一旦配置完成，使用起来就非常方便。对上面的配置文件，凡是`INFO`级别的日志，会自动输出到屏幕，而`ERROR`级别的日志，不但会输出到屏幕，还会同时输出到文件。并且，一旦日志文件达到指定大小（1MB），Log4j就会自动切割新的日志文件，并最多保留10份。

因为Log4j也是一个第三方库，需要下载Log4j，解压后，把以下3个jar包放到`classpath`中：

- log4j-api-2.x.jar
- log4j-core-2.x.jar
- log4j-jcl-2.x.jar

因为Commons Logging会自动发现并使用Log4j，所以，把上一节下载的`commons-logging-1.2.jar`也放到`classpath`中。

要打印日志，只需要按Commons Logging的写法写，不需要改动任何代码，就可以得到Log4j的日志输出，类似：

```
03-03 12:09:45.880 [main] INFO  com.itranswarp.learnjava.Main
Start process...
```

在开发阶段，始终使用Commons Logging接口来写入日志，并且开发阶段无需引入Log4j。如果需要把日志写入文件， 只需要把正确的配置文件和Log4j相关的jar包放入`classpath`，就可以自动把日志切换成使用Log4j写入，无需修改任何代码。



### 使用SLF4J和Logback

SLF4J类似于Commons Logging，也是一个日志接口，而Logback类似于Log4j，是一个日志的实现。

因为对Commons Logging的接口不满意，有人就搞了SLF4J。因为对Log4j的性能不满意，有人就搞了Logback。

在Commons Logging中，要打印日志，有时候得这么写：

```java
int score = 99;
p.setScore(score);
log.info("Set score " + score + " for Person " + p.getName() + " ok.");
```

拼字符串是一个非常麻烦的事情，所以SLF4J的日志接口改进成这样了：

```java
int score = 99;
p.setScore(score);
logger.info("Set score {} for Person {} ok.", score, p.getName());
```

SLF4J的日志接口传入的是一个带占位符的字符串，用后面的变量自动替换占位符，所以看起来更加自然。

如何使用SLF4J？它的接口实际上和Commons Logging几乎一模一样：

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

class Main {
    final Logger logger = LoggerFactory.getLogger(getClass());
}
```

对比一下Commons Logging和SLF4J的接口：

| Commons Logging                       | SLF4J                   |
| :------------------------------------ | :---------------------- |
| org.apache.commons.logging.Log        | org.slf4j.Logger        |
| org.apache.commons.logging.LogFactory | org.slf4j.LoggerFactory |

不同之处就是Log变成了Logger，LogFactory变成了LoggerFactory。

使用SLF4J和Logback和前面讲到的使用Commons Logging加Log4j是类似的，先分别下载[SLF4J](https://www.slf4j.org/download.html)和[Logback](https://logback.qos.ch/download.html)，然后把以下jar包放到classpath下：

- slf4j-api-1.7.x.jar
- logback-classic-1.2.x.jar
- logback-core-1.2.x.jar

然后使用SLF4J的Logger和LoggerFactory即可。和Log4j类似，仍然需要一个Logback的配置文件，把`logback.xml`放到classpath下，配置如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>

	<appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
		<encoder>
			<pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
		</encoder>
	</appender>

	<appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
		<encoder>
			<pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
			<charset>utf-8</charset>
		</encoder>
		<file>log/output.log</file>
		<rollingPolicy class="ch.qos.logback.core.rolling.FixedWindowRollingPolicy">
			<fileNamePattern>log/output.log.%i</fileNamePattern>
		</rollingPolicy>
		<triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">
			<MaxFileSize>1MB</MaxFileSize>
		</triggeringPolicy>
	</appender>

	<root level="INFO">
		<appender-ref ref="CONSOLE" />
		<appender-ref ref="FILE" />
	</root>
</configuration>
```

运行即可获得类似如下的输出：

```
13:15:25.328 [main] INFO  com.itranswarp.learnjava.Main - Start process...
```

从目前的趋势来看，越来越多的开源项目从Commons Logging加Log4j转向了SLF4J加Logback。



# 多线程

## 程序、进程、 线程  

程序(program)是为完成特定任务、用某种语言编写的一组指令的集合。即指一段静态的代码，静态对象。

进程(process)是程序的一次执行过程，或是正在运行的一个程序。是一个动态的过程：有它自身的产生、存在和消亡的过程。 ——生命周期

- 如：运行中的QQ，运行中的MP3播放器
- 程序是静态的，进程是动态的
- 进程作为**资源分配的单位**， 系统在运行时会为每个进程分配不同的内存区域

线程(thread)，进程可进一步细化为线程，是一个**程序内部的一条执行路径**。

- 若一个进程同一时间并行执行多个线程，就是支持多线程的
- 线程作为**调度和执行的单位**，每个线程拥有独立的运行栈和程序计数器(pc)，线程切换的开销小
- 一个进程中的多个线程共享相同的内存单元/内存地址空间—>它们从同一堆中分配对象，可以访问相同的变量和对象。这就使得线程间通信更简便、高效。但多个线程操作共享的系统资源可能就会带来安全的隐患。  

单核CPU和多核CPU的理解

- 单核CPU，其实是一种假的多线程，因为在一个时间单元内，也只能执行一个线程的任务。例如：虽然有多车道，但是收费站只有一个工作人员在收费，只有收了费才能通过，那么CPU就好比收费人员。如果有某个人不想交钱， 那么收费人员可以把他“挂起”（晾着他，等他想通了，准备好了钱，再去收费） 。 但是因为CPU时间单元特别短，因此感觉不出来。
- 如果是多核的话，才能更好的发挥多线程的效率。（现在的服务器都是多核的）
- 一个Java应用程序java.exe，其实至少有三个线程： main()主线程， gc()垃圾回收线程，异常处理线程。当然如果发生异常，会影响主线程。

并行与并发

- 并行： 多个CPU同时执行多个任务。比如：多个人同时做不同的事。
- 并发： 一个CPU(采用时间片)同时执行多个任务。比如：秒杀、多个人做同一件事。  

多线程的优点  

以单核CPU为例， 只使用单个线程先后完成多个任务（调用多个方法），肯定比用多个线程来完成用的时间更短，为何仍需多线程呢？

多线程程序的优点：

- 提高应用程序的响应。对图形化界面更有意义，可增强用户体验。
- 提高计算机系统CPU的利用率
- 改善程序结构。将既长又复杂的进程分为多个线程，独立运行，利于理解和
  修改  

何时需要多线程  

- 程序需要同时执行两个或多个任务。
- 程序需要实现一些需要等待的任务时，如用户输入、文件读写操作、网络操作、搜索等。
- 需要一些后台运行的程序时  

## 线程的创建和使用  

### Thread类 

Java语言的JVM允许程序运行多个线程，它通过java.lang.Thread类来体现。

Thread类的特性

- 每个线程都是通过某个特定Thread对象的run()方法来完成操作的，经常把**run()方法的主体称为线程体**
- 通过该Thread对象的start()方法来启动这个线程，而非直接调用run()  

Thread类构造器

- Thread()： 创建新的Thread对象
- Thread(String threadname)： 创建线程并指定线程实例名
- Thread(Runnable target)： 指定创建线程的目标对象，它实现了Runnable接口中的run方法
- Thread(Runnable target, String name)： 创建新的Thread对象  

Thread类的有关方法  

- void `start()`: 启动线程，并执行对象的run()方法
- `run()`: 线程在被调度时执行的操作
- String `getName()`: 返回线程的名称
- void `setName(String name)`:设置该线程名称
- static Thread `currentThread()`: 返回当前线程。在Thread子类中就是this，通常用于主线程和Runnable实现类  
- static void `yield()`： 线程让步。暂停当前正在执行的线程，把执行机会让给优先级相同或更高的线程；若队列中没有同优先级的线程，忽略此方法
- `join()` ： 当某个程序执行流中调用其他线程的 join() 方法时， 调用线程将被阻塞，直到 join() 方法加入的 join 线程执行完为止，低优先级的线程也可以获得执行
- static void `sleep(long millis)`： (指定时间:毫秒)，令**当前活动线程在指定时间段内放弃对CPU控制**,使其他线程有机会被执行,时间到后重排队。抛出InterruptedException异常
- `stop()`: 强制线程生命期结束，不推荐使用
- boolean `isAlive()`： 返回boolean，判断线程是否还活着  

### 创建线程的两种方式  

JDK1.5之前创建新执行线程有两种方法：

- 继承Thread类的方式
- 实现Runnable接口的方式  

#### 方式一： 继承Thread类

- 定义子类继承Thread类。
- 子类中重写Thread类中的run方法。
- 创建Thread子类对象，即创建了线程对象。
- 调用线程对象start方法：启动线程，调用run方法。  

```java
//创建两个线程，一个遍历1-100的偶数，一个遍历1-100的奇数

//1.创建一个继承于Thread类的子类
class MyThread1 extends Thread{
    //2.重写Thread类的run()
    public void run(){
        for(int i=0;i<=100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}

class MyThread2 extends Thread{
    //2.重写Thread类的run()
    public void run(){
        for(int i=0;i<=100;i++){
            if(i%2!=0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}

public class ThreadTest {
    public static void main(String[] args) {
        MyThread1 m1=new MyThread1();
        MyThread2 m2=new MyThread2();

        m1.start();
        m2.start();
    }
}

```

注意点：

- 想要启动多线程，必须调用start方法。如果自己手动调用run()方法，那么就只是普通方法，没有启动多线程模式。
- 一个线程对象只能调用一次start()方法启动，如果重复调用了，则将抛出以上的异常“IllegalThreadStateException” 。  
- run()方法由JVM调用，什么时候调用，执行的过程控制都有操作系统的CPU调度决定。

#### 方式二：实现Runnable接口

- 定义子类，实现Runnable接口。
- 子类中重写Runnable接口中的run方法。
- 通过Thread类含参构造器创建线程对象。
- 将Runnable接口的子类对象作为实际参数传递给Thread类的构造器中。
- 调用Thread类的start方法：开启线程， 调用Runnable子类接口的run方法。  

```java
//1.创建实现Runnable接口的类
class MyThread implements Runnable{
    //2.实现类去实现Runnable中的抽象方法
    @Override
    public void run() {
        for(int i=0;i<=100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}
public class ThreadTest1 {
    public static void main(String[] args) {
        //3.创建实现类的对象
        MyThread m=new MyThread();
        //4.将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
        Thread t=new Thread(m);
        //5.通过Thread类的对象调用start()
        t.start();
        
        //再启动一个线程
        Thread t1=new Thread(m);
        t1.start();
    }
}
```

继承方式和实现方式的联系与区别  

```java
public class Thread extends Object implements Runnable  
```

区别

- 继承Thread：线程代码存放Thread子类run方法中。
- 实现Runnable：线程代码存在接口的子类的run方法。

实现方式的好处

- 避免了单继承的局限性
- 多个线程可以共享同一个接口实现类的对象，非常适合多个相同线
  程来处理同一份资源  

```java
//三个卖票窗口合卖100张票
class Window1 implements Runnable{
    private int ticket=100;

    @Override
    public void run() {
        while(true){
            if(ticket>0){
                System.out.println(Thread.currentThread().getName()+"：卖票，票号为："+ticket);
                ticket--;
            }else{
                break;
            }
        }
    }
}
public class WindowTest {
    public static void main(String[] args) {
        Window1 w=new Window1();
        Thread t1=new Thread(w);
        Thread t2=new Thread(w);
        Thread t3=new Thread(w);

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

### 线程的调度  

调度策略：时间片  

![image-20220126201447309](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220126201447309-166529427007736.png)

抢占式： 高优先级的线程抢占CPU  

Java的调度方法

- 同优先级线程组成先进先出队列（先到先服务），使用时间片策略
- 对高优先级，使用优先调度的抢占式策略  

线程的优先级  

线程的优先级等级

- MAX_PRIORITY： 10
- MIN _PRIORITY： 1
- NORM_PRIORITY： 5(默认优先级)

涉及的方法

- getPriority() ： 返回线程优先值
- setPriority(int newPriority) ： 改变线程的优先级

```java
public class ThreadTest {
    public static void main(String[] args) {
        MyThread1 m1=new MyThread1();
        MyThread2 m2=new MyThread2();

        m1.setName("线程1");
        m1.setPriority(Thread.MAX_PRIORITY);
        m1.start();

        m2.setName("线程2");
        m2.setPriority(Thread.MIN_PRIORITY);
        m2.start();

        Thread.currentThread().setName("主线程");
        for(int i=0;i<=100;i++){
            if(i%5==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}
```

说明

- 线程创建时继承父线程的优先级
- 低优先级只是获得调度的概率低，并非一定是在高优先级线程之后才被调用  

### 线程的分类  

Java中的线程分为两类：一种是守护线程，一种是用户线程。

- 它们在几乎每个方面都是相同的，唯一的区别是判断JVM何时离开。
- 守护线程是用来服务用户线程的，通过在start()方法前调用`thread.setDaemon(true)`可以把一个用户线程变成一个守护线程。
- Java垃圾回收就是一个典型的守护线程。
- 若JVM中都是守护线程，当前JVM将退出。
- 形象理解： 兔死狗烹，鸟尽弓藏  

## 线程的生命周期  

JDK中用Thread.State类定义了线程的几种状态

要想实现多线程， 必须在主线程中创建新的线程对象。 Java语言使用Thread类及其子类的对象来表示线程， 在它的一个完整的生命周期中通常要经历如下的五种状态：

- 新建： 当一个Thread类或其子类的对象被声明并创建时，新生的线程对象处于新建状态
- 就绪： 处于新建状态的线程被start()后，将进入线程队列等待CPU时间片，此时它已具备了运行的条件，只是没分配到CPU资源
- 运行： 当就绪的线程被调度并获得CPU资源时,便进入运行状态， run()方法定义了线程的操作和功能
- 阻塞： 在某种特殊情况下，被人为挂起或执行输入输出操作时，让出 CPU 并临时中止自己的执行，进入阻塞状态
- 死亡： 线程完成了它的全部工作或线程被提前强制性地中止或出现异常导致结束  

![image-20220126212159163](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220126212159163-166529427007737.png)

## 线程的同步

问题的提出

- 多个线程执行的不确定性引起执行结果的不稳定
- 多个线程对数据的共享，会造成操作的不完整性，会破坏数据  

以三个窗口同时卖票为例

![image-20220127082259853](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220127082259853-166529427007842.png)

![image-20220127082316756](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220127082316756-166529427007739.png)

多线程出现了安全问题的原因：

当多条语句在操作同一个线程共享数据时，**一个线程对多条语句只执行了一部分，还没有执行完，另一个线程参与进来执行**。导致共享数据的错误。

解决办法：对多条操作共享数据的语句，**让一个线程先把这些语句全部执行完**，在执行过程中，其他线程不可以参与执行。  

### Synchronized的使用方法  

Java对于多线程的安全问题提供了专业的解决方式： 同步机制  

#### 方式1：同步代码块

```java
synchronized (同步监视器){
	// 需要被同步的代码；
}
```

说明：

- 共享数据：多个线程共同操作的变量
- 需要被同步的代码：**操作共享数据的代码**
- 同步监视器：俗称“锁”。任何一个类的对象都可以充当锁。要求多个线程必须用同一把锁

实现接口方式卖票的同步代码块举例

```java
class Window2 implements Runnable{
    private int ticket=100;
    Object obj=new Object();//创建锁

    @Override
    public void run() {
        while(true){
            //synchronized(obj){
            synchronized(this){//此时的this：唯一的Windows2的对象
                if(ticket>0){
                    System.out.println(Thread.currentThread().getName()+"：卖票，票号为："+ticket);
                    ticket--;
                }else{
                    break;
                }
            }
        }
        //}
    }
}
```

如果将`while (true)`也同步，因为循环入口也在同步范围内，将会只有线程1在执行

但是即使入口没有被同步，也可能出现的全部是线程1，原因是当线程1执行完这些语句后，又得到了执行权

#### 同步的范围  

如何找问题， 即代码是否存在线程安全？ （非常重要）

- 明确哪些代码是多线程运行的代码
- 明确多个线程是否有共享数据
- 明确多线程运行代码中是否有多条语句操作共享数据  

如何解决呢？ （非常重要）

**对多条操作共享数据的语句， 只能让一个线程先将这些语句都执行完，其它语句才能使用**， 在执行过程中， 其他线程不可以参与执行。即所有操作共享数据的这些语句都要放在同步范围中 

切记：

- 范围太小：没锁住所有有安全问题的代码
- 范围太大：没发挥多线程的功能   

#### 方式2：同步方法

```java
public synchronized void show (String name){
	…
}
```

实现接口方式卖票的同步方法举例

```java
class Window1 implements Runnable{
    private int ticket=100;
    Object obj=new Object();

    @Override
    public void run() {
        while(true) {
            show();
        }
    }
    public synchronized void show() {//同步监视器默认为this
        if(ticket>0){
            System.out.println(Thread.currentThread().getName()+"：卖票，票号为："+ticket);
            ticket--;
        }
    }
}
```

#### 同步机制中的锁 

对于并发工作， 需要某种方式来防止两个任务访问相同的资源（其实就是共享资源竞争） 。 防止这种冲突的方法就是当资源被一个任务使用时， 在其上加锁。 **第一个访问某项资源的任务必须锁定这项资源， 使其他任务在其被解锁之前， 就无法访问它了， 而在其被解锁之时， 另一个任务就可以锁定并使用它了**。

synchronized的锁是什么？

- 任意对象都可以作为同步锁。 所有对象都自动含有单一的锁（监视器） 。
- 同步方法的锁：静态方法（`类名.class`）(**继承类方式实现多线程时使用**，保证所有对象的锁是同一个，即`类名.class`) 、 非静态方法（`this`）
- 同步代码块：自己指定， 很多时候也是指定为`this`或`类名.class`

注意：

- 必须确保使用同一个资源的多个线程共用一把锁， 这个非常重要， 否则就无法保证共享资源的安全
- 一个线程类中的所有静态方法共用同一把锁（`类名.class`） ， 所有非静态方法共用同一把锁（`this`） ， 同步代码块指定需谨慎  

#### 锁的释放

释放锁的操作：  

- 当前线程的同步方法、同步代码块执行结束。
- 当前线程在同步代码块、同步方法中遇到break、 return终止了该代码块、该方法的继续执行。
- 当前线程在同步代码块、同步方法中出现了未处理的Error或Exception， 导致异常结束。
- 当前线程在同步代码块、同步方法中执行了线程对象的wait()方法，当前线程暂停，并释放锁  

不会释放锁的操作

- 线程执行同步代码块或同步方法时，程序调用Thread.sleep()、Thread.yield()方法暂停当前线程的执行
- 线程执行同步代码块时，其他线程调用了该线程的suspend()方法将该线程挂起，该线程不会释放锁（同步监视器）。应尽量避免使用suspend()和resume()来控制线程  

#### 单例设计模式之懒汉式(线程安全)  

```java
class Singleton {
	private static Singleton instance = null;
	private Singleton(){}
	public static Singleton getInstance(){
        if(instance==null){
            synchronized(Singleton.class){
                if(instance == null){
                    instance=new Singleton();
                }
            } 
        }
		return instance;
	} 
}
public class SingletonTest{
	public static void main(String[] args){
		Singleton s1=Singleton.getInstance();
		Singleton s2=Singleton.getInstance();
		System.out.println(s1==s2);
	} 
}
```

#### 线程的死锁问题 

不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁，出现死锁后，不会出现异常，不会出现提示，只是所有的线程都处于阻塞状态，无法继续

解决方法

- 专门的算法、原则
- 尽量减少同步资源的定义
- 尽量避免嵌套同步  

死锁举例

```java
public class DeadLockTest {
	public static void main(String[] args) {
		final StringBuffer s1 = new StringBuffer();
		final StringBuffer s2 = new StringBuffer();
		new Thread() {//匿名子类
			public void run() {
				synchronized (s1) {
					s2.append("A");
					synchronized (s2) {
						s2.append("B");
						System.out.print(s1);
						System.out.print(s2);
                    }
                }
            }
        }.start();
        new Thread() {
            public void run() {
            	synchronized (s2) {
            		s2.append("C");
            		synchronized (s1) {
            			s1.append("D");
            			System.out.print(s2);
            			System.out.print(s1);
					}
				}
			}
		}.start();
	}
}     
```

### Lock(锁)  

从JDK 5.0开始， Java提供了更强大的线程同步机制——通过显式定义**同步锁对象**来实现同步，即同步锁使用Lock对象充当。`java.util.concurrent.locks.Lock`接口是控制多个线程对共享资源进行访问的工具。 锁提供了对共享资源的独占访问，**每次只能有一个线程对Lock对象加锁，线程开始访问共享资源之前应先获得Lock对象**。

`ReentrantLock`类实现了 Lock接口 ，它拥有与 synchronized 相同的并发性和内存语义， 在实现线程安全的控制中，比较常用的是ReentrantLock， 可以显式加锁、释放锁。  

```java
class A{
	private final ReentrantLock lock = new ReenTrantLock(none/true/false);
	public void m(){
		lock.lock();
		try{
			//保证线程安全的代码;
		}
		finally{
			lock.unlock();
		}
	}
}
```

设置为true，为公平锁，**按照线程进入的先后顺序，实现执行顺序**，体现在卖票程序中就是三个窗口轮流卖票

```java
class Window2 implements Runnable{
    private int ticket=100;
    //1.实例化ReentrantLock
    private ReentrantLock lock=new ReentrantLock();

    @Override
    public void run() {
        while(true) {
            try {
                //2.调用lock方法
                lock.lock();

                if (ticket > 0) {
                    System.out.println(Thread.currentThread().getName() + "：卖票，票号为：" + ticket);
                    ticket--;
                } else {
                    break;
                }
            }finally{
                //3.调用解锁方法
                lock.unlock();
            }
        }
    }
}
```

如果同步代码有异常，要将unlock()写入finally语句块  

#### synchronized 与 Lock 的对比  

- Lock是显式锁（手动开启和关闭锁，别忘记关闭锁）， synchronized是隐式锁，出了作用域自动释放
- Lock只有代码块锁， synchronized有代码块锁和方法锁
- 使用Lock锁， JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性（提供更多的子类）

优先使用顺序：
Lock ——>同步代码块（已经进入了方法体，分配了相应资源）——>同步方法（在方法体之外）  

## 线程的通信  

例题：使用两个线程打印 1-100。线程1, 线程2 交替打印  

```java
class Communication implements Runnable {
    int i = 1;
    public void run() {
        while (true) {
            synchronized (this) {
                notify();//唤醒正在排队等待同步资源的线程中优先级最高者结束等待
                if (i <= 100) {
                    System.out.println(Thread.currentThread().getName() +":" + i++);
                } else
                    break;
                try {
                    wait();
                    //令当前线程挂起并放弃CPU、 同步资源并等待， 使别的线程可访问并修改共享资源
                    //当前线程排队等候其他线程调用notify()或notifyAll()方法唤醒
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

public class CommuncationTest {
    public static void main(String[] args) {
        Communication c=new Communication();
        Thread t1=new Thread(c);
        Thread t2=new Thread(c);

        t1.setName("线程1");
        t2.setName("线程2");

        t1.start();
        t2.start();
    }
}
```

`wait()` 与 `notify()` 和 `notifyAll()`  

- `wait()`：令当前线程挂起并放弃CPU、 同步资源并等待， 使别的线程可访问并修改共享资源，而当前线程排队等候其他线程调用notify()或notifyAll()方法唤醒，唤醒后等待重新获得对监视器的所有权后才能继续执行。
- `notify()`：唤醒正在排队等待同步资源的线程中优先级最高者结束等待
- `notifyAll ()`：唤醒正在排队等待资源的所有线程结束等待.  

注意

- 这三个方法只有在synchronized同步方法或代码块中才能使用，
- 这三个方法必须由同步锁对象调用，
- 由于任意对象都可以作为synchronized的同步锁，**因此这三个方法只能在Object类中声明**  

### wait() 方法  

在当前线程中调用方法： `对象名.wait()`，使当前线程进入等待（某对象）状态 ，直到另一线程对该对象发出 notify(或notifyAll) 为止。

调用方法的必要条件：当前线程必须具有对该对象的监控权（加锁）

调用此方法后，当前线程将释放对象监控权 ，然后进入等待。在当前线程被notify后，要重新获得监控权，然后从断点处继续代码的执行  

sleep()与wait()异同

1.相同点：一旦执行方法，都可以使得当前线程阻塞

2.不同点：

- 声明位置不同：sleep()在Thread中声明，wait()在Object中声明
- 调用要求不同：sleep()在任何场景都可以调用，wait()必须在同步代码块或方法中
- sleep()不会释放锁，wait()会释放锁

## JDK5.0新增线程创建方式  

### 方式1：实现Callable接口  

与使用Runnable相比， Callable功能更强大些

- 相比run()方法，call()可以有返回值
- 方法可以抛出异常
- 支持泛型的返回值
- 需要借助FutureTask类，比如获取返回结果  

Future接口  

- 可以对具体Runnable、 Callable任务的执行结果进行取消、查询是否完成、获取结果等。
- FutrueTask是Futrue接口的唯一的实现类
- FutureTask 同时实现了Runnable, Future接口。它既可以作为Runnable被线程执行，又可以作为Future得到Callable的返回值  

```java
//1.创建Callable接口的实现类
class NumThread implements Callable{
    //2.实现call()方法，将此线程需要执行的操作声明在call()中
    public Object call() throws Exception{
        int sum=0;
        for(int i=1;i<=100;i++){
            if(i%2==0){
                System.out.println(i);
                sum+=i;
            }
        }
        return sum;//自动装箱
    }
}
public class ThreadNew {
    public static void main(String[] args) {
        //3.创建Callable接口实现类的对象
        NumThread num=new NumThread();
        //4.将此对象作为实参传递到FutureTask构造器中，创建FutureTask的对象
        FutureTask futureTask=new FutureTask(num);
        //5.将FutureTask的对象作为参数传递到Thread类构造器中，创造Thread对象，并调用Start()
        new Thread(futureTask).start();

        try {
            //6.获取Callable中call()方法的返回值
            Object sum=futureTask.get();
            System.out.println("总和为"+sum);
        }catch(ExecutionException e){
            e.printStackTrace();
        }catch (InterruptedException e){
            e.printStackTrace();
        }
    }
}
```

### 方式2：使用线程池  

背景： 经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大。

思路： 提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁创建销毁、实现重复利用

好处：

- 提高响应速度（减少了创建新线程的时间）
- 降低资源消耗（重复利用线程池中线程，不需要每次都创建）
- 便于线程管理
  corePoolSize：核心池的大小
  maximumPoolSize：最大线程数
  keepAliveTime：线程没有任务时最多保持多长时间后会终止  

线程池相关API  

JDK 5.0起提供了线程池相关API： ExecutorService 和 Executors

ExecutorService：真正的线程池接口。常见子类ThreadPoolExecutor

- void `execute(Runnable command)` ：执行任务/命令，没有返回值，一般用来执行Runnable
- <T> Future<T> `submit(Callable<T> task)`：执行任务，有返回值，一般又来执行Callable
- void `shutdown()` ：关闭连接池

Executors：工具类、线程池的工厂类，用于创建并返回不同类型的线程池

- `Executors.newCachedThreadPool()`：创建一个可根据需要创建新线程的线程池
- `Executors.newFixedThreadPool(n)`： 创建一个可重用固定线程数的线程池
- `Executors.newSingleThreadExecutor()` ：创建一个只有一个线程的线程池
- `Executors.newScheduledThreadPool(n)`：创建一个线程池，它可安排在给定延迟后运行命令或者定期地执行  

```java
class Num1 implements Runnable {
    public void run(){
        for(int i=1;i<=100;i++){
            if(i%2==0){
                System.out.println(i);
            }
        }
    }
}

class Num2 implements Runnable {
    public void run(){
        for(int i=1;i<=100;i++){
            if(i%2!=0){
                System.out.println(i);
            }
        }
    }
}

public class ThreadPool {
    public static void main(String[] args) {
        //1.提供指定线程数量的线程池
        ExecutorService service= Executors.newFixedThreadPool(10);
        //2.执行指定的线程的操作。需要提供Runnable接口或Callable接口实现类的对象
        service.execute(new Num1());//适合使用于Runnable
        service.execute(new Num2());
        //service.submit();//适合使用于Callable
        //3.关闭连接池
        service.shutdown();
    }
}
```



# 集合

## 集合概述  

一方面， 面向对象语言对事物的体现都是以对象的形式，为了方便对多个对象的操作，就要对对象进行存储。另一方面，使用Array存储对象方面具有一些弊端，而Java**集合就像一种容器，可以动态地把多个对象的引用放入容器中**。此时的存储主要指内存方面的存储，不涉及持久化的存储

数组在内存存储方面的特点：

- 数组初始化以后，长度就确定了。
- 数组声明的类型，就决定了进行元素初始化时的类型

数组在存储数据方面的弊端：

- 数组初始化以后，长度就不可变了，不便于扩展
- 数组中提供的属性和方法少，不便于进行添加、删除、插入等操作， 且效率不高。同时无法直接获取存储元素的个数
- 数组存储的数据是有序的、可以重复的。 ---->存储数据的特点单一

Java 集合类可以用于存储数量不等的多个对象，还可用于保存具有映射关系的关联数组。  

### 集合的使用场景  

![image-20220130135252328](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220130135252328-166529427007845.png)

### Java 集合框架概述  

Java 集合可分为 Collection 和 Map 两种体系

- Collection接口： 单列数据， 定义了存取一组对象的方法的集合

  List： 元素**有序、可重复**的集合

  Set： 元素**无序、不可重复**的集合

- Map接口： 双列数据，保存具有映射关系“`key-value`对”的集合  

## Collection接口及方法  

Collection 接口是 List、 Set 和 Queue 接口的父接口，JDK不提供此接口的任何直接实现，而是提供子接口(如Set和List)实现。

在 Java5 之前， Java 集合会丢失容器中所有对象的数据类型，把所有对象都当成 Object 类型处理； 从 JDK 5.0 增加了泛型以后， **Java 集合可以记住容器中对象的数据类型**。  



**Collection 接口方法**  

添加

- `add(Object obj)`
- `addAll(Collection coll)`

获取有效元素的个数

- int `size()`

清空集合

- void `clear()`

是否是空集合

- boolean `isEmpty()`

是否包含某个元素

- boolean `contains(Object obj)`： 是通过元素的equals方法来判断是否是同一个对象
- boolean `containsAll(Collection c)`： 也是调用元素的equals方法来比较的。 拿两个集合的元素挨个比较

删除

- boolean `remove(Object obj)` ： 通过元素的equals方法判断是否是要删除的那个元素。 只会删除找到的第一个元素
- boolean `removeAll(Collection coll)`： 取当前集合的差集

取两个集合的交集

- boolean `retainAll(Collection c)`： 把交集的结果存在当前集合中，不影响c

集合是否相等

- boolean `equals(Object obj)`

转成对象数组

- Object[] `toArray()`

获取集合对象的哈希值

- `hashCode()`

遍历

- `iterator()`： 返回迭代器对象，用于集合遍历  

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Date;

class Person1{
    private String name;
    private int age;
    Person1(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
public class CollectionTest {
    @Test
    public void test1(){
        Collection coll=new ArrayList();
        //add()将元素添加到集合中
        coll.add("AA");
        coll.add("BB");
        coll.add(123);//自动装箱
        coll.add(new Date());
        coll.add(new String("Tom"));
        coll.add(new Person1("Han",22));
        //size()获取添加的元素的个数
        System.out.println(coll.size());
        //addAll()添加集合中的元素
        Collection coll1=new ArrayList();
        coll1.add(456);
        coll1.add("CC");
        coll.addAll(coll1);
        System.out.println(coll);
        //isEmpty()判断集合是否为空
        System.out.println(coll.isEmpty());
        //contains()判断是否包含某元素(利用equals方法判断)
        System.out.println(coll.contains(new String("Tom")));
        System.out.println(coll.contains(new Person1("Han", 22)));
    }
}
/*
6
[AA, BB, 123, Mon Jan 31 09:37:10 CST 2022, Tom, UsualClass.Person1@5eb5c224, 456, CC]
false
true
false
```



## Iterator迭代器接口

### 使用 Iterator 接口遍历集合元素  

Iterator对象称为迭代器(设计模式的一种)，主要用于遍历 Collection 集合中的元素。

GOF给迭代器模式的定义为：提供一种方法访问一个容器(container)对象中各个元素，而又不需暴露该对象的内部细节。 迭代器模式，就是为容器而生。 类似于“公交车上的售票员”、“火车上的乘务员”、 “空姐” 。

Collection接口继承了java.lang.Iterable接口，该接口有一个`iterator()`方法，那么所有实现了Collection接口的集合类都有一个`iterator()`方法，用以**返回一个实现了Iterator接口的对象**。

Iterator 仅用于遍历集合， Iterator 本身并不提供承装对象的能力。如果需要创建Iterator 对象，则必须有一个被迭代的集合。集合对象**每次调用**`iterator()`方法**都得到一个全新的迭代器对象**，默认游标都在集合的第一个元素之前。  

![image-20220130143353652](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220130143353652-166529427007740.png)

![image-20220130143402235](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220130143402235-166529427007841.png)

在调用`it.next()`方法之前必须要调用`it.hasNext()`进行检测。若不调用，且下一条记录无效，直接调用`it.next()`会抛出NoSuchElementException异常

```java
@Test
    public void test2(){
        Collection coll=new ArrayList();
        //add()将元素添加到集合中
        coll.add("AA");
        coll.add("BB");
        coll.add(123);//自动装箱
        coll.add(new Date());

        Iterator iterator= coll.iterator();
        System.out.println(iterator.next());
        System.out.println(iterator.next());
        System.out.println(iterator.next());
        System.out.println(iterator.next());
        System.out.println(iterator.next());
    }
/*
AA
BB
123
Mon Jan 31 09:41:55 CST 2022

java.util.NoSuchElementException
*/

@Test
    public void test3(){
        Collection coll=new ArrayList();
        //add()将元素添加到集合中
        coll.add("AA");
        coll.add("BB");
        coll.add(123);//自动装箱
        coll.add(new Date());

        Iterator iterator= coll.iterator();
        
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }
        
        //错误方式1
		Iterator iterator= coll.iterator();
        //除了空指针异常外，还会跳着输出
        while (iterator.next()!=null){
            System.out.println(iterator.next());
        }
        
        //错误方式2
        //持续输出"AA"
        while (coll.iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
/*
AA
BB
123
Mon Jan 31 09:41:55 CST 2022
*/
```

### Iterator接口remove()方法  

```java
Iterator iter = coll.iterator();//回到起点
while(iter.hasNext()){
	Object obj = iter.next();
	if(obj.equals(123)){
		iter.remove();
	}
}
```

注意：

- Iterator可以删除集合的元素， 但是是遍历过程中通过迭代器对象的remove方法， 不是集合对象的remove方法。
- 如果还未调用`next()`或在上一次调用 next 方法之后已经调用了 remove 方法，再调用remove都会报IllegalStateException。  

### 使用 foreach 循环遍历集合元素  

Java 5.0 提供了 foreach 循环迭代访问 Collection和数组。遍历操作不需获取Collection或数组的长度，无需使用索引访问元素。遍历集合的底层调用Iterator完成操作。foreach还可以用来遍历数组。  

![image-20220130143812108](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220130143812108-166529427007844.png)

```java
for(Object obj:coll){
    System.out.println(obj);
}
```

内部调用的仍然是迭代器



## Collection子接口之List

鉴于Java中数组用来存储数据的局限性，我们通常使用List替代数组

List集合类中**元素有序、且可重复**，集合中的每个元素都有其对应的顺序索引。List容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素。JDK API中List接口的实现类常用的有： `ArrayList`、 `LinkedList`和`Vector`。  



### List接口方法  

List除了从Collection集合继承的方法外， List 集合里添加了一些根据索引来操作集合元素的方法。

- void `add(int index, Object ele)`:在index位置插入ele元素
- boolean `addAll(int index, Collection eles)`:从index位置开始将eles中的所有元素添加进来
- Object `get(int index)`:获取指定index位置的元素
- int `indexOf(Object obj)`:返回obj在集合中首次出现的位置
- int `lastIndexOf(Object obj)`:返回obj在当前集合中末次出现的位置
- Object `remove(int index)`:移除指定index位置的元素，并返回此元素
- Object `set(int index, Object ele)`:设置指定index位置的元素为ele
- List `subList(int fromIndex, int toIndex)`:返回从fromIndex到toIndex位置的子集合  

```java
	@Test
    public void test3(){
        ArrayList list=new ArrayList<>();
        list.add(123);
        list.add("AA");
        list.add(new Person1("Wang",22));
        System.out.println(list);

        //add(int index, Object ele)
        list.add(1,"BB");
        System.out.println(list);
        //addAll(int index, Collection eles)
        List list1=Arrays.asList(1,2,3);
        list.addAll(list1);
        System.out.println(list);
        //get(int index)
        System.out.println(list.get(0));
    }
/*
[123, AA, Collection.Person1@6bf2d08e]
[123, BB, AA, Collection.Person1@6bf2d08e]
[123, BB, AA, Collection.Person1@6bf2d08e, 1, 2, 3]
123
*/
```



### List实现类之一： ArrayList

ArrayList 是 List 接口的典型实现类、主要实现类，本质上， ArrayList是**对象**引用的一个”变长”数组，线程不安全，效率高，底层使用Object[] elementData存储

ArrayList的JDK1.8之前与之后的实现区别？

- JDK1.7： ArrayList像饿汉式，直接创建一个初始容量为10的数组，当容量不足时直接扩容1.5倍，并将原有数据复制到新的数组中
- JDK1.8： ArrayList像懒汉式，一开始创建一个长度为0的数组，当添加第一个元素时再创建一个始容量为10的数组，扩容与1.7无异

`Arrays.asList(…)` 方法返回的 List 集合， 既不是 ArrayList 实例，也不是Vector 实例。 `Arrays.asList(…)` 返回值是一个**固定长度的 List 集合**  

![image-20220130144432328](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220130144432328-166529427007843.png)



### List实现类之二： LinkedList

对于频繁的插入或删除元素的操作，建议使用LinkedList类，效率较高，其新增方法：

- void `addFirst(Object obj)`
- void `addLast(Object obj)`
- Object `getFirst()`
- Object `getLast()`
- Object `removeFirst()`
- Object `removeLast()` 

LinkedList： 双向链表， 内部没有声明数组，而是定义了Node类型的first和last，用于记录首末元素。同时，定义内部类Node，作为LinkedList中保存数据的基本结构。 

Node除了保存数据，还定义了两个变量：

- prev变量记录前一个元素的位置
- next变量记录下一个元素的位置  

```java
private static class Node<E> {
	E item;
	Node<E> next;
	Node<E> prev;
    
	Node(Node<E> prev, E element, Node<E> next) {
		this.item = element;
		this.next = next;
		this.prev = prev;
	}
}
```

![image-20220130145022130](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220130145022130-166529427007846.png)



### List 实现类之三： Vector

Vector 是一个古老的集合， JDK1.0就有了。大多数操作与ArrayList相同，区别之处在于Vector是线程安全的。

在各种list中，最好把ArrayList作为缺省选择。当插入、删除频繁时，使用LinkedList； Vector总是比ArrayList慢，所以尽量避免使用。

新增方法：

- void `addElement(Object obj)`
- void `insertElementAt(Object obj,int index)`
- void `setElementAt(Object obj,int index)`
- void `removeElement(Object obj)`
- void `removeAllElements()`  



## Collection子接口之Set

Set接口是Collection的子接口，存储**无序、不可重复**的数据， set接口没有提供额外的方法

- 无序：不等于随机性，存储的数据在底层数组中并非按照索引的顺序添加，而是根据**数据的哈希值**决定
- 不可重复：Set 集合不允许包含相同的元素，如果试把两个相同的元素加入同一个Set 集合中，则添加操作失败。Set 判断两个对象是否相同不是使用 == 运算符，而是根据 `equals()` 方法，不能返回true

```java
@Test
    public void test4(){
        Set set=new HashSet();
        set.add(123);
        set.add("AA");
        set.add(new Person1("Tom",20));

        Iterator ite=set.iterator();
        while (ite.hasNext()){
            System.out.println(ite.next());
        }
    }
/*
AA
123
Collection.Person1@6bf2d08e
*/
```



### Set实现类之一： HashSet  

HashSet 是 Set 接口的典型实现，大多数时候使用 Set 集合时都使用这个实现类。HashSet 按 Hash 算法来存储集合中的元素，因此具有很好的存取、查找、删除性能。

HashSet 具有以下特点：

- 不能保证元素的排列顺序
- HashSet 不是线程安全的
- 集合元素可以是 null

HashSet 集合判断两个元素相等的标准： 两个对象通过 `hashCode()` 方法比较相等，并且两个对象的 `equals()` 方法返回值也相等。

对于**存放在Set容器中的对象**， 对应的**类一定要重写**`equals()`和`hashCode(Object obj)`方法，以实现对象相等规则。即： “相等的对象必须具有相等的散列码” 。  

向HashSet中添加元素的过程：

- 当向 HashSet 集合中存入一个元素a时， HashSet 会调用元素a的 `hashCode()` 方法来得到该对象的**哈希值**， 然后根据哈希值， 通过某种散列函数决定该对象在 HashSet 底层数组中的存储位置，判断在此位置上是否已经有其他元素 
- 如果此位置上没有其他元素，则元素a添加成功——>情况1
- 如果此位置上有其他元素b(或以链表形式存在的多个元素)，则比较元素a和元素b的哈希值
- 如果哈希值不同，则元素a添加成功——>情况2
- 如果两个元素的`hashCode()`值相等， 会再继续调用`equals()`方法，  如果为false， 那么元素a保存成功——>情况3
- 如果两个元素的 `equals()` 方法返回 true，但它们的 `hashCode()` 返回值不相等， HashSet 将会把它们存储在不同的位置，依然可以添加成功。  

![image-20220131121253598](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131121253598-166529427007847.png)

对于情况2、3，元素a与已经存在指定索引位置上的数据以链表的方式存储

- jdk7：元素a放到数组中，指向原来的元素
- jdk8：原来的元素放在数组中，指向元素a

HashSet底层也是数组， 初始容量为16， 当如果使用率超过0.75,（16*0.75=12）就会扩大容量为原来的2倍（16扩容为32， 依次为64,128等）  

重写 `hashCode()` 方法的基本原则

- 在程序运行时，同一个对象多次调用 `hashCode()` 方法应该返回相同的值。
- 当两个对象的 `equals()` 方法比较返回 true 时，这两个对象的 `hashCode()`方法的返回值也应相等。
- 对象中用作 `equals()` 方法比较的属性，都应该用来计算哈希值。  

重写 `equals()` 方法的基本原则  

以自定义的Customer类为例，何时需要重写`equals()`？

- 当一个类有自己特有的“逻辑相等”概念,当改写`equals()`的时候，总是要改写`hashCode()`，根据一个类的equals方法（改写后），两个截然不同的实例有可能在逻辑上是相等的，但是， 根据`Object.hashCode()`方法，它们仅仅是两个对象。
- 因此，违反了“相等的对象必须具有相等的散列码”。
- 结论：复写`equals()`方法的时候一般都需要同时复写`hashCode()`方法。 通常参与计算`hashCode()`的对象的属性也应该参与到`equals()`中进行计算。  

IDEA工具里hashCode()的重写

IDEA为例，在自定义类中可以调用工具自动重写equals和hashCode。

问题： 为什么用IDEA复写hashCode方法，有31这个数字？  

- 选择系数的时候要选择尽量大的系数。因为如果计算出来的hash地址越大，所谓的“冲突”就越少，查找起来效率也会提高。（减少冲突）
- 并且31只占用5bits,相乘造成数据溢出的概率较小。
- 31可以 由i*31== (i<<5)-1来表示,现在很多虚拟机里面都有做相关优化。 （提高算法效率）
- 31是一个素数，素数作用就是如果我用一个数字来乘以这个素数，那么最终出来的结果只能被素数本身和被乘数还有1来整除！ (减少冲突)  



### Set实现类之二： LinkedHashSet

- LinkedHashSet 是 HashSet 的子类
- LinkedHashSet 根据元素的 hashCode 值来决定元素的存储位置，但它同时使用双向链表维护元素的次序，这使得元素看起来是以插入顺序保存的。
- LinkedHashSet插入性能略低于 HashSet， 但在迭代访问 Set 里的全部元素时有很好的性能。
- LinkedHashSet 不允许集合元素重复  

![image-20220131122551154](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131122551154-166529427007848.png)



### Set实现类之三： TreeSet  

TreeSet 是 SortedSet 接口的实现类， TreeSet 可以确保**集合元素处于排序状态**。TreeSet底层使用红黑树结构存储数据

新增的方法如下： (了解)

- Comparator `comparator()`
- Object `first()`
- Object `last()`
- Object `lower(Object e)`
- Object `higher(Object e)`
- SortedSet `subSet(fromElement, toElement)`
- SortedSet `headSet(toElement)`
- SortedSet `tailSet(fromElement)`

TreeSet 两种排序方法： 自然排序和定制排序。默认情况下， TreeSet 采用自然排序。  

TreeSet和后面要讲的TreeMap采用红黑树的存储结构  

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131123258842-166529427007854.png" alt="image-20220131123258842" style="zoom:50%;" />

特点：有序，查询速度比List快  



#### 排 序—自然排序

自然排序： TreeSet 会调用集合元素的 compareTo(Object obj) 方法来比较元素之间的大小关系，然后将集合元素按升序(默认情况)排列

如果试图把一个对象添加到 TreeSet 时，则该对象的类必须实现 Comparable接口。实现 Comparable 的类必须实现 compareTo(Object obj) 方法，两个对象即通过compareTo(Object obj) 方法的返回值来比较大小。

Comparable 的典型实现：

- BigDecimal、 BigInteger 以及所有的数值型对应的包装类：按它们对应的数值大小进行比较
- Character：按字符的 unicode值来进行比较
- Boolean： true 对应的包装类实例大于 false 对应的包装类实例
- String：按字符串中字符的 unicode 值进行比较
- Date、 Time：后边的时间、日期比前面的时间、日期大  

向 TreeSet 中添加元素时，只有第一个元素无须比较compareTo()方法，后面添加的所有元素都会调用compareTo()方法进行比较。因为只有相同类的两个实例才会比较大小，所以**向 TreeSet 中添加的应该是同一个类的对象**。

对于 TreeSet 集合而言，它**判断两个对象是否相等的唯一标准**是：两个对象通过 `compareTo(Object obj)` 方法比较返回值。

当需要把一个对象放入 TreeSet 中，重写该对象对应的 `equals()` 方法时，应保证该方法与 compareTo(Object obj) 方法有一致的结果：**如果两个对象通过equals() 方法比较返回 true，则通过 compareTo(Object obj) 方法比较应返回 0**。否则，让人难以理解。  



#### 排 序—定制排序

TreeSet的自然排序要求元素所属的类实现Comparable接口，如果元素所属的类没有实现Comparable接口，或不希望按照升序(默认情况)的方式排列元素或希望按照其它属性大小进行排序，则考虑使用定制排序。定制排序，通过Comparator接口来实现。 需要重写`compare(T o1,T o2)`方法。

利用int `compare(T o1,T o2)`方法，比较o1和o2的大小：如果方法返回正整数，则表示o1大于o2；如果返回0，表示相等；返回负整数，表示o1小于o2。

要实现定制排序，需要将实现Comparator接口的实例作为形参传递给TreeSet的构造器。此时， 仍然只能向TreeSet中添加类型相同的对象。否则发生ClassCastException异常。

使用定制排序判断两个元素相等的标准是：通过Comparator比较两个元素返回了0。  



## Map接口  

### Map接口继承树

![image-20220131124424583](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131124424583-166529427007850.png)

### Map接口概述  

Map与Collection并列存在，用于保存具有映射关系的数据:key-value，key 和 value 都可以是任何引用类型的数据

Map 中的 key 用Set来存放， 不允许重复，即同一个 Map 对象所对应的类，须重写`hashCode()`和`equals()`方法，常用String类作为Map的“键”。key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到**唯一的、确定的** value

Map接口的常用实现类： HashMap、 TreeMap、 LinkedHashMap和Properties。 其中， HashMap是 Map 接口使用频率最高的实现类 

- HashMap：Map的主要实现类，线程不安全，效率高，可以存储null的key和value
- LinkedHashMap：保证在遍历Map元素时，可以按添加的顺序实现遍历。原因：在原有的HashMap底层基础结构上添加了一对指针，指向前一个元素和后一个元素。对于频繁的遍历操作，此类执行效率高于HashMap
- TreeMap：保证按照添加的key-value对进行排序，实现排序遍历。此时考虑key的自然排序或定制排序。底层为红黑树
- Properties：常用来处理配置文件，key和value都是String类型 



### 常用方法

添加、 删除、修改操作：

- Object `put(Object key,Object value)`：将指定key-value添加到(或修改)当前map对象中
- void `putAll(Map m)`:将m中的所有key-value对存放到当前map中
- Object `remove(Object key)`：移除指定key的key-value对，并返回value
- void `clear()`：清空当前map中的所有数据

元素查询的操作：

- Object `get(Object key)`：获取指定key对应的value
- boolean `containsKey(Object key)`：是否包含指定的key
- boolean `containsValue(Object value)`：是否包含指定的value
- int `size()`：返回map中key-value对的个数
- boolean `isEmpty()`：判断当前map是否为空
- boolean `equals(Object obj)`：判断当前map和参数对象obj是否相等

元视图操作的方法：

- Set `keySet()`：返回所有key构成的Set集合
- Collection `values()`：返回所有value构成的Collection集合
- Set `entrySet()`：返回所有key-value对构成的Set集合  



### Map实现类之一： HashMap

HashMap是 Map 接口使用频率最高的实现类。

允许使用null键和null值，与HashSet一样，不保证映射的顺序。

- 所有的key构成的集合是Set：无序的、**不可重复**的。所以， key所在的类要重写`equals()`和`hashCode()`
- 所有的value构成的集合是Collection：无序的、可以重复的。所以， value所在的类要重写`equals()`
- 一个key-value构成一个entry，所有的**entry构成的集合是Set**：无序的、**不可重复**的
- HashMap判断两个 key 相等的标准是：两个 key 通过 `equals()` 方法返回 true，哈希值也相等。
- HashMap 判断两个 value相等的标准是：两个 value 通过 `equals()` 方法返回 true  

![image-20220131124856380](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131124856380-166529427007849.png)

```java
@Test
public void test1() {
    Map map = new HashMap();
    map.put("AA","A");
    map.put(123,1);
    map.put("BB","B");
    map.put(456,4);

    System.out.println(map);

    System.out.println("map的所有key:");
    Set keys = map.keySet();// HashSet
    for (Object key : keys) {
        System.out.println(key + "->" + map.get(key));
    }
    System.out.println("map的所有的value：");
    Collection values = map.values();
    Iterator iter = values.iterator();
    while (iter.hasNext()) {
        System.out.println(iter.next());
    }
    System.out.println("map所有的映射关系：");
    // 映射关系的类型是Map.Entry类型，它是Map接口的内部接口
    Set mappings = map.entrySet();
    for (Object mapping : mappings) {
        Map.Entry entry = (Map.Entry) mapping;
        System.out.println("key是：" + entry.getKey() + "，value是：" + entry.getValue());
    }
}
/*
{AA=A, BB=B, 456=4, 123=1}
map的所有key:
AA->A
BB->B
456->4
123->1
map的所有的value：
A
B
4
1
map所有的映射关系：
key是：AA，value是：A
key是：BB，value是：B
key是：456，value是：4
key是：123，value是：1
*/
```

#### HashMap的存储结构   

**JDK 1.8之前**

![image-20220131130302732](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131130302732-166529427007851.png)

HashMap的内部存储结构其实是**数组和链表**的结合。 

当实例化一个HashMap时，系统会创建一个长度为Capacity（默认16）的Entry数组， 这个长度在哈希表中被称为容量。

在这个数组中可以存放元素的**位置**我们称之为“桶” (bucket)， 每个bucket都有自己的索引， 系统可以根据索引快速的查找bucket中的元素。每个bucket中存储一个元素， 即一个Entry对象， 但每一个Entry对象可以带一个**引用变量**， 用于指向下一个元素， 因此， 在一个桶中， 就有可能生成一个Entry链。而且**新添加的元素作为链表的head**。

**添加元素的过程**

- 向HashMap中添加entry1(key， value)， 需要首先计算entry1中key的哈希值(根据key所在类的`hashCode()`计算得到)， 此哈希值经过处理以后， 得到在底层Entry[]数组中要存储的位置i。 
- 如果位置i上没有元素， 则entry1直接添加成功。
- 如果位置i上已经存在entry2(或还有链表存在的entry3， entry4)， 则需要通过循环的方法， 依次比较entry1中**key**和其他的entry。 
- 如果哈希值不同， 则直接添加成功。 
- 如果哈希值相同， 继续比较二者是否equals。 
- 如果返回值为true， 则使用entry1的value去替换**equals为true的entry的value**。 
- 如果遍历一遍以后， 发现所有的equals返回都为false，则entry1仍可添加成功。 entry1指向原有的entry元素。  

**HashMap的扩容**

当HashMap中的元素越来越多的时候， hash冲突的几率也就越来越高， 因为数组的长度是固定的。 所以为了提高查询的效率， 就要对HashMap的数组进行扩容， 而在HashMap数组扩容之后， 最消耗性能的点就出现了：原数组中的数据必须重新计算其在新数组中的位置， 并放进去， 这就是resize

**HashMap什么时候进行扩容**

当HashMap中的元素个数超过（数组大小 * loadFactor） 时 ， 就 会 进 行 数 组 扩 容 

loadFactor 的 默 认 值(DEFAULT_LOAD_FACTOR)为0.75， 这是一个折中的取值，数组大小默认值(DEFAULT_INITIAL_CAPACITY)为16， 当HashMap中元素个数超过16 * 0.75=12（这个值就是代码中的threshold值， 也叫做临界值）的时候， 就把数组的大小扩展为2*16=32， 即**扩大一倍**， 然后重新计算每个元素在数组中的位置，而这是一个非常消耗性能的操作， 所以如果我们已经预知HashMap中元素的个数，那么预设元素的个数能够有效的提高HashMap的性能

**JDK 1.8**

![image-20220131130318541](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131130318541-166529427007852.png)

HashMap的内部存储结构其实是**数组+链表+树**的结合。 

当实例化一个HashMap时， 会初始化initialCapacity和loadFactor， 在put第一对映射关系时， 系统会创建一个长度为initialCapacity的Node数组， 这个长度在哈希表中被称为容量(Capacity)。

在这个数组中可以存放元素的位置我们称之为“桶” (bucket)， 每个bucket都有自己的索引， 系统可以根据索引快速的查找bucket中的元素。每个bucket中存储一个元素， 即一个Node对象， 但每一个Node对象可以带一个引用变量next， 用于指向下一个元素， 因此， 在一个桶中， 就有可能生成一个Node链。 

也可能是一个一个TreeNode对象， 每一个TreeNode对象可以有两个叶子结点left和right， 因此， 在一个桶中， 就有可能生成一个TreeNode树。 而新添加的元素作为链表的last， 或树的叶子结点

**HashMap什么时候进行扩容和树形化**

当HashMap中的元素个数超过（数组大小 * loadFactor）时 ， 就 会 进 行 数 组 扩 容

loadFactor 的 默 认 值(DEFAULT_LOAD_FACTOR)为0.75， 这是一个折中的取值，数组默认大小(DEFAULT_INITIAL_CAPACITY)为16， 当HashMap中元素个数超过16 * 0.75=12（这个值就是代码中的threshold值， 也叫做临界值）的时候， 就把数组的大小扩展为2*16=32， 即扩大一倍， 然后重新计算每个元素在数组中的位置， 而这是一个非常消耗性能的操作， 所以如果我们已经预知HashMap中元素的个数， 那么预设元素的个数能够有效的提高HashMap的性能。

当HashMap中的其中一个链的对象个数如果达到了8个

- 如果capacity没有达到64，那么HashMap会先扩容解决
- 如果已经达到了64，那么这个链会变成树，结点类型由Node变成TreeNode类型
- 如果当映射关系被移除后，下次resize方法时判断树的结点个数低于6个，也会把树再转为链表。  

关于映射关系的key是否可以修改？ answer：不要修改

映射关系存储到HashMap中会存储key的hash值，这样就不用在每次查找时重新计算每一个Entry或Node（TreeNode）的hash值了，因此如果已经put到Map中的映射关系，再修改key的属性，而这个属性又参与hashcode值的计算，那么会导致匹配不上。  

总结： JDK1.8相较于之前的变化：

- `HashMap map = new HashMap()`;//默认情况下，先不创建长度为16的数组
- 当首次调用`map.put()`时，再创建长度为16的数组
- 数组为Node类型，在jdk7中称为Entry类型
- 形成链表结构时，新添加的key-value对在链表的尾部（七上八下）
- 当数组指定索引位置的链表长度>8时，且map中的数组的长度> 64时，此索引位置上的所有key-value对使用红黑树进行存储。  

#### HashMap源码中的重要常量

DEFAULT_INITIAL_CAPACITY : HashMap的默认容量， 16

MAXIMUM_CAPACITY ： HashMap的最大支持容量， 2^30

DEFAULT_LOAD_FACTOR： HashMap的默认加载因子

TREEIFY_THRESHOLD： Bucket中链表长度大于该默认值，转化为红黑树

UNTREEIFY_THRESHOLD： Bucket中红黑树存储的Node小于该默认值，转化为链表

MIN_TREEIFY_CAPACITY： 桶中的Node被树化时最小的hash表容量。（当桶中Node的数量大到需要变红黑树时，若hash表容量小于MIN_TREEIFY_CAPACITY时，此时应执行resize扩容操作这个MIN_TREEIFY_CAPACITY的值至少是TREEIFY_THRESHOLD的4倍。）

table： 存储元素的数组，总是2的n次幂

entrySet： 存储具体元素的集

size： HashMap中存储的键值对的数量

modCount： HashMap扩容和结构改变的次数。

threshold： 扩容的临界值， =容量*填充因子

loadFactor： 填充因子  

面试题：负载因子值的大小，对HashMap有什么影响

- 负载因子的大小决定了HashMap的数据密度。
- 负载因子越大密度越大，发生碰撞的几率越高，数组中的链表越容易长,造成查询或插入时的比较次数增多，性能会下降。
- 负载因子越小，就越容易触发扩容，数据密度也越小，意味着发生碰撞的几率越小，数组中的链表也就越短，查询和插入时比较的次数也越小，性能会更高。但是会浪费一定的内容空间。而且经常扩容也会影响性能，建议初始化预设大一点的空间。
- 按照其他语言的参考及研究经验，会考虑将负载因子设置为0.7~0.75，此时平均检索长度接近于常数。  

### Map实现类之二： LinkedHashMap

LinkedHashMap 是 HashMap 的子类，在HashMap存储结构的基础上，**使用了一对双向链表来记录添加元素的顺序**，与LinkedHashSet类似， LinkedHashMap可以维护 Map 的迭代顺序：迭代顺序与 Key-Value 对的插入顺序一致

HashMap中的内部类： Node

```java
static class Node<K,V> implements Map.Entry<K,V> {
	final int hash;
	final K key;
	V value;
	Node<K,V> next;
}
```

LinkedHashMap中的内部类： Entry

```java
static class Entry<K,V> extends HashMap.Node<K,V> {
	Entry<K,V> before, after;
	Entry(int hash, K key, V value, Node<K,V> next) {
		super(hash, key, value, next);
	}
}
```

### Map实现类之三： TreeMap

TreeMap存储 Key-Value 对时， 需要根据 key-value 对进行排序。TreeMap 可以保证所有的 Key-Value 对处于有序状态。TreeSet底层使用红黑树结构存储数据

TreeMap 的 Key 的排序：

- 自然排序： TreeMap 的所有的 Key 必须实现 Comparable 接口，而且所有的 Key 应该是同一个类的对象，否则将会抛出 ClasssCastException
- 定制排序：创建 TreeMap 时，传入一个 Comparator 对象，该对象负责对TreeMap 中的所有 key 进行排序。此时不需要 Map 的 Key 实现Comparable 接口

TreeMap判断两个key相等的标准：两个key通过compareTo()方法或者compare()方法返回0。  

### Map实现类之四： Hashtable

Hashtable是个古老的 Map 实现类， JDK1.0就提供了。Hashtable实现原理和HashMap相同，功能相同。底层都使用哈希表结构，查询速度快，很多情况下可以互用。 与HashMap一样， Hashtable 也不能保证其中 Key-Value 对的顺序，Hashtable判断两个key相等、两个value相等的标准， 与HashMap一致。

不同于HashMap：

- Hashtable是线程安全的
- Hashtable 不允许使用 null 作为 key 和 value

###  Map实现类之五： Properties  

Properties 类是 Hashtable 的子类，该对象用于处理属性文件

由于属性文件里的 key、 value 都是字符串类型，所以 Properties 里的 key和 value 都是字符串类型

存取数据时，建议使用`setProperty(String key,String value)`方法和`getProperty(String key)`方法  

```java
Properties pros = new Properties();
pros.load(new FileInputStream("jdbc.properties"));
String user = pros.getProperty("user");
System.out.println(user);
```

## Collections工具类

Collections 是一个操作 Set、 List 和 Map 等集合的工具类，Collections 中提供了一系列静态的方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法  

排序操作： （均为static方法）

- `reverse(List)`： 反转 List 中元素的顺序
- `shuffle(List)`： 对 List 集合元素进行随机排序
- `sort(List)`： 根据元素的自然顺序对指定 List 集合元素按升序排序
- `sort(List， Comparator)`： 根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
- `swap(List， int， int)`： 将指定 list 集合中的 i 处元素和 j 处元素进行交换  

### Collections常用方法

查找、替换

- Object `max(Collection)`： 根据元素的自然顺序，返回给定集合中的最大元素
- Object `max(Collection， Comparator)`： 根据 Comparator 指定的顺序，返回给定集合中的最大元素
- Object `min(Collection)`
- Object `min(Collection， Comparator)`
- int `frequency(Collection， Object)`： 返回指定集合中指定元素的出现次数
- void `copy(List dest,List src)`：将src中的内容复制到dest中
- boolean `replaceAll(List list，Object oldVal，Object newVal)`： 使用新值替换List 对象的所有旧值  

### Collections常用方法：同步控制

Collections 类中提供了多个 `synchronizedXxx()` 方法，该方法可使将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题  

![image-20220131135043965](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131135043965-166529427007853.png)



# 泛型

## 为什么要有泛型

集合容器类在设计阶段/声明阶段不能确定这个**容器到底实际存的是什么类型的对象**， 所以在JDK1.5之前只能把元素类型设计为Object， JDK1.5之后使用泛型来解决。 因为这个时候除了元素的类型不确定， 其他的部分是确定的， 例如关于这个元素如何保存， 如何管理等是确定的， 因此此时**把元素的类型设计成一个参数， 这个类型参数叫做泛型**。 `Collection<E>， List<E>， ArrayList<E>`， 这个`<E>`就是类型参数， 即泛型。  

### 泛型的概念

所谓泛型， 就是允许在定义类、 接口时通过一个标识表示**类中某个属性的类型或者是某个方法的返回值及参数类型**。 这个类型参数将在使用时（例如，继承或实现这个接口， 用这个类型声明变量、 创建对象时）确定（即传入实际的类型参数，也称为类型实参）。

从JDK1.5以后， Java引入了“参数化类型（ Parameterized type） ” 的概念，允许我们在创建集合时指定集合元素的类型， 正如： `List<String>`， 这表明该List只能保存字符串类型的对象。

JDK1.5改写了集合框架中的全部接口和类， 为这些接口、 类增加了泛型支持，从而可以在声明集合变量、 创建集合对象时传入类型实参。

### 为什么要有泛型

- 解决元素存储的安全性问题
- 解决获取数据元素时， 需要类型强制转换的问题

在集合中没有泛型时

![image-20220131135959110](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131135959110-166529427007856.png)

- 任何类型都可以添加到集合中： 类型不安全  
- 读取出来的对象需要强转， 繁琐，可能有ClassCastException  

```java
import org.junit.Test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class GenericTest {
    public void test1(){
        ArrayList list=new ArrayList();
        //需求：存放学生成绩
        list.add(67);
        list.add(79);
        list.add(85);
        list.add(70);
        //问题1：类型不安全
        list.add("Tom");
        for(Object score:list){
            //问题2:强转时，可能出现ClassCastException
            int stuScore=(Integer)score;
            System.out.println(stuScore);
        }
    }
```

在集合中有泛型时

![image-20220131140123142](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220131140123142-166529427007855.png)

- 只有指定类型才可以添加到集合中：类型安全 
- 读取出来的对象不需要强转：便捷  

```java
 @Test
    public void test2(){
        ArrayList<Integer> list1=new ArrayList<Integer>();
        list1.add(67);
        list1.add(79);
        list1.add(85);
        list1.add(70);
        for(Integer score:list1){
            System.out.println(score);
        }

    }
```

Java泛型可以保证如果程序在编译时没有发出警告，运行时就不会产生ClassCastException异常。同时，代码更加简洁、健壮。  

## 在集合中使用泛型

集合接口或集合类在jdk5.0时都修改为带泛型的结构

- 在实例化集合类后，可以指明具体的泛型类型
- 指明完以后，在集合类或接口中凡是定义类或接口时，内部结构(方法、构造器、属性)使用到类的泛型位置，都指定为实例化时的泛型类型。比如：`add<E e>`---->实例化后：`add(Integer e)`
- 泛型的类型必须是类，不能是基本类型数据，需要用到基本数据类型的位置用包装类替代
- 如果实例化时没有指明泛型类型，默认类型为java.lang.Object

```java
    @Test
    public void test3(){
        
        Map<String,Integer> map=new HashMap<String,Integer>();
        
        map.put("Tom",87);
        map.put("Jerry",69);
        map.put("Jack",79);
        Set<Map.Entry<String,Integer>> entry=map.entrySet();
        System.out.println(entry);
    }
/*
[Tom=87, Jerry=69, Jack=79]
*/
```

## 自定义泛型结构

### 泛型类、泛型接口

```java
class Order<T>{
    String orderName;
    int orderID;

    //类的内部构造就可以使用类的泛型
    T orderT;

    public Order(){};
    public Order(String orderName,int orderID,T orderT){
        this.orderName=orderName;
        this.orderID=orderID;
        this.orderT=orderT;
    }
    
    public T getOrderT() {
        return orderT;
    }
    
    public void setOrderT(T orderT) {
        this.orderT = orderT;
    }
}
```

- T不代表值，而是表示类型。 这里使用任意字母都可以，常用T表示，是Type的缩写
- 泛型类可能有多个参数，此时应将多个参数一起放在尖括号内。比如：`<E1,E2,E3>`
- 泛型类的构造器如下： `public GenericClass(){}`。而`public GenericClass<E>(){}`是错误的
- 在类/接口上声明的泛型，在本类或本接口中即代表某种类型，可以作为非静态属性的类型、非静态方法的参数类型、非静态方法的返回值类型。但在静态方法中不能使用类的泛型
- 异常类不能是泛型的

泛型如果不指定，将被擦除，泛型对应的类型均按照Object处理，但不等价于Object。 经验： 泛型要使用一路都用；要不用一路都不要用。建议在实例化时指明类的泛型。

```java
@Test
    public void test4(){
        Order<String> order=new Order<String>("orderAA",1000,"order:AA");
        order.setOrderT("hello");
    }
```

- 如果泛型结构是一个接口或抽象类，则不可创建泛型类的对象
- jdk1.7，泛型实例化的简化操作： `ArrayList<Fruit> flist = new ArrayList<>();` 
- **T只能是类**，不能用基本数据类型填充。但可以使用包装类填充
- 实例化后，操作原来泛型位置的结构必须与指定的泛型类型一致
- 泛型不同的引用不能相互赋值。在编译时`ArrayList<String>`和`ArrayList<Integer>`是两种类型，在运行时只有一个ArrayList被加载到 JVM中
- 使用泛型的主要优点是能够在编译时而不是在运行时检测错误
- 不能使用`new E[]`。但是可以`E[] elements = (E[])new Object[capacity]`；参考： ArrayList源码中声明： `Object[] elementData`， 而非泛型参数类型数组。

父类有泛型，子类可以选择保留泛型也可以选择指定泛型类型

如果子类继承带泛型的父类时，已经直接指明泛型类型，则实例化该子类时不需要再次指明泛型。此时的SubOrder已经不再是泛型类

```java
class SubOrder extends Order<Integer>{}
    
@Test
    public void test5(){
        SubOrder sub=new SubOrder();
        sub.setOrderT(1122);
    }
```

如果子类继承带泛型的父类时未指明泛型类型，则实例化该子类时需要指明泛型。此时的SubOrder已经仍然是泛型类

```java
class SubOrder1<T> extends Order<T>{}

@Test
    public void test6(){
        SubOrder1<String> sub=new SubOrder1<>();
        sub.setOrderT("order2");
    }
```

- 子类不保留父类的泛型：按需实现
   没有类型 擦除
   具体类型
- 子类保留父类的泛型：泛型子类
   全部保留
   部分保留

结论：子类必须是“富二代”，子类除了指定或保留父类的泛型，还可以增加自己的泛型  

### 泛型方法

方法也可以被泛型化，在泛型方法中可以定义泛型参数

此时，参数的类型就是传入数据的类型。方法的泛型参数与类的泛型参数没有任何联系，不管此时定义在其中的类是不是泛型类。   

泛型方法的格式：  

```java
[访问权限] <泛型> 返回类型 方法名([泛型标识 参数名称]) 抛出的异常
```

 举例

```java
class Order<T>{
    String orderName;
    int orderID;

    //类的内部构造就可以使用类的泛型
    T orderT;

    public Order(){};
    public Order(String orderName,int orderID,T orderT){
        this.orderName=orderName;
        this.orderID=orderID;
        this.orderT=orderT;
    }

    public <E>List<E> copyFromArrayList(E[] arr){
        ArrayList<E> list=new ArrayList<>();
        for (E e:arr){
            list.add(e);
        }
        return list;
    }
}

	@Test
    public void test7(){
        Order<String> order=new Order<>();
        Integer[] arr=new Integer[]{1,2,3,4};
        List<Integer> list=order.copyFromArrayList(arr);
        System.out.println(list);
    }
```

泛型方法可以声明为static

## 泛型在继承上的体现  

如果B是A的一个子类型（子类或者子接口），而G是具有泛型声明的类或接口， `G<B>`并不是`G<A>`的子类型！比如： String是Object的子类，但是`List<String >`并不是`List<Object>`的子类  

补充：类A是类B的父类，`A<G>`是`B<G>`的父类

## 通配符的使用

使用类型通配符：？

比如： `List<?> ，Map<?,?>`。`List<?>`是`List<String>、 List<Object>`等各种泛型List的父类。

读取`List<?>`的对象list中的元素时，永远是安全的，因为不管list的真实类型是什么，它包含的都是Object。

写入list中的元素时：不行  

```java
Collection<?> c = new ArrayList<String>();
c.add(new Object()); // 编译时错误
```

add方法有类型参数E作为集合的元素类型。我们传给add的任何参数都必须是一个未知类型的子类。因为我们不知道那是什么类型，所以我们无法传任何东西进去。

唯一的例外的是null，它是所有类型的成员。另一方面，我们可以调用get()方法并使用其返回值。返回值是一个未知的类型，但是我们知道，它总是一个Object 

### 注意点

```java
//注意点1：编译错误：不能用在泛型方法声明上，返回值类型前面<>不能使用?
public static <?> void test(ArrayList<?> list){}
//注意点2：编译错误：不能用在泛型类的声明上
class GenericTypeClass<?>{}
//注意点3：编译错误：不能用在创建对象上，右边属于创建集合对象
ArrayList<?> list2 = new ArrayList<?>();
```

### 有限制的通配符  

<?>允许所有泛型的引用调用

通配符指定上限

- 上限extends：使用时指定的类型必须是继承某个类，或者实现某个接口，即<=

通配符指定下限

- 下限super：使用时指定的类型不能小于操作的类，即>=

举例：

```java
<? extends Number> (无穷小 , Number]
```

只允许泛型为Number及Number子类的引用调用

```java
<? super Number> [Number , 无穷大)
```

只允许泛型为Number及Number父类的引用调用

```java
<? extends Comparable>
```

只允许泛型为实现Comparable接口的实现类的引用调用  



# IO流

## File类

java.io.File类：文件和文件目录路径的抽象表示形式，与平台无关

File 能新建、删除、重命名文件和目录，但 File 不能访问文件内容本身。如果需要访问文件内容本身，则需要使用输入/输出流。 

想要在Java程序中表示一个真实存在的文件或目录，那么必须有一个File对象，但是Java程序中的一个File对象，可能没有一个真实存在的文件或目录。**File对象可以作为参数传递给流的构造器**

### 常用构造器

public `File(String pathname)` ：以pathname为路径创建File对象，可以是**绝对路径或者相对路径**，如果pathname是相对路径，则默认的当前路径在系统属性user.dir中存储。

- 绝对路径：是一个固定的路径,从盘符开始
- 相对路径：是相对于某个位置开始

public `File(String parent,String child)`：以parent为父路径，child为子路径创建File对象。 

public `File(File parent,String child)`：根据一个父File对象和子文件路径创建File对象

```java
@Test
public void test1(){
    //构造器1
    File file1=new File("test.txt");//相对于当前的moudle
    File file2=new File("F:\\JavaStudy\\JavaSEStudy\\test.txt");
    //构造器2
    File file3= new File("F:\\JavaStudy", "JavaSEStudy");
    //构造器3
    new File(file3,"test.txt");
}
```



### **路径分隔符**

路径中的每级目录之间用一个**路径分隔符**隔开。路径分隔符和系统有关：

- windows和DOS系统默认使用“ \ \ ”来表示
- UNIX和URL使用“/”来表示

Java程序支持跨平台运行，因此路径分隔符要慎用。为了解决这个隐患，File类提供了一个常量：public static final String `separator`。根据操作系统，动态的提供分隔符

```java
File file1 = new File("d:\\atguigu\\info.txt");
File file2 = new File("d:" + File.separator + "atguigu" + File.separator + "info.txt");
File file3 = new File("d:/atguigu");
```

![image-20220203225428472](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220203225428472-166529427007857.png)

### 常用方法

#### 信息获取

public String `getAbsolutePath()`：获取绝对路径

public String `getPath()` ：获取路径

public String `getName()` ：获取名称

public String `getParent()`：获取上层文件目录路径。若无，返回null

public long `length()` ：获取文件长度（即：字节数）。不能获取目录的长度。 

public long `lastModified()` ：获取最后一次的修改时间，毫秒值

```java
@Test
public void test2(){
    File file1=new File("test.txt");//硬盘中存在该文件
    File file2 = new File("hello.txt");//硬盘中不存在该文件
    System.out.println(file1.getAbsolutePath());
    System.out.println(file1.getPath());
    System.out.println(file1.getName());
    System.out.println(file1.getParent());
    System.out.println(file1.length());
    System.out.println(file1.lastModified());
    System.out.println();
    System.out.println(file2.getAbsolutePath());
    System.out.println(file2.getPath());
    System.out.println(file2.getName());
    System.out.println(file2.getParent());
    System.out.println(file2.length());
    System.out.println(file2.lastModified());
}
/*
F:\JavaStudy\JavaSEStudy\test.txt
test.txt
test.txt
null
12
1644042632357

F:\JavaStudy\JavaSEStudy\hello.txt
hello.txt
hello.txt
null
0
0
```

public String[] `list()` ：获取指定目录下的所有文件或者文件目录的名称数组

public File[] `listFiles()` ：获取指定目录下的所有文件或者文件目录的File数组

```java
@Test
public void test3(){
    File file1 = new File("F:\\JavaStudy\\JavaSEStudy");
    String[] list=file1.list();
    for(String s:list){
        System.out.println(s);
    }
    File[] file= file1.listFiles();
    for (File f:file){
        System.out.println(f);
    }
}
/*
JavaSEStudy.iml
src
test.txt
F:\JavaStudy\JavaSEStudy\JavaSEStudy.iml
F:\JavaStudy\JavaSEStudy\src
F:\JavaStudy\JavaSEStudy\test.txt
```



#### 重命名

public boolean `renameTo(File dest)`:把文件重命名为指定的文件路径

```java
@Test
public void test4(){
    File file1=new File("test.txt");
    File file2=new File("F:\\test1.txt");
    File file3=new File("F:\\test\\test2.txt");

    boolean renameTo1=file1.renameTo(file2);//由于file1在硬盘中存在，file2文件在硬盘中不存在，因此file1重写到file2，结果为true
    boolean renameTo2=file2.renameTo(file3);//由于file3文件夹不存在，file2对应的文件无法重写到file3

    System.out.println(renameTo1);
    System.out.println(renameTo2);
    }
/*
true
false
```



#### 判断功能

public boolean `isDirectory()`：判断是否是文件目录

public boolean `isFile()` ：判断是否是文件

public boolean `exists()` ：判断是否存在

public boolean `canRead()` ：判断是否可读

public boolean `canWrite()` ：判断是否可写

public boolean `isHidden()` ：判断是否隐藏



#### 创建功能

public boolean `createNewFile()` ：创建文件。若文件存在，则不创建，返回false

public boolean `mkdir()` ：创建文件目录。

- 如果此文件目录存在，就不创建了。
- 如果此文件目录的上层目录不存在，也不创建。 

public boolean `mkdirs()` ：创建文件目录。

- 如果上层文件目录不存在，一并创建

注意事项：如果创建文件或者文件目录没有写盘符路径，那么，默认在项目路径下。



#### 删除功能

public boolean `delete()`：删除文件或者文件夹

删除注意事项：Java中的删除不走**回收站**。 要删除一个文件目录，请注意该文件目录内不能包含文件或者文件目录

```java
File dir1 = new File("D:/IOTest/dir1");
if (!dir1.exists()) { // 如果D:/IOTest/dir1不存在，就创建为目录
		dir1.mkdir();
}
// 创建以dir1为父目录,名为"dir2"的File对象
File dir2 = new File(dir1, "dir2");
if (!dir2.exists()) { // 如果还不存在，就创建为目录
	dir2.mkdirs();
}
File dir4 = new File(dir1, "dir3/dir4");
if (!dir4.exists()) {
	dir4.mkdirs();
}
// 创建以dir2为父目录,名为"test.txt"的File对象
File file = new File(dir2, "test.txt");
if (!file.exists()) { // 如果还不存在，就创建为文件
	file.createNewFile();
}
```



## FileFilter

`FileFilter` 过滤器是一个函数式接口，用于抽象路径名的过滤器。使用时候要创建一个接口的实现类。**（通常使用匿名内部类或者lambda表达式来完成，因为一般该接口只适用于本次的过滤需求，没有广泛的适用性。）**

```java
@FunctionalInterface
public interface FileFilter {
    boolean accept(File pathname);
}
```

`accept`：测试指定抽象路径名是否应该包含在某个路径名列表中。**返回`false`表示过滤该文件，`ture`则不过滤**



**File 类使用过滤器的方法**

根据指定文件过滤器获得当前文件夹下的过滤后的所有文件的`File`对象数组

```java
public File[] listFiles(FileFilter filter)
```

返回抽象路径名数组，这些路径名表示**此抽象路径名表示的目录中满足指定过滤器的文件和目录**



**使用步骤与示例**

1.	定义一个类实现`FileFilter`接口**（通常使用匿名内部类或者lambda表达式来完成）**
2.	重写`accept`方法,满足条件的返回`true`,不满足条件的返回`false`
3.	创建`FileFilter`接口的实现类对象
4.	`file.listFiles()`方法参数中传入过滤器

使用文件过滤器示例:

```java
import java.io.File;
import java.io.FileFilter;

/*
 * 需求：只输出文件夹中所有的.pptx文件
 */
public class MoonZero {
	public static void main(String[] args) {
		// 创建文件夹对象
		File file = new File("E:\\temp");
		// 调用读取所有文件的方法
		printAllFile(file);
	}

	// 创建读取当前文件夹下的的有文件递归方法
	public static void printAllFile(File file) {
		// 创建FileFilter接口的实现类对象
		FileFilterDemo ff = new FileFilterDemo();
		// 使用File[] listFiles(FileFilter filter)方法，获取过滤后的File对象数组
		File[] list = file.listFiles(ff);
		// 利用增强for遍历File对象数组
		for (File f : list) {
			// 再判断是否是文件，如果是文件，直接输出（递归的出口）
			if (f.isFile()) {
				// 直接输出对像是绝对路径，是因为File重写了toString方法
				System.out.println(f);
			} else {
				// 不是文件，则就是文件夹，就进行递归，继续执行。
				printAllFile(f);
			}
		}
	}
}

// 定义一个类实现FileFilter接口
class FileFilterDemo implements FileFilter {
	// 重写过滤器 FileFilter的accept抽象方法，
	// 根据需求定义过滤的条件
	@Override
	public boolean accept(File pathname) {
		// 要先判断传入的File对象是文件还是文件夹
		// 如果是文件夹则直接不过滤，如果是文件，则进行判断过滤。
		if (pathname.isDirectory()) {
			return true;
		} else {
			return pathname.getName().endsWith(".pptx");
		}
		// 另一种简单写法
		// return (pathname.isDirectory()) || (pathname.getName().endsWith(".pptx"));
	}
}
```

使用文件过滤器示例2:(使用匿名内部类)

```java
import java.io.File;
import java.io.FileFilter;

/*
 * 需求：只输出文件夹中所有的.pptx文件
 */
public class MoonZero {
	public static void main(String[] args) {
		// 创建文件夹对象
		File file = new File("E:\\temp");
		// 调用读取所有文件的方法
		printAllFile(file);
	}

	// 创建读取当前文件夹下的的有文件递归方法
	public static void printAllFile(File file) {
		// 使用File[] listFiles(FileFilter filter)方法，获取过滤后的File对象数组
		File[] list = file.listFiles(new FileFilter() {
			// 创建FileFilter接口的匿名内部类，直接重写accept抽象方法
			@Override
			public boolean accept(File pathname) {
				// 要先判断传入的File对象是文件还是文件夹
				// 如果是文件夹则直接不过滤，如果是文件，则进行判断过滤。
				return (pathname.isDirectory()) || (pathname.getName().endsWith(".pptx"));
			}
		});
		// 利用增强for遍历File对象数组
		for (File f : list) {
			// 再判断是否是文件，如果是文件，直接输出（递归的出口）
			if (f.isFile()) {
				// 直接输出对像是绝对路径，是因为File重写了toString方法
				System.out.println(f);
			} else {
				// 不是文件，则就是文件夹，就进行递归，继续执行。
				printAllFile(f);
			}
		}
	}
}
```



## IO流原理及流的分类

### IO原理

I/O是Input/Output的缩写， I/O技术用于**处理设备之间的数据传输**。如读/写文件，网络通讯等。

Java程序中，对于数据的输入/输出操作以**“流**(stream)” 的方式进行。java.io包下提供了各种“流”类和接口，用以获取不同种类的数据，并通过**标准的方法**输入或输出数据。

- 输入input**：**读取外部数据（磁盘、光盘等存储设备的数据）到程序（内存）中
- 输出output：将程序（内存）数据输出到磁盘、光盘等存储设备中



### 流的分类

按操作**数据单位**不同分为：**字节流**(8 bit)，**字符流**(16 bit)

按数据流的**流向**不同分为：**输入流，输出流**

按流的**角色**的不同分为：**节点流，处理流**

| (抽象基类) | 字节流       | 字符流 |
| ---------- | ------------ | ------ |
| 输入流     | InputStream  | Reader |
| 输出流     | OutputStream | Writer |

Java的IO流共涉及40多个类，实际上非常规则，都是从上表4个抽象基类派生的。由这四个类派生出来的子类名称都是以其**父类名作为子类名后缀**  

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220204083928352-166529427007960.png" alt="image-20220204083928352" style="zoom:67%;" />



### 节点流和处理流  

**节点流**：直接从数据源或目的地读写数据  

![image-20220204084200238](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220204084200238-166529427007958.png)



**处理流**：不直接连接到数据源或目的地，而是“连接” 在已存在的流（节点流或处理流）之上，通过对数据的处理为程序提供更为强大的读写功能。  

![image-20220204084223910](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220204084223910-166529427007959.png)



## IO 流体系

![image-20220204084041531](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220204084041531-166529427007962.png)



### InputStream & Reader  

InputStream 和 Reader 是所有输入流的基类。

InputStream典型实现：**FileInputStream**

- int `read()`
- int `read(byte[] b)`
- int `read(byte[] b, int off, int len)`

Reader典型实现： **FileReader**

- int `read()`
- int `read(char [] c)`
- int `read(char [] c, int off, int len)`

程序中打开的文件 IO 资源不属于内存里的资源，垃圾回收机制无法回收该资源，所以应该**显式关闭文件 IO 资源**。

FileInputStream 从文件系统中的某个文件中获得输入字节，用于读取非文本数据之类的原始字节流。

要读取字符流，需要使用 FileReader  



#### InputStream

int `read()`

- 从输入流中读取数据的下一个字节
- 返回 0 到 255 范围内的 int 字节值
- 如果因为已经到达流末尾而没有可用的字节， 则返回值 -1

int `read(byte[] b)`

- 每次将输入流中将**最多 b.length 个字节**的数据读入一个 byte 数组中
- 后一次读入会将上一次读入数组的内容覆盖，如果读入字节的数量小于b.length，则只能覆盖部分
- 如果因为已经到达流末尾而没有可用的字节， 则返回值 -1
- 否则**以整数形式返回本次实际读取的字节数**

int `read(byte[] b, int off,int len)`

- 将输入流中**最多 len 个数据字节读入 byte 数组**
- **从off处开始存储， 最多读len个字节** 
- 以整数形式返回实际读取的字节数。 
- 如果因为流位于文件末尾而没有可用的字节， 则返回值 -1

public void `close() throws IOException`

- 关闭此输入流并释放与该流关联的所有系统资源  




#### Reader

int `read()`

- **读取单个字符**
- 作为整数读取的字符， 范围在 0 到 65535 之间 (0x00-0xffff)（2个字节的Unicode码）
- 如果已到达流的末尾， 则返回 -1

int `read(char[] cbuf)`

- 将字符读入数组
- 如果已到达流的末尾， 则返回 -1
- 否则返回**本次读取的字符数**

int `read(char[] cbuf,int off,int len)`

- 将输入流中**最多 len 个数据字符读入char数组**
- **从off处开始存储， 最多读len个字符**
- 如果已到达流的末尾， 则返回 -1
- 否则返回本次读取的字符数

public void `close() throws IOException`

- 关闭此输入流并释放与该流关联的所有系统资源  




### OutputStream & Writer 

OutputStream 和 Writer 也非常相似：

- void `write(int b/int c)`;

- void `write(byte[] b/char[] cbuf)`;

- void `write(byte[] b/char[] buff, int off, int len)`;

- void `flush()`;

- void `close()`; 需要先刷新，再关闭此流


因为字符流直接以字符作为操作单位，所以 Writer 可以用字符串来替换字符数组，即以 String 对象作为参数

- void `write(String str)`;

- void `write(String str, int off, int len)`;


FileOutputStream 从文件系统中的某个文件中获得输出字节，用于写出非文本数据之类的原始**字节流**

要写出字符流， 需要使用 FileWriter  



#### OutputStream

void `write(int b)`

- 将指定的字节写入此输出流
- 向输出流写入一个字节。 要写入的字节是参数 b 的八个低位。 b 的 24 个高位将被忽略。 即写入0~255范围的。

void `write(byte[] b)`

- 将 `b.length` 个字节从指定的 byte 数组写入此输出流
- 应该与调用 write(b, 0, b.length) 的效果完全相同。

void `write(byte[] b,int off,int len)`

- 将指定 byte 数组中从偏移量 off 开始的 len 个字节写入此输出流。


public void `flush()throws IOException`

- 刷新此输出流并强制写出所有缓冲的输出字节， 调用此方法指示应将这些字节立即写入它们预期的目标。


public void `close() throws IOException`

- 关闭此输出流并释放与该流关联的所有系统资源  




#### Writer

void `write(int c)`

- 写入单个字符
- 要写入的字符包含在给定整数值的 16 个低位中，即写入0 到 65535 之间的Unicode码

void `write(char[] cbuf)`

- 写入字符数组。


void `write(char[] cbuf,int off,int len)`

- 写入字符数组的某一部分
- 从off开始， 写入len个字符

void `write(String str)`

- 写入字符串


void `write(String str,int off,int len)`

- 写入字符串的某一部分


void `flush()`

- 刷新该流的缓冲， 则立即将它们写入预期目标


public void `close() throws IOException`

- 关闭此输出流并释放与该流关联的所有系统资源




## 节点流

### 读取文件

```java
//将moudle下的test.txt文件内容读入到程序中，并输出到控制台
@Test
public void test1()  {
    FileReader fr=null;
    try {
        //1.实例化File类对象，指明要操作的文件
        File file = new File("test.txt");
        //2.提供具体的流
        fr = new FileReader(file);
        
        //3.数据的读入
        //方式1
        int data = fr.read();
        while (data != -1) {
            System.out.print((char) data);
            data = fr.read();
        }

        //方式2
        char[] cbuf=new char[5];
        int len;
        while ((len=fr.read(cbuf))!=-1) {
            //错误的写法
            //for (int i = 0; i <cbuf.length;i++){
            //正确的写法
            for (int i = 0; i <len;i++){
                System.out.println(cbuf[i]);
            }
        }


    }catch(IOException e){
        e.printStackTrace();
    }finally {
        //4.流的关闭
        try {
            fr.close();
        }catch (IOException e){
            e.printStackTrace();
        }
    }
}
```

为了保证流资源一定可以关闭，故要使用try-catch-finally

### 写入文件

```java
//从内存中写出数据到硬盘中
/*
1.输出操作对应的File可以不存在，不会报异常
2.File对应的硬盘中的文件如果不存在，在输出的过程中会自动创建
  File对应的硬盘中的文件如果存在
    若构造器是FileWriter(file,false)/FileWriter(file)：对原有文件进行覆盖
    若构造器是FileWriter(file,true)：不会对原有文件覆盖，而是在原有内容进行追加
 */
@Test
public void test2() throws IOException {
    //1.提供File类的对象，指明写出到的文件
    File file=new File("test1.txt");
    //2.提供具体的流
    FileWriter fw=new FileWriter(file);
    //3.数据的写出
    fw.write("I have a dream!\n");
    fw.write("You need to have a dream!".toCharArray());
    //4.流的关闭
    fw.close();
}
```



### 注意点

- 定义文件路径时，注意：可以用“/”或者“\\”。
- 在写入一个文件时，如果使用构造器FileOutputStream(file)，则目录下有同名文件将被覆盖。
- 如果使用构造器FileOutputStream(file,true)，则目录下的同名文件不会被覆盖，在文件内容末尾追加内容。
- 在读取文件时，必须保证该文件已存在，否则报异常。
- **字节流操作字节，比如： .mp3， .avi， .rmvb， mp4， .jpg， .doc， .ppt**
- **字符流操作字符，只能操作普通文本文件**。 最常见的文本文件： .txt， .java， .c， .cpp 等语言的源代码。尤其注意.doc,excel,ppt这些不是文本文件。  



### 文件内容传输

```java
@Test
public void test3()  {
    FileReader fr=null;
    FileWriter fw=null;
    try {
        //1.实例化File类对象，指明读入和写出的文件
        File srcFile = new File("test.txt");
        File destFile = new File("test1.txt");

        //2.创建输入、输出流的对象
        fr = new FileReader(srcFile);
        fw = new FileWriter(destFile);

        //3.数据的读入和写出操作
        char[] cbuf=new char[5];
        int len;//记录每次读入到cbuf数组中的字符的个数
        while ((len=fr.read(cbuf))!=-1) {
            //每次写出len个字符
            fw.write(cbuf,0,len);
        }
    }catch(IOException e){
        e.printStackTrace();
    }finally {
        //4.流的关闭
        try {
            fw.close();
            fr.close();
        }catch (IOException e){
            e.printStackTrace();
        }
    }
}
```



## 处理流

### 缓冲流  

为了**提高数据读写的速度**， Java API提供了带缓冲功能的流类，在使用这些流类时，会创建一个内部缓冲区数组，缺省使用8192个字节(8Kb)的缓冲区  

![image-20220204101918776](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220204101918776-166529427007961.png)

缓冲流要“套接”在相应的节点流之上，根据数据操作单位可以把缓冲流分为：

- BufferedInputStream 和 BufferedOutputStream
- BufferedReader 和 BufferedWriter  

当**读取数据时，数据按块读入缓冲区，其后的读操作则直接访问缓冲区**

```java
@Test
public void test4() {
    FileReader fr=null;
    FileWriter fw=null;
    BufferedReader bis=null;
    BufferedWriter bos=null;
    try {
        //1.造文件
        File srcFile = new File("test.txt");
        File destFile = new File("test1.txt");

        //2.造节点流
        fr = new FileReader(srcFile);
        fw = new FileWriter(destFile);

        //3.造缓冲流
        bis=new BufferedReader(fr);
        bos=new BufferedWriter(fw);

        //4.复制的细节：读取、写入
        char[] cbuf = new char[5];
        int len;//记录每次读入到cbuf数组中的字符的个数
        while ((len = bis.read(cbuf)) != -1) {
            //每次写出len个字符
            bos.write(cbuf, 0, len);
        }
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        //4.流的关闭：先关闭外层的流，再关闭内层的流
        try {
            bos.close();
            bis.close();

            fw.close();
            fr.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

当使用BufferedInputStream读取字节文件时， BufferedInputStream会一次性从文件中读取8192个(8Kb)， 存在缓冲区中， 直到缓冲区装满了， 才重新从文件中读取下一个8192个字节数组。

向流中写入字节时， 不会直接写到文件， 先写到缓冲区中直到缓冲区写满，BufferedOutputStream才会把缓冲区中的数据一次性写到文件里。使用方法flush()可以强制将缓冲区的内容全部写入输出流

关闭流的顺序和打开流的顺序相反。只要关闭最外层流即可， 关闭最外层流也会相应关闭内层节点流

flush()方法的使用：手动将buffer中内容写入文件

如果是带缓冲区的流对象的close()方法， 不但会关闭流， 还会在关闭流之前刷新缓冲区， 关闭后不能再写出  



### 转换流  

转换流提供了在字节流和字符流之间的转换。Java API提供了两个转换流：

- InputStreamReader：将InputStream转换为Reader
- OutputStreamWriter：将Writer转换为OutputStream

字节流中的数据都是字符时，转成字符流操作更高效。

很多时候我们**使用转换流来处理文件乱码问题，实现编码和解码的功能**。  

#### InputStreamReader

将字节的输入流按**指定字符集（取决于文件保存格式）**转换为字符的输入流，需要和InputStream“套接”。

构造器

```java
public InputStreamReader(InputStream in)
public InputSreamReader(InputStream in,String charsetName)
```

如：

```java
Reader isr = new InputStreamReader(System.in,”gbk”);  
```

#### OutputStreamWriter

将字符的输出流按指定字符集转换为字节的输出流，需要和OutputStream“套接”。

构造器

```java
public OutputStreamWriter(OutputStream out)
public OutputSreamWriter(OutputStream out,String charsetName) 
```

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220204142000518-166529427007963.png" alt="image-20220204142000518" style="zoom:50%;" />

#### 补充：字符编码  

编码表的由来

计算机只能识别二进制数据，早期由来是电信号。为了方便应用计算机，让它可以识别各个国家的文字。就将各个国家的文字用数字来表示，并一一对应，形成一张表。这就是编码表。

常见的编码表

- ASCII： 美国标准信息交换码。用一个字节的7位可以表示。
- ISO8859-1： 拉丁码表。欧洲码表用一个字节的8位表示。
- GB2312： 中国的中文编码表。最多两个字节编码所有字符
- GBK： 中国的中文编码表升级，融合了更多的中文文字符号。最多两个字节编码
- Unicode： 国际标准码， 融合了目前人类使用的所有字符。为每个字符分配唯一的字符码。所有的文字都用两个字节来表示。
- UTF-8： 变长的编码方式，可用1-4个字节来表示一个字符。  

在Unicode出现之前，所有的字符集都是和具体编码方案绑定在一起的（即字
符集≈编码方式） ，都是直接将字符和最终字节流绑定死了。GBK等双字节编码方式， 用最高位是1或0表示两个字节和一个字节  



### 标准输入、输出流

System.in和System.out分别代表了系统标准的输入和输出设备。

默认输入设备是： 键盘， 输出设备是：显示器

System.in的类型是InputStream

System.out的类型是PrintStream，其是OutputStream的子类FilterOutputStream 的子类

```java
public class OtherStream {
    public static void main(String[] args) {
        BufferedReader br= null;
        try {
            InputStreamReader isr=new InputStreamReader(System.in);
            br = new BufferedReader(isr);
            while (true){
                System.out.println("输入字符串");
                String data=br.readLine();
                if("e".equalsIgnoreCase(data)||"exit".equalsIgnoreCase(data)){
                    System.out.println("程序结束");
                    break;
                }
                String upperCase=data.toUpperCase();
                System.out.println(upperCase);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                br.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

重定向：通过System类的setIn， setOut方法对默认设备进行改变。

```java
public static void setIn(InputStream in)
public static void setOut(PrintStream out)  
```



### 打印流

实现将**基本数据类型的数据格式转化为字符串输出**

- 打印流： PrintStream和PrintWriter
- 提供了一系列重载的print()和println()方法，用于多种数据类型的输出
- PrintStream和PrintWriter的输出不会抛出IOException异常
- PrintStream和PrintWriter有自动flush功能
- PrintStream 打印的所有字符都使用平台的默认字符编码转换为字节。在需要写入字符而不是写入字节的情况下，应该使用 PrintWriter 类。
- System.out返回的是PrintStream的实例  

```java
PrintStream ps = null;
try {
    FileOutputStream fos = new FileOutputStream(new File("D:\\IO\\text.txt"));
    // 创建打印输出流,设置为自动刷新模式(写入换行符或字节 '\n' 时都会刷新输出缓冲区)
    ps = new PrintStream(fos, true);
    if (ps != null) {
        // 把标准输出流(控制台输出)改成文件
    	System.setOut(ps);
    }
    for (int i = 0; i <= 255; i++) { // 输出ASCII字符
    	System.out.print((char) i);
    	if (i % 50 == 0) { // 每50个数据一行
    	System.out.println(); // 换行
    	} 
    }
} catch (FileNotFoundException e) {
	e.printStackTrace();
} finally {
	if (ps != null) {
		ps.close();
	} 
}
```



### 数据流

为了方便地**操作Java语言的基本数据类型和String的数据**，可以使用数据流。

数据流有两个类： (用于读取和写出基本数据类型、 String类的数据）

DataInputStream 和 DataOutputStream，分别“套接”在 InputStream 和 OutputStream 子类的流上

DataInputStream中的方法

- boolean `readBoolean() `
- byte `readByte()`
- char `readChar()` 
- float `readFloat()`
- double `readDouble()` 
- short `readShort()`
- long `readLong()` 
- int `readInt()`
- String `readUTF()`
- void `readFully(byte[] b)`

DataOutputStream中的方法：将上述的方法的read改为相应的write即可。

```java
DataOutputStream dos = null;
try { // 创建连接到指定文件的数据输出流对象
    dos = new DataOutputStream(new FileOutputStream("destData.dat"));
    dos.writeUTF("我爱北京天安门"); // 写UTF字符串
    dos.writeBoolean(false); // 写入布尔值
    dos.writeLong(1234567890L); // 写入长整数
    System.out.println("写文件成功!");
} catch (IOException e) {
	e.printStackTrace();
} finally { // 关闭流对象
    try {
    	if (dos != null) {
    // 关闭过滤流时,会自动关闭它包装的底层节点流
    		dos.close();
		}
	} catch (IOException e) {
		e.printStackTrace();
	}
}

DataInputStream dis = null;
try {
    dis = new DataInputStream(new FileInputStream("destData.dat"));
    String info = dis.readUTF();
    boolean flag = dis.readBoolean();
    long time = dis.readLong();
    System.out.println(info);
    System.out.println(flag);
    System.out.println(time);
} catch (Exception e) {
	e.printStackTrace();
} finally {
	if (dis != null) {
		try {
			dis.close();
		} catch (IOException e) {
			e.printStackTrace();
		} 
    } 
}
```



### 对象流

ObjectInputStream和OjbectOutputSteam：用于存储和读取基本数据类型数据或对象的处理流。它的强大之处就是**可以把Java中的对象写入到数据源中，也能把对象从数据源中还原回来**。

- 序列化： 用ObjectOutputStream类保存基本类型数据或对象的机制
- 反序列化： 用ObjectInputStream类读取基本类型数据或对象的机制

ObjectOutputStream和ObjectInputStream不能序列化static和transient修饰的成员变量  

```java
public class ObjectStream {
    @Test
    public void test(){
        /*序列化过程
        需要使用ObjectOutputStream
         */
        ObjectOutputStream oos= null;
        try {
            oos = new ObjectOutputStream(new FileOutputStream("test.txt"));
            oos.writeObject(new String("测试"));
            oos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                oos.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    @Test
    public void test2(){
        /*反序列化过程
        需要使用ObjectInputStream
         */
        ObjectInputStream ois= null;
        try {
            ois = new ObjectInputStream(new FileInputStream("test.txt"));
            Object obj=ois.readObject();
            String str=(String) obj;
            System.out.println(str);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            try {
                ois.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```



### 对象的序列化

对象序列化机制允许**把内存中的Java对象转换成平台无关的二进制流，从而允许把这种二进制流持久地保存在磁盘上，或通过网络将这种二进制流传输到另一个网络节点。当其它程序获取了这种二进制流，就可以恢复成原来的Java对象**

序列化的好处在于可**将任何实现了Serializable接口的对象转化为字节数据**，使其在保存和传输时可被还原。序列化是 RMI（Remote Method Invoke – 远程方法调用）过程的参数和返回值都必须实现的机制，而 RMI 是 JavaEE 的基础。因此序列化机制是JavaEE 平台的基础

**如果需要让某个对象支持序列化机制**，则必须让对象所属的类及其属性是可序列化的，为了让某个类是可序列化的，**该类必须实现如下两个接口之一**。否则，会抛出NotSerializableException异常

- Serializable
- Externalizable  

凡是实现Serializable接口的类都有一个表示序列化版本标识符的静态变量：

```java
private static final long serialVersionUID=46374637829L;//值可以随便取
```

serialVersionUID用来表明类的不同版本间的兼容性。 简言之，其目的是以序列化对象进行版本控制，有关各版本反序列化时是否兼容。如果类没有显示定义这个静态常量，它的值是Java运行时环境根据类的内部细节自动生成的。 若**类的实例变量做了修改， serialVersionUID 可能发生变化**。 故**建议显式声明**。

简单来说， Java的序列化机制是通过在运行时判断类的serialVersionUID来验证版本一致性的。在进行反序列化时， JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进行比较，**如果相同就认为是一致的，可以进行反序列化**，否则就会出现序列化版本不一致的异常。 (InvalidCastException)  

使用对象流序列化对象

若某个类实现了 Serializable 接口，该类的对象就是可序列化的：

- 创建一个 ObjectOutputStream
- 调用 ObjectOutputStream 对象的 writeObject(对象) 方法输出可序列化对象
- 注意**写出一次，操作flush()一次**

反序列化

- 创建一个 ObjectInputStream
- 调用 readObject() 方法读取流中的对象

强调： **如果某个类的属性不是基本数据类型或 String 类型，而是另一个引用类型，那么这个引用类型必须是可序列化的，否则拥有该类型的Field 的类也不能序列化**  

**谈谈你对java.io.Serializable接口的理解，我们知道它用于序列化，是空方法接口，还有其它认识吗？**  

实现了Serializable接口的对象，可将它们转换成一系列字节，并可在以后完全恢复回原来的样子。 这一过程亦可通过网络进行。这意味着序列化机制能自动补偿操作系统间的差异。 换句话说，可以先在Windows机器上创建一个对象，对其序列化，然后通过网络发给一台Unix机器，然后在那里准确无误地重新“装配”。不必关心数据在不同机器上如何表示，也不必关心字节的顺序或者其他任何细节。

由于大部分作为参数的类如String、 Integer等都实现了java.io.Serializable的接口，也可以利用多态的性质，作为参数使接口更灵活。  



## 随机存取文件流  

RandomAccessFile 类

RandomAccessFile 声明在java.io包下，但直接继承于java.lang.Object类。且它实现了DataInput、 DataOutput这两个接口，也就意味着这个类**既可以读也可以写**。

RandomAccessFile 类支持 “随机访问” 的方式，程序可以直接跳到文件的任意地方来读、写文件

- 支持只访问文件的部分内容
- 可以向已存在的文件后追加内容

RandomAccessFile 对象包含一个记录指针，用以标示当前读写处的位置。RandomAccessFile 类对象可以自由移动记录指针：

- long `getFilePointer()`： 获取文件记录指针的当前位置
- void `seek(long pos)`： 将文件记录指针定位到 pos 位置  

构造器

```java
public RandomAccessFile(File file, String mode)
public RandomAccessFile(String name, String mode)
```

创建 RandomAccessFile 类实例需要指定一个 mode 参数，该参数指定 RandomAccessFile 的访问模式：

- r: 以只读方式打开
- rw：打开以便读取和写入
- rwd:打开以便读取和写入；同步文件内容的更新
- rws:打开以便读取和写入； 同步文件内容和元数据的更新

如果模式为只读r。则不会创建文件，而是会去读取一个已经存在的文件，如果读取的文件不存在则会出现异常。 如果模式为rw读写。如果文件不存在则会去创建文件，如果存在则不会创建。  

流是用来处理数据的。处理数据时，一定要先明确数据源，与数据目的地

- 数据源可以是文件，可以是键盘。
- 数据目的地可以是文件、显示器或者其他设备。
- 流只是在帮助数据进行传输,并对传输的数据进行处理，比如过滤处理、转换处理等。  

```java
//读取文件
RandomAccessFile raf = new RandomAccessFile(“test.txt”, “rw”）;
raf.seek(5);
byte [] b = new byte[1024];
int off = 0;
int len = 5;
raf.read(b, off, len);
String str = new String(b, 0, len);
System.out.println(str);
raf.close();

//写入文件
RandomAccessFile raf = new RandomAccessFile("test.txt", "rw");
raf.seek(5);
//先读出来
String temp = raf.readLine();
raf.seek(5);
raf.write("xyz".getBytes());
raf.write(temp.getBytes());
raf.close();

RandomAccessFile raf1 = new RandomAccessFile("hello.txt", "rw");
raf1.seek(5);
//方式一：
//StringBuilder info = new StringBuilder((int) file.length());
//byte[] buffer = new byte[10];
//int len;
//while((len = raf1.read(buffer)) != -1){
////info += new String(buffer,0,len);
//info.append(new String(buffer,0,len));
//}
//方式二：
ByteArrayOutputStream baos = new ByteArrayOutputStream();
byte[] buffer = new byte[10];
int len;
while((len = raf1.read(buffer)) != -1){
	baos.write(buffer, 0, len);
}
raf1.seek(5);
raf1.write("xyz".getBytes());
raf1.write(baos.toString().getBytes());
baos.close();
raf1.close();
```



## IO流总结（字符流和字节流）

![Java IO体系.xmind](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20210614100907212_13577-166529427007964.png)

![Java IO 分类总结.drawio](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20210614104502846_582-166529427007965.jpg)



## BIO 编程

BIO 有的称之为 basic(基本) IO，有的称之为 block(阻塞) IO，主要应用于文件 IO 和网络 IO



### BIO 之 网络IO

在 JDK1.4 之前，建立网络连接的时候只能采用 BIO，需要先在服务端启动一个ServerSocket，然后在客户端启动 Socket 来对服务端进行通信，默认情况下服务端需要对每个请求建立一个线程等待请求，而客户端发送请求后，先咨询服务端是否有线程响应，如果没有则会一直等待或者遭到拒绝，如果有的话，客户端线程会等待请求结束后才继续执行，这就是阻塞式 IO



### 基本用法示例（基于 TCP）

- 编写TCP服务端

```java
package com.moon.system.testmodule.bio;

import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

/**
 * BIO 编程测试 - TCP服务器端程序
 */
public class TCPServer {

    public static void main(String[] args) throws IOException {
        // 1. 创建ServerSocket对象，设置端口号为9999
        ServerSocket serverSocket = new ServerSocket(9999);

        while (true) {
            // 2. 监听客户端
            System.out.println("serverSocket.accept()执行前");
            Socket socket = serverSocket.accept();  // 阻塞，等客户端启动
            System.out.println("serverSocket.accept()执行完");

            // 3. 从连接中取出输入流来接收消息
            InputStream inputStream = socket.getInputStream();  // 阻塞，等待接收客户端发出的消息
            byte[] bytes = new byte[1024];
            // 读取数据
            inputStream.read(bytes);

            String clientIP = socket.getInetAddress().getHostAddress();
            System.out.println(String.format("%s说：%s", clientIP, new String(bytes).trim()));

            // 4. 从连接中取出输出流并回话
            OutputStream outputStream = socket.getOutputStream();
            outputStream.write("TCPServer收到消息".getBytes());

            //  5. 关闭socket
            socket.close();
        }
    }
}
```

- 上述代码编写了一个服务器端程序，绑定端口号 9999，accept 方法用来监听客户端连接，如果没有客户端连接，就一直等待，程序会阻塞在`serverSocket.accept()`方法

```java
package com.moon.system.testmodule.bio;

import java.io.InputStream;
import java.io.OutputStream;
import java.net.Socket;
import java.util.Scanner;

/**
 * BIO 编程测试 - TCP客户端程序
 */
public class TCPClient {

    public static void main(String[] args) throws Exception {
        while (true) {
            // 1.创建Socket对象，连接9999端口
            Socket socket = new Socket("127.0.0.1", 9999);

            // 2.从连接中取出输出流并发消息
            OutputStream outputStream = socket.getOutputStream();
            System.out.println("请输入:");
            Scanner sc = new Scanner(System.in);
            String msg = sc.nextLine();
            outputStream.write(msg.getBytes());

            // 3.从连接中取出输入流并接收回话
            InputStream is = socket.getInputStream(); // 阻塞，一直等待服务端的响应
            byte[] bytes = new byte[20];
            is.read(bytes);
            System.out.println("TCPServer回复：" + new String(bytes).trim());

            // 4.关闭
            socket.close();
        }
    }
}
```

上述代码编写了一个客户端程序，通过 9999 端口连接服务器端，getInputStream 方法用来等待服务器端返回数据，如果没有返回，就一直等待，程序会阻塞在`socket.getInputStream()`方法



## NIO 编程

### 概述

java.nio 全称 java non-blocking IO，是指 JDK 提供的新 API。从 JDK1.4 开始，Java 提供了一系列改进的输入/输出的新特性，被统称为 NIO(即 New IO)。新增了许多用于处理输入输出的类，这些类都被放在 java.nio 包及子包下，并且对原 java.io 包中的很多类进行改写，新增了满足 NIO 的功能

![NIO包结构](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191002182312547_11612-166529427007967.png)

NIO 和 BIO 有着相同的目的和作用，但是它们的实现方式完全不同，BIO 以流的方式处理数据，而 NIO 以块的方式处理数据，块 I/O 的效率比流 I/O 高很多。另外，NIO 是非阻塞式的，这一点跟 BIO 也很不相同，使用它可以提供非阻塞式的高伸缩性网络

**NIO 主要有三大核心部分：Channel(通道)，Buffer(缓冲区), Selector(选择器)**。传统的 BIO基于字节流和字符流进行操作，而 NIO 基于 Channel(通道)和 Buffer(缓冲区)进行操作，数据总是从通道读取到缓冲区中，或者从缓冲区写入到通道中。Selector(选择区)用于监听多个通道的事件（比如：连接请求，数据到达等），因此使用单个线程就可以监听多个客户端通道



### 文件 IO

#### 缓冲区（Buffer）概述

缓冲区（Buffer）：实际上是一个容器，是一个特殊的数组，缓冲区对象内置了一些机制，能够跟踪和记录缓冲区的状态变化情况。Channel 提供从文件、网络读取数据的渠道，但是读取或写入的数据都必须经由 Buffer，如下图所示

![](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191002184623913_10099-166529427007966.png)



#### 缓冲区（Buffer）核心 API

在 NIO 中，`Buffer` 是一个顶层父类，它是一个抽象类，对于 Java 中的基本数据类型，都有一个 `Buffer` 类型与之相对应，常用的 `Buffer` 子类有

| Buffer 子类  | 作用类型               |
| ------------ | ---------------------- |
| ByteBuffer   | 存储字节数据到缓冲区   |
| ShortBuffer  | 存储字符串数据到缓冲区 |
| CharBuffer   | 存储字符数据到缓冲区   |
| IntBuffer    | 存储整数数据到缓冲区   |
| LongBuffer   | 存储长整型数据到缓冲区 |
| DoubleBuffer | 存储小数到缓冲区       |
| FloatBuffer  | 存储小数到缓冲区       |

##### ByteBuffer 常用方法

最常用的自然是ByteBuffer 类（二进制数据），该类的主要方法如下所示

- 存储字节数据到缓冲区

```java
public abstract ByteBuffer put(byte[] b);
```

- 从缓冲区获得字节数据

```java
public abstract byte[] get();
```

- 把缓冲区数据转换成字节数组

```java
public final byte[] array();
```

- 设置缓冲区的初始容量

```java
public static ByteBuffer allocate(int capacity);
```

- 把一个现成的数组放到缓冲区中使用

```java
public static ByteBuffer wrap(byte[] array);
```

- 翻转缓冲区，重置位置到初始位置

```java
public final Buffer flip();
```



#### 通道（Channel）概述

通道（Channel）：类似于 BIO 中的 stream。例如 `FileInputStream` 对象，用来建立到目标（文件，网络套接字，硬件设备等）的一个连接。

需要注意：**BIO 中的 stream 是单向的**，例如 `FileInputStream` 对象只能进行读取数据的操作。而 **NIO 中的通道(Channel)是双向的**，既可以用来进行读操作，也可以用来进行写操作。

常用的 `Channel` 实现类有：

| Channel 实现类      | 作用                |
| ------------------- | ------------------- |
| FileChannel         | 用于文件的数据读写  |
| DatagramChannel     | 用于 UDP 的数据读写 |
| ServerSocketChannel | 用于 TCP 的数据读写 |
| SocketChannel       | 用于 TCP 的数据读写 |

![Channel接口实现关系图](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191002190510596_5957-166529427007968.png)

##### FileChannel 类常用方法

该类主要用来对本地文件进行 IO 操作，主要方法如下

- 从通道读取数据并放到缓冲区中

```java
public int read(ByteBuffer dst);
```

- 把缓冲区的数据写到通道中

```java
public int write(ByteBuffer src);
```

- 从目标通道中复制数据到当前通道

```java
public long transferFrom(ReadableByteChannel src, long position, long count);
```

- 把数据从当前通道复制给目标通道

```java
public long transferTo(long position, long count, WritableByteChannel target);
```



#### 文件 NIO 示例

测试使用NIO进行本地文件的读、写和复制操作，和BIO进行对比

##### 往本地文件中写数据

```java
/* 往本地文件中写数据 */
@Test
public void testWrite() throws Exception {
    // 1. 创建输出流
    FileOutputStream fileOutputStream = new FileOutputStream("E:\\00-Downloads\\moon.txt");
    // 2. 从流中得到一个通道
    FileChannel fileChannel = fileOutputStream.getChannel();
    // 3. 提供一个缓冲区
    ByteBuffer buffer = ByteBuffer.allocate(1024);
    // 4. 往缓冲区中存入数据
    String str = "hello,nio";
    buffer.put(str.getBytes());
    // 5. 翻转缓冲区
    buffer.flip();
    // 6. 把缓冲区写到通道中
    fileChannel.write(buffer);
    // 7. 关闭
    fileOutputStream.close();
}
```

> NIO 中的通道是从输出流对象里通过 `getChannel` 方法获取到的，该通道是双向的，既可以读，又可以写。在往通道里写数据之前，必须通过 put 方法把数据存到 `ByteBuffer` 中，然后通过通道的 `write` 方法写数据。在 `write` 之前，需要调用 `flip` 方法翻转缓冲区，把内部重置到初始位置，这样在接下来写数据时才能把所有数据写到通道里



##### 从本地文件中读数据

```java
/* 从本地文件中读取数据 */
@Test
public void test2() throws Exception {
    File file = new File("E:\\00-Downloads\\moon.txt");
    // 1. 创建输入流
    FileInputStream fileInputStream = new FileInputStream(file);
    // 2. 得到一个通道
    FileChannel fileChannel = fileInputStream.getChannel();
    // 3. 准备一个缓冲区
    ByteBuffer buffer = ByteBuffer.allocate((int) file.length());
    // 4. 从通道里读取数据并存到缓冲区中
    fileChannel.read(buffer);
    System.out.println(new String(buffer.array()));
    // 5. 关闭
    fileInputStream.close();
}
```

> 上面示例从输入流中获得一个通道，然后提供 ByteBuffer 缓冲区，该缓冲区的初始容量和文件的大小一样，最后通过通道的 read 方法把数据读取出来并存储到了 ByteBuffer 中



##### 复制本地文件

```java
/* 使用BIO实现文件复制 */
@Test
public void testBioCopy() throws Exception {
    // 1. 创建两个流
    FileInputStream fileInputStream = new FileInputStream("E:\\00-Downloads\\moon.txt");
    FileOutputStream fileOutputStream = new FileOutputStream("E:\\00-Downloads\\moon_copy.txt");
    // 2. 定义字节数组，使用一次读取数组方式复制文件
    byte[] bytes = new byte[1024];
    int len;
    while ((len = fileInputStream.read(bytes)) != -1) {
        fileOutputStream.write(bytes, 0, len);
    }
    // 3. 关闭资源
    fileInputStream.close();
    fileOutputStream.close();
}
```

> 上面示例是通过传统的 BIO 复制一个文件，分别通过输入流和输出流实现了文件的复制

```java
/* 使用NIO实现文件复制 */
@Test
public void testNioCopy() throws Exception {
    // 1. 创建两个流
    FileInputStream fileInputStream = new FileInputStream("E:\\00-Downloads\\moon.txt");
    FileOutputStream fileOutputStream = new FileOutputStream("E:\\00-Downloads\\moon_copy.txt");
    // 2. 得到两个通道
    FileChannel fileInChannel = fileInputStream.getChannel();
    FileChannel fileOutChannel = fileOutputStream.getChannel();
    // 3. 复制
    fileOutChannel.transferFrom(fileInChannel, 0, fileInChannel.size());
    // 4. 关闭
    fileInputStream.close();
    fileOutputStream.close();
}
```

> 上面示例分别从两个流中得到两个通道，sourceCh 负责读数据，destCh 负责写数据，然后直接调用 transferFrom 方法一步到位实现了文件复制



### 网络 IO

#### 概述

Java NIO 中的网络通道是非阻塞 IO 的实现，基于事件驱动，非常适用于服务器需要维持大量连接，但是数据交换量不大的情况，例如一些即时通信的服务等等...

在 Java 中编写 Socket 服务器，通常有以下几种模式

- 一个客户端连接用一个线程，优点：程序编写简单；缺点：如果连接非常多，分配的线程也会非常多，服务器可能会因为资源耗尽而崩溃。
- 把每一个客户端连接交给一个拥有固定数量线程的连接池，优点：程序编写相对简单，可以处理大量的连接。确定：线程的开销非常大，连接如果非常多，排队现象会比较严重。
- 使用 Java 的 NIO，用非阻塞的 IO 方式处理。这种模式可以用一个线程，处理大量的客户端连接



#### 核心 API

##### Selector(选择器)

`Selector`选择器，能够检测多个注册的通道上是否有事件发生，如果有事件发生，便获取事件然后针对每个事件进行相应的处理。这样就可以只用一个单线程去管理多个通道，也就是管理多个连接。这样使得只有在连接真正有读写事件发生时，才会调用函数来进行读写，就大大地减少了系统开销，并且不必为每个连接都创建一个线程，不用去维护多个线程，并且避免了多线程之间的上下文切换导致的开销。

![Selector类关系图](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191003102234080_15327-166529427007969.png)

常用方法如下：

- 得到一个选择器对象

```java
public static Selector open()
```

- 监控所有注册的通道，当其中有 IO 操作可以进行时，将对应的 SelectionKey 加入到内部集合中并返回，参数用来设置超时时间

```java
public int select(long timeout)
```

- 从内部集合中得到所有的 SelectionKey

```java
public Set<SelectionKey> selectedKeys()
```

- 获取所有准备就绪的网络通道

```java
public abstract Set<SelectionKey> keys();
```



##### SelectionKey(网络通道key)

`SelectionKey`，代表了 `Selector` 和网络通道的注册关系，一共四种：

- `int OP_ACCEPT`：有新的网络连接可以 accept，值为 16
- `int OP_CONNECT`：代表连接已经建立，值为 8
- `int OP_READ` 和 `int OP_WRITE`：代表了读、写操作，值为 1 和 4

该类的常用方法如下所示：

- 得到与之关联的 Selector 对象

```java
public abstract Selector selector()
```

- 得到与之关联的通道

```java
public abstract SelectableChannel channel()
```

- 得到与之关联的共享数据

```java
public final Object attachment()
```

- 设置或改变监听事件

```java
public abstract SelectionKey interestOps(int ops)
```

- 是否可以 accept

```java
public final boolean isAcceptable()
```

- 是否可以读

```java
public final boolean isReadable()
```

- 是否可以写

```java
public final boolean isWritable()
```



##### ServerSocketChannel(通道)

ServerSocketChannel，用来在服务器端监听新的客户端 Socket 连接。常用方法如下

- 得到一个 ServerSocketChannel 通道

```java
public static ServerSocketChannel open()
```

- 设置服务器端端口号

```java
public final ServerSocketChannel bind(SocketAddress local)
```

- 设置阻塞或非阻塞模式，取值 false 表示采用非阻塞模式

```java
public final SelectableChannel configureBlocking(boolean block)
```

- 接受一个连接，返回代表这个连接的通道对象

```java
public SocketChannel accept()
```

- 注册一个选择器并设置监听事件

```java
public final SelectionKey register(Selector sel, int ops)
```



##### SocketChannel(网络 IO 通道)

SocketChannel，网络 IO 通道，具体负责进行读写操作。NIO 总是把缓冲区的数据写入通道，或者把通道里的数据读到缓冲区。常用方法如下所示

- 得到一个 SocketChannel 通道

```java
public static SocketChannel open()
```

- 设置阻塞或非阻塞模式，取值 false 表示采用非阻塞模式

```java
public final SelectableChannel configureBlocking(boolean block)
```

- 连接服务器

```java
public boolean connect(SocketAddress remote)
```

- 如果上面的方法连接失败，接下来就要通过该方法完成连接操作

```java
public boolean finishConnect()
```

- 往通道里写数据

```java
public int write(ByteBuffer src)
```

- 从通道里读数据

```java
public int read(ByteBuffer dst)
```

- 注册一个选择器并设置监听事件，最后一个参数可以设置共享数据

```java
public final SelectionKey register(Selector sel, int ops, Object att)
```

- 关闭通道

```java
public final void close()
```

![网络NIO流程图](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191003110743007_5665-166529427007973.png)



#### 基础示例

需求分析：实现服务器端和客户端之间的数据通信（非阻塞）

![数据通信示例](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191004101220248_11427-166529427007971.png)

- 网络服务器端程序

```java
package com.moon.system.testmodule.nio.socket;

import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.util.Iterator;

/**
 * NIO案例 - 网络服务器端程序
 */
public class NIOServer {
    public static void main(String[] args) throws Exception {
        // 1. 得到一个ServerSocketChannel对象
        ServerSocketChannel serverSocketChannel = ServerSocketChannel.open();
        // 2. 得到一个Selector对象
        Selector selector = Selector.open();
        // 3. 绑定一个端口号
        serverSocketChannel.bind(new InetSocketAddress(9999));
        // 4. 设置非阻塞方式
        serverSocketChannel.configureBlocking(false);
        // 5. 把ServerSocketChannel对象注册给Selector对象
        serverSocketChannel.register(selector, SelectionKey.OP_ACCEPT);
        // 6. 处理逻辑
        while (true) {
            // 6.1 监控客户端
            if (selector.select(2000) == 0) {  // nio非阻塞式的优势
                System.out.println("Server:没有客户端搭理我，我就干点别的事");
                continue;
            }
            // 6.2 得到SelectionKey,判断通道里的事件
            Iterator<SelectionKey> keyIterator = selector.selectedKeys().iterator();
            while (keyIterator.hasNext()) {
                SelectionKey key = keyIterator.next();
                // 客户端连接请求事件
                if (key.isAcceptable()) {
                    System.out.println("OP_ACCEPT");
                    SocketChannel socketChannel = serverSocketChannel.accept();
                    socketChannel.configureBlocking(false);
                    // 将每个新连接的通道注册给Selector对象
                    socketChannel.register(selector, SelectionKey.OP_READ, ByteBuffer.allocate(1024));
                }

                // 读取客户端数据事件
                if (key.isReadable()) {
                    SocketChannel channel = (SocketChannel) key.channel();
                    // 获取客户端发送的附件，读取数据放到缓冲区
                    ByteBuffer buffer = (ByteBuffer) key.attachment();
                    channel.read(buffer);
                    System.out.println("客户端发来数据：" + new String(buffer.array()));
                }
                // 6.3 手动从集合中移除当前key,防止重复处理
                keyIterator.remove();
            }
        }
    }
}
```

> 上面是用 NIO 实现了一个服务器端程序，能不断接受客户端连接并读取客户端发过来的数据

- 网络客户端程序

```java
package com.moon.system.testmodule.nio.socket;

import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SocketChannel;

/**
 * NIO案例 - 网络客户端程序
 */
public class NIOClient {
    public static void main(String[] args) throws Exception {
        // 1. 得到一个网络通道
        SocketChannel socketChannel = SocketChannel.open();
        // 2. 设置非阻塞方式
        socketChannel.configureBlocking(false);
        // 3. 提供服务器端的IP地址和端口号
        InetSocketAddress address = new InetSocketAddress("127.0.0.1", 9999);
        // 4. 连接服务器端
        if (!socketChannel.connect(address)) {
            while (!socketChannel.finishConnect()) {  // nio作为非阻塞式的优势
                System.out.println("Client:连接服务器端的同时，我还可以干别的一些事情");
            }
        }
        // 5. 得到一个缓冲区并存入数据
        String msg = "hello,Server";
        ByteBuffer byteBuffer = ByteBuffer.wrap(msg.getBytes());
        // 6. 发送数据
        socketChannel.write(byteBuffer);
        System.in.read();   // 为了不让程序停止（因为客户端停止，服务端会抛出异常，暂时不想多做处理），特意设置等待输入，让程序阻塞在此处
    }
}
```

> 上面通过 NIO 实现了一个客户端程序，连接上服务器端后发送了一条数据
>
> ![NIO示例运行效果](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/20191005091833634_10778-166529427007970.png)



#### 网络聊天案例

需求：使用NIO实现多人聊天

- 使用 NIO 编写了一个聊天程序的服务器端，可以接受客户端发来的数据，并能把数据广播给所有客户端

```java
package com.moon.system.testmodule.nio.chat;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.Channel;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Iterator;

/**
 * NIO案例 - 聊天程序服务器端
 */
public class ChatServer {

    /* 定义监听通道 */
    private ServerSocketChannel listenerChannel;
    /* 选择器对象 */
    private Selector selector;
    /* 服务器端口 */
    private static final int PORT = 9999;
    /* 缓冲区字节数组大小 */
    private static final int BYTE_SIZE = 1024;

    // 创建基于JDK1.8的DateTimeFormatter（线程安全）
    private static final DateTimeFormatter DATE_TIME_FORMATTER = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

    /**
     * 定义构造方法，初始化相关设置
     */
    public ChatServer() {
        try {
            // 1. 得到监听通道
            listenerChannel = ServerSocketChannel.open();
            // 2. 得到选择器
            selector = Selector.open();
            // 3. 绑定端口
            listenerChannel.bind(new InetSocketAddress(PORT));
            // 4. 设置为非阻塞模式
            listenerChannel.configureBlocking(false);
            // 5. 将选择器绑定到监听通道并监听accept事件
            listenerChannel.register(selector, SelectionKey.OP_ACCEPT);
            printInfo("Chat Server is ready.......");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * 服务端的相关业务逻辑
     *
     * @throws Exception
     */
    public void start() throws Exception {
        try {
            /* 循环不停的监控 */
            while (true) {
                // 判断是否有新的客户端连接
                if (selector.select(2000) == 0) {
                    System.out.println("Server:暂无新客户端连接，可进行其他业务逻辑");
                    continue;
                }

                // 获取所有的网络通道key
                Iterator<SelectionKey> keyIterator = selector.selectedKeys().iterator();
                // 迭代所有网络通道
                while (keyIterator.hasNext()) {
                    SelectionKey selectionKey = keyIterator.next();

                    // 客户端连接请求事件
                    if (selectionKey.isAcceptable()) {
                        // 获取客户端连接通道对象
                        SocketChannel socketChannel = listenerChannel.accept();
                        // 设置非阻塞方式
                        socketChannel.configureBlocking(false);
                        // 将每个新连接的通道注册给Selector对象
                        socketChannel.register(selector, SelectionKey.OP_READ);
                        // 做客户端连接成功后的相关业务逻辑...
                        System.out.println(socketChannel.getRemoteAddress().toString().substring(1) + "上线了...");
                    }

                    // 读取客户端数据事件
                    if (selectionKey.isReadable()) {
                        readMsg(selectionKey);
                    }

                    // 手动从集合中移除当前key,防止重复处理
                    keyIterator.remove();
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * 读取客户端发来的消息并广播出去
     *
     * @param selectionKey 网络通道key
     */
    private void readMsg(SelectionKey selectionKey) throws Exception {
        // 根据key获取客户端连接通道
        SocketChannel channel = (SocketChannel) selectionKey.channel();
        // 创建缓冲区
        ByteBuffer buffer = ByteBuffer.allocate(BYTE_SIZE);
        // 获取客户端发送的附件，读取数据放到缓冲区
        int count = channel.read(buffer);
        // 判断是否读取到客户端消息
        if (count > 0) {
            String msg = new String(buffer.array());
            // 打印消息
            this.printInfo(msg);
            // 将消息发送广播
            broadCast(channel, msg);
        }
    }

    /**
     * 给所有的客户端发广播
     *
     * @param channel 客户端连接通道
     * @param msg     消息字符串
     */
    private void broadCast(SocketChannel channel, String msg) {
        System.out.println("服务器发送了广播...");
        /*
         * 过Selector对象以下方法，获取所有准备就绪的网络，循环所有客户端网络通道key
         *  public abstract Set<SelectionKey> keys();
         */
        this.selector.keys().forEach(key -> {
            // 获取其他客户端的连接通道对象
            Channel targetChannel = key.channel();

            // 判断排除本身以内的其他客户端连接通道
            if (targetChannel instanceof SocketChannel && targetChannel != channel) {
                SocketChannel destChannel = (SocketChannel) targetChannel;
                // 获取缓冲区
                ByteBuffer buffer = ByteBuffer.wrap(msg.getBytes());
                try {
                    // 通过连接通道，发送信息
                    destChannel.write(buffer);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        });
    }

    /**
     * 往控制台打印消息
     *
     * @param str 输入的信息
     */
    private void printInfo(String str) {
        System.out.println("[" + DATE_TIME_FORMATTER.format(LocalDateTime.now()) + "] -> " + str);
    }

    public static void main(String[] args) throws Exception {
        // 测试
        new ChatServer().start();
    }
}
```

- 通过 NIO 编写了一个聊天程序的客户端，可以向服务器端发送数据，并能接收服务器广播的数据

```java
package com.moon.system.testmodule.nio.chat;

import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SocketChannel;

/**
 * NIO案例 - 聊天程序客户端
 */
public class ChatClient {

    /* 定义服务器地址 */
    private static final String HOST = "127.0.0.1";
    /* 定义服务器端口 */
    private static final int PORT = 9999;
    /* 定义网络通道 */
    private SocketChannel socketChannel;
    /* 聊天用户名 */
    private String userName;

    /* 缓冲区字节数组大小 */
    private static final int BYTE_SIZE = 1024;

    /**
     * 定义构造方法，初始化业务设置
     *
     * @throws Exception
     */
    public ChatClient() throws Exception {
        // 1. 得到一个网络通道
        socketChannel = SocketChannel.open();
        // 2. 设置非阻塞方式
        socketChannel.configureBlocking(false);
        // 3. 提供服务器端的IP地址和端口号
        InetSocketAddress address = new InetSocketAddress(HOST, PORT);
        // 4. 连接服务器端
        if (!socketChannel.connect(address)) {
            while (!socketChannel.finishConnect()) {
                System.out.println("Client:连接服务器端的同时，我还可以干别的一些事情");
            }
        }
        // 5. 得到客户端IP地址和端口信息，作为聊天用户名使用
        userName = socketChannel.getLocalAddress().toString().substring(1);
        System.out.println("---------------Client(" + userName + ") is ready---------------");
    }

    /**
     * 向服务器端发送数据
     *
     * @param msg 消息字符串
     * @throws Exception
     */
    public void sendMsg(String msg) throws Exception {
        // 定义结束聊天的信息
        if (msg.equalsIgnoreCase("bye")) {
            socketChannel.close();
            return;
        }

        // 给服务端发送数据
        msg = userName + "说：" + msg;
        ByteBuffer buffer = ByteBuffer.wrap(msg.getBytes());
        socketChannel.write(buffer);
    }

    /**
     * 从服务器端接收数据
     *
     * @throws Exception
     */
    public void receiveMsg() throws Exception {
        // 获取字节缓冲区
        ByteBuffer buffer = ByteBuffer.allocate(BYTE_SIZE);
        // 读取数据
        int size = socketChannel.read(buffer);
        if (size > 0) {
            // 如果有接收数据，进行相关业务逻辑处理
            String msg = new String(buffer.array());
            System.out.println(msg.trim());
        }
    }
}
```

- 运行了聊天程序的客户端，并在主线程中发送数据，在另一个线程中不断接收服务器端的广播数据，该代码运行一次就是一个聊天客户端，可以同时运行多个聊天客户端

```java
public class TestChat {
    public static void main(String[] args) throws Exception {
        // 启动客户端
        ChatClient chatClient = new ChatClient();

        // 单独开一个线程不断的接收服务器端广播的数据
        new Thread(() -> {
            while (true) {
                try {
                    // 接收服务端发送的数据
                    chatClient.receiveMsg();
                    // 休眠2秒
                    Thread.currentThread().sleep(2000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }).start();

        // 模拟客户端输入消息
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNextLine()) {
            String msg = scanner.nextLine();
            // 向服务端发送消息
            chatClient.sendMsg(msg);
        }
    }
}
```



### AIO 编程

JDK 7 引入了 Asynchronous I/O，即 AIO。在进行 I/O 编程中，常用到两种模式：Reactor 和 Proactor。Java 的 NIO 就是 Reactor，当有事件触发时，服务器端得到通知，进行相应的处理

IO 即 NIO2.0，叫做异步不阻塞的 IO。AIO 引入异步通道的概念，采用了 Proactor 模式，简化了程序编写，一个有效的请求才启动一个线程，它的特点是先由操作系统完成后才通知服务端程序启动线程去处理，一般适用于连接数较多且连接时间较长的应用

> *目前 AIO 还没有广泛应用*



## IO 对比总结

- IO 的方式通常分为几种：同步阻塞的 BIO、同步非阻塞的 NIO、异步非阻塞的 AIO。
  - **BIO 方式**适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4 以前的唯一选择，但程序直观简单易理解。
  - **NIO 方式**适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4 开始支持。
  - **AIO 方式**使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用 OS 参与并发操作，编程比较复杂，JDK7 开始支持。

> - 举个例子再理解一下：
>   - 同步阻塞：你到饭馆点餐，然后在那等着，啥都干不了，饭馆没做好，你就必须等着！
>   - 同步非阻塞：你在饭馆点完餐，就去玩儿了。不过玩一会儿，就回饭馆问一声：好了没啊！
>   - 异步非阻塞：饭馆打电话说，我们知道您的位置，一会给你送过来，安心玩儿就可以了，类似于现在的外卖。

| 对比总结     | BIO      | NIO                    | AIO        |
| ------------ | -------- | ---------------------- | ---------- |
| IO 方式      | 同步阻塞 | 同步非阻塞（多路复用） | 异步非阻塞 |
| API 使用难度 | 简单     | 复杂                   | 复杂       |
| 可靠性       | 差       | 好                     | 好         |
| 吞吐量       | 低       | 高                     | 高         |





# 序列化与加密算法

## 序列化

如果需要持久化 Java 对象比如将 Java 对象保存在文件中，或者在网络传输 Java 对象，这些场景都需要用到序列化

简单来说：

- **序列化**： 将数据结构或对象转换成二进制字节流的过程
- **反序列化**：将在序列化过程中所生成的二进制字节流的过程转换成数据结构或者对象的过程

对于 Java 这种面向对象编程语言来说，我们序列化的都是对象（Object）也就是实例化后的类(Class)，但是在 C++这种半面向对象的语言中，struct(结构体)定义的是数据结构类型，而 class 对应的是对象类型。

维基百科是如是介绍序列化的：

> **序列化**（serialization）在计算机科学的数据处理中，是指将数据结构或对象状态转换成可取用格式（例如存成文件，存于缓冲，或经由网络中发送），以留待后续在相同或另一台计算机环境中，能恢复原先状态的过程。依照序列化格式重新获取字节的结果时，可以利用它来产生与原始对象相同语义的副本。对于许多对象，像是使用大量引用的复杂对象，这种序列化重建的过程并不容易。面向对象中的对象序列化，并不概括之前原始对象所关系的函数。这种过程也称为对象编组（marshalling）。从一系列字节提取数据结构的反向操作，是反序列化（也称为解编组、deserialization、unmarshalling）。

综上：**序列化的主要目的是通过网络传输对象或者说是将对象存储到文件系统、数据库、内存中。**

![img](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/a478c74d-2c48-40ae-9374-87aacf05188c-166529427007972.png)

**实际开发中有哪些用到序列化和反序列化的场景？**

1. 对象在进行网络传输（比如远程方法调用 RPC 的时候）之前需要先被序列化，接收到序列化的对象之后需要再进行反序列化；
2. 将对象存储到文件中的时候需要进行序列化，将对象从文件中读取出来需要进行反序列化。
3. 将对象存储到缓存数据库（如 Redis）时需要用到序列化，将对象从缓存数据库中读取出来需要反序列化。

**序列化协议对应于 TCP/IP 4 层模型的哪一层？**

网络通信的双方必须要采用和遵守相同的协议。TCP/IP 四层模型是下面这样的，序列化协议属于哪一层呢？

1. 应用层
2. 传输层
3. 网络层
4. 网络接口层

![TCP/IP 4层模型](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/6ecb84cd-4227-4c7b-a2e8-b77054604400-20200802201216504-166529427007974.png)

如上图所示，OSI 七层协议模型中，表示层做的事情主要就是对应用层的用户数据进行处理转换为二进制流。反过来的话，就是将二进制流转换成应用层的用户数据。这不就对应的是序列化和反序列化么？

因为，OSI 七层协议模型中的应用层、表示层和会话层对应的都是 TCP/IP 四层模型中的应用层，所以序列化协议属于 TCP/IP 协议应用层的一部分



**常见序列化协议对比**

二进制序列化

- 保持类型保真度，在应用程序的不同调用之间保留对象的状态很有用。例如，通过将对象序列化到剪贴板，可在不同的应用程序之间共享对象。可以将对象序列化到流、磁盘、内存和网络等等。远程处理使用序列化“通过值”在计算机或应用程序域之间传递对象。

XML序列化

- 仅序列化公共属性和字段，且不保持类型保真度。当要提供或使用数据而不限制使用该数据的应用程序时，这一点是很有用的。由于 XML 是一个开放式标准，因此，对于通过 Web 共享数据而言，这是一个很好的选择。SOAP 同样是一个开放式标准，这使它也成为一个颇具吸引力的选择



## XML

### 简介

XML介绍：

- XML 指可扩展标记语言（EXtensible Markup Language）
- XML 是一种**标记语言**，很类似 HTML，HTML文件也是XML文档
- XML 的设计宗旨是**传输数据**，而非显示数据
- XML 标签没有被预定义，需要自行定义标签
- XML 被设计为具有自我描述性，易于阅读
- XML 是 W3C 的推荐标准

**XML 与 HTML 的区别**：

* XML 不是 HTML 的替代，XML 和 HTML 为不同的目的而设计
* XML 被设计为传输和存储数据，其焦点是数据的内容；XMl标签可自定义，便于阅读
* HTML 被设计用来显示数据，其焦点是数据的外观；HTML标签被预设好，便于浏览器识别
* HTML 旨在显示信息，而 XML 旨在传输信息

XML有几个特点：

- 纯文本，默认使用UTF-8编码
- 可嵌套，适合表示结构化数据。如果把XML内容存为文件，那么它就是一个XML文件，例如`book.xml`
- XML内容经常通过网络作为消息传输

XML有固定的结构

- 格式正确的XML：XML的格式是正确的，可以被解析器正常读取
- 合法的XML：不但XML格式正确，而且它的数据结构可以被DTD或者XSD验证

如何验证XML文件的正确性？

- 最简单的方式是直接把XML文件拖拽到浏览器窗口，如果格式错误，浏览器会报错

和结构类似的HTML不同，浏览器对HTML有一定的“容错性”，缺少关闭标签也可以被解析，但XML要求严格的格式，任何没有正确嵌套的标签都会导致错误。

XML是一个技术体系，除了经常用到的XML文档本身外，XML还支持：

- DTD和XSD：验证XML结构和数据是否有效；
- Namespace：XML节点和属性的名字空间；
- XSLT：把XML转化为另一种文本；
- XPath：一种XML节点查询语言；
- ...

XML的这些相关技术实现起来非常复杂，在实际应用中很少用到，了解一下就可以了



****



### XML结构

person.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<person id="110">
	<age>18</age>		<!--年龄-->
	<name>张三</name>	  <!--姓名-->
	<sex/>				<!--性别-->
</person>
```

XML 文件中常见的组成元素有:文档声明、元素、属性、注释、转义字符、字符区。文件后缀名为 xml

* **文档声明** 
  `<?xml version="1.0" encoding="utf-8" standalone="yes" ?>`，文档声明必须在第一行，以 `<?xml` 开头，以 `?>` 结束，

  * version：指定 XML 文档版本。必须属性，这里一般选择 1.0
  * enconding：指定当前文档的编码，可选属性，默认值是 utf-8
  * standalone：该属性不是必须的，描述 XML 文件是否依赖其他的 xml 文件，取值为 yes/no

* **元素**        

  * 格式 1：`<person></person> ` 
  * 格式 2：`<person/>`
  * 普通元素的结构由开始标签、元素体、结束标签组成
  * 标签由一对尖括号和合法标识符组成，标签必须成对出现。特殊的标签可以不成对，必须有结束标记 </>

* 元素体：可以是元素，也可以是文本，例如：``<person><name>张三</name></person>``

  * 空元素：空元素只有标签，而没有结束标签，但**元素必须自己闭合**，例如：``<sex/>``
  * 元素命名：区分大小写、不能使用空格冒号、不建议用 XML、xml、Xml 等开头
  * 必须存在一个根标签，有且只能有一个

* **属性**：`<name id="1" desc="高富帅">`

  * 属性是元素的一部分，它必须出现在元素的开始标签中
  * 属性的定义格式：`属性名=“属性值”`，其中属性值必须使用单引或双引号括起来
  * 一个元素可以有 0~N 个属性，但一个元素中不能出现同名属性
  * 属性名不能使用空格 , 不要使用冒号等特殊字符，且必须以字母开头

* **注释**：<!--注释内容-->
  XML的注释与HTML相同，既以 `<!--` 开始，`-->` 结束。

* **转义字符**
  XML 中的转义字符与 HTML 一样。因为很多符号已经被文档结构所使用，所以在元素体或属性值中想使用这些符号就必须使用转义字符（也叫实体字符），例如：">"、"<"、"'"、"""、"&"
  XML 中仅有字符 < 和 & 是非法的。省略号、引号和大于号是合法的，把它们替换为实体引用

  | 字符 | 预定义的转义字符 |  说明  |
  | :--: | :--------------: | :----: |
  |  <   |     ``&lt;``     |  小于  |
  |  >   |    `` &gt;``     |  大于  |
  |  "   |   `` &quot;``    | 双引号 |
  |  '   |   `` &apos;``    | 单引号 |
  |  &   |    `` &amp;``    |  和号  |

* **字符区**

  ```xml
  <![CDATA[
  	文本数据
  ]]>
  ```

  * CDATA 指的是不应由 XML 解析器进行解析的文本数据（Unparsed Character Data）

* CDATA 部分由 "<![CDATA[" 开始，由 "]]>" 结束；

  * 大量的转义字符在xml文档中时，会使XML文档的可读性大幅度降低。这时使用CDATA段就会好一些

  * 规则：
    * CDATA 部分不能包含字符串 ]]>，也不允许嵌套的 CDATA 部分
    * 标记 CDATA 部分结尾的 ]]> 不能包含空格或折行

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <?xml-stylesheet type="text/css" href="../css/xml.css" ?>
  <!-- 7.处理指令：导入外部的css样式控制xml的界面效果，没有啥用，xml不是为了展示好看的！-->
  <!-- 1.申明 抬头 必须在第一行-->
  <!-- 2.注释，本处就是注释，必须用前后尖括号围起来 -->
  <!-- 3.标签（元素），注意一个XML文件只能有一个根标签-->
  <student>
      <!-- 4.属性信息：id , desc-->
      <name id="1" desc="高富帅">西门庆</name>
      <age>32</age>
      <!-- 5.实体字符：在xml文件中，我们不能直接写小于号，等一些特殊字符
          会与xml文件本身的内容冲突报错，此时必须用转义的实体字符。
      -->
      <sql>
         <!-- select * from student where age < 18 && age > 10; -->
          select * from student where age &lt; 18 &amp;&amp; age &gt; 10;
      </sql>
      <!-- 6.字符数据区：在xml文件中，我们不能直接写小于号，等一些特殊字符
          会与xml文件本身的内容冲突报错，此时必须用转义的实体字符
          或者也可以选择使用字符数据区，里面的内容可以随便了！
          -->
      <sql2>
          <![CDATA[
               select * from student where age < 18 && age > 10;
          ]]>
      </sql2>
  </student>
  ```

  

****



### XML约束

#### DTD

##### DTD 定义

DTD 是文档类型定义（Document Type Definition）。DTD 可以定义在 XML 文档中出现的元素、这些元素出现的次序、它们如何相互嵌套以及 XML 文档结构的其它详细信息。

DTD 规则：

* 约束元素的嵌套层级

  ```dtd
  <!ELEMENT 父标签 （子标签1，子标签2，…）>
  ```

* 约束元素体里面的数据

* 语法

  ```dtd
  <!ELEMENT 标签名字 标签类型>
  ```

* 判断元素
      简单元素：没有子元素。
      复杂元素：有子元素的元素；

  * 标签类型

  | 标签类型 | 代码写法  | 说明                 |
  | -------- | --------- | -------------------- |
  | PCDATA   | (#PCDATA) | 被解释的字符串数据   |
  | EMPTY    | EMPTY     | 即空元素，例如\<hr/> |
  | ANY      | ANY       | 即任意类型           |

   * 代码

     ```dtd
     <!ELEMENT persons (person+)>   	<!--约束人们至少一个人-->
     <!ELEMENT person (name,age)>	<!--约束元素人的子元素必须为姓名、年龄，并且按顺序-->
     <!ELEMENT name (#PCDATA)>		<!--"姓名"元素体为字符串数据-->
     <!ELEMENT age ANY>       		<!--"年龄"元素体为任意类型-->
     ```

   * 数量词

     | 数量词符号 | 含义                         |
     | ---------- | ---------------------------- |
     | 空         | 表示元素出现一次             |
     | *          | 表示元素可以出现0到多个      |
     | +          | 表示元素可以出现至少1个      |
     | ?          | 表示元素可以是0或1个         |
     | ,          | 表示元素需要按照顺序显示     |
     | \|         | 表示元素需要选择其中的某一个 |

     

* 属性声明

  * 语法

    ```dtd
    <!ATTLIST 标签名称 
    		属性名称1 属性类型1 属性说明1
    		属性名称2 属性类型2 属性说明2
    		…
    >
    ```

  * 属性类型

    | 属性类型   | 含义                                                         |
    | ---------- | ------------------------------------------------------------ |
    | CDATA      | 代表属性是文本字符串， eg:<!ATTLIST 属性名 CDATA 属性说明>   |
    | ID         | 代码该属性值唯一，不能以数字开头， eg:<!ATTLIST 属性名 ID 属性说明> |
    | ENUMERATED | 代表属性值在指定范围内进行枚举 Eg:<!ATTLIST属性名 (社科类\|工程类\|教育类) "社科类"> "社科类"是默认值，属性如果不设置默认值就是"社科类" |

  * 属性说明

    | 属性说明  | 含义                                                        |
    | --------- | ----------------------------------------------------------- |
    | #REQUIRED | 代表属性是必须有的                                          |
    | #IMPLIED  | 代表属性可有可无                                            |
    | #FIXED    | 代表属性为固定值，实现方式：book_info CDATA #FIXED "固定值" |

  * 代码

    ```dtd
    <!ATTLIST 书									<!--设置"书"元素的的属性列表-->
    	id ID #REQUIRED						 <!--"id"属性值为必须有-->
    	编号 CDATA #IMPLIED				    <!--"编号"属性可有可无-->
    	出版社 (清华|北大|传智播客) "传智播客" <!--"出版社"属性值是枚举值，默认为“传智播客”-->
    	type CDATA #FIXED "IT"            <!--"type"属性为文本字符串并且固定值为"IT"-->
    >
    <!ATTLIST person id CDATA #REQUIRED>  <!--id是文本字符串必须有-->
    ```

    

****



##### DTD 引入

* 引入本地 dtd

  ```dtd
  <!DOCTYPE 根元素名称 SYSTEM ‘DTD文件的路径'>
  ```

* 在 xml 文件内部引入

  ```dtd
  <!DOCTYPE 根元素名称 [ dtd文件内容 ]>
  ```

* 引入网络 dtd

  ```dtd
  <!DOCTYPE 根元素的名称 PUBLIC "DTD文件名称" "DTD文档的URL">
  ```

```dtd
<!--这是persondtd.dtd文件中的内容,已经提前写好-->
<!ELEMENT persons (person)>
<!ELEMENT person (name,age)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT age (#PCDATA)>
```

```xml
<!--引入本地DTD-->
<!DOCTYPE persons SYSTEM 'persondtd.dtd'>
<persons>
    <person>
        <name>张三</name>
        <age>23</age>
    </person>

</persons>
```

```xml-dtd
<!--内部引入DTD-->
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE persons [
        <!ELEMENT persons (person)>
        <!ELEMENT person (name,age)>
        <!ELEMENT name (#PCDATA)>
        <!ELEMENT age (#PCDATA)>
        ]>

<persons>
    <person>
        <name>张三</name>
        <age>23</age>
    </person>
</persons>
```

```dtd
<!--引入网络DTD--><?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE persons PUBLIC "dtd文件的名称" "dtd文档的URL">

<persons>
    <person>
        <name>张三</name>
        <age>23</age>
    </person>
</persons>
```



***



##### DTD 实现

persondtd.dtd 文件

```dtd
<!ELEMENT persons (person+)>   	<!--约束人们至少一个人-->
<!ELEMENT person (name,age)>	<!--约束元素人的子元素必须为姓名、年龄，并且按顺序-->
<!ELEMENT name (#PCDATA)>		<!--"姓名"元素体为字符串数据-->
<!ELEMENT age ANY>       		<!--"年龄"元素体为任意类型-->
<!ATTLIST person id CDATA #REQUIRED>  <!--id是文本字符串必须有-->
```

```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE persons SYSTEM 'persondtd.dtd'>

<persons>
    <person id="001">
        <name>张三</name>
        <age>23</age>
    </person>

    <person id = "002">
        <name>张三</name>
        <age>23</age>
    </person>
</persons>
```



***



#### Schema

##### XSD 定义

1. Schema 语言也可作为 XSD（XML Schema Definition）
2. Schema 约束文件本身也是一个 XML 文件，符合 XML 的语法，这个文件的后缀名 .xsd
3. 一个 XML 中可以引用多个 Schema 约束文件，多个 Schema 使用名称空间区分（名称空间类似于 Java 包名）
4. dtd 里面元素类型的取值比较单一常见的是 PCDATA 类型，但是在 Schema 里面可以支持很多个数据类型
5. **Schema 文件约束 XML 文件的同时也被别的文件约束着**



***



##### XSD 规则

1. 创建一个文件，这个文件的后缀名为 .xsd
2. 定义文档声明
3. schema 文件的根标签为： <schema>
4. 在 <schema> 中定义属性：
   * xmlns=http://www.w3.org/2001/XMLSchema
   * 代表当前文件时约束别人的，同时这个文件也对该 Schema 进行约束
5. 在<schema>中定义属性 ：
   * targetNamespace = 唯一的 url 地址，指定当前这个 schema 文件的名称空间。
   * **名称空间**：当其他 xml 使用该 schema 文件，需要引入此空间
6. 在<schema>中定义属性 ：
   * elementFormDefault="qualified“，表示当前 schema 文件是一个质量良好的文件。
7. 通过 element 定义元素
8. **判断当前元素是简单元素还是复杂元素**

person.xsd

```scheme
<?xml version="1.0" encoding="UTF-8" ?>
<schema
    xmlns="http://www.w3.org/2001/XMLSchema"     <!--本文件是约束别人的，也被约束-->
    targetNamespace="http://www.seazean.cn/javase"<!--自己的名称空间-->
    elementFormDefault="qualified"				  <!--本文件是质量好的-->
>

    <element name="persons">    		  <!--定义persons复杂元素-->
        <complexType>           		  <!--复杂的元素-->
            <sequence>					  <!--里面的元素必须按照顺序定义-->
                <element name = "person"> <!--定义person复杂元素-->
                    <complexType>
                        <sequence>
                            <!--定义name和age简单元素-->
                            <element name = "name" type = "string"></element>
                            <element name = "age" type = "string"></element>
                        </sequence>
                    </complexType>
                </element>
            </sequence>
        </complexType>
    </element>
    
</schema>
```



****



##### XSD 引入

1. 在根标签上定义属性 xmlns="http://www.w3.org/2001/XMLSchema-instance"
2. **通过 xmlns 引入约束文件的名称空间**
3. 给某一个 xmlns 属性添加一个标识，用于区分不同的名称空间，格式为 `xmlns:标识="名称空间url"` ，标识可以是任意的，但是一般取值都是 xsi
4. 通过 xsi:schemaLocation 指定名称空间所对应的约束文件路径，格式为 `xsi:schemaLocation = "名称空间url 文件路径`

```scheme
<?xml version="1.0" encoding="UTF-8" ?>
<persons
	xmlms:xis="http://www.w3.org/2001/XMLSchema-instance" <!--被别人约束-->
    xmlns="http://www.seazean.cn/javase"                  <!--约束文件的名称空间-->
    xsi:schemaLocation="http://www.seazean.cn/javase person.xsd"
>

 <person>
        <name>张三</name>
        <age>23</age>
    </person>

</persons>
```



****



##### XSD 属性

```scheme
<?xml version="1.0" encoding="UTF-8" ?>
<schema
    xmlns="http://www.w3.org/2001/XMLSchema"
    targetNamespace="http://www.seazean.cn/javase"
    elementFormDefault="qualified"
>

    <!--定义persons复杂元素-->
    <element name="persons">
        <complexType>
            <sequence>
                <!--定义person复杂元素-->
                <element name = "person">
                    <complexType>
                        <sequence>
                            <!--定义name和age简单元素-->
                            <element name = "name" type = "string"></element>
                            <element name = "age" type = "string"></element>
                        </sequence>
                        <!--定义的位置是sequence的外面，complexType的里面-->
                        <!--定义属性，required( 必须的)/optional( 可选的)-->
                        <attribute name="id" type="string" use="required">		
						</attribute>
                    </complexType>
                    
                </element>
            </sequence>
        </complexType>
    </element>
    
</schema>

<?xml version="1.0" encoding="UTF-8" ?>
<persons
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://www.seazean.cn/javase"
    xsi:schemaLocation="http://www.seazean.cn/javase person.xsd"
>
    <person id="001">
        <name>张三</name>
        <age>23</age>
    </person>

</persons>
```



***

### XML解析

XML 解析就是从 XML 中获取到数据

因为XML是一种树形结构的文档，它有两种标准的解析API：

- DOM：一次性读取XML，并在内存中表示为树形结构；
- SAX：以流的形式读取XML，使用事件回调。



#### DOM

DOM是Document Object Model的缩写，DOM模型就是把XML结构作为一个树形结构处理，从根节点开始，每个节点都可以包含任意个子节点。

以下面的XML为例：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<book id="1">
    <name>Java核心技术</name>
    <author>Cay S. Horstmann</author>
    <isbn lang="CN">1234567</isbn>
    <tags>
        <tag>Java</tag>
        <tag>Network</tag>
    </tags>
    <pubDate/>
</book>
```

如果解析为DOM结构，大概长这样：

<img src="https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220620101512790-166529427008076.png" alt="image-20220620101512790" style="zoom: 67%;" />

最顶层的document代表XML文档，它是真正的“根”，而`<book>`虽然是根元素，但它是`document`的一个子节点。

Java提供了DOM API来解析XML，它使用下面的对象来表示XML的内容：

- Document：代表整个XML文档；
- Element：代表一个XML元素；
- Attribute：代表一个元素的某个属性。

使用DOM API解析一个XML文档的代码如下：

```java
InputStream input = Main.class.getResourceAsStream("/book.xml");
DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
DocumentBuilder db = dbf.newDocumentBuilder();
Document doc = db.parse(input);
```

`DocumentBuilder.parse()`用于解析一个XML，它可以接收InputStream，File或者URL，如果解析无误，将获得一个Document对象，这个对象代表了整个XML文档的树形结构，需要遍历以便读取指定元素的值：

```java
void printNode(Node n, int indent) {
    for (int i = 0; i < indent; i++) {
        System.out.print(' ');
    }
    switch (n.getNodeType()) {
    case Node.DOCUMENT_NODE: // Document节点
        System.out.println("Document: " + n.getNodeName());
        break;
    case Node.ELEMENT_NODE: // 元素节点
        System.out.println("Element: " + n.getNodeName());
        break;
    case Node.TEXT_NODE: // 文本
        System.out.println("Text: " + n.getNodeName() + " = " + n.getNodeValue());
        break;
    case Node.ATTRIBUTE_NODE: // 属性
        System.out.println("Attr: " + n.getNodeName() + " = " + n.getNodeValue());
        break;
    default: // 其他
        System.out.println("NodeType: " + n.getNodeType() + ", NodeName: " + n.getNodeName());
    }
    for (Node child = n.getFirstChild(); child != null; child = child.getNextSibling()) {
        printNode(child, indent + 1);
    }
}
```

解析结构如下：

```bash
Document: #document
 Element: book
  Text: #text = 
    
  Element: name
   Text: #text = Java核心技术
  Text: #text = 
    
  Element: author
   Text: #text = Cay S. Horstmann
  Text: #text = 
  ...
```

对于DOM API解析出来的结构，从根节点Document出发，可以遍历所有子节点，获取所有元素、属性、文本数据，还可以包括注释，这些节点被统称为Node，每个Node都有自己的Type，根据Type来区分一个Node到底是元素，还是属性，还是文本，等等。

使用DOM API时，如果要读取某个元素的文本，需要访问它的Text类型的子节点，所以使用起来还是比较繁琐的。

#### SAX

使用DOM解析XML的优点是用起来省事，但它的主要缺点是内存占用太大。

另一种解析XML的方式是SAX。SAX是Simple API for XML的缩写，它是一种基于流的解析方式，边读取XML边解析，并以事件回调的方式让调用者获取数据。因为是一边读一边解析，所以无论XML有多大，占用的内存都很小。

SAX解析会触发一系列事件：

- startDocument：开始读取XML文档；
- startElement：读取到了一个元素，例如`<book>`；
- characters：读取到了字符；
- endElement：读取到了一个结束的元素，例如`</book>`；
- endDocument：读取XML文档结束。

如果用SAX API解析XML，Java代码如下：

```java
InputStream input = Main.class.getResourceAsStream("/book.xml");
SAXParserFactory spf = SAXParserFactory.newInstance();
SAXParser saxParser = spf.newSAXParser();
saxParser.parse(input, new MyHandler());
```

关键代码`SAXParser.parse()`除了需要传入一个`InputStream`外，还需要传入一个回调对象，这个对象要继承自`DefaultHandler`：

```java
class MyHandler extends DefaultHandler {
    public void startDocument() throws SAXException {
        print("start document");
    }

    public void endDocument() throws SAXException {
        print("end document");
    }

    public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {
        print("start element:", localName, qName);
    }

    public void endElement(String uri, String localName, String qName) throws SAXException {
        print("end element:", localName, qName);
    }

    public void characters(char[] ch, int start, int length) throws SAXException {
        print("characters:", new String(ch, start, length));
    }

    public void error(SAXParseException e) throws SAXException {
        print("error:", e);
    }

    void print(Object... objs) {
        for (Object obj : objs) {
            System.out.print(obj);
            System.out.print(" ");
        }
        System.out.println();
    }
}
```

运行SAX解析代码，可以打印出下面的结果：

```
start document
start element:  book
characters:
     
start element:  name
characters: Java核心技术
end element:  name
characters:
     
start element:  author
...
```

如果要读取`<name>`节点的文本，就必须在解析过程中根据`startElement()`和`endElement()`定位当前正在读取的节点，可以使用栈结构保存，每遇到一个`startElement()`入栈，每遇到一个`endElement()`出栈，这样，读到`characters()`时我们才知道当前读取的文本是哪个节点的。可见，使用SAX API仍然比较麻烦。



#### Jackson

无论是DOM还是SAX，使用起来都不直观。观察XML文档的结构：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<book id="1">
    <name>Java核心技术</name>
    <author>Cay S. Horstmann</author>
    <isbn lang="CN">1234567</isbn>
    <tags>
        <tag>Java</tag>
        <tag>Network</tag>
    </tags>
    <pubDate/>
</book>
```

发现它完全可以对应到一个定义好的JavaBean中：

```java
public class Book {
    public long id;
    public String name;
    public String author;
    public String isbn;
    public List<String> tags;
    public String pubDate;
}
```

如果能直接从XML文档解析成一个JavaBean，那比DOM或者SAX不知道容易到哪里去了。

幸运的是，一个名叫Jackson的开源的第三方库可以轻松做到XML到JavaBean的转换。要使用Jackson，先添加两个Maven的依赖：

- com.fasterxml.jackson.dataformat:jackson-dataformat-xml:2.10.1
- org.codehaus.woodstox:woodstox-core-asl:4.4.1

然后，定义好JavaBean，就可以用下面几行代码解析：

```java
InputStream input = Main.class.getResourceAsStream("/book.xml");
JacksonXmlModule module = new JacksonXmlModule();
XmlMapper mapper = new XmlMapper(module);
Book book = mapper.readValue(input, Book.class);
System.out.println(book.id);
System.out.println(book.name);
System.out.println(book.author);
System.out.println(book.isbn);
System.out.println(book.tags);
System.out.println(book.pubDate);
```

注意到`XmlMapper`就是需要创建的核心对象，可以用`readValue(InputStream, Class)`直接读取XML并返回一个JavaBean。运行上述代码，就可以直接从Book对象中拿到数据：

```
1
Java核心技术
Cay S. Horstmann
1234567
[Java, Network]
null
```

如果要解析的数据格式不是Jackson内置的标准格式，那么需要编写一点额外的扩展来告诉Jackson如何自定义解析。这里我们不做深入讨论，可以参考Jackson的[官方文档](https://github.com/FasterXML/jackson)。



## JSON

### 简介

XML的特点是功能全面，但标签繁琐，格式复杂。在Web上使用XML现在越来越少，取而代之的是JSON这种数据结构。

JSON是JavaScript Object Notation的缩写，它去除了所有JavaScript执行代码，只保留JavaScript的对象格式。一个典型的JSON如下：

```json
{
    "id": 1,
    "name": "Java核心技术",
    "author": {
        "firstName": "Abc",
        "lastName": "Xyz"
    },
    "isbn": "1234567",
    "tags": ["Java", "Network"]
}
```

JSON作为数据传输的格式，有几个显著的优点：

- JSON只允许使用UTF-8编码，不存在编码问题；
- JSON只允许使用双引号作为key，特殊字符用`\`转义，格式简单；
- 浏览器内置JSON支持，如果把数据用JSON发送给浏览器，可以用JavaScript直接处理。

因此JSON适合表示层次结构，因为它格式简单，仅支持以下几种数据类型：

- 键值对：`{"key": value}`
- 数组：`[1, 2, 3]`
- 字符串：`"abc"`
- 数值（整数和浮点数）：`12.34`
- 布尔值：`true`或`false`
- 空值：`null`

浏览器直接支持使用JavaScript对JSON进行读写：

```javascript
// JSON string to JavaScript object:
jsObj = JSON.parse(jsonStr);

// JavaScript object to JSON string:
jsonStr = JSON.stringify(jsObj);
```

所以，开发Web应用的时候，使用JSON作为数据传输，在浏览器端非常方便。因为JSON天生适合JavaScript处理，所以，绝大多数REST API都选择JSON作为数据传输格式。



### 序列化

在Java中，针对 JSON也有标准的 JSR 353 API，Jackson也可以解析JSON，只需要引入以下Maven依赖：

- com.fasterxml.jackson.core:jackson-databind:2.12.0

**把 JSON解析为JavaBean的过程称为反序列化：**

```java
InputStream input = Main.class.getResourceAsStream("/book.json");
ObjectMapper mapper = new ObjectMapper();
// 反序列化时忽略不存在的JavaBean属性:
mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
Book book = mapper.readValue(input, Book.class);
```

核心代码是创建一个`ObjectMapper`对象。

关闭`DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES`功能：解析时如果JavaBean不存在该属性时解析不会报错。

**把 JavaBean变为 JSON是序列化**：

```java
String json = mapper.writeValueAsString(book);
```



要把 JSON的某些值解析为特定的Java对象，例如`LocalDate`，也是完全可以的。例如：

```json
{
    "name": "Java核心技术",
    "pubDate": "2016-09-01"
}
```

要解析为：

```java
public class Book {
    public String name;
    public LocalDate pubDate;
}
```

只需要引入标准的JSR 310关于JavaTime的数据格式定义至Maven：

- com.fasterxml.jackson.datatype:jackson-datatype-jsr310:2.12.0

然后，在创建`ObjectMapper`时，注册一个新的`JavaTimeModule`：

```java
ObjectMapper mapper = new ObjectMapper().registerModule(new JavaTimeModule());
```



**内置的解析规则和扩展的解析规则如果都不满足需求，还可以自定义解析**

假设`Book`类的`isbn`是一个`BigInteger`：

```java
public class Book {
	public String name;
	public BigInteger isbn;
}
```

但 JSON数据并不是标准的整形格式：

```json
{
    "name": "Java核心技术",
    "isbn": "978-7-111-54742-6"
}
```

直接解析肯定报错。这时需要自定义一个`IsbnDeserializer`，用于解析含有非数字的字符串：

```java
public class IsbnDeserializer extends JsonDeserializer<BigInteger> {
    public BigInteger deserialize(JsonParser p, DeserializationContext ctxt) throws IOException, JsonProcessingException {
        // 读取原始的JSON字符串内容:
        String s = p.getValueAsString();
        if (s != null) {
            try {
                return new BigInteger(s.replace("-", ""));
            } catch (NumberFormatException e) {
                throw new JsonParseException(p, s, e);
            }
        }
        return null;
    }
}
```

然后在`Book`类中使用注解标注：

```java
public class Book {
    public String name;
    // 表示反序列化isbn时使用自定义的IsbnDeserializer:
    @JsonDeserialize(using = IsbnDeserializer.class)
    public BigInteger isbn;
}
```

类似的，自定义序列化时需要自定义一个`IsbnSerializer`，然后在`Book`类中标注`@JsonSerialize(using = ...)`即可。



在反序列化时，Jackson要求Java类需要一个默认的无参数构造方法，否则，无法直接实例化此类。存在带参数构造方法的类，如果要反序列化，注意再提供一个无参数构造方法。

对于`enum`字段，Jackson按String类型处理，即：

```java
class Book {
    public DayOfWeek start = MONDAY;
}
```

序列化为：

```json
{
    "start": "MONDAY"
}
```

对于`record`类型，Jackson会自动找出它的带参数构造方法，并根据JSON的key进行匹配，可直接反序列化。对`record`类型的支持需要版本`2.12.0`以上。

****



## 加密与安全

假设Bob要给Alice发一封邮件，

- 在邮件传送的过程中，黑客可能会窃取到邮件的内容，所以需要防窃听。
- 黑客还可能会篡改邮件的内容，Alice必须有能力识别出邮件有没有被篡改。
- 黑客可能假冒Bob给Alice发邮件，Alice必须有能力识别出伪造的邮件。

应对潜在的安全威胁，需要做到三防：

- 防窃听
- 防篡改
- 防伪造

计算机加密技术就是为了实现上述目标，而现代计算机密码学理论是建立在严格的数学理论基础上的，密码学已经逐渐发展成一门科学。对于绝大多数开发者来说，设计一个安全的加密算法非常困难，验证一个加密算法是否安全更加困难，当前被认为安全的加密算法仅仅是迄今为止尚未被攻破。因此，要编写安全的计算机程序需要做到：

- 不要自己设计山寨的加密算法；
- 不要自己实现已有的加密算法；
- 不要自己修改已有的加密算法。

下面介绍最常用的加密算法，以及如何通过Java代码实现



### 编码算法

ASCII码就是一种编码，字母`A`的编码是十六进制的`0x41`，字母`B`是`0x42`，以此类推：

| 字母 | ASCII编码 |
| :--- | :-------- |
| A    | 0x41      |
| B    | 0x42      |
| C    | 0x43      |
| D    | 0x44      |
| …    | …         |

因为ASCII编码最多只能有127个字符，要想对更多的文字进行编码，就需要用Unicode。而中文的中使用Unicode编码就是`0x4e2d`，使用UTF-8则需要3个字节编码：

| 汉字 | Unicode编码 | UTF-8编码 |
| :--- | :---------- | :-------- |
| 中   | 0x4e2d      | 0xe4b8ad  |
| 文   | 0x6587      | 0xe69687  |
| 编   | 0x7f16      | 0xe7bc96  |
| 码   | 0x7801      | 0xe7a081  |
| …    | …           | …         |

因此，最简单的编码是直接给每个字符指定一个若干字节表示的整数，复杂一点的编码就需要根据一个已有的编码推算出来。

比如UTF-8编码，它是一种不定长编码，但可以从给定字符的Unicode编码推算出来。



#### URL编码

URL编码是浏览器发送数据给服务器时使用的编码，它通常附加在URL的参数部分，例如：

[https://www.baidu.com/s?wd=%E4%B8%AD%E6%96%87](https://www.baidu.com/s?wd=中文)

之所以需要URL编码，是因为出于兼容性考虑，很多服务器只识别ASCII字符。但如果URL中包含中文、日文这些非ASCII字符怎么办？不要紧，URL编码有一套规则：

- 如果字符是`A`~ `Z`，`a`~ `z`，`0`~`9`以及`-`、`_`、`.`、`*`，则保持不变；
- 如果是其他字符，先转换为UTF-8编码，然后对每个字节以`%XX`表示。

例如：字符`中`的UTF-8编码是`0xe4b8ad`，因此，它的URL编码是`%E4%B8%AD`。URL编码总是大写。

Java标准库提供了一个`URLEncoder`类来对任意字符串进行URL编码：

```java
import java.net.URLEncoder;
import java.nio.charset.StandardCharsets;

public class Main {
    public static void main(String[] args) {
        String encoded = URLEncoder.encode("中文!", StandardCharsets.UTF_8);
        System.out.println(encoded);
    }
}
```

上述代码的运行结果是`%E4%B8%AD%E6%96%87%21`，`中`的URL编码是`%E4%B8%AD`，`文`的URL编码是`%E6%96%87`，`!`虽然是ASCII字符，也要对其编码为`%21`。

和标准的URL编码稍有不同，URLEncoder把空格字符编码成`+`，而现在的URL编码标准要求空格被编码为`%20`，不过，服务器都可以处理这两种情况。

如果服务器收到URL编码的字符串，就可以对其进行解码，还原成原始字符串。Java标准库的`URLDecoder`就可以解码：

```java
import java.net.URLDecoder;
import java.nio.charset.StandardCharsets;

public class Main {
    public static void main(String[] args) {
        String decoded = URLDecoder.decode("%E4%B8%AD%E6%96%87%21", StandardCharsets.UTF_8);
        System.out.println(decoded);
    }
}
```

要特别注意：URL编码是编码算法，不是加密算法。URL编码的目的是把任意文本数据编码为`%`前缀表示的文本，编码后的文本仅包含`A`~`Z`，`a`~`z`，`0`~`9`，`-`，`_`，`.`，`*`和`%`，便于浏览器和服务器处理。



#### Base64编码

URL编码是对字符进行编码，表示成`%xx`的形式，而Base64编码是对二进制数据进行编码，表示成文本格式。

Base64编码可以把任意长度的二进制数据变为纯文本，且只包含`A` ~ `Z`、`a` ~ `z`、`0`~`9`、`+`、`/`、`=`这些字符。它的原理是把3字节的二进制数据按6bit一组，用4个int整数表示，然后查表，把int整数用索引对应到字符，得到编码后的字符串。

举个例子：3个byte数据分别是`e4`、`b8`、`ad`，按6bit分组得到`39`、`0b`、`22`和`2d`：

![image-20220620104617171](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220620104617171-166529427008075.png)

因为6位整数的范围总是`0` ~ `63`，所以，能用64个字符表示：字符`A` ~ `Z`对应索引`0` ~ `25`，字符`a` ~ `z`对应索引`26` ~ `51`，字符`0`~ `9`对应索引`52`~`61`，最后两个索引`62`、`63`分别用字符`+`和`/`表示。

在Java中，二进制数据就是`byte[]`数组。Java标准库提供了`Base64`来对`byte[]`数组进行编解码：

```java
public class Main {
    public static void main(String[] args) {
        byte[] input = new byte[] { (byte) 0xe4, (byte) 0xb8, (byte) 0xad };
        String b64encoded = Base64.getEncoder().encodeToString(input);
        System.out.println(b64encoded);
    }
}
```

编码后得到`5Lit`4个字符。要对`Base64`解码，仍然用`Base64`这个类：

```java
public class Main {
    public static void main(String[] args) {
        byte[] output = Base64.getDecoder().decode("5Lit");
        System.out.println(Arrays.toString(output)); // [-28, -72, -83]
    }
}
```

如果输入的`byte[]`数组长度不是3的整数倍怎么办？

- 需要对输入的末尾补一个或两个`0x00`，编码后，在结尾加一个`=`表示补充了1个`0x00`，加两个`=`表示补充了2个`0x00`，解码的时候，去掉末尾补充的一个或两个`0x00`即可。

实际上，因为编码后的长度加上`=`总是4的倍数，所以即使不加`=`也可以计算出原始输入的`byte[]`。Base64编码的时候可以用`withoutPadding()`去掉`=`，解码出来的结果是一样的：

```java
public class Main {
    public static void main(String[] args) {
        byte[] input = new byte[] { (byte) 0xe4, (byte) 0xb8, (byte) 0xad, 0x21 };
        String b64encoded = Base64.getEncoder().encodeToString(input);
        String b64encoded2 = Base64.getEncoder().withoutPadding().encodeToString(input);
        System.out.println(b64encoded);
        System.out.println(b64encoded2);
        byte[] output = Base64.getDecoder().decode(b64encoded2);
        System.out.println(Arrays.toString(output));
    }
}
```

因为标准的Base64编码会出现`+`、`/`和`=`，所以不适合把Base64编码后的字符串放到URL中。一种针对URL的Base64编码可以在URL中使用的Base64编码，它仅仅是把`+`变成`-`，`/`变成`_`：

```java
public class Main {
    public static void main(String[] args) {
        byte[] input = new byte[] { 0x01, 0x02, 0x7f, 0x00 };
        String b64encoded = Base64.getUrlEncoder().encodeToString(input);
        System.out.println(b64encoded);
        byte[] output = Base64.getUrlDecoder().decode(b64encoded);
        System.out.println(Arrays.toString(output));
    }
}
```

Base64编码的目的是把二进制数据变成文本格式，这样在很多文本中就可以处理二进制数据。例如，电子邮件协议就是文本协议，如果要在电子邮件中添加一个二进制文件，就可以用Base64编码，然后以文本的形式传送。

Base64编码的缺点是传输效率会降低，因为它把原始数据的长度增加了1/3。

和URL编码一样，Base64编码是一种编码算法，不是加密算法。

如果把Base64的64个字符编码表换成32个、48个或者58个，就可以使用Base32编码，Base48编码和Base58编码。字符越少，编码的效率就会越低。

### 防篡改

#### Hash算法

哈希算法（Hash）又称摘要算法（Digest），它的作用是：对任意一组输入数据进行计算，得到一个固定长度的输出摘要。

哈希算法最重要的特点就是：

- 相同的输入一定得到相同的输出；
- 不同的输入大概率得到不同的输出。

哈希算法的目的就是为了验证原始数据是否被篡改。

Java字符串的`hashCode()`就是一个哈希算法，它的输入是任意字符串，输出是固定的4字节`int`整数：

```java
"hello".hashCode(); // 0x5e918d2
"hello, java".hashCode(); // 0x7a9d88e8
"hello, bob".hashCode(); // 0xa0dbae2f
```

两个相同的字符串永远会计算出相同的`hashCode`，否则基于`hashCode`定位的`HashMap`就无法正常工作。这也是为什么当我们自定义一个class时，覆写`equals()`方法时我们必须正确覆写`hashCode()`方法。

#### 哈希碰撞

哈希碰撞是指，两个不同的输入得到了相同的输出：

```java
"AaAaAa".hashCode(); // 0x7460e8c0
"BBAaBB".hashCode(); // 0x7460e8c0
```

有童鞋会问：碰撞能不能避免？答案是不能。碰撞是一定会出现的，因为输出的字节长度是固定的，`String`的`hashCode()`输出是4字节整数，最多只有4294967296种输出，但输入的数据长度是不固定的，有无数种输入。所以，哈希算法是把一个无限的输入集合映射到一个有限的输出集合，必然会产生碰撞。

碰撞不可怕，担心的不是碰撞，而是碰撞的概率，因为碰撞概率的高低关系到哈希算法的安全性。一个安全的哈希算法必须满足：

- 碰撞概率低；
- 不能猜测输出。

不能猜测输出是指，输入的任意一个bit的变化会造成输出完全不同，这样就很难从输出反推输入（只能依靠暴力穷举）。假设一种哈希算法有如下规律：

```java
hashA("java001") = "123456"
hashA("java002") = "123457"
hashA("java003") = "123458"
```

那么很容易从输出`123459`反推输入，这种哈希算法就不安全。安全的哈希算法从输出是看不出任何规律的：

```java
hashB("java001") = "123456"
hashB("java002") = "580271"
hashB("java003") = ???
```

常用的哈希算法有：

| 算法       | 输出长度（位） | 输出长度（字节） |
| :--------- | :------------- | :--------------- |
| MD5        | 128 bits       | 16 bytes         |
| SHA-1      | 160 bits       | 20 bytes         |
| RipeMD-160 | 160 bits       | 20 bytes         |
| SHA-256    | 256 bits       | 32 bytes         |
| SHA-512    | 512 bits       | 64 bytes         |

根据碰撞概率，哈希算法的输出长度越长，就越难产生碰撞，也就越安全。

Java标准库提供了常用的哈希算法，并且有一套统一的接口。以MD5算法为例，看看如何对输入计算哈希：

```java
import java.math.BigInteger;
import java.security.MessageDigest;

public class Main {
    public static void main(String[] args) throws Exception {
        // 创建一个MessageDigest实例:
        MessageDigest md = MessageDigest.getInstance("MD5");
        // 反复调用update输入数据:
        md.update("Hello".getBytes("UTF-8"));
        md.update("World".getBytes("UTF-8"));
        byte[] result = md.digest(); // 16 bytes: 68e109f0f40ca72a15e05cc22786f8e6
        System.out.println(new BigInteger(1, result).toString(16));
    }
}
```

使用`MessageDigest`时，我们首先根据哈希算法获取一个`MessageDigest`实例，然后，反复调用`update(byte[])`输入数据。当输入结束后，调用`digest()`方法获得byte[]数组表示的摘要，最后，把它转换为十六进制的字符串。

运行上述代码，可以得到输入`HelloWorld`的MD5是`68e109f0f40ca72a15e05cc22786f8e6`。



#### 哈希算法的用途

因为相同的输入永远会得到相同的输出，因此，如果输入被修改了，得到的输出就会不同。

我们在网站上下载软件的时候，经常看到下载页显示的哈希：

![image-20220620105620484](https://cdn.jsdelivr.net/gh/Hanjl1203/images/imgs/image-20220620105620484-166529427008077.png)

如何判断下载到本地的软件是原始的、未经篡改的文件？我们只需要自己计算一下本地文件的哈希值，再与官网公开的哈希值对比，如果相同，说明文件下载正确，否则，说明文件已被篡改。

哈希算法的另一个重要用途是存储用户口令。如果直接将用户的原始口令存放到数据库中，会产生极大的安全风险：

- 数据库管理员能够看到用户明文口令；
- 数据库数据一旦泄漏，黑客即可获取用户明文口令。

不存储用户的原始口令，那么如何对用户进行认证？

方法是存储用户口令的哈希，例如，MD5。

在用户输入原始口令后，系统计算用户输入的原始口令的MD5并与数据库存储的MD5对比，如果一致，说明口令正确，否则，口令错误。

因此，数据库存储用户名和口令的表内容应该像下面这样：

| username | password                         |
| :------- | :------------------------------- |
| bob      | f30aa7a662c728b7407c54ae6bfd27d1 |
| alice    | 25d55ad283aa400af464c76d713c07ad |
| tim      | bed128365216c019988915ed3add75fb |

这样一来，数据库管理员看不到用户的原始口令。即使数据库泄漏，黑客也无法拿到用户的原始口令。想要拿到用户的原始口令，必须用暴力穷举的方法，一个口令一个口令地试，直到某个口令计算的MD5恰好等于指定值。

使用哈希口令时，还要注意防止彩虹表攻击。

什么是彩虹表呢？上面讲到了，如果只拿到MD5，从MD5反推明文口令，只能使用暴力穷举的方法。

然而黑客并不笨，暴力穷举会消耗大量的算力和时间。但是，如果有一个预先计算好的常用口令和它们的MD5的对照表：

| 常用口令 | MD5                              |
| :------- | :------------------------------- |
| hello123 | f30aa7a662c728b7407c54ae6bfd27d1 |
| 12345678 | 25d55ad283aa400af464c76d713c07ad |
| passw0rd | bed128365216c019988915ed3add75fb |
| 19700101 | 570da6d5277a646f6552b8832012f5dc |
| …        | …                                |
| 20201231 | 6879c0ae9117b50074ce0a0d4c843060 |

这个表就是彩虹表。如果用户使用了常用口令，黑客从MD5一下就能反查到原始口令：

bob的MD5：`f30aa7a662c728b7407c54ae6bfd27d1`，原始口令：`hello123`；

alice的MD5：`25d55ad283aa400af464c76d713c07ad`，原始口令：`12345678`；

tim的MD5：`bed128365216c019988915ed3add75fb`，原始口令：`passw0rd`。

这就是为什么不要使用常用密码，以及不要使用生日作为密码的原因。

即使用户使用了常用口令，我们也可以采取措施来抵御彩虹表攻击，方法是对每个口令额外添加随机数，这个方法称之为加盐（salt）：

```
digest = md5(salt+inputPassword)
```

经过加盐处理的数据库表，内容如下：

| username | salt  | password                         |
| :------- | :---- | :------------------------------- |
| bob      | H1r0a | a5022319ff4c56955e22a74abcc2c210 |
| alice    | 7$p2w | e5de688c99e961ed6e560b972dab8b6a |
| tim      | z5Sk9 | 1eee304b92dc0d105904e7ab58fd2f64 |

加盐的目的在于使黑客的彩虹表失效，即使用户使用常用口令，也无法从MD5反推原始口令。

#### SHA-1

SHA-1也是一种哈希算法，它的输出是160 bits，即20字节。SHA-1是由美国国家安全局开发的，SHA算法实际上是一个系列，包括SHA-0（已废弃）、SHA-1、SHA-256、SHA-512等。

在Java中使用SHA-1，和MD5完全一样，只需要把算法名称改为`"SHA-1"`：

```java
import java.math.BigInteger;
import java.security.MessageDigest;

public class Main {
    public static void main(String[] args) throws Exception {
        // 创建一个MessageDigest实例:
        MessageDigest md = MessageDigest.getInstance("SHA-1");
        // 反复调用update输入数据:
        md.update("Hello".getBytes("UTF-8"));
        md.update("World".getBytes("UTF-8"));
        byte[] result = md.digest(); // 20 bytes: db8ac1c259eb89d4a131b253bacfca5f319d54f2
        System.out.println(new BigInteger(1, result).toString(16));
    }
}
```

类似的，计算SHA-256，我们需要传入名称`"SHA-256"`，计算SHA-512，我们需要传入名称`"SHA-512"`

>  注意：MD5因为输出长度较短，短时间内破解是可能的，目前已经不推荐使用。



### 防窃听

#### 对称加密算法

对称加密算法就是传统的用一个密码进行加密和解密。常用的WinZIP和WinRAR对压缩包的加密和解密，就是使用对称加密算法

从程序的角度看，所谓加密，就是这样一个函数，它接收密码和明文，然后输出密文：

```java
secret = encrypt(key, message);
```

而解密则相反，它接收密码和密文，然后输出明文：

```java
plain = decrypt(key, secret);
```

在软件开发中，常用的对称加密算法有：

| 算法 | 密钥长度    | 工作模式             | 填充模式                                |
| :--- | :---------- | :------------------- | :-------------------------------------- |
| DES  | 56/64       | ECB/CBC/PCBC/CTR/... | NoPadding/PKCS5Padding/...              |
| AES  | 128/192/256 | ECB/CBC/PCBC/CTR/... | NoPadding/PKCS5Padding/PKCS7Padding/... |
| IDEA | 128         | ECB                  | PKCS5Padding/PKCS7Padding/...           |

密钥长度直接决定加密强度，而工作模式和填充模式可以看成是对称加密算法的参数和格式选择。Java标准库提供的算法实现并不包括所有的工作模式和所有填充模式，但是通常我们只需要挑选常用的使用就可以了。

最后注意，DES算法由于密钥过短，可以在短时间内被暴力破解，所以现在已经不安全了。

##### 使用AES加密

AES算法是目前应用最广泛的加密算法。我们先用ECB模式加密并解密：

```java
import java.security.*;
import java.util.Base64;

import javax.crypto.*;
import javax.crypto.spec.*;

public class Main {
    public static void main(String[] args) throws Exception {
        // 原文:
        String message = "Hello, world!";
        System.out.println("Message: " + message);
        // 128位密钥 = 16 bytes Key:
        byte[] key = "1234567890abcdef".getBytes("UTF-8");
        // 加密:
        byte[] data = message.getBytes("UTF-8");
        byte[] encrypted = encrypt(key, data);
        System.out.println("Encrypted: " + Base64.getEncoder().encodeToString(encrypted));
        // 解密:
        byte[] decrypted = decrypt(key, encrypted);
        System.out.println("Decrypted: " + new String(decrypted, "UTF-8"));
    }

    // 加密:
    public static byte[] encrypt(byte[] key, byte[] input) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance("AES/ECB/PKCS5Padding");
        SecretKey keySpec = new SecretKeySpec(key, "AES");
        cipher.init(Cipher.ENCRYPT_MODE, keySpec);
        return cipher.doFinal(input);
    }

    // 解密:
    public static byte[] decrypt(byte[] key, byte[] input) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance("AES/ECB/PKCS5Padding");
        SecretKey keySpec = new SecretKeySpec(key, "AES");
        cipher.init(Cipher.DECRYPT_MODE, keySpec);
        return cipher.doFinal(input);
    }
}
```

Java标准库提供的对称加密接口非常简单，使用时按以下步骤编写代码：

1. 根据算法名称/工作模式/填充模式获取Cipher实例；
2. 根据算法名称初始化一个SecretKey实例，密钥必须是指定长度；
3. 使用SerectKey初始化Cipher实例，并设置加密或解密模式；
4. 传入明文或密文，获得密文或明文。

ECB模式是最简单的AES加密模式，它只需要一个固定长度的密钥，固定的明文会生成固定的密文，这种一对一的加密方式会导致安全性降低，更好的方式是通过CBC模式，它需要一个随机数作为IV参数，这样对于同一份明文，每次生成的密文都不同：

```java
import java.security.*;
import java.util.Base64;
import javax.crypto.*;
import javax.crypto.spec.*;

public class Main {
    public static void main(String[] args) throws Exception {
        // 原文:
        String message = "Hello, world!";
        System.out.println("Message: " + message);
        // 256位密钥 = 32 bytes Key:
        byte[] key = "1234567890abcdef1234567890abcdef".getBytes("UTF-8");
        // 加密:
        byte[] data = message.getBytes("UTF-8");
        byte[] encrypted = encrypt(key, data);
        System.out.println("Encrypted: " + Base64.getEncoder().encodeToString(encrypted));
        // 解密:
        byte[] decrypted = decrypt(key, encrypted);
        System.out.println("Decrypted: " + new String(decrypted, "UTF-8"));
    }

    // 加密:
    public static byte[] encrypt(byte[] key, byte[] input) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        SecretKeySpec keySpec = new SecretKeySpec(key, "AES");
        // CBC模式需要生成一个16 bytes的initialization vector:
        SecureRandom sr = SecureRandom.getInstanceStrong();
        byte[] iv = sr.generateSeed(16);
        IvParameterSpec ivps = new IvParameterSpec(iv);
        cipher.init(Cipher.ENCRYPT_MODE, keySpec, ivps);
        byte[] data = cipher.doFinal(input);
        // IV不需要保密，把IV和密文一起返回:
        return join(iv, data);
    }

    // 解密:
    public static byte[] decrypt(byte[] key, byte[] input) throws GeneralSecurityException {
        // 把input分割成IV和密文:
        byte[] iv = new byte[16];
        byte[] data = new byte[input.length - 16];
        System.arraycopy(input, 0, iv, 0, 16);
        System.arraycopy(input, 16, data, 0, data.length);
        // 解密:
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        SecretKeySpec keySpec = new SecretKeySpec(key, "AES");
        IvParameterSpec ivps = new IvParameterSpec(iv);
        cipher.init(Cipher.DECRYPT_MODE, keySpec, ivps);
        return cipher.doFinal(data);
    }

    public static byte[] join(byte[] bs1, byte[] bs2) {
        byte[] r = new byte[bs1.length + bs2.length];
        System.arraycopy(bs1, 0, r, 0, bs1.length);
        System.arraycopy(bs2, 0, r, bs1.length, bs2.length);
        return r;
    }
}
```

在CBC模式下，需要一个随机生成的16字节IV参数，必须使用`SecureRandom`生成。因为多了一个`IvParameterSpec`实例，因此，初始化方法需要调用`Cipher`的一个重载方法并传入`IvParameterSpec`。

观察输出，可以发现每次生成的IV不同，密文也不同。

##### 小结

对称加密算法使用同一个密钥进行加密和解密，常用算法有DES、AES和IDEA等；

密钥长度由算法设计决定，AES的密钥长度是128/192/256位；

使用对称加密算法需要指定算法名称、工作模式和填充模式。

#### 口令加密算法

AES加密密钥长度是固定的128/192/256位，而不是用WinZip/WinRAR那样，随便输入几位都可以。

这是因为对称加密算法决定了口令必须是固定长度，然后对明文进行分块加密。又因为安全需求，口令长度往往都是128位以上，即至少16个字符。

但是我们平时使用的加密软件，输入6位、8位都可以，难道加密方式不一样？

实际上用户输入的口令并不能直接作为AES的密钥进行加密（除非长度恰好是128/192/256位），并且用户输入的口令一般都有规律，安全性远远不如安全随机数产生的随机口令。因此，用户输入的口令，通常还需要使用PBE算法，采用随机数杂凑计算出真正的密钥，再进行加密。

PBE就是Password Based Encryption的缩写，它的作用如下：

```
key = generate(userPassword, secureRandomPassword);
```

PBE的作用就是把用户输入的口令和一个安全随机的口令采用杂凑后计算出真正的密钥。以AES密钥为例，我们让用户输入一个口令，然后生成一个随机数，通过PBE算法计算出真正的AES口令，再进行加密，代码如下：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        // 把BouncyCastle作为Provider添加到java.security:
        Security.addProvider(new BouncyCastleProvider());
        // 原文:
        String message = "Hello, world!";
        // 加密口令:
        String password = "hello12345";
        // 16 bytes随机Salt:
        byte[] salt = SecureRandom.getInstanceStrong().generateSeed(16);
        System.out.printf("salt: %032x\n", new BigInteger(1, salt));
        // 加密:
        byte[] data = message.getBytes("UTF-8");
        byte[] encrypted = encrypt(password, salt, data);
        System.out.println("encrypted: " + Base64.getEncoder().encodeToString(encrypted));
        // 解密:
        byte[] decrypted = decrypt(password, salt, encrypted);
        System.out.println("decrypted: " + new String(decrypted, "UTF-8"));
    }

    // 加密:
    public static byte[] encrypt(String password, byte[] salt, byte[] input) throws GeneralSecurityException {
        PBEKeySpec keySpec = new PBEKeySpec(password.toCharArray());
        SecretKeyFactory skeyFactory = SecretKeyFactory.getInstance("PBEwithSHA1and128bitAES-CBC-BC");
        SecretKey skey = skeyFactory.generateSecret(keySpec);
        PBEParameterSpec pbeps = new PBEParameterSpec(salt, 1000);
        Cipher cipher = Cipher.getInstance("PBEwithSHA1and128bitAES-CBC-BC");
        cipher.init(Cipher.ENCRYPT_MODE, skey, pbeps);
        return cipher.doFinal(input);
    }

    // 解密:
    public static byte[] decrypt(String password, byte[] salt, byte[] input) throws GeneralSecurityException {
        PBEKeySpec keySpec = new PBEKeySpec(password.toCharArray());
        SecretKeyFactory skeyFactory = SecretKeyFactory.getInstance("PBEwithSHA1and128bitAES-CBC-BC");
        SecretKey skey = skeyFactory.generateSecret(keySpec);
        PBEParameterSpec pbeps = new PBEParameterSpec(salt, 1000);
        Cipher cipher = Cipher.getInstance("PBEwithSHA1and128bitAES-CBC-BC");
        cipher.init(Cipher.DECRYPT_MODE, skey, pbeps);
        return cipher.doFinal(input);
    }
}
```

使用PBE时，我们还需要引入BouncyCastle，并指定算法是`PBEwithSHA1and128bitAES-CBC-BC`。观察代码，实际上真正的AES密钥是调用`Cipher`的`init()`方法时同时传入`SecretKey`和`PBEParameterSpec`实现的。在创建`PBEParameterSpec`的时候，我们还指定了循环次数`1000`，循环次数越多，暴力破解需要的计算量就越大。

如果我们把salt和循环次数固定，就得到了一个通用的“口令”加密软件。如果我们把随机生成的salt存储在U盘，就得到了一个“口令”加USB Key的加密软件，它的好处在于，即使用户使用了一个非常弱的口令，没有USB Key仍然无法解密，因为USB Key存储的随机数密钥安全性非常高。

**小结**

PBE算法通过用户口令和安全的随机salt计算出Key，然后再进行加密；

Key通过口令和安全的随机salt计算得出，大大提高了安全性；

PBE算法内部使用的仍然是标准对称加密算法（例如AES）。

#### 密钥交换算法

对称加密算法解决了数据加密的问题。我们以AES加密为例，在现实世界中，小明要向路人甲发送一个加密文件，他可以先生成一个AES密钥，对文件进行加密，然后把加密文件发送给对方。因为对方要解密，就必须需要小明生成的密钥。

现在问题来了：如何传递密钥？

在不安全的信道上传递加密文件是没有问题的，因为黑客拿到加密文件没有用。但是，如何如何在不安全的信道上安全地传输密钥？

要解决这个问题，密钥交换算法即DH算法：Diffie-Hellman算法应运而生。

DH算法解决了密钥在双方不直接传递密钥的情况下完成密钥交换，这个神奇的交换原理完全由数学理论支持。

我们来看DH算法交换密钥的步骤。假设甲乙双方需要传递密钥，他们之间可以这么做：

1. 甲首选选择一个素数`p`，例如509，底数`g`，任选，例如5，随机数`a`，例如123，然后计算`A=g^a mod p`，结果是215，然后，甲发送`p＝509`，`g=5`，`A=215`给乙；
2. 乙方收到后，也选择一个随机数`b`，例如，456，然后计算`B=g^b mod p`，结果是181，乙再同时计算`s=A^b mod p`，结果是121；
3. 乙把计算的`B=181`发给甲，甲计算`s＝B^a mod p`的余数，计算结果与乙算出的结果一样，都是121。

所以最终双方协商出的密钥`s`是121。注意到这个密钥`s`并没有在网络上传输。而通过网络传输的`p`，`g`，`A`和`B`是无法推算出`s`的，因为实际算法选择的素数是非常大的。

所以，更确切地说，DH算法是一个密钥协商算法，双方最终协商出一个共同的密钥，而这个密钥不会通过网络传输。

如果我们把`a`看成甲的私钥，`A`看成甲的公钥，`b`看成乙的私钥，`B`看成乙的公钥，DH算法的本质就是双方各自生成自己的私钥和公钥，私钥仅对自己可见，然后交换公钥，并根据自己的私钥和对方的公钥，生成最终的密钥`secretKey`，DH算法通过数学定律保证了双方各自计算出的`secretKey`是相同的。

使用Java实现DH算法的代码如下：

```java
import java.math.BigInteger;
import java.security.*;
import java.security.spec.*;

import javax.crypto.KeyAgreement;

public class Main {
    public static void main(String[] args) {
        // Bob和Alice:
        Person bob = new Person("Bob");
        Person alice = new Person("Alice");

        // 各自生成KeyPair:
        bob.generateKeyPair();
        alice.generateKeyPair();

        // 双方交换各自的PublicKey:
        // Bob根据Alice的PublicKey生成自己的本地密钥:
        bob.generateSecretKey(alice.publicKey.getEncoded());
        // Alice根据Bob的PublicKey生成自己的本地密钥:
        alice.generateSecretKey(bob.publicKey.getEncoded());

        // 检查双方的本地密钥是否相同:
        bob.printKeys();
        alice.printKeys();
        // 双方的SecretKey相同，后续通信将使用SecretKey作为密钥进行AES加解密...
    }
}

class Person {
    public final String name;

    public PublicKey publicKey;
    private PrivateKey privateKey;
    private byte[] secretKey;

    public Person(String name) {
        this.name = name;
    }

    // 生成本地KeyPair:
    public void generateKeyPair() {
        try {
            KeyPairGenerator kpGen = KeyPairGenerator.getInstance("DH");
            kpGen.initialize(512);
            KeyPair kp = kpGen.generateKeyPair();
            this.privateKey = kp.getPrivate();
            this.publicKey = kp.getPublic();
        } catch (GeneralSecurityException e) {
            throw new RuntimeException(e);
        }
    }

    public void generateSecretKey(byte[] receivedPubKeyBytes) {
        try {
            // 从byte[]恢复PublicKey:
            X509EncodedKeySpec keySpec = new X509EncodedKeySpec(receivedPubKeyBytes);
            KeyFactory kf = KeyFactory.getInstance("DH");
            PublicKey receivedPublicKey = kf.generatePublic(keySpec);
            // 生成本地密钥:
            KeyAgreement keyAgreement = KeyAgreement.getInstance("DH");
            keyAgreement.init(this.privateKey); // 自己的PrivateKey
            keyAgreement.doPhase(receivedPublicKey, true); // 对方的PublicKey
            // 生成SecretKey密钥:
            this.secretKey = keyAgreement.generateSecret();
        } catch (GeneralSecurityException e) {
            throw new RuntimeException(e);
        }
    }

    public void printKeys() {
        System.out.printf("Name: %s\n", this.name);
        System.out.printf("Private key: %x\n", new BigInteger(1, this.privateKey.getEncoded()));
        System.out.printf("Public key: %x\n", new BigInteger(1, this.publicKey.getEncoded()));
        System.out.printf("Secret key: %x\n", new BigInteger(1, this.secretKey));
    }
}
```

但是DH算法并未解决中间人攻击，即甲乙双方并不能确保与自己通信的是否真的是对方。消除中间人攻击需要其他方法。

#### 非对称加密算法

从DH算法我们可以看到，公钥-私钥组成的密钥对是非常有用的加密方式，因为公钥是可以公开的，而私钥是完全保密的，由此奠定了非对称加密的基础。

非对称加密就是加密和解密使用的不是相同的密钥：只有同一个公钥-私钥对才能正常加解密。

因此，如果小明要加密一个文件发送给小红，他应该首先向小红索取她的公钥，然后，他用小红的公钥加密，把加密文件发送给小红，此文件只能由小红的私钥解开，因为小红的私钥在她自己手里，所以，除了小红，没有任何人能解开此文件。

非对称加密的典型算法就是RSA算法，它是由Ron Rivest，Adi Shamir，Leonard Adleman这三个哥们一起发明的，所以用他们仨的姓的首字母缩写表示。

非对称加密相比对称加密的显著优点在于，对称加密需要协商密钥，而非对称加密可以安全地公开各自的公钥，在N个人之间通信的时候：使用非对称加密只需要N个密钥对，每个人只管理自己的密钥对。而使用对称加密需要则需要`N*(N-1)/2`个密钥，因此每个人需要管理`N-1`个密钥，密钥管理难度大，而且非常容易泄漏。

既然非对称加密这么好，那我们抛弃对称加密，完全使用非对称加密行不行？也不行。因为非对称加密的缺点就是运算速度非常慢，比对称加密要慢很多。

所以，在实际应用的时候，非对称加密总是和对称加密一起使用。假设小明需要给小红需要传输加密文件，他俩首先交换了各自的公钥，然后：

1. 小明生成一个随机的AES口令，然后用小红的公钥通过RSA加密这个口令，并发给小红；
2. 小红用自己的RSA私钥解密得到AES口令；
3. 双方使用这个共享的AES口令用AES加密通信。

可见非对称加密实际上应用在第一步，即加密“AES口令”。这也是我们在浏览器中常用的HTTPS协议的做法，即浏览器和服务器先通过RSA交换AES口令，接下来双方通信实际上采用的是速度较快的AES对称加密，而不是缓慢的RSA非对称加密。

Java标准库提供了RSA算法的实现，示例代码如下：

```java
import java.math.BigInteger;
import java.security.*;
import javax.crypto.Cipher;

public class Main {
    public static void main(String[] args) throws Exception {
        // 明文:
        byte[] plain = "Hello, encrypt use RSA".getBytes("UTF-8");
        // 创建公钥／私钥对:
        Person alice = new Person("Alice");
        // 用Alice的公钥加密:
        byte[] pk = alice.getPublicKey();
        System.out.println(String.format("public key: %x", new BigInteger(1, pk)));
        byte[] encrypted = alice.encrypt(plain);
        System.out.println(String.format("encrypted: %x", new BigInteger(1, encrypted)));
        // 用Alice的私钥解密:
        byte[] sk = alice.getPrivateKey();
        System.out.println(String.format("private key: %x", new BigInteger(1, sk)));
        byte[] decrypted = alice.decrypt(encrypted);
        System.out.println(new String(decrypted, "UTF-8"));
    }
}

class Person {
    String name;
    // 私钥:
    PrivateKey sk;
    // 公钥:
    PublicKey pk;

    public Person(String name) throws GeneralSecurityException {
        this.name = name;
        // 生成公钥／私钥对:
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("RSA");
        kpGen.initialize(1024);
        KeyPair kp = kpGen.generateKeyPair();
        this.sk = kp.getPrivate();
        this.pk = kp.getPublic();
    }

    // 把私钥导出为字节
    public byte[] getPrivateKey() {
        return this.sk.getEncoded();
    }

    // 把公钥导出为字节
    public byte[] getPublicKey() {
        return this.pk.getEncoded();
    }

    // 用公钥加密:
    public byte[] encrypt(byte[] message) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.ENCRYPT_MODE, this.pk);
        return cipher.doFinal(message);
    }

    // 用私钥解密:
    public byte[] decrypt(byte[] input) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.DECRYPT_MODE, this.sk);
        return cipher.doFinal(input);
    }
}
```

RSA的公钥和私钥都可以通过`getEncoded()`方法获得以`byte[]`表示的二进制数据，并根据需要保存到文件中。要从`byte[]`数组恢复公钥或私钥，可以这么写：

```java
byte[] pkData = ...
byte[] skData = ...
KeyFactory kf = KeyFactory.getInstance("RSA");
// 恢复公钥:
X509EncodedKeySpec pkSpec = new X509EncodedKeySpec(pkData);
PublicKey pk = kf.generatePublic(pkSpec);
// 恢复私钥:
PKCS8EncodedKeySpec skSpec = new PKCS8EncodedKeySpec(skData);
PrivateKey sk = kf.generatePrivate(skSpec);
```

以RSA算法为例，它的密钥有256/512/1024/2048/4096等不同的长度。长度越长，密码强度越大，当然计算速度也越慢。

如果修改待加密的`byte[]`数据的大小，可以发现，使用512bit的RSA加密时，明文长度不能超过53字节，使用1024bit的RSA加密时，明文长度不能超过117字节，这也是为什么使用RSA的时候，总是配合AES一起使用，即用AES加密任意长度的明文，用RSA加密AES口令。

此外，只使用非对称加密算法不能防止中间人攻击。



### 防伪造

#### 签名算法

使用非对称加密算法的时候，对于一个公钥-私钥对，通常是用公钥加密，私钥解密。

如果使用私钥加密，公钥解密是否可行呢？实际上是完全可行的。

不过我们再仔细想一想，私钥是保密的，而公钥是公开的，用私钥加密，那相当于所有人都可以用公钥解密。这个加密有什么意义？

这个加密的意义在于，如果小明用自己的私钥加密了一条消息，比如`小明喜欢小红`，然后他公开了加密消息，由于任何人都可以用小明的公钥解密，从而使得任何人都可以确认`小明喜欢小红`这条消息肯定是小明发出的，其他人不能伪造这个消息，小明也不能抵赖这条消息不是自己写的。

因此，私钥加密得到的密文实际上就是数字签名，要验证这个签名是否正确，只能用私钥持有者的公钥进行解密验证。使用数字签名的目的是为了确认某个信息确实是由某个发送方发送的，任何人都不可能伪造消息，并且，发送方也不能抵赖。

在实际应用的时候，签名实际上并不是针对原始消息，而是针对原始消息的哈希进行签名，即：

```
signature = encrypt(privateKey, sha256(message))
```

对签名进行验证实际上就是用公钥解密：

```
hash = decrypt(publicKey, signature)
```

然后把解密后的哈希与原始消息的哈希进行对比。

因为用户总是使用自己的私钥进行签名，所以，私钥就相当于用户身份。而公钥用来给外部验证用户身份。

常用数字签名算法有：

- MD5withRSA
- SHA1withRSA
- SHA256withRSA

它们实际上就是指定某种哈希算法进行RSA签名的方式。

```java
import java.math.BigInteger;
import java.nio.charset.StandardCharsets;
import java.security.*;

public class Main {
    public static void main(String[] args) throws GeneralSecurityException {
        // 生成RSA公钥/私钥:
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("RSA");
        kpGen.initialize(1024);
        KeyPair kp = kpGen.generateKeyPair();
        PrivateKey sk = kp.getPrivate();
        PublicKey pk = kp.getPublic();

        // 待签名的消息:
        byte[] message = "Hello, I am Bob!".getBytes(StandardCharsets.UTF_8);

        // 用私钥签名:
        Signature s = Signature.getInstance("SHA1withRSA");
        s.initSign(sk);
        s.update(message);
        byte[] signed = s.sign();
        System.out.println(String.format("signature: %x", new BigInteger(1, signed)));

        // 用公钥验证:
        Signature v = Signature.getInstance("SHA1withRSA");
        v.initVerify(pk);
        v.update(message);
        boolean valid = v.verify(signed);
        System.out.println("valid? " + valid);
    }
}
```





使用其他公钥，或者验证签名的时候修改原始信息，都无法验证成功。

**DSA签名**

除了RSA可以签名外，还可以使用DSA算法进行签名。DSA是Digital Signature Algorithm的缩写，它使用ElGamal数字签名算法。

DSA只能配合SHA使用，常用的算法有：

- SHA1withDSA
- SHA256withDSA
- SHA512withDSA

和RSA数字签名相比，DSA的优点是更快。

**ECDSA签名**

椭圆曲线签名算法ECDSA：Elliptic Curve Digital Signature Algorithm也是一种常用的签名算法，它的特点是可以从私钥推出公钥。比特币的签名算法就采用了ECDSA算法，使用标准椭圆曲线secp256k1。BouncyCastle提供了ECDSA的完整实现。



#### 数字证书

摘要算法用来确保数据没有被篡改，非对称加密算法可以对数据进行加解密，签名算法可以确保数据完整性和抗否认性，把这些算法集合到一起，并搞一套完善的标准，这就是数字证书。

因此，数字证书就是集合了多种密码学算法，用于实现数据加解密、身份认证、签名等多种功能的一种安全标准。

数字证书可以防止中间人攻击，因为它采用链式签名认证，即通过根证书（Root CA）去签名下一级证书，这样层层签名，直到最终的用户证书。而Root CA证书内置于操作系统中，所以，任何经过CA认证的数字证书都可以对其本身进行校验，确保证书本身不是伪造的。

我们在上网时常用的HTTPS协议就是数字证书的应用。浏览器会自动验证证书的有效性

要使用数字证书，首先需要创建证书。正常情况下，一个合法的数字证书需要经过CA签名，这需要认证域名并支付一定的费用。开发的时候，我们可以使用自签名的证书，这种证书可以正常开发调试，但不能对外作为服务使用，因为其他客户端并不认可未经CA签名的证书。

注：[腾讯云](https://cloud.tencent.com/)可申请有效期1年的免费SSL证书，[Let's Encrypt](https://letsencrypt.org/)可申请有效期90天的免费SSL证书。

在Java程序中，数字证书存储在一种Java专用的key store文件中，JDK提供了一系列命令来创建和管理key store。我们用下面的命令创建一个key store，并设定口令123456：

```
keytool -storepass 123456 -genkeypair -keyalg RSA -keysize 1024 -sigalg SHA1withRSA -validity 3650 -alias mycert -keystore my.keystore -dname "CN=www.sample.com, OU=sample, O=sample, L=BJ, ST=BJ, C=CN"
```

几个主要的参数是：

- keyalg：指定RSA加密算法；
- sigalg：指定SHA1withRSA签名算法；
- validity：指定证书有效期3650天；
- alias：指定证书在程序中引用的名称；
- dname：最重要的`CN=www.sample.com`指定了`Common Name`，如果证书用在HTTPS中，这个名称必须与域名完全一致。

执行上述命令，JDK会在当前目录创建一个`my.keystore`文件，并存储创建成功的一个私钥和一个证书，它的别名是`mycert`。

有了key store存储的证书，我们就可以通过数字证书进行加解密和签名：

```java
import java.io.InputStream;
import java.math.BigInteger;
import java.security.*;
import java.security.cert.*;
import javax.crypto.Cipher;

public class Main {
    public static void main(String[] args) throws Exception {
        byte[] message = "Hello, use X.509 cert!".getBytes("UTF-8");
        // 读取KeyStore:
        KeyStore ks = loadKeyStore("/my.keystore", "123456");
        // 读取私钥:
        PrivateKey privateKey = (PrivateKey) ks.getKey("mycert", "123456".toCharArray());
        // 读取证书:
        X509Certificate certificate = (X509Certificate) ks.getCertificate("mycert");
        // 加密:
        byte[] encrypted = encrypt(certificate, message);
        System.out.println(String.format("encrypted: %x", new BigInteger(1, encrypted)));
        // 解密:
        byte[] decrypted = decrypt(privateKey, encrypted);
        System.out.println("decrypted: " + new String(decrypted, "UTF-8"));
        // 签名:
        byte[] sign = sign(privateKey, certificate, message);
        System.out.println(String.format("signature: %x", new BigInteger(1, sign)));
        // 验证签名:
        boolean verified = verify(certificate, message, sign);
        System.out.println("verify: " + verified);
    }

    static KeyStore loadKeyStore(String keyStoreFile, String password) {
        try (InputStream input = Main.class.getResourceAsStream(keyStoreFile)) {
            if (input == null) {
                throw new RuntimeException("file not found in classpath: " + keyStoreFile);
            }
            KeyStore ks = KeyStore.getInstance(KeyStore.getDefaultType());
            ks.load(input, password.toCharArray());
            return ks;
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

    static byte[] encrypt(X509Certificate certificate, byte[] message) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance(certificate.getPublicKey().getAlgorithm());
        cipher.init(Cipher.ENCRYPT_MODE, certificate.getPublicKey());
        return cipher.doFinal(message);
    }

    static byte[] decrypt(PrivateKey privateKey, byte[] data) throws GeneralSecurityException {
        Cipher cipher = Cipher.getInstance(privateKey.getAlgorithm());
        cipher.init(Cipher.DECRYPT_MODE, privateKey);
        return cipher.doFinal(data);
    }

    static byte[] sign(PrivateKey privateKey, X509Certificate certificate, byte[] message)
            throws GeneralSecurityException {
        Signature signature = Signature.getInstance(certificate.getSigAlgName());
        signature.initSign(privateKey);
        signature.update(message);
        return signature.sign();
    }

    static boolean verify(X509Certificate certificate, byte[] message, byte[] sig) throws GeneralSecurityException {
        Signature signature = Signature.getInstance(certificate.getSigAlgName());
        signature.initVerify(certificate);
        signature.update(message);
        return signature.verify(sig);
    }
}
```

在上述代码中，我们从key store直接读取了私钥-公钥对，私钥以`PrivateKey`实例表示，公钥以`X509Certificate`表示，实际上数字证书只包含公钥，因此，读取证书并不需要口令，只有读取私钥才需要。如果部署到Web服务器上，例如Nginx，需要把私钥导出为Private Key格式，把证书导出为X509Certificate格式。

以HTTPS协议为例，浏览器和服务器建立安全连接的步骤如下：

1. 浏览器向服务器发起请求，服务器向浏览器发送自己的数字证书；
2. 浏览器用操作系统内置的Root CA来验证服务器的证书是否有效，如果有效，就使用该证书加密一个随机的AES口令并发送给服务器；
3. 服务器用自己的私钥解密获得AES口令，并在后续通讯中使用AES加密。

上述流程只是一种最常见的单向验证。如果服务器还要验证客户端，那么客户端也需要把自己的证书发送给服务器验证，这种场景常见于网银等。

注意：数字证书存储的是公钥，以及相关的证书链和算法信息。私钥必须严格保密，如果数字证书对应的私钥泄漏，就会造成严重的安全威胁。如果CA证书的私钥泄漏，那么该CA证书签发的所有证书将不可信。数字证书服务商[DigiNotar](https://en.wikipedia.org/wiki/DigiNotar)就发生过私钥泄漏导致公司破产的事故。



# 反射与注解

## 反射

### 测试框架

单元测试的经典框架：Junit，是 Java 语言编写的第三方单元测试框架

单元测试：

* 单元：在 Java 中，一个类就是一个单元
* 单元测试：Junit 编写的一小段代码，用来对某个类中的某个方法进行功能测试或业务逻辑测试	

Junit 单元测试框架的作用：

* 用来对类中的方法功能进行有目的的测试，以保证程序的正确性和稳定性
* 能够**独立的**测试某个方法或者所有方法的预期正确性

测试方法注意事项：**必须是 public 修饰的，没有返回值，没有参数，使用注解@Test修饰**

Junit常用注解（Junit 4.xxxx 版本），@Test 测试方法：

* @Before：用来修饰实例方法，该方法会在每一个测试方法执行之前执行一次
* @After：用来修饰实例方法，该方法会在每一个测试方法执行之后执行一次
* @BeforeClass：用来静态修饰方法，该方法会在所有测试方法之前**只**执行一次
* @AfterClass：用来静态修饰方法，该方法会在所有测试方法之后**只**执行一次

Junit 常用注解（Junit5.xxxx 版本），@Test 测试方法：

* @BeforeEach：用来修饰实例方法，该方法会在每一个测试方法执行之前执行一次
* @AfterEach：用来修饰实例方法，该方法会在每一个测试方法执行之后执行一次
* @BeforeAll：用来静态修饰方法，该方法会在所有测试方法之前只执行一次
* @AfterAll：用来静态修饰方法，该方法会在所有测试方法之后只执行一次

作用：

* 开始执行的方法：初始化资源
* 执行完之后的方法：释放资源

```java
public class UserService {
    public String login(String loginName , String passWord){
        if("admin".equals(loginName)&&"123456".equals(passWord)){
            return "success";
        }
        return "用户名或者密码错误！";
    }
    public void chu(int a , int b){
        System.out.println(a / b);
    }
}
```

```java
//测试方法的要求：1.必须public修饰 2.没有返回值没有参数 3. 必须使注解@Test修饰
public class UserServiceTest {
     // @Before：用来修饰实例方法，该方法会在每一个测试方法执行之前执行一次。
    @Before
    public void before(){
        System.out.println("===before===");
    }
    // @After：用来修饰实例方法，该方法会在每一个测试方法执行之后执行一次。
    @After
    public void after(){
        System.out.println("===after===");
    }
    // @BeforeClass：用来静态修饰方法，该方法会在所有测试方法之前只执行一次。
    @BeforeClass
    public static void beforeClass(){
        System.out.println("===beforeClass===");
    }
    // @AfterClass：用来静态修饰方法，该方法会在所有测试方法之后只执行一次。
    @AfterClass
    public static void afterClass(){
        System.out.println("===afterClass===");
    }
    @Test
    public void testLogin(){
        UserService userService = new UserService();
        String rs = userService.login("admin","123456");
        /**断言预期结果的正确性。
         * 参数一：测试失败的提示信息。
         * 参数二：期望值。
         * 参数三：实际值
         */
        Assert.assertEquals("登录业务功能方法有错误，请检查！","success",rs);
    }
    @Test
    public void testChu(){
        UserService userService = new UserService();
        userService.chu(10 , 0);
    }
}
```





****



### 介绍反射

反射是指对于任何一个类，在"运行的时候"都可以直接得到这个类全部成分

* 构造器对象：Constructor
* 成员变量对象：Field

* 成员方法对象：Method

核心思想：在运行时获取类编译后的**字节码文件对象**，然后解析类中的全部成分

反射提供了一个 Class 类型：HelloWorld.java → javac → HelloWorld.class

* `Class c = HelloWorld.class` 

注意：反射是工作在**运行时**的技术，只有运行之后才会有 class 类对象

作用：可以在运行时得到一个类的全部成分然后操作，破坏封装性，也可以破坏泛型的约束性。

反射的优点：

- 可扩展性：应用程序可以利用全限定名创建可扩展对象的实例，来使用来自外部的用户自定义类
- 类浏览器和可视化开发环境：一个类浏览器需要可以枚举类的成员，可视化开发环境（如 IDE）可以从利用反射中可用的类型信息中受益，以帮助程序员编写正确的代码
- 调试器和测试工具： 调试器需要能够检查一个类里的私有成员，测试工具可以利用反射来自动地调用类里定义的可被发现的 API 定义，以确保一组测试中有较高的代码覆盖率

反射的缺点：

- **性能开销**：反射涉及了动态类型的解析，所以 JVM 无法对这些代码进行优化，反射操作的效率要比那些非射操作低得多，应该避免在经常被执行的代码或对性能要求很高的程序中使用反射
- 安全限制：使用反射技术要求程序必须在一个没有安全限制的环境中运行，如果一个程序必须在有安全限制的环境中运行
- 内部暴露：由于反射允许代码执行一些在正常情况下不被允许的操作（比如访问私有的属性和方法），所以使用反射可能会导致意料之外的副作用，这可能导致代码功能失调并破坏可移植性。反射代码破坏了抽象性，因此当平台发生改变的时候，代码的行为就有可能也随着变化



***



### 获取元素

#### 获取类

反射技术的第一步是先得到 Class 类对象，有三种方式获取：

* 类名.class
* 类的对象.getClass()
* Class.forName("类的全限名")：`public static Class<?> forName(String className) `

Class 类下的方法：

| 方法                   | 作用                                                         |
| ---------------------- | ------------------------------------------------------------ |
| String getSimpleName() | 获得类名字符串：类名                                         |
| String getName()       | 获得类全名：包名+类名                                        |
| T newInstance()        | 创建 Class 对象关联类的对象，底层是调用无参数构造器，已经被淘汰 |

```java
public class ReflectDemo{
    public static void main(String[] args) throws Exception {
        // 反射的第一步永远是先得到类的Class文件对象: 字节码文件。
        // 1.类名.class
        Class c1 = Student.class;
        System.out.println(c1);//class _03反射_获取Class类对象.Student

        // 2.对象.getClass()
        Student swk = new Student();
        Class c2 = swk.getClass();
        System.out.println(c2);

        // 3.Class.forName("类的全限名")
        // 直接去加载该类的class文件。
        Class c3 = Class.forName("_03反射_获取Class类对象.Student");
        System.out.println(c3);

        System.out.println(c1.getSimpleName()); // 获取类名本身（简名）Student
        System.out.println(c1.getName()); //获取类的全限名_03反射_获取Class类对象.Student
    }
}
class Student{}
```



***



#### 获取构造

获取构造器的 API：

* Constructor getConstructor(Class... parameterTypes)：根据参数匹配获取某个构造器，只能拿 public 修饰的构造器
* Constructor getDeclaredConstructor(Class... parameterTypes)：根据参数匹配获取某个构造器，只要申明就可以定位，不关心权限修饰符
* Constructor[] getConstructors()：获取所有的构造器，只能拿 public 修饰的构造器
* Constructor[] getDeclaredConstructors()：获取所有构造器，只要申明就可以定位，不关心权限修饰符

Constructor 的常用 API：

| 方法                              | 作用                                    |
| --------------------------------- | --------------------------------------- |
| T newInstance(Object... initargs) | 创建对象，注入构造器需要的数据          |
| void setAccessible(true)          | 修改访问权限，true 攻破权限（暴力反射） |
| String getName()                  | 以字符串形式返回此构造函数的名称        |
| int getParameterCount()           | 返回参数数量                            |
| Class<?>[] getParameterTypes      | 返回参数类型数组                        |

```java
public class TestStudent01 {
    @Test
    public void getDeclaredConstructors(){
        // a.反射第一步先得到Class类对象
        Class c = Student.class ;
        // b.定位全部构造器，只要申明了就可以拿到
        Constructor[] cons = c.getDeclaredConstructors();
        // c.遍历这些构造器
        for (Constructor con : cons) {
            System.out.println(con.getName()+"->"+con.getParameterCount());
        }
    }
    @Test
    public void getDeclaredConstructor() throws Exception {
        // a.反射第一步先得到Class类对象
        Class c = Student.class ;
        // b.定位某个构造器，根据参数匹配，只要申明了就可以获取
        //Constructor con = c.getDeclaredConstructor(); // 可以拿到！定位无参数构造器！
        Constructor con = c.getDeclaredConstructor(String.class, int.class); //有参数的！!
        // c.构造器名称和参数
        System.out.println(con.getName()+"->"+con.getParameterCount());
    }
}
```

```java
public class Student {
    private String name ;
    private int age ;
    private Student(){
        System.out.println("无参数构造器被执行~~~~");
    }
    public Student(String name, int age) {
        System.out.println("有参数构造器被执行~~~~");
        this.name = name;
        this.age = age;
    }
}
```

```java
//测试方法
public class TestStudent02 {
    // 1.调用无参数构造器得到一个类的对象返回。
    @Test
    public void createObj01() throws Exception {
        // a.反射第一步是先得到Class类对象
        Class c = Student.class ;
        // b.定位无参数构造器对象
        Constructor constructor = c.getDeclaredConstructor();
        // c.暴力打开私有构造器的访问权限
        constructor.setAccessible(true);
        // d.通过无参数构造器初始化对象返回
        Student swk = (Student) constructor.newInstance(); // 最终还是调用无参数构造器的！
        System.out.println(swk);//Student{name='null', age=0}
    }

    // 2.调用有参数构造器得到一个类的对象返回。
    @Test
    public void createObj02() throws Exception {
        // a.反射第一步是先得到Class类对象
        Class c = Student.class ;
        // b.定位有参数构造器对象
        Constructor constructor = c.getDeclaredConstructor(String.class , int.class);
        // c.通过无参数构造器初始化对象返回
        Student swk = (Student) constructor.newInstance("孙悟空",500); // 最终还是调用有参数构造器的！
        System.out.println(swk);//Student{name='孙悟空', age=500}
    }
}


```



***



#### 获取变量

获取 Field 成员变量 API：

* Field getField(String name)：根据成员变量名获得对应 Field 对象，只能获得 public 修饰
* Field getDeclaredField(String name)：根据成员变量名获得对应 Field 对象，所有申明的变量
* Field[] getFields()：获得所有的成员变量对应的 Field 对象，只能获得 public 的
* Field[] getDeclaredFields()：获得所有的成员变量对应的 Field 对象，只要申明了就可以得到 

Field 的方法：给成员变量赋值和取值

| 方法                               | 作用                                                        |
| ---------------------------------- | ----------------------------------------------------------- |
| void set(Object obj, Object value) | 给对象注入某个成员变量数据，**obj 是对象**，value 是值      |
| Object get(Object obj)             | 获取指定对象的成员变量的值，**obj 是对象**，没有对象为 null |
| void setAccessible(true)           | 暴力反射，设置为可以直接访问私有类型的属性                  |
| Class getType()                    | 获取属性的类型，返回 Class 对象                             |
| String getName()                   | 获取属性的名称                                              |

```Java
public class FieldDemo {
    //获取全部成员变量
    @Test
    public void getDeclaredFields(){
        // a.先获取class类对象
        Class c = Dog.class;
        // b.获取全部申明的成员变量对象
        Field[] fields = c.getDeclaredFields();
        for (Field field : fields) {
            System.out.println(field.getName()+"->"+field.getType());
        }
    }
    //获取某个成员变量
    @Test
    public void getDeclaredField() throws Exception {
        // a.先获取class类对象
        Class c = Dog.class;
        // b.定位某个成员变量对象 :根据名称定位！！
        Field ageF = c.getDeclaredField("age");
        System.out.println(ageF.getName()+"->"+ageF.getType());
    }
}
```

```java
public class Dog {
    private String name;
    private int age ;
    private String color ;
    public static String school;
    public static final String SCHOOL_1 = "宠物学校";

    public Dog() {
    }

    public Dog(String name, int age, String color) {
        this.name = name;
        this.age = age;
        this.color = color;
    }
}
```

```java
//测试方法
public class FieldDemo02 {
    @Test
    public void setField() throws Exception {
        // a.反射的第一步获取Class类对象
        Class c = Dog.class ;
        // b.定位name成员变量
        Field name = c.getDeclaredField("name");
        // c.为这个成员变量赋值！
        Dog d = new Dog();
        name.setAccessible(true);
        name.set(d,"泰迪");
        System.out.println(d);//Dog{name='泰迪', age=0, color='null'}
        // d.获取成员变量的值
        String value = name.get(d)+"";
        System.out.println(value);//泰迪
    }
}
```



***



#### 获取方法

获取 Method 方法 API：

* Method getMethod(String name,Class...args)：根据方法名和参数类型获得方法对象，public 修饰
* Method getDeclaredMethod(String name,Class...args)：根据方法名和参数类型获得方法对象，包括 private
* Method[] getMethods()：获得类中的所有成员方法对象返回数组，只能获得 public 修饰且包含父类的
* Method[] getDeclaredMethods()：获得类中的所有成员方法对象，返回数组，只获得本类申明的方法

Method 常用 API：

* public Object invoke(Object obj, Object... args)：使用指定的参数调用由此方法对象，obj 对象名

```java
public class MethodDemo{
    //获得类中的所有成员方法对象
    @Test
    public void getDeclaredMethods(){
        // a.先获取class类对象
        Class c = Dog.class ;
        // b.获取全部申明的方法!
        Method[] methods = c.getDeclaredMethods();
        // c.遍历这些方法
        for (Method method : methods) {
            System.out.println(method.getName()+"->"
                    + method.getParameterCount()+"->" + method.getReturnType());
        }
    }
    @Test
    public void getDeclardMethod() throws Exception {
        Class c = Dog.class;
        Method run = c.getDeclaredMethod("run");
        // c.触发方法执行!
        Dog d = new Dog();
        Object o = run.invoke(d);
        System.out.println(o);// 如果方法没有返回值，结果是null
        
		//参数一：方法名称   参数二：方法的参数个数和类型(可变参数！)
        Method eat = c.getDeclaredMethod("eat",String.class);
        eat.setAccessible(true); // 暴力反射！
        
       	//参数一：被触发方法所在的对象  参数二：方法需要的入参值
        Object o1 = eat.invoke(d,"肉");
        System.out.println(o1);// 如果方法没有返回值，结果是null
    }
}

public class Dog {
    private String name ;
    public Dog(){
    }
    public void run(){System.out.println("狗跑的贼快~~");}
	private void eat(){System.out.println("狗吃骨头");}
	private void eat(String name){System.out.println("狗吃"+name);}
	public static void inAddr(){System.out.println("在吉山区有一只单身狗！");}
}
```



***



### 暴力攻击

泛型只能工作在编译阶段，运行阶段泛型就消失了，反射工作在运行时阶段

1. 反射可以破坏面向对象的封装性（暴力反射）
2. 同时可以破坏泛型的约束性

```java
public class ReflectDemo {
    public static void main(String[] args) throws Exception {
        List<Double> scores = new ArrayList<>();
        scores.add(99.3);
        scores.add(199.3);
        scores.add(89.5);
        // 拓展：通过反射暴力的注入一个其他类型的数据进去。
        // a.先得到集合对象的Class文件对象
        Class c = scores.getClass();
        // b.从ArrayList的Class对象中定位add方法
        Method add = c.getDeclaredMethod("add", Object.class);
        // c.触发scores集合对象中的add执行（运行阶段，泛型不能约束了）
        add.invoke(scores,"波仔");
        System.out.println(scores);
    }
}
```

 



***





## 注解

### 概念

注解：类的组成部分，可以给类携带一些额外的信息，提供一种安全的类似注释标记的机制，用来将任何信息或元数据（metadata）与程序元素（类、方法、成员变量等）进行关联

* 注解是给编译器或 JVM 看的，编译器或 JVM 可以根据注解来完成对应的功能
* 注解类似修饰符，应用于包、类型、构造方法、方法、成员变量、参数及本地变量的声明语句中
* **父类中的注解是不能被子类继承的**

注解作用：

* 标记
* 框架技术多半都是在使用注解和反射，都是属于框架的底层基础技术
* 在编译时进行格式检查，比如方法重写约束 @Override、函数式接口约束 @FunctionalInterface.



***



### 注解格式

定义格式：自定义注解用 @interface 关键字，注解默认可以标记很多地方

```java
修饰符 @interface 注解名{
     // 注解属性
}
```

使用注解的格式：@注解名

```java
@Book
@MyTest
public class MyBook {
    //方法变量都可以注解
}

@interface Book{
}
@interface MyTest{
}
```



***



### 注解属性

#### 普通属性

注解可以有属性，**属性名必须带 ()**，在用注解的时候，属性必须赋值，除非属性有默认值

属性的格式：

* 格式 1：数据类型 属性名()
* 格式 2：数据类型 属性名() default 默认值

属性适用的数据类型:

* 八种数据数据类型（int，short，long，double，byte，char，boolean，float）和 String、Class
* 以上类型的数组形式都支持

```java
@MyBook(name="《精通Java基础》",authors = {"播仔","Dlei","播妞"} , price = 99.9 )
public class AnnotationDemo01 {
    @MyBook(name="《精通MySQL数据库入门到删库跑路》",authors = {"小白","小黑"} ,
     					price = 19.9 , address = "北京")
    public static void main(String[] args) {
    }
}
// 自定义一个注解
@interface MyBook{
    String name();
    String[] authors(); // 数组
    double price();
    String address() default "武汉";
}

```



***



#### 特殊属性

注解的特殊属性名称：value

* 如果只有一个 value 属性的情况下，使用 value 属性的时候可以省略 value 名称不写
* 如果有多个属性，且多个属性没有默认值，那么 value 是不能省略的

```java
//@Book("/deleteBook.action")
@Book(value = "/deleteBook.action" , age = 12)
public class AnnotationDemo01{
}

@interface Book{
    String value();
    int age() default 10;
}
```



***



### 元注解

元注解是 sun 公司提供的，用来注解自定义注解

元注解有四个：

* @Target：约束自定义注解可以标记的范围，默认值为任何元素，表示该注解用于什么地方，可用值定义在 ElementType 类中：

  - `ElementType.CONSTRUCTOR`：用于描述构造器
  - `ElementType.FIELD`：成员变量、对象、属性（包括 enum 实例）
  - `ElementType.LOCAL_VARIABLE`：用于描述局部变量
  - `ElementType.METHOD`：用于描述方法
  - `ElementType.PACKAGE`：用于描述包
  - `ElementType.PARAMETER`：用于描述参数
  - `ElementType.TYPE`：用于描述类、接口（包括注解类型）或 enum 声明

* @Retention：定义该注解的生命周期，申明注解的作用范围：编译时，运行时，可使用的值定义在 RetentionPolicy 枚举类中：

  - `RetentionPolicy.SOURCE`：在编译阶段丢弃，这些注解在编译结束之后就不再有任何意义，只作用在源码阶段，生成的字节码文件中不存在，`@Override`、`@SuppressWarnings` 都属于这类注解
  - `RetentionPolicy.CLASS`：在类加载时丢弃，在字节码文件的处理中有用，运行阶段不存在，默认值
  - `RetentionPolicy.RUNTIME` : 始终不会丢弃，运行期也保留该注解，因此可以使用反射机制读取该注解的信息，自定义的注解通常使用这种方式

* @Inherited：表示修饰的自定义注解可以被子类继承

* @Documented：表示是否将自定义的注解信息添加在 Java 文档中

```java
public class AnnotationDemo01{
    // @MyTest // 只能注解方法
    private String name;

    @MyTest
    public static void main( String[] args) {
    }
}
@Target(ElementType.METHOD) // 申明只能注解方法
@Retention(RetentionPolicy.RUNTIME) // 申明注解从写代码一直到运行还在，永远存活！！
@interface MyTest{
}
```



***



### 注解解析

开发中经常要知道一个类的成分上面到底有哪些注解，注解有哪些属性数据，这都需要进行注解的解析

注解解析相关的接口：

* Annotation：注解类型，该类是所有注解的父类，注解都是一个 Annotation 的对象
* AnnotatedElement：该接口定义了与注解解析相关的方法
* Class、Method、Field、Constructor 类成分：实现 AnnotatedElement 接口，拥有解析注解的能力

Class 类 API ：

* `Annotation[] getDeclaredAnnotations()`：获得当前对象上使用的所有注解，返回注解数组
* `T getDeclaredAnnotation(Class<T> annotationClass)`：根据注解类型获得对应注解对象
* `T getAnnotation(Class<T> annotationClass)`：根据注解类型获得对应注解对象
* `boolean isAnnotationPresent(Class<Annotation> class)`：判断对象是否使用了指定的注解
* `boolean isAnnotation()`：此 Class 对象是否表示注释类型

注解原理：注解本质是**特殊接口**，继承了 `Annotation` ，其具体实现类是 Java 运行时生成的**动态代理类**，通过反射获取注解时，返回的是运行时生成的动态代理对象 `$Proxy1`，通过代理对象调用自定义注解（接口）的方法，回调 `AnnotationInvocationHandler` 的 `invoke` 方法，该方法会从 `memberValues`  这个 Map 中找出对应的值，而 `memberValues` 的来源是 Java 常量池

解析注解数据的原理：注解在哪个成分上，就先拿哪个成分对象，比如注解作用在类上，则要该类的 Class 对象，再来拿上面的注解

```java
public class AnnotationDemo{
    @Test
    public void parseClass() {
        // 1.定位Class类对象
        Class c = BookStore.class;
        // 2.判断这个类上是否使用了某个注解
        if(c.isAnnotationPresent(Book.class)){
            // 3.获取这个注解对象
            Book b = (Book)c.getDeclarAnnotation(Book.class);
            System.out.println(book.value());
            System.out.println(book.price());
            System.out.println(Arrays.toString(book.authors()));
        }
    }
    @Test
    public void parseMethod() throws Exception {
        Class c = BookStore.class;
        Method run = c.getDeclaredMethod("run");
        if(run.isAnnotationPresent(Book.class)){
            Book b = (Book)run.getDeclaredAnnotation(Book.class);
           	sout(上面的三个);
        }
    }
}

@Book(value = "《Java基础到精通》", price = 99.5, authors = {"波仔","波妞"})
class BookStore{
    @Book(value = "《Mybatis持久层框架》", price = 199.5, authors = {"dlei","播客"})
    public void run(){
    }
}
@Target({ElementType.TYPE,ElementType.METHOD}) // 类和成员方法上使用
@Retention(RetentionPolicy.RUNTIME) // 注解永久存活
@interface Book{
    String value();
    double price() default 100;
    String[] authors();
}
```



***



### 注解模拟

注解模拟写一个 Junit 框架的基本使用

1. 定义一个自定义注解 MyTest，只能注解方法，存活范围一直都在。
2. 定义若干个方法，只要有 @MyTest 注解的方法就能被触发执行，没有这个注解的方法不能执行！！

```java
public class TestDemo{
    @MyTest
    public void test01(){System.out.println("===test01===");}
    public void test02(){System.out.println("===test02===");}
    @MyTest
    public void test03(){System.out.println("===test03===");}
    @MyTest
    public void test04(){System.out.println("===test04===");}
    
    public static void main(String[] args) throws Exception {
        TestDemo t = new TestDemo();
        Class c = TestDemo.class;
        Method[] methods = c.getDeclaredMethods();
        for (Method method : methods) {
            if(method.isAnnotationPresent(MyTest.class)){
                method.invoke(t);
            }
        }
    }
}

@Target(ElementType.METHOD) // 只能注解方法！
@Retention(RetentionPolicy.RUNTIME) // 一直都活着
@interface MyTest{
}
```



