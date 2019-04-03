---
layout: post
title:  "关于常见的像素单位"
subtitle: 'dp, px, dpi'
author: "Pick"
tags:
  - OS
---

### px
> 即像素，`1px` 代表屏幕上一个物理的像素点

- 由于像素密度不同，同样 `100px` 的图片，在不同手机上显示的实际大小可能不同

### DPI
> 像素密度的单位 `dpi` 是 `Dots Per Inch` 的缩写，即每英寸像素数量

- `Android` 系统定义了四种像素密度：低（120dpi）、中（160dpi）、高（240dpi）和超高（320dpi）
- 它们对应的 `dp` 到`px` 的系数分别为 0.75、1、1.5 和 2，这个系数乘以 `dp` 长度就是像素数 `px`

### dp(dip)
> `Density independent pixels`，设备无关像素

- `dp` 与 `dip` 完全相同，只是名字不同而已。在早期的 `Android` 版本里多使用 `dip`，后来为了与 `sp` 统一就建议使用 `dp` 这个名字了
- `dp` 与 `px` 换算公式如下： `dp = (DPI/160) px`

### 为什么使用 `160dpi` 作为标准
- 因为第一款 `Android` 设备（HTC的T-Mobile G1）是属于 `160dpi` 的
- 方便换算，其余三个分别是 `160dpi` 的 `0.75、1.5、2` 倍，若使用 `240dpi` 则会出现无限小数