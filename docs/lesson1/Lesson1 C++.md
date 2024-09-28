# Lesson 1  C++的环境设置、数据类型、运算符和输入和输出

## 前言：为什么要学习C++

- C++是一门功能强大且灵活多样的面向对象编程语言，‌它具有多种特点，‌包括复杂性、‌面向对象、‌高效性能、‌低级内存操作、‌跨平台支持、‌多线程以及泛型编程。
- C++可以用于编写桌面应用程序、‌系统软件、‌游戏开发、‌实时系统和嵌入式系统应用程序等多种类型的应用程序。尽管C++在其传统领域中受到其他竞争语言的冲击，但其主要优势在于强大的抽象能力、高性能以及低功耗。
- 实用场景示例：
    - **游戏开发**：许多大型游戏和游戏引擎，如Unreal Engine和Unity的底层部分，都是用C++编写的。C++的高性能和对硬件资源的直接控制使其成为游戏开发的理想选择。

    - **系统软件**：操作系统、驱动程序和嵌入式系统等需要高效性能和低级硬件访问的软件，通常使用C++编写。例如，Windows操作系统的许多部分都是用C++实现的。

    - **金融行业**：高频交易系统和实时分析工具等对性能要求极高的应用程序，经常用C++开发。C++的低延迟特性在金融领域尤其重要。

    - **嵌入式系统**：许多嵌入式设备，如家用电器、汽车控制系统和物联网设备，都使用C++编程。C++允许开发者在受限的硬件资源环境中编写高效的代码。

    - **科学计算**：在需要处理大量数据和复杂计算的科学研究领域，C++经常被用来开发高性能计算程序。诸如CERN的大型强子对撞机数据分析软件就是用C++编写的。

通过这些实际案例，可以更好地理解C++在不同领域的应用和重要性。学习C++不仅可以增强编程能力，还能为进入多个高需求行业打下坚实的基础。

本文档涉及范围对标大学计算机大一入门课程，帮助大学学生以及准备学习算法竞赛的初高中生，入门C++编程语言，通过针对性算法训练掌握语法和基础算法，为下一阶段学习做准备。
## 1. C++环境配置

### 1.1 下载 VS Code

- 访问 Visual Studio Code 官方网站 https://code.visualstudio.com/
- 点击“Download”按钮，选择适合你操作系统的安装程序（Windows、macOS 或 Linux）。

