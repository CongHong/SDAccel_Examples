Getting Started Examples
==================================
此页面包含Xilinx SDx OpenCL Flows新手的用户示例。这些示例的重点是针对Xilinx器件的代码优化。该表按用户可以遵循的建议顺序列出了各种类别的示例。


__前期准备__
 - 用户熟悉OpenCL流程的基础知识。
 - 用户已通过SDx教程，熟悉工具功能和术语的基础知识。

编号    | 目录       | 描述 
--------|-----------|-----------------------------------------
1 | [hello_world][]      |"Hello World"新用户示例
2 | [cpu_to_fpga][]      |实验室通过内核优化展示cpu到fpga的转换。
3 | [host][]      |OpenCL主机代码，用于优化与Xilinx器件的接口。
4 | [kernel_to_gmem][]      |内核到全局内存访问优化。
5 | [kernel_opt][]      |性能的内核优化。
6 | [dataflow][]      |通过宏级别流水线进行内核优化。
7 | [clk_freq][]      |通过优化代码提高内核时钟频率。
8 | [debug][]      |内核的调试和分析。
9 | [rtl_kernel][]      |基于RTL内核的示例。

 __实例列表__ 

实例           | 描述                  | 关键概念/关键词 
---------------|-----------------------|-------------------------
[hello_world/helloworld_c/][]|这是添加向量的简单示例，用于描述如何在Sdx环境中使用HLS内核。此示例突出显示像PIPELINE这样的概念，它可以提高内核性能。 |__Key__ __Concepts__<br> - HLS C Kernel<br> - OpenCL Host APIs<br>__Keywords__<br> - gmem<br> - bundle<br> - #pragma HLS INTERFACE<br> - m_axi<br> - s_axi4lite
[hello_world/helloworld_ocl/][]|这个例子是一个简单的OpenCL应用程序。它将突出显示OpenCL应用程序的基本流程。|__Key__ __Concepts__<br> - OpenCL API<br>
[cpu_to_fpga/00_cpu/][]|这是矩阵乘法（行 x 列）的简单示例。|
[cpu_to_fpga/01_ocl/][]|这是OpenCL矩阵乘法（行 x 列）的一个简单示例。|__Key__ __Concepts__<br> - OpenCL APIs<br>
[cpu_to_fpga/02_lmem_ocl/][]|这是矩阵乘法（行 x 列）的一个简单示例，用于演示如何使用本地内存减少内存访问次数。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Local Memory<br>
[cpu_to_fpga/03_burst_rw_ocl/][]|这是矩阵乘法（行 x 列）的一个简单示例，用于演示如何通过突发读取和写入本地存储器或DDR来实现更好的流水线。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Burst Read/Write<br>
[cpu_to_fpga/04_partition_ocl/][]|这是矩阵乘法（行 x 列）的一个简单示例，用于演示如何通过数组分区和循环展开来实现更好的性能。|__Key__ __Concepts__<br> - Array Partition<br> - Loop Unroll<br>__Keywords__<br> - xcl_pipeline_loop<br> - xcl_array_partition(complete, dim)<br> - opencl_unroll_hint
[host/concurrent_kernel_execution_c/][]|此示例将演示如何使用多个和乱序命令队列在FPGA上同时执行多个内核。|__Key__ __Concepts__<br> - Concurrent execution<br> - Out of Order Command Queues<br> - Multiple Command Queues<br>__Keywords__<br> - CL_QUEUE_OUT_OF_ORDER_EXEC_MODE_ENABLE<br> - clSetEventCallback()
[host/copy_buffer_c/][]|此复制缓冲区示例演示如何从一个缓冲区复制到另一个缓冲区。|__Key__ __Concepts__<br> - Copy Buffer<br>__Keywords__<br> - cl::CommandQueue::enqueueCopyBuffer()
[host/data_transfer_c/][]|此示例说明了使用OpenCL API向FPGA传输数据和从FPGA传输数据的几种方法。|__Key__ __Concepts__<br> - OpenCL API<br> - Data Transfer<br> - Write Buffers<br> - Read Buffers<br> - Map Buffers<br> - Async Memcpy<br>__Keywords__<br> - enqueueWriteBuffer()<br> - enqueueReadBuffer()<br> - enqueueMapBuffer()<br> - enqueueUnmapMemObject()<br> - enqueueMigrateMemObjects()
[host/device_query_c/][]|此示例打印平台及其设备的OpenCL属性。它还显示硬件的限制和功能。|__Key__ __Concepts__<br> - OpenCL API<br> - Querying device properties<br>__Keywords__<br> - clGetPlatformIDs()<br> - clGetPlatformInfo()<br> - clGetDeviceIDs()<br> - clGetDeviceInfo()
[host/device_query_cpp/][]|此示例使用OpenCL CPP API打印平台及其设备的OpenCL属性。它还显示硬件的限制和功能。|__Key__ __Concepts__<br> - OpenCL API<br> - Querying device properties<br>
[host/errors_c/][]|此示例讨论OpenCL中错误的不同原因以及如何在运行时处理它们。|__Key__ __Concepts__<br> - OpenCL API<br> - Error handling<br>__Keywords__<br> - CL_SUCCESS<br> - CL_DEVICE_NOT_FOUND<br> - CL_DEVICE_NOT_AVAILABLE
[host/errors_cpp/][]|此示例讨论了OpenCL C ++中出现错误的不同原因以及如何在运行时处理它们。|__Key__ __Concepts__<br> - OpenCL C++ API<br> - Error handling<br>__Keywords__<br> - CL_SUCCESS<br> - CL_DEVICE_NOT_FOUND<br> - CL_DEVICE_NOT_AVAILABLE<br> - CL_INVALID_VALUE<br> - CL_INVALID_KERNEL_NAME<br> - CL_INVALID_BUFFER_SIZE
[host/host_global_bandwidth/][]|主机到全局内存带宽测试。|
[host/kernel_swap_c/][]|此示例显示主机如何交换内核并在两个内核之间共享相同的缓冲区，这两个内核存在于单独的二进制容器中。动态平台不会保留缓冲区数据，因此主机必须在交换下一个内核之前将数据从设备迁移到主机内存。内核交换后，主机必须将缓冲区迁移回设备。|__Key__ __Concepts__<br> - Handling Buffer sharing across multiple binaries<br> - Multiple Kernel Binaries<br>__Keywords__<br> - clEnqueueMigrateMemObjects()<br> - CL_MIGRATE_MEM_OBJECT_HOST
[host/multiple_devices_c/][]|此示例显示如何在系统上利用多个FPGA。它将展示如何初始化OpenCL上下文，在两个设备上分配内存并在每个FPGA上执行内核。|__Key__ __Concepts__<br> - OpenCL API<br> - Multi-FPGA Execution<br> - Event Handling<br>__Keywords__<br> - cl_device_id<br> - clGetDeviceIDs()
[host/multiple_process_c/][]|此示例将演示如何运行多个进程以在FPGA设备上同时使用多个内核。如果每个进程使用相同的xclbin，则多个进程可以共享对同一设备的访问。进程共享对所有设备资源的访问权限，但不支持任何进程对资源的独占访问。|__Key__ __Concepts__<br> - Concurrent execution<br> - Multiple HLS kernels<br> - Multiple Process Support<br>__Keywords__<br> - PID<br> - fork<br> - XCL_MULTIPROCESS_MODE<br> - multiprocess
[host/overlap_c/][]|此示例演示了允许用户在应用程序中重叠主机（CPU）和FPGA计算的技术。它将涵盖异步操作和事件对象。|__Key__ __Concepts__<br> - OpenCL API<br> - Synchronize Host and FPGA<br> - Asynchronous Processing<br> - Events<br> - Asynchronous memcpy<br>__Keywords__<br> - cl_event<br> - clCreateCommandQueue<br> - CL_QUEUE_OUT_OF_ORDER_EXEC_MODE_ENABLE<br> - clEnqueueMigrateMemObjects
[host/stream_access_c/][]|这是一个简单的示例，演示了如何处理输入数据流以便在应用程序中进行计算。它显示了如何执行异步操作和事件处理。|__Key__ __Concepts__<br> - OpenCL API<br> - Synchronize Host and FPGA<br> - Asynchronous Processing<br> - Events<br> - Asynchronous Data Transfer<br>__Keywords__<br> - cl::event<br> - CL_QUEUE_OUT_OF_ORDER_EXEC_MODE_ENABLE
[host/sub_devices_c/][]|此示例演示如何创建多次使用单个内核的OpenCL子设备，以显示如何独立处理每个实例，包括独立缓冲区，命令队列和排序。|__Key__ __Concepts__<br> - Sub Devices<br>__Keywords__<br> - cl_device_partition_property<br> - createSubDevices<br> - CL_DEVICE_PARTITION_EQUALLY
[kernel_to_gmem/burst_rw_c/][]|这是使用AXI4主接口进行突发读写的简单示例。|__Key__ __Concepts__<br> - burst access<br>__Keywords__<br> - memcpy<br> - max_read_burst_length<br> - max_write_burst_length
[kernel_to_gmem/burst_rw_ocl/][]|这是使用AXI4主接口进行突发读写的简单示例|__Key__ __Concepts__<br> - burst access<br>__Keywords__<br> - param:compiler.interfaceWrBurstLen<br> - param:compiler.interfaceRdBurstLen
[kernel_to_gmem/custom_datatype_c/][]|这是RGB到HSV转换的简单示例，用于演示基于C的内核中的自定义数据类型用法。 Xilinx HLS编译器支持自定义数据类型，用于内核和全局内存之间的操作和内存接口。|__Key__ __Concepts__<br> - Custom Datatype<br>__Keywords__<br> - struct<br> - #pragma HLS data_pack<br> - #pragma HLS LOOP_TRIPCOUNT
[kernel_to_gmem/custom_datatype_ocl/][]|This is simple example of RGB to HSV conversion to demonstrate Custom DATA Type usages in OpenCL Based Kernel. Xilinx HLS Compiler Supports Custom Data Type to use for operation as well as Memory Interface between Kernel and Global Memory.|__Key__ __Concepts__<br> - Dataflow<br> - Custom Datatype<br>__Keywords__<br> - struct
[kernel_to_gmem/full_array_2d_c/][]|This is a simple example of accessing full data from 2d array|__Key__ __Concepts__<br> - 2D data full array Access<br>
[kernel_to_gmem/full_array_2d_ocl/][]|This is a simple example of accessing full data from 2d array|__Key__ __Concepts__<br> - 2D data full array Access<br>
[kernel_to_gmem/gmem_2banks_c/][]|This example of 2ddr to demonstrate on how to use 2ddr DSA. How to create buffers in each DDR.|__Key__ __Concepts__<br> - Multiple Banks<br>__Keywords__<br> - max_memory_ports<br> - misc:map_connect<br> - XCL_MEM_DDR_BANK0<br> - XCL_MEM_DDR_BANK1<br> - XCL_MEM_DDR_BANKx<br> - HLS Interface m_axi bundle
[kernel_to_gmem/gmem_2banks_ocl/][]|This example of 2ddr to demonstrate on how to use 2ddr DSA. How to create buffers in each DDR.|__Key__ __Concepts__<br> - Multiple Banks<br>__Keywords__<br> - max_memory_ports<br> - misc:map_connect<br> - XCL_MEM_DDR_BANK0<br> - XCL_MEM_DDR_BANK1<br> - XCL_MEM_DDR_BANKx
[kernel_to_gmem/kernel_global_bandwidth/][]|Bandwidth test of global to local memory.|
[kernel_to_gmem/memcoalesce_hang_c/][]|This example shows Memory Coalesce Deadlock/Hand situation and how to handle it. User can switch between BAD and GOOD case using makefile variable KFLOW.|__Key__ __Concepts__<br> - Memory Coalesce<br> - Memory Deadlock/Hang<br> - Multiple Interfaces<br>__Keywords__<br> - HLS INTERFACE<br> - bundle<br> - m_axi
[kernel_to_gmem/plram_access_c/][]|This example shows the usage of PLRAM and how to use it with simple matrix multiplication (Row x Col).|__Key__ __Concepts__<br> - SDx Memory Hierarchy<br> - PLRAMs<br>__Keywords__<br> - PLRAM
[kernel_to_gmem/row_array_2d_c/][]|This is a simple example of accessing each row of data from 2d array|__Key__ __Concepts__<br> - Row of 2D data array access<br>__Keywords__<br> - hls::stream
[kernel_to_gmem/row_array_2d_ocl/][]|This is a simple example of accessing each row of data from 2d array|__Key__ __Concepts__<br> - Row of 2D data array access<br>__Keywords__<br> - xcl_dataflow<br> - xcl_pipeline_loop
[kernel_to_gmem/slr_assign/][]|This is simple example to describe SLR assignment information for a platform design. This example highlights how to provide extra input to assign the logic of the kernel into a nominated SLR. In this example we are assigning first kernel(Vector Multiplication) to SLR0 and assigning the second kernel(Vector Addition) to SLR1|__Key__ __Concepts__<br> - SLR Assignments<br>__Keywords__<br> - slr
[kernel_to_gmem/wide_mem_rw_c/][]|This is simple example of vector addition to demonstrate Wide Memory Access using ap_uint<512> data type. Based on input argument type, xocc compiler will figure our the memory datawidth between Global Memory and Kernel. For this example, ap_uint<512> datatype is used, so Memory datawidth will be 16 x (integer bit size) = 16 x 32 = 512 bit.|__Key__ __Concepts__<br> - Kernel to DDR<br> - wide memory access<br> - burst read and write<br>__Keywords__<br> - ap_uint<><br> - ap_int.h
[kernel_to_gmem/wide_mem_rw_ocl/][]|This is simple example of vector addition to demonstrate Wide Memory Access using uint16 data type. Based on input argument type, xocc compiler will figure our the memory datawidth between Global Memory and Kernel. For this example, uint16 datatype is used, so Memory datawidth will be 16 x (integer bit size) = 16 x 32 = 512 bit.|__Key__ __Concepts__<br> - Kernel to DDR<br> - wide memory access<br> - burst read and write<br>__Keywords__<br> - uint16<br> - xcl_pipeline_loop
[kernel_to_gmem/window_array_2d_c/][]|This is a simple example of accessing each window of data from 2d array|__Key__ __Concepts__<br> - window of 2D data array access<br>__Keywords__<br> - #pragma HLS DATAFLOW<br> - #pragma HLS PIPELINE<br> - #pragma HLS stream
[kernel_to_gmem/window_array_2d_ocl/][]|This is a simple example of accessing each window of data from 2d array|__Key__ __Concepts__<br> - window/tile of 2D data array access<br>__Keywords__<br> - pipe<br> - xcl_pipeline_loop<br> - xcl_reqd_pipe_depth
[kernel_opt/aos_vs_soa_ocl/][]|This example demonstrates how data layout can impact the performance of certain kernels. The example we will demonstrate how using the Structure of Array data layout can impact certain data parallel problems.|__Key__ __Concepts__<br> - Kernel Optimization<br> - Data Layout<br>
[kernel_opt/array_partition_c/][]|This is a simple example of matrix multiplication (Row x Col) to demonstrate how to achieve better performance by array partitioning, using HLS kernel in SDx Environment.|__Key__ __Concepts__<br> - Kernel Optimization<br> - HLS C Kernel<br> - Array Partition<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION<br> - complete
[kernel_opt/array_partition_ocl/][]|This example shows how to use array partitioning to improve performance of a kernel|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br>__Keywords__<br> - xcl_array_partition<br> - complete
[kernel_opt/dependence_inter_c/][]|This Example demonstrates the HLS pragma 'DEPENDENCE'.Using 'DEPENDENCE' pragma, user can provide additional dependency details to the compiler by specifying if the dependency in consecutive loop iterations on buffer is true/false, which allows the compiler to perform unrolling/pipelining to get better performance.|__Key__ __Concepts__<br> - Inter Dependence<br>__Keywords__<br> - DEPENDENCE<br> - inter<br> - WAR
[kernel_opt/lmem_2rw_c/][]|This is simple example of vector addition to demonstrate how to utilized both ports of Local Memory memory.|__Key__ __Concepts__<br> - Kernel Optimization<br> - 2port BRAM Utilization<br> - two read/write Local Memory<br>__Keywords__<br> - #pragma HLS UNROLL FACTOR=2
[kernel_opt/lmem_2rw_ocl/][]|This is simple example of vector addition to demonstrate how to utilized both ports of Local Memory.|__Key__ __Concepts__<br> - Kernel Optimization<br> - 2port BRAM Utilization<br> - two read/write Local Memory<br>__Keywords__<br> - opencl_unroll_hint(2)
[kernel_opt/loop_fusion_c/][]|This example will demonstrate how to fuse two loops into one to improve the performance of an OpenCL  C/C++ Kernel.|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop Fusion<br> - Loop Pipelining<br>__Keywords__<br> - #pragma HLS PIPELINE
[kernel_opt/loop_fusion_ocl/][]|This example will demonstrate how to fuse two loops into one to improve the performance of an OpenCL kernel.|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop Fusion<br> - Loop Pipelining<br>__Keywords__<br> - xcl_pipeline_loop
[kernel_opt/loop_pipeline_ocl/][]|This example demonstrates how loop pipelining can be used to improve the performance of a kernel.|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop Pipelining<br>__Keywords__<br> - xcl_pipeline_loop
[kernel_opt/loop_reorder_c/][]|This is a simple example of matrix multiplication (Row x Col) to demonstrate how to achieve better pipeline II factor by loop reordering.|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop reorder to improve II<br>__Keywords__<br> - #pragma HLS PIPELINE<br> - #pragma HLS ARRAY_PARTITION
[kernel_opt/loop_reorder_ocl/][]|This is a simple example of matrix multiplication (Row x Col) to demonstrate how to achieve better pipeline II factor by loop reordering.|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop reorder to improve II<br>__Keywords__<br> - xcl_pipeline_loop<br> - xcl_array_partition(complete, 2)
[kernel_opt/partition_cyclicblock_c/][]|This example shows how to use array block and cyclic partitioning to improve performance of a kernel|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br> - Block Partition<br> - Cyclic Partition<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION<br> - cyclic<br> - block<br> - factor<br> - dim
[kernel_opt/partition_cyclicblock_ocl/][]|This example shows how to use array block and cyclic partitioning to improve performance of a kernel|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br> - Block Partition<br> - Cyclic Partition<br>__Keywords__<br> - xcl_array_partition<br> - cyclic<br> - block
[kernel_opt/shift_register_c/][]|This example demonstrates how to shift values in registers in each clock cycle|__Key__ __Concepts__<br> - Kernel Optimization<br> - Shift Register<br> - FIR<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION
[kernel_opt/shift_register_ocl/][]|This example demonstrates how to shift values in registers in each clock cycle|__Key__ __Concepts__<br> - Kernel Optimization<br> - Shift Register<br> - FIR<br>__Keywords__<br> - xcl_array_partition<br> - getprofilingInfo()
[kernel_opt/sum_scan_ocl/][]|This is a simple example to explain the usage of pipeline and array partitioning for designing parallel prefix sum |__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br> - Pipeline<br>__Keywords__<br> - xcl_array_partition<br> - xcl_pipeline_loop
[kernel_opt/systolic_array_c/][]|This is a simple example of matrix multiplication (Row x Col) to help developers learn systolic array based algorithm design. Note : Systolic array based algorithm design is well suited for FPGA.|
[kernel_opt/systolic_array_ocl/][]|This is a simple example of matrix multiplication (Row x Col) to help developers learn systolic array based algorithm design. Note: Systolic array based algorithm design is well suited for FPGA.|
[kernel_opt/vectorization_memorycoalescing_ocl/][]|This example is a simple OpenCL application which highlights the vectorization concept. It provides a basis for calculating the bandwidth utilization when the compiler looking to vectorize.|__Key__ __Concepts__<br> - Vectorization<br> - Memory Coalescing<br>__Keywords__<br> - vec_type_hint
[dataflow/dataflow_func_ocl/][]|This is simple example of vector addition to demonstrate Dataflow functionality in OpenCL Kernel. OpenCL Dataflow allows user to run multiple functions together to achieve higher throughput.|__Key__ __Concepts__<br> - Function/Task Level Parallelism<br>__Keywords__<br> - xcl_dataflow<br> - xclDataflowFifoDepth
[dataflow/dataflow_pipes_ocl/][]|This is simple example of vector addition to demonstrate OpenCL Pipe Memory usage. OpenCL PIPE memory functionality allows user to achieve kernel-to-kernel data transfer without using global memory.|__Key__ __Concepts__<br> - Dataflow<br> - kernel to kernel pipes<br>__Keywords__<br> - pipe<br> - xcl_reqd_pipe_depth<br> - read_pipe_block()<br> - write_pipe_block()
[dataflow/dataflow_stream_array_c/][]|This is simple example of Multiple Stages Vector Addition to demonstrate Array of Stream usage in HLS C Kernel Code.|__Key__ __Concepts__<br> - Array of Stream<br>__Keywords__<br> - dataflow<br> - hls::stream<>
[dataflow/dataflow_stream_c/][]|This is simple example of vector addition to demonstrate Dataflow functionality of HLS. HLS Dataflow allows user to schedule multiple task together to achieve higher throughput.|__Key__ __Concepts__<br> - Task Level Parallelism<br>__Keywords__<br> - dataflow<br> - hls::stream<>
[dataflow/dataflow_subfunc_ocl/][]|This is simple example of vector addition to demonstrate how OpenCL Dataflow allows user to run multiple sub functions together to achieve higher throughput.|__Key__ __Concepts__<br> - SubFunction Level Parallelism<br>__Keywords__<br> - xcl_dataflow<br> - xclDataflowFifoDepth
[clk_freq/critical_path_ocl/][]|This example shows a normal coding style which could lead to critical path issue and design will give degraded timing.  Example also contains better coding style which can improve design timing.|__Key__ __Concepts__<br> - Critical Path handling<br> - Improve Timing<br>
[clk_freq/large_loop_c/][]|This is a CNN (Convolutional Neural Network) based example which mainly focuses on Convolution operation of a CNN network. The goal of this example is to demonstrate a method to overcome kernel design timing failure issue. It also presents the effectiveness of using multiple compute units to improve performance.|__Key__ __Concepts__<br> - Clock Frequency<br> - Multiple Compute Units<br> - Convolutional Neural Networks<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION<br> - #pragma HLS PIPELINE<br> - #pragma HLS INLINE
[clk_freq/large_loop_ocl/][]|This is a CNN (Convolutional Neural Network) based example which mainly focuses on Convolution operation of a CNN network. The goal of this example is to demonstrate a method to overcome kernel design timing failure issue. It also presents the effectiveness of using multiple compute units to improve performance.|__Key__ __Concepts__<br> - Clock Frequency<br> - Multiple Compute Units<br> - Convolutional Neural Networks<br>__Keywords__<br> - xcl_array_partition<br> - xcl_pipeline_loop<br> - always_inline
[clk_freq/split_kernel_c/][]|This is a multi-filter image processing application to showcase effectiveness of Dataflow/Streams usage. This examples is intended to help developers to break down the complex kernels into multiple sub-functions using HLS Dataflow/Streams. It presents a way to concurrently execute multiple functions with better area utilization compared to a complex single kernel implementation. The main objective of this example is to showcase a way to build a optimal FPGA design which achieves maximum frequency with optimal resource utilization and achieves better performance compared to single complex kernel implementations.|__Key__ __Concepts__<br> - Dataflow<br> - Stream<br>__Keywords__<br> - #pragma HLS DATAFLOW<br> - hls::stream<br> - #pragma HLS INLINE<br> - #pragma HLS ARRAY_PARTITION<br> - #pragma HLS PIPELINE
[clk_freq/split_kernel_ocl/][]|This is a multi-filter image processing application to showcase effectiveness of Dataflow/Streams usage. This examples is intended to help developers to break down the complex kernel into multiple sub-functions using OpenCL Dataflow. It presents a way to concurrently execute multiple functions with better area utilization compared to a complex single kernel implementation. The main objective of this example is to showcase a way to build a optimal FPGA design which achieves maximum frequency with optimal resource utilization and achieves better performance compared to single kernel implementations.|__Key__ __Concepts__<br> - Dataflow<br> - Stream<br>__Keywords__<br> - xcl_dataflow<br> - xcl_array_partition<br> - xcl_pipeline_loop
[clk_freq/too_many_cu_c/][]|This is simple example of vector addition to demonstrate effectiveness of using single compute unit with heavy work load to achieve better performance. Bad example uses multiple compute units to achieve good performance but it results in heavy usage of FPGA resources and area due to which design fails timing. Good example uses single compute unit to compute with heavier work load, it helps in less resource utilization and also helps in kernel scalability. To switch between Good/Bad cases use the flag provided in makefile.|__Key__ __Concepts__<br> - Clock Frequency<br> - Data Level Parallelism<br> - Multiple Compute Units<br>__Keywords__<br> - #pragma HLS PIPELINE<br> - #pragma HLS ARRAY_PARTITION
[clk_freq/too_many_cu_ocl/][]|This is simple example of vector addition to demonstrate effectiveness of using single compute unit with heavy work load to achieve better performance. Bad example uses multiple compute units to achieve good performance but it results in heavy usage of FPGA resources and area due to which design fails timing. Good example uses single compute unit to compute with heavier work load, it helps in less resource utilization and also helps in kernel scalability. To switch between Good/Bad cases use the flag provided in makefile.|__Key__ __Concepts__<br> - Clock Frequency<br> - Data Level Parallelism<br> - Multiple Compute Units<br>__Keywords__<br> - xcl_array_partition(complete, 1)<br> - xcl_pipeline_loop
[debug/debug_printf_ocl/][]|This is simple example of vector addition and printing of data that is computational result (addition). It is based on vectored addition that demonstrates printing of work item data (integer product in this case)|__Key__ __Concepts__<br> - Use of print statements for debugging<br>__Keywords__<br> - printf<br> - param:compiler.enableAutoPipelining=false
[debug/debug_profile_ocl/][]|This is simple example of vector addition and printing profile data (wall clock time taken between start and stop). It also dump a waveform file which can be reloaded to vivado to see the waveform. Run command 'vivado -source ./scripts/open_waveform.tcl -tclargs <device_name>-<kernel_name>.<target>.<device_name>.wdb' to launch waveform viewer. User can also update batch to gui in sdaccel.ini file to see the live waveform while running application.|__Key__ __Concepts__<br> - Use of Profile API<br> - Waveform Dumping and loading<br>
[rtl_kernel/rtl_adder_pipes/][]|This example shows an adder with pipes using 3 RTL kernels.|__Key__ __Concepts__<br> - RTL Kernel<br> - Multiple RTL Kernels<br>
[rtl_kernel/rtl_vadd/][]|Simple example of vector addition using RTL Kernel|__Key__ __Concepts__<br> - RTL Kernel<br>
[rtl_kernel/rtl_vadd_2clks/][]|This example shows vector addition with 2 kernel clocks using RTL Kernel.|__Key__ __Concepts__<br> - RTL Kernel<br> - Multiple Kernel Clocks<br>__Keywords__<br> - --kernel_frequency
[rtl_kernel/rtl_vadd_2kernels/][]|This example has two RTL Kernels. Both Kernel_0 and Kernel_1 perform vector addition. The Kernel_1 reads the output from Kernel_0 as one of two inputs.|__Key__ __Concepts__<br> - Multiple RTL Kernels<br>
[rtl_kernel/rtl_vadd_hw_debug/][]|This is an example that showcases the Hardware Debug of Vector Addition RTL Kernel in Hardware.|__Key__ __Concepts__<br> - RTL Kernel Debug<br>
[rtl_kernel/rtl_vadd_mixed_cl_vadd/][]|This example has one RTL kernel and one CL kernel. Both RTL kernel and CL kernel perform vector addition. The CL kernel reads the output from RTL kernel as one of two inputs.|__Key__ __Concepts__<br> - Mixed Kernels<br>

