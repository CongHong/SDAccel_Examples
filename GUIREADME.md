Executing SDx Examples in the SDx GUI
===============================================================================

可以使用提供的Makefile或SDx GUI编译SDx GitHub存储库中可用的示例。有关如何进行Makefile编译的文档包含在每个示例的README文件中。本文档概述了在SDx GUI中运行示例应用程序的步骤。

要在GUI中使用示例，必须将其作为示例模板下载，然后必须使用示例模板创建新项目。执行此操作的步骤如下所述。

### Download the example template in the GUI
- 通过在终端窗口中运行以下命令来打开SDx GUI：
```
    sdx
```

- 从*Xilinx* 菜单中选择*SDx Example Store...* 。这将打开一个对话框，您可以在其中下载示例模板。
- 第一次打开对话框时，将下载示例存储库。要下载示例的更新，请单击*Update*。

- 下载示例后，示例将显示为*Installed*。
*注意：*安装示例后，在创建新的SDx项目时，它们将作为项目模板提供。

- 关闭对话框。


### 在GUI中创建Hello Application示例项目
- 在SDx GUI中，为示例设计创建一个新项目。这将打开*New Project Wizard*。

- 在*Templates* 页面中，选择已下载的示例。


*注意：*某些示例需要特定的硬件或运行时支持，并且仅适用于*New Project Wizard*中的匹配平台和运行时。

- 完成向导。将使用构建和运行示例所需的源和项目设置创建项目。

- 构建并运行应用程序.

