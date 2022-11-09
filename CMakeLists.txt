cmake_minimum_required(VERSION 3.22)

project(yolo)

add_subdirectory(ncnn EXCLUDE_FROM_ALL)

find_package( OpenCV REQUIRED )

add_executable(yolo
    yolo.cpp 
    yolov7main.cpp)
target_link_libraries(yolo ncnn pthread dl gomp ${OpenCV_LIBS})