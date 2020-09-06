=====================

记录自己学习贪心学院经典NLP笔记

=====================

# 1 week01
## 1.1 Lecture
### 1.1.1 NLP领域顶会
> 自然语言处理领域: ACL,EMNLP,NAACL

> 机器学习/深度学习领域：ICML,NIPS,UAI,AISTATS;ICLR

> paper网站推荐： https://arxiv.org/

### 1.1.2 NLP常见基础任务
NLP分为自然语言理解NLU,自然语言生成NLG

### 1.1.3 需具备基础
贝叶斯、决策树、SVM、神经网络、强化学习

# 2 week02 多分类文本处理与特征工程
## 2.1 语言模型基础
LM:Unigram,Biggram,N-gram

Smoothing:Laplace Smoothing(Add-one Smoothing, Add-k Smoothing)

预处理

perplexity

autoregressive model: XLNet,ELMo;
autoencoding:Bert


## 2.2 语言模型在拼写纠错(spell correction)中的应用

Distributional

矩阵分解：global，能更好的反应全局信息

Word2vec:Skip-gram,CBOW

Glove:将全局（矩阵分解）和局部（skip-gram）结合

Gaussian Embedding:学习出来的模型设置可信度？

OOV(Out-of-Vocahulang)

FastText:主要解决OOV问题
4-gram

contextualized Embeding

## 2.3 词向量的训练以及使用
## 2.3.1 文本表示方法
基于one-hot、tf-idf 的bag-of-words；

主题模型：LSA（SVD）、pLSA、LDA；

基于词向量的固定表征：word2vec、fastText、glove

基于词向量的动态表征：elmo、GPT、bert。

## 2.3.2 各种词向量的特点
__One-hot:__

> 维度灾难、语义鸿沟

__矩阵分解 (LSA)__

> 利用全局语料特征，但SVD求解计算复杂度大；

__分布式表示 (distributed representation)__

> 基于分布式假设 -- 相同上下文语境的词有似含义

> 基于NNLM/RNNLM的词向量：词向量为副产物，存在效率不高等问题；

> word2vec、fastText：优化效率高，但是基于局部语料；

> glove：基于全局预料，结合了LSA和word2vec的优点；

> ELMo、GPT、bert：动态特征，可以解决一词多义的问题。

## 2.4 词向量的训练
### 2.4.1 word2vec
__word2vec两种模型：__
CBOW:根据中心词周围的词来预测中心词（根据上下文预测中心词）；

Skip-gram:根据中心词来预测周围词（根据中心词预测上下文）。

__经验来说，Skip-gram更好一些__

### 2.4.2 word2vec是如何工作的

1) 输入层：上下文单词的onehot.
2) 所有onehot分别乘以共享的输入权重矩阵W. 
3) 所得的向量相加求平均作为隐层向量, size为1*N.
4) 乘以输出权重矩阵W’ 
5) 得到向量 {1*V} 激活函数处理得到V-dim概率分布，概率最大的index所指示的单词为预测出的中间词（target word）
6) 与true label的onehot做比较，误差越小越好

### 2.4.3 Glove的使用
官方glove，C实现： https://github.com/stanfordnlp/GloVe

Python 实现： https://github.com/maciejkula/glove-python

.安装
pip install glove_python

glove的使用：https://blog.csdn.net/sinat_26917383/article/details/83029140

## 2.5 ELMo、GPT、BERT

特征提取器：elmo采用LSTM进行提取，GPT和bert则采用Transformer进行提取。很多任务表明Transformer特征提取能力强于LSTM，elmo采用1层静态向量+2层LSTM，多层提取能力有限，而GPT和bert中的Transformer可采用多层，并行计算能力强

单/双向语言模型：
GPT采用单向语言模型，ELMo和BERT采用双向语言模型

GPT和BERT都采用Transformer，Transformer是Encoder-Decoder结构，GPT的单向语言模型采用Decoder结构，Decoder的部分见到的都是不完整的句子；BERT的双向语言模型则采用Encoder部分，能够看到完整句子

### 2.5.1 BERT源码阅读
BERT源码阅读
http://fancyerii.github.io/2019/03/09/bert-codes/

BERT源代码
https://github.com/google-research/bert




# 3 week03
## 3.1 工业界模型训练和部署
### 3.1.1 需求分析
### 3.1.2 数据生成
### 3.1.3 模型训练
### 3.1.4 模型验证
准确率(Accuracy):所有样本中预测正确的<br>
Accuracy=(TN+TP)/(TN+FN+TP+FP)

