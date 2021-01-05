cmake_minimum_required(VERSION 3.17)
project(Final_Project)

set(CMAKE_CXX_STANDARD 14)

set(LOCAL_INCLUDE_DIR ${CMAKE_CURRENT_LIST_DIR}/include)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")

aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src SRC_FLIES)

# 设置OpenCV目录所在
set(OpenCV_DIR "E:\\opencv\\new_build")
find_package(OpenCV REQUIRED)
# 添加OpenCV头文件目录
include_directories(${OpenCV_INCLUDE_DIRS} ${LOCAL_INCLUDE_DIR})

#寻找OpenBLAS库
find_package(OpenBLAS REQUIRED)
#包含项目头文件和OpenBLAS相关头文件路径
include_directories(${PROJECT_SOURCE_DIR} ${OpenBLAS_INCLUDE_DIRS})

# openMP 配置
FIND_PACKAGE(OpenMP REQUIRED)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")


add_executable(Final_Project main.cpp ${SRC_FLIES})


# 链接OpenCV库文件
target_link_libraries(Final_Project ${OpenCV_LIBS})
# 链接OpenBlas库文件
target_link_libraries(Final_Project ${OpenBLAS_LIBRARIES})
