
## 检查您的 PC 硬件

- **显示器**：显示器的类型并不是特别关键，除非它必须能够显示视频卡所使用的屏幕分辨率。屏幕分辨率以水平和垂直方向上的图像元素（*像素*）数量来表示（例如，1024 × 768）。安装程序可以检测大多数现代显示器。如果它未能检测您的显示器，您可以选择具有特定分辨率（如 1024 × 768）的通用显示器类型。您还可以通过其制造商和型号（可在显示器背面找到）来指定显示器。

- **鼠标**：安装程序可以检测鼠标。所有类型的鼠标（如 PS/2 或 USB）都适用于 Linux 和 X 窗口系统。

- **网卡**：并非所有 PC 都有网卡，但如果您有，安装程序通常可以检测并使用它。如果您遇到问题，请尝试查找其制造商和型号（如 Linksys LNE100TX 快速以太网适配器），以便您可以搜索 Linux 是否支持该网卡的信息。

- **处理器**：400 MHz Pentium II 或更高配置最佳。只要速度超过 400 MHz，以 *MHz*（兆赫兹）或 *GHz*（吉赫兹）表示的处理器速度就不那么重要。但越快越好。Linux 可以运行在其他 Intel 兼容处理器上，如 AMD、Cyrix 和 VIA 处理器。

- **内存（RAM）**：*RAM* 是您系统拥有的内存量。与处理速度一样，内存越多越好。您需要 256MB 内存来安装 Linux 和 X 窗口系统，并舒适地运行图形用户界面（GUI）桌面。

- **SCSI 控制器**：一些高性能 PC 拥有 SCSI 控制器，用于将磁盘驱动器和其他外设连接到 PC。如果您的 PC 恰好有 SCSI 控制器，您可能需要查找该控制器的制造商和型号。

- **声卡**：如果您的 PC 有声卡并且您希望在 Linux 中获得声音，必须确保其兼容性。您可以在成功安装 Linux 后配置声卡。

- **视频卡**：Linux 在文本模式下与所有视频卡（也称为 *显示适配器*）配合良好，但如果您想要图形界面，则需要一个能与 X 窗口系统配合工作的视频卡。安装程序可以检测受支持的视频卡并正确配置 X 窗口系统。但是，如果安装程序无法检测视频卡，知道您视频卡的制造商和型号会有所帮助。

- **打印机**：除了这些硬件之外，您还需要查找计划在 Linux 中使用的任何打印机的制造商和型号。

![](img/11709a8f88c8cd03868a929dc94c0e2b_60_0.png)

许多发行版，如 Debian GNU/Linux，运行在与 Linux 内核兼容的任何硬件上。有关 Linux 兼容硬件的信息，请参见 www.tldp.org/HOWTO/Hardware-HOWTO。

