# Rajawali 微小 OpenGL 开源库介绍

&gt; 开发一些纯粹的渲染项目时，你肯定要用到OpenGL，安卓平台本来已支持原生的OpenGL，不过那只是一个底层架构，并没有一套适合快速开发框架。当然你可以能说可以用游戏引擎啊，这个我们也想过，主要是我们的需求只需要简单的渲染功能，要求的是\*\*速度快、体积小、占用资源少\*\*。满足这个需求的，我这里推荐Rajawali这个OpenGL库。



\[仓库地址\]\(https://github.com/Rajawali/Rajawali\)

\# 一、Rajawali 介绍

Rajawali是基于java的开源库，在同类库中人气最高的一个库，github上已经有一千多个赞，五百多次fork，而且社区维护还很频繁，目前还有AR的一些组件正在开发当中。

以下主要讲讲Rajawali 相对 OpenGL 做了哪些事情：

\#\# OpenGL ES

首先了解下OpenGL ES的基本框架

!\[OpenGL 结构\]\(http://upload-images.jianshu.io/upload\_images/4143184-942d75371325255c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240\)

在安卓中需要一个SurfaceView来指定绘图区域，渲染过程中每帧会回调一次进行渲染动作。OpenGL ES框架如上图所示，支持直接Shader 程序的开发，提供VBO等供存储顶点等图元数据。

\#\# Rajawali



!\[Rajawali 结构图\]\(http://upload-images.jianshu.io/upload\_images/4143184-b25ab4425306ac46.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240\)

如上图，Rajawali 相对 OpenGL 主要做了以下几件事。

- 提供场景的概念，支持动画、摄像头，最主要的场景是所有UI树的根节点

- 封装了3D模型，支持立方体、圆柱等等基本图形

- 提供材质的概念，并直接封装了纹理、着色器程序



因此包装了OpenGL 编译Shader、申请VBO、渲染， 写一个简单3D效果时，可能只是需要几十行代码，关键是直接避开了OpenGL流程化的底层代码，而是面向业务逻辑开发。





\# 二、Rajawali 效果

抛砖引玉，提供几张效果图给大家了解下，有兴趣的话clone 仓库即可学习作者提供的几十个例程。

\#\# 1、批量加载纹理，性能扛扛

!\[2000Pictures.gif\]\(http://upload-images.jianshu.io/upload\_images/4143184-71b45e75a9a85427.gif?imageMogr2/auto-orient/strip\)



\#\# 2、加载3D模型，支持光照效果

!\[光照效果.gif\]\(http://upload-images.jianshu.io/upload\_images/4143184-b490c12977809284.gif?imageMogr2/auto-orient/strip\)

