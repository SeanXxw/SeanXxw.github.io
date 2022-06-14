---
title: VFX-顶点动画
author: Sean
layout: post
---
这一篇，是关于顶点动画的两个效果应用。两种效果的实现方式属于同一类型，所以放在一起记录了。<br />

****

<font size="7">输入文章内容</font>

1. [传送效果](#传送效果)
   - [实现方式](#实现方式)
2. [黑洞效果](#黑洞效果)

### 传送效果
效果如下：<br>
![gif_01](https://user-images.githubusercontent.com/106949238/173237262-a0c10011-1c95-4ed8-b348-5f73dcea18c3.gif)

#### 实现方式
1、时间循环<br>
这里我把时间做了一个6s的循环。<br>
0-2s用来做方块向下的渐变UV动画、顶点动画、Alpha剔除。<br>
3-5s用来做方块向上的渐变UV动画、顶点动画、Alpha显示。<br>
5-6s为了视觉对称做了停顿。<br>
如下图：<br>
`时间循环节点`<br>
![time_node](https://user-images.githubusercontent.com/106949238/173389684-d28060ec-ad85-4680-a5d7-e0f6dc2d59cc.png)

`时间循环动态展示`<br>
![time](https://user-images.githubusercontent.com/106949238/173387844-5a77a87f-3346-430c-84b3-f73b0fb4934d.gif)

2、与方块纹理样式结合的渐变UV动画<br>
利用`BoundingBoxBased_0-1_UVW`节点去获取模型Z轴的渐变。<br>
Panner采样一张方块纹理与上面的时间循环利用Smoothstep结合，得到带方块纹理的UV动画。<br>

如下图：<br>
`结合方块纹理节点`<br>
![time_node_02](https://user-images.githubusercontent.com/106949238/173390949-f033ba68-e084-4457-83b8-893e2ff0da09.png)

`动态展示`<br>
![time_02](https://user-images.githubusercontent.com/106949238/173391374-50b63683-6f21-4fae-95cb-d6aa4af4fb47.gif)

3、世界位置偏移<br>
定义一个偏移距离。<br>
当时间循环从0-1表示从原点偏移到目标距离。<br>
当时间循环从1-0表示从目标距离偏移到原点。<brx>
并且和利用`BoundingBoxBased_0-1_UVW`节点去获取模型Z轴的渐变结合，让这个偏移存在先后关系，打破统一性。<br>
`WPO节点`<br>
![wpo](https://user-images.githubusercontent.com/106949238/173393718-24f0e52e-6cb2-48ed-bf83-fa360e00fa2d.png)

4、Alpha<br>
Alpha的剔除和出现，就是利用前面提到的与方块纹理样式结合的渐变UV动画取反即可。


### 黑洞效果
效果如下：<br>
![holesuck](https://user-images.githubusercontent.com/106949238/173475942-5980f7f3-a743-4822-834a-a3373922504f.gif)

#### 实现方式
和传送效果的实现方式基本一致。这里的区别在于WPO。<br>
传送效果的世界位置偏移是一个整体的偏移量。<br>
而这里作为黑洞吸入的效果，我们需要以一个世界坐标点为目标点，去计算每个顶点与目标点的向量再进行偏移。从而才能达到一种吸入的效果。<br>

如下图：<br>
![wpo2](https://user-images.githubusercontent.com/106949238/173477949-997f2f52-904f-4b81-a942-f1a0228fbac4.png)

除此之外，从模型的哪个位置开始偏移，这里也是利用了`BoundingBoxBased_0-1_UVW`节点产生遮罩。可以根据自己的需要自行调整。<br>
![offset-mask](https://user-images.githubusercontent.com/106949238/173478837-0ea4d818-0d75-429c-804c-795c7f23970f.png)


