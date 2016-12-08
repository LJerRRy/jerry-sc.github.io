---
layout: post
title: 线性可分支持向量机
date: 2016-12-07
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Machine Learning
---

### 待解决问题
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/1.png)

当样本线性可分时，我们想要找到一个**鲁棒性最好**的超平面，即拥有最大间隔的超平面。
间隔定义：离超平面最近的点 到 超平面的距离。

### 问题转换
根据点到平面的距离公式，可将上图的式子转化为如下：

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/2.png)

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/3.png)

考虑到w,b的放缩，并不影响最终结果。因此，我们假设样本点到超平面的**函数间隔**最小为1，此时目标函数变为||w||的倒数的最大化。转化后得到下图：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/4.png)

由于样本点到超平面的最小函数间隔都已经为1，所以对于第一个约束条件（所有样本点到超平面的函数间隔都大于0）可以删除。简化后得：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/5.png)

然而由于上式的约束条件中带有最小化操作，使得实际求解变得复杂。我们将约束条件进行放松处理，虽然从直观上来说，约束条件的放松，会使得最终结果不相同，因为取值范围的增大，有更大可能找到更优解；但是如果取得最优值的解仍然满足原始约束条件的话，那么放松处理不会带来任何影响。下面进行证明：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/6.png)

我们将约束条件从原来的（样本点到超平面的函数间隔最小为1）放松为（任何样本点到超平面的距离都大于等于1）。通过反证法，我们可以发现：最优解一定满足原来的约束条件。从而说明，此条件宽松处理，并不影响最终结果。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/7.png)

最后，我们为了后面的方便求解，对目标函数作适当变形，将原来的求最大值转为求最小值，以向量形式体现，并在前面加上系数二分之一。

### 问题求解
以上式子是一个二次规划式，因此可用求解二次规划的工具进行求解。求解之前，需要转为成标准的二次规划式：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/8.png)

### 线性可分支持向量机的解释

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/linear_svm/9.png)
我们可以将此算法与使用正规化避免过拟合的模型比较。由上图可以发现，两者所做的事情其实相同，只不过顺序交换而已，所以线性可分支持向量机的实现过程中已经考虑了避免过拟合现象发生。

### 满足条件
使用上述方法求解的SVM模型必须满足***线性可分***

### Reference
- 台大《机器学习》——林轩田
