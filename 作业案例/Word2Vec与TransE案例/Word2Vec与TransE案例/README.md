# 作业一 Word2Vec&TranE的实现

## 案例简介

Word2Vec是词嵌入的经典模型，它通过词之间的上下文信息来建模词的相似度。TransE是知识表示学习领域的经典模型，它借鉴了Word2Vec的思路，用“头实体+关系=尾实体”这一简单的训练目标取得了惊人的效果。本次任务要求在给定的框架中分别基于Wikipedia和Wikidata数据集实现Word2Vec和TransE，并用具体实例体会词向量和实体/关系向量的含义。

## A Word2Vec实现

在这个部分，你需要基于给定的代码实现Word2Vec，在Wikipedia语料库上进行训练，并在给定的WordSim353数据集上进行测试。

我们提供了一份基于gensim的Word2Vec实现，请同学们阅读代码并在Wikipedia语料库上进行训练。

运行`word2vec.py` 后，模型会保存在`embedding/word2vec_gensim`中，可以使用以下代码加载模型并衡量两个单词的相似性

```python
from gensim.models import Word2Vec
en_wiki_word2vec_model = Word2Vec.load('embeddings/word2vec_gensim')
sim = en_wiki_word2vec_model.similarity('woman', 'man')

```

在WordSim353数据集中，表格的第一、二列是一对单词，第三列中是该单词对的人工打分，分值范围为0-10之间。同学们需要在数据集上用Spearman\[1]相关系数衡量词向量的质量。关于gensim的Word2Vec模型更多接口和用法，请参考\[2]

### 任务

* 运行`word2vec.py`训练Word2Vec模型并保存，在WordSim353上衡量词向量的质量。
* 探究Word2Vec中各个参数对模型的影响，例如词向量维度、窗口大小、最小出现次数。如果wiki数据太大，可以在我们提供的text8语料或你找到的其他语料上进行实验。
* （选做）对Word2Vec模型进行改进，改进的方法可以参考\[3]，包括加入词义信息、字向量和词汇知识等方法。请详细叙述采用的改进方法和实验结果分析。

## B TransE实现

这个部分中，你需要根据提供的代码框架实现TransE，在wikidata数据集训练出实体和关系的向量表示，并对向量进行分析。

### 任务

* 在文件`TransE.py`中，你需要补全`TransE`类中的缺失项，完成TransE模型的训练。需要补全的部分为：
  * `_calc()`：计算给定三元组的得分函数(score function)
  * `loss()`：计算模型的损失函数(loss function)
* 完成TransE的训练，得到实体和关系的向量表示，存储在`entity2vec.txt`和`relation2vec.txt`中。
* 给定头实体Q30，关系P36，最接近的尾实体是哪些？
* 给定头实体Q30，尾实体Q49，最接近的关系是哪些？
* 在 <https://www.wikidata.org/wiki/Q30> 和 <https://www.wikidata.org/wiki/Property:P36> 中查找上述实体和关系的真实含义，你的程序给出了合理的结果吗？请分析原因。
* （选做）改变参数`p_norm`和`margin`，重新训练模型，分析模型的变化。

## 评分标准

请提交代码和实验报告，评分将从代码的正确性、报告的完整性和任务的完成情况等方面综合考量。

## 参考资料

\[1] <https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient>

\[2] <https://radimrehurek.com/gensim/models/word2vec.html>

\[3] A uniﬁed model for word sense representation and disambiguation. in Proceedings of EMNLP, 2014.
