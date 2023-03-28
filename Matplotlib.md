Matplotlib图像分为四层结构

- Canvas(画板)--最底层，导入matplotlib自动存在。
- Figure（画布），建立在canvas之上。
- axes（子图），将figure分成不同块。
- 图表信息（构图元素），添加或修改axes上的图形信息。

pyplot模块提供API创建图形

<img src="/Users/bytedance/Library/Application Support/typora-user-images/image-20230228133517571.png" alt="image-20230228133517571" style="zoom:50%;" />

- 导入模块

  ```python
  import matplotlib.pyplot as plt
  ```

- 创建画布与创建子图

  ```python
  # 创建画布，尺寸为7x8，像素值为80
  fig = plt.figure(figsize=(7, 8), dpi=80)
  # 将画布划分为2x1图形阵，并选择第1张图片
  ax1 = fig.add_subplot(2, 1, 1)
  ```

- 添加画图内容





matplotlib/mpl-data/stylelib/*.mplstyle中 预设风格



rc配置或rc参数

matplotlib/mpl-data/matplotlibrc文件中

`matplotlib.rc()`修改rc参数





散点图

`matplotlib.pyplot.scatter()`函数