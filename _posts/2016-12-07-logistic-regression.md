---
layout: post
title: Logistic Regression
date: 2016-12-07
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Python
- Machine Learning
---

> 虽然名字中带有“回归”二字，但是其为分类方法。可用于二元分类，或者多元分类。从各种书中，视频中的举例来看，常用于流行病的预测分类。


### 通俗的理解
当我们的分类类别为**0或者1**时，由于线性函数的输出常常大于1或者小于0，使得最小化损失函数的过程中造成误差。因此，引入逻辑回归，逻辑回归的目标函数取值范围为**[0,1]**

### Sigmoid 函数引入
为了使线性函数的输出映射到[0,1]，我们引入Sigmoid函数
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/sigmoid.png)
其图像为：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/sigmoid_graph.png)
可以看到，当z=0时，g(z)=0.5
因此得到预测函数
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/h%28x%29.png)
其含义为：***表示分类结果为1的概率***。由此得到如下两个公式：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/meaning.png)

### 决策边界
我们另h(x)中的自变量x为决策边界，如果x大于0，则说明样本属于正类，否则属于负类。
对于线性边界的情况来说，边界形式如下：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/liner.png)
如果h(x)>0，则此实例为正样本，反之亦然。线性边界与非线性决策边界如下图所示：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/linerboundary.png)

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/nonelinerboundary.png)

### 推导
由以上可知，每个样本出现的概率为：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/prob_every.png)
取似然函数为：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/siran.png)
对数似然为：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/duishusiran.png)
最大似然估计就是求使上式最大值的theta，可以使用梯度上升法求解，求得的theta就是最佳参数。而在Andrew Ng的课程中将此公式变形为：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/bianxing.png)
由于乘了一个负系数，所以变形为求最小值。
对theta的梯度下降可表示为：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/qiudao.png)
简写成：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/tiedai.png)

### 正则化
为防止决策边界产生过拟合现象，在J(theta)式中加上正则项，防止模型过于复杂。
***注意：不要对theta[0]进行正则化处理*** 

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/rl/zhengze.png)

### 多类分类
上面描述的均为二元分类，如果为K元分类，只需保留其中的一类，其余的都作为另一类。训练K个分类器，对于一个新的输入变量x，分别对每一类就行预测，取概率最大的那个类作为分类结果。

### 梯度下降与随机梯度下降比较与实现
参考博文[随机梯度下降（Stochastic gradient descent）和 批量梯度下降（Batch gradient descent ）的公式对比、实现对比](http://blog.csdn.net/lilyth_lilyth/article/details/8973972)

#### 随机梯度下降算法优化
1. 动态调整alpha值，使得alpha随着迭代次数的增多而减小，但永远保证其大于0
2. 在进行梯度下降赋值时，随机选择样本进行梯度更新

以上方法可使得算法尽快收敛，并且减少周期性波动。
**注意：批量梯度下降无需改变alpha值，因为随着迭代进行，梯度一直在减小，越接近全局最优点时，梯度越接近0。相当于在减小alpha值。**

### 关于数据预处理的一些建议
对于Logistic Regression来说，可以将缺省值设为0，然后在梯度更新时做判断，如果某特征值对应值为0，那么该特征的系数不作更新；然而不能任意赋值，因为可能会影响梯度更新。
如果出现类别缺失的情况，可能选择丢弃该样本会是一种更好的选择。因为很难根据特征去判断类别是什么，而且类别的不同会严重影响算法的结果，例如KNN的结果。


### 代码
[Github](https://github.com/jerry-sc/machine_learning_in_action)

### Reference
- 机器学习实战

