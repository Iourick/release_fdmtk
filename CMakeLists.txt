cmake_minimum_required(VERSION 3.8)
set(CUDA_PATH "/usr/bin" CACHE PATH "CUDA Toolkit path")
set(CUDACXX "/usr/local/cuda-12.5/bin/nvcc")
set(CMAKE_CUDA_ARCHITECTURES "native")
set(CMAKE_CUDA_COMPILER "/usr/local/cuda-12.5/bin/nvcc")

# Project name
project(fdmtk LANGUAGES CXX CUDA)

# Set the C++ and CUDA standards
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)

include(CheckLanguage)
check_language(CUDA)
enable_language(CUDA)

# Set CUDA path and CUB path
include_directories(/usr/local/cuda-12.5/targets/x86_64-linux/include/cub)
include_directories(${CMAKE_SOURCE_DIR})

# List of source files
set(SRC_FILES
    fdmtk.cu
    array.cu
    boxcar.cu
    CandidateList.cu
    CandidateSink.cu
    CpuTimer.cu
    cudafdmt.cu
    CudaTimer.cu
    DataSource.cu
    fdmt.cu
    rescale.cu
    SigprocFile.cu
    SigprocFileSet.cu 
    fdmt_base.cu
    fdmt_gpu.cu
    fdmtUtils.cu    
)

# Add executable target
add_executable(CUFDMT ${SRC_FILES})

# Link CUDA libraries
target_link_libraries(CUFDMT cudadevrt cudart_static rt pthread dl)
