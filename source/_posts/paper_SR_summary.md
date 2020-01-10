---
date: 2018-11-07 17:10:00
title: 论文笔记：SR总结
urlname: SR
comments: true
tags:
 - 论文笔记
 - 超分辨
categories: [文章阅读]
copyright: true
mathjax: true
---


写在前面：
这是一篇不太完善的CNN超分辨总结，整理了近年来深度学习在超分辨领域比较有代表性的工作，随缘更新。

<!--more-->



**SRCNN**

(有码)

论文：
 - [Learning a Deep Convolutional Network for Image Super-Resolution, ECCV2014](http://personal.ie.cuhk.edu.hk/~ccloy/files/eccv_2014_deepresolution.pdf)
 - [Image Super-Resolution Using Deep Convolutional Networks, TPAMI2015](https://ieeexplore.ieee.org/document/7115171?arnumber=7115171)

项目主页：http://mmlab.ie.cuhk.edu.hk/projects/SRCNN.html
作者：Chao Dong, Chen Change Loy, Kaiming He, Xiaoou Tang.

**VDSR**

论文：[Accurate Image Super-Resolution Using Very Deep Convolutional Networks, CVPR2016](https://cv.snu.ac.kr/research/VDSR/VDSR_CVPR2016.pdf)
代码：
- official: https://cv.snu.ac.kr/research/VDSR/
- pytorch: https://github.com/twtygqyy/pytorch-vdsr
- tensorflow: https://github.com/Jongchan/tensorflow-vdsr

作者：Jiwon Kim Jung Kwon Lee Kyoung Mu Lee 

**ESPCN**
论文：[Real-Time Single Image and Video Super-Resolution Using an Efficient Sub-Pixel Convolutional Neural Network，CVPR2016](https://arxiv.org/pdf/1609.05158.pdf)
代码：https://github.com/Tetrachrome/subpixel
作者：Wenzhe Shi, Jose Caballero, Ferenc Huszar, Johannes Totz, Andrew P. Aitken,Rob Bishop, Daniel Rueckert, Zehan Wang


**SRGAN**

论文：[Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network, CVPR2017](http://openaccess.thecvf.com/content_cvpr_2017/papers/Ledig_Photo-Realistic_Single_Image_CVPR_2017_paper.pdf)
代码：
- github(tensorflow): https://github.com/zsdonghao/SRGAN
- github(tensorflow): https://github.com/buriburisuri/SRGAN
- github(torch): https://github.com/junhocho/SRGAN
- github(caffe): https://github.com/ShenghaiRong/caffe_srgan
- github(tensorflow): https://github.com/brade31919/SRGAN-tensorflow
- github(keras): https://github.com/titu1994/Super-Resolution-using-Generative-Adversarial-Networks
- github(pytorch): https://github.com/ai-tor/PyTorch-SRGAN
作者：Christian Ledig, Lucas Theis, Ferenc Huszar, Jose Caballero, Andrew Cunningham,Alejandro Acosta, Andrew Aitken, Alykhan Tejani, Johannes Totz, Zehan Wang, Wenzhe Shi（Twitter的十一个作者，和deepmind的二十几个作者还有差距:)  ）


**RCAN**
论文：[RCAN Image Super-Resolution Using Very Deep Residual Channel Attention Networks-ECCV2018](https://eccv2018.org/openaccess/content_ECCV_2018/papers/Yulun_Zhang_Image_Super-Resolution_Using_ECCV_2018_paper.pdf)
代码：github(official-pytorch)https://github.com/yulunzhang/RCAN
作者：Yulun Zhang, Kunpeng Li, Kai Li, Lichen Wang, Bineng Zhong, Yun Fu

### Reference
[GAN相关：SRGAN，GAN在超分辨率中的应用](https://blog.csdn.net/edogawachia/article/details/79731091)
[从SRCNN到EDSR，总结深度学习端到端超分辨率方法发展历程](https://blog.csdn.net/aBlueMouse/article/details/78710553)
[A collection of high-impact and state-of-the-art SR methods](https://github.com/YapengTian/Single-Image-Super-Resolution)
[Super-Resolution via Deep Learning](https://arxiv.org/abs/1706.09077)
[CSDN解读 RCAN Image Super-Resolution Using Very Deep Residual Channel Attention Networks-ECCV2018 ](https://blog.csdn.net/aaa958099161/article/details/82836846)


