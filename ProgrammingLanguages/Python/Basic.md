Python是**解释型语言**，使用**缩进**而不是括号组织代码块，语句**不需要分号结尾**，使用`#`**单行注释**。

**万物皆对象**，对象模型的一致性，每个对象都有关联的类型。

**动态引用，强类型**，在运行时才会确定变量类型，隐式转换只在特定的情况下发生。

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

#### 导入

```python
import numpy
import pandas as pd
from datetime import datetime, date, time
```

#### 二元运算符

| 运算  | 说明 |
| ----- | ---- |
| `a + b` | a 加 b |
| `a - b` | a 减 b |
| `a * b` | a 乘 b |
| `a / b` | a 除以 b |
| `a // b` | a 整除以 b，只保留结果的整数部分 |
| `a ** b` | a 的 b 次幂 |
| `a & b` | 逻辑**且**；对于整数，逐位**与**运算 |
| `a | b` | 逻辑**或**；对于整数，逐位**或**运算 |
| `a ^ b` | 逻辑**异或**；对于整数，逐位**异或**运算 |
| `a == b` | a 是否等于 b |
| `a != b` | a 是否不等于 b |
| `a < b`, `a <= b` | a 是否小于/小于等于 b |
| `a > b`, `a >= b` | a 是否大于/大于等于 b |
| `a is b` | a 和 b 是否引用同一个对象 |
| `a is not b` | a 和 b 是否引用不同的对象 |

`is`和`is not`常用于判断变量是否为`None`，因为`None`的实例是唯一的：

```python
v1 = None
v2 = 42
print(v1 is None) # True
print(v2 is None) # False
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

### 控制流

- `if`, `elif`, `else`
- `for value in collection`
	- `continue`
	- `break`
- `while`
- `pass`: 不执行任何操作的代码块占位符
- `range(start_include, end_exclude, step)`函数生成一个均匀分布的整数序列，`range()`函数返回的是**迭代器**。

```python
val = 42
if val < 18:
    print("val < 18")
elif(val < 60):
    pass # 占位符
else:
    print("val > 60")

list = list(range(0, 10, 1))
print(list) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
# range()函数常见用法是用索引迭代序列
seq = [1, 3, 5]
for idx in range(len(seq)):
	# element_0: 1
    # element_1: 3
    # element_2: 5
	print(f"element_{idx}: {seq[idx]}")
```
