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
### 1.xx.3 tf.placeholder 占位符
```py
# 利用placeholder定义输入数据

import tensorflow as tf
# 声明变量：权重，并设定随机种子seed，以保证每次运行的结构一样
w1 = tf.Variable(tf.random_normal((2,3),stddev=1,seed=1))
w2 = tf.Variable(tf.random_normal((3,1),stddev=1,seed=1))

# placeholder定义输入数据
x = tf.placeholder(tf.float32, shape=(3, 2), name="input")

# 定义模型计算
a = tf.matmul(x, w1)
y = tf.matmul(a, w2)

with tf.Session() as sess:
    # 初始化所有变量
    sess.run(tf.global_variables_initializer())
    
    # 输出y
    print(sess.run(y, feed_dict={x: [[0.7,0.9], [0.1, 0.4], [0.5, 0.8]]}))
    
# 使用sigmoid函数将y装换伟0~1之间的数值
y = tf.sigmoid(y)
# 定义损失函数 tf.clip_by_value(y, min, max) 限制y取值范围
cross_entropy = -tf.reduce_mean(
    y_ * tf.log(tf.clip_by_value(y, 1e-10, 1.0))
    + (1-y)*tf.log(tf.clip_by_value(1-y, 1e-10, 1.0)))
# 定义学习率
learning_rate = 0.001
# 定义反向传播算法来优化神经网络参数
train_step = tf.train.AdamOptimizer(lenarning_rate).minimize(cross_entropy)
```
### 1.xx.3 tf.train.exponential_decay指数衰减
该函数可以先使用较大的学习率快速得到一个比较优的解，然后随着迭代的继续逐步减小学习率，使得模型在训练后期更加稳定。  
实现了：
```py
decayed_learning_rate = learning_rate * decay_rate ^ (global_step/decay_steps)
```
函数定义：
```py
def exponential_decay(learning_rate,
                      global_step,
                      decay_steps,
                      decay_rate,
                      staircase=False,
                      name=None):
```
样例：
```py
#coding:utf-8
#设损失函数 loss=(w+1)^2, 令w初值是常数10。反向传播就是求最优w，即求最小loss对应的w值
#使用指数衰减的学习率，在迭代初期得到较高的下降速度，可以在较小的训练轮数下取得更有收敛度。
import tensorflow as tf

LEARNING_RATE_BASE = 0.1 #最初学习率
LEARNING_RATE_DECAY = 0.99 #学习率衰减率
LEARNING_RATE_STEP = 1  #喂入多少轮BATCH_SIZE后，更新一次学习率，一般设为：总样本数/BATCH_SIZE

#运行了几轮BATCH_SIZE的计数器，初值给0, 设为不被训练
global_step = tf.Variable(0, trainable=False)
#定义指数下降学习率
learning_rate = tf.train.exponential_decay(LEARNING_RATE_BASE,
                                           global_step,
                                           LEARNING_RATE_STEP,
                                           LEARNING_RATE_DECAY,
                                           staircase=True)
#定义待优化参数，初值给10
w = tf.Variable(tf.constant(5, dtype=tf.float32))
#定义损失函数loss
loss = tf.square(w+1)
#定义反向传播方法
train_step = tf.train.GradientDescentOptimizer(learning_rate).minimize(loss,
                                                                       global_step=global_step)  # 每运行一次，这里的global_step都+1
#生成会话，训练40轮
with tf.Session() as sess:
    init_op=tf.global_variables_initializer()
    sess.run(init_op)
    for i in range(40):
        sess.run(train_step)
        learning_rate_val = sess.run(learning_rate)
        global_step_val = sess.run(global_step)
        w_val = sess.run(w)
        loss_val = sess.run(loss)
        print ("After %s steps: global_step is %f, w is %f, learning rate is %f, loss is %f" % (i, global_step_val, w_val, learning_rate_val, loss_val))

```

# 2 TensorFlow 2.x


# 3  1.x与2.x的主要不同点
