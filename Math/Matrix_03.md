## 分块矩阵 `Block Matrix`

**分块矩阵**将一个矩阵用若干条横线和竖线分割成多个**子块矩阵**。

**切丝、切条**

将矩阵 $\boldsymbol{X}_{n \times D}$ 看做是 **$n$ 个行向量**或 **$D$ 个列向量**按照一定规则构造而成。
$$
\boldsymbol{X}_{n \times D} = \begin{bmatrix} x_{1,1}&x_{1,2}&\cdots&x_{1,D} \\ x_{2,1}&x_{2,2}&\cdots&x_{2,D} \\ \vdots&\vdots&\ddots&\vdots \\ x_{n,1}&x_{n,2}&\cdots&x_{n,D} \end{bmatrix} = \begin{bmatrix} \boldsymbol{x}^{(1)} \\ \boldsymbol{x}^{(2)} \\ \vdots \\ \boldsymbol{x}^{(n)} \end{bmatrix} = \begin{bmatrix} \boldsymbol{x}_1 & \boldsymbol{x}_2 & \cdots & \boldsymbol{x}_D \end{bmatrix}
$$
**切块**
$$
\boldsymbol{A} = \begin{bmatrix} 1&2&3&0&0\\4&5&6&0&0\\0&0&0&-1&0\\0&0&0&0&1 \end{bmatrix} = \begin{bmatrix} \boldsymbol{A}_{1,1} & \boldsymbol{A}_{1,2} \\ \boldsymbol{A}_{2,1} & \boldsymbol{A}_{2,2} \end{bmatrix} \\\\
\boldsymbol{A}_{1,1} = \begin{bmatrix} 1&2&3\\4&5&6 \end{bmatrix},\quad \boldsymbol{A}_{1,2} = \begin{bmatrix} 0&0 \\ 0&0 \end{bmatrix},\quad \boldsymbol{A}_{2,1} = \begin{bmatrix} 0&0&0 \\ 0&0&0 \end{bmatrix},\quad \boldsymbol{A}_{2,2} = \begin{bmatrix} -1&0 \\ 0&1 \end{bmatrix}
$$

**转置**

先将子块当做元素进行转置运算，然后对子块矩阵转置运算。
$$
\boldsymbol{A}^T = \begin{bmatrix} \boldsymbol{A}_{1,1}^T & \boldsymbol{A}_{2,1}^T \\ \boldsymbol{A}_{1,2}^T & \boldsymbol{A}_{2,2}^T \end{bmatrix}
$$
**标量乘法**
$$
k\boldsymbol{A} = \begin{bmatrix} k\boldsymbol{A}_{1,1} & k\boldsymbol{A}_{1,2} \\ k\boldsymbol{A}_{2,1} & k\boldsymbol{A}_{2,2} \end{bmatrix}
$$
**加减法**

矩阵 $\boldsymbol{A}$ 和 $\boldsymbol{B}$ 形状相同，并采用相同的分块法切割 $\boldsymbol{A}$ 和 $\boldsymbol{B}$。
$$
\boldsymbol{A} + \boldsymbol{B} = \begin{bmatrix} \boldsymbol{A}_{1,1} & \boldsymbol{A}_{1,2} \\ \boldsymbol{A}_{2,1} & \boldsymbol{A}_{2,2} \end{bmatrix} + \begin{bmatrix} \boldsymbol{B}_{1,1} & \boldsymbol{B}_{1,2} \\ \boldsymbol{B}_{2,1} & \boldsymbol{B}_{2,2} \end{bmatrix} = \begin{bmatrix} \boldsymbol{A}_{1,1}+\boldsymbol{B}_{1,1} & \boldsymbol{A}_{1,2}+\boldsymbol{B}_{1,2} \\ \boldsymbol{A}_{2,1}+\boldsymbol{B}_{2,1} & \boldsymbol{A}_{2,2}+\boldsymbol{B}_{2,2} \end{bmatrix}
$$
**矩阵乘法**

