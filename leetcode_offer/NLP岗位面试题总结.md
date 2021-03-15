---
总结常见面试题
---

# 算法常见面试题
传统机器学习算法，我列举一些如：
K-近邻，K-Means，朴素贝叶斯，决策树(ID3, C4.5, CART, GBDT, Xgboost, Lightgbm, 随机森林等)，
逻辑回归，最大熵模型，支持向量机SVM，EM算法，隐马尔科夫模型，条件随机场等，
这些传统机器学习算法在面试中经常会被问到原理，或者直接让你公式推导，
推荐阅读的书籍如：李航-统计机器学习，周志华-西瓜书，刘铁岩-分布式机器学习等

深度学习模型的考察通常会结合实际的项目场景进行考察，那掌握模型的原理便是基础，常考查的深度学习模型如:
1、CNN，RNN/GRU/LSTM，Transformer（NLP特征提取）
2、Word2Vec，Glove，FastText，Elmo，Bert，Flair（预训练词向量）
3、CNN，RNN，RCNN，DPCNN，FastText，HAN，Bert（NLP分类模型）
4、GNN，GCN，SGCN（图模型）
深度学习算法复习推荐书籍如：花书-深度学习，python神经网络编程等


## 蚂蚁金服
1. 偏差和方差的区别
2. 介绍一些传统机器学习的分类体系
3. Bert和Elmo在工程中存在的一些Trick

1.挖简历 挖简历 挖简历
2.让描述一下xgboost
3.xgboost和gbdt的区别（说了泰勒展开和正则化，面试官说让我可以回去再查查其他的）
4.分类树准确与否的衡量标准。（我说是entropy，面试官说是准确率精确率召回率，还给我讲了entropy是干啥用的）
5.常见的损失函数
6.LR的损失函数
7.LR支不支持非线性分类(映射到高维)
8.平时如何关注前沿新知识？

## 阿里达摩院
1. CNN 模型中池化层的作用，Max Pooling 是如何反向传递梯度的。
2. 机器学习中正则化做什么的？约束模型参数，防止过拟合。
3. 正则化有 L1 和 L2 正则化区别是什么
4. Transformer 模型架构, Transformer 和 BERT 的位置编码有什么区别
5. Dropout 有什么作用

## 腾讯
1. 介绍过拟合的方法，L1和L2正则的区别，L1正则为什么产生稀疏解
2. dropout方法如何防止过拟合，直接简化网络和dropout的区别
3. 介绍深度模型中的优化函数以及优缺点，介绍实际工程中如何判定过拟合;

1. 多层次分类如何处理
2. 分类文本中如果含有一些关键词扰乱分类结果如何处理，举例
3. 分类文本中如果出现一些新词无法识别导致分类错误如何处理
4. 分词多个分类模型的优缺点如CNN，RNN，FastText以及应用场景

1. rule激活函数如果不加在卷积层之后而是加在最大池化层之后有什么影响
2. 介绍Bert、XLNet、Attention、CNN的原理，
3. python中字典和集合的实现结构
4. 使用Tensorflow实现Softmax函数

## 头条
1. word2vec和FastText模型以及二者的区别
2. FastText算法N-gram作用

## 美团
1. 对于分类问题中的多标签问题/或者多级字标签问题如何解决
2. 写出交叉熵公式并解释为什么要使用交叉熵作为损失函数去评估误差

## 百度
L1/L2正则化及对损失函数造成影响的区别
逻辑回归、GBDT原理以及残差实现细节
GBDT和Xgboost对比
高斯过程原理
吉布斯采样原理

1. 激活函数有哪些以及激活函数如何选用;
2. 介绍Bert、Transformer、Attention原理;
3. 手推SVM

## 滴滴
1. word2vec原理、如何得到词向量
2. fasttext原理
3. GDBT梯度决策提升树、xgboost、lightgbm原理及区别

## 香侬科技
GBDT和xgboost的原理，
为什么常说xgboost可以并行的，
GBDT和xgboost有什么区别;
L1正则化和L2正则化的区别，L1正则为什么产生大量稀疏解;

## 微软
CNN架构理解，梯度消失和梯度爆炸，L1正则和L2正则，损失函数；
手推Bayes公式;
手推CBOW和Skip-gram公式;
维护一个项目上线最主要的是什么，NLP领域都有哪些任务，词向量预训练发展整个过程;

1. 介绍HAN模型原理，Attention机制原理
2、给出QA中的Question和Answer，你能做些什么
3、word2vec中cbow\skip-gram滑动窗口设定大小有何影响
4、有事笔记本电脑跑程序出现内存不够用，但是打开任务管理器发现还有空余内存为什么

1、手推逻辑回归
2、CNN和RNN中反向梯度传播过程，为什么会出现梯度消失或梯度爆炸


# TextCNN
https://www.cnblogs.com/bymo/p/9675654.html

# bert
https://blog.csdn.net/yangdelong/article/details/85070608

# 常见激活函数优缺点：
https://blog.csdn.net/kuweicai/article/details/93926393
https://blog.csdn.net/tyhj_sf/article/details/79932893

# nlp常见选择题：
https://tech.sina.com.cn/csj/2019-12-26/doc-iihnzhfz8434019.shtml


# nlp面试题：
https://blog.csdn.net/qq_17677907/article/details/86448214



# fastText
https://zhuanlan.zhihu.com/p/32965521
https://www.cnblogs.com/ylaoda/p/11339925.html
https://www.cnblogs.com/Fosen/p/12609193.html
