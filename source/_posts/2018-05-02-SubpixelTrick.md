---
title: 使用神经网络进行图像超分辨踩的坑
date: 2018-05-02 20:45:00
updated: 2018-05-02 20:45:00
comments: true
tags:
- 图像处理
- XJBX

categories: [图像处理]
copyright: true
urlname: SubpixelTrick

---



1、matlab的bicubic结果会有小于0或者大于255的情况出现。

Image interpolation wrong for pixel values exceeding vmax #8631
MATLAB`resize`函数中也说明了：

```matlab
%   For bicubic interpolation, the output image may have some values
%   slightly outside the range of pixel values in the input image.  This
%   may also occur for user-specified interpolation kernels.
%
```

<!--more-->


2、神经网络训练出来的结果也会有小于0或者大于255的情况出现


Also remember that loss function is based on scaled images (pixel values between 0 and 1), so the predicted residual has to be scaled back by 255 before it is added to low resolution image. If some pixels become negative or go above 255, we return them to 0 and 255 respectively before saving.

解决方法：
**make sure no pixels are outside [0, 255] interval
**

参考
1.https://www.cntk.ai/pythondocs/CNTK_302A_Evaluation_of_Pretrained_Super-resolution_Models.html
2.https://cntk.ai/pythondocs/CNTK_302B_Image_Super-resolution_Using_CNNs_and_GANs.html
3.https://blog.csdn.net/Autism_/article/details/79401798
4.https://github.com/matplotlib/matplotlib/issues/8631