## Makefile



`.PHONY`

伪目标是这样一个目标：它不代表一个真正的文件名，在执行make时可以指定这个目标来执行所在规则定义的命令，有时也可以将一个伪目标称为标签。伪目标通过PHONY来指明。

## CMAKE

https://www.hahack.com/codes/cmake/



`project (Demo4)`  项目信息

`message("1.PROJECT_BINARY_DIR = ${PROJECT_BINARY_DIR}")` 打印信息

`set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/modules")` 设置变量值



`aux_source_directory(. DIR_SRCS)` 查找目录下的所有源文件将名称保存到 DIR_SRCS 变量

`add_executable(Demo ${DIR_SRCS}) `指定生成目标

`add_subdirectory(math)` 添加 math 子目录

`target_link_libraries(Demo MathFunctions)` 添加链接库



`option (USE_MYMATH "Use provided math implementation" ON)`



`configure_file (`

 `"${PROJECT_SOURCE_DIR}/config.h.in"`

 `"${PROJECT_BINARY_DIR}/config.h"`

 `)`



`include_directories ("${PROJECT_SOURCE_DIR}/math")`

将给定目录添加到编译器用于搜索包含文件的目录中。相对路径被解释为相对于当前源目录

`add_dependencies(jvpp_${name} jvpp_common jvpp_registry japigen-${name})`



`execute_process` 调用shell命令或脚本



`function` 定义一个可在CMake脚本其他位置调用的函数。

```
function(<name>[arg1 [arg2 [arg3 ...]]])
  COMMAND1(ARGS ...)
  COMMAND2(ARGS ...)
  ...

endfunction(<name>)
```

######  `string(REGEX REPLACE <match-regex> <replace-expr> <out-var> <input>...)`



STRING(REGEX REPLACE "\n" ";" corefiles "${corefiles}")



`find_package`

假设此时我们需要引入glog库来进行日志的记录，我们在Module目录下并没有找到 FindGlog.cmake。所以我们需要自行安装glog库，再进行引用。

安装完成后

此时我们便可以通过与引入curl库一样的方式引入glog库了

```cmake
find_package(GLOG)
add_executable(glogtest glogtest.cc)
if(GLOG_FOUND)
    # 由于glog在连接时将头文件直接链接到了库里面，所以这里不用显示调用target_include_directories
    target_link_libraries(glogtest glog::glog)
else(GLOG_FOUND)
    message(FATAL_ERROR ”GLOG library not found”)
endif(GLOG_FOUND)
```







使用命令

`ccmake .` 设置变量值











**语法：** SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]]) 
**指令功能:** 用来显式的定义变量 
**例子:** SET (SRC_LST main.c other.c) 
**说明:** 用变量代替值，例子中定义SRC_LST代替后面的字符串。



```
1，set(libs "${CMAKE_SOURCE_DIR}/src/main/jnilibs")

其中CMAKE_SOURCE_DIR 是一个cmake内置变量，指定了CMakeLists.txt所在的目录。详细介绍可参考：http://www.cnblogs.com/xianghang123/p/3556425.html。
```

