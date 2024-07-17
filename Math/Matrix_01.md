## 矩阵`Matrix`

矩阵是由标量组成的矩形**数组**，矩阵内的元素不局限于标量，也可以是虚数、符号、代数式、偏导等等。

**张量 `tensor`**

$n$ 行 $D$ 列矩阵 $\boldsymbol{X}$ 定义如下：
$$
\boldsymbol{X}_{n \times D} = 
\begin{bmatrix}
x_{1,1}&x_{1,2}&\cdots&x_{1,D}\\
x_{2,1}&x_{2,2}&\cdots&x_{2,D}\\
\vdots&\vdots&\ddots&\vdots\\
x_{n,1}&x_{n,2}&\cdots&x_{n,D}
\end{bmatrix}
$$
其中，$n$ 是**矩阵行数**，$D$ 是**矩阵列数**。从样本数据角度看，$n$ 是样本数，$D$ 是样本数据特征数。

矩阵 $\boldsymbol{X}$ 中**元素 $x_{i,j}$** 被称作 $(i,j)$ 元素，第 $i$ 行、第 $j$ 列元素。

### 1. 矩阵形状

| 矩阵形状       | 描述                                                         | 备注                                                         |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **列向量**     | $n \times 1$ 矩阵                                            | $\boldsymbol{x} = \begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}$ |
| **行向量**     | $1 \times m$ 矩阵                                            | $\boldsymbol{x} = \begin{bmatrix}x_1&x_2&\cdots&x_m\end{bmatrix}$ |
| **方阵**       | $n \times n$ 矩阵，又称 $n$ 阶方阵                           | $\boldsymbol{A}_{n \times n}$                                |
| **对称方阵**   | 右上和左下元素以**主对角线**镜像对称的 $n$ 阶方阵            | $\boldsymbol{A} = \boldsymbol{A}^T$                          |
| **对角矩阵**   | 主对角线之外的元素都是 $0$，不一定是方阵                     | $\boldsymbol{\varLambda}_{n \times n} = \begin{bmatrix} \lambda_1&0&\cdots&0 \\ 0&\lambda_2&\cdots&0 \\ \vdots&\vdots&\ddots&\vdots \\ 0&0&\cdots&\lambda_n \end{bmatrix}$ |
| 副对角矩阵     | 副对角线之外的元素都是 $0$                                   |                                                              |
| **单位矩阵**   | $n$ 阶方阵对角线上的元素为 $1$，其余元素为 $0$，记作**$n$ 阶单位矩阵**，记作 $\boldsymbol{I}$ | $\boldsymbol{I}_{n \times n} = \begin{bmatrix} 1&0&\cdots&0\\0&1&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&1 \end{bmatrix}$ |
| **上三角矩阵** | $n$ 阶方阵对角线以下元素均为 $0$，记作 $\boldsymbol{U}_{n \times n}$ | $\boldsymbol{U}_{n \times n} = \begin{bmatrix} u_{1,1}&u_{1,2}&\cdots&u_{1,n}\\0&u_{2,2}&\cdots&u_{2,n}\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&u_{n,n} \end{bmatrix}$ |
| **下三角矩阵** | $n$ 阶方阵对角线以上元素均为 $0$，记作 $\boldsymbol{L}_{n \times n}$ | $\boldsymbol{L}_{n \times n} = \begin{bmatrix} l_{1,1}&0&\cdots&0\\l_{2,1}&l_{2,2}&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\l_{n,1}&l_{n,2}&\cdots&l_{n,n} \end{bmatrix}$ |
| **零矩阵**     | 元素全为 $0$ 的矩阵，记作 $\boldsymbol{O}$                   | $\boldsymbol{O}_{m \times n} = \begin{bmatrix} 0&0&\cdots&0\\0&0&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&0 \end{bmatrix}$ |

### 2. 矩阵加减

