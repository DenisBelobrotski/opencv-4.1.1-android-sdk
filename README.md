# opencv-4.1.1-android-sdk
OpenCV 4.1.1 build for Android

For linking OpenCV sdk in your native CMake powered library you need:

1. Add to "build.gradle" file the following lines:
```gradle

defaultConfig {
        ........

        externalNativeBuild {
            cmake {
                cppFlags "-fexceptions", "-frtti"
                arguments "-DANDROID_STL=c++_shared"
            }
        }
    }
.........

sourceSets {
        main {
            jniLibs.srcDirs = jniLibs.srcDirs + ['{PATH_TO_THE_REPOSITORY}' + '/sdk/native/libs']
        }
    }

```

2. Add to "CMakeLists.txt" file the following lines:
```cmake

..........

set(OpenCV_DIR {PATH_TO_THE_REPOSITORY}/sdk/native/jni)
set(ANDROID_OPENCV_COMPONENTS "opencv_java" CACHE STRING "")
find_package(OpenCV REQUIRED COMPONENTS ${ANDROID_OPENCV_COMPONENTS})
..........

target_link_libraries(.........
                      ${ANDROID_OPENCV_COMPONENTS})

```
