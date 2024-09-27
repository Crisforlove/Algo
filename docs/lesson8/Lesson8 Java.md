# Lesson8 字符串循环+切片/字符串数学运算专题

## 目录
1. [字符串循环+切片](#1-字符串循环切片)
     - [LC14 最长公共前缀](#lc14-最长公共前缀)  
     - [LC125 验证回文串](#lc125-验证回文串)  
     - [LC459 重复的子字符串](#lc459-重复的子字符串)  
     - [LC796 旋转字符串](#lc796-旋转字符串)  
     - [LC28 查找字符串中的第一个匹配项索引](#lc28-查找字符串中的第一个匹配项索引)  
     
2. [字符串数学运算](#2-字符串数学运算)  
     - [LC415 字符串相加](#lc415-字符串相加)  
     - [LC7 整数反转](#lc7-整数反转)  
     - [LC67 二进制求和](#lc-67-二进制求和)  
     - [LC989 数组形式的整数加法](#lc989-数组形式的整数加法)  

3. [课后练习](#课后练习)  

## 1. 字符串循环+切片

## 例题讲解
### LC14 最长公共前缀

### 题目描述
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

### 题目分析

要找到字符串数组中的最长公共前缀，我们可以依次比较每个字符串的字符，直到找到不匹配的位置为止。这个问题可以通过多种方法解决，比如纵向扫描、横向扫描、分治法、二分查找等。我们这里采用一种较为直观的横向扫描法。

### 思路

1. **边界情况**: 
   - 如果字符串数组为空，直接返回空字符串。
   - 如果字符串数组只有一个字符串，那么最长公共前缀就是这个字符串本身。

2. **从第一个字符串开始**:
   - 假设第一个字符串是最长公共前缀，接下来逐一与数组中的其他字符串进行比较。
   - 每次比较时，逐字符地进行比较，直到找到不匹配的字符或比较完成一个字符串的所有字符。
   - 更新当前的最长公共前缀为匹配的部分。

3. **返回结果**:
   - 最后返回匹配后的公共前缀，如果没有匹配到任何前缀，则返回空字符串。
    

### 参考解答

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        // 边界情况处理
        if (strs == null || strs.length == 0) {
            return "";
        }

        // 初始化最长公共前缀为第一个字符串
        String prefix = strs[0];

        // 依次与其他字符串比较
        for (int i = 1; i < strs.length; i++) {
            // 当前前缀与下一个字符串比较
            while (strs[i].indexOf(prefix) != 0) {
                // 缩短前缀长度
                prefix = prefix.substring(0, prefix.length() - 1);
                // 如果前缀为空，返回空字符串
                if (prefix.isEmpty()) {
                    return "";
                }
            }
        }

        return prefix;
    }
}
```

### LC125 验证回文串

### 题目描述

如果在将所有大写字符转换为小写字符、并移除所有非字母数字字符之后，短语正着读和反着读都一样。则可以认为该短语是一个 回文串 。

字母和数字都属于字母数字字符。

给你一个字符串 s，如果它是回文串，返回 `true`；否则，返回 `false` 。

### 题目分析

我们需要统计字符串中的单词个数，单词是由连续的非空格字符组成的。空格可以用来分隔单词。题目保证字符串中没有不可打印字符，因此不需要处理特殊字符。

### 思路

对字符串 s 进行一次遍历，并将其中的字母和数字字符进行保留，放在另一个字符串 sgood 中。这样我们只需要判断 sgood 是否是一个普通的回文串即可。

可以使用语言中的字符串翻转 API 得到 sgood 的逆序字符串 sgood_rev，只要这两个字符串相同，那么 sgood 就是回文串。

### 参考解答

```java
class Solution {
   public boolean isPalindrome(String s) {
      StringBuilder sgood = new StringBuilder(); // 用于存储有效字符
      int length = s.length();

      // 遍历输入字符串
      for (int i = 0; i < length; i++) {
         char ch = s.charAt(i); // 获取当前字符

         // 判断是否为字母或数字
         if (Character.isLetterOrDigit(ch)) {
            sgood.append(Character.toLowerCase(ch)); // 转为小写并添加到有效字符中
         }
      }

      // 创建反转后的有效字符字符串
      StringBuilder sgood_rev = new StringBuilder(sgood).reverse();

      // 使用 contentEquals 方法比较有效字符和反转字符
      return sgood.contentEquals(sgood_rev);
   }
}
```

## 举一反三

### LC459 重复的子字符串

### 题目描述

给定一个非空的字符串 `s` ，检查是否可以通过由它的一个子串重复多次构成。

### 解题思路

1. **遍历可能的子串长度**：
   - 从 `1` 开始遍历到字符串长度的一半，检查字符串是否能通过重复某个子串构成。

2. **判断是否可以整除**：
   - 通过检查 `len % i == 0`，判断当前子串的长度 `i` 是否可以整除整个字符串的长度。如果可以整除，那么 `s.length()` 必须是子串长度的倍数。

3. **构建新字符串**：
   - 取出当前的子串 `substring`，然后通过 `StringBuilder` 将该子串重复 `(len / i)` 次构造出一个新的字符串。

4. **比较**：
   - 如果新构建的字符串与原字符串 `s` 相同，则返回 `true`，表示 `s` 是通过该子串的重复构成的。

5. **时间复杂度**：
   - 最坏情况下时间复杂度为 `O(n^2)`，因为外层循环要执行 `n / 2` 次，且每次需要构建和比较字符串。


### 示例代码

```java
class Solution {
    public static repeatedSubstringPattern(String s) {
        int n = s.length();
        
        // 遍历可能的子串长度
        for (int i = 1; i <= n / 2; i++) {
            // 检查是否可以整除
            if (n % i == 0) {
                String substring = s.substring(0, i);
                // 构造由子串重复的字符串
                StringBuilder repeated = new StringBuilder();
                for (int j = 0; j < n / i; j++) {
                    repeated.append(substring);
                }
                // 比较构造的字符串与原字符串
                if (repeated.toString().equals(s)) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

### 更高效的解法

可以利用字符串的特性来进一步优化：

1. 将字符串 `s` 自身拼接一遍，得到 `s + s`。
2. 去掉开头和结尾的字符，检查 `s` 是否在新的字符串中出现。
3. 如果出现，说明 `s` 可以由某个子串构成。

### 优化示例代码
```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        String doubled = s + s; // 将字符串拼接
        String subString = doubled.substring(1, doubled.length() - 1); // 去掉首尾字符
        return subString.contains(s); // 检查是否包含原字符串
    }
}
```
### 证明：字符串拼接后掐头去尾可以用于判断重复的子字符串

#### 补充：什么是前缀和后缀？

1. **前缀（Prefix）**：从字符串的**开头**开始的连续字符子串。例如，字符串 `"abcde"` 的前缀有：
   - 前缀 1：`"a"`
   - 前缀 2：`"ab"`
   - 前缀 3：`"abc"`
   - 前缀 4：`"abcd"`
   - 前缀 5：`"abcde"`（整个字符串本身也是一个前缀）

2. **后缀（Suffix）**：从字符串的**结尾**开始的连续字符子串。例如，字符串 `"abcde"` 的后缀有：
   - 后缀 1：`"e"`
   - 后缀 2：`"de"`
   - 后缀 3：`"cde"`
   - 后缀 4：`"bcde"`
   - 后缀 5：`"abcde"`（整个字符串本身也是一个后缀）

   
#### 充分必要性证明

为了证明给定字符串 `s` 是由某个子串重复构成的充分必要性，我们需要从两个方向来进行证明：

1. **充分性**：如果一个字符串 `s` 是由某个子串重复构成的，那么在拼接后的字符串 `s + s` 中，掐头去尾后，一定能再次找到 `s`。
2. **必要性**：如果在掐头去尾的 `s + s` 中找到了 `s`，那么 `s` 一定是由某个子串重复构成的。

---

#### **1. 充分性**

**假设**：设字符串 `s` 是由一个较短的子串 `p` 重复多次构成的，即 `s = p + p + ... + p`（假设 `p` 重复 `k` 次）。

**举例**：比如 `s = "abab"`，这是由 `p = "ab"` 重复两次构成的。

**拼接 `s + s`**：我们将 `s` 拼接得到 `s + s`，例如：

```
s + s = "abababab"
```

接着，掐头去尾，去掉首尾字符，得到 `new_s = (s + s).substring(1, (s + s).length() - 1)`，对于上面的例子：

```
new_s = "bababa"
```

**寻找 `s` 在 `new_s` 中的出现**：由于 `s` 是由子串 `p` 多次重复（至少两次）构成的，`s + s` 就会重复至少 **4** 次 `p`，掐头去尾后，重复至少 **2** 次 `p`，前缀和后缀必然有重叠，一定能再次找到 `s`。

```
new_s = "bababa"
          ^^^^ (这里找到 "abab")
```
充分性证毕。

---


#### **2. 必要性**

**假设**：我们已经在去掉首尾字符的 `s + s` 中再次找到了 `s`。现在我们需要证明，`s` 一定是由某个子串重复构成的。

**构造 `new_s`**：首先，构造 `new_s = (s + s).substring(1, (s + s).length() - 1)`，假设 `s` 在 `new_s` 中匹配的位置是从 `i` 开始。也就是说，我们找到了一个偏移量 `i`，使得 `s.substring(i) + s.substring(0, i)` 和 `s` 完全相同，这意味着：

```
s == s.substring(i) + s.substring(0, i);
```
也就是说，`s` 的某个 **后缀** 与它的某个 **前缀** 重叠匹配。

**举例说明**：
```
s + s = "abababab"
去掉首尾字符后得到：new_s = "bababa"
```
   - `s` 的前缀有：`'a', 'ab', 'aba', 'abab'`
   - `s` 的后缀有：`'b', 'ab', 'bab', 'abab'`

可以发现，`s = "abab"` 在 `"bababa"` 中确实再次出现，且匹配发生在交界处（偏移量为1），这时 `s` 的前缀和后缀出现了重合。


这种现象说明 `s` 的前缀和后缀存在交替重叠，表明 `s` 具有周期性，意味着 `s` 是由一个较短的子串重复构成的。**换句话说，如果 `s` 的前缀和后缀有某种重叠，形成了周期性，那么 `s` 就可以通过重复某个子串构成。**

必要性证毕。

---

#### 总结：

我们已经证明了：

1. **充分性**：如果 `s` 是由某个子串重复构成的，那么在 `s + s` 中掐头去尾后，一定能够再次找到 `s`。这是因为重复子串会使得前缀和后缀有重叠。

2. **必要性**：如果在掐头去尾的 `s + s` 中找到了 `s`，那么 `s` 一定是由某个子串重复构成的。这是因为只有当 `s` 具有周期性时，它的前缀和后缀才会交替重叠，形成匹配。

因此，拼接 `s + s` 并去掉首尾字符后能否再次找到 `s`，可以用来判断 `s` 是否由某个子串重复构成。


#### 补充材料：

[充分性及必要性证明](https://writings.sh/post/algorithm-repeated-string-pattern)

[Leetcode官方题解证明](https://leetcode.cn/problems/repeated-substring-pattern/solutions/386481/zhong-fu-de-zi-zi-fu-chuan-by-leetcode-solution/)


### LC796 旋转字符串

### 问题描述

给定两个字符串, `s` 和 `goal`。如果在若干次旋转操作之后，`s` 能变成 `goal`，那么返回 `true`。

`s` 的 `旋转操作` 就是将 `s` 最左边的字符移动到最右边。 

例如, 若 s = 'abcde'，在旋转一次之后结果就是'bcdea' 。

要判断字符串 `s` 是否可以通过若干次旋转操作变成字符串 `goal`，我们可以采用以下思路进行解决：

### 解题思路

1. **字符串旋转的特性**：
   - 如果我们将字符串 `s` 进行两次拼接，得到 `s + s`，这个新字符串包含了所有可能的旋转形式。
   - 例如：
     - 对于 `s = "abcde"`，拼接后 `s + s = "abcdeabcde"`，其中包含了 `"abcde"` 的所有旋转形式，如 `"abcde"`、`"bcdea"`、`"cdeab"`、`"deabc"` 和 `"eabcd"`。

2. **判断 `goal` 是否在 `s + s` 中**：
   - 只需检查 `goal` 是否是 `s + s` 的子串。
   - 如果 `goal` 是 `s + s` 的子串，则返回 `true`，否则返回 `false`。

### 示例代码

```java
class Solution {
    public boolean rotateString(String s, String goal) {
        // 检查长度是否相等
        if (s.length() != goal.length()) {
            return false;
        }
        
        // 拼接字符串
        String doubled = s + s;
        
        // 检查 goal 是否为 doubled 的子串
        return doubled.contains(goal);
    }
}
```
### 简洁写法
```java
class Solution {
    public boolean rotateString(String s, String goal) {
        return s.length() == goal.length() && (s + s).contains(goal);
    }
}
```


### LC28 查找字符串中的第一个匹配项索引

### 问题描述

给定两个字符串 `haystack` 和 `needle`，你需要在 `haystack` 字符串中找出 `needle` 字符串出现的第一个位置（从 0 开始）。如果不存在，则返回 `-1`。

### 思路分析

1. **如果 `needle` 为空字符串，直接返回 `0`。**
2. **遍历 `haystack`，从每个索引位置检查是否与 `needle` 匹配。**
3. **如果匹配成功，返回该索引，否则继续遍历。**
4. **如果遍历结束后未找到，返回 `-1`。**

### 参考解答
```java
class Solution {
    public int strStr(String haystack, String needle) {
        // 如果needle为空字符串，直接返回0
        if (needle.isEmpty()) {
            return 0;
        }

        // 获取两个字符串的长度
        int n = haystack.length();
        int m = needle.length();

        // 遍历haystack，直到剩余的部分长度小于needle长度
        for (int i = 0; i <= n - m; i++) {
            // 比较从i开始的子串是否等于needle
            if (haystack.substring(i, i + m).equals(needle)) {
                return i;
            }
        }

        // 如果遍历结束后没有找到，返回-1
        return -1;
    }
}
```

## 2. 字符串数学运算

字符串数学模拟的基本解题思路主要涉及如何通过逐步操作和简单的数学运算，处理字符串形式的数字计算。

### 基本概念

1. **字符转数字**：
   - 字符串中的数字是以字符的形式存在的，例如字符 `'0'` 到 `'9'`。
   - 可以通过 `char - '0'` 将字符转为对应的数字。例如，`'5' - '0'` 的结果为 `5`。

2. **进位处理**：
   - 在进行加法运算时，如果某一位的和大于或等于 `10`，则需要处理进位（carry），将 `1` 加到下一位的计算中。
   - 进位的计算可以通过 `carry = sum / 10` 来实现，而当前位的结果则是 `sum % 10`。

3. **逆序计算**：
   - 字符串通常从右到左进行加法，因为我们从个位开始。处理完最后一位后，继续处理十位、百位等。
   - 为了方便存储结果，通常会使用 `StringBuilder` 逐位添加，最后再反转字符串以获得正确的顺序。
   

## 例题讲解

### LC415 字符串相加

### 题目描述
给定两个字符串形式的非负整数 `num1` 和 `num2` ，计算它们的和并同样以字符串形式返回。

你不能使用任何內建的用于处理大整数的库（比如 BigInteger），也不能直接将输入的字符串转换为整数形式。

### 题目分析
要计算两个字符串形式的非负整数 `num1` 和 `num2` 的和，并返回结果为字符串形式，我们需要手动模拟加法的过程，类似于在纸上进行加法计算。下面是详细的解题思路和步骤。

### 解题思路

1. **从右到左遍历**：
   - 加法通常是从个位开始计算，因此我们需要从两个字符串的末尾开始遍历。

2. **逐位相加**：
   - 对于 `num1` 和 `num2` 中的每一位，分别将它们转化为数字，进行加法操作。
   - 需要考虑进位（carry）的影响，即如果某一位的和大于或等于 10，则需要将 1 进位到下一位。

3. **处理不同长度的字符串**：
   - 在进行加法时，如果两个字符串的长度不同，我们需要确保从最右边开始添加上短字符串的缺失部分。
   - 例如，对于 `num1` 长度为 5 和 `num2` 长度为 3 的情况，我们只需要在计算时考虑 `num2` 的前三位。

4. **处理最后的进位**：
   - 如果遍历结束后还有进位（carry）未处理，需要将其添加到结果中。

5. **结果拼接**：
   - 由于我们是从后向前计算的，因此最终的结果需要反转一下。
   
### 示例代码

```java
public class Solution{
    public static String addStrings(String num1, String num2) {
        StringBuilder result = new StringBuilder();
        int carry = 0;  // 进位
        int i = num1.length() - 1;  // num1 的最后一位索引
        int j = num2.length() - 1;  // num2 的最后一位索引
        
        // 循环直到 num1 和 num2 都遍历完
        while (i >= 0 || j >= 0 || carry > 0) {
            int sum = carry;  // 从进位开始
            if (i >= 0) {
                sum += num1.charAt(i) - '0';  // 将字符转为数字
                i--;  // 移动到上一位
            }
            if (j >= 0) {
                sum += num2.charAt(j) - '0';  // 将字符转为数字
                j--;  // 移动到上一位
            }
            
            result.append(sum % 10);  // 当前位的结果
            carry = sum / 10;  // 更新进位
        }
        
        return result.reverse().toString();  // 反转结果并返回
    }
}
```

### LC7 整数反转

### 题目描述
给你一个 32 位的有符号整数 `x` ，返回将 `x` 中的数字部分反转后的结果。

### 解题思路

1. **取出最后一位数字**：`digit = x % 10` 用于提取 `x` 的最后一位数字。
2. **更新结果**：`result = result * 10 + digit` 将数字加入到 `result` 中，逐步构建反转后的整数。
3. **移除最后一位数字**：`x /= 10` 用于去除 `x` 的最后一位数字。
4. **溢出检查**：
   - 当 `result > Integer.MAX_VALUE / 10` 时，若继续添加一位数字，反转结果将超过 `Integer.MAX_VALUE`。
   - 当 `result == Integer.MAX_VALUE / 10` 时，最后一位数字 `digit` 必须小于等于 7（即最大值的最后一位）。
   - 类似地，处理负数时也要检查最小值 `Integer.MIN_VALUE`，并确保 `digit` 小于等于 -8（最小值的最后一位）。
5. **返回结果**：如果没有溢出，则返回反转后的整数；如果溢出则返回 0。

### 溢出条件说明
- `Integer.MAX_VALUE = 2147483647`，最后一位是 7。
- `Integer.MIN_VALUE = -2147483648`，最后一位是 -8。

### 参考解答

```java
class Solution {
   public int reverse(int x) {
      int result = 0;

      while (x != 0) {
         int digit = x % 10;

         // 检查是否会溢出：如果 result 超过了边界，返回 0
         if (result > Integer.MAX_VALUE / 10 || (result == Integer.MAX_VALUE / 10 && digit > 7)) {
            return 0;
         }
         if (result < Integer.MIN_VALUE / 10 || (result == Integer.MIN_VALUE / 10 && digit < -8)) {
            return 0;
         }

         // 构建反转后的结果
         result = result * 10 + digit;
         // 移除 x 的最后一位
         x /= 10;
      }

      return result;
   }
}
```

## 举一反三

### LC67 二进制求和

### 题目描述

给你两个二进制字符串 `a` 和 `b` ，以二进制字符串的形式返回它们的和。

### 解题思路

1. **从右到左遍历**：
   - 由于二进制加法是从最右侧的位（最低位）开始的，我们需要从字符串的末尾开始处理。

2. **逐位相加**：
   - 使用两个指针分别指向两个字符串的末尾（即最后一位）。
   - 逐位相加并处理进位（carry）。

3. **处理不同长度的字符串**：
   - 如果两个字符串的长度不同，短的字符串在计算时会缺失部分位。需要在处理过程中检查是否已经超出某个字符串的长度。

4. **处理最后的进位**：
   - 如果遍历结束后仍然有进位（carry），需要将其添加到结果中。

5. **拼接和反转结果**：
   - 由于我们是从后向前计算的，因此需要在最后反转结果字符串。

### 示例代码

```java
public class Solution {
    public String addBinary(String a, String b) {
        StringBuilder result = new StringBuilder();
        int carry = 0; // 进位
        int i = a.length() - 1; // a 的最后一位索引
        int j = b.length() - 1; // b 的最后一位索引

        // 循环直到 a 和 b 都遍历完
        while (i >= 0 || j >= 0 || carry > 0) {
            // 计算当前位的和
            if (i >= 0) {
                carry += a.charAt(i--) - '0'; // 取 a 的当前位并转为数字
            }
            if (j >= 0) {
                carry += b.charAt(j--) - '0'; // 取 b 的当前位并转为数字
            }

            // 将当前位的结果添加到结果中
            result.append(carry % 2); // 当前位结果
            carry /= 2; // 更新进位
        }

        return result.reverse().toString(); // 反转结果并返回
    }
}
```

### LC989 数组形式的整数加法

### 题目描述
整数的数组形式 `num` 是按照从左到右的顺序表示其数字的数组。

例如，对于 `num = 1321` ，数组形式是 `[1,3,2,1]` 。
给定 `num` ，整数的数组形式，和整数 `k` ，返回 整数 `num + k` 的数组形式。

### 解题思路

1. **从右到左进行加法**：
   - 从数组 `num` 的最后一位（最低位）开始加，逐位处理。
  
2. **处理进位**：
   - 每一位的和可能会产生一个进位，我们需要记录这个进位并在下一位的加法中使用。

3. **遍历结束后的处理**：
   - 如果在遍历结束时仍有进位，需要将进位添加到结果中。

4. **结果构建**：
   - 将计算的结果存储在一个列表中，最后需要反转这个列表，因为我们是从最低位开始计算的。
   

### 示例代码

```java
import java.util.ArrayList;

public class Solution {
    public ArrayList<Integer> addToArrayForm(int[] num, int k) {
        ArrayList<Integer> result = new ArrayList<>();
        int carry = 0; // 初始化进位
        int n = num.length; // 数组长度
        
        // 从数组的最后一位开始处理
        for (int i = n - 1; i >= 0; i--) {
            int sum = num[i] + (k % 10) + carry; // 当前位的和
            result.add(sum % 10); // 当前位结果
            carry = sum / 10; // 更新进位
            k /= 10; // 移动到 k 的下一位
        }
        
        // 处理 k 可能还有的剩余位
        while (k > 0 || carry > 0) {
            int sum = (k % 10) + carry; // 当前位的和
            result.add(sum % 10); // 当前位结果
            carry = sum / 10; // 更新进位
            k /= 10; // 移动到 k 的下一位
        }
        
        // 由于我们是从后向前构建的结果，需要反转
        ArrayList<Integer> finalResult = new ArrayList<>();
        for (int j = result.size() - 1; j >= 0; j--) {
            finalResult.add(result.get(j));
        }
        
        return finalResult;
    }
}
```

## 课后练习

### 字符串循环+切片

| 题目编号  | 题目名称          | 简介                                         |
|-------|------------------|--------------------------------------------|
| LC 1002 | 找到共同字符       | 找到给定字符串数组中所有字符串的共同字符。         |
| LC 541  | 反转字符串 II     | 反转字符串中的指定部分，每隔一个指定长度反转一次。   |
| LC 771  | 珠宝与石头        | 计算在石头中有多少个珠宝字符。                     |
| LC 844  | 回退字符串比较    | 比较两个字符串，考虑到回退字符（‘#’）的影响。       |
| LC 925  | 长按键入的名字    | 检查一个名字是否可以通过长按另一个名字的字符来实现。   |


### 字符串数学运算
| 题目编号  | 题目名称          | 简介                                         |
|-------|------------------|--------------------------------------------|
| LC 2243 | 计算字符串中的数字和 | 计算字符串中所有数字字符的总和。                     |
| LC 66   | 加一              | 在数组形式的数字上加一，并返回结果的数组形式。       |