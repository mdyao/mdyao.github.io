---
date: 2019-10-28 14:45:00
title: 论文笔记|Neural RGB-D Sensing Depth and Uncertainty from a Video Camera
urlname: papers_20191014
comments: true
tags:
 - 论文笔记
 - 视角合成
categories: [文章阅读]
copyright: true
mathjax: true
---

此文发于CVPR2019, oral, Best Paper Finalist。

题目：Neural RGB→D Sensing: Depth and Uncertainty from a Video Camera
作者：Chao Liu1,2∗ Jinwei Gu1,3∗ Kihwan Kim1 Srinivasa G. Narasimhan2 Jan Kautz1
1NVIDIA 2Carnegie Mellon University 3SenseTime

Extreme view synthesis, Section 3: "Rather than using a single depth estimate for a given pixel, our method accounts for the depth’s probability distribution, which is similar in spirit to the work of Liu et al."


<!--more-->



### 背景

之前引出的论文
<div align = center>
<img src = ./paper_201910_Extreme_View_Synthesis/overview.png />
</div>


### 引出新的要读的论文

Chao Liu, Jinwei Gu, Kihwan Kim, Srinivasa G Narasimhan, and Jan Kautz. Neural RGB ! D sensing: Depth and uncertainty from a video camera. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2019

Local light field fusion: Practical view synthesis with prescriptive sampling guidelines. In ACM Transactions on Graphics (SIGGRAPH), 2019

DeepMVS: Learning multi-view stereopsis. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2018.

High-resolution image synthesis and semantic manipulation with conditional GANs. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pages 8798–8807, 2018. 

Structure-from-motion revisited. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016.

Soft 3D reconstruction for view synthesis. In ACM Transactions on Graphics (SIGGRAPH), 2017. 

DeepStereo: Learning to predict new views from the world’s imagery. In IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016.


