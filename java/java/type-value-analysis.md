---
title: "Analysis of value range based on java type"
date: 2020-05-12T21:48:09+08:00
draft: false
categories: ["java"]
tags: ["java type"]
---
&emsp;&emsp;求"2^100 %
5"的值，通过分析，需要注意的是在定义时所使用的数据类型，如果定义的数据类型过小，获得的结果就会越界，不能取得正确的结果。   

#### 基本类型的取值范围表

|   类型   |  存储需求  |    取值范围    |
|   :-:    |    :-:     |      :-:       |
|   byte   |     1      |    -127~128    |
|   short  |     2      |   -2^15~2^15-1 |
|   int    |     4      |   -2^31~2^31-1 |
|  long    |     8      |   -2^63~2^63-1 |
|  float   |     4      | -3.402823*10^38~3.402823*10^38|
| double   |     8      | -1.7977*10^308~1.977*10^308   |
|  char    |     2      |                |
| boolean  |     1      |  true 或 false |
