---
date: 2019-11-28 23:23:00
title: 论文笔记|Deep Blind Hyperspectral Image Fusion
urlname: papers_201911_Deep_blind_hyperspectral_image_fusion
comments: true
tags:
 - 论文笔记
 - 光谱
categories: [文章阅读]
copyright: true
mathjax: true
---

此文发于ICCV2019。

题目：Deep Blind Hyperspectral Image Fusion
作者：Wu Wang1, Weihong Zeng1, Yue Huang1, Xinghao Ding1∗ , John Paisley2
1Fujian Key Laboratory of Sensing and Computing for Smart City,
School of Information Science and Engineering, Xiamen University, China
2Department of Electrical Engineering, Columbia University, New York, NY, USA



<!--more-->

本文要提出的方法针对的 如何利用高空间分辨率的多光谱图像(HR-MSI)辅助低空间分辨率的高光谱图像(LR-HSI)重建出高空间分辨率的高光谱图像(HR-HSI) 的问题。

首先对光谱图像的观测模型进行建模：

<div align = center>
<img src = ./paper_201911_Deep_blind_hyperspectral_image_fusion/observemodel.png />
</div>

其中，Y是LR-HSI,Z是HR-MSI,X是HR-HSI，B和S均为线性操作子，B代表HR-HSI与点扩散函数之间的卷积(?)，S是下采样操作；R是MSI相机的光谱响应函数。

之前的方法中均假设R、B、S是已知的，所以可以通过优化求解如下形式的目标函数得到X的解。

<div align = center>
<img src = ./paper_201911_Deep_blind_hyperspectral_image_fusion/objectivefunction.png />
</div>

但实际中R、B、S往往是不可得的，所以本文提出了一种基于神经网络迭代进行blind fusion的方式。

作者铺垫了许多话语来解释如何设计迭代式的网络以在正确地恢复HR-HSI的同时估计出降质模型。其中重点是为什么要采用迭代式的网络结构，这里简要说明一下。

本任务是已知Y、Z，求X，这个逆问题的模型参数是未知的。同时，当我们已知X，求Y、Z的时候，因为R、B、S未知，所以这个降质模型的参数也是未知的。所以本文设计了两个网络(g,f)来模拟从X得到YZ和从YZ恢复X的过程。首先初始化得到一个X0，送入网络g得到Y0,Z0,然后与Y，Z求残差，将残差送入f网络，f网络的输出可以看做从Y，Z残差中学习到的X的残差，随后将f网络的输出与X0相加得到X1，重复上述过程，可以得到最终要恢复的Xn。

网络的结构如下，没什么好说的，至于为什么g模型只有一层卷积，作者解释说实验更多的卷积戏能没有得到提升所以这里一层就够用了。

<div align = center>
<img src = ./paper_201911_Deep_blind_hyperspectral_image_fusion/network.png />
</div>


一个疑问，为什么说g网络输出的就是Y，Z，g学习到的是降质过程吗？作者将g的输出可视化出来（如下图），一次来说明说明g的输出就是Y，Z。我总感觉这种解释有些怪异。

<div align = center>
<img src = ./paper_201911_Deep_bilnd_hyperspectral_image_fusion/HR-MSIlearn.png />
</div>

