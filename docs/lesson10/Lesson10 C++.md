# Lesson 10: 集合专题
1. [Unordered Set 的基本概念](#1-unordered-set-的基本概念)
   - [1.1 `unordered_set` 的特性](#11-unordered_set-的特性)
   - [1.2 `unordered_set` 的应用场景](#12-unordered_set-的应用场景)
   - [1.3 完整实例](#13-完整实例)
2. [例题讲解](#2-例题讲解)
   - [2.1 LC349 两个数组的交集](#21-lc349-两个数组的交集)
   - [2.2 LC645 错误的集合](#22-lc645-错误的集合)
3. [举一反三](#3-举一反三)
   - [3.1 LC575 分糖果](#31-lc575-分糖果)
   - [3.2 LC771 宝石与石头](#32-lc771-宝石与石头)
4. [课后练习](#4-课后练习)

## 1. Unordered Set 的基本概念

`unordered_set` 是 C++ STL 中的一个容器类，用于存储**无序**的、**不重复**的元素。`unordered_set` 不允许包含重复的元素，如果插入相同的元素，只会保留一个。此外，`unordered_set` 不保证元素的存储顺序。

### 1.1 `unordered_set` 的特性：
1. **元素唯一性**：`unordered_set` 不允许重复元素，每个元素在集合中只能出现一次。
2. **无序**：`unordered_set` 不保证元素的插入顺序。
3. **常用方法**：
   - `insert(const T& value)`：向集合中添加元素，如果元素已经存在，则不会插入。
   - `erase(const T& value)`：从集合中移除指定的元素。
   - `find(const T& value)`：查找集合中是否包含某个元素，返回一个迭代器，如果找不到则返回 `end()`。
   - `size()`：返回集合中元素的数量。
   - `empty()`：判断集合是否为空。
   - `clear()`：清空集合中的所有元素。

### 1.2 `unordered_set` 的应用场景

`unordered_set` 基于哈希表实现，提供了插入、删除和查找操作，适用于以下场景：

- **去重功能**：当需要存储不重复的元素时，`unordered_set` 是理想的选择。例如，用于存储唯一的用户ID、用户名等。
- **集合操作**：`unordered_set` 支持经典的集合操作，如交集、并集和差集，能够有效处理两个集合间的运算。

   - **交集**（两个集合共有的元素）：
     ```cpp
     std::unordered_set<int> set1 = {1, 2, 3};
     std::unordered_set<int> set2 = {2, 3, 4};
     std::unordered_set<int> intersection;
     
     for (int elem : set1) {
         if (set2.find(elem) != set2.end()) {
             intersection.insert(elem);
         }
     }
     // intersection 现在是 {2, 3}
     ```
   - **并集**（两个集合的所有元素）：
     ```cpp
     std::unordered_set<int> union_set = set1;
     union_set.insert(set2.begin(), set2.end());
     // union_set 现在是 {1, 2, 3, 4}
     ```
   - **差集**（仅存在于第一个集合的元素）：
     ```cpp
     std::unordered_set<int> difference;
     for (int elem : set1) {
         if (set2.find(elem) == set2.end()) {
             difference.insert(elem);
         }
     }
     // difference 现在是 {1}
     ```

### 1.3 完整实例

以下是一个完整的使用 `unordered_set` 实现集合操作的 C++ 示例：

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    // 创建两个集合
    std::unordered_set<int> set1 = {1, 2, 3};
    std::unordered_set<int> set2 = {2, 3, 4};

    // 交集
    std::unordered_set<int> intersection;
    for (int elem : set1) {
        if (set2.find(elem) != set2.end()) {
            intersection.insert(elem);
        }
    }
    std::cout << "Intersection (交集): ";
    for (int elem : intersection) std::cout << elem << " ";
    std::cout << std::endl;

    // 并集
    std::unordered_set<int> union_set = set1;
    union_set.insert(set2.begin(), set2.end());
    std::cout << "Union (并集): ";
    for (int elem : union_set) std::cout << elem << " ";
    std::cout << std::endl;

    // 差集
    std::unordered_set<int> difference;
    for (int elem : set1) {
        if (set2.find(elem) == set2.end()) {
            difference.insert(elem);
        }
    }
    std::cout << "Difference (差集): ";
    for (int elem : difference) std::cout << elem << " ";
    std::cout << std::endl;

    return 0;
}
```

### 2. 例题讲解

#### 2.1 LC349 两个数组的交集

#### 题目描述

给定两个数组 `nums1` 和 `nums2`，返回它们的交集。输出结果中的每个元素一定是唯一的，可以不考虑输出结果的顺序。



### 解法1：遍历法

#### 思路分析

1. **遍历**：
   - 使用两个嵌套的循环，遍历 `nums2` 中的每个元素，并检查它是否在 `nums1` 中存在。
   
2. **去重操作**：
   - 使用 `find()` 函数来确保结果中没有重复的元素。

#### 代码实现

```cpp
class Solution {
public:
    std::vector<int> intersection(std::vector<int>& nums1, std::vector<int>& nums2) {
        std::vector<int> result{};
        for(int i = 0; i < nums2.size(); i++) {  // 遍历 nums2 中的每个元素
            for(int j = 0; j < nums1.size(); j++) {  // 在 nums1 中查找该元素
                if(nums1[j] == nums2[i]) {
                    // 确保 result 中没有重复元素
                    if(std::find(result.begin(), result.end(), nums2[i]) == result.end()) {
                        result.push_back(nums2[i]);
                    }
                    break;  // 找到后跳出内层循环
                }
            }
        }
        return result;
    }
};
```

### 解法2：遍历 + `unordered_set`

#### 思路分析

1. **遍历**：
   - 同样使用两个嵌套的循环，遍历 `nums2` 中的每个元素，检查是否存在于 `nums1` 中。
   
2. **使用 `unordered_set` 去重**：
   - 使用 `unordered_set` 存储结果，避免重复的元素。
   
3. **将结果从 `unordered_set` 转换为 `vector`**：
   - 最后，将 `unordered_set` 中的元素存入 `vector` 并返回。

#### 参考解答

```cpp
class Solution {
public:
    std::vector<int> intersection(std::vector<int>& nums1, std::vector<int>& nums2) {
        std::unordered_set<int> result{};
        for(int i = 0; i < nums2.size(); i++) {  // 遍历 nums2 中的每个元素
            for(int j = 0; j < nums1.size(); j++) {  // 在 nums1 中查找该元素
                if(nums1[j] == nums2[i]) {
                    result.insert(nums2[i]);  // 使用 unordered_set 自动去重
                    break;  // 找到后跳出内层循环
                }
            }
        }

        // 将 unordered_set 转换为 vector 并返回
        std::vector<int> return_answer{};
        for (auto it = result.begin(); it != result.end(); ++it) {
            return_answer.push_back(*it);
        }

        return return_answer;
    }
};
```

### 2.2 LC645 错误的集合

### 问题描述

集合 `s` 包含从 `1` 到 `n` 的整数。不幸的是，因为数据错误，导致集合里面某一个数字复制了成了集合里面的另外一个数字的值，导致集合丢失了一个数字，并且有一个数字重复 。

给定一个数组 `nums` 代表了集合 `S` 发生错误后的结果。

请你找出重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。


### 解题思路

1. **使用 `unordered_set` 存储出现的数字**：
   - 遍历 `nums`，将数字添加到 `unordered_set` 中。由于 `unordered_set` 不允许重复元素，我们可以在插入时检查是否有重复的数字。
   
2. **计算丢失的数字**：
   - 通过数学公式计算从 `1` 到 `n` 的总和，并减去 `unordered_set` 中的元素和，即可得出丢失的数字。
   
3. **返回结果**：
   - 将找到的重复数字和丢失的数字以数组形式返回。



### 参考解答

```cpp
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        unordered_set<int> arrange{};
        int repeat;
        
        // 找到重复的数字
        for(int c : nums) {
            bool can_insert = arrange.insert(c).second;
            if (!can_insert) {
                repeat = c;
            } 
        }
        
        // 计算 1 到 n 的总和
        int expected_sum = (1 + nums.size()) * nums.size() / 2;
        
        // 计算实际集合中的数字和
        int sum = 0;
        for(int c : arrange) {
            sum += c;
        }
        
        // 计算丢失的数字
        int difference = expected_sum - sum;
        
        // 返回结果
        vector<int> output{repeat, difference};
        return output;
    }
};
```


## 3. 举一反三

### 3.1 LC575 分糖果

#### 问题描述

Alice 有 `n` 枚糖，其中第 `i` 枚糖的类型为 `candyType[i]`。Alice 注意到她的体重正在增长，所以前去拜访了一位医生。

医生建议 Alice 要少摄入糖分，只吃掉她所有糖的 `n / 2` 即可（n 是一个偶数）。Alice 非常喜欢这些糖，她想要在遵循医生建议的情况下，尽可能吃到最多不同种类的糖。

给你一个长度为 `n` 的整数数组 `candyType`。

返回： Alice 在仅吃掉 `n / 2` 枚糖的情况下，可以吃到糖的最多种类数。


### 解题思路

1. **统计糖果的种类**：
   - 使用 `unordered_set` 来存储糖果的不同种类。`unordered_set` 自动去除重复元素，从而可以记录不同类型的糖果。

2. **计算可吃的糖果数量**：
   - 由于 Alice 只能吃掉 `n / 2` 枚糖果，计算糖果的不同种类数量与 `n / 2` 的最小值，即 Alice 最多能吃到的种类数。

3. **返回结果**：
   - 使用 `min` 函数返回 `unordered_set` 中糖果种类的数量与 Alice 能吃掉糖果数量（`n / 2`）的较小值。


### 参考解答
```cpp
#include <vector>
#include <unordered_set>
#include <algorithm>
using namespace std;

class Solution {
public:
    int distributeCandies(vector<int>& candyType) {
        // 使用 unordered_set 来存储糖果的种类
        unordered_set<int> types{};
        
        // 将所有糖果类型插入 unordered_set，自动去重
        for (int c : candyType) {
            types.insert(c);
        }
        
        // 计算 Alice 可以吃的最多种类的糖果
        return min(types.size(), candyType.size() / 2);
    }
};
```
### 解释

1. **存储糖果种类**：通过遍历 `candyType` 数组，将所有糖果类型存储在 `unordered_set` 中，自动去除重复的糖果种类。
   
2. **计算能吃的糖果种类**：
   - `types.size()` 表示糖果的不同种类数。
   - `candyType.size() / 2` 表示 Alice 按照医生建议可以吃的糖果总数。
   
3. **取最小值**：最终返回 `min(types.size(), candyType.size() / 2)`，表示 Alice 能够吃到的最多不同种类的糖果。



### 3.2 LC771 宝石与石头

### 问题描述

给你一个字符串 `jewels` 代表石头中宝石的类型，另有一个字符串 `stones` 代表你拥有的石头。 

`stones` 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。

字母区分大小写，因此 `"a"` 和 `"A"` 是不同类型的石头。


### 解题思路

1. **遍历宝石类型**：
   - 不使用额外的容器，直接遍历字符串 `stones` 中的每个字符，并在 `jewels` 字符串中查找是否存在该字符。
   
2. **统计宝石数量**：
   - 如果在 `jewels` 中找到对应的字符，计数器 `count` 增加。


### 参考解答

```cpp
#include <string>
using namespace std;

class Solution {
public:
    int numJewelsInStones(string jewels, string stones) {
        int count = 0;
        
        // 遍历 stones 中的每个字符，检查是否在 jewels 中
        for (char i : stones) {
            if (jewels.find(i) != string::npos) {  // 如果在 jewels 中找到对应的字符
                count += 1;
            }
        }
        
        return count;  // 返回宝石的数量
    }
};
```

## 4. 课后练习
| 题目编号 | 题目名称                 | 简介                                                     |
| -------- | ------------------------ | -------------------------------------------------------- |
| LC 187   | 重复的 DNA 序列          | 找到所有出现次数超过一次的 DNA 序列。                    |
| LC 961   | N 次重复元素在 2N 数组中 | 在长度为 2N 的数组中找到出现 N 次的元素。                |
| LC 2441  | 存在其负数的最大正整数   | 找到一个正整数，其负数也在数组中存在。                   |
| LC 2357  | 通过减去相同数使数组为零 | 通过减去相同的数使数组中的所有元素变为零的最小操作次数。 |
| LC 217  | 存在重复元素 | 给你一个整数数组nums，如果任一值在数组中出现至少两次，返回true，否则false。 |
