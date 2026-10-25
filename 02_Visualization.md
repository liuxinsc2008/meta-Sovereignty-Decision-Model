# 四维相空间的视觉编码规范

为了在三维空间中表示四维数据 `(x, y, z, w)`，我们采用**圆柱体视觉编码**。

## 编码规则
1.  **底面圆心 (x, y, z)**：定位个体的基础三维状态。
2.  **圆柱方向 \(u\)**：所有点统一沿固定向量 \(u\)（如 `(1,1,1)` 方向）。
3.  **圆柱高度 \(h = k \cdot w\)**：表示“安全混乱波动值”。
    *   \(w > 0\)：向 \(+u\) 方向延伸（高频震荡）。
    *   \(w < 0\)：向 \(-u\) 方向延伸（僵化死寂）。
    *   \(w = 0\)：无高度（绝对平静的稳态）。

## 示例：Python (Matplotlib) 生成动态心理相图

```python
import matplotlib.pyplot as plt
import numpy as np
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

# 定义画柱体的函数
def draw_cylinder(ax, x, y, z, w, color='b', alpha=0.7):
    # 伪W轴方向 u = (1, 1, 1) 归一化
    u = np.array([1, 1, 1]) / np.sqrt(3)
    # 圆柱高度映射
    height = w 
    # 顶面圆心
    top = np.array([x, y, z]) + height * u
    
    # 画中心轴线
    ax.plot([x, top[0]], [y, top[1]], [z, top[2]], color=color, linewidth=2, alpha=alpha)
    
    # 画底面圆心和顶面圆心的点
    ax.scatter([x], [y], [z], color=color, s=50)
    ax.scatter([top[0]], [top[1]], [top[2]], color=color, s=50)

# 数据点
# (3, 4, 5, 6): 恐惧回避型，极度压抑且极度混乱
draw_cylinder(ax, 3, 4, 5, 6, color='r')
# (0, 0, 0, 0): 终极安全型，主权者平静
draw_cylinder(ax, 0, 0, 0, 0, color='g')
# (8, 9, 8, 9): NPD恶龙，高频震荡的控制源
draw_cylinder(ax, 8, 9, 8, 9, color='purple')

# 设置坐标轴标签
ax.set_xlabel('X (回避度)')
ax.set_ylabel('Y (焦虑度)')
ax.set_zlabel('Z (需求压抑值)')

plt.title("Human Dynamics 4D: Sovereign State Visualization")
plt.show()
