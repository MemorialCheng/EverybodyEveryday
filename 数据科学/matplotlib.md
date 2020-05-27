# matplotlib学习笔记
---
# 1 什么是matplotlib?
## 1.1 matplotlib描述
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
## 1.2 matplotlib图形信息设置
### 1.2.1 设置刻度

### 1.2.2 设置中文
matplotlib默认不显示中文，当我们需要在轴刻度中显示中文时需要进行如下设置。
1) 先查看支持的字体：fc-list
  查看支持的中文：fc-list :lang-zh  (冒号前有空格）
2) 如何修改matplotlib的默认字体？
  通过matplotlib.rc可以修改，需要修font代码块；
  ```py
  # 例如
    font = {'family' : 'Microsoft YaHei'
            'weight' : 'bold'
            'size' : 'larger'}
     matplotlib.rc('font', **font)
  ```




