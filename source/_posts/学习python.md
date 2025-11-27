---
title: 学习Python
date: 2025-11-20
tag: 练习
categories: Python
---

# 学习python的计划

## 初步规划

- 计划的时间为2~3个月（开始时间为2024年11月20日到2025年1月20日或者2025年2月20日）
- 至少要达到中阶左右水平

```txt
《Python编程从入门到实践（第2版）》：Python入门基础，建议完成书中的项目。
《代码整洁之道》：学习良好的代码风格和实践，培养编程规范。
数据结构与算法入门
《算法（第4版）》：了解常用的数据结构和算法，如排序、查找、递归等。
《数据结构与算法 Python语言实现》：结合Python语言理解数据结构和算法的基本实现。
操作系统和系统基础
数学基础
《高等数学（上下册）》（同济大学数学系编）：数学基础，尤其是微积分知识。
《线性代数及其应用》：理解矩阵和向量，为机器学习和数据分析中的线性代数运算奠定基础。
计算机基础原理
《编码 隐匿在计算机软硬件背后的语言》：了解编码、二进制、数字表示等概念，构建计算机内部原理的基本理解。
Python和编程进阶
《流畅的Python》：进一步理解Python语言特性，掌握高级用法。
《Python3网络爬虫开发实战（第2版）》：学习网络爬虫，掌握网络数据采集和处理方法。
算法与数据结构进阶
《离散数学及其应用》：学习离散数学中的逻辑、图论、组合数学等内容，夯实算法和数据结构的理论。
```

**推荐的初阶学习顺序**
**数学基础：**
**先学习 《高等数学》 的基本微积分内容，帮助理解连续变化和渐进增长等概念。**
**接着学习 《线性代数及其应用》，理解向量、矩阵等基础，这对后续的数据分析和算法理解也有帮助。**
**数据结构与算法：**
**在具备数学基础后，进入 《算法（第4版）》 和 《数据结构与算法 Python语言实现》。**
**学习时，可以结合实践和简单的算法实现，把数学知识应用到编程中。**
**这种顺序将使你在数学和算法学习之间形成良好的衔接，提升理解力和应用能力。**

- 了解python生态
- 实战项目

## 每日总结

### 2024/11/20

