# Lesson 1  Java的环境设置、数据类型、运算符和输入和输出

## 目录

1. [Java环境配置](#1-Java环境配置)
   - [1.1 Java下载](#11-Java下载)
   - [1.2 Java安装](#12-Java安装)
   - [1.3 Java配置](#13-Java配置)
     - [1.3.1 Mac 系统电脑](#131-Mac-系统电脑)
     - [1.3.2 Windows 系统电脑](#132-Windows-系统电脑)
   - [1.4 验证结果](#14-验证结果)
   - [1.5 Java编译&运行](#15-java编译运行)

2. [第一个程序：Hello World！](#2-第一个程序hello-world)

3. [Java常用的集成开发环境（IDE）](#3-java常用的集成开发环境ide)
   - [3.1 IntelliJ IDEA（推荐）](#31-intellij-idea推荐)
   - [3.2 Eclipse](#32-eclipse)
   - [3.3 样例展示](#33-样例展示)

4. [Java中的标识符](#4-Java中的标识符)
   - [4.1 标识符](#41-标识符)
   - [4.2 关键字和保留字](#42-关键字和保留字)

5. [Java中的变量](#5-Java中的变量)
   - [5.1 什么是变量](#51-什么是变量)
   - [5.2 变量的声明](#52-变量的声明)
   - [5.3 变量的初始化](#53-变量的初始化)
   - [5.4 变量的访问](#54-变量的访问)

6. [Java的数据类型](#6-Java的数据类型)
   - [6.1 基本数据类型](#61-基本数据类型)
     - [6.1.1 整数类型](#611-整数类型)
     - [6.1.2 浮点类型](#612-浮点类型)
     - [6.1.3 字符类型](#613-字符类型)
     - [6.1.4 布尔类型](#614-布尔类型)
   - [6.2 引用数据类型](#62-引用数据类型)
     - [6.2.1 字符串类型](#621-字符串类型)
   - [6.3 常用数据类型的使用实例](#63-常用数据类型的使用实例)

7. [Java中的运算符](#7-Java中的运算符)
   - [7.1 算术运算符](#71-算术运算符)
   - [7.2 赋值运算符](#72-赋值运算符)
   - [7.3 比较运算符](#73-比较运算符)
   - [7.4 逻辑运算符](#74-逻辑运算符)
   - [7.5 条件（三目）运算符](#75-条件三目运算符)
   - [7.6 位运算符](#76-位运算符)
8. [Java的输入与输出](#8-java的输入与输出)
    - [8.1 使用scanner读取字符串整数浮点数](#81-使用-scanner-读取字符串整数浮点数)
    - [8.2 System.out.println()](#82-systemoutprintln)
    - [8.3 System.out.print()](#83-systemoutprint)
    - [8.4 InputStream/OutputStream](#84-inputstreamoutputstream)
9. [课后总结及练习](#9-课程总结)
    
## 前言：为什么要学习Java

- Java是一门功能强大且简单易用的面向对象编程语言**，‌它具有多种特点，‌包括简单性、‌面向对象、‌分布式、‌健壮性、‌安全性、‌平台独立与可移植性、‌多线程以及动态性。‌
- Java可以用于编写桌面应用程序、‌Web应用程序、‌分布式系统和嵌入式系统应用程序等多种类型的应用程序。‌Java的独立于平台的特点，‌即“一次编写，‌到处运行”（‌Write Once, Run Anywhere，‌简称WORA）‌，‌是其最大的优势之一，‌这使得Java应用程序可以在多个平台上运行，‌而无需对每个平台进行单独的编译。


- 本文档涉及范围对标大学计算机大一入门课程，帮助大学学生以及准备学习算法竞赛的初高中生，入门Java编程语言，通过针对性算法训练掌握语法和基础算法，为下一阶段学习做准备。
## 1. Java环境配置

### 1.1 Java下载

Java 官方下载地址：[https://www.oracle.com/java/technologies/downloads/](https://www.oracle.com/java/technologies/downloads/)

点击上方链接即可跳转到官网下载界面，根据需要选择对应配置进行下载！
![](https://markdown.liuchengtu.com/work/uploads/upload_0261bf205472cdecb31b81cdb147b4de.png)


### 1.2 Java安装

对于 Windows 和 Mac 来说，Java 的安装步骤很简单，我们可以选择对应的安装程序（.exe/.dmg）然后根据步骤来进行安装：

- Mac 系统的默认安装路径为下述地址：
    ```shell
    ~/Library/Java/JavaVirtualMachines/
    ```
- Windows 在安装时注意指定好安装路径即可

    
### 1.3 Java配置

#### 1.3.1 Mac 系统电脑
- 对于Mac 系列电脑，如果是第一次安装，在下载安装JDK后系统会自动进行配置Java环境，直接根据指引安装即可，安装完毕后跳转至步骤1.4。

![](https://markdown.liuchengtu.com/work/uploads/upload_905b7be0d3ccae79fa56c627226b6897.png)
![](https://markdown.liuchengtu.com/work/uploads/upload_bda8492d28a8dadcfda4099f549da1a0.png)


注意，如果安装了多个版本的JDK，就需要手动配置Java的环境变量。要配置`$JAVA_HOME`环境变量，找到以下三个配置文件中的任意一个：
```shell
~/.bash_profile
~/.bashrc
~/.zshrc
```
- 添加下面这行代码：
    ```shell
    # 以 Java8 举例，其中 "JAVA_HOME=" 后面是 你的Java JDK 的实际安装地址，需要根据实际情况修改
    export JAVA_HOME=/Users/xxx/Library/Java/JavaVirtualMachines/corretto-1.8.0_332
    export PATH=$JAVA_HOME/bin:$PATH:.
    export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib
    ``` 

#### 1.3.2 Windows 系统电脑
- 对于 windows 系统：

    打开系统设置，点击高级系统设置，打开环境变量以后点击系统变量的新建：新建 JAVA_HOME 变量（单词大写，符合是英文），如果是用默认安装路径可以直接复制使用：
    ![](https://markdown.liuchengtu.com/work/uploads/upload_a9c6b983008cc1a9b9071be7a49fa940.png)

    找到系统变量中的 Path 变量，选中然后点击编辑，然后点击新建，这里都一样，可以直接复制使用：
    ```shell
    %JAVA_HOME%\bin
    %JAVA_HOME%\jre\bin
    ``` 
    ![](https://markdown.liuchengtu.com/work/uploads/upload_0c89d96c23b480ab24589992452f9134.png)

    
### 1.4 验证结果

- 打开终端，输入`java -version`，查看安装版本，输入`javac -version`验证JRE环境，代表配置安装完成。
![](https://markdown.liuchengtu.com/work/uploads/upload_2c984c9ef0127f72e2d31fd32ca76d45.png)

### 1.5 Java编译&运行

#### Java的运行过程

Java 程序的运行必须经过编写、编译和运行 3 个步骤。

- 编写：在 Java 开发环境中编写程序代码，形成后缀名为 .java 的 Java 源文件。
- 编译：使用 Java 编译器（javac 命令）对源文件进行编译，如果源代码中没有语法错误，编译器会生成后缀名为 .class 的字节码文件。这个字节码文件是跨平台的，可以在任何安装了 Java 运行环境（JRE）的机器上运行。
- 运行：使用 Java 解释器（java 命令）对字节码文件进行解释运行，将字节码翻译成机器代码并执行，最后显示运行结果。这个过程中，Java 的跨平台特性得到了充分体现，即"一次编写，到处运行"。

    ![](https://markdown.liuchengtu.com/work/uploads/upload_5584d3220ab8c18657844e04696b8aaf.png)


## 2. 第一个程序：Hello World！

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
将以上代码保存为`HelloWorld.java`文件。

然后，我们使用 Java 编译器`javac`对源文件进行编译：

对于Mac系统，打开 `终端` 软件，对于Windows系统，打开 `命令行` 软件
```shell
javac HelloWorld.java
```

随后当前目录会新生成一个HelloWorld.class文件，要运行Java文件，使用：
```shell
java HelloWorld
```

运行成功后，控制台会输出 “Hello, World!”，这就是我们的程序运行结果。



## 3. Java常用的集成开发环境（IDE）

集成开发环境（Integrated Development Environment，简称IDE）是一种软件工具，提供了一套集成的功能和工具，用于开发、编写、测试和调试软件应用程序。

IDE通常包括以下核心组件：代码编辑器、编译器/解释器、调试器、构建工具、版本控制系统集成、图形用户界面设计器、项目管理工具。

通过集成这些功能和工具，IDE可以提高开发人员的生产力，简化开发过程，并提供更好的代码质量和可维护性。IDE通常与特定的编程语言或开发平台相关，例如Java开发中常用的Eclipse、IntelliJ IDEA和NetBeans等。

企业中一般采用集成开发环境软件作为Java开发平台使用，其自动化程度好、编程效率高，可以大大简化开发流程，提高开发效率。

目前比较常用的Java集成开发环境有：

### 3.1 IntelliJ IDEA（推荐）
- IntelliJ IDEA官网为  https://www.jetbrains.com.cn/idea/download/

  IntelliJ IDEA 有两个版本：旗舰版(ULtimate) 社区版(Community)，其中社区版是免费版本。


### 3.2 Eclipse
- Eclipse官网为  https://www.eclipse.org/

    Eclipse有着多个版本，每个版本都有自己特定的用途和功能，主要包括以下版本：

    ①Eclipse for Java Developers：这个版本适合Java开发者，集成了CVS，Git，XML编辑器，Mylyn，Maven integration和WindowBuilder等插件。

    ②Eclipse for Java EE Developers：这个版本集成了Java EE开发常用插件，方便动态web网站开发，适合Java web开发者使用。集成了XML编辑器、数据库查看工具，提供jsp可视化编辑器。

    ③Eclipse Standard：这个版本是Eclipse最基础的版本，适合Java se个人开发者、或希望根据自己需求配置插件的开发者使用。

### 3.3 样例展示
这里以IntelliJ IDEA 为例展示如何使用IDE编写你的第一个Hello World 程序：

- 选择新建项目，如果前序步骤的Java JDK安装成功，则可以在JDK栏成功找到相应JDK，选择可使用的JDK并新建项目。
    ![](https://markdown.liuchengtu.com/work/uploads/upload_5517a0c85e9607e16cd42e2f2ee587f0.png)

- 进入项目界面，右击src文件夹并新建一个名为HelloWorld的类(class)，src文件夹是存放源代码的位置。
    ![](https://markdown.liuchengtu.com/work/uploads/upload_cfb70ead436fd2d04f3d92dab7a55d94.png)

- 复制以下代码：
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("Hello, World!");
        }
    }
    ```
- 点击运行图标运行该段代码：
    ![](https://markdown.liuchengtu.com/work/uploads/upload_112ea91497c6c91f4bc0ec48a1896c6a.png)
- 当点击运行图标后，IDE实际上帮助我们完成了编译和运行两个步骤，即上文中提到的`javac` 和 `java` 命令。

- 成功编译并运行后，控制台输出如下信息：

    ![](https://markdown.liuchengtu.com/work/uploads/upload_55b3b6cd0c750739d488aa797063c32b.png)

至此，你已经完成Java环境的所有配置。

## 4. Java中的标识符

### 4.1 标识符

标识符是指用来标识某个实体的一个符号。在Java语言中，主要是指在编程时使用的名字。标识符的使用须遵循一定的规则：Java中的标识符由字母、数字、下划线或美元符号组成，且必须以字母、下划线（_）或美元符号（$）开头。规则总结如下：

- 可以包含数字，但不能以数字开头。
- 除下划线（_）和美元符号（$）以外，不包含任何其他特殊字符，如空格。
- 不能用Java关键字或保留字做标识符。
- Java标识符大小写敏感。

合法的标识符，如：
```java
int a = 3;
int _123 = 3;
int $12aa = 3;
int 变量1 = 3; //不建议使用中文
```
不合法的标识符，如：
```java
int 1a = 3; //不能使用数字开头
int a# = 3; //不能包含#这样的特殊字符
int int = 3; //不能使用关键字
```
注意：虽然Java的语法允许使用下划线（_）和美元符号（$）作为标识符的开始，但是在很多企业的开发规范中约定，不能使用这两者作为标识符的开始，以达到统一标识符格式，减少歧义的效果。


### 4.2 关键字和保留字

关键字和保留字是Java语言中具有特殊含义的单词或符号。关键字是Java语言本身定义的，用于表示特定的语法结构和操作，不能用作标识符，如变量名、类名等。

Java语言共有50个关键字，如下所示：

    abstract    continue    for         new         switch
    assert      default     if          package     synchronized
    boolean     do          goto        private     this
    break       double      implements  protected   throw
    byte        else        import      public      throws
    case        enum        instanceof  return      transient
    catch       extends     int         short       try
    char        final       interface   static      void
    class       finally     long        strictfp    volatile
    const       float       native      super       while

- 这些关键字具有固定的语法含义，不能被用作变量名或其他标识符。
- 保留字是指被保留但目前未被使用的关键字，它们在Java语言中没有特定的功能，但为了保留未来可能使用的关键字而被保留。
- 我们在编写代码时应避免使用关键字作为标识符，以免引发编译错误或语法混淆。


## 5. Java中的变量

### 5.1 什么是变量

变量是Java程序中的基本存储单元，它的作用是用来存储数据。变量本质上代表了内存中的一个存储的区域，这个区域里的数据在同一数据类型中可以不断的变化。通过变量可以方便的读取和操作该区域中的数据。

- 变量：顾名思义，会变的量。
- 常量：自然界中规定好了的、不会变的值。

### 5.2 变量的声明
在Java中，需要先声明一个变量，才能使用这个变量。变量的声明包含两点：变量的数据类型和变量名，语法格式如下：
```shell
数据类型 变量名； 
```

数据类型可以是Java的任意数据类型之一；变量名即变量的名称，用于存储变量值：
```java
int a;
char b;
```
可以同时声明多个同一数据类型的变量，变量之间用“,”隔开，例如：
```java
int c，d，e;
 
等同于：
 
int c;
int d;
int e;
```
### 5.3 变量的初始化

Java语法规定：变量在使用之前必须初始化，即必须给该变量赋予特定的值。

变量的第一次赋值即对变量的初始化。在Java中，使用等号(=)实现变量的赋值。

变量的初始化有以下两种方式：

1、在声明变量时，同时对变量进行初始化，语法如下：
```java
数据类型 变量名 = 初始值；
 
例如：
int f = 5;
```
2、第一次使用变量前，对变量进行初始化，语法如下：
```java
数据类型 变量名；
    ……
变量名 = 初始值；
例如：
 
int sum;                      // 声明变量sum
System.out.println(sum);      // 报错，不能使用未赋值的变量
sum = 100;                    // 给变量sum赋值
System.out.println(sum);      // 正确，输出100
```
### 5.4 变量的访问

变量在声明和初始化后，可以对变量进行访问，包括读取变量的值和修改变量的值。代码如下：

```java
int sum = 100;               // 声明变量sum
System.out.println(sum);     // 输出变量的值 -> 100
sum = 200;                   // 修改变量sum的值
System.out.println(sum);     // 再次输出变量的值 -> 200
```
变量的访问应注意以下几个方面：

1、变量的操作必须与类型匹配。

变量在声明时指定了类型，Java编译器会检测对该变量的操作是否与其他类型匹配，如果对变量的赋值或者操作与其类型不匹配，会产生编译错误，例如：

```java
//编译错误，变量a的类型为int整型，不能赋值为浮点类型的值
int a = 3.14;  
```

2、变量的数据类型只写一次。

变量在第一次声明的时候写数据类型，再次使用时不写数据类型，例如：
```java
int n;
n = 5;   // 正确，再次使用变量n时不写数据类型
int n = 10; // 再次指定变量的数据类型会出现编译错误
```

3、未经声明的变量不能使用。

变量必须先声明，否则会出现编译错误，例如：

```java
k=5;    
System.out.println(p);  // 编译错误，变量没有声明
```

4、变量初始化后才可以使用。

声明一个变量，必须初始化后才能使用，例如：
```java
int t;                             
System.out.println(t);  // 变量t没有初始化，出现编译错误
```

## 6. Java的数据类型
Java的数据类型分为两大类：基本数据类型和引用数据类型。

### 6.1 基本数据类型
Java基本数据类型包括4类8种。4类分别是整数类型、浮点数类型、字符类型和布尔类型。
Java中整数类型包括：byte、short、int 和long型，它们之间的区别仅仅是宽度和范围的不同。

#### 6.1.1 整数类型
- 一个byte类型的变量代表的值占用1个字节的内存空间（8位），能够表示的10进制整数数据范围是负128到正127，包含0。
- 一个int类型的变量代表的值占用4个字节的内存空间（32）位，能够表示的10进制整数数据范围是负2147483648到正2147483647，包含0。

#### 6.1.2 浮点类型

- 浮点类型主要用来储存小数数值，也可以用来储存范围较大的整数。
- 它分为单精度浮点数（float）和双精度浮点数（double）两种，双精度浮点数比单精度浮点数所使用的内存空间更大，可表示的数值范围与精确度也比较大。

#### 6.1.3 字符类型

字符类型表示单个字符，Java中的字符类型变量使用char关键字进行声明，而字符型字面量必须用单引号括起来，例如：
```java
char c = 'A';
```
#### 6.1.4 布尔类型

- 布尔类型在Java语言中使用关键字boolean 声明，它只有两个字面量：true和false。
- 与C语言不同，Java不允许使用0或非0的整数来代替true和false，也不能将其他基本数据类型的值直接转换为布尔类型。
- 布尔类型用于判断逻辑条件的结果，通常在程序的分支和循环控制语句中使用，根据逻辑判断的结果来决定程序的执行流程。
```java
boolean isBig = true;
boolean isSmall = false;
```
### 6.2 引用数据类型
引用类型是指除基本数据类型以外的所有类型，包括类、接口、数组、枚举等，是高阶内容，不在本次教学范围内，这里只选取Java中常用的一种引用数据类型进行介绍。

#### 6.2.1 字符串类型

字符串类型是Java中用于存储多个字符的数据类型，使用String关键字声明字符串变量。例如：
```java
String str = "abc";
```
需要强调两点：

- Java中的字符串类型字面量是String类型的，而不是char类型的。
- String类型不是基本数据类型，而是引用类型。

### 6.3 常用数据类型的使用实例

```java
public class StudentInformation {
    public static void main(String[] args) {
        // 学生信息
        int studentId = 12345;
        String studentName = "赵镇";
        int age = 20;
        double score = 92.5;
        char gender = '男';
        boolean isMarried = false;
        
        // 输出学生信息
        System.out.println("学生信息：");
        System.out.println("学号：" + studentId);
        System.out.println("姓名：" + studentName);
        System.out.println("年龄：" + age);
        System.out.println("成绩：" + score);
        System.out.println("性别：" + gender);
        System.out.println("婚否：" + isMarried);
    }
}
```

## 7. Java中的运算符

### 7.1 算术运算符
- **运算符**：`+`（加）、`-`（减）、`*`（乘）、`/`（除）、`%`（求余）、`++`（自增）、`--`（自减）
- **用途**：执行基本的数学运算
- **示例代码**：
    ```java
    int a = 10;
    int b = 20;
    int result = a + b; // 30
    a++; // 11
    ```

### 7.2 赋值运算符
- **运算符**：`=`（等于）、`+=`（自加一次等于）、`-=`（自减一次等于）、`*=`（自乘一次等于）、`/=`（自除一次等于）、`%=`（求模并赋值）
- **用途**：将计算结果赋值给变量
- **示例代码**：
    ```java
    int x = 10;
    x += 5; // 等同于 x = x + 5;
    ```

### 7.3 比较运算符
- **运算符**：`<`（小于）、`>`（大于）、`>=`（大于等于）、`<=`（小于等于）、`==`（等于）、`!=`（不等于）
- **用途**：比较两个值的大小或相等性
- **示例代码**：
    ```java
    int m = 10;
    int n = 20;
    boolean result = (m > n); // 比较 m 是否大于 n
    ```

### 7.4 逻辑运算符
- **运算符**：`&&`（短路与）、`||`（短路或）、`!`（非）
- **用途**：组合布尔表达式，实现逻辑运算
- **示例代码**：
    ```java
    boolean condition1 = true;
    boolean condition2 = false;
    boolean result = condition1 && condition2; // 使用短路与运算符
    ```

### 7.5 条件（三目）运算符
- **运算符**：`?:`
- **用途**：根据条件表达式的结果选择两个值中的一个
- **语法**：`result = (condition) ? value1 : value2;`
- **示例代码**：
    ```java
    int age = 20;
    String message = (age >= 18) ? "成年人" : "未成年人"; // 根据年龄判断成年人或未成年人
    ```

### 7.6 位运算符
- **运算符**：`&`（按位与）、`|`（按位或）、`^`（异或）、`~`（非、取反）
- **用途**：对二进制位进行操作
- **示例代码**：
    ```java
    int a = 5; // 二进制为 101
    int b = 3; // 二进制为 011
    int result = a & b; // 按位与操作
    ```

### 7.7 复合赋值运算符
- **运算符**：`+=`, `-=`, 等
- **用途**：将操作简化
- **示例**：`x += 5` 等价于 `x = x + 5`

### 7.8 字符串连接运算符
- **运算符**：`+`
- **用途**：用于连接字符串
- **示例代码**：
    ```java
    String str1 = "Hello, ";
    String str2 = "World!";
    String result = str1 + str2; // "Hello, World!"
    ```

Java中的运算符不仅包括上述基本类型，还包括复合赋值运算符，如 +=, -= 等，此外，Java还支持字符串连接操作，其中 + 运算符除了用于数值的加法运算外，还可以用于连接字符串。

## 8. Java的输入与输出

### 8.1 使用 Scanner 读取字符串/整数/浮点数
Scanner 可以读取用户的键盘输入。
例如：
```java
import java.util.Scanner; // 导入 util 包
public class scannerReader {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你的姓名：");
        String name = sc.nextLine();
        System.out.println("请输入你的年龄：");
        int age = sc.nextInt();
        System.out.println("请输入你的工资：");
        float salary = sc.nextFloat();
        System.out.println("你的信息如下：");
        System.out.println("姓名: " + name + "\n" + "年龄：" + age + "\n" + "工资：" + salary);
        sc.close(); //调用关闭方法
    }
}
```
### 8.2 System.out.println()
`System.out.println()`可以打印一行内容，输出完自动换行。
```java
public class Inputoutput {
    public static void main(String[] args){
        System.out.println("hello,java!");
        int a=9;
        System.out.println("output:"+a);
    }
}
```

### 8.3 System.out.print()
`System.out.print()`可以打印字符串以及其他的类型。
```java
public class Inputoutput {
    public static void main(String[] args){
        char c='我';//在Java中char有两字节，所以可以存中文
        int a=2187;
        byte b=127;
        System.out.print(c);
        System.out.print('\n');
        System.out.print(a);
        System.out.print("output:"+b);
    }
}
```
### 8.4 InputStream/OutputStream
在 Java 中，InputStream 和 OutputStream 是两个基本的 I/O 类，用于处理字节流的输入和输出。它们分别是输入和输出操作的基类，并且都有多个子类，支持从各种数据源读取数据和将数据写入各种数据目标。以下是它们的关系、基类、子类及其常见用途的详细介绍。

InputStream 和 OutputStream 的关系：

- InputStream：是一个抽象类，表示字节输入流的所有类的超类。它定义了从不同输入源（如文件、内存缓冲区、网络连接）读取字节数据的基本方法。
- OutputStream：是一个抽象类，表示字节输出流的所有类的超类。它定义了向不同输出目标（如文件、内存缓冲区、网络连接）写入字节数据的基本方法。
- InputStream 和 OutputStream 并没有直接的继承关系，但它们是互补的，分别处理输入和输出操作。

例如：

##### 使用 `InputStream` 读取文件
```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
 
public class InputStreamExample {
    public static void main(String[] args) {
        try (InputStream inputStream = new FileInputStream("example.txt")) {
            int data;
            while ((data = inputStream.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

##### 使用 `OutputStream` 写入文件
```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
 
public class OutputStreamExample {
    public static void main(String[] args) {
        String data = "Hello, World!";
        try (OutputStream outputStream = new FileOutputStream("example.txt")) {
            outputStream.write(data.getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
## 9. 课程总结

- Java环境安装正常。
- 完成第一个Hello World程序。
- 认识变量类型和命名方式。
- Java中的运算符。
- Java的输入与输出。



# 课后练习

#课后练习  
  
1.编写一个Python程序来找出满足以下条件的最小正整数：  
  
-该数除以12余1  
-该数除以23也余1  
-该数除以31也余1  
  
请在以下选项中选择一个正确的答案，该答案满足上述所有条件：  
  
(A) 4191  
  
(B) 3232  
  
(C) 8577  
  
(D) 9233  
  
  
  
参考程序：  
  
``` java
import java.util.Scanner;

public class FindNumber {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // 获取用户输入的选项
        System.out.print("请输入一个选项：");
        int option = scanner.nextInt();

        // 计算余数
        int a = option % 12;
        int b = option % 23;
        int c = option % 31;

        // 打印余数结果
        System.out.println("For option " + option + ":");
        System.out.println("a = " + a + ", b = " + b + ", c = " + c);

        // 判断是否满足条件
        if (a == 1 && b == 1 && c == 1) {
            System.out.println("Correct, That's what I find!! The number is: " + option);
        } else {
            System.out.println("Wrong, Please try another Answer!");
        }

        scanner.close();
    }
}
```  
  
  
  
2.编写一个Java程序，用于模拟餐厅的点单过程。程序应提前告知用户汉堡、薯条和可乐的价格，并通过用户输入获得点单信息。最后，程序应分行输出客户点的内容，并打印出总价。  
  
**价格信息：**  
  
-汉堡：$5 
-薯条：$2  
-可乐：$1 
  
**功能要求：** 
  
1.显示各项食物的价格。 
2.提示用户输入每种食物的数量。 
3.计算并显示每种食物的点单数量。 
4.计算并显示总价。 
  
**输入输出示例：** 
 
示例输出： 
  
```  
汉堡：$5  
薯条：$2  
可乐：$1  
  
请输入汉堡的数量：2  
请输入薯条的数量：1  
请输入可乐的数量：3  
  
您的点单如下：  
汉堡X 2  
薯条X 1  
可乐X 3  
  
总价：$15  
```  
  
**提示：** 
  
- 使用`Scanner`函数获取用户输入。 
- 使用算术运算计算总价。 
- 使用`System.out.println()`函数输出结果。 
  

  
示例代码： 
  
``` java
import java.util.Scanner;

public class RestaurantOrder {
    public static void main(String[] args) {
        // 定义食物的价格
        int burgerPrice = 5;
        int friesPrice = 2;
        int colaPrice = 1;

        // 显示价格信息
        System.out.println("汉堡：$" + burgerPrice);
        System.out.println("薯条：$" + friesPrice);
        System.out.println("可乐：$" + colaPrice + "\n");

        // 获取用户输入的点单数量
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入汉堡的数量：");
        int burgerCount = scanner.nextInt();
        System.out.print("请输入薯条的数量：");
        int friesCount = scanner.nextInt();
        System.out.print("请输入可乐的数量：");
        int colaCount = scanner.nextInt();

        // 计算总价
        int totalPrice = burgerCount * burgerPrice +
                         friesCount * friesPrice +
                         colaCount * colaPrice;

        // 输出点单内容和总价
        System.out.println("\n您的点单如下：");
        System.out.println("汉堡 X " + burgerCount);
        System.out.println("薯条 X " + friesCount);
        System.out.println("可乐 X " + colaCount);
        System.out.println("\n总价：$" + totalPrice);

        scanner.close();
    }
}

```



