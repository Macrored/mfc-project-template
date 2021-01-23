cmake_minimum_required(VERSION 3.0)
project(MFCProjectTemplate)

# 编译参数
if(CMAKE_SYSTEM_NAME MATCHES "Linux")
    add_definitions(-std=c++14) # c++14标准
    add_compile_options(-g) # gdb调试模式，默认则是三级二进制优化模式-O3
elseif(CMAKE_SYSTEM_NAME MATCHES "Windows")
    add_definitions(/std:c++14)
    # 忽略warning C4996
    add_definitions(-D_CRT_SECURE_NO_DEPRECATE)

    # 所有接口使用静态库链接
    # set(CMAKE_CXX_FLAGS_RELEASE "/MT")
    # set(CMAKE_CXX_FLAGS_DEBUG "/MTd")
endif(CMAKE_SYSTEM_NAME MATCHES "Linux")

add_definitions(-DUNICODE -D_UNICODE) # 定义工程的字符编码为Unicode编码
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

message(STATUS "CMAKE_BUILD_TYPE:${CMAKE_BUILD_TYPE}")

# 查找OpenSSL
set(OPENSSL_USE_STATIC_LIBS TRUE)
if(WIN32)
    # set(OPENSSL_MSVC_STATIC_RT TRUE)
endif()
find_package(OpenSSL 1.1.1 REQUIRED)
message(STATUS "OPENSSL_INCLUDE_DIRS:${OPENSSL_INCLUDE_DIR}")
message(STATUS "OPENSSL_LIBRARIES:${OPENSSL_LIBRARIES}")

# 查找Boost
set(Boost_USE_STATIC_LIBS ON)
if(WIN32)
    # set(Boost_USE_STATIC_RUNTIME ON)
endif()
find_package(Boost 1.7.0 REQUIRED COMPONENTS filesystem locale)
message(STATUS "Boost_INCLUDE_DIRS:${Boost_INCLUDE_DIRS}")
message(STATUS "Boost_LIBRARY_DIRS:${Boost_LIBRARY_DIRS}")
message(STATUS "Boost_LIBRARIES:${Boost_LIBRARIES}")


# 公用模块
add_subdirectory(common)

if(WIN32)   
    # windows主模块
    add_subdirectory(gui)
elseif(APPLE)
    # macos主模块
elseif(UNIX)
    # add you code
endif()

