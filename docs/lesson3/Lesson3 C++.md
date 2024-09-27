# Lesson 3 C++ 的自定义函数与参数

## 目录
- [1. C++函数的定义和使用](#1-c函数的定义和使用)
  - [1.1 函数的定义语法](#11-函数的定义语法)
  - [1.2 返回类型](#12-返回类型)
  - [1.3 函数名命名规则](#13-函数名命名规则)
- [2. 形式参数与实际参数](#2-形式参数与实际参数)
  - [2.1 形式参数（Formal Parameters）](#21-形式参数formal-parameters)
  - [2.2 实际参数（Actual Arguments）](#22-实际参数actual-arguments)
  - [2.3 总结](#23-总结)
- [3. 函数的定义和调用示例](#3-函数的定义和调用示例)
  - [3.1 定义一个不返回值的函数](#31-定义一个不返回值的函数)
  - [3.2 定义一个带参数的函数](#32-定义一个带参数的函数)
  - [3.3 带返回值的函数](#33-带返回值的函数)

- [4. 参数传递方式](#4-参数传递方式)
  - [4.1 值传递（Pass-by-Value）](#41-值传递pass-by-value)
  - [4.2 引用传递（Pass-by-Reference）](#42-引用传递pass-by-reference)
- [5. 课后练习](#5-课后练习)
  - [5.1 函数的定义](#51-函数的定义)
  - [5.2 形式参数与实际参数判断题](#52-形式参数与实际参数判断题)


## 1. C++函数的定义和使用

函数是C++编程的基础构建模块之一，它可以帮助我们将复杂的程序划分为更小的、独立的部分，每个部分完成特定的任务。这样不仅使代码更加清晰和易于维护，还增强了代码的可重用性。

### 1.1 函数的定义语法

在C++中，函数的定义通常遵循以下结构：

```cpp
返回类型 函数名(参数列表) {
    // 函数体
    // 在这里编写函数执行的具体操作
    // 函数可以使用传入的参数，并且可能会返回一个值
}
```

- **返回类型（Return Type）：** 这是函数返回值的类型。如果函数不需要返回任何值，就使用 `void` 作为返回类型。常见的返回类型有 `int`、`float`、`double`、`char` 和 `string` 等。
- **函数名（Function Name）：** 函数的名称，用来在程序中调用这个函数。函数名应尽量简洁明了，并能反映函数的功能。
- **参数列表（Parameter List）：** 这是函数接收的输入数据，多个参数用逗号分隔。如果函数不需要任何输入参数，参数列表可以为空。
- **函数体（Function Body）：** 包含了函数执行的具体操作。这部分代码实现了函数的核心逻辑，是函数的主体。

**示例：**

```cpp
int add(int a, int b) {
    return a + b;
}
```

在上述示例中，`add` 函数接收两个整数作为参数，返回它们的和。



### 1.2 返回类型

返回类型决定了函数返回给调用者的数据类型。例如，如果编写一个函数来计算两个数字的乘积，函数的返回类型可以是 `int`、`float` 等。函数可以返回任何数据类型的值，包括自定义的类型。

如果一个函数不需要返回任何值，比如它仅用于打印信息，则返回类型为 `void`。

**示例：**

```cpp
// 返回一个整数
int multiply(int a, int b) {
    return a * b;
}

// 不返回值
void printHello() {
    std::cout << "Hello, World!" << std::endl;
}
```

### 1.3 函数名命名规则

函数名用于标识和调用函数。选择一个有意义的函数名可以让代码更易读和理解。以下是一些命名规则和建议：

- **使用有意义的名称：** 函数名应能反映函数的功能。例如，`calculateSum` 比 `func1` 更具描述性。
- **遵循命名规范：** 通常使用小写字母和驼峰式命名法（camelCase），如 `getUserInput`。
- **避免使用保留字：** 不要使用C++的保留关键字作为函数名，如 `int`、`return` 等。
- **简洁明了：** 函数名应简短明了，便于记忆和调用。

**示例：**

```cpp
// 合适的函数名
double calculateArea(double radius);

// 不推荐的函数名
double func1(double a);
```

## 2. 形式参数与实际参数

在C++中，函数可以接收外部输入，这些输入被称为参数。参数分为形式参数（形参）和实际参数（实参）。理解这两者的区别对于正确使用函数非常重要。

### 2.1 形式参数（Formal Parameters）

形式参数是在函数定义时声明的参数，它们作为函数的一部分，用来接收调用函数时传递的实际参数的值。形式参数在函数定义的括号内部声明，并指定它们的类型和名称。

**示例：**

```cpp
void calculateSum(int a, int b) {
    int sum = a + b;
    std::cout << "Sum: " << sum << std::endl;
}
```

在这个例子中，`calculateSum` 是一个函数，它接受两个形式参数 `a` 和 `b`，它们的类型都是 `int`。这些形式参数在函数被调用时用于接收传递给函数的实际参数的值。

### 2.2 实际参数（Actual Arguments）

实际参数是在调用函数时传递给函数的值或者表达式。它们是真正用来执行函数操作的数据。在函数调用时，实际参数被传递给函数的形式参数。

**示例：**

```cpp
#include <iostream>

void calculateSum(int a, int b) {
    int sum = a + b;
    std::cout << "Sum: " << sum << std::endl;
}

int main() {
    int num1 = 10;
    int num2 = 20;

    // 调用函数并传递实际参数
    calculateSum(num1, num2);

    return 0;
}
```

**解释：**
- 在这个示例中，`num1` 和 `num2` 是 `main` 函数中的两个变量，它们作为实际参数传递给 `calculateSum` 函数。
- 在函数调用 `calculateSum(num1, num2);` 中，`num1` 和 `num2` 分别传递给 `a` 和 `b` 形式参数，进而在函数内部计算它们的和。

### 2.3 总结

- **形式参数** 是在函数定义中声明的变量，它们用于接收实际参数的值。
- **实际参数** 是在函数调用时传递给函数的值或表达式，它们被传递给形式参数，用于函数执行。

理解形式参数和实际参数的区别，有助于正确传递数据到函数，并确保函数能够正确处理输入。

## 3. 函数的定义和调用示例

### 3.1 定义一个不返回值的函数

在C++中，函数不一定需要返回值。当一个函数执行某些操作，但不需要返回任何值时，我们可以使用 `void` 作为返回类型。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个不返回值的函数
void printHello() {
    // 打印一条消息
    cout << "Hello, World!" << endl;
}

int main() {
    // 调用 printHello 函数
    printHello();
    return 0;
}
```

**解释：**
- `printHello` 函数没有参数（空括号表示没有参数），返回类型是 `void`，表示它不返回任何值。
- 函数体里只有一行代码，用来打印 "Hello, World!"。
- 在 `main` 函数中，通过 `printHello();` 调用这个函数，函数会执行其代码。



### 3.2 定义一个带参数的函数

带参数的函数能够接收外部传递的数据，以完成特定的任务。

#### 3.2.1 带一个参数的函数

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个带有一个参数的函数
void printNumber(int num) {
    cout << "The number is: " << num << endl;
}

int main() {
    int myNumber = 10;
    // 调用 printNumber 函数并传递参数
    printNumber(myNumber);
    return 0;
}
```

**解释：**
- `printNumber` 函数接收一个 `int` 类型的参数 `num`，然后打印这个数字。
- 在 `main` 函数中，通过 `printNumber` 调用函数，并传递变量 `myNumber` 作为参数。

#### 3.2.2 带多个参数的函数

函数也可以接受多个参数，并使用这些参数来执行更复杂的操作。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个带有两个参数的函数
void printSum(int a, int b) {
    int sum = a + b;
    cout << "Sum: " << sum << endl;
}

int main() {
    int num1 = 10;
    int num2 = 20;
    // 调用 printSum 函数并传递参数
    printSum(num1, num2);
    return 0;
}
```

**解释：**
- `printSum` 函数接收两个 `int` 类型的参数 `a` 和 `b`，计算它们的和并打印。
- 在 `main` 函数中，通过 `printSum` 调用函数，并传递 `num1` 和 `num2` 作为参数。

### 3.3 带返回值的函数

在C++中，函数可以返回多种类型的值：

#### 3.3.1 定义一个返回`int`类型的函数

在C++中，我们可以定义一个返回具体值的函数。以下示例展示了一个返回两个整数乘积的函数。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个返回两个整数乘积的函数
int multiply(int a, int b) {
    // 计算乘积并返回结果
    return a * b;
}

int main() {
    int num1 = 5;
    int num2 = 7;
    // 调用 multiply 函数并保存返回值
    int result = multiply(num1, num2);
    cout << "Multiplication Result: " << result << endl;
    return 0;
}
```
**解释：**
- `multiply` 函数接受两个 `int` 类型的参数 `a` 和 `b`，返回类型是 `int`，表示它会返回一个整数。
- 函数体中，使用 `a * b` 计算乘积，并使用 `return` 语句将结果返回。
- 在 `main` 函数中，调用 `multiply` 函数，并将返回的结果保存在变量 `result` 中，最后将结果输出到屏幕上。

#### 3.3.2 定义一个返回`string`类型的函数

我们还可以定义一个返回 `string` 类型的函数。以下是一个示例，展示了如何连接两个字符串并返回结果。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个连接两个字符串的函数
string concatenateStrings(string str1, string str2) {
    // 连接字符串并返回结果
    return str1 + " " + str2;
}

int main() {
    string firstName = "John";
    string lastName = "Doe";
    // 调用 concatenateStrings 函数并保存返回值
    string fullName = concatenateStrings(firstName, lastName);
    cout << "Full Name: " << fullName << endl;
    return 0;
}
```

**解释：**
- `concatenateStrings` 函数接受两个 `string` 类型的参数 `str1` 和 `str2`，返回类型是 `string`。
- 函数体中，使用 `+` 运算符连接两个字符串，并在它们之间加了一个空格，然后返回连接后的字符串。
- 在 `main` 函数中，调用 `concatenateStrings` 函数，并将返回的完整姓名保存在变量 `fullName` 中，最后将结果输出到屏幕上。

#### 3.3.3 返回 `float` 类型的函数

`float` 类型用于存储带小数点的数字。你可以定义一个返回 `float` 类型的函数，执行浮点数运算。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个返回两个浮点数和的函数
float addFloats(float a, float b) {
    return a + b;
}

int main() {
    float num1 = 5.5;
    float num2 = 7.3;
    // 调用 addFloats 函数并接收返回值
    float result = addFloats(num1, num2);
    cout << "Sum of floats: " << result << endl;
    return 0;
}
```

**解释：**
- `addFloats` 函数接受两个 `float` 类型的参数 `a` 和 `b`，返回它们的和。
- 在 `main` 函数中，通过调用 `addFloats` 并接收返回的浮点数结果，然后打印输出。

#### 3.3.4 返回 `bool` 类型的函数

`bool` 类型用于表示布尔值，即 `true`（真）或 `false`（假）。你可以编写一个函数来比较两个数字，并返回一个布尔值。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个比较两个整数大小的函数
bool isGreater(int a, int b) {
    return a > b;
}

int main() {
    int num1 = 10;
    int num2 = 20;
    // 调用 isGreater 函数并接收返回值
    bool result = isGreater(num1, num2);
    cout << "Is num1 greater than num2? " << (result ? "Yes" : "No") << endl;
    return 0;
}
```

**解释：**
- `isGreater` 函数接受两个 `int` 类型的参数 `a` 和 `b`，并返回一个 `bool` 类型的值，表示 `a` 是否大于 `b`。
- 在 `main` 函数中，通过调用 `isGreater` 并接收返回的布尔值，然后根据结果输出 "Yes" 或 "No"。

#### 3.3.5 返回 `char` 类型的函数

`char` 类型用于存储单个字符。你可以定义一个返回 `char` 类型的函数，处理字符数据。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个获取字符串第一个字符的函数
char getFirstChar(string str) {
    return str[0];
}

int main() {
    string name = "Alice";
    // 调用 getFirstChar 函数并接收返回值
    char firstChar = getFirstChar(name);
    cout << "The first character is: " << firstChar << endl;
    return 0;
}
```

**解释：**
- `getFirstChar` 函数接受一个 `string` 类型的参数 `str`，并返回该字符串的第一个字符。
- 在 `main` 函数中，通过调用 `getFirstChar` 并接收返回的字符，然后打印输出。

## 4. 参数传递方式

在C++中，函数的参数传递方式有两种：值传递（pass-by-value）和引用传递（pass-by-reference）。理解这两种方式的区别对于编写高效和正确的代码至关重要。

### 4.1 值传递（Pass-by-Value）

值传递是将实际参数的值复制到函数的形参变量中。函数内部对参数的修改不会影响实际参数。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个带有值传递的函数
void increment(int a) {
    a++;
}

int main() {
    int num = 10;
    increment(num);
    cout << "After increment: " << num << endl; // 输出：10
    return 0;
}
```

**解释：**
- 在这个示例中，`increment` 函数对参数 `a` 进行了自增操作，但 `main` 函数中的变量 `num` 不受影响，因为 `a` 是 `num` 的副本。

### 4.2 引用传递（Pass-by-Reference）

引用传递将参数的引用传递给函数。函数内部对参数的修改会直接影响实际参数。

**示例：**

```cpp
#include <iostream>
using namespace std;

// 定义一个带有引用传递的函数
void increment(int& a) {
    a++;
}

int main() {
    int num = 10;
    increment(num);
    cout << "After increment: " << num << endl; // 输出：11
    return 0;
}
```

**解释：**
- 在这个示例中，`increment` 函数接受一个引用参数 `a`，对 `a` 的修改会直接影响 `main` 函数中的变量 `num`。

## 5. 课后练习

通过练习，可以巩固对函数定义和参数传递的理解。以下是一些练习题，帮助你更好地掌握本节内容。

### 5.1 函数的定义

请将下列代码（Lesson2课后练习）的点单、打印客户点单内容、计算订单总价三个功能封装成独立的方法。

**原始代码：**

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    // 定义价格常量
    const double BURGER_PRICE = 12.5;
    const double FRIES_PRICE = 6.0;
    const double COKE_PRICE = 4.5;

    // 初始化总销售额
    double totalSales = 0.0;

    // 开始循环，直到顾客选择退出
    while (true) {
        // 初始化点单数量
        int option = 0;
        int burgers = 0;
        int fries = 0;
        int cokes = 0;

        // 获取用户点单
        cout << "\n请点单（输入-1退出，其他整数进入点单）：";
        cin >> option;

        // 如果输入为-1，则退出循环
        if (option == -1) {
            break;
        }
        
        cout << "请输入汉堡的数量：";
        cin >> burgers;

        cout << "请输入薯条的数量：";
        cin >> fries;

        cout << "请输入可乐的数量：";
        cin >> cokes;

        // 打印客户点单内容
        cout << "\n客户点单内容：" << endl;
        if (burgers > 0) {
            cout << "汉堡 x " << burgers << endl;
        }
        if (fries > 0) {
            cout << "薯条 x " << fries << endl;
        }
        if (cokes > 0) {
            cout << "可乐 x " << cokes << endl;
        }

        // 计算本次点单的总价
        double orderTotal = burgers * BURGER_PRICE + fries * FRIES_PRICE + cokes * COKE_PRICE;
        // 累加到总销售额
        totalSales += orderTotal;

        // 打印本次点单的总价
        cout << "\n本次点单总价：" << orderTotal << " 元" << endl;
    }

    // 打印所有顾客的总销售额
    cout << "\n所有顾客的总销售额：" << totalSales << " 元" << endl;

    return 0;
}
```

**参考答案：**

```cpp
#include <iostream>
#include <string>

using namespace std;

// 定义价格常量
const double BURGER_PRICE = 12.5;
const double FRIES_PRICE = 6.0;
const double COKE_PRICE = 4.5;

// 获取用户的点单选项
int getUserOption() {
    int option;
    cout << "\n请点单（输入-1退出，其他整数进入点单）：";
    cin >> option;
    return option;
}

// 获取特定商品的数量
int getQuantity(const string& itemName) {
    int quantity;
    cout << "请输入" << itemName << "的数量：";
    cin >> quantity;
    return quantity;
}

// 打印客户点单内容
void printOrderDetails(int burgers, int fries, int cokes) {
    cout << "\n客户点单内容：" << endl;
    if (burgers > 0) {
        cout << "汉堡 x " << burgers << endl;
    }
    if (fries > 0) {
        cout << "薯条 x " << fries << endl;
    }
    if (cokes > 0) {
        cout << "可乐 x " << cokes << endl;
    }
}

// 计算订单总价
double calculateOrderTotal(int burgers, int fries, int cokes) {
    return burgers * BURGER_PRICE + fries * FRIES_PRICE + cokes * COKE_PRICE;
}

int main() {
    double totalSales = 0.0;

    while (true) {
        int option = getUserOption();

        if (option == -1) {
            break;
        }

        int burgers = getQuantity("汉堡");
        int fries = getQuantity("薯条");
        int cokes = getQuantity("可乐");

        printOrderDetails(burgers, fries, cokes);
        double orderTotal = calculateOrderTotal(burgers, fries, cokes);
        totalSales += orderTotal;

        cout << "\n本次点单总价：" << orderTotal << " 元" << endl;
    }

    cout << "\n所有顾客的总销售额：" << totalSales << " 元" << endl;

    return 0;
}
```

**说明：**

- **`getUserOption` 函数：** 负责获取用户的点单选项。
- **`getQuantity` 函数：** 负责获取特定商品的数量，参数为商品名称。
- **`printOrderDetails` 函数：** 负责打印客户的点单内容，参数为各商品的数量。
- **`calculateOrderTotal` 函数：** 负责计算订单的总价，参数为各商品的数量，返回订单总价。
- **`main` 函数：** 负责控制程序的流程，调用上述函数实现点单、计算和打印功能。

通过将不同的功能封装成独立的函数，代码结构更加清晰，便于维护和扩展。

### 5.2 形式参数与实际参数判断题

**题目：** 观察以下代码，判断参数 `x` 和 `y` 是实际参数还是形式参数，它们是否会被修改，`modifyValues` 方法是否会对它们产生影响。选择正确的答案并解释原因。

```cpp
#include <iostream>
using namespace std;

void modifyValues(int a, int b) {
    a = a * 2;
    b = b + 3;
}

int main() {
    int x = 5;
    int y = 10;
    modifyValues(x, y);
    cout << "x = " << x << ", y = " << y << endl;
    return 0;
}
```

**A. 正确，`x` 和 `y` 的值会被修改**

**B. 错误，`x` 和 `y` 的值不会被修改**

**答案：** B. 错误

**理由：** 在 C++ 中，函数参数是按值传递的。当 `modifyValues` 函数被调用时，`a` 和 `b` 是 `x` 和 `y` 的副本，对它们的修改不会影响到原始的 `x` 和 `y`。因此，`x` 和 `y` 的值不会被修改，输出仍然是 `x = 5, y = 10`。
