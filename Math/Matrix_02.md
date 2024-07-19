## 矩阵乘法

### 1. 向量乘向量

$$
\boldsymbol{x} = \begin{bmatrix} x_1\\x_2\\\vdots\\x_n \end{bmatrix}, \quad
\boldsymbol{y} = \begin{bmatrix} y_1\\y_2\\\vdots\\y_n \end{bmatrix}
$$

**向量内积**可以表示成矩阵乘法
$$
\boldsymbol{x} \cdot \boldsymbol{y} = \boldsymbol{y} \cdot \boldsymbol{x} = \langle\boldsymbol{x}, \boldsymbol{y}\rangle = \boldsymbol{x}^T\boldsymbol{y} = (\boldsymbol{x}^T\boldsymbol{y})^T = \boldsymbol{y}^T\boldsymbol{x} = x_1y_1 + x_2y_2 + \cdots + x_ny_n = \sum_{i=1}^nx_iy_i = \big\Vert \boldsymbol{a} \big\Vert \big\Vert \boldsymbol{b} \big\Vert \cos\theta
$$

列向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$ 的**张量积**，等同于  $\boldsymbol{x}$ 和 $\boldsymbol{y}^T$ 的矩阵乘法
$$
\boldsymbol{x}_{n \times 1} \otimes \boldsymbol{y}_{m \times 1} = \boldsymbol{x}\boldsymbol{y}^T \\
\boldsymbol{y}_{m \times 1} \otimes \boldsymbol{x}_{n \times 1} = \boldsymbol{y}\boldsymbol{x}^T \\
\boldsymbol{x} \otimes \boldsymbol{x} = \boldsymbol{x}\boldsymbol{x}^T = \begin{bmatrix} x_1x_1&x_1x_2&\cdots&x_1x_n\\x_2x_1&x_2x_2&\cdots&x_2x_n\\\vdots&\vdots&\ddots&\vdots\\x_nx_1&x_nx_2&\cdots&x_nx_n \end{bmatrix}
$$

### 2. 矩阵乘向量

#### 2.1 线性方程组

$$
\begin{cases}
a_{1,1}x_1 + a_{1,2}x_2 + \cdots + a_{1,D}x_D = b_1 \\
a_{2,1}x_1 + a_{2,2}x_2 + \cdots + a_{2,D}x_D = b_2 \\
\vdots\\
a_{n,1}x_1 + a_{n,2}x_2 + \cdots + a_{n,D}x_D = b_n
\end{cases}
$$

可以写成 $\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b}$，其中

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

- 有唯一解的方程组被称为**恰定方程组**。
- 有无穷多解的方程组被称作**欠定方程组**。
- 解不存在的方程组被称作**超定方程组**。

如果矩阵 $\boldsymbol{A}$ 可逆，则 $\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b}$ 有唯一解：
$$
\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b} \Rightarrow \boldsymbol{x} = \boldsymbol{A}^{-1}\boldsymbol{b}
$$
如果 $\boldsymbol{A}^T\boldsymbol{A}$ 可逆，则可以进一步求解：
$$
\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b} \Rightarrow \boldsymbol{A}^T\boldsymbol{A}\boldsymbol{x} = \boldsymbol{A}^T\boldsymbol{b} \Rightarrow \boldsymbol{x} = \underbrace{(\boldsymbol{A}^T\boldsymbol{A})^{-1}\boldsymbol{A}^T}_{\boldsymbol{A}^+}\boldsymbol{b}
$$
$(\boldsymbol{A}^T\boldsymbol{A})^{-1}\boldsymbol{A}^T$ 常被称作 **广义逆**或**伪逆**。

#### 2.2 线性组合

$$
\boldsymbol{A}_{n \times D} = \begin{bmatrix} \boldsymbol{a}_1&\boldsymbol{a}_2&\cdots&\boldsymbol{a}_D \end{bmatrix}, \quad \boldsymbol{a}_i = \begin{bmatrix} a_{i,1} \\ a_{i,2} \\ \vdots \\ a_{i,n} \end{bmatrix} \\\\
\begin{array}{lcl}
\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b} \\
\Rightarrow \begin{bmatrix} \boldsymbol{a}_1&\boldsymbol{a}_2&\cdots&\boldsymbol{a}_D \end{bmatrix}\begin{bmatrix} x_1\\x_2\\\vdots\\x_D \end{bmatrix} = \boldsymbol{b} \\
\Rightarrow x_1\boldsymbol{a}_1 + x_2\boldsymbol{a}_2 + \cdots + x_D\boldsymbol{a}_D = \boldsymbol{b}_{n \times 1}
\end{array}
$$

