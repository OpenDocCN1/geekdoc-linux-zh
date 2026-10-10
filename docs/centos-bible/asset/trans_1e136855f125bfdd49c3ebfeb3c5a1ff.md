
## 启动应用程序

根据应用程序安装程序的应用方式，您可能可以通过以下几种方式在 WINE 中启动 Windows 应用程序：

- **控制面板** — 如果应用程序为 Windows 控制面板设置了小工具，您可以打开 Windows 控制面板，然后选择该小工具以从那里启动应用程序。要启动 Windows 控制面板，请输入以下命令：
  ```
  $ wine control
  ```
- **WINE 文件系统浏览器** — 如果您安装了 `wine-tools` 包，可以启动 `winefile` 命令以查看 Wine 文件窗口。此窗口显示与您在 WINE 中配置驱动器相关的文件系统树状结构。选择包含您想要启动的应用程序的盘符，浏览到该应用程序，然后双击它以启动。

正如前文所述启动应用程序安装程序的方式，您也可以从命令行启动已安装在文件系统中的 Windows 应用程序。同样，您可以使用盘符来指示您想要启动的应用程序的位置。但是，为了使应用程序路径被正确解析，通常应该用引号将其包围：

```
$ wine "C:\program files\appid\app.exe"
```

作为 Windows 文件路径，您使用反斜杠 (\) 而不是斜杠 (/) 来分隔子目录。除了使用双引号外，您还可以在每个空格或反斜杠前添加一个额外的反斜杠。

一旦您拥有了运行 Windows 应用程序的可用 wine 命令行，您可以将该命令添加到 CentOS 桌面上的启动器中。有关将应用程序启动器添加到面板、菜单或桌面区域的信息，请参见第 3 章。

## 调整和配置 WINE

由于您通过 WINE 运行的 Windows 应用程序期望在 Linux 系统上找到 Windows 资源，这些资源要么必须由 WINE 提供，要么需要映射到现有的 Linux 系统中。例如，应用程序可能需要一个 WINE 未包含的特定 DLL 文件。或者，您可能需要将 COM 或 LPT 端口映射到 WINE 期望找到它们的位置。

以下是一些帮助您调整 WINE 配置的技巧：

- **Windows 版本** — 不同版本的 Windows 为应用程序提供不同的运行环境。WINE 默认模拟 Windows XP，但允许您让 WINE 针对每个应用程序运行近十种不同的 Windows 版本。从 Wine 配置窗口中，选择“应用程序”选项卡，然后点击“添加应用程序”按钮。从文件系统中选择您想要的 Windows 应用程序，然后选择希望其运行的 Windows 版本。
- **修改注册表项** — 当您需要修改 Windows 注册表项时，WINE 提供了三个可供操作的文件：system.reg、user.reg 和 userdef.reg。所有这些文件都位于用户的 $HOME/.wine 目录中。您可以使用 wineprefixcreate 实用程序来更新注册表，但通常您不再需要这样做，因为这应该会自动化完成。
- **配置端口** — 与 Windows 盘符类似，您可以将串行端口和并行端口的链接添加到您的 $HOME/.wine/dosdevices 目录中。例如，要为第一个并行端口 (LPT1) 和串行端口 (COM1) 添加条目，您可以从 $HOME/.wine/dosdevices 目录运行以下命令：
  ```
  $ ln -s /dev/lp0 lpt1
  $ ln -s /dev/ttyS0 com1
  ```
- **添加 DLL** — WINE 提供了运行 Windows 系统所需的许多基础库（DLL 文件）。然而，应用程序可能需要的一些 DLL 可能未包含在内，或者包含的某些 DLL 可能无法适用于您的应用程序。使用 Windows 配置窗口（“库”选项卡），您可以替换 WINE 提供的 DLL，或添加您从已安装应用程序中获取的其他 DLL。
- **图形设置** — 您可以通过 Windows 配置窗口上的“图形”选项卡更改与图形显示相关的设置。特别是，您可以更改 Windows 应用程序在 Linux 桌面上被管理的程度。
- **添加字体** — 要向您的 WINE 安装添加字体，请将 TrueType 字体（ttf 文件）复制到 WINE 虚拟驱动器上的 C:\windows\fonts 目录中。

有关配置 WINE 以在 Linux 中运行 Windows 应用程序的更多信息，请参阅 WINE 用户指南 (www.winehq.org/docs/en/wineusr-guide.html)。

### 寻找更多适用于 WINE 的 Windows 应用程序

