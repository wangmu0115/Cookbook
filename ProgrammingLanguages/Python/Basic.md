Python是**解释型语言**，使用**缩进**而不是括号组织代码块，使用`#`进行单行注释，使用`'''`或 `"""`进行多行注释。

### 变量

**变量（variable）**是用于存储数据值的标识符。Python是**动态类型语言**，不需要在编写代码时显式指定变量的数据类型，程序在运行时会自动进行类型检查；Python是**强类型语言**，计算时需要显式转换为正确的类型，隐式转换只在特定的情况下才会发生。

#### 变量类型

| 类型（`type()`） | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| `NoneType`       | Python的`null`值（只存在一个`None`对象实例）                 |
| `str`            | 字符串类型，存有Unicode（UTF-8编码）字符串，是一系列字符的序列 |
| `bytes`          | 原生ASCII字节（或Unicode编码字节）                           |
| `bool`           | `True`或`False`                                              |
| `float`          | 双精度（64位）浮点数                                         |
| `int`            | 任意精度整数                                                 |
| `complex`        | 复数                                                         |
| `list`           | 一组有序的元素序列，可以修改                                 |
| `tuple`          | 一组有序的元素序列，不可以修改                               |
| `set`            | 一组无序的元素序列，序列中的元素必须可哈希，元素不重复       |
| `dict`           | 一组键值对，键必须可哈希，键不重复                           |

#### 运算符

- 算术运算符：`+`、`-`、`*`、`\`、`\\`、`%`、`**`
- 赋值运算符：`=`、`+=`、`-=`、`*=`、`\=`、...
- 比较运算符：`==`、`!=`、`>`、`>=`、`<`、`<=`
- 逻辑运算符：`and`、`or`、`not`
- 位运算符：`~`、`&`、`|`、`^`、`<<`、`>>`
- 成员运算符：`in`、`not in`
- 身份运算符：`is`、`is not`

### 导入

```python
# 直接导入整个包
import numpy
# [推荐] 导入整个包并指定别名
import pandas as pd
# [推荐] 导入部分模块或函数到当前的命名空间中
from datetime import datetime, date, time
# 导入所有模块或函数到当前的命名空间中
from datetime import *
```

### 控制结构

- `if...elif...else...`
- `for`
- `while`
- `for...else...`

```python
"""
# if num > 3:
0       1       2       3       
# if num > 5:
0       1       2       3       4
For loop finished
"""
for num in range(5):
    # 如果for循环没有执行到结尾，`for..else`的`else`语句不会执行
    # 例如break改成`num > 5`，则会打印`For loop finished`
    if num > 3:
    # if num > 5:
        break
    else:
        print(num, end="\t")
else:
    print("\nFor loop finished")
```

- `break`, `continue`, `pass`

```python
"""
# break: 0 1 2
# continue: 0 1 2 4
# pass: 0 1 2 3 4
"""
for i in range(5):
    if i == 3:
        # break
        # continue
        pass # 空语句占位符
    print(i, end=' ')
```

### 列表生成式

**`[expression for item in iterable if condition]`**

- `expression`要生成的元素
- `item`迭代的变量
- `iterable`迭代的对象
- `if condition`可选的过滤条件

```python
# 矩阵转置：[[1, 2, 3], [4, 5, 6]] => [[1, 4], [2, 5], [3, 6]]
def transpose(matrix):
    matrix_x = []
    num_row = len(matrix)
    num_col = len(matrix[0])
    return [[matrix[i][j] for i in range(num_row)] for j in range(num_col)]
    # transposed_matrix = []
    # for j in range(num_col):
    #     transposed_matrix.append([matrix[i][j] for i in range(num_row)])
    # return transposed_matrix
# 矩阵逐项积，相同矩阵中相应位置上的元素逐一相乘
# [[1, 2], [3, 4]] \otimes [[5, 6], [7, 8]] => [[5, 12], [21, 32]]
def hadamard_prod(M1, M2):
    if len(M1) != len(M2) or len(M1[0]) != len(M2[0]):
        raise ValueError("Matrices must have the same shape")
    num_row = len(M1)
    num_col = len(M1[0])
    return [[M1[i][j] * M2[i][j] for j in range(num_col)] for i in range(num_row)]