召回率(Recall): 真实值为正样本中预测正确的<br>
Recall=TP/(TP+FN)

精确率(Precision): 预测值为正样本中预测正确的<br>
Precision=TP/(FP+TP)

F1-score=(2*Precision*Recall)/(Precision+Recall)

__根据用户需求为模型选择合适的评价指标：__
理论上F1-score最能体现一个模型的综合性能，但实际应用中，往往选择高精确率或高召回率

__尽量使用真实场景下分布均匀的数据构建一个数据集，用来对模型是否上线进行评估__


### 3.1.5 模型部署
> 服务器端框架：如tfserving
> 模型格式转换：如tf_ckpt to tf_savedmodel
> AI模型服务、接口封装、业务逻辑等模块都运行与容器中，如用k8s进行容器管理

### 3.1.6 实战分享


## 3.2 数据不平衡问题


## 3.3 常见处理方法
欠采样(也叫下采样)
过采样
模型算法
## 评价指标
## 自然语言处理中的数据增强

# 4 week04
## 4.1 pytorch使用
### 4.1.1 pytorch安装

安装pytorch参考博客链接：

[参考链接1](https://blog.csdn.net/weixin_38314865/article/details/100306832?biz_id=102&utm_term=torch%E5%9C%A8pycharm%E9%87%8C%E5%AF%BC%E5%85%A5&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-100306832&spm=1018.2118.3001.4187)  |  [参考链接2](https://blog.csdn.net/weixin_38314865/article/details/102410673)  |  [参考链接2](https://blog.csdn.net/WannaSeaU/article/details/88427010)

__梳理总结__

- 添加清华镜像源
```py
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes
```
- 新建编程环境
```py
conda create -n pytorch_cpu_py36 python=3.6
```
- 安装pytorch  （如果还是慢可删除-c pytorch）
```py
conda install pytorch torchvision cpuonly -c pytorch
```
- 安装好后如果在pycharm使用需要配置新建环境下的python编译器
- 如果在jupyter notebook中使用新建环境，可以参考下面链接

[在jupyter notebook 打开已经建立好了的虚拟环境](https://blog.csdn.net/csdnhuizhu/article/details/105257845?biz_id=102&utm_term=jypyter%E6%89%93%E5%BC%80%E8%87%AA%E5%B7%B1%E6%90%AD%E5%BB%BA%E5%A5%BD%E7%9A%84%E7%8E%AF%E5%A2%83&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-105257845&spm=1018.2118.3001.4187)

## 4.2 pytorch常用操作
### 4.2.1 pytorch的tensor 与 numpy中的ndarray相互转换
- ndarray ——> tensor : __torch.from_numpy(np_arr)__

- tensor ——> ndarray : __tor_arr.numpy()__
```py
import numpy as np
import torch
 
# 创建np array 和 创建 tensor 的方法 类似
x_numpy = np.array([0.1, 0.2, 0.3])
x_torch = torch.tensor([0.1, 0.2, 0.3])
print('======x_numpy, x_torch=========')
print(x_numpy, x_torch)
print()

# Tensor 和 numpy 的转换  不改变原来的
print('======to and from numpy and pytorch======')
print(torch.from_numpy(x_numpy))
print(x_torch.numpy())
print()
print('======x_numpy, x_torch======')
print(x_numpy, x_torch)
print()
```
```py
# 输出结果
======x_numpy, x_torch=========
[0.1 0.2 0.3] tensor([0.1000, 0.2000, 0.3000])

======to and from numpy and pytorch======
tensor([0.1000, 0.2000, 0.3000], dtype=torch.float64)
[0.1 0.2 0.3]

======x_numpy, x_torch======
[0.1 0.2 0.3] tensor([0.1000, 0.2000, 0.3000])
```
- 均匀分布：torch.rand()

- 标准正态分布：torch.randn()

- 离散正态分布：torch.normal()

- 线性间距向量：torch.linespace()

- 求范数norm ,默认二阶范数
```py
print(np.linalg.norm(x_numpy), torch.norm(x_torch))
```
```py
0.37416573867739417 tensor(0.3742)
```

- x.item(),x.data
```py
xx = torch.tensor([5.0])
print(xx.item())
print(xx.data)
```
```py
# 输出结果
5.0
tensor([5.])
```


# 5 week05
## 5.1 RNN
### 5.1.1 RNN的常见应用
- 情感分类
- 诗词生成
- 流畅性评价ppl
- 词槽(slot)填充:如订票










