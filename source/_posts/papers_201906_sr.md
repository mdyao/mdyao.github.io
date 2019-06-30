---
date: 2019-06-25 20:36:00
title: 论文笔记|近期论文合集——超分辨CVPR2019
urlname: papers_21090626
comments: true
tags:
 - 论文笔记
categories: [文章阅读]
copyright: true
mathjax: true
---




下面是最近读的几篇论文的合集，主要是AAAI2018和CVPR2019。

<!--more-->



###Learning a Single Convolutional Super-Resolution Network for Multiple Degradations

此文发于CVPR2018

题目：Learning a Single Convolutional Super-Resolution Network for Multiple Degradations
作者：Kai Zhang1;2;3, Wangmeng Zuo1, Lei Zhang2
1School of Computer Science and Technology, Harbin Institute of Technology, Harbin, China
2Dept. of Computing, The Hong Kong Polytechnic University, Hong Kong, China
3DAMO Academy, Alibaba Group

作者提出了一种可以handle不同降质模型的网络；维度拉伸策略处理LR图像/模糊和/噪声水平之间的不匹配问题。
先用PCA把模糊和和噪声水平到和LR图像一样大小。
<div align = center>
<img src = ./papers_201906_sr/SRMD_pca.png />
</div>

然后卷积+pixelshuffle恢复HR。

<div align = center>
<img src = ./papers_201906_sr/SRMD_overview.png />
</div>

处理方式较为粗暴。

###Blind Super-Resolution With Iterative Kernel Correction

此文发于CVPR2019

题目：Blind Super-Resolution With Iterative Kernel Correction
作者：Jinjin Gu1∗, Hannan Lu2∗, Wangmeng Zuo2, Chao Dong3
1The School of Science and Engineering, The Chinese University of Hong Kong, Shenzhen
2School of Computer Science and Technology, Harbin Institute of Technology, Harbin, China
3ShenZhen Key Lab of Computer Vision and Pattern Recognition, SIAT-SenseTime Joint Lab,
Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences


urlname: nonlocalGlobal_HSI_denoising_cvpr2019

本文提出一种迭代核相关方法来估计超分辨问题中的模糊核。文章清晰易懂，值得一读。
整体结构如下：

<div align = center>
<img src = ./papers_201906_sr/IKC_overview.png />
</div>

h为估计出的模糊核。






### Image Super-Resolution by Neural Texture Transfer

