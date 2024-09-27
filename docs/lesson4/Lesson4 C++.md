# Lesson 4 字符串基础

## 目录
- [4.1 创建字符串](#41-创建字符串)
- [4.2 访问字符串中的值](#42-访问字符串中的值)
- [4.3 字符串连接与更新](#43-字符串连接与更新)
- [4.4 C++ 字符串格式化](#44-c-字符串格式化)
- [4.5 C++ 转义字符](#45-c-转义字符)
- [4.6 C++ 字符串运算符](#46-c-字符串运算符)
- [4.7课后练习](#47-课后练习)

## 4.1 创建字符串

C++中使用 `std::string` 类来表示字符串，可以使用双引号 `" "` 来创建字符串变量。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string var1 = "Hello World!";
    string var2 = "CodeRaft";

    return 0;
}
```

## 4.2 访问字符串中的值

C++中访问字符串中的字符可以使用索引，索引从0开始。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string var1 = "Hello World!";
    char firstChar = var1[0]; // 获取索引为0的字符 'H'
    string substr = var1.substr(1, 4); // 截取字符串 var1 的第2到第5个字符（"ello"）

    cout << "First character: " << firstChar << endl;
    cout << "Substring: " << substr << endl;

    return 0;
}
```

## 4.3 字符串连接与更新

在C++中，字符串是可变的，这意味着你可以修改它们的内容。字符串连接是将两个或多个字符串合并成一个新的字符串。C++ 提供了多种方法来实现字符串的连接和更新，包括使用 `+` 操作符和 `append` 方法。

### 4.3.1 使用 `+` 操作符连接字符串

`+` 操作符是最常用的字符串连接方式，它将两个字符串合并，并返回一个新的字符串。你还可以将连接后的字符串赋值给原变量，从而更新字符串的值。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string var1 = "Hello";
    var1 = var1 + " CodeRaft!"; // 连接字符串并更新 var1
    cout << var1 << endl;

    return 0;
}
```
- 在这个示例中，字符串 `var1` 的初始值为 `"Hello"`。
- 通过使用 `+` 操作符，将 `" CodeRaft!"` 连接到 `var1` 上，并将结果赋值回 `var1`，从而更新了 `var1` 的值。
- 最终输出的字符串是 `"Hello CodeRaft!"`。

### 4.3.2 使用 `append` 方法连接字符串

`append` 方法是另一个用于连接字符串的常用方式，它直接将一个字符串追加到另一个字符串的末尾，并更新原始字符串。

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string var1 = "Hello";
    var1.append(" CodeRaft!"); // 使用 append 方法连接字符串并更新 var1
    cout << var1 << endl;

    return 0;
}
```

- 在这个示例中，`var1` 的初始值为 `"Hello"`。
- 使用 `append` 方法，将 `" CodeRaft!"` 追加到 `var1` 的末尾。
- `append` 方法会修改 `var1`，使其更新为 `"Hello CodeRaft!"`。
- 最终输出的字符串与上一个示例相同，都是 `"Hello CodeRaft!"`。

## 4.4 C++ 字符串格式化

C++中可以使用 `sprintf` 函数进行字符串格式化，或者使用 `std::ostringstream` 进行格式化输出。

### 4.4.1 使用 `sprintf`

```cpp
#include <iostream>
#include <string>
#include <cstdio>
using namespace std;

int main() {
    char buffer[100];
    string name = "CodeRaft";
    int age = 10;
    sprintf(buffer, "我叫 %s 今年 %d 岁!", name.c_str(), age);
    string formattedString = buffer;

    cout << formattedString << endl;

    return 0;
}
```

### 4.4.2 使用 `std::ostringstream`

```cpp
#include <iostream>
#include <string>
#include <sstream>
using namespace std;

int main() {
    ostringstream oss;
    string name = "CodeRaft";
    int age = 10;

    oss << "我叫 " << name << " 今年 " << age << " 岁!";
    string formattedString = oss.str();

    cout << formattedString << endl;

    return 0;
}
```

### 4.4.3 格式化符号

- **%s**：格式化字符串
- **%d**：格式化整数
- **%f**：格式化浮点数

### 示例

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <cstdio>
using namespace std;

int main() {
    string name = "小明";
    int age = 10;
    double height = 1.75;

    // 使用 sprintf 格式化字符串
    char buffer[100];
    sprintf(buffer, "我叫 %s，今年 %d 岁，身高 %.2f 米", name.c_str(), age, height);
    string formattedString1 = buffer;

    // 使用 ostringstream 格式化字符串
    ostringstream oss;
    oss << "我叫 " << name << "，今年 " << age << " 岁，身高 " << height << " 米";
    string formattedString2 = oss.str();

    cout << formattedString1 << endl; // 输出：我叫 小明，今年 10 岁，身高 1.75 米
    cout << formattedString2 << endl; // 输出：我叫 小明，今年 10 岁，身高 1.75 米

    return 0;
}
```

## 4.5 C++ 转义字符

在C++中，转义字符用于表示特殊字符和控制字符。以下是一些常见的转义字符示例：

| 转义字符 | 描述                                           | 示例                                |
| -------- | ---------------------------------------------- | ----------------------------------- |
| `\\`     | 反斜杠符号                                     | `cout << "\\" << endl;`   |
| `\'`     | 单引号                                         | `cout << "\'" << endl;`   |
| `\"`     | 双引号                                         | `cout << "\"" << endl;`   |
| `\n`     | 换行                                           | `cout << "Hello\nWorld!";`     |
| `\t`     | 制表符                                         | `cout << "Hello\tWorld!";`     |

### 示例代码

```cpp
#include <iostream>
using namespace std;

int main() {
    // 单引号
    cout << '\'' << endl; // 输出：'

    // 换行符
    cout << "Hello, world!\nHow are you?" << endl;

    // 制表符
    cout << "Hello, world!\tHow are you?" << endl;

    // 退格符
    cout << "Hello,\b world!" << endl;

    // ASCII 值
    char ch = 'A';
    cout << "A 对应的 ASCII 值为：" << static_cast<int>(ch) << endl;
    
    return 0;
}
```

## 4.6 C++ 字符串运算符

### 4.6.1 C++ 字符串运算符

1. **字符串连接运算符 `+`**

   字符串连接运算符 `+` 用于将两个字符串连接起来。

   **示例：**
   ```cpp
   string str1 = "Hello";
   string str2 = "World";
   string result = str1 + str2;
   cout << result << endl; // 输出：HelloWorld
   ```

2. **通过索引获取字符 `operator[]`**

   `operator[]` 用于获取字符串中指定位置的字符。

   **示例：**
   ```cpp
   string str = "Hello";
   char ch = str[1]; // 获取索引为1的字符，即第2个字符 'e'
   cout << ch << endl; // 输出：e
   ```

3. **截取子字符串 `substr()`**

   `substr()` 方法用于截取字符串的一部分。

   **示例：**
   ```cpp
   string str = "HelloWorld";
   string subStr = str.substr(3, 4); // 从索引3开始截取4个字符，即 "loWo"
   cout << subStr << endl; // 输出：loWo
   ```

4. **成员运算符 `find()` 和 `rfind()`**

   `find()` 和 `rfind()` 方法用于获取字符或字符串在目标字符串中第一次出现的位置索引和最后一次出现的位置索引。

   **示例

：**
   ```cpp
   string str = "HelloWorld";
   size_t firstIndex = str.find('o'); // 第一次出现 'o' 的位置索引，索引从0开始
   size_t lastIndex = str.rfind('o'); // 最后一次出现 'o' 的位置索引
   cout << "第一次出现 'o' 的位置索引：" << firstIndex << endl; // 输出：4
   cout << "最后一次出现 'o' 的位置索引：" << lastIndex << endl; // 输出：7
   ```

## 4.7 课后练习

**题目 1: 字符串索引与切片**

观察以下代码，输出结果是什么？

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "Hello, World!";
    string slice = str.substr(7, 5);
    cout << slice << endl;
    return 0;
}
```

A. Hello

B. World

C. World!

D. , Wor

**答案：** B. World

**理由：** `substr(7, 5)` 方法返回从索引 7 开始，长度为 5 的子字符串，即 "World"。

---

**题目 2: 字符串常用函数**

观察以下代码，输出结果是什么？

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = " C++ Programming ";
    int length = str.length();
    string lower = str;
    for (int i = 0; i < lower.length(); i++) {
        if (lower[i] >= 'A' && lower[i] <= 'Z') {
            lower[i] = lower[i] + ('a' - 'A'); // 转换为小写
        }
    }
    string concatenated = lower + " is fun!";
    cout << "Length: " << length << endl;
    cout << "Concatenated: " << concatenated << endl;
    return 0;
}
```

A. Length: 18; Concatenated: C++ programming is fun!

B. Length: 17; Concatenated: C++ programming is fun!

C. Length: 18; Concatenated: C++ programming is fun!

D. Length: 16; Concatenated: C++ programming is fun!

**答案：** C. Length: 18; Concatenated: C++ programming is fun!

**理由：** `length()` 返回字符串的长度，循环手动将所有大写字符转换为小写，`+` 运算符进行字符串拼接，结果是 "C++ programming is fun!"。

---

**题目 3: 字符串格式化**

观察以下代码，输出结果是什么？

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int age = 25;
    string name = "Alice";
    string formatted = "Name: " + name + ", Age: " + to_string(age);
    cout << formatted << endl;
    return 0;
}
```

A. Name: Alice, Age: 25

B. Name: %s, Age: %d

C. Name: Alice, Age: 25

D. Name: Alice, Age: age

**答案：** A. Name: Alice, Age: 25

**理由：** `+` 运算符用于字符串拼接，`to_string` 将整数转为字符串，结果是 "Name: Alice, Age: 25"。

---

### 代码题

**题目 1: 字符串索引与切片**

**题目：** 编写一个 C++ 程序，创建一个字符串 "Programming in C++"。使用 `substr` 方法提取并输出从索引 0 到索引 11 的子字符串。

**示例代码：**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "Programming in C++";
    // 请在这里编写代码
}
```

**答案：**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "Programming in C++";
    string substring = str.substr(0, 11);
    cout << substring << endl;  // 输出 "Programming"
    return 0;
}
```

---
**题目 2: 字符串常用函数**

**题目：** 编写一个 C++ 程序，创建一个字符串 `"   C++ Programming   "`。去除字符串前后的空白字符，转换为大写，并拼接 `" is fun!"`。输出最终结果。

**示例代码：**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "   C++ Programming   ";
    // 请在这里编写代码
}
```

**答案：**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str = "   C++ Programming   ";

    // 去除前导空格
    int start = 0;
    while (start < str.length() && str[start] == ' ') {
        start++;
    }

    // 去除后续空格
    int end = str.length() - 1;
    while (end >= 0 && str[end] == ' ') {
        end--;
    }

    // 截取去除空格后的字符串
    str = str.substr(start, end - start + 1);

    // 转换为大写
    for (int i = 0; i < str.length(); i++) {
        if (str[i] >= 'a' && str[i] <= 'z') {
            str[i] = str[i] - ('a' - 'A');
        }
    }

    // 拼接字符串
    string result = str + " IS FUN!";
    
    cout << result << endl;  // 输出 "C++ PROGRAMMING IS FUN!"
    return 0;
}
```

---

**题目 3: 字符串格式化**

**题目：** 编写一个 C++ 程序，创建一个整数变量 `score` 赋值为 85，创建一个字符串变量 `student` 赋值为 "John"。使用字符串拼接方法格式化字符串，输出 "Student John scored 85 points"。

**示例代码：**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int score = 85;
    string student = "John";
    // 请在这里编写代码
}
```

**答案：**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int score = 85;
    string student = "John";
    string formatted = "Student " + student + " scored " + to_string(score) + " points";
    cout << formatted << endl;  // 输出 "Student John scored 85 points"
    return 0;
}
```