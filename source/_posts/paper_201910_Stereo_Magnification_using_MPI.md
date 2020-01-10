---
date: 2019-10-10 20:36:00
title: 论文笔记|Stereo Magnification_Learning view synthesis using multiplane images
urlname: papers_201910_Stereo_Magnification_Learning_view_synthesis_using_multiplane_images
comments: true
tags:
 - 论文笔记
 - 视角合成
categories: [文章阅读]
copyright: true
mathjax: true
---

此文发于SIGGRAPH2018。

题目：Stereo Magnification: Learning view synthesis using multiplane images
作者：

TINGHUI ZHOU, University of California, Berkeley
RICHARD TUCKER, Google
JOHN FLYNN, Google
GRAHAM FYFFE, Google
NOAH SNAVELY, Google

项目地址:https://people.eecs.berkeley.edu/~tinghuiz/projects/mpi/



<!--more-->

最近需要有任务做视角合成相关的工作,之前对这个领域是完全不了解的.读了几篇文章,记录如下.


### 背景


手机相机的图像质量正逐渐提升,这得益于硬件效果的提升以及HDR,散焦等摄影功能的实现.多摄像头的应用也使得手机有潜力超越传统摄影.

本文探讨的是针对用于立体视觉的双摄手机,如何对获取的双目图像扩大基线(baseline),得到新基线条件下的双目图像,作者将此称为 Stereo Magification.

不同于以往的工作,扩大基线的主要难点在于基线相当于对双目图像进行外插,而以往的基于双目图像进行视角合成的工作多是对双目之间的视角进行插值(内插).本文在外插方面做到了较好的视觉效果,且内插结果也更为流畅合理.

除此之外,本文的另一贡献是使用deep learning的方法,并制作了相关的数据集.


初次接触这个领域,下面从Related Work 中摘取一些内容,以备后记.

#### 传统视角合成方法

视角合成,即将一个或多个视角的场景作为输入,产生多个新视角的图像,是计算机图形学领域的一个经典问题,也是许多基于图像的渲染任务的核心.

multiple (>2) input views:
 - 密集视角内插(light field)
 - 稀疏视角内插

基于立体视觉的视角合成:
 - 三维立体视频转化为多视角视频以用于裸眼多视显示
 - 从微基线立体视觉合成4d光场
 - 从多个小基线视角重建几何

本文关注立体视觉并针对更大的外插.

#### 基于学习的视角合成

利用深度网络强大的表征能力，视角合成问题可以用深度网络进行建模求解．
　- DeepStereo　(cvpr2016,是利用深度学习进行视角合成的影响力较大的一篇工作)
　- LearningBased View Synthesis for Light Field Cameras.(siggraph asia2016)
上述方法只能根据训练输出特定视角的目标场景,本文则通过预测场景的表征,利用这些表征去渲染一个范围内的视角.

其他文章对合成立体图像对,大相机运动,甚至单幅图像生成光场都有了探讨.本文针对更为复杂多样的室内外场景,并可以应用在VR设备上.

#### 视角合成的场景表征
场景的视角合成主要分为两类,一类是对每个输入的视角进行表征,然后利用插值求得目标视角的图;另一种方式是对整个场景进行表征,这种表征多为体素堆积或者"层"的形式.例如layered depth images(LDIs,1998).

与本文最为接近的是Soft 3D Reconstruction for View Synthesis.(SIGGRAPH Asia2017),他们通过显式建模置信度以达到soft的效果(本文通过透明度).

本文的Multiplane Image (MPI) 结合了多层表示和层之间的softness.

### 方法

通过端到端的学习,本文的算法可以直接输出基于MPI的场景表征.并根据这个表征+目标视角的姿态渲染目标视角.

所谓MPI,可以参考[1].

网络结构如图所示

<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/overview.png />
</div>

输入两张图像,reference source and second source,将second source进行shift+stack(就是立体匹配中的cost volume),然后把reference source 堆上去,形成一个BHWx3(D+1)的tensor,作为输入送进网络,与此同时送入网络的还有相机的内参外参.所以网络的输入共有两组量:volume+内外参.

默认情况下,网络输出为一张rgb背景图HW3,D通道个权重图HWD,D通道个alpha图HWD,所以网络的输出参数量为HWx(2D+3),rgb背景图与权重图组合得到rgb,最终得到场景的MPI表征:一系列RGBa图像,这种方式比直接输出rgba(HWx4D)计算量要小.

得到场景的MPI表征后,在测试时根据预期目标视角的相机姿态(外参)+MPI表征就可以通过warp+alpha over compositing[2]得到预期视角的图像了.

优化函数如下图.

<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/objective_function.png />
</div>

L为loss函数,本文采用的是vgg loss.

R是warp+alpha合成操作,$f_\theta$是输入图到MPI场景表征的映射.I1,I2是输入图像,c1,c2是对应的内外参数,ct,It为目标视角的内外参和合成视角的图像.c1=<p1,k1>.pi,ki分别为外参和内参.

具体的warp方式如下,是标准的反向warp.
<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/inverse_homography.png />
</div>


### 数据集制作
本文的另一大贡献在于数据集的制作.作者利用在youtube上扒下来的房地产视频,使用structure from motion 和SLAM的方式获取相机参数,制作了数据集.
数据集的制作:
<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/dataset.png />
</div>


### 结果复现

利用作者提供的model跑了一下代码,这是输出的结果.从alpha图像可以看出对每一个深度平面的估计结果是比较好的,能够明显看出从后向前的深度变化.
MPI_alpha 通道的图像.
<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/MPI_a1.png />
</div>


MPI图像:
<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/MPI_1.png />
</div>

最后的渲染效果:
<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/render_1.png />
</div>

我在另一个数据集上测试了下,效果不怎么好,看起来MPI就没有估计对,猜测是相机的参数没有设置正确.


<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/MPI_a2.png />
</div>


<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/MPI_2.png />
</div>


<div align = center>
<img src = ./paper_201910_Stereo_Magnification_using_MPI/render_2.png />
</div>



### Reference

[1]关于Disney Multiplane camera 的介绍: https://www.bilibili.com/video/av29925039/
https://en.wikipedia.org/wiki/Multiplane_camera

[2]Alpha compositing: https://en.wikipedia.org/wiki/Alpha_compositing

[3]国内视频：http://www.sohu.com/a/258973610_100279313
#### 相关文章：
Pratul P. Srinivasan, Tongzhou Wang, Ashwin Sreelal, Ravi Ramamoorthi, and Ren Ng. 2017. Learning to Synthesize a 4D RGBD Light Field from a Single Image. In ICCV.

Nima Khademi Kalantari, Ting-Chun Wang, and Ravi Ramamoorthi. 2016. LearningBased View Synthesis for Light Field Cameras. In Proc. SIGGRAPH Asia

Eric Penner and Li Zhang. 2017. Soft 3D Reconstruction for View Synthesis. In Proc. SIGGRAPH Asia.

John Flynn, Ivan Neulander, James Philbin, and Noah Snavely. 2016. DeepStereo: Learning to Predict New Views From the World’s Imagery. In CVPR.
