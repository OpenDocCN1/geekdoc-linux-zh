
| `/opt/ignite/inst1_boottab` | 记录用于引导 PA-RISC 客户端的 IP 地址 |
| `/opt/ignite/bin/bootbys` | 更新已经运行 HP-UX 的客户端 |
| `/opt/ignite/bin/make_config` | 使用安装仓库创建配置信息文件 |
| `/opt/ignite/bin/make_depots` | 从某些源介质创建安装仓库 |
| `/opt/ignite/bin/manage_index` | 将仓库添加到 Ignite-UX 索引中 |
| `/opt/ignite/sbin/setup_server` | 通过 NFS 共享 `/var/opt/ignite/clients` |
| `/var/opt/ignite/clients` | 存储客户端配置文件（目录） |
| `/var/opt/ignite/data` | 传统上用于存放安装仓库（目录） |
| `/var/opt/ignite/INDEX` | 为 Ignite-UX 已知的所有安装仓库建立索引 |

`make_depots` 命令会提取安装软件包，并将其设置为可供客户端安装的操作环境仓库。创建仓库后，运行 `make_config` 读取仓库内容，并创建一个描述这些内容的配置文件。通过 `manage_index` 命令，Ignite-UX 可以获知该配置；该命令会将配置添加到 `INDEX` 文件中。下面展示了用于版本 11i v3 的一组示例命令。

```
hp-ux% cd /opt/ignite/bin
hp-ux% sudo ./make_depots -s /dev/dsk/c2t2d0
    -d /var/opt/ignite/depots/Rel_B.11.31/oe_media
hp-ux% sudo ./make_config -s /var/opt/ignite/depots/Rel_B.11.31/core_media
    -c /var/opt/ignite/data/Rel_B.11.31/oe_media.cfg
hp-ux% sudo ./manage_index -n "HP-UX B.11.31 Default" -c "11i v3"
hp-ux% sudo ./manage_index -a
    -f /var/opt/ignite/data/Rel_B.11.31/oe_media.cfg -c "11i v3"
```

在客户端可以使用服务器之前，必须启用 BOOTP 并共享 `clients` 目录。还必须根据客户端机器是 PA-RISC 还是 Itanium，将各个客户端添加到 `inst1_boottab` 或 `bootptab` 文件中。

要通过 NFS 共享配置目录，只需运行 `/opt/ignite/sbin/setup_server`。在后台，该命令只是在 `/etc/dfs/sharetab` 中创建一个 NFS 共享。

可以通过取消 `/etc/inetd.conf` 中 `bootps` 行的注释来启用 BOOTP。然后运行 `/usr/sbin/inetd -c`，让 `inetd` 重新读取其配置。

对于 PA-RISC 系统，请编辑文件 `/etc/opt/ignite/inst1_boottab`。该文件中的行采用以下格式：

```
IP_address:MAC_address:datetime_last_used [ : reserve ]
```

`IP_address` 字段为新客户端分配一个 IP 地址，供其在访问安装服务时使用。可选的 `MAC_address` 字段用于标识特定的客户端机器；如果省略该字段，任何客户端都可以使用这个 IP 地址（但请注意与 `reserve` 关键字的交互）。第三个字段由 Ignite-UX 使用和维护；添加新条目时请将其留空。

如果最后一列中包含关键字 `reserve`，则该 IP 地址保留给第二列中 MAC 地址所对应的客户端使用。如果未指定 `reserve`，则第二列仅显示使用过该 IP 地址的最后一个 MAC 地址。

用于引导 Itanium 系统的 `/etc/bootptab` 和 `/etc/dhcptab` 文件采用了非常不同的格式。这些文件注释详尽，并大量提供了示例，我们在此不再重复。（请注意，在 HP-UX 系统中，单个守护进程 `bootpd` 同时处理 BOOTP 和 DHCP 请求。）对于 Itanium 系统，DHCP 是首选的引导方法，因为它可以提供匿名客户端服务。详细说明请参阅 `/etc/bootptab` 和 `/etc/dhcpv6tab` 中的注释。

按照上述方法配置好 Ignite-UX 服务器后，客户端即可通过网络从中引导。在客户端一侧，中断正常引导过程，进入 EFI 启动管理器，然后添加网络设备。客户端将请求 IP 地址，Ignite-UX 服务器则会响应并开始安装。

