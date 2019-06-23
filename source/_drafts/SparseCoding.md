---
title: SparseCoding
date: 2018-07-31 21:54:00
updated: 2018-07-31 21:54:00
comments: true
tags:
- 图像处理

categories: [深度学习]
copyright: true
urlname: SparseCoding
---


### 稀疏编码(sparse coding)

所谓稀疏编码，就是**使用一组“超完备”基向量来表示样本数据**。稀疏编码算法的目的就是找到一组基向量 $\phi_i$ ，使得我们能将输入向量 $x$ 表示为这些基向量的**线性组合**：

$$ \rm x=\sum_{i=1}^k a_i\phi_i$$

下面定义具有$m$个向量的稀疏编码代价函数：

$$ {min}_{a_{k}^{(j)} ,\phi_i} \sum_{j=1}^m \|\rm x-\sum_{i=1}^ka_i^{(j)}\phi_i\|^2+\lambda \sum_{i=1}^k\mit{S}\left( a_i^{(j)} \right)$$

上式中，$\mit{S(.)}$为稀疏惩罚函数，由它对远大于零$a_i$进行**惩罚**，使得$\rm x$的表达变得稀疏。而第一项则可以理解为对$\rm x$的重构项，迫使稀疏编码算法能够为$\rm x$提供一个**高度拟合的线性表达式**。

对于稀疏惩罚函数$\mit{S(.)}$，具有多种形式


<div align = center>
<img src="../" width = "300" alt = "单应性矩阵" />
</div>

如图，两张图片中的相同的点叫做corresponding points,比如图中红色的两点就是一对corresponding points。单应性(homography)矩阵就是表示从一张图到另一张图的映射关系的变换矩阵。
<div align = center>
$ H=\begin{bmatrix}
h_{00} & h_{01} & h_{02}\\
h_{10} & h_{11} & h_{12}\\
h_{20} & h_{21} & h_{22}
\end{bmatrix} $

$ \begin{bmatrix}
x_1\\y_1\\1\end{bmatrix}=H\begin{bmatrix}x_2\\y_2\\1\end{bmatrix}=
\begin{bmatrix}h_{00} & h_{01} & h_{02}\\
h_{10} & h_{11} & h_{12}\\
h_{20} & h_{21} & h_{22}\end{bmatrix}
\begin{bmatrix}x_2\\y_2\\1\end{bmatrix}
$
</div>



### 单应性变换应用




中间时代广场左上角的广告牌被替换为"Les Horribles Cernettes"的海报。
### 参考资料：
[1] [深度学习浅层理解（四）-- 稀疏编码](https://www.cnblogs.com/caocan702/p/5666175.html)
[2] [UFLDL稀疏编码](http://ufldl.stanford.edu/wiki/index.php/%E7%A8%80%E7%96%8F%E7%BC%96%E7%A0%81)
[3] [Deep Learning（深度学习）学习笔记整理系列之（五）](https://blog.csdn.net/zouxy09/article/details/8777094)
[4] [【deep learning精华部分】稀疏自编码提取高阶特征、多层微调完全解释及代码逐行详解](https://www.cnblogs.com/happylion/p/4270013.html)