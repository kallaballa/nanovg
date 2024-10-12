cmake_minimum_required(VERSION 3.1.0)

set(PROJECT_NAME nanovg)
project(${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_FLAGS "-D__STDC_CONSTANT_MACROS")

set(SRC_DIR "src")

file(GLOB SRCS ${SRC_DIR}/*.c)
file(GLOB HDRS ${SRC_DIR}/*.h)

option(NANOVG_GLES3 "GLES3" OFF)

if(NANOVG_GLES3)
  add_definitions(-DNANOVG_GLES3_IMPLEMENTATION=1 )
else()
  add_definitions(-DNANOVG_GL3_IMPLEMENATION=1 )
endif()

add_library(${PROJECT_NAME} ${SRCS})
target_link_libraries(${PROJECT_NAME} -lm)
target_compile_options(${PROJECT_NAME} PUBLIC -fvisibility=default)

install(TARGETS ${PROJECT_NAME}
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include/${PROJECT_NAME}
)

install(FILES ${HDRS} DESTINATION include/${PROJECT_NAME}/)

