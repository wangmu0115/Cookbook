## 集合对象（Set Types）

集合对象是**不同**的**可哈希**对象的**无序**集合，即集合中的元素必须是可哈希的（hashable）。

当前具有两个内建的集合类型，`set`和`frozenset`。**`set`是可变的**和不可哈希的，不能作为`dict`的键或另外一个集合的元素。**`frozenset`是不可变的**和可哈希的，其内容在创建后无法更改，可以作为`dict`的键或另外一个集合的元素。

- **`class set([iterable])`**
- **`class frozenset[iterable]`**

```python
# 集合字面量，`{}`内使用逗号分隔元素列表
s1 = {'hello', 42, 'jack'}
s2 = {'hello', 'world', 42, 'world'}
print(s1) # {'jack', 42, 'hello'}
print(s2) # {42, 'world', 'hello'}
# 集合推导式
s3 = {ch for ch in 'abracadabra' if ch not in 'abc'}
print(s3) # {'r', 'd'}
# 构造函数，`set()`和`frozenset()`
s4 = set()
s5 = set('foobar')
s6 = set(range(0, 5))
s7 = frozenset(['a', 'foo', 42, 'a'])
print(s4) # set()
print(s5) # {'f', 'b', 'o', 'a', 'r'}
print(s6) # {0, 1, 2, 3, 4}
print(s7) # frozenset({'a', 'foo', 42})
```

