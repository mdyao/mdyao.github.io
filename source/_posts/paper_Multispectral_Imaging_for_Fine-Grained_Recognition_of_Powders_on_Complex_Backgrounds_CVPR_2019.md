---
date: 2019-06-24 10:42:00
title: 论文笔记|Multispectral Imaging for Fine-Grained Recognition of Powders on Complex Backgrounds
urlname: HS_FineGrain_cvpr2019
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

题目：Multispectral Imaging for Fine-Grained Recognition of Powders on Complex Backgrounds
作者：Tiancheng Zhi, Bernardo R. Pires, Martial Hebert and Srinivasa G. Narasimhan
Carnegie Mellon University
此文略读，没细看。
<!--more-->


本文使用光谱图像对粉末进行细粒度识别。

粉末状物体，如药品，毒药，炸药，化妆品，食品添加剂，具有无定形，哑光，无颜色，无纹理，易与背景表面混合等特点。针对此挑战，作者提出了首个粉末物体识别的数据集以及对应的方法。

本文提出一种提高识别精度的同时，选择识别谱带的方法，显著缩短了采集时间。


<div align = center>
<img src = ./paper_Multispectral_Imaging_for_Fine-Grained_Recognition_of_Powders_on_Complex_Backgrounds_CVPR_2019/powder_eg.png />
这一大堆粉末名词...头晕</div>


作者使用了三个相机(RGB,近红外NIR,短波红外SWIR)，搭建系统如下：使用了分光镜\*2+反射镜\*1.
<div align = center>
<img src = ./paper_Multispectral_Imaging_for_Fine-Grained_Recognition_of_Powders_on_Complex_Backgrounds_CVPR_2019/system.png />
</div>

使用传统的光散射和吸收理论建模，用最近邻分类器balabla，用deeplab v3+做的分割。更加依赖于物质和光的物理模型，对图像的处理很少，看起来不像是做CV的人做的。





