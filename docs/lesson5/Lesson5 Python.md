# Lesson 5 列表与初级搜索

写在前面：

数组在Java，C / C ++，JavaScript等大多数编程语言中都很流行。但是，在Python中，它们并不常见。人们经常谈论Python数组时，他们谈论的是Python列表。

列表比数组灵活得多。它们可以存储不同数据类型的元素，包括字符串。列表比数组要快，如果需要对数组和矩阵进行数学计算，可以使用Numpy库之类的方法，本章着重讨论列表的各种操作方法。

创建一个列表，只要把逗号分隔的不同的数据项使用方括号括起来即可。如下所示：

```python
list1 = ['Google', 'Baidu', 1997, 2000]
list2 = [1, 2, 3, 4, 5 ]
list3 = ["a", "b", "c", "d"]
list4 = ['red', 'green', 'blue', 'yellow', 'white', 'black']
```
## 目录

- [1 列表](#1-列表)
    - [1.1 访问列表中的值](#11-访问列表中的值)
    - [1.2 更新列表](#12-更新列表)
        - [1.2.1 使用append方法](#121-使用append方法)
        - [1.2.2 使用insert方法](#122-使用insert方法)
    - [1.3 删除列表元素](#13-删除列表元素)
    - [1.4 Python列表操作符](#14-Python-列表操作符)
    - [1.5 Python-列表截取与拼接](#15-Python-列表截取与拼接)
    - [1.6 嵌套列表](#16-嵌套列表)
    - [1.7 python列表函数和方法](#17-Python-列表函数和方法)

- [2 初级搜索](#2-初级搜索)
    - [2.1 index方法查找索引](#21-index方法查找索引)
    - [2.2 for循环获取索引](#22-for循环获取索引)
    - [总结](#总结)

- [课后练习](#课后练习)
    - [问题描述](#问题描述)
    - [hints](#hints)
    - [任务](#任务)

## 1 列表

### 1.1 访问列表中的值

与字符串的索引一样，列表索引从 **0** 开始，第二个索引是 **1**，依此类推。

通过索引列表可以进行截取、组合等操作。

![img](https://www.runoob.com/wp-content/uploads/2014/05/positive-indexes-1.png)

```python
list = ['red', 'green', 'blue', 'yellow', 'white', 'black']
print(list[0])
print(list[1])
print(list[2])
```

以上实例输出结果：

```
red
green
blue
```

索引也可以从尾部开始，最后一个元素的索引为 **-1**，往前一位为 **-2**，以此类推。

![img](https://www.runoob.com/wp-content/uploads/2014/05/negative-indexes.png)

```python
list = ['red', 'green', 'blue', 'yellow', 'white', 'black']
print(list[-1])
print(list[-2])
print(list[-3])
```

以上实例输出结果：

```
black
white
yellow
```

使用下标索引来访问列表中的值，同样你也可以使用方括号 **[]** 的形式截取字符，如下所示：

![img](https://www.runoob.com/wp-content/uploads/2014/05/first-slice.png)

```python
nums = [10, 20, 30, 40, 50, 60, 70, 80, 90]
print(nums[0:4])
```

以上实例输出结果：

```
[10, 20, 30, 40]
```

使用负数索引值截取：

```python
list = ['Google', 'Amazon', "Zhihu", "Taobao", "Wiki"]

# 读取第二位
print ("list[1]: ", list[1])
# 从第二位开始（包含）截取到倒数第二位（不包含）
print ("list[1:-2]: ", list[1:-2])
```

以上实例输出结果：

```
list[1]:  Amazon
list[1:-2]:  ['Amazon', 'Zhihu']
```

### 1.2 更新列表

#### 1.2.1 使用append()方法

你可以对列表的数据项进行修改或更新，你也可以使用 append() 方法来添加列表项，如下所示：

```python
list = ['Google', 'Amazon', 1997, 2000]

print ("第三个元素为 : ", list[2])
list[2] = 2001
print ("更新后的第三个元素为 : ", list[2])

list1 = ['Google', 'Amazon', 'Taobao']
list1.append('Baidu')   #append()用于添加元素添加到列表最后一位
print ("更新后的列表 : ", list1)
```

以上实例输出结果：

```
第三个元素为 :  1997
更新后的第三个元素为 :  2001
更新后的列表 :  ['Google', 'Amazon', 'Taobao', 'Baidu']
```

#### 1.2.2 使用insert()方法

你还可以使用 `insert()` 方法在列表的指定位置插入元素。`insert()` 方法语法格式如下：

```python
list.insert(index, obj)
```

其中，`index` 是插入位置的索引，`obj` 是要插入的对象。

示例代码如下：

```python
list2 = ['Google', 'Amazon', 'Taobao']
list2.insert(1, 'Baidu')  # 在索引为1的位置插入'Baidu'
print("插入元素后的列表：", list2)
```

以上实例输出结果：

```
插入元素后的列表： ['Google', 'Baidu', 'Amazon', 'Taobao']
```



### 1.3 删除列表元素

可以使用 del 语句来删除列表中的元素，如下实例：

```python
list = ['Google', 'Amazon', 1997, 2000]
 
print ("原始列表 : ", list)
del list[2]
print ("删除第三个元素 : ", list)
```

以上实例输出结果：

```
原始列表 :  ['Google', 'Amazon', 1997, 2000]
删除第三个元素 :  ['Google', 'Amazon', 2000]
```

### 1.4 Python 列表操作符

列表对 + 和 * 的操作符与字符串相似。+ 号用于组合列表，* 号用于重复列表。

如下所示：

| Python 表达式                         | 结果                         | 描述                 |
| :------------------------------------ | :--------------------------- | :------------------- |
| len([1, 2, 3])                        | 3                            | 长度                 |
| [1, 2, 3] + [4, 5, 6]                 | [1, 2, 3, 4, 5, 6]           | 组合                 |
| ['Hi!'] * 4                           | ['Hi!', 'Hi!', 'Hi!', 'Hi!'] | 重复                 |
| 3 in [1, 2, 3]                        | True                         | 元素是否存在于列表中 |
| for x in [1, 2, 3]: print(x, end=" ") | 1 2 3                        | 迭代                 |

### 1.5 Python 列表截取与拼接

Python 的列表截取与字符串操作类似，如下所示：

```
L=['Google', 'Apple', 'Taobao']
```

操作：

| Python 表达式 | 结果                | 描述                                               |
| :------------ | :------------------ | :------------------------------------------------- |
| L[2]          | 'Taobao'            | 读取第三个元素                                     |
| L[-2]         | 'Apple'             | 从右侧开始读取倒数第二个元素: count from the right |
| L[1:]         | ['Apple', 'Taobao'] | 输出从第二个元素开始后的所有元素                   |

```
>>> L=['Google', 'Apple', 'Taobao']
>>> L[2]
'Taobao'
>>> L[-2]
'Apple'
>>> L[1:]
['Apple', 'Taobao']
>>>
```

列表还支持拼接操作：

```
>>> squares = [1, 4, 9, 16, 25]
>>> squares += [36, 49, 64, 81, 100]
>>> squares
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
>>>
```

### 1.6 嵌套列表

使用嵌套列表即在列表里创建其它列表，例如：

```
>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[0][1]
'b'
```

### 1.7 Python 列表函数和方法

Python包含以下函数:

| 序号 | 函数                         |
| :--- | :--------------------------- |
| 1    | len(list) 列表元素个数       |
| 2    | max(list) 返回列表元素最大值 |
| 3    | min(list)返回列表元素最小值  |
| 4    | list(seq)将元组转换为列表    |

Python包含以下方法:

| 序号 | 方法                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html) 在列表末尾添加新的对象 |
| 2    | [list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html) 统计某个元素在列表中出现的次数 |
| 3    | [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| 4    | [list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html) 从列表中找出某个值第一个匹配项的索引位置 |
| 5    | [list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html) 将对象插入列表 |
| 6    | [list.pop(\[index=-1\])](https://www.runoob.com/python3/python3-att-list-pop.html) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| 7    | [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html) 移除列表中某个值的第一个匹配项 |
| 8    | [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html) 反向列表中元素 |
| 9    | [list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html) 对原列表进行排序 |
| 10   | [list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html) 清空列表 |
| 11   | [list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html) 复制列表 |

## 2 初级搜索

### 2.1 index()方法查找索引

Python 的内置 `index()` 方法可以被用作搜索工具，`index()` 方法的语法如下所示：

```python
my_list.index(item, start, end)
```

- `my_list` 是你正在搜索的列表的名称。
- `.index()` 是采用三个参数的搜索方法，一个参数是必需的，另外两个是可选的。
- `item` 是必需的参数，它是你要搜索其索引的元素。
- `start` 是第一个可选参数，这是你开始搜索的索引。
- `end` 是第二个可选参数，这是你将结束搜索的索引。

示例：

```python
programming_languages = ["JavaScript","Python","Java","C++"]

print(programming_languages.index("Python"))

```

输出为：

```
1
```

传递的参数是区分大小写的。这意味着如果你传递的是 “python”，而不是 “Python”，你将收到一个错误，因为带有小写 “p” 的 “python” 不是列表的一部分。

当然上面这种index方法有一个需要注意的点：如果我们index找不到搜索的值，就会报错，类似：

```python
programming_languages = ["JavaScript","Python","Java","C++"]

print(programming_languages.index("C"))
```

报错为：

```
    print(programming_languages.index("C"))
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ValueError: 'C' is not in list
```

为了避免这种错误的发生，我们可以使用if-else的方法来避免系统报错，示例为：

```python
def find_index(lst, item):
    if item in lst:
        return lst.index(item)  # 如果找到，返回该值
    else:
        return -1  # 否则返回-1

programming_languages = ["JavaScript", "Python", "Java", "C++"]

print(find_index(programming_languages, "Python"))  # 输出: 1
print(find_index(programming_languages, "python"))  # 输出: -1
```

输出为：

```
1
-1
```



### 2.2 for循环获取索引

下面列表出现了三个字符串 “Python”。

```python
programming_languages = ["JavaScript","Python","Java","Python","C++","Python"]
```

首先，创建一个新的空列表，用于存储 “Python” 所有索引的列表。

```python
programming_languages = ["JavaScript","Python","Java","Python","C++","Python"]

python_indices = []
```

接下来，使用 `for` 循环，并使用 `append()` 方法将元素添加到列表中。

```python
programming_languages = ["JavaScript","Python","Java","Python","C++","Python"]

python_indices = []

for i in range(len(programming_languages)):
    if programming_languages[i] == "Python":
      python_indices.append(i)

print(python_indices)
```

输出结果为：

```
[1, 3, 5]
```

当然也可以通过索引来遍历内容，

```python
programming_languages = ["JavaScript","Python","Java","Python","C++","Python"]
for i in range(3):
    print(programming_languages[i])
```

结果为：

```
JavaScript
Python
Java
```

### 总结

Python列表是一种灵活且常用的数据结构，可以存储和操作任意类型的元素，适用于各种编程任务。更多高级搜索方式如二分搜索（Binary Search）散列搜索（Hash Search），同学们会在进阶的算法与数据结构内容中接触。



## 课后练习


### 问题描述

假设我们有一个包含多个姓名的列表。实现一个函数来搜索一个给定姓名在列表中的位置，并返回其索引。如果找不到匹配的姓名，则返回 -1。

### Hints

在主程序中，创建一个包含多个姓名的列表。然后实现一个函数，通过遍历列表找到目标姓名的位置，并返回其索引。如果找不到，返回 -1。

#### 任务

1. 创建姓名列表: 在主程序中，创建一个包含多个姓名的列表。
2. 线性搜索函数: 实现一个 linear_search 函数，该函数接受一个包含姓名的列表和一个字符串参数（要搜索的姓名）。在这个函数中，使用简单的 for 循环遍历列表，逐个比较每个姓名是否与目标姓名匹配。
3.返回结果: 如果找到匹配的姓名，返回该姓名在列表中的索引；如果找不到，返回 -1。

代码示例：

```python
def linear_search(name_list, target_name):
    for index in range(len(name_list)):
        if name_list[index] == target_name:
            return index
    return -1

# 示例用法
names = ["Alice", "Bob", "Charlie", "David", "Eve"]

# 搜索 "Bob" 的位置
index = linear_search(names, "Bob")
print(f"Bob's index is: {index}")  # 输出: Bob's index is: 1

# 搜索 "Frank" 的位置
index = linear_search(names, "Frank")
print(f"Frank's index is: {index}")  # 输出: Frank's index is: -1
```

参考输出：

```
Bob's index is: 1
Frank's index is: -1
```

