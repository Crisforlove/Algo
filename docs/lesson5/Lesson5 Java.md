# Lesson5 数组/列表与初级搜索

## 目录
1. [数组（Array）](#1-数组array)
    - [1.1 声明和初始化数组](#11-声明和初始化数组)
    - [1.2 访问数组元素](#12-访问数组元素)
    - [1.3 数组的长度](#13-数组的长度)
    - [1.4 多维数组](#14-多维数组)
    - [1.5 数组的特点和注意事项](#15-数组的特点和注意事项)
    - [示例](#示例)
2. [列表（ArrayList）](#2-列表arraylist)
    - [2.1 创建和初始化列表](#21-创建和初始化列表)
    - [2.2 基本操作](#22-基本操作)
    - [2.3 特性和注意事项](#23-特性和注意事项)
    - [示例](#示例-1)
3. [初级搜索](#3-初级搜索)
    - [3.1 数组的线性搜索（Linear Search）](#31-数组的线性搜索linear-search)
    - [3.2 列表（List）的初级搜索](#32-列表list的初级搜索)
4. [课后练习](#4-课后练习)
    - [ArrayList](#arraylist)
    - [线性搜索](#线性搜索)


## 1. 数组（Array）
在Java中，数组是一种用来存储固定大小的同类型元素的数据结构。它是一个连续的内存区域，可以存储多个相同数据类型的元素，并通过索引来访问这些元素。以下是关于Java数组的详细介绍：

### 1.1 声明和初始化数组

在Java中，数组的声明和初始化可以分为以下几种方式：

- **声明数组变量：** 声明数组需要指定数组的类型和变量名，但不分配内存空间。
```java
int[] myArray;
```
- **创建数组并分配内存空间：** 使用`new`关键字创建数组并指定数组的大小（即元素个数）。
```java
myArray = new int[5]; // 创建了一个包含5个整数元素的数组
```

- **同时声明和初始化：** 也可以在声明数组变量时直接初始化数组。
```java
int[] myArray = new int[5]; // 声明并初始化一个包含5个整数元素的数组
```

- **使用数组初始化列表（Array Initializer）：** 在声明数组时直接指定初始元素的值，Java会根据提供的元素个数自动确定数组大小。
```java
int[] myArray = {1, 2, 3, 4, 5}; // 声明并初始化包含5个整数元素的数组
```

### 1.2 访问数组元素

Java数组的元素通过索引访问，索引从0开始到数组长度减1。

```java
int[] myArray = {10, 20, 30, 40, 50};
int firstElement = myArray[0]; // 访问第一个元素，值为10
int thirdElement = myArray[2]; // 访问第三个元素，值为30
```

### 1.3 数组的长度

可以使用数组的`length`属性获取数组的长度，即数组中元素的个数。

```java
int[] myArray = {10, 20, 30, 40, 50};
int length = myArray.length; // 获取数组的长度，值为5
```

### 1.4 多维数组

Java支持多维数组，即数组的元素可以是数组。例如，二维数组的声明和初始化如下所示：

```java
int[][] twoDArray = new int[3][4]; // 声明一个3行4列的二维整数数组

int[][] twoDArray = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
}; // 声明并初始化一个3行3列的二维整数数组
```

### 1.5 数组的特点和注意事项

- **数组是引用类型：** 在Java中，数组是对象，它们存储在堆内存中。因此，数组变量实际上是引用，存储的是数组对象的地址。

- **长度不可变：** 一旦创建了数组，其长度就不可变。如果需要改变数组的大小，通常需要创建一个新的数组。

- **默认初始化：** 数组元素在创建时会根据其类型进行默认初始化。例如，整数数组中的元素默认值为0，对象数组中的元素默认值为null。

- **数组越界异常（ArrayIndexOutOfBoundsException）：** 访问数组元素时，如果使用了不存在的索引，会抛出数组越界异常。

### 示例

以下是一个简单的示例，展示了如何声明、初始化和使用一个一维整数数组：

```java
public class ArrayExample {
    public static void main(String[] args) {
        // 声明并初始化一个整数数组
        int[] myArray = {10, 20, 30, 40, 50};

        // 计算数组元素的总和
        int sum = 0;
        for (int i = 0; i < myArray.length; i++) {
            sum += myArray[i];
        }

        // 打印数组元素的总和
        System.out.println("数组元素的总和为：" + sum);
    }
}
```
在这个示例中，`myArray`数组包含5个整数元素，通过循环计算了这些元素的总和，并输出到控制台。

## 2. 列表（ArrayList）

### 2.1 创建和初始化列表

在Java中，可以使用`ArrayList`类来创建和初始化列表：

#### 使用 ArrayList 创建列表

```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        // 创建一个ArrayList实例
        ArrayList<String> arrayList = new ArrayList<>();

        // 添加元素到列表
        arrayList.add("Apple");
        arrayList.add("Banana");
        arrayList.add("Cherry");

        // 打印列表元素
        System.out.println("ArrayList elements: " + arrayList);
    }
}
```

### 2.2 基本操作

#### 添加和访问元素

可以使用`add()`方法添加元素到列表中，并使用索引访问元素。

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // 创建一个 ArrayList 并添加元素
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");

        // 获取第一个元素
        String firstFruit = fruits.get(0); // 获取第一个元素，值为"Apple"

        // 输出第一个元素
        System.out.println("The first fruit is: " + firstFruit);
    }
}
```

#### 删除元素

使用`remove()`方法删除指定位置或指定元素。

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // 创建一个 ArrayList 并添加元素
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");
      
        // 删除索引为1的元素，即"Banana"
        fruits.remove(1);

        // 打印删除后的列表
        System.out.println("Fruits list after removal: " + fruits);
    }
}

```

#### 获取列表大小

使用`size()`方法获取列表中元素的个数。

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // 创建一个 ArrayList 并添加元素
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");

        // 获取列表大小
        int size = fruits.size(); // 获取当前列表的大小，值为3
      
        // 删除索引为1的元素，即"Banana"
        fruits.remove(1);

        // 获取列表大小
        int size = fruits.size(); // 获取当前列表的大小，值为2
        System.out.println("The size of the fruits list is: " + size);

        // 打印删除后的列表
        System.out.println("Fruits list after removal: " + fruits);
    }
}

```

#### 迭代列表元素
可以使用增强`for`循环或迭代器遍历`ArrayList`中的元素。

##### 增强`for`循环
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // 创建一个 ArrayList 并添加元素
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");
      
        // 使用增强的 for 循环遍历并打印列表中的每个元素
        System.out.println("Fruits in the list:");
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}
```

##### 迭代器
迭代器（Iterator）是 Java 集合框架中一个重要的设计模式，允许程序员在不暴露集合内部结构的情况下，逐个访问集合中的元素。它提供了一种统一的方式来遍历集合，包括 `List`、`Set` 和 `Map` 等。

主要的方法包括：

   - `boolean hasNext()`: 如果迭代器有更多元素可供遍历，则返回 `true`。
   - `E next()`: 返回迭代器的下一个元素。


##### 使用迭代器的示例

下面是一个使用迭代器遍历 `ArrayList` 的示例：

```java
import java.util.ArrayList;
import java.util.Iterator;

public class IteratorExample {
    public static void main(String[] args) {
        // 创建一个 ArrayList 并添加元素
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");

        // 创建迭代器
        Iterator<String> iterator = fruits.iterator();

        // 使用迭代器遍历集合
        while (iterator.hasNext()) {
            String fruit = iterator.next();
            System.out.println(fruit);
        }
    }
}
```

### 代码解析

1. **`while (iterator.hasNext())`**:
   - 这是一个循环条件，使用 `iterator.hasNext()` 方法检查迭代器是否还有更多的元素可以遍历。
   - `hasNext()` 返回 `true` 时，表示还有下一个元素可以访问；如果没有更多元素，返回 `false`，循环结束。

2. **`String fruit = iterator.next();`**:
   - 当 `hasNext()` 返回 `true` 时，`iterator.next()` 被调用以获取下一个元素。
   - `next()` 方法返回当前元素，并将迭代器的游标移动到下一个元素。
   - 这里，将获取到的字符串类型元素赋值给变量 `fruit`。



### 2.3 特性和注意事项

- **有序性：** 列表中的元素是有序的，可以按照它们被插入的顺序访问。

- **可重复性：** 列表中允许存储重复的元素。

- **索引访问：** 可以通过索引访问列表中的元素，索引从0开始到列表大小减1。


### 示例

以下是一个使用`ArrayList`的简单示例：

```java
import java.util.ArrayList;

public class ListExample {
    public static void main(String[] args) {
        // 使用 ArrayList 创建列表
        ArrayList<String> arrayList = new ArrayList<>();
        arrayList.add("Apple");
        arrayList.add("Banana");
        arrayList.add("Cherry");
        System.out.println("ArrayList elements: " + arrayList);
    }
}
```
在这个示例中，展示了如何使用`ArrayList`创建、添加和访问列表元素。


## 3. 初级搜索

### 3.1 数组的线性搜索（Linear Search）

线性搜索是最简单的数组搜索方法，它从数组的第一个元素开始逐个检查，直到找到目标元素或遍历完整个数组。

```java
public class ArraySearchExample {
    public static void main(String[] args) {
        int[] numbers = {5, 8, 2, 10, 3};
        int target = 10;

        int index = linearSearch(numbers, target);

        if (index != -1) {
            System.out.println("元素 " + target + " 在数组中的索引为：" + index);
        } else {
            System.out.println("元素 " + target + " 不在数组中。");
        }
    }

    // 线性搜索方法
    public static int linearSearch(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i; // 返回目标元素的索引
            }
        }
        return -1; // 没有找到目标元素
    }
}
```

在上面的示例中，`linearSearch`方法接受一个整型数组和目标整数作为参数，然后使用for循环逐个检查数组中的元素，直到找到目标元素或者遍历完整个数组。

### 3.2 列表（List）的初级搜索

列表的线性搜索与数组类似，可以使用迭代器或增强for循环来遍历列表中的元素，查找目标元素。

```java
import java.util.ArrayList;

public class ArrayListSearchExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");
        String target = "Banana";

        int index = linearSearch(fruits, target);

        if (index != -1) {
            System.out.println("元素 " + target + " 在列表中的索引为：" + index);
        } else {
            System.out.println("元素 " + target + " 不在列表中。");
        }
    }

    // 线性搜索方法
    public static int linearSearch(List<String> list, String target) {
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).equals(target)) {
                return i; // 返回目标元素的索引
            }
        }
        return -1; // 没有找到目标元素
    }
}
```

在上面的示例中，`linearSearch`方法接受一个`List`和目标元素作为参数，然后使用for循环遍历列表中的元素，使用`equals`方法比较每个元素和目标元素是否相等。

## 4. 课后练习


### `ArrayList`

1. **题目：** 创建一个包含1-5整数的`ArrayList`，并打印这些整数。
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
     // To be implemented
    }
}
```

   **解答：**
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);
        System.out.println(list);
    }
}
```

2. **题目：** 从一个`ArrayList`中移除特定的元素，比如数字3。
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);

         // To be implemented

        System.out.println(list);
    }
}
```
   **解答：**
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        list.add(5);
        list.remove(Integer.valueOf(3));  // 使用包装类来移除特定元素
        System.out.println(list);
    }
}
```

3. **题目：** 访问`ArrayList`中的第三个元素并打印出来。
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        // To be implemented
    }
}
```
   **解答：**
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        System.out.println(list.get(2));  // 索引从0开始，所以第三个元素是索引2
    }
}
```


### `线性搜索`

**题目：** 编写一个Java程序，该程序创建一个`ArrayList`，其中包含`10, 20, 30, 40, 50`。编写一个方法，该方法使用线性搜索来查找一个指定的整数，并返回它在`ArrayList`中的索引。如果该整数不在列表中，则返回-1。最后，调用该方法并打印出结果。

```java
import java.util.ArrayList;

public class LinearSearchExample {
    public static void main(String[] args) {
        // 创建一个包含一些整数的 ArrayList
        // To be implemented
   
       
        // 要查找的目标元素
        int target = 30;
   
       
        // 线性搜索方法
        // To be implemented
   
        // 打印结果
        if (index != -1) {
            System.out.println("元素 " + target + " 在列表中的索引是: " + index);
        } else {
            System.out.println("元素 " + target + " 不在列表中。");
        }
    }
}

```

**解答：**

```java
import java.util.ArrayList;

public class LinearSearchExample {
    public static void main(String[] args) {
        // 创建一个包含一些整数的 ArrayList
        ArrayList<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        list.add(40);
        list.add(50);

        // 要查找的目标元素
        int target = 30;

         // 线性搜索方法
        int index = -1;
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i) == target) {
                index = i;  // 找到目标元素，记录索引
                break;  // 一旦找到就可以退出循环
            }
       } 

        // 打印结果
        if (index != -1) {
            System.out.println("元素 " + target + " 在列表中的索引是: " + index);
        } else {
            System.out.println("元素 " + target + " 不在列表中。");
        }
    }
}

```
