# Lesson 15: 前缀和与差分数组

## 目录
- [1. 前缀和（Prefix Sum）](#1-前缀和prefix-sum)
- [2. 差分数组（Difference Array）](#2-差分数组difference-array)
- [3. 例题讲解](#3-例题讲解)
    - [3.1 前缀和例题](#31-前缀和例题)
        - [3.1.1 LC303 区域和检索 - 数组不可变](#311-lc303-区域和检索---数组不可变)
    - [3.2 差分数组例题](#32-差分数组例题讲解)
        - [3.2.1 LC2848 与车相交的点](#321-lc2848-与车相交的点)
      
- [4. 举一反三](#4-举一反三)
    - [4.1 前缀和举一反三](#41-前缀和举一反三)
        - [4.1.1 LC724 寻找数组的中心下标](#411-lc724-寻找数组的中心下标)
        - [4.1.2 LC1588 所有奇数长度子数组的和](#412-lc1588-所有奇数长度子数组的和)
        - [4.1.3 LC1732 找到最高海拔](#413-lc1732-找到最高海拔)
    - [4.2 差分数组举一反三](#42-差分数组举一反三)
        - [4.2.1 LC1094 拼车](#421-lc1094-拼车)
        - [4.2.2 LC1854 人口最多的年份](#422-lc1854-人口最多的年份)
        - [4.2.3 LC1450 在既定时间做作业的学生人数](#423-lc1450-在既定时间做作业的学生人数)
- [5. 课后练习](#5-课后练习)

---

## 1. 前缀和（Prefix Sum）

### 定义
前缀和是一种常用的算法技巧，用来快速计算数组中任意区间的元素之和。前缀和数组的每个元素表示原数组从起点到该位置的元素和。通过使用前缀和，可以在常数时间内高效计算任意区间的和，而不需要每次都重新遍历数组。

给定一个长度为 `n` 的数组 `A`，前缀和数组 `P` 的定义如下：

- `P[i] = A[0] + A[1] + ... + A[i]`，对于所有 `i` 在区间 `[0, n-1]` 内。

### 构建前缀和数组
构建前缀和数组的时间复杂度是 `O(n)`，因为我们只需要遍历一遍数组即可计算出所有前缀和。按照这个思路，代码如下：

```java
public static int[] prefixSum(int[] arr) {
    int n = arr.length;
    int[] prefix = new int[n];  // 前缀和数组与原数组同长度

    // 初始化第一个元素
    prefix[0] = arr[0];  // 第一个前缀和就是数组的第一个元素

    // 构建前缀和数组
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + arr[i];  // P[i] = P[i-1] + A[i]
    }
    return prefix;
}

// 计算区间和 [i, j]
public static int rangeSum(int[] prefix, int i, int j) {
    return prefix[j] - prefix[i - 1];
}
```
### 思考：这段代码有没有什么问题

#### 数组越界
对于：
```java
return prefix[j] - prefix[i - 1];
```

当计算区间和 [0, j]，即i = 0 时，数组会越界。

#### 解决方式：添加条件判断
```java
public static int[] prefixSum(int[] arr) {
    int n = arr.length;
    int[] prefix = new int[n];  // 前缀和数组与原数组同长度

    // 初始化第一个元素
    prefix[0] = arr[0];  // 第一个前缀和就是数组的第一个元素

    // 构建前缀和数组
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + arr[i];  // P[i] = P[i-1] + A[i]
    }
    return prefix;
}

// 计算区间和 [i, j]
public static int rangeSum(int[] prefix, int i, int j) {
    if (i == 0) {
        return prefix[j];  // 当 i = 0 时，直接返回 prefix[j]
    } else {
        return prefix[j] - prefix[i - 1];  // 否则，使用 prefix[j] - prefix[i-1]
    }
}
```
### 思考：有没有更好的解决方式

#### 构建前缀和数组时多开一格
```java
 // 构建前缀和数组，前缀和数组多一格，并使P[0] = 0
public static int[] prefixSum(int[] arr) {
    int n = arr.length;
    int[] prefix = new int[n + 1];  // 前缀和数组比原数组多一位
    prefix[0] = 0;  // P[0] = 0

    // 构建前缀和数组
    for (int i = 1; i <= n; i++) {
        prefix[i] = prefix[i - 1] + arr[i - 1];  // P[i] = P[i-1] + A[i-1]
    }
    return prefix;
}
```

### 总结：`prefixSum` 多开一格的原因与好处

#### 避免边界问题：

假设你不多开一格，并且前缀和数组 `prefix[i]` 表示 `arr[0]` 到 `arr[i]` 的和，那么对于区间 `[i, j]` 的和，你需要计算：

- `区间和 [i, j] = prefix[j] - prefix[i-1]`

但此时，如果 `i = 0`，就会出现 `prefix[-1]` 访问越界的问题。为了避免每次都要额外判断 `i = 0` 的情况，可以通过多开一格，让 `prefix[0] = 0`，从而使得：

- `区间和 [0, j] = prefix[j + 1] - prefix[0]`

这样，即使 `i = 0` 时，也不用特别判断，直接套用通用公式 `prefix[j + 1] - prefix[i]`，从而避免越界问题。

### 代码实现

```java
// 构建前缀和数组，前缀和数组多开一格，P[0] = 0
public static int[] prefixSum(int[] arr) {
    int n = arr.length;
    int[] prefix = new int[n + 1];  // 前缀和数组比原数组多一位
    prefix[0] = 0;  // P[0] = 0，表示空前缀的和

    // 构建前缀和数组
    for (int i = 1; i <= n; i++) {
        prefix[i] = prefix[i - 1] + arr[i - 1];  // P[i] = P[i-1] + A[i-1]
    }
    return prefix;
}

// 计算区间和 [i, j]
public static int rangeSum(int[] prefix, int i, int j) {
    return prefix[j + 1] - prefix[i];
}
```

### 示例解释

假设我们有一个数组 `arr = {1, 2, 3, 4}`，对应的前缀和数组 `prefix` 为：

```
arr:     1   2   3   4
prefix:  0   1   3   6   10
```

- `prefix[1] = 1` 表示 `arr[0]` 的和为 1。
- `prefix[2] = 3` 表示 `arr[0] + arr[1]` 的和为 3。
- `prefix[3] = 6` 表示 `arr[0] + arr[1] + arr[2]` 的和为 6。
- `prefix[4] = 10` 表示 `arr[0] + arr[1] + arr[2] + arr[3]` 的和为 10。

要计算区间 `[i, j]` 的和，比如 `[1, 3]`，我们直接用公式：

```
区间和 [1, 3] = prefix[4] - prefix[1] = 10 - 1 = 9
```

这是因为 `arr[1] + arr[2] + arr[3] = 2 + 3 + 4 = 9`。


### 优点
- **高效查询**：对于频繁的区间和查询，前缀和可以在 `O(1)` 的时间内给出结果。
- **简洁**：前缀和的概念简单易用，可以用于多种场景。

### 缺点
- **空间消耗**：需要额外的数组存储前缀和，会占用额外的空间。


## 2. 差分数组（Difference Array）

### 定义
差分数组是一种快速处理数组区间更新的技巧。它能够在常数时间内对数组的区间进行加减操作，并在最终需要时构建出原始数组的结果。

给定一个数组 `A`，其差分数组 `D` 定义如下：

- `D[0] = A[0]`
- `D[i] = A[i] - A[i-1]`，对于所有 `i` 在区间 `[1, n-1]` 内。

也就是说，差分数组的每个元素表示原数组相邻元素之间的差。

### 构建差分数组
构建差分数组的时间复杂度是 `O(n)`，因为我们只需要遍历一遍原数组即可计算差分数组。代码如下：

```java
public static int[] buildDifferenceArray(int[] arr) {
    int n = arr.length;
    int[] diff = new int[n];
    diff[0] = arr[0];  // 差分数组的第一个元素等于原数组的第一个元素

    for (int i = 1; i < n; i++) {
        diff[i] = arr[i] - arr[i - 1];  // 计算差分
    }

    return diff;
}
```

### 更新区间
差分数组的一个强大之处在于，可以在常数时间内对原数组的一个区间 `[l, r]` 进行加 `x` 操作。具体方法如下：

- `D[l] += x` （表示从 `l` 开始加 `x`）
- 如果 `r + 1 < n`，则 `D[r + 1] -= x` （表示从 `r + 1` 开始减去 `x`，恢复后续不受影响）

### 恢复原数组
在完成所有区间操作后，可以通过前缀和的方式恢复原数组。恢复操作的时间复杂度为 `O(n)`，伪代码如下：

```java
public static int[] recoverArrayFromDifference(int[] diff) {
    int n = diff.length;
    int[] arr = new int[n];
    arr[0] = diff[0];  // 原数组的第一个元素

    for (int i = 1; i < n; i++) {
        arr[i] = arr[i - 1] + diff[i];  // 通过累加差分数组恢复原数组
    }

    return arr;
}
```

### 示例
假设有一个数组 `A = {2, 5, 7, 11, 15}`，构建它的差分数组 `D`：

- `D[0] = 2`
- `D[1] = 5 - 2 = 3`
- `D[2] = 7 - 5 = 2`
- `D[3] = 11 - 7 = 4`
- `D[4] = 15 - 11 = 4`

因此差分数组为 `D = {2, 3, 2, 4, 4}`。

如果要对区间 `[1, 3]` 加 `2`，那么：

- `D[1] += 2`，差分数组变为 `D = {2, 5, 2, 4, 4}`
- `D[4] -= 2`，差分数组变为 `D = {2, 5, 2, 4, 2}`

最终通过前缀和可以恢复出修改后的数组。

### 参考代码

```java
public class DifferenceArrayExample {

    // 构建差分数组
    public static int[] buildDifferenceArray(int[] arr) {
        int n = arr.length;
        int[] diff = new int[n];
        diff[0] = arr[0];  // 差分数组的第一个元素等于原数组的第一个元素

        for (int i = 1; i < n; i++) {
            diff[i] = arr[i] - arr[i - 1];  // 计算差分
        }

        return diff;
    }

    // 对区间 [l, r] 加上 x
    public static void updateRange(int[] diff, int l, int r, int x) {
        diff[l] += x;  // 在 l 位置加 x
        if (r + 1 < diff.length) {
            diff[r + 1] -= x;  // 在 r+1 位置减 x，确保后续不受影响
        }
    }

    // 通过差分数组恢复原数组
    public static int[] recoverArrayFromDifference(int[] diff) {
        int n = diff.length;
        int[] arr = new int[n];
        arr[0] = diff[0];  // 原数组的第一个元素

        for (int i = 1; i < n; i++) {
            arr[i] = arr[i - 1] + diff[i];  // 通过累加差分数组恢复原数组
        }

        return arr;
    }

    public static void main(String[] args) {
        int[] A = {2, 5, 7, 11, 15};
        int[] D = buildDifferenceArray(A);

        // 对区间 [1, 3] 加上 2
        updateRange(D, 1, 3, 2);

        // 恢复修改后的原数组
        int[] updatedA = recoverArrayFromDifference(D);

        // 输出恢复后的数组
        for (int num : updatedA) {
            System.out.print(num + " ");  // 输出结果应为 2 7 9 13 15
        }
    }
}
```

### 优点
- **高效更新**：可以在 `O(1)` 的时间内对数组的区间进行加减操作，适用于需要频繁更新的场景。
- **简单恢复**：通过一次遍历即可恢复原数组，时间复杂度为 `O(n)`。

### 缺点
- **只适用于加减操作**：差分数组只能处理加减更新，无法用于乘法或其他复杂操作。
- **额外的空间消耗**：需要存储一个与原数组大小相同的差分数组。


## 3. 例题讲解

## 3.1 前缀和

## 3.1.1 LC303 区域和检索 - 数组不可变

### 题目描述
给定一个整数数组 `nums`，处理以下类型的多个查询:

计算索引 `left` 和 `right`（包含 `left` 和 `right`）之间的 `nums` 元素的和，其中 `left` <= `right`

实现 NumArray 类：
- NumArray(int[] nums) 使用数组 `nums` 初始化对象
- int sumRange(int i, int j) 返回数组 `nums` 中索引 `left` 和 `right` 之间的元素的总和 ，包含 `left` 和 `right` 两点（也就是 nums[left] + nums[left + 1] + ... + nums[right] )

### 解题思路

我们可以通过 **前缀和** 的方式优化计算多个区间的和。通过构建一个前缀和数组，我们可以快速求出任意区间的和。

### 前缀和数组定义

对于给定的数组 `nums`，我们构建一个前缀和数组 `prefixSum`，其中 `prefixSum[i]` 表示数组 `nums` 从第 0 项到第 i 项的元素之和。

用公式表示为：
- `prefixSum[i] = nums[0] + nums[1] + ... + nums[i]`

### 如何计算区间和

要计算 `nums[i]` 到 `nums[j]` 之间的和，可以通过前缀和数组来实现：
- `sumRange(i, j) = prefixSum[j + 1] - prefixSum[i]`

注意这里的 `prefixSum[j + 1]` 是为了处理数组的边界问题，使得计算区间和时只需简单的减法。

### 步骤：
1. 构建前缀和数组 `prefixSum`。
2. 对于每次查询，使用 `prefixSum` 数组计算出区间和。

### 参考解答

```java
class NumArray {
    private int[] prefixSum;  // 用于存储前缀和

    // 构造函数，初始化前缀和数组
    public NumArray(int[] nums) {
        int n = nums.length;
        prefixSum = new int[n + 1];  // 创建前缀和数组，多开一格用于处理边界情况
        prefixSum[0] = 0;  // 第一个元素为 0，表示没有元素时的和
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];  // 构建前缀和
        }
    }

    // 查询区间和，使用前缀和数组计算
    public int sumRange(int left, int right) {
        return prefixSum[right + 1] - prefixSum[left];  // 区间和等于 prefixSum[right + 1] - prefixSum[left]
    }
}
```

### 示例

以数组 `nums = [-2, 0, 3, -5, 2, -1]` 为例，前缀和数组 `prefixSum` 如下：

- `prefixSum[0] = 0`
- `prefixSum[1] = -2`
- `prefixSum[2] = -2`
- `prefixSum[3] = 1`
- `prefixSum[4] = -4`
- `prefixSum[5] = -2`
- `prefixSum[6] = -3`

查询示例：
- `sumRange(0, 2)` 返回 `1`，即 `prefixSum[3] - prefixSum[0] = 1 - 0 = 1`
- `sumRange(2, 5)` 返回 `-1`，即 `prefixSum[6] - prefixSum[2] = -3 - (-2) = -1`
- `sumRange(0, 5)` 返回 `-3`，即 `prefixSum[6] - prefixSum[0] = -3 - 0 = -3`


## 3.2 差分数组例题讲解

## 3.2.1 LC2848 与车相交的点
### 问题描述

给定一个下标从 0 开始的二维整数列表 `nums`，其中 `nums[i] = [start_i, end_i]` 表示第 `i` 辆车在数轴上占据的区间 `[start_i, end_i]`。需要返回数轴上被**至少一辆车覆盖的整数点的数目**。

### 解题思路

我们可以使用**差分数组**来高效解决这个问题。差分数组是解决区间更新和查询问题的常用技巧，它可以帮助我们快速计算区间上的变化和覆盖情况。

### 具体步骤：

1. **寻找数轴的最大端点**：
   由于给定的区间终点可能不同，为了高效地构建差分数组，我们首先要找到所有区间中的最大端点 `C`。这样，我们只需考虑 `1` 到 `C` 之间的点。

2. **构建差分数组**：
    - 初始化一个长度为 `C + 2` 的差分数组 `diff`，其中 `diff[i]` 表示点 `i` 处开始被覆盖的次数变化，`diff[i + 1]` 表示结束覆盖的变化。
    - 对于每个区间 `[start_i, end_i]`，在 `diff[start_i]` 位置增加 `1`，在 `diff[end_i + 1]` 位置减去 `1`。这表明区间 `[start_i, end_i]` 内的所有点被覆盖。

3. **构建前缀和**：
    - 遍历差分数组 `diff`，逐步累加，得到前缀和数组。前缀和数组中，每个位置的值表示该点被覆盖的次数。如果前缀和值大于 `0`，说明该点被至少一辆车覆盖。

4. **统计被覆盖的点数**：
    - 遍历前缀和数组，统计所有被覆盖的点，即前缀和大于 `0` 的点。


### 特别注意：为什么需要 `C + 2` 的长度

当处理到某个区间 `[start, end]` 时，我们在 `end + 1` 位置进行减 `1` 操作，这就需要确保 `end + 1` 在差分数组的范围内，防止越界。因此，我们在初始化差分数组时，需要为 `C + 1` 和 `C + 2` 留出空间。

#### 案例分析

假设我们有如下区间输入：

```plaintext
nums = [[1, 3], [2, 5], [4, 6]]
```

1. **寻找最大终点 `C`**：
    - 通过遍历 `nums`，我们可以发现最大终点 `C` 为 `6`。

2. **构建差分数组**：
    - 初始化一个差分数组 `diff`，长度为 `C + 2 = 8`，即 `diff[0]` 到 `diff[7]`。

3. **差分数组填充过程**：
    - 对于第一个区间 `[1, 3]`：
        - `diff[1] += 1` （从 `1` 开始覆盖）
        - `diff[4] -= 1` （从 `4` 位置不再覆盖）
    - 对于第二个区间 `[2, 5]`：
        - `diff[2] += 1` （从 `2` 开始覆盖）
        - `diff[6] -= 1` （从 `6` 位置不再覆盖）
    - 对于第三个区间 `[4, 6]`：
        - `diff[4] += 1` （从 `4` 开始覆盖）
        - `diff[7] -= 1` （从 `7` 位置不再覆盖）

可以发现，对于本题而言，需要 `C + 2` 大小的数组才不会发生越界的情况。

### 参考解答

```java
import java.util.List;

class Solution {
    public int numberOfPoints(List<List<Integer>> nums) {
        int C = 0;
        
        // 找出最大终点 C
        for (List<Integer> interval : nums) {
            C = Math.max(C, interval.get(1));
        }

        // 差分数组，长度为 C + 2，避免越界
        int[] diff = new int[C + 2];
        // 构建差分数组
        for (List<Integer> interval : nums) {
            int start = interval.get(0);    // 区间起始点
            int end = interval.get(1);      // 区间结束点

            // 标记区间的开始：从 'start' 位置开始，覆盖的点加 1
            diff[start] += 1;

            // 标记区间的结束：'end + 1' 位置不再覆盖，因此减 1
            diff[end + 1] -= 1;
        }
        
        int ans = 0, count = 0;
        
        // 计算前缀和，统计被覆盖的点数
        for (int i = 1; i <= C; ++i) {
            count += diff[i];  // 前缀和
            if (count > 0) {
                ++ans;  // 如果被覆盖，计数加 1
            }
        }
        
        return ans;
    }
}
```

### 解释

1. **寻找最大终点 `C`**：
    - 遍历输入列表 `nums`，找到所有区间中的最大终点。这样我们只需要处理从 `1` 到 `C` 范围内的点。

2. **构建差分数组**：
    - 对于每个区间 `[start_i, end_i]`，在 `diff[start_i]` 位置加 `1`，表示从 `start_i` 开始有车覆盖；在 `diff[end_i + 1]` 位置减 `1`，表示从 `end_i + 1` 以后不再有覆盖。

3. **计算前缀和**：
    - 遍历差分数组 `diff`，逐点累加前缀和。每个点的前缀和表示该点被覆盖的车的数量。若前缀和大于 `0`，说明该点被至少一辆车覆盖。

4. **统计被覆盖的点数**：
    - 统计前缀和大于 `0` 的点，即为被车覆盖的整数点。

## 4. 举一反三
## 4.1 前缀和举一反三

## 4.1.1 LC724 寻找数组的中心下标

### 题目描述

给定一个整数数组 `nums`，请计算并返回数组的**中心下标**。数组的中心下标是满足以下条件的一个下标 `i`：

- `nums[0] + nums[1] + ... + nums[i-1] = nums[i+1] + nums[i+2] + ... + nums[n-1]`，即 `i` 左边元素的和等于右边元素的和。

- 如果中心下标位于数组的最左端，那么左侧的和视为 0，因为下标左边没有元素；同样地，如果中心下标位于数组的最右端，则右侧的和视为 0。

- 如果数组有多个中心下标，返回**最靠近左边的**那个。如果数组不存在中心下标，则返回 `-1`。


### 解题思路

我们可以通过**前缀和**的思想来解决这个问题。核心思想是，遍历数组的每个下标 `i`，检查它是否满足条件：左侧的前缀和等于右侧的前缀和。

假设数组的总和为 `total`，那么对于任意下标 `i`，左侧的前缀和为 `leftSum`，右侧的前缀和为 `total - leftSum - nums[i]`。如果满足 `leftSum == total - leftSum - nums[i]`，那么 `i` 就是中心下标。

### 参考解答

```java
class Solution {
    public int pivotIndex(int[] nums) {
        // 计算数组的总和
        int total = 0;
        for (int num : nums) {
            total += num;
        }

        // 遍历数组，计算每个下标的左侧和，并检查是否满足条件
        int leftSum = 0;
        for (int i = 0; i < nums.length; i++) {
            // 如果左侧和等于右侧和（右侧和 = 总和 - 左侧和 - 当前元素）
            if (leftSum == total - leftSum - nums[i]) {
                return i;
            }
            // 更新左侧和
            leftSum += nums[i];
        }

        // 如果没有找到中心下标，返回 -1
        return -1;
    }
}
```

### 代码解释

1. **计算数组的总和**：首先，遍历整个数组，计算所有元素的总和 `total`。
2. **遍历数组，寻找中心下标**：
    - 初始化左侧和 `leftSum = 0`。
    - 遍历数组的每一个元素 `nums[i]`，检查是否满足 `leftSum == total - leftSum - nums[i]`。如果满足，则当前的 `i` 就是中心下标。
    - 如果不满足条件，继续遍历，同时更新左侧和 `leftSum += nums[i]`。
3. **返回结果**：如果找到了符合条件的下标，直接返回该下标；如果遍历完数组都没有找到，返回 `-1`。


## 4.1.2 LC1588 所有奇数长度子数组的和

### 问题描述

给定一个正整数数组 `arr`，要求计算数组中所有可能的奇数长度子数组的和。一个**子数组**是指数组中一段连续的子序列。我们需要返回**所有奇数长度子数组**的和。

### 解题思路

要高效地求解这个问题，可以使用**前缀和**来快速计算子数组的和。

### 详细思路：

1. **定义前缀和数组**：前缀和数组可以帮助我们快速计算任意区间 `[i, j]` 的和。设 `prefixSum[i]` 表示 `arr` 数组前 `i` 个元素的累加和。这样 `arr[i] + arr[i+1] + ... + arr[j]` 可以用 `prefixSum[j+1] - prefixSum[i]` 表示。

2. **遍历所有子数组**：我们枚举数组中的每一个起点 `i`，并从该起点开始，枚举所有可能的奇数长度的子数组。
    - 奇数长度的子数组可能是长度为 1、3、5、7... 的子数组。
    - 在遍历过程中，使用前缀和数组计算每个奇数长度子数组的和。

3. **累加和**：对于每一个奇数长度的子数组，计算其和并累加到最终结果中。


### 参考解答

```java
class Solution {
    public int sumOddLengthSubarrays(int[] arr) {
        int n = arr.length;
        int[] prefixSum = new int[n + 1]; // 前缀和数组

        // 构建前缀和数组
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + arr[i];
        }

        int totalSum = 0;

        // 遍历所有可能的奇数长度子数组
        for (int start = 0; start < n; start++) {
            for (int length = 1; start + length <= n; length += 2) { // 只考虑奇数长度
                int end = start + length - 1;
                totalSum += prefixSum[end + 1] - prefixSum[start]; // 使用前缀和计算子数组和
            }
        }

        return totalSum;
    }
}
```

### 代码解释

1. **构建前缀和数组**：
    - `prefixSum[i + 1] = prefixSum[i] + arr[i]`，表示前 `i+1` 个元素的累加和。
    - `prefixSum[i+1] - prefixSum[start]` 可以快速得到从 `arr[start]` 到 `arr[end]` 的子数组和。

2. **遍历奇数长度子数组**：
    - `start` 表示子数组的起始位置。
    - `length` 表示子数组的长度，只取奇数（`1, 3, 5...`）。
    - 使用前缀和数组快速计算每个奇数长度子数组的和，并将其累加到 `totalSum`。

3. **返回结果**：
    - 最后返回 `totalSum`，即所有奇数长度子数组的和。


## 4.1.3 LC1732 找到最高海拔

### 问题描述

有一个自行车手打算进行一场公路骑行，这条路线总共由 `n + 1` 个不同海拔的点组成。自行车手从海拔为 `0` 的点 `0` 开始骑行。

给你一个长度为 `n` 的整数数组 `gain`，其中 `gain[i]` 是点 `i` 和点 `i + 1` 的净海拔高度差（`0 <= i < n`）。请你返回最高点的海拔。

### 思路讲解

为了找到最高海拔，我们可以使用**前缀和**的思想：

1. **初始化**：我们从海拔 `0` 开始骑行，所以可以设定 `currentAltitude` 为 `0`，并用 `maxAltitude` 来记录当前最高海拔。

2. **遍历数组**：依次遍历 `gain` 数组中的每个海拔高度差：
    - 将当前的 `gain[i]` 加到 `currentAltitude` 中，得到当前海拔。
    - 更新 `maxAltitude` 为 `max(maxAltitude, currentAltitude)`，即在每次计算完当前海拔后，检查是否需要更新最高海拔。

3. **返回结果**：遍历完成后，`maxAltitude` 就是我们要找的最高海拔。

### 参考解答

```java
class Solution {
    public int largestAltitude(int[] gain) {
        int currentAltitude = 0; // 当前海拔
        int maxAltitude = 0; // 最高海拔

        // 遍历 gain 数组
        for (int i = 0; i < gain.length; i++) {
            currentAltitude += gain[i]; // 更新当前海拔
            maxAltitude = Math.max(maxAltitude, currentAltitude); // 更新最高海拔
        }

        return maxAltitude; // 返回最高海拔
    }
}
```

## 4.2 差分数组举一反三

## 4.2.1 LC1094 拼车

### 题目描述
车上最初有 `capacity` 个空座位。车只能向一个方向行驶（也就是说，不允许掉头或改变方向）

给定整数 `capacity` 和一个数组 `trips`，trip[i] = [numPassengers<sub>i</sub>, from<sub>i</sub>, to<sub>i</sub>] 表示第 i 次旅行有 numPassengers<sub>i</sub> 乘客，接他们和放他们的位置分别是 from<sub>i</sub> 和 to<sub>i</sub>。这些位置是从汽车的初始位置向东的公里数。

当且仅当你可以在所有给定的行程中接送所有乘客时，返回 `true`，否则请返回 `false`。

### 题目解析

题目要求判断能否在所有给定行程中接送乘客，给定条件为：
- 每次行程有特定数量的乘客，需要从一个起点 `from` 接上，并在 `to` 位置放下。
- 汽车有一个初始载客量 `capacity`，只能向一个方向行驶。

核心问题在于：
- 判断某个时间点乘客数量是否会超过汽车的最大载客量。

### 思路讲解

我们可以使用**差分数组**来解决这个问题，思路如下：
1. 每次在某个起点 `from` 位置增加乘客数量，在终点 `to` 位置减少乘客数量。通过这种方式，我们可以标记每个位置上的乘客变化情况。
2. 然后通过遍历这些标记，累加每个位置的乘客数，检查是否在任何位置超出汽车的最大载客量 `capacity`。

### 步骤

1. **创建差分数组**：差分数组的大小取决于最远的行程终点，表示沿途的每个位置乘客的变化情况。
2. **处理每个行程**：对于每个行程，在差分数组的 `from` 位置增加乘客，在 `to` 位置减少乘客。
3. **前缀和计算当前乘客数**：通过计算差分数组的前缀和，得到每个位置实际的乘客数，并判断是否超出载客量。

### 代码实现

```java
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        // 找出最远的目的地，用于确定差分数组的大小
        int maxDistance = 0;
        for (int[] trip : trips) {
            maxDistance = Math.max(maxDistance, trip[2]);
        }

        // 差分数组，用于记录每个位置乘客数的变化
        int[] diff = new int[maxDistance + 1];

        // 处理每个行程，更新差分数组
        for (int[] trip : trips) {
            int numPassengers = trip[0];  // 乘客数量
            int from = trip[1];           // 上车位置
            int to = trip[2];             // 下车位置

            // 上车位置增加乘客
            diff[from] += numPassengers;
            // 下车位置减少乘客
            diff[to] -= numPassengers;
        }

        // 前缀和计算当前车上的乘客数量，判断是否超出容量
        int currentPassengers = 0;
        for (int i = 0; i <= maxDistance; i++) {
            currentPassengers += diff[i];
            if (currentPassengers > capacity) {
                return false;  // 超出容量
            }
        }

        return true;  // 所有位置都未超出容量
    }
}
```

### 代码解释

1. **找出最远的目的地**：我们通过遍历每个行程，找到最远的终点 `to`，从而确定差分数组的大小。
2. **构建差分数组**：对于每个行程，记录乘客的变化情况：
    - 在 `from` 位置上车，因此 `diff[from]` 加上该行程的乘客数。
    - 在 `to` 位置下车，因此 `diff[to]` 减去该行程的乘客数。
3. **前缀和计算**：通过遍历差分数组计算车上实际的乘客数 `currentPassengers`，一旦超过 `capacity`，返回 `false`。


## 4.2.2 LC1854 人口最多的年份
给你一个二维整数数组 `logs`，其中每个 logs[i] = [birth<sub>i</sub>, death<sub>i</sub>] 表示第 i 个人的出生和死亡年份。

年份 `x` 的人口定义为这一年期间活着的人的数目。第 i 个人被计入年份 `x` 的人口需要满足：`x` 在闭区间 [birth<sub>i</sub>, death<sub>i</sub> - 1] 内。注意，人不应当计入他们死亡当年的人口中。

返回人口最多且最早的年份。

### 题目解析

我们需要找到一个年份，该年份的人口数最多，且如果有多个年份人口数相同，返回最早的那个年份。

每个人的生存年份是一个区间 `[birthi, deathi - 1]`，即从出生年算起到死亡年份的前一年为止。我们要统计每个年份的生存人口数。

### 思路

1. **差分数组思想**：
    - 我们可以把出生当年的人口加 1，死亡当年的人口减 1。然后，通过差分数组求出每一年的实际人口变化。
    - 通过计算每年的前缀和（即累积人数变化），得到每年的人口数量。

2. **步骤概述**：
    - 初始化一个数组 `years` 来表示年份的人口变化（可以从最早年份开始，直到死亡的最大年份结束）。
    - 遍历每个人的 `birthi` 和 `deathi`：
        - 在 `birthi` 位置增加人口数量（即 `years[birthi] += 1`）。
        - 在 `deathi` 位置减少人口数量（即 `years[deathi] -= 1`，因为死亡年不计入人口数）。
    - 通过前缀和计算每一年的实际人口数量，找到人口最多的年份。

### 代码实现

```java
class Solution {
    public int maximumPopulation(int[][] logs) {
        // 假设年份范围从1950到2050
        int[] populationChange = new int[101]; // 存储人口变化的数组，范围为1950到2050

        // 记录每个人的出生和死亡年份对人口的影响
        for (int[] log : logs) {
            int birth = log[0] - 1950;
            int death = log[1] - 1950;
            populationChange[birth] += 1;  // 出生年份人口增加
            populationChange[death] -= 1;  // 死亡年份人口减少
        }

        // 计算每一年的实际人口，并找出人口最多的年份
        int maxPopulation = 0;
        int maxYear = 1950;
        int currentPopulation = 0;

        // 遍历每一年，计算人口数量
        for (int year = 0; year < 101; year++) {
            currentPopulation += populationChange[year]; // 通过前缀和计算当前年份的人口
            if (currentPopulation > maxPopulation) {
                maxPopulation = currentPopulation;
                maxYear = 1950 + year; // 记录人口最多的年份
            }
        }

        return maxYear;
    }
}
```

### 代码解释

1. **年份映射**：
    - 由于年份范围是从 1950 年到 2050 年，因此我们使用长度为 101 的数组 `populationChange` 来记录每一年的人口变化情况。`populationChange[0]` 对应的是 1950 年，`populationChange[100]` 对应的是 2050 年。

2. **处理每个人的出生和死亡年份**：
    - 对于每个人，出生年份会使当年的人口增加 1 (`populationChange[birth] += 1`)。
    - 死亡年份会使该年的人口减少 1 (`populationChange[death] -= 1`)，因为死亡年不计入该年的人口。

3. **前缀和计算**：
    - 通过遍历年份，累加每年的人口变化，实时计算当前年份的实际人口数量。
    - 找到最大人口对应的年份，如果出现多个最大值，自动返回最早的年份，因为我们按顺序遍历年份。


## 4.2.3 LC1450 在既定时间做作业的学生人数

### 题目描述
给你两个整数数组 `startTime`（开始时间）和 `endTime`（结束时间），并指定一个整数 `queryTime` 作为查询时间。

已知，第 `i` 名学生在 `startTime[i]` 时开始写作业并于 `endTime[i]` 时完成作业。

请返回在查询时间 `queryTime` 时正在做作业的学生人数。形式上，返回能够使 `queryTime` 处于区间 `[startTime[i], endTime[i]]`（含）的学生人数。

请使用差分数组的方法完成此题。

### 思路讲解

1. **定义范围**：
    - 创建一个足够大的差分数组，数组的大小至少为 `maxTime + 2`，防止越界
    - 当我们处理某个学生的作业时间 `[startTime[i], endTime[i]]` 时，我们在 `startTime[i]` 位置上增加 1，表示从这个时刻开始有一个学生在做作业。
    - 因为题目要求包含`endTime`，即`endTime`时学生仍在做作业，因此需要在 `endTime[i] + 1` 位置上减少 1，表示从 `endTime[i] + 1` 这个时刻开始，这个学生不再做作业。
    - 如果 `endTime` 是最大时间，比如 `maxTime`，那么 `endTime[i] + 1` 将会是 `maxTime + 1`。
    - 为了确保我们在访问 `diff` 数组的 `endTime[i] + 1` 位置时不会越界，因此我们需要将差分数组的长度设为 `maxTime + 2`。这样可以确保数组索引不会超出界限。

2. **构建差分数组**：
    - 对于每个学生的作业时间 `[startTime[i], endTime[i]]`，在差分数组的 `startTime[i]` 位置增加 `1`，在 `endTime[i] + 1` 位置减少 `1`。这样可以标记在作业开始和结束时的变化。

3. **计算前缀和**：
    - 遍历差分数组并计算前缀和，以得到在每个时间点的正在做作业的学生人数。

4. **查询结果**：
    - 最后，根据 `queryTime` 的值直接返回差分数组中对应的结果。

### 代码实现

```java
class Solution {
    public int busyStudent(int[] startTime, int[] endTime, int queryTime) {
        // 找到结束时间的最大值
        int maxTime = 0;
        for (int end : endTime) {
            maxTime = Math.max(maxTime, end);
        }

        // 初始化差分数组，长度为 maxTime + 2，避免越界
        int[] diff = new int[maxTime + 2];

        // 更新差分数组
        for (int i = 0; i < startTime.length; i++) {
            diff[startTime[i]] += 1;          // 开始写作业
            diff[endTime[i] + 1] -= 1;        // 停止写作业
        }

        // 计算前缀和，得到每个时间点的在做作业的学生人数
        int currentCount = 0;
        for (int i = 0; i <= queryTime; i++) {
            currentCount += diff[i];
        }

        return currentCount;  // 返回在 queryTime 时正在做作业的学生人数
    }
}
```

## 5. 课后练习

### 前缀和
| 题目编号   | 题目名称                     | 简介                                                                 |
|--------|------------------------|--------------------------------------------------------------------|
| LC238  | 除自身以外数组的乘积           | 给定一个整数数组 `nums`，返回一个数组，其中每个元素是 `nums` 中其他所有元素的乘积。                    |
| LC560  | 和为 K 的子数组              | 给定一个整数数组 `nums` 和一个整数 `k`，计算 `nums` 中和为 `k` 的连续子数组的个数。                     |
| LC1991 | 找到数组的中心位置           | 给定一个整数数组，找到中心位置，使得该位置左边的元素和等于右边的元素和，返回该位置的索引。                   |
| LC3028 | 边界上的蚂蚁                | 给定一个数组，模拟蚂蚁在边界上移动，返回最后蚂蚁的位置。                                                  |
| LC974  | 和可被 K 整除的子数组          | 给定一个整数数组 `nums` 和一个整数 `k`，返回 `nums` 中和可被 `k` 整除的子数组的个数。                      |

### 差分数组
| 题目编号 | 题目名称                     | 简介                                                                  |
|---------|------------------------|---------------------------------------------------------------------|
| LC995   | K 连续位的最小翻转次数        | 给定一个二进制数组，求出将 `K` 个连续的位翻转为 `1` 所需的最小翻转次数。                        |
| LC1109  | 航班预定统计               | 给定一个二维数组 `bookings`，每个航班的乘客预定信息，计算每个航班的最终乘客数量。                  |
| LC1893  | 检查是否区域内所有整数都被覆盖 | 给定一个二维数组 `ranges`，检查是否在指定的区间内所有整数都被覆盖。                                |
| LC2381  | 字母移位II                | 给定一个字符串和一个移位值，返回移位后的新字符串。                                                    |
| LC2251  | 花期内花的数目            | 给定一个植物的花期和一个查询，返回在查询范围内开花的植物数目。                                          |