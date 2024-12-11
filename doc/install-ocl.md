# AdaptiveCpp installation instructions for SPIR-V/OpenCL

You will need an OpenCL implementation, and the OpenCL icd loader. The OpenCL library can be specified using `cmake -DOpenCL_LIBRARY=/path/to/libOpenCL.so`.

The OpenCL backend can be enabled using `cmake -DWITH_OPENCL_BACKEND=ON` when building AdaptiveCpp.
In order to run code successfully on an OpenCL device, it must support SPIR-V ingestion and the Intel USM (unified shared memory) extension. In a degraded mode, devices supporting OpenCL fine-grained system SVM (shared virtual memory) may work as well.

This is a sample command to activate OpenCL backend:
*  OpenCL backend is only available with `-DWITH_SSCP_COMPILER=ON` to generate SPIRV code
* `OCL_HEADERS`, `OCL_CXX_HEADERS`, and `LLVM_SPIRVTRANS` are optional
* The latest `OCL_CXX_HEADERS` can lead to compilation failed. Release 2023.12.14 is tested and it is compatiable.

```sh
cmake -B build -S . -G Ninja -DCMAKE_BUILD_TYPE=Debug \
-DCMAKE_EXPORT_COMPILE_COMMANDS=ON  -DCMAKE_INSTALL_PREFIX=<install-prefix> \
-DCMAKE_CXX_COMPILER=g++ -DCMAKE_C_COMPILER=gcc  \
-DBOOST_ROOT=/thfs1/home/penglin_jianbin/lhz/opt/boost \
-DWITH_SSCP_COMPILER=ON -DWITH_OPENCL_BACKEND=ON  \
-DWITH_LEVEL_ZERO_BACKEND=OFF -DWITH_STDPAR_COMPILER=OFF \
-DOpenCLICDLoader_DIR=<oclicd-install-dir>/share/cmake/OpenCLICDLoader \
-DOpenCL_LIBRARY=<oclicd-insatll-dir>/lib/libOpenCL.so \
-DOCL_HEADERS=<src-of-OpenCL-Headers> \
-DOCL_CXX_HEADERS=<src-of-OpenCL-CLHPP> \
-DLLVM_SPIRVTRANS=<src-of-SPIRV-LLVM-Translator>
```
