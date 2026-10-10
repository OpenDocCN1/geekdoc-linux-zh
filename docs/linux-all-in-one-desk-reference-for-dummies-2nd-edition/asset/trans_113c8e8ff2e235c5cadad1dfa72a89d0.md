

## 检查您的 PC 硬件

-   **显示器：** 显示器的类型并不特别关键，但它必须能够显示显卡所使用的屏幕分辨率。屏幕分辨率以水平方向和垂直方向的像素（*pixels*）数量来表示（例如，1024 x 768）。安装程序可以检测大多数现代显示器。如果它无法检测您的显示器，您可以选择具有特定分辨率的通用显示器类型（如 1024 x 768）。您也可以根据显示器的品牌和型号（这可以在显示器的背面找到）来指定显示器。

-   **鼠标：** 安装程序可以检测鼠标。所有类型的鼠标（如 *PS/2* 或 *USB*）都可以与 Linux 和 X 窗口系统配合使用。

-   **网卡：** 并非所有 PC 都有网卡，但如果您的 PC 有，安装程序通常可以检测并使用它。如果遇到问题，请尝试查找网卡的品牌和型号（例如 *Linksys LNE100TX 快速以太网适配器*），以便您可以搜索 Linux 是否支持该网卡的信息。

-   **处理器：** 最好是 400 MHz Pentium II 或更高级别的处理器。只要速度超过 400 MHz，处理器速度（以 *MHz*（兆赫兹）或 *GHz*（吉赫兹）表示）并不是很重要。但越快越好。Linux 也可以在其他 Intel 兼容处理器上运行，例如 AMD、Cyrix 和 VIA 处理器。

-   **内存：** *RAM* 是您系统的内存量。与处理速度一样，内存越多越好。您需要 256MB 内存来安装 Linux 和 X 窗口系统，并舒适地运行图形用户界面桌面。

-   **SCSI 控制器：** 一些高性能 PC 配有 SCSI 控制器，用于将磁盘驱动器和其他外设连接到 PC。如果您的 PC 恰好拥有 SCSI 控制器，您可能想要查找该控制器的品牌和型号。

-   **声卡：** 如果您的 PC 有声卡并且您希望在 Linux 中有声音，您需要确保其兼容性。您可以在成功安装 Linux 后配置声卡。

-   **显卡：** Linux 在文本模式下与所有显卡（也称为 *显示适配器*）配合良好，但如果您想要图形用户界面，您需要一张支持 X 窗口系统的显卡。安装程序可以检测支持的显卡并正确配置 X 窗口系统。然而，如果安装程序无法检测显卡，了解显卡的品牌和型号会有所帮助。

-   **打印机：** 除了这些硬件之外，您还需要查找您计划在 Linux 中使用的任何打印机的品牌和型号。

![](img/792720823146d68f19fd50c99ebfce4b_60_0.png)

许多发行版，如 Debian GNU/Linux，可以在任何与 Linux 内核兼容的硬件上运行。有关 Linux 兼容硬件的信息，请访问 www.tldp.org/HOWTO/Hardware-HOWTO。

![](img/792720823146d68f19fd50c99ebfce4b_61_0.png)

要检查您的 PC 硬件是否与 SUSE Linux 兼容，请访问位于 http://hardwaredb.suse.de 的 SUSE Linux 硬件兼容性列表。对于 MEPIS，请查阅位于 www.mepisusers.org/hwdatabase 的 MEPIS 硬件数据库。Ubuntu 的硬件兼容性列表位于 https://wiki.ubuntu.com/HardwareSupport/。对于 Xandros Desktop，您可以在 www.xandros.com/support/hcl.html 找到硬件兼容性列表。

## 试用 Knoppix Live CD

在安装任何内容之前，值得一试的是从随附 DVD 中试用 Knoppix（K 不发音）。除了熟悉 Linux 桌面的感觉外，您还可以从 Knoppix 中执行一些额外的安装前任务。如果您决定安装 Fedora 以外的发行版——Debian、MEPIS、SUSE、Ubuntu 或 Xandros——您可以将本书随附 DVD 上提供的 ISO 镜像文件中的 CD 或 DVD 刻录出来。您也可以使用 Knoppix 下的 QTParted 工具在硬盘上为 Linux 腾出空间。

要启动 Knoppix，请遵循以下步骤：

