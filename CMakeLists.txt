cmake_minimum_required(VERSION 3.10)
project(MyTensorRTProject)

set(CMAKE_CXX_STANDARD 14)

# Defina os caminhos para o TensorRT e CUDA
set(TENSORRT_DIR /home/adriano/Documents/tools/TensorRT-8.6.0.12/)
set(CUDA_TOOLKIT_ROOT_DIR "/usr/local/cuda-12.5")

find_package(CUDA REQUIRED)
find_package(pybind11 REQUIRED)

# Inclui diretórios do TensorRT e CUDA
include_directories(${TENSORRT_DIR}/include)
include_directories(${CUDA_TOOLKIT_ROOT_DIR}/targets/x86_64-linux/include)
include_directories(${CMAKE_SOURCE_DIR}/include)

# Linka bibliotecas do TensorRT e CUDA
link_directories(${TENSORRT_DIR}/lib)
link_directories(${CUDA_TOOLKIT_ROOT_DIR}/lib64)

# Adiciona as fontes do projeto
add_executable(MyApp src/main.cpp)

# Linka as bibliotecas necessárias
target_link_libraries(MyApp nvinfer nvonnxparser ${CUDA_LIBRARIES})

# Configuração para gerar a biblioteca Python usando pybind11
# Cria o módulo Python
#pybind11_add_module(MyTensorRT python_bindings/bindings.cpp src/engine.cpp)
#target_link_libraries(MyTensorRT PRIVATE nvinfer nvonnxparser ${CUDA_LIBRARIES})
