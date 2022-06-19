---
title: Tool - Maya - C#工具开发
author: Sean
layout: post
---
这一篇，是关于工具开发的。讲述了如何部署环境以及在Maya中使用C#开发工具。

****

1. [环境部署](#环境部署)
2. [运行模板示例](#运行模板示例)
3. [最终效果](#最终效果)  
  
### 环境部署  
#### - 获取Maya Devkit:
<font size="3">
    在<a href="https://www.autodesk.com/developer-network/platform-technologies/maya">Autodesk Developer Network Maya</a>中找到对应版本的工具包。</br>
    解压工具包后，将解压的文件复制到Maya的安装目录下，例如：C:\Program Files\Autodesk\Maya2018</br>
</font>
  
#### - 配置系统环境变量:
<font size="3">
  在系统高级设置中配置环境变量：<b>DEVKIT_LOCATION</b>和<b>MAYA_LOCATION</b>。如下图：</br>
</font>

  ![enviroment](https://user-images.githubusercontent.com/106949238/174418947-286b9ea2-0a5f-470e-a3a9-05f9f5280d31.png)
  
### 运行模板示例  
#### - 获取示例文件：
<font size="3">
    在<a href="https://github.com/ADN-DevTech/Maya-Net-Wizards">Github</a>下载示例文件zip包。</br>
    解压工具包后，分别将下图中红框的3个zip包拷贝到C:\Users\username\Documents\Visual Studio 2019\Templates的ItemTemplates以及绿框中的zip包拷贝到ProjectTemplates。</br>
</font>

  ![zip](https://user-images.githubusercontent.com/106949238/174422936-4e2190e6-116d-432e-acf5-282fe0814a60.png)
  
<font size="3">
    这个时候打开Visual Studio新建项目，就能够看到Maya C# plug-in的模板。如下图：</br>
</font>

  ![vs maya](https://user-images.githubusercontent.com/106949238/174423016-da32b9ba-b47d-4f31-a47a-048c1937938f.png)
  
#### - 添加Maya Module
<font size="3">
    为了能够让制作的工具能够在Maya Plug-in中正常开启调用，这里需要添加Module。</br>
    Module的目录结构形式，以及描述文件MOD形式如下图：</br>
</font>

  ![module](https://user-images.githubusercontent.com/106949238/174423353-273bf690-00cf-4418-8c54-7931b9b30656.png)
  
<font size="3">
    <b>创建Module的步骤</b>：</br>
    1. 找到Maya的目录，C:\Users\username\Documents\maya。在这级目录下新建文件夹命名为<b>modules</b>。</br>
    2. 在modules文件夹下再新建一个目录，命名代表的就是Plugin的名字。</br>
    3. 按照上图Module目录结构，在这个自定义的Plugin文件夹下创建其余目录结构。如下图：</br>
</font>

  ![module_02](https://user-images.githubusercontent.com/106949238/174423587-86afe1af-a7de-4a3c-bb71-61eee29297a1.png)
  
<font size="3">
    4. 找到Maya版本的目录，例如：C:\Users\username\Documents\maya\2018。在这级目录下新建文件夹命名为<b>modules</b>。</br>
    5. 在modules文件夹下创建MOD描述文件，命名要和前面定义的插件名相同。内容如下图：</br>
</font> 

  ![modfile](https://user-images.githubusercontent.com/106949238/174424525-88bea7e4-83dd-4edf-96fd-011267d9d17d.png)
  
#### - HelloWorld
<font size="3">
    为了能够让制作的工具能够在Maya Plug-in中正常开启调用，这里需要添加Module。</br>
    Module的目录结构形式，以及描述文件MOD形式如下图：</br>
</font>
  
