cmake_minimum_required (VERSION 3.1)
set(name "TRACKER")
set(libname "yolo")
project ( ${name} )

set(CMAKE_BUILD_TYPE "Release")
if(CMAKE_BUILD_TYPE STREQUAL "Release")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2")
endif()

# set output path
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${PROJECT_BINARY_DIR})    
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${PROJECT_BINARY_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${PROJECT_BINARY_DIR}/bin/Debug)    
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${PROJECT_BINARY_DIR}/bin/Release)  

#c++ version
set (CMAKE_CXX_STANDARD 11)

#cuda
find_package(CUDA)
set(CUDA_NVCC_FLAGS
    ${CUDA_NVCC_FLAGS}
#    -O3 
	-gencode=arch=compute_61,code=\"sm_61,compute_61\"
    )
	
#opencv 
if ( WIN32 )
	set(OpenCV_DIR "E:/libs/OpenCV/x64/vc14/lib")
	set(OpenCV_CONFIG_PATH "E:/libs/OpenCV")
	set(WIN_HEADER_PATH "${PROJECT_SOURCE_DIR}/winheadfile")
    include_directories(${WIN_HEADER_PATH})
endif()

# OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
message(${OpenCV_INCLUDE_DIRS})

set(MY_HEADER_FILES
# C++ header file
    activation_layer.h
    activations.h
avgpool_layer.h
batchnorm_layer.h
blas.h
box.h
classifier.h
col2im.h
connected_layer.h
convolutional_layer.h
cost_layer.h
crnn_layer.h
crop_layer.h
cuda.h
data.h
deconvolutional_layer.h
demo.h
detection_layer.h
dropout_layer.h
gemm.h
getopt.h
gettimeofday.h
gru_layer.h
http_stream.h
im2col.h
image.h
layer.h
list.h
local_layer.h
matrix.h
maxpool_layer.h
network.h
normalization_layer.h
option_list.h
parser.h
region_layer.h
reorg_layer.h
reorg_old_layer.h
rnn_layer.h
route_layer.h
shortcut_layer.h
softmax_layer.h
stb_image.h
stb_image_write.h
tree.h
unistd.h
upsample_layer.h
utils.h
yolo_layer.h
)
set(MY_CUDA_FILES
# CUDA files
activation_kernels.cu
avgpool_layer_kernels.cu
blas_kernels.cu
col2im_kernels.cu
convolutional_kernels.cu
crop_layer_kernels.cu
deconvolutional_kernels.cu
dropout_layer_kernels.cu
im2col_kernels.cu
maxpool_layer_kernels.cu
network_kernels.cu
)
set(MY_SOURCE_FILES 
# C++ code
activation_layer.c
activations.c
art.c
avgpool_layer.c
batchnorm_layer.c
blas.c
box.c
captcha.c
cifar.c
classifier.c
coco.c
col2im.c
compare.c
connected_layer.c
convolutional_layer.c
cost_layer.c
cpu_gemm.c
crnn_layer.c
crop_layer.c
cuda.c
darknet.c
data.c
deconvolutional_layer.c
demo.c
detection_layer.c
detector.c
dice.c
dropout_layer.c
gemm.c
getopt.c
gettimeofday.c
go.c
gru_layer.c
im2col.c
image.c
layer.c
list.c
local_layer.c
matrix.c
maxpool_layer.c
network.c
nightmare.c
normalization_layer.c
option_list.c
parser.c
region_layer.c
reorg_layer.c
reorg_old_layer.c
rnn.c
rnn_layer.c
rnn_vid.c
route_layer.c
shortcut_layer.c
softmax_layer.c
super.c
swag.c
tag.c
tree.c
upsample_layer.c
utils.c
voxel.c
writing.c
yolo.c
yolo_layer.c
http_stream.cpp
)

