## [`itertools`](https://docs.python.org/3/library/itertools.html)

### 排列组合迭代器

| 库函数                                                 | 说明                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| `itertools.permutations(iterable, r=None)`             | 指定长度所有可能排列方式，数量：$\frac{n!}{(n-r)!}$          |
| `itertools.combinations(iterable, r)`                  | 指定长度所有可能组合方式，数量：$\binom{n}{r} = \frac{n!}{(n-r)!r!}$ |
| `itertools.product(*iterables, repeat=1)`              | 有放回的所有可能排列方式，数量：$n^{repeat}$                 |
| `itertools.combinations_with_replacement(iterable, r)` | 有放回的所有可能组合方式，数量：$\frac{(n + r - 1)!}{r!(n-1)!}$ |

```python
import itertools

# 3!/(3-2)! [('a', 'b'), ('a', 'c'), ('b', 'a'), ('b', 'c'), ('c', 'a'), ('c', 'b')]
print(list(itertools.permutations('abc', 2)))
# 4!/2!/(4-2)! [('a', 'b'), ('a', 'c'), ('a', 'd'), ('b', 'c'), ('b', 'd'), ('c', 'd')]
print(list(itertools.combinations('abcd', 2)))
# [('a', 'x'), ('a', 'y'), ('b', 'x'), ('b', 'y'), ('c', 'x'), ('c', 'y')]
print(list(itertools.product('abc', 'xy')))
# [('a', 'a'), ('a', 'b'), ('a', 'c'), ('b', 'a'), ('b', 'b'), ('b', 'c'), ('c', 'a'), ('c', 'b'), ('c', 'c')]
print(list(itertools.product('abc', repeat=2)))
# [('a', 'a'), ('a', 'b'), ('a', 'c'), ('b', 'b'), ('b', 'c'), ('c', 'c')]
print(list(itertools.combinations_with_replacement('abc', 2)))
```

