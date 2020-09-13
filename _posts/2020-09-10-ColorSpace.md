---
layout: post
title: 颜色空间
date: 2020-9-10
categories: blog
tags: [Image Processing]
description: 介绍常用的颜色空间。
---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>



## 颜色空间

​	本文章按照自己的理解记录一下常用的颜色空间，若有不正确的地方，欢迎指出。定义颜色空间通常的参考标准为CIELAB或者CIEXYZ

##  Lab

Lab空间：其中L表示的是亮度（黑色为0，白色为100），a表示从绿色（-128）到红色（+127），b表示蓝色（-128）到黄色（+127）。当 a = 0,b = 0 时，表示的为灰色。其设计的目的是使得视觉感知变化量与颜色的数值变化量近似，其是一种与设备无关的颜色模型（球）。

## XYZ

XYZ颜色空间中包含所有的色觉信息，因此，XYZ表示的颜色具有设备不变性。XYZ的出现是避免了RGB空间出现的负值？因为在最早的LMS空间中，并非每个值都是有意义的，如M分量非零，而L和S分量为零，这在物理上是不存在的。而定义的XYZ空间，所有的非负坐标都是有意义的。

## sRGB

​	sRGB 空间为非线性空间（其由线性部分和非线性部分分组成），其响应曲线恰好类似于gamma 曲线，因此可以在CRTS设备上显示，无须gamma校正。

​    sRGB 与 RGB 和 XYZ空间的相互转换:

​	首先转成 RGB 线性空间:
$$
\left[\begin{matrix} R_{linear}\\G_{linear}\\B_{linear} \end{matrix}\right] = \left[\begin{matrix} 3.24096994 & -1.53738318 & -0.49861076 \\-0.96924364 & 1.8759675 & 0.04155506\\0.05563008 & -0.20397696 & 1.05697151\end{matrix}\right]\left[\begin{matrix}X\\Y\\Z\end{matrix}\right]
$$
​	

​	RGB线性空间转成sRGB非线性空间：
$$
r_u =\left\{\begin{aligned} 12.92u && u≤0.0031308\\1.055u^{1/2.4}-0.055 && otherwise \end{aligned}\right.
$$
​	反变换：即将sRGB->RGB->XYZ:


$$
r^{-1}_{u} =\left\{\begin{aligned}u/12.92 && u≤0.04045\\(\frac{u+0.055}{1.055})^{2.4}-0.055 && otherwise \end{aligned}\right.
$$

$$
\left[\begin{matrix} X\\Y\\Z \end{matrix}\right] = \left[\begin{matrix}0.41239080 & 0.35758434 & 0.18048079\\0.21263901&0.71516868&0.07219232\\0.01933082&0.11919478&0.95053215\end{matrix}\right]\left[\begin{matrix}R_{linear}\\G_{linear}\\B_{linear}\end{matrix}\right]
$$


## HSV

HSV 空间：H表示色调（0~360度），S为饱和度（0~100%），V为明度（0~1）





#### 参考

[1] [wikipedia](https://en.wikipedia.org/wiki/SRGB#)