矩阵 $\boldsymbol{A}$ 和 $\boldsymbol{B}$ 相乘时，首先保证 $\boldsymbol{A}$ 的列数等于 $\boldsymbol{B}$ 的行数，$\boldsymbol{A}$ 和 $\boldsymbol{B}$ 分块时，保证 $\boldsymbol{A}$ 的每一个子块矩阵的列数分别等于对应位置 $\boldsymbol{B}$​ 的每个子块的行数。
$$
\boldsymbol{A}\boldsymbol{B} = \begin{bmatrix} \boldsymbol{A}_{1,1} & \boldsymbol{A}_{1,2} \\ \boldsymbol{A}_{2,1} & \boldsymbol{A}_{2,2} \end{bmatrix}\begin{bmatrix} \boldsymbol{B}_{1,1} & \boldsymbol{B}_{1,2} \\ \boldsymbol{B}_{2,1} & \boldsymbol{B}_{2,2} \end{bmatrix} = \begin{bmatrix} \boldsymbol{A}_{1,1}\boldsymbol{B}_{1,1}+\boldsymbol{A}_{1,2}\boldsymbol{B}_{2,1} & \boldsymbol{A}_{1,1}\boldsymbol{B}_{1,2}+\boldsymbol{A}_{1,2}\boldsymbol{B}_{2,2} \\ \boldsymbol{A}_{2,1}\boldsymbol{B}_{1,1}+\boldsymbol{A}_{2,2}\boldsymbol{B}_{2,1} & \boldsymbol{A}_{2,1}\boldsymbol{B}_{1,2}+\boldsymbol{A}_{2,2}\boldsymbol{B}_{2,2} \end{bmatrix}
$$

### 1. 矩阵乘法视角：标量积展开

$$
\begin{array}{lcl}
\boldsymbol{A}_{n \times D} = \begin{bmatrix} a_{1,1}&a_{1,2}&\cdots&a_{1,D} \\ a_{2,1}&a_{2,2}&\cdots&a_{2,D} \\ \vdots&\vdots&\ddots&\vdots \\ a_{n,1}&a_{n,2}&\cdots&a_{n,D} \end{bmatrix} = \begin{bmatrix} \boldsymbol{a}^{(1)} \\ \boldsymbol{a}^{(2)} \\ \vdots \\ \boldsymbol{a}^{(n)} \end{bmatrix}, \quad \boldsymbol{a}^{(i)} = \underbrace{\begin{bmatrix} a_1^{(i)}&a_2^{(i)}&\cdots&a_D^{(i)} \end{bmatrix}}_{D个元素}
\\\\
\boldsymbol{B}_{D \times m} = \begin{bmatrix} b_{1,1}&b_{1,2}&\cdots&b_{1,m} \\ b_{2,1}&b_{2,2}&\cdots&b_{2,m} \\ \vdots&\vdots&\ddots&\vdots \\ b_{D,1}&b_{D,2}&\cdots&b_{D,m} \end{bmatrix} = \begin{bmatrix} \boldsymbol{b}_1 & \boldsymbol{b}_2 & \cdots & \boldsymbol{b}_m \end{bmatrix}, \quad \boldsymbol{b}_j = \underbrace{\begin{bmatrix} b_{j,1}\\b_{j,2}\\\vdots\\b_{j,D} \end{bmatrix}}_{D个元素}
\\\\
\boldsymbol{C}_{n \times m} = \boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \begin{bmatrix} \boldsymbol{a}^{(1)} \\ \boldsymbol{a}^{(2)} \\ \vdots \\ \boldsymbol{a}^{(n)} \end{bmatrix}\begin{bmatrix} \boldsymbol{b}_1 & \boldsymbol{b}_2 & \cdots & \boldsymbol{b}_m \end{bmatrix} = \begin{bmatrix} \boldsymbol{a}^{(1)}\boldsymbol{b}_1&\boldsymbol{a}^{(1)}\boldsymbol{b}_2&\cdots&\boldsymbol{a}^{(1)}\boldsymbol{b}_m \\ \boldsymbol{a}^{(2)}\boldsymbol{b}_1&\boldsymbol{a}^{(2)}\boldsymbol{b}_2&\cdots&\boldsymbol{a}^{(2)}\boldsymbol{b}_m \\ \vdots&\vdots&\ddots&\vdots \\ \boldsymbol{a}^{(n)}\boldsymbol{b}_1&\boldsymbol{a}^{(n)}\boldsymbol{b}_2&\cdots&\boldsymbol{a}^{(n)}\boldsymbol{b}_m \end{bmatrix}
\\\\
c_{i,j} = \boldsymbol{a}^{(i)}\boldsymbol{b}_j = (\boldsymbol{a}^{(i)})^T\cdot\boldsymbol{b}_j = a_1^{(i)}b_{j,1} + a_2^{(i)}b_{j,2} + \cdots + a_D^{(i)}b_{j,D}
\end{array}
$$

