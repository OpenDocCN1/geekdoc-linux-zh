
![](img/af53325d7f38f1cdafca9f44568e4ab8_149_0.png)

让我们回顾一下打开对话框。

- 1. 你的U盘必须至少为 64MB。
- 这是最低要求；当然，今天制造商甚至不再生产这么小的U盘。似乎U盘和所有闪存设备的价格正在迅速下降，而容量却不断扩大。在撰写本文时，1GB 的U盘售价为 20 美元。但不用担心多余的空间——你可以在第二个分区中使用所有这些空间来存放扩展或其他媒体。
- 2. 你的U盘将被格式化为两个分区。
- 3. 一个小的用于 USB_ZIP 启动兼容性，并用于存放 DSL。
- 编号 2 和 3 指的是为计算机 BIOS 设置几何结构，以便将笔式设备识别为可 USB-ZIP 启动的驱动器，其中分区需要有 64 个磁头和 32 个扇区作为第一个分区的操作空间。
- 4. 剩余的分区将用于备份和扩展。
- 第二个分区会自动用于备份你的主目录以及你认为必要并添加到 `filetool.lst` 中的任何其他文件或目录。此外，它还是你在U盘启动时 MyDSL 扩展的默认位置。

请注意警告并确保你的U盘未挂载。如果已挂载，请退出安装脚本，卸载你的U盘，然后重新启动安装脚本。

如果一切看起来都正常，你就可以开始安装过程了。输入 `y` 开始。

在 USB-ZIP 安装脚本的下一个对话框中，会询问你是否想查看 USB 存储设备信息。除非你完全确定设备位置，否则应输入 `y` 并验证位置。脚本会从 `dmesg` 中 `grep` 信息，探测 SCSI 仿真，并以易于阅读的方式显示信息。如果一切正常，设备将被高亮显示为绿色。

在确认了你的笔式驱动器的物理位置后，脚本现在会询问这是全新安装还是升级。如果是新的笔式驱动器安装，输入 `1`；如果是升级（意味着你已在此笔式驱动器上运行 Damn Small Linux，并且想要重新安装或升级你正在使用的 Damn Small Linux 版本），输入 `u`。

在脚本继续之前，它需要知道你是在首次安装 DSL 还是在升级。对话框显示在图 6-8 中。

### FIGURE 6-8 After the pen drive location is displayed, you are asked if you want to upgrade or install.

![](img/af53325d7f38f1cdafca9f44568e4ab8_150_0.png)

在接下来的步骤中，会询问目标设备是什么。查看脚本两步前完成的 `dmesg` 探测数据，并输入设备位置。务必输入正确的设备名称而不是完整路径——例如，对于 `/dev/sda`，只需输入 `sda`。

接下来会询问：Use DSL iso from [L]iveCD, from [F]ile, from [W]eb。最直接且最快的安装方式是选择 LiveCD。由于本教程中你是从 CD 运行，因此无需下载任何额外文件。如果想下载最新版本的 Damn Small Linux 并将其安装到 USB 驱动器，而无需额外刻录光盘的步骤，则可以调用 File 或 Web 选项。如果你想在从旧版 DSL 安装时使用最新的 ISO，可以提前下载并使用 File 选项，或选择 Web 选项让脚本为你下载。

接下来会询问你是否需要任何特殊启动选项，例如 `toram`、`ftp` 或 `vga=normal`。DSL 有很多可能有用或有助于在特定硬件上启动的启动选项；然而，开发者已选择合理的默认值，因此我们的标准启动配置适用于大多数用户。（请参阅第 2 章，Robert 在其中详细概述了可用的启动选项。）

通过在提示时添加变量，可以对启动过程进行自定义，如图 6-9 所示。

![](img/af53325d7f38f1cdafca9f44568e4ab8_151_0.png)

### FIGURE 6-9 Special boot options may be entered at this point.

在下一个问题中，你可以选择除英语之外的其他语言支持。英语是 Damn Small Linux 的默认语言，但也对其他语言提供一定支持。在 USB 启动安装中选择选项之前，先使用你选择的语言选项从 live CD 启动是个好主意。这样，你可以确认所选语言下的一切都符合你的预期。在提示时输入你的语言选择，如图 6-10 所示，如果选择的是“English”，则留空。

