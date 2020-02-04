# Relation-BiLSTM_Attention-Baseline

The-Implementation-of-BiLSTM-Attention-Relation

学习笔记：https://www.jianshu.com/p/9b7c3e4e149e

### 一、写在前面的话
这篇论文发表于ACL2016，和《Relation Classification via Convolutional Deep Neural Network》一样是关系分类领域经典的论文之一，引入了attention+BiLSTM的结构进行关系分类任务，同时不使用位置向量，而是通过Position Indicators来引入实体信息，在不使用任何Lexical-Feature的情况下，可以到达较高的分类准确率，但该研究同样存在创新不足的问题（在关系分类领域这个问题其实蛮严重的，很大一部分的研究都只是简单地迁移了文本分类的模型。现如今随着预训练模型愈发火热，如何做好关系领域的预训练任务将是未来的一个方向）。

### 二、论文笔记

#### 1. 论文整体架构

下图是论文网络的整体架构，基本上就是照搬文本分类中的Attention+BiLSTM，在结构上完全没有为了关系分类这一任务做什么调整。

![](https://upload-images.jianshu.io/upload_images/10798244-3b393914e9faa61f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Attention部分也是较为简单的self-attention，其式子如下所示：

$$M=tanh(H)$$

$$\alpha=softmax(w^TM)$$

$$r=H\alpha^T$$

$$h^*=tanh(r)$$

#### 2. Position Indicators

Position Indicators直接使用标签来表示两个entity的位置，例如在SemEval2010_task中:

###### The <e1> child </e1>  was carefully wrapped and bound into the <e2> cradle </e2> by means of a cord

这个句子，就可以使用  `<e1>`、`<\e1>`、`<e2>`、`<\e2>`  作为四个Indicators。在训练的时候，直接将这四个标签作为普通的word即可突出两个entity。
这个方法也不是该论文首创的，在《Relation classification via recurrent neural network》，已经被提到，其效果如下图所示：

![](https://upload-images.jianshu.io/upload_images/10798244-5cb8748d21bdd2c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3. 实验结果

![](https://upload-images.jianshu.io/upload_images/10798244-61de37dc1de1bea2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在没有使用额外特征的情况下，达到84%的F1 Score，充分说明了Attention机制的作用，但个人在复现的时候并没有达到这个分数，具体过程在能达到差不多的分数后再补充。


### 三、总结

同《Relation Classification via Convolutional Deep Neural Network》大同小异，都是简单地迁移了文本分类中效果较好的模型，相较前者，该论文则迁移地更彻底，创新性不是很足，但同样对于刚踏入这一领域的人来说，这篇论文是入门的必选之一。
