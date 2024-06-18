Python是解释型语言，使用缩进而不是括号组织代码块。Python语句不需要用分号结尾。
万物皆对象，对象模型的一致性，每个对象都有关联的类型
#注释
函数和对象方法
变量赋值，绑定变量
当你将对象作为参数传递给函数时，新的局部变量创建了对原始对象的引用，而不是复制。如果在函数里将一个新对象绑定到一个变量，这个操作不会影响到该函数（即函数圆括号以内的部分）以外“范围”的同名变量。因此，可以修改可变参数的内部值。假设有以下函数：

动态引用，强类型

isinstance()函数

import导入
as关键字



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
print(v1 is None) // True
print(v2 is None) // False
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
print(True and False) // False
print(True and True)  // True
print(True or False)  // True
print(False or False) // False
print(not True) // False
```

##### 字符串









