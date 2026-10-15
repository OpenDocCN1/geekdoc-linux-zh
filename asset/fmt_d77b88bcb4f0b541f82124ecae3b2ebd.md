
一旦你重启了 `cupsd`，远程系统就可以使用 `Listen` 指令指定的 IP 地址和端口号在本地系统的打印机上进行打印。如果服务器运行着防火墙，你需要允许远程系统通过该防火墙连接；参见第 549 页。

或者，你可以使用 CUPS 的访问控制列表（ACL）来仅允许选定的机器连接到本地打印机。访问控制列表定义在 `<Location>` 容器内部（关于 Apache 中的等效功能，参见第 918 页）。以下示例仅允许位于 IP 地址 `192.168.1.101` 的系统和本地系统向指定打印机打印：

```
<Location /printers>
 Order Allow,Deny
 Allow from localhost
 Allow from 192.168.1.101
</Location>
```

`/printers` 表示此容器引用所有本地打印机。或者，你可以通过指定 `/printers/printer-name`（其中 `printer-name` 是打印机名称）或指定 `/printers/path.ppd`（其中 `path.ppd` 是打印机使用的 PPD 文件的完整路径名，参见第 561 页）来按打印机控制访问权限。

`Order Deny,Allow` 指令默认允许访问，仅拒绝 `Deny from` 指令中指定的客户端的访问。`Order Allow,Deny` 指令默认拒绝打印请求，仅允许来自指定地址的请求。在 `Allow from` 和 `Deny from` 指令中，你可以使用域名（包括通配符）以及带有通配符或子网掩码的 IP 地址范围。这些指令的工作方式与 Apache 中相同。更多信息请参阅第 931 页的“Order”部分。

在使用 `Order Deny,Allow` 指令时，`Deny from` 指定了 CUPS 不接受连接的唯一 IP 地址。当使用 `Order Allow,Deny` 指令时，`Allow from` 指定了 CUPS 接受连接的唯一 IP 地址。

## 从 Windows 进行打印

本节介绍如何从 Windows 机器使用 Linux CUPS 服务器上的打印机。与使用 Samba 从 Windows 打印相比，CUPS 更易于管理，并且可以设置得更加安全。

### 使用 CUPS 进行打印

现代版本的 Windows（2000 及以后版本）支持 IPP，因此可以直接与 CUPS 通信。要使用此功能，必须配置 Linux 打印服务器上的 CUPS 以允许远程 IPP 打印；你还需要在 Windows 系统上创建一个新打印机，该打印机指向 Linux 打印服务器的 IP 地址。

首先，按照第 565 页“共享 CUPS 打印机”中的说明设置 `/etc/cups/cupsd.conf` 文件，以允许来自客户端的网络打印。设置 CUPS 以允许从 Windows 机器打印，与设置其允许从 Linux 客户端系统打印完全相同。如有必要，请按第 549 页的说明打开防火墙。

从 Windows XP 开始，转到控制面板→打印机和传真，点击**添加打印机**。在介绍窗口中点击“下一步”，选择**网络连接上的打印机或其他计算机附接的打印机**。点击“下一步”。选择**连接到互联网或家庭/办公室网络上的打印机**，并在标记为 **URL** 的文本框中输入以下信息：

`http://host-name:631/printer-name`

其中，`host-name` 是 Linux CUPS 服务器系统的名称或 IP 地址，`printer-name` 是该系统上打印机的名称。例如，对于位于 IP 地址为 `192.168.0.12` 的名为 `dog` 的系统上名为 `dog88` 的打印机，你可以输入 `http://dog:631/printers/dog88` 或 `http://192.168.0.12:631/printers/dog88`。如果你使用主机名，它必须在 Windows 机器上的 `hosts` 文件中定义。Windows 会要求你指定打印机的制造商和型号，或者为打印机提供驱动程序。如果你提供打印机驱动程序，请使用该驱动程序的 Windows 版本。

