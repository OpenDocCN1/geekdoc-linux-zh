

## 在支持 64 位处理器的计算机上，我应该安装 32 位还是 64 位 Linux？

> 以下信息可能有助于您决定在支持 64 位处理器的计算机上安装 32 位还是 64 位 Linux。

-   EM64T/AMD64 处理器可以同样出色地运行两种版本的 Linux。
-   64 位发行版允许每个进程寻址超过 4 GB 的内存。更大的地址空间是 64 位发行版最大的优势。它通常仅对特定的工程/科学计算工作以及运行多个虚拟机时有用。
-   总体而言，64 位处理器并不比 32 位处理器更快；大多数基准测试显示性能大体相似。在某些情况下性能更好，而在某些情况下性能更差：两种类型的处理器都没有明显的性能优势。
-   64 位 Linux 的内存模型使得指针的大小是 32 位 Linux 中指针大小的两倍。这种大小差异会导致内存使用量增加 5% 以上，具体取决于应用程序。如果系统内存紧张，这种开销可能会使 64 位系统的性能变差。
-   ASLR（地址空间布局随机化）在 64 位系统提供的更大地址空间下工作得更好。ASLR 有助于提高系统安全性。参见 en.wikipedia.org/wiki/Address_space_layout_randomization。
-   一些多媒体编码器在 64 位 Linux 下运行速度提升 10-30%。
-   某些专有第三方应用程序的功能在 64 位架构上不可用。
-   64 位 Linux 系统可以运行 32 位应用程序，但 32 位 Linux 系统无法运行 64 位应用程序。
-   如果不重新安装 Linux，就没有简单的方法在 32 位和 64 位版本之间来回切换。
-   如果您不确定使用哪个版本，请安装 64 位版本。

## 界面：安装程序和已安装系统

当您安装 Fedora/RHEL 时，您可以选择在安装过程中使用的界面（用于与 Anaconda 安装程序交互）。您也可以选择在操作已安装系统时使用的界面。本节介绍了两种基本界面：文本式和图形式。

**文本式 (TUI/CLI)**
TUI（文本用户界面），也称为 CLI（命令行界面）或基于字符的界面，显示字符和一些简单的图形符号。它是面向行的；您仅使用键盘向其发出指令。

**图形式 (GUI)**
GUI（图形用户界面）通常显示桌面（例如 GNOME）和窗口；您使用鼠标和键盘向其发出指令。您可以通过打开终端模拟器窗口在 GUI 中运行文本界面（第 120 页）。与文本界面相比，GUI 使用更多的计算机资源（CPU 时间和内存）。

**伪图形式**
伪图形式界面是一种利用基于文本的显示设备（如终端）上图形元素的文本界面。它还可能使用颜色。该界面使用文本元素，包括简单的图形符号，来绘制模仿 GUI 窗口和按钮的粗糙框。通常，按下 TAB 键会将光标（高亮显示）从一个元素移动到下一个元素，而按下 RETURN 键则选择光标所在的元素。

**优势**
GUI 用户友好，而文本界面紧凑，使用更少的系统资源，并且可以在纯文本终端或纯文本连接上工作。由于效率更高，文本界面适用于较旧、较慢的系统以及内存极少的系统。服务器系统通常使用文本界面，因为它允许系统将更多资源用于执行其设定的任务，而更少资源用于取悦系统管理员。不运行 GUI 还可以提高系统安全性。

## Fedora、RHEL 和 CentOS

本书介绍了两种产品：Fedora 和 RHEL（红帽企业 Linux）。本节简要介绍了这些产品。

**Fedora**
Fedora 项目由红帽赞助并得到开源社区的支持。Fedora 版本大约每六个月发布一次，该 Linux 发行版融入了尖端代码。它*不是*受支持的红帽产品，也*不建议*用于生产环境，因为在生产环境中软件包和功能集需要在较长时间内保持恒定。Fedora 旨在反映其融入的上游项目，包括内核。它被广泛认为是最稳定的“免费” Linux 发行版。相比之下，RHEL 包含了许多由 Fedora 引入的更改。

Fedora 项目大约每六个月分发一个新版本的 Fedora。每个版本都有一个编号和一个名称。例如，Fedora 18 名为 Spherical Cow（球体牛），Fedora 19 名为 Schrödinger’s Cat（薛定谔的猫）。之前的版本名为 Lovelock（15）、Verne（16）和 Beefs Miracle（17）。有关名称选择方法的描述，请参阅 [fedoraproject.org/wiki/History_of_Fedora_release_names](fedoraproject.org/wiki/History_of_Fedora_release_names)。

