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

```py
    tf.InteractiveSession()  # 交互式环境下该函数可以自动将生成的会话注册为默认会话
    sess = tf.Session()
    with sess.as_default():
        print(result.eval())
    # 等价于下面一句：
    sess = tf.InteractiveSession()
    print(result.eval())
    sess.close()
```


## 1.xx 常用函数
### 1.xx.1 tf.clip_by_value(y, min, max)  
限制y取值范围：y小于min时取min;大于max时取max;中间取y

### 1.xx.2 tf.where;tf.greater
tf.where三个参数，第一个参数为True时选择第二个参数值，为False时选择第三个参数；  
tf.greater()比较函数。

```py
import tensorflow as tf
v1 = tf.constant([1,3,5])
v2 = tf.constant([2,1,6])
with tf.Session() as sess:
    print(tf.greater(v1,v2).eval()) # [False  True False]
    print(tf.where(tf.greater(v1,v2),v1,v2).eval()) # [2 3 6]
```


# 2 TensorFlow 2.x


# 3  1.x与2.x的主要不同点
