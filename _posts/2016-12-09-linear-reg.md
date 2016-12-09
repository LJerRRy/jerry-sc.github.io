---
layout: post
title: 线性回归
date: 2016-12-08
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Machine Learning
---


### 简单线性回归
当使用均方误差时：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_reg/1.png)
将目标函数使用向量表示：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_reg/2.png)
根据梯度下降算法，求对a的偏微分，并令其等于0：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_reg/3.png)

需要注意的是：**当特征数目大于样本数目的时候，X乘以X的转置不可逆**，则无法使用。后文中，当我们使用岭回归，可以解决此问题。

### 岭回归（Ridge Regression）
所谓岭回归，相当于加了正规化项，也称L2范式项。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_reg/4.png)

岭回归可以有效控制模型的复杂度。当选用较大lambda时，会使得模型参数接近于0，从而使模型变得简单，避免过拟合。
我们可以通过交叉验证方法选取适当的lambda。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_reg/5.png)

### LASSO 
使用L1范式的正规化项。
与Ridge Regression 比较
1. Ridge Regression 纯粹是为了“惩罚”系数，将系数降低，并且Ridge有一个好处是，计算公式简单，容易计算得到一个稳定解
2. LASSO 不只是降低系数，而且会将系数降低到0，使得最后模型变为Sparse，这样带来的好处是，使得计算效率的提升。此外，如果要进行特征选择，推荐使用LASSO，因为只需要选择系数不为0的项就可以。LASSO的缺点是，不再是一个凸优化问题，可能无法找到全局最优点，不稳定。
 ![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_reg/6.png)


### 总结
当使用岭回归或者LASSO模型的时候，除了我们可以有效控制模型的复杂度之外；我们可以通过这些方法进行**特征缩减**，删去没什么特别大作用的参数，从而加快模型训练。
例如，当我们使用岭回归计算得到权重向量后，观察权重向量各个分量的值，相比较而言，绝对值越大的特征分量，对模型越重要，如果要进行特征筛选，我们可以删除权重分量约等于0的特征。