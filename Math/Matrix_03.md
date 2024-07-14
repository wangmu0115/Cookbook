### 矩阵转置



### 逆矩阵



### 迹`trace`

$n \times n$ 矩阵 $\boldsymbol{A}$ 的**迹**是其对角线元素之和：
$$
\text{tr}(\boldsymbol{A}) = \sum_{i=1}^n a_{i,i} = a_{1,1} + a_{2,2} + \cdots + a_{n,n}
$$
矩阵迹的性质：
$$
\begin{array}{lcl}
\text{tr}(\boldsymbol{A} + \boldsymbol{B}) = \text{tr}(\boldsymbol{A}) + \text{tr}(\boldsymbol{B}) \\
\text{tr}(k\boldsymbol{A}) = k \cdot \text{tr}(\boldsymbol{A}) \\
\text{tr}(\boldsymbol{A}^T) = \text{tr}(\boldsymbol{A}) \\
\text{tr}(\boldsymbol{A}\boldsymbol{B}) = \text{tr}(\boldsymbol{B}\boldsymbol{A})
\end{array}
$$
如果 $\boldsymbol{x}$ 和 $\boldsymbol{y}$ 列向量行数相同，则以下几个运算等价：
$$
\boldsymbol{x}^T\boldsymbol{y} = \boldsymbol{y}^T\boldsymbol{x} = \boldsymbol{x} \cdot \boldsymbol{y} = \boldsymbol{y} \cdot \boldsymbol{x} = \langle \boldsymbol{x}, \boldsymbol{y} \rangle = \text{tr}(\boldsymbol{x}\boldsymbol{y}^T) = \text{tr}(\boldsymbol{y}\boldsymbol{x}^T) = \text{tr}(\boldsymbol{x} \otimes \boldsymbol{y})
$$

### 逐项积

**元素乘积**，**阿玛达乘积**或**逐项积**：两个形状相同的矩阵对应元素分别相乘，结果形状不变。
$$
\boldsymbol{A}_{n \times m} \odot \boldsymbol{B}_{n \times m} = 
\begin{bmatrix}
a_{1,1}b_{1,1} & a_{1,2}b_{1,2} & \cdots & a_{1,m}b_{1,m} \\
a_{2,1}b_{2,1} & a_{2,2}b_{2,2} & \cdots & a_{2,m}b_{2,m} \\
\vdots & \vdots & \ddots & \vdots\\
a_{n,1}b_{n,1} & a_{n,2}b_{n,2} & \cdots & a_{n,m}b_{n,m} \\
\end{bmatrix}
$$

### 行列式

方阵 $\boldsymbol{A}$ 的**行列式**值可以表示为 $\left\vert \boldsymbol{A} \right\vert$ 或 $\det(\boldsymbol{A})$，**如果方阵的行列式值非零，则称方阵可逆或非奇异**。

一阶方阵的行列式值
$$
\begin{vmatrix} a_{1,1} \end{vmatrix} = a_{1,1}
$$
二阶方阵的行列式值
$$
\begin{vmatrix}
a_{1,1} & a_{1,2} \\
a_{2,1} & a_{2,2}
\end{vmatrix} = a_{1,1}a_{2,2} - a_{1,2}a_{2,1}
$$
三阶方阵的行列式值
$$
\begin{vmatrix}
a_{1,1} & a_{1,2} & a_{1,3} \\
a_{2,1} & a_{2,2} & a_{2,3} \\
a_{3,1} & a_{3,2} & a_{3,3}
\end{vmatrix} = 
a_{1,1}
\begin{vmatrix}
a_{2,2} & a_{2,3} \\
a_{3,2} & a_{3,3}
\end{vmatrix}
-a_{1,2}
\begin{vmatrix}
a_{2,1} & a_{2,3} \\
a_{3,1} & a_{3,3}
\end{vmatrix}
+a_{1,3}
\begin{vmatrix}
a_{2,1} & a_{2,2} \\
a_{3,1} & a_{3,2}
\end{vmatrix}
$$
$n \times n$ 矩阵 $\boldsymbol{A}$ 的行列式值可以通过递归计算得到。

行列式性质：
$$
\begin{array}{lcl}
\det(\boldsymbol{A}\boldsymbol{B}) = \det(\boldsymbol{A}) \cdot \det(\boldsymbol{B}) \\
\det(c\boldsymbol{A}_{n \times n}) = c^n\det(\boldsymbol{A}) \\
\det(\boldsymbol{A}^T) = \det(\boldsymbol{A}) \\
\det(\boldsymbol{A}^n) = \det(\boldsymbol{A})^n \\
\det(\boldsymbol{A}^{-1}) = \dfrac{1}{\det(\boldsymbol{A})} \\
\det(\boldsymbol{A} + \boldsymbol{B}) \neq \det(\boldsymbol{A}) + \det(\boldsymbol{B})
\end{array}
$$

















