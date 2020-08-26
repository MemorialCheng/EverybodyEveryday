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


# 3 week03
## 3.1 词向量的训练以及使用
## 3.1.1 文本表示方法
基于one-hot、tf-idf 的bag-of-words；

主题模型：LSA（SVD）、pLSA、LDA；

基于词向量的固定表征：word2vec、fastText、glove

基于词向量的动态表征：elmo、GPT、bert。

## 3.1.2 各种词向量的特点
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

## 3.2 词向量的训练
### 3.2.1 word2vec
__word2vec两种模型：__
CBOW:根据中心词周围的词来预测中心词（根据上下文预测中心词）；

Skip-gram:根据中心词来预测周围词（根据中心词预测上下文）。

__经验来说，Skip-gram更好一些__

### 3.2.2 word2vec是如何工作的

1) 输入层：上下文单词的onehot.
2) 所有onehot分别乘以共享的输入权重矩阵W. 
3) 所得的向量相加求平均作为隐层向量, size为1*N.
4) 乘以输出权重矩阵W’ 
5) 得到向量 {1*V} 激活函数处理得到V-dim概率分布，概率最大的index所指示的单词为预测出的中间词（target word）
6) 与true label的onehot做比较，误差越小越好