Windows 复制完某些文件后，打印机将出现在“打印机和传真”窗口中。右键单击打印机并选择**设为默认打印机**，即可将其设为默认打印机。你可以通过右键单击打印机并选择**属性**来指定打印机的注释、位置及其他属性。

## 使用 Samba 进行打印

本节假设 Samba（参见第 797 页）已安装并正在控制你想从 Windows 使用的打印机的 Linux 系统上运行。必须配置 Samba，使得执行打印的 Windows 用户映射到一个 Linux 用户（包括将 Windows `guest`（来宾）用户映射到 Linux 用户 `nobody`）。确保这些用户拥有 Samba 密码。请参阅第 799 页的“Samba 用户、用户映射和密码”。

Windows 支持通过 SMB 共享打印机，这使得打印机能够使用与文件共享相同的机制在 Windows 系统之间透明共享。Samba 允许 Windows 用户使用连接到 Linux 系统的打印机，就像使用其他共享打印机一样。由于所有 Linux 打印机传统上都表现为 PostScript 打印机，Linux 打印服务器表现得像是在共享一个 PostScript 打印机。Windows 不包含通用的 PostScript 打印机驱动程序。相反，Windows 用户必须为 PostScript 打印机选择一个打印机驱动程序。Apple LaserWriter 12/640ps 驱动程序是一个很好的选择。

当你安装 Samba 时，`dpkg postinst` 脚本会创建一个名为 `/var/spool/samba` 的目录，该目录由 `root` 账户所有，任何人可读可写。为此目录设置了粘滞位（参见第 1174 页），这使得作为 Linux 用户启动打印作业的 Windows 用户能够删除该作业，但拒绝用户删除其他用户的打印作业。确保该目录已就位，并具有正确的所有权和权限：

```bash
$ ls -ld /var/spool/samba
drwxrwxrwt 2 root root 4096 2010-10-10 12:29 /var/spool/samba
```

将以下两行放入 `/etc/samba/smb.conf` 文件的 `[global]` 部分：

```ini
[global]
...
    printing = cups
    printcap name = cups
```

打印机的共享列在 `smb.conf` 的 `[printers]` 部分中。在以下示例中，`path` 是 Samba 用作暂存目录的路径，而非常规共享路径。这些设置允许任何人（包括来宾）使用该打印机。默认 `smb.conf` 文件中的 `[printers]` 部分包含以下条目，这些条目适用于大多数设置：

```ini
[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
    guest ok = no
    writable = no
    printable = yes
```

理想情况下，计划打印的每个用户都应该有一个账户。否则，当多个用户共享同一个账户（例如，`nobody` 账户）时，他们可以相互删除打印作业。

## 打印到 Windows

CUPS 查看 Windows 机器上的打印机的方式与查看任何其他打印机的方式完全相同。唯一的区别在于连接时需要指定的 URL。要配置连接到 Windows 机器的打印机，请进入 CUPS Web 界面的打印机页面，并选择**添加打印机**，就像处理本地打印机一样。当被要求选择设备时，选择通过 **SAMBA** 连接的 **Windows Printer**（Windows 打印机）。按以下格式输入打印机的 URL：

```
smb://windows_system/printer_name
```

其中，`windows_system` 可以是 IP 地址或主机名。添加打印机后，你可以像使用其他打印机一样使用它。

## 章节摘要

CUPS 等打印系统负责设置打印机。它还负责将打印作业从应用程序或命令行通过适当的过滤器移动到合适打印机的队列中，然后打印这些作业。

CUPS 是一个基于 IPP（互联网打印协议）构建的跨平台打印服务器。它通过打印队列处理作业的设置与发送。配置打印机最简单的方法是通过打印窗口（`system-config-printer`）。你也可以使用 Web 界面来配置 CUPS，只需将 Web 浏览器指向打印机所连接系统的 `localhost:631` 即可访问。通过 Web 界面，你可以配置打印队列并修改队列中的打印作业。

