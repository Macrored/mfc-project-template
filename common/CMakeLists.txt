set(CUS_TARGET_NAME common)

aux_source_directory(src SourceFiles)
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${Boost_INCLUDE_DIRS}
)

link_directories(
    ${Boost_LIBRARY_DIRS}
)

# 指定生成目标
add_library(${CUS_TARGET_NAME} STATIC ${SourceFiles})
target_link_libraries(${CUS_TARGET_NAME} ${Boost_LIBRARIES})