![](https://i.imgur.com/d5496B6.png)



### 1.2 安装 VS Code

- 下载完成后，运行安装程序。
- 按照安装向导完成安装过程。

    
### 1.3 安装 C++ 插件

#### 1.3.1 启动 VS Code
- 安装完成后，启动 VS Code。
#### 1.3.2 安装 C++ 插件
- 点击左侧活动栏中的“Extensions”图标（或按 Ctrl+Shift+X）。
- 在搜索框中输入 C++。
- 找到并安装由 Microsoft 发布的“C/C++”扩展。
![](https://i.imgur.com/d7yZSlQ.png)
安装完成后，点击"重新加载"按钮重新加载VSCode或重启VSCode

### 1.4 安装C++编译器
#### 1.4.1 检查是否已安装编译器
如果你想要检查你的电脑上是否已经安装了 GNU Compiler Collection (GCC) 或者 Clang 编译器，可以按照以下步骤操作：
1. 打开 VSCode，然后打开一个新的终端窗口（使用快捷键 ``` ⌃⇧` ``` 或 点击左上角查看->终端）。
2. 输入以下命令来检查 GCC 编译器 g++ 的版本:
   `g++ --version`
   或者使用以下命令来检查 Clang 编译器 clang 的版本：
   `clang --version`
3. 如果你的电脑已经安装了对应的编译器，命令会显示编译器的版本信息和详细内容。
4. 如果没有找到对应的编译器，确保你的编译器可执行文件在系统的路径中（在 Windows 下是 `%PATH`，Linux 和 macOS 下是 `$PATH`），这样 C/C++ 扩展就可以找到它。

**如果没有安装对应的编译器**，可以按照下面的步骤安装一个编译器。



#### 1.4.2 对于 Windows 用户：
Windows 常用的C/C++编译器是**MSVC**和**MinGW**。你可以选择其中一种进行安装,此处展示MSVC安装教程
##### MSVC 安装和配置教程
1. 安装步骤：
   - 打开链接 https://visualstudio.microsoft.com/zh-hans/downloads/
   - 将页面划到最底下的“所有下载”，并找到“用于 Visual Studio 的工具”
    ![](https://i.imgur.com/EgQWq2K.png)
   - 点击下载Visual Stuio 2022 生成工具
   - 下载完成后打开，这将启动 Visual Studio 安装程序，勾选 “使用C++的桌面开发”，然后选择安装按钮进行安装。
    ![](https://i.imgur.com/pHk8hdA.png)
2. 检查你的 Microsoft Visual C++ 安装是否成功
   - 在 Windows 开始菜单中搜索 "developer"，选择合适的 Visual Studio 开发人员命令提示符版本（根据你安装的 Visual Studio 或 Build Tools 版本选择）。
    ![](https://i.imgur.com/mfkxCC4.png)
   - 在打开的命令提示符窗口中，输入 `cl` 并按下 `Enter` 键。
   - 如果编译器正确安装，你应该会看到一个包含版本号和基本使用说明的版权信息.


#### 1.4.2 对于 macOS 用户：
##### 检查是否已安装Clang
- 打开终端，运行命令 `clang --version`

##### 如果没有，则安装Clang:
- 打开终端，运行命令 ```xcode-select --install```
- 安装完成后，运行命令检查  ```clang --version```

### 1.5 C++编译&运行

#### C++的运行过程

C++程序的运行必须经过编写、编译和运行 3 个步骤。

- 编写：在 C++ 开发环境中编写程序代码，形成后缀名为 .cpp 的 C++ 源文件
- 编译：使用 C++ 编译器（如 g++ 命令）对源文件进行编译。如果源代码中没有语法错误，编译器会生成目标文件（通常是后缀为 .o 或 .obj 的文件）以及最终的可执行文件（在 Linux 上通常没有后缀，在 Windows 上通常是 .exe 文件）。
- 运行：通过操作系统直接运行生成的可执行文件。C++ 生成的可执行文件是平台相关的，必须在生成该文件的平台上运行，或者使用相应的工具进行跨平台执行。

    ![](https://i.imgur.com/zSpGhlj.png)


## 2. 第一个程序：Hello World！
### C++常用的集成开发环境（IDE）

集成开发环境（Integrated Development Environment，简称IDE）是一种软件工具，提供了一套集成的功能和工具，用于开发、编写、测试和调试软件应用程序。

IDE通常包括以下核心组件：代码编辑器、编译器/解释器、调试器、构建工具、版本控制系统集成、图形用户界面设计器、项目管理工具。

通过集成这些功能和工具，IDE可以提高开发人员的生产力，简化开发过程，并提供更好的代码质量和可维护性。IDE通常与特定的编程语言或开发平台相关，例如C++开发中常用的Visual Studio、CLion和Eclipse CDT等。

这些 IDE 都具有丰富的功能集，能够显著提高 C++ 开发人员的生产力，简化开发过程，并通过强大的工具和集成环境提高代码质量和可维护性。选择适合的 IDE 取决于个人偏好、团队需求以及项目特点。

针对 C++ 开发，以下是几个常用的集成开发环境（IDE）：
#### Visual Studio (Microsoft)
    
- 官网: https://visualstudio.microsoft.com/
- Visual Studio 提供了多个版本，包括 Community（免费）、Professional 和 Enterprise。
- 它是一个功能强大的 IDE，支持多种语言，包括 C++。Visual Studio 提供了丰富的调试工具、图形化界面设计、代码分析和优化等功能，特别适合 Windows 平台的 C++ 开发。
#### CLion (JetBrains)
- 官网: https://www.jetbrains.com/clion/
- CLion 是 JetBrains 公司专门为 C++ 开发者设计的 IDE。它集成了智能代码编辑、强大的调试器、版本控制等功能，支持跨平台开发（Windows、macOS 和 Linux）。
- CLion 提供了许多现代化的工具和功能，能够显著提高 C++ 开发的效率和代码质量。
#### Eclipse CDT (Eclipse)
- 官网: https://www.eclipse.org/cdt/
- Eclipse CDT 是 Eclipse 的 C/C++ 开发工具集成，提供了丰富的功能如代码编辑、调试、版本控制等。它是一个开源、跨平台的 IDE，适合需要灵活配置和丰富插件支持的开发者使用。


这里以 VSCode为例展示如何使用IDE编写你的第一个Hello World 程序：

打开终端（MacOS）/ Developer Command Prompt for VS（Windows）并输入以下命令：
```shell
mkdir projects
cd projects
mkdir helloworld
cd helloworld
code .
```
以上命令会依次在默认路径下创建 projects 文件夹、helloworld 子文件夹，并在 helloworld 文件夹中打开 VS Code。

#### 常见问题：
**如果在 Windows 上`mkdir`后显示“拒绝访问”：**

- 可以尝试退出后右键单击 "Developer Command Prompt for VS"
- 选择 "以管理员身份运行"。
- 在管理员权限的窗口中尝试再次运行以上 `mkdir` 命令

**如果在 Mac 上输入`code .` 后显示 `command not found`:**

- 打开 VSCode，按下 `Command + Shift + P` 打开命令面板。
输入 "shell command" 并选择 "Shell Command: Install 'code' command in PATH" 选项。这会在终端中配置 code 命令的路径。
![](https://i.imgur.com/PPadh3d.png)
- 在终端再次尝试运行以上 `mkdir` 命令


##### 添加源代码文件
在 VS Code 的资源管理器标题栏中，选择“新文件”按钮，并命名为 ```helloworld.cpp```。
![](https://i.imgur.com/2IlBqfi.png)
##### 添加 Hello World 源代码
  将以下代码粘贴到 ```helloworld.cpp``` 文件中：
```cpp
#include <iostream>
using namespace std;

int main(){
    cout << "Hello World! " << endl;
}
```
按 `⌘S` (Mac) 或 `Ctrl+S` (Windows) 保存文件。保存后，文件资源管理器视图中会显示新添加的文件。
![](https://i.imgur.com/Id8g35j.png)

### 运行 `helloworld.cpp` 


- 点击右上角的 “运行 C/C++“ 
![](https://i.imgur.com/Rv281qF.png)
- 选择运行配置
    - **对于Windows用户：**
    选择 C/C++: cl.exe build and debug active file
    ![](https://i.imgur.com/xf2shmQ.png)
    运行的结果将会显示在集成终端中
    ![](https://i.imgur.com/obQLi1U.png)

    - **对于Mac用户：**
    选择 C/C++: clang++ build and debug active file
    ![](https://i.imgur.com/FbGTi9c.png)
    运行的结果将会显示在调试控制台
    ![](https://i.imgur.com/XSwJdhW.png)



**至此，恭喜你完成了你的第一个C++程序！:)**

## 4. C++中的标识符

### 4.1 标识符

标识符是指用来标识某个实体的一个符号。在C++语言中，标识符主要是指在编程时使用的名字。标识符的使用须遵循一定的规则：C++中的标识符由字母、数字和下划线组成，且必须以字母或下划线（_）开头。规则总结如下：

- 可以包含数字，但不能以数字开头。
- 除下划线（_）以外，不包含任何其他特殊字符，如空格。
- 不能用C++关键字或保留字做标识符。
- C++标识符大小写敏感。


合法的标识符，如：
```cpp
int a = 3;
int _123 = 3;
int myVar = 3;
int 变量1 = 3; //虽然合法，但不推荐使用中文
```
不合法的标识符，如：
```cpp
int 1a = 3; //不能使用数字开头
int a# = 3; //不能包含#这样的特殊字符
int int = 3; //不能使用关键字
```
注意：虽然C++的语法允许使用下划线（_）作为标识符的开始，但是在很多企业的开发规范中约定，不能使用下划线作为标识符的开始，以达到统一标识符格式，减少歧义的效果。

### 4.2 关键字和保留字

关键字和保留字是C++语言中具有特殊含义的单词或符号。关键字是C++语言本身定义的，用于表示特定的语法结构和操作，不能用作标识符，如变量名、类名等。

C++语言关键字如下所示：
![](https://i.imgur.com/4q4z1a7.jpeg)

- 这些关键字具有固定的语法含义，不能被用作变量名或其他标识符。
- 保留字是指被保留但目前未被使用的关键字，它们在C++语言中没有特定的功能，但为了保留未来可能使用的关键字而被保留。
- 我们在编写代码时应避免使用关键字作为标识符，以免引发编译错误或语法混淆。


## 5. C++中的变量

### 5.1 什么是变量
变量是C++程序中的基本存储单元，用于存储数据。变量本质上代表了内存中的一个存储区域，在这个区域中的数据可以在同一数据类型范围内不断变化。通过变量，程序可以方便地读取和操作该区域中的数据。

- 变量：顾名思义，会变的量。
- 常量：自然界中规定好了的、不会变的值。

### 5.2 变量的声明
在C++中，需要先声明一个变量，才能使用这个变量。变量的声明包含两点：变量的数据类型和变量名，语法格式如下：
```shell
数据类型 变量名； 
```

数据类型可以是C++的任意数据类型之一；变量名即变量的名称，用于存储变量值：
```cpp
int a;
char b;
```
可以同时声明多个同一数据类型的变量，变量之间用“,”隔开，例如：
```cpp
int c，d，e;
 
等同于：
 
int c;
int d;
int e;
```
### 5.3 变量的初始化

C++语法规定：变量可以不进行初始化，只声明后在使用前进行赋值。虽然C++允许未初始化的变量，但使用未初始化的变量会导致不确定的行为。变量的第一次赋值即对变量的初始化。在C++中，使用等号(=)实现变量的赋值。

变量的初始化有以下两种方式：

1、在声明变量时，同时对变量进行初始化，语法如下：
```cpp
数据类型 变量名 = 初始值；
 
例如：
int f = 5;
```
2、第一次使用变量前，对变量进行初始化，语法如下：
```cpp
数据类型 变量名；
    ……
变量名 = 初始值；
例如：
 
int sum;                  // 声明变量sum
cout << sum << endl;  // 报错，不能使用未赋值的变量
sum = 100;                // 给变量sum赋值
cout << sum << endl;      // 正确，输出100
```
### 5.4 变量的访问

变量在声明和初始化后，可以对变量进行访问，包括读取变量的值和修改变量的值。代码如下：

```cpp
int sum = 100;           // 声明变量sum并初始化
cout << sum << endl;     // 输出变量的值 -> 100
sum = 200;               // 修改变量sum的值
cout << sum << endl;     // 再次输出变量的值 -> 200
```
变量的访问应注意以下几个方面：

1、变量的操作必须与类型匹配。

变量在声明时指定了类型，C++编译器会检测对该变量的操作是否与其他类型匹配，如果对变量的赋值或者操作与其类型不匹配，会产生编译错误，例如：

```cpp
//编译错误，变量a的类型为int整型，不能赋值为浮点类型的值
int a = 3.14;  
```

2、变量的数据类型只写一次。

变量在第一次声明的时候写数据类型，再次使用时不写数据类型，例如：
```cpp
int n;
n = 5;   // 正确，再次使用变量n时不写数据类型
int n = 10; // 错误，再次指定变量的数据类型会出现编译错误
```

3、未经声明的变量不能使用。

变量必须先声明，否则会出现编译错误，例如：

```cpp
k = 5;    
cout << k << endl;  // 编译错误，变量k没有声明
```

4、变量初始化后才可以使用。

C++允许声明变量而不初始化，但使用未初始化的变量会导致不可预测的结果，例如：
```cpp
int t;                             
cout << t << endl;  // 变量t没有初始化，可能输出垃圾值
```

## 6. C++的数据类型
C++的数据类型分为：基本数据类型、复合数据类型和指针类型等，本文档针对初学者，仅对基本数据类型进行详细介绍。

### 6.1 基本数据类型
C++基本数据类型包括4类：整数类型、浮点数类型、字符类型和布尔类型。

#### 6.1.1 整数类型
C++中的整数类型包括：int, short, long, long long型，它们之间的区别是宽度和范围的不同。 

##### int类型：
- 大小：通常为4字节（32位）。
- 范围：基于编译器和平台，一般范围为约-2,147,483,648到2,147,483,647。

##### short类型：
- 大小：通常为2字节（16位）。
- 范围：基于编译器和平台，一般范围为约-32,768到32,767。

##### long类型：
- 大小：通常为4字节（32位），但在一些平台上可能为8字节（64位）。
- 范围：基于编译器和平台，32位long类型的范围约为-2,147,483,648到2,147,483,647，64位long类型的范围更大。

##### long long类型：
- 大小：通常为8字节（64位）。
- 范围：基于编译器和平台，范围约为-9,223,372,036,854,775,808到9,223,372,036,854,775,807。

#### 6.1.2 浮点类型
在C++中，浮点数类型主要由 float 和 double 两种表示。

以下是关于这两种浮点数类型的说明：

##### float 类型：

- 字节数：通常为4字节（32位）。
- 表示范围：约 ±3.402823466e+38F （14位有效数字）。
- 精度：通常为6位有效数字。

初始化：可以使用浮点数常量、整数常量或转换来初始化。
```cpp
float f1 = 3.14f; // 使用浮点数常量初始化
float f2 = 10; // 使用整数初始化，会进行隐式类型转换
float f3 = static_cast<float>(5); // 使用显式类型转换初始化
```

##### double 类型：

- 字节数：通常为8字节（64位）。
- 表示范围：约 ±1.7976931348623158e+308 （15位有效数字）。
- 精度：通常为15位有效数字。

初始化：可以使用浮点数常量、整数常量或转换来初始化。
```cpp
double d1 = 3.14; // 使用浮点数常量初始化
double d2 = 10; // 使用整数初始化，会进行隐式类型转换
double d3 = static_cast<double>(5); // 使用显式类型转换初始化
```

##### 注意事项：

- 浮点数类型的精度是有限的，计算过程中可能会存在舍入误差。
- 使用浮点数进行计算时，尤其是比较大小或判断相等时，应考虑舍入误差可能导致的不精确性。可以使用适当的容差值进行比较。
- 在使用浮点数时，应注意避免除以零或进行无效的运算，这可能会导致NaN（非数字）的结果。
- 根据具体需求和精确性要求，选择适当的浮点数类型。如果需要更高的精度，则可以考虑使用 long double 类型，它的字节数通常为10或16字节。

#### 6.1.3 字符类型

在C++中，字符类型 char 用于表示单个字符，并使用ASCII编码。它是一种整数类型，通常占用1个字节（8位）。以下是关于 char 类型的一些说明：

初始化：

- char 类型可以通过单个字符来进行初始化。例如：
```cpp
char ch1 = 'A'; // 使用单引号初始化
char ch2 = 65; // 使用整数值初始化，对应ASCII码中的字符 'A'
char ch3 = '\n'; // 使用转义字符初始化，表示换行符
```

字符串：

- 在C++中，char 类型也可以用于表示字符数组，即字符串。字符串是由多个字符组成的字符序列，以null终止。例如：
```cpp
char str1[] = "Hello"; // 声明并初始化一个字符串
char str2[10]; // 声明一个字符数组（字符串）
strcpy(str2, "World"); // 将字符串复制到字符数组中
```

#### 6.1.4 布尔类型

在C++中，布尔类型 bool 用于表示逻辑值，只有两个取值：true 和 false。bool 类型主要用于控制流程和条件判断。

以下是布尔类型的一些说明：

初始化： 

- bool 类型可以通过 true 或者 false 来进行初始化。例如：
```cpp
bool flag1 = true; // 初始化为true
bool flag2 = false; // 初始化为false
```

条件判断：

- 布尔类型常用于条件判断，例如 if 语句和循环语句中。只有当条件为 true 时，相应的代码块才会执行。例如：
```cpp
bool isTrue = true;
if (isTrue) {
// 条件为真，执行这里的代码
cout << "Condition is true!";
}
```

逻辑运算：

- 布尔类型可以进行逻辑运算，包括逻辑与 &&、逻辑或 || 和逻辑非 !。逻辑运算的结果也是布尔类型。例如：
```cpp
bool condition1 = true;
bool condition2 = false;
bool result1 = condition1 && condition2; // 逻辑与，结果为false
bool result2 = condition1 || condition2; // 逻辑或，结果为true
bool result3 = !condition1; // 逻辑非，结果为false
```
比较运算：

- 布尔类型可以进行比较运算，如等于 == 和不等于 !=。比较运算的结果也是布尔类型。例如：
```cpp
bool result1 = (10 == 5); // 结果为false
bool result2 = (10 != 5); // 结果为true
```
- 布尔类型在内存中通常占用1个字节的空间，但实际上其值只能是 true 或者 false。在进行值的赋值、计算或比较时，可以使用布尔类型来简洁地表达逻辑关系。

### 6.2 字符串

在C++中，字符串有两种主要表示方式：C风格字符串（字符数组）和C++风格字符串（`std::string`）。

#### 1. C++风格字符串（`std::string`）

C++标准库提供了`std::string`类，用于更方便和安全地处理字符串。使用`std::string`时，需要包含`<string>`头文件。

**示例：**
```cpp
#include <iostream>
#include <string>

int main() {
    std::string str = "abc";
    std::cout << str << std::endl;
    return 0;
}
```
**优点：**

- 提供丰富的成员函数，支持字符串的各种操作（例如拼接、查找、替换等）。
- 自动管理内存，避免手动管理字符数组带来的复杂性和潜在错误。
- 支持使用`+`操作符进行字符串拼接。

**适用场景：**

- 需要频繁进行字符串操作（如拼接、查找、替换等）。
- 需要动态长度的字符串。
- 希望代码更简洁、易读且不易出错。

#### 2. C风格字符串（字符数组）

C风格字符串是一个以`'\0'`（空字符）结尾的字符数组。字符数组使用`char`类型，并需要手动管理字符串的长度和内存。

**示例：**
```cpp
#include <iostream>

int main() {
    char str[] = "abc";
    std::cout << str << std::endl;
    return 0;
}
```
**优点：**

- 更接近底层，可以更高效地操作内存。
- 在某些低级编程场景下（如嵌入式编程）更加常用。

**适用场景：**

- 需要与C语言代码兼容。
- 内存和性能要求非常高的低级编程场景。
- 字符串长度固定，且不需要复杂的字符串操作。

#### 比较与选择

| 特性                | `std::string`        | 字符数组（C风格字符串） |
|-------------------|----------------------|-------------------------|
| 内存管理          | 自动管理             | 手动管理                |
| 操作便利性        | 提供丰富的成员函数   | 需要手动实现很多操作    |
| 安全性            | 高                   | 低，容易出现缓冲区溢出  |
| 动态长度          | 支持                 | 不支持                  |
| 拼接操作          | 使用`+`操作符        | 使用`strcat`等函数      |
| 适用场景          | 复杂字符串操作，易用性 | 与C兼容，性能和内存优化 |

#### 选择指南

- 如果你需要处理字符串的长度不固定，或者需要频繁操作字符串（如拼接、查找、替换等），建议使用`std::string`。
- 如果你在进行底层编程，或者需要与C语言代码兼容，且字符串长度是固定的，可以使用字符数组。

通过理解这两种字符串类型的区别和适用场景，你可以更好地选择合适的类型来满足编程需求。
### 6.3 复合数据类型：
- 数组类型：用于存储相同类型的一系列元素
- 结构体类型：用于定义一组不同类型的数据作为一个单独的实体
- 枚举类型：用于定义一组具有离散值的常量

### 6.4 指针类型
- 用于存储内存地址

### 6.5 其他数据类型：
- 空类型：void，用于表示无类型或无返回值的函数

### 6.6 常用数据类型的使用实例

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    // 学生信息
    int studentId = 12345;
    string studentName = "赵镇";
    int age = 20;
    double score = 92.5;
    char gender = '男';
    bool isMarried = false;
    
    // 输出学生信息
    cout << "学生信息：" << endl;
    cout << "学号：" << studentId << endl;
    cout << "姓名：" << studentName << endl;
    cout << "年龄：" << age << endl;
    cout << "成绩：" << score << endl;
    cout << "性别：" << gender << endl;
    cout << "婚否：" << boolalpha << isMarried << endl;

    return 0;
}
```

## 7. C++中的运算符

C++中的运算符种类丰富，包括算术运算符、赋值运算符、比较运算符、逻辑运算符、条件（三目）运算符和位运算符

- 算术运算符：
  算术运算符用于执行基本的数学运算，包括：
    - ```+```（加）
    - ```-```（减）
    - ```*```（乘）
    - ```/```（除）
    - ```%```（求余）
    - ```++```（自增）
    - ```--```（自减）
    - ```++``` 和 ```-- ```可以作为前缀或后缀形式出现，影响变量的值。
    ```cpp
    int a = 10;
    int b = 20;
    int result = a + b; // 30
    a++; // 11
    ```
- 赋值运算符：
  赋值运算符用于将计算结果赋值给变量，包括：
    - ```=```（等于）
    - ```+=```（自加一次等于）
    - ```-=```（自减一次等于）
    - ```*=```（自乘一次等于）
    - ```/=```（自除一次等于）
    - ```%=```（求模并赋值）
    ```cpp
    int x = 10;
    x += 5; // 等同于 x = x + 5;
    ```
- 比较运算符：
  比较运算符用于比较两个值的大小或相等性，包括：
    - ```<```（小于）
    - ```>```（大于）
    - ```>=```（大于等于）
    - ```<=```（小于等于）
    - ```==```（等于）
    - ```!=```（不等于）

    ```cpp
   int m = 10;
    int n = 20;
    bool result = (m > n); // 比较 m 是否大于 n
    ```
  
- 逻辑运算符：
  逻辑运算符用于组合布尔表达式，实现逻辑运算，包括：

  - ```&&```（逻辑与）
  - ```||```（逻辑或）
  - ```!```（逻辑非）
    ```cpp
    bool condition1 = true;
    bool condition2 = false;
    bool result = condition1 && condition2; // 使用逻辑与运算符
    ```
    
- 条件（三目）运算符 `?:` ：
    条件运算符 ?: 是一个三元运算符，用于根据条件表达式的结果选择两个值中的一个。语法形式为 ```result = (condition) ? value1 : value2;``` 其中，```condition``` 是要评估的布尔表达式，```value1``` 是如果 ```condition``` 为 ```true``` 则返回的值，而 ```value2``` 是如果 ```condition``` 为 ```false``` 则返回的值。
    ```cpp
    int age = 20;
    string message = (age >= 18) ? "成年人" : "未成年人";  // 根据年龄判断成年人或未成年人
    ```
  
- 位运算符：
  位运算符用于对二进制位进行操作，包括：

    - ```&```（按位与）
    - ```|```（按位或）
    - ```^```（按位异或）
    - ```~```（按位取反）
    - ```<<```（左移）
    - ```>>```（右移）
    ```cpp
    int a = 5;  // 二进制为 101
    int b = 3;  // 二进制为 011
    int result = a & b; // 按位与操作，结果为 001，即 1
    ```
C++中的运算符不仅包括上述基本类型，还包括其他运算符例如```sizeof```, ```typeid```等。此外，C++还支持字符串连接操作，其中 ```+``` 运算符可以用于连接 ```std::string``` 类型的字符串。

## 8. C++的输入与输出

### 8.1 使用 cin 读取字符串/整数/浮点数
```cin``` 可以读取用户的键盘输入。例如：
例如：
```cpp
#include <iostream>
using namespace std;

int main() {
    string name;
    int age;
    float salary;
    
    cout << "请输入你的姓名：" << endl;
    getline(cin, name); // 读取整行字符串，包括空格
    cout << "请输入你的年龄：" << endl;
    cin >> age; // 读取整数
    cout << "请输入你的工资：" << endl;
    cin >> salary; // 读取浮点数
    
    cout << "你的信息如下：" << endl;
    cout << "姓名: " << name << "\n" << "年龄：" << age << "\n" << "工资：" << salary << endl;
    
    return 0;
}
```
### 8.2 cout
`cout` 可以打印一行内容，若加上`endl`打印完会自动换行，不加则不会换行
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "hello, C++!" << endl;
    int a = 9;
    cout << "output: " << a << endl;
    return 0;
}
```
### 8.3 printf
`printf` 用于格式化输出，可以输出各种类型的数据，但不会自动换行。
```cpp
#include <iostream>
using namespace std;

int main() {
    string a = "wniuniu";
    string b = "brilliantgby";
    printf("%s", a.c_str());
    printf("%s", b.c_str());
    printf("\n");
    printf("OvO\n");
    return 0;
}
```

### 8.4 输入输出流（`ifstream`/`ofstream`）
在 C++ 中，`ifstream` 和 `ofstream` 是两个基本的 I/O 类，用于处理文件流的输入和输出。它们分别是输入和输出操作的类，并且有多个子类，支持从各种数据源读取数据和将数据写入各种数据目标。

`ifstream` 和 `ofstream` 的关系
在 C++ 中，`ifstream` 和 `ofstream` 分别继承自抽象类 `istream` 和 `ostream`并提供了处理文件流的具体实现。虽然 `ifstream` 和 `ofstream` 没有直接的继承关系，但它们是互补的，分别处理文件的输入和输出操作。

- `ifstream`：继承自 `istream`，用于从文件中读取数据。表示文件输入流。
- `ofstream`：继承自 `ostream`，用于向文件中写入数据。表示文件输出流。
- `fstream`：继承自 `iostream`，结合了 `ifstream` 和 `ofstream` 的功能，既可以进行文件的输入操作也可以进行文件的输出操作。

例如：

##### 使用 `ifstream` 读取文件
`ifstream` 用于打开一个文件进行读取操作，并继承了 `istream` 的所有功能，可以使用各种输入操作符和方法读取文件内容。
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ifstream inputFile("example.txt"); // 打开文件进行读取
    if (!inputFile) {
        cerr << "无法打开文件" << endl;
        return 1;
    }
    
    string line;
    while (getline(inputFile, line)) { // 逐行读取文件内容
        cout << line << endl;
    }
    
    inputFile.close(); // 关闭文件
    return 0;
}

```

##### 使用 `ofstream` 写入文件
`ofstream` 用于打开一个文件进行写入操作，并继承了 `ostream` 的所有功能，可以使用各种输出操作符和方法写入文件内容。
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream outputFile("example.txt"); // 打开文件进行写入
    if (!outputFile) {
        cerr << "无法打开文件" << endl;
        return 1;
    }
    
    string data = "Hello, World!";
    outputFile << data << endl; // 写入数据到文件
    
    outputFile.close(); // 关闭文件
    return 0;
}
```

##### 使用 `fstream` 进行同时读写操作
`fstream` 结合了 `ifstream`和 `ofstream` 的功能，可以同时进行文件的读写操作。
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    fstream file("example.txt", ios::in | ios::out | ios::trunc); // 打开文件进行读写
    if (!file) {
        cerr << "无法打开文件" << endl;
        return 1;
    }
    
    file << "Hello, World!" << endl; // 写入数据到文件
    file.seekg(0); // 移动到文件开头
    string line;
    while (getline(file, line)) { // 读取文件内容
        cout << line << endl;
    }
    
    file.close(); // 关闭文件
    return 0;
}

```
## 9. 课程总结

