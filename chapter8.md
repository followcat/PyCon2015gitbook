# Python & LLVM

## Python Binding for LLVM


LLVM C API:
    http://llvm.org/docs/doxygen/html/group_LLVMC.html

* [llvmpy](http://www.llvmpy.org)
  * REQUIRES_RTTI
* [llvmlite](https://github.com/numba/llvmlite)
    * /llvmlite/binding/ir
* HPC
    * Heterogeneous Parallel Computing
    * High Performance Computing
      * NVCC: CUDA compiler
      * CICC: LLVM based hgih level optimizer and PTX generator
      * PTX: Virtual Instruction Set
* Anaconda

## Debugging
1. [LLDB](http://lldb.llvm.org)
    * source/core/PluginManager.cpp
2. [LLDB-Capstone](https://github.com/upbit/lldb-capstone-arm.git)
    * dis_capstone.py