重新学习了python，在B站上面找了一个讲的还不错的视频观看，视频链接为[python入门到精通](https://www.bilibili.com/video/BV1wD4y1o7AS?t=2.1&p=25)

+ 学习了比较多的基础知识，例如用python进行进制之间的转换，认识了数据类型和保留字，算术运算符、比较运算符、逻辑运算符、位运算符，以及它们之间的优先级。

```python
# python 哲学
import this
print(this)


# python 保留字
import keyword
print(keyword.kwlist)
# python有多少个保留字
print(len(keyword.kwlist))


# 算数运算符 + - * / // % **
# 比较运算符 > < == >= <= !=
# 逻辑运算符 and 与 or 或  not 非
# 位运算符 & 位与  | 位或  ^ 异或  ~取反  <<  左移位   >> 右移位 

```

```txt
算术运算符
+：加法
-：减法
*：乘法
/：除法（返回浮点数结果，即使整除）
//：整除（只保留商的整数部分）
%：取模（返回余数）
**：幂运算（指数）
比较运算符
>：大于
<：小于
==：等于（注意是比较相等，不是赋值）
>=：大于等于
<=：小于等于
!=：不等于
逻辑运算符
and：逻辑与（当且仅当两个条件均为真时，结果为真）
or：逻辑或（当至少一个条件为真时，结果为真）
not：逻辑非（将条件取反）
位运算符
&：按位与（两位均为 1 时，结果为 1，否则为 0）
|：按位或（两位至少有一位为 1 时，结果为 1）
^：按位异或（两位不同则为 1，相同则为 0）
~：按位取反（将每个位取反）
<<：左移位（按位左移，左边丢弃，右边补 0，相当于乘以 2 的 n 次方）
>>：右移位（按位右移，右边丢弃，左边根据符号位补 0 或 1，相当于除以 2 的 n 次方）
```



+ 重点有字符串切片，例如[-3, -2],索引为-2的字符不取。python的编程规范等等

```txt
python编程规范主要参考PEP8
1. 代码格式
缩进
使用 4 个空格来缩进代码。
禁止使用 Tab 键混用缩进（可以通过 IDE 设置）。
每行字符数限制
每行代码建议不超过 79 个字符。
文档字符串或注释建议不超过 72 个字符。
空行
顶级函数和类定义之间用两行空行隔开。
类中方法之间用一行空行隔开。
函数中逻辑段落之间用一行空行隔开。
空格使用
运算符两侧使用单个空格（推荐）：
python
a = b + c
不要在括号内部加空格：
python
# 正确：
my_func(a, b)

# 错误：
my_func( a, b )
2. 命名规范
变量命名
使用 小写字母和下划线（snake_case）：
python
total_count = 10
函数命名
函数名使用 小写字母和下划线：
python
def calculate_area():
    pass
类命名
使用 首字母大写的驼峰命名法（PascalCase）：
python
class MyClass:
    pass
常量命名
使用 全大写字母和下划线（UPPER_SNAKE_CASE）：
python
MAX_RETRIES = 5
私有变量或方法
使用单个下划线开头：
python
_private_variable = 42
def _private_method():
    pass
3. 注释
单行注释
使用 #，并在 # 后留一个空格：
python
# 这是一个单行注释
total = 10  # 这是变量的含义
多行注释
使用多行 # 注释块或文档字符串：
python
# 这是一个多行注释
# 用于描述较复杂的逻辑。
文档字符串
使用 """ 来注释模块、类和函数：
python
def my_function():
    """
    这是一个函数的文档字符串。
    作用：描述函数的功能和用途。
    """
    pass
4. 代码结构
导入顺序
导入分为三部分，按以下顺序排列并用空行隔开：

标准库模块
第三方模块
本地模块或自定义模块
python
import os
import sys

import requests

from my_project.utils import my_function
每行只导入一个模块
python
# 正确：
import os
import sys

# 错误：
import os, sys
5. 异常处理
使用 try-except 块捕获异常：

python
复制代码
try:
    result = 1 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
不要使用裸 except，而是指定异常类型：

python
# 正确：
try:
    pass
except ValueError:
    pass

# 错误：
try:
    pass
except:
    pass
6. 其他建议
遵循 Python 的 "显式优于隐式" 和 "简单优于复杂" 原则（来自 Python 之禅 import this）。
避免滥用全局变量。
尽量保持函数短小，每个函数只做一件事情。
使用类型注解：
python
def add_numbers(a: int, b: int) -> int:
    return a + b
7. 工具辅助
使用自动化工具检查代码风格，例如：
flake8：静态检查代码是否符合 PEP 8。
black：自动格式化代码。
pylint：提供代码质量分析。
```



+ eval函数、input函数、print函数、id函数、round函数，len函数等等

![image-20241120215022726](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20241120215022726.png)

### 2024/11/21

今天没学习多少，有事耽搁了。（比较重要的事）

python学习了以下内容

- 顺序结构
- 选择结构
- 双分支结构
- 多分支结构

### 2024/11/22

今天在解决一个编程问题（打印一个菱形）时遇到的问题。

```python
# 打印一个菱形
rows = 9

for i in range(1, rows + 1):
    print(' ' * (rows - i) + '*' * (2 * i - 1))

range_list = [i for i in range(1, rows + 1)]
range_list.reverse()
for i in range_list:
    print(' ' * (rows - i) + '*' * (2 * i - 1))
```

```python
# chatgpt优化的代码
rows = 9

# 打印上半部分和下半部分
for i in range(1, rows + 1):
    print(' ' * (rows - i) + '*' * (2 * i - 1))
for i in range(rows - 1, 0, -1):  # 倒序从 rows-1 开始
    print(' ' * (rows - i) + '*' * (2 * i - 1))
    
# 封装成一个函数
def print_diamond(rows):
    # 打印菱形的上半部分
    for i in range(1, rows + 1):
        print(' ' * (rows - i) + '*' * (2 * i - 1))
    # 打印菱形的下半部分
    for i in range(rows - 1, 0, -1):
        print(' ' * (rows - i) + '*' * (2 * i - 1))

# 调用函数
print_diamond(9)


# 空心菱形
def print_hollow_diamond(rows):
    # 上半部分
    for i in range(1, rows + 1):
        if i == 1:
            print(' ' * (rows - i) + '*')
        else:
            print(' ' * (rows - i) + '*' + ' ' * (2 * i - 3) + '*')

    # 下半部分
    for i in range(rows - 1, 0, -1):
        if i == 1:
            print(' ' * (rows - i) + '*')
        else:
            print(' ' * (rows - i) + '*' + ' ' * (2 * i - 3) + '*')

# 调用函数
print_hollow_diamond(9)
```



- `reverse()`函数是原地修改列表，而不是返回一个新的列表。（例如：列表`x_list = y_list.reverse()` 打印x_list返回的是None）

如果需要获取反转后的列表，可用切片方法或者`reversed()`函数。

- 切片方法会反转一个新的列表。

```python
# 打印一个菱形
rows = 9

for i in range(1, rows + 1):
    print(' ' * (rows - i) + '*' * (2 * i - 1))

range_list = [i for i in range(1, rows + 1)]

for i in range_list[::-1]:
    print(' ' * (rows - i) + '*' * (2 * i - 1))
```

- `reversed()` 函数返回一个反转的迭代器，可以用 `list()` 转换为列表：

```python
range_list = [i for i in range(1, rows + 1)]
x_list = list(reversed(range_list))
print(x_list)
```

- 使用`reverse()`的场景

`reverse()` 是一个**就地修改**（in-place modification）的方法，它直接改变原列表的顺序而不返回新的列表。它适合以下场景：

1. **需要就地修改原列表的顺序** 
    如果你不需要保留原列表的顺序，也不需要新创建一个反转后的列表，而是直接修改当前列表，使用 `reverse()` 是最有效的选择。

  ```python
  my_list = [1, 2, 3, 4, 5]
  my_list.reverse()  # 直接修改列表
  print(my_list)  # 输出：[5, 4, 3, 2, 1]
  ```

2. **性能优化**

​       `reverse()` 是原地操作，消耗的内存更少，适合在性能要求较高的情况下使用。

       ```python	
       big_list = list(range(1, 1000000))
       big_list.reverse()  # 原地修改，不生成新列表
       ```

相比之下，切片 `[::-1]` 会创建一个新列表，占用额外内存。

3. **在不需要返回值的场景中**
    当反转列表只是一个步骤，并不需要进一步处理反转后的列表：

  ```python
  names = ["Alice", "Bob", "Charlie"]
  names.reverse()  # 原地反转
  print("Reversed names:", names)
  ```

4. **简化逻辑**
    在特定算法中，需要反转列表以简化操作时，用 `reverse()` 可以让代码更清晰：

  ```python
  numbers = [1, 2, 3, 4, 5]
  
  # 反转后就地进行其他操作
  numbers.reverse()
  for num in numbers:
      print(num)  # 依次打印 5, 4, 3, 2, 1
  ```

5. **注意事项**
    **不可链式调用** `reverse()` 返回 `None`，不能像某些其他方法那样链式调用：

  ```python
  my_list = [1, 2, 3]
  # 错误：不能链式调用
  reversed_list = my_list.reverse().append(4)  # 会报错
  ```

  **不可用于不可变数据类型** `reverse()` 只能用于列表，像字符串、元组等不可变类型需要用其他方式反转，例如 `[::-1]` 或 `reversed()`。

6. **总结**

  + **用 `reverse()`**：当你只想就地修改列表顺序，并不需要新列表。
  + **用 `[::-1]` 或 `reversed()`**：当你需要保留原列表或返回一个新的反转版本。

### 2024/11/23

+ python3.11新特性match ... case...结构
+ 循环结构有两种：for遍历循环和while无限循环

#### 九九乘法表（chatgpt）

##### 实现1 基本九九乘法表

```python
for i in range(1, 10):				# 外层循环控制行数
    for j in range(1, i + 1):		# 内层循环控制每一行的列数
        print(f"{j}*{i}={i * j}", end='\t')			# 用 f-string 格式化输出 打印每个乘法表达式
    print()			# 换行
```

##### 实现2 对齐九九乘法表

通过指定每个单元格的宽度，让表格整齐对齐：

```python
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}*{i}={i * j:2}", end='\t')  # `:2` 表示结果占 2 个字符宽度
    print()
```

##### 实现3 封装为函数

将九九乘法表封装为函数，支持灵活调用：

```python
def print_multiplication_table(n=9):
    """打印 n*n 的乘法表"""
    for i in range(1, n + 1):
        for j in range(1, i + 1):
            print(f"{j}*{i}={i * j:2}", end='\t')
        print()

# 调用函数
print_multiplication_table()
```

##### 实现4 动态可扩展乘法表

为支持自定义范围（如：12X12或者更多），扩展功能：

```python
def print_multiplication_table(rows, cols=None):
    """打印自定义行数和列数的乘法表"""
    if cols is None:
        cols = rows  # 如果列数未指定，默认为方形表
    for i in range(1, rows + 1):
        for j in range(1, min(i, cols) + 1):
            print(f"{j}*{i}={i * j:2}", end='\t')
        print()

# 调用函数，打印标准 9×9
print_multiplication_table(9)

# 调用函数，打印 12×12
print_multiplication_table(12)
```

##### 实现5 结果保存到文件

```python
def save_multiplication_table_to_file(filepath, n=9):
    """将乘法表保存到文件"""
    with open(filepath, 'w') as f:
        for i in range(1, n + 1):
            for j in range(1, i + 1):
                f.write(f"{j}*{i}={i * j:2}\t")
            f.write("\n")

# 保存到文件
save_multiplication_table_to_file("multiplication_table.txt")
```

##### 总结

1. 实现原则：
   - 简洁但不失可读性，优先使用 `f-string`。
   - 考虑代码的扩展性和灵活性，封装为函数是我常用的方式。
   - 输出美观，尽量对齐。
2. 常用代码：
   + 如果是一次性使用，我会用实现 1 或 2；如果需要多次使用，我会用实现 3 或 4，甚至实现 5 来保存结果。

#### 猜数游戏(chatgpt)

```python
import random

def guess_number_game():
    """猜数字游戏"""
    # 累加猜测次数
    attempts = 0

    # 随机生成目标数字
    random_number = random.randint(1, 100)

    print("欢迎来到猜数字游戏！目标数字是 1 到 100 之间的整数。")
    print("试着猜猜看吧！")

    while True:
        try:
            user_number = int(input("请输入您猜的数字："))
            attempts += 1
            if user_number > random_number:
                print("您所猜的数字大了。")
            elif user_number < random_number:
                print("您猜的数字小了。")
            else:
                print(f"恭喜您猜对了！目标数字是 {random_number}。")
                print(f"您一共猜了 {attempts} 次。")
                break
        except ValueError:
            print("请输入一个有效的整数！")

# 开始游戏
guess_number_game()
```

### 2024/11/24

今日未能坚持学习，明天要去成都玩几天。回来复习以下前面的知识再学习。加油！

### 2024/12/02

已复习（又去玩了两天 后面不能去玩了）

### 2024/12/04

善用列表推导式(python内部对推导式进行了优化)

```python
import random

# 生成随机数列表
random_list = [random.randint(0, 100) for _ in range(10)]

# 使用 enumerate 构造字典
index_random_map = {index: item for index, item in enumerate(random_list, 1)}

# 打印结果
print("Random List:", random_list)
print("Index to Random Map:", index_random_map)

```

### 2024/12/11

前段时间属于堕落贪玩了。

打印二维列表（表格数据）

```python
# 二维列表
# 创建一个二维列表

lst = [
    ['城市', '环比', '同比'],
    ['北京', '121', '111'],
    ['上海', '101', '102'],
]

for row in lst:
    for item in row:
        print(item, end='\t')
    print()     # 换行
```

更优雅的写法

```python
# 二维列表
# 创建一个二维列表

lst = [
    ['城市', '环比', '同比'],
    ['北京', '121', '111'],
    ['上海', '101', '102'],
]

for row in lst:
    print('\t'.join(row))  # 使用 tab 分隔
```

```python
lst = [
    ['城市', '环比', '同比'],
    ['北京', '121', '111'],
    ['上海', '101', '102'],
]

# 转换为一个包含字符串的列表
formatted_rows = ['\t'.join(row) for row in lst]
for row in formatted_rows:
    print(row)
```

### 2024/12/12

```python
# 问题1： 基本数据结构操作
"""
编写一个函数，输入一个字符串，返回字符串中每个字符出现的次数（频率）。
"""
def count_str():
    str = input("请输入一个字符串: ")
    key_str = ''.join(dict.fromkeys(str))
    value = {i: str.count(i) for i in key_str}
    print(value)
```

```python
# 问题2：控制结构(暴力解法)
"""
编写一个函数，输入一个整数列表 nums 和一个目标值 target，返回列表中两个数之和等于目标值的索引。
"""

def two_num(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
    return None

nums = [2, 7, 11, 15]
target = 9

x = two_num(nums, target)
print(x)
```

```python
# 问题2：控制结构
"""
编写一个函数，输入一个整数列表 nums 和一个目标值 target，返回列表中两个数之和等于目标值的索引。
"""


def two_sum(nums, target):
    # 创建一个空字典来存储数值及其对应的索引
    num_to_index = {}

    # 遍历数组
    for i, num in enumerate(nums):
        complement = target - num  # 计算目标值的补数
        if complement in num_to_index:  # 如果补数已经在字典中，直接返回
            return [num_to_index[complement], i]
        num_to_index[num] = i  # 否则，将当前数及索引存入字典

    return None  # 如果没有找到，返回 None


nums = [2, 7, 11, 15]
target = 9

x = two_sum(nums, target)
print(x)
```

```python
# 问题2：控制结构(哈希表)更优解法
"""
编写一个函数，输入一个整数列表 nums 和一个目标值 target，返回列表中两个数之和等于目标值的索引。
"""
```

```python
# 递归
"""
编写一个递归函数，计算给定数字的阶乘。
"""
def factorial(n):
    # 递归终止条件
    if n == 0 or n == 1:
        return 1
    # 递归公式
    return n * factorial(n - 1)

# 测试代码
num = 5
result = factorial(num)
print(f"{num}! = {result}")  # 输出 5! = 120
```

```python
# 迭代
def factorial(n):
    result = 1
    for i in range(1, n + 1):  # 使用循环累乘
        result *= i
    return result
```

#### 递归和迭代

![image-20241213015005310](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20241213015005310.png)

### 2024/12/14

```python
# 写一个程序，要求用户输入一个整数 n，输出从 1 到 n 所有整数的平方。

def print_square():
    n = int(input('请输入一个整数: '))
    square = [i**2 for i in range(1, n + 1)]
    return square

x = print_square()
print(x)
```

```python
# 编写一个函数，将两个字典合并。如果存在相同的键，则值相加。（这题不是自己想出来的，这一块的基础知识较为薄弱）
def merge_dict(dict1, dict2):
    # 获取唯一的键
    all_keys = set(dict1) | set(dict2)

    # 创建新的字典，相同键的值相加，不同键的值保持不变
    merged_dict = {key: dict1.get(key, 0) + dict2.get(key, 0) for key in all_keys}
    print(merged_dict)

dict1 = {"a": 1, "b": 2, "c": 3}
dict2 = {"b": 3, "c": 4, "d": 5}

merge_dict(dict1, dict2)
```

```python
# 用递归实现斐波那契数列，返回第 n 个斐波那契数。

def fibonacci(n):
    if n == 1 or n == 2:
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

n = 7
x = fibonacci(n)
print(x)

# 动态规划 优化 动态规划实现斐波那契数列
def fibonacci(n):
    if n <= 2:
        return 1
    fib = [0] * (n + 1)
    fib[1], fib[2] = 1, 1
    for i in range(3, n + 1):
        fib[i] = fib[i - 1] + fib[i - 2]
    return fib[n]

n = 7
print(fibonacci(n))
```

```python
# 需要从文件 input.txt 中读取每一行，将其内容反转后写入 output.txt。
def reverse_lines(input_file, output_file):
    with open(input_file, 'r') as infile, open(output_file, 'w') as outfile:
        for line in infile:
            outfile.write(line.strip()[::-1] + '\n')  # 反转并写入

# 假设 input.txt 文件内容：
# hello world
# python is great

reverse_lines('input.txt', 'output.txt')
# output.txt 输出：
# dlrow olleh
# taerg si nohtyp

```

```python
"""
编写一个程序完成以下任务：

计算所有学生的平均分。
按照分数从高到低排序，返回排序后的列表。
找到最高分的学生姓名。
"""
students = [
    {"name": "Alice", "score": 85},
    {"name": "Bob", "score": 92},
    {"name": "Charlie", "score": 87},
    {"name": "David", "score": 78},
]

# 计算平均分
average_score = sum(student['score'] for student in students) / len(students)
print(f"平均分：{average_score}")

# 按分数从高到低排序
sorted_students = sorted(students, key=lambda x: x['score'], reverse=True)
print(f"排序：{sorted_students}")
v 
highest_score_student = max(students, key=lambda x: x['score'])
print(f"最高分学生：{highest_score_student['name']}")

```

### 2024/12/27

#### 扩展赋值运算符

```python
alpha = [1, 2, 3]
beta = alpha
beta += [4, 5]
beta = beta + [6, 7]
print(alpha)
print(beta)
# 这个例子展现了语句beta += foo, beta = beta + foo 在列表语义方面的微妙差异。
```

### 2025/2/8

```python
# 输入两个数字并计算和、差、积和商
def calculate(a, b):
    try:
        add_sum = a + b
        subtract_sum = a - b
        multiply_sum = a * b
        divide_sum = a / b
        return add_sum, subtract_sum, multiply_sum, divide_sum
    except ZeroDivisionError:
        print("错误：除数不能为零")
        return None

a, b = map(float, input("请输入两个数字（以空格分开）：").split())
result = calculate(a, b)
if result:
    print(f"和: {result[0]}, 差: {result[1]}, 积: {result[2]}, 商: {result[3]}")
```

```python
#  判断奇偶性
def is_even_or_odd(n):
    if n % 2 == 0:
        return "偶数"
    else:
        return "奇数"

n = int(input("请输入一个整数："))
result = is_even_or_odd(n)
print(f"用户输入的是{result}。")
```

```python
# 替换列表中的偶数为平方
def replace_square_number(lst):
    return [x**2 if x % 2 == 0 else x for x in lst]

n = [1, 2, 3, 4, 5]
x = replace_square_number(n)
print(x)  # 输出: [1, 4, 3, 16, 5]
```

```python
# 字符串反转
def reverse_string(s):
    return s[::-1]

n = 'abcdefg'
reversed_n = reverse_string(n)
print(reversed_n)  # 输出: gfedcba
```

```python
# 根据分数对学生排序
# 创建学生姓名和分数的字典
students = {
    "Alice": 90,
    "Bob": 85,
    "Charlie": 95,
    "David": 88,
    "Eve": 92
}

# 根据分数对学生进行降序排序
sorted_students = sorted(students.items(), key=lambda item: item[1], reverse=True)

# 输出排序结果
for name, score in sorted_students:
    print(f"{name}: {score}")
```

```python
# 斐波那契数列递归
from functools import lru_cache

@lru_cache(None)  # 缓存结果，避免重复计算
def fibonacci(n):
    if n == 1 or n == 2:
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)

n = int(input("请输入斐波那契数列的项数："))
print(f"第 {n} 项是：{fibonacci(n)}")
```

```python
# 文件读写
def count_word_frequency(filename):
    word_count = {}
    with open(filename, 'r', encoding='utf-8') as file:
        for line in file:
            words = line.strip().split()
            for word in words:
                word_count[word] = word_count.get(word, 0) + 1
    return word_count

filename = input("请输入文件名：")
word_freq = count_word_frequency(filename)
for word, count in word_freq.items():
    print(f"{word}: {count}")
```

```python
# 列表推导式
number_list = [i for i in range(1, 101) if i % 3 == 0 or i % 5 == 0]
print(number_list)

```

```python
#  异常处理
while True:
    number = input('请输入一个数字：')
    try:
        number = float(number)
        break
    except ValueError:
        print("---请重新输入---")

print(f"您输入的数字是：{number}")
```

```python
# 定义类 Rectangle
class Rectangle:
    def __init__(self, width, height):
        if width <= 0 or height <= 0:
            raise ValueError("宽度和高度必须为正数")
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

# 示例使用
rect = Rectangle(5, 10)
print(f"面积: {rect.area()}, 周长: {rect.perimeter()}")
```

### 2025/2/21

```python
# 罗马数字转阿拉伯数字(leecode算法题)
def romanToInt(self, s):
        roman_dict = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        total = 0

        for i in range(len(s)):
            if i < len(s) - 1 and roman_dict[s[i]] < roman_dict[s[i + 1]]:
                total -= roman_dict[s[i]]
            else:
                total += roman_dict[s[i]]
        return total
```

```python
# progression
class Progression:
    """Iterator producing a generic progression.

    Default iterator produces the whole numbers 0,1,2, ...
    """

    def __init__(self, start=0):
        """Initialize current to the first value of the progression."""
        self._current = start

    def _advance(self):
        """Update self._current to a new value.

        This should be overridden by a subclass to customize progression.
        By convention, if current is set to None, this designates the end of a finite progression.
        """
        self._current += 1

    def __next__(self):
        """Return the next element, or else raise StopIteration error."""
        if self._current is None:           # our convention to end a progression
            raise StopIteration()
        else:
            answer = self._current          # record current value to return
            self._advance()                 # advance to prepare for next time
            return answer

    def __iter__(self):
        """By convention, an iterator must return itself as an iterator."""
        return self

    def print_progression(self, n):
        """Print next n values of the progression."""
        print(' '.join(str(next(self)) for j in range(n)))


class ArithmeticProgression(Progression):
    """Iterator producing an arithmetic progression."""

    def __init__(self, increment=1, start=0):
        """Create a new arithmetic progression.


        increment   the fixed constant to add to each term (default 1)
        start       the first term of the progression (default 0)
        """
        super().__init__(start)             # initialize base class
        self._increment = increment

    def _advance(self):                     # override inherited version
        """Update current value by adding the fixed increment."""
        self._current += self._increment


class GeometricProgression(Progression):
    """Iterator producing a geometric progression."""

    def __init__(self, base=2, start=1):
        """Create a new geometric progression.


        base   the fixed constant multiplied to each term (default 2)
        start  the first term of the progression (default 1)
        """
        super().__init__(start)
        self._base = base

    def _advance(self):                     # override inherited version
        """Update current value by multiplying it by the base value."""
        self._current *= self._base


class FibonacciProgression(Progression):
    """Iterator producing a generalized Fibonacci progression."""

    def __init__(self, first=0, second=1):
        """Create a new fibonacci progression.


        first    the first term of the progression (default 0)
        second   the second term of the progression (default 1)
        """
        super().__init__(first)              # start progression at first
        self._prev = second - first          # fictitious value preceding the first

    def _advance(self):
        """Update current value by taking sum of previous two."""
        self._prev, self._current = self._current, self._prev + self._current


if __name__ == '__main__':
    print('Default progression:')
    Progression().print_progression(10)

    print('Arithmetic progression with increment 5:')
    ArithmeticProgression(5).print_progression(10)

    print('Arithmetic progression with increment 5 and start 2:')
    ArithmeticProgression(5, 2).print_progression(10)

    print('Geometric progression with default base:')
    GeometricProgression().print_progression(10)

    print('Geometric progression with base 3:')
    GeometricProgression(3).print_progression(10)

    print('Fibonacci progression with default start values:')
    FibonacciProgression().print_progression(10)

    print('Fibonacci progression with start values 4 and 6:')
    FibonacciProgression(4, 6).print_progression(10)

```

### 2025/2/23

```python
# 最长公共前缀
def longestCommonPrefix(strs):
    if not strs:
        return ""
    for i in range(len(strs[0])):
        char = strs[0][i]
        for s in strs[1:]:
            if i >= len(s) or s[i] != char:
                return strs[0][:i]
    return strs[0]

"""给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
每个右括号都有一个对应的相同类型的左括号。
"""
def isValid(s):
    if len(s) & 1 != 0:
        return False
    stack = []
    mapping = {')': '(', ']': '[', '}': '{'}
    for i in s:
        if i in mapping:
            if not stack or stack[-1] != mapping[i]:
                return False
            stack.pop()
        else:
            stack.append(i)
    return not stack
```

### 2025/2/28

```python
""" 编写一个Python程序，接受一个字符串作为输入，并输出该字符串中出现次数最多的字符及其出现次数。"""
def count_str():
    n = input("输入一个字符串: ").strip()
    if not n:
        return "空字符串"
    count_dict = {}
    for char in n:
        count_dict[char] = count_dict.get(char, 0) + 1
    max_char = max(count_dict, key=lambda k: count_dict[k])
    return max_char, count_dict[max_char]
    
"""实现一个Python函数，接受一个整数列表作为参数，返回列表中所有偶数的平方和。"""
def sum_even_square(n):
    even_square_total = sum([i ** 2 for i in n if i % 2 == 0])
    return even_square_total

""" 编写一个Python程序，模拟一个简单的银行账户管理系统。要求实现账户的创建、存款、取款、查询余额等功能。"""
class BankAccount:
    def __init__(self, name, gender, phone):
        self.name = name
        self.gender = gender
        self.phone = phone
        self.balance = 0
    
    def deposit(self, amount):
        self.balance += amount
    
    def withdraw(self, amount):
        if amount > self.balance:
            raise ValueError("余额不足")
        self.balance -= amount
    
    def get_balance(self):
        return self.balance

""" 编写一个Python程序，生成斐波那契数列的前N项，其中N由用户输入。"""
def fibonacci(n):
    fib_sequence = []
    a, b = 0, 1
    for _ in range(n):
        fib_sequence.append(a)
        a, b = b, a + b

    return fib_sequence
    
"""实现一个Python函数，接受一个字典作为参数，返回字典中值最大的键。"""
def max_dict_key(d):
    return max(d, key=lambda k: d[k])


"""实现一个Python函数，接受两个字符串作为参数，返回这两个字符串的最长公共子串。"""
def longest_common_substring(s1, s2):
    matrix = [[0]*(len(s2)+1) for _ in range(len(s1)+1)]
    max_len = 0
    end_pos = 0
    for i in range(1, len(s1)+1):
        for j in range(1, len(s2)+1):
            if s1[i-1] == s2[j-1]:
                matrix[i][j] = matrix[i-1][j-1] + 1
                if matrix[i][j] > max_len:
                    max_len = matrix[i][j]
                    end_pos = i
    return s1[end_pos-max_len:end_pos]



"""实现一个Python函数，接受一个列表作为参数，返回列表中所有元素的排列组合。"""
from itertools import permutations

def all_permutations(lst):
    return list(permutations(lst))

# 示例
print(all_permutations([1,2,3]))  # 输出所有排列

```



## 《数据结构与算法 python语言实现》练习题

### 第一章

```python
"""
编写一个python函数is_multiple(n, m),用来接收两个整数值n和m,如果n是m的倍数，即存在整数i使得n = mi,那么函数返回True,否则返回False.
"""


def is_multiple(n, m):
    if n % m == 0:
        return True
    else:
        return False


# AI优化
def is_multiple(n, m):
    if m == 0:
        raise ValueError("The divisor 'm' cannot be zero.")
    return n % m == 0


"""
编写一个Python函数is_even(k),用来接收一个整数K，如果k是偶数返回True，否则返回False。但是，函数不能使用乘法、除法或者取余操作。
"""


def is_even(k):
    a = []
    for i in range(0, k + 1, 2):
        a.append(i)
    if k in a:
        return True
    else:
        return False
###
不需要创建列表a，可以通过位运算或减法来判断奇偶性。
使用位运算k & 1可以高效判断是否为偶数（偶数的最低位为0）。
###

# AI优化
def is_even(k):
    return (k & 1) == 0

"""
编写一个python函数minmax(data)，用来在数的序列中找出最小数和最大数，并以一个长度为2的元组的形式返回。注意：不能通过内置函数min和max来实现。
"""


def minmax(data):
    sorted(data, reverse=False)
    return data[0], data[-1]


###
sorted(data)不会修改原列表，而是返回一个新的排序列表。因此，这里并没有真正排序data。
直接遍历列表找到最小值和最大值，避免不必要的排序操作。
###

# AI优化
def minmax(data):
    if not data:
        raise ValueError("The input list cannot be empty.")
    min_val = max_val = data[0]
    for num in data[1:]:
        if num < min_val:
            min_val = num
        if num > max_val:
            max_val = num
    return min_val, max_val

 
"""
编写一个python函数，用来接收正整数n，返回1~n的平方和。
"""


def square_add(n):
    s = 0
    for i in range(1, n + 1):
        s += i ** 2

    return s
###
可以直接使用数学公式计算平方和：n * (n + 1) * (2 * n + 1) // 6。
###

# AI优化
def square_add(n):
    return n * (n + 1) * (2 * n + 1) // 6

"""
基于Python的解析语法和内置函数sum，写一个单独的命令来计算上一题1~n的平方和。
"""

n = [1, 2, 3, 4]
n_square_add = sum([i**2 for i in n])
print(n_square_add)

###
列表解析可以用生成器表达式替代，节省内存。
###

# AI优化
n = [1, 2, 3, 4]
n_square_add = sum(i**2 for i in n)
print(n_square_add)

"""
编写一个python函数，用来接收正整数n,并返回1~n中所有奇数的平方和。
"""


def odd_square_add(n):
    s = 0
    for i in range(1, n + 1, 2):
        s += i ** 2

    return s

# AI优化
def odd_square_add(n):
    return sum(i**2 for i in range(1, n + 1, 2))

"""
基于Python的解析语法和内置函数sum，写一个单独的命令来计算上一题1~n中所有奇数的平方和。
"""

n = [1, 2, 3, 4]
n_odd_square_add = sum([i**2 for i in range(1, n + 1, 2)])
print(n_odd_square_add)

# AI优化
n = [1, 2, 3, 4]
n_odd_square_add = sum(i**2 for i in range(1, n + 1, 2))
print(n_odd_square_add)

"""
python允许负整数作为序列的索引值，如一个长度为n的字符串s，当索引值-n<=k<0时，所指的元素为s[k],那么求一个正整数索引值j>=0,使得s[j]指向的也是相同的元素。
"""

# k + j == 0

# AI优化
j = len(s) + k

"""
要生成一个值为50, 60, 70, 80的排列，求range构造函数的参数。
"""
# range(50, 81, 10)

"""
要生成一个值为8, 6, 4, 2, 0, -2, -4, -6, -8的排列，求range构造函数的参数。
"""

# range(8, -9, -2)

"""
演示怎么使用python列表解析语法来产生列表[1, 2, 4, 8, 16, 32, 64, 128, 256]。
"""
two_square_sequ = [2 ** i for i in range(0, 9)]


"""
python的random模块包括一个函数choice(data),可以从一个非空序列返回一个随机元素。
Random模块还包括一个更基本的randrange函数，参数化类似于内置的range函数，可以在给定范围内返回一个随机数。只使用randrange函数，实现自己的choice函数。
"""


import random

n = [1, 3, 8, 22, 32]
while True:
    m = random.randrange(1, 33)
    if m in n:
        print(m)
        break
    else:
        continue
###
不需要无限循环，直接从n中随机选择一个元素即可。
###
# AI优化
import random

def custom_choice(data):
    index = random.randrange(len(data))
    return data[index]

n = [1, 3, 8, 22, 32]
print(custom_choice(n))

```

### 第二章

```
# 给出3个生死攸关的软件应用程序的例子
"""
1. 医疗设备控制系统（如呼吸机、心脏起搏器）
作用：现代医疗设备（如呼吸机、心脏起搏器、放疗机）依赖软件精确控制治疗参数。例如：
呼吸机：调节氧气输送量和呼吸频率，维持危重患者的生命。
Therac-25 放疗机（历史案例）：1980年代因软件并发编程错误，导致多起患者因过量辐射死亡。
风险：软件故障可能导致设备失控，例如呼吸机停止工作或放疗剂量超标，直接危及患者生命。
2. 航空飞行控制系统（如飞机自动驾驶系统）
作用：现代客机的飞行控制系统（如自动驾驶、失速保护系统）依赖软件处理传感器数据并调整飞行姿态。
波音 737 MAX MCAS 系统：2018-2019年因软件错误（依赖单一传感器数据）导致两起空难，共346人死亡。
空客 A380 飞控系统：软件需实时协调数百万行代码，确保飞行安全。
风险：软件逻辑错误或传感器数据处理失误可能导致飞机失控或坠毁。
3. 核电站安全监控系统
作用：核电站使用软件监控反应堆温度、压力、辐射水平，并在异常时触发紧急停堆或冷却措施。
福岛核事故（2011年）：虽主要由硬件（海堤）和供电故障引发，但安全系统的软件响应速度直接影响事故严重性。
现代数字化控制系统：需实时处理数据并执行安全协议，防止堆芯熔毁或辐射泄漏。
风险：软件延迟或逻辑错误可能导致无法及时阻止灾难性后果。
"""
# 给出一个软件应用程序的例子，其中适应性意味着产品销售和破产的生命周期间的不同。
"""
案例：桌面出版软件（DTP）领域的生死竞争
QuarkXPress vs Adobe InDesign
背景：20世纪90年代，QuarkXPress 是桌面出版行业的绝对霸主，市场份额超过90%，广泛应用于杂志、报纸和印刷品设计。其软件功能强大，但商业模式僵化（高单价买断制），且用户体验封闭。

适应性差异如何决定生死
1. Adobe InDesign的适应性策略
技术适配：
Adobe于1999年推出InDesign，初期功能不如QuarkXPress，但通过快速迭代整合自家Photoshop、Illustrator的协同生态，吸引设计师。
2000年代初期，主动适配Mac OS X和Unicode（支持多语言），而QuarkXPress因兼容性延迟失去用户。
商业模式转型：
2013年推出Adobe Creative Cloud订阅服务，降低用户初始成本，并提供持续更新。
通过云端协作（如Adobe Stock、Libraries）适应远程办公趋势。
2. QuarkXPress的失败
技术停滞：
长期忽视用户对跨平台协作、XML数据整合的需求，更新缓慢。
2004年推出的QuarkXPress 7因兼容性问题遭用户抵制。
商业模式固化：
坚持高价买断制（单套软件超$1000），拒绝订阅模式，中小企业转向Adobe。
未建立生态，无法对抗Adobe的「全家桶」优势。
结果：适应性决定企业生死
Adobe：凭借持续适应市场需求，InDesign在2010年后市场份额反超，Quark公司收入暴跌，裁员收缩，濒临破产边缘。
Quark：从行业巨头沦为小众工具，2020年其母公司被迫出售资产，退出主流市场。
"""
# 描述文本编辑器GUI的组件和它的封装的方法
"""
文本编辑器 GUI 的典型组件与封装方法
文本编辑器的 GUI 设计需兼顾功能性与代码可维护性。以下是核心组件及其面向对象封装策略（以跨平台框架如 Qt 或 Java Swing 为例）：

1. 核心组件分解
1.1 顶层容器（MainWindow）
功能：窗口框架，包含菜单栏、工具栏、编辑区、状态栏等子组件。
封装方法：
Python
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.init_ui()
    
    def init_ui(self):
        self.setWindowTitle("Text Editor")
        self._create_menu_bar()  # 封装菜单栏逻辑
        self._create_tool_bar()  # 封装工具栏逻辑
        self._create_editor()    # 封装文本编辑区
        self._create_status_bar()# 封装状态栏
关键点：将不同区域的初始化逻辑拆分为独立方法，避免 MainWindow 类臃肿。
1.2 菜单栏（MenuBar）
功能：提供文件操作（新建、打开、保存）、编辑操作（撤销、重做）、格式设置等功能入口。
封装方法：
Python
class MenuBar(QMenuBar):
    def __init__(self, parent=None):
        super().__init__(parent)
        self._create_file_menu()
        self._create_edit_menu()
    
    def _create_file_menu(self):
        file_menu = self.addMenu("文件")
        new_action = QAction("新建", self)
        new_action.triggered.connect(self._on_new)  # 绑定事件
        file_menu.addAction(new_action)
    
    def _on_new(self):
        # 委托给主窗口或控制器处理业务逻辑
        self.parent().handle_new_file()  
关键点：
菜单项操作通过信号（如 triggered）与业务逻辑解耦。
禁止在 MenuBar 中直接操作文本内容，通过接口调用主窗口或控制器。
1.3 文本编辑区（TextEditorWidget）
功能：文本输入、语法高亮、行号显示、滚动支持。
封装方法（继承框架组件 + 扩展功能）：
Python
class TextEditorWidget(QPlainTextEdit):
    def __init__(self):
        super().__init__()
        self._init_editor_ui()
    
    def _init_editor_ui(self):
        self.setLineWrapMode(QPlainTextEdit.NoWrap)  # 禁用自动换行
        self.highlighter = SyntaxHighlighter(self.document())  # 语法高亮组件
        self.line_number_area = LineNumberArea(self)  # 行号区域（自定义绘制）
    
    def keyPressEvent(self, event):
        if event.key() == Qt.Key_Tab:
            self.insertPlainText("    ")  # 自定义 Tab 行为
        else:
            super().keyPressEvent(event)
关键点：
通过继承 QPlainTextEdit 复用基础功能，重写事件方法（如 keyPressEvent）实现定制行为。
将语法高亮、行号等子功能拆分为独立类（如 SyntaxHighlighter），通过组合模式注入。
1.4 状态栏（StatusBar）
功能：显示光标位置、文件编码、行/列统计等信息。
封装方法（观察者模式）：
Python
class EditorStatusBar(QStatusBar):
    def __init__(self, editor):
        super().__init__()
        self.editor = editor
        self._position_label = QLabel()
        self.addWidget(self._position_label)
        # 监听编辑器光标变化
        editor.cursorPositionChanged.connect(self._update_position)
    
    def _update_position(self):
        line = self.editor.textCursor().blockNumber() + 1
        column = self.editor.textCursor().columnNumber() + 1
        self._position_label.setText(f"行: {line}, 列: {column}")
关键点：通过事件监听（如 cursorPositionChanged）实现数据同步，状态栏不主动轮询编辑器状态。
2. 封装原则与设计模式
单一职责原则：每个类仅处理单一功能（如 MenuBar 只管理菜单项，不涉及文件读写逻辑）。
观察者模式：状态栏监听编辑器事件，而非直接访问其内部状态。
组合模式：将行号区域、语法高亮器等作为子组件注入编辑器。
MVC 分离：
Model：文本内容、用户配置（独立于 GUI 的纯数据类）。
View：MainWindow 及其子组件，仅负责渲染和输入事件。
Controller：处理业务逻辑（如文件保存、编辑操作），通过接口与 View 交互。
3. 进阶封装策略
插件系统：
Python
class PluginInterface(ABC):
    @abstractmethod
    def install(self, editor: TextEditorWidget):
        pass

class SpellCheckPlugin(PluginInterface):
    def install(self, editor):
        editor.installEventFilter(SpellCheckFilter())
通过接口定义插件规范，支持动态加载功能模块。
主题引擎：
Python
class ThemeManager:
    def apply_theme(self, theme: str):
        with open(f"themes/{theme}.json") as f:
            colors = json.load(f)
            QApplication.setPalette(colors["palette"])
将样式配置外部化（JSON/CSS），实现界面换肤。
总结
文本编辑器的 GUI 封装需遵循 高内聚、低耦合 原则，通过面向对象设计模式将组件模块化。例如：

使用继承复用框架控件功能（如 QPlainTextEdit）。
通过组合模式集成子功能（行号、高亮）。
借助观察者模式实现组件间通信。
这种设计使得代码易于扩展（如新增插件）和维护（修改某一组件不影响其他模块）。
"""
# 编写一个类Flower。该类有str、int、float类型的三种实例变量，分别代表花的名字、花瓣的数量和价格。该类必须含有一个构造函数，该构造函数给每个变量初始化一个合适的值。该类应包含设置和检索每种类型值的方法。
class Flower:
    def __init__(self, name: str = "", petals: int = 0, price: float = 0.0):
        """构造函数初始化花的属性，支持类型验证和自动转换"""
        self.set_name(name)
        self.set_petals(petals)
        self.set_price(price)

    # 名称属性方法组
    def set_name(self, name: str) -> None:
        """设置花名，强制字符串类型"""
        if not isinstance(name, str):
            raise TypeError("Name must be a string.")
        self._name = name

    def get_name(self) -> str:
        """返回花名"""
        return self._name

    # 花瓣属性方法组
    def set_petals(self, petals: int) -> None:
        """设置花瓣数，强制整数类型"""
        if not isinstance(petals, int):
            raise TypeError("Petals must be an integer.")
        self._petals = petals

    def get_petals(self) -> int:
        """返回花瓣数"""
        return self._petals

    # 价格属性方法组
    def set_price(self, price: float) -> None:
        """设置价格，支持整数/浮点数输入，自动转为浮点"""
        if isinstance(price, (int, float)):
            self._price = float(price)
        else:
            raise TypeError("Price must be a numeric type.")

    def get_price(self) -> float:
        """返回价格"""
        return self._price

    # 可选：属性式访问（兼容传统getter/setter）
    name = property(get_name, set_name)
    petals = property(get_petals, set_petals)
    price = property(get_price, set_price)
    
# 初始化实例
rose = Flower("Rose", 12, 9.99)

# 属性式访问
print(f"{rose.name} 有 {rose.petals} 瓣，售价 ${rose.price:.2f}")
# 输出：Rose 有 12 瓣，售价 $9.99

# 传统方法调用
rose.set_petals(24)
print(f"升级版 {rose.get_name()} 有 {rose.get_petals()} 瓣")
# 输出：升级版 Rose 有 24 瓣

# 类型安全验证测试
try:
    rose.set_name(123)  # 传入非字符串名称
except TypeError as e:
    print(f"错误捕获：{e}")
# 输出：错误捕获：Name must be a string.

# AI优化
class Flower:
    def __init__(self, name: str = "Unknown", petals: int = 0, price: float = 0.0):
        """
        构造函数，通过属性设置器进行初始化验证
        :param name: 花名，默认"Unknown"
        :param petals: 花瓣数，默认0
        :param price: 价格，默认0.0
        """
        self.name = name
        self.petals = petals
        self.price = price

    # 名称属性
    @property
    def name(self) -> str:
        """返回花名"""
        return self._name

    @name.setter
    def name(self, value: str):
        """设置花名，强制字符串类型"""
        if not isinstance(value, str):
            raise TypeError("花名必须为字符串类型")
        self._name = value

    # 花瓣属性
    @property
    def petals(self) -> int:
        """返回花瓣数量"""
        return self._petals

    @petals.setter
    def petals(self, value: int):
        """设置花瓣数，必须为非负整数"""
        if not isinstance(value, int):
            raise TypeError("花瓣数量必须为整数")
        if value < 0:
            raise ValueError("花瓣数量不能为负数")
        self._petals = value

    # 价格属性
    @property
    def price(self) -> float:
        """返回价格（保留两位小数）"""
        return self._price

    @price.setter
    def price(self, value: float):
        """设置价格，支持数值类型，自动保留两位小数"""
        if not isinstance(value, (int, float)):
            raise TypeError("价格必须为数字类型")
        if value < 0:
            raise ValueError("价格不能为负数")
        # 处理浮点精度，四舍五入到分
        self._price = round(float(value), 2)

    def __str__(self) -> str:
        """中文格式化输出"""
        return f"花卉详情：名称={self.name}，花瓣数={self.petals}，价格=￥{self.price:.2f}"

    def __repr__(self) -> str:
        """开发调试用表示"""
        return f"<Flower {self.name} (petals={self.petals}, price={self.price})>"


if __name__ == "__main__":
    # 正常使用测试
    lily = Flower("百合", 6, 15.99)
    print(lily)  # 花卉详情：名称=百合，花瓣数=6，价格=￥15.99

    # 边界值测试
    default_flower = Flower()
    print(default_flower)  # 花卉详情：名称=Unknown，花瓣数=0，价格=￥0.00

    # 价格精度测试
    rose = Flower("玫瑰", 12, 9.999)
    print(rose)  # 自动四舍五入 => 花卉详情：名称=玫瑰，花瓣数=12，价格=￥10.00

    # 异常处理测试
    try:
        Flower(123, 5, 9.99)  # 错误名称类型
    except TypeError as e:
        print(f"异常捕获：{e}")  # 花名必须为字符串类型

    try:
        Flower("雏菊", -3, 5.0)  # 负数花瓣
    except ValueError as e:
        print(f"异常捕获：{e}")  # 花瓣数量不能为负数

    try:
        Flower("郁金香", 6, "free")  # 非数字价格
    except TypeError as e:
        print(f"异常捕获：{e}")  # 价格必须为数字类型

    # 动态修改测试
    lily.petals = 8
    lily.price = 19.999  # 自动四舍五入为20.00
    print(f"升级版：{lily.name} 有 {lily.petals} 片花瓣，售价 {lily.price} 元")
    # 升级版：百合 有 8 片花瓣，售价 20.0 元

```



## 算法和数据结构的学习

### 前缀和算法思想

#### 核心方法：

1. 预处理
2. 区间和计算

### 递归和迭代

#### 核心概念对比

##### 递归（Recursion）

- **本质**：通过函数自我调用实现问题分解
- **数学模型**：符合分治法（Divide and Conquer）思想
- **关键要素**：
  - 基线条件（Base Case）：终止递归的明确条件
  - 递归条件（Recursive Case）：将问题分解为更小规模的子问题
- **典型应用**：树遍历、分形计算、回溯算法

##### 迭代（Iteration）

- **本质**：通过循环结构重复执行代码块
- **数学模型**：基于数学归纳法的逐步推进
- **关键要素**：
  - 循环条件（Termination Condition）
  - 状态变量（State Variable）
  - 迭代步长（Step Size）
- **典型应用**：数组遍历、数值计算、状态机实现

#### 执行机制对比

| 维度         | 递归                     | 迭代                 |
| ------------ | ------------------------ | -------------------- |
| **内存占用** | 调用栈存储上下文（O(n)） | 固定内存空间（O(1)） |
| **时间效率** | 函数调用开销较大         | 循环控制开销较小     |
| **可读性**   | 逻辑简洁但需抽象思维     | 步骤明确但可能冗长   |
| **调试难度** | 栈跟踪复杂               | 单步调试直观         |
| **适用场景** | 树状/分治问题            | 线性/重复计算        |

#### 经典案例对比分析

##### 阶乘计算

```python
# 递归实现
def factorial_r(n):
    return 1 if n == 0 else n * factorial_r(n-1)

# 迭代实现
def factorial_i(n):
    result = 1
    for i in range(1, n+1):
        result *= i
    return result
```

## 线性结构

### 数组(array)

#### 静态数组 vs 动态数组

1. **静态数组**

- **定义**： 编译时确定大小，内存分配在栈区或全局区的数组
- **特点**：
  + **不可变容量**： 初始化后大小固定（如C语言中的**int arr[10]**）
  + **内存分配**： 在栈内存中直接分配（访问速度快）
  + **类型约束**： 所有元素必须为相同类型（强类型语言）

   ```c
   int static_arr[5];  // 静态数组声明
   static_arr[0] = 10; //正确
   // static_arr[5] = 20; // 越界访问，导致未定义行为
   ```

2. **动态数组**

- **定义**： 运行时确定大小，内存分配在堆区的数组
- **特点**：
  + **可变容量**： 通过自动扩容机制动态调整大小（如Python列表）
  + **内存分配**： 通过指针管理堆内存（需要手动释放或依赖GC）
  + **类型灵活**： 在弱类型语言中可存储不同类型（如Python列表）
- **扩容原理**：
  1. 初始分配固定容量（如Python列表初始分配空间为**大于元素数量的最小2^n**)
  2. 当元素数量达到当前容量时：
     * 新容量 = 旧容量 * **扩容因子**（通常为1.5~2倍）
     * 申请新内存空间---->复制旧数据---->释放旧内存
  3. **均摊时间复杂度**：单次插入操作平均O(1)

