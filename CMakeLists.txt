# 指定 cmake 版本，预防某些用户使用较低版本的来编译该项目
cmake_minimum_required(VERSION 3.2)

# 指定一个项目名称，后面可以通过 `${PROJECT_NAME}` 来引用
PROJECT(my_project)

# 指定头文件目录，改参数为头文件所在的文件夹名字
INCLUDE_DIRECTORIES(include)

# 源文件目录
AUX_SOURCE_DIRECTORY(src DIR_SRCS)

# 选择性设置环境变量，然后通过 ${CUSTOM_VAR} 来引用
# SET(CUSTOM_VAR ${DIR_SRCS})

# 添加需要编译的源文件 test.cpp 和 输出的可执行文件名字 exe_main
# ADD_EXECUTABLE(${PROJECT_NAME} ${DIR_SRCS})

# 设置一个动态库名字，因为 `ADD_LIBRARY` 中的参数不给设置字符常量
SET(LIB_NAME statictest)

# 生成一个库
#ADD_LIBRARY(a
# 			SHARED
# 			src/a.cpp include/a.h)

# 连接一个现有的库
# 这种方法是可以的
LINK_DIRECTORIES(lib)

# 其它博客有这样引用第三方库的，我这儿却行不通
# 我暗定 ADD_LIBRARY() 不通常用来链接一个第三方库
# ADD_LIBRARY(${LIB_NAME}
# 			SHARED
# 			IMPORTED)

#SET_TARGET_PROPERTIES(${LIB_NAME}
#        PROPERTIES IMPORTED_LOCATION 
#        lib/libdytest.dylib)

# 添加需要编译的源文件 test.cpp 和 输出的可执行文件名字 exe_main
ADD_EXECUTABLE(exe_main 
			src/test.cpp)

# 连接
TARGET_LINK_LIBRARIES(exe_main 
					${LIB_NAME}
					a)
