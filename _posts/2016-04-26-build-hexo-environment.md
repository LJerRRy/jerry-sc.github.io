---
layout: post
title: 手把手教你在Ubuntu平台搭建 Github + Hexo 免费博客
date: 2016-04-26
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Hexo
- NexT
- Ubuntu
---


## 前言
昨晚注定是一个悲伤的夜晚，我电脑是 win7 + ubuntu 双系统，然后手贱格式化了ubuntu分区，然后就没有然后了。软件不见了也无所谓，装起来比较简单，最大的损失是我的博客所有配置都没有了，当初搞这个Hexo博客，加上NexT主题的配置，弄了我有两三天时间，现在全没有了，全没有了！！！

虽然博客的内容可以在我的[github](https://github.com/jerry-sc/jerry-sc.github.io)上找到，但那些内容都是通过hexo生成的，无法还原到之前的状态。

既然要重头开始了，那就这里写个教程，方便那些想拥有自己博客的小白做个参考。

## 安装
这里以`Ubuntu`平台为例，所有平台的安装步骤是相同的，如果是其他平台的用户，自己去google或百度下相应的安装即可。

### Git安装
直接一条命令即可
```
sudo sudo apt-get install git
```

### Node.js安装
Node.js的安装有很多种方式，[Hexo的官方文档](https://hexo.io/zh-cn/docs/)建议是用nvm安装，但我尝试了下，不行。所以又参考了一篇文章，使用编译源码安装的方式安装。

#### 在安装前，首先需要配置安g++编译器
```
sudo apt-get install build-essential
```

#### 下载
去https://nodejs.org/en/download/ 官网下载源代码，选择最后一项，Source Code

#### 解压到某一目录，然后进入此目录,依次执行以下3条命令
```
./configure
make
sudo make install
```

#### 执行以下命令，检测是否已经装好node.js
```
node -v
```

## npm安装
```
curl http://npmjs.org/install.sh | sudo sh
```
一条命令即可解决。

## Hexo安装
```
npm install -g hexo
```
到此为止。博客所需要的所有依赖已经安装完毕。如果你不想使用NexT主题，无需阅读下文，去Github找一些hexo主题，进行你的定制吧。

## 创建博客
建立一个目录存放你的博客，然后进入此目录，依次执行
```
hexo init
npm install
```

## NexT主题安装
继续在此目录下执行：
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
此时，主题安装完毕。至于具体的配置，请查看官网介绍。http://theme-next.iissnan.com/