### 2. 矩阵乘法视角：向量积/外积展开

$$
\begin{array}{lcl}
\boldsymbol{A}_{n \times D} = \begin{bmatrix} a_{1,1}&a_{1,2}&\cdots&a_{1,D} \\ a_{2,1}&a_{2,2}&\cdots&a_{2,D} \\ \vdots&\vdots&\ddots&\vdots \\ a_{n,1}&a_{n,2}&\cdots&a_{n,D} \end{bmatrix} = \begin{bmatrix} \boldsymbol{a}_1 & \boldsymbol{a}_2 & \cdots & \boldsymbol{a}_D \end{bmatrix}, \quad \boldsymbol{a}_i = \underbrace{\begin{bmatrix} a_{i,1}\\a_{i,2}\\\vdots\\a_{i,n} \end{bmatrix}}_{n个元素}
\\\\
\boldsymbol{B}_{D \times m} = \begin{bmatrix} b_{1,1}&b_{1,2}&\cdots&b_{1,m} \\ b_{2,1}&b_{2,2}&\cdots&b_{2,m} \\ \vdots&\vdots&\ddots&\vdots \\ b_{D,1}&b_{D,2}&\cdots&b_{D,m} \end{bmatrix} = \begin{bmatrix} \boldsymbol{b}^{(1)} \\ \boldsymbol{b}^{(2)} \\ \vdots \\ \boldsymbol{b}^{(D)} \end{bmatrix}, \quad \boldsymbol{b}^{(j)} = \underbrace{\begin{bmatrix} b^{(j)}_1&b^{(j)}_2&\cdots&b^{(j)}_m \end{bmatrix}}_{m个元素}
\\\\
\boldsymbol{C}_{n \times m} = \boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \begin{bmatrix} \boldsymbol{a}_1 & \boldsymbol{a}_2 & \cdots & \boldsymbol{a}_D \end{bmatrix} \begin{bmatrix} \boldsymbol{b}^{(1)} \\ \boldsymbol{b}^{(2)} \\ \vdots \\ \boldsymbol{b}^{(D)} \end{bmatrix} = \boldsymbol{a}_1\boldsymbol{b}^{(1)} + \boldsymbol{a}_2\boldsymbol{b}^{(2)} + \cdots + \boldsymbol{a}_D\boldsymbol{b}^{(D)} = \sum\limits_{i=1}^D\boldsymbol{a}_i\boldsymbol{b}^{(i)}
\end{array}
$$

令 $\boldsymbol{C}_i = \boldsymbol{a}_i\boldsymbol{b}^{(i)}$，矩阵 $\boldsymbol{C}$ 相当于 $D$ 个矩阵 $\boldsymbol{C}_i$ 叠加之和
$$
\boldsymbol{C} = \boldsymbol{C}_1 + \boldsymbol{C}_2 + \cdots + \boldsymbol{C}_D = \sum_{i=1}^D\boldsymbol{C}_i
$$
$\boldsymbol{a}_i\boldsymbol{b}^{(i)}$ 矩阵乘法可以写成张量积 $\boldsymbol{a}_i \otimes (\boldsymbol{b}^{(i)})^T$
$$
\boldsymbol{C} = \boldsymbol{a}_1 \otimes \left(\boldsymbol{b}^{(1)}\right)^T + \boldsymbol{a}_2 \otimes \left(\boldsymbol{b}^{(2)}\right)^T + \cdots + \boldsymbol{a}_D \otimes \left(\boldsymbol{b}^{(D)}\right)^T = \sum_{i=1}^D\boldsymbol{a}_i \otimes \left(\boldsymbol{b}^{(i)}\right)^T
$$

### 3. 分块矩阵乘法 $\boldsymbol{A}\boldsymbol{B}$

