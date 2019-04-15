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
[cpu_to_fpga/00_cpu/][]|这是矩阵乘法（Row x Col）的简单示例。|
[cpu_to_fpga/01_ocl/][]|这是OpenCL矩阵乘法（Row x Col）的一个简单示例。|__Key__ __Concepts__<br> - OpenCL APIs<br>
[cpu_to_fpga/02_lmem_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何使用本地内存减少内存访问次数。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Local Memory<br>
[cpu_to_fpga/03_burst_rw_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何通过突发读取和写入本地存储器或DDR来实现更好的流水线。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Burst Read/Write<br>
[cpu_to_fpga/04_partition_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何通过数组分区和循环展开来实现更好的性能。|__Key__ __Concepts__<br> - Array Partition<br> - Loop Unroll<br>__Keywords__<br> - xcl_pipeline_loop<br> - xcl_array_partition(complete, dim)<br> - opencl_unroll_hint
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
[kernel_to_gmem/custom_datatype_ocl/][]|这是RGB到HSV转换的简单示例，用于演示基于OpenCL的内核中的自定义数据类型用法。 Xilinx HLS编译器支持自定义数据类型，用于内核和全局内存之间的操作和内存接口。|__Key__ __Concepts__<br> - Dataflow<br> - Custom Datatype<br>__Keywords__<br> - struct
[kernel_to_gmem/full_array_2d_c/][]|这是从2d数组访问完整数据的简单示例|__Key__ __Concepts__<br> - 2D data full array Access<br>
[kernel_to_gmem/full_array_2d_ocl/][]|这是从2d数组访问完整数据的简单示例|__Key__ __Concepts__<br> - 2D data full array Access<br>
[kernel_to_gmem/gmem_2banks_c/][]|这个2ddr的例子演示了如何使用2ddr DSA。如何在每个DDR中创建缓冲区。|__Key__ __Concepts__<br> - Multiple Banks<br>__Keywords__<br> - max_memory_ports<br> - misc:map_connect<br> - XCL_MEM_DDR_BANK0<br> - XCL_MEM_DDR_BANK1<br> - XCL_MEM_DDR_BANKx<br> - HLS Interface m_axi bundle
[kernel_to_gmem/gmem_2banks_ocl/][]|这个2ddr的例子演示了如何使用2ddr DSA。如何在每个DDR中创建缓冲区。|__Key__ __Concepts__<br> - Multiple Banks<br>__Keywords__<br> - max_memory_ports<br> - misc:map_connect<br> - XCL_MEM_DDR_BANK0<br> - XCL_MEM_DDR_BANK1<br> - XCL_MEM_DDR_BANKx
[kernel_to_gmem/kernel_global_bandwidth/][]|全局到本地内存的带宽测试。|
[kernel_to_gmem/memcoalesce_hang_c/][]|此示例显示了Memory Coalesce Deadlock / Hand情况以及如何处理它。用户可以使用makefile变量KFLOW在BAD和GOOD之间切换。|__Key__ __Concepts__<br> - Memory Coalesce<br> - Memory Deadlock/Hang<br> - Multiple Interfaces<br>__Keywords__<br> - HLS INTERFACE<br> - bundle<br> - m_axi
[kernel_to_gmem/plram_access_c/][]|此示例显示了PLRAM的用法以及如何将其与简单矩阵乘法（Row x Col）一起使用。|__Key__ __Concepts__<br> - SDx Memory Hierarchy<br> - PLRAMs<br>__Keywords__<br> - PLRAM
[kernel_to_gmem/row_array_2d_c/][]|这是从2d数组访问每行数据的简单示例。|__Key__ __Concepts__<br> - Row of 2D data array access<br>__Keywords__<br> - hls::stream
[kernel_to_gmem/row_array_2d_ocl/][]|这是从2d数组访问每行数据的简单示例。|__Key__ __Concepts__<br> - Row of 2D data array access<br>__Keywords__<br> - xcl_dataflow<br> - xcl_pipeline_loop
[kernel_to_gmem/slr_assign/][]|这是描述平台设计的SLR分配信息的简单示例。此示例重点介绍如何提供额外的输入以将内核的逻辑分配给指定的SLR。在这个例子中，我们将第一个内核（Vector Multiplication）分配给SLR0并将第二个内核（Vector Addition）分配给SLR1。|__Key__ __Concepts__<br> - SLR Assignments<br>__Keywords__<br> - slr
[kernel_to_gmem/wide_mem_rw_c/][]|这是使用ap_uint <512>数据类型演示宽内存访问的向量添加的简单示例。根据输入参数类型，xocc编译器将计算全局内存和内核之间的内存数据宽度。对于此示例，使用ap_uint <512>数据类型，因此内存数据宽度将为16 x（整数位大小）= 16 x 32 = 512位。|__Key__ __Concepts__<br> - Kernel to DDR<br> - wide memory access<br> - burst read and write<br>__Keywords__<br> - ap_uint<><br> - ap_int.h
[kernel_to_gmem/wide_mem_rw_ocl/][]|这是使用uint16数据类型演示宽内存访问的向量添加的简单示例。根据输入参数类型，xocc编译器将计算全局内存和内核之间的内存数据宽度。对于此示例，使用uint16数据类型，因此内存数据宽度将为16 x（整数位大小）= 16 x 32 = 512位。|__Key__ __Concepts__<br> - Kernel to DDR<br> - wide memory access<br> - burst read and write<br>__Keywords__<br> - uint16<br> - xcl_pipeline_loop
[kernel_to_gmem/window_array_2d_c/][]|这是从2d数组访问每个数据窗口的简单示例。|__Key__ __Concepts__<br> - window of 2D data array access<br>__Keywords__<br> - #pragma HLS DATAFLOW<br> - #pragma HLS PIPELINE<br> - #pragma HLS stream
[kernel_to_gmem/window_array_2d_ocl/][]|这是从2d数组访问每个数据窗口的简单示例。|__Key__ __Concepts__<br> - window/tile of 2D data array access<br>__Keywords__<br> - pipe<br> - xcl_pipeline_loop<br> - xcl_reqd_pipe_depth
[kernel_opt/aos_vs_soa_ocl/][]|此示例演示了数据布局如何影响某些内核的性能。我们将演示如何使用Array of Array数据布局如何影响某些数据并行问题。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Data Layout<br>
[kernel_opt/array_partition_c/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何使用SDx环境中的HLS内核通过数组分区实现更好的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - HLS C Kernel<br> - Array Partition<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION<br> - complete
[kernel_opt/array_partition_ocl/][]|此示例显示如何使用数组分区来提高内核的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br>__Keywords__<br> - xcl_array_partition<br> - complete
[kernel_opt/dependence_inter_c/][]|此示例演示了HLS编译指示'DEPENDENCE'。使用'DEPENDENCE'编译指示，用户可以通过指定缓冲区上连续循环迭代中的依赖项是否为true / false来向编译器提供其他依赖项详细信息，这允许编译器执行展开/流水线操作获得更好的表现。|__Key__ __Concepts__<br> - Inter Dependence<br>__Keywords__<br> - DEPENDENCE<br> - inter<br> - WAR
[kernel_opt/lmem_2rw_c/][]|这是向量添加的简单示例，用于演示如何利用本地存储器的两个端口。|__Key__ __Concepts__<br> - Kernel Optimization<br> - 2port BRAM Utilization<br> - two read/write Local Memory<br>__Keywords__<br> - #pragma HLS UNROLL FACTOR=2
[kernel_opt/lmem_2rw_ocl/][]|这是添加向量的简单示例，用于演示如何利用本地内存的两个端口。|__Key__ __Concepts__<br> - Kernel Optimization<br> - 2port BRAM Utilization<br> - two read/write Local Memory<br>__Keywords__<br> - opencl_unroll_hint(2)
[kernel_opt/loop_fusion_c/][]|此示例将演示如何将两个循环融合为一个以提高OpenCL C / C ++内核的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop Fusion<br> - Loop Pipelining<br>__Keywords__<br> - #pragma HLS PIPELINE
[kernel_opt/loop_fusion_ocl/][]|此示例将演示如何将两个循环融合为一个以提高OpenCL内核的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop Fusion<br> - Loop Pipelining<br>__Keywords__<br> - xcl_pipeline_loop
[kernel_opt/loop_pipeline_ocl/][]|此示例演示了如何使用循环流水线来提高内核的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop Pipelining<br>__Keywords__<br> - xcl_pipeline_loop
[kernel_opt/loop_reorder_c/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何通过循环重新排序实现更好的流水线II因子。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop reorder to improve II<br>__Keywords__<br> - #pragma HLS PIPELINE<br> - #pragma HLS ARRAY_PARTITION
[kernel_opt/loop_reorder_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，用于演示如何通过循环重新排序实现更好的流水线II因子。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Loop reorder to improve II<br>__Keywords__<br> - xcl_pipeline_loop<br> - xcl_array_partition(complete, 2)
[kernel_opt/partition_cyclicblock_c/][]|此示例显示如何使用数组块和循环分区来提高内核的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br> - Block Partition<br> - Cyclic Partition<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION<br> - cyclic<br> - block<br> - factor<br> - dim
[kernel_opt/partition_cyclicblock_ocl/][]|此示例显示如何使用数组块和循环分区来提高内核的性能。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br> - Block Partition<br> - Cyclic Partition<br>__Keywords__<br> - xcl_array_partition<br> - cyclic<br> - block
[kernel_opt/shift_register_c/][]|此示例演示如何在每个时钟周期中移位寄存器中的值。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Shift Register<br> - FIR<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION
[kernel_opt/shift_register_ocl/][]|此示例演示如何在每个时钟周期中移位寄存器中的值。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Shift Register<br> - FIR<br>__Keywords__<br> - xcl_array_partition<br> - getprofilingInfo()
[kernel_opt/sum_scan_ocl/][]|这是一个简单的例子来解释用于设计并行前缀和的管道和数组分区的用法。|__Key__ __Concepts__<br> - Kernel Optimization<br> - Array Partitioning<br> - Pipeline<br>__Keywords__<br> - xcl_array_partition<br> - xcl_pipeline_loop
[kernel_opt/systolic_array_c/][]|这是矩阵乘法（Row x Col）的一个简单示例，可帮助开发人员学习基于脉动阵列的算法设计。注意：基于脉动阵列的算法设计非常适合FPGA。|
[kernel_opt/systolic_array_ocl/][]|这是矩阵乘法（Row x Col）的一个简单示例，可帮助开发人员学习基于脉动阵列的算法设计。注意：基于脉动阵列的算法设计非常适合FPGA。|
[kernel_opt/vectorization_memorycoalescing_ocl/][]|这个例子是一个简单的OpenCL应用程序，它突出了矢量化概念。它为编译器寻求矢量化时计算带宽利用率提供了基础。|__Key__ __Concepts__<br> - Vectorization<br> - Memory Coalescing<br>__Keywords__<br> - vec_type_hint
[dataflow/dataflow_func_ocl/][]|这是添加向量的简单示例，用于演示OpenCL内核中的Dataflow功能。 OpenCL Dataflow允许用户一起运行多个功能以实现更高的吞吐量。|__Key__ __Concepts__<br> - Function/Task Level Parallelism<br>__Keywords__<br> - xcl_dataflow<br> - xclDataflowFifoDepth
[dataflow/dataflow_pipes_ocl/][]|这是向量添加的简单示例，用于演示OpenCL管道内存使用情况。 OpenCL PIPE内存功能允许用户在不使用全局内存的情况下实现内核到内核的数据传输。|__Key__ __Concepts__<br> - Dataflow<br> - kernel to kernel pipes<br>__Keywords__<br> - pipe<br> - xcl_reqd_pipe_depth<br> - read_pipe_block()<br> - write_pipe_block()
[dataflow/dataflow_stream_array_c/][]|这是多阶段向量添加的简单示例，用于演示HLS C内核代码中的流使用数组。|__Key__ __Concepts__<br> - Array of Stream<br>__Keywords__<br> - dataflow<br> - hls::stream<>
[dataflow/dataflow_stream_c/][]|这是向量添加的简单示例，用于演示HLS的数据流功能。 HLS Dataflow允许用户一起安排多个任务以实现更高的吞吐量。|__Key__ __Concepts__<br> - Task Level Parallelism<br>__Keywords__<br> - dataflow<br> - hls::stream<>
[dataflow/dataflow_subfunc_ocl/][]|这是添加向量的简单示例，用于演示OpenCL Dataflow如何允许用户一起运行多个子功能以实现更高的吞吐量。|__Key__ __Concepts__<br> - SubFunction Level Parallelism<br>__Keywords__<br> - xcl_dataflow<br> - xclDataflowFifoDepth
[clk_freq/critical_path_ocl/][]|此示例显示了正常的编码样式，这可能导致关键路径问题，并且设计会降低时序。示例还包含更好的编码风格，可以改善设计时序。|__Key__ __Concepts__<br> - Critical Path handling<br> - Improve Timing<br>
[clk_freq/large_loop_c/][]|这是基于CNN（卷积神经网络）的示例，其主要关注于CNN网络的卷积操作。此示例的目标是演示克服内核设计时序故障问题的方法。它还介绍了使用多个计算单元来提高性能的有效性。|__Key__ __Concepts__<br> - Clock Frequency<br> - Multiple Compute Units<br> - Convolutional Neural Networks<br>__Keywords__<br> - #pragma HLS ARRAY_PARTITION<br> - #pragma HLS PIPELINE<br> - #pragma HLS INLINE
[clk_freq/large_loop_ocl/][]|这是基于CNN（卷积神经网络）的示例，其主要关注于CNN网络的卷积操作。此示例的目标是演示克服内核设计时序故障问题的方法。它还介绍了使用多个计算单元来提高性能的有效性。|__Key__ __Concepts__<br> - Clock Frequency<br> - Multiple Compute Units<br> - Convolutional Neural Networks<br>__Keywords__<br> - xcl_array_partition<br> - xcl_pipeline_loop<br> - always_inline
[clk_freq/split_kernel_c/][]|这是一个多过滤器图像处理应用程序，用于展示Dataflow / Streams使用的有效性。此示例旨在帮助开发人员使用HLS Dataflow / Streams将复杂内核分解为多个子功能。与复杂的单个内核实现相比，它提供了一种同时执行多个功能并具有更好区域利用率的方法。此示例的主要目的是展示一种构建最佳FPGA设计的方法，该设计可实现最佳频率和最佳资源利用率，并且与单个复杂内核实现相比，可实现更好的性能。|__Key__ __Concepts__<br> - Dataflow<br> - Stream<br>__Keywords__<br> - #pragma HLS DATAFLOW<br> - hls::stream<br> - #pragma HLS INLINE<br> - #pragma HLS ARRAY_PARTITION<br> - #pragma HLS PIPELINE
[clk_freq/split_kernel_ocl/][]|这是一个多过滤器图像处理应用程序，用于展示Dataflow / Streams使用的有效性。此示例旨在帮助开发人员使用OpenCL Dataflow将复杂内核分解为多个子功能。与复杂的单个内核实现相比，它提供了一种同时执行多个功能并具有更好区域利用率的方法。此示例的主要目的是展示一种构建最佳FPGA设计的方法，该设计可实现最佳频率和最佳资源利用率，并且与单核实现相比，可实现更好的性能。|__Key__ __Concepts__<br> - Dataflow<br> - Stream<br>__Keywords__<br> - xcl_dataflow<br> - xcl_array_partition<br> - xcl_pipeline_loop
[clk_freq/too_many_cu_c/][]|这是添加矢量的简单示例，以证明使用具有繁重工作负载的单个计算单元以实现更好性能的有效性。不好的例子使用多个计算单元来实现良好的性能，但由于设计失败，导致FPGA资源和面积的大量使用。好的示例使用单个计算单元来计算较重的工作负载，它有助于减少资源利用率并有助于内核可伸缩性。要在Good / Bad情况之间切换，请使用makefile中提供的标志。|__Key__ __Concepts__<br> - Clock Frequency<br> - Data Level Parallelism<br> - Multiple Compute Units<br>__Keywords__<br> - #pragma HLS PIPELINE<br> - #pragma HLS ARRAY_PARTITION
[clk_freq/too_many_cu_ocl/][]|这是添加矢量的简单示例，以证明使用具有繁重工作负载的单个计算单元以实现更好性能的有效性。不好的例子使用多个计算单元来实现良好的性能，但由于设计失败，导致FPGA资源和面积的大量使用。好的示例使用单个计算单元来计算较重的工作负载，它有助于减少资源利用率并有助于内核可伸缩性。要在Good / Bad情况之间切换，请使用makefile中提供的标志。|__Key__ __Concepts__<br> - Clock Frequency<br> - Data Level Parallelism<br> - Multiple Compute Units<br>__Keywords__<br> - xcl_array_partition(complete, 1)<br> - xcl_pipeline_loop
[debug/debug_printf_ocl/][]|这是作为计算结果（加法）的向量添加和数据打印的简单示例。它基于向量添加，演示了工作项数据的打印（在这种情况下为整数乘积）|__Key__ __Concepts__<br> - Use of print statements for debugging<br>__Keywords__<br> - printf<br> - param:compiler.enableAutoPipelining=false
[debug/debug_profile_ocl/][]|这是矢量添加和打印配置文件数据（开始和停止之间的挂钟时间）的简单示例。它还会转储一个波形文件，可以将其重新加载到vivado以查看波形。运行命令“vivado -source ./scripts/open_waveform.tcl -tclargs <device_name>-<kernel_name>.<target>.<device_name>.wdb”以启动波形查看器。用户还可以在sdaccel.ini文件中将批处理更新为gui，以便在运行应用程序时查看实时波形。|__Key__ __Concepts__<br> - Use of Profile API<br> - Waveform Dumping and loading<br>
[rtl_kernel/rtl_adder_pipes/][]|此示例显示了一个使用3个RTL内核的管道的加法器。|__Key__ __Concepts__<br> - RTL Kernel<br> - Multiple RTL Kernels<br>
[rtl_kernel/rtl_vadd/][]|使用RTL内核添加向量的简单示例。|__Key__ __Concepts__<br> - RTL Kernel<br>
[rtl_kernel/rtl_vadd_2clks/][]|此示例使用RTL内核显示带有2个内核时钟的向量加法。|__Key__ __Concepts__<br> - RTL Kernel<br> - Multiple Kernel Clocks<br>__Keywords__<br> - --kernel_frequency
[rtl_kernel/rtl_vadd_2kernels/][]|此示例有两个RTL内核。 Kernel_0和Kernel_1都执行向量加法。 Kernel_1将Kernel_0的输出读取为两个输入之一。|__Key__ __Concepts__<br> - Multiple RTL Kernels<br>
[rtl_kernel/rtl_vadd_hw_debug/][]|这是一个展示硬件中向量加法RTL内核的硬件调试的示例。|__Key__ __Concepts__<br> - RTL Kernel Debug<br>
[rtl_kernel/rtl_vadd_mixed_cl_vadd/][]|此示例具有一个RTL内核和一个CL内核。 RTL内核和CL内核都执行向量添加。 CL内核将RTL内核的输出读取为两个输入之一。|__Key__ __Concepts__<br> - Mixed Kernels<br>

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
