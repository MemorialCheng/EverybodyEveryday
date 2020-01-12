深度学习（花书）学习笔记（只记录了自己学习需要记录和总结的，并不包含完整的知识点）
# 第二章 线性代数
## 范数（norm）
范数（包括L^p 范数）是将向量映射到非负值的函数。直观上来说，向量x的范数衡量从原点到点x 的距离。用来衡量向量大小。
![image](https://github.com/MemorialCheng/EverybodyEveryday/blob/master/deeplearning/images/norm.png) <br>
当p = 2 时，L2 范数被称为欧几里得范数（Euclidean norm）。它表示从原点出发到向量x 确定的点的欧几里得距离。经常简化表示为∥x∥，略去了下标2。平方L2 范数也经常用来衡量向量的大小，可以简单地通过点积x^⊤x 计算。<br>
但是在很多情况下，平方L2 范数也可能不受欢迎，因为它在原点附近增长得十分缓慢。所以，当机器学习问题中零和非零元素之间的差异非常重要时，通常会使用L1 范数。

## 主成分分析（principal components analysis, PCA）

# 第三章 概率与信息论
## 条件概率

## 期望、方差和协方差
1. __期望（expectation）__ 、 __期望值（expected value）__ ; <br>

2. __方差（variance）__ 衡量的是当我们对x 依据它的概率分布进行采样时，随机变量x 的函数值会呈现多大的差异：<br>
Var(f(x)) = E[(f(x) - E[f(x)])^2] <br>
当方差很小时，f(x) 的值形成的簇比较接近它们的期望值。方差的平方根被称为 __标准差（standard deviation）__

3. __正态分布（normal distribution），也称为高斯分布（Gaussian distribution）__

4. 结构化概率模型

# 第四章 数值计算

上溢，下溢


