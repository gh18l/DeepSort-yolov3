# DeepSort-yolov3
## Description
It is a robust version of multiple target tracking originated from [DeepSort](https://github.com/bitzy/DeepSort) (it only uses a simple detector) with YOLO-v3. It is easy to check and compile according to the CMakeLists.txt. 

The "build/libyolo.so" contains of YOLOv3-based detector compiled by myself.

It only tests in ubuntu, I am not sure if it can be used in other operating system.

## Usage
You can change macro variable *VIDEO* in "main.cpp" to define the video path. It will detect and track all pedestrians in scene automatically.
