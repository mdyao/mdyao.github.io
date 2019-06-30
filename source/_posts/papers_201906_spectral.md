---
date: 2019-06-25 20:36:00
title: 论文笔记|近期论文合集
urlname: papers_21090625
comments: true
tags:
 - 论文笔记
categories: [文章阅读]
copyright: true
mathjax: true
---




下面是最近读的几篇论文的合集，主要是AAAI2018和CVPR2019。

<!--more-->



### Meta-SR
此文发于CVPR2019

题目：Meta-SR: A Magnification-Arbitrary Network for Super-Resolution
作者：Xuecai Hu∗1,2 , Haoyuan Mu∗ 4, Xiangyu Zhang3, Zilei Wang1, Tieniu Tan1,2, Jian Sun3
1 University of Science and Technology of China
2 Center for Research on Intelligent Perception and Computing, NLPR, CASIA
3 Megvii Inc (Face++) 4 Tsinghua University

urlname:meta_sr_cvpr2019



使用meta-learning解决单模型连续尺度超分辨的的问题。
主要贡献是提出一个meta upscale 模块，根据放缩尺度r学习了不同的卷积核，但是具体如何实现上采样操作，矩阵乘法如何实现的没有搞懂，需要看代码。

网络结构如下图所示：
<div align = center>
<img src = ./papers_201906_spectral/metasr_overview.png />
</div>



### MSI fine grain recognition of powders

此文发于CVPR2019。

题目：Multispectral Imaging for Fine-Grained Recognition of Powders on Complex Backgrounds
作者：Tiancheng Zhi, Bernardo R. Pires, Martial Hebert and Srinivasa G. Narasimhan
Carnegie Mellon University

urlname:MSI_powders_recongnition_cvpr2019

使用光谱图像对粉末进行分类，建立了粉末物体的数据集，方法貌似没有创新，属于工程应用。
【各种粉末名词劝退】

系统搭的有点意思，使用了三个相机拍摄：

<div align = center>
<img src = ./papers_201906_spectral/powder_system.png />
</div>

粉末举例：
<div align = center>
<img src = ./papers_201906_spectral/powder_eg.png />
</div>






### Hyperspectral Imaging with Random Printed Mask

此文发于CVPR2019
题目：Hyperspectral Imaging with Random Printed Mask
作者：Yuanyuan Zhao1 Hui Guo1 Zhan Ma1 Xun Cao1 Tao Yue1,2 Xuemei Hu1
1Nanjing University, Nanjing, China
2NJU institute of sensing and imaging engineering, Nanjing, China


urlname: random_printed_HSI_cvpr2019


提出一种使用商用打印机打印掩膜的重建高光谱图像的方法。
实质是对mask的改进，不过脑洞还是挺大的。也通过硬件实现，有说服力。

Overview：
<div align = center>
<img src = ./papers_201906_spectral/HSIrandom_mask.png />
</div>



### non-local-global HSI denoising

此文发于CVPR2019

题目：Non-local Meets Global: An Integrated Paradigm for Hyperspectral Denoising
作者：Wei He1, Quanming Yao2∗, Chao Li1, Naoto Yokoya1y, Qibin Zhao1
1RIKEN AIP 2HKUST

urlname: nonlocalGlobal_HSI_denoising_cvpr2019





### Multispectral Transfer Network

此文发于AAAI2018

题目：Multispectral Transfer Network:Unsupervised Depth Estimation for All-Day Vision
作者：Namil Kim,∗1,2 Yukyung Choi,∗1,3 Soonmin Hwang,1 In So Kweon1
1Korea Advanced Institute of Science and Technology (KAIST), Korea
2NAVER LABS Corp., Korea 3Clova, NAVER Corp., Korea


urlname: Multispectral_Transfer_Network_aaai2019





### unsupervised cross_spectral_stereo_cycleGAN


此文发于AAAI2019，欢迎在文末留言交流。


题目：Unsupervised Cross-spectral Stereo Matching by Learning to Synthesize
作者：Mingyang Liang1;2∗, Xiaoyang Guo3∗, Hongsheng Li3, Xiaogang Wang3, You Song1 y
1Beihang University, Beijing, China
2SenseTime Research
3The Chinese University of Hong Kong, Hong Kong, China

urlname:cross_spec_stereo_cycleGAN_AAAI2019




<div align = center>
<img src = ./paper_Hyperspectral_Image_Reconstruction_Using_a_Deep_Spatial-Spectral_Prior_CVPR_2019/eq3.png />
</div>


### Reference

