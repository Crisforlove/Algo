# Lesson3 Java的自定义函数与参数

## 目录
1. [Java方法的定义和使用](#1-java方法的定义和使用)
   - [1.1 方法的定义语法](#11-方法的定义语法)
   - [1.2 修饰符（Modifiers）](#12-修饰符modifiers)
   - [1.3 返回类型](#13-返回类型)
   - [1.4 方法名命名规则](#14-方法名命名规则)
2. [Java传参的三种方式](#2-java传参的三种方式)
   - [2.1 按值传递](#21-按值传递)
   - [2.2 按引用传递](#22-按引用传递)
   - [总结](#总结)
3. [形式参数与实际参数](#3-形式参数与实际参数)
   - [3.1 形式参数（Formal Parameters）](#31-形式参数formal-parameters)
   - [3.2 实际参数（Actual Arguments）](#32-实际参数actual-arguments)
   - [3.3 总结](#33-总结)
4. [课后练习](#4-课后练习)
   - [4.1 方法的定义](#41-方法的定义)
   - [4.2 形式参数与实际参数](#42-形式参数与实际参数)



## 1. Java方法的定义和使用

在Java中，方法（Methods）是用来执行特定任务的代码块，可以被重复调用。

### 1.1 方法的定义语法

 ```java
 修饰符 返回类型 方法名(参数列表) {
     // 方法体
     // 可以包含一系列的语句来实现特定功能
     // 可以使用参数，并且可能会返回一个值
 }
 ```

- **修饰符（Modifiers）**：可以是 `public`、`private`、`protected` 。
- **返回类型（Return Type）**：方法可以返回一个值的类型，如果方法不返回任何值，则使用 `void`。
- **方法名（Method Name）**：方法的名称，用来在程序中调用该方法。
- **参数列表（Parameter List）**：可选的参数，用于接收方法执行所需的输入数据。
- **方法体（Method Body）**：包含了实现方法功能的一系列语句。

### 1.2 修饰符（Modifiers）

修饰符定义了方法的访问级别和行为特性：

- **public**：可以被任何类访问。
- **private**：只能在同一个类中访问。
- **protected**：可以被同一个包内的类和子类访问。

对于现阶段，只需掌握public类型方法即可。
#### public

- **描述**：`public` 修饰符表示方法可以被任何类访问。
- **示例**：

 ```java
public class Main {
    public static void greet(String name) {
        System.out.println("Hello, " + name + "!");
    }

    public static void main(String[] args) {
        greet("Alice"); // 输出：Hello, Alice!
    }
}
 ```

### 1.3 返回类型

返回类型指定了方法返回的数据类型。如果方法不返回任何值，则使用 `void`。

**示例1：返回类型为 `int`**

 ```java
 public class MathUtils {
     public int add(int a, int b) {
         return a + b;
     }
 }
 ```

**示例2：返回类型为 `void`**

 ```java
 public class Printer {
     public void printMessage(String message) {
         System.out.println(message);
     }
 }
 ```

### 1.4 方法名命名规则

方法名必须是一个合法的标识符（identifier），遵循以下规则：

- 方法名可以包含字母、数字、下划线和美元符号。
- 方法名不能以数字开头。
- 方法名不应该是Java关键字。
- 方法名应该具有描述性，清晰地表达方法的功能。

## 2. Java传参的两种方式

在Java中，我们可以使用不同的方式来传递参数给方法或函数。下面将介绍Java传参的两种常见方式：按值传递和按引用传递。

### 2.1 按值传递

按值传递意味着将参数的值复制一份，然后将这份复制的值传递给方法。在方法内部对参数的修改不会影响到原始参数。这种方式适用于基本数据类型（如`int`、`double`等）。

**示例**：
```java
public void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

public static void main(String[] args) {
    int x = 10;
    int y = 20;
    swap(x, y);
    System.out.println("x = " + x); // 输出：x = 10
    System.out.println("y = " + y); // 输出：y = 20
}
```
在这个例子中，虽然`swap`方法内部交换了`a`和`b`的值，但这并不会影响`main`方法中的`x`和`y`，因为传递的是值的副本。

### 2.2 按引用传递

按引用传递意味着将参数的引用（内存地址）传递给方法。在方法内部对参数的修改会影响到原始参数。在Java中，除了基本数据类型，其他所有的数据类型（如数组和对象）都是按引用传递的。

**示例**：
```java
public void swap(int[] array) {
    int temp = array[0];
    array[0] = array[1];
    array[1] = temp;
}

public static void main(String[] args) {
    int[] nums = {10, 20};
    swap(nums);
    System.out.println("nums[0] = " + nums[0]); // 输出：nums[0] = 20
    System.out.println("nums[1] = " + nums[1]); // 输出：nums[1] = 10
}
```
在这个例子中，传递了一个数组`nums`给`swap`方法，方法内部对数组元素的交换操作会直接影响到原始数组。


### 总结

- **按值传递**：传递参数值的副本，不会影响原始参数。
- **按引用传递**：传递参数的引用，方法内部的修改会影响原始参数。

根据具体的需求，选择合适的参数传递方式可以更好地实现程序功能。


## 3. 形式参数与实际参数

在Java中，函数的参数分为形式参数（形参）和实际参数（实参）。这两者在函数调用和定义中扮演不同的角色：

### 3.1 形式参数（Formal Parameters）

形式参数是在函数定义时声明的参数，它们作为函数的一部分，用来接收调用函数时传递的实际参数的值。形式参数在函数定义的括号内部声明，并指定它们的类型和名称。例如，以下是一个简单的函数定义，它有两个形式参数：

 ```java
 public void calculateSum(int a, int b) {
     // 函数体
     int sum = a + b;
     System.out.println("Sum: " + sum);
 }
 ```

在这个例子中，`calculateSum` 是一个函数，它接受两个形式参数 `a` 和 `b`，它们的类型都是 `int`。这些形式参数在函数被调用时用于接收传递给函数的实际参数的值。

### 3.2 实际参数（Actual Arguments）

实际参数是在调用函数时传递给函数的值或者表达式。它们是真正用来执行函数操作的数据。在函数调用时，实际参数被传递给函数的形式参数。例如，下面是如何调用上面定义的 `calculateSum` 函数，并传递实际参数：

 ```java
 public class Main {
     public static void main(String[] args) {
         int num1 = 10;
         int num2 = 20;

         // 调用函数并传递实际参数
         calculateSum(num1, num2);
     }

     // 定义函数
     public static void calculateSum(int a, int b) {
         // 函数体
         int sum = a + b;
         System.out.println("Sum: " + sum);
     }
 }
 ```

在这个示例中，`num1` 和 `num2` 是 `main` 函数中的两个变量，它们作为实际参数传递给 `calculateSum` 函数。在函数调用 `calculateSum(num1, num2);` 中，`num1` 和 `num2` 分别传递给 `a` 和 `b` 形式参数，进而在函数内部计算它们的和。

### 3.3 总结

- 形式参数是在函数定义中声明的变量，它们用于接收实际参数的值。
- 实际参数是在函数调用时传递给函数的值或表达式，它们被传递给形式参数，用于函数执行。

## 4. 课后练习

### 4.1 方法的定义
### 题目 1: 在MathUtils中定义 multiply 方法，它会接受两个 float 参数，并返回它们的乘积。
 ```java
 public class MathUtils {

    // To be implemented

    public static void main(String[] args) {
        MathUtils utils = new MathUtils();
        float product = utils.multiply(5.5f, 3.2f);
        System.out.println("The product is: " + product);  // 输出应该是 17.6
    }
}
 ```
解答
 ```java
public class MathUtils {
    public float multiply(float a, float b) {
        return a * b;
    }

    public static void main(String[] args) {
        MathUtils utils = new MathUtils();
        float product = utils.multiply(5.5f, 3.2f);
        System.out.println("The product is: " + product);  // 输出应该是 17.6
    }
}
 ```

### 题目 2: 请将下列代码（Lesson2课后练习）的点单、打印客户点单内容、计算订单总价三个功能封装成独立的方法。

 ```java
 import java.util.Scanner;

 public class RestaurantOrder {
     public static void main(String[] args) {
         // 定义价格常量
         final double BURGER_PRICE = 12.5;
         final double FRIES_PRICE = 6.0;
         final double COKE_PRICE = 4.5;

         // 创建Scanner对象以获取用户输入
         Scanner scanner = new Scanner(System.in);

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
             System.out.print("\n请点单（输入-1退出，其他整数进入点单）：");
             option = scanner.nextInt();

             // 如果输入为0，则退出循环
             if (option == -1) {
                 break;
             }

             System.out.print("请输入汉堡的数量：");
             burgers = scanner.nextInt();

             System.out.print("请输入薯条的数量：");
             fries = scanner.nextInt();

             System.out.print("请输入可乐的数量：");
             cokes = scanner.nextInt();

             // 打印客户点单内容
             System.out.println("\n客户点单内容：");
             if (burgers > 0) {
                 System.out.println("汉堡 x " + burgers);
             }
             if (fries > 0) {
                 System.out.println("薯条 x " + fries);
             }
             if (cokes > 0) {
                 System.out.println("可乐 x " + cokes);
             }

             // 计算本次点单的总价
             double orderTotal = burgers * BURGER_PRICE + fries * FRIES_PRICE + cokes * COKE_PRICE;
             // 累加到总销售额
             totalSales += orderTotal;

             // 打印本次点单的总价
             System.out.println("\n本次点单总价：" + orderTotal + " 元");
         }

         // 打印所有顾客的总销售额
         System.out.println("\n所有顾客的总销售额：" + totalSales + " 元");

         // 关闭Scanner
         scanner.close();
     }
 }
 ```

参考答案
 ```java
 import java.util.Scanner;

 public class RestaurantOrder {
 // 定义价格常量
 private static final double BURGER_PRICE = 12.5;
 private static final double FRIES_PRICE = 6.0;
 private static final double COKE_PRICE = 4.5;

     public static void main(String[] args) {
         Scanner scanner = new Scanner(System.in);
         double totalSales = 0.0;

         while (true) {
             int option = getUserOption(scanner);

             if (option == -1) {
                 break;
             }

             int burgers = getQuantity(scanner, "汉堡");
             int fries = getQuantity(scanner, "薯条");
             int cokes = getQuantity(scanner, "可乐");

             printOrderDetails(burgers, fries, cokes);
             double orderTotal = calculateOrderTotal(burgers, fries, cokes);
             totalSales += orderTotal;

             System.out.println("\n本次点单总价：" + orderTotal + " 元");
         }

         System.out.println("\n所有顾客的总销售额：" + totalSales + " 元");

         scanner.close();
     }

     // 获取用户的点单选项
     private static int getUserOption(Scanner scanner) {
         System.out.print("\n请点单（输入-1退出，其他整数进入点单）：");
         return scanner.nextInt();
     }

     // 获取特定商品的数量
     private static int getQuantity(Scanner scanner, String itemName) {
         System.out.print("请输入" + itemName + "的数量：");
         return scanner.nextInt();
     }

     // 打印客户点单内容
     private static void printOrderDetails(int burgers, int fries, int cokes) {
         System.out.println("\n客户点单内容：");
         if (burgers > 0) {
             System.out.println("汉堡 x " + burgers);
         }
         if (fries > 0) {
             System.out.println("薯条 x " + fries);
         }
         if (cokes > 0) {
             System.out.println("可乐 x " + cokes);
         }
     }

     // 计算订单总价
     private static double calculateOrderTotal(int burgers, int fries, int cokes) {
         return burgers * BURGER_PRICE + fries * FRIES_PRICE + cokes * COKE_PRICE;
     }
 }
 ```


### 4.2 形式参数与实际参数

### 判断题

**题目：** 观察以下代码，判断参数 `x` 和 `y` 是实际参数还是形式参数，它们是否会被修改，`modifyValues` 方法是否会对它们产生影响。选择正确的答案并解释原因。

```java
public class Test {
    public static void main(String[] args) {
        int x = 5;
        int y = 10;
        modifyValues(x, y);
        System.out.println("x = " + x + ", y = " + y);
    }

    public static void modifyValues(int a, int b) {
        a = a * 2;
        b = b + 3;
    }
}
```

**A. 正确，`x` 和 `y` 的值会被修改**

**B. 错误，`x` 和 `y` 的值不会被修改**


**答案：** B. 错误

**理由：** 在 Java 中，方法参数是按值传递的。当 `modifyValues` 方法被调用时，`a` 和 `b` 是 `x` 和 `y` 的副本，对它们的修改不会影响到原始的 `x` 和 `y`。因此，`x` 和 `y` 的值不会被修改，输出仍然是 `x = 5, y = 10`。

