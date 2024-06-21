## 序列类型（Sequence Types）

- 基本序列类型：**[`list`, `tuple`, `range`](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)**
- 文本字符串序列类型：**[`str`](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)**
- 二进制数据序列类型：**[`bytes`, `bytearray`, `memoryview` ](https://docs.python.org/3/library/stdtypes.html#binary-sequence-types-bytes-bytearray-memoryview)**

### 常见序列操作

`s`和`t`是相同类型的序列，`n`、`i`、`j`和`k`是整数，`x`是满足`s`施加的任何类型和值限制的对象。

| 操作                   | 描述                                                        |
| ---------------------- | ----------------------------------------------------------- |
| `x in s`               | s 中是否存在元素等于 x                                      |
| `x not in s`           | s 中是否不存在任何元素等于 x                                |
| `s + t`                | s 和 t 序列连接                                             |
| `n * s`, `s * n`       | 相当于将 s 加到自身 n 次                                    |
| `s[i]`                 | s 中第`i`个元素，`i`从0开始                                 |
| `s[i:j]`               | 从`i`到`j`的 s 切片                                         |
| `s[i:j:k]`             | 从`i`到`j`的 s 切片，步长是`k`                              |
| `len(s)`               | s 中元素的数量                                              |
| `min(s)`               | s 中最小的元素                                              |
| `max(s)`               | s 中最大的元素                                              |
| `s.index(x[, i[, j]])` | s 中第一次出现 x 的索引（在索引`i`处或之后且在索引`j`之前） |
| `s.count(x)`           | s 中出现 x 的总次数                                         |

- `in`和`not in`操作符用于简单包含，但是`str`、`bytes`和`bytearray`等序列也可以使用它们进行**子序列匹配**。

```python
s1 = "HelloWorld"
s2 = list(s1)
print("ll" in s1) # True
print("ll" in s2) # True
print("l" not in s2) # False
```

- 使用运算符`+`连接不可变序列总是会产生一个新对象，因此需要注意重复连接产生的运行时成本。
- 使用运算符`*`重复序列时，需要注意当`n <= 0`时相当于清空序列中的元素，`n > 1`复制的不是序列的元素而是元素的引用。

```python
# 连接序列会产生一个新的序列
s3 = [1, 3, 5]
s4 = [2, 4, 6]
print(s3 + s4) # [1, 3, 5, 2, 4, 6]
print(s4 + s3) # [2, 4, 6, 1, 3, 5]
# n <= 0则相当于清空序列
s5 = s3 * 0 # []
s6 = s3 * -1 # []
s7 = s3 * 2 # [1, 3, 5, 1, 3, 5]
# 重复的不是元素，而是元素的引用
s8 = [[1, 3], [2, 4]]
s9 = s8 * 2
s9[0].append(5)
print(s9) # [[1, 3, 5], [2, 4], [1, 3, 5], [2, 4]]
```







### 可变序列类型

下表中的操作定义在可变序列类型，`s`是可变序列类型的实例，`t`是可迭代对象，`x`是满足`s`施加的任何类型和值限制的对象。

| 操作                    | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| `s[i] = x`              | s 的第`i`个元素替换为 x （`i`从`0`开始）                     |
| `s[i:j] = t`            | s 从`i`到`j`的切片被可迭代对象 t 的元素替换                  |
| `del s[i:j]`            | 等同于`s[i:j] = []`                                          |
| `s[i:j:k] = t`          | `s[i:j:k]`的元素被 t 的元素替换                              |
| `del s[i:j:k]`          | 将`s[i:j:k]`的元素从序列中删除                               |
| `s.append(x)`           | 将 x 添加到 s 的末尾，等同于`s[len(s):len(s)] = [x]`         |
| `s.insert(i, x)`        | 将 x 插入到 s 的第`i`处，等同于`s[i:i] = x`                  |
| `s.pop()`, `s.pop(i)`   | 检索 s 的第`i`个元素，并从序列中删除，`i`默认值是`-1`，即 s 的最后一项 |
| `s.remove(x)`           | 删除 s 中第一个等于 x 的元素                                 |
| `s.clear()`             | 删除 s 中所有元素，等同于`del s[:]`                          |
| `s.copy()`              | 浅复制 s 的副本，等同于 `s[:]`                               |
| `s.extend(t)`, `s += t` | 使用 t 的内容扩展 s，绝大部分情况下等同于`s[len(s):len(s)] = t` |
| `s *= n`                | 更新 s，使其内容重复 n 次                                    |
| `s.reverse()`           | 反转 s                                                       |

- `s[i:j] = t`替换后的序列长度是：`len(s) - len(s[i:j]) + len(t)`

```python
s1 = list(range(0, 6)) # [0, 1, 2, 3, 4, 5]
# 替换`index=3`的元素
s1[3] = 42
print(s1) # [0, 1, 2, 42, 4, 5]
# 将切片替换为迭代对象的元素
s1[1:4] = range(11, 16) 
print(s1) # [0, 11, 12, 13, 14, 15, 4, 5]
# 删除序列一部分元素，等同于 s1[1:3] = []
del s1[1:3]
print(s1) # [0, 13, 14, 15, 4, 5]
```

- `s[i:j:k] = t`替换时，t 的长度必须和切片的元素数量相同

```python
s2 = list(range(0, 11))
# 替换的迭代对象的元素数量**必须等于**切片的元素数量
s2[1:9:2] = range(41, 45)
print(s2) # [0, 41, 2, 42, 4, 43, 6, 44, 8, 9, 10]
# 删除序列的一部分元素
del s2[1:9:2]
print(s2) # [0, 2, 4, 6, 8, 9, 10]
```

- `remove(x)`是，如果序列中不存在元素等于 x 则会报错`ValueError`

```python
s3 = [1, 3, 5]
# `append(x)`序列末尾追加元素，等同于s[len(s):len(s)] = [x]
s3.append(7)
s3[len(s3):len(s3)] = [11]
print(s3) # [1, 3, 5, 7, 11]
# `insert(index, x)`将元素添加到指定位置，并将位置后续元素向后移动
s3.insert(1, 42)
print(s3) # [1, 42, 3, 5, 7, 11]
# `pop(index)`移除指定位置的元素，默认是移除序列尾部元素
s3.pop()
print(s3) # [1, 42, 3, 5, 7]
s3.pop(1)
print(s3) # [1, 3, 5, 7]
# `remove(x)` 删除第1个等于x的元素
s3.append(3) # [1, 3, 5, 7, 3]
print(s3)
# s3.remove(42) # 如果删除的元素在`s3`中不存在，则会报错`ValueError`
s3.remove(3)
print(s3) # [1, 5, 7, 3]
```

- `s *= n`，如果`n <= 0`则会清空序列，即相当于`del s[:]`或`s.clear()`，序列中的元素不会被复制，只是复制它们的多次引用

```python
s4 = [1, 3, 5]
# `s.clear()`清空序列元素，等同于`del s[:]`
s4.clear()
# del s4[:]
print(s4) # []
# `s.copy()`复制序列，等同于`s[:]`
s4 = [1, 3, 5]
s5 = s4.copy()
s6 = s4[:]
s4.append(7)
s5.append(9)
s6.append(11)
print(s4) # [1, 3, 5, 7]
print(s5) # [1, 3, 5, 9]
print(s6) # [1, 3, 5, 11]

# 序列扩展, `s.extend(t)` `s += t` `s[len(s):len(s)] = t`
s7 = [2, 4, 6]
s7.extend(range(3)) # [2, 4, 6, 0, 1, 2]
s7 += range(10, 13) # [2, 4, 6, 0, 1, 2, 10, 11, 12]
s7[len(s7):len(s7)] = range(20, 23) # [2, 4, 6, 0, 1, 2, 10, 11, 12, 20, 21, 22]
# 重复序列，`s *= n`，如果n<=0则相当于`del s[:]`(`s.clear()`)
s8 = [1, 3, 5]
s8 *= 0
print(s8) # []
s9 = [[1, 3], [2, 4]]
# 元素不会被复制，而是复制元素的引用
s9 *= 2
print(s9) # [[1, 3], [2, 4], [1, 3], [2, 4]]
s9[0].append(5)
print(s9) # [[1, 3, 5], [2, 4], [1, 3, 5], [2, 4]]
```

- `reverse()`方法会产生副作用，即会直接修改序列

```python
s10 = [1, 3, 2, 4]
print(s10.reverse()) # None
print(s10) # [4, 2, 3, 1]
```

### 元组（Tuple）

元组是**不可变序列**，可以用于存储同构或异构数据集合。

**`class tuple ([iterable])`**

```python
# `()`表示空元组
tup1 = ()
# `a,`或`(a,)`尾随逗号表示单例元组
tup2 = 42,
tup3 = (42,)
# `a,b,c`或`(a,b,c)`使用逗号分隔项
tup4 = 42, 'hello', True
tup5 = (2, 4, 6)
# 使用内置函数`class tuple([iterable])`
tup6 = tuple('Hello')
tup7 = tuple(range(5))

print(tup1) # ()
print(tup2) # (42,)
print(tup3) # (42,)
print(tup4) # (42, 'hello', True)
print(tup5) # (2, 4, 6)
print(tup6) # ('H', 'e', 'l', 'l', 'o')
print(tup7) # (0, 1, 2, 3, 4)
```

元组实现了**所有常见的序列操作**。

对于异构数据集合，通过名称访问比通过索引访问更清晰，可以使用[`collections.namedtuple()`](https://docs.python.org/3/library/collections.html#collections.namedtuple)。

**逗号**构成了元组，括号是可选的，除非元组为空或者需要使用括号来避免语法歧义。



























### 文本序列类型 : `str`

`str`是由Unicode码点构成的不可变序列。字符串字面量可以通过`'`、`"`、`"""`或`'''`创建：

```python
# 单引号
single_quote_str = 'allows embedded "double" quotes'
# 双引号
double_quote_str = "allows embedded 'single' quotes"
# 三引号，允许跨越多行，所有空字符都会将包含在字符串文字中
triple_quote_str1 = """Tress double quotes
    second line
last line"""
triple_quote_str2 = '''Three single quotes'''
```

- **`class str(object='')`**
  - 等价于`type(object).__str__(object)`
  - 如果`object`没有`__str()__`方法，则等价于`repr(object)`
- **`class str(object=b'', encoding='utf-8', errors='strict')`**
  - `object`是`bytes`或`bytearray`对象，则等价于`bytes.encode(encoding, errors)`
  - `object`是其他类型，则会先获取缓冲层对象底层的字节对象















