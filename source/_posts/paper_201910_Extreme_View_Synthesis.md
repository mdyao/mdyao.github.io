---
date: 2019-10-14 22:14:00
title: 论文笔记|Extreme View Synthesis
urlname: papers_201910_Extreme_View_Synthesis
comments: true
tags:
 - 论文笔记
 - 视角合成
categories: [文章阅读]
copyright: true
mathjax: true
---

此文发于CVPR2019。

题目：Extreme View Synthesis
作者：Inchang Choi1;2 Orazio Gallo1 Alejandro Troccoli1 Min H. Kim2 Jan Kautz1
1NVIDIA 2KAIST

继承上一篇的视角合成的工作，这一篇的主要贡献是能够合成更大的基线距离的新视角，不过整体框架与SIGGRAPH2018完全不同。

<!--more-->



### 背景
本文合成新视角的思路遵从传统的基于深度图warp并细化的方案，并进行了一些小的改进。具体来说，首先估计一个深度图的概率体积，然后用此深度概率图warp得到初始的新视角，然后结合输入图中的图像先验与深度的不确定性进行优化以合成更少瑕疵的新视角图像。据说可以达到30x的基线扩展。【但是论文中的有些视觉结果并不是很好】

传统视角合成方案在像素空间插值和在光线空间插值(light field rendering 参考SIGGRAPH1996)。同时，还可以显式结合几何约束，如深度图。但是会出现遮挡和深度估计不准的问题。

作者是以之前的siggraph2018 stereo magnification 作为baseline的。相比于stereo magnification,本文允许更大30x的基线扩展，也允许增加虚拟视角进行旋转等操作。

作者为什么能在更大的基线扩展下做到更好或者comparable的结果呢？私以为除了使用多张深度概率图进行warp之外，更重要的是对合成之后的图像利用原始图像进行了细节增强，将原始图像的信息引入到合成的视角中，类似于ref-sr。不过本文是把从估计深度概率图到warp到最后的细节增强姿态的视角合成。作为一个整体看待的。

下面详细说明作者的思路。

### 算法

<div align = center>
<img src = ./paper_201910_Extreme_View_Synthesis/overview.png />
</div>

输入包含N个视角的图像以及对应的相机位姿，输出为合成的新视角的图像。

算法分为三个部分，对每个视角进行深度估计并将估计到的深度warp到目标视角，根据目标视角的深度合成新视角图像，最后进行细节增强。
#### 估计深度图
对于输入图像的相机参数，作者使用Colmap（Structure-from-motion revisited. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016）进行估计。

已知视角的深度图使用DeepMvs进行估计。对每一个视角估计出深度图(其实是probability volumes)，然后再根据相机位姿把所有已知视角的深度图warp到新视角，得到新视角的深度图。

#### 合成新视角
根据新视角的深度图反向加权warp合成新视角，加权系数与已知视角和新视角的距离有关，越远越小。
根据depth平面从后往前覆盖像素。。。

#### 细节增强

自然而然，可以使用ref-sr，inpainting等方法。

作者截取原视角中的patch来增强新视角中的patch。不过这存在两个疑问：1、如何确定要增强的patch位置？2、如何选定对应的原视角中的patch的位置。

第一个问题猜测是对全图进行操作，不限定有artifacts的部分。第二个问题，作者根据深度图得到patch部分的单应性矩阵，使用单应性矩阵得到warped patch。但这种方式计算量应是很大的,用于细节增强的时间有28s.

【其实另一个方式是使用特征卷积搜索，类似SRNTT】

<div align = center>
<img src = ./paper_201910_Extreme_View_Synthesis/refinet.png />
</div>

### 结果

数据集： 
simulation:
MVS-Synth,CVPR2018
Stereo Magnification SIGGRAPH2018

real-scene: like Stereo magnification

<div align = center>
<img src = ./paper_201910_Extreme_View_Synthesis/withsoft3d.png />
</div>

右边作者的结果明显不如左边soft3d(siggraph2017)的结果，但这个对比设定很奇怪，没有控制变量：soft3d使用所有的视角而作者只使用了 两个视角。

<div align = center>
<img src = ./paper_201910_Extreme_View_Synthesis/result1.png />
</div>

以及这个场景，作者在做摄像头逐渐拉近的操作，但是广告牌上的人脸却因为镜头拉近而扭曲消失，按说直接做插值放大也不会出现这种结果啊。

当然，其他作者展示的场景效果还是可以的。

### 引出新的要读的论文

Chao Liu, Jinwei Gu, Kihwan Kim, Srinivasa G Narasimhan, and Jan Kautz. Neural RGB ! D sensing: Depth and uncertainty from a video camera. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2019

Local light field fusion: Practical view synthesis with prescriptive sampling guidelines. In ACM Transactions on Graphics (SIGGRAPH), 2019

DeepMVS: Learning multi-view stereopsis. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2018.

High-resolution image synthesis and semantic manipulation with conditional GANs. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pages 8798–8807, 2018. 

Structure-from-motion revisited. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016.

Soft 3D reconstruction for view synthesis. In ACM Transactions on Graphics (SIGGRAPH), 2017. 

DeepStereo: Learning to predict new views from the world’s imagery. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016.


