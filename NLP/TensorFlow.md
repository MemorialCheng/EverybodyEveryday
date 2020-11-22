---
TensorFlow学习笔记
---
# 1 TensorFlow 1.x
张量表示数据，计算图搭建神经网络，用会话执行计算图，优化线上权重参数，得到模型。

维数|阶|名字|例子
----|--|----|---
0-D|0|标量(scalar)|s=1
1-D|1|向量(vector)|v=[1,2,3]
2-D|2|矩阵(matrix)|m=[[1,2,3],[1,2,3],[1,2,3]]
n-D|n|张量(tensor)|t=[[[...


## 计算图(Graph):搭建神经网络的计算过程，只搭建，不运算。

### multiply和matmul区别：
multiply对应元素相乘
matmul矩阵相乘
https://www.cnblogs.com/AlvinSui/p/8987707.html

## 1.1 数据类型
tf.float32  
tf.int32  
...
```py
# 常量：
tf.constant()
# 变量：
tf.Variable()
```

```py

# TensorFlow导包警告
解决方法1；
pip install numpy==1.16.0
解决方法2：暴力法
import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'


```




# 2 TensorFlow 2.x


# 3  1.x与2.x的主要不同点
