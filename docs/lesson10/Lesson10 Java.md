# Lesson10 集合专题

## 目录

1. [集合的基本概念](#1-集合的基本概念)
    - [1.1 Set 接口的特性](#11-set-接口的特性)
    - [1.2 Set 的种类](#12-set-的种类)
    - [1.3 Set 的应用场景](#13-set-的应用场景)
    - [1.4 完整实例](#14-完整实例)
2. [例题讲解](#2-例题讲解)
    - [2.1 LC349 两个数组的交集](#21-lc349-两个数组的交集)
    - [2.2 LC645 错误的集合](#22-lc645-错误的集合)
3. [举一反三](#3-举一反三)
    - [3.1 LC575 分糖果](#31-lc575-分糖果)
    - [3.2 LC771 宝石与石头](#32-lc771-宝石与石头)
4. [课后练习](#4-课后练习)


## 1. 集合的基本概念

`Set` 是 Java 集合框架中的一个重要接口，它用于存储**无序**的、**不重复**的元素。`Set` 不允许包含重复的元素，即使插入相同的元素，也只会保留一个。此外，`Set` 并不保证元素的存储顺序。

### 1.1 Set 接口的特性：
1. **元素唯一性**：`Set` 不允许重复元素，这意味着每个元素在集合中只能出现一次。
2. **无序**：`Set` 不保证元素的插入顺序（但某些实现，如 `LinkedHashSet` 可以维护插入顺序）。
3. **常用方法**：
   - `add(E e)`：向集合中添加元素，如果元素已经存在，则不会添加并返回 `false`。
   - `remove(Object o)`：从集合中移除指定的元素。
   - `contains(Object o)`：检查集合是否包含某个元素。
   - `size()`：返回集合中元素的数量。
   - `isEmpty()`：判断集合是否为空。
   - `clear()`：清空集合。

### 1.2 Set 的种类

Java 提供了几种常见的 `Set` 实现类，包括 `HashSet`，`LinkedHashSet`，`TreeSet`等，本章节仅对最常见的`HashSet`进行介绍

### **HashSet**
- `HashSet` 是最常用的 `Set` 实现，它基于哈希表来存储元素，因而具有很好的性能。
- 元素无序，不保证插入顺序。
- 允许存储 `null` 元素。

**使用示例：**
```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Java");
        set.add("Python");
        set.add("Java"); // 重复元素不会被添加

        // 遍历并输出集合中的元素
        for (String lang : set) {
            System.out.println(lang);
        }

        // 判断集合中是否包含某个元素
        if (set.contains("Java")) {
            System.out.println("Set contains Java");
        }

        // 移除元素
        set.remove("Python");
        System.out.println("After removing Python: " + set);

        // 输出集合大小
        System.out.println("Set size: " + set.size());
    }
}

```

### 1.3 Set 的应用场景
- **去重功能**：当需要存储不重复的元素时，`Set` 是理想的选择。例如，在一个系统中去除重复的用户名。
- **集合操作**：`Set` 具有很强的集合操作能力，如求交集、并集和差集，可以通过 `retainAll()`、`addAll()`、`removeAll()` 等方法来实现。
   - **交集**（两个集合共有的元素）：
```java
Set<String> set1 = new HashSet<>(Arrays.asList("A", "B", "C"));
Set<String> set2 = new HashSet<>(Arrays.asList("B", "C", "D"));
set1.retainAll(set2);  // set1 现在是 ["B", "C"]
```

   - **并集**（两个集合的所有元素）：

```java
set1.addAll(set2);  // set1 现在是 ["A", "B", "C", "D"]
```

   - **差集**（仅存在于第一个集合的元素）：

```java
set1.removeAll(set2);  // set1 现在是 ["A"]
```
     
### 1.4 完整实例
```java
import java.util.HashSet;
import java.util.Set;

public class SetOperationsExample {
    public static void main(String[] args) {
        // 创建两个集合
        Set<String> set1 = new HashSet<>();
        set1.add("A");
        set1.add("B");
        set1.add("C");

        Set<String> set2 = new HashSet<>();
        set2.add("B");
        set2.add("C");
        set2.add("D");

        // 交集（保留两个集合共有的元素）
        Set<String> intersection = new HashSet<>(set1);
        intersection.retainAll(set2);
        System.out.println("Intersection (交集): " + intersection);  // 输出：[B, C]

        // 并集（两个集合所有元素的组合）
        Set<String> union = new HashSet<>(set1);
        union.addAll(set2);
        System.out.println("Union (并集): " + union);  // 输出：[A, B, C, D]

        // 差集（只存在于 set1 中的元素）
        Set<String> difference = new HashSet<>(set1);
        difference.removeAll(set2);
        System.out.println("Difference (差集): " + difference);  // 输出：[A]
    }
}
```

## 2. 例题讲解

### 2.1 LC349 两个数组的交集

### 题目描述

给定两个数组 `nums1` 和 `nums2` ，返回它们的 `交集`。

输出结果中的每个元素一定是唯一的。我们可以不考虑输出结果的顺序 。

### 解法1 

### 思路分析：

1. **使用两个 Set 存储数组的唯一元素**：
   - 将 `nums1` 和 `nums2` 中的元素分别放入两个 `HashSet`，以去重并存储唯一的元素。

2. **比较 Set 的大小**：
   - 在 `intersection` 方法中，通过比较 `set1` 和 `set2` 的大小，选择较小的集合进行遍历。这样做的原因是较小的集合中元素较少，因此能减少遍历和查找的次数，提高效率。

3. **遍历较小的集合**：
   - 使用 `getIntersection` 方法时，较小的集合 `smallerSet` 被遍历，并检查其中的元素是否存在于较大的集合 `largerSet` 中。如果存在，则将该元素加入交集集合 `intersectionSet`。

4. **将交集集合转换为数组**：
   - 将 `intersectionSet` 中的交集元素存入数组，最终返回这个数组。

### 参考解答

```java
import java.util.HashSet;
import java.util.Set;

public class ArrayIntersection {
    public int[] intersection(int[] nums1, int[] nums2) {
        // 将第一个数组的元素放入 Set 中
        Set<Integer> set1 = new HashSet<>();
        for (int num : nums1) {
            set1.add(num);
        }

        // 将第二个数组的元素放入 Set 中
        Set<Integer> set2 = new HashSet<>();
        for (int num : nums2) {
            set2.add(num);
        }

        // 直接根据大小判断，遍历较小的集合
        if (set1.size() > set2.size()) {
            return getIntersection(set2, set1);
        } else {
            return getIntersection(set1, set2);
        }
    }

    public int[] getIntersection(Set<Integer> smallerSet, Set<Integer> largerSet) {
        // 创建一个 Set 用于存储交集
        Set<Integer> intersectionSet = new HashSet<>();
        for (int num : smallerSet) {
            if (largerSet.contains(num)) {
                intersectionSet.add(num);
            }
        }

        // 将交集集合转换为数组并返回
        int[] intersection = new int[intersectionSet.size()];
        int index = 0;
        for (int num : intersectionSet) {
            intersection[index++] = num;
        }
        return intersection;
    }
}
```

### 解法2

### 解题思路：

1. 将两个数组分别转换为 `HashSet`，因为 `Set` 能去除重复的元素，并且可以方便地进行集合运算。
2. 使用 `retainAll()` 方法来获取两个集合的交集。
3. 将交集结果转换为数组并返回。

### 参考解答

```java
import java.util.HashSet;
import java.util.Set;

public class ArrayIntersection {
    public int[] intersection(int[] nums1, int[] nums2) {
        // 将两个数组转换为 Set
        Set<Integer> set1 = new HashSet<>();
        for (int num : nums1) {
            set1.add(num);
        }

        Set<Integer> set2 = new HashSet<>();
        for (int num : nums2) {
            set2.add(num);
        }

        // 使用 retainAll() 保留交集
        set1.retainAll(set2);

        // 将交集转换为数组并返回
        int[] result = new int[set1.size()];
        int index = 0;
        for (int num : set1) {
            result[index++] = num;
        }
        return result;
    }
}
```

### 2.2 LC645 错误的集合

### 问题描述

集合 `s` 包含从 `1` 到 `n` 的整数。不幸的是，因为数据错误，导致集合里面某一个数字复制了成了集合里面的另外一个数字的值，导致集合丢失了一个数字，并且有一个数字重复 。

给定一个数组 `nums` 代表了集合 `S` 发生错误后的结果。

请你找出重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

### 解题思路：

1. **使用 HashSet 存储出现的数字**：
   - 遍历数组 `nums`，将所有数字添加到一个 `HashSet` 中。由于 `HashSet` 不允许重复的元素，我们可以在添加时检查是否已经存在该数字，从而找到重复的数字。

2. **检查数字范围**：
   - 由于集合应包含从 `1` 到 `n` 的所有数字，我们可以通过遍历从 `1` 到 `n` 的每一个数字，检查这些数字是否存在于 `HashSet` 中。若某个数字不在 `HashSet` 中，则该数字是丢失的数字。

3. **返回结果**：
   - 将找到的重复数字和丢失数字以数组的形式返回。

### 参考解答

```java
import java.util.HashSet;

public class Solution {
    public int[] findErrorNums(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        int duplicate = -1;
        int n = nums.length;

        // 查找重复的数字并将所有数字添加到 HashSet
        for (int num : nums) {
            if (!set.add(num)) {  // add() 返回 false 表示已经存在
                duplicate = num;  // 找到重复的数字
            }
        }

        int missing = -1;

        // 查找丢失的数字
        for (int i = 1; i <= n; i++) {
            if (!set.contains(i)) { // 如果 HashSet 中不包含数字 i
                missing = i;        // 记录丢失的数字
                break;              // 找到后直接退出循环
            }
        }

        return new int[] {duplicate, missing};
    }
}
```

## 3. 举一反三

### 3.1 LC575 分糖果

#### 问题描述

Alice 有 `n` 枚糖，其中第 `i` 枚糖的类型为 `candyType[i]`。Alice 注意到她的体重正在增长，所以前去拜访了一位医生。

医生建议 Alice 要少摄入糖分，只吃掉她所有糖的 `n / 2` 即可（n 是一个偶数）。Alice 非常喜欢这些糖，她想要在遵循医生建议的情况下，尽可能吃到最多不同种类的糖。

给你一个长度为 `n` 的整数数组 `candyType`。

返回： Alice 在仅吃掉 `n / 2` 枚糖的情况下，可以吃到糖的最多种类数。


### 解题思路

1. **统计糖的种类**：使用一个 `HashSet` 来存储不同类型的糖，这样可以自动去除重复的糖类型。
2. **计算能吃的糖的数量**：由于 Alice 只能吃掉 \( n / 2 \) 枚糖，我们需要计算不同类型的糖的数量与 \( n / 2 \) 的最小值。
3. **返回结果**：返回能吃到的最多种类的糖。

### 参考解答

```java
import java.util.HashSet;

public class Solution {
    public int distributeCandies(int[] candyType) {
        // 使用 HashSet 来存储不同的糖的种类
        HashSet<Integer> uniqueCandyTypes = new HashSet<>();
        
        // 将所有糖的类型添加到 HashSet
        for (int candy : candyType) {
            uniqueCandyTypes.add(candy);
        }

        // 计算 Alice 能吃的糖的数量
        int n = candyType.length;
        int maxTypes = uniqueCandyTypes.size(); // 不同糖的种类数
        int canEatCount = n / 2; // Alice 能吃的糖的数量

        // 返回最多可以吃到的种类数
        return Math.min(maxTypes, canEatCount);
    }
}
```

### 逻辑推理

- **种类数 vs 可吃数量**：
   - **种类数 (`maxTypes`)**：这是 Alice 可以选择的不同糖的类型数量。如果 `maxTypes` 小于 `canEatCount`，这意味着 Alice 可以吃掉更多的糖，但因为不同种类的糖不足，所以她的选择受到限制。
   - **可吃数量 (`canEatCount`)**：这是 Alice 依据医生建议所能吃掉的糖的数量。如果 `canEatCount` 小于 `maxTypes`，这意味着虽然 Alice 拥有足够多的糖种类，但她只能选择一部分，因为她不能吃掉超过她的配额。

### 为什么取最小值

- 使用 `Math.min(maxTypes, canEatCount)` 计算最终结果，确保 Alice 在吃糖的数量和糖的种类之间做出合理的选择。具体来说：
   - 如果 `maxTypes` 大于 `canEatCount`，则 Alice 只能吃掉 `canEatCount` 的糖。她虽然有更多种类可选，但只能选择其中的 \( n/2 \) 个。
   - 如果 `maxTypes` 小于 `canEatCount`，则 Alice 可以选择所有的不同种类的糖，而不必担心数量限制，因为她只想吃不同的糖。



### 3.2 LC771 宝石与石头

### 问题描述

给你一个字符串 `jewels` 代表石头中宝石的类型，另有一个字符串 `stones` 代表你拥有的石头。 

`stones` 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。

字母区分大小写，因此 `"a"` 和 `"A"` 是不同类型的石头。

### 解题思路：

1. **添加宝石字符**：
   - 使用 `for` 循环遍历 `jewels` 字符串，将每个字符添加到 `HashSet` 中。

2. **计算宝石数量**：
   - 初始化计数器 `count` 为 0，然后遍历 `stones` 字符串，检查每个字符是否在 `jewelSet` 中。
   - 如果存在，将计数器加一。


### 参考解答
```java
import java.util.HashSet;

public class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        // 创建一个 HashSet 来存储宝石的类型
        HashSet<Character> jewelSet = new HashSet<>();
        
        // 将 jewels 中的每个字符添加到 HashSet 中
        for (char jewel : jewels.toCharArray()) {
            jewelSet.add(jewel);
        }

        // 初始化计数器
        int count = 0;

        // 遍历 stones，计算宝石的数量
        for (char stone : stones.toCharArray()) {
            if (jewelSet.contains(stone)) {
                count++; // 如果 stone 是宝石，计数加一
            }
        }

        return count; // 返回宝石的数量
    }
}
```

## 4. 课后练习
| 题目编号 | 题目名称                 | 简介                                                     |
| -------- | ------------------------ | -------------------------------------------------------- |
| LC 187   | 重复的 DNA 序列          | 找到所有出现次数超过一次的 DNA 序列。                    |
| LC 961   | N 次重复元素在 2N 数组中 | 在长度为 2N 的数组中找到出现 N 次的元素。                |
| LC 2441  | 存在其负数的最大正整数   | 找到一个正整数，其负数也在数组中存在。                   |
| LC 2357  | 通过减去相同数使数组为零 | 通过减去相同的数使数组中的所有元素变为零的最小操作次数。 |
| LC 217  | 存在重复元素 | 给你一个整数数组nums，如果任一值在数组中出现至少两次，返回true，否则false。 |
