## 常用命令说明

1. `cmake_minimum_required (VERSION 2.8)`：指定运行此配置文件所需的 CMake 的最低版本；
2. `project (Demo1)`：参数值是 `Demo1`，该命令表示项目的名称是 `Demo1` 。
3. `add_executable(Demo main.cc)`： 将名为 [main.cc](http://main.cc/) 的源文件编译成一个名称为 Demo 的可执行文件。
4. `cuda_add_executable`  
5. `add_subdirectory(math)`: 添加math子目录
6. `aux_source_directory` ：查找指定目录下的所有源文件，然后将结果存进指定变量名
7. `target_link_libraries`： 链接静态库和动态库，相当于指定-l参数
8. `link_libraries`:   **添加需要链接的库文件路径，注意这里是全路径**

```
1，link_libraries用在add_executable之前，target_link_libraries用在add_executable之后

2，link_libraries用来链接静态库，target_link_libraries用来链接导入库，即按照header file + .lib + .dll方式隐式调用动态库的.lib库
```



1. `include_directories` ： 指定头文件的搜索路径，相当于指定gcc的-I参数

2. `link_directories`：动态链接库或静态链接库的搜索路径，相当于gcc的-L参数

3. `configure_file`: 命令用于加入一个配置头文件 config.h ，这个文件由 CMake 从 [config.h.in](http://config.h.in/) 生成，通过这样的机制，将可以通过预定义一些参数和变量来控制代码的生成。

   ```
   # 加入一个配置头文件，用于处理 CMake 对源码的设置
   configure_file (
     "${PROJECT_SOURCE_DIR}/config.h.in"
     "${PROJECT_BINARY_DIR}/config.h"
     )
   ```

4. `find_path(<VAR> name1[path1 path2 …])`:该命令在参数path*指示的目录中查找文件name1并将查找到的路径保存在变量VAR中(其中使用”[…]”包含的项表示可忽略项，使用”…|…”分割的项表示只能选择其中一项)；

5. `find_library(${var} NAMES name1[name2 …] PATHS path1 [path2 …] PATH_SUFFIXES suffix1 [uffix2 …]):`搜索一个外部的链接库文件,并将结果的全部路径保存到var变量中。要搜索的链接库文件名字可能是name1,name2等；搜索路径为path1, path2等；此外还可以指定路径的后缀词为suffix1,suffix2等；

6. `find_package(name):`在指定的模块目录中搜索一个名为`Find<name>.cmake`(例如，FindOSG.cmake)的CMake脚本模块文件，执行其中的内容，意图搜索到指定的外部依赖库头文件和库文件位置；

7. `add_library`: 将指定的源文件生成链接文件，然后添加到工程中去

```
add_library(<name> [STATIC | SHARED | MODULE]
            [EXCLUDE_FROM_ALL]
            [source1] [source2] [...])
            
其中<name>表示库文件的名字，该库文件会根据命令里列出的源文件来创建。而STATIC、SHARED和MODULE的作用是指定生成的库文件的类型。STATIC库是目标文件的归档文件，在链接其它目标的时候使用。SHARED库会被动态链接（动态链接库），在运行时会被加载。MODULE库是一种不会被链接到其它目标中的插件，但是可能会在运行时使用dlopen-系列的函数。默认状态下，库文件将会在于源文件目录树的构建目录树的位置被创建，该命令也会在这里被调用。
而语法中的source1 source2分别表示各个源文件。
```

8. `message`  打印消息，在控制台或者对话框输出一行或多行调试信息
9. `set_target_properties` 用来设置输出的名称，对于动态库，还可以用来指定动态库版本和API版本
10. `configure_file(infile outfile)`  将文件infile复制到outfile的位置，同时执行其中变量的自动配置和更替;

## 内置变量、环境变量：

1.  `CMAKE_C_COMPILER`: 指定C编译器；
2. `CMAKE_CXX_COMPILER` 指定C++编译器 ;
3. `CMAKE_C_FLAGS`: 指定编译C文件时的编译选项，如-g，也可以通过add_definitions添加编译选项；
4. `  CMAKE_CXX_FLAGS` 设置C++编译选项；
5. `CMAKE_BUILD_TYPE`  build类型(Debug,Release,…),CMAKE_BUILD_TYPE=Debug;
6. `CMAKE_COMMAND`  也就是CMake可执行文件本身的全路径
7. ` CMAKE_DEBUG_POSTFIX`  Debug版本生成目标的后缀，通常可以设置为”d”字符
8. ` CMAKE_GENERATOR` 编译器名称，例如”UnixMakefiles”, “Visual Studio 7”等；
9. `CMAKE_INSTALL_PREFIX` 工程安装目录，所有生成和调用所需的可执行程序，库文件，头文件都会安装到该路径下，Unix/Linux下默认为/usr/local, windows下默认为C:\Program Files;
10. `CMAKE_CURRENT_SOURCE_DIR` 指的是当前处理的CMakeLists.txt所在的路径；
11. `CMAKE_CURRENT_BINARY_DIR`:如果是in-source编译，则跟`CMAKE_CURRENT_SOURCE_DIR`一致；如果是out-of-source，指的是target编译目录；
12. `CMAKE_CURRENT_LIST_FILE`: 输出调用这个变量的CMakeLists.txt的完整路径；
13. 

```
1,CMAKE_BINARY_DIR
  PROJECT_BINARY_DIR
 <projectname>_BINARY_DIR
这三个变量指代的内容是一致的,如果是 in source 编译,指得就是工程顶层目录,如果是 out-of-source 编译,指的是工程编译发生的目录。PROJECT_BINARY_DIR 跟其他指令稍有区别,现在,你可以理解为他们是一致的。
2,CMAKE_SOURCE_DIR
   PROJECT_SOURCE_DIR
   <projectname>_SOURCE_DIR
这三个变量指代的内容是一致的,不论采用何种编译方式,都是工程顶层目录。
也就是在 in source 编译时,他跟 CMAKE_BINARY_DIR 等变量一致。
PROJECT_SOURCE_DIR 跟其他指令稍有区别,现在,你可以理解为他们是一致的。

3,CMAKE_CURRENT_SOURCE_DIR
指的是当前处理的 CMakeLists.txt 所在的路径,比如上面我们提到的 src 子目录。

4,CMAKE_CURRRENT_BINARY_DIR
如果是 in-source 编译,它跟 CMAKE_CURRENT_SOURCE_DIR 一致,如果是 out-of-source 编译,他指的是 target 编译目录。
使用我们上面提到的 ADD_SUBDIRECTORY(src bin)可以更改这个变量的值。
使用 SET(EXECUTABLE_OUTPUT_PATH <新路径>)并不会对这个变量造成影响,它仅仅修改了最终目标文件存放的路径。

5,CMAKE_CURRENT_LIST_FILE
输出调用这个变量的 CMakeLists.txt 的完整路径

 

6,CMAKE_CURRENT_LIST_LINE
输出这个变量所在的行

 

7,CMAKE_MODULE_PATH
这个变量用来定义自己的 cmake 模块所在的路径。如果你的工程比较复杂,有可能会自己编写一些 cmake 模块,这些 cmake 模块是随你的工程发布的,为了让 cmake 在处理CMakeLists.txt 时找到这些模块,你需要通过 SET 指令,将自己的 cmake 模块路径设置一下。
比如
SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
这时候你就可以通过 INCLUDE 指令来调用自己的模块了。

8,EXECUTABLE_OUTPUT_PATH 和 LIBRARY_OUTPUT_PATH
分别用来重新定义最终结果的存放目录,前面我们已经提到了这两个变量。

9,PROJECT_NAME
返回通过 PROJECT 指令定义的项目名称。
```































```
内部变量

CMAKE_C_COMPILER：指定C编译器

CMAKE_CXX_COMPILER：

CMAKE_C_FLAGS：编译C文件时的选项，如-g；也可以通过add_definitions添加编译选项

EXECUTABLE_OUTPUT_PATH：可执行文件的存放路径

LIBRARY_OUTPUT_PATH：库文件路径

CMAKE_BUILD_TYPE:：build 类型(Debug, Release, ...)，CMAKE_BUILD_TYPE=Debug

BUILD_SHARED_LIBS：Switch between shared and static libraries

内置变量的使用：

>> 在CMakeLists.txt中指定，使用set

>> cmake命令中使用，如cmake -DBUILD_SHARED_LIBS=OFF



命令


project (HELLO)   #指定项目名称，生成的VC项目的名称；

>>使用${HELLO_SOURCE_DIR}表示项目根目录

include_directories：指定头文件的搜索路径，相当于指定gcc的-I参数

>> include_directories (${HELLO_SOURCE_DIR}/Hello)  #增加Hello为include目录

link_directories：动态链接库或静态链接库的搜索路径，相当于gcc的-L参数

       >> link_directories (${HELLO_BINARY_DIR}/Hello)     #增加Hello为link目录

add_subdirectory：包含子目录

       >> add_subdirectory (Hello)

add_executable：编译可执行程序，指定编译，好像也可以添加.o文件

       >> add_executable (helloDemo demo.cxx demo_b.cxx)   #将cxx编译成可执行文件——

add_definitions：添加编译参数

>> add_definitions(-DDEBUG)将在gcc命令行添加DEBUG宏定义；

>> add_definitions( “-Wall -ansi –pedantic –g”)

target_link_libraries：添加链接库,相同于指定-l参数

>> target_link_libraries(demo Hello) #将可执行文件与Hello连接成最终文件demo

add_library:

>> add_library(Hello hello.cxx)  #将hello.cxx编译成静态库如libHello.a

add_custom_target:

message( status|fatal_error, “message”):

set_target_properties( ... ): lots of properties... OUTPUT_NAME, VERSION, ....

link_libraries( lib1 lib2 ...): All targets link with the same set of libs




FAQ

1）  怎样获得一个目录下的所有源文件
>> aux_source_directory(<dir> <variable>)

>> 将dir中所有源文件（不包括头文件）保存到变量variable中，然后可以add_executable (ss7gw ${variable})这样使用。

2）  怎样指定项目编译目标
>>  project命令指定

3）  怎样添加动态库和静态库
>> target_link_libraries命令添加即可

4）  怎样在执行CMAKE时打印消息
>> message([SEND_ERROR | STATUS | FATAL_ERROR] "message to display" ...)

>> 注意大小写

5）  怎样指定头文件与库文件路径
>> include_directories与link_directories

>>可以多次调用以设置多个路径

>> link_directories仅对其后面的targets起作用

6）  怎样区分debug、release版本
>>建立debug/release两目录，分别在其中执行cmake -DCMAKE_BUILD_TYPE=Debug（或Release），需要编译不同版本时进入不同目录执行make即可；

Debug版会使用参数-g；Release版使用-O3 –DNDEBUG

>> 另一种设置方法——例如DEBUG版设置编译参数DDEBUG

IF(DEBUG_mode)

    add_definitions(-DDEBUG)

ENDIF()

在执行cmake时增加参数即可，例如cmake -D DEBUG_mode=ON

7）  怎样设置条件编译
例如debug版设置编译选项DEBUG，并且更改不应改变CMakelist.txt

>> 使用option command，eg：

option(DEBUG_mode "ON for debug or OFF for release" ON)

IF(DEBUG_mode)

    add_definitions(-DDEBUG)

ENDIF()

>> 使其生效的方法：首先cmake生成makefile，然后make edit_cache编辑编译选项；Linux下会打开一个文本框，可以更改，该完后再make生成目标文件——emacs不支持make edit_cache；

>> 局限：这种方法不能直接设置生成的makefile，而是必须使用命令在make前设置参数；对于debug、release版本，相当于需要两个目录，分别先cmake一次，然后分别make edit_cache一次；

>> 期望的效果：在执行cmake时直接通过参数指定一个开关项，生成相应的makefile——可以这样做，例如cmake –DDEBUGVERSION=ON

8）  怎样添加编译宏定义
>> 使用add_definitions命令，见命令部分说明

9）  怎样添加编译依赖项
用于确保编译目标项目前依赖项必须先构建好

>>add_dependencies

10）        怎样指定目标文件目录
>> 建立一个新的目录，在该目录中执行cmake生成Makefile文件，这样编译结果会保存在该目录——类似

>> SET_TARGET_PROPERTIES(ss7gw PROPERTIES

                      RUNTIME_OUTPUT_DIRECTORY "${BIN_DIR}")

11）        很多文件夹，难道需要把每个文件夹编译成一个库文件？
>> 可以不在子目录中使用CMakeList.txt，直接在上层目录中指定子目录

12）        怎样设定依赖的cmake版本
>>cmake_minimum_required(VERSION 2.6)

13）        相对路径怎么指定
>> ${projectname_SOURCE_DIR}表示根源文件目录，${ projectname _BINARY_DIR}表示根二进制文件目录？

14）        怎样设置编译中间文件的目录
>> TBD

15）        怎样在IF语句中使用字串或数字比较
>>数字比较LESS、GREATER、EQUAL，字串比STRLESS、STRGREATER、STREQUAL，

>> Eg：

set(CMAKE_ALLOW_LOOSE_LOOP_CONSTRUCTS ON)

set(AAA abc)

IF(AAA STREQUAL abc)

    message(STATUS "true")   #应该打印true

ENDIF()

16）        更改h文件时是否只编译必须的cpp文件
>> 是

17）        机器上安装了VC7和VC8，CMAKE会自动搜索编译器，但是怎样指定某个版本？
>> TBD

18）        怎样根据OS指定编译选项
>> IF( APPLE ); IF( UNIX ); IF( WIN32 )

19）        能否自动执行某些编译前、后命令？
>> 可以，TBD

20）        怎样打印make的输出
make VERBOSE=1
```

