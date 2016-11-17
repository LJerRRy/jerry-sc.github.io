---
layout: post
title: Machine Learning in Action 中的Python学习
date: 2016-11-17
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Python
---

### numpy
    array.shape[0] # 获取第一个维度
    tile(x,y) # 重复x共y次，如果y是一个元组，表示将x复制到元组表示的空间中
    sum(a,axis=None)  # 表示对a所有元素求和，如果axis等于0表示对列求和，1表示对行求和
    array.argsort() # 递增排序，返回元素所在的下标
    zeors((row,column)) # 创建一个[row,column]的零矩阵 
> Numpy函数库会自动将字符串型的数值转换为数值型，无需自己处理  

### Matplotlib
    import matplotlib.pyplot as plt
    fig = plt.figure() # 创建图表
    ax = fig.add_subplot(111) # 在大的画布中绘制小画布，111表明:将画布分成1行1列，获取从上到下，从左到右第1块小画布
     ax.scatter(datingDataMat[:,1],datingDataMat[:,2], 15 * array(datingLabels), 15 * array(datingLabels)) # 在画布中绘制散点图， 并指定颜色和大小
     plt.show()

### Python

#### dict
    dict.iteritems() # 遍历时，获取所有key-value对
    dict.iterkeys() 
    dict.itervalues() # 遍历时，获取所有key或value
    dict.get(key, defaultValue) # 如果key不存在，那么插入该key，并返回默认值

#### sorted
    sorted(iterable, key=排序函数, reverse=True) # reverse默认为false，表示从小到大排序
    
#### operator
    operator.itemgetter(dim) # 返回一个函数，该函数用于获取对象的哪些维数据，例如：
	a = [1,2,3]
    b=operator.itemgetter(1) # 定义函数b，获取对象的第一个元素
    b(a) # 得到2，即获取a的第一个元素
    
#### 文件操作
    fr = open('fileName') # open file
    fr.read() # 一次性读取文件所有内容
    fr.read(size) # 反复读取size字节大小的内容
    fr.readline() # 每次读取一行
    fr.readlines() # 一次读取所有内容，返回一个list，元素为每行内容

#### str
    str.strip(char) # 移除字符串头尾的char字符，默认移除空格��除字符串头尾的char字符，默认移除空格