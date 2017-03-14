## SurfaceView
- App端它仍在View hierachy中，但在Server端（WMS和SF）中，它与宿主窗口是分离的。
- Surface的渲染可以放到单独线程去做

## GLSurfaceView
- SurfaceView的一种典型使用模式。在SurfaceView的基础上，它加入了EGL的管理，并自带了渲染线程。

## SurfaceTexture
- 作为一个图像流的处理类，用来生成纹理供GLSurfaceView或TextureView来使用
- 从图像流中获取帧内容作为OpenGL的纹理，因此可用于图像流数据的二次处理（如Camera滤镜，桌面特效等）
- 图像流可以来源于摄像头和视频解码


## TextureView
- 用来显示内容流，比如视频和OpenGL场景
- 可以在应用进程操作也可在远程进程
- 只能用来硬件加速窗口
- 作为一个通用的view，它不会创建分离的窗口，这意味着可以像常用的view一样移动、绽放


