# Lesson2 C++的条件语句与循环语句

## 1. C++的条件语句
以下是C++ 中的常见逻辑条件：

* 小于：`a < b`
* 小于或等于：`a <= b`
* 大于：`a > b`
* 大于或等于：`a >= b`
* 等于：`a == b`
* 不等于：`a != b`

可以通过使用这些条件来针对不同的决定执行不同的操作

#### C++ 具有以下条件语句：

* 使用 `if` 来指定一个代码块，如果指定的条件为 `true`，则执行该代码块
* 使用 `else` 来指定一个代码块，如果相同的条件为 `false`，则执行该代码块
* 使用 `else if` 来指定一个新的条件进行测试，如果第一个条件为 `false`，则执行该条件
* 使用 `switch` 来指定许多替代代码块来执行

### 1.1 if 语句
使用`if`语句来指定一个代码块，如果条件为`true`,则执行该代码块。
语法：
```cpp
if (condition) {
  // 如果条件为 true，则执行的代码块
}
```
请注意，`if`是小写字母。大写字母（`If` 或 `IF`）将生成错误。

以下为示例：
```cpp
int a = 20;
int b = 10;
if (a > b) {
  cout << "a is greater than b";
}
```

### 1.2 else 语句
如果 if 语句中的布尔表达式成立（true），则执行 if 语句中的代码块，如果不成立（false），则执行else语句中的代码块。

语法：
```cpp
if (condition) {
  // 如果条件为 true，则执行的代码块
} else {
  // 如果条件为 false，则执行的代码块
}
```
以下为示例：
```cpp
int a = 66;
int b = 666;
if (a > b) {
  cout << "a is greater than b";
}
else{
    cout << "a is smaller than b";
}
```

### 1.3 else if 语句
`else if`在第一个条件为 false 时指定一个新条件。
```cpp
if (condition1) {
  // 如果 condition1 为 true，则执行的代码块
} else if (condition2) {
  // 如果 condition1 为 false 且 condition2 为 true，则执行的代码块
} else {
  // 如果 condition1 和 condition2 均为 false，则执行的代码块
}
```
以下为示例：
```cpp
int a = 66;
int b = 666;
if (a > b) {
  cout << "a is greater than b";
}
else if (a == b){
    cout << "a is equal to b";
}
else {
    cout << "a is smaller than b";
}
```

### 1.4 switch 语句
`switch`语句用于根据不同的条件执行不同的代码块。相比于多重的`if-else`结构，当有多个条件需要判断时，`switch`语句显得更加清晰和简洁。

语法：
```cpp
switch (expression) {
    case constant1:
        // 代码块1
        break;
    case constant2:
        // 代码块2
        break;
    ...
    default:
        // 默认代码块
        break;
}
```
* `expression`: 是一个整数表达式（可以是int、char等类型）。
* `case`：每个case后跟一个常量值，当expression的值与该常量相等时，执行对应的代码块。
* `break`：表示退出switch语句。如果没有break，程序会继续执行后续的case代码块（即“穿透”）。
* `default`：当所有的case都不匹配时，执行default后的代码块。

以下为示例：
```cpp
#include <iostream>

int main() {
    int day = 3;
    switch (day) {
        case 1:
            std::cout << "Monday" << std::endl;
            break;
        case 2:
            std::cout << "Tuesday" << std::endl;
            break;
        case 3:
            std::cout << "Wednesday" << std::endl;
            break;
        case 4:
            std::cout << "Thursday" << std::endl;
            break;
        case 5:
            std::cout << "Friday" << std::endl;
            break;
        case 6:
            std::cout << "Saturday" << std::endl;
            break;
        case 7:
            std::cout << "Sunday" << std::endl;
            break;
        default:
            std::cout << "Invalid day" << std::endl;
            break;
    }

    return 0;
}
```

## 2. C++的循环语句
循环语句用于反复执行某段代码，直到满足特定条件。C++提供了三种基本的循环语句：
* `for`循环
* `while`循环

### 2.1 for 循环
语法：
```cpp
for (initialization; condition; increment/decrement) {
    // 循环体
}
```
* `initialization`：用于初始化循环控制变量，在循环开始前执行一次。通常用于定义并初始化循环计数器变量。例如：`int i = 0;`。
* `condition`：循环继续执行的条件表达式。在每次循环开始时进行计算，如果条件为true，则执行循环体；否则，退出循环，例如`i < 5`。
* `increment/decrement`：在每次循环体执行后执行的操作，通常用于更新循环控制变量,例如`i++`（递增），`i--`（递减）。

以下为示例（**顺序遍历**）：
```cpp
#include <iostream>

int main() {
    for (int i = 0; i < 5; i++) {
        std::cout << "i = " << i << std::endl;
    }
    return 0;
}
```

在这个例子中，`i`从0开始，每次循环`i`加1，直到`i`不小于5。输出结果为：
```cpp
i = 0
i = 1
i = 2
i = 3
i = 4
```

#### 倒序遍历
倒序遍历是指从一个较大的值开始，逐步递减循环变量，直到达到指定的条件为止。这种遍历方式与顺序遍历（从小到大递增）相反。在C++中，通过设置for循环的初始化条件、判断条件和递减操作，可以实现倒序遍历。

假设我们希望从一个较大的数字开始，逐步减少该数字，直到达到一个特定值。我们可以通过以下代码实现:
```cpp
#include <iostream>

int main() {
    for (int i = 5; i > 0; i--) {
        std::cout << "i = " << i << std::endl;
    }
    return 0;
}
```
在这个例子中，i 的初始值为5，每次循环i减1，直到i不大于0。输出结果为：
```cpp
i = 5
i = 4
i = 3
i = 2
i = 1
```

