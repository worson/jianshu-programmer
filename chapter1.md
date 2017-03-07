# OpenGL 教程(1)：Android OpenGL ES 之画三角形

> 本文主要介绍入门基于Android OpenGL ES的Hello world工程基本环境搭建。

![效果图](http://upload-images.jianshu.io/upload_images/4143184-b3c718a5b70a446d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 概要
- 编译OpenGL 程序
- 配置相关顶点数据
- 绘制操作

# 介绍
使用OpenGL绘制图形时，类似向服务器发起各种绘制的请求，本地端代码其实就是围绕着如何发起请求、组织数据，因此OpenGL其实是一个大的状态机，接收各种指令而进行绘制操作。

#编译OpenGL 程序
既然OpenGL是在服务器端运行的，它肯定也需要运行代码的。OpenGL的代码是由本地提交源文件，进行编译、连接、运行的，这和C语言的运行的流程是一致的。
OpenGL上运行代码分为顶点着色器和片段着色器，顶点着色器是告诉GPU三角形的三个顶点是在哪里画，片段着色器是告诉GPU这个三角形中每个像素是要画成什么样的颜色。如何来表示这个逻辑，OpenGL用的是自己的GLSL语言，这其实也跟C语言是差不多的。
```
version 300 es 			 
in vec4 vPosition;          
void main()                 
 {                            
    gl_Position = vPosition;  
}  
```
以上是顶点着色器的代码，“gl_Position = vPosition ”中，gl_Position 是内置变量，其实就是告诉CPU当前要在哪个位置顶点。编译一个OpenGL 代码实现如下：
```
String vShaderStr =
   "#version 300 es 			  \n"
   +   "in vec4 vPosition;           \n"
   + "void main()                  \n"
   + "{                            \n"
   + "   gl_Position = vPosition;  \n"
   + "}                            \n";

String fShaderStr =
   "#version 300 es		 			          	\n"
   + "precision mediump float;					  	\n"
   + "out vec4 fragColor;	 			 		  	\n"
   + "void main()                                  \n"
   + "{                                            \n"
   + "  fragColor = vec4 ( 1.0, 0.0, 0.0, 1.0 );	\n"
   + "}                                            \n";

int vertexShader;
int fragmentShader;
int programObject;
int[] linked = new int[1];

// Load the vertex/fragment shaders
vertexShader = LoadShader ( GLES30.GL_VERTEX_SHADER, vShaderStr );
fragmentShader = LoadShader ( GLES30.GL_FRAGMENT_SHADER, fShaderStr );

// Create the program object
programObject = GLES30.glCreateProgram();

if ( programObject == 0 )
{
   return;
}

GLES30.glAttachShader ( programObject, vertexShader );
GLES30.glAttachShader ( programObject, fragmentShader );

// Bind vPosition to attribute 0
GLES30.glBindAttribLocation ( programObject, 0, "vPosition" );

// Link the program
GLES30.glLinkProgram ( programObject );

// Check the link status
GLES30.glGetProgramiv ( programObject, GLES30.GL_LINK_STATUS, linked, 0 );

if ( linked[0] == 0 )
{
   Log.e ( TAG, "Error linking program:" );
   Log.e ( TAG, GLES30.glGetProgramInfoLog ( programObject ) );
   GLES30.glDeleteProgram ( programObject );
   return;
}
```
其中加载编译任一着色器代码如下：
```
private int LoadShader ( int type, String shaderSrc )
   {
      int shader;
      int[] compiled = new int[1];

      // Create the shader object
      shader = GLES30.glCreateShader ( type );

      if ( shader == 0 )
      {
         return 0;
      }

      // Load the shader source
      GLES30.glShaderSource ( shader, shaderSrc );

      // Compile the shader
      GLES30.glCompileShader ( shader );

      // Check the compile status
      GLES30.glGetShaderiv ( shader, GLES30.GL_COMPILE_STATUS, compiled, 0 );

      if ( compiled[0] == 0 )
      {
         Log.e ( TAG, GLES30.glGetShaderInfoLog ( shader ) );
         GLES30.glDeleteShader ( shader );
         return 0;
      }

      return shader;
   }
```
以上的所有操作就是给GPU准备一个可供着色器运行的程序，但是目前仍没有上传数据。

## 上传渲染数据
###说明
上传给着色器的数据分为两种：
**属性数据(Attribute)：**如顶点位置、纹理坐标、用于光线计算的表面法线用于计算屏幕上每个顶点的最终位置，针对每个顶点着色器都会执行一次
**Uniform数据：** 我在理解中，属性数据如果相当于常量数据，那么Uniform相当于程序中的变量，每次渲染时CPU都可以给其上传一个新的值供着色器使用
### 上传数据
要上传数据给CPU，需要先绑定顶点着色器的位置：
```
GLES30.glBindAttribLocation ( programObject, 0, "vPosition" );
```
以上绑定程序programObject顶点着色器的vPosition属性变量的标识下标为0，该下标是对vPosition操作的标识，接下来上传顶点数据 ：
```
GLES30.glVertexAttribPointer ( 0, 3, GLES30.GL_FLOAT, false, 0, mVertices );
GLES30.glEnableVertexAttribArray ( 0 );
```
glVertexAttribPointer用来上传顶点数据
```
public static void glVertexAttribPointer(
        int indx,
        int size,
        int type,
        boolean normalized,
        int stride,
        java.nio.Buffer ptr
    )
```
上传数据的参数比较多，涵义如下：
```
int index,//属性数据下标位置，也就是之前绑定的下标
int size,//每个顶点有多少个分量与其关联，如果只使用(x,y)，那就是2
int type,//顶点的数据类型
boolean normalized,//type为整形有意义
int stride,//一个数据存储于多个属性时，表示每个顶点的跨距
java.nio.Buffer ptr//数据区
```
## 绘制图形
直接使用顶点数据不使用VBO来绘制使用的是：
```
void glDrawArrays(	GLenum  	mode,
 	GLint  	first,
 	GLsizei  	count);
```
对应在本程序中使用：
```
GLES30.glDrawArrays ( GLES30.GL_TRIANGLES, 0, 3 );
```
mode 指绘制模式，包括点、线、三角形等方式
first 指原来顶点数据的以指定的size（3）切分之后的起始坐标
count 指绘制3个三个形

##结语
[示例代码](http://download.csdn.net/detail/wsx1048/9772672)