要检查您的 PC 硬件是否与 SUSE Linux 兼容，请访问 [SUSE Linux 硬件兼容性列表](http://hardwardedb.suse.de)。对于 MEPIS，请查阅 [MEPIS 硬件数据库](www.mepislovers.org/hwdatabase)。Ubuntu 的硬件兼容性列表位于 [https://wiki.ubuntu.com/HardwareSupport/](https://wiki.ubuntu.com/HardwareSupport/)。对于 Xandros Desktop，您可以在 [www.xandros.com/support/hcl.html](www.xandros.com/support/hcl.html) 找到硬件兼容性列表。

## 试用 Knoppix 启动光盘

在安装任何内容之前，试用随附光盘中的 Knoppix（K 不发音）是值得的。除了体验 Linux 桌面外，您还可以通过 Knoppix 执行一些额外的预安装工作。如果您决定安装除 Fedora 以外的发行版——Debian、MEPIS、SUSE、Ubuntu 或 Xandros——您可以将此书随附光盘上提供的 ISO 镜像文件刻录到 CD 或 DVD 上。您还可以使用 Knoppix 下的 QTParted 工具在硬盘上为 Linux 腾出空间。

要启动 Knoppix，请遵循以下步骤：

1. **从此书随附光盘启动您的 PC。**
   会出现一个 `boot:` 提示符。在此提示符下，您可以输入各种命令来控制启动过程。特别是，您可以输入命令来禁用某些可能导致安装失败的硬件检测类型。
2. **几分钟后，您会看到 Knoppix 使用的 KDE GUI 桌面。**
   现在您可以开始使用 Knoppix。

![](img/11709a8f88c8cd03868a929dc94c0e2b_61_0.png)

如果您在笔记本电脑上尝试 Knoppix 并在显示有关探测 SCSI（这是一种接口类型的名称）消息后挂起，请重新启动。当 `boot:` 提示符出现时，输入 **knoppix noscsi**。告诉 Knoppix 不检查 SCSI 应该能让您通过这个问题。对于在 ACPI（高级配置和电源接口）方面存在问题的 PC，请在启动提示符处输入 **knoppix acpi=off**。在启动提示符处按 F3 查看 Knoppix 启动选项列表。

在获得 Knoppix 桌面后，您可以开始探索 Knoppix。查阅本迷你书的第 4 章以获取更多关于试用 Linux 的信息。如果您想使用 Knoppix 刻录 CD 或调整硬盘分区大小，请参阅本章中“使用 Knoppix 刻录 CD 或 DVD”部分和“在 Knoppix 中使用 QTParted 调整分区大小”部分。

当您结束使用 Knoppix 时，选择 **主菜单::注销**，并从出现的 KDE 结束会话对话框中选择 **重新启动计算机**。在 Knoppix 关机后，移除 DVD 并按 **Enter**。

## 从 ISO 镜像刻录 CD 或 DVD

此书的随附光盘包含 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 发行版，形式为 ISO 镜像，组织在 DVD 的 distros 文件夹内的独立文件夹中。要安装其中任何一个发行版，您必须首先将所选发行版的 ISO 镜像刻录到 CD 或 DVD，视情况而定。通常，您可以使用带有 CD/DVD 刻录机的 PC 执行此步骤，很可能是在使用 Microsoft Windows 的情况下，因为大多数新 PC 都预装了 Windows。另一种选择是从随附光盘启动 Knoppix，然后使用 Knoppix 刻录 CD 或 DVD。我在接下来的两节中描述了这些选项。

### 使用 CD 刻录应用程序

在 Microsoft Windows 中，您可以使用 CD 刻录应用程序（如 Nero）将 ISO 镜像刻录到可记录 CD 上。如果您没有用于 Microsoft Windows 的 CD 刻录应用程序，请从 DVD 启动 Knoppix，并在图形桌面上选择 主菜单 > 多媒体 > K3b 以启动 CD/DVD 刻录应用程序。从 ISO 镜像刻录 CD 的具体步骤取决于您使用的 CD 刻录应用程序。一般步骤如下。（如果您有 DVD 刻录机，请使用相同的说明来刻录 DVD。）

1. **将随附 DVD-ROM 放入 PC 的 DVD 驱动器中。**
   如果您的 DVD 驱动器是 DVD/CD 组合刻录机，您必须首先将 Linux 发行版的 ISO 镜像文件从 DVD 复制到 PC 的硬盘上，以便您可以使用同一个驱动器刻录 CD。
2. **启动 CD 刻录应用程序。**
3. **从 CD 刻录应用程序打开镜像文件。**
   具体步骤取决于 CD 刻录应用程序。在 Knoppix 下的 K3b 中，从菜单中选择 工具 > CD > 刻录 CD 镜像。在其他 CD 刻录应用程序中，通常通过选择 文件 > 打开来完成此操作。从打开对话框中选择该发行版的 ISO 镜像文件。如果您不确定，请在应用程序的在线帮助中搜索有关从 ISO 镜像刻录 CD 的信息。
4. **将空白可记录 CD 放入 CD 刻录机中。**
5. **将 ISO 镜像刻录到可记录 CD 上。**
   通常，CD 刻录应用程序有一个工具栏按钮，您可以点击它将 ISO 镜像刻录到空白 CD 上。
6. **如果发行版有更多的 ISO 镜像，请对剩余的 ISO 镜像重复步骤 2 到 4。**

> 启动 CD 发行版以单个 ISO 镜像的形式提供，您可以将其刻录到单个 CD 上。其他发行版通常以多个 ISO 镜像的形式提供，您必须将每个镜像文件刻录到单独的 CD 上。

