
对于诸如网卡或声卡之类的设备，Linux 需要单独的驱动程序。因为 Linux 可免费获得（或相对便宜），并且世界各地的许多程序员共同合作开发 Linux，所以你不能要求对特定硬件提供支持。你最好的办法是希望能够编写 Linux 驱动程序的人拥有与你相同的硬件。很可能那个人会编写一个驱动程序，最终会进入 Linux 的某个版本；然后你就可以在 Linux 下使用该硬件。Linux 支持新接口可能需要一段时间。

即使某些外设没有可用的 Linux 驱动程序，你也可以安装并运行 Red Hat Linux。然而，至少你必须拥有 Linux 兼容的处理器、总线类型、硬盘、显卡、显示器、键盘、鼠标和 CD-ROM 驱动器，才能从随附的 CD-ROM 安装 Red Hat Linux。如果你想运行 X Window System 以及 GNOME 或 KDE 等图形桌面，还必须确保 XFree86（Linux 的 X Window System）支持鼠标、显卡和显示器。

## 检查 Red Hat Linux 是否支持你的 PC 硬件

要检查 Red Hat Linux 是否支持你的 PC 中的硬件，请执行以下步骤：

- 1. 收集安装在你的 PC 中的所有硬件的品牌、型号和其他技术细节。这就是你的硬件清单。你可以查阅 PC 的手册（如果有的话）。你也可以使用当前的操作系统来查找有关硬件的信息。例如，在 Windows 95/98 下，双击控制面板中的系统图标即可收集其中一些信息。（在系统属性窗口中单击设备管理器选项卡以查看系统中的特定设备信息。）
- 2. 携带你的硬件清单，访问 Red Hat 的网站 http://www.redhat.com/hardware。该网站包含最新版 Red Hat Linux 支持的硬件列表。将你的 PC 硬件与该列表进行核对，并确保 Red Hat Linux 支持关键硬件组件。

## 探索 PC 硬件

以下各节概述了 Red Hat Linux 支持的 PC 硬件。在你继续在 PC 上安装 Red Hat Linux 之前，应尽可能收集有关硬件的尽可能多的信息。

## 处理器

处理器是中央处理器（CPU）——执行 PC 中所有处理的集成电路芯片。至少，你需要 Intel 80386 处理器才能运行 Red Hat Linux。任何 Intel 80386、80486、Celeron 或 Pentium 兼容处理器都可以运行 Linux 操作系统。在兼容处理器中，Red Hat Linux 可以在 AMD K5、K6 和 Cyrix 处理器上运行。Red Hat Linux 还支持具有对称多处理（SMP）Linux 内核的多处理器主板。

## 总线

总线是处理器与其外设之间的标准电气连接。存在几种类型的 PC 总线。最流行的总线是工业标准架构（ISA）总线，以前称为 AT 总线，因为 IBM 于 1984 年在 IBM PC-AT 计算机中引入了它。其他总线包括扩展工业标准架构（EISA）；VESA 局部总线（VL-bus）；微通道架构（MCA）；以及最近的 Peripheral Component Interconnect（PCI）。目前，Red Hat Linux 支持所有常见的 PC 总线。

## 内存

通常称为随机存取存储器或 RAM，内存不是兼容性的因素。然而，你至少需要 32MB 的 RAM 才能获得良好的性能。虽然你可能能够在拥有 16MB RAM 的 PC 上安装并运行 Red Hat Linux，但你无法在该 PC 上运行 X Window System。X Window System 通过 X 服务器管理图形界面，X 服务器是一个大型程序，需要大量内存才能高效运行。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_30_0.png)

如果你正在购买新 PC，它很可能至少配备 32MB 的 RAM——如果不是 64MB 或更多的话。如果你有一台 RAM 少于 8MB 的旧 PC，你可能需要添加一些内存，使总量达到（至少）16MB。系统拥有的物理内存越多，运行多个程序的效率就越高，因为程序都可以装入内存。虽然 Red Hat Linux 可以使用硬盘的一部分作为虚拟内存，但这种基于磁盘的内存比物理内存慢得多。所需的物理内存量取决于 Linux 操作系统的大小以及你必须始终运行的其他软件，例如 X Window System。

## 显卡和显示器

Red Hat Linux 在文本模式下与所有显卡配合良好。但当涉及到 XFree86——X Window System 的 Linux 版本时，情况就大不相同了。如果 XFree86 没有明确支持你的显卡，你可能需要付出很大努力才能为你的显卡配置 XFree86。