[hello_world]:hello_world
[hello_world/helloworld_c/]:hello_world/helloworld_c/
[hello_world/helloworld_ocl/]:hello_world/helloworld_ocl/
[cpu_to_fpga]:cpu_to_fpga
[cpu_to_fpga/00_cpu/]:cpu_to_fpga/00_cpu/
[cpu_to_fpga/01_ocl/]:cpu_to_fpga/01_ocl/
[cpu_to_fpga/02_lmem_ocl/]:cpu_to_fpga/02_lmem_ocl/
[cpu_to_fpga/03_burst_rw_ocl/]:cpu_to_fpga/03_burst_rw_ocl/
[cpu_to_fpga/04_partition_ocl/]:cpu_to_fpga/04_partition_ocl/
[host]:host
[host/concurrent_kernel_execution_c/]:host/concurrent_kernel_execution_c/
[host/copy_buffer_c/]:host/copy_buffer_c/
[host/data_transfer_c/]:host/data_transfer_c/
[host/device_query_c/]:host/device_query_c/
[host/device_query_cpp/]:host/device_query_cpp/
[host/errors_c/]:host/errors_c/
[host/errors_cpp/]:host/errors_cpp/
[host/host_global_bandwidth/]:host/host_global_bandwidth/
[host/kernel_swap_c/]:host/kernel_swap_c/
[host/multiple_devices_c/]:host/multiple_devices_c/
[host/multiple_process_c/]:host/multiple_process_c/
[host/overlap_c/]:host/overlap_c/
[host/stream_access_c/]:host/stream_access_c/
[host/sub_devices_c/]:host/sub_devices_c/
[kernel_to_gmem]:kernel_to_gmem
[kernel_to_gmem/burst_rw_c/]:kernel_to_gmem/burst_rw_c/
[kernel_to_gmem/burst_rw_ocl/]:kernel_to_gmem/burst_rw_ocl/
[kernel_to_gmem/custom_datatype_c/]:kernel_to_gmem/custom_datatype_c/
[kernel_to_gmem/custom_datatype_ocl/]:kernel_to_gmem/custom_datatype_ocl/
[kernel_to_gmem/full_array_2d_c/]:kernel_to_gmem/full_array_2d_c/
[kernel_to_gmem/full_array_2d_ocl/]:kernel_to_gmem/full_array_2d_ocl/
[kernel_to_gmem/gmem_2banks_c/]:kernel_to_gmem/gmem_2banks_c/
[kernel_to_gmem/gmem_2banks_ocl/]:kernel_to_gmem/gmem_2banks_ocl/
[kernel_to_gmem/kernel_global_bandwidth/]:kernel_to_gmem/kernel_global_bandwidth/
[kernel_to_gmem/memcoalesce_hang_c/]:kernel_to_gmem/memcoalesce_hang_c/
[kernel_to_gmem/plram_access_c/]:kernel_to_gmem/plram_access_c/
[kernel_to_gmem/row_array_2d_c/]:kernel_to_gmem/row_array_2d_c/
[kernel_to_gmem/row_array_2d_ocl/]:kernel_to_gmem/row_array_2d_ocl/
[kernel_to_gmem/slr_assign/]:kernel_to_gmem/slr_assign/
[kernel_to_gmem/wide_mem_rw_c/]:kernel_to_gmem/wide_mem_rw_c/
[kernel_to_gmem/wide_mem_rw_ocl/]:kernel_to_gmem/wide_mem_rw_ocl/
[kernel_to_gmem/window_array_2d_c/]:kernel_to_gmem/window_array_2d_c/
[kernel_to_gmem/window_array_2d_ocl/]:kernel_to_gmem/window_array_2d_ocl/
[kernel_opt]:kernel_opt
[kernel_opt/aos_vs_soa_ocl/]:kernel_opt/aos_vs_soa_ocl/
[kernel_opt/array_partition_c/]:kernel_opt/array_partition_c/
[kernel_opt/array_partition_ocl/]:kernel_opt/array_partition_ocl/
[kernel_opt/dependence_inter_c/]:kernel_opt/dependence_inter_c/
[kernel_opt/lmem_2rw_c/]:kernel_opt/lmem_2rw_c/
[kernel_opt/lmem_2rw_ocl/]:kernel_opt/lmem_2rw_ocl/
[kernel_opt/loop_fusion_c/]:kernel_opt/loop_fusion_c/
[kernel_opt/loop_fusion_ocl/]:kernel_opt/loop_fusion_ocl/
[kernel_opt/loop_pipeline_ocl/]:kernel_opt/loop_pipeline_ocl/
[kernel_opt/loop_reorder_c/]:kernel_opt/loop_reorder_c/
[kernel_opt/loop_reorder_ocl/]:kernel_opt/loop_reorder_ocl/
[kernel_opt/partition_cyclicblock_c/]:kernel_opt/partition_cyclicblock_c/
[kernel_opt/partition_cyclicblock_ocl/]:kernel_opt/partition_cyclicblock_ocl/
[kernel_opt/shift_register_c/]:kernel_opt/shift_register_c/
[kernel_opt/shift_register_ocl/]:kernel_opt/shift_register_ocl/
[kernel_opt/sum_scan_ocl/]:kernel_opt/sum_scan_ocl/
[kernel_opt/systolic_array_c/]:kernel_opt/systolic_array_c/
[kernel_opt/systolic_array_ocl/]:kernel_opt/systolic_array_ocl/
[kernel_opt/vectorization_memorycoalescing_ocl/]:kernel_opt/vectorization_memorycoalescing_ocl/
[dataflow]:dataflow
[dataflow/dataflow_func_ocl/]:dataflow/dataflow_func_ocl/
[dataflow/dataflow_pipes_ocl/]:dataflow/dataflow_pipes_ocl/
[dataflow/dataflow_stream_array_c/]:dataflow/dataflow_stream_array_c/
[dataflow/dataflow_stream_c/]:dataflow/dataflow_stream_c/
[dataflow/dataflow_subfunc_ocl/]:dataflow/dataflow_subfunc_ocl/
[clk_freq]:clk_freq
[clk_freq/critical_path_ocl/]:clk_freq/critical_path_ocl/
[clk_freq/large_loop_c/]:clk_freq/large_loop_c/
[clk_freq/large_loop_ocl/]:clk_freq/large_loop_ocl/
[clk_freq/split_kernel_c/]:clk_freq/split_kernel_c/
[clk_freq/split_kernel_ocl/]:clk_freq/split_kernel_ocl/
[clk_freq/too_many_cu_c/]:clk_freq/too_many_cu_c/
[clk_freq/too_many_cu_ocl/]:clk_freq/too_many_cu_ocl/
[debug]:debug
[debug/debug_printf_ocl/]:debug/debug_printf_ocl/
[debug/debug_profile_ocl/]:debug/debug_profile_ocl/
[rtl_kernel]:rtl_kernel
[rtl_kernel/rtl_adder_pipes/]:rtl_kernel/rtl_adder_pipes/
[rtl_kernel/rtl_vadd/]:rtl_kernel/rtl_vadd/
[rtl_kernel/rtl_vadd_2clks/]:rtl_kernel/rtl_vadd_2clks/
[rtl_kernel/rtl_vadd_2kernels/]:rtl_kernel/rtl_vadd_2kernels/
[rtl_kernel/rtl_vadd_hw_debug/]:rtl_kernel/rtl_vadd_hw_debug/
[rtl_kernel/rtl_vadd_mixed_cl_vadd/]:rtl_kernel/rtl_vadd_mixed_cl_vadd/
