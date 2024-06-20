## 映射类型（Mapping Types)

映射对象（mapping object）将**可哈希值**（hashable value）映射到任意对象，映射是**可变对象**，当前只有一个标准映射类型：[`dict`](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)。映射类型的键必须是**可哈希的**，同名的键会覆盖已经存在的键值对。

- **`class dict(**kwargs)`**
- **`class dict(mapping, **kwargs)`**
- **`class dict(iterable, **kwargs)`**

```python
# 字典字面量，`{}`中一组逗号分隔的键值对
dict1 = {"Jack": 27, "Grag": 29}
dict2 = {"odds": [1, 3, 5, 7], "evens": [2, 4, 6, 8]}
# 字典推导式
dict3 = {str(x): x ** 2 for x in range(2, 6)}
# 类型构造函数，`dict()`
dict4 = dict()
dict5 = dict([('foo', 100), ('bar', 200)])
dict6 = dict(foo=42, bar=24)

print(dict1) # {'Jack': 27, 'Grag': 29}
print(dict2) # {'odds': [1, 3, 5, 7], 'evens': [2, 4, 6, 8]}
print(dict3) # {'2': 4, '3': 9, '4': 16, '5': 25}
print(dict4) # {}
print(dict5) # {'foo': 100, 'bar': 200}
print(dict6) # {'foo': 42, 'bar': 24}
```

下面示例提供了多种方式创建同一个映射对象`{"one": 1, "two": 2, "three": 3}`

```python
x1 = {"one": 1, "two": 2, "three": 3}
x2 = dict(one=1, two=2, three=3)
x3 = dict(zip(["one", "two", "three"], (1, 2, 3)))
x4 = dict([("one", 1), ("two", 2), ("three", 3)])
x5 = dict({"one": 1, "two": 2, "three": 3})
x6 = dict([("one", 1), ("two", 2)], three=3)
x7 = dict({"two": 2, "three": 3},one=1)
print(x1) # {'one': 1, 'two': 2, 'three': 3}
print(x1 == x2 == x3 == x4 == x5 == x6 == x7) # True
```

### 映射类型操作

`d`是一个`dict`类型对象

| 操作                       | 说明                                                         |
| -------------------------- | ------------------------------------------------------------ |
| `list(d)`                  | 返回`d`的所有键组成的列表                                    |
| `len(d)`                   | 返回`d`中键值对的数量                                        |
| `d[key]`                   | 返回`d`中键`key`映射的对象，如果`key`不存在则会引发[`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError) |
| `d.get(key, default=None)` | 返回`d`中键`key`映射的对象，如果`key`不存在则返回默认值，默认为`None` |
| `d[key] = value`           | 将`d`中键`key`映射到新的对象，如果`key`已经存在则会覆盖旧值  |
| `del d[key]`               | 从`d`中移除键`key`对应的键值对，如果`key`不存在则会引发[`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError) |
| `d.pop(key [, default])`   | 从`d`中移除键`key`对应的键值对，并返回`key`映射的值<br/>如果`key`不存在则会返回默认值，如果默认值未指定则会引发[`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError) |
| `key in d`                 | 键`key`是否在`d`中存在                                       |
| `key not in d`             | 键`key`是否不存在`d`中                                       |
| `iter(d)`                  | 返回`d`键上的迭代器，等同于`iter(d.keys())`                  |
| `d.clear()`                | 移除`d`中的所有键值对                                        |
| `d.copy()`                 | 返回`d`的浅复制                                              |
|                            |                                                              |
|                            |                                                              |
|                            |                                                              |
|                            |                                                              |
|                            |                                                              |

```python
d = {"one": 1, "two": 2, "three": 3}
print(list(d)) # ['one', 'two', 'three']
print(len(d)) # 3
# `d[key]`的默认值版本
print(d["one"]) # 1
# print(d['four']) # KeyError: 'four'
print(d.get("four", 4)) # 4
d["one"] = 42
d["four"] = 4
print(d) # {'one': 42, 'two': 2, 'three': 3, 'four': 4}
# 删除字典中的键值对
del d["one"]
print(d.pop("one", 1)) # 1
print(d.pop("two")) # 2
# print(d.pop("one")) # KeyError: 'one'
# del d["five"] # KeyError: 'five'
# 检查某个`key`在字典中是否存在
print("one" in d) # False
print("one" not in d) # True
```

```python
# `copy()`浅复制
d1 = {"one": 1, "two": 2, "three": 3, "odds": [1, 3, 5]}
d2 = d1.copy()
d3 = d1.copy()
d1["odds"].append(7)
d2["four"] = 4
d3["five"] = 5
print(d1) # {'one': 1, 'two': 2, 'three': 3, 'odds': [1, 3, 5, 7]}
print(d2) # {'one': 1, 'two': 2, 'three': 3, 'odds': [1, 3, 5, 7], 'four': 4}
print(d3) # {'one': 1, 'two': 2, 'three': 3, 'odds': [1, 3, 5, 7], 'five': 5}
```



### 字典视图对象

`dict.keys()`、`dict.values()`和`dict.items()`返回的对象是视图对象，即当字典发生变化时，这些动态视图会反应这些变化。

```python
d = {"one": 1, "two": 2, "three": 3}
keys = d.keys()
values = d.values()
items = d.items()
# 视图对象
print(keys)   # dict_keys(['one', 'two', 'three'])
print(values) # dict_values([1, 2, 3])
print(items)  # dict_items([('one', 1), ('two', 2), ('three', 3)])
# 字典添加新的键值对
d["four"] = 4
print(keys)   # dict_keys(['one', 'two', 'three', 'four'])
print(values) # dict_values([1, 2, 3, 4])
print(items)  # dict_items([('one', 1), ('two', 2), ('three', 3), ('four', 4)])
# 从字典中移除键值对
d.pop("one")
print(keys)   # dict_keys(['two', 'three', 'four'])
print(values) # dict_values([2, 3, 4])
print(items)  # dict_items([('two', 2), ('three', 3), ('four', 4)])
```





































