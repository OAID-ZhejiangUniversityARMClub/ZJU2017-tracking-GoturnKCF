cmake_minimum_required(VERSION 2.8)
project(mygoturn)
# avoid "can not find -lopencv_dep_cudart"
set(CUDA_USE_STATIC_CUDA_RUNTIME OFF)



if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
    message(STATUS "No build type selected, default to ${CMAKE_BUILD_TYPE}")
endif()

find_package(Boost COMPONENTS system filesystem regex REQUIRED)


set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")






set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
find_package(Boost COMPONENTS system filesystem regex REQUIRED)


set(OpenCV_DIR "/home/firefly/opencv-3.3.0/build")

find_package( OpenCV REQUIRED )
message("Open CV version is ${OpenCV_VERSION}")

include_directories("/home/firefly/opencv-3.3.0/include ")
include_directories("/home/firefly/opencv-3.3.0/build/opencv2 ")
include_directories("/home/firefly/opencv-3.3.0/build/opencv ")
include_directories("/home/firefly/opencv-3.3.0/build ")











set(AID-tool "/usr/local/AID")
set(Caffe_DIR ${AID-tool}/CaffeOnACL)
set(Caffe_INCLUDE_DIRS ${Caffe_DIR}/include)
set(Caffe_LIBRARIES ${Caffe_DIR}/lib/libcaffe.so.1.0.0-rc5)

message("Caffe_LIBRARIES HINTS is ${Caffe_DIR}/build/lib")
message("Caffe_LIBRARIES is ${Caffe_LIBRARIES}")

if(Caffe_LIBRARIES AND Caffe_INCLUDE_DIRS)
    set(Caffe_FOUND 1)
endif()





set(Caffe_DEFINITIONS -DCPU_ONLY)
add_definitions(${Caffe_DEFINITIONS})
set(Caffe_DEFINITIONS ${AID-tool}/CaffeOnACL/include )
message("Caffe_DEFINITIONS is ${Caffe_DEFINITIONS}")
message("Caffe_DIR is ${Caffe_DIR}")
message("Caffe_INCLUDE_DIRS is ${Caffe_INCLUDE_DIRS}")
message("Caffe_LIBRARIES is ${Caffe_LIBRARIES}")







find_package(Caffe REQUIRED)
#include_directories("/home/firefly/CaffeOnACL/build ")
include_directories("/home/firefly/CaffeOnACL/distribute/include ")
include_directories("/home/firefly/CaffeOnACL/cmake/External ")




add_definitions("/home/firefly/CaffeOnACL/include/caffe")    # ex. -DCPU_ONLY
message("Caffe_DIR is ${Caffe_DIR}")

#add_library (
#/usr/lib/aarch64-linux-gnu/libglog.so.0
#)
#
#        src/network/regressor.cpp
#        src/network/regressor_base.cpp
#        src/tracker/tracker.cpp
#        src/helper/helper.cpp
#        src/helper/bounding_box.cpp
#        src/helper/image_proc.cpp
#
#        src/visualizer/runTracker.cpp
#
#        src/loader/loader_base.cpp
#        src/loader/loader_base.h
#
#
#        src/network/regressor.h
#        src/network/regressor_base.h
#        src/tracker/tracker.h
#        src/helper/helper.h
#        src/helper/bounding_box.h
#        src/helper/image_proc.h
#       )

include_directories(src)

FILE(GLOB_RECURSE SOURCE_FILES "src/*.cpp")
add_executable(runTracker ${SOURCE_FILES})
target_link_libraries(runTracker ${OpenCV_LIBS} ${Caffe_LIBRARIES} ${Boost_LIBRARIES} /usr/lib/aarch64-linux-gnu/libglog.so.0  )
