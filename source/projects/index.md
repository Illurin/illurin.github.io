---
title: 项目
date: 2022-12-6 22:08:00
---

我的主要研究方向是计算机图形学/游戏引擎设计，可以在此处找到一些我做的个人项目。

# Vulkan Graphics Engine

<font size=3>基于Vulkan的渲染框架。</font>

![](https://github.com/Illurin/VulkanGraphicsEngine/blob/engine/Information/%E6%BC%94%E7%A4%BA%E5%9B%BE%E7%89%877.png?raw=true)

该项目于三年前开发而成，目前尚无维护计划。

<font size=5><i class="fa-brands fa-github-alt"></i> [Github链接](https://github.com/Illurin/VulkanGraphicsEngine)</font>

# Soft Renderer

<font size=3>
A pipeline-like software rendering frame

仿图形渲染管线设计的CPU软渲染器。
</font>

已实现功能：

* 基于SDL2的窗口显示和绘制
* 基础光栅化算法，三维空间内绘制点，线，三角形
* Camera摄像机自由移动功能
* 深度缓冲和基于绕序的背面剔除
* 纹理映射（最近邻过滤和线性过滤）和各种纹理寻址模式
* 基本的基于Alpha分量的颜色混合
* 基本的Blinn-Phong和BRDF光照算法
* 基本的MSAA反走样算法
* 曲面细分，曲面简化，生成曲线/曲面

待完善功能：

* 建立完备的数学库
* 纹理Mipmap
* 完整的几何细分和LOD支持

<font size=5><i class="fa-brands fa-github-alt"></i> [Github链接](https://github.com/Illurin/SoftRenderer)</font>