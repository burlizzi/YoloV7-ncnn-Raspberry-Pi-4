project(yolo)

find_package( OpenCV REQUIRED )

cmake_minimum_required(VERSION 3.22)
add_executable(yolo yolo.cpp yolov7main.cpp)
include_directories(/usr/include/opencv4 ${CMAKE_SOURCE_DIR}/ncnn/build/install/include/ncnn)
target_link_libraries(yolo ${CMAKE_SOURCE_DIR}/ncnn/build/install/lib/libncnn.a pthread dl gomp ${OpenCV_LIBS})