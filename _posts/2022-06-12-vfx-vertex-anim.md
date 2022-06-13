---
title: VFX-顶点动画
author: Sean
layout: post
---
这一篇，是关于顶点动画的两个效果应用。两种效果的实现方式属于同一类型，所以放在一起记录了。

***

1. [传送效果](#传送效果)
   - [实现方式](#实现方式)
2. [黑洞效果](#黑洞效果)


#### 传送效果
效果如下：

![gif_01](https://user-images.githubusercontent.com/106949238/173237262-a0c10011-1c95-4ed8-b348-5f73dcea18c3.gif)

#### 实现方式
1.时间循环
这里我把时间做了一个6s的循环。
0-2s用来做方块向下的渐变UV动画、顶点动画、Alpha剔除。
3-5s用来做方块向上的渐变UV动画、顶点动画、Alpha显示。
5-6s为了视觉对称做了停顿。
如下图：
![time](https://user-images.githubusercontent.com/106949238/173387009-43706eb4-c2a3-4d54-9fbb-4fda8765c7ba.gif)


#### 黑洞效果
效果如下：
