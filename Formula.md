## Fomula

#### 1.AUROC

**AUROC（Area Under the Receiver Operating Characteristic curve）是评估二分类模型性能的重要指标，它衡量模型区分正负类样本的能力。**

首先要理解ROC曲线，ROC曲线是以假正率（FPR）为横轴。真正率（TPR）为纵轴绘制的曲线。

假正率(FPR) = FP / (FP + TN)

真正率(TPR/Recall) = TP / (TP+FN)

对于TP、FP这些指标，是否分类正确主要看第一个是T还是F，第二个代表预测的标签

AUROC值是ROC曲线下的面积，范围为[0, 1]，0.5时是随机猜测，1是完美分类，0是完全错误分类

当预测一个二分类问题时，往往会给出置信度，收集一系列的样本，将每个样本的置信度作为阈值进行划分，计算每一个阈值的ROC坐标，然后将其连接起来，就是ROC曲线。

#### 2.BLEU和ROUGE

**BLEU(Bilingual Evaluation Understudy)是用于评估机器翻译质量的指标，衡量机器翻译结果与参考翻译之间的相似度。**

```
BLEU = BP × exp(∑(w_n × log p_n))
```

其中：

- BP (Brevity Penalty) = 1 if c > r, else e^(1-r/c)
- c: 候选翻译长度
- r: 最接近的参考翻译长度
- p_n: n-gram精确度
- w_n: 权重(通常均匀分布)

**ROUGE(Recall-Oriented Understudy for Gisting Evaluation)主要用于评估自动文摘质量，衡量系统生成摘要与参考摘要的重叠程度。**

>  ROUGE主要有以下常见变体：

**ROUGE-N**: 计算n-gram重叠

```
ROUGE-N = ∑(匹配的n-gram数) / ∑(参考摘要中的n-gram数)
```

**ROUGE-L**: 基于最长公共子序列(LCS)

```
ROUGE-L = LCS(X,Y)/m (m是参考摘要长度)
```

**ROUGE-S**: 跳跃二元组(skip-bigram)统计









