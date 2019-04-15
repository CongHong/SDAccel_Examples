CPU to FPGA Examples
==================================
Labs to showcase the cpu to fpga conversion with kernel optimizations.

 __Examples Table__ 

Example        | Description           | Key Concepts / Keywords 
---------------|-----------------------|-------------------------
[00_cpu/][]|这是矩阵乘法（Row x Col）的简单示例。|
[01_ocl/][]|这是OpenCL矩阵乘法（Row x Col）的一个简单示例。|__Key__ __Concepts__<br> - OpenCL APIs<br>
[02_lmem_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何使用本地内存减少内存访问次数。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Local Memory<br>
[03_burst_rw_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何通过突发读取和写入本地存储器从/向DDR来实现更好的流水线。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Burst Read/Write<br>
[04_partition_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何通过数组分区和循环展开来实现更好的性能。|__Key__ __Concepts__<br> - Array Partition<br> - Loop Unroll<br>__Keywords__<br> - xcl_pipeline_loop<br> - xcl_array_partition(complete, dim)<br> - opencl_unroll_hint

[.]:.
[00_cpu/]:00_cpu/
[01_ocl/]:01_ocl/
[02_lmem_ocl/]:02_lmem_ocl/
[03_burst_rw_ocl/]:03_burst_rw_ocl/
[04_partition_ocl/]:04_partition_ocl/
