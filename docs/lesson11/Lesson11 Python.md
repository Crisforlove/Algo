# Lesson11 字典专题

## 目录

[1. 字典知识介绍](#1-字典知识介绍) 

   - [1.1 哈希表常用操作](#11-哈希表常用操作)  

   - [1.2 哈希表简单实现](#12-哈希表简单实现)  

   - [1.3 哈希冲突与扩容](#13-哈希冲突与扩容)
     
[2. 频率统计与计数](#2-频率统计与计数)

   - [2.1 词频统计介绍](#21-词频统计介绍)  

   - [2.2 例题讲解](#22-例题讲解)  

      - [2.2.1 LC 242 有效的字母异位词](#221-lc-242-有效的字母异位词)
     
   - [2.3 举一反三](#23-举一反三)  

      - [2.3.1 LC 387 字符串中的第一个唯一字符](#231-lc-387-字符串中的第一个唯一字符)
        
[3. 快速查找](#3-快速查找)

   - [3.1 快速查找介绍](#31-快速查找介绍)  

   - [3.2 例题讲解](#32-例题讲解)  

      - [3.2.1 LC 1 两数之和](#321-lc-1-两数之和)  
     
   - [3.3 举一反三](#33-举一反三)  

      - [3.3.1 LC 217 存在重复元素](#331-lc-217-存在重复元素)
        
[4. 哈希映射](#4-哈希映射)  

   - [4.1 哈希映射介绍](#41-哈希映射介绍)  

   - [4.2 例题讲解](#42-例题讲解)  

      - [4.2.1 LC 697 数组的度](#421-lc-697-数组的度)  
     
   - [4.3 举一反三](#43-举一反三)  

      - [4.3.1 LC 205 同构字符串](#431-lc-205-同构字符串)  
     
      - [4.3.2 LC 219 存在重复元素II](#432-lc-219-存在重复元素ii)
        
[5. 课后练习](#5-课后练习)


## 1 字典知识介绍

字典是Python中的一个强大工具。它不仅能以键值对的形式高效存储数据，还能在许多常见算法问题中显著提升性能，而Python中的字典又是通过哈希表来实现的。哈希表（hash table），又称散列表，它通过建立键 `key` 与值 `value` 之间的映射，实现高效的元素查询。具体而言，我们向哈希表中输入一个键 `key` ，则可以在 O(1) 时间内获取对应的值 `value` 。

给定 n 个学生，每个学生都有“姓名”和“学号”两项数据。假如我们希望实现“输入一个学号，返回对应的姓名”的查询功能，则可以采用下图所示的哈希表来实现。

![哈希表的抽象表示](https://www.hello-algo.com/chapter_hashing/hash_map.assets/hash_table_lookup.png)

### 1.1  哈希表常用操作

哈希表的常见操作包括：初始化、查询操作、添加键值对和删除键值对等，示例代码如下：

```python
# 初始化哈希表
hmap = {}

# 添加操作
# 在哈希表中添加键值对 (key, value)
hmap[12836] = "小哈"
hmap[15937] = "小啰"
hmap[16750] = "小算"
hmap[13276] = "小法"
hmap[10583] = "小鸭"

print(hmap)
# 查询操作
# 向哈希表中输入键 key ，得到值 value
name = hmap[15937]
print(name)

# 删除操作
# 在哈希表中删除键值对 (key, value)
hmap.pop(10583)
print(hmap)

#修改操作
hmap[10583] = "小鹅"
print(hmap)
```

输出：

```
{12836: '小哈', 15937: '小啰', 16750: '小算', 13276: '小法', 10583: '小鸭'}
小啰
{12836: '小哈', 15937: '小啰', 16750: '小算', 13276: '小法'}
{12836: '小哈', 15937: '小啰', 16750: '小算', 13276: '小法', 10583: '小鹅'}
```

哈希表有三种常用的遍历方式：遍历键值对、遍历键和遍历值。示例代码如下：

```python
# 初始化哈希表
hmap = {}

# 添加操作
# 在哈希表中添加键值对 (key, value)
hmap[12836] = "小哈"
hmap[15937] = "小啰"
hmap[16750] = "小算"
hmap[13276] = "小法"
hmap[10583] = "小鸭"

# 遍历哈希表
# 遍历键值对 key->value
for key, value in hmap.items():
    print(key, "->", value)
# 单独遍历键 key
for key in hmap.keys():
    print(key)
# 单独遍历值 value
for value in hmap.values():
    print(value)
```

输出：

```
12836 -> 小哈
15937 -> 小啰
16750 -> 小算
13276 -> 小法
10583 -> 小鸭
12836
15937
16750
13276
10583
小哈
小啰
小算
小法
小鸭
```

### 1.2 哈希表简单实现

我们先考虑最简单的情况，**仅用一个数组来实现哈希表**。在哈希表中，我们将数组中的每个空位称为桶（bucket），每个桶可存储一个键值对。因此，查询操作就是找到 `key` 对应的桶，并在桶中获取 `value` 。

那么，如何基于 `key` 定位对应的桶呢？这是通过哈希函数（hash function）实现的。哈希函数的作用是将一个较大的输入空间映射到一个较小的输出空间。在哈希表中，输入空间是所有 `key` ，输出空间是所有桶（数组索引）。换句话说，输入一个 `key` ，**我们可以通过哈希函数得到该 `key` 对应的键值对在数组中的存储位置**。

输入一个 `key` ，哈希函数的计算过程分为以下两步。

1. 通过某种哈希算法 `hash()` 计算得到哈希值。

2. 将哈希值对桶数量（数组长度）`capacity` 取模，从而获取该 `key` 对应的数组索引 `index`。

```
index = hash(key) % capacity
```

   随后，我们就可以利用 `index` 在哈希表中访问对应的桶，从而获取 `value` 。

   设数组长度 `capacity = 100`、哈希算法 `hash(key) = key` ，易得哈希函数为 `key % 100` 。下图以 `key` 学号和 `value` 姓名为例，展示了哈希函数的工作原理。

   ![哈希函数工作原理](https://www.hello-algo.com/chapter_hashing/hash_map.assets/hash_function.png)

   

### 1.3 哈希冲突与扩容

从本质上看，哈希函数的作用是将所有 `key` 构成的输入空间映射到数组所有索引构成的输出空间，而输入空间往往远大于输出空间。因此，**理论上一定存在“多个输入对应相同输出”的情况**。

对于上述示例中的哈希函数，当输入的 `key` 后两位相同时，哈希函数的输出结果也相同。例如，查询学号为 12836 和 20336 的两个学生时，我们得到：

```
12836 % 100 = 36
20336 % 100 = 36
```

如下图所示，两个学号指向了同一个姓名，这显然是不对的。我们将这种多个输入对应同一输出的情况称为哈希冲突（hash collision）。

![哈希冲突示例](https://www.hello-algo.com/chapter_hashing/hash_map.assets/hash_collision.png)

**如果出现哈希冲突了，只是会降低查找的性能，因为同一个哈希值对应的桶当中，还会以链表的形式存储多个值，如果发现哈希冲突，就会沿着链表查找，因为是遍历，所以性能会降低。**

![链地址法](https://camo.githubusercontent.com/0047c9c8ab9b85a19c9ffd4c9e72760215457bec54bd7ff0a935a48220d51da3/68747470733a2f2f7163646e2e69746368617267652e636e2f696d616765732f3230323430353039323331393332372e706e67)

容易想到，哈希表容量 n 越大，多个 `key` 被分配到同一个桶中的概率就越低，冲突就越少。因此，**我们可以通过扩容哈希表来减少哈希冲突**。

如下图所示，扩容前键值对 `(136, A)` 和 `(236, D)` 发生冲突，扩容后冲突消失。![哈希表扩容](https://www.hello-algo.com/chapter_hashing/hash_map.assets/hash_table_reshash.png)

类似于数组扩容，哈希表扩容需将所有键值对从原哈希表迁移至新哈希表，非常耗时；并且由于哈希表容量 `capacity` 改变，我们需要通过哈希函数来重新计算所有键值对的存储位置，这进一步增加了扩容过程的计算开销。为此，编程语言通常会预留足够大的哈希表容量，防止频繁扩容。

## 2 频率统计与计数

### 2.1 词频统计介绍

字典最常见的用途之一是**频率统计**，即用来统计数据出现的次数或频率。在需要处理大量数据时，字典可以通过键值对快速记录每个元素的出现次数。这样的操作时间复杂度为 O(1)，因此相比于使用列表的 O(n) 查找，性能大幅提升。

词频统计是哈希映射的一种特殊应用，重点在于将一个值（如字符、数字等）映射到其出现次数上。它狭义地定义了键值对中的“值”是该键出现的频率，常用于统计数据集中的元素频率。词频统计通常用于字符统计、元素频率统计等。

**简单来说，词频统计是一种特定的哈希映射，狭义地将键值对定义为“元素: 出现频率”，用于频率统计问题中。**

例如，在字符串中统计每个字符的出现频率时，字典的键是字符，值是该字符的出现次数。

#### 常见应用：

- 查找出现次数最多的元素
- 判断数据集中是否存在重复元素
- 统计每个字符/数字/元素的频率

```python
# 统计字符频率
def count_frequency(s):
    freq_dict = {}
    for char in s:
        if char in freq_dict:
            freq_dict[char] += 1
        else:
            freq_dict[char] = 1
    return freq_dict
```

### 2.2 例题讲解

### 2.2.1 LC 242 有效的字母异位词

#### 问题描述

**描述**：给定两个字符串s和t。

**要求**：判断t和s是否使用了相同的字符构成（字符出现的种类和数目都相同）。

#### 思路分析

1.如果字符长度不相同，直接返回False；

2.使用字典统计每个字符出现的次数，比较两个字符串中每个字符的频率是否相等。

#### 提示

创建两个字典储存频率次数，进行比较。

#### 参考解答

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        count_s, count_t = {}, {}
        for i in range(len(s)):
            count_s[s[i]] = count_s.get(s[i], 0) + 1
            count_t[t[i]] = count_t.get(t[i], 0) + 1
        return count_s == count_t
```



### 2.3 举一反三

### 2.3.1 LC 387 字符串中的第一个唯一数字

#### 问题描述

给定一个字符串 `s` ，找到 *它的第一个不重复的字符，并返回它的索引* 。如果不存在，则返回 `-1` 。

#### 思路分析

这道题目要求我们找到一个字符串中第一个不重复的字符。最简单的办法是使用**两次遍历**。第一次遍历字符串时，使用**字典**记录每个字符出现的次数。第二次遍历时，检查哪个字符的出现次数是1，第一个满足条件的字符就是我们要找的，返回它的索引。如果没有找到这样的字符，就返回 `-1`。

#### 提示

两次遍历字符串的方法很常用。第一次用来统计每个字符出现的次数，第二次用来找出第一个不重复的字符。

使用字典可以方便地记录每个字符的出现次数。

#### 参考示例

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        count = dict()
        for i in range(len(s)):
            if s[i] in count:
                count[s[i]] += 1  # 如果字符已经在字典中，频率加1
            else:
                count[s[i]] = 1  # 如果字符不在字典中，初始化为1
        for k, v in count.items():
            if v == 1:
                return s.index(k)
        return -1
```



## 3 快速查找

### 3.1 快速查找介绍

快速查找是通过哈希表实现的，它利用哈希函数的性质在常数时间内完成查找任务。其核心在于高效性——相比于列表遍历的 O(n)时间复杂度，字典通过哈希查找可以在 O(1) 时间内找到对应的值。快速查找并不关心具体的映射关系，而是着重强调查找速度的提升。

**简单来说，快速查找是字典利用哈希表实现的高效查找操作，强调时间复杂度为 O(1)，适用于在数据集中快速定位特定元素。**

例如，通过给定学生学号，查找对应的学生姓名时，字典通过哈希表可以快速返回查询结果。

```python
# 创建字典，存储学号和姓名
students = {
    1001: "Alice",
    1002: "Bob",
    1003: "Charlie"
}

# 根据学号快速查找对应的学生姓名
student_id = 1002
print(students[student_id])  # 输出：Bob
```

### 3.2例题讲解

### 3.2.1 LC 1 两数之和

#### 问题描述

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案，并且你不能使用两次相同的元素。

你可以按任意顺序返回答案。

#### 思路分析

遍历数组，对于每一个数nums[i]：

1. 查找字典中书否存在target-nums[i]，存在则输出target-nums[i]对应的下标和当前数组的下标 i。
2. 不存在则在字典中存入target-nums[i]的下标i。

#### 提示

属于字典中的快速查找。

#### 参考解答：

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashtable = dict()
        for i, num in enumerate(nums):
            if target - num in hashtable:
                return [hashtable[target - num], i]
            hashtable[nums[i]] = i
        return []
```

### 3.3 举一反三

###  3.3.1 LC 217 存在重复元素

#### 问题描述

给你一个整数数组 `nums` 。如果任一值在数组中出现 **至少两次** ，返回 `true` ；如果数组中每个元素互不相同，返回 `false` 。

#### 思路分析

这道题目要求判断一个数组里有没有重复的数字。我们可以使用一个**字典**来存储每个数字是否已经出现过。当我们遍历数组时，每遇到一个数字，就检查它是否已经存在于字典中。如果已经存在，说明这个数字重复了，直接返回 `true`；如果没有，就把这个数字加到字典里，继续检查下一个数字。遍历完数组后，如果没有找到任何重复数字，就返回 `false`。

这样做的好处是每个数字只会检查一次，并且查找和存储数字的操作也很快，因此整个过程很高效。

#### 提示

字典可以用来快速存储和查找数字，这样可以避免重复的数字，属于频率统计与计数。

#### 参考解答

```python
class Solution(object):
    def containsDuplicate(self, nums):
        seen = {}
        for num in nums:
            if num in seen:
                return True
            seen[num] = True
        return False
```

## 4 哈希映射

### 4.1 哈希映射介绍

哈希映射是一个更广泛的概念，表示通过哈希函数将一个键（key）映射到一个值（value），这种键值对可以用于构建各种关系，不仅限于频率统计或快速查找。例如，将人名映射到学校，或者将学校映射到一个包含所有学生的人名列表，都是哈希映射的应用。哈希映射可以支持一对一、一对多等复杂的关系结构。

**简单来说，哈希映射是广泛使用的映射机制，能够灵活实现键值对关系，应用于更多复杂场景，如一对一、一对多的映射。**

例如，将人名与学校关联，或将学校与其所有学生关联，都可以通过哈希映射来实现。

```python
# 人名到学校的一对一映射
people_to_school = {
    "Alice": "Harvard",
    "Bob": "MIT"
}

# 学校到人名列表的一对多映射
school_to_people = {
    "Harvard": ["Alice", "Charlie"],
    "MIT": ["Bob"]
}
```

### 4.2 例题讲解

### 4.2.1 LC 697 数组的度

#### 问题描述

给定一个非空且只包含非负数的整数数组 `nums`，数组的 **度** 的定义是指数组里任一元素出现频数的最大值。

你的任务是在 `nums` 中找到与 `nums` 拥有相同大小的度的最短连续子数组，返回其长度。

#### 思路分析

记原数组中出现次数最多的数为 x，那么和原数组的度相同的最短连续子数组，必然包含了原数组中的全部 x，且两端恰为 x 第一次出现和最后一次出现的位置。

因为符合条件的 x 可能有多个，即多个不同的数在原数组中出现次数相同。所以为了找到这个子数组，我们需要统计每一个数出现的次数，同时还需要统计每一个数第一次出现和最后一次出现的位置。

在实际代码中，我们使用哈希表实现该功能，每一个数映射到一个长度为 3 的数组，数组中的三个元素分别代表这个数出现的次数、这个数在原数组中第一次出现的位置和这个数在原数组中最后一次出现的位置。当我们记录完所有信息后，我们需要遍历该哈希表，找到元素出现次数最多，且前后位置差最小的数。

#### 提示

1.先记录每个元素出现的次数，第一次和最后一次的索引

2.找到数组的度和最短子数组的长度

#### 参考解答

```python
class Solution:
    def findShortestSubArray(self, nums: List[int]) -> int:
        mp = dict()

        for i, num in enumerate(nums):
            if num in mp:
                mp[num][0] += 1
                mp[num][2] = i
            else:
                mp[num] = [1, i, i]
        
        maxNum = minLen = 0
        for count, left, right in mp.values():
            if maxNum < count:
                maxNum = count
                minLen = right - left + 1
            elif maxNum == count:
                if minLen > (span := right - left + 1):
                    minLen = span
        
        return minLen
```

#### 解题过程：

1. 初始化字典mp

2. 遍历数组nums，记录出现次数，第一次出现的索引，最后一次出现的索引

3. 遍历字典 `mp` 的值，提取每个数字的出现次数、第一次和最后一次出现的位置。

   - `maxNum` 记录当前出现次数最多的值（即数组的度）。

   - `minLen` 记录具有相同度的子数组的最短长度。

   - 如果当前元素的出现次数大于 `maxNum`，更新 `maxNum` 和最短子数组长度 `minLen`。

   - 如果出现次数相同，检查当前子数组是否比之前的短，并更新 `minLen`。

### 4.3 举一反三

### 4.3.1 LC 205 同构字符串

#### 问题描述

给定两个字符串 `s` 和 `t` ，判断它们是否是同构的。

如果 `s` 中的字符可以按某种映射关系替换得到 `t` ，那么这两个字符串是同构的。

每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。

#### 思路分析

根据题目意思，字符串 *s* 和 *t* 每个位置上的字符是一一对应的。*s* 的每个字符都与 *t* 对应位置上的字符对应。可以考虑用哈希表来存储 s[i]:t[i]的对应关系。但是这样只能保证对应位置上的字符是对应的，但不能保证是唯一对应的。所以还需要另一个哈希表来存储 t[i]:s[i]的对应关系来判断是否是唯一对应的。

#### 提示

属于建立映射，通过创建字典建立字母和出现字母的映射关系。

#### 参考解答

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        s_dict = dict()
        t_dict = dict()
        for i in range(len(s)):
            if s[i] in s_dict and s_dict[s[i]] != t[i]:
                return False
            if t[i] in t_dict and t_dict[t[i]] != s[i]:
                return False
            s_dict[s[i]] = t[i]
            t_dict[t[i]] = s[i]
        return True
```

### 4.3.2 LC 219 存在重复元素II

#### 问题描述

给你一个整数数组 `nums` 和一个整数 `k` ，判断数组中是否存在两个 **不同的索引** `i` 和 `j` ，满足 `nums[i] == nums[j]` 且 `abs(i - j) <= k` 。如果存在，返回 `true` ；否则，返回 `false` 。

#### 思路分析

这道题目是 `LC 217` 的扩展版，不仅要判断是否有重复元素，还要求这些重复元素的索引之差不超过给定的数字 `k`。我们可以继续使用**字典**，记录每个数字的**最后一次出现位置**。当我们遇到一个数字时，先检查字典中是否有它。如果有，还要检查它之前出现的位置和当前的位置之差是否小于等于 `k`。如果满足条件，就返回 `true`；如果不满足条件，就更新它在字典中的位置。遍历完数组后，如果没有找到符合条件的数字，返回 `false`。

#### 提示

我们需要在字典中记录数字的出现位置，而不是单纯地记录它是否出现过。

要小心处理索引之间的距离，确保两个相同的数字之间的索引差小于等于 `k`。

#### 参考解答

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        pos = {}
        for i,num in enumerate(nums):
            if num in pos and i - pos[num] <= k:
                return True
            pos[num] = i
        return False
```

## 5 课后练习
#### 频率统计

| 题目编号 | 题目名称                   | 题目描述                                             |
| -------- | -------------------------- | ---------------------------------------------------- |
| LC 451   | 根据字符出现频率排序       | 给定一个字符串，请将字符按出现频率排序。             |
| LC 692   | 前K个高频单词              | 给定一个单词列表，返回前 K 个出现频率最高的单词。    |
| LC 347   | 前K个高频元素              | 给定一个整数数组，返回出现频率前 K 高的元素          |
| LC 554   | 砌墙                       | 计算通过一堵墙的垂直线段穿过的砖块数量最少的地方。   |
| LC 2085  | 统计出现过一次的公共字符串 | 返回在两个字符串数组中都恰好出现一次的字符串的数目。 |



#### 快速查找

| 题目编号 | 题目名称       | 题目描述                                             |
| -------- | -------------- | ---------------------------------------------------- |
| LC 594   | 最长和谐子序列 | 找到和谐子序列的最长长度，最大值和最小值相差为1。    |
| LC 525   | 连续数组       | 给定一个二进制数组，找到长度相同的0和1的最长子数组。 |
| LC 49    | 字母异位词分组 | 给定一个字符串数组，将字母异位词组合在一起。         |
| LC 169   | 多数元素       | 给定一个大小为n的数组nums，返回其中的多数元素。      |
| LC 409   | 最长回文串     | 给定一个字符串，返回其中可以构成的最长回文串的长度。 |



#### 哈希映射

| 题目编号 | 题目名称             | 题目描述                                                     |
| -------- | -------------------- | ------------------------------------------------------------ |
| LC 290   | 单词规律             | 给定一种规律 pattern 和一个字符串 s ，判断 s 是否遵循相同的规律。 |
| LC 560   | 和为K的子数组        | 找出数组中和为 `k` 的连续子数组的个数。                      |
| LC 249   | 移位字符串分组 | 给定一个包含仅小写字母字符串的列表，将该列表中所有满足 “移位” 操作规律的组合进行分组并返回。                  |
| LC 953   | 验证外星语词典       | 给定一个外星词典的顺序表，判断一组单词是否按照这个外星词典的顺序排列。 |
| LC 12    | 整数转罗马数字       | 给定一个整数，将其转换为罗马数字。                           |
