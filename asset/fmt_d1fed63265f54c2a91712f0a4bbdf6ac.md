
`vnc=1` 表示应在安装系统上启动 VNC 服务器。`vncpasswd=` 指定客户端在连接到主机时需要提供的密码。密码长度必须至少为六个字符；否则，VNC 主机启动时会生成错误，您将无法进行身份验证。安装源（`install=`）可以手动指定（通过指定相关目录的协议和 URL，例如 `ftp://.../install_files` 或 `nfs://10.6.7.9/inst11_files`），也可以是 `install=slp`。在后一种情况下，安装源由 SLP 查询自动确定。

### 警告

如果未指定 `install=`，则使用服务器的本地 CD-ROM 驱动器，在进行远程安装时这可能不是您想要的。

在 IBM 服务器上设置 VNC 主机的具体步骤和语法因型号而异，因此您应参考系统特定文档以获取详细信息。

### WARNING

SLES 9 安装和配置指南第 3.1.7 节“向 linuxrc 传递参数”中显示的参数关键字示例是为了清楚地反映在命令行输入时使用等号（`=`）来分隔关键字及其值，而不是冒号（`:`），如示例所示。

### TIP

默认情况下，基于 VNC 的安装使用 DHCP 获取主机的 IP 信息。但是，您可以通过在 `linuxrc` 参数中包含 `hostip=x.x.x.x netmask=x.x.x.x` 来指定静态 IP 地址。必须与 `hostip` 一起指定 `netmask`；否则将使用 DHCP。

SLES 9 在 CD1 上的 `dosutils/tightvnc` 目录中包含 Windows 32 位 VNC 客户端（TightVNC）。您也可以从 `www.tightvnc.com` 获取最新的 TightVNC 客户端，或使用其他 VNC 客户端，例如来自 `www.realvnc.com` 的客户端。

VNC 服务器还内置了一个小型 HTTP 服务器。通过此功能，您可以使用启用 Java 的 Web 浏览器连接到 VNC 服务器。VNC 服务器在 5801 端口监听 HTTP 连接；例如，要使用的 URL 为 `http://server_name_or_ip_address:5801`。Java 小程序会提示您输入密码（见图 1.2），然后显示桌面。

### FIGURE 1.2

通过 HTTP 访问 VNC 服务器。

![](img/ae8469257d2662b469f2360b3bbbe322_27_0.png)

注意：VNC 默认情况下未加密，因此任何有权访问您与服务器之间网络路径并使用数据包嗅探器的人都可以捕获您的会话并提取密码、服务器设置或其他输入数据。因此，如果您正在执行远程安装，强烈建议您仅在受信任的网络或类似 VMWare 的环境中进行不安全的 VNC 安装。如果您必须在不安全的网络（例如 Internet）上执行 VNC 安装，我们建议您在通过 SSH 或类似的安全连接方法完成安装后立即更改 root 密码以及在不安全会话期间输入的任何其他密码。

## Network-Based Installation

网络安装

通常，将所有必要的安装文件放在中央服务器上并通过网络进行安装要方便得多。这通常比使用“光盘操作员”方法更快。此外，服务器上的文件可以轻松更新。拥有此类安装服务器的一个附带好处是以后安装软件包的便捷性；您可以简单地将 YaST 指向该服务器，而不必找到 CD 并希望服务器的 CD-ROM 驱动器没有被灰尘堵塞。有两种方法可以设置网络安装所需的目录结构。一种方法是将每个 CD 的内容复制到单独的目录中。这具有目录结构更清晰的优点，并且使更新特定 CD 更容易。缺点是当 YaST 需要访问不同 CD 上的内容时，您将被提示输入相应目录的名称，从而稍微减慢安装过程。另一种方法是将所有 CD 的内容复制到单个目录中。使用此设置，YaST 不会提示您“切换”CD。

与其设置临时中央安装服务器（例如在 NetWare 上运行的 FTP 服务器），SUSE LINUX 为 YaST 提供了安装服务器模块，支持通过 FTP、NFS 和 HTTP 连接进行安装。有关更多详细信息，请参阅 SLES 9 安装和配置指南第 4 章“中央软件安装和更新”。