你可以使用传统的 UNIX 命令从命令行向打印机发送作业（`lpr/lp`）、显示打印队列（`lpq/lpstat`）以及从打印队列中移除作业（`lpw/cancel`）。此外，CUPS 提供了 `lpinfo` 和 `lpadmin` 实用工具，允许你从命令行配置打印机。

CUPS 和 Samba 使你能够从 Windows 计算机在 Linux 打印机上打印，反之亦然。

### 练习

1. 你可以使用哪些命令从命令行向默认打印机发送文件？
2. 你应该使用哪个命令来取消系统上的所有打印作业？
3. 哪些命令可以列出你未完成的打印作业？
4. 使用 Samba 共享 Linux 打印机的目的是什么？
5. 请列举 CUPS 支持的三种打印协议。其中 CUPS 的原生协议是哪种？

### 进阶练习

6. 哪个命令可以列出 CUPS 可用的已安装打印机驱动程序？
7. 如何不使用打印队列而将一个文本文件发送到连接到第一个并行口的打印机？为什么这样做是个坏主意？
8. 假设你有一个带有制造商提供的 PostScript 打印机定义文件（名为 `newprinter.ppd`）的 USB 打印机。你会使用哪个命令将此打印机以 `USBprinter` 的名称添加到系统的第一 USB 端口？
9. 如何定义一个配额，允许每个用户每周向名为 `LaserJet` 的打印机打印不超过 50 页？
10. 在 `/etc/cups/cupsd.conf` 内的 `<Location>` 容器中定义一组访问控制规则，允许任何人打印到所有打印机，只要他们位于本地系统或 `mydomain.com` 域中。

*此页故意留白*

# 15 构建 Linux 内核

**本章内容**

- 下载内核源代码 . . . . . . . . . . . . . . . . . . 573
- 配置和编译 Linux 内核 . . . . . . . . . . . . . 575
- 安装内核、模块及相关文件 . . . . . . . . . . 582
- GRUB：Linux 引导加载程序 . . . . . . . . . . . 583
- dmesg：显示内核消息 . . . . . . . . . . . . . . . . . . 589

安装 Ubuntu Linux 后，你可能希望重新配置并构建一个新的 Linux 内核。Ubuntu Linux 附带一个预构建的内核，简化了安装过程。然而，该内核可能并未针对所有系统功能进行适当配置。通过配置和构建新内核，你可以创建一个针对特定系统及其独特需求定制的内核。定制的内核通常比通用内核更小。

有时你并不需要构建新内核。相反，你可以动态更改许多过去需要重新构建内核才能修改的设置。实现这些更改的两种方法是使用 `boot` 命令行参数（第 82 页）或修改 `/etc/sysctl.conf`（`sysctl` 在系统启动时使用该文件，见第 572 页）。

你可以将在引导命令线上使用的相同参数添加到 `/etc/default/grub` 中的 `GRUB_CMDLINE_LINUX_DEFAULT` 变量中。例如，`acpi=off` 可以防止 `acpid`（高级配置和电源接口守护进程）启动。更多信息请参见第 82 页。

`sysctl` 实用工具在系统运行时修改内核参数。该实用工具利用了 `/proc/sys` 的功能，后者定义了 `sysctl` 可以修改的参数。

命令 `sysctl -a` 显示 `sysctl` 参数的完整列表。以下示例展示了显示和更改 `domainname` 内核参数的过程。在本示例中引号不是必需的，但你必须为否则会被 shell 解释的任何字符加上引号。

```bash
$ /sbin/sysctl kernel.domainname
kernel.domainname = tcorp.com
$ sudo /sbin/sysctl -w kernel.domainname="example.com"
kernel.domainname = example.com
$ /sbin/sysctl kernel.domainname
kernel.domainname = example.com
```

## 在构建新内核时请备妥安装 CD/DVD

