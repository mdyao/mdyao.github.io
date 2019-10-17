---
date: 2019-06-19 20:49:00
title: 论文笔记|Multispectral and Hyperspectral Image Fusion by MS/HS Fusion Net
urlname: MS_HS_fusion_cvpr2019
comments: true
tags:
 - 论文笔记
 - 光谱
categories: [文章阅读]
copyright: true
mathjax: true
---


写在前面：此文发于CVPR2019，欢迎在文末留言交流。

[//]:，并公布了[代码](https://github.com/JiaRenChang/PSMNet)

题目：Multispectral and Hyperspectral Image Fusion by MS/HS Fusion Net
作者：Qi Xie1, Minghao Zhou1, Qian Zhao1, Deyu Meng1,∗ , Wangmeng Zuo2, Zongben Xu
1Xi’an Jiaotong University; 2Harbin Institute of Technology

<!--more-->

作者提出了一种融合HR-MS和LR-HS的方法，从而生成HR-HS。作者提出的想融合模型考虑了低分辨率图像的观测模型和HR-HS的低秩特性。随后作者设计了一种迭代优化方法，并利用近端梯度法(Proximal Gradient Method, PG)求解此模型。最后作者将以上模型表示成深度网络形式(MS/HS Fusion Net)，通过卷积神经网络学习近端(proximal)操作子和模型参数。


直接恢复高分辨率的高光谱图像是一个病态的逆问题，通常操作是赋予先验。如，1、利用HR-MS训练的字典可以稀疏表示HR-HS的空间信息；2、假设HR-HS的局部空间平滑先验，使用全变分正则将其编码到优化模型中；3、除了探索空间先验，充分利用内部光谱相关性作为先验，使用低秩方法在光谱维度上编码先验以减少光谱畸变。


本文的贡献如下：1本文提出的融合模型不仅考虑了观测模型，并且使用了近似低秩先验结构以减少光谱畸变。2、将迭代策略集成到深度网络框架中。3、实验证明结果有效。

基于机器学习的方法1、使用稀疏编码在HR Patch上学习字典，然后学习从LR到HR的相关系数矩阵。2、稀疏矩阵分解学习LR光谱字典然后使用光谱字典和HRMS图像共同重建HRMS。3、非负矩阵分解。

### 建模

基本模型：
$$Y=XR+N_y\tag{1}$$
$$Z=CX+N_y\tag{2}$$

其中$Y$是HRMS，$X$是HRHS，$R$为MS的光谱响应曲线，$N_y$是HRMS的噪声。
$Z$是LRHS，$C$是线性下采样操作，$N_z$是LRHS的噪声。



理论1：

<div align = center>
<img src = ./paper_Multispectral_and_Hyperspectral_Image_Fusion_by_MSHS_Fusion_Net_CVPR_2019/th1.png />
</div>

又由于$\tilde{Y}=Y-N_y$,所以式(1)可等价于
$$X=YA+\hat{Y}B+N_x \tag{5}$$
其中，$Y$秩为s，$X$秩为r，$[Y,\hat{Y}]$秩为r。

同时存在以下结论：
<div align = center>
<img src = ./paper_Multispectral_and_Hyperspectral_Image_Fusion_by_MSHS_Fusion_Net_CVPR_2019/cl2.png />
</div>

所以式(1)(2)可以表示成
$$Z=C(YA+\hat{Y}B)+N \tag{8}$$

这里Z的秩为r.

【一个疑问，这里的秩只针对的是光谱维度？理论上讲，lr相比较于HR也是降秩了的。但这里Z好像和X的秩是一样的？这种一样是因为$Z=CX$中C是线性下采样？】
<div align = center>
<img src = ./paper_Multispectral_and_Hyperspectral_Image_Fusion_by_MSHS_Fusion_Net_CVPR_2019/fusmodel.png />
</div>

作者解释这种优化可以保持空间信息。

我自己来看，恢复HRHS可以从两个方向去看，一个是从HRMS进行光谱维度上采样，LRHS提供光谱维度的引导信息；另一个是从LRHS进行空间维度上采样，HRMS提供空间维度的引导信息。
两种方式孰优孰劣，直觉上空间维度的信息其实是更难恢复的。

### 近端梯度法（Proximal Gradient Method ，PG）


近端梯度法是一种特殊的梯度下降方法，主要用于求解目标函数不可微的最优化问题。如果目标函数在某些点是不可微的，那么该点的梯度无法求解，传统的梯度下降法也就无法使用。PG算法的思想是，使用临近算子作为近似梯度，进行梯度下降。


<div align = center>
<img src = ./paper_Multispectral_and_Hyperspectral_Image_Fusion_by_MSHS_Fusion_Net_CVPR_2019/opt2net.png />
</div>





### 网络模型

<div align = center>
<img src = ./paper_Multispectral_and_Hyperspectral_Image_Fusion_by_MSHS_Fusion_Net_CVPR_2019/overview.png />
</div>

### Reference

[近端梯度法(Proximal Gradient Method, PG)](https://blog.csdn.net/qq547276542/article/details/78251779)

