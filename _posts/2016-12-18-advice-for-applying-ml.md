---
layout: post
title: Advice for Applying Machine Learning
date: 2016-12-18
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Machine Learning
---

最近开始进军Kaggle，认识到了特征工程的重要性，再一次看了Andrew Ng的week 6课程。给我最大感受就是：Ng的课程虽然简单适合入门，但真的包含的信息量特别大，每次看都会有新的体会。

### Learning Curves(学习曲线)
我们可以使用学习曲线来判断某一个学习算法是否处于偏差、方差问题。学习曲线是学习算法的一个很好的合理检验。
> 学习曲线是将训练集误差和验证集误差作为训练集实例数量（m）的函数绘制的图表

#### 高偏差/欠拟合问题

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/advice/high%20bias.jpg)

从上图可以看出，由于模型过于简单，无法拟合训练集，导致随着m的增大，训练误差与验证误差越来越接近，且维持在一个很高的错误率。所以增加训练数据集不会有帮助。

***解决方案：***
- 尝试增加特征数量
- 尝试增阿基多项式特征
- 尝试减少归一化程度lambda

#### 高方差/过拟合

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/advice/high%20variance.jpg)

首先，训练误差依旧是递增的，但是由于模型复杂度很高，随着m的增大，训练误差依旧维持在很小；而对于验证误差来说，当m比较小时，模型过拟合，所以验证误差很大，但这一现象会随着m的增大消失。所以增大训练集误差可以有效的解决高方差问题。当m足够大时，两条曲线也会足够接近，但是此时的error很小。

***解决方案：***
- 获得更多的训练实例
- 尝试减少特征的数量
- 尝试增加归一化程度lambda

### 构建流程

1. 从一个简单的能快速实现的算法开始，实现该算法并用交叉验证集数据测试这个算法
2. 绘制学习曲线，决定是增加更多的数据，或者添加更多特征，还是其他选择
3. 进行误差分析：人工检查交叉验证集中我们算法中产生预测误差的实例，看看这些实例是否有某种规律