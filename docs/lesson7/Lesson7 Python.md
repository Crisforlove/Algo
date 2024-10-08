# Lesson 7 Ascii 转换与进制转换

## 目录
1. [理解 ASCII](#1-理解-ascii)
    - [1.1 什么是 ASCII](#11-什么是-ascii)
    - [1.2 ASCII 的应用](#12-ascii-的应用)
    - [1.3 ASCII 例题讲解](#13-ascii例题讲解)
        - [1.3.1 LC1309 - 解码字母到整数映射](#131-lc1309-解码字母到整数映射)
    - [1.4 ASCII 举一反三](#14-ascii-举一反三)
        - [1.4.1 LC387 - 字符串中的第一个唯一字符](#141-lc387-字符串中的第一个唯一字符-)
        - [1.4.2 LC171 - Excel 表列序号](#142-lc171-excel表列序号)
        - [1.4.3 LC804 - 唯一摩斯密码词](#143-lc804-唯一摩斯密码词)

2. [进制转换](#2-进制转换)
    - [2.1 数字进制概述](#21-数字进制概述)
    - [2.2 十进制到二进制的转换](#22-十进制到二进制的转换)
    - [2.3 二进制到十进制的转换](#23-二进制到十进制的转换)
    - [2.4 十进制到十六进制的转换](#24-十进制到十六进制的转换)
    - [2.5 二进制到十六进制的转换](#25-二进制到十六进制的转换)
    - [2.6 进制 例题讲解](#26-进制例题讲解)
        - [2.6.1 LC504 - 七进制数](#261-lc504-七进制数)
    - [2.7 进制 举一反三](#27-进制举一反三)
        - [2.7.1 LC168 - Excel 表列名称](#271-lc168-excel表列名称)
        - [2.7.2 LC728 - 自除数](#272-lc728-自除数)
        - [2.7.3 LC693 - 交替位二进制数](#273-lc693-交替位二进制数)

3. [课后练习](#3-课后练习)

在本课中，我们将探讨字符如何通过 ASCII 值存储和处理，并学习如何在不同的进制（如二进制、八进制、十进制和十六进制）之间进行转换。

## 1. 理解 ASCII

### 1.1 什么是 ASCII？

ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）是一种字符编码标准，它使用数值来表示字符。每个字符（如字母、数字、符号等）都有一个唯一的 ASCII 代码，通常范围从 0 到 127。
这些值可以用于字符与数字之间的转换。例如，将字符 '0' 到 '9' 转换为对应的整数，或反向操作。

### 示例 ASCII 表

| 字符        | ASCII 值 | 二进制   | 十六进制 |
| ----------- | -------- | -------- | -------- |
| 'A'         | 65       | 01000001 | 0x41     |
| 'a'         | 97       | 01100001 | 0x61     |
| '0'         | 48       | 00110000 | 0x30     |
| ' '（空格） | 32       | 00100000 | 0x20     |

完整ASCII表格：https://www.ascii-code.com/ 

### 1.2 ASCII 的应用

在 Python 中，每个字符都以其对应的 ASCII 值形式存储为整数。因此我们可以通过将字符视为整数来轻松地操作它们。

通过ASCII值，我们可以对字符进行加减运算，甚至是转换。

#### 使用+ord(‘0’)和-ord(‘0’)进行转换

##### `-ord('0')`：字符到整数的转换

通过将字符减去`ord('0')`，可以得到对应的整数值。比如`ord('3')`-`ord('0')`的结果是`3`。

**示例：字符到整数的转换**

```python
digit = '5'  # '5' 的 ASCII 值是 53
num = ord(digit) - ord('0')  # '5' - '0' = 5
print(f"字符 {digit} 转换为整数是 {num}")
```

输出：

```
字符 5 转换为整数是 5
```

##### `+ord('0')`：整数到字符的转换

通过将整数加上`ord('0')`，可以得到对应的字符。比如`5`+`ord('0')`的结果是字符`'5'`。

**示例：整数到字符的转换**

```python
num = 7
digit = chr(num + ord('0'))  # 7 + '0' = '7'
print(f"整数 {num} 转换为字符是 {digit}")
```

输出：

```
整数 7 转换为字符是 7
```

#### 使用+ord(‘A’)和-ord(‘A’)进行转换

通过在字符上加上或减去字符`ord('A')`，我们可以将字符与字母表的位置关联起来。例如，将字符`'C'`减去`'A'`可以得到`'C'`在字母表中的位置（从0开始计数）。这对于实现简单的字母编码或解码非常有用。

##### `-ord('A')`：字符到字母表位置的转换

通过将字符减去`ord('A')`，可以得到字符在字母表中的位置（从0开始）。比如`ord('C')`-`ord('A')`的结果是`2`。

**示例：字符到字母表位置的转换**

```python
letter = 'C'  # 'C' 的 ASCII 值是 67
position = ord(letter) - ord('A')  # 'C' - 'A' = 2
print(f"字符 {letter} 在字母表中的位置是 {position}")
```

输出：

```
字符 C 在字母表中的位置是 2
```

##### `+ord('A')`：字母表位置到字符的转换

通过将字母表中的位置加上`ord('A')`，可以得到对应的字符。比如`2`+`ord('A')`的结果是字符`'C'`。

**示例：字母表位置到字符的转换**

```python
position = 2
letter = chr(position + ord('A'))  # 2 + 'A' = 'C'
print(f"字母表中位置 {position} 对应的字符是 {letter}")
```

输出：

```
字母表中位置 2 对应的字符是 C
```

### 综合运用 +ord(‘0’)和 -ord(‘0’)以及+ord(‘A’)和-ord(‘A’)

通过结合使用这些操作符，我们可以灵活地在字符、数字和字母表位置之间进行转换。例如，可以编写一个程序，将字符串中的每个数字字符转换为整数，然后进行简单的运算，再将结果转换回字符；或者将字母字符转换为在字母表中的位置，并进行一些加密操作。

**示例：处理字符串中的数字和字母**

```python
str_input = "A3C7"
sum_num = 0

for ch in str_input:
    if '0' <= ch <= '9':
        sum_num += (ord(ch) - ord('0'))  # 将数字字符转换为整数并求和
    elif 'A' <= ch <= 'Z':
        pos = ord(ch) - ord('A')  # 将字母字符转换为字母表位置
        print(f"{ch} 在字母表中的位置是: {pos}")

print(f"字符串 {str_input} 中数字字符的和是: {sum_num}")
```

输出：

```
A 在字母表中的位置是: 0
C 在字母表中的位置是: 2
字符串 A3C7 中数字字符的和是: 10
```

### 1.3 ASCII例题讲解

### 1.3.1 LC1309: 解码字母到整数映射

#### 题目描述：

给定一个加密字符串`s`，它由数字`'0'`到`'9'`、`'#'`和字母组成。我们按照下述规则解码：

1. 字符（`'1'`-`'9'`）表示映射到小写字母（`'a'`-`'i'`）。
2. 字符（`'10#'`-`'26#'`）表示映射到小写字母（`'j'`-`'z'`）。
   返回字符串`s`解码后的结果。
   **注意：**

- 输入只包含数字、字符`'#'`和小写字母。
- 字符串的长度范围是`[1, 1000]`。

#### 示例：

```
输入：s = "10#11#12"
输出："jkab"
```



#### 提示

1. 准备一个列表`mapping`来存储字母`a`到`z`的映射。
2. 遍历字符串`s`：
   - 如果当前字符是数字且后面有`'#'`，就将当前的数字和下一个数字拼接成两位数字，然后将其转换为字母。
   - 如果当前字符是单独的数字，则直接转换为字母。
3. 构建解密后的字符串。

#### 参考答案

```python
class Solution:
    def freqAlphabets(self, s: str) -> str:
        # 用一个列表存储字母 a-z 的映射
        mapping = [chr(i + ord('a')) for i in range(26)]

        result = []
        n = len(s)

        i = 0
        while i < n:
            if i + 2 < n and s[i + 2] == '#':  # 检查是否是 '10#' 到 '26#'
                num = int(s[i:i + 2])  # 计算两位数
                result.append(mapping[num - 1])  # 将其映射为字母
                i += 3  # 跳过数字和 '#'
            else:  # 单个数字 '1' 到 '9'
                num = int(s[i])  # 转换成数字
                result.append(mapping[num - 1])  # 映射为字母
                i += 1

        return ''.join(result)  # 将列表转换为字符串
```

1. **构建映射表**：mapping = [chr(i + ord('a')) for i in range(26)]创建一个名为`mapping`的列表，它包含了从`'a'`到`'z'`的所有小写英文字母。这是通过列表推导式和`chr`函数实现的，`ord('a')`返回字符`'a'`的ASCII值，然后`chr(i + ord('a'))`返回从`'a'`开始的第`i`个字母。
2. **遍历字符串**：循环遍历加密字符串`s`。
   - 如果当前字符后面两个字符构成一个有效的`"#"`序列，提取该序列，计算对应的数字并映射为字母。
   - 如果是单个数字，则直接映射为相应的字母。
3. **结果构建**：将解密后的字符拼接到结果字符串中。

### 1.4 ASCII举一反三

### 1.4.1 LC387. 字符串中的第一个唯一字符 

#### 问题描述

给定一个字符串`s`，找到第一个不重复出现的字符，并返回它的索引。如果不存在，则返回`-1`。

#### 思路分析

通过 **列表** 来实现字符频率统计。我们可以使用一个大小为 26 的列表来存储每个字母出现的次数。

具体步骤如下：

1. **字符频率统计**：使用一个大小为 26 的列表来统计每个字母的出现次数。通过`ord(s[i]) - ord('a')`可以确定字母在列表中的索引位置。
2. **遍历字符串**：先遍历一次字符串，统计每个字符的出现次数。
3. **找到第一个唯一字符**：再次遍历字符串，根据统计结果找到第一个出现次数为 1 的字符。

#### 参考解答

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        # 定义大小为26的列表，记录每个字符出现的次数
        count = [0] * 26

        # 第一次遍历：统计每个字符的频率
        for char in s:
            count[ord(char) - ord('a')] += 1

        # 第二次遍历：找到第一个出现次数为1的字符
        for i, char in enumerate(s):
            if count[ord(char) - ord('a')] == 1:
                return i  # 返回第一个不重复字符的索引

        return -1  # 没有找到不重复的字符，返回-1
```

#### 代码讲解

1. **`count = [0] * 26`**：初始化一个长度为26的列表`count`，用于记录小写英文字母每个字符出现的次数。列表中的每个元素都初始化为0。
2. **第一次遍历字符串**：在第一次遍历中，使用`ord(char) - ord('a')`计算它的索引（其中`'a'`是字母表中的起始字母），然后在`count`列表中对应的索引位置增加1，以此来统计每个字符出现的次数。
3. **第二次遍历字符串**：通过第二次遍历字符串，找出第一个出现次数为 1 的字符，并返回该字符的索引。
4. **返回结果**：如果没有找到唯一字符，则返回`-1`。

### 1.4.2 LC171. Excel表列序号

#### 问题描述

给定一个字符串`columnTitle`，表示 Excel 表格中的列名。请将其转换为对应的列序号。

例如：

```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```

#### 思路分析

通过 **进制转换** 的方法，将 Excel 列名看作一个以 26 为基数的数字系统，每个字母代表一个数字。`A` 到`Z` 分别代表 1 到 26，我们需要将列名转换成相应的数字。

具体步骤如下：

1. **字符转换为数字**：每个字符从`A` 到`Z` 对应的值为`1` 到`26`，可以通过`columnTitle[i] - ord('A') + 1` 得到其对应的数值。
2. **进制转换**：将列名看作是 26 进制数，从右到左遍历字符串，将每个字符转换成数字并乘以 26 的幂次累加到结果中。
3. **返回结果**：最终的累加结果即为 Excel 表格列名对应的列序号。

```python
class Solution:
    def titleToNumber(self, columnTitle: str) -> int:
        result = 0
        pow_num = 0
        
        # 从右到左遍历列名
        for i in range(len(columnTitle) - 1, -1, -1):
            # 将字符转换为对应的数值
            extract_char = ord(columnTitle[i]) - ord('A') + 1
            
            # 计算 26 的幂次，并累加到结果中
            result += extract_char * (26 ** pow_num)
            pow_num += 1
        
        return result
```

#### 代码讲解

1. **`extract_char = ord(columnTitle[i]) - ord('A') + 1`**：将字母`A-Z` 转换为对应的 1-26 数字。
2. **进制转换**：每个字符的位置对应 26 的幂次，最右边的字符乘以`26^0`，第二个字符乘以`26^1`，依次类推。
3. **`result += extract_char * (26 ** pow_num)`**：将每个字符对应的值乘以 26 的幂次，并累加到结果中。
4. **返回结果**：最终结果是列名对应的列序号。

### 1.4.3 LC804. 唯一摩斯密码词

#### 问题描述

给定一个字符串数组`words`，其中每个单词由小写字母组成。每个字母可以用摩斯密码表示，例如：

- 'a' -> ".-"
- 'b' -> "-..."
- 'c' -> "-.-."
- ...

你需要将每个单词转换为摩斯密码表示，并返回唯一摩斯密码词的个数。

#### 思路分析

1. **摩斯密码映射**：每个字母对应一个固定的摩斯密码，可以用数组来表示每个字母的摩斯密码。
2. **逐字转换**：遍历每个单词，将其转换为摩斯密码组合。
3. **唯一性检查**：通过向量存储已转换的摩斯密码，并检查每个转换是否是唯一的。
4. **返回结果**：最终返回唯一摩斯密码的数量。

#### 参考解答

```python
class Solution:
    def uniqueMorseRepresentations(self, words: list[str]) -> int:
        # 用数组来存储字母到摩斯密码的映射
        morse_code = [".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", 
                      "..", ".---", "-.-", ".-..", "--", "-.", "---", ".--.", 
                      "--.-", ".-.", "...", "-", "..-", "...-", ".--", "-..-", 
                      "-.--", "--.."]
        
        # 使用集合来存储唯一的摩斯密码表示
        result = set()
        
        # 遍历每个单词
        for word in words:
            combination = ""
            
            # 将单词转换为摩斯密码表示
            for char in word:
                combination += morse_code[ord(char) - ord('a')]  # 通过 'a' 的 ASCII 值找到对应的摩斯密码
            
            # 将唯一的摩斯密码表示加入集合
            result.add(combination)
        
        return len(result)
```

#### 代码讲解

1. **摩斯密码映射**：用长度为 26 的数组`morse_code` 来存储字母 'a' 到 'z' 对应的摩斯密码表示。
2. **单词转换**：通过遍历单词的每个字符，根据字符的 ASCII 值找到对应的摩斯密码并将其组合起来。
3. **检查唯一性**：通过集合set（）的方式确保当前摩斯密码组合在`result`中的唯一性。
4. **返回结果**：返回存储唯一摩斯密码组合的向量`result`的大小，即唯一摩斯密码的数量。

## 2. 进制转换

### 2.1 数字进制概述

- **二进制（Base 2）：** 使用数字 0 和 1。例如：`1010`（二进制） =`10`（十进制）。

- **八进制（Base 8）：** 使用数字 0 到 7。例如：`12`（八进制） =`10`（十进制）。

- **十进制（Base 10）：** 标准数字系统。例如：`10`（十进制）。

- **十六进制（Base 16）：** 使用数字 0-9 和字母 A-F。例如：`A`（十六进制）=`10`（十进制）。

  以下表格展示了十进制数字从1到10的二进制、八进制和十六进制表示:

  | 十进制 (Decimal) | 二进制 (Binary) | 八进制 (Octal) | 十六进制 (Hexadecimal) |
  | ---------------- | --------------- | -------------- | ---------------------- |
  | 1                | 1               | 1              | 1                      |
  | 2                | 10              | 2              | 2                      |
  | 3                | 11              | 3              | 3                      |
  | 4                | 100             | 4              | 4                      |
  | 5                | 101             | 5              | 5                      |
  | 6                | 110             | 6              | 6                      |
  | 7                | 111             | 7              | 7                      |
  | 8                | 1000            | 10             | 8                      |
  | 9                | 1001            | 11             | 9                      |
  | 10               | 1010            | 12             | A                      |


### 2.2 十进制到二进制的转换

#### 手动方法：使用短除法

- 将十进制数除以 2。
- 记录余数。
- 用商继续除以 2，直到商为 0。
- 二进制数即为逆序读取的余数序列。

#### 示例：将 13 转换为二进制

```
13 / 2 = 6 余 1
6 / 2 = 3 余 0
3 / 2 = 1 余 1
1 / 2 = 0 余 1
```

结果：`13 (十进制) = 1101 (二进制)`

### 用 Python实现十进制到二进制的转换

```python
def decimal_to_binary(num):
    ans = ""
    while num > 0:
        ans += str(num % 2)
        num = num // 2
    return ans[::-1]  # 逆序输出

num = int(input("Enter a number: "))
binary_representation = decimal_to_binary(num)
print(binary_representation)
```

代码解释：

- ans += str(num % 2)：使用`num % 2`计算当前位的二进制值（0 或 1），并将其转换为字符串，添加到`ans`字符串的末尾。
- num = num // 2：使用整数除法`//`更新`num`为当前的商，以便在下一次迭代中继续计算下一个二进制位。
- return ans[::-1]：由于计算得到的二进制位是逆序的（最低位在前，最高位在后），使用切片`[::-1]`将字符串逆序，以得到正确的二进制表示。

### 2.3 二进制到十进制的转换

#### 手动方法：

- 将每个二进制位乘以 2 的相应次方（从右往左，位置从 0 开始）。
- 将所有结果相加。

#### 示例：将 1101 转换为十进制

```
1 * 2^3 + 1 * 2^2 + 0 * 2^1 + 1 * 2^0 = 8 + 4 + 0 + 1 = 13
```

结果：`1101 (二进制) = 13 (十进制)`

### 用 Python实现二进制到十进制的转换

```python
def binary_to_decimal(binary_str):
    ans = 0
    for char in binary_str:
        ans = ans * 2 + int(char)
    return ans

binary_str = input("Enter a number with base of 2: ")
decimal_value = binary_to_decimal(binary_str)
print(decimal_value)
```

- ans = ans * 2 + int(char)：在每次迭代中，将当前结果`ans`乘以 2（二进制的基数），然后加上当前字符代表的数值（`int(char)`将字符 '0' 或 '1' 转换为整数 0 或 1）。这样，每次迭代都会正确地将二进制位转换为对应的十进制值。
- 这个过程模拟了手动计算的过程，每次乘以 2 相当于在十进制中将位数进一位，然后加上当前的二进制位。

### 2.4 十进制到十六进制的转换

#### 手动方法：

- 将十进制数除以 16。

- 记录余数，如果余数大于 9，则将其转换为对应的十六进制字符（A-F）。

- 用商继续除以 16，直到商为 0。

- 十六进制数即为逆序读取的余数序列。

#### 示例：将 479 转换为十六进制

```
479 / 16 = 29 余 F
29 / 16 = 1 余 D
1 / 16 = 0 余 1
```

结果：`479 (十进制) = 1DF (十六进制)`



#### 示例：用 Python 实现十进制到十六进制的转换

```python
def dec_to_hex(num):
    result = ""
    while num != 0:
        remainder = num % 16
        if remainder >= 10:
            result += chr(remainder - 10 + ord('a'))
        else:
            result += str(remainder)
        num = num // 16
    return result[::-1]  # 逆序输出

# 主程序
print(dec_to_hex(479))
```

- remainder = num % 16：使用`num % 16`计算当前位的余数（0-15），这个余数就是当前位的十六进制值。
- result += chr(remainder - 10 + ord('a'))：如果余数大于等于10（即A-F），使用`chr(remainder - 10 + ord('a'))`将余数转换为对应的十六进制字符（'a' 到 'f'）。
- result += str(remainder)：如果余数小于10，直接将余数转换为字符串，并添加到`result`的末尾。
- return result[::-1]：计算得到的十六进制位是逆序的（最低位在前，最高位在后），使用切片`[::-1]`将字符串逆序，以得到正确的十六进制表示。

### 2.5 二进制到十六进制的转换

### 手动方法：

二进制转换为十六进制的方法是将二进制数每4位分为一组，然后将每组的二进制数转换为对应的十六进制数。因为十六进制是以4位二进制为基础的，所以这个过程非常直接。

#### 步骤：

1. 从右到左，将二进制数每4位分为一组。如果不足4位，则在左侧补零。
2. 将每组二进制数转换为对应的十六进制数。
3. 将转换后的十六进制数连接起来，得到最终结果。

#### 示例：将二进制`110111101`转换为十六进制

步骤：

1. 将`110111101`分为`1101`和`1110`，不足4位的左侧补零：`0110 1110 1101`
2. 将每组转换为十六进制：
   -`0110`转换为`6`
   -`1110`转换为`E`
   -`1101`转换为`D`
3. 将这些转换结果连接起来：`6ED`

结果：`110111101 (二进制) = 6ED (十六进制)`

代码实现部分我们现在先不需要深入了解，因为涉及到其他的一些函数和库的使用，一般做法还是先将二进制转十进制，再将十进制转十六进制。当前我们主要专注于理解手动方法，这样可以帮助更好地掌握进制转换的基础概念。

### 2.6 进制例题讲解

### 2.6.1 LC504. 七进制数

#### 问题描述

给定一个整数`num`，返回它的 7 进制表示字符串。

#### 思路分析

将一个整数转换为7进制本质上和转换为任何其他进制的思路一致。我们可以通过不断地取模（`%`）和除法（`/`）操作来逐位获取7进制的各位数字，最后将其反转即可得到最终的结果。

1. **处理负数**：
   - 如果输入`num`是负数，先取它的绝对值进行计算，最后在结果前添加负号。
2. **处理 0 的特殊情况**：
   - 如果`num == 0`，直接返回`"0"`。
3. **取模法构建7进制**：
   - 我们不断将`num`除以 7，取出余数作为当前位的7进制数字，将其加入到结果字符串中。然后将`num`更新为`num / 7`，直到`num`变为 0 为止。
4. **反转字符串**：
   - 因为我们从最低位开始计算，所以最终需要将字符串反转。

#### 参考解答

```python
class Solution:
    def convertToBase7(self, num: int) -> str:
        initial_num = num  # 保存初始值
        
        # 如果是负数，取绝对值进行计算
        if num < 0:
            num = -num
        
        # 特殊情况：num 为 0，直接返回 "0"
        if num == 0:
            return "0"
        
        # 构建 7 进制
        ans = []
        while num > 0:
            ans.append(str(num % 7))  # 将每一位的 7 进制数字加入到列表
            num //= 7  # 除以 7，进行下一位的计算
        
        # 如果初始值是负数，添加负号
        if initial_num < 0:
            ans.append('-')
        
        # 最后反转并拼接列表为字符串
        return ''.join(ans[::-1])
```

1. **`initial_num = num`**：保留原始的`num`值，用于后续判断是否需要添加负号。
2. **处理负数**：如果`num`为负数，先取绝对值，计算完后再在结果前加上`'-'`。
3. **处理0的情况**：如果`num`为 0，直接返回`"0"`。
4. **取模和除法**：通过`num % 7`获取当前位的7进制数字，并将其加入到结果字符串中；然后通过`num /= 7`进行下一位的计算。
5. **反转字符串**：由于从最低位开始构建字符串，最后需要反转得到正确的顺序。
6. **返回结果**：经过所有处理后，返回结果字符串。

### 2.7 进制举一反三

### 2.7.1 LC168. excel表列名称

#### 问题描述

给定一个正整数，返回它在 Excel 表中对应的列标题。Excel 列是以`A-Z`的方式排列的，例如：

```
1 -> A
2 -> B
3 -> C
...
26 -> Z
27 -> AA
28 -> AB
...
```

#### 思路分析

这是一个典型的进制转换问题。需要将数字转换成以`A-Z`为基础的26进制表示法，类似于十进制转换为二进制或十六进制。由于 Excel 列编号从 1 开始，而不是从 0 开始，所以在转换时需要一些额外的调整。

1. **从 1 开始的26进制：**
   - 我们可以将`A-Z`对应的数字看作是一个基于26的进制系统。
   - 但与常见进制不同的是，Excel 列编号是从 1 开始的，而不是从 0 开始，因此在每次取余时需要做一些调整：每次将`columnNumber`减去 1。

2. **处理逻辑：**
   - 不断将`columnNumber`减去1，并计算出对应的字母。
   - 每次通过`columnNumber % 26`得到一个字母，将其加入结果字符串中。
   - 将`columnNumber`除以26，继续处理下一个数字，直到`columnNumber`为 0。

3. **反转字符串：**
   - 由于我们从最低位开始构造字符串，因此最后需要将结果字符串反转。

#### 参考解答

```python
class Solution:
    def convertToTitle(self, columnNumber: int) -> str:
        result = []
        
        # 处理进制转换
        while columnNumber > 0:
            # 因为是从 1 开始的列，所以需要先减 1
            columnNumber -= 1
            
            # 计算当前位对应的字母
            temp = columnNumber % 26
            result.append(chr(temp + ord('A')))
            
            # 减少列号
            columnNumber //= 26
        
        # 反转结果
        return ''.join(result[::-1])
```

#### 代码讲解

1. **`columnNumber -= 1`**：先将列号减 1，以便将问题转换为以 0 为基准的 26 进制。
2. **`columnNumber % 26`**：计算当前的列对应的字母编号（0 到 25 对应`A`到`Z`）。
3. **`result.append(chr(temp + ord('A')))`**：将编号转换为字母并添加到结果字符串中。
4. **`columnNumber //= 26`**：将列号除以 26，处理下一位。
5. **字符串反转**：因为字母是从最低位开始计算的，因此需要在最后反转字符串。

### 2.7.2 LC728. 自除数

#### 问题描述

自除数是指一个整数，它的每一位数字都能整除这个数本身。给定一个范围`[left, right]`，返回该范围内所有的自除数。

一个自除数必须满足以下条件：

1. 该数不能包含数字`0`。
2. 该数能被它的每一位数字整除。

#### 思路分析

1. **逐位检查**：对于每个数字，将其每一位提取出来，检查该位是否为 0，并且能否整除原数字。
2. **遍历范围**：对于给定的范围`[left, right]`，逐一检查每个数字是否是自除数，如果是，将其加入结果列表中。
3. **返回结果**：返回在`[left, right]` 范围内所有自除数的列表。

#### 参考解答

```python
class Solution:
    def selfDividingNumbers(self, left: int, right: int) -> List[int]:
        def isSelfDividing(num: int) -> bool:
            x = num
            while x:
                x, d = divmod(x, 10)
                if d == 0 or num % d:
                    return False
            return True
        return [i for i in range(left, right + 1) if isSelfDividing(i)]
```

1. **`divmod(x, 10)`**: 用于同时获得商和余数，比`x // 10` 和`x % 10` 更简洁。

2. **遍历范围**：在`selfDividingNumbers` 函数中，遍历范围`[left, right]`，使用 isSelfDividing 函数判断每个数是否是自除数，如果是则将其加入结果列表。

3. **返回结果**：最终返回`[left, right]` 范围内所有自除数的列表。

### 2.7.3 LC693. 交替位二进制数

#### 问题描述

给定一个正整数`n`，检查其二进制表示是否为交替位二进制数，交替位二进制数的定义是其相邻的两个位始终不同，即二进制中`0` 和`1` 交替出现。

#### 思路分析

1. **逐位检查**：通过不断将`n` 右移，并提取其当前的最后一位，检查是否相邻的两位相同。
2. **终止条件**：当某一位和其相邻的上一位相同时，直接返回`False`。
3. **全部检查通过**：如果所有相邻的位都不同，则返回`True`。

#### 参考解答

```python
class Solution:
    def hasAlternatingBits(self, n: int) -> bool:
        now = n % 2  # 提取当前位
      
        while n > 0:
            n //= 2  # 右移，去掉当前位
            next_bit = n % 2  # 提取下一位
            
            if next_bit == now:
                return False  # 如果相邻的两位相同，返回 False
            
            now = next_bit  # 更新当前位为下一位
        
        return True  # 全部位都交替，返回 True
```

#### 代码讲解

1. `now = n % 2`：提取当前最低位。
2. `n //= 2：右移`n，去掉已经检查的最低位。
3.  next_bit = n % 2：提取右移后的下一位。
4.  **相邻位比较**：如果`next` 和`now` 相等，则说明相邻的两位相同，返回 False。
5.  **检查通过**：如果所有位都不同，返回 True`，表示`n 是交替位二进制数。

## 3. 课后练习


### ASCII 相关问题
| 题目编号 | 题目名称                                | 简介                                                                 |
|---------|-------------------------------------|--------------------------------------------------------------------|
| LC405   | 数字转换为十六进制数   | 将一个整数转换为其 16 进制表示。                                                    |
| LC806   | 写字符串需要的行数     | 给定若干行字符串，计算写入所需的行数。                                                |
| LC2309  | 间距大小写的最好英文字母 | 找到包含大写和小写字母的最大英文字母。                                |
| LC383   | 赎金信                                 | 判断一个字符串中的字符是否能由另一个字符串中的字符构成。                              |
| LC389   | 找不同                                  | 给定两个字符串，找出一个在其中多出的字符。                                          |


### 进制转换相关问题

| 题目编号 | 题目名称                                 | 简介                                                     |
|---------|------------------------------------|--------------------------------------------------------|
| LC868   | 二进制间距                             | 找到二进制数中最大的 0 和 1 间的距离。                                |
| LC1317  | 将整数转换为两个无零整数的和              | 将一个整数转换为两个非零整数之和。                                   |
| LC1281  | 整数的各位积和之差                      | 返回一个整数各位数字乘积与和的差值。                                 |
| LC67    | 二进制求和                             | 给定两个二进制字符串，返回它们的和（以二进制表示）。                            |
