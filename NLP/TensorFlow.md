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

## 1.2 一个完整的神经网络样例
```py
import tensorflow as tf
from numpy.random import RandomState  # 用于生成模拟数据集

# 定义batch大小
batch_size = 8
# 定义神经网络参数
w1 = tf.Variable(tf.random_normal((2, 3), stddev=1, seed=1))
w2 = tf.Variable(tf.random_normal((3, 1), stddev=1, seed=1))
# 定义input,lable数据
x = tf.placeholder(tf.float32, shape=[None, 2], name="x-input")
y_ = tf.placeholder(tf.float32, shape=[None, 1], name="y-input")

# 定义神经网络前向传播过程
a = tf.matmul(x, w1)
y = tf.matmul(a, w2)

# 定义损失函数
y = tf.sigmoid(y)
cross_entropy = -tf.reduce_mean(
    y_*tf.log(tf.clip_by_value(y, 1e-10, 1.0))
    +(1-y_)*tf.log(tf.clip_by_value(1-y, 1e-10, 1.0)))

# 定义学习率和反向传播算法
learning_rate = 0.001
train_step = tf.train.AdamOptimizer(learning_rate).minimize(cross_entropy)

# 通过随机数生成一个模型数据集
rdm = RandomState(1)
dataset_size = 128
X = rdm.rand(dataset_size, 2)
# 定义标签，假设x1+x2 < 1为正样本，其他为负样本
Y = [[int(x1+x2<1)] for (x1,x2) in X]

# 创建会话运行tf程序
with tf.Session() as sess:
    init_op = tf.global_variables_initializer()
    # 初始化变量
    sess.run(init_op)
    print("========训练前网络参数==========")
    print(sess.run(w1))
    print(sess.run(w2))
    
    # 设定训练轮数
    epochs = 5000
    
    for i in range(epochs):
        # 每次取batch_size个样本训练
        start = (i*batch_size)%dataset_size
        end = min(start+batch_size, dataset_size)
        
        # 通过选取的样本训练神经网络并更新参数
        sess.run(train_step, feed_dict={x:X[start:end], y_:Y[start:end]})
        
        # 设置训练1000次后计算所有数据上的交叉熵并输出
        if i % 1000 == 0:
            total_cross_entropy = sess.run(
                cross_entropy, feed_dict={x:X, y_:Y})
            print("After %d training step(s), cross entropy on all data is %g"%(i, total_cross_entropy))
    
    print("========训练后网络参数==========")
    print(sess.run(w1))
    print(sess.run(w2)) 
```
## 1.3 神经网络全模型
```py
import tensorflow as tf
from tensorflow.examples.tutorials.mnist import input_data

# 1.设置输入和输出节点的个数,配置神经网络的参数
INPUT_NODE = 784     # 输入节点
OUTPUT_NODE = 10     # 输出节点
LAYER1_NODE = 500    # 隐藏层数       
                              
BATCH_SIZE = 100     # 每次batch打包的样本个数        

# 模型相关的参数
LEARNING_RATE_BASE = 0.8      
LEARNING_RATE_DECAY = 0.99    
REGULARAZTION_RATE = 0.0001   
TRAINING_STEPS = 5000        
MOVING_AVERAGE_DECAY = 0.99

# 2. 定义辅助函数来计算前向传播结果，使用ReLU做为激活函数
def inference(input_tensor, avg_class, weights1, biases1, weights2, biases2):
    # 不使用滑动平均类
    if avg_class == None:
        layer1 = tf.nn.relu(tf.matmul(input_tensor, weights1) + biases1)
        return tf.matmul(layer1, weights2) + biases2
    else:
        # 使用滑动平均类
        layer1 = tf.nn.relu(tf.matmul(input_tensor, avg_class.average(weights1)) + avg_class.average(biases1))
        return tf.matmul(layer1, avg_class.average(weights2)) + avg_class.average(biases2)

# 3. 定义训练过程
def train(mnist):
    x = tf.placeholder(tf.float32, [None, INPUT_NODE], name='x-input')
    y_ = tf.placeholder(tf.float32, [None, OUTPUT_NODE], name='y-input')
    # 生成隐藏层的参数。
    weights1 = tf.Variable(tf.truncated_normal([INPUT_NODE, LAYER1_NODE], stddev=0.1))
    biases1 = tf.Variable(tf.constant(0.1, shape=[LAYER1_NODE]))
    # 生成输出层的参数。
    weights2 = tf.Variable(tf.truncated_normal([LAYER1_NODE, OUTPUT_NODE], stddev=0.1))
    biases2 = tf.Variable(tf.constant(0.1, shape=[OUTPUT_NODE]))

    # 计算不含滑动平均类的前向传播结果
    y = inference(x, None, weights1, biases1, weights2, biases2)
    
    # 定义训练轮数及相关的滑动平均类 
    global_step = tf.Variable(0, trainable=False)
    variable_averages = tf.train.ExponentialMovingAverage(MOVING_AVERAGE_DECAY, global_step)
    variables_averages_op = variable_averages.apply(tf.trainable_variables())
    average_y = inference(x, variable_averages, weights1, biases1, weights2, biases2)
    
    # 计算交叉熵及其平均值
    cross_entropy = tf.nn.sparse_softmax_cross_entropy_with_logits(logits=y, labels=tf.argmax(y_, 1))
    cross_entropy_mean = tf.reduce_mean(cross_entropy)
    
    # 损失函数的计算
    regularizer = tf.contrib.layers.l2_regularizer(REGULARAZTION_RATE)
    regularaztion = regularizer(weights1) + regularizer(weights2)
    loss = cross_entropy_mean + regularaztion
    
    # 设置指数衰减的学习率。
    learning_rate = tf.train.exponential_decay(
        LEARNING_RATE_BASE,
        global_step,
        mnist.train.num_examples / BATCH_SIZE,
        LEARNING_RATE_DECAY,
        staircase=True)
    
    # 优化损失函数
    train_step = tf.train.GradientDescentOptimizer(learning_rate).minimize(loss, global_step=global_step)
    
    # 反向传播更新参数和更新每一个参数的滑动平均值
    with tf.control_dependencies([train_step, variables_averages_op]):
        train_op = tf.no_op(name='train')

    # 计算正确率
    correct_prediction = tf.equal(tf.argmax(average_y, 1), tf.argmax(y_, 1))
    accuracy = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))
    
    # 初始化会话，并开始训练过程。
    with tf.Session() as sess:
        tf.global_variables_initializer().run()
        validate_feed = {x: mnist.validation.images, y_: mnist.validation.labels}
        test_feed = {x: mnist.test.images, y_: mnist.test.labels}
        
        # 循环的训练神经网络。
        for i in range(TRAINING_STEPS):
            if i % 1000 == 0:
                validate_acc = sess.run(accuracy, feed_dict=validate_feed)
                print("After %d training step(s), validation accuracy using average model is %g " % (i, validate_acc))
            
            xs,ys=mnist.train.next_batch(BATCH_SIZE)
            sess.run(train_op,feed_dict={x:xs,y_:ys})

        test_acc=sess.run(accuracy,feed_dict=test_feed)
        print(("After %d training step(s), test accuracy using average model is %g" %(TRAINING_STEPS, test_acc)))

# 主函数
def main(argv=None):
    mnist = input_data.read_data_sets("../../../datasets/MNIST_data", one_hot=True)
    train(mnist)
if __name__=='__main__':
    main()
```
# 1.4 MNIST最佳实战


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


