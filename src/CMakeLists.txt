cmake_minimum_required(VERSION 3.20)

project(MPM LANGUAGES CXX CUDA)

add_subdirectory(partio)

include_directories(./)

find_package(CUDAToolkit)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CUDA_SEPARABLE_COMPILATION ON)
set(CMAKE_CUDA_ARCHITECTURES 61)

add_library(mpm_cpp
    ../Simulation/Material/Material.cpp
    ../Simulation/Particle/ParticleDomain.cpp
    ../Simulation/Grid/GridDomain.cpp
    ../Simulation/DomainTransform/DomainTransformer.cpp
    ../Simulation/MPM/Simulator.cpp
    ../Simulation/MPM/SimulatorBuilder.cpp
    ../SPGrid_Utilities.cpp
    ../SPGrid_Geometry.cpp
    ../MnBase/Math/Probability/Probability.cpp
)
target_link_libraries(mpm_cpp PUBLIC CUDA::cudart partio)

add_executable(p2g_cuda
main.cpp

Benchmarks.cuh
Benchmarks.cu

helper_cuda.h
helper_string.h
setting.h
SPGrid_Allocator.h
SPGrid_Array.h
SPGrid_Geometry.h
SPGrid_Geometry.cpp
SPGrid_Mask.h
SPGrid_Set.h
SPGrid_Utilities.h
SPGrid_Utilities.cpp	
std_array.h

# MnBase
MnBase/Singleton.h
MnBase/AggregatedAttribs.h
MnBase/Math/Matrix/MatrixKernels.cu
MnBase/Math/Matrix/MatrixKernels.cuh
MnBase/Math/Matrix/svd3.h
MnBase/Math/Probability/Probability.h
MnBase/Math/Probability/Probability.cpp
MnBase/Meta/AllocMeta.h
MnBase/Meta/Meta.h

# Simulation
Simulation/ConstitutiveModel/ConstitutiveModelKernels.cuh

Simulation/DomainTransform/DomainTransformer.cpp
Simulation/DomainTransform/DomainTransformer.cu
Simulation/DomainTransform/DomainTransformer.cuh
Simulation/DomainTransform/DomainTransformKernels.cu
Simulation/DomainTransform/DomainTransformKernels.cuh

Simulation/Geometry/Geometry.h

Simulation/Grid/GridDomain.cpp
Simulation/Grid/GridDomain.cu
Simulation/Grid/GridDomain.cuh
Simulation/Grid/GridKernels.cu
Simulation/Grid/GridKernels.cuh
    
Simulation/Material/Material.cpp
Simulation/Material/Material.h

Simulation/Model/Model.cuh
    
Simulation/MPM/ModelInitSchemes.hpp
Simulation/MPM/Simulator.cpp
Simulation/MPM/Simulator.cu
Simulation/MPM/Simulator.h
Simulation/MPM/SimulatorKernels.cu
Simulation/MPM/SimulatorKernels.cuh

Simulation/Particle/ParticleDomain.cpp
Simulation/Particle/ParticleDomain.cu
Simulation/Particle/ParticleDomain.cuh
Simulation/Particle/ParticleKernels.cu
Simulation/Particle/ParticleKernels.cuh

Simulation/TimeIntegrator/ExplicitTimeIntegrator.cu
Simulation/TimeIntegrator/G2PKernels.cu
Simulation/TimeIntegrator/G2PKernels.cuh
Simulation/TimeIntegrator/GridUpdateKernels.cu
Simulation/TimeIntegrator/GridUpdateKernels.cuh
Simulation/TimeIntegrator/ImplicitTimeIntegrator.cu
Simulation/TimeIntegrator/MPMComputationKernels.cu
Simulation/TimeIntegrator/MPMComputationKernels.cuh
Simulation/TimeIntegrator/MPMTimeIntegrator.cu
Simulation/TimeIntegrator/P2GKernels.cu
Simulation/TimeIntegrator/P2GKernels.cuh
Simulation/TimeIntegrator/TimeIntegrator.cuh 

# System
System/CudaDevice/CudaDevice.h
System/CudaDevice/CudaDevice.cpp
System/CudaDevice/CudaDeviceUtils.cuh
System/CudaDevice/CudaDeviceUtils.cu
System/CudaDevice/CudaExecutionPolicy.h  
System/CudaDevice/CudaHostUtils.hpp
System/CudaDevice/CudaKernelLauncher.cu  

System/Log/Logger.hpp

# Utility
Utility/PoissonDisk/cyCore.h
Utility/PoissonDisk/cyHeap.h
Utility/PoissonDisk/cyPoint.h
Utility/PoissonDisk/cyPointCloud.h
Utility/PoissonDisk/cySampleElim.h
Utility/PoissonDisk/PoissonDisk.h
Utility/PoissonDisk/SampleGenerator.h

Utility/Profiler/CudaTimer.hpp
Utility/Profiler/Timer.hpp
)

target_link_libraries(p2g_cuda PRIVATE mpm_cpp partio)