- C++环境安装正常。
- 完成第一个Hello World程序。
- 认识变量类型和命名方式。
- C++中的运算符。
- C++的输入与输出。



# 课后练习

1.编写一个C++程序来找出满足以下条件的最小正整数：

- 该数除以12余1
- 该数除以23也余1
- 该数除以31也余1

请在以下选项中选择一个正确的答案，该答案满足上述所有条件：

(A) 4191

(B) 3232

(C) 8577

(D) 9233



参考程序：

```cpp
#include <iostream>
using namespace std;

int main() {
    // 获取用户输入的选项
    cout << "请输入一个选项：";
    int option;
    cin >> option;

    // 计算余数
    int a = option % 12;
    int b = option % 23;
    int c = option % 31;

    // 打印余数结果
    cout << "For option " << option << ":" << endl;
    cout << "a = " << a << ", b = " << b << ", c = " << c << endl;

    // 判断是否满足条件
    if (a == 1 && b == 1 && c == 1) {
        cout << "Correct, That's what I find!! The number is: " << option << endl;
    } else {
        cout << "Wrong, Please try another Answer!" << endl;
    }

    return 0;
}

```



2.编写一个C++程序，用于模拟餐厅的点单过程。程序应提前告知用户汉堡、薯条和可乐的价格，并通过用户输入获得点单信息。最后，程序应分行输出客户点的内容，并打印出总价。