#### 3.1 $\boldsymbol{B}$ 切成列向量

$$
\boldsymbol{C} = \boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \boldsymbol{A}\begin{bmatrix} \boldsymbol{b}_1 & \boldsymbol{b}_2 & \cdots & \boldsymbol{b}_m \end{bmatrix} = \begin{bmatrix} \boldsymbol{A}\boldsymbol{b}_1 & \boldsymbol{A}\boldsymbol{b}_2 & \cdots & \boldsymbol{A}\boldsymbol{b}_m \end{bmatrix}, \quad \boldsymbol{b}_i = \begin{bmatrix} b_{i,1}\\b_{i,2}\\\vdots\\b_{i,D} \end{bmatrix}
$$

如果存在一下一组矩阵乘法运算：
$$
\boldsymbol{A}\boldsymbol{b}_1 = \boldsymbol{c}_1,\quad \boldsymbol{A}\boldsymbol{b}_2 = \boldsymbol{c}_2,\quad \boldsymbol{A}\boldsymbol{b}_m = \boldsymbol{c}_m
$$
其中，列向量 $\boldsymbol{b}_1,\boldsymbol{b}_2,\ldots,\boldsymbol{b}_m$ 的形状相同，则可以将 $m$ 个等式合成得到：
$$
\boldsymbol{A}\underbrace{\begin{bmatrix} \boldsymbol{b}_1&\boldsymbol{b}_2&\cdots&\boldsymbol{b}_m \end{bmatrix}}_{\boldsymbol{B}} = \underbrace{\begin{bmatrix} \boldsymbol{c}_1&\boldsymbol{c}_2&\cdots&\boldsymbol{c}_m \end{bmatrix}}_{\boldsymbol{C}}
$$

#### 3.2 $\boldsymbol{B}$ 左右切一刀

$$
\boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \boldsymbol{A}\begin{bmatrix}\boldsymbol{B}^{(1)}_{D \times r}&\boldsymbol{B}^{(2)}_{D \times (m-r)}\end{bmatrix} = \begin{bmatrix}\boldsymbol{A}\boldsymbol{B}^{(1)}&\boldsymbol{A}\boldsymbol{B}^{(2)}\end{bmatrix}
$$

#### 3.3 $\boldsymbol{A}$ 切成一组行向量

$$
\boldsymbol{C} = \boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \begin{bmatrix} \boldsymbol{a}^{(1)} \\ \boldsymbol{a}^{(2)} \\ \vdots \\ \boldsymbol{a}^{(n)} \end{bmatrix} \boldsymbol{B} = \begin{bmatrix} \boldsymbol{a}^{(1)}\boldsymbol{B} \\ \boldsymbol{a}^{(2)}\boldsymbol{B} \\ \vdots \\ \boldsymbol{a}^{(n)}\boldsymbol{B} \end{bmatrix}, \quad \boldsymbol{a}^{(i)} = \begin{bmatrix} \boldsymbol{a}^{(i)}_1&\boldsymbol{a}^{(i)}_2&\cdots&\boldsymbol{a}^{(i)}_D \end{bmatrix}
$$

#### 3.4 $\boldsymbol{A}$ 上下切一刀

$$
\boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \begin{bmatrix}\boldsymbol{A}^{(1)}_{k \times D}\\\boldsymbol{A}^{(2)}_{(n-k) \times D}\end{bmatrix}\boldsymbol{B} = \begin{bmatrix}\boldsymbol{A}^{(1)}\boldsymbol{B}\\\boldsymbol{A}^{(2)}\boldsymbol{B}\end{bmatrix}
$$

#### 3.5 $\boldsymbol{A}$ 上下切，$\boldsymbol{B}$ 左右切

$$
\boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \begin{bmatrix}\boldsymbol{A}^{(1)}_{k \times D}\\\boldsymbol{A}^{(2)}_{(n-k) \times D}\end{bmatrix}\begin{bmatrix}\boldsymbol{B}^{(1)}_{D \times r}&\boldsymbol{B}^{(2)}_{D \times (m-r)}\end{bmatrix} = \begin{bmatrix}\left(\boldsymbol{A}^{(1)}\boldsymbol{B}^{(1)}\right)_{k \times r}&\left(\boldsymbol{A}^{(1)}\boldsymbol{B}^{(2)}\right)_{k \times (m-r)}\\\left(\boldsymbol{A}^{(2)}\boldsymbol{B}^{(1)}\right)_{(n-k) \times r}&\left(\boldsymbol{A}^{(2)}\boldsymbol{B}^{(2)}\right)_{(n-k) \times (m-r)}\end{bmatrix}
$$

