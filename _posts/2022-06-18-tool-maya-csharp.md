---
title: Tool - Maya/C#工具开发
author: Sean
layout: post
---
这一篇，是关于工具开发的。讲述了如何部署环境以及在Maya中使用C#开发工具。

****

1. [环境部署](#环境部署)
2. [运行模板示例](#运行模板示例)
3. [自定义界面操作物体](#自定义界面操作物体)
4. [个人总结](#个人总结)
  
### 环境部署  
#### - 获取Maya Devkit:
<font size="3">
    在<a href="https://www.autodesk.com/developer-network/platform-technologies/maya">Autodesk Developer Network Maya</a>中找到对应版本的工具包。<br>
    解压工具包后，将解压的文件复制到Maya的安装目录下，例如：C:\Program Files\Autodesk\Maya2018<br>
</font>
  
#### - 配置系统环境变量:
<font size="3">
  在系统高级设置中配置环境变量：<b>DEVKIT_LOCATION</b>和<b>MAYA_LOCATION</b>。如下图：<br>
</font>

  ![enviroment](https://user-images.githubusercontent.com/106949238/174418947-286b9ea2-0a5f-470e-a3a9-05f9f5280d31.png)
  
### 运行模板示例  
#### - 获取示例文件：
<font size="3">
    在<a href="https://github.com/ADN-DevTech/Maya-Net-Wizards">Github</a>下载示例文件zip包。<br>
    解压工具包后，分别将下图中红框的3个zip包拷贝到C:\Users\username\Documents\Visual Studio 2019\Templates的ItemTemplates以及绿框中的zip包拷贝到ProjectTemplates。<br>
</font>

  ![zip](https://user-images.githubusercontent.com/106949238/174422936-4e2190e6-116d-432e-acf5-282fe0814a60.png)
  
<font size="3">
    这个时候打开Visual Studio新建项目，就能够看到Maya C# plug-in的模板。如下图：<br>
</font>

  ![vs maya](https://user-images.githubusercontent.com/106949238/174423016-da32b9ba-b47d-4f31-a47a-048c1937938f.png)
  
#### - 添加Maya Module
<font size="3">
    为了能够让制作的工具能够在Maya Plug-in中正常开启调用，这里需要添加Module。<br>
    Module的目录结构形式，以及描述文件MOD形式如下图：<br>
</font>

  ![module](https://user-images.githubusercontent.com/106949238/174423353-273bf690-00cf-4418-8c54-7931b9b30656.png)
  
<font size="3">
    <b>创建Module的步骤</b>：<br>
    1. 找到Maya的目录，C:\Users\username\Documents\maya。在这级目录下新建文件夹命名为<b>modules</b>。<br>
    2. 在modules文件夹下再新建一个目录，命名代表的就是Plugin的名字。<br>
    3. 按照上图Module目录结构，在这个自定义的Plugin文件夹下创建其余目录结构。如下图：<br>
</font>

  ![module_02](https://user-images.githubusercontent.com/106949238/174423587-86afe1af-a7de-4a3c-bb71-61eee29297a1.png)
  
<font size="3">
    4. 找到Maya版本的目录，例如：C:\Users\username\Documents\maya\2018。在这级目录下新建文件夹命名为<b>modules</b>。<br>
    5. 在modules文件夹下创建MOD描述文件，命名要和前面定义的插件名相同。内容如下图：<br>
</font> 

  ![modfile](https://user-images.githubusercontent.com/106949238/174424525-88bea7e4-83dd-4edf-96fd-011267d9d17d.png)
  
#### - HelloWorld
<font size="3">
    <b>第一个程序HelloWorld</b>：<br>
    创建工程，在C#文件中需要做几件事情：<br>
    1. 引入命名空间<b>Autodesk.Maya.OpenMaya</b>。<b>注意：</b><br>
       如果这里报错的话，需要在项目中引入<b>openmayacs.dll</b>库。这个库的路径通常在<b>C:\Program Files\Autodesk\Maya2018\bin</b>。<br>
    2. 新建类，这个类需要继承自<b>MPxCommand</b>以及接口<b>IMPxCommand</b>。<br>
    3. 重写doIt方法，Maya调用执行的具体功能都放在这里实现。<br>
    4. 注册绑定命令，以供Maya通过Mel或者Python调用到。<br>
    如下图：<br>
</font>

  ![class](https://user-images.githubusercontent.com/106949238/174469377-0656b58b-e7c8-4f0c-8f53-3943598cfda5.png)

<font size="3">
    5. 需要把VS生成改成Release，然后重新生成解决方案。生成后，可在项目文件夹的Release目录下找到生成的.dll文件。<br>
    <b>要注意的是，如果生成的后缀不是.nll.dll，那么要将文件后缀改成.nll.dll</b><br>
    6. 将dll文件复制到modules下的plug-ins文件夹内。如下图：<br>
</font>

  ![dllpic](https://user-images.githubusercontent.com/106949238/174469465-bf5dcba7-3a4e-4445-9c37-fbfa112cf7c5.png)

<font size="3">
    7. 打开Maya，在插件管理器下加载插件。<br>
    8. 通过MEL或者Python调用我们注册的命令。如下图：<br>
</font>
  
  ![mayacall](https://user-images.githubusercontent.com/106949238/174469538-5e24a5b9-2f0d-46bf-91e6-24ee3fe7840b.png)
  
### 自定义界面操作物体
<font size="3">
    在VS中使用WPF来编辑UI，以及绑定事件，处理逻辑是一件非常方便的事情。所以我这里就想能否通过上面的方式，让Maya打开WPF界面，来操作Maya中的物体。<br>
    经过尝试之后，这里发现是可行的。这里有一个很简单的重命名工具展示。如下图：<br>
</font>

  ![wpf](https://user-images.githubusercontent.com/106949238/174470124-50617a00-9cca-4d9b-b331-c45ffbf33873.gif)

### 个人总结
<font size="3">
    使用C#来制作Maya插件以及结合WPF来自定义UI界面在我看来各有利弊，纯属个人观点。<br>
</font>  

#### 优点
<font size="3">
    1. 对熟悉C#的同学很友好，并且VS有很多便捷的功能。<br>
    2. 实际操作过程中，使用WPF来自定义UI界面并且绑定事件处理逻辑，比使用QtDesigner设计界面再转成Python再去对功能空间做绑定事件处理逻辑来的便捷。<br>
    3. 我看到3D Max也是支持.NET的，所以这意味着同样的功能，可以使用同一套设计的WPF界面，美术同学在两个软件切换使用的时候不会有差异性。<br>
    4. Maya集成.NET插件主要依赖于.NET框架的版本，只要依赖的.NET框架版本是正确的，就不用考虑担心Maya版本不同导致API变化导致功能出现问题。<br>
    5. 如果工具要给到第三方，通过.dll的加密会更安全。<br>
</font>

#### 缺点
<font size="3">
    1. 使用.NET的方式在调试以及编译上不如Python。<br>
    2. 对于已经非常熟悉Maya，Python，Qt，PySide的同学，似乎没什么必要这么做。<br>
</font>
