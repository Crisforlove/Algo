# Lesson 4 字符串基础

## 目录
  - [1 字符串创建、修改、拼接](#1-字符串创建修改拼接)
    - [1.1 字符串的创建](#11-字符串的创建)
    - [1.2 Python 访问字符串中的值](#12-python-访问字符串中的值)
    - [1.3 Python 字符串拼接](#13-python-字符串拼接)
  - [2 转义字符与字符串运算](#2-转义字符与字符串运算)
    - [2.1 转义字符](#21-转义字符)
    - [2.2 字符串运算符](#22-字符串运算符)
  - [3 Python 字符串格式化](#3-python-字符串格式化)
  - [4 Python三引号](#4-python三引号)
  - [5 f-string](#5-f-string)
  - [6 字符串函数](#6-字符串函数)
  - [7 课后练习](#7-课后练习)
    - [7.1 选择题](#71-选择题)
    - [7.2 代码题](#72-代码题)

## 1 字符串创建、修改、拼接

### 1.1 字符串的创建

字符串是 Python 中最常用的数据类型。我们可以使用引号( **'** 或 **"** )来创建字符串。

创建字符串很简单，只要为变量分配一个值即可。例如：

```
var1 = 'Hello World!'
var2 = "CodeRaft"
```

### 1.2 Python 访问字符串中的值

Python 不支持单字符类型，单字符在 Python 中也是作为一个字符串使用。

Python 访问子字符串，可以使用方括号 **[]** 来截取字符串，字符串的截取的语法格式如下：

```
变量[头下标:尾下标]
```

索引值以 **0** 为开始值，**-1** 为从末尾的开始位置。

参考示例1:

```
word = 'CodeRaft'
for i in range(len(word)):
    print(word[i])
```

输出为：

```
C
o
d
e
R
a
f
t
```

参考示例2:

```
word = 'CodeRaft'
for i in range(len(word) - 1, -1, -1):
    print(word[i])
```

输出为：

```
t
f
a
R
e
d
o
C
```

参考示例3:

```
var1 = 'Hello World!'
var2 = "CodeRaft"
 
print ("var1[0]: ", var1[0])
print ("var2[1:5]: ", var2[1:5])
```

以上实例执行结果：

```
var1[0]:  H
var2[1:5]:  odeR
```

### 1.3 Python 字符串拼接

需要注意的是，在Python中是不可以直接对字符串索引元素进行赋值进行修改的，以下示例展示了直接修改系统会提示我们字符串的不可修改：

```
val = 'CodeRaft'
print(val)
val[0] = 'R'
print(val)
```

系统提示为：

```
    val[0] = 'R'
    ~~~^^^
TypeError: 'str' object does not support item assignment
```

你可以截取字符串的一部分并与其他字段拼接，如下实例：

```
var1 = 'Hello World!'
 
print ("已更新字符串 : ", var1[:6] + 'CodeRaft!')
```

以上实例执行结果：

```
已更新字符串 :  Hello CodeRaft!
```

## 2 转义字符与字符串运算

### 2.1 转义字符

| 转义字符     | 描述       | 实例                                                         |
| :----------- | :--------- | :----------------------------------------------------------- |
| \\(在行尾时) | 续行符     | `>>> print("line1 \ ... line2 \ ... line3") line1 line2 line3 >>> ` |
| \\          | 反斜杠符号 | `>>> print("\\") \`                                          |
| \\'          | 单引号     | `>>> print('\'') '`                                          |
| \\"          | 双引号     | `>>> print("\"") "`                                          |
| \t           | 横向制表符 | `>>> print("Hello \t World!") Hello    World! >>>`           |
| \n           | 换行       | `>>> print("\n")  >>>`a                                      |



以下实例，我们使用了常用的转义字符来演示：

```

# 单引号
print('\'Hello, world!\'')  # 输出：'Hello, world!'

# 双引号
print("\"Hello, world!\"")  # 输出："Hello, world!"

# 换行
print("Hello\nWorld!")  # 输出：
                        # Hello
                        # World!

# 横向制表符
print("Hello\tWorld!")  # 输出：Hello    World!

# 反斜杠
print("\\")  # 输出：\

# 续行符
print("line1 \
... line2 \
... line3")  # 输出：line1 line2 line3

```

### 2.2 字符串运算符

下表实例变量 a 值为字符串 "Hello"，b 变量值为 "Python"：

| 操作符 | 描述                                                                                                   | 实例                            |
| :----- |:-----------------------------------------------------------------------------------------------------| :------------------------------ |
| +      | 字符串连接                                                                                                | a + b 输出结果： HelloPython    |
| *      | 重复输出字符串                                                                                              | a*2 输出结果：HelloHello        |
| []     | 通过索引获取字符串中字符                                                                                         | a[1] 输出结果 **e**             |
| [ : ]  | 截取字符串中的一部分，遵循**左闭右开**原则，str[0:2] 是不包含第 3 个字符的。                                                       | a[1:4] 输出结果 **ell**         |
| in     | 成员运算符 - 如果字符串中包含给定的字符返回 True                                                                         | **'H' in a** 输出结果 True      |
| not in | 成员运算符 - 如果字符串中不包含给定的字符返回 True                                                                        | **'M' not in a** 输出结果 True  |
| r/R    | 原始字符串 - 所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母 **r**（可以大小写）以外，与普通字符串有着几乎完全相同的语法。 | `print( r'\n' ) print( R'\n' )` |

```
a = "Hello"
b = "Python"
 
print("a + b 输出结果：", a + b)
print("a * 2 输出结果：", a * 2)
print("a[1] 输出结果：", a[1])
print("a[1:4] 输出结果：", a[1:4])
 
if("H" in a) :
    print("H 在变量 a 中")
else :
    print("H 不在变量 a 中")
 
if("M" not in a) :
    print("M 不在变量 a 中")
else :
    print("M 在变量 a 中")
 
print (r'\n')
print (R'\n')
```

以上实例输出结果为：

```
a + b 输出结果： HelloPython
a * 2 输出结果： HelloHello
a[1] 输出结果： e
a[1:4] 输出结果： ell
H 在变量 a 中
M 不在变量 a 中
\n
\n
```

## 3 Python 字符串格式化

Python 支持格式化字符串的输出 。尽管这样可能会用到非常复杂的表达式，但最基本的用法是将一个值插入到一个有字符串格式符 %s 的字符串中。

在 Python 中，字符串格式化使用与 C 中 sprintf 函数一样的语法。

```
print ("我叫 %s 今年 %d 岁!" % ('小明', 10))
```

以上实例输出结果：

```
我叫 小明 今年 10 岁!
```

python常用的字符串格式化符号：

| 符  号 | 描述                                 |
| :----- | :----------------------------------- |
| %s     | 格式化字符串                         |
| %d     | 格式化整数                           |
| %f     | 格式化浮点数字，可指定小数点后的精度 |

## 4 Python三引号

python三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。实例如下

```
para_str = """这是一个多行字符串的实例
多行字符串可以使用制表符
TAB (\t)。
也可以使用换行符 [\n]。
"""
print(para_str)
```

以上实例执行结果为：

```
这是一个多行字符串的实例
多行字符串可以使用制表符
TAB (    )。
也可以使用换行符 [ 
 ]。
```

三引号让程序员从引号和特殊字符串的泥潭里面解脱出来，自始至终保持一小块字符串的格式是所谓的WYSIWYG（所见即所得）格式的。

## 5 f-string

f-string 是 python3.6 之后版本添加的，称之为字面量格式化字符串，是新的格式化字符串的语法。

之前我们习惯用百分号 (%):

```
>>> name = 'CodeRaft'
>>> 'Hello %s' % name
'Hello CodeRaft'
```

**f-string** 格式化字符串以 **f** 开头，后面跟着字符串，字符串中的表达式用大括号 {} 包起来，它会将变量或表达式计算后的值替换进去，实例如下：

```
>>> name = 'CodeRaft'
>>> f'Hello {name}'  # 替换变量
'Hello CodeRaft'
>>> f'{1+2}'         # 使用表达式
'3'

>>> w = {'name': 'Runoob', 'url': 'www.runoob.com'}
>>> f'{w["name"]}: {w["url"]}'
'Runoob: www.runoob.com'
```

用了这种方式明显更简单了，不用再去判断使用 %s，还是 %d。

在 Python 3.8 的版本中可以使用 **=** 符号来拼接运算表达式与结果：

```
>>> x = 1
>>> print(f'{x+1}')   # Python 3.6
2

>>> x = 1
>>> print(f'{x+1=}')   # Python 3.8
x+1=2
```

## 6 字符串函数

下列字符串函数展示了在Python中我们可以对字符串进行的部分操作：

| 函数       | 作用                           | 输入                     | 示例                  | 输出                 |
| ---------- | ------------------------------ | ------------------------ | --------------------- | -------------------- |
| split      | 分割字符串                     | `s = "Hello World"`      | `s.split(" ")`        | `['Hello', 'World']` |
| join       | 合并字符串                     | `s = ['Hello', 'World']` | `" # ".join(s)`       | `Hello#World`        |
| capitalize | 只让首字母大写, 其他都小写     | `s = "py Hello World"`   | `s.capitalize()`      | `Py hello world`     |
| lower      | 所有字符小写                   | `s = "Hello World"`      | `s.lower()`           | `hello world`        |
| upper      | 所有字符大写                   | `s = "Hello World"`      | `s.upper()`           | `HELLO WORLD`        |
| replace    | 替换字符                       | `s = "Hello World"`      | `s.replace("o", "m")` | `Hellm Wmrld`        |
| count      | 计算字符串中某些字符的出现次数 | `s = "Hello World"`      | `s.count("o")`        | `2`                  |
| strip      | 去除字符串开始和末尾的空格     | `s = " Hello World "`    | `s.strip()`           | `Hello World`        |

## 7 课后练习

### 7.1 选择题

**题目 1: 字符串索引与切片**

观察以下代码，输出结果是什么？

```
str = "Hello, World!"
slice = str[7:12]
print(slice)
```
A. Hello

B. World

C. World!

D. , Wor

答案: B. World

理由: 切片 str[7:12] 返回从索引 7 开始到索引 12 之前的子字符串，即 "World"。

**题目 2: 字符串常用函数**

观察以下代码，输出结果是什么？

```
str = " Python Programming "
length = len(str.strip())
lower = str.lower()
concatenated = lower + " is fun!"
print("Length:", length, ";", "Concatenated:", concatenated)
```

A. Length: 16; Concatenated: python programming is fun!

B. Length: 18; Concatenated: Python programming is fun!

C. Length: 17; Concatenated: python programming is fun!

D. Length: 18; Concatenated: python programming is fun!

答案: D. Length: 18; Concatenated: python programming is fun!

理由: strip() 去除前后空格，所以 length 是 18。lower() 将所有字符转为小写，字符串拼接得到 "python programming is fun!"。

**题目 3: 字符串格式化**

观察以下代码，输出结果是什么？
```
age = 25
name = "Alice"
formatted = "Name: {}, Age: {}".format(name, age)
print(formatted)
```

A. Name: Alice, Age: 25

B. Name: {}, Age: {}

C. Name: Alice, Age: 25

D. Name: Alice, Age: age


答案: A. Name: Alice, Age: 25

理由: format 方法用于格式化字符串，{} 被替换为 name 和 age 的值。

### 7.2 代码题

**题目 1: 字符串索引与切片**

编写一个 Python 程序，创建一个字符串 "Programming in Python"。使用切片提取并输出从索引 0 到索引 11 的子字符串。

示例代码:
```
str = "Programming in Python"
# 请在这里编写代码
```

答案：
```
str = "Programming in Python"
substring = str[:11]
print(substring)  # 输出 "Programming"
```

**题目 2: 字符串常用函数**

编写一个 Python 程序，创建一个字符串 " Python Programming "。去除字符串前后的空白字符，转换为大写，并拼接 " is fun!"。输出最终结果。

示例代码:
```
str = "   Python Programming   "
# 请在这里编写代码
```

答案：
```
str = "   Python Programming   "
trimmed = str.strip()
upper = trimmed.upper()
result = upper + " is fun!"
print(result)  # 输出 "PYTHON PROGRAMMING is fun!"
```

**题目 3: 字符串格式化**

编写一个 Python 程序，创建一个整数变量 score 赋值为 85，创建一个字符串变量 student 赋值为 "John"。使用 f-string 格式化字符串，输出 "Student John scored 85 points"。

示例代码:
```
score = 85
student = "John"
# 请在这里编写代码
```

答案：
```
score = 85
student = "John"
formatted = f"Student {student} scored {score} points"
print(formatted)  # 输出 "Student John scored 85 points"
```
