# Lesson10 集合专题

## 目录
1. [集合的基本概念](#1-集合的基本概念)
   - [1.1 集合的创建](#11-集合的创建)
   - [1.2 集合的特性](#12-集合的特性)
   - [1.3 set 的应用场景](#13-set-的应用场景)
   - [1.4 完整实例](#14-完整实例)
2. [例题讲解](#2-例题讲解)
   - [2.1 LC349 两个数组的交集](#21-lc349-两个数组的交集)
   - [2.2 LC645 错误的集合](#22-lc645-错误的集合)
3. [举一反三](#3-举一反三)
   - [3.1 LC575 分糖果](#31-lc575-分糖果)
   - [3.2 LC771 宝石与石头](#32-lc771-宝石与石头)
4. [课后练习](#4-课后练习)

## 1. 集合的基本概念

`set` 是 Python 中一个无序且不重复的元素集合。集合中的元素是唯一的，且存储的顺序不固定。

### 1.1 集合的创建

#### 集合的创建

集合（set）是一个无序的不重复元素序列。

集合中的元素不会重复，并且可以进行交集、并集、差集等常见的集合操作。

可以使用大括号 **{ }** 创建集合，元素之间用逗号 **,** 分隔， 或者也可以使用 **set()** 函数创建集合。

**创建格式：**

```
parame = {value01,value02,...}
或者
set(value)
```

以下是一个简单实例：

```
set1 = {1, 2, 3, 4}            # 直接使用大括号创建集合
set2 = set([4, 5, 6, 7])      # 使用 set() 函数从列表创建集合
```

**注意：**创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。

### 1.2 集合的特性

1. **元素唯一性**：集合中的元素不能重复，每个元素在集合中只能出现一次。
2. **无序**：集合中的元素没有固定的存储顺序。
3. **常用方法**：
   - `add()`：向集合中添加元素。如果元素已存在，则不会重复添加。
   - `remove()`：从集合中删除指定的元素。
   - `discard()`：删除元素，但如果元素不存在，则不会报错。
   - `clear()`：清空集合中的所有元素。
   - `len()`：返回集合中元素的数量。
   - `in`：判断某个元素是否在集合中。

```
# 创建集合
languages = {"Python", "Java", "JavaScript"}

# 向集合中添加元素
languages.add("Ruby")
print(languages)  # 输出: {'Python', 'Ruby', 'Java', 'JavaScript'}

# 删除元素
languages.remove("JavaScript")
print(languages)  # 输出: {'Python', 'Ruby', 'Java'}

# 获取集合的长度
print(len(languages))  # 输出: 3

# 检查元素是否存在
print("Python" in languages)  # 输出: True

# 清空集合
languages.clear()
print(languages)  # 输出: set()
```



### 1.3 `set` 的应用场景

**去重**：当需要去除重复元素时，集合非常有用。例如，从列表中删除重复项。

**集合操作**：集合支持各种集合运算，如交集、并集和差集。

交集：找到两个集合中共同的元素

```
set1 = {"A", "B", "C"}
set2 = {"B", "C", "D"}
intersection = set1 & set2
print(intersection)  # 输出: {'B', 'C'}
```

并集：合并两个集合的所有元素

```
union = set1 | set2
print(union)  # 输出: {'A', 'B', 'C', 'D'}
```

差集：找出只存在于第一个集合中的元素

```
difference = set1 - set2
print(difference)  # 输出: {'A'}
```

### 1.4 完整实例

```
# 集合操作的示例
set1 = {"A", "B", "C"}
set2 = {"B", "C", "D"}

# 交集
intersection = set1 & set2
print("Intersection (交集):", intersection)  # 输出: {'B', 'C'}

# 并集
union = set1 | set2
print("Union (并集):", union)  # 输出: {'A', 'B', 'C', 'D'}

# 差集
difference = set1 - set2
print("Difference (差集):", difference)  # 输出: {'A'}
```

## 2. 例题讲解

### 2.1 LC349 两个数组的交集

### 题目描述

给定两个数组 `nums1` 和 `nums2` ，返回它们的 `交集`。

输出结果中的每个元素一定是唯一的。我们可以不考虑输出结果的顺序 。

### 解法1 思路分析

1. **初始化集合**：首先，将其中一个数组（例如 `nums2`）转换为集合，这样我们可以快速检查元素是否存在。
2. **创建结果集合**：初始化一个空集合，用于存储最终的交集结果。
3. **遍历并检查**：遍历另一个数组（例如 `nums1`），对于数组中的每个元素，检查它是否存在于 `nums2` 的集合中。
4. **添加到结果集合**：如果元素存在于 `nums2` 的集合中，将其添加到结果集合中，并从 `nums2` 的集合中移除该元素，以确保结果中的元素是唯一的。
5. **转换为列表**：最后，将结果集合转换为列表并返回。

### 参考解答

```
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # 将nums2转换为集合
        set2 = set(nums2)
        # 使用集合来存储交集结果
        intersect_set = set()
        # 遍历nums1，检查每个元素是否在set2中
        for num in nums1:
            if num in set2:
                intersect_set.add(num)
                # 从set2中移除该元素，确保结果中元素唯一
                set2.remove(num)
        # 返回结果集合转换为列表
                            return list(intersect_set)
```



### 解法2 思路分析

1.将两个数组变为使用set()变为集合

2.直接使用&运算符来获得两个集合的交集

3.返回list

### 参考答案：

```
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        set1 = set(nums1)
        set2 = set(nums2)
        # 求交集并返回
        return list(set1 & set2)
```

### 2.2 LC645 错误的集合

### 问题描述

集合 `s` 包含从 `1` 到 `n` 的整数。不幸的是，因为数据错误，导致集合里面某一个数字复制了成了集合里面的另外一个数字的值，导致集合丢失了一个数字，并且有一个数字重复 。

给定一个数组 `nums` 代表了集合 `S` 发生错误后的结果。

请你找出重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

### 思路分析

1. 使用集合来存储出现过的数字，找到重复的数字。

2. 遍历 1 到 `n` 的数字，找出丢失的那个。

3. 返回重复的数字和丢失的数字。

### 参考解答

```
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        num_set = set()
        duplicate = 0
        n = len(nums)

        # 查找重复的数字
        for num in nums:
            if num in num_set:
                duplicate = num
            else:
                num_set.add(num)

        # 查找丢失的数字
        for i in range(1, n+1):
            if i not in num_set:
                missing = i
                break
        return [duplicate, missing]
```

## 3. 举一反三

### 3.1 LC575 分糖果

#### 问题描述

Alice 有 `n` 枚糖，其中第 `i` 枚糖的类型为 `candyType[i]`。Alice 注意到她的体重正在增长，所以前去拜访了一位医生。

医生建议 Alice 要少摄入糖分，只吃掉她所有糖的 `n / 2` 即可（n 是一个偶数）。Alice 非常喜欢这些糖，她想要在遵循医生建议的情况下，尽可能吃到最多不同种类的糖。

给你一个长度为 `n` 的整数数组 `candyType`。

返回： Alice 在仅吃掉 `n / 2` 枚糖的情况下，可以吃到糖的最多种类数。


### 解题思路

1. 使用集合去重计算糖果的种类数。
2. 返回糖果种类数与可吃糖果数量中的较小值。

### 参考解答

```
class Solution:
    def distributeCandies(self, candyType: List[int]) -> int:
        # 使用集合来去重
        unique_candies = set(candyType)
        
        # Alice 能吃的糖果数量
        n = len(candyType) // 2
        
        # 返回能吃的最多种类
        return min(len(unique_candies), n)
```

### 逻辑推理

- **种类数 vs 可吃数量**：
  - **种类数 (len(unique_candies))**：这是 Alice 可以选择的不同糖的类型数量。如果 `种类数` 小于 `可吃数量`，这意味着 Alice 可以吃掉更多糖，但由于糖的种类不足，她的选择会受到限制。
  - **可吃数量 (n)**：这是 Alice 根据医生建议能吃的糖的数量。如果 `可吃数量` 小于 `种类数`，这意味着虽然 Alice 拥有足够多的糖种类，但她只能选择一部分，因为她不能吃超过她的配额。

### 为什么取最小值

- 使用 Python 内置的 `min()` 函数来计算最终结果，确保 Alice 在吃糖数量和糖种类之间做出合理的选择。具体来说：
  - 如果 种类数 大于 可吃数量n，则 Alice 只能吃 n 个糖，即使有更多种类，她也只能选择一部分。
  - 如果 种类数 小于 可吃数量n，则 Alice 可以选择所有不同种类的糖，不用担心数量限制。

### 3.2 LC771 宝石与石头

### 问题描述

给你一个字符串 `jewels` 代表石头中宝石的类型，另有一个字符串 `stones` 代表你拥有的石头。 

`stones` 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。

字母区分大小写，因此 `"a"` 和 `"A"` 是不同类型的石头。

### 解题思路：

1. 使用集合存储宝石的类型。

2. 遍历石头的字符串，检查是否为宝石，计数出现次数。


### 参考解答

```
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        jewel_set = set(jewels)
    
        # 计数石头中宝石的数量
        count = 0
        for stone in stones:
            if stone in jewel_set:
                count += 1
        
        return count
```

## 4. 课后练习

| 题目编号 | 题目名称                 | 简介                                                     |
| -------- | ------------------------ | -------------------------------------------------------- |
| LC 187   | 重复的 DNA 序列          | 找到所有出现次数超过一次的 DNA 序列。                    |
| LC 961   | N 次重复元素在 2N 数组中 | 在长度为 2N 的数组中找到出现 N 次的元素。                |
| LC 2441  | 存在其负数的最大正整数   | 找到一个正整数，其负数也在数组中存在。                   |
| LC 2357  | 通过减去相同数使数组为零 | 通过减去相同的数使数组中的所有元素变为零的最小操作次数。 |
| LC 217  | 存在重复元素 | 给你一个整数数组nums，如果任一值在数组中出现至少两次，返回true，否则false。 |

