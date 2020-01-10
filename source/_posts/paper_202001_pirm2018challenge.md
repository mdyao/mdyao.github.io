---
date: 2020-01-10 :14:00
title: 论文笔记|The 2018 PIRM Challenge on Perceptual Image Super-resolution
urlname: papers_202001_pirm_challenge
comments: true
tags:
 - 论文笔记
categories: [文章阅读]
copyright: true
mathjax: true
---

此文为2018 PIRM perceptual image super resolution challenge的总结报告。

题目：The 2018 PIRM Challenge on Perceptual Image Super-resolution
作者：Yochai Blau1⋆, Roey Mechrez1⋆, Radu Timofte2, Tomer Michaeli1, and Lihi Zelnik-Manor1
1 Technion–Israel Institute of Technology, Haifa, Israel
2 ETH Zurich, Switzerland

<!--more-->


超分问题中的perception-distortion tradeoff已经成为了业界的一个共识，本文总结了PIRM2018 perception sr各队的方法，并验证了竞赛所用感知指标与human-opinion scores(MOS)的相关性，以及其他no-ref 指标与人类感知不相关，另外，竞赛结果也表明在good repceptual quality regime算法还有很大的提升空间。


pirm2018 perception sr 使用4倍bicubic下采样图片进行测试和训练，在100张图上进行最终测试。评测方法上，把perception-distortion平面分按照rmse分为了三个区域，目标是是获得每个区域内最好的perceptual quality.（但最终还是使用了MOS,组织者最后计算了pi和mos之间的相关系数为0.83）

<div align = center>
<img src =./paper_202001_pirm2018challenge/pd_plane.png />
</div>

竞赛选用了Perception Index作为评价指标：$PI=\frac{1}{2}((10-Ma)+NIQE)$。


竞赛结果如下，可以看出不同方法在不同区域的竞赛排名是完全不同的，即没有一种方法是适用所有区域。但这里的*着实是没有明白。

The top 9 submissions in each region. For submissions with a marginal PI difference (up to 0.01), the one with the lower RMSE is ranked higher. Submission with marginal differences in both the PI and RMSE are ranked together (marked by ∗). 

<div align = center>
<img src =./paper_202001_pirm2018challenge/challenge_board.png />
</div>


下面是参赛者提交的结果，提供了一个明显的tradeoff，尤其是在Region1中是最明显的，这表明最大化psnr对perception指标是有害的。而在region3中，rmse的增加对感知指标的提升有限，换句话说，rmse和感知指标并不是那么明显的反比关系，感知指标的提升可以不用以牺牲rmse（或极少牺牲）为代价。

<div align = center>
<img src =./paper_202001_pirm2018challenge/sub_pd_plane.png />
</div>



另外，对于某些图片，所有的算法表现都很好，而某些图片所有算法表现都不理想。区域1中的算法对于结构性较强的图片恢复视觉效果较好，区域3中的算法对于纹理性较强的图片视觉效果好。
这提醒我们可以针对不同类型的图像设计在pd 曲线上不同点的网络。

下面这张图就说明作者提出的pi指标是最吼的！得到了人类的高度通过。

<div align = center>
<img src =./paper_202001_pirm2018challenge/PI_best.png />
</div>


总结各种算法，作者指出了三个趋势，第一个是修改loss，大部分参赛者使用了ganloss，Relativistic gan loss，以及perception loss和Contextual loss，gramloss，甚至还有ms-ssimloss,DCT loss等。第二个是魔改网络结构。第三个就是尝试不同的pd trade-off的方式，如像素融合或者网络融合等。





