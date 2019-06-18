---
title: MATLAB读取曲线图并重新绘制
date: 2018-04-08 22:30:00
updated: 2018-04-08 22:31:00
comments: true
tags:
- MATLAB
- XJBX

categories: [深度学习]
copyright: true
urlname: MatlabRePlot

---


最近需要从datasheet中读取某款相机的光谱响应曲线，发现下面这段代码[^1]。但是最后发现和自己的需求并不匹配，自己是要最终求出曲线的函数，完成由离散的点到数学公式的转换过程。这个小demo能够实现的仅仅是re-draw the pictures.仍旧记之。

<!--more-->
```matlab
I = imread('target.png');%读取处理好的图片，必须是严格坐标轴线为边界的图片
I=rgb2gray(I);           %灰度变化
I(I>200)=255;           %二值化
I(I<=200)=0;            %二值化
imshow(I)                 %显示图片
figure;
[y,x] = find(I==0);     %找出曲线的像素位置
y = max(y) -y;           %将屏幕坐标转换为有手系迪卡坐标
plot(x,y,'r.','markersize',2)%显示转换后的图像
[Xx,Yy]= ginput(2);       % 读取真是坐标左上角和右下角的两点
min_x = min(Xx);
max_x = max(Xx);
min_y= min(Yy);
max_y = max(Yy);
% x1 = (x-Xx(1))*(max_x-min_x)/(Xx(2)- Xx(1))+min_x;
% y1 = (y-Yy(1))*(min_y-max_y)/(Yy(2)- Yy(1))+max_y;
%% 坐标变化，如果坐标原点不为0，则需在该轴加上省去的坐标轴数
xo = 0;%原始图像起点坐标x
yo = 0;%原始图像起点坐标x
xl = 3;    %原始图像x轴长
yl=25;      %原始图像y轴长
x1 = (x - min(Xx))*xl/(max(Xx)-min(Xx))+xo ;%数据点x值
y1 = (y - min(Yy))*yl/(max(Yy)-min(Yy))+yo;%数据点y值
plot(x1,y1,'r.','markersize',2)
axis([0,3,0,25])
```

原图：
![原图](https://upload-images.jianshu.io/upload_images/10342473-f5d64bb515e856ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
效果图：
![效果图](https://upload-images.jianshu.io/upload_images/10342473-77f3b13d4c05b48b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[^1]:[用matlab提取jpg曲线数据或者jpg图片重新复原](https://www.cnblogs.com/Kermit-Li/p/6829778.html)