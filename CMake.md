# CMake
## 创建CMakeLists.txt文件
`touch CMakeLists.txt`
## Cmake语法
* 基本信息
```cmake
#指定cmake支持的最低版本
cmake_minimum_required(VERSION 3.3.0)
# 定义工程名称等信息
project(my_project
VERSION 1.0
DESCRIPTION "Description for this project."
HOMEPAGE_URL "https://github.com/**"
LANGUAGES CXX)
```
* 变量 set()
```cmake
# 使用set() 字符串存储到SRC_LIST中,使用${SRC_LIST}将变量转换回字符串
set(SRC_LIST a.cpp b.cpp)
```
* 预定义宏 add_definitions()
```cmake
#添加_DEBUG宏，相当于源码中添加 #define DEBUG
add_definitions(-D_DEBUG) 
```
以下是CMake中常用的预定义宏，需要使用set指定其值
![预定义宏](pic/CMake/marco.png)
```cmake
# 指定C++标准
set(CMAKE_CXX_STANDARD 14)
# 指定编译类型
set(CMAKE_BUILD_TYPE Debug)
# 指定可执行文件输出目录
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/bin)
# 指定动态库输出目录(Linux)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin) 
# 指定静态库输出目录(Linux)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin) 
# 指定动态/静态库输出目录(Windown)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin) 
```
* 文件搜索 file()和aux_source_directory()
```cmake
# 搜索路径下对应后缀文件,将目录下搜索到的某一类型文件存储到列表中
# GLOB/GLOB_RECURSE是否递归搜索
file(GLOB SRC_LISTS ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp) 
# 搜索路径下所有文件,将目录下搜索到的所有文件存储到列表中
aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR}/src SRC_LISTS) #
```
* 添加包含目录 include_directories()
```cmake
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
```
* 生成动/静态库 add_library()
```cmake
# 库名称：name，bin目录下生成的动态库名称为libname.so/libname.a
# 动态库 SHARED / 静态库 STATIC
add_library(name SHARED ${LIB_SRC_LISTS})
```
* 生成可执行文件 add_executable()
```cmake
# 生成与项目名称相同的可执行文件
add_executable(${PROJECT_NAME} ${DEMO_SRC_LISTS})
```
* 链接动态库 target_link_libraries()
```cmake
# 链接动态库要在生成可执行文件之后进行，本例${PROJECT_NAME}链接了三个动态库目录（实际不止三个）
target_link_libraries(${PROJECT_NAME} ${LIB_KEYSTONE} ${LIB_CBDETECT} ${OpenCV_LIBS})
```
* 添加子目录 add_subdirectory()
```cmake
# 子目录下必须有CMakeLists.txt文件，该命令会执行子目录下的CMake文件指令
# 父目录的变量可以单向传递到子目录，即父目录的变量在子目录也是生效的
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/3rd/libcbdetect)
```
* 消息输出 message()
```cmake
# STATUS：输出状态信息，默认情况下这些信息不会被当作错误处理
# WARNING：输出警告信息，通常表示可能存在但不致命的问题
# SEND_ERROR: 输出错误信息，但会继续CMake配置
# FATAL_ERROR：输出致命错误信息，停止生成步骤并中断CMake配置
message(STATUS "I am OK!")
```
* 条件判断if()-else()-endif()
```cmake
# 判断文件或者目录是否存在
if(EXISTS path-to-file-or-directory)
# 判断是不是目录
if(IS_DIRECTORY path)
# 判断是不是绝对路径
if(IS_ABSOLUTE path)
# 比较两个路径是否相等
if(<variable|string> PATH_EQUAL <variable|string>)
# 字符串比较
if(<variable|string> STREQUAL <variable|string>)
# 举例，如果CMAKE_BUILD_TYPE为Debug则添加一个_DEBUG宏
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_definitions(-D_DEBUG) # 添加_DEBUG宏    
    message(STATUS "_DEBUG Macro Added!")
else()
    message(STATUS "_DEBUG Macro Not Added!")
endif()
```
* 添加OpenCV库
```cmake
# lib目录：${OpenCV_LIBS}
# include目录：${OpenCV_INCLUDE_DIRS}
find_package(OpenCV REQUIRED)
if(OPENCV_FOUND)
    include_directories(${OpenCV_INCLUDE_DIRS}) #添加包含目录
    message(STATUS "OpenCV Found!")
else()
    message(SEND_ERROR "Can not find OpenCV Modules!!!")
endif()
``` 
