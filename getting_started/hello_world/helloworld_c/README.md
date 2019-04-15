Hello World (HLS C/C++ Kernel)
======================

“README”文件包含以下部分：

1. 概述
2. 如何下载存储库
3. 软件工具和系统要求
4. 设计文件层次结构
5. 编制和执行
6. 在云环境中的执行
7. 支持
8. 许可和对存储的贡献
9. 致谢


## 1. 概述
这是添加向量的简单示例，用于描述如何在Sdx环境中使用HLS内核。此示例突出显示像PIPELINE这样的概念，它可以提高内核性能

***主要概念：*** HLS C内核，OpenCL主机API

***关键词:*** gmem, bundle, #pragma HLS INTERFACE, m_axi, s_axi4lite

## 2. 如何下载存储库
要获取SDAccel示例存储库的本地副本，请使用以下命令将此存储库克隆到本地系统：
```
git clone https://github.com/Xilinx/SDAccel_Examples examples
```
其中examples是存储库将存储在本地系统上的目录的名称。此命令只需执行一次即可检索所有SDAccel示例的最新版本。唯一需要的软件是git的本地安装。

## 3. 软件工具和系统要求
板卡  | 设备名称     | 软件版本
------|-------------|-----------------
Xilinx Alveo U250|xilinx_u250_xdma_201820_1|SDx 2018.3
Xilinx Kintex UltraScale KCU1500|xilinx_kcu1500_dynamic|SDx 2018.3
Xilinx Virtex UltraScale+ VCU1525|xilinx_vcu1525_dynamic|SDx 2018.3
Xilinx Alveo U200|xilinx_u200_xdma_201820_1|SDx 2018.3


*注意：*可以通过将DEVICES变量添加到make命令来更改用于编译的板/设备，如下所示
```
make DEVICES=<.xpfm file path> all
```
## 4. 设计文件层次结构
应用程序代码位于src目录中。加速器二进制文件将被编译到xclbin目录。 Makefile需要xclbin目录，并且在编译期间将填充其内容。此示例中的所有文件的列表如下所示

```
Makefile
README.md
description.json
qor.json
sdaccel.ini
src/host.cpp
src/vadd.cpp
utils.mk
```

## 5. 编制和执行
### 编译应用程序仿真
作为应用程序开发人员可用功能的一部分，SDAccel包括用于在软件功能级别和硬件模拟级别测试应用程序正确性的环境。
这些名为sw_emu和hw_emu的模式允许开发人员在编译板执行之前分析和评估设计的性能。
建议所有应用程序至少在sw_emu模式下执行，然后在FPGA板上编译和执行。
```
make all TARGET=<sw_emu|hw_emu> DEVICE=<FPGA Platform>
```
where
```
	sw_emu = software emulation
	hw_emu = hardware emulation
```

*注意：*软件仿真流程仅为功能正确性检查。它不会估计应用程序在硬件中的性能。
硬件仿真流程是为应用程序生成的硬件的周期精确模拟。因此，预计此模拟需要很长时间。
对于此示例，建议用户跳过运行硬件仿真或修改示例以处理简化数据集。
### Executing Emulated Application 
***Recommended Execution Flow for Example Applications in Emulation*** 

The makefile for the application can directly executed the application with the following command:
```
make check TARGET=<sw_emu|hw_emu> DEVICE=<FPGA Platform>

```
where
```
	sw_emu = software emulation
	hw_emu = hardware emulation
```
If the application has not been previously compiled, the check makefile rule will compile and execute the application in the emulation mode selected by the user.

***Alternative Execution Flow for Example Applications in Emulation*** 

An emulated application can also be executed directly from the command line without using the check makefile rule as long as the user environment has been properly configured.
To manually configure the environment to run the application, set the following
```
export LD_LIBRARY_PATH=$XILINX_SDX/runtime/lib/x86_64/:$LD_LIBRARY_PATH
export XCL_EMULATION_MODE=<sw_emu|hw_emu>
emconfigutil --platform 'xilinx_vcu1525_dynamic' --nd 1
```
Once the environment has been configured, the application can be executed by
```
./host ./xclbin/vadd.<emulation target>.<device name>.xclbin
```
This is the same command executed by the check makefile rule
### Compiling for Application Execution in the FPGA Accelerator Card
The command to compile the application for execution on the FPGA acceleration board is
```
make all DEVICE=<FPGA Platform>
```
The default target for the makefile is to compile for hardware. Therefore, setting the TARGETS option is not required.
*NOTE:* Compilation for application execution in hardware generates custom logic to implement the functionality of the kernels in an application.
It is typical for hardware compile times to range from 30 minutes to a couple of hours.

## 6. 在云环境中的执行
FPGA acceleration boards have been deployed to the cloud. For information on how to execute the example within a specific cloud, take a look at the following guides.
* [AWS F1 Application Execution on Xilinx Virtex UltraScale Devices]
* [Nimbix Application Execution on Xilinx Kintex UltraScale Devices]


## 7. 支持
For more information about SDAccel check the [SDAccel User Guides][]

For questions and to get help on this project or your own projects, visit the [SDAccel Forums][].

To execute this example using the SDAccel GUI, follow the setup instructions in [SDAccel GUI README][]


## 8. 许可和对存储的贡献
The source for this project is licensed under the [3-Clause BSD License][]

To contribute to this project, follow the guidelines in the [Repository Contribution README][]

## 9. 致谢
This example is written by developers at
- [Xilinx](http://www.xilinx.com)

[3-Clause BSD License]: ../../../LICENSE.txt
[SDAccel Forums]: https://forums.xilinx.com/t5/SDAccel/bd-p/SDx
[SDAccel User Guides]: http://www.xilinx.com/support/documentation-navigation/development-tools/software-development/sdaccel.html?resultsTablePreSelect=documenttype:SeeAll#documentation
[Nimbix Getting Started Guide]: http://www.xilinx.com/support/documentation/sw_manuals/xilinx2016_2/ug1240-sdaccel-nimbix-getting-started.pdf
[Walkthrough Video]: http://bcove.me/6pp0o482
[Nimbix Application Submission README]: ../../../utility/nimbix/README.md
[Repository Contribution README]: ../../../CONTRIBUTING.md
[SDaccel GUI README]: ../../../GUIREADME.md
[AWS F1 Application Execution on Xilinx Virtex UltraScale Devices]: https://github.com/aws/aws-fpga/blob/master/SDAccel/README.md
[Nimbix Application Execution on Xilinx Kintex UltraScale Devices]: ../../../utility/nimbix/README.md
