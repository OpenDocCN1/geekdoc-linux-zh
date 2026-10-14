

![](img/39e65eeb4f54001ede08c6114ae3cc6c_64_0.png)

图 2-6：K3b CD 刻录主窗口。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_64_1.png)

图 2-7：使用 Brasero 工具刻录 ISO 镜像文件。

## 在 Windows 中刻录 CD

Windows 环境默认不包含 CD 刻录软件。市面上有许多免费和商业软件包，但并非所有软件都提供刻录 ISO 镜像文件的选项。

如果你的特定 CD 刻录软件包无法刻录 CD 镜像，Ubuntu 推荐一款名为 InfraRecorder 的免费 CD 镜像刻录软件。InfraRecorder 软件包可以在流行的 SourceForge 网站上找到（infrarecorder.sourceforge.net）。

只需下载 InfraRecorder 软件包并安装到你的 PC 上。启动 InfraRecorder 后，点击 Actions 菜单栏项目，然后选择 Burn Image。你会看到一个选择要刻录镜像的对话框，然后会出现另一个对话框（如图 2-8 所示），等待你插入空白 CD 开始刻录。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_65_0.png)

**图 2-8：** 用于 Microsoft Windows 的 InfraRecorder CD 刻录工具。

一旦插入空白 CD，InfraRecorder 就会将 ISO 镜像文件刻录到 CD 上。获得 LiveCD ISO 镜像的 CD 后，就该开始尝试使用 Ubuntu 了！

## 启动 LiveCD

Ubuntu LiveCD 的美妙之处在于，它让你在无需经历安装过程的情况下，真正体验在 PC 上运行 Ubuntu 的感觉。当你从 PC 启动 LiveCD 时，Ubuntu 会像实际安装在 PC 硬盘上一样经历所有正常的启动过程。这包括检测 PC 硬件并尝试加载适当的驱动程序（在 Linux 中称为模块）以与检测到的硬件交互。

以下各节将介绍 Ubuntu LiveCD 启动过程以及从 LiveCD 启动 Ubuntu 后如何使用 Ubuntu。

## 启动过程

启动 LiveCD 的第一步是确定你的 PC 是否能够从其 CD 驱动器启动以及如何启动。许多 PC 默认即可实现。只需将 Ubuntu LiveCD 放入 CD 托盘并重新启动 PC 即可。如果你的特定 PC 无法从 CD 启动，在放弃之前可以尝试以下几种方法。

首先，进入 PC BIOS，查看是否已设置为允许从 CD 驱动器启动。不同的 PC 主板制造商使用不同的 BIOS 软件，配置此设置的方式多种多样。图 2-9 显示了示例 BIOS 设置中的启动顺序部分。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_66_0.png)

图 2-9：启动顺序 BIOS 设置。

找到启动顺序部分后，确保 CD 在列表中位于硬盘之上。这会强制 PC 在尝试从硬盘启动之前先检查是否有可启动的 CD。

许多 PC 制造商在启动过程中使用热键来选择启动设备。在某些 PC 上，在启动画面期间按下 F12 键会弹出启动菜单，允许用户选择要从哪个设备启动。用户选择 CD/DVD 设备，系统就会从 CD 启动。

## 使用 Ubuntu

启动 Ubuntu 启动过程后，你应该会看到如图 2-10 所示的主 Ubuntu 启动屏幕。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_67_0.png)

图 2-10：Ubuntu 启动菜单。

除了启动 Ubuntu 外，LiveCD 还允许你执行以下四项功能：

- 将 Ubuntu 安装到硬盘。
- 检查 LiveCD 的有效性。
- 测试 PC 的内存。
- 从 PC 的硬盘启动。

最后这个选项在紧急情况下可能成为救命稻草。硬盘上的引导扇区可能会损坏，导致 Linux 操作系统无法启动。只需插入可靠的 Ubuntu LiveCD，选择从硬盘启动选项，你可能就能拯救你的数据！

如果你选择从 CD 镜像启动，Ubuntu 会像从已安装的镜像启动一样进行所有硬件检测过程。

你会注意到，可以使用键盘上的 F 键从启动菜单访问多个选项。表 2-1 显示了这些键各自的功能。

## 表 2-1：Ubuntu LiveCD 启动菜单键

| Key | Description |
|-----|-------------|
| F1 | 显示一个帮助屏幕，列出 F 键选项。 |
| F2 | 选择 Ubuntu 菜单使用的默认语言。 |
| F3 | 选择 Ubuntu 使用的键盘映射。 |
| F4 | 选择视频设备的启动模式。 |
| F5 | 启用特殊辅助功能，例如屏幕放大镜或屏幕键盘。 |
| F6 | 向 GRUB（引导加载程序）提供额外的启动参数 |