#### 动态数组的实质

1. **与静态数组的关系**

   - **底层实现**: 动态数组本质是静态数组的封装

   - **核心差异**：

     | 特性         | 静态数组               | 动态数组               |
     | ------------ | ---------------------- | ---------------------- |
     | 内存分配位置 | 栈内存                 | 堆内存                 |
     | 容量可变性   | 固定大小               | 自动扩容               |
     | 访问速度     | 更快（无额外指针跳转） | 稍慢（需指针间接访问） |

2. **Python列表的真相**

   + **看似矛盾的现象**：
   
     ```python
     my_list = [1, "text", 3.14]  # 存储不同类型元素
     ```
   
   + **实现机制**：
   
     + 动态数组内部存储的是**对象指针**（所有元素均为**PyObject**类型）
     + 物理内存连续存储指针，而非实际数据
     + 实际数据分散在堆内存中，通过指针引用

#### 数据类型约束本质

1. **严格类型语言（C/Java**）

   - **内存结构**：直接存储元素值

     ```java
     int[] arr = new int[3]: 	//内存中连续存储3
     ```

   - **类型限制**：

     - 所有元素必须为声明类型
     - 访问时直接按类型长度计算偏移量

2. **弱类型语言（Python/JavaScript）**

   - **内存结构**： 存储指向对象的指针

     ```text
     Python列表内存布局：
     [指针0] --> 整数对象
     [指针1] --> 字符串对象
     [指针2] --> 浮点数对象
     ```

   - **特殊性质**：

     + **逻辑上**可存储不同类型
     + **物理上**指针数组仍然是连续内存空间

