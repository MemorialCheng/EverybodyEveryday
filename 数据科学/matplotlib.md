# matplotlib学习笔记
---
# 什么是matplotlib?
matplotlib是最流行的python底层绘图库，主要用作数据可视化。

[matplotlib画廊入口](https://matplotlib.org/)：点击画廊中的图表，即可查看用于生成图表的代码。

```py
# 一个简单的画图例子

from matplotlib import pyplot as plt

x = range(2,26,2)
y = [15,13,7,5,9,3,9,10,15,19,8,10]

# 设置宽高figsize=(10, 6); 图片清晰度dpi = 100
plt.figure(figsize=(10, 6), dpi = 100)

# 画图
plt.plot(x, y)
# 保存图片
plt.savefig('./example1.png')
# 展示图
plt.show
```
