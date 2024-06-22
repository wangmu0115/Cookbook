> [`math`](https://docs.python.org/3/library/math.html)
>
> `import math`

### 常量

| 库常量     | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `math.pi`  | $\pi$                                                        |
| `math.tau` | $2\pi$                                                       |
| `math.e`   | $e$                                                          |
| `math.inf` | 正无穷大，`float("inf")`                                     |
| `math.nan` | `Not a Number`，`float("nan")`，使用`math.isnan()`判断是否为`NaN` |

### 常用函数

| 库函数                        | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| `math.ceil(x)`                | 向上取整，$\left\lceil x \right\rceil$                       |
| `math.floor(x)`               | 向下取整，$\left\lfloor x \right\rfloor$                     |
| `math.comb(n, k)`             | 组合数，$\binom{n}{k}$                                       |
| `math.perm(n, k)`             | 排列数，$\mathrm{P}_n^k$                                     |
| `math.fabs(x)`                | 绝对值，$\left\vert x \right\vert$                           |
| `math.factorial(n)`           | 阶乘，$n!$                                                   |
| `math.sqrt(x)`                | 平方根，$\sqrt x$                                            |
| `math.cbrt(x)`                | 立方根，$\sqrt[3] x$                                         |
| `math.pow(a, x)`              | 以`a`为底的指数，$a^x$                                       |
| `math.exp(x)`                 | 以`e`为底的指数，等同于`math.pow(math.e, x)`，$e^x$          |
| `math.log(x)`                 | 以`e`为底的对数，$\ln x$                                     |
| `math.log2(x)`                | 以`2`为底的对数，比`math.log(x, 2)`更准确，$\log_2 x$        |
| `math.log10(x)`               | 以`10`为底的对数，比`math.log(x, 10)`更准确，$\log_{10} x$   |
| `math.dist(p, q)`             | 欧几里得距离，$\left\Vert \vec p - \vec q \right\Vert$       |
| `math.hypot(x1, x2, x3, ...)` | 距离原点的欧几里得距离，$\left\Vert \vec x \right\Vert = \sqrt{x_1^2 + x_2^2 + x_3^2 + ...}$ |
| `math.sin(x)`                 | 正弦，输入为弧度，$\sin x$                                   |
| `math.cos(x)`                 | 余弦，输入为弧度，$\cos x$                                   |
| `math.tan(x)`                 | 正切，输入为弧度，$\tan x $                                  |
| `math.asin(x)`                | 反正弦，$\in \left[ -\frac{\pi}{2}, \frac{\pi}{2} \right]$，$\arcsin x$ |
| `math.acos(x)`                | 反余弦，$\in \left[ 0, \pi \right]$，$\arccos x$             |
| `math.atan(x)`                | 反正切，$\in \left[ -\frac{\pi}{2}, \frac{\pi}{2} \right]$，$\arctan x$ |
| `math.atan2(y, x)`            | 反正切，$\in \left[ -\pi, \pi \right]$，$\arctan {\frac{y}{x}}$，相比`math.atan(x)`可以计算角度正确的象限 |
| `math.sinh(x)`                | 双曲正弦，$\sinh x$                                          |
| `math.cosh(x)`                | 双曲余弦，$\cosh x$                                          |
| `math.tanh(x)`                | 双曲正切，$\tanh x$                                          |
| `math.asinh(x)`               | 反双曲正弦，$\sinh^{-1}x$                                    |
| `math.acosh(x)`               | 反双曲余弦，$\cosh^{-1}x$                                    |
| `math.atanh(x)`               | 反双曲正切，$\tanh^{-1}x$                                    |
| `math.radians(x)`             | 将角度转换为弧度，$\frac{\pi}{180} \times x$                 |
| `math.degrees(x)`             | 将弧度转换为角度，$\frac{x}{\pi} \times 180$                 |
| `math.erf(x)`                 | 误差函数，$\frac{2}{\sqrt{\pi}}\int\limits_{0}^{x}e^{-t^2}\,dt$ |
| `math.gamma(x)`               | Gamma函数，$\Gamma(x)=(x-1)!$                                |

