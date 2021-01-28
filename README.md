# DeepSort-yolov3
## Description
It is a robust YOLO-v3 version originated from [DeepSort](https://github.com/bitzy/DeepSort) (it only uses a simple detector) to track multiple target. It is easy to check and compile according to the CMakeLists.txt. 

The "build/libyolo.so" contains of YOLOv3-based detector compiled by myself.

It only tests in ubuntu, the others version is not sure if it can be used.

## Usage
You can change macro variable *VIDEO* in "main.cpp" to define the video path. It will detect and track all pedestrians in scene automatically.