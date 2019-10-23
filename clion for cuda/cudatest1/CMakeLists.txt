cmake_minimum_required(VERSION 3.6)
PROJECT(lbmslv)

FIND_PACKAGE(CUDA REQUIRED)

INCLUDE(FindCUDA)
#INCLUDE_DIRECTORIES(/usr/local/cuda/include ${MPI_INCLUDE_PATH})
FILE(GLOB SOURCES "*.cu" "*.cpp" "*.c" "*.h")
#set(SOURCE_FILES main.cpp)
add_executable(demo_projet3 main.cpp)
#add_executable(demo_projet ${SOURCE_FILES} vector.cpp vector1.cpp)
CUDA_ADD_EXECUTABLE(lbmslv vectorAdd.cu)



LIST(APPEND CMAKE_CXX_FLAGS "-std=c++0x -O3 -ffast-math -Wall")

LIST(APPEND CUDA_NVCC_FLAGS --compiler-options -fno-strict-aliasing -lineinfo -use_fast_math -Xptxas -dlcm=cg)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_20,code=sm_20)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_30,code=sm_30)
LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_35,code=sm_35)

TARGET_LINK_LIBRARIES(lbmslv /usr/local/cuda/lib64/libcudart.so)



#cmake_minimum_required(VERSION 3.7)
#project(demo_projet)
#
#set(CMAKE_CXX_STANDARD 11)
##set(CMAKE_CXX_STANDARD 14)
#
#set(SOURCE_FILES main.cpp)
#add_executable(demo_projet ${SOURCE_FILES})
#add_executable(demo_target demo.cpp)
#add_executable(demo_target1 demo1.cpp)
#add_executable(demo_target2 demo2.cpp)
#add_executable(demo_target3 demo3.cpp)
#add_executable(demo_target4 demo4.cpp)
#add_executable(demo_target5 demo5.cpp)
#add_executable(demo_target6 demo6.cpp)
#add_executable(demo_target7 demo7.cpp)
#add_executable(demo_target8 demo8.cpp)
#
##find_package(CUDA REQUIRED)
##file(GLOB CU test.cu)
##cuda_add_executable(demo_target8 test.cu)