### 2.2 `while`循环

语法
```cpp
while (condition) {
    // 循环体
}
```
`condition`：在每次循环开始时计算。如果为`true`，执行循环体；否则，退出循环。

以下为示例：
```cpp
#include <iostream>

int main() {
    int i = 0;
    while (i < 5) {
        std::cout << "i = " << i << std::endl;
        i++;
    }
    return 0;
}
```
在这个例子中，`i`从0开始，每次循环`i`加1，直到`i`不小于5。输出结果与`for`循环相同。


## 3. Break 和 Continue

### 3.1 `break`语句

`break`语句用于立即退出循环，不再执行循环体中的其他代码，也不会继续进行下一次循环。

以下为示例
```cpp
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break; // 当i等于5时，退出循环
        }
        std::cout << "i = " << i << std::endl;
    }
    return 0;
}
```
在这个例子中，当`i`等于5时，`break`语句会立即退出循环。输出结果为：
```
i = 0
i = 1
i = 2
i = 3
i = 4
```

### 3.2 `continue`语句

`continue`语句用于跳过当前循环中的剩余代码，立即开始下一次循环。

##### 示例代码
```cpp
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue; // 如果i是偶数，跳过本次循环，继续下一次循环
        }
        std::cout << "i = " << i << std::endl;
    }
    return 0;
}
```
在这个例子中，当`i`是偶数时，`continue`语句会跳过当前循环的剩余部分，继续下一次循环。输出结果为：
```
i = 1
i = 3
i = 5
i = 7
i = 9
```


## 4. 课后练习

### 4.1 点餐程序

#### 题目描述：

设计一个简单的餐厅点单程序，程序能够连续接受多个顾客的点单。程序提前知道汉堡、薯条和可乐的价格。每位顾客可以选择点汉堡、薯条和可乐的数量，程序将输出每位顾客的点单内容和总价，最后输出所有顾客的总销售额。


#### 要求：

1. 程序开始时，定义汉堡、薯条和可乐的价格常量。
2. 使用循环语句连续接受顾客的点单，在开始计算前，可以设置一个专用的变量获取用户意图是继续点单还是退出（例：输入-1退出并计算总销售额，其他数字则进行下一轮点单）。
3. 每次接受顾客的点单后，输出顾客的点单内容和本次点单的总价。
4. 累加每位顾客的点单总价到总销售额中。
5. 退出点单后，输出所有顾客的总销售额。



#### 示例运行：

假设操作流程如下：

1. 第一位顾客点汉堡 2，薯条 1，可乐 3；
2. 第二位顾客点汉堡 1，薯条 2，可乐 2；
3. 选择退出程序。

程序的输出应如下所示：

```
请点单（输入-1退出）：
0
请输入汉堡的数量：1
请输入薯条的数量：2
请输入可乐的数量：3

客户点单内容：
汉堡 x 2
薯条 x 1
可乐 x 3

本次点单总价：48.5 元

请点单（输入-1退出）：
0
请输入汉堡的数量：1
请输入薯条的数量：2
请输入可乐的数量：2

客户点单内容：
汉堡 x 1
薯条 x 2
可乐 x 2

本次点单总价：35.0 元

请点单（输入-1退出）：
-1

所有顾客的总销售额：83.5 元

请点单（输入0退出）：
请输入汉堡的数量：0

所有顾客的总销售额：83.5 元
```

#### 参考解答：

```cpp
#include <iostream>
using namespace std;

int main() {
    // 定义价格常量
    const double BURGER_PRICE = 12.5;
    const double FRIES_PRICE = 6.0;
    const double COKE_PRICE = 4.5;

    // 初始化总销售额
    double totalSales = 0.0;

    // 创建输入流
    int option = 0;
    int burgers = 0, fries = 0, cokes = 0;

    // 开始循环，直到顾客选择退出
    while (true) {
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

### 4.2 计算并输出1到100之间所有不能被3整除的数的平方和

#### 题目描述：

编写一个程序，计算并输出1到100之间所有不能被3整除的数的平方和。在计算过程中，如果平方和超过1000，则停止计算并输出当前的平方和值。

#### 解题思路：

1. 使用一个循环来遍历从1到100的所有数。
2. 对于每个数，使用条件语句判断是否能被3整除：
    - 如果能被3整除，使用`continue`跳过这个数，不进行平方和的累加。
    - 如果不能被3整除，计算该数的平方，并累加到平方和变量中。
3. 在累加过程中，使用条件语句检查平方和是否超过1000：
    - 如果超过1000，则使用`break`停止循环。
4. 最终输出停止时的平方和值。

#### 参考解答：

```cpp
#include <iostream>

int main() {
    int sum = 0;

    for (int i = 1; i <= 100; i++) {
        if (i % 3 == 0) {
            continue; // 跳过能被3整除的数
        }

        int square = i * i;
        sum += square;

        if (sum > 1000) {
            std::cout << "当前平方和超过1000，停止计算。\n";
            std::cout << "当前平方和为: " << sum << "\n";
            break;
        }
    }

    if (sum <= 1000) {
        std::cout << "最终平方和为: " << sum << "\n";
    }

    return 0;
}
```

#### 示例运行和输出：

在运行上述代码时，会依次计算1到100之间所有不能被3整除的数的平方，并累加到平方和变量`sum`中。如果累加过程中发现平方和超过1000，则停止计算，并输出当前的平方和值。

输出示例：
```
当前平方和超过1000，停止计算。
当前平方和为: 1025
```