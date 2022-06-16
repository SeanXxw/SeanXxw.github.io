---
title: VFX-全息
author: Sean
layout: post
---
这一篇，是关于UV动画的。讲述了在引擎中如何制作全息的效果。

****

先上效果图：<br>

![final](https://user-images.githubusercontent.com/106949238/173721483-4fa01103-65a9-425e-ab09-78755aba1ee7.gif)

### 实现方式

#### 扫描线
<font size="3">
  扫描线通过SD制作。<br>
  通过TileSampler节点生成扫描线，用一个Dirt做SlopBlur操作，一个Dirt做明暗叠加。<br>
  在UE4中通过Panner节点去对纹理进行采样。<br>
  如下图：
</font>

![scanline](https://user-images.githubusercontent.com/106949238/173819196-917f412e-43f7-4d53-b136-11fb44862bf9.png)
![scanline_02](https://user-images.githubusercontent.com/106949238/173820159-99a8e143-68ae-40b7-8e53-4827ebd4a578.gif)

#### 粗高亮线
<font size="3">
  为了表现更丰富，在扫描线上在叠加一层粗的高亮线。<br>
  通过UV的V轴，做一个渐变Mask向上移动的动画。
  如下图：
</font>

![boldline](https://user-images.githubusercontent.com/106949238/173823038-aa0a2ffe-efa6-4e81-bb2d-f649bdf48c8d.png)
![boldline](https://user-images.githubusercontent.com/106949238/173823160-94c0abde-229f-456e-9fb6-6839a3d46d1a.gif)

#### Alpha部分
<font size="3">
  1、是利用扫面线的灰度值做一个基础的Alpha,通过灰度值和时间比较做Alpha变化。<br>
  2、比较重要的就是消失和出现的时候一个闪烁渐变的Alpha。<br>
</font> 


  `从0-1循环的结果`  
   <font size="3">这里利用Sin函数，把[-1, 1]的结果映射到[0, 1]。然后利用easeOutQuint函数做一个曲率的映射[0, 1]的结果。如下图：<br></font> 
  
  ![curve](https://user-images.githubusercontent.com/106949238/173852587-f0cae60d-4b4b-41fa-b496-fbab806be264.png) 
  ![curvetime](https://user-images.githubusercontent.com/106949238/173853464-13dcb508-f9b3-4394-80a5-2ccbb58d9b6d.gif)
  
  `利用UV形成最后的遮罩`     
  <font size="3">将上一步中得到的结果，通过SphereMask，结合U和V进行遮罩处理。节点如下图：<br></font> 
    
  ![alpha](https://user-images.githubusercontent.com/106949238/173853955-96d1a813-3540-4a1e-97ca-0bb8ea95f3f9.png) 
  ![curvetime02](https://user-images.githubusercontent.com/106949238/173855700-d35991fa-0e9b-49d9-afd6-d7f3959c310d.gif)