**价格信息：**

- 汉堡：$5
- 薯条：$2
- 可乐：$1

**功能要求：**

1. 显示各项食物的价格。
2. 提示用户输入每种食物的数量。
3. 计算并显示每种食物的点单数量。
4. 计算并显示总价。

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
汉堡 X 2
薯条 X 1
可乐 X 3

总价：$15
```

**提示：**

- 使用 `cin >>` 函数获取用户输入。
- 使用算术运算计算总价。
- 使用 `cout <<` 函数输出结果。



示例代码：

```cpp
#include <iostream>
using namespace std;

int main() {
    // 定义食物的价格
    int burger_price = 5;
    int fries_price = 2;
    int cola_price = 1;

    // 显示价格信息
    cout << "汉堡：$" << burger_price << endl;
    cout << "薯条：$" << fries_price << endl;
    cout << "可乐：$" << cola_price << endl << endl;

    // 获取用户输入的点单数量
    int burger_count, fries_count, cola_count;
    cout << "请输入汉堡的数量：";
    cin >> burger_count;
    cout << "请输入薯条的数量：";
    cin >> fries_count;
    cout << "请输入可乐的数量：";
    cin >> cola_count;

    // 计算总价
    int total_price = burger_count * burger_price +
                      fries_count * fries_price +
                      cola_count * cola_price;

    // 输出点单内容和总价
    cout << "\n您的点单如下：" << endl;
    cout << "汉堡 X " << burger_count << endl;
    cout << "薯条 X " << fries_count << endl;
    cout << "可乐 X " << cola_count << endl;
    cout << "\n总价：$" << total_price << endl;

    return 0;
}

```


