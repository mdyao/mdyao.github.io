---
date: 2019-06-23 19:21:00
title: 论文笔记|Spectral Reconstruction from Dispersive Blur:A Novel Light Efficient Spectral Imager
urlname: Spectral_from_blur_cvpr2019
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

题目：Spectral Reconstruction from Dispersive Blur: A Novel Light Efficient Spectral Imager
作者：Yuanyuan Zhao∗,1 Xuemei Hu∗,1 Hui Guo1 Zhan Ma1 Tao Yue1,2 Xun Cao1
1Nanjing University, Nanjing, China
2NJU institute of sensing and imaging engineering, Nanjing, China

<!--more-->



作者提出一种利用DOB(difference of blur)获取多光谱图像的方法。在理论上证明了从单个棱镜blur图像以及一个场景中任意点光谱 恢复整幅高光谱图像的方法。

所谓DOB约束，即沿每个边缘的色散方向的色散模糊的导数正好是相邻区域的光谱差。特别地，多光谱图像重建问题可以被建模为N维线性方程组，并且通过图模型，作者理论证明了DoB约束提供了N
-1个独立约束，所以需要额外的点来恢复光谱图像。作者引入边缘掩膜来获得边缘点的附加频谱信息，实现多光谱图像的全秩检索。

### 理论

基于两个假设，1、图像可以被显示地分割为一系列区域，并且在每个区域内经过一个缩放因子光谱是可以达到均匀；2、每对相邻边沿分散方向的最大间距均大于分散尺寸。



####　DoB约束

通过三棱镜，一个点的光谱可以分散到空间维度上。考虑两个区域$(i,j)$之间的边界，Dob可以表示为：
$$\nabla_\theta b=\delta_{ij}*(s_i-s_j)\tag{1}$$

$\delta$是冲击函数，$*$是卷积，$\nabla_\theta b表示$沿着投影角度$\theta$对图像强度b求导数。因此，如果我们知道冲击函数的位置，我们就可以从色散模糊的导数中得到光谱$s_i$和$s_j$的差。

对一幅色散模糊图像，我们可以定义边界矩阵A和DoB矩阵B去表示一个DOB约束，使用AB的每一行表示一个边界的DOB约束，一幅色散模糊图所有的DOB约束可以表示为：

$$AS=B \tag{2}$$

S表示光谱区域。A的每一行只有两个非零值(1,-1),下面证明A的秩为N-1，并且需要额外的光谱信息去全秩恢复S。



#### 光谱重建图理论

为了讨论A的秩，作者建立了一个相关的图模型，$\mathcal{G}=(\mathcal{V},\mathcal{\varepsilon})$,其中，V是顶点集，每一个顶点代表一个表面。$\epsilon$表示边集合。

<div align = center>
<img src = ./paper_Zhao_Spectral_Reconstruction_From_Dispersive_Blur_A_Novel_Light_Efficient_Spectral_CVPR_2019/overview.png />
</div>


### Reference
[机器学习&数据挖掘笔记_12（对Conjugate Gradient 优化的简单理解）](https://www.cnblogs.com/tornadomeet/p/3265225.html)

[HQS——Half Quadratic Splitting半二次方分裂](https://www.cnblogs.com/wxl845235800/p/10734866.html)


Learning Deep CNN Denoiser Prior for Image Restoration