set(FEATURE
    ${PROJECT_SOURCE_DIR}/src/feature/FeatureTensor.cpp
    ${PROJECT_SOURCE_DIR}/src/feature/model.cpp
    ${PROJECT_SOURCE_DIR}/src/feature/dataType.h
    ${PROJECT_SOURCE_DIR}/src/feature/FeatureTensor.h
    ${PROJECT_SOURCE_DIR}/src/feature/model.h
)
set(MATCHING
    ${PROJECT_SOURCE_DIR}/src/matching/kalmanfilter.cpp
    ${PROJECT_SOURCE_DIR}/src/matching/linear_assignment.cpp
    ${PROJECT_SOURCE_DIR}/src/matching/nn_matching.cpp
    ${PROJECT_SOURCE_DIR}/src/matching/track.cpp
    ${PROJECT_SOURCE_DIR}/src/matching/tracker.cpp
    ${PROJECT_SOURCE_DIR}/src/matching/kalmanfilter.h
    ${PROJECT_SOURCE_DIR}/src/matching/linear_assignment.h
    ${PROJECT_SOURCE_DIR}/src/matching/nn_matching.h
    ${PROJECT_SOURCE_DIR}/src/matching/track.h
    ${PROJECT_SOURCE_DIR}/src/matching/tracker.h
)
set(THIRD
    ${PROJECT_SOURCE_DIR}/src/thirdPart/hungarianoper.cpp
    ${PROJECT_SOURCE_DIR}/src/thirdPart/munkres.cpp
    ${PROJECT_SOURCE_DIR}/src/thirdPart/boostmatrixadapter.cpp
    ${PROJECT_SOURCE_DIR}/src/thirdPart/adapter.cpp
    ${PROJECT_SOURCE_DIR}/src/thirdPart/hungarianoper.h
    ${PROJECT_SOURCE_DIR}/src/thirdPart/munkres.h
    ${PROJECT_SOURCE_DIR}/src/thirdPart/matrix.h
    ${PROJECT_SOURCE_DIR}/src/thirdPart/boostmatrixadapter.h
    ${PROJECT_SOURCE_DIR}/src/thirdPart/adapter.h
)
set(SOURCE
    ${PROJECT_SOURCE_DIR}/src/errmsg.cpp
    ${PROJECT_SOURCE_DIR}/src/main.cpp
    ${PROJECT_SOURCE_DIR}/src/VideoTracker.cpp
    ${PROJECT_SOURCE_DIR}/src/errmsg.h
    ${PROJECT_SOURCE_DIR}/src/VideoTracker.h
)

include_directories(
    /usr/local/cuda/include
    /home/lgh/.cache/bazel/_bazel_lgh/5c3057d6871aa63630396c83a6b7aeeb/external/eigen_archive/Eigen
    /home/lgh/.cache/bazel/_bazel_lgh/5c3057d6871aa63630396c83a6b7aeeb/external/eigen_archive
    /home/lgh/.cache/bazel/_bazel_lgh/5c3057d6871aa63630396c83a6b7aeeb/external/nsync/public
    /home/lgh/Downloads/tensorflow-r1.4/bazel-genfiles
    /home/lgh/Downloads/tensorflow-r1.4
    /home/lgh/Downloads/darknetAl-so/include
)

set(CUDNN_LIBS
    /usr/local/cuda/lib64/libcudnn.so
)

set(TENSORFLOWLIB
    /home/lgh/Downloads/tensorflow-r1.4/bazel-bin/tensorflow/libtensorflow_cc.so
    /home/lgh/Downloads/tensorflow-r1.4/bazel-bin/tensorflow/libtensorflow_framework.so
)

add_definitions(-DGPU)
add_definitions(-DCUDNN)
add_definitions(-DOPENCV)


cuda_add_executable(${name}
    ${FEATURE}
    ${MATCHING}
    ${THIRD}
    ${SOURCE}
)

target_link_libraries(${name} 
    ${OpenCV_LIBS}
    ${CUDNN_LIBS} 
    ${TENSORFLOWLIB} 
	${CUDA_LIBRARIES}
	${CUDA_CUBLAS_LIBRARIES}
	${CUDA_curand_LIBRARY}
	${CUDA_npp_LIBRARY}
    ${CUDA_nppc_LIBRARY}
    ${PROJECT_BINARY_DIR}/libyolo.so
)
