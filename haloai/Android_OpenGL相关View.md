# TextureView
- 用来显示内容流，比如视频和OpenGL场景
- 可以在应用进程操作也可在远程进程
- 只能用来硬件加速窗口
- 作为一个通用的view，它不会创建分离的窗口，这意味着可以像常用的view一样移动、绽放
# SurfaceTexture
- 从图像流只获取帧内容作为OpenGL的纹理
- 图像流可以来源于摄像头和视频解码

# GLSurfaceView