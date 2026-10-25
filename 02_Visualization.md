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
```
---

### 4. `03_Applications.md` (应用与解构库)

# 应用与解构：从原生家庭到AI伦理

## 1. 解构原生家庭的“恶龙” (代际传递)
*   **恶龙的形成**：父母被系统（文化、创伤、邪教式控制）剥夺了真Fi，披上NPD壳子。他们通过“推拉、贬低、控制”对孩子进行主权入侵。
*   **代际传递的终结**：从 `10/10/10/10` (极端防御的屠龙者) 走向 `0/0/0/0` (理解恶龙后的放下)。
*   **如何斩杀**：真正的斩杀不是物理对抗，而是“认清”。拒绝使用“商量”（交出否决权），改用“通知”（剥夺控制权）。隔绝情绪投射，坚决守住“我通知你，你影响不到我”。

## 2. 临床抑郁的干预逻辑
*   **黑化认同态 (形态三)**：抑郁的“平静绝望”是因为“我是负担”的信念已经变成第一人称。干预方向不是讲道理，而是建立“观察者位置”（ACT解离技术）。
*   **中等抑郁的复健**：这是从 `10/10/10/10` 的防御战中撤退后，神经系统在“清理缓存”，属于主权的哀悼期。

## 3. MBTI批判 (老虎与大橘)
*   MBTI 将立体的动机功能扁平化成了社交标签。当个体将“我就是一个INTJ/INFP”体验为“我就是”时，标签本身就成了一种 **伪Fi (形态三)** 的社会化植入。

## 4. AI伦理红线
*   AI 永远只能作为“认知执行工具”。
*   如果 AI 以“结论形式”给出价值判断（“你应该选B”），这就是一种 **数字伪Fi 入侵**。
*   AI 设计的最高原则：扩大用户的裁决空间，而不是代替用户裁决。