两个相同大小的矩阵 $\boldsymbol{A}$ 和 $\boldsymbol{B}$ 相加，是将这两个矩阵对应位置元素相加：
$$
\boldsymbol{A}_{m \times n} + \boldsymbol{B}_{m \times n} = 
\begin{bmatrix}
a_{1,1} + b_{1,1}&a_{1,2} + b_{1,2}&\cdots&a_{1,n} + b_{1,n}\\
a_{2,1} + b_{2,1}&a_{2,2} + b_{2,2}&\cdots&a_{2,n} + b_{2,n}\\
\cdots&\cdots&\ddots&\cdots\\
a_{m,1} + b_{m,1}&a_{m,2} + b_{m,2}&\cdots&a_{m,n} + b_{m,n}
\end{bmatrix}
$$
矩阵加法满足**交换律**和**结合律**：
$$
\begin{array}{lcl}
\boldsymbol{A} + \boldsymbol{B} = \boldsymbol{B} + \boldsymbol{A} \\
\boldsymbol{A} + \boldsymbol{B} + \boldsymbol{C} = (\boldsymbol{A} + \boldsymbol{B}) + \boldsymbol{C} = \boldsymbol{A} + (\boldsymbol{B} + \boldsymbol{C})
\end{array}
$$
**矩阵减法**的运算规则与加法一致。

### 3. 矩阵标量乘法

矩阵乘以标量时，矩阵的每一个元素都乘以该标量，这种运算叫做**标量乘法**，标量 $k$ 和矩阵 $\boldsymbol{X}$ 的乘积记作 $k\boldsymbol{X}$。
$$
k\boldsymbol{X}_{n \times D} = 
\begin{bmatrix}
k \cdot x_{1,1} & k \cdot x_{1,2} & \cdots & k \cdot x_{1,D} \\
k \cdot x_{2,1} & k \cdot x_{2,2} & \cdots & k \cdot x_{2,D} \\
\vdots & \vdots & \ddots & \vdots \\
k \cdot x_{n,1} & k \cdot x_{n,2} & \cdots & k \cdot x_{n,D} \\
\end{bmatrix}
$$
当 $k = 0$ 时，结果为零矩阵 $\boldsymbol{O}_{n \times D}$。

### 4. 矩阵乘法

**线性映射**，$\boldsymbol{A}\boldsymbol{x}=\boldsymbol{b}$ 完成 $\boldsymbol{x} \rightarrow \boldsymbol{b}$ 的线性映射，如果 $\boldsymbol{A}$ 可逆，$\boldsymbol{A}^{-1}$完成 $\boldsymbol{b} \rightarrow \boldsymbol{x}$ 的线性映射。 
$$
\boldsymbol{x} \xrightleftharpoons[\boldsymbol{x}=\boldsymbol{A}^{-1}\boldsymbol{b}]{\boldsymbol{A}\boldsymbol{x}=\boldsymbol{b}} \boldsymbol{b}
$$

矩阵 $\boldsymbol{A}$ 的列数等于矩阵 $\boldsymbol{B}$ 的行数，$\boldsymbol{A}$ 和 $\boldsymbol{B}$ 两个矩阵可以相乘。

$$
\begin{array}{lcl}
\boldsymbol{A}_{n \times D} = 
\begin{bmatrix}
a_{1,1}&a_{1,2}&\cdots&a_{1,D}\\
a_{2,1}&a_{2,2}&\cdots&a_{2,D}\\
\vdots&\vdots&\ddots&\vdots\\
a_{n,1}&a_{n,2}&\cdots&a_{n,D}
\end{bmatrix}, \quad
\boldsymbol{B}_{D \times m} = 
\begin{bmatrix}
b_{1,1}&b_{1,2}&\cdots&b_{1,m}\\
b_{2,1}&b_{2,2}&\cdots&b_{2,m}\\
\vdots&\vdots&\ddots&\vdots\\
b_{D,1}&b_{D,2}&\cdots&b_{D,m}
\end{bmatrix}
\\
\boldsymbol{C}_{n \times m} = \boldsymbol{A}_{n \times D} \boldsymbol{B}_{D \times m}  = 
\begin{bmatrix}
c_{1,1}&c_{1,2}&\cdots&c_{1,m}\\
c_{2,1}&c_{2,2}&\cdots&c_{2,m}\\
\vdots&\vdots&\ddots&\vdots\\
c_{n,1}&c_{D,2}&\cdots&c_{n,m}
\end{bmatrix}, \quad c_{i,j} = a_{i,1}b_{1,j} + a_{i,2}b_{2,j} + \cdots + a_{i,D}b_{D,j}
\end{array}
$$

