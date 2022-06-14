---
title: VFX-极光
author: Sean
layout: post
---
这一篇，是关于UV动画的。讲述了在引擎中如何制作极光的效果。

****

1. [模型处理](#模型处理)
2. [材质节点处理](#材质节点处理)
3. [最终效果](#最终效果)

### 模型处理
#### 纹理部分
<font size="3">
   纹理有两张，均在SD中制作。<br>
   第一张纹理RGB通道分别为：整体Alpha强度、底部亮度叠加纹理、极光纹理。<br>
</font>

   ![texture01](https://user-images.githubusercontent.com/106949238/173581457-99df3a7f-b280-4b80-933c-3fd184cb5e4a.png)
   
<font size="3">
   第2张纹理是一张类似焦散效果的纹理，用来模拟动态的波纹<br>
</font>

   ![texture02](https://user-images.githubusercontent.com/106949238/173582158-36245b19-ea15-467f-97e4-55d35c7e6a87.png)
   
#### 模型部分
<font size="3">
   模型在Blender中制作。<br>
   先拉取一个面片，然后挤出几段，细分1级(注意这里要对边卡一下线)之后调整点的位置即可。<br>
</font>  

   ![model](https://user-images.githubusercontent.com/106949238/173584904-31dbf2d4-e70c-4d2e-89f8-2d58a73dd965.gif)
   
   
<font size="3">
   UV的话结合纹理来调整好就行。如下图：<br>
</font>

   ![uv](https://user-images.githubusercontent.com/106949238/173585353-ab90c406-be8e-47e6-84d7-66d863dec409.png)

### 材质节点处理
#### 颜色部分
<font size="3">
   首先给波纹上色，利用<b>Panner</b>节点采样纹理，V坐标进行遮罩处理。下图中标1的部分。<br>
   然后给极光底部上色，与波纹的颜色进行的叠加。下图中标2的部分。<br>
</font>

   ![texture03](https://user-images.githubusercontent.com/106949238/173590981-c440b793-8a1b-46ef-baec-d70f90aaae05.png)

#### Alpha部分
<font size="3">
   首先对缩放的UV做一个线性转化，<b>使用LinearGradient节点。</b>
   对两端进行一个Alpha过渡的控制。下图中标1的部分。<br>
   然后同样使用<b>Panner</b>节点去采样纹理1。与上面的Alpha相乘。下图中标2的部分。<br>
</font>

   ![texture04](https://user-images.githubusercontent.com/106949238/173591981-9e8905f1-0acb-4386-8222-9f97a3d80f09.png)
   
****

### 最终效果

![final](https://user-images.githubusercontent.com/106949238/173593675-199e47c8-680f-4715-b59e-1dcdf2266e2a.gif)