1.  **从本书的随附 DVD 启动您的 PC。**
    会出现 `boot:` 提示符。在此提示符下，您可以输入各种命令来控制启动过程。特别是，您可以输入命令来禁用某些可能正在导致安装失败的硬件检测类型。
2.  **几分钟后，您将看到 Knoppix 使用的 KDE 图形用户界面桌面。**
    您现在可以开始使用 Knoppix。

![](img/792720823146d68f19fd50c99ebfce4b_61_1.png)

如果您在笔记本电脑上尝试 Knoppix 并且在显示关于探测 SCSI（这是一种接口类型的名称）的消息后挂起，请重新启动。当出现 `boot:` 提示符时，输入 `knoppix noisci`。通过告诉 Knoppix 不要检查 SCSI，这应该能让您通过该问题。对于遇到 ACPI（高级配置和电源接口）问题的 PC，请在启动提示符处输入 `knoppix acpi=off`。在启动提示符处按 F3 可获取 Knoppix 启动选项列表。

获得 Knoppix 桌面后，您可以开始探索 Knoppix。有关试用 Linux 的更多信息，请参阅本小册子的第 4 章。如果您想使用 Knoppix 刻录 CD 或调整硬盘分区大小，请参阅本章中的“使用 Knoppix 刻录 CD 或 DVD”部分和“使用 Knoppix 中的 QTParted 调整分区大小”部分。

当您结束使用 Knoppix 时，选择主菜单:注销，并在出现的 KDE 结束会话对话框中选择重新启动计算机。Knoppix 关闭后，取出 DVD 并按 Enter 键。

## 从 ISO 镜像刻录 CD 或 DVD

本书的随附 DVD 包含以 ISO 镜像形式存在的 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 发行版，它们被组织在 DVD 的 **distros** 文件夹中的不同文件夹里。要安装这些发行版中的任何一个，您首先必须根据情况将所选发行版的 ISO 镜像刻录到 CD 或 DVD 上。通常，您可以在拥有 CD/DVD 刻录机的 PC 上执行此步骤，最可能是在使用 Microsoft Windows 的情况下，因为大多数新 PC 都预装了 Windows。另一种选择是从随附 DVD 启动 Knoppix，然后使用 Knoppix 刻录 CD 或 DVD。我在接下来的两个部分中描述了这些选项。

### 使用 CD 刻录应用程序

在 Microsoft Windows 中，您可以使用 CD 刻录应用程序（如 Nero）将 ISO 镜像刻录到可录制 CD 上。如果您没有用于 Microsoft Windows 的 CD 刻录应用程序，请从 DVD 启动 Knoppix，并从图形用户界面桌面选择主菜单→多媒体→K3b 以启动 CD/DVD 刻录应用程序。从 ISO 镜像刻录 CD 的具体步骤取决于您使用的 CD 刻录应用程序。一般步骤如下。（如果您拥有 DVD 刻录机，请使用相同的说明来刻录 DVD。）

1.  **将随附 DVD-ROM 放入 PC 的 DVD 驱动器中。**
    如果您的 DVD 驱动器是组合 DVD/CD 刻录机，您必须首先将 Linux 发行版的 ISO 镜像文件从 DVD 复制到 PC 硬盘，以便您可以使用同一驱动器来刻录 CD。
2.  **启动 CD 刻录应用程序。**
3.  **从 CD 刻录应用程序打开镜像文件。**
    具体步骤取决于 CD 刻录应用程序。在 Knoppix 下的 K3b 中，从菜单中选择 工具→CD→刻录 CD 镜像。在其他 CD 刻录应用程序中，通常通过选择 文件→打开 来执行此操作。在 打开 对话框中，选择该发行版的 ISO 镜像文件。如果您不确定，请搜索该应用程序的在线帮助以获取有关从 ISO 镜像刻录 CD 的信息。
4.  **将一张空白可录制 CD 放入 CD 刻录机中。**
5.  **将 ISO 镜像刻录到可录制 CD 上。**
    通常，CD 刻录应用程序有一个工具栏按钮，您可以点击它以开始将 ISO 镜像刻录到空白 CD 上。
6.  **如果发行版有多个 ISO 镜像，请对剩余的 ISO 镜像重复步骤 2 至 4。**
    Live CD 发行版以单个 ISO 镜像形式提供，您可以将其刻录在单个 CD 上。其他发行版通常以多个 ISO 镜像形式提供，您必须将每个镜像文件刻录到单独的 CD 上。

![](img/792720823146d68f19fd50c99ebfce4b_62_0.png)