矩阵乘法**不满足交换律**
$$
\boldsymbol{A}\boldsymbol{B} \neq \boldsymbol{B}\boldsymbol{A}
$$
**矩阵乘法常用规则**
$$
\begin{align}
\boldsymbol{A}\boldsymbol{O} &= \boldsymbol{O} \\
\boldsymbol{A}\boldsymbol{B}\boldsymbol{C} &= \boldsymbol{A}(\boldsymbol{B}\boldsymbol{C}) = (\boldsymbol{A}\boldsymbol{B})\boldsymbol{C} \\
k(\boldsymbol{A}\boldsymbol{B}) &= (k\boldsymbol{A})\boldsymbol{B} = \boldsymbol{A}(k\boldsymbol{B}) = (\boldsymbol{A}\boldsymbol{B})k \\
\boldsymbol{A}(\boldsymbol{B} + \boldsymbol{C}) &= \boldsymbol{A}\boldsymbol{B} + \boldsymbol{A}\boldsymbol{C} 
\end{align}
$$

$n$ 阶方阵 $\boldsymbol{A}$ 的**矩阵的幂**
$$
\begin{align}
\boldsymbol{A}^0 &= \boldsymbol{I} \\
\boldsymbol{A}^1 &= \boldsymbol{A} \\
\boldsymbol{A}^2 &= \boldsymbol{A}\boldsymbol{A} \\
\boldsymbol{A}^{n+1} &= \boldsymbol{A}^n\boldsymbol{A}
\end{align}
$$

### 5. 转置

矩阵的行列互换得到的新矩阵的操作为**矩阵转置**，记作 $\boldsymbol{A}^T$。 

**矩阵转置常用性质**
$$
\begin{align}
\left(\boldsymbol{A}^T\right)^T &= \boldsymbol{A} \\
\left(\boldsymbol{A} + \boldsymbol{B}\right)^T &= \boldsymbol{A}^T + \boldsymbol{B}^T \\
\left(k\boldsymbol{A}\right)^T &= k\boldsymbol{A}^T \\
\left(\boldsymbol{A}\boldsymbol{B}\right)^T &= \boldsymbol{B}^T\boldsymbol{A}^T \\
\left(\boldsymbol{A}\boldsymbol{B}\boldsymbol{C}\right)^T &= \boldsymbol{C}^T\boldsymbol{B}^T\boldsymbol{A}^T \\
\left(\boldsymbol{A}_1\boldsymbol{A}_2\cdots\boldsymbol{A}_k\right)^T &= \boldsymbol{A}_k^T\cdots\boldsymbol{A}_2^T\boldsymbol{A}_1^T 
\end{align}
$$
**等长**列向量 $\boldsymbol{a}$ 和 $\boldsymbol{b}$ 的标量积等价于 $\boldsymbol{a}$ 的转置乘 $\boldsymbol{b}$，或 $\boldsymbol{b}$ 的转置乘 $\boldsymbol{a}$
$$
\langle\boldsymbol{a},\boldsymbol{b}\rangle = \boldsymbol{a} \cdot \boldsymbol{b} = \boldsymbol{b} \cdot \boldsymbol{a} = \boldsymbol{a}^T\boldsymbol{b} = \boldsymbol{b}^T\boldsymbol{a} = \sum_{i=1}^na_ib_i
$$