在构建新的 Linux 内核以安装新版本或修改现有版本配置时，请确保手边有安装 CD/DVD。即使系统软件被完全破坏，这张光盘也能让你重新引导系统。备用这张 CD/DVD 可能是暂时恐慌与全面精神崩溃之间的区别。

在开始构建新内核之前，你必须下载、安装并清理源代码。你还需要构建一个描述你想要构建的新内核的配置文件。本章描述了完成这些任务所涉及的步骤。

## 先决条件

安装以下软件包：

- `linux-source`（最新发布的 Ubuntu 内核源代码；如果使用 `git` 下载代码则不需要）尝试安装 `linux-source` 时会显示包含最新内核的软件包名称，然后你安装该软件包；参见下一节。
- `build-essential`（元软件包；包含编译代码所需的软件包）
- `fakeroot`, `kernel-package`（内核专用）
- `git-core`（使用 `git` 下载内核源代码）
- `ncurses-dev`（使用 `make menuconfig` 配置内核）
- `libglade2-dev`（使用 `make gconfig` 配置内核）
- `module-assistant`, `debhelper`（用于创建模块）

### 编译内核需要大量磁盘空间

**提示** 在编译内核前请确保你有足够的磁盘空间。一旦编译默认内核，它会占用大约 3.5 GB 的空间。这些磁盘空间必须在你编译内核所在的文件系统中可用。

### 下载内核源代码

本节描述了在本地系统上下载内核源代码的两种方法：`aptitude`（或 Synaptic，第 133 页）和 `git`。如果你希望下载未被 Ubuntu 定制（打补丁）的代码，请访问 kernel.org 或参见关于 git 的部分。

#### aptitude：下载和安装内核源代码

下载并安装 Ubuntu 内核最近发布版本的更新内核源代码最简单的方法是使用 `aptitude`。以下命令确保软件包索引是最新的并下载 linux-source 软件包。`dpkg postinst` 脚本将压缩的源代码放置在 `/usr/src/linux-source*` 中：

```bash
$ sudo aptitude update
...
$ sudo aptitude install linux-source
...
The following NEW packages will be installed:
  linux-source linux-source-2.6.32{a}
...
$ ls -l /usr/src/linux-source*
-rw-r---- 1 root root 65726108 2010-04-09 18:23 /usr/src/linux-source-2.6.32.tar.bz2
```

由于 `/usr/src` 与 `src` 组关联，如果你是该组的成员（第 492 页），你可以在 `/usr/src` 目录中提取和构建内核。否则，你可以在任何你有写权限的目录中解包内核。

#### 不要使用 root 权限操作

**注意** 在配置或构建内核的任何部分，除了安装（最后一步）外，你不需要也不应该以具有 `root` 权限的用户身份操作。内核 `README` 文件说：“切勿徒有虚名地提及 root。” 只要你是 `src` 组的成员，你就可以在 `/usr/src` 下的目录中下载、配置和编译内核，而无需使用 `root` 权限。

你可以使用 `usermod` 将用户添加到 `src` 组。以下命令将 Max 添加到 `src` 组，以便他可以在 `/usr/src` 中工作。Max 必须注销并重新登录，以使系统识别他为 `src` 组的成员。

```bash
$ sudo usermod --append --groups src max
```

如果你不在 `/usr/src` 目录下工作，你必须将 `linux-source*` 文件复制到当前工作目录；否则，请切换到 `/usr/src`。使用 `tar` 命令解包 Linux 源代码文件：

```bash
$ tar -xjf linux-source-2.6.32.tar.bz2
```

## git：获取最新的内核源代码

`git` 工具（GNU 交互式工具，git-scm.com）可以下载多个不同内核的最新版本源代码，并保持这些源代码为最新状态。如果尚未安装，请执行以下命令来安装 `git`：

```bash
$ sudo aptitude install git-core
```

### 安装 git-core 软件包，而不是 git 软件包

> 请确保安装 `git-core` 软件包，而不是 `git` 软件包。`git` 软件包对于下载内核源代码没有帮助。