#### 关键概念对比表

![image-20250301101702153](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250301101702153.png)

#### 常见误区

**误区1： 动态数组直接存储数据**

- **真相**：动态数组存储的是指针（Python等语言），实际数据分散存储

**误区2： 所有语言的数组都允许不同类型元素**

- **正解**： 仅在弱类型语言中成立， 强类型语言严格限制元素类型

**误区3： 动态数组扩容是实时完成的**

- **实际策略**： 采用**预分配机制**（超额分配）如Python List

### 链表（Linked List)

#### 什么是链表（Linked List）?

定义： 链表是由一系列节点（Node）组成的线性数据结构，每个节点包含：

1. **数据域**： 存储实际数据
2. **指针域**： 存储下一个节点的内存地址

核心特征：

+ **非连续存储**： 节点在内存中分散存放
+ **动态扩展**： 不需要预先分配固定空间
+ **单向/双向**： 单链表每个节点只有一个指针，双链表有两个指针（前驱和后继）

#### 链表的作用

1. **动态内存管理**

```python
# 传统数组需要预先分配连续内存
arr = [None] * 10 			# 强制占用10个位置

# 链表按需动态分配内存
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None	# 随时可扩展新节点
```

2. 高效插入/删除

| 操作     | 数组时间复杂度 | 链表时间复杂度  |
| -------- | -------------- | --------------- |
| 头部插入 | O(n)           | O(1)            |
| 中间插入 | O(n)           | O(1) (已知位置) |
| 尾部插入 | O(1)           | O(n)            |