当 $x_1, x_2, \ldots, x_D$ 取具体值时，上式代表**线性组合**。

#### 2.3 线性映射

$$
\underbrace{\begin{bmatrix} a_{1,1}&a_{1,2}&\cdots&a_{1,D} \\ a_{2,1}&a_{2,2}&\cdots&a_{2,D} \\ \vdots&\vdots&\ddots&\vdots \\ a_{n,1}&a_{n,2}&\cdots&a_{n,D} \end{bmatrix}}_{\boldsymbol{A}_{n \times D}} \underset{\boldsymbol{x}_{D \times 1}}{\begin{bmatrix} x_1\\x_2\\\vdots\\x_D \end{bmatrix}} = \underset{\boldsymbol{b}_{n \times 1}}{\begin{bmatrix} b_1\\b_2\\\vdots\\b_n \end{bmatrix}}
$$

上式代表从 $\mathbb{R}^D$ 空间到 $\mathbb{R}^n$ 空间的**线性映射**，当且仅当 $\boldsymbol{A}$ 可逆，可以完成从 $\mathbb{R}^n$ 空间到 $\mathbb{R}^D$ 空间的映射。当 $n=D$ 时，称这种线性映射叫**线性变换**。

### 3. 向量乘矩阵乘向量

**二次型**的矩阵算式
$$
\boldsymbol{x}^T\boldsymbol{Q}\boldsymbol{x} = q 
$$
$\boldsymbol{Q}$ 是**对称矩阵**，$q \in \mathbb{R}$。
$$
\boldsymbol{x} = \begin{bmatrix} x_1\\x_2\\\vdots\\x_D \end{bmatrix}, \quad \boldsymbol{Q} = \begin{bmatrix} q_{1,1}&q_{1,2}&\cdots&q_{1,D}\\q_{2,1}&q_{2,2}&\cdots&q_{2,D}\\\vdots&\vdots&\ddots&\vdots\\q_{D,1}&q_{D,2}&\cdots&q_{D,D}\\ \end{bmatrix}
$$
**三个方阵连乘**





### 4. 方阵乘方阵

$$
\boldsymbol{A}^2 = \boldsymbol{A}
$$

则称 $\boldsymbol{A}$​ 为**幂等矩阵**。



### 5. 对角阵



### 6. 置换矩阵

置换矩阵是由 0 和 1 组成的方阵。置换矩阵的每一行、每一列都恰好只有一个 1，其余元素均为 0。置换矩阵的作用是调换元素顺序。
$$
\begin{bmatrix} a_1&a_2&a_3&a_4 \end{bmatrix}\begin{bmatrix}0&1&0&0\\0&0&0&1\\1&0&0&0\\0&0&1&0\end{bmatrix} = \begin{bmatrix} a_3&a_1&a_4&a_2 \end{bmatrix}
$$







### 全 $1$ 列向量

$$
\boldsymbol{1}_{n \times 1} = \begin{bmatrix} 1\\1\\\vdots\\1 \end{bmatrix}
$$

复制行向量或列向量形成矩阵

$$
\boldsymbol{1}_{n \times 1}\text{@}\boldsymbol{a}_{1 \times m} = \begin{bmatrix} \boldsymbol{a}\\\boldsymbol{a}\\\vdots\\\boldsymbol{a} \end{bmatrix}_{n \times m} \\\\
\boldsymbol{b}_{n \times 1}\text{@}\boldsymbol{1}_{m \times 1}^T = \begin{bmatrix} \boldsymbol{b}&\boldsymbol{b}&\cdots&\boldsymbol{b} \end{bmatrix}_{n \times m}
$$
列向量元素求和
$$
\boldsymbol{1} \cdot \boldsymbol{x} = \boldsymbol{1}^T\boldsymbol{x} = \boldsymbol{x}^T\boldsymbol{1} = \sum_{i=1}^n{x_i}
$$
元素平均数
$$
\text{E}(\boldsymbol{x}) = \dfrac{1}{n}\sum_{i=1}^n{x_i} = \dfrac{\boldsymbol{1} \cdot \boldsymbol{x}}{n} = \dfrac{\boldsymbol{1}^T\boldsymbol{x}}{n} = \dfrac{\boldsymbol{x}^T\boldsymbol{1}}{n}
$$
元素平方和
$$
\boldsymbol{x}\cdot\boldsymbol{x} = \boldsymbol{x}^T\boldsymbol{x} = \sum_{i=1}^n{x_i^2}
$$

每列元素求和



$$

$$
