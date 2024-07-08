$$
\boldsymbol{x} = \begin{bmatrix} x_1 & x_2 & \cdots & x_n \end{bmatrix}^T \\
\big\Vert \boldsymbol{x} \big\Vert_p = \left( \big\vert x_1 \big\vert^p + \big\vert x_2 \big\vert^p + \cdots + \big\vert x_n \big\vert^p \right)^{1/p} = \left( \sum_{i=1}^n \big\vert x_i \big\vert^p \right)^{1/p}
$$

向量 $\boldsymbol{x}$ 的 $L^p$ 范数，$\big\Vert \boldsymbol{x} \big\Vert_p \geqslant 0$，$L^p$ 范数代表“距离”，一种“向量 $\rightarrow$ 标量”的运算规则。

**$L^2$ 范数**
$$
\big\Vert \boldsymbol{x} \big\Vert = \big\Vert \boldsymbol{x} \big\Vert_2 = \sqrt{x_1^2 + x_2^2 + \cdots + x_n^2} = \left( \sum_{i=1}^n x_i^2 \right)^{\frac{1}{2}}
$$
$\big\Vert \boldsymbol{x} \big\Vert$ 默认为 $L^2$ 范数。

$p \to \infty$ 时，对应的范数记为 $L^{\infty}$
$$
\big\Vert \boldsymbol{x} \big\Vert_\infty = \max(\big\vert x_1 \big\vert, \big\vert x_2 \big\vert, \cdots, \big\vert x_n \big\vert)
$$
$\big\Vert \boldsymbol{x} \big\Vert_\infty$ 为 $\big\vert x_i \big\vert$ 中的最大值。

 $L^p$ 范数丈量一个向量的“大小”