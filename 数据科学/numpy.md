**numpy学习笔记**
---

## 1.1 生成数组

```py
import numpy as np
import random

# 生成数组，默认numpy.ndarray类型
print('===========t1==============')
t1 = np.array([1,2,3])
print(t1)
print(type(t1))

# np.arange(star,stop,step=1,dtype=None)
print('===========t2==============')
t2 = np.arange(0,10,2,dtype = 'int8')
print(t2)
print(type(t2)) # 数组的类名
print(t2.dtype) # 元素的类型

# 生成小数 np.round([],weishu)四舍五入保留多少位小数; 
print('===========t3==============')
t3 = np.round([random.random() for i in range(10)],2)
print(t3)
print(t3.dtype)
```

## 1.2生成矩阵


## 1.3 改变矩阵形状 reshape()


## 1.4 转置 t.transpose()

## 1.5 numpy的三元表达式
小于10的设为2，否则为5
np.where(t<10, 2, 5) 

## 1.6 clip 裁剪
小于10的替换为10，大于18的替换为18
t.clip(10, 18)

## 1.7 astype()改变数据类型
改为浮点型
t.astype(float)

## 1.8 数组拼接
将t1和t2进行垂直拼接
np.vstack(t1, t2)


将t1和t2进行水平拼接
np.hstack(t1, t2)

## 1.9 全为0、全为1的矩阵，单位方阵
元素全为1的3*4矩阵
np.ones((3,4))
元素全为0的2*4矩阵
np.zeros((2,4))
对角线为1的5*5的方阵
np.eye(5)

## 1.10 获取最大值、最小值的位置
axis=0表示行与行之间比较即列最大值，axis=1表示列与列之间比较即行最大值

np.argmax(t, axis = 0)
np.argmin(t, axis = 1)

## 1.11 矩阵赋值
表示将矩阵t中为1的元素，改为-1
t[t == 1] = -1

## 1.12 复制
a=b 完全不复制，a和b相互影响；
a = b[:],视图的操作，一种切片，会创建新的对象a，但是a的数据完全由b保管，他们两个的数据变化是一致的，相互影响；
a = b.copy(),复制，a和b互不影响