# 笛卡尔积
column1 = [1, 2, 3]
column2 = ['a', 'b']
# [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b'), (3, 'a'), (3, 'b')]
print([(x, y) for x in column1 for y in column2])
```

### 函数

- 内置函数：Python解释器提供的函数
- 自定义函数
- Lambda函数：匿名函数，通过`lambda`关键字定义
- 生成器函数：用于生成一个迭代器，使用`yield`关键字定义
- 方法：与对象相关联的函数，使用`.`运算符调用















### 异常

在 Python 中，异常 (exception) 是指在程序执行期间出现的错误或异常情况。当出现异常时，程序的正常流程被中断，转 而执行异常处理的代码块，以避免程序崩溃或产生不可预知的结果。

Python 中有许多不同类型的异常，每种异常都代表了特定类型的错误。以下是一些常见的异常类型:ValueError (数值错 误):当函数接收到一个不合法的参数值时引发。TypeError (类型错误):当使用不兼容的类型进行操作或函数调用时引发。 IndexError (索引错误):当尝试访问列表、元组或字符串中不存在的索引时引发。FileNotFoundError (文件未找到错 误):当尝试打开不存在的文件时引发。ZeroDivisionError (零除错误):当尝试将一个数除以零时引发。

可以使用 try-except 语句来捕获并处理这些异常，以便在程序出现问题时执行适当的操作或提供错误信息。







`isinstance()`函数可以检查对象是否为特定类型的实例。

```python
v1 = 42
v2 = True
v3 = "HelloWorld"
print(isinstance(v1, int)) # True
print(isinstance(v2, float)) # False
# 接收包含类型的元组作为参数，检查对象类型是否在类型元组中
print(isinstance(v2, (float, bool))) # True
print(isinstance(v3, str)) # True
```

点运算符(`.`)可以调用对象的属性和方法。用`getattr()`函数通过名字访问属性和方法，`hasattr()`函数和`setattr()`也用于查询对象是否包含/设置某个属性和方法。

```python
sVal = "HelloWorld"
# 直接调用`count()`方法
print(sVal.count("l")) # 3
# 通过`getattr()`函数获取sVal的`count()`方法，再执行调用
print(getattr(sVal, 'count')("l")) # 3

# 通过`hasattr()`函数判断一个对象是否可迭代(是否具有`__iter__`这个魔术方法)
def isiterable(obj):
    if(hasattr(obj, "__iter__")):
        return True
    else:
        return False
print(isiterable(42)) # False
print(isiterable(True)) # False
print(isiterable('Hello')) # True
print(isiterable([2, 4, 6])) # True
```

#### 标量类型

| 类型    | 说明                                           |
| ------- | ---------------------------------------------- |
| `None`  | Python的`null`值（只存在一个`None`对象的实例） |
| `str`   | 字符串类型，存有Unicode（UTF-8编码）字符串     |
| `bytes` | 原生ASCII字节（或Unicode编码字节）             |
| `bool`  | `True`或`False`                                |
| `float` | 双精度（64位）浮点数                           |
| `int`   | 任意精度整数                                   |

##### `bool`类型可以与关键字`and`, `or`, `not`结合使用

```python
print(True and False) # False
print(True and True)  # True
print(True or False)  # True
print(False or False) # False
print(not True) # False
```

##### 字符串

- 单引号，双引号或三引号创建字符串常量。
- 字符串是**不可变的**，不能修改字符串。
- 转义字符（`\`）。
- 原生字符串，前缀`r`。
- `+`运算符可以用于拼接字符串。
- 字符串模版：`format()`方法，**`f-string`**

```python
# 转义字符串：`\`
print('hello\tworld') # hello   world
# 原生(raw)字符串：`r`
print(r'hello\n\tworld\r') # hello\n\tworld\r
# 字符串拼接：`+`
print('hello ' + 'world') # hello world
# 字符串模版：第1个参数格式化为带2个小数的浮点数，第2个参数格式化为字符串，第3个参数格式化为整数
template = "{0:.2f} {1:s} are worth US${2:d}"
print(template.format(32.1, "Abc Pesos", 17)) # 32.10 Abc Pesos are worth US$17
# f-string：可以在表达式后添加格式说明符
amount = 10; rate = 88.86; currency = "Pesos"
result = f"{amount} {currency} is worth US${amount / rate:.2f}"
print(result) # 10 Pesos is worth US$0.11
```

##### 类型转换

- `type()`函数返回变量的数据类型。
- `str()`, `float()`, `int()`和`bool()`函数可以将其他数据转换成对应的类型。

```python
val = "3.1415926"
print(float(val)) # 3.1415926
print(int(float(val))) # 3
print(bool(val)) # True
print(str(val)) # 3.1415926
print(type(str(42))) # <class 'str'>
```





