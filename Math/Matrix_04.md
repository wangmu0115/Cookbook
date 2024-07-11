
$$
\boldsymbol{x} = \begin{bmatrix} x_1\\x_2\\\vdots\\x_n \end{bmatrix}, \quad
\boldsymbol{y} = \begin{bmatrix} y_1\\y_2\\\vdots\\y_n \end{bmatrix}
$$

常用矩阵乘法代替向量内积运算。

$$
\boldsymbol{x} \cdot \boldsymbol{y} = \boldsymbol{y} \cdot \boldsymbol{x} = \langle\boldsymbol{x}, \boldsymbol{y}\rangle = \boldsymbol{x}^T\boldsymbol{y} = (\boldsymbol{x}^T\boldsymbol{y})^T = \boldsymbol{y}^T\boldsymbol{x} = x_1y_1 + x_2y_2 + \cdots + x_ny_n = \sum_{i=1}^nx_iy_i
$$

$\boldsymbol{x}$ 和 $\boldsymbol{y}$ 正交，则向量内积为零。
$$
\boldsymbol{x} \cdot \boldsymbol{y} = \boldsymbol{y} \cdot \boldsymbol{x} = \langle\boldsymbol{x}, \boldsymbol{y}\rangle = \boldsymbol{x}^T\boldsymbol{y} = (\boldsymbol{x}^T\boldsymbol{y})^T = \boldsymbol{y}^T\boldsymbol{x} = 0
$$


**全 $\boldsymbol{1}$ 列向量**
$$
\boldsymbol{1}\text{@}\boldsymbol{a} = \begin{bmatrix} 1\\1\\\vdots\\1 \end{bmatrix}_{n \times 1} \text{@} \boldsymbol{a}_{1 \times m} = \begin{bmatrix} \boldsymbol{a}\\\boldsymbol{a}\\\vdots\\\boldsymbol{a} \end{bmatrix}_{n \times m}
$$
全 $\boldsymbol{1}$ 列向量乘以行向量 $\boldsymbol{a}$ 相当于对行向量 $\boldsymbol{a}$ 进行复制，向下叠放
$$
\boldsymbol{b}_{n \times 1} \text{@} \boldsymbol{1}^T_{1 \times m} = 
$$
向量内积求和



### 矩阵乘向量

$$
\boldsymbol{A}_{n \times D} = 
\begin{bmatrix}
a_{1,1}&a_{1,2}&\cdots&a_{1,D} \\
a_{2,1}&a_{2,2}&\cdots&a_{2,D} \\
\vdots&\vdots&\ddots&\vdots \\
a_{n,1}&a_{n,2}&\cdots&a_{n,D}
\end{bmatrix}, \quad
\boldsymbol{x}_{D \times 1} = 
\begin{bmatrix}
x_1\\x_2\\\vdots\\x_D
\end{bmatrix}, \quad
\boldsymbol{b}_{n \times 1} = 
\begin{bmatrix}
x_1\\x_2\\\vdots\\x_n
\end{bmatrix}
$$

$$
\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b} \Rightarrow \\
\underbrace{ \begin{bmatrix}
a_{1,1}&a_{1,2}&\cdots&a_{1,D} \\
a_{2,1}&a_{2,2}&\cdots&a_{2,D} \\
\vdots&\vdots&\ddots&\vdots \\
a_{n,1}&a_{n,2}&\cdots&a_{n,D}
\end{bmatrix} }_{\boldsymbol{A}_{n \times D}}
\underbrace{\begin{bmatrix}
x_1\\x_2\\\vdots\\x_D
\end{bmatrix}}_{\boldsymbol{x}_{D \times 1}} = 
\underbrace{\begin{bmatrix}
x_1\\x_2\\\vdots\\x_n
\end{bmatrix}}_{\boldsymbol{b}_{n \times 1}}
$$

