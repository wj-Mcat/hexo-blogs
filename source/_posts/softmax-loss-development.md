---
title: softmax-loss-development
date: 2020-07-03 07:43:39
tags: [nlp, deeplearning, softmax]
---

# softmax

> 参考链接：https://zhuanlan.zhihu.com/p/34044634

看到`softmax`大家应该不陌生，这是一个函数，并不是一个`loss`，主要是用于将数据映射到（0，1）概率分布的空间中，也可以说是一种压缩数据空间的一种方法。具体公式如下：

$$
f\left(z_{k}\right)=e^{z_{k}} /\left(\sum_{j} e^{z_{j}}\right)
$$

公式简单，计算高效，也能够转化成凸函数，有利于梯度计算，这也是为什么会被广泛使用的一些原因。

> **⚠️ 注意**: 有些文章中有谈到过 `softmax loss` 这个词组，准确的来讲是不正确的，因为`softmax`只是一个数据空间压缩的方法，并没有进行实质上的损失的计算，更多的是作为一中基础的算法提供给其他算法来计算。
> 
> 参考链接：[cs231n-linear-classify](https://cs231n.github.io/linear-classify/)

`softmax`在实际中的应用面非常广泛，只要与概率有关的基础都可以使用，比如：`cross-entropy-loss`, `Attention`权重的计算等。

# cross entropy loss

交叉熵在**多分类**任务上应用很广泛，效果也是非常好，公式如下：

$$
\operatorname{loss}(x, \text { class })=-\log \left(\frac{\exp (x[\text { class }])}{\sum_{j} \exp (x[j])}\right) = -x[\text { class }]+\log \left(\sum_{j} \exp (x[j])\right)
$$

很明显，上述公式中应用了`softmax`函数，$x$为（0，1）之间的概率分布，$x[class]$为$class$分类上的概率，所以其为[0, len(classes)-1]的整数值。

从另外角度来看，交叉熵是评价`softmax`结果好坏的一种方法。

# Large-Margin Softmax Loss

softmax loss擅长于学习类间的信息，因为它采用了类间竞争机制，它只关心对于正确标签预测概率的准确性，忽略了其他非正确标签的差异，导致学习到的特征比较散。

论文：[Large-Margin Softmax Loss for Convolutional Neural Networks](https://arxiv.org/abs/1612.02295) 提到了一种large-margin softmax loss 的方法，就是为了解决这种问题。公式如下所示：

![](/imgs/2020_07/large-margin-loss-formula.png)

论文中的实验数据为：

![](/imgs/2020_07/large-margin-loss.png)

m是一个控制距离的变量，它越大训练会变得越困难，因为类内不可能无限紧凑。

# soft softmax loss

$$
f\left(z_{k}\right)=e^{z_{k} / T} /\left(\sum_{j} e^{z_{j} / T}\right)
$$


