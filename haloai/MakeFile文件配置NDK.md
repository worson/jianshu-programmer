
## Android.mk 示例
```
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)

OPENCV_LIB_TYPE:=STATIC #SHARED
include C:\files\OpenCV-android-sdk\sdk\native\jni\OpenCV.mk

#枚举源文件，以空格分隔多个文件：
LOCAL_SRC_FILES  := HaloECP.cpp algorithm.cpp CrossRoad.cpp FileDataEnginePlaceholder.cpp LinkFileInfo.cpp MergeMapData.cpp NaviFile.cpp

LOCAL_C_INCLUDES += $(LOCAL_PATH)
LOCAL_C_INCLUDES += C:\files\OpenCV-android-sdk\sdk\native\jni\include\
LOCAL_LDLIBS     := -llog -ldl -llibPath
# 存储您要构建的模块的名称
LOCAL_MODULE     := HaloECP
LOCAL_PROGUARD_ENABLED:= disabled
# 帮助系统将所有内容连接到一起,脚本确定要构建的内容及其操作方法。
include $(BUILD_SHARED_LIBRARY)
```

