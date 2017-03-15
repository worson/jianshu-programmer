
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

```
productFlavors {
    arm7 {
        // in the future, ndk.abiFilter might also work
        ndk {
            abiFilter 'armeabi-v7a'
        }
    }
    arm8 {
        ndk {
            abiFilters 'arm64-v8a'
        }
    }
    arm {
        ndk {
            abiFilter 'armeabi'
        }
    }
    x86 {
        ndk {
            abiFilter 'x86'
        }
    }
    x86_64 {
        ndk {
            abiFilter 'x86_64'
        }
    }
    mips {
        ndk {
            abiFilters 'mips', 'mips64'
        }
    }
    universal {
        ndk {
            abiFilters 'mips', 'mips64', 'x86', 'x86_64'
        }
    }
    }
```