### 1.xx.4 tf.train.exponential_decay指数衰减
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
### 1.xx.5 tf.reduce_mean 
参考：https://blog.csdn.net/dcrmg/article/details/79797826  
tf.reduce_mean 函数用于计算张量tensor沿着指定的数轴（tensor的某一维度）上的的平均值，主要用作降维或者计算tensor（图像）的平均值。  
```py
reduce_mean(input_tensor,
                axis=None,
                keep_dims=False,
                name=None,
                reduction_indices=None)
```
类似函数还有:
```py
tf.reduce_sum ：计算tensor指定轴方向上的所有元素的累加和;
tf.reduce_max  :  计算tensor指定轴方向上的各个元素的最大值;
tf.reduce_all :  计算tensor指定轴方向上的各个元素的逻辑和（and运算）;
tf.reduce_any:  计算tensor指定轴方向上的各个元素的逻辑或（or运算）;
```
### 1.xx.6 tf.contrib.layers.l2_regularizer(lambda)(w) 正则化
```py
import tensorflow as tf
w = tf.constant([[1.0,2.0],[-3.0,4.0]])
with tf.Session() as sess:
    print(sess.run(tf.contrib.layers.l1_regularizer(.5)(w))) # 5.0
    print(sess.run(tf.contrib.layers.l2_regularizer(.5)(w))) # 7.5
```
### 1.xx.7 tf.expand_dims()
语法：
```py
tf.expand_dims(
    input,
    axis=None,
    name=None,
    dim=None)
```
功能：是给定一个input，在axis轴处给input增加一个为1的维度  
举例：
```py
# 't2' is a tensor of shape [2, 3, 5]
tf.shape(tf.expand_dims(t2, 0))  # [1, 2, 3, 5]
```
因为axis=0所以矩阵的维度变成1*2*3*5。  