#### 链表存在的意义

1. **解决数组的痛点**
   + **内存碎片利用**： 允许使用分散的内存块
   + **避免整体复制**： 插入元素无需移动其他元素
   + **无限扩展性（理论上）**： 无固定容量限制
2. **特殊场景优势**
   + **实现栈/队列**： 适合频繁的头部操作
   + **内存敏感场景**： 嵌入式系统中管理动态内存
   + **内核开发**：Linux内核的任务调度使用链表

#### 哨兵节点技巧（Dummy Node）

1. **作用**

   + 消除头节点的特殊性处理
   + 统一所有节点的操作逻辑

2. **使用示例（单链表删除节点）**

   ```python
   def delete_node(head, val):
       dummy = Node(0)  # 哨兵节点
       dummy.next = head
       curr = dummy
       
       while curr.next:
           if curr.next.val == val:
               curr.next = curr.next.next
               break
           curr = curr.next
       return dummy.next  # 返回新头节点
   ```

3. **哨兵节点优势对比**

   | 场景       | 无哨兵代码行数 | 有哨兵代码行数 |
   | ---------- | -------------- | -------------- |
   | 空链表     | 需要特殊处理   | 无需处理       |
   | 删除头节点 | 单独逻辑判断   | 统一处理       |

#### 链表节点的本质

1. **节点结构示例**

```python
class ListNode:
    def __init__(self, x):
        self.val = x	# 数据域
        self.next = None  # 指针域（单链表）
        # self.prev = None	# 双向链表需要前驱指针
```

2. **节点连接示意图**

   ```text
   节点A             节点B             节点C
   +-------+------+  +-------+------+  +-------+------+
   | val=5 | next |→ | val=3 | next |→ | val=7 | next |→ None
   +-------+------+  +-------+------+  +-------+------+
   ```

#### 指针在链表中的本质

1. **指针的物理含义**

   + 内存地址标识符： 每个节点存放的位置标记
   + 引用传递工具： 通过地址找到下一个节点

2. **Python中的实现特性**

   虽然Python没有显式指针，但通过**对象引用**实现相同的功能：

   ```python
   class ListNode:
       def __init__(self, x):
           self.val = x	# 数据域
           self.next = None  # 指针域（单链表）
           # self.prev = None	# 双向链表需要前驱指针
   
           
   # 创建两个节点
   node1 = ListNode(10)
   node2 = ListNode(20)
   
   # 通过引用建立连接
   node1.next = node2  # node1的next指针指向node2
   ```

#### 数组 vs 链表

![image-20250302132439368](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250302132439368.png)

```text
是否需要频繁中间插入/删除？
├── 是 → 链表
└── 否 → 
    ├── 是否需要高速随机访问？
    │   ├── 是 → 数组
    │   └── 否 → 
    │       ├── 内存是否敏感？
    │       │   ├── 是 → 数组
    │       │   └── 否 → 链表
    └── 是否需要保证内存连续性？
        ├── 是 → 数组
        └── 否 → 链表
```

![image-20250302132534360](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250302132534360.png)

##### 关键对比表

![image-20250302130612635](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250302130612635.png)



### 栈和队列

#### 栈与队列的本质定义

1. **栈（stack）**
   - **结构特性**: LIFO（Last In First On， 后进先出）
   - **核心操作**:
     + **push()**: 元素入栈（时间复杂度O(1)）
     + **pop()**: 弹出栈顶元素（O(1)）
     + **peek()**: 查看栈顶元素（O(1)）
2. **队列（Queue）**
   + **结构特性**: FIFO（First In First Out， 先进先出）
   + **核心操作**: 
     + **enqueue()**: 元素入队尾（O(1)）
     + **dequeue()**: 从队首出队（O(1)）
     + **front()**: 查看队首元素（O(1)）

#### 关键实现细节

1. **栈的实现选择**

   | 实现方式 | 优点                 | 缺点                   | 典型场景           |
   | -------- | -------------------- | ---------------------- | ------------------ |
   | 数组     | 缓存友好，访问速度快 | 扩容成本高             | 明确最大深度的场景 |
   | 链表     | 动态扩展无内存浪费   | 指针跳转增加缓存未命中 | 深度不可预知的场景 |

   ```python
   # 基于列表实现栈
   class ArrayStack:
       def __init__(self):
           self._data = []
       
       def push(self, val):
           self._data.append(val)  # O(1)均摊时间
       
       def pop(self):
           if not self._data:
               raise IndexError("Pop from empty stack")
           return self._data.pop()
   ```

2. **队列的实现陷阱**

   - **假溢出问题**: 数组实现的队列需要循环缓冲区
   
   - **线程安全**: 多线程环境需使用双锁或原子操作

   - **优先队列**：基于堆实现按优先级出队
   
     ```python
     class CircularQueue:
         def __init__(self, capacity):
             self._data = [None] * (capacity + 1)  # 多留一个空位判满
             self._head = 0
             self._tail = 0
         
         def enqueue(self, val):
             if (self._tail + 1) % len(self._data) == self._head:
                 raise Exception("Queue is full")
             self._data[self._tail] = val
             self._tail = (self._tail + 1) % len(self._data)
     ```
   

