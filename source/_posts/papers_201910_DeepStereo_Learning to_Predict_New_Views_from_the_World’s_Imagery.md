---
date: 2019-10-14 22:14:00
title: 论文笔记|DeepStereo_Learning to Predict New Views from the World’s Imagery
urlname: papers_20191014
comments: true
tags:
 - 论文笔记
 - 视角合成
categories: [文章阅读]
copyright: true
mathjax: true
---

此文发于CVPR2016。

题目：DeepStereo: Learning to Predict New Views from the World’s Imagery
作者：
John Flynn,Zoox∗
Ivan Neulander,Google Inc.
James Philbin,Zoox∗
Noah Snavely,Google Inc.


视频:[DeepStereo](https://tv.sohu.com/v/dXMvMTEwMTYwNzY1LzgwNzEzNDU2LnNodG1s.html)

<!--more-->

最近需要有zz任务做视角合成相关的工作,之前对这个领域是完全不了解的.读了几篇文章,记录如下.


### 背景

<div align = center>
<img src = ./papers_201910_Stereo_Magnification_Learning_view_synthesis_using_multiplane_images/overview.png />
</div>


### Reference

[1]关于Disney Multiplane camera 的介绍: 
https://en.wikipedia.org/wiki/Multiplane_camera

[2]Alpha compositing: https://en.wikipedia.org/wiki/Alpha_compositing

[3]国内视频：http://www.sohu.com/a/258973610_100279313
#### 相关文章：
Pratul P. Srinivasan, Tongzhou Wang, Ashwin Sreelal, Ravi Ramamoorthi, and Ren Ng. 2017. Learning to Synthesize a 4D RGBD Light Field from a Single Image. In ICCV.

Nima Khademi Kalantari, Ting-Chun Wang, and Ravi Ramamoorthi. 2016. LearningBased View Synthesis for Light Field Cameras. In Proc. SIGGRAPH Asia

Eric Penner and Li Zhang. 2017. Soft 3D Reconstruction for View Synthesis. In Proc. SIGGRAPH Asia.

John Flynn, Ivan Neulander, James Philbin, and Noah Snavely. 2016. DeepStereo: Learning to Predict New Views From the World’s Imagery. In CVPR.
