
您的 Linux 文件系统组织成目录，其中的文件用于不同的系统功能（见表 27-6）。对于基本的系统管理，您应该熟悉存放应用程序的系统程序目录、放置大多数配置文件的系统配置目录（`/etc`），以及保存系统日志（记录系统活动）的系统日志目录（`/var/log`）。其他系统目录在各自章节中涵盖，许多在第 30 章中讨论。

### 表 27-6：系统目录

| 目录 | 描述 |
|---|---|
| `/bin` | 系统相关程序 |
| `/sbin` | 用于专门任务 的系统程序 |
| `/lib` | 系统库 |
| `/etc` | 系统和网络服务及应用程序的配置文件 |
| `/home` | 用户主目录和服务器数据目录的位置，如 Web 和 FTP 站点文件 |
| `/mnt` | CD-ROM 和软盘文件系统挂载的位置（第 30 章） |
| `/var` | 文件持续变化的系统目录的位置，如日志、打印机打印作业文件和锁定文件（第 30 章） |
| `/usr` | 用户相关程序和文件；包含几个关键子目录，如 `/usr/bin`、`/usr/X11` 和 `/usr/doc` |
| `/usr/bin` | 用户程序 |

### 表 27-6：系统目录

| 目录 | 描述 |
|---|---|
| `/dev` | 设备文件（第 32 章） |
| `/usr/X11` | X 窗口系统配置文件 |
| `/usr/share` | 共享文件 |
| `/usr/share/doc` | 应用程序的文档 |
| `/tmp` | 系统临时文件目录 |

#### 程序目录

名称中包含 `bin` 的目录用于存放程序。`/bin` 目录存放基本用户程序，例如 `login`、shell（`BASH`、`TCSH` 和 `ZSH`）以及文件命令（`cp`、`mv`、`rm`、`ln` 等）。`/sbin` 目录存放专门用于此类任务的系统程序，如文件系统管理（`fsck`、`fdisk`、`mkfs`）以及关机（`shutdown`）和启动（`init`）等系统操作。`/usr/bin` 目录存放设计用于用户任务程序文件。`/usr/sbin` 目录存放与用户相关的系统操作，例如使用 `useradd` 添加新用户。`/lib` 目录存放系统使用的所有库，包括主要的 Linux 库 `libc` 以及诸如 `modules` 之类的子目录，后者存放所有当前的内核模块。

#### 配置目录和文件

当您配置系统的不同元素，如用户、应用程序、服务器或网络连接时，会用到保存在某些系统目录中的配置文件。在 Red Hat 中，配置文件放置在 `/etc` 目录中，更具体的设备和配置文件位于 `/etc/sysconfig` 目录中。

##### 配置文件：`/etc`

`/etc` 目录存放系统、网络、服务器和应用程序的配置文件。在这里可以找到列出文件系统的 `fstab` 文件、包含系统中主机 IP 地址的 `hosts` 文件，以及供 GRUB 引导加载程序支持的启动系统使用的 `grub.conf`。此目录包含各种子目录，例如用于 Apache Web 服务器配置文件的 `/apache` 和用于 X 窗口系统及窗口管理器配置文件的 `/X11`。您可以通过直接编辑其配置文件来配置许多应用程序和服务，但最好使用相应的管理工具，例如 Red Hat 提供的工具。表 27-7 列出了在 `/etc` 目录中找到的几种常用配置文件。

##### `/etc/sysconfig`

在 Red Hat 系统中，配置和启动信息也保存在 `/etc/sysconfig` 目录中。在这里可以找到包含用于配置键盘和鼠标等设备的系统变量定义的文件。这些条目是在安装期间配置设备时为您定义的。您还将找到网络定义以及用于启动和停止网络连接的脚本。

这里展示了键盘文件 `/etc/sysconfig/keyboard` 的示例。

```
KEYBOARDTYPE="pc"
KEYTABLE="us"
```

###### 表 27-7：配置文件