**RHEL**
RHEL 通常通过包含技术支持的年度订阅销售。它比 Fedora 更稳定，但不如 Fedora 尖端。RHEL 提供 10 年的更新；Fedora 提供 13 个月。

红帽企业 Linux 有多种配置；更多信息请参见 www.redhat.com/wapps/store/catalog.html。有关 RHEL 各个版本的更多信息，请参见 www.redhat.com/rhel/compare。

红帽每隔几年分发一个新的大版本 RHEL。有关 RHEL 生命周期的信息，请参见 access.redhat.com/support/policy/updates/errata。

**CentOS**
CentOS（www.centos.org）是一个免费的、与 RHEL 兼容的 Linux 发行版。它比 Fedora 具有更长的稳定性，但与 RHEL 不同，CentOS 不提供支持。由于 CentOS 与 RHEL 兼容，本书也介绍了 CentOS。CentOS 版本通常跟随 RHEL 版本发布。

## Fedora 标准版本：Live、Install 和 Network 镜像

Fedora 标准版本针对 i386（32 位）和 x86_64（64 位）架构编译，可通过 BitTorrent、直接下载和镜像站获取。要下载标准版本，请访问 fedoraproject.org/en/get-fedora-all。

### 术语：CD、DVD、安装介质和安装镜像

> > Fedora 有三种版本：Fedora Desktop Live Media（Fedora 桌面 Live 介质）、Fedora DVD 和 Fedora Network Install CD（Fedora 网络安装 CD）。版本名称中的 DVD 和 CD 是惯例用语，与该版本可用的实际介质无关。这些版本中的每一个都提供为安装（ISO）镜像文件，可以写入 CD、DVD、USB 闪存驱动器或其他适当大小的介质（即安装介质）。本书使用术语“安装镜像”来指代存在于任何介质上的安装（ISO）镜像文件。除非上下文需要，否则它并不特指 CD、DVD 或 USB 闪存驱动器。

本书将 Fedora Desktop Live Media 称为 *Live 镜像*。Live 镜像运行 *Live 会话*：它在未将 Fedora 安装到硬盘的情况下运行 Fedora，尽管您可以从 Live 会话安装基本的 Fedora 系统。安装完成后，您可以使用 Internet 连接向系统添加更多软件包。

要从 Live 镜像启动，请确保 Live ISO 设置为从 DVD 或 USB 驱动器启动；更多信息请参见“BIOS 设置”和“CMOS”，均位于第 51 页。从 Live 镜像启动会显示 GNOME 桌面（如果您从 KDE Live 镜像启动，则显示 KDE 桌面）：您正在运行 Live 会话。当您退出 Live 会话时，系统恢复到从 Live 镜像启动前的状态。如果系统有 Linux swap 分区（大多数 Linux 系统都有；参见第 40 页），Live 会话将使用它来提高性能，但除此之外不会写入硬盘。RHEL 不提供 Live 镜像。

运行 Live 会话是测试硬件和修复无法从硬盘启动的系统的好方法。Live 会话对于刚接触 Fedora 或 Linux 并想尝试 Fedora 或不同桌面环境但尚未准备好将其安装到系统中的人来说是理想的。

### 在 Live 会话期间保存文件

> > 您无法将文件保存到持有 Live 镜像的 DVD 上，因为这是只读介质。在 Live 会话期间，即使您看似保存了文件，在您退出 Live 会话后，它也不会存在。要保存来自 Live 会话的数据，请将其保存到网络共享或 USB 闪存驱动器，或者通过电子邮件发送给自己。或者，您可以从具有持久存储功能的 Live USB 闪存驱动器启动。您可以使用 livusb-creator（第 50 页）创建这样的 USB 驱动器。更多信息请参见 fedoraproject.org/wiki/How_to_create_and_use_Live_USB。

### Install 镜像比 Live 镜像使用更少的内存

> > 使用 Install 镜像安装 Fedora 系统比使用 Live 镜像安装系统使用更少的内存（RAM）。如果您在旧系统上使用 Live 镜像安装时遇到问题，请尝试使用 Install 镜像安装。