#### 3.6 $\boldsymbol{A}$ 左右切，$\boldsymbol{B}$ 上下切

$$
\boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} = \begin{bmatrix}\boldsymbol{A}^{(1)}_{n \times s}&\boldsymbol{A}^{(2)}_{n \times (D-s)}\end{bmatrix}\begin{bmatrix}\boldsymbol{B}^{(1)}_{s \times m}\\\boldsymbol{B}^{(2)}_{(D-s) \times m}\end{bmatrix} = \left(\boldsymbol{A}^{(1)}\boldsymbol{B}^{(1)}\right)_{n \times m} + \left(\boldsymbol{A}^{(2)}\boldsymbol{B}^{(2)}\right)_{n \times m}
$$

#### 3.7 $\boldsymbol{A}$ 和 $\boldsymbol{B}$ 都上下左右分块

$$
\begin{align}
\boldsymbol{A}_{n \times D}\boldsymbol{B}_{D \times m} 
&= \begin{bmatrix}
\boldsymbol{A}^{(1,1)}_{k \times s}&\boldsymbol{A}^{(1,2)}_{k \times (D-s)} \\ \boldsymbol{A}^{(2,1)}_{(n-k) \times s}&\boldsymbol{A}^{(2,2)}_{(n-k) \times (D-s)}\end{bmatrix}
\begin{bmatrix}\boldsymbol{B}^{(1,1)}_{s \times r}&\boldsymbol{B}^{(1,2)}_{s \times (m-r)} \\ \boldsymbol{B}^{(2,1)}_{(D-s) \times r}&\boldsymbol{B}^{(2,2)}_{(D-s) \times (m-r)}
\end{bmatrix} \\\nonumber\\
&= \begin{bmatrix}
\left(\boldsymbol{A}^{(1,1)}\boldsymbol{B}^{(1,1)}+\boldsymbol{A}^{(1,2)}\boldsymbol{B}^{(2,1)}\right)_{k \times r}&\left(\boldsymbol{A}^{(1,1)}\boldsymbol{B}^{(1,2)}+\boldsymbol{A}^{(1,2)}\boldsymbol{B}^{(2,2)}\right)_{k \times (m-r)} \\ \left(\boldsymbol{A}^{(2,1)}\boldsymbol{B}^{(1,1)}+\boldsymbol{A}^{(2,2)}\boldsymbol{B}^{(2,1)}\right)_{(n-k) \times r}&\left(\boldsymbol{A}^{(2,1)}\boldsymbol{B}^{(1,2)}+\boldsymbol{A}^{(2,2)}\boldsymbol{B}^{(2,2)}\right)_{(n-k) \times (m-r)}
\end{bmatrix}
\end{align}
$$

### 4. 分块矩阵的逆

