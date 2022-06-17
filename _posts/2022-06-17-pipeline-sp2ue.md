---
title: Pipeline - SP对齐UE4
author: Sean
layout: post
---
这一篇，是关于制作管线。讲述了如何让SP去对齐UE4的效果，解决制作管线中DCC和引擎渲染差异较大的痛点。

****

1. [实现方式](#实现方式)
    - <font size="3">造成差异的原因</font>
    - <font size="3">光照对齐</font>
    - <font size="3">反射对齐</font>
    - <font size="3">ToneMapping对齐</font>
2. [步骤拆解对比图](#步骤拆解对比图)
3. [最终效果](#最终效果)

### 实现方式

#### - 造成差异的原因
<font size="3">
  1、光照部分：SP基于IBL的。而游戏引擎中通常简单的光照包含了：主光、SkyLight(SkyGI)、IBL反射。<br>
    这些光照的差异直接影响了Shading Model的计算。<br>
  2、ToneMapping算法不同，导致后期在颜色从HDR转回LDR的时候出现了差异。<br>
  <b>所以总结起来，要实现两边的对齐，就要在SP中自定义Shading Model去和引擎匹配</b>。<br>
</font>


#### - 光照对齐
<font size="3">
  <b>主光部分</b>：<br>
    因为主光是一个无限远的光源，只有方向，没有位置。所以在Shader中需要定一个主光源的方向。<br>
    这里要注意的一点就是标红框部分，Z轴需要使用SP中的内置变量<b>enviroment_rotation</b>。<br>
    这样才能够通过shift + 右键正常的旋转灯光。
</font>

  ![light](https://user-images.githubusercontent.com/106949238/174303014-22c91c23-d35b-4f4f-b7fe-450af25db4d2.png)

<font size="3">
  <b>SkyLight</b>：<br>
    以UE4为例，天光通常通过球谐的方式来获取Cubemap。<br>
    这里要注意一点的是，有时候在SkyLight上会勾选下半球的颜色去补充下半部分的颜色。如果有勾选的话，这里可以使用一个Trick，对Cubemap贴图的下半部分做一个纯色填充。
    如下图：<br>
</font>

  ![skylight_01](https://user-images.githubusercontent.com/106949238/174304444-8e1acac0-6a04-4697-a8e0-6451da72b850.png)
  ![skylight_02](https://user-images.githubusercontent.com/106949238/174304809-2cca1415-1880-41ba-8cf4-5a3d8b1f1f44.png)

<font size="3">
  Shading Model中对应的SH代码处理如下图：<br>
</font>

  ![sh](https://user-images.githubusercontent.com/106949238/174305059-37de2768-7254-4063-99f6-adb0f428936e.png)

#### - 反射对齐
<font size="3">
  <b>IBL反射</b>：<br>
    以UE4为例，这里对应的就是Reflection Capture。<br>
    Shading Model中对应的代码如下图：<br>
</font>

  ![ibl](https://user-images.githubusercontent.com/106949238/174305530-5dfc962a-27f6-496b-8751-e616dd7d1a8c.png)

#### - ToneMapping对齐
<font size="3">
  <b>ToneMapping</b>：<br>
    这一步发生在颜色最终输出之前，我们用的ToneMapping代码如下：<br>
</font>

  ![tonemapping](https://user-images.githubusercontent.com/106949238/174306868-339052e2-f18d-42d0-9c9c-2bed72d9dd16.png)  

### 步骤拆解对比图
<font size="3">
  这里的步骤拆解分别对应的是Shading Model中几个比较关键的计算项拆解。<br>
</font>
<font size="3">
  <b>Diffuse</b><br>
</font>

  ![diffuse](https://user-images.githubusercontent.com/106949238/174308439-8335b9f2-f270-4ff3-85f6-d292a079bff0.png)

<font size="3">
  <b>Specular</b><br>
</font>

  ![specular](https://user-images.githubusercontent.com/106949238/174308552-d67356e7-53f5-4b27-a163-499323de081c.png)
  
<font size="3">
  <b>SpecularIBL</b><br>
</font>

  ![specular_ibl](https://user-images.githubusercontent.com/106949238/174308704-b4313c4d-898c-4096-bee1-1624162f9ecf.png)

<font size="3">
  <b>EnvFactor</b><br>
</font>

  ![EnvFactor](https://user-images.githubusercontent.com/106949238/174308880-539d78b2-0c80-41a8-9007-794cc8cba3c7.png)

<font size="3">
  <b>SH</b><br>
</font>

  ![SH_02](https://user-images.githubusercontent.com/106949238/174308919-0132e67e-d3be-41ca-bda5-d04693513c0d.png)

### 最终效果

  ![show](https://user-images.githubusercontent.com/106949238/174309072-6995407b-fd74-4c4c-86df-692f979580ee.png)

