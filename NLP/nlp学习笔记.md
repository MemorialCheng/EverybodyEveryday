自然语言处理NLP学习笔记


NLP入门数据集：影评 http://ai.stanford.edu/~amaas/data/sentiment/
AI Challenger 2018 细粒度用户评论情感分析  https://github.com/AIChallenger/AI_Challenger_2018/tree/master/Baselines/sentiment_analysis2018_baseline

金融公司公告新闻分类


问题归总

1.	命名实体识别(NER)，Named Entity Recognition，简称NER。主要用于提取时间、地点、人物、组织机构名。https://www.cnblogs.com/gczr/p/10255338.html
2.	二级文本抽取
3.	spark与Hadoop区别，同时体现出spark在应用在机器学习的优势https://blog.csdn.net/vaychen/article/details/83578527

事件抽取

CCKS 比赛

4、5 抽取   短文本  长文本
网络搜索

图谱
bert
L-bert
https://baijiahao.baidu.com/s?id=1635933482287434194&wfr=spider&for=pc

https://zhuanlan.zhihu.com/p/46652512




事件抽取+知识图谱


如：债务违约  违约方，被违约方，违约金额……
不同事件类型抽取的

天池 k

情感分析

常见的基于情感词典，基于机器学习，深度学习


事件抽取
于BERT-BiLSTM-CRF深度学习网络架构,通过BERT模型来对语料进行文本特征提取,作为BiLSTM网络的输入。BiLSTM克服了传统机器学习的长距离依赖难以获取的缺点,从而对标签序列做出有效的预测。CRF可以通过训练学习得到标签转移概率和约束条件,在最终预测时防止非法标签的出现。实验结果表明,BERT-BiLSTM-CRF模型拥有良好的识别效果



基于Bert细粒度情感分析

Bert模型改进

神经网络CNN,RNN

数据增强

Seq2Seq

Word2Vec

# 1 词向量
## One-hot
容易发生泛化能力弱的情况，过拟合，local泛化能力

## global generation of distributed representation
泛化能力强，global泛化能力

## 词向量分为两个方向
>上线文无关：Skip-Gran,CBOW ...

Skip-Gran用中间词预测两边的，CBOW用两边预测中间的

>上线文有关：ELMo,Bert...

## 负采样 Negative Samping

