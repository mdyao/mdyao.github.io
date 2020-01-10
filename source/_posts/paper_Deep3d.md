---
date: 2018-11-07 17:10:00
title: 论文笔记|DEEP3D
urlname: DEEP3D
comments: true
tags:
 - 论文笔记
 - 深度估计
categories: [文章阅读]
copyright: true
mathjax: true
---


写在前面：
Deep3d,由2D到3D视频转换，非常经典的视角重建。[有码](https://github.com/piiswrong/deep3d)。
论文：[Deep3D: Fully Automatic 2D-to-3D Video Conversion with Deep Convolutional Neural Networks](https://arxiv.org/pdf/1612.00496.pdf)，
作者：Junyuan Xie, Ross Girshick, Ali Farhadi
University of Washington
<!--more-->

此文并不是先预测一张深度图，然后用这张深度图通过一个单独的算法去重建缺失的视角，而是在同一神经网络中重新创建端到端的方法来训练它。



### Reference
[Deep3D 中文翻译及阅读笔记](https://blog.csdn.net/Xingyb14/article/details/83384653)
[开源|如何使用CNN将视频从2D到3D进行自动转换（附源代码）](https://www.sohu.com/a/128924237_642762)


