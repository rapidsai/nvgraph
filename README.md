# nvGraph - NVIDIA graph library

Data analytics is a growing application of high-performance computing. Many advanced data analytics problems can be couched as graph problems. In turn, many of the common graph problems today can be couched as sparse linear algebra. This is the motivation for nvGraph, which harnesses the power of GPUs for linear algebra to handle large graph analytics.

This repository contains the legacy version of nvGraph as it was in the NVIDIA CUDA Toolkit. The aim is to provide a way for nvGraph users to continue using nvGraph after the CUDA Toolkit stops releasing it. While we still accept bug reports, we do not actively develop this product. If you find and can reproduce bugs in nvGRAPH, please [report issues on GitHub](https://github.com/rapidsai/nvgraph/issues/new).

Recently, NVIDIA started developing [cuGraph](https://github.com/rapidsai/cugraph) a collection of graph analytics that process data found in GPU Dataframes as part of [RAPIDS](https://rapids.ai/). Most nvGraph algorithms are now part of cuGraph too. In addition, cuGraph aims to provide a NetworkX-like API that will be familiar to data scientists, so they can now build GPU-accelerated workflows more easily. For more project details, see [rapids.ai](https://rapids.ai/).

## Get nvGrpah
#### Prerequisites

Compiler requirement:

* `gcc`     version 5.4+
* `nvcc`    version 9.2
* `cmake`   version 3.12



CUDA requirement:

* CUDA 9.2+
* NVIDIA driver 396.44+
* Pascal architecture or better

You can obtain CUDA from [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads).
Compiler requirements:

### Using the script

It is easy to install nvGraph from source. As a convenience, a `build.sh` script is provided. Run the script as shown below to download the source code, build and install the library.  Note that the library will be installed to the location set in `$CUDA_ROOT` (eg. `export CUDA_ROOT=/usr/local/cuda`). These instructions were tested on Ubuntu 18.04.

  ```bash
  git clone https://github.com/rapidsai/nvgraph.git
  cd nvgraph
  export CUDA_ROOT=/usr/local/cuda
  ./build.sh  # build the nvGraph library and install it to $CUDA_ROOT (you may need to add the sudo prefix)
  ```


### Manually build from Source 

The following instructions are for developers and contributors to nvGraph development. These instructions were tested on Linux Ubuntu 18.04. Use these instructions to build nvGraph from source and contribute to its development.  Other operating systems may be compatible, but are not currently tested.

The nvGraph package is a C/C++ CUDA library. It needs to be installed in order for nvGraph to operate correctly.  

The following instructions are tested on Linux systems.

#### Build and Install the C/C++ CUDA components

To install nvGraph from source, ensure the dependencies are met and follow the steps below:

1) Clone the repository and submodules

  ```bash
  # Set the localtion to nvGraph in an environment variable NVGRAPH_HOME 
  export NVGRAPH_HOME=$(pwd)/nvgraph

  # Download the nvGraph repo
  git clone https://github.com/rapidsai/nvgraph.git $NVGRAPH_HOME

  # Next load all the submodules
  cd $NVGRAPH_HOME
  git submodule update --init --recursive
  ```

2) Build and install `libnvgraph_rapids.so`. CMake depends on the `nvcc` executable being on your path or defined in `$CUDACXX`.

  This project uses cmake for building the C/C++ library. To configure cmake, run:

  ```bash
  cd $NVGRAPH_HOME
  cd cpp	# enter nvgraph's cpp directory
  mkdir build   		# create build directory 
  cd build     		# enter the build directory
  cmake .. -DCMAKE_INSTALL_PREFIX=$CONDA_PREFIX 

  # now build the code
  make -j				# "-j" starts multiple threads
  make install		# install the libraries 
  ```

The default installation  locations are `$CMAKE_INSTALL_PREFIX/lib` and `$CMAKE_INSTALL_PREFIX/include/nvgraph` respectively.

#### C++ stand alone tests

```bash
# Run the tests
cd $NVGRAPH_HOME
cd cpp/build
gtests/NVGRAPH_TEST # this is an executable file
```
These tests verify that the library was properly built and that the graph structure works as expected.
We currently do not maintain the algorithm test suite. Most graph analytics features are now developed and tested in [cuGraph](https://github.com/rapidsai/cugraph).

## Documentation

The C API documentation can be found in the [CUDA Toolkit Documentation](https://docs.nvidia.com/cuda/archive/10.0/nvgraph/index.html).