同理如果axis=2，矩阵就会变为2*3*1*5。  

0其实代表的第一维度，那么1代表第二维度，2代表第三维度。以此类推  
### 1.xx.8 tf.layers.conv1d和tf.nn.conv1d区别
参考博客：https://blog.csdn.net/u013323018/article/details/90444952  
- tf.nn.conv1d()主要参数value,filters,stride,padding,name
```py
# tf.nn.conv1d
def conv1d(
    value=None,
    filters=None,
    stride=None,
    padding=None,
    use_cudnn_on_gpu=None,
    data_format=None,
    name=None,
    input=None,  # pylint: disable=redefined-builtin
    dilations=None):
```
- tf.layers.conv1d()主要参数inputs,filters,kernel_size,strides,padding,name
```py
# tf.layers.conv1d
tf.layers.conv1d(
inputs,
filters,
kernel_size,
strides=1,
padding='valid',
data_format='channels_last',
dilation_rate=1,
activation=None,
use_bias=True,
kernel_initializer=None,
bias_initializer=tf.zeros_initializer(),
kernel_regularizer=None,
bias_regularizer=None,
activity_regularizer=None,
kernel_constraint=None,
bias_constraint=None,
trainable=True,
name=None,
reuse=None
```
个人小结：tf.nn.conv1d()的filters格式[filter_width, in_channels, out_channels];  
tf.layers.conv1d()的filters过滤器的个数;kernel_size卷积核的大小，卷积核其实应该是一个二维的，这里只需要指定一维，是因为卷积核的第二维与输入的词向量维度是一致的，因为对于句子而言，卷积的移动方向只能是沿着词的方向，即只能在列维度移动。

### 1.xxx.9 tf.nn，tf.layers， tf.contrib模块介绍
https://blog.csdn.net/Yuancccc/article/details/89472133?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control

### 1.xxx.10 tf.summary.xxx函数
- tf.summary.scalar(tags, values, collections=None, name=None)
如：tf.summary.scalar('loss', loss);  
一般在画loss,accuary时会用到这个函数.

- tf.summary.histogram(tags, values, collections=None, name=None) 
 如：tf.summary.histogram('weights',W);  
 一般用来显示训练过程中变量的分布情况,用来显示直方图信息
 
- Summary：所有需要在TensorBoard上展示的统计结果。

- tf.name_scope()：为Graph中的Tensor添加层级，TensorBoard会按照代码指定的层级进行展示，初始状态下只绘制最高层级的效果，点击后可展开层级看到下一层的细节。

- tf.summary.scalar()：添加标量统计结果。

- tf.summary.histogram()：添加任意shape的Tensor，统计这个Tensor的取值分布。

- tf.summary.merge_all()：添加一个操作，代表执行所有summary操作，这样可以避免人工执行每一个summary op。

- tf.summary.FileWrite：用于将Summary写入磁盘，需要制定存储路径logdir，如果传递了Graph对象，则在Graph Visualization会显示Tensor Shape Information。执行summary op后，将返回结果传递给add_summary()方法即可。

### 1.xxx.11 tf.cast()数据类型转换

```py
cast(x, dtype, name=None)
```
- 第一个参数 x:   待转换的数据（张量）
- 第二个参数 dtype： 目标数据类型
- 第三个参数 name： 可选参数，定义操作的名称

参考：https://blog.csdn.net/dcrmg/article/details/79747814



# 2 TensorFlow 2.x


# 3  1.x与2.x的主要不同点
