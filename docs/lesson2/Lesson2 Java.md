# Lesson2 Java的条件语句与循环语句

## 目录
1. [Java的条件语句](#java的条件语句)
    - [1.1 if 条件语句](#11-if-条件语句)
    - [1.2 if...else 条件语句](#12-ifelse-条件语句)
    - [1.3 if...else if...else](#13-ifelse-ifelse)
    - [1.4 嵌套的if...else 语句](#14-嵌套的ifelse-语句)
    - [1.5 switch 语句](#15-switch-语句)

2. [Java的循环语句](#java的循环语句)
    - [2.1 for循环](#21-for循环)
    - [2.2 倒序遍历](#22-倒序遍历)
    - [2.3 IntStream.range()函数](#23-intstreamrange函数)
    - [2.4 while循环](#24-while循环)
    - [2.5 增强for循环（for each循环）](#25-增强for循环foreach循环)

3. [break 语句](#break-语句)
    - [3.1 在循环中使用 break](#31-在循环中使用-break)
    - [3.2 在 switch 语句中使用 break](#32-在-switch-语句中使用-break)
    - [3.3 嵌套循环的break](#33-嵌套循环的break)

4. [continue 语句](#4-continue-语句)

5. [课后练习](#5-课后练习)
    - [5.1 点餐程序](#51-点餐程序)
    - [5.2 计算并输出 1 到 100 之间所有不能被 3 整除的数的平方和](#52-计算并输出-1-到-100-之间所有不能被-3-整除的数的平方和)


## 1. Java的条件语句

条件语句是编程中一种基本的控制结构，用于根据不同的条件执行不同的代码块。它们使程序能够根据输入、状态或计算结果来做出决策和执行相应的操作。在Java中，常见的条件语句包括`if`、`else if`和`else`组合以及`switch`语句。

1. **if语句**：用于在条件为真时执行特定的代码块，如果条件不满足，可以选择执行一个备用代码块。
  
2. **else if语句**：用于检查多个条件，如果前一个条件不满足，则检查下一个条件，直到找到一个满足条件的分支执行相应的代码块。
  
3. **else语句**：可选的，当所有上述条件都不满足时执行的默认代码块。
  
4. **switch语句**：用于在多个固定选项之间进行选择，根据表达式的值执行对应的代码块，每个选项被称为一个`case`，可以包含一个可选的`default`分支作为所有`case`不匹配时的备选方案。
  

条件语句使得程序在运行时可以根据不同的情况采取不同的行动，从而增强了程序的灵活性和逻辑性。以下是常见的组合：

### 1.1 **if 条件语句**
语法如下：
```java
if(布尔表达式)
{
   //如果布尔表达式为true将执行的语句
}
```
如果布尔表达式成立（true），则执行 if 语句中的代码块，如果不成立（false）则执行 if 语句块后面的代码。

简单案例：

键盘录入一个数，如果这个数大于10并且小于100，则控制台输出合格

```java
import java.util.Scanner;
 
public class IfTest01 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个数字");
        int num = sc.nextInt();
 
        if (num > 10 && num < 100){
            System.out.println("合格");
        }
    }
}
```

### 1.2 **if...else 条件语句**

语法如下：
```java
if(布尔表达式){
   //如果布尔表达式的值为true
} else {
   //如果布尔表达式的值为false
}
```
如果布尔表达式成立（true），则执行 if 语句中的代码块，如果不成立（false），则执行else语句中的代码块。

简单案例：

定义一个布尔类型，将true赋值给incident。如果事件（incident）为真则输出正确，否则输出错误。
```java
public class IfTest02 {
    public static void main(String[] args) {
 
        //定义事件为真
        boolean incident = true;
        if (incident){
            System.out.println("正确");
        } else {
            System.out.println("错误");
        }
    }
}
```

### 1.3 **if...else if...else**
语法如下：

```java
if(布尔表达式 1){
   //如果布尔表达式 1的值为true执行代码
} else if(布尔表达式 2){
   //如果布尔表达式 2的值为true执行代码
} else if(布尔表达式 3){
   //如果布尔表达式 3的值为true执行代码
} else {
   //如果以上布尔表达式都不为true执行代码
}
```
如果布尔表达式1为真，则执行布尔表达式2；如果布尔表达式2为真，则执行布尔表达式3；依次执行后面的布尔表示，直到布尔表示为假，则执行else语句中的代码块。

简单案例：

某超市会员制度分为vip1，vip2，vip3三个等级，每个等级对应的折扣不同：vip1客户购买商品打9折，vip2客户购买商品打8折，vip3客户购买商品打7折。现要求定义一个商品价格，在控制台输入客户等级，计算出该客户对应的vip等级购买商品后应该付多少钱。

```java
import java.util.Scanner;
 
public class IfTest05f {
    public static void main(String[] args) {
        int price = 1000;
 
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入会员的级别");
        int vip = sc.nextInt();
 
        if (vip == 1){
            System.out.println("实际支付的钱为" + (price * 0.9));
        } else if (vip == 2) {
            System.out.println("实际支付的钱为" + (price * 0.8));
        } else if (vip == 3) {
            System.out.println("实际支付的钱为" + (price * 0.7));
        } else {
            System.out.println("实际支付的钱为" + price);
        }
    }
}
```

### 1.4 **嵌套的if...else 语句**
语法如下：
```java
if(布尔表达式 1){
   如果布尔表达式 1的值为true执行代码
   if(布尔表达式 2){
      如果布尔表达式 2的值为true执行代码
   }
}
```
简单案例：

键盘录入一个整数代表学生的成绩，规定范围在（0-100）。当输入的成绩大于等于90时，控制台输出优秀；大于等于80小于90时，控制台输出良好；大于等于60小于80时，控制台输出合格；小于60时，控制台输出不合格。其他情况则提示输入不合法。
```java
import java.util.Scanner;
 
public class IfTest04 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入一个整数");
        int num = sc.nextInt();
 
        if (num > 0 && num <= 100) {
 
            if (num >= 90) {
                System.out.println("优秀");
            } else if (num >= 80 && num < 90) {
                System.out.println("良好");
            } else if (num >= 60 && num < 80) {
                System.out.println("合格");
            } else {
                System.out.println("不合格");
            }
        } else {
            System.out.println("输入不合法");
        }
    }
}
```

### 1.5 **switch 语句**
语法如下：
```java
switch (expression) {
    case value1:
        // 当表达式的值等于value1时执行的代码块
        break;
    case value2:
        // 当表达式的值等于value2时执行的代码块
        break;
    ...
    default:
        break;
        // 当表达式的值与所有case不匹配时执行的代码块（可选）
}
```

简单案例：根据阿拉伯数字输出文字信息的星期几。

```java
int dayOfWeek = 1;
switch (dayOfWeek) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    // 省略其余case
    default:
        System.out.println("Invalid day");
        break;
}
```

## 2. Java的循环语句

在Java中，循环语句用于重复执行一段代码，直到满足某个条件为止或达到指定的次数。主要的循环语句有以下几种：

### 2.1 **for循环**：
   ```java
   for (initialization; condition; update) {
       // 循环体
   }
   ```
   - `initialization`：循环变量的初始化。
   - `condition`：循环条件，每次循环开始前都会检查。
   - `update`：循环变量更新，通常是增加或减少循环变量的值。
   
   示例：
   ```java
   for (int i = 1; i <= 5; i++) {
       System.out.println("Count is: " + i);
   }
   ```
### 2.2 **倒序遍历**

倒序遍历是指从大到小或从后向前遍历数据集合中的元素。在Java中，倒序遍历通常用于数组、列表或需要逆序输出的情况。以下是一个示例和详细解释：

```java
for (int i = 5; i > 0; i--) {
    System.out.println("Count is: " + i);
}
```

### 2.3 **IntStream.range()函数**
在Java中，并没有像一些其他编程语言（如Python）中直接提供的内置的 `range` 函数，不过Java 8 引入了 `IntStream` 类来支持函数式编程风格的操作。可以使用 `IntStream.range()` 方法来生成一个整数范围。
```java
IntStream.range(start, end).forEach(i -> {
    // 这里执行循环体内的操作，i 是当前的整数值
});
```

   这里的 `start` 是范围的起始值（包含），`end` 是范围的结束值（不包含）。

### 参数说明

- **起始值 (`start`)**: 数值范围的起始值，可以是任意整数。
- **结束值 (`end`)**: 数值范围的结束值，可以是任意整数。在使用 `for` 循环时，结束值是包含在范围内的；而在使用 `IntStream.range()` 方法时，结束值是不包含在范围内的。

### 示例

下面是一个使用 `IntStream.range()` 方法来遍历数值范围的示例：

```java
// 使用 IntStream.range() 遍历范围 [1, 5)
System.out.println("\nUsing IntStream.range():");
IntStream.range(1, 6).forEach(i -> System.out.println("Count is: " + i));
```

### 输出结果

```
Count is: 1
Count is: 2
Count is: 3
Count is: 4
Count is: 5
```

### 2.4 **while循环**：
   ```java
   while (condition) {
       // 循环体
   }
   ```
   - `condition`：循环条件，在每次循环迭代开始之前评估。
   
   示例：
   ```java
   int i = 1;
   while (i <= 5) {
       System.out.println("Count is: " + i);
       i++;
   }
   ```

### 2.5 **增强for循环（foreach循环）**：
   用于遍历数组或集合中的元素，不需要显式地控制循环变量。
   ```java
   for (type element : array/collection) {
       // 循环体
   }
   ```
   示例：
   ```java
   int[] numbers = {1, 2, 3, 4, 5};
   for (int number : numbers) {
       System.out.println("Number is: " + number);
   }
   ```

## 3. break 语句
在Java中，`break` 是一种控制流语句，通常用于在循环或 switch 语句中提前结束代码块的执行。具体来说，`break` 语句可以用于以下两种情况：

### 3.1 **在循环中使用 `break`**：
   当在循环中执行 `break` 语句时，程序将立即退出当前的循环，继续执行循环后面的代码。这对于在满足某个条件后不再继续执行循环体内的代码非常有用。

   示例：
   ```java
   for (int i = 1; i <= 10; i++) {
       System.out.println(i);
       if (i == 5) {
           break; // 当 i 等于 5 时退出循环
       }
   }
   ```
   输出：
   ```
   1
   2
   3
   4
   5
   ```

### 3.2 **在 switch 语句中使用 `break`**：
   在 switch 语句中，每个 `case` 分支通常会在执行完毕后继续执行下一个 `case` 分支，除非在某个 `case` 分支中使用了 `break` 语句。这时程序将跳出 switch 语句，不再继续执行后续的 `case` 分支。

   示例：
   ```java
   int dayOfWeek = 3;
   switch (dayOfWeek) {
       case 1:
           System.out.println("Monday");
           break;
       case 2:
           System.out.println("Tuesday");
           break;
       case 3:
           System.out.println("Wednesday");
           break;
       default:
           System.out.println("Invalid day");
           break;
   }
   ```
   输出：
   ```
   Wednesday
   ```

### 注意事项：
- `break` 语句只能用在循环 (`for`, `while`, `do-while`) 或 switch 语句的内部。
- 在嵌套的循环中，`break` 语句默认退出最内层的循环，如果想要退出外层循环，可以使用带标签的 `break` 语句（例如 `break label;`）。

### 3.3 嵌套循环的break
### 语法：
带标签的 `break` 语法如下：
```java
labelName: 
outerLoop {
    // 循环体
    innerLoop {
        // 循环体
        if (condition) {
            break labelName; // 跳出标签为 labelName 的外层循环
        }
    }
}
```
其中 `labelName` 是用户定义的标签名，通常遵循标识符命名规则。

### 示例：
假设我们有一个嵌套的循环结构，我们想在内层循环中找到某个条件满足时退出外层循环。

```java
public class BreakWithLabelExample {
    public static void main(String[] args) {
        outerLoop: // 标签名 outerLoop
        for (int i = 1; i <= 3; i++) {
            System.out.println("Outer loop iteration " + i);
            
            innerLoop:
            for (int j = 1; j <= 3; j++) {
                System.out.println("    Inner loop iteration " + j);
                
                if (i == 2 && j == 2) {
                    break outerLoop; // 当 i 等于 2 且 j 等于 2 时跳出外层循环
                }
            }
        }
        
        System.out.println("Loop ends");
    }
}
```

### 示例解释：
- `outerLoop` 是外层循环的标签名。
- `innerLoop` 是内层循环。
- 在内层循环中，当 `i` 等于 2 且 `j` 等于 2 时，执行 `break outerLoop;`，这会立即跳出外层循环 `outerLoop`，继续执行外层循环后面的代码。
- 控制台输出如下：
  ```
  Outer loop iteration 1
      Inner loop iteration 1
      Inner loop iteration 2
  Loop ends
  ```

### 注意事项：
- 使用带标签的 `break` 语句时，标签必须位于你想要跳出的循环之前，并且紧跟在 `break` 关键字之后。
- 标签名可以是任何合法的Java标识符，但建议使用有意义的名字来提高代码的可读性和可维护性。

带标签的 `break` 语句在处理复杂的嵌套循环结构或希望在特定条件下提前跳出外层循环时非常有用。

## 4. continue 语句
在Java中，`continue` 是一种控制流语句，用于跳过当前循环的剩余代码，直接进入下一次循环的迭代。它通常用于循环结构中，可以帮助程序跳过某些特定条件下不必要的代码执行。

### 使用方法和语法：

在循环中使用 `continue` 的一般语法如下：

```java
for (initialization; condition; update) {
    // 代码块
    if (conditionToSkip) {
        continue; // 跳过本次循环的剩余代码，进行下一次循环
    }
    // 其他代码
}
```

或者在 `while` 循环中使用：

```java
while (condition) {
    // 代码块
    if (conditionToSkip) {
        continue; // 跳过本次循环的剩余代码，进行下一次循环
    }
    // 其他代码
}
```

### 示例：

以下是一个使用 `continue` 的示例，演示了如何在循环中跳过偶数的打印：

```java
public class ContinueExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 5; i++) {
            if (i % 2 == 0) {
                continue; // 跳过偶数
            }
            System.out.println(i);
        }
    }
}
```

输出：
```
1
3
5
```

### 解释和注意事项：

- 当程序执行到 `continue;` 语句时，会立即结束当前循环的本次迭代，并开始下一次迭代。
- `continue` 主要用于在不满足某些条件时跳过剩余代码的执行，可以提高代码的效率和简洁性。
- 在嵌套循环中，`continue` 默认只会影响最内层的循环。如果想要跳过外层循环的迭代，可以考虑使用带标签的 `continue` 语句，类似于带标签的 `break` 语句的用法。

`continue` 是编写控制流程更加灵活和清晰的重要工具之一，特别是在需要根据某些条件跳过特定代码块的情况下，它能有效简化代码逻辑。


## 5. 课后练习

### 5.1 点餐程序

题目描述：

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
```
参考解答：
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

### 5.2 计算并输出 1 到 100 之间所有不能被 3 整除的数的平方和

题目描述：

编写一个程序，计算并输出 1 到 100 之间所有不能被 3 整除的数的平方和。在计算过程中，如果平方和超过 1000，则停止计算并输出当前的平方和值。

解题思路：

1. 使用一个循环来遍历从 1 到 100 的所有数。
2. 对于每个数，使用条件语句判断是否能被 3 整除：
    - 如果能被 3 整除，使用 `continue` 跳过这个数，不进行平方和的累加。
    - 如果不能被 3 整除，计算该数的平方，并累加到平方和变量中。
3. 在累加过程中，使用条件语句检查平方和是否超过 1000：
    - 如果超过 1000，则使用 `break` 停止循环。
4. 最终输出停止时的平方和值。

#### 示例代码：

```java
public class SumOfSquares {
    public static void main(String[] args) {
        int sum = 0;
        
        for (int i = 1; i <= 100; i++) {
            if (i % 3 == 0) {
                continue; // 跳过能被 3 整除的数
            }
            
            int square = i * i;
            sum += square;
            
            if (sum > 1000) {
                System.out.println("当前平方和超过 1000，停止计算。");
                System.out.println("当前平方和为: " + sum);
                break;
            }
        }
        
        if (sum <= 1000) {
            System.out.println("最终平方和为: " + sum);
        }
    }
}
```

#### 示例运行和输出：

在运行上述代码时，会依次计算 1 到 100 之间所有不能被 3 整除的数的平方，并累加到平方和变量 `sum` 中。如果累加过程中发现平方和超过 1000，则停止计算，并输出当前的平方和值。

输出示例：
```
当前平方和超过 1000，停止计算。
当前平方和为: 1025
```



