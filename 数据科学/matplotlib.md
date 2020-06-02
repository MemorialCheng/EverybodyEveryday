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

# 设置宽高figsize=(10, 6); 图片清晰度dpi = 100; 背景颜色
plt.figure(figsize=(10, 6), dpi = 100, facecolor = 'lightgray')

# 画图
plt.plot(x, y)
# 保存图片
plt.savefig('./example1.png')
# 展示图
plt.show
```
## 1.2 matplotlib图形信息设置
### 1.2.1 设置刻度

plt.xticks()
plt.yticks()
<img src="https://github.com/MemorialCheng/EverybodyEveryday/edit/master/数据科学/images/设置中文.png" width = "500">


### 1.2.2 设置中文
matplotlib默认不显示中文，当我们需要在轴刻度中显示中文时需要进行如下设置。
1) 先查看支持的字体：fc-list

  查看支持的中文：fc-list :lang-zh  (冒号前有空格）
  
2) 如何修改matplotlib的默认字体？

  >通过matplotlib.rc可以修改，需要修font代码块；
  ```py
  # 例如
    font = {'family' : 'Microsoft YaHei'
            'weight' : 'bold'
            'size' : 'larger'}
     matplotlib.rc('font', **font)
  ```
  >通过matplotlib下的font_manager进行设置
  <img src="https://github.com/MemorialCheng/EverybodyEveryday/edit/master/数据科学/images/设置中文.png" width = "500">
  
### 1.2.3 表格添加描述信息
```py
# 设置title
plt.title("温度随时间变化情况", fontsize=14)
# 设置x轴
plt.xlabel("时间")
# 设置y轴
plt.ylabel("温度 单位('C)")
```
如果不能正常显示中文，可以按照1.2.2进行设置
### 1.2.4 添加图例
1）在画图时设置label参数
```py
plt.plot(x, y1, label = "student1")
plt.plot(x, y1, labe2 = "student2")
```
2) 添加图例代码
```py
plt.legend(loc = "upper left")  # 不传参数loc默认自动选择一个合适的位置
```
### 1.2.5 设置线条颜色和风格
在plt.plot()中设置参数
```py
# 颜色，风格，粗细，透明度
color = 'r,
linestyle = '--',
linewidth = '5,
alpha = '0.5'  
```
# 2 绘制图形
## 2.1 绘制散点图
plt.scatter(x, y)

**scatter绘制散点，plot绘制经过点的曲线。**

## 2.2 绘制条形图
```py
plt.bar(x, y, width = 0.3) # 纵向： width表示柱宽

plt.barh(x, y, height = 0.3) # 横向：height表示柱宽

```

## 2.3 绘制多次条形图

例1
假设你知道了列表a中电影分别在2017-09-14(b_14), 2017-09-15(b_15), 2017-09-16(b_16)三天的票房,为了展示列表中电影本身的票房以及同其他电影的数据对比情况,应该如何更加直观的呈现该数据?

a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
b_16 = [15746,312,4497,319]
b_15 = [12357,156,2045,168]
b_14 = [2358,399,2358,362]

```py
from matplotlib import pyplot as plt

a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
b_16 = [15746,312,4497,319]
b_15 = [12357,156,2045,168]
b_14 = [2358,399,2358,362]

bar_width = 0.2

x_14 = list(range(len(a)))
x_15 = [i + bar_width for i in x_14] 
x_16 = [i + bar_width*2 for i in x_14]

# 设置图形大小
plt.figure(figsize = (20, 8), dpi = 80)

plt.bar(x_14, b_14, width = bar_width, label = "September 14th")
plt.bar(x_15, b_15, width = bar_width, label = "September 15th")
plt.bar(x_16, b_16, width = bar_width, label = "September 16th")

# 设置图例
plt.legend()

# 设置刻度
plt.xticks(b_14, a)

plt.show()
```

