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