#### 典型应用场景

1. **栈的核心应用**

   + **括号匹配**（LeetCode 20）

   ```python
   def is_valid(s: str) -> bool:
       stack = []
       mapping = {')':'(', ']':'[', '}':'{'}
       for char in s:
           if char in mapping:
               top = stack.pop() if stack else '#'
               if mapping[char] != top:
                   return False
           else:
               stack.append(char)
       return not stack
   ```

   + **函数调用栈**: 程序执行时的上下文存储
   + **撤销操作**： 操作历史栈

2. 队列的核心应用

   - **BFS广度优先搜索**（LeetCode 102二叉树层序遍历）

   ```python
   from collections import deque
   def level_order(root):
       if not root: return []
       res = []
       queue = deque([root])
       while queue:
           level = []
           for _ in range(len(queue)):
               node = queue.popleft()
               level.append(node.val)
               if node.left: queue.append(node.left)
               if node.right: queue.append(node.right)
           res.append(level)
       return res
   ```

   - **消息队列**： 系统间异步通信
   - **打印机任务调度**： 按提交顺序处理

#### 选择决策树

```text
需要处理最近关联元素吗？
├── 是 → 使用栈（如括号匹配、递归展开）
└── 否 → 
    ├── 需要保持处理顺序吗？
    │   ├── 是 → 使用队列（如任务调度、BFS）
    │   └── 否 → 
    │       ├── 需要优先级处理吗？
    │       │   ├── 是 → 优先队列（如Dijkstra算法）
    │       │   └── 否 → 基本队列
    └── 需要双向操作吗？
        ├── 是 → 双端队列（如滑动窗口）
        └── 否 → 基本队列
```

#### 在数据结构体现中的地位

1. **算法基础支撑**

   + **递归的本质**: 函数调用栈的隐式使用
   + **DFS vs BFS**: 显式使用栈和队列
   + **语法解析**: 编译器使用栈进行语法树构建

2. **系统底层引用**

   ![image-20250303093153318](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250303093153318.png)

3. **进阶算法基石**

   + **单调栈**: 解决Next Greater Element类问题 （LeetCode 496）

   + **优先队列**: 合并K个有序链表 (LeetCode 23)

   + **双栈实现队列** (LeetCode 232)

     ```python
     class MyQueue:
         def __init__(self):
             self.in_stack = []
             self.out_stack = []
     
         def push(self, x):
             self.in_stack.append(x)
         
         def _transfer(self):
             if not self.out_stack:
                 while self.in_stack:
                     self.out_stack.append(self.in_stack.pop())
         
         def pop(self):
             self._transfer()
             return self.out_stack.pop()
     ```

#### 常见误区警示

1. **栈溢出风险**:
   - 递归深度过大导致栈溢出（Python默认递归深度约1000层）
   - 解决方案： 改用迭代或者尾递归优化
2. **队列假满判断**：
   - 循环队列中**head == tail**既可表示空也可以表示满
   - 正确做法： 始终保留一个空位或使用计数器
3. **时间复杂度误判**：
   + 动态数组实现的栈： **push()**操作均摊O(1)但单词可能O(n)
   + 链式队列的**dequeue()**需注意指针操作的顺序

### 哈希表（Hash Table）

#### 哈希表（Hash Table）的本质

哈希表是一种通过**键（Key）直接访问值（Value）**的数据结构，其核心设计包含两个关键组件：

1. **哈希函数（HashFunction）**
   - 将任意大小的数据（Key）映射到固定范围的整数值（哈希值）
   - 数学表达： hash(key) --> integer
2. **存储结构**
   - **数组**： 存储数据的核心容器
   - **冲突解决机制**： 处理不同Key映射到同一数组索引的情况

#### 哈希函数的核心特征

| 特征         | 说明                                                | 示例（Python内置哈希）                     |
| ------------ | --------------------------------------------------- | ------------------------------------------ |
| **确定性**   | 相同Key始终得到相同哈希值                           | hash("apple")恒为固定值                    |
| **均匀性**   | 哈希值应均匀分布在值域范围内                        | 好的哈希函数减少冲突概率                   |
| **高效性**   | 计算速度快（时间复杂度O(1)）                        | 字符串哈希通常设计为线性时间               |
| **抗碰撞性** | 不同Key生成相同哈希值的概率低（密码学哈希要求更高） | MD5、SHA-1（但常规哈希表不要求密码学强度） |

#### 可哈希性（Hashability）判断

在python中，一个对象是否可哈希由以下特征决定:

1. **可哈希对象的核心特征**

   + **不可变性（Immutable）**: 对象创建后无法修改内部状态
   + **实现\_\_hash\_\_()方法**: 返回整型哈希值
   + **实现\_\_eq\_\_()方法**: 用于比较相等性

2. Python内置类型的可哈希性

   ![image-20250303104231624](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250303104231624.png)

3. 自定义类的可哈希性

   ```python
   class User:
       def __init__(self, id):
           self.id = id  # 若id不可变，可哈希
       
       def __hash__(self):
           return hash(self.id)
       
       def __eq__(self, other):
           return self.id == other.id
   
   # 此时User实例可作为字典的键
   user_dict = {User(1001): "Alice"}
   ```

#### 哈希表的工作原理

1. 存储结构示意图

   ```text
   索引 | 存储内容（假设使用链地址法）
   -----|------------------------------
   0    | → (key1, val1) → (key4, val4)
   1    | → (key2, val2)
   2    | 空
   3    | → (key3, val3)
   ```

2. **操作流程**

   + **插入数据**:
     1. 计算机Key的哈希值<strong>`h = hash(key)`</strong>
     2. 计算数组索引<strong>`index = h % array_size`</strong>
     3. 处理冲突（如链地址法将节点挂到链表）
   + 查找数据:
     1. 同样计算索引定位到桶（Bucket）
     2. 遍历桶内元素比较Key（需要<strong>`__eq__`</strong>方法）

3. 冲突解决策略

   | 策略           | 原理                     | 优点               | 缺点                   |
   | -------------- | ------------------------ | ------------------ | ---------------------- |
   | **链地址法**   | 每个桶用链表存储冲突元素 | 简单，适合频繁插入 | 指针跳转增加缓存未命中 |
   | **开放寻址法** | 线性探测下一个空槽       | 缓存友好，内存紧凑 | 删除操作复杂           |

#### 哈希表在数据结构体系中角色

1. **核心地位**

   + **基础数据结构**： 与数组、链表、树同为构建复杂系统的基石
   + **高效操作**： 平均O(1)的查找/插入/删除时间复杂度

2. **典型应用场景**

   ![image-20250303105500161](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250303105500161.png)

3. **进阶衍生结构**

   + **布隆过滤器（Bloom Filter）**: 概率型数据结构，用于快速判断元素不存在
   + **一致性哈希**：分布式系统负载均衡的关键算法
   + **完美哈希**：无冲突的静态哈希表构造方法

#### 性能优化关键点

1. **负载因子（Load Factor）控制**

   ```python
   # Python字典的自动扩容策略
   load_factor = used_buckets / total_buckets
   # 当负载因子超过2/3时触发扩容（容量翻倍）
   ```

2. **哈希函数设计原则**

   + **雪崩效应**： 微小输入变化导致哈希值剧烈变化
   + **避免聚焦**： 防止大量Key映射到相邻索引

3. **冲突处理效率**

   ```text
   最坏情况时间复杂度：
   - 无冲突 → O(1)
   - 全冲突 → O(n)（退化为链表） 
   ```

### 经典问题

```python3
# Leetcode 146 LRU缓存
class DLinkedNode:
    def __init__(self, key=0, value=0):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.cache = dict()
        self.capacity = capacity
        self.head = DLinkedNode()
        self.tail = DLinkedNode()
        self.head.next = self.tail
        self.tail.prev = self.head

    def _remove_node(self, node):
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node

    def _add_to_head(self, node):
        node.prev = self.head
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node

    def _move_to_head(self, node):
        self._remove_node(node)
        self._add_to_head(node)

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        node = self.cache[key]
        self._move_to_head(node)
        return node.value

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            node = self.cache[key]
            node.value = value
            self._move_to_head(node)
        else:
            new_node = DLinkedNode(key, value)
            if len(self.cache) >= self.capacity:
                last_node = self.tail.prev
                self._remove_node(last_node)
                del self.cache[last_node.key]
            self.cache[key] = new_node
            self._add_to_head(new_node)
```

## 树形结构

### 二叉树和二叉搜索树

1. **二叉树（Binary Tree）**

   - **定义**：每个节点最多有**两个子节点**（左子节点和右子节点）的树形结构。

   - **特点**：

     - 节点间没有顺序限制
     - 结构灵活，可表示层次关系。

   - 示例：

     ```text
           A
          / \
         B   C
        / \   \
       D  E    F
     ```

2. **二叉搜索树（Binary Search Tree， BST）**

   - **定义**：在二叉树基础上增加**有序性约束**：

     - 左子树所有节点的值**小于**根节点
     - 右子树所有节点的值**大于**根节点

   - 特点：

     - 支持高效查找、插入、删除（平均O(log n)）
     - 中序遍历结果为**升序序列**

   - **示例**：

     ```text
           8
          / \
         3   10
        / \    \
       1  6    14
     ```

#### 递归 vs 迭代实现二叉树

1. **递归实现**

   - **优点**：

     - 代码简洁，逻辑直观（符合树的分形特性）
     - 天然匹配树的层次遍历逻辑

   - **缺点**：

     - 栈溢出风险（深度过大时）
     - 调试困难

   - **示例（前序遍历）**：

     ```python
     def preorder(root):
         if not root:
             return
         print(root.val)
         preorder(root.left)
         preorder(root.right)
     ```

2. **迭代实现**

   - **优点**：

     - 无栈溢出风险（手动控制栈/队列）
     - 内存使用可控

   - **缺点**：

     - 代码复杂度高
     - 需要显式管理数据结构

   - **示例（前序遍历）**：

     ```python3
     def preorder_iterative(root):
         stack = [root]
         while stack:
             node = stack.pop()
             if node:
                 print(node.val)
                 stack.append(node.right)  # 右子节点先入栈
                 stack.append(node.left)
     ```

3. 对比表

   ![image-20250314095734031](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250314095734031.png)


#### 二叉树解决的问题

1.  **数据层次化存储**

    - **应用场景**：
        - 文件系统目录结构
        - 组织架构图
        - 家谱关系

2.  **高效搜索与动态操作**

    - **优势对比**：

        ![image-20250314095950635](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250314095950635.png)

3. **特殊场景优化**

    - **哈夫曼编码**： 使用二叉树生成最优前缀码

    - **表达式解析**： 构建语法树处理运算优先级

        ```text
        表达式 (3 + 5) * 2 对应的二叉树：
              *
             / \
            +   2
           / \
          3   5
		```

#### 树形结构的意义

1. **突破线性结构限制**
    - **线性结构缺陷**
        - 数组： 插入/删除效率低（需移动元素）
        - 链表： 随机访问效率低（需遍历）
2. **高效分层管理**
    - **分层优势**
        - 快速缩小搜索范围（如BST每次比较排除一半子树）
        - 自然表达包含关系（如XML/JSON解析）
3. **平衡时间与空间**
    - **复杂度优化**：
        - 树结构在动态操作与查询间取得平衡
        - 通过平衡策略（如AVL树、红黑树）保持高效

#### 二叉搜索树的核心功能

1. **高效查找**

   - **实现机制**：

     ```python3
     def search(root, target):
         while root:
             if root.val == target:
                 return True
             elif target < root.val:
                 root = root.left
             else:
                 root = root.right
         return False
     ```

2.  **动态维护有序数据集**

   - **插入操作**：

     ```python
     def insert(root, val):
         if not root:
             return TreeNode(val)
         if val < root.val:
             root.left = insert(root.left, val)
         else:
             root.right = insert(root.right, val)
         return root
     ```

3. **范围查询与遍历**

   - **中序遍历有序输出**：

     ```python
     def inorder(root):
         if root:
             inorder(root.left)
             print(root.val)
             inorder(root.right)
     ```