| 文件 | 描述 |
|---|---|
| `/etc/inittab` | 设置默认状态以及终端连接 |
| `/etc/passwd` | 包含用户密码和登录配置 |
| `/etc/shadow` | 包含用户加密后的密码 |
| `/etc/group` | 包含组列表及其各自的配置 |
| `/etc/fstab` | 启动系统时自动挂载文件系统 |
| `/etc/grub.conf` | GRUB 引导加载程序的 GRUB 配置文件 |
| `/etc/modules.conf` | 系统中要自动加载的模块 |
| `/etc/printcap` | 包含每个打印机及其规格的列表 |
| `/etc/termcap` | 包含可连接到系统的终端类型规格的列表 |
| `/etc/skel` | 保存初始化文件（如 `.bash_profile`）版本的目录，这些文件会被复制到新用户的主目录中 |
| `/etc/services` | 系统中运行的服务及其使用的端口 |
| `/etc/profile` | 用户的默认 shell 配置文件 |
| `/etc/shells` | 系统中安装的用户可以使用的 shell |
| `/etc/motd` | 系统管理员的每日消息 |

其中一些文件由 Red Hat 管理工具生成，例如 `redhat-config-mouse`、`redhat-config-keyboard` 或 `redhat-config-network`。表 27-8 列出了几种常用工具及其控制的 sysconfig 文件。例如，`redhat-config-mouse` 生成鼠标设备名称、类型和特定功能的配置变量，并将其放置在 `/etc/sysconfig/mouse` 文件中，如下所示：

```
FULLNAME="Generic - 3 Button Mouse (PS/2)"
MOUSETYPE="PS/2"
XMOUSETYPE="PS/2"
XEMU3="no"
DEVICE="/dev/mouse"
```

其他文件，如 `hwconf`，列出您所有的硬件设备，定义配置变量，例如它的类（视频、CD-ROM、硬盘）、它使用的总线（PCI、IDE）、其设备名称（如 `hdd` 或 `st0`）、它使用的驱动以及设备的描述。这里展示了一个 CD-ROM 条目：

```
class: CDROM
bus: IDE
detached: 0
device: hdd
driver: ignore
desc: "TOSHIBA DVD-ROM SD-M1402"
```

包含几个目录，例如 `network-scripts`，其中列出了几个网络连接启动脚本，例如 `ifup-ppp`，用于启动 PPP 连接。

###### 表 27-8：Sysconfig 文件及对应的 Red Hat 系统管理工具

| 工具 | 配置文件 | 描述 |
|---|---|---|
| `authconfig-gtk` | `/etc/sysconfig/authconfig`<br>`/etc/sysconfig/network` | 身份验证选项，如启用 NIS、shadow 密码、Kerberos 和 LDAP。 |
| `redhat-config-securitylevel` | `/etc/sysconfig/iptables` | 选择防火墙保护级别：高、中和无。 |
| `redhat-config-keyboard` | `/etc/sysconfig/keyboard` | 选择键盘类型。 |
| `redhat-config-mouse` | `/etc/sysconfig/mouse` | 选择鼠标类型。 |
| `redhat-config-network` | `/etc/sysconfig/network`<br>`/etc/sysconfig/network-scripts/ifcfg-ethN` | 设置您的网络配置。 |
| `redhat-config-date` | `/etc/sysconfig/clock` | 设置时间和日期。 |
| `redhat-logviewer` | `/etc/sysconfig/redhat-logviewer` | Red Hat 日志查看器，查看和搜索系统日志。 |

某些管理工具使用多个 sysconfig 文件。`redhat-config-network` 将其网络配置信息（如主机名和网关）放在 `/etc/sysconfig/network` 文件中。特定的以太网设备配置（包括您的 IP 地址和子网掩码）被放置在 `/etc/sysconfig/network-scripts` 目录中相应的以太网设备配置文件中。例如，用于 `eth0` 以太网设备的 IP 地址和子网掩码可以在 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中找到。本地主机设置位于 `/etc/sysconfig/network-scripts/ifcfg-lo`。

##### 提示

某些管理工具，如 `authconfig-gtk`，将进一步配置所选服务的配置文件。`authconfig-gtk` 工具配置 `/etc/sysconfig/authconfig` 以及 `/etc/krb5`。
