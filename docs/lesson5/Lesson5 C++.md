# Lesson5 数组/列表与初级搜索
## 目录
- [1. 数组（Array）](#1-数组array)
  - [1.1 声明与初始化数组](#11-声明与初始化数组)
  - [1.2 访问数组元素](#12-访问数组元素)
  - [1.3 数组的长度](#13-数组的长度)
  - [1.4 多维数组](#14-多维数组)
  - [1.5 数组的特点和注意事项](#15-数组的特点和注意事项)
- [2. 动态数组和列表（std::vector）](#2-动态数组和列表stdvector)
  - [2.1 创建和初始化动态数组](#21-创建和初始化动态数组)
  - [2.2 基本操作](#22-基本操作)
  - [2.3 特性和注意事项](#23-特性和注意事项)
- [3. 初级搜索](#3-初级搜索)
  - [3.1 数组的线性搜索（Linear Search）](#31-数组的线性搜索linear-search)
  - [3.2 `std::vector`的线性搜索](#32-stdvector的线性搜索)
- [4. 课后练习](#4-课后练习)
  - [4.1 学生成绩管理系统](#41-学生成绩管理系统)

## 1. 数组（Array）
在C++中，数组是一种用来存储固定大小的同类型元素的数据结构。它是一个连续的内存区域，可以存储多个相同数据类型的元素，并通过索引来访问这些元素。以下是关于C++数组的详细介绍：

### 1.1 声明与初始化数组

在C++中，数组的声明和初始化可以分为以下几种方式：

- **声明数组变量：** 声明数组需要指定数组的类型和大小，但不初始化数组元素。
```cpp
int myArray[5];
```
- **声明并初始化数组：**  在声明数组的同时进行初始化，未显式初始化的元素将被设置为默认值（通常为0）。
```cpp
int myArray[5] = {1, 2, 3}; // 前三个元素初始化为1, 2, 3，后两个元素为0
```

- **使用数组初始化列表：** 可以在声明时直接指定所有初始元素的值。
```cpp
int myArray[] = {1, 2, 3, 4, 5}; // 编译器自动确定数组大小为5
```

- **动态分配数组：** 使用`new`关键字在运行时动态分配数组并指定数组的大小。
```cpp
int* myArray = new int[5]; // 动态分配一个包含5个整数元素的数组
```

### 1.2 访问数组元素

C++数组的元素通过索引访问，索引从0开始到数组长度减1。

```cpp
int myArray[] = {10, 20, 30, 40, 50};
int firstElement = myArray[0]; // 访问第一个元素，值为10
int thirdElement = myArray[2]; // 访问第三个元素，值为30
```

### 1.3 数组的长度

在 C++ 中，数组的长度指数组中元素的数量。计算数组长度时，需要区分静态分配数组和动态分配数组，因为它们的处理方式是不同的。

#### 静态分配数组

静态分配数组的大小在编译时已经确定，不能在运行时修改。在 C++ 中，可以使用 `sizeof` 运算符计算静态数组的大小。

**示例代码：**

```cpp
int myArray[] = {10, 20, 30, 40, 50};
int length = sizeof(myArray) / sizeof(myArray[0]); // 获取数组的长度，值为 5
```

**解释：**

- `sizeof(myArray)`: `sizeof` 运算符返回数组 `myArray` 占用的总字节数。例如，如果 `myArray` 是一个包含 5 个 `int` 类型元素的数组，而每个 `int` 占用 4 个字节，那么 `sizeof(myArray)` 的值为 20（5 * 4）。

- `sizeof(myArray[0])`: 返回数组中单个元素的字节大小。对于 `int` 类型的数组元素，通常是 4 个字节。

- `sizeof(myArray) / sizeof(myArray[0])`: 通过将数组的总字节数除以单个元素的字节大小，可以得到数组的元素个数（即数组的长度）。例如，假设 `myArray` 是一个包含 5 个 `int` 类型元素的数组，`sizeof(myArray)` 的值为 20，`sizeof(myArray[0])` 的值为 4，那么 `sizeof(myArray) / sizeof(myArray[0])` 的值为 5。

#### 动态分配数组

动态分配数组的大小在运行时确定，并且可以在运行时通过 `new` 运算符分配内存。对于动态分配的数组，`sizeof` 运算符无法用于计算数组的长度，因此需要在分配内存时手动保存数组的长度。

**示例代码：**

```cpp
int* myArray = new int[5];
int length = 5; // 手动记录数组长度
```

**解释：**

- **动态分配数组的特点**：动态分配的数组无法通过 `sizeof` 运算符获取长度，因为 `sizeof(myArray)` 只返回指针的大小，而不是数组的实际大小。因此，我们通常需要在分配内存时手动保存数组的长度。

#### 静态分配 vs 动态分配

- **静态分配数组**: 数组的大小在编译时已经确定，数组长度是固定的，不能在程序运行期间改变数组的大小。使用 `sizeof` 可以计算数组的长度。

- **动态分配数组**: 数组的大小在运行时动态确定，可以在程序运行期间改变数组的大小。`sizeof` 不能用于计算数组的长度，通常需要手动记录长度。


### 1.4 多维数组

C++支持多维数组，即数组的元素可以是数组。例如，二维数组的声明和初始化如下所示：

```cpp
int twoDArray[3][4]; // 声明一个3行4列的二维整数数组

int twoDArray[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
}; // 声明并初始化一个3行3列的二维整数数组

```

### 1.5 数组的特点和注意事项

- **数组是固定大小的：** 在C++中，数组的大小在声明时就确定了，且不可变。如果需要改变数组的大小，通常需要创建一个新的数组并复制元素。

- **数组可以在栈或堆中分配：** 静态数组在栈中分配，动态数组使用new关键字在堆中分配，需手动释放内存。

- **默认初始化：** 静态数组的元素在声明时未显式初始化时，其值是未定义的。动态数组的元素也未定义，除非显式初始化。

- **数组越界：** 访问数组元素时，如果使用了不存在的索引，会导致未定义行为（通常是程序崩溃），而不会抛出异常。


### 示例

以下是一个简单的示例，展示了如何声明、初始化和使用一个一维整数数组：

```cpp
#include <iostream>
using namespace std;

int main() {
    // 声明并初始化一个整数数组
    int myArray[] = {10, 20, 30, 40, 50};

    // 计算数组元素的总和
    int sum = 0;
    for (int i = 0; i < sizeof(myArray) / sizeof(myArray[0]); i++) {
        sum += myArray[i];
    }

    // 打印数组元素的总和
    cout << "数组元素的总和为：" << sum << endl;

    return 0;
}

```

在这个示例中，`myArray`数组包含5个整数元素，通过循环计算了这些元素的总和，并输出到控制台。


## 2. 动态数组和列表（std::vector）

### 2.1 创建和初始化动态数组

在C++中，可以使用std::vector类来创建和初始化动态数组：
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // 创建一个vector实例
    vector<int> myVector = {10, 20, 30, 40, 50};

    // 打印vector元素
    for (int i = 0; i < myVector.size(); i++) {
        cout << "Element at index " << i << ": " << myVector[i] << endl;
    }

    // 添加新元素
    myVector.push_back(60);

    // 打印添加后的元素
    cout << "After adding an element, vector elements: ";
    for (int i = 0; i < myVector.size(); i++) {
        cout << myVector[i] << " ";
    }
    cout << endl;

    return 0;
}
```

### 2.2 基本操作

#### 添加和访问元素

可以使用`push_back()`方法添加元素到`vector`中，并使用索引访问元素

```cpp
vector<int> myVector;
myVector.push_back(10);
myVector.push_back(20);
myVector.push_back(30);

int firstElement = myVector[0]; // 获取第一个元素，值为10
```

#### 删除元素

使用`erase()`方法删除指定位置的元素，或使用`pop_back()`删除最后一个元素。

```cpp
myVector.erase(myVector.begin() + 1); // 删除索引为1的元素，即20。如果想删除索引为2的元素则+2， 以此类推
myVector.pop_back(); // 删除最后一个元素
```

#### 获取`vector`大小

使用`size()`方法获取`vector`中元素的个数。

```cpp
int size = myVector.size(); // 获取vector大小。
```

#### 迭代`vector`元素

可以使用范围for循环或迭代器遍历`vector`中的元素。

```cpp
//使用for循环
for (int element : myVector) {
    cout << element << " ";
}
cout << endl;

// 或者使用迭代器
for (auto it = myVector.begin(); it != myVector.end(); ++it) {
    cout << *it << " ";
}
cout << endl;
```

### 2.3 特性和注意事项

- **动态调整大小：** `std::vector` 可以根据需要自动调整其大小，不需要手动管理内存。
- **性能：** `std::vector` 在随机访问和尾部插入/删除操作上具有高效的性能，但在中间插入/删除操作上相对较慢。
- **线程安全性：** `std::vector` 不是线程安全的，如果需要在多线程环境中使用`vector`，需要手动实现同步。


### 示例

以下是一个使用`std::vector`的简单示例：

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // 创建一个vector实例
    vector<int> myVector = {10, 20, 30, 40, 50};

    // 打印vector元素
    cout << "Vector elements: ";
    for (int element : myVector) {
        cout << element << " ";
    }
    cout << endl;

    // 添加新元素
    myVector.push_back(60);

    // 打印添加后的元素
    cout << "After adding an element, vector elements: ";
    for (int element : myVector) {
        cout << element << " ";
    }
    cout << endl;

    return 0;
}
```
在这个示例中，展示了如何使用`std::vector创建`、添加和访问元素，以及打印`vector`的内容。

## 3. 初级搜索

### 3.1 数组的线性搜索（Linear Search）

线性搜索是最简单的数组搜索方法，它从数组的第一个元素开始逐个检查，直到找到目标元素或遍历完整个数组。

```cpp
#include <iostream>
using namespace std;

int linearSearch(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i; // 返回目标元素的索引
        }
    }
    return -1; // 没有找到目标元素
}

int main() {
    int numbers[] = {5, 8, 2, 10, 3};
    int target = 10;
    int size = sizeof(numbers) / sizeof(numbers[0]);

    int index = linearSearch(numbers, size, target);

    if (index != -1) {
        cout << "元素 " << target << " 在数组中的索引为：" << index << endl;
    } else {
        cout << "元素 " << target << " 不在数组中。" << endl;
    }

    return 0;
}
```

在上面的示例中，`linearSearch`函数接受一个整型数组、数组大小和目标整数作为参数，然后使用for循环逐个检查数组中的元素，直到找到目标元素或者遍历完整个数组。
### 3.2 `std::vector`的线性搜索

`std::vector`的线性搜索与数组类似，可以使用范围for循环或迭代器遍历`vector`中的元素，查找目标元素。
```cpp
#include <iostream>
#include <vector>
using namespace std;

int linearSearch(vector<string> vec, string target) {
    for (int i = 0; i < vec.size(); i++) {
        if (vec[i] == target) {
            return i; // 返回目标元素的索引
        }
    }
    return -1; // 没有找到目标元素
}

int main() {
    vector<string> fruits = {"Apple", "Banana", "Cherry"};
    string target = "Banana";

    int index = linearSearch(fruits, target);

    if (index != -1) {
        cout << "元素 " << target << " 在vector中的索引为：" << index << endl;
    } else {
        cout << "元素 " << target << " 不在vector中。" << endl;
    }

    return 0;
}
```

在上面的示例中，`linearSearch`函数接受一个`vector`和目标元素作为参数，然后使用for循环遍历`vector`中的元素，查找目标元素是否存在。
### 总结
- **数组（Array）：** 使用固定大小的连续存储空间来存储元素，通过索引访问元素。初级搜索通常采用线性搜索方法。

- **std::vector：** 是一种动态数组，实现了更灵活的操作和搜索方法。初级搜索也可以采用线性搜索方法。
- **性能比较：** std::vector 在随机访问和尾部插入/删除操作上具有高效的性能，但在中间插入/删除操作上相对较慢。

- **注意事项：** std::vector 不是线程安全的，需要在多线程环境中手动实现同步。


这些示例和说明提供了在C++中使用数组和std::vector进行基本操作和线性搜索的基础知识。

## 4. 课后练习

### 4.1 学生成绩管理系统
#### 描述：
设计并实现一个简单的学生成绩管理系统。系统要求能够存储多个学生的姓名和对应的成绩，并提供以下功能：

1. 添加学生及其成绩。

2. 计算并输出所有学生的平均成绩。

3. 查找并输出某个学生的成绩。

4. 输出成绩最高的学生及其成绩。

#### 模板

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// 添加学生信息到students和grades列表中
void addStudent(vector<string>& students, vector<int>& grades, const string& name, int grade) {
    // 填写代码
}

// 计算所有学生的平均成绩
double calculateAverage(const vector<int>& grades) {
    // 填写代码
}

// 查找指定学生的成绩
int findGrade(const vector<string>& students, const vector<int>& grades, const string& name) {
    // 填写代码
}

// 找出成绩最高的学生及其成绩
void findTopStudent(const vector<string>& students, const vector<int>& grades, string& topStudent, int& topGrade) {
    // 填写代码
}

int main() {
    vector<string> students;
    vector<int> grades;
    
    // 添加学生信息
    addStudent(students, grades, "Alice", 85);
    addStudent(students, grades, "Bob", 90);
    addStudent(students, grades, "Charlie", 78);
    addStudent(students, grades, "David", 92);

    // 输出所有学生的平均成绩
    double average = calculateAverage(grades);
    cout << "所有学生的平均成绩为：" << average << endl;

    // 查找某个学生的成绩
    string targetName = "Bob";
    int grade = findGrade(students, grades, targetName);
    if (grade != -1) {
        cout << targetName << " 的成绩为：" << grade << endl;
    } else {
        cout << targetName << " 不存在。" << endl;
    }

    // 找出成绩最高的学生
    string topStudent;
    int topGrade;
    findTopStudent(students, grades, topStudent, topGrade);
    cout << "成绩最高的学生是 " << topStudent << "，成绩为：" << topGrade << endl;

    return 0;
}
```

#### 参考答案

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// 添加学生信息到students和grades列表中
void addStudent(vector<string>& students, vector<int>& grades, const string& name, int grade) {
    students.push_back(name);
    grades.push_back(grade);
}

// 计算所有学生的平均成绩
double calculateAverage(const vector<int>& grades) {
    int total = 0;
    for (int i = 0; i < grades.size(); i++) {
        total += grades[i];
    }
    return static_cast<double>(total) / grades.size();
}

// 查找指定学生的成绩
int findGrade(const vector<string>& students, const vector<int>& grades, const string& name) {
    for (int i = 0; i < students.size(); i++) {
        if (students[i] == name) {
            return grades[i];
        }
    }
    return -1; // 如果没有找到，返回-1
}

// 找出成绩最高的学生及其成绩
void findTopStudent(const vector<string>& students, const vector<int>& grades, string& topStudent, int& topGrade) {
    topGrade = grades[0];
    topStudent = students[0];
    for (int i = 1; i < grades.size(); i++) {
        if (grades[i] > topGrade) {
            topGrade = grades[i];
            topStudent = students[i];
        }
    }
}

int main() {
    vector<string> students;
    vector<int> grades;
    
    // 添加学生信息
    addStudent(students, grades, "Alice", 85);
    addStudent(students, grades, "Bob", 90);
    addStudent(students, grades, "Charlie", 78);
    addStudent(students, grades, "David", 92);

    // 输出所有学生的平均成绩
    double average = calculateAverage(grades);
    cout << "所有学生的平均成绩为：" << average << endl;

    // 查找某个学生的成绩
    string targetName = "Bob";
    int grade = findGrade(students, grades, targetName);
    if (grade != -1) {
        cout << targetName << " 的成绩为：" << grade << endl;
    } else {
        cout << targetName << " 不存在。" << endl;
    }

    // 找出成绩最高的学生
    string topStudent;
    int topGrade;
    findTopStudent(students, grades, topStudent, topGrade);
    cout << "成绩最高的学生是 " << topStudent << "，成绩为：" << topGrade << endl;

    return 0;
}
```

### 说明

- **addStudent**: 通过 `push_back` 方法将学生姓名和成绩添加到 `students` 和 `grades` 两个 `vector` 中。
- **calculateAverage**: 通过遍历 `grades`，计算所有学生的成绩总和并返回平均值。
- **findGrade**: 通过遍历 `students`，查找指定学生的姓名并返回对应的成绩。如果找不到，返回 `-1`。
- **findTopStudent**: 通过遍历 `grades`，找出最高成绩的学生姓名和成绩。