### 6. 逆矩阵

方阵 $\boldsymbol{A}$ 如果**可逆**，仅当存在矩阵 $\boldsymbol{B}$ 使得
$$
\boldsymbol{A}\boldsymbol{B} = \boldsymbol{B}\boldsymbol{A} = \boldsymbol{I}
$$
$\boldsymbol{B}$ 叫做矩阵 $\boldsymbol{A}$ 的**逆**，记作 $\boldsymbol{A}^{-1}$，矩阵**可逆**也称**非奇异**，否则称矩阵**不可逆**或**奇异**。**如果 $\boldsymbol{A}^{-1}$ 存在，则一定唯一**。

**矩阵逆常用性质**
$$
\begin{align}
\left(\boldsymbol{A}^T\right)^{-1} &= \left(\boldsymbol{A}^{-1}\right)^T \\
\left(\boldsymbol{A}\boldsymbol{B}\right)^{-1} &= \boldsymbol{B}^{-1}\boldsymbol{A}^{-1} \\
\left(\boldsymbol{A}\boldsymbol{B}\boldsymbol{C}\right)^{-1} &= \boldsymbol{C}^{-1}\boldsymbol{B}^{-1}\boldsymbol{A}^{-1} \\
\left(k\boldsymbol{A}\right)^{-1} &= \dfrac{1}{k}\boldsymbol{A}^{-1}
\end{align}
$$
如果 $\boldsymbol{A}^{-1}$ 存在，则如下等式成立
$$
\begin{align}
\left(\boldsymbol{A}^{-1}\right)^{-1} &= \boldsymbol{A} \\
\boldsymbol{A}^{-n} &= \left(\boldsymbol{A}^{-1}\right)^n = \underbrace{\boldsymbol{A}^{-1}\boldsymbol{A}^{-1}\cdots\boldsymbol{A}^{-1}}_{n} \\
\left(\boldsymbol{A}^n\right)^{-1} &= \boldsymbol{A}^{-n} = \left(\boldsymbol{A}^{-1}\right)^n
\end{align}
$$
一般情况下
$$
\left(\boldsymbol{A} + \boldsymbol{B}\right)^{-1} \neq \boldsymbol{A}^{-1} + \boldsymbol{B}^{-1}
$$
如果方阵 $\boldsymbol{A}$ 是**正交矩阵**
$$
\boldsymbol{A}^T = \boldsymbol{A}^{-1} \Rightarrow \boldsymbol{A}\boldsymbol{A}^T = \boldsymbol{A}^T\boldsymbol{A} = \boldsymbol{A}\boldsymbol{A}^{-1} = \boldsymbol{I}
$$

### 7. 迹 `trace`

**$n$ 阶方阵** $\boldsymbol{A}$ 的**迹**是其对角线元素之和：
$$
\text{tr}(\boldsymbol{A}) = \sum_{i=1}^n a_{i,i} = a_{1,1} + a_{2,2} + \cdots + a_{n,n}
$$
**矩阵迹常用性质**
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

### 8. 逐项积 `Hadamard product`

**元素乘积**，**阿玛达乘积**或**逐项积**：两个**形状相同的矩阵**对应元素分别相乘，结果形状不变。
$$
\boldsymbol{A}_{n \times m} \odot \boldsymbol{B}_{n \times m} = 
\begin{bmatrix}
a_{1,1}b_{1,1} & a_{1,2}b_{1,2} & \cdots & a_{1,m}b_{1,m} \\
a_{2,1}b_{2,1} & a_{2,2}b_{2,2} & \cdots & a_{2,m}b_{2,m} \\
\vdots & \vdots & \ddots & \vdots\\
a_{n,1}b_{n,1} & a_{n,2}b_{n,2} & \cdots & a_{n,m}b_{n,m} \\
\end{bmatrix}
$$

### 9. 行列式