你使用的显示器类型不是特别关键，但它必须能够显示显卡使用的屏幕分辨率。这些分辨率以水平和垂直方向上的像素数（例如 1024×768）表示。

通常，XFree86 对显卡的支持取决于视频芯片组——控制显示器并使显示器显示输出的集成电路。你可以从显卡的文档中查出显卡使用的视频芯片组名称。

如果你在 http://www.redhat.com/support/hardware/ 出现的列表中看不到你的显卡名称，请不要惊慌。大多数流行的显卡使用 Red Hat 网站上列出的视频芯片组之一。事实上，相同的芯片组可以在许多不同的显卡中发挥作用。例如，NVidia RIVA TNT 芯片组被用于许多显卡中，包括 Diamond Viper V550、Hercules TNT、STB Velocity 4400 和 ELSA ERAZOR II。在安装 Red Hat Linux 时，Red Hat Linux 安装程序在设置 X Window System 时会自动检测视频芯片组。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_31_0.png)

## 硬盘

Red Hat Linux 支持 PC 的基本输入/输出系统（BIOS）支持的任何硬盘。在许多较旧的 386 和 486 PC 中，你必须使用单独的驱动程序来访问大容量硬盘——系统 BIOS 无法处理这些驱动器。你无法在这样的系统上安装 Linux。简而言之，只有当系统 BIOS 在没有任何额外驱动程序的情况下支持硬盘时，Red Hat Linux 才会支持你的硬盘——有一个重要的限制。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_31_1.png)

要能够从大容量硬盘（任何具有超过 1,024 个磁柱的驱动器）启动 Red Hat Linux，Linux 加载器（LILO）、Linux 内核和 LILO 配置文件必须位于驱动器的前 1,024 个磁柱中。这是因为 Linux 加载器使用 BIOS 加载内核，而 BIOS 无法访问超出前 1,024 个磁柱的磁柱。

对于通过 SCSI（小型计算机系统接口）控制器卡连接到 PC 的硬盘，Red Hat Linux 必须具有使 SCSI 控制器能够访问和使用硬盘的驱动程序。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_32_0.png)

关于硬盘的唯一剩余决定是其容量。如果你有一台旧 PC，你可能有一块相对低容量的硬盘——可能低至 500MB。虽然你可以在 500MB 内安装 Red Hat Linux 和 X Window System，但这样做不会为 Windows 95/98/2000 留下太多空间。（你需要至少 2GB 的磁盘空间来同时运行 Linux 和 Windows 95/98/2000。）因此，如果你的旧 PC 具有 IDE 接口并且只有一个小型硬盘（500MB 或更少），你可能想要添加第二个硬盘，因为大多数 IDE 控制器可以支持两个。添加第二个硬盘可以防止你弄乱第一个硬盘。如果你有 SCSI 卡，你可以连接多达七个 SCSI 设备。

如果你正在购买新 PC，请记住，完整的 Red Hat Linux 安装（包含所有 Red Hat 软件包）占用超过 1GB 的磁盘空间。除此之外，你还需要一些磁盘空间用于工作。幸运的是，大多数新 PC 的硬盘尺寸范围从 2GB 到 20GB 不等。范围内任何硬盘都足够大，因此你可以将 Windows 保留在一个分区上，然后选择启动 Windows 或 Red Hat Linux。

## 软盘驱动器

正如它们对硬盘所做的那样，Linux 驱动程序使用 PC BIOS 访问软盘驱动器。因此，你的软盘驱动器与 Red Hat Linux 兼容。然而，在安装期间，你必须从软盘驱动器启动 Red Hat Linux。为此，你需要一个高密度 3.5 英寸（容量 1.44MB）软盘驱动器。只要你可以在 MS-DOS 下启动 PC（不是在 Windows 95/98/2000 下的 MS-DOS 窗口），并且可以从 DOS 命令提示符访问 CD-ROM，你就可以避免从软盘启动。

## 键盘和鼠标

Red Hat Linux 支持任何已在你的 PC 上工作的键盘。然而，鼠标需要在 Red Hat Linux 中得到明确支持。如果你想配置和运行 XFree86，即 Linux 的 X Window System，你需要一个鼠标。Red Hat Linux 支持大多数流行的鼠标，包括常见的 PS/2 风格鼠标。

