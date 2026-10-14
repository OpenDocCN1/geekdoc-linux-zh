

在 USB-ZIP 安装脚本的下一个对话框中，会询问你是否想查看 USB 存储设备信息。除非你完全确定设备位置，否则应输入 y 并验证位置。脚本会从 dmesg 中 grep 信息，探测 SCSI 仿真，并以易于阅读的方式显示信息。如果一切正常，设备将被高亮显示为绿色。

在确认了你的笔式驱动器的物理位置后，脚本现在会询问这是全新安装还是升级。如果是新的笔式驱动器安装，输入 1；如果是升级（意味着你已在此笔式驱动器上运行 Damn Small Linux，并且想要重新安装或升级你正在使用的 Damn Small Linux 版本），输入 u。

在脚本继续之前，它需要知道你是在首次安装 DSL 还是在升级。对话框显示在图 6-8 中。

## FIGURE 6-8 After the pen drive location is displayed, you are asked if you want to upgrade or install.

![](img/af53325d7f38f1cdafca9f44568e4ab8_150_0.png)

在接下来的步骤中，会询问目标设备是什么。查看脚本两步前完成的 dmesg 探测数据，并输入设备位置。务必输入正确的设备名称而不是完整路径——例如，对于 /dev/sda，只需输入 sda。

接下来会询问：Use DSL iso from [L]iveCD, from [F]ile, from [W]eb。最直接且最快的安装方式是选择 LiveCD。由于本教程中你是从 CD 运行，因此无需下载任何额外文件。如果想下载最新版本的 Damn Small Linux 并将其安装到 USB 驱动器，而无需额外刻录光盘的步骤，则可以调用 File 或 Web 选项。如果你想在从旧版 DSL 安装时使用最新的 ISO，可以提前下载并使用 File 选项，或选择 Web 选项让脚本为你下载。

接下来会询问你是否需要任何特殊启动选项，例如 toram、ftp 或 vga=normal。DSL 有很多可能有用或有助于在特定硬件上启动的启动选项；然而，开发者已选择合理的默认值，因此我们的标准启动配置适用于大多数用户。（请参阅第 2 章，Robert 在其中详细概述了可用的启动选项。）

通过在提示时添加变量，可以对启动过程进行自定义，如图 6-9 所示。

![](img/af53325d7f38f1cdafca9f44568e4ab8_151_0.png)

## FIGURE 6-9 Special boot options may be entered at this point.

在下一个问题中，你可以选择除英语之外的其他语言支持。英语是 Damn Small Linux 的默认语言，但也对其他语言提供一定支持。在 USB 启动安装中选择选项之前，先使用你选择的语言选项从 live CD 启动是个好主意。这样，你可以确认所选语言下的一切都符合你的预期。在提示时输入你的语言选择，如图 6-10 所示，如果选择的是“English”，则留空。

![](img/af53325d7f38f1cdafca9f44568e4ab8_151_1.png)

## FIGURE 6-10 Enter your choice of language.

下一个提示，如图 6-11 所示（红色部分），显示即将被格式化并写入的设备——这是不可回头的点。如果你输入 **y**，脚本将继续安装过程；如果你输入除 **y** 之外的任何内容并按 Enter，脚本将直接退出。仔细检查物理设备是否显示正确，如果你确信显示无误，请输入 **y** 并按 Enter 继续。

## FIGURE 6-11

Your last chance to exit the script before it begins the installation process.

![](img/af53325d7f38f1cdafca9f44568e4ab8_152_0.png)

从此时起，脚本开始执行其操作。首先，它设置分区几何结构，然后格式化启动分区和存储分区。接下来，脚本设置引导加载程序、启动映像和系统映像到第一个分区。最后，脚本完成，应该没有其他事情可做，只需按一个键退出程序即可。你的 USB 笔式驱动器应该可以启动了。在脚本结束时，对话框将如下图 6-12 所示。

## FIGURE 6-12

If all goes well, your USB pen drive script should conclude with a similar dialog.

![](img/af53325d7f38f1cdafca9f44568e4ab8_152_1.png)

