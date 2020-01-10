---
date: 2019-11-30 21:04:00
title: 论文笔记|Pro-Cam SSfM Projector-Camera System for Structure and Spectral Reflectance From Motion
urlname: papers_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion
comments: true
tags:
 - 论文笔记
 - 光谱
categories: [文章阅读]
copyright: true
mathjax: true
---


写在前面：此文发于ICCV2019。


题目：Pro-Cam SSfM: Projector-Camera System for Structure and Spectral Reflectance from Motion

作者：Chunyu Li, Yusuke Monno, Hironori Hidaka, and Masatoshi Okutomi
Tokyo Institute of Technology, Tokyo, Japan

该工作项目主页：http://www.ok.sc.e.titech.ac.jp/res/PCSSfM/reflectance.html
<!--more-->

本文提出了一种同时对物体进行三维重建和获取光谱反射信息的方法。其中，三维重建是基于的结构光+多视角几何+sfm的方法，获取光谱反射信息是基于多种已知光源求取物体的反射特性。
文章声明三个主要贡献：1、一种多视角自标定的结构光方法。2、提出一种光谱反射估计模型，将物体的3d点和投影仪位置考虑在目标函数内。3、系统原型贡献。

想法直接，思路清晰，感觉工作量不小，光谱效果还可以，但三维重建的效果看起来不是很好，分辨率较低（项目主页提供了重建三维模型的动画）。

方法介绍将分为三个部分：1、数据采集。2、3d重建。3、光谱反射估计。

首先看数据采集部分。整个系统由一个相机和一个投影仪组成，围绕物体进行360度拍摄。具体拍摄方式如下图（b），投影仪在每一个位置上会投射出如下图（a）所示的不同的编码光和均匀光，以分别用于3d重建和光谱反射估计。

<div align = center>
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/data.png"/>
</div>


3d重建部分，包含相机的自标定和目标物体3d点获取。首先是特征相关点的获取，是基于此课题组之前工作（本文3D部分是基于同课题组Chunyu Li, Akihiko Torii, and Masatoshi Okutomi. Robust, precise, and calibration-free shape acquisition with an offthe-shelf camera and projector. Proc. of IEEE Conf. on Consumer Electronics (ICCE), pages 1–6, 2018.的工作）的扩展。 然后是投影仪-相机姿态估计，基于标准的sfm框架，可以得到相机和投影仪的内参姿态以及目标物体的3d点。


最后是光谱重建，首先建立渲染模型，并将其离散表示为矩阵形式。
<div align = center>
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq3.png"/>
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq4.png"/>
渲染模型，r为光谱反射率，l为光源（投影仪）的光谱能量分布，c为相机的光谱响应函数，s为shading factor。k为3d坐标点的索引，n,m分别为投影仪n-th的光照和相机的m-th channel。
</div>

其次建立光谱反射模型，

<div align = center>
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq5.png"/>
反射率可以用基矩阵B和系数向量alpha表示。
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq6.png"/>
所以渲染模型可以表示为eq.6.
</div>

C,L实际中均可获得，所以此时eq.6中只有s，alpha未知，而alpha是待求解的量，所以还要对s进行建模，结果如下。

<div align = center>
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq10.png"/>
</div>


至此，模型已经建立完毕，设置目标函数如下：

<div align = center>
<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq11.png"/>

<img src = "./paper_201911_Pro_Cam_SSfM_Projector_Camera System_for_Structure_and_Spectral_Reflectance_From_Motion/eq13.png"/>
</div>

目标函数也没什么好说的，Eren中的V是归一化项，代表被计算的点，Essm是光谱平滑项。









