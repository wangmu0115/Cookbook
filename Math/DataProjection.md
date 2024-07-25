## 数据投影 `Data Projection`

$$
\boldsymbol{Z} = \boldsymbol{X}\boldsymbol{V}
$$

$\boldsymbol{X}_{n \times D}$ 是数据矩阵，每一行代表一个数据样本，每一列代表一个特征。

$\boldsymbol{V}_{D \times D}$ 是正交矩阵，$\boldsymbol{V} = \begin{bmatrix}\boldsymbol{v}_1, \boldsymbol{v}_2, \ldots, \boldsymbol{v}_D\end{bmatrix}$ 是 $\mathbb{R}^D$ 空间的一组规范正交基。

几何视角下，矩阵乘法 $\boldsymbol{X}\boldsymbol{V}$ 完成的是 $\boldsymbol{X}$ 向规范正交基 $\boldsymbol{V} = \begin{bmatrix}\boldsymbol{v}_1, \boldsymbol{v}_2, \ldots, \boldsymbol{v}_D\end{bmatrix}$ 投影，$\boldsymbol{Z}$ 代表 $\boldsymbol{X}$ 在新的规范正交基下的坐标。

矩阵乘法 $\boldsymbol{Z} = \boldsymbol{X}\boldsymbol{V}$ 也是一个线性映射过程。



**列向量**
$$
\begin{align}
\begin{bmatrix} \boldsymbol{z}_1 & \boldsymbol{z}_2 & \cdots & \boldsymbol{z}_D \end{bmatrix} 
&=\boldsymbol{X}\begin{bmatrix} \boldsymbol{v}_1 & \boldsymbol{v}_2 & \cdots & \boldsymbol{v}_D \end{bmatrix} \\
&=\begin{bmatrix} \boldsymbol{X}\boldsymbol{v}_1 & \boldsymbol{X}\boldsymbol{v}_2 & \cdots & \boldsymbol{X}\boldsymbol{v}_D \end{bmatrix}
\end{align}
$$
数据列向量之间的转换
$$
\boldsymbol{z}_j = \boldsymbol{X}\boldsymbol{v}_j
=\underbrace{\begin{bmatrix} \boldsymbol{x}_1 & \boldsymbol{x}_2 & \cdots & \boldsymbol{x}_D \end{bmatrix}}_{\boldsymbol{X}} \underset{\boldsymbol{v}_j}{\begin{bmatrix} {v}_{1,j} \\ {v}_{2,j} \\ \vdots \\ {v}_{D,j} \end{bmatrix}} = {v}_{1,j}\boldsymbol{x}_1 + {v}_{2,j}\boldsymbol{x}_2 + \cdots + {v}_{D,j}\boldsymbol{x}_D
$$
线性组合

**行向量**










$$
\boldsymbol{X} = \boldsymbol{X}\boldsymbol{I} = \boldsymbol{X}\boldsymbol{V}\boldsymbol{V}^T
$$

$$
\boldsymbol{V}_{D \times D} = \begin{bmatrix} \boldsymbol{v}_1&\boldsymbol{v}_2&\cdots&\boldsymbol{v}_D \end{bmatrix}
$$

$$
\boldsymbol{X} = \boldsymbol{X}\boldsymbol{V}\boldsymbol{V}^T
= \boldsymbol{X}\begin{bmatrix} \boldsymbol{v}_1&\boldsymbol{v}_2&\cdots&\boldsymbol{v}_D \end{bmatrix}\begin{bmatrix} \boldsymbol{v}_1^T\\\boldsymbol{v}_2^T\\\vdots\\\boldsymbol{v}_D \end{bmatrix}
= \boldsymbol{X}\boldsymbol{v}_1\boldsymbol{v}_1^T + \boldsymbol{X}\boldsymbol{v}_2\boldsymbol{v}_2^T + \cdots + \boldsymbol{X}\boldsymbol{v}_D\boldsymbol{v}_D^T
$$

$$
\boldsymbol{X}_j = \boldsymbol{X}\boldsymbol{v}_j\boldsymbol{v}_j^T
$$

$$
\boldsymbol{X} = \boldsymbol{X}_1 + \boldsymbol{X}_2 + \cdots + \boldsymbol{X}_D
$$

$\boldsymbol{X}$ 是 $n \times D$ 
$$
\boldsymbol{X}_{n \times D} = \begin{bmatrix}\boldsymbol{x}^{(1)}\\\boldsymbol{x}^{(2)}\\\cdots\\\boldsymbol{x}^{(n)}\end{bmatrix}
$$
$\boldsymbol{X}_j$ 的第 $i$ 行行向量 $\boldsymbol{x}_j^{(i)}$​
$$
\boldsymbol{x}_j^{(i)} = \boldsymbol{x}^{(i)}\boldsymbol{v}_j\boldsymbol{v}_j^T
$$
