4.  **支持衍生结构**

   - **平衡BST**: 如AVL树、红黑树，解决普通BST退化为链表的问题
   - **数据库索引**：B树、B+树基于BST思想优化磁盘I/O

#### 实际应用案例

1. **数据库系统**

   - **索引结构**： MySQL的InnoDB引擎使用B+树（BST的扩展）加速查询

2. **游戏开发**

   - **场景管理**： 四叉树（二维空间划分）优先碰撞检测

3. **机器学习**

   - **决策树**： 二叉树结构实现分类模型

     ```text
     是否购买电脑？
     ├── 年龄<=30 → 继续询问学生身份
     └── 年龄>30 → 直接推荐购买
     ```


### AVL树（Adelson-Velsky and Landis Tree）

#### AVL树的定义

**AVL树**（Adelson-Velsky and Landis Tree）是最早发明的 **自平衡二叉搜索树**。其核心特性是通过 **平衡因子**（Balance Factor）维护树的平衡性，确保任意节点的左右子树高度差不超过1。

- **平衡因子**：**左子树高度 - 右子树高度**
- **平衡规则**： 每个节点的平衡因子绝对值 <= 1

#### AVL树的作用

1. **防止二叉搜索树退化**

   普通BST在插入有序数据时会退化为链表（时间复杂度从O(log n)退化为O(n)）， AVL树通过自动平衡避免这一问题。

2. **保证高效操作**

   所有操作（查找、插入、删除）的时间复杂度稳定为O(log n)。

3. **优化数据查询场景**

   适用于频繁查询但较少修改的场景（如数据库索引）。

#### AVL树 vs 二叉搜索树

![image-20250315111048940](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250315111048940.png)

#### AVL树的核心机制

1. **平衡因子维护**

   每个节点额外存储**高度信息**，插入或删除后递归更新高度并检查平衡因子:

   ```python3
   class AVLNode:
       def __init__(self, val):
           self.val = val
           self.left = None
           self.right = None
           self.height = 1  # 新增高度属性
   ```

2. **旋转操作(可能有误)**

   当平衡因子超出±1时，通过旋转恢复平衡。共有**四种旋转类型**:

   1. **左旋（Left Rotation）** ：解决右子树过高的情况。
   2. **右旋（Right Rotation）** ：解决左子树过高的情况。
   3. **左右旋（LR Rotation）** ：先左旋左子树，再右旋当前节点。
   4. **右左旋（RL Rotation）** ：先右旋右子树，再左旋当前节点。

   ```python3
   def right_rotate(z):
       y = z.left
       T3 = y.right
   
       y.right = z
       z.left = T3
   
       # 更新高度（需重新计算z和y的高度）
       z.height = 1 + max(get_height(z.left), get_height(z.right))
       y.height = 1 + max(get_height(y.left), get_height(y.right))
       
       return y  # 新的根节点
   ```

#### AVL树解决的问题

1. **BST的性能退化问题**

   输入有序数据时，BST退化为链表，操作效率骤降。

   **示例**： 依次插入1，2，3，4，5， AVL树会自动平衡，而BST会变成右斜链。

2. **动态数据高效维护**

   在频繁插入/删除的场景中，保持稳定的查询效率。

#### 知识点补充

1. **插入操作步骤**

   1. **标准BST插入**： 按二叉搜索树规则插入新节点。
   2. **更新高度**： 从插入点向上回溯更新祖先节点高度。
   3. **检查平衡因子**： 若某节点失衡， 进行旋转调整。

2. **删除操作的特殊性**

   - 删除可能导致多个祖先节点失衡，需从删除点向上逐层检查并旋转。
   - 时间复杂度仍为O(log n), 但实际开销比插入更大。

3. **平衡代价的权衡**

   ![image-20250315112106759](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250315112106759.png)

4. **高度与节点数的关系**

   AVL树的高度h与节点数n满足：

   $$ h \leq 1.44 \log_{2}(n + 2) - 0.328 $$

   这意味着即使最坏情况下，AVL树的高度仍为O(log n)。

#### 实战应用

1. **数据库索引**

   - **场景**： MySQL的MEMORY存储引擎使用AVL树实现索引。
   - **优势**： 精确范围查询和快速点查。

2. **实时系统**

   - **场景**：航空管制系统中的航班优先级队列。
   - **优势**： 保证最坏的情况下的操作延迟可控。

3. **代码实现（插入核心逻辑）**

   ```python3
   def insert(root, key):
       # 1. 标准BST插入
       if not root:
           return AVLNode(key)
       elif key < root.val:
           root.left = insert(root.left, key)
       else:
           root.right = insert(root.right, key)
       
       # 2. 更新高度
       root.height = 1 + max(get_height(root.left), get_height(root.right))
       
       # 3. 检查平衡因子
       balance = get_balance(root)
       
       # 4. 处理失衡
       # 左左失衡
       if balance > 1 and key < root.left.val:
           return right_rotate(root)
       # 右右失衡
       if balance < -1 and key > root.right.val:
           return left_rotate(root)
       # 左右失衡
       if balance > 1 and key > root.left.val:
           root.left = left_rotate(root.left)
           return right_rotate(root)
       # 右左失衡
       if balance < -1 and key < root.right.val:
           root.right = right_rotate(root.right)
           return left_rotate(root)
       
       return root
   ```
### 红黑树（Red-Black Tree）

#### 什么是红黑树？

   红黑树是一种自平衡二叉搜索树，通过引入颜色标记（红色或黑色）和旋转操作，在插入和删除节点时动态调整树的结构，确保以下核心性质：

   1. 节点颜色： 每个节点是红色或黑色
   2. 根节点： 根节点是黑色。
   3. 叶子节点（NIL）： 所有叶子节点（空节点）是黑色。
   4. 红色节点的子节点： 红色节点的子节点必须是黑色（即不允许连续红色节点）。
   5. 黑色路径一致性：从任意节点到其后代叶子节点的路径中，黑色节点的数量相同（称为"黑高"）。

   1. 红黑树定义

      红黑树是一种近似平衡的二叉搜索树，通过颜色标记和规则约束，确保从根到叶子的最长路径不超过最短路径的2倍。

   2. 红黑规则

      1. 每个节点为红色或黑色
      2. 根节点为黑色
      3. 叶子节点（NIL节点）为黑色
      4. 红色节点的子节点必须为黑色（无连续红节点）
      5. 从任一节点到其所有叶子节点的路径包含相同数量的黑色节点（黑高相同）

   3. 与AVL树的对比

      ![image-20250315163150925](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250315163150925.png)

#### **为何实际开发更常见红黑树？**
**1. 性能权衡**
- **插入/删除效率**：红黑树的调整代价更低（旋转次数更少）
  例如，插入时红黑树最多2次旋转，而AVL树可能需要O(log n)次旋转。
- **综合性能**：在频繁动态修改的场景中，红黑树在查询与修改间取得更好平衡。
**2. 实现简化**
- **颜色标记替代高度计算**：红黑树通过颜色规则简化了平衡判断逻辑，减少了维护成本。
**3. 实际应用案例**
- **Java的TreeMap**：基于红黑树实现键值对的有序存储。
- **Linux内核进程调度**：使用红黑树管理就绪队列，快速定位高优先级任务。
- **C++ STL的map/set**：底层采用红黑树保障高效操作。
#### 红黑树的核心操作
**1. 插入调整**
插入新节点（默认红色）后，可能违反红黑规则，需通过以下操作修复：
- **颜色翻转**（Recoloring）
- **旋转**（Rotation）
**典型调整场景**：
1. **叔节点为红色** → 颜色翻转
2. **叔节点为黑色** → 旋转 + 颜色调整
**2. 删除调整**
删除节点后，若破坏黑高规则，需通过类似插入的调整策略修复，但逻辑更复杂。
**3. 时间复杂度**
- 查找：O(log n)
- 插入/删除：O(log n)（均摊时间）

#### 总结：为何需要红黑树?

1. **平衡效率与实现复杂度**：在保持近似平衡的前提下，减少维护成本。
2. **适应动态数据场景**：适合频繁插入/删除的场景（如数据库事务日志）。
3. **工程实践优化**：相比AVL树，红黑树在综合性能上更贴近实际系统需求。

### 堆（Heap）

#### 堆（Heap）的定义

**堆**是一种特殊的**完全二叉树**，满足以下性质：

- **堆属性**： 每个节点的值 ≥（最大堆）或 ≤ （最小堆）其子节点的值。
- **结构特性**：所有层级（除最后一层）完全填充，最后一层节点尽可能左对齐。

示例（最大堆）：

```text
        90
       /  \
      70   80
     / \   /
    60 20 75
```

#### 堆 vs 栈 vs 队列

1. **数据结构特性对比**

   ![image-20250316094144214](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250316094144214.png)

2. **内存管理中的“堆”与数据结构堆**

   - **内存堆**： 程序运行时动态分配内存的区域（如**malloc()**操作）。
   - **数据结构堆**：一种树形结构，用于高效管理优先级。
   - **关键区别**：二者概念不同，仅名称相同，功能无关联。

#### 堆的特点与不足

**优点**

1. **高效极值操作**： 获取最大/最小元素时间复杂度为O(1)。
2. **动态维护效率**： 插入和删除操作时间复杂度为O(log n)。
3. **空间紧凑**： 可用数组实现， 无需额外指针存储（完全二叉树特性）。

**缺点**

1. **不支持快速搜索**： 查找非极值元素需要O(n)时间。
2. **内存占用**： 数组实现需预留空间（动态数组扩容有成本）。
3. **构建成本**： 将无序数组构建成堆需O(n)时间，优于逐个插入的O(n log n)。

#### 堆为何是树形结构？

1. **层级关系需求**： 堆属性要求父子节点间有明确的大小关系，树形结构天然支持这种层级比较。
2. **操作高效性**：
   - **上浮（Percolate Up）**： 插入元素后， 通过树路径向上调整。
   - **下沉（Percolate Down）**： 删除根节点后， 将末尾元素移至根部并向下调整。
3. **数组实现可行性**： 完全二叉树可映射到数组，无需指针（索引计算父子关系）：
   - 父节点索引： **parent(i) = (i-1) // 2**
   - 左子节点索引： **left_child(i) = 2*i + 1**
   - 右子节点索引： **right_child(i) = 2*i + 2**

####  堆的知识点补充

1. **堆的数组表示**

   ```python3
   # 最大堆示例（数组存储）
   heap = [90, 70, 80, 60, 20, 75]
   # 索引映射：
   #       0(90)
   #     /     \
   #    1(70)  2(80)
   #   /  \    /
   # 3(60)4(20)5(75)
   ```

2. **堆的核心操作**

   - **插入元素：**

     ```python3
     def heap_insert(heap, val):
         heap.append(val)
         idx = len(heap) - 1
         # 上浮调整
         while idx > 0 and heap[idx] > heap[(idx-1)//2]:
             heap[idx], heap[(idx-1)//2] = heap[(idx-1)//2], heap[idx]
             idx = (idx-1) // 2
     ```

   - **删除堆顶元素：**

     ```python3
     def heap_extract_max(heap):
         if not heap:
             return None
         max_val = heap[0]
         heap[0] = heap[-1]
         heap.pop()
         idx = 0
         # 下沉调整
         while True:
             left = 2*idx + 1
             right = 2*idx + 2
             largest = idx
             if left < len(heap) and heap[left] > heap[largest]:
                 largest = left
             if right < len(heap) and heap[right] > heap[largest]:
                 largest = right
             if largest == idx:
                 break
             heap[idx], heap[largest] = heap[largest], heap[idx]
             idx = largest
         return max_val
     ```

3. **堆的应用场景**

    - **堆排序：** 时间复杂度O(n log n)，空间复杂度O(1)。
    - **优先队列：** 操作系统进程调度、Dijkstra最短路径算法。
    - **Top K 问题：** 快速找出海量数据中最大/最小的K个元素。

4. **堆的变种**

    ![image-20250316100106536](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250316100106536.png)

#### 总结

- **堆的核心价值：** 在动态数据流中高效维护极值。
- **选择建议：**
  - 需要快速获取最大/最小值 ➡堆
  - 需要先进先出管理➡队列
  - 需要后进先出管理➡栈
