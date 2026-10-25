# 02 四维相空间的可视化编码

本模型拒绝静态标签，采用四维连续变量（X,Y,Z,W）对个体状态进行动力学定位。

## 1. 坐标轴定义
*   **X轴（回避度）**：行为矢量，趋近或撤退。
*   **Y轴（焦虑度）**：能量标量，警报或平静。
*   **Z轴（需求压抑值）**：内核深度，真实表达与假性疏离（决定去激活漂移）。
*   **W轴（安全混乱波动值）**：系统稳定性。趋近于0是死水（稳态），趋近于1是高压电（推拉崩溃）。

## 2. 视觉编码规范（三维空间中表示四维）
在 (x,y,z) 处画一个圆柱：
*   **底面圆心**：(x, y, z)。
*   **圆柱轴向**：统一沿 \(u=(1,1,1)\)，作为“伪W轴”。
*   **圆柱高度**：\(h = k \cdot w\)。正 w 向上延伸（高频震荡），负 w 向下延伸（僵化死寂）。

## 3. 典型个体状态示例
*   **终极安全型**：`(0, 0, 0, 0)`，极低矮的点（主权者的平静）。
*   **恐惧回避型**：`(8, 9, 8, 9)`，在极高压抑和回避处，拔地而起一根剧烈震荡的高柱。
*   **纯粹疏离型**：`(9, 1, 9, -3)`，在极低焦虑处，呈现向下的死寂冰柱。

## 4. Python (Matplotlib) 可视化代码
```python
import matplotlib.pyplot as plt
import numpy as np

fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

def draw_cylinder(ax, x, y, z, w, color='b', alpha=0.7):
    # 伪W轴方向 u
    u = np.array([1, 1, 1]) / np.sqrt(3)
    top = np.array([x, y, z]) + w * u
    
    ax.plot([x, top[0]], [y, top[1]], [z, top[2]], color=color, linewidth=2, alpha=alpha)
    ax.scatter([x], [y], [z], color=color, s=30)
    ax.scatter([top[0]], [top[1]], [top[2]], color=color, s=30)

# 绘制 (3,4,5,6) - 恐惧回避型
draw_cylinder(ax, 3, 4, 5, 6, color='red')
# 绘制 (0,0,0,0) - 终极安全型
draw_cylinder(ax, 0, 0, 0, 0, color='green')

ax.set_xlabel('X (回避度)')
ax.set_ylabel('Y (焦虑度)')
ax.set_zlabel('Z (需求压抑)')
plt.title("Meta-Sovereignty 4D Phase Space")
plt.show()
