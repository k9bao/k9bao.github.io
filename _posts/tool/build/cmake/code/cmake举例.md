# 1. cmake 举例

- [1. cmake 举例](#1-cmake-举例)
  - [1.1. 单文件编译](#11-单文件编译)
  - [1.2. 多文件编译](#12-多文件编译)
  - [1.3. 库编译](#13-库编译)
  - [1.4. 库调用](#14-库调用)

## 1.1. 单文件编译

```目录结构
├─single_file
│      CMakeLists.txt
│      main.cpp
```

```bash
cd single_file
cmake -B build -G Ninja #可以不用 -G 指定 Generators
cmake --build build     #编译生成可执行程序
```

CMakeList.txt

```shell
cmake_minimum_required(VERSION 3.10)

# set the project name
project(helloword)

# add the executable
add_executable(helloword main.cpp)
```

main.cpp

```C++
#include <iostream>

int main(){
    std::cout<<"hello world"<<std::endl;
    return 0;
}
```

## 1.2. 多文件编译

```目录结构
├─mult_file
│  │  CMakeLists.txt
│  │  hello.cpp
│  │  hello.h
│  │  main.cpp
│  └─subDir
│          hello2.cpp
│          hello2.h
```

```bash
cd mult_file
cmake -B build -G Ninja #可以不用 -G 指定 Generators
cmake --build build     #编译生成可执行程序
```

CMakeList.txt

```shell
cmake_minimum_required(VERSION 3.10)
# set the project name
project(helloword)

FILE (GLOB ALL_SOURCES "*.cpp" "./subDir/*.cpp" )
# add the executable
add_executable(helloword ${ALL_SOURCES})
```

```C++
//main.cpp
#include "hello.h"
#include "subDir/hello2.h"

int main(){
    print_hello();
    print_hello2();
    return 0;
}

//hello.h
int print_hello();
//hello.cpp
#include <iostream>

int print_hello(){
    std::cout<<"hello world"<<std::endl;
    return 0;
}

//hello2.h
int print_hello2();
//hello2.cpp
#include <iostream>

int print_hello2(){
    std::cout<<"hello world"<<std::endl;
    return 0;
}
```

## 1.3. 库编译

```目录结构
lib
   CMakeLists.txt
   hello.cpp
   hello.h
```

```bash
cd lib
cmake -B build -G Ninja #可以不用 -G 指定 Generators
cmake --build build     #编译生成动态库和静态库，这里使用Nigja,在windows下生成的是.a和.dll
```

```bash
cd lib
cmake -B build
cmake --build build     #编译生成动态库和静态库，这里使用Visual Studio,在build\lib\Debug下生成.dll和.lib
```

CMakeList.txt

```shell
cmake_minimum_required(VERSION 3.10)

# set the project name
project(helloword)
SET (LIB_NAME hello)

FILE (GLOB LIBHELLO_SRC "*.cpp" )

# 结果生成在编译目录下的lib目录
SET (LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
ADD_LIBRARY (${LIB_NAME} SHARED ${LIBHELLO_SRC})

# 因为hello作为一个target是不能重名的， 故把上面的hello修改为hello_static
ADD_LIBRARY (${LIB_NAME}_static STATIC ${LIBHELLO_SRC})

# 希望 "hello_static" 在输出时，不是"hello_static"，而是以"hello"的名字显示，故设置如下：
SET_TARGET_PROPERTIES (${LIB_NAME}_static PROPERTIES OUTPUT_NAME ${LIB_NAME})

# cmake在构建一个新的target时，会尝试清理掉其他使用这个名字的库，
# 为了回避这个问题，再次使用SET_TARGET_PROPERTIES定义 CLEAN_DIRECT_OUTPUT属性。
SET_TARGET_PROPERTIES (${LIB_NAME}_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)
SET_TARGET_PROPERTIES (${LIB_NAME} PROPERTIES CLEAN_DIRECT_OUTPUT 1)

# 按照规则，动态库是应该包含一个版本号的，
# VERSION指代动态库版本，SOVERSION指代API版本。
SET_TARGET_PROPERTIES (${LIB_NAME} PROPERTIES VERSION 1.2 SOVERSION 1)

# 我们需要将libhello.a, libhello.so.x以及hello.h安装到系统目录，才能真正让其他人开发使用，
# 在本例中我们将hello的共享库安装到<prefix>/lib目录；
# 将hello.h安装<prefix>/include/hello目录。
# INSTALL (TARGETS ${LIB_NAME} ${LIB_NAME}_static LIBRARY DESTINATION lib ARCHIVE DESTINATION lib)
# INSTALL (FILES hello.h DESTINATION include/hello)
```

```C++
//hello.h
int print_hello();
//hello.cpp
#include <iostream>

int print_hello(){
    std::cout<<"hello world"<<std::endl;
    return 0;
}
```

## 1.4. 库调用

先执行“库编译”章节，后调用库,lib目录详见库编译

```目录结构
├─used_lib
  │  CMakeLists.txt
  │  main.cpp
  └─lib
          CMakeLists.txt
          hello.cpp
          hello.h
```

```bash
rm -r build
cmake -B build -G Ninja
cmake --build build
cd build
helloword.exe
cd ..
```

CMakeList.txt

```shell
cmake_minimum_required(VERSION 3.10)

# set the project name
project(helloword)

add_definitions(-std=c++11)
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb -Wl,-rpath=./:./lib:./lib/build/lib") #-Wl,-rpath=./
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wl,-rpath=./:./lib") #-Wall

# add the executable
add_executable(${PROJECT_NAME} main.cpp)
# target_link_libraries(${PROJECT_NAME} hello)#默认连接动态库，如果连接动态库，执行时要保证能找到动态库
```

```C++
//main.cpp
#include "hello.h"

int main(){
    print_hello();
    return 0;
}
```