- **工程实践**： 优先使用语言内置的堆实现（如Python的**heapq**模块）

### Trie树

#### Trie树的定义

**Trie树**（发音"try"），又称**前缀树**或**字典树**，是一种专用于**字符串快速检索**的树形数据结构。其核心特点是**利用字符串的公共前缀减少重复存储**，从而实现高效查询。

- **结构特性**：
  - 每个节点表示**一个字符**。
  - 从根节点到某一节点的路径，构成该节点对应的字符串。
  - 根节点为空字符，标记字符串的起点。
  - 叶子节点（或特定标记节点）表示字符串的结束。

**示例(存储"apple","app","banana")：**

```text
        (root)
       /     \
      a       b
     /         \
    p           a
   / \           \
  p   p           n
 /     \           \
l       l           a
 \       \           \
  e (★)   e (★)       n
                     \
                      a (★)
```

#### 命名与核心特性

1. **为什么叫Trie树？**

   - **词源**： 名称来自**"retrieval"**(检索)的中间部分，强调其高效检索的特性。
   - **别称：**前缀树（利用前缀共享）、字典树（类似字典按字母顺序组织）。

2. **是否具有哈希表性质的树形结构？**

   - **相似性**：支持快速查找（类似哈希表直接通过键访问）

   - **差异性：**

     ![image-20250316172117360](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250316172117360.png)
     

#### Trie树的核心

1. **前缀共享**
   - **机制**： 不同字符串的公共前缀共享同一路径。
   - **优势**： 避免重复存储，节省空间。
2. **逐字符匹配**
   - **操作逻辑**： 从根节点开始， 按字符逐层向下匹配。
   - **时间复杂度**： 查询、插入、删除均为**O(L)**（L为字符串长度）。

#### 知识点补充与细节

1. **节点结构设计**

   - **基础节点：**

     ```python
     class TrieNode:
         def __init__(self):
             self.children = {}  # 字符到子节点的映射（字典实现）
             self.is_end = False  # 标记是否为单词结尾
             # 可选：存储额外信息（如词频）
             self.count = 0
     ```

   - **优化变种：**

     - **压缩Tire树**（Radix Tree）： 合并单链节点， 减少层数。
     - **三向Tire树**（Ternary Search Trie）： 平衡时间与空间效率。

2. **核心操作：**

   - **插入字符串：**

     ```python
     def insert(root, word):
         node = root
         for char in word:
             if char not in node.children:
                 node.children[char] = TrieNode()
             node = node.children[char]
         node.is_end = True
         node.count += 1
     ```

   - **搜索字符串：**

     ```python
     def search(root, word):
         node = root
         for char in word:
             if char not in node.children:
                 return False
             node = node.children[char]
         return node.is_end
     ```

3. **应用场景**

   - **搜索引擎自动补全**： 输入前缀即时提示候选词。
   - **拼写检查**： 快速判断单词是否存在。
   - **路由表最长前缀匹配**： IP路由选择最佳匹配规则。
   - **生物信息学**： DNA序列模式匹配。

4. **优缺点分析**

   ![image-20250316172958638](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250316172958638.png)

5. **优化策略**

   - **字符串映射优化**： 使用数组代替字典（如仅小写字母➡长度26的数组）。
   - **延迟删除**：删除操作标记节点而非立即清理路径。
   - **双数组Trie**：压缩存储结构，减少内存占用。

#### Trie树 vs 哈希表：实战对比

**场景： 存储100万个英文单词**

![image-20250316173255409](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250316173255409.png)

#### 总结

- **Trie树的本质**：通过树形路径表达字符串集合，核心价值在于**前缀共享**。
- **适用场景**： 需频繁前缀匹配、有序遍历或处理公共前缀的场景。
- **工程选择**： 若仅需精确查找且内存敏感，哈希表更优；若需前缀操作，Trie树不可替代。

## 图论

**图论**是研究**顶点（Vertex）和边（Edge）**构成的抽象结构的数学分支，用于建模事物间的关系。核心问题包括路径查找、连通性分析、网络流优化等。

#### 图的表示方法对比

1. **邻接矩阵（Adjacency Matrix）**

   - **定义：**

     用二维数组表示图，矩阵的行和列对应顶点，元素值表示顶点间的边。

   - **特点：**

     - **稠密图适用**：存储所有可能的边（无论是否存在）。
     - **快速查询**： 判断两顶点是否相邻的时间复杂度为**O(1)**。
     - **空间复杂度**：O(V²)（V为顶点数），适合顶点数较少的图。

   - **示例**（无向图）：
   ```text
   顶点：A, B, C, D
   边：A-B, A-C, B-D, C-D
   邻接矩阵：
      A B C D
    A 0 1 1 0
    B 1 0 0 1
    C 1 0 0 1
    D 0 1 1 0

2. **邻接矩阵（Adjacency Matrix）**

   - **定义：**

     用数组或字典的集合表示图，每个顶点对应一个链表/数组，存储其邻接顶点。

   - **特点：**

     - **稀疏图适用**：仅存储实际存在的边。
     - **节省空间**：空间复杂度为**O(V + E)**（E为边数）。
     - **高效遍历邻接点**： 获取某顶点的所有邻接点时间复杂度为O(1)。

   - **示例**（无向图）：

     ```text
     A → B → C
     B → A → D
     C → A → D
     D → B → C
     ```

#### 邻接矩阵 vs 邻接表：核心对比

![image-20250317134922569](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250317134922569.png)

#### 邻接矩阵与邻接表的关系

1. **功能等价**：两者均可完整表示图的拓扑结构。
2. **空间-时间权衡**：
   - 邻接矩阵以空间换时间，适合快速查询。
   - 邻接表以时间换空间，适合高效存储和遍历。
3. **相互转化**：可通过遍历边集在两种表示间转换（时间复杂度O(V²)）或O((E))。

#### 知识点补充

1. **有权图的表示**

   - **邻接矩阵**：矩阵元素存储边的权重（无边可设为0或∞）。

   - **邻接表**： 链表节点需额外存储权重。

     ```python
     # 邻接表示例（Python字典实现有权图）
     graph = {
         'A': {'B': 2, 'C': 5},
         'B': {'A': 2, 'D': 3},
         'C': {'A': 5, 'D': 1},
         'D': {'B': 3, 'C': 1}
     }
     ```

2. **动态图的处理**

   - **邻接矩阵**：调整矩阵大小复杂（需重新分配内存）。
   - **邻接表：**动态增删顶点更灵活（链表/字典天然支持动态扩展）。

3. **实际应用场景**

   - **邻接矩阵：**
     - Floyd-Warshall算法（全源最短路径）。
     - 小规模图的快速操作（如游戏地图的碰撞检测）。
   - **邻接表**
     - Dijkstra算法（单源最短路径）。
     - 社交网络的好友关系建模。

#### 总结

- **邻接矩阵**： 空间换时间，适合稠密图和频繁边查询。
- **邻接表**：时间换空间， 适合稀疏图和高效邻接点遍历。
- **选择依据**：根据图的规模、密度和操作类型灵活选择。

### 图论的核心算法详解

#### 遍历算法

1. **BFS（广度优先搜素， 层序遍历）**

   - **核心思想**： 逐层访问节点，使用队列实现。
   - **步骤**：
     1. 初始化队列，将起点入队并标记已访问。
     2. 循环出队节点，访问其未访问的邻接节点并入队。
     3. 重复直至队列为空。
   - **时间复杂度**： O(V + E)（V为顶点数， E为边数）。
   - **应用场景**：
     - 无权图的最短路径（如迷宫问题）。
     - 社交网络中的层级关系分析。
   - **关键细节**：
     - 层序遍历： 记录每层节点数可实现分层处理。
     - 避免重复访问： 使用标记数组或哈希表。

2. **DFS（深度优先搜素，回溯剪枝）**

   - **核心思想**： 沿分支深入到底再回溯，使用栈或递归实现。

   - **步骤**：

     1.  从起点出发，标记已访问。
     2. 递归访问未访问的邻接节点。
     3. 回溯时撤销状态（用于路径记录或剪枝）。

   - **时间复杂度**：O(V + E).

   - **应用场景**：

     - 拓扑排序、连通分量检测。
     - 组合优化问题（如八皇后、全排列）。

   - **关键细节**：

     - **剪枝优化**： 提前终止无效分支（如约束不满足时）。
     - **非递归实现**： 显式栈替代递归调用。

   - **对比BFS：**

     ![image-20250318100154063](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250318100154063.png)

#### 最短路径算法

1. **Dijkstra算法（单源最短路径，非负权图）**
   - **核心思想**：贪心策略，每次选择离源点最近的顶点。
   - **步骤**：
     1. 初始化距离数组，源点距离为0，其余为无穷大。
     2. 使用优先队列（最小堆）选择当前最短距离顶点。
     3. 松弛（Relax）其邻接顶点的距离。
     4. 重复直至队列为空。
   - **时间复杂度**：O((V + E) log V)（y优先队列优化）。
   - **限制**： 无法处理负权边。
   - **关键细节**：
     - **优先队列优化**：避免每次遍历查找最小距离。
     - **负权陷阱**：负权边会导致已确定最短路径的顶点被错误更新。
2. **Floyd-Warshall算法（全源最短路径， 动态规划）**
   - **核心思想**： 动态规划，逐步允许通过中间顶点。
   - **步骤**：
     1. 初始化距离矩阵为图的邻接矩阵。
     2. 三重循环更新： **dist\[i]\[j] = min(dist\[i]\[j], dist\[i]\[k] + dist\[k]\[j])**。
     3. 最终矩阵保存所有顶点对的最短距离。
   - **时间复杂度**： $$O(V^3)$$。
   - **应用场景**：
     - 小规模图的全源最短路径。
     - 可处理负权边（但不允许负权环）。
   - **关键细节**：
     - **空间优化**： 原地更新矩阵， 无额外空间。
     - **路径重建**： 记录前驱矩阵回溯路径。

**Dijkstra vs Floyd:**

![image-20250318101509169](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250318101509169.png)

#### 最小生成树算法

1. **Prim 算法 （适合稠密图）**
   - **核心思想**： 贪心策略，逐步扩展生成树。
   - **步骤**：
     1. 任选起点，初始化优先队列（存储边权）。
     2. 选择当前最小权边连接的顶点加入生成树。
     3. 更新队列中与新加入顶点邻接的边。
     4. 重复直至所有顶点加入。
   - **时间复杂度**：
     - 邻接矩阵： $$O(V^2)$$。
     - 优先队列优化：$$O(E log V)$$。
   - **关键细节**：
     - **与Dijlstra相似性**：均使用优先队列，但Prim更新的是到生成树的距离而非到源点的距离。
     - **稠密图优化**： 邻接矩阵实现更高效。
2. **Kruskal算法（适合稀疏图）**
   - **核心思想**：按边权升序选择，避免环。
   - **步骤**：
     1. 将所有边按权值排序。
     2. 依次选择最小边，若两端点不在同一连通分量则加入生成树。
     3. 使用并查集（Union-Find）检测环。
   - **时间复杂度**： $$O(ElogE)$$（主要开销在排序）。
   - **关键细节**：
     - **并查集优化**： 路径压缩和按秩合并降低时间复杂度。
     - **适用场景**： 边数远小于顶点数平方时更高效。

**Prim vs Kruskal:**

![image-20250318102637757](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250318102637757.png)

#### 关键对比与总结

![image-20250318102705028](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250318102705028.png)

#### 实战应用示例

![image-20250318102748032](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20250318102748032.png)

## 算法范式

1. **分治算法**
   - 归并排序的实现
   - 最大子数组问题（LeetCode 53）

2. **贪心算法**
   - 区间调度问题
   - 霍夫曼编码实现

3. **动态规划**

   动态规划（Dynamic Programming，DP）是一种通过将复杂问题分解为重叠子问题，并利用子问题的最优解来构造全局最优解的算法范式。其核心思想是**避免重复计算**。

   - 0-1背包问题（空间优化版本）
   - 股票买卖系列（LeetCode 121-123）
   - 编辑距离（状态转移方程推导）

4. **回溯算法**
   - 全排列问题（剪枝优化）
   - N皇后问题（位运算优化）





























































































