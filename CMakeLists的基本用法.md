# CMakeLists的基本用法

## CMake

- CMake是跨平台自动化构建系统（不管是Windows，Linux，还是Mac OS），不依赖特定的编辑器，可以支持多层目录，多应用程序与多个库（**比较方便进行大型项目构建**）。
- CMakeList是CMake用于构建Makefile或者projects/workspace的配置文件。也就是说，我们不需要关注不同的Make工具需要的不同格式的MakeFile文件，而是直接使用CMake构建出适应当前平台的Makefile进二进行代码编译。
- **CMakeList其实就是适配CMake语法的一个配置文件。**

## 如何编写CMakeList

- 以下是一个CMakeLists.txt的基本实例

```txt
#工程目录
----build
----include
----library
----util
----src
CMakeLists.txt

#cmakelist中，所有的相关语法命令是大小写不敏感的


#以下为一个完整的CMakeLists.txt目录
#cmake 编译相关
cmake_minimum_required(version 2.8) #cmake 最低版本要求，一般都是2.8往上，最好和目标平台的cmake版本一致
project(demo) #定义工程名称,这里用demo作为工程名称
message(status "Project Directory: ${PROJECT_SOURCE_DIR}") #打印相关消息消息，可以用来检查相关设置是否正确
set(cmake_build_type DEBUG)                      #指定编译类型 DEBUG/RELEASE
set(cmake_c_flags_debug "-g -Wall) # 指定编译器
add_compile_options(-std=gnu++11)  #添加编译选项，一些具体的编译选项大家可以自己查一下

option(_LINUX "build the project on linux " ON) #设置option，可以根据option从而选择代码中的宏定义部分
if(_LINUX)
    add_definitions("-D_LINUX") 
endif()

#工程配置相关，需要根据实际情况进行调整
include_directories(${CMAKE_SOURCE_DIR}/include) #添加引用的头文件目录，这里是相对目录的形式
link_directories(${CMAKE_SOURCE_DIR}/library) #添加引用的库文件目录，这里是相对目录的形式
add_subdirectory(${CMAKE_SOURCE_DIR}/util) #当需要构建大型工程，各个子目录都有对应的CMakeList时，使用该条语法
aux_source_directories(${CMAKE_SOURCE_DIR}/src DIR_SRC) #添加需要编译源文件到DIR_SRC变量

#生成可执行文件
add_executable(demo ${DIR_SRC})  #设置生成的可执行文件名字，并且把可执行文件和编译源文件关联
target_link_library(demo lib1,lib2,lib3) #上面只是link了库文件所在的目录，那么这里就是把具体的库和可执行文件相关联

#生成库文件
add_library(demo SHARED ${DIR_SRC}) #这里生成库文件有两种形式，一种是STATIC 静态库，一种是SHARED 共享库，如果需要跨硬件运行，一般是生成共享库
target_link_library(demo lib1,lib2,lib3)
```

