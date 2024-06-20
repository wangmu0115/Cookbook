## 映射类型（Mapping Types)

映射对象（mapping object）将可哈希值（hashable value）映射到任意对象，映射是**可变对象**，当前只有一个标准映射类型：[`dict`](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)。

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

