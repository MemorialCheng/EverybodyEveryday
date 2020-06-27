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
<img src="https://github.com/MemorialCheng/EverybodyEveryday/blob/master/数据科学/images/设置中文.png" width = "500">


### 1.2.2 设置中文
matplotlib默认不显示中文，当我们需要在轴刻度中显示中文时需要进行如下设置。
1) 先查看支持的字体：fc-list

  查看支持的中文：fc-list :lang-zh  (冒号前有空格）
  
2) 如何修改matplotlib的默认字体？

  >通过matplotlib.rc可以修改，需要修font代码块；
  ```py
  # 例如
    font = {'family' : 'Microsoft YaHei',
            'weight' : 'bold',
            'size' : 'larger'}
     matplotlib.rc('font', **font)
  ```
  >通过matplotlib下的font_manager进行设置
  <img src="https://github.com/MemorialCheng/EverybodyEveryday/blob/master/数据科学/images/设置中文.png" width = "500">
  
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
plt.legend(loc = "upper left", prop={'size':6})  # 不传参数loc默认自动选择一个合适的位置, prop={'size':6} 设置属性

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
## 2.1 绘制折线图
plt.plot(x, y)
```py
from matplotlib import pyplot as plt

x = range(2, 26, 2)
y = [15,13,7,5,9,3,9,10,15,19,8,10]

# 设置宽高figsize=(10,6); 图片清晰度dpi=100
plt.figure(figsize=(7, 4), dpi = 100)

# 画图
plt.plot(x, y)

# 保存图片
plt.savefig('./example01.png')

# 展示图
plt.show
```

## 2.2 绘制散点图
plt.scatter(x, y)

**scatter绘制散点，plot绘制经过点的曲线。**

## 2.3 绘制条形图
```py
plt.bar(x, y, width = 0.3) # 纵向： width表示柱宽

plt.barh(x, y, height = 0.3) # 横向：height表示柱宽

```

## 2.4 绘制多次条形图

例1
假设你知道了列表a中电影分别在2017-09-14(b_14), 2017-09-15(b_15), 2017-09-16(b_16)三天的票房,为了展示列表中电影本身的票房以及同其他电影的数据对比情况,应该如何更加直观的呈现该数据?

a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
b_16 = [15746,312,4497,319]
b_15 = [12357,156,2045,168]
b_14 = [2358,399,2358,362]

```py
from matplotlib import pyplot as plt
from matplotlib import font_manager

# 设置中文
# 法1
# font = {'family': 'MicroSoft YaHei',
#         'weight': 'bold'
#        'size': 20}
# matplotlib.rc("font", **font)

# 法2
# my_font = font_manager.FontProperties(fname = "C:\Windows\Fonts\STFANGSO.TTF", size = 20)
my_font = font_manager.FontProperties(fname = "C:\Windows\Fonts\STFANGSO.TTF", size = 20)

a = ["猩球崛起3：终极之战","敦刻尔克","蜘蛛侠：英雄归来","战狼2"]
b_16 = [15746,312,4497,319]
b_15 = [12357,156,2045,168]
b_14 = [2358,399,2358,362]

bar_width = 0.2

x_14 = list(range(len(a)))
x_15 = [i + bar_width for i in x_14] 
x_16 = [i + bar_width*2 for i in x_14]

# 设置图形大小
plt.figure(figsize = (10, 4), dpi = 100)

# 画图
plt.bar(x_14, b_14, width = bar_width, label = "9月14日")
plt.bar(x_15, b_15, width = bar_width, label = "9月15日")
plt.bar(x_16, b_16, width = bar_width, label = "9月16日")

#设置图例并且设置图例的字体及大小
font1 = {'family' : 'STSong',
'weight' : 'normal',
'size'   : 15,
}
plt.legend(prop=font1)

# 设置刻度 , 设置倾斜度rotation= 45，设置字体 fontproperties=my_font
y_loc = list(range(0,16001,2000))
y_labels = list(map(str, y_loc))

plt.xticks(x_15, a, rotation = 45, fontproperties = my_font)
plt.yticks(y_loc, y_labels,fontproperties = my_font)

# 保存图片
plt.savefig('多个柱状图.png')

# 表格添加描述信息
# 设置title
plt.title("9月14-16日电影票房统计", fontproperties = my_font, fontsize=14)
# 设置x轴
plt.xlabel("电影名称", fontproperties = my_font, fontsize = 15)
# 设置y轴
plt.ylabel("票房数量", fontproperties = my_font, fontsize = 15)


# 展示图
plt.show()
```
 <img src="https://github.com/MemorialCheng/EverybodyEveryday/blob/master/数据科学/images/多个柱状图.png" width = "500">
 
## 2.5 绘制直方图

``py
# 绘制直方图 plt.hist(a, num_bins)

from matplotlib import pyplot as plt
from matplotlib import font_manager

# 数据
d = 6
a=[131,  98, 125, 131, 124, 139, 131, 117, 128, 108, 135, 138, 131, 102, 107, 114, 119, 128, 121, 142, 127, 130, 124, 101, 110, 116, 117, 110, 128, 128, 115,  99, 136, 126, 134,  95, 138, 117, 111,78, 132, 124, 113, 150, 110, 117,  86,  95, 144, 105, 126, 130,126, 130, 126, 116, 123, 106, 112, 138, 123,  86, 101,  99, 136,123, 117, 119, 105, 137, 123, 128, 125, 104, 109, 134, 125, 127,105, 120, 107, 129, 116, 108, 132, 103, 136, 118, 102, 120, 114,105, 115, 132, 145, 119, 121, 112, 139, 125, 138, 109, 132, 134,156, 106, 117, 127, 144, 139, 139, 119, 140,  83, 110, 102,123,107, 143, 115, 136, 118, 139, 123, 112, 118, 125, 109, 119, 133,112, 114, 122, 109, 106, 123, 116, 131, 127, 115, 118, 112, 135,115, 146, 137, 116, 103, 144,  83, 123, 111, 110, 111, 100, 154,136, 100, 118, 119, 133, 134, 106, 129, 126, 110, 111, 109, 141,120, 117, 106, 149, 122, 122, 110, 118, 127, 121, 114, 125, 126,114, 140, 103, 130, 141, 117, 106, 114, 121, 114, 133, 137,  92,121, 112, 146,  97, 137, 105,  98, 117, 112,  81,  97, 139, 113,134, 106, 144, 110, 137, 137, 111, 104, 117, 100, 111, 101, 110,105, 129, 137, 112, 120, 113, 133, 112,  83,  94, 146, 133, 101,131, 116, 111,  84, 137, 115, 122, 106, 144, 109, 123, 116, 111,111, 133, 150]
num_bins = (max(a) - min(a))//d # 组距


# 设置图形大小
plt.figure(figsize=(10, 5), dpi = 100)

# 画图   参数normed=True表示百分比形式显示
plt.hist(a, num_bins)

# 设置刻度
plt.xticks(range(min(a), max(a)+d, d))

# 设置网状线
plt.grid()

# 展示图
plt.show()

``
