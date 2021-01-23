add_definitions(-D_AFXDLL)

set(CUS_TARGET_NAME gui)
# It should be set to 1 for the static MFC library, and 2 for the shared MFC library.
set(CMAKE_MFC_FLAG 2)

# 头文件查找路径
include_directories(
    ${PROJECT_SOURCE_DIR}
	${CMAKE_CURRENT_SOURCE_DIR}/include
    ${Boost_INCLUDE_DIRS})

# 获取源文件
FILE(GLOB SRC_FILES "./*.cpp")
FILE(GLOB HEAD_FILES "./*.h")
FILE(GLOB RC_FILES "./*.rc")
# 生成目标文件
add_executable(${CUS_TARGET_NAME} ${SRC_FILES} ${HEAD_FILES} ${RC_FILES})
set_target_properties(${CUS_TARGET_NAME} PROPERTIES LINK_FLAGS "/SUBSYSTEM:WINDOWS")
# 链接库文件
# target_link_libraries(${CUS_TARGET_NAME} ${Boost_LIBRARIES})