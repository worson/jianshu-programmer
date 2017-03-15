
## Android.mk 示例
示例1
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

示例2
```
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)

$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d)
$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d/external)
$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d/cocos)
$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d/cocos/audio/include)

LOCAL_MODULE := MyGame_shared

LOCAL_MODULE_FILENAME := libMyGame

LOCAL_SRC_FILES := hellocpp/main.cpp \
                   ../../../Classes/AppDelegate.cpp \
                   ../../../Classes/HelloWorldScene.cpp

LOCAL_C_INCLUDES := $(LOCAL_PATH)/../../../Classes

# _COCOS_HEADER_ANDROID_BEGIN
# _COCOS_HEADER_ANDROID_END


LOCAL_STATIC_LIBRARIES := cocos2dx_static

# _COCOS_LIB_ANDROID_BEGIN
# _COCOS_LIB_ANDROID_END

include $(BUILD_SHARED_LIBRARY)

$(call import-module,.)

# _COCOS_LIB_IMPORT_ANDROID_BEGIN
# _COCOS_LIB_IMPORT_ANDROID_END
```
## Application.mk 示例

```
APP_STL := gnustl_static

APP_CPPFLAGS := -frtti -DCC_ENABLE_CHIPMUNK_INTEGRATION=1 -std=c++11 -fsigned-char
APP_LDFLAGS := -latomic

APP_ABI := armeabi


ifeq ($(NDK_DEBUG),1)
  APP_CPPFLAGS += -DCOCOS2D_DEBUG=1
  APP_OPTIM := debug
else
  APP_CPPFLAGS += -DNDEBUG
  APP_OPTIM := release
endif

```
