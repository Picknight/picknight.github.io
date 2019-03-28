---
layout: post
title:  "关于字符编码"
subtitle: 'Unicode、UTF-8、UTF-16'
author: "Pick"
tags:
  - OS
---

### Unicode
> `Universal Multiple-Octet Coded Character Set`

- 可以容纳世界上所有文字和符号的字符编码方案
- 简称 `UCS`，俗称 `Unicode`，规定必须用两个字节，也就是16位来统一表示所有的字符  
- 因为计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用8个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），0 - 255被用来表示大小写英文字母、数字和一些符号，这个编码表被称为`ASCII`编码，比如大写字母A的编码是65，小写字母z的编码是122  
- 需要注意的是，`Unicode`只是一个符号集，它只规定了符号的二进制代码，却没有规定这个二进制代码应该如何存储

### UTF-8
> `UCS Transfer Format`

- 互联网的普及，强烈要求出现一种统一的编码方式。`UTF-8` 就是在互联网上使用最广的一种 `Unicode` 的实现方式。其他实现方式还包括`UTF-16`（字符用两个字节或四个字节表示）和 `UTF-32`（字符用四个字节表示）  
- `Unicode`一个中文字符占2个字节，而`UTF-8`一个中文字符占3个字节。从`Unicode`到`UTF-8`并不是直接的对应，而是要过一些算法和规则来转换  
- 总而言之：`Unicode`定义世界每个字符的索引值。`UTF-8/UTF-16` 实现 `Unicode` 的标准，把字符存储到存储介质中。  

### UTF-16

- 编码以 16 位无符号整数为单位，我们把 `Unicode` 编码记作U。编码规则如下：
- 如果`U<0x10000`，U的`UTF-16`编码就是U对应的16位无符号整数（为书写简便，下文将16位无符号整数记作`WORD`）
- 如果`U≥0x10000`，我们先计算`U’=U-0x10000`，然后将`U’`写成二进制形式：`yyyy yyyy yyxx xxxx xxxx`，U的`UTF-16`编码（二进制）就是：`110110yyyyyyyyyy 110111xxxxxxxxxx`
- 为了将一个`WORD`的`UTF-16`编码与两个`WORD`的`UTF-16`编码区分开来，`Unicode`编码的设计者将`0xD800-0xDFFF`保留下来，并称为代理区（Surrogate）


### JavaScript 相关

- `ES6` 新增的 `codePointAt()、String.fromCodePoint()、for...of` 能够正确识别32位的`UTF-16`编码
- 所对应的旧接口依次是 `charAt()、String.fromCharCode()、普通 for 循环`，它们则没有这样的能力，只能识别16位的`UTF-16`编码