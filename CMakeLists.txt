cmake_minimum_required(VERSION 3.16)
add_compile_options("$<$<AND:$<C_COMPILER_ID:MSVC>,$<COMPILE_LANGUAGE:C>>:/utf-8>")
add_compile_options("$<$<AND:$<CXX_COMPILER_ID:MSVC>,$<COMPILE_LANGUAGE:CXX>>:/utf-8>")
add_compile_options("$<$<AND:$<CXX_COMPILER_ID:MSVC>,$<COMPILE_LANGUAGE:CXX>>:/Zc:__cplusplus>")

set(PROJECT_NAME simplebinder)
set(PROJECT_VERSION 1.00)

project(${PROJECT_NAME} VERSION ${PROJECT_VERSION})

if(NOT TARGET tp_stub)
add_subdirectory(../tp_stub ${CMAKE_CURRENT_BINARY_DIR}/tp_stub)
endif()

add_library(${PROJECT_NAME} STATIC
    v2link.cpp
)

target_include_directories(${PROJECT_NAME} PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_libraries(${PROJECT_NAME} PUBLIC
    tp_stub
)

if (TVP_STATIC_PLUGIN)
target_compile_definitions(${PROJECT_NAME} PRIVATE
    TVP_STATIC_PLUGIN
)
endif()