将一个 $n$ 阶方阵分割成四个子矩阵 $\boldsymbol{A}、\boldsymbol{B}、\boldsymbol{C}、\boldsymbol{D}$，其中 $\boldsymbol{A}$ 和 $\boldsymbol{D}$ 是方阵，当原矩阵可逆时，原矩阵的逆可以通过子块矩阵运算得到
$$
\begin{bmatrix} \boldsymbol{A}&\boldsymbol{B}\\\boldsymbol{C}&\boldsymbol{D} \end{bmatrix}^{-1} =
\begin{bmatrix}
\left(\boldsymbol{A} - \boldsymbol{B}\boldsymbol{D}^{-1}\boldsymbol{C}\right)^{-1} &
-\left(\boldsymbol{A} - \boldsymbol{B}\boldsymbol{D}^{-1}\boldsymbol{C}\right)^{-1}\boldsymbol{B}\boldsymbol{D}^{-1} \\
-\boldsymbol{D}^{-1}\boldsymbol{C}\left(\boldsymbol{A} - \boldsymbol{B}\boldsymbol{D}^{-1}\boldsymbol{C}\right)^{-1} & 
\boldsymbol{D}^{-1} + \boldsymbol{D}^{-1}\boldsymbol{C}\left(\boldsymbol{A} - \boldsymbol{B}\boldsymbol{D}^{-1}\boldsymbol{C}\right)^{-1}\boldsymbol{B}\boldsymbol{D}^{-1}
\end{bmatrix}
$$
令 $\boldsymbol{H} = \left(\boldsymbol{A} - \boldsymbol{B}\boldsymbol{D}^{-1}\boldsymbol{C}\right)^{-1}$，则
$$
\begin{bmatrix} \boldsymbol{A}&\boldsymbol{B}\\\boldsymbol{C}&\boldsymbol{D} \end{bmatrix}^{-1} =
\begin{bmatrix}
\boldsymbol{H} & -\boldsymbol{H}\boldsymbol{B}\boldsymbol{D}^{-1} \\
-\boldsymbol{D}^{-1}\boldsymbol{C}\boldsymbol{H} & \boldsymbol{D}^{-1} + \boldsymbol{D}^{-1}\boldsymbol{C}\boldsymbol{H}\boldsymbol{B}\boldsymbol{D}^{-1}
\end{bmatrix}
$$

### 5. 克罗内克积

**克罗内克积**也叫矩阵张量积，矩阵 $\boldsymbol{A}$ 的形状为 $n \times m$，$\boldsymbol{B}$ 的形状为 $p \times q$，$\boldsymbol{A} \otimes \boldsymbol{B}$ 的形状为 $np \times mq$。
$$
\boldsymbol{A}_{n \times m} \otimes \boldsymbol{B}_{p \times q} = \begin{bmatrix} a_{1,1}&a_{1,2}&\cdots&a_{1,m} \\ a_{2,1}&a_{2,2}&\cdots&a_{2,m} \\ \vdots&\vdots&\ddots&\vdots \\ a_{n,1}&a_{n,2}&\cdots&a_{n,m} \end{bmatrix} \otimes \boldsymbol{B}_{p \times q} = \begin{bmatrix} a_{1,1}\boldsymbol{B}_{p \times q}&a_{1,2}\boldsymbol{B}_{p \times q}&\cdots&a_{1,m}\boldsymbol{B}_{p \times q} \\ a_{2,1}\boldsymbol{B}_{p \times q}&a_{2,2}\boldsymbol{B}_{p \times q}&\cdots&a_{2,m}\boldsymbol{B}_{p \times q} \\ \vdots&\vdots&\ddots&\vdots \\ a_{n,1}\boldsymbol{B}_{p \times q}&a_{n,2}\boldsymbol{B}_{p \times q}&\cdots&a_{n,m}\boldsymbol{B}_{p \times q} \end{bmatrix}
$$
**克罗内克积常用性质**
$$
\begin{align}
\boldsymbol{A} \otimes (\boldsymbol{B} + \boldsymbol{C}) &= \boldsymbol{A} \otimes \boldsymbol{B} + \boldsymbol{A} \otimes \boldsymbol{C} \nonumber\\
(\boldsymbol{B} + \boldsymbol{C}) \otimes \boldsymbol{A} &= \boldsymbol{B} \otimes \boldsymbol{A} + \boldsymbol{C} \otimes \boldsymbol{A} \nonumber\\
(k\boldsymbol{A}) \otimes \boldsymbol{B} &= \boldsymbol{A} \otimes (k\boldsymbol{B}) = k(\boldsymbol{A} \otimes \boldsymbol{B}) \nonumber\\
(\boldsymbol{A} \otimes \boldsymbol{B}) \otimes \boldsymbol{C} &= \boldsymbol{A} \otimes (\boldsymbol{B} \otimes  \boldsymbol{C}) \nonumber\\
\boldsymbol{A} \otimes \boldsymbol{0} &= \boldsymbol{0} \otimes \boldsymbol{A} = \boldsymbol{0} \nonumber\\
\end{align}
$$
克罗内克积讲究顺序，**一般情况下 $\boldsymbol{A} \otimes \boldsymbol{B} \neq \boldsymbol{B} \otimes \boldsymbol{A}$**。