此方法最适合与 Ignite-UX 服务器位于同一子网的系统。对于客户端不在服务器子网中的配置，HP 在《Ignite-UX 管理指南》中列出了多种选项。

### 自动化 Ignite-UX 安装

Ignite-UX 网络引导配置是自动化安装的前提条件，但如果在配置 Ignite-UX 时未指定自动引导详细信息，则会进行交互式安装。Ignite-UX 还可以：

- 使用之前安装中保存的配置来自动化未来的安装。
- 依赖可按客户端、按版本或由管理员自行决定而设置的配置文件。
- 为某些配置选项（如 DNS 服务器）指定默认值，并让其他选项在交互式安装期间由用户选择。

自动化安装文件位于 `/opt/ignite/data` 中，Ignite-UX 安装包中包含多个示例和样例配置。`release` 和 `example` 子目录是很好的入手点。

## 12.4 使用网络安装管理器安装 AIX

网络安装管理器，或 NIM，是 AIX 对 Kickstart、JumpStart 和 Ignite-UX 的回应。自 AIX 5.3 以来的 NIM 版本也可以安装 Linux 系统。NIM “主”服务器从一个或多个安装映像安装客户端，其中客户端可以是独立机器、无盘或无数据工作站，或工作负载分区。² 安装依赖于 TFTP、NFS 以及 DHCP 或 BOOTP，与其他系统类似。³ NIM 包含在标准 AIX 安装介质上。

所有 NIM 环境至少有一个提供一组供客户端使用的软件的“资源服务器”。资源服务器可能与主服务器是同一系统，也可能不是。对于具有复杂网络拓扑或地理位置分散的环境，应使用本地化资源服务器以提高安装性能。

配置 NIM 有三种方法：

- 使用基于 Web 的系统管理器
- 使用 `smit nim` 或 `smit ezinim` 快捷路径
- 使用 `nim` 工具从命令行操作

我们发现 SMIT 是配置 NIM 环境最快、最方便的界面。“EZ”版本涵盖了大多数常见的 NIM 任务，例如快速设置主服务器、更新、备份或重新安装现有客户端，以及配置新客户端。功能齐全的 `smit nim` 版本在 EZ NIM 之上增加了一些复杂性，但增加了更多配置选项，例如能够包含自定义软件包以及对已安装客户端进行更精细的控制。

如果你坚持使用命令行操作，`nim_master_setup` 工具是最好的入门位置。（SMIT 的 EZ-NIM 配置主服务器选项实际上只是使用指定选项调用 `nim_master_setup`。）此工具为 NIM 软件资源初始化文件系统，创建必要的配置文件，并复制一份示例客户端配置文件供你编辑以用于本地客户端。

最基本的用法是 `nim_master_setup -a device=/dev/cd0`，其中 `/dev/cd0` 是包含目标 AIX 版本安装介质的驱动器。与本章描述的大多数其他安装系统不同，NIM 主服务器只能安装相同修订级别或更早版本的 AIX；AIX 5.2 服务器无法安装 AIX 6.1 版本。

表 12.4 列出了一些最有用的 NIM 相关命令行工具。

2. 无盘客户端没有用于本地文件系统的硬盘，依赖网络服务进行存储。无数据客户端仅有本地交换空间，也许还有 `/tmp` 和 `/home` 文件系统。

3. 由于各厂商都使用大致相同的协议和架构，你难道不高兴他们合作并确定了一个标准的安装系统吗？:-)

## 12.6 管理 Linux 软件包

Linux 系统上常见使用两种软件包格式。Red Hat、SUSE 以及其他几个发行版使用 RPM，即 Red Hat 软件包管理器。Ubuntu 使用单独但同样流行的 `**.deb**` 格式（以 Ubuntu 最初基于的 Debian 发行版命名）。这两种格式在功能上相似。

使用诸如 `kjennet.net/programs/alien` 上的 `**alien**` 之类的工具，可以轻松地在两种软件包格式之间转换。`**alien**` 对软件包内部的软件一无所知，因此如果内容与你的发行版不兼容，`**alien**` 也无能为力。一般来说，最好坚持使用发行版使用的原生软件包机制。

RPM 和 `**.deb**` 打包系统现在都作为双层端到端配置管理工具运行。在最低层是安装、卸载和查询软件包的工具：RPM 系统使用 `**rpm**`，`** .deb**` 使用 `**dpkg**`。
