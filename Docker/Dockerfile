# syntax=docker/dockerfile:1

FROM ubuntu AS base
RUN apt update
ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt install -y tzdata libopencv-imgcodecs4.5d && rm -rf /var/lib/apt/lists/*

FROM base AS Build
WORKDIR /opencv
RUN apt update
RUN apt install -y libopencv-dev git cmake build-essential && rm -rf /var/lib/apt/lists/*
RUN git clone --recurse-submodules https://github.com/burlizzi/YoloV7-ncnn-Raspberry-Pi-4
WORKDIR /opencv/YoloV7-ncnn-Raspberry-Pi-4
RUN cmake -D NCNN_DISABLE_RTTI=OFF \
    -D NCNN_BUILD_TOOLS=ON\
    -D CMAKE_TOOLCHAIN_FILE=./ncnn/toolchains/pi3.toolchain.cmake -B build .
RUN cmake --build build -j`nproc`



FROM base  
WORKDIR /root/
COPY --from=Build /opencv/YoloV7-ncnn-Raspberry-Pi-4/build/yolo ./
COPY --from=Build /opencv/YoloV7-ncnn-Raspberry-Pi-4/yolov7-tiny* ./
CMD ["./yolo"]