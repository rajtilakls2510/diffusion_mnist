cmake_minimum_required(VERSION 3.16)
project(ddpm LANGUAGES CXX CUDA)

set(CMAKE_PREFIX_PATH "${CMAKE_PREFIX_PATH};/media/riju/New Volume2/libtorch")

# Torch
find_package(Torch CONFIG REQUIRED)

# OpenCV
find_package(OpenCV REQUIRED)

# Global include directories
include_directories(${OpenCV_INCLUDE_DIRS})

# Set flags (Torch requires some)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")

add_executable(train train.cpp network.cpp trainer.cpp mnist_loader.cpp)
target_link_libraries(train ${TORCH_LIBRARIES} ${OpenCV_LIBS})
set_property(TARGET train PROPERTY CXX_STANDARD 17)

add_executable(sample sampler.cpp network.cpp)
target_link_libraries(sample ${TORCH_LIBRARIES} ${OpenCV_LIBS})
set_property(TARGET sample PROPERTY CXX_STANDARD 17)