此文发于CVPR2019，[代码]( https://github.com/ZZUTK/SRNTT)

题目： Image Super-Resolution by Neural Texture Transfer
作者：Zhifei Zhang Zhaowen Wang Zhe Lin Hairong Qi
ADOBE工作。

基本思想是patch match，从Ref图像中找到与LR最像的patch进行引导，不过由于Ref和LR是unpair的，所以匹配和融合都是在特征层面上操作。

网络结构没有看明白的一点是他的不同大小的分辨率是什么意思。如何保证swap取出的特征大小是相同的?
<div align = center>
<img src = ./papers_201906_sr/SRNTT_overview.png />
</div>

下面是纹理转换模块的内部结构，其实就是resnet+upsample.

<div align = center>
<img src = ./papers_201906_sr/SRNTT_NTT.png />
</div>

关于数据集制作，使用了网络搜索的图作为Ref。工作量有，提供了数据集，很棒。

<div align = center>
<img src = ./papers_201906_sr/SRNTTdataset.png />
</div>

至于结果，因为提供了ref图，所以可以从ref图中获取原有的LR图中几乎不可能恢复的信号，如下图的美国国旗，即使是SRGAN也不能从LR中恢复，但是本文由于有Ref，可以从Ref中获取极强的先验恢复美国国旗。（让我想到了华为P30拍月亮）。
<div align = center>
<img src = ./papers_201906_sr/SRNTT_result.png />
</div>

Loss有四个部分：mse，vggLOSS，生成loss，还有作者自己设计的纹理loss(这个应该是借鉴的STYLE tranfer)。

idea很自然，实验也充足。总的来说，不错的一篇工作。



### Feedback Network for Image Super-Resolution

此文发于CVPR2019，[代码](https://github.com/Paper99/SRFBN_CVPR19)

题目： Feedback Network for Image Super-Resolution
作者：Zhen Li1 Jinglei Yang2 Zheng Liu3 Xiaomin Yang1∗ Gwanggil Jeon4 Wei Wu1∗
1Sichuan University, 2University of California, Santa Barbara, 3University of British Columbia,
4Incheon National University


和2017cvpr Feedback networks很像，你懂得。
使用带约束的RNN隐状态作为反馈，课程学习策略进行训练。

所谓curriculum learning 就是先训练简单的数据，再训练复杂的数据。对应到本文，即对每一步的loss分配权重。


本文网络结构，看看2017cvpr  Feedback networks就明白了，作者把原文的ConvLSTM替换为了Feedback Block(FB).

<div align = center>
<img src = ./papers_201906_sr/SRFBN_overview.png />
</div>

这就是作者设计的FB模块：
<div align = center>
<img src = ./papers_201906_sr/FB.png />
</div>


总的来说，本文让我了解了Feedback Network和curriculum learning.Hhhh



### Dual Residual Networks Leveraging the Potential of Paired Operations for Image Restoration

此文发于CVPR2019

题目： Dual Residual Networks Leveraging the Potential of Paired Operations for Image Restoration
作者：Xing Liuy Masanori Suganumayz Zhun Sunz Takayuki Okataniyz
yGraduate School of Information Sciences, Tohoku University zRIKEN Center for AIP

看到文章第一幅图猜想是篇以实验取胜的论文，嗯，可以参考简书:[文章学习40“Dual Residual Networks Leveraging the Potential of Paired Operations for Image Restoration”](https://www.jianshu.com/p/f5b85a4e2b86)

总的来说，网络结构加加减减，实验很足，效果很好。


### “Double-DIP” :Unsupervised Image Decomposition via Coupled Deep-Image-Priors

此文发于CVPR2019

题目：“Double-DIP” :Unsupervised Image Decomposition via Coupled Deep-Image-Priors
作者：：Yossi Gandelsman Assaf Shocher Michal Irani
Dept. of Computer Science and Applied Mathematics
The Weizmann Institute of Science, Israel

这篇文章的基础是CVPR2018 Deep Image Prior.[论文解读](https://zhuanlan.zhihu.com/p/31595192)

没什么好说的，你懂得。
<div align = center>
<img src = ./papers_201906_sr/DIP_overview.png />
</div>



### Unprocessing Images for Learned Raw Denoising

此文发于CVPR2019

题目：Unprocessing Images for Learned Raw Denoising
作者：Tim Brooks1 Ben Mildenhall2 Tianfan Xue1
Jiawen Chen1 Dillon Sharlet1 Jonathan T. Barron1
1Google Research, 2UC Berkeley


提出图像逆处理,将图像根据成像过程转换为调色、gamma调节、白平衡、色域转换等流程，通过直接处理原始图像传感器的原始测量数据来去噪。Darmstadt Noise数据集上得到了14%-38% 的提升和 9×-18×训练加速。




### Learning Parallax Attention for Stereo Image Super-Resolution

此文发于CVPR2019


题目：Learning Parallax Attention for Stereo Image Super-Resolution
作者：Longguang Wang1, Yingqian Wang1, Zhengfa Liang2, Zaiping Lin1, Jungang Yang1, Wei An1, Yulan Guo1∗
1College of Electronic Science and Technology, National University of Defense Technology, China
2National Key Laboratory of Science and Technology on Blind Signal Processing, China


首先使用Res_ASPP提取特征,然后使用PAM(parallax attention module)计算相似性并对齐，最后聚合特征上采样得到SR。
<div align = center>
<img src = ./papers_201906_sr/PASSR_overview.png />
</div>

重点关注其PAM的设计以及loss设计。


### Enhancing the Spatial Resolution of Stereo Images using a Parallax Prior

此文发于CVPR2018

题目：Enhancing the Spatial Resolution of Stereo Images using a Parallax Prior
作者：Daniel S. Jeon Seung-Hwan Baek Inchang Choi Min H. Kim∗
Korea Advanced Institute of Science and Technology (KAIST)



### Reference

