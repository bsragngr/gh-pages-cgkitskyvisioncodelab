---
title: Getting started
description: 5
---

## **Integrating HMS SDK**

**1. Create a Native C++ Android Studio Project**

- Create a project named as “**XXX”** in Android Studio, and select **Native C++**.

- The directory tree is as follows: 

  <div style="padding: 5px"><img style="width: 250.00px ; padding: 5px" src="https://raw.githubusercontent.com/bsragngr/gh-pages-cgkitskyvisioncodelab/gh-pages/assets/cg1.png">
  </div>
  
  

**2.  Modify the app/build.gradle file to specify the C++ file for CMake build.**

- Create the build dependencies of CMake in the **/app/build.gradle** file (in **externalNativeBuild** at the same level as **defaultConfig** under **Android**):

  ![](C:\Users\b00568925\Desktop\gh-pages-cgkitcodelab\assets\cg2.png)

- Configure the **NDK ABI** filter:

  ![](C:\Users\b00568925\Desktop\gh-pages-cgkitcodelab\assets\cg3.png)

**3. Copy libraries and header files.**

- Download the [SDK package](https://developer.huawei.com/consumer/en/doc/HMSCore-Library-V5/sdk-download-0000001050441521-V5) and unzip it. 

- Copy the SDK header files to the resource library.

  Copy the header files in the SDK package to the **src/main/cpp/include** directory in Android Studio.

  ![](C:\Users\b00568925\Desktop\gh-pages-cgkitcodelab\assets\cg4.png)

- Copy the .so files in the SDK package to the resource library.

  Copy **libs\arm64-v8a\libcgkit.so** and **libs\armeabi-v7a\libcgkit.so** in the SDK package to **libs/arm64-v8a** and **/libs/armeabi-v7a** in Android Studio, respectively.

   ![](C:\Users\b00568925\Desktop\gh-pages-cgkitcodelab\assets\cg5.png)

  

-  Overwrite the **CMakeLists.txt** file in **app/src/main/cpp** with the following code. The **CGRenderingFramework** folder name can user-defined.`

  ```
  cmake_minimum_required(VERSION 3.4.1)
  include_directories(
          ${CMAKE_SOURCE_DIR}/include/CGRenderingFramework )
  include_directories(
          ${CMAKE_SOURCE_DIR}/include/MainApplication )
  add_library(
          main-lib
          SHARED
          source/Main.cpp
          source/MainApplication.cpp)
  ADD_LIBRARY(
          cgkit
          SHARED
          IMPORTED)
  set_target_properties(cgkit
          PROPERTIES IMPORTED_LOCATION
          ${CMAKE_SOURCE_DIR}/../../../libs/${ANDROID_ABI}/libcgkit.so
          )
  SET(
          VULKAN_INCLUDE_DIR
          "$ENV{VULKAN_SDK}/include")
  #"${ANDROID_NDK}/sources/third_party/vulkan/src/include")
  include_directories(${VULKAN_INCLUDE_DIR})
  SET(
          NATIVE_APP_GLUE_DIR
          "${ANDROID_NDK}/sources/android/native_app_glue")
  FILE(
          GLOB NATIVE_APP_GLUE_FILLES
          "${NATIVE_APP_GLUE_DIR}/*.c"
          "${NATIVE_APP_GLUE_DIR}/*.h")
  ADD_LIBRARY(native_app_glue
          STATIC
          ${NATIVE_APP_GLUE_FILLES})
  TARGET_INCLUDE_DIRECTORIES(
          native_app_glue
          PUBLIC
          ${NATIVE_APP_GLUE_DIR})
  find_library(
          log-lib
          log )
  target_link_libraries(
          main-lib
          cgkit
          native_app_glue
          android
          ${log-lib} )
  SET(
          CMAKE_SHARED_LINKER_FLAGS
          "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")
  ```

- After that don’t forget to click **Sync Project with Gradle Files**.

Now, you’re set up, and ready.

