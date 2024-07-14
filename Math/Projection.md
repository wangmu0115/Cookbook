## 正交投影 `Orthogonal Projection`

**正交投影**类似正午头顶阳光将物体投影到地面上，光线之间相互平行且与地面**垂直**。

<img src="./_Resources/projection/projection_001.png" style="zoom:30%;" />

$\boldsymbol{x}$ 在 $\boldsymbol{v}$ 方向上的投影是向量 $\boldsymbol{z}$，$\boldsymbol{z}$ 的模就是 $\boldsymbol{x}$ 在$\boldsymbol{v}$ 方向上的**标量投影**。
$$
s = \big\Vert \boldsymbol{z} \big\Vert, \quad \boldsymbol{z} = s\dfrac{\boldsymbol{v}}{\big\Vert \boldsymbol{v} \big\Vert} \\
(\boldsymbol{x} - {\boldsymbol{z}}) \perp \boldsymbol{v} \Rightarrow (\boldsymbol{x} - {\boldsymbol{z}}) \cdot \boldsymbol{v} = (\boldsymbol{x} - {\boldsymbol{z}})^T \boldsymbol{v} = 0 \\
\left(\boldsymbol{x} - s\dfrac{\boldsymbol{v}}{\big\Vert \boldsymbol{v} \big\Vert}\right)^T \boldsymbol{v} = 0 \Rightarrow \\
\left(\boldsymbol{x}^T - s\dfrac{\boldsymbol{v}^T}{\big\Vert \boldsymbol{v} \big\Vert}\right)\boldsymbol{v} = 0 \Rightarrow \\
\boldsymbol{x}^T\boldsymbol{v} - s\dfrac{\boldsymbol{v}^T\boldsymbol{v}}{\big\Vert \boldsymbol{v} \big\Vert} \Rightarrow \\
s = \dfrac{\boldsymbol{x}^T\boldsymbol{v}}{\big\Vert \boldsymbol{v} \big\Vert}
$$
 $\boldsymbol{x}$ 在$\boldsymbol{v}$ 方向上的**标量投影**为：
$$
s = \big\Vert \boldsymbol{z} \big\Vert = \dfrac{\boldsymbol{x}^T\boldsymbol{v}}{\big\Vert \boldsymbol{v} \big\Vert} = \dfrac{\boldsymbol{v}^T\boldsymbol{x}}{\big\Vert \boldsymbol{v} \big\Vert} = \dfrac{\boldsymbol{x} \cdot \boldsymbol{v}}{\big\Vert \boldsymbol{v} \big\Vert} = \dfrac{\boldsymbol{v} \cdot \boldsymbol{x}}{\big\Vert \boldsymbol{v} \big\Vert} = \dfrac{\langle \boldsymbol{x}, \boldsymbol{v}\rangle}{\big\Vert \boldsymbol{v} \big\Vert}
$$
