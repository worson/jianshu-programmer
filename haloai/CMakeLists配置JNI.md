
## 指定外部编译工具
在build.gradle中
```
defaultConfig {
        applicationId 'com.example.hellojni'
        minSdkVersion 15
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        externalNativeBuild {
            cmake {
                arguments '-DANDROID_TOOLCHAIN=clang'
            }
        }
    }
```

```
externalNativeBuild {
        cmake {
            path "src/main/cpp/CMakeLists.txt"
        }
    }
```