## [`random`](https://docs.python.org/3/library/random.html)

```python
import random

random.seed(42)
print(random.gauss(mu=0.0, sigma=1.0)) # -0.14409032957792836
```

### 常用函数

| 库函数                                         | 描述                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `random.random()`                              | 返回随机浮点数，$\in \left[0.0, 1.0\right)$                  |
| `random.randint(a, b)`                         | 返回随机整数，$\in \left[a, b\right]$                        |
| `random.uniform(a, b)`                         | 返回随机浮点数，$\in\left[a, b\right]$                       |
| `random.gauss(mu, sigma)`                      | 生成一个服从**一元高斯分布**的随机数，`mu=均值，sigma=标准层` |
| `random.seed(seed)`                            | 使用给定种子`seed`初始化随机数生成器，有助于结果可复刻       |
| `random.choice(seq)`                           | 从序列`seq`中随机选择一个元素并返回                          |
| `random.choice(population, weights=None, k=k)` | 从序列`population`中随机选择`k`个元素，通过`weights`为元素指定被选中的概率权重 |
| `random.shuffle(seq)`                          | 随机打乱序列`seq`中元素的顺序                                |
| `random.sample(population, k)`                 | 从序列`population`中随机选择`k`个不重复的元素，相当于采集`k`个不重复的样本 |
| `random.betavariate(alpha, beta)`              | 生成一个服从**Beta分布**的随机数，`alpha`和`beta`控制Beta概率分布的形状 |
| `random.expovariate(lambd)`                    | 生成一个服从**指数分布**的随机数，`lambd`是指数分布的参数    |

