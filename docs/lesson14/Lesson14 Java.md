# Lesson 14 列表双指针算法

## 目录
- [1.1 对撞指针求解步骤](#11-对撞指针求解步骤)
    - [1.2 对撞指针伪代码模板](#12-对撞指针伪代码模板)
    - [1.3 对撞指针适用范围](#13-对撞指针适用范围)
    - [1.4 例题讲解](#14-例题讲解)
        - [1.4.1 LC167 两数之和II - 输入有序数组](#141-LC167-两数之和II---输入有序数组)
    - [1.5 举一反三](#15-举一反三)
        - [1.5.1 LC11 盛水最多的容器](#151-LC11-盛水最多的容器)
        - [1.5.2 LC881 救生艇](#152-LC881-救生艇)
        - [1.5.3 LC658 找到K个最接近的元素](#153-LC658-找到K个最接近的元素)
- [2 滑动窗口](#2-滑动窗口)
    - [2.1 固定长度滑动窗口](#21-固定长度滑动窗口)
        - [2.2 固定窗口例题讲解](#22-固定窗口例题讲解)
            - [2.2.1 LC1343 大小为 K 且平均值大于等于阈值的子数组数目](#221-LC1343-大小为-K-且平均值大于等于阈值的子数组数目)
        - [2.3 固定窗口举一反三](#23-固定窗口举一反三)
            - [2.3.1 LC1052 爱生气的书店老板](#231-LC1052-爱生气的书店老板)
            - [2.3.2 LC239 滑动窗口的最大值](#232-LC239-滑动窗口的最大值)
            - [2.3.3 LC643 子数组最大平均数](#233-LC643-子数组最大平均数)
    - [2.4 不定长度滑动窗口](#24-不定长度滑动窗口)
    - [2.5 不定窗口例题讲解](#25-不定窗口例题讲解)
        - [2.5.1 LC209 长度最小的子数组](#251-LC209-长度最小的子数组)
    - [2.6 不定窗口举一反三](#26-不定窗口举一反三)
        - [2.6.1 LC713 乘积小于K的子数组](#261-LC713-乘积小于K的子数组)
        - [2.6.2 LC424 替换后的最长重复字符](#262-LC424-替换后的最长重复字符)
        - [2.6.3 LC1658 将x减到0的最小操作数](#263-LC1658-将x减到0的最小操作数)
- [3 课后练习](#3-课后练习)
    - [对撞指针](#对撞指针)
    - [固定长度滑动窗口](#固定长度滑动窗口)
    - [不定长度滑动窗口](#不定长度滑动窗口)

## 1 对撞指针

> **对撞指针**：指的是两个指针`left`、`right`分别指向序列第一个元素和最后一个元素，然后`left`指针不断递增，`right`不断递减，直到两个指针的值相撞（即`left == right`），或者满足其他要求的特殊条件为止。

![对撞指针](https://qcdn.itcharge.cn/images/202405092155032.png)

### 1.1 对撞指针求解步骤

1. 使用两个指针`left`,`right`。`left`指向序列第一个元素，即：`left = 0`,`right`指向序列最后一个元素，即：`right = nums.length - 1`。
2. 在循环体中将左右指针相向移动，当满足一定条件时，将左指针右移,`left ++`。当满足另外一定条件时，将右指针左移,`right--`。
3. 直到两指针相撞（即`left == right`) ，或者满足其他要求的特殊条件时，跳出循环体。

### 1.2 对撞指针伪代码模板

```java
public class Solution {
    public int twoPointerTemplate(int[] nums) {
        int left = 0, right = nums.length - 1;

        while (left < right) {
            if (满足要求的特殊条件) {
                return 符合条件的值;  // 找到符合条件的结果时返回
            } else if (一定条件1) {
                left++;  // 根据条件移动左指针
            } else if (一定条件2) {
                right--;  // 根据条件移动右指针
            }
        }

        return 没找到或找到对应值;  // 返回找到的结果或表示没找到的值
    }
}
```

### 1.3 对撞指针适用范围

对撞指针一般用来解决有序数组或者字符串问题：

- 查找有序数组中满足某些约束条件的一组元素问题：比如二分查找、数字之和等问题。
- 字符串反转问题：反转字符串、回文数、颠倒二进制等问题。

### 1.4 例题讲解

### 1.4.1 LC167 两数之和II - 输入有序数组

#### 问题描述

给你一个下标从 **1** 开始的整数数组`numbers`，该数组已按 **非递减顺序排列** ，请你从数组中找出满足相加之和等于目标数`target`的两个数。如果设这两个数分别是`numbers[index1]`和`numbers[index2]`，则`1 <= index1 < index2 <= numbers.length`。

以长度为 2 的整数数组`[index1, index2]`的形式返回这两个整数的下标`index1`和`index2`。

你可以假设每个输入 **只对应唯一的答案** ，而且你 **不可以** 重复使用相同的元素。

你所设计的解决方案必须只使用常量级的额外空间。

#### 思路分析

可以考虑使用对撞指针来减少时间复杂度。具体做法如下：

1. 使用两个指针`left`,`right`。`left`指向数组第一个值最小的元素位置,`right`指向数组值最大元素位置。
2. 判断两个位置上的元素的和与目标值的关系。
   1. 如果元素和等于目标值，则返回两个元素位置。
   2. 如果元素和大于目标值，则让`right`左移，继续检测。
   3. 如果元素和小于目标值，则让`left`右移，继续检测。
3. 直到`left`和`right`移动到相同位置停止检测。
4. 如果最终仍没找到，则返回`[-1, -1]`。

#### 参考解答

```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;
        
        while (left < right) {
            int total = numbers[left] + numbers[right];
            if (total == target) {
                return new int[]{left + 1, right + 1}; // 返回 1-based 索引
            } else if (total < target) {
                left++; // 总和小于目标值，移动左指针
            } else {
                right--; // 总和大于目标值，移动右指针
            }
        }
        
        return new int[]{-1, -1}; // 如果没有找到符合条件的组合
    }
}
```

### 1.5 举一反三

### 1.5.1 LC11 盛水最多的容器

#### 问题描述

给定一个长度为`n`的整数数组`height`。有`n`条垂线，第`i`条线的两个端点是`(i, 0)`和`(i, height[i])`。

找出其中的两条线，使得它们与`x`轴共同构成的容器可以容纳最多的水。

返回容器可以储存的最大水量。

**说明：** 你不能倾斜容器。

**示例**：


![](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)

```text
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

#### 思路分析

从示例中可以看出，如果确定好左右两端的直线，容纳的水量是由「左右两端直线中较低直线的高度 * 两端直线之间的距离」所决定的。所以我们应该使得「**左右两端的直线尽量高且距离尽可能远**」，这样才能使盛水面积尽可能的大。

可以使用对撞指针求解。移动较低直线所在的指针位置，从而得到不同的高度和面积，最终获取其中最大的面积。具体做法如下：

1. 使用两个指针`left`,`right`。`left`指向数组开始位置,`right`指向数组结束位置。
2. 计算`left`和`right`所构成的面积值，同时维护更新最大面积值。
3. 判断`left`和`right`的高度值大小。
   1. 如果`left`指向的直线高度比较低，则将`left`指针右移。
   2. 如果`right`指向的直线高度比较低，则将`right`指针左移。

4. 如果遇到`left == right`，跳出循环，最后返回最大的面积。

这里其实用到了贪心的思想，因为在每一步中，我们总是基于当前的**局部最优解**作出选择。

在本题中所说的局部最优解为“每次向里移动更短的那一条边“就是我们所说的局部最优解。

**为什么是这样？**

首先假设我们移动的是两边中更长的那一条边，那么移动之后底边的距离是一定缩短的，而长的一边（如上图为右边红色）的长度不管是变长还是变短，由于木桶短板效应，最终要乘的高度都不可能大于短的一边（如上图左边红色）的高，所以得到的新容器的容积一定是小于原容器的。

那既然移动长的得到容积一定更小，那想要得到容积变大的可能只能是移动更短的那一边，才有可能实现。

而通过对撞指针，刚好可以通过收窄两边的指针来寻找最优解，且从左右两边开始，过程中记录最值，可以保证没有漏掉最优解。

#### 参考解答

```java
public class Solution {
    public int maxArea(int[] height) {
        int left = 0;  // 左指针
        int right = height.length - 1;  // 右指针
        int ans = 0;  // 记录最大面积
        
        // 双指针从两端向中间移动
        while (left < right) {
            // 计算当前区域的面积
            int area = Math.min(height[left], height[right]) * (right - left);
            // 更新最大面积
            ans = Math.max(ans, area);
            
            // 移动较小的指针，寻找更高的边
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        return ans;  // 返回最大盛水面积
    }
}
```



### 1.5.2 LC881 救生艇

#### 问题描述

给定数组`people`。`people[i]`表示第`i`个人的体重 ，**船的数量不限**，每艘船可以承载的最大重量为`limit`。

每艘船最多可同时载两人，但条件是这些人的重量之和最多为`limit`。

返回 *承载所有人所需的最小船数* 。

#### 思路分析

我们也可以利用贪心算法的思想，让最重的和最轻的人一起走。这样一只船就可以尽可能的带上两个人。

具体做法如下：

1. **先对数组进行升序排序**，使用变量`ans`记录所需最小船只数量。

2. **使用两个指针**，`left`和`right`：
   - `left`指向数组的开始位置。
   - `right`指向数组的结束位置。

3. **判断`people[left]`和`people[right]`之和**：
   1. 如果`people[left] + people[right] > limit`，则让重的人（`right`）上船，船数量加 1，并令`right`左移，继续判断。
   2. 如果`people[left] + people[right] <= limit`，则两个人都可以上船，船数量加 1，并令`left`右移，`right`左移，继续判断。

4. **如果`left == right`**，则让最后一个人上船，船数量加 1，并返回答案。

#### 参考解答

```java
import java.util.Arrays;

public class Solution {
    public int numRescueBoats(int[] people, int limit) {
        // 先对 people 数组进行排序
        Arrays.sort(people);
        int left = 0;  // 左指针指向最轻的人
        int right = people.length - 1;  // 右指针指向最重的人
        int ans = 0;  // 记录所需的船数
        
        // 使用双指针法
        while (left < right) {
            // 如果最轻的和最重的两个人的重量之和大于 limit，则只能让最重的单独乘船
            if (people[left] + people[right] > limit) {
                right--;  // 最重的人自己一艘船
            } else {
                // 如果两个人可以一起乘船，则更新左右指针
                left++;
                right--;
            }
            ans++;  // 每次循环结束时，无论是单独还是一起，都需要一艘船
        }
        
        // 如果最后 left == right，表示还有一人没有乘船，需要加一艘船
        if (left == right) {
            ans++;
        }
        
        return ans;  // 返回总共需要的船数
    }
}
```

### 1.5.3 LC658 找到K个最接近的元素

#### 问题描述

给定一个 **排序好** 的数组`arr`，两个整数`k`和`x`，从数组中找到最靠近`x`（两数之差最小）的`k`个数。返回的结果必须要是按升序排好的。

整数`a`比整数`b`更接近`x`需要满足：

- `|a - x| < |b - x|`或者
- `|a - x| == |b - x|`且`a < b`

#### 思路分析

1.**初始化指针**

- 左指针`left`指向数组的开头（索引`0`）。
- 右指针`right`指向数组的末尾（索引`n-1`）。

2.**移动指针**

我们希望最终找到一段长度为`k`的子数组，其中元素距离`x`最接近。因此，在移动过程中要对比`arr[left]`和`arr[right]`与`x`的距离：

- 如果`arr[left]`与`x`的距离大于`arr[right]`与`x`的距离，说明右边的元素更接近`x`，因此应移动左指针`left++`，缩小左侧的搜索空间。
- 如果`arr[right]`与`x`的距离更远，说明左边的元素更接近`x`，因此应移动右指针`right--`，缩小右侧的搜索空间。

3.**停止条件**

当窗口中剩下的元素数量刚好为`k`时，停止移动指针，此时窗口中的元素就是我们要找的`k`个最接近`x`的元素。

#### 参考解答

```java
import java.util.*;

public class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int left = 0;
        int right = arr.length - 1;

        // 当区间长度大于 k 时，缩小区间
        while (right - left >= k) {
            // 比较两端的距离，移动较远的一端
            if (Math.abs(arr[left] - x) > Math.abs(arr[right] - x)) {
                left++;
            } else {
                right--;
            }
        }

        // 返回从 left 到 left + k 的 k 个元素，转为 List
        List<Integer> result = new ArrayList<>();
        for (int i = left; i < left + k; i++) {
            result.add(arr[i]);
        }

        return result;
    }
}
```

## 2 滑动窗口

在计算机网络中，滑动窗口协议（Sliding Window Protocol）是传输层进行流控的一种措施，接收方通过通告发送方自己的窗口大小，从而控制发送方的发送速度，从而达到防止发送方发送速度过快而导致自己被淹没的目的。我们所要讲解的滑动窗口算法也是利用了同样的特性。

> **滑动窗口算法（Sliding Window）**：在给定数组 / 字符串上维护一个固定长度或不定长度的窗口。可以对窗口进行滑动操作、缩放操作，以及维护最优解操作。

- **滑动操作**：窗口可按照一定方向进行移动。最常见的是向右侧移动。
- **缩放操作**：对于不定长度的窗口，可以从左侧缩小窗口长度，也可以从右侧增大窗口长度。

滑动窗口利用了双指针中的快慢指针技巧，我们可以将滑动窗口看做是快慢指针两个指针中间的区间，也可以将滑动窗口看做是快慢指针的一种特殊形式。

![滑动窗口](https://qcdn.itcharge.cn/images/202405092203225.png)

#### 滑动窗口适用范围

滑动窗口算法一般用来解决一些查找满足一定条件的连续区间的性质（长度等）的问题。该算法可以将一部分问题中的嵌套循环转变为一个单循环，因此它可以减少时间复杂度。

按照窗口长度的固定情况，我们可以将滑动窗口题目分为以下两种：

- **固定长度窗口**：窗口大小是固定的。
- **不定长度窗口**：窗口大小是不固定的。
  - 求解最大的满足条件的窗口。
  - 求解最小的满足条件的窗口。

### 2.1 固定长度滑动窗口

> **固定长度滑动窗口算法（Fixed Length Sliding Window）**：在给定数组 / 字符串上维护一个固定长度的窗口。可以对窗口进行滑动操作、缩放操作，以及维护最优解操作。

![固定长度滑动窗口](https://qcdn.itcharge.cn/images/202405092204712.png)

#### 固定长度滑动窗口算法步骤

1. 使用两个指针 `left` 和 `right`。初始时，`left` 和 `right` 都指向序列的第一个元素，即：`left = 0`，`right = 0`，区间 `[left, right]` 被称为一个「窗口」。

2. 当窗口未达到 `window_size` 大小时，不断移动 `right`，先将数组前 `window_size` 个元素填入窗口中，即 `window.add(nums[right])`。

3. 当窗口达到 `window_size` 大小时，即满足 `right - left + 1 >= window_size` 时，判断窗口内的连续元素是否满足题目限定的条件。
   1. 如果满足，再根据要求更新最优解。
   2. 然后向右移动 `left`，从而缩小窗口长度，即 `left++`，使得窗口大小始终保持为 `window_size`。

4. 向右移动 `right`，将元素填入窗口中，即 `window.add(nums[right])`。

5. 重复步骤 2 至 4，直到 `right` 到达数组末尾。


#### 固定长度滑动窗口代码模板

```java
import java.util.*;

public class Solution {
    public void slidingWindow(int[] nums, int windowSize) {
        int left = 0;
        int right = 0;
        List<Integer> window = new ArrayList<>(); // 用 ArrayList 来模拟窗口

        while (right < nums.length) {
            // 将当前元素加入窗口
            window.add(nums[right]);

            // 如果当前窗口的大小超过了规定的 windowSize，缩小窗口
            if (right - left + 1 > windowSize) {
                // 维护答案的逻辑可以放在这里
                window.remove(0);  // 移除窗口最左侧的元素
                left++;  // 移动左指针，缩小窗口
            }

            // 向右移动窗口
            right++;
        }
    }
}
```

### 2.2 例题讲解

### 2.2.1 LC1343 大小为 K 且平均值大于等于阈值的子数组数目

#### 问题描述

给你一个整数数组`arr`和两个整数`k`和`threshold`。

请你返回长度为`k`且平均值大于等于`threshold`的子数组数目。

#### 思路分析

这道题目是典型的固定窗口大小的滑动窗口题目。窗口大小为 `k`。具体做法如下：

1. `ans` 用来维护答案数目。 `windowSum` 用来维护窗口中元素的和。

2. `left` 和 `right` 都指向序列的第一个元素，即：`left = 0`，`right = 0`。

3. 向右移动 `right`，先将 `k` 个元素填入窗口中，即 `windowSum += arr[right]`。

4. 当窗口元素个数为 `k` 时，即满足 `right - left + 1 >= k` 时，判断窗口内的元素和平均值是否大于等于阈值 `threshold`。
    1. 如果满足，则答案数目加 `1`。
    2. 然后向右移动 `left`，从而缩小窗口长度，即 `left++`，使得窗口大小始终保持为 `k`。

5. 重复步骤 3 至 4，直到 `right` 到达数组末尾。

6. 最后输出答案数目。


#### 参考解答

```java
class Solution {
    public int numOfSubarrays(int[] arr, int k, int threshold) {
        int left = 0;
        int right = 0;
        int windowSum = 0;
        int ans = 0;

        // 滑动窗口遍历数组
        while (right < arr.length) {
            windowSum += arr[right]; // 将右边界的元素加入窗口

            // 检查窗口大小是否达到了 k
            if (right - left + 1 >= k) {
                // 判断当前窗口的平均值是否 >= threshold
                if (windowSum >= k * threshold) {
                    ans++; // 符合条件的子数组数加一
                }
                // 将左边界的元素移出窗口，缩小窗口
                windowSum -= arr[left];
                left++; // 移动左边界
            }

            right++; // 向右扩展窗口
        }

        return ans; // 返回满足条件的子数组的数量
    }
}
```

### 2.3 举一反三

### 2.3.1 LC1052 爱生气的书店老板

#### 问题描述

有一个书店老板，他的书店开了`n`分钟。每分钟都有一些顾客进入这家商店。给定一个长度为`n`的整数数组`customers`，其中`customers[i]`是在第`i`分钟开始时进入商店的顾客数量，所有这些顾客在第`i`分钟结束后离开。

在某些分钟内，书店老板会生气。 如果书店老板在第`i`分钟生气，那么`grumpy[i] = 1`，否则`grumpy[i] = 0`。

当书店老板生气时，那一分钟的顾客就会不满意，若老板不生气则顾客是满意的。

书店老板知道一个秘密技巧，能抑制自己的情绪，可以让自己连续`minutes`分钟不生气，但却只能使用一次。

请你返回 *这一天营业下来，最多有多少客户能够感到满意* 。

#### 思路分析

这是一个固定长度的滑动窗口问题。我们可以维护一个窗口大小为`minutes`的滑动窗口。使用`windowCount`记录当前窗口内生气的顾客人数。然后滑动求出窗口中最多的顾客数，最后累加上老板未生气时的顾客数，就是答案。具体做法如下：

1. 用`ans`来维护答案数目。`windowCount`用来维护窗口中生气的顾客人数。

2. `left`和`right`都指向序列的第一个元素，即：`left = 0`，`right = 0`。

3. 如果书店老板生气，则将这一分钟的顾客数量加入到`windowCount`中，然后向右移动`right`。

4. 当窗口元素个数大于`minutes`时，即：`right - left + 1 > count`时，如果最左边界老板处于生气状态，则向右移动`left`，从而缩小窗口长度，即`left++`，使得窗口大小始终保持小于`minutes`。

5. 重复步骤 3～4，直到`right`到达数组末尾。

6. 最后累加上老板未生气时的顾客数，最后输出答案。

#### 参考解答

```java
class Solution {
    public int maxSatisfied(int[] customers, int[] grumpy, int minutes) {
        int left = 0;
        int right = 0;
        int windowCount = 0;
        int ans = 0;

        // 滑动窗口，计算最多可以挽回的不满顾客数
        while (right < customers.length) {
            if (grumpy[right] == 1) {
                windowCount += customers[right]; // 不满意的情况下加上顾客数量
            }

            // 当窗口大小大于 minutes 时，开始缩小窗口
            if (right - left + 1 > minutes) {
                if (grumpy[left] == 1) {
                    windowCount -= customers[left]; // 左侧窗口移出不满意的顾客
                }
                left++; // 移动左边界
            }

            right++; // 移动右边界
            ans = Math.max(ans, windowCount); // 更新最大值
        }

        // 计算所有不受影响的满意顾客数量
        for (int i = 0; i < customers.length; i++) {
            if (grumpy[i] == 0) {
                ans += customers[i]; // 非不满的顾客数量直接计入结果
            }
        }

        return ans; // 返回最大满意顾客数量
    }
}

```

### 2.3.2 LC239 滑动窗口的最大值

#### 问题描述

给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

返回 *滑动窗口中的最大值*。

**示例：**

```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

#### 思路分析

**使用索引而不是值：** 我们使用 `window` 列表来存储数组中元素的**索引**，而不是直接存储元素值。通过这些索引，我们可以快速访问到数组中的元素值。

**保持 `window` 中的元素递减顺序：** 为了确保每次窗口滑动时都能快速得到最大值，我们在 `window` 中保存的索引对应的元素值是**递减的**。也就是说，`window` 中第一个元素（`window[0]`）对应的数组值总是当前窗口的最大值。

**每次新元素进入窗口时：**

- **移除超出范围的元素索引：** 如果窗口最左边的元素已经不在当前窗口范围内（超出了窗口的大小 `k`），我们就把它从 `window` 里移除。
- **移除比当前元素小的索引：** 如果当前元素比 `window` 中最后一个索引对应的元素值大，那么我们就把这些较小的元素索引移除，因为它们不可能再成为窗口中的最大值了。

#### 举例分析

假设 `nums = [1, 3, -1, -3, 5, 3, 6, 7]`，`k = 3`，即窗口大小为 3。

1. **开始时**，我们遍历数组，遇到 `1`，把它的索引 `0` 放入 `window`。
   - `window = [0]`，最大值是 `1`。
2. **遇到 `3`** 时，`3` 比 `1` 大，所以我们移除 `1` 的索引 `0`，然后把 `3` 的索引 `1` 放入 `window`。
   - `window = [1]`，最大值是 `3`。
3. **遇到 `-1`** 时，`-1` 小于 `3`，我们直接把 `-1` 的索引 `2` 放入 `window`，此时最大值仍然是 `3`。
   - `window = [1, 2]`，最大值是 `3`。
4. **窗口向右滑动**，当我们进入下一个元素时，如果 `window` 里的第一个索引已经超出了窗口的范围（即索引小于 `i - k`），我们就把它移除，确保 `window[0]` 总是当前窗口内的索引。

`window` 里面的元素数量不一定等于 `k`。`window` 中存储的是滑动窗口内的**元素索引**，并通过两个关键操作来确保它的正确性：

1. **移除超出当前窗口范围的元素**：`window` 中的第一个索引如果超出窗口范围（即已经不属于当前窗口的 `k` 个元素），就会被移除。
2. **保持单调递减顺序**：我们移除 `window` 里比当前元素小的元素索引，因此 `window` 里可能并不包含完整的 `k` 个元素。

#### 参考解答

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        List<Integer> window = new ArrayList<>();  // 用来存储当前窗口中的元素索引
        int[] result = new int[n - k + 1];  // 用于存储结果的数组
        int resultIndex = 0;

        for (int i = 0; i < n; i++) {
            // 移除窗口中不在范围内的元素（超出窗口大小k的）
            if (!window.isEmpty() && window.get(0) <= i - k) {
                window.remove(0);
            }

            // 移除窗口中所有小于当前元素的元素
            while (!window.isEmpty() && nums[window.get(window.size() - 1)] <= nums[i]) {
                window.remove(window.size() - 1);
            }

            // 将当前元素索引添加到窗口
            window.add(i);

            // 当窗口的大小达到k时，记录窗口的最大值
            if (i >= k - 1) {
                result[resultIndex++] = nums[window.get(0)];  // 窗口的第一个元素是最大值的索引
            }
        }

        return result;
    }
}
```

#### 关键解释

`window` 的长度不同于 `k`，但仍然属于**固定滑动窗口**。

##### 1. **窗口的大小是固定的：**

无论 `window` 列表中的元素个数是多少，我们在逻辑上始终处理一个大小为 `k` 的窗口。即便 `window` 列表中存储的索引数量可能少于 `k`，我们每次移动窗口时，都保证窗口覆盖数组的 `k` 个连续元素。

##### 2. **窗口的范围是固定的：**

每次处理新元素时，窗口总是包含 `k` 个连续的元素。例如，如果窗口大小 `k=3`，当遍历到第 `i` 个元素时，窗口对应的是 `nums[i-(k-1)]` 到 `nums[i]` 这 `k` 个元素。

##### 3. **`window` 列表和实际窗口不同：**

- **`window` 列表**：它只是用来存储可能成为当前窗口最大值的索引，因此它的长度是动态的。
- **实际滑动窗口**：逻辑上，窗口总是固定大小的，包含 `k` 个元素。我们只是通过 `window` 列表高效地找到当前窗口的最大值，而不是实际存储所有窗口中的元素。

#### 关键点：

- **固定滑动窗口**：窗口的大小始终是 `k`，每次只滑动一格。
- **`window` 列表长度不等于窗口大小**：`window` 列表只存储与计算最大值相关的索引，因此长度可能小于 `k`。

### 2.3.3 LC643 子数组最大平均数

#### 问题描述

给你一个由`n`个元素组成的整数数组`nums`和一个整数`k`。

请你找出平均数最大且 **长度为`k`** 的连续子数组，并输出该最大平均数。

任何误差小于`10^-5`的答案都将被视为正确答案。

#### 思路分析

1，**初始变量定义**：

- 用`ans`变量维持子数组的最大平均数，初始值为负无穷，即`Double.NEGATIVE_INFINITY`。
- 用`windowTotal`来维持窗口中元素的和。

2.**初始化指针**：

- `left`和`right`都指向数组的第一个元素，即：`left = 0`，`right = 0`。

3.**向右移动`right`指针**：

- 将`k`个元素填入窗口中。

4.**窗口元素数量为`k`时**：

- 当`right - left + 1 >= k`时，计算窗口内的元素和，并维护子数组的最大平均数。

5.**向右移动`left`指针**：

- 从而缩小窗口长度，即`left++`，使得窗口大小始终保持为`k`。

6.**重复步骤 4 到 5**：

- 直到`right`到达数组末尾。

7.**输出结果**：

- 最后输出答案`ans`。

#### 参考解答

```java
import java.util.List;

class Solution {
    public double findMaxAverage(List<Integer> nums, int k) {
        int left = 0;
        int right = 0;
        int windowTotal = 0;
        double ans = Double.NEGATIVE_INFINITY; // 初始化为负无穷

        while (right < nums.size()) {
            windowTotal += nums.get(right); // 添加当前元素到窗口总和

            // 当窗口大小达到 k
            if (right - left + 1 >= k) {
                ans = Math.max(windowTotal / (double) k, ans); // 计算平均值并更新最大值
                windowTotal -= nums.get(left); // 移除左边的元素
                left++; // 移动左边界
            }

            // 向右侧增大窗口
            right++;
        }

        return ans; // 返回最大平均值
    }
}
```

### 2.4 不定长度滑动窗口

> **不定长度滑动窗口算法（Sliding Window）**：在给定数组 / 字符串上维护一个不定长度的窗口。可以对窗口进行滑动操作、缩放操作，以及维护最优解操作。

![不定长度滑动窗口](https://qcdn.itcharge.cn/images/202405092206553.png)

#### 不定长度滑动窗口算法步骤

1. 使用两个指针`left`、 `right`。初始时,`left`、 `right`都指向序列的第一个元素。即：`left = 0`,`right = 0`，区间`[left, right]`被称为一个「窗口」。
2. 将区间最右侧元素添加入窗口中，即`window.add(nums[right])`。
3. 然后向右移动`right`，从而增大窗口长度，即`right++`。直到窗口中的连续元素满足要求。
4. 此时，停止增加窗口大小。转向不断将左侧元素移出窗口，即`window.remove(s[left])`。
5. 然后向右移动`left`，从而缩小窗口长度，即`left++`。直到窗口中的连续元素不再满足要求。
6. 重复 2 ~ 5 步，直到`right`到达序列末尾。

#### 不定长度滑动窗口代码模板

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int slidingWindowExample(int[] nums) {
        int left = 0;
        int right = 0;
        List<Integer> window = new ArrayList<>(); // 用于存储窗口中的元素
        int answer = 0; // 用于维护答案

        while (right < nums.length) {
            window.add(nums[right]); // 向窗口添加右边的元素

            // 当窗口需要缩小时
            while (需要缩小窗口的条件) {
                // 维护答案，例如更新最大值
                answer = Math.max(answer, calculateSomeValue(window));

                window.remove(0); // 移除窗口的第一个元素
                left++; // 移动左边界
            }

            // 向右侧增大窗口
            right++;
        }

        return answer; // 返回维护的答案
    }
}
```

### 2.5 例题讲解

### 2.5.1 LC209 长度最小的子数组

#### 问题描述

给定一个含有`n`个正整数的数组和一个正整数`target`。

找出该数组中满足其总和大于等于`target`的长度最小的子数组:
[nums<sub>l</sub>, nums<sub>l+1</sub>, ..., nums<sub>r-1</sub>, nums<sub>r</sub>]

并返回其长度。如果不存在符合条件的子数组，返回`0`。

#### 思路分析

用滑动窗口来记录连续子数组的和，设定两个指针：`left` 和 `right`，分别指向滑动窗口的左右边界，保证窗口中的和刚好大于等于 `target`。

1. 一开始，`left` 和 `right` 都指向 `0`。

2. 向右移动 `right`，将最右侧元素加入当前窗口和 `windowSum` 中。

3. 如果 `windowSum >= target`，则不断右移 `left`，缩小滑动窗口长度，并更新窗口和的最小值，直到 `window_sum < target`。

4. 然后继续右移 `right`，直到 `right >= nums.size()` 结束。

5. 输出窗口和的最小值作为答案。

#### 参考解答

```java
import java.util.List;

class Solution {
    public int minSubArrayLen(int target, List<Integer> nums) {
        int size = nums.size();
        int ans = size + 1; // 初始设为一个大于可能的长度
        int left = 0; // 左指针
        int right = 0; // 右指针
        int windowSum = 0; // 当前窗口的总和

        while (right < size) {
            windowSum += nums.get(right); // 将右指针的元素加入窗口总和

            // 当窗口总和大于或等于目标时
            while (windowSum >= target) {
                ans = Math.min(ans, right - left + 1); // 更新答案
                windowSum -= nums.get(left); // 从窗口中移除左指针的元素
                left++; // 左指针向右移动
            }

            right++; // 右指针向右移动
        }

        return ans != size + 1 ? ans : 0; // 如果未更新答案，返回 0
    }
}

```

### 2.6 举一反三

### 2.6.1 LC713 乘积小于K的子数组

#### 问题描述

给你一个整数数组`nums`和一个整数`k`，请你返回子数组内所有元素的乘积严格小于`k`的连续子数组的数目。

#### 思路分析

滑动窗口（不定长度）

1. 设定两个指针：`left` 和 `right`，分别指向滑动窗口的左右边界，保证窗口内所有数的乘积 `windowProduct` 都小于 `k`。使用 `windowProduct` 记录窗口中的乘积值，使用 `count` 记录符合要求的子数组个数。

2. 一开始，`left` 和 `right` 都指向 `0`。

3. 向右移动 `right`，将最右侧元素加入当前子数组乘积 `windowProduct` 中。

4. 如果 `windowProduct >= k`，则不断右移 `left`，缩小滑动窗口长度，并更新当前乘积值 `windowProduct` 直到 `windowProduct < k`。

5. 记录累积答案个数加 `1`，继续右移 `right`，直到 `right >= nums.length` 结束。

6. 输出累积答案个数。


#### 参考解答

```java
public class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        // 步骤1：初始化指针和变量
        int left = 0; // 左指针
        int right = 0; // 右指针
        int count = 0; // 记录符合要求的子数组个数
        int windowProduct = 1; // 记录当前窗口的乘积值

        // 步骤2：开始遍历数组
        while (right < nums.length) {
            // 步骤3：将最右侧元素加入当前子数组乘积
            windowProduct *= nums[right];

            // 步骤4：检查乘积是否满足条件
            while (windowProduct >= k && left <= right) {
                windowProduct /= nums[left]; // 更新当前乘积
                left++; // 缩小滑动窗口长度
            }

            // 步骤5：记录符合要求的子数组个数
            count += right - left + 1; // 所有子数组数量等于窗口的长度
            right++; // 向右移动右指针
        }

        // 步骤6：返回累积答案个数
        return count;
    }
}

```

### 2.6.2 LC424 替换后的最长重复字符

#### 问题描述

给你一个字符串 `s` 和一个整数 `k` 。你可以选择字符串中的任一字符，并将其更改为任何其他大写英文字符。该操作最多可执行 `k` 次。

在执行上述操作后，返回 *包含相同字母的最长子字符串的长度。*

#### 思路分析

1. 使用 `counts` 数组来统计字母频数。使用 `left`、`right` 双指针分别指向滑动窗口的首尾位置，使用 `max_count` 来维护最长子串的长度。
2. 不断右移 `right` 指针，增加滑动窗口的长度。
3. 对于当前滑动窗口的子串，如果当前窗口的间距 > 当前出现最大次数的字符的次数 + k 时，意味着替换 k 次仍不能使当前窗口中的字符全变为相同字符，则此时应该将左边界右移，同时将原先左边界的字符频次减少。

### 具体案例

假设 `s = "AABABBA"`, `k = 1`，我们需要找出在允许最多 `1` 个字符替换的情况下，窗口内能够包含相同字符的最大长度。

#### 1. **初始情况**：
- 我们从左边界 `left = 0` 和右边界 `right = 0` 开始。
- `max_count = 1`，即当前窗口中出现次数最多的字符 `A` 出现了 1 次。

#### 2. **逐渐扩展窗口**：
- **扩展到 `right = 1`** 时，窗口变为 `AA`。窗口内出现最多的字符 `A` 出现了 2 次，因此 `max_count = 2`。
   - 窗口大小减去 `max_count` 为 `2 - 2 = 0`，小于等于 `k`（即 `k = 1`），所以我们不缩小窗口。

- **扩展到 `right = 2`** 时，窗口变为 `AAB`。此时出现最多的字符 `A` 出现了 2 次，`max_count` 仍然是 2。
   - 窗口大小减去 `max_count` 为 `3 - 2 = 1`，等于 `k`，仍然不需要缩小窗口。

#### 3. **窗口不再满足条件，缩小窗口**：
- **扩展到 `right = 4`** 时，窗口变成 `AABAB`。此时 `A` 仍然是出现次数最多的字符，`max_count = 2`，但窗口大小是 5。`5 - 2 = 3`，超过了 `k = 1`。
   - 这时必须缩小窗口，将 `left` 向右移动，移除最左边的 `A`，窗口变成 `ABAB`。
   - 移除一个 `A` 后，`max_count` 暂时没有变化，因为窗口中还有其他 `A` 存在。

#### 4. **继续扩展窗口**：
- 在右边界继续扩展时，`max_count` 会根据新窗口的字符动态更新，即使移除掉当前最大频次的字符，也不影响结果。

#### 5. **结果计算**：
- 返回窗口的最大长度，即 `right - left + 1`，这是满足条件的窗口的最大长度。

#### 参考解答

```java
class Solution {
    public int characterReplacement(String s, int k) {
        int[] counts = new int[26];  // 统计窗口中各字符的出现次数
        int maxCount = 0;  // 当前窗口中出现次数最多的字符的次数
        int left = 0;  // 窗口的左边界
        int maxLength = 0;  // 记录最大窗口长度

        // 使用滑动窗口遍历字符串
        for (int right = 0; right < s.length(); right++) {
            int index = s.charAt(right) - 'A';  // 将字符转换为0-25的索引
            counts[index]++;  // 增加当前字符的计数
            maxCount = Math.max(maxCount, counts[index]);  // 更新最大出现次数

            // 如果当前窗口大小减去出现最多的字符次数大于k，说明需要缩小窗口
            if (right - left + 1 - maxCount > k) {
                counts[s.charAt(left) - 'A']--;  // 移除左边字符的计数
                left++;  // 左边界右移，缩小窗口
            }

            // 更新最大窗口长度
            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;  // 返回最大窗口长度
    }
}
```

### 2.6.3 LC1658 将x减到0的最小操作数

#### 问题描述

给你一个整数数组`nums`和一个整数`x`。每一次操作时，你应当移除数组`nums`最左边或最右边的元素，然后从`x`中减去该元素的值。请注意，需要 **修改** 数组以供接下来的操作使用。

如果可以将`x`**恰好** 减到`0`，返回 **最小操作数** ；否则，返回`-1`。

#### 思路分析

1.**定义目标值**

设定 `target` 为 `nums` 内所有元素之和减去 `x`，意图找到和为 `target` 的最长连续子数组。

2.**初始化变量**

- `windowSum` 用于记录滑动窗口内元素的和。
- `maxLen` 用于跟踪和等于 `target` 的最长子数组长度。
- `left` 和 `right` 初始化为 `0`，用于标识滑动窗口的边界。

3.**滑动窗口操作**

- **增加右侧元素**：向右移动 `right` 指针，扩大窗口，更新 `windowSum`。
- **调整左侧边界**：当 `windowSum > target` 时，逐步右移 `left`，缩小窗口，直到 `windowSum <= target`。
- **检查窗口和**：如果 `windowSum == target`，更新 `maxLen`。
- 继续此过程直到 `right` 越过数组末端。

4.**计算结果**

输出 `size - maxLen`，代表需要移除的最少元素数量以达到除了最长和为 `target` 子数组外的元素。

#### 参考代码

```java
import java.util.List;

class Solution {
    public int minOperations(List<Integer> nums, int x) {
        // 计算数组元素的总和
        int target = 0;
        for (int num : nums) {
            target += num;
        }
        target -= x; // 调整目标为剩余需要达到的和

        int size = nums.size();
        if (target < 0) {
            return -1; // 如果目标小于0，说明无法达到
        }
        if (target == 0) {
            return size; // 如果目标为0，说明需要移除所有元素
        }

        int left = 0, right = 0;
        int windowSum = 0; // 当前窗口的和
        int maxLen = Integer.MIN_VALUE; // 初始化最大子数组长度为负无穷

        // 使用滑动窗口
        while (right < size) {
            windowSum += nums.get(right); // 将当前元素添加到窗口和中

            // 当窗口和大于目标时，收缩窗口左边界
            while (windowSum > target) {
                windowSum -= nums.get(left);
                left++;
            }
            // 如果当前窗口和等于目标，更新最大长度
            if (windowSum == target) {
                maxLen = Math.max(maxLen, right - left + 1);
            }
            right++; // 移动右指针以扩大窗口
        }

        // 返回最小操作数：数组总大小减去最大长度；若无有效子数组则返回-1
        return maxLen != Integer.MIN_VALUE ? size - maxLen : -1;
    }
}
```

## 3 课后练习


#### 对撞指针

| 题目编号 | 题目名称         | 题目描述                                             |
| -------- | ---------------- | ---------------------------------------------------- |
| 15       | 三数之和         | 判断整数数组是否存在三元组满足条件。                 |
| 16       | 最接近的三数之和 | 找出数组中三个数之和最接近目标值的组合。             |
| 18       | 四数之和         | 在数组中找出四个数，使得它们的和等于目标值。         |
| 977      | 有序数的平方     | 返回非递减顺序的每个数的平方组成的新数组。           |
| 611      | 有效三角形的个数 | 返回非负整数的数组可以组成三角形三条边的三元组个数。 |

#### 固定长度滑动窗口

| 题目编号 | 题目名称                   | 题目描述                                                     |
| -------- | -------------------------- | ------------------------------------------------------------ |
| 1423     | 可获得的最大点数           | 从数组两端选择一定数量的元素，求最大点数。                   |
| 1456     | 定长子串中元音的最大数目   | 找出定长子串中包含最多元音字母的子串。                       |
| 1151     | 最少交换次数来组合所有的 1 | 通过交换位置，将数组中任何位置上的1组合到一起返回所有可能中所需的最少交换次数。 |
| 1100     | 长度为 K 的无重复字符子串  | 找出所有长度为k且不含重复字符的子串，返回全部满足要求的子串的数目。 |
| 567      | 字符串的排列               | 判断 `s2` 是否包含 `s1` 的排列。                             |

#### 不定长度滑动窗口

| 题目编号 | 题目名称                          | 题目描述                                                     |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 1695     | 删除子数组的最大得分              | 删除子数组，使得剩余元素的和最大。                           |
| 795      | 区间子数组个数                    | 计算满足条件的子数组的数量。                                 |
| 718      | 最长重复子数组                    | 给两个数组返回公共最长子数组长度。                           |
| 904      | 水果成篮                          | 给一个整数数组返回手机水果的最大数目。                       |
| 1493     | 删掉一个元素以后全为1的最长子数组 | 删掉元素的结果数组中，返回最长的且只包含 1 的非空子数组的长度。 |