`Linuxrc` 安装过程支持 FTP、NFS、Samba、HTTP、TFTP 和 SLP 协议进行网络安装。

## AutoYaST-Based Installation

基于 AutoYaST 的安装

如果您使用相似的硬件部署服务器，并且配置了相同的一组基本服务，则可以使用 AutoYaST。AutoYaST 依赖于 YaST 的硬件检测机制，通常使用默认设置，但也可以根据您的特定需求进行自定义。因此，安装主机不必完全相同。它们具有相似的硬件设置就足够了。您仍需考虑硬件本身的限制，AutoYaST 无法规避这些限制。

YaST 包含一个 AutoYaST 模块，可用于创建必要的配置。然后将此配置写入 XML 文件，因此也可以对其进行编辑甚至手动创建。当您对 XML 文件的内容满意时，将其复制到软盘，以便用于安装新系统。在下一台服务器上，在启动选项字段中传递以下内容

`autoyast=floppy:///filename.xml`

其中 `filename.xml` 是您的配置文件。

### CAUTION

注意

请注意用于执行基于 AutoYaST 安装的“URL”中的三个斜杠。

有关 AutoYaST 的更多信息和大量文档包含在 `autoyast2` 包中。您可以在 `www.suse.de/~nashif/autoinstall` 找到在线文档，其中包含许多示例。

## Pre-Installation Planning

安装前规划

在实际安装软件之前，请花几分钟时间进行安装前规划。服务器配置的某些方面（例如硬盘分区方案和文件系统类型选择）在 SLES 9 安装后很难更改。因此，花几分钟时间规划可以为您节省以后数小时的重新配置工作。

您首先应确保服务器硬件满足表 1.2 中列出的 SLES 9 最低系统要求。

**TABLE 1.2**

**表 1.2**

SLES 9 System Requirements

SLES 9 系统要求

| REQUIREMENT | NOTES |
|---|---|
| 安装所需的最低系统内存要求 | 如果您执行本地安装，需要 256MB；基于 SSH 的网络图形安装需要 256MB；而通过 FTP 的基于 VNC 的网络安装需要 512MB。 |
| 运行所需的最低系统要求 | 具有 Pentium II 或 AMD K7 450 MHz 处理器和 384MB RAM 的服务器级计算机。根据软件包选择，需要 500MB 硬盘空间用于系统软件（精简、无图形界面、基础安装占用 400MB，而完整安装占用 2.5GB 磁盘空间），另需 500MB 硬盘空间用于用户数据。如果从 CD 介质安装，需要 4X CD-ROM 驱动器；如果 CD-ROM 驱动器不支持启动，则需要软盘驱动器。 |

**TABLE 1.2**

**表 1.2**

**SLES 9 System Requirements (continued)**

**SLES 9 系统要求（续）**

| REQUIREMENT | NOTES |
|---|---|
| 推荐的运行系统要求 | 具有 Pentium 4 或 AMD K8 或更高端（如 Intel Xeon EM64T）处理器和 512MB 至 3GB RAM 的服务器级计算机；您应每颗 CPU 至少配备 512MB RAM。分配 4GB 硬盘空间用于系统软件，10GB（或更多）用于用户数据。如果从 CD 介质安装，需要 48X CD-ROM 驱动器；如果 CD-ROM 驱动器不支持启动，则需要软盘驱动器。 |

SLES 9 支持 Intel x86、AMD、AMD64、Intel Xeon EM64T 和 Itanium 处理器系列。它还可在 IBM POWER 处理器（以前的 IBM iSeries 和 IBM pSeries 系统）、IBM zSeries 和 IBM S/390 系统上运行。有关更详细的系统要求，例如特定于 IBM zSeries 64 位系统的要求，请参阅位于 `www.novell.com/documentation/sles9/index.html` 的 SUSE LINUX Enterprise Server 9 文档。

### NOTE

注意

Novell 的 Open Enterprise Server (OES) 软件同时包含 NetWare 内核和 Linux 内核（SLES 9）。因此，如果您计划稍后向服务器添加 OES 服务，请务必在初始配置服务器时考虑额外的 RAM 和磁盘空间要求。