关于已在 WINE 中测试运行的 Windows 应用程序的信息，请参阅 WINE 应用程序数据库 (http://appdb.winehq.org)。CodeWeavers 也维护了自己经过测试可在 WINE 下运行的应用程序数据库。有关运行 Windows 应用程序的信息，请参阅 CodeWeavers 兼容性中心 (www.codeweavers.com/compatibility)。在那里，您可以查看 CodeWeavers 自己的包含 3300 多个 Windows 应用程序的数据库。

另一个提供 WINE 应用程序信息的网站是 Frank's Corner (www.frankscorner.org)。该网站充斥着让图形、互联网、多媒体、办公、游戏及其他应用程序在 WINE 中运行的良好提示。

## 在虚拟环境中运行应用程序

近年来，虚拟化已成为 Linux 领域的一个热门话题。虚拟化不再允许计算机一次只运行一个操作系统，而是允许多个来宾操作系统在宿主系统上运行。当作为宿主操作系统时，CentOS 提供了两种主要的虚拟化方法：Xen 和 KVM。

在一台计算机上运行多个虚拟化操作系统有许多优点。例如，您可以配置一个仅包含 Web 服务器的虚拟机。通过这种方式将 Web 服务器进行隔间化，您可以将其调整为高效运行，并保护在同一计算机上运行的软件免受外部入侵者攻击。通过分别运行不同的操作系统，您可以使用相同的硬件来运行未针对同一操作系统制作的应用程序。

接下来的部分将为您介绍 CentOS 中的 Xen 和 KVM 虚拟化软件。

### 使用 Xen 虚拟运行应用程序

Xen (www.xensource.com) 是包含在 CentOS 中的虚拟化软件。Xen 由 Citrix 拥有。使用 Xen，您可以在正在运行的 CentOS 系统中运行多个操作系统实例。这些操作系统称为虚拟机，不仅可以运行专门为这些操作系统构建的应用程序，还可以出现在网络中，就好像它们运行在完全不同的机器上一样。

为了演示 Xen 的功能，本节中的过程描述了如何设置一个将在已安装宿主 CentOS 系统上运行的 CentOS 虚拟机。目前，要在 CentOS 的 Xen 上运行其他操作系统，您需要提供操作系统映像，而不是如以下过程所示从零开始构建。

您可以从 Xen Source 维基 (http://wiki.xensource.com/xenwiki) 上找到有关 Xen 的工作原理及其性质的更多信息。特别是，选择 Xen FAQ 链接以了解 Xen 是什么，或选择 HowTos 链接以获取用户手册和特别 HowTos 的链接。

### 安装 Xen 之前

Xen 运行需要大量资源。每个操作系统实例（称为*来宾操作系统*）几乎需要独立运行所需的完整资源量。因此，在开始之前，请确保您的系统至少具备以下条件：

- **RAM** — 通常，您的计算机应为每个您想要拥有的来宾提供至少 256 MB 的可用 RAM，加上您所选 CentOS 安装类型所需的 RAM 量。
- **硬盘** — 除了安装 CentOS 所需的资源外，您还需要每个已安装操作系统来宾所需的全部磁盘空间。当然，这些数量可能差异很大，最小服务器安装从约 600 MB 开始，而平均桌面安装通常从 2 GB 或 3 GB 开始。
- **半虚拟化 (PAE) 支持** — 您的计算机 CPU 必须支持 PAE 扩展。许多笔记本电脑不具有 PAE 支持。要查看您的计算机是否支持 PAE，请输入以下命令：
  ```
  # cat /proc/cpuinfo | grep pae
  flags : fpu vme de pse tsc msr pae mce cx8 apic
  mtrr pge mca cmov pat pse36 mmm fxs sycall
  mmxext 3dnowext 3dnow up
  ```
  在此示例中，支持 PAE。如果不受支持，则不会返回任何内容。
- **完全虚拟化来宾支持** — 为了运行完全虚拟化的来宾，您需要根据处理器支持 Intel VT 或 AMD-V。再次检查您的 cpuinfo（如上所示），但这次查找 vmx 或 svm（分别在 Intel 或 AMD 处理器上）。同样，如果您看到输出，则表示支持该程序。
- **GRUB 引导加载器** — 您使用的计算机的最后要求是 GRUB 必须作为您的引导加载器。当您安装 Xen 时，它会自动将自己添加到您的 GRUB 引导加载器中，作为您可以选择以启动的操作系统内核的次要选择。

### 安装 Xen

要在 CentOS 中运行 Xen，您需要安装并从一个特别配置的 Xen 内核启动。Xen 内核包默认不包含在 CentOS 中，因此您必须在安装时选择它们或稍后添加。以下是安装您需要的 Xen 包的方法：

