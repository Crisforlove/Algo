# Lesson 4 字符串基础

## 目录
1. [创建字符串](#1-创建字符串)
2. [访问字符串中的值](#2-访问字符串中的值)
3. [字符串连接与更新](#3-字符串连接与更新)
4. [Java字符串格式化](#4-java字符串格式化)
    - [4.1 使用 String.format](#41-使用-stringformat)
    - [4.2 文本块（Text Blocks）](#42-文本块text-blocks)
    - [4.3 使用 String.format() 和文本块结合](#43-使用-stringformat-和文本块结合)
    - [4.4 使用 StringBuilder 进行格式化](#44-使用-stringbuilder-进行格式化)
5. [Java 转义字符](#5-java-转义字符)
6. [Java 字符串运算符](#6-java-字符串运算符)
    - [6.1 length()](#61-length)
    - [6.2 charAt(int index)](#62-charatint-index)
    - [6.3 substring(int beginIndex, int endIndex)](#63-substringint-beginindex-int-endindex)
    - [6.4 toLowerCase()](#64-tolowercase)
    - [6.5 toUpperCase()](#65-touppercase)
    - [6.6 trim()](#66-trim)
    - [6.7 replace(CharSequence target, CharSequence replacement)](#67-replacecharsequence-target-charsequence-replacement)
    - [6.8 split(String regex)](#68-splitstring-regex)
    - [6.9 concat(String str)](#69-concatstring-str)
    - [6.10 字符串连接运算符 +](#610-字符串连接运算符-)
    - [6.11 重复输出字符串运算符 repeat()](#611-重复输出字符串运算符-repeat)
    - [6.12 通过索引获取字符 charAt()](#612-通过索引获取字符-charat)
    - [6.13 截取子字符串 substring()](#613-截取子字符串-substring)
    - [6.14 成员运算符 contains()](#614-成员运算符-contains)
    - [6.15 成员运算符 indexOf() 和 lastIndexOf()](#615-成员运算符-indexof-和-lastindexof)
7. [课后练习](#7-课后练习)
    - [7.1 选择题](#71-选择题)
    - [7.2 代码题](#72-代码题)



## 1. 创建字符串

Java中使用 `String` 类来表示字符串，可以使用双引号 `" "` 来创建字符串变量。

```java
String var1 = "Hello World!";
String var2 = "CodeRaft";
```

## 2. 访问字符串中的值

Java中访问字符串中的字符可以使用索引，索引从0开始。

```java
char firstChar = var1.charAt(0); // 获取索引为0的字符 'H'
String substr = var2.substring(1, 5); // 截取字符串 var2 的第2到第5个字符（"odeR"）
```

## 3. 字符串连接与更新

Java中字符串是不可变的，每次连接字符串都会创建一个新的字符串对象。

```java
String var1 = "Hello";
var1 = var1 + " CodeRaft!"; // 连接字符串并更新 var1
```

## 4. Java字符串格式化

字符串格式化是将数据（如变量的值）插入到字符串中的一种技术。这使得构建动态字符串变得更加方便和可读。

### 4.1 使用 `String.format`

Java中格式化字符串可以使用 `String.format` 方法


**%s：格式化字符串**

`%s` 用于格式化字符串。

**示例：**
```java
String name = "小明";
int age = 10;
String formattedString = String.format("我叫 %s 今年 %d 岁!", name, age);
System.out.println(formattedString); // 输出：我叫 小明 今年 10 岁!
```

**%d：格式化整数**

`%d` 用于格式化整数。

**示例：**
```java
int number = 12345;
String formattedNumber = String.format("数字：%d", number);
System.out.println(formattedNumber); // 输出：数字：12345
```

**%f：格式化浮点数**

`%f` 用于格式化浮点数，默认保留六位小数。

**示例：**
```java
double pi = 3.14159;
String formattedPi = String.format("π 的近似值为：%.2f", pi);
System.out.println(formattedPi); // 输出：π 的近似值为：3.14
```


### 使用示例

```java
String name = "小明";
int age = 10;
double height = 1.75;

String formattedString = String.format("我叫 %s，今年 %d 岁，身高 %.2f 米", name, age, height);
System.out.println(formattedString); // 输出：我叫 小明，今年 10 岁，身高 1.75 米
```


### 4.2 文本块（Text Blocks）

文本块允许你编写多行字符串而无需使用换行符或转义字符。例如：

```java
String textBlock = """
    This is a text block.
    It can span multiple lines.
    """;
System.out.println(textBlock);
```

### 4.3 使用 `String.format()` 和文本块结合

虽然文本块本身不支持内嵌变量，但你可以使用 `String.format()` 将变量插入文本块中：

```java
String name = "Alice";
int age = 30;

String formattedString = String.format("""
    My name is %s.
    I am %d years old.
    """, name, age);

System.out.println(formattedString);
// 输出：
// My name is Alice.
// I am 30 years old.
```

### 4.4 使用 `StringBuilder` 进行格式化

Java中建议使用 `StringBuilder` 类来动态构建字符串，特别是在需要频繁连接和修改字符串时，因此对于复杂的字符串构建，你可以结合使用 `StringBuilder` 和字符串格式化：

```java
String name = "Bob";
double score = 95.5;

StringBuilder sb = new StringBuilder();
sb.append(String.format("Student %s scored %.2f marks.%n", name, score));
System.out.println(sb.toString());
// 输出：Student Bob scored 95.50 marks.
```


## 5. Java 转义字符

在Java中，转义字符用于表示特殊字符和控制字符。以下是一些常见的转义字符示例：

| 转义字符 | 描述                                           | 示例                                                       |
| -------- | ---------------------------------------------- | ---------------------------------------------------------- |
| `\\`     | 反斜杠符号                                     | `System.out.println("\\");`                                 |
| `\'`     | 单引号                                         | `System.out.println("\'");`                                 |
| `\"`     | 双引号                                         | `System.out.println("\"");`                                 |
| `\n`     | 换行                                           | `System.out.println("Hello\nWorld!");`                     |
| `\t`     | 制表符                                         | `System.out.println("Hello\tWorld!");`                     |
| `\b`     | 退格                                           | `System.out.println("Hello\bWorld!");`                     |
| `\r`     | 回车                                           | `System.out.println("Hello\rWorld!");`                     |
| `\f`     | 换页                                           | `System.out.println("Hello\fWorld!");`                     |
| `\u####` | Unicode 字符，其中####是字符的四位十六进制代码 | `System.out.println("\u0048\u0065\u006C\u006C\u006F!");` |



使用了不同的转义字符来演示单引号、换行符、制表符、退格符、换页符的效果：

```java
public class EscapeCharacters {
    public static void main(String[] args) {
        // 单引号
        System.out.println('\''); // 输出：'

        // 换行符
        System.out.println("Hello, world!\nHow are you?");
        // 输出：
        // Hello, world!
        // How are you?

        // 制表符
        System.out.println("Hello, world!\tHow are you?"); // 输出：Hello, world!    How are you?

        // 退格符
        System.out.println("Hello,\b world!"); // 输出：Hello world!

        // 换页符
        System.out.println("Hello,\f world!");
        // 输出：
        // Hello,
        //  world!
    }
}
```

## 6. Java 字符串运算符

在Java中，字符串是一种常见的数据类型，提供了多种操作符来对字符串进行操作和处理。下面我们将介绍Java中常用的字符串运算符及其用法。

在 Java 中，常用的字符串函数包括：

### 6.1 `length()`
- **功能：** 返回字符串的长度。
- **示例：**
```java
String str = "Hello, World!";
int length = str.length();  // 13
```

### 6.2 `charAt(int index)`
- **功能：** 返回指定位置的字符。
- **示例：**
```java
String str = "Hello";
char ch = str.charAt(1);  // 'e'
```

### 6.3 `substring(int beginIndex, int endIndex)`
- **功能：** 返回从 `beginIndex` 到 `endIndex` 之间的子字符串。
- **示例：**
```java
String str = "Hello, World!";
String substr = str.substring(7, 12);  // "World"
```

### 6.4 `toLowerCase()`
- **功能：** 将字符串转换为小写。
- **示例：**
```java
String str = "HELLO";
String lower = str.toLowerCase();  // "hello"
```

### 6.5 `toUpperCase()`
- **功能：** 将字符串转换为大写。
- **示例：**
```java
String str = "hello";
String upper = str.toUpperCase();  // "HELLO"
```

### 6.6 `trim()`
- **功能：** 去除字符串前后的空白字符。
- **示例：**
```java
String str = "   Hello, World!   ";
String trimmed = str.trim();  // "Hello, World!"
```

### 6.7 `replace(CharSequence target, CharSequence replacement)`
- **功能：** 替换字符串中的指定子字符串。
- **示例：**
```java
String str = "Hello, World!";
String replaced = str.replace("World", "Java");  // "Hello, Java!"
```

### 6.8 `split(String regex)`
- **功能：** 根据正则表达式分割字符串。
- **示例：**
```java
String str = "apple,banana,cherry";
String[] fruits = str.split(",");  // ["apple", "banana", "cherry"]
```

### 6.9 `concat(String str)`
- **功能：** 将指定的字符串连接到当前字符串的末尾。
- **示例：**
```java
String str = "Hello";
String concatenated = str.concat(", World!");  // "Hello, World!"
```

### 6.10 **字符串连接运算符 `+`**

   字符串连接运算符 `+` 用于将两个字符串连接起来。

   **示例：**
```java
String str1 = "Hello";
String str2 = "World";
String result = str1 + str2;
System.out.println(result); // 输出：HelloWorld
```

### 6.11 **重复输出字符串运算符 `repeat()`**

   Java 11 引入了 `repeat()` 方法来重复字符串。

   **示例：**
```java
String str = "Hello";
String repeatedStr = str.repeat(3);
System.out.println(repeatedStr); // 输出：HelloHelloHello
```

   注意：`repeat()` 方法在 Java 11 及以上版本可用。

### 6.12 **通过索引获取字符 `charAt()`**

   `charAt()` 方法用于获取字符串中指定位置的字符。

   **示例：**
```java
String str = "Hello";
char ch = str.charAt(1); // 获取索引为1的字符，即第2个字符 'e'
System.out.println(ch); // 输出：e
```

### 6.13 **截取子字符串 `substring()`**

   `substring()` 方法用于截取字符串的一部分。

   **示例：**
```java
String str = "HelloWorld";
String subStr = str.substring(3, 7); // 从索引3开始到索引6（不包括7）的子字符串，即 "loWo"
System.out.println(subStr); // 输出：loWo
```

### 6.14 **成员运算符 `contains()`**

   `contains()` 方法用于检查字符串是否包含指定的字符序列。

   **示例：**
```java
String str = "HelloWorld";
boolean contains = str.contains("Wo"); // 检查是否包含 "Wo"
System.out.println(contains); // 输出：true
```

### 6.15 **成员运算符 `indexOf()` 和 `lastIndexOf()`**

   `indexOf()` 和 `lastIndexOf()` 方法用于获取字符或字符串在目标字符串中第一次出现的位置索引和最后一次出现的位置索引。

   **示例：**
```java
String str = "HelloWorld";
int firstIndex = str.indexOf('o'); // 第一次出现 'o' 的位置索引，索引从0开始
int lastIndex = str.lastIndexOf('o'); // 最后一次出现 'o' 的位置索引
System.out.println("第一次出现 'o' 的位置索引：" + firstIndex); // 输出：4
System.out.println("最后一次出现 'o' 的位置索引：" + lastIndex); // 输出：7
```


## 7. 课后练习

### 7.1 选择题
#### 题目 1: 字符串索引与切片
观察以下代码，输出结果是什么？

```java
public class StringTest {
    public static void main(String[] args) {
        String str = "Hello, World!";
        String slice = str.substring(7, 12);
        System.out.println(slice);
    }
}
```

**A. Hello**

**B. World**

**C. World!**

**D. , Wor**

**答案：** B. World

**理由：** `substring(7, 12)` 方法返回从索引 7 开始到索引 12 之前的子字符串，即 `"World"`。

---

#### 题目 2: 字符串常用函数
观察以下代码，输出结果是什么？

```java
public class StringFunctions {
    public static void main(String[] args) {
        String str = " Java Programming ";
        int length = str.trim().length();
        String lower = str.toLowerCase();
        String concatenated = lower.concat(" is fun!");
        System.out.println("Length: " + length);
        System.out.println("Concatenated: " + concatenated);
    }
}
```

**A. Length: 16; Concatenated: java programming is fun!**

**B. Length: 18; Concatenated: java programming is fun!**

**C. Length: 17; Concatenated: java programming is fun!**

**D. Length: 18; Concatenated:  java programming is fun!**

**答案：** D. Length: 18; Concatenated: java programming is fun!

**理由：** `trim()` 去除前后空格，所以 `length` 是 18。`toLowerCase()` 将所有字符转为小写，`concat(" is fun!")` 进行字符串拼接，结果是 `"java programming is fun!"`。

---

#### 题目 3: 字符串格式化

观察以下代码，输出结果是什么？

```java
public class StringFormat {
    public static void main(String[] args) {
        int age = 25;
        String name = "Alice";
        String formatted = String.format("Name: %s, Age: %d", name, age);
        System.out.println(formatted);
    }
}
```

**A. Name: Alice, Age: 25**

**B. Name: %s, Age: %d**

**C. Name: Alice, Age: 25**

**D. Name: Alice, Age: age**

**答案：** A. Name: Alice, Age: 25

**理由：** `String.format` 方法用于格式化字符串，`%s` 替换为 `name` 的值，`%d` 替换为 `age` 的值。



### 7.2 代码题

### 题目 1: 字符串索引与切片

**题目：** 编写一个 Java 程序，创建一个字符串 `"Programming in Java"`。使用 `substring` 方法提取并输出从索引 0 到索引 11 的子字符串。

**示例代码：**
```java
public class StringTest {
    public static void main(String[] args) {
        String str = "Programming in Java";
        // 请在这里编写代码
    }
}
```

**答案：**
```java
public class StringTest {
    public static void main(String[] args) {
        String str = "Programming in Java";
        String substring = str.substring(0, 11);
        System.out.println(substring);  // 输出 "Programming"
    }
}
```

---

### 题目 2: 字符串常用函数

**题目：** 编写一个 Java 程序，创建一个字符串 `"   Java Programming   "`。去除字符串前后的空白字符，转换为大写，并拼接 `" is fun!"`。输出最终结果。

**示例代码：**
```java
public class StringFunctions {
    public static void main(String[] args) {
        String str = "   Java Programming   ";
        // 请在这里编写代码
    }
}
```

**答案：**
```java
public class StringFunctions {
    public static void main(String[] args) {
        String str = "   Java Programming   ";
        String trimmed = str.trim();
        String upper = trimmed.toUpperCase();
        String result = upper.concat(" is fun!");
        System.out.println(result);  // 输出 "JAVA PROGRAMMING is fun!"
    }
}
```

---

### 题目 3: 字符串格式化

**题目：** 编写一个 Java 程序，创建一个整数变量 `score` 赋值为 85，创建一个字符串变量 `student` 赋值为 `"John"`。使用 `String.format` 方法格式化字符串，输出 `"Student John scored 85 points"`。

**示例代码：**
```java
public class StringFormat {
    public static void main(String[] args) {
        int score = 85;
        String student = "John";
        // 请在这里编写代码
    }
}
```

**答案：**
```java
public class StringFormat {
    public static void main(String[] args) {
        int score = 85;
        String student = "John";
        String formatted = String.format("Student %s scored %d points", student, score);
        System.out.println(formatted);  // 输出 "Student John scored 85 points"
    }
}
```