![](img/af53325d7f38f1cdafca9f44568e4ab8_151_1.png)

### FIGURE 6-10 Enter your choice of language.

下一个提示，如图 6-11 所示（红色部分），显示即将被格式化并写入的设备——这是不可回头的点。如果你输入 `y`，脚本将继续安装过程；如果你输入除 `y` 之外的任何内容并按 Enter，脚本将直接退出。仔细检查物理设备是否显示正确，如果你确信显示无误，请输入 `y` 并按 Enter 继续。

### FIGURE 6-11 Your last chance to exit the script before it begins the installation process.

![](img/af53325d7f38f1cdafca9f44568e4ab8_152_0.png)

从此时起，脚本开始执行其操作。首先，它设置分区几何结构，然后格式化启动分区和存储分区。接下来，脚本设置引导加载程序、启动映像和系统映像到第一个分区。最后，脚本完成，应该没有其他事情可做，只需按一个键退出程序即可。你的 USB 笔式驱动器应该可以启动了。在脚本结束时，对话框将如下图 6-12 所示。

### FIGURE 6-12 If all goes well, your USB pen drive script should conclude with a similar dialog.

![](img/af53325d7f38f1cdafca9f44568e4ab8_152_1.png)

## 当你的电脑 BIOS 不支持 USB 启动时该怎么办

如果你的笔式驱动器要在不支持 USB 启动的电脑上使用，你有两个选择：

- 使用我们特别创建的启动软盘 `bootfloppy-usb.img` 从软盘启动。
- 使用带有特殊启动参数的 CD 启动，该参数告诉 Syslinux 访问笔式驱动器所在设备位置的系统映像。

## 为 USB 笔式驱动器创建启动软盘

第一步是下载 USB 启动软盘映像。你可以在任何下载站点找到该映像。其中一个位置是：

```
ftp://ibiblio.org/pub/Linux/distributions/damnsmall/current/bootfloppy-usb.img
```

如果你正在运行 Damn Small Linux（或几乎任何其他 Linux 发行版），你可以通过打开一个终端窗口并输入以下内容来下载最新的 USB 启动软盘映像：

```
wget ftp://ibiblio.org/pub/Linux/distributions/damnsmall/current/bootfloppy-usb.img
```

使用 `wget` 下载 USB 启动软盘映像后，你可以通过在终端窗口中发出以下命令来格式化软盘：

```
dd if=bootfloppy-usb.img of=/dev/fd0
```

有了你新可启动的软盘驱动器后，即使你使用的电脑 BIOS 不支持 USB 启动，你也可以启动你的 USB 笔式驱动器。

## 使用 LiveCD 启动笔式驱动器

50MB 的 hockey ring 光盘比软盘更小巧，便于携带。对于许多人来说，使用可启动的 USB 笔式驱动器，然后使用迷你 CD 作为软盘驱动器的替代启动介质可能更容易。

当你使用一台无法原生从 USB 设备启动的电脑时，你可以使用启动 CD 和笔式驱动器来模拟大部分 USB 启动行为。我们将回顾在启动提示符下可以使用的一些选项，以利用你的笔式驱动器。

要从你的笔式驱动器使用你的 MyDSL 扩展，输入以下内容：

```
dsl mydsl=sda1
```

要从你的笔式驱动器使用你的备份/恢复文件，输入以下内容：

```
dsl restore=sda1
```

要访问你笔式驱动器上的映像，输入以下内容：

```
dsl fromhd=/dev/sda1
```

如果你的 CD 和笔式驱动器上都有相同版本的 DSL，那么实际上没有必要发出命令 `fromhd=/dev/sda1`；然而，如果你的 CD 上的 DSL 版本比你的笔式驱动器旧，你可能想要这样做。通过使用 `fromhd` 命令，每次 DSL 有新版本发布时，你就不必刻录新的 CD。

你也可以在启动提示符下使用全部三个命令，以几乎与从笔式驱动器原生启动相同的方式访问笔式驱动器：

```
dsl fromhd=sda1 mydsl=sda1 restore=sda1
```
