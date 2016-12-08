---
layout: post
title: Kernel SVM
date: 2016-12-08
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Machine Learning
---

### 问题引入
在上文中，我们发现即使我们引入了对偶形式的SVM，但是我们在计算Q矩阵的时候，仍然需要涉及到w的复杂度，如果w的维度过高，依然存在计算量过大的问题。

### 核函数引入

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/1.png)

考虑以上特征转换，在进行内积计算的时候，优先进行合并，使得最终的计算不依赖于w的复杂度，发现计算复杂度可以下降一个等级。我们称这样的转换为核函数。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/2.png)

有了核函数转换，我们发现在计算b以及最终的分类模型的时候都可以运用核函数，都可以使得计算速度变快。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/3.png)

以上给出了使用 核函数后每一步的时间复杂度。

### 多项式核函数

当然，二次项转换的规则不只有上面这一个，我们可以通过调节系数得到不同的核函数。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/4.png)

上面这些核函数的相同点是：都是映射到二维空间的转换。区别在于不同的核函数会使得几何空间的定义不同，使得间隔的定义不同，最终计算得到的SV支持向量不同，最终的SVM模型也不同。
由此看到，使用核函数的SVM模型时，调参变为调整核函数的选择。
**通常，二维空间转换可以满足需求。**

#### 推广
同样，我们可以使用更高维度的空间转换。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/5.png)

虽然我们进行特征转换后，引入高维度空间，但是通过核函数的帮助，我们无需进行高复杂度计算，并且，由于SVM模型考虑了最大间隔，相当于作了一些正规化处理，避免模型过拟合。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/6.png)

虽然我们有了核函数，可以进行高维空间的转换，但是通常而言，**我们仍然应该首先尝试线性分类**。

### 高斯核函数

![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/7.png)

经过上面的推导，我们可以使用上述高斯核函数，将特征空间映射到任意维度中去。然而，虽然理论上如此，但是伽马选取过大，仍然会导致过拟合。也就是说**SVM仍然会产生过拟合现象，尽管有最大边界保护**。
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/8.png)

**通常不建议使用太大的gama。**

### 核函数比较
*Linear Kernel:*
优点：
- 安全，简单。应该优先选用
- 求解快，可以直接使用原始问题求解，利用市面上特有的工具
- 解释性好，可以计算得到w，从而知道每个特征的权重

缺点：
- 仅限用于线性可分情况下

*线性核函数优先尝试！！！*

---

*Polynomial Kernel:*
优点：
- 相比线性核函数来说，约束少，可以用于非线性情况
- 可以控制映射空间的维度，如果我们已知最优空间维度的话，效果很好。

缺点：
![enter image description here](http://7xt1xs.com1.z0.glb.clouddn.com/ml/kernel_svm/9.png)

当Q太大的时候，计算得到的值可能过大或者过小，对于二次规划的计算工具来说是一个挑战；此外，核函数中包含了3个参数，调参比较复杂。

**通常，当我们心中有个理想的Q时，选用多项式核函数是一个不错的选择。此外，在Q不太大的时候，与线性核函数相比，线性核函数有时候可能有更加好的结果。**

---

*Gaussian Kernel:*
优点：
- 相比另外两个，更加强大
- 由于高斯核函数的取值范围在0到1之间，不会存在计算上的困难
- 只有一个参数，调参容易

缺点：
- 解释性差
- 计算速度相比其他慢
- 太强大，导致过拟合

***此核函数是最常用的核函数，但是必须小心使用。***

### Reference
- 台大《机器学习》——林轩田