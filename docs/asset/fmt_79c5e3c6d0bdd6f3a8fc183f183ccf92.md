
![](img/110fa0d6324f0893fff03cee6394144d_73_0.png)

2. 接下来，选择你的语言：

![](img/110fa0d6324f0893fff03cee6394144d_74_0.png)

图 2.16 – 安装语言

3. 选择语言后点击“继续”。接下来，你应该看到安装摘要部分：

# 安装摘要

# ORACLE LINUX 8.7 安装

## 本地化

## 软件

## 系统

- 键盘
English (US)
- 安装源
设置基 存储库出错
- 安装目标
自动分区选择
- 语言支持
English (United States)
- 软件选择
未设置安装源
- KDUMP
Kdump 已启用
- 时间和日期
America/New York 时区
- 网络和主机名
未连接
- 安全性策略
未选择配置文件

## 用户设置

- Root 密码 
Root 账户已禁用。

> 请在继续下一步之前完成带有此图标标记的项目。

![](img/110fa0d6324f0893fff03cee6394144d_75_0.png)

现在，我们需要完成两个任务：

- 启用网络
- 将安装源设置为 Oracle 的 yum 仓库

要启用网络，点击 `Network & Host Name` 选项。

4. 在这里，你需要开启以太网并用服务器名称更新主机名。这将在后续步骤中显示。如果你是从 ISO 或 USB 安装，跳过

## 网络和主机名

# ORACLE LINUX 8.7 安装

![](img/110fa0d6324f0893fff03cee6394144d_76_0.png)

有线 (enp3)
已连接
速度 1000 Mbps
IP 地址
DHCP
主机名：localhost

以及网域。当你启用网络时，系统将自动获取 DHCP 信息。如果你想手动配置此项，请点击“配置...”（`Configure...`）：

![](img/110fa0d6324f0893fff03cee6394144d_80_0.png)

图 2.22 - 访问手动网络设置

2. 这将带你进入网络详情，你可以在那里手动设置 MTU、IP 地址和其他网卡（NIC）特定设置。如果需要，你还可以禁用 IPv6。

![](img/110fa0d6324f0893fff03cee6394144d_81_0.png)

3. 网络设置完成后，你可以使用 NTP 服务器等网络资源来同步时钟。要执行此操作，在“时间与日期”（`TIME & DATE`）下，点击齿轮图标：

## 时间与日期

# ORACLE LINUX 8.7 安装

完成 (`Done`)

帮助！(`Help!`)

区域：美洲 城市：纽约

网络时间：开启 (`Network Time ON`)

![](img/110fa0d6324f0893fff03cee6394144d_82_0.png)

21:28

24小时制 AM/PM

01 / 03 / 2023

> [!IMPORTANT]
> 你没有配置可用的 NTP 服务器

图 2.24 – 访问 NTP 设置

- 4. 接着，你可以添加 NTP 服务器。默认使用公共服务器，但如果你运行了本地 NTP 服务器，请确保在此处添加这些服务器。

| 添加并标记为使用的 NTP 服务器 |
|---|---|---|---|
| 主机名 (Host Name) | 池 (Pool) | 正常 (Working) | 使用 (Use) |
| 2.poolntp.org | [x] | [x] | [x] |

图 2.25 – NTP 设置

- 5. 接下来，根据需要在“安装源”（Installation Source）下添加额外的软件源。这在之前进行网络安装时已经完成。

你还可以设置安装哪些 RPM 组以及任何额外的软件。这在“软件选择”（`SOFTWARE SELECTION`）下进行：

![](img/110fa0d6324f0893fff03cee6394144d_83_0.png)

6. 设置好基础环境（Base Environment）并添加任何额外软件后，下一个任务是设置安装目标。这通过点击“安装目标”（Installation Destination）完成。

在这里，你应该能看到系统可用的物理和逻辑驱动器。默认是将存储配置设置为“自动”（`Automatic`），但让我们通过选择自定义配置（`custom configuration`）来探索不同的启动磁盘结构。一旦选择了“自定义”（`Custom`），点击“完成”（`Done`）按钮。

## 安装目标

# ORACLE LINUX 8.7 安装

完成 (`Done`)

美国 (US)

帮助！(`Help!`)

## 设备选择 (Device Selection)

选择你想要安装的设备（s）。在你点击主菜单上的“开始安装”（`Begin Installation`）按钮之前，它们将保持不变。

## 本地标准磁盘 (Local Standard Disks)

100 GIB
ATA VBOX 虚拟硬盘
sda / 100 GIB 空闲

![](img/110fa0d6324f0893fff03cee6394144d_84_0.png)

此处未选中的磁盘将不会被触碰。

## 特殊与网络磁盘 (Specialized & Network Disks)

![](img/110fa0d6324f0893fff03cee6394144d_84_1.png)

此处未选中的磁盘将不会被触碰。

## 存储配置 (Storage Configuration)

- 自动 (`Automatic`)
- 自定义 (`Custom`)

全磁盘摘要和引导程序...

已选择 1 个磁盘：100 GIB 容量：100 GIB 空闲 刷新... (`Refresh...`)

> 图 2.27 – 安装目标

7. 从这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

## 手动分区 (MANUAL PARTITIONING)

# ORACLE LINUX 8.7 安装

完成 (`Done`)

...（此处内容）

图 2.28 – 手动分区

- 8. 在这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

## 手动分区 (MANUAL PARTITIONING)

# ORACLE LINUX 8.7 安装

完成 (`Done`)

...（此处内容）

图 2.29 – Btrfs

- 9. 在这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

## 手动分区 (MANUAL PARTITIONING)

# ORACLE LINUX 8.7 安装

完成 (`Done`)

...（此处内容）

图 2.30 – 应用策略

- 10. 在这里，你可以选择默认的卷管理策略，也可以手动创建新布局。大多数系统将使用 LVM。

图 2.31 – 应用策略

| Option Name | firewall |
| --- | --- |
| Description | 用于配置已安装系统上的防火墙。 |
| Options | - 必须使用 `--enabled` 或 `-enable`。启用或禁用防火墙。<br>- 必须使用 `--disabled` 或 `-disable`。如果禁用，则不配置 iptables 规则。<br>- `--trust` 设置受信任的网络设备，允许所有流量通过防火墙。若要配置多个设备，请让每个设备作为一个独立的条目，且之间不加逗号，例如 `-trust eth0 -trust eth8`。<br><br>- `--incoming` 添加以下每个标记，用以允许这些常用服务的入站流量：
  - `-ssh`
  - `-smtp`
  - `-http`
  - `-ftp`<br>- `--port=` 指定用于访问服务器的端口。您可以使用 /etc/service 中的端口来指定特定的端口:协议组合。多个端口可以用逗号分隔。例如 ldap:tcp, 1521:tcp。<br>- `--service=` 提供了一种启用特定服务的简便方法，例如 CUPS 服务，或需要打开多个 UDP/TCP 端口的服务。这允许您以可读的格式轻松地打开这些端口。<br>- `--use-system-defaults` 不配置防火墙。如果指定了其他选项，它们将被忽略。 |

| Option Name | firstboot |
| --- | --- |
| Description | 此选项可以在系统启动时禁用设置程序的运行。请确保您已安装了 `initial-setup.rpm`（如果需要 GUI，则安装 `initial-setup-gui.rpm`）。此选项默认禁用。 |
| Options | - `--enable` 或 `-enabled` 在系统首次启动时启动设置程序。<br>- `--disable` 或 `-disabled` 在系统首次启动时不启动设置程序。<br>- `--reconfig` 允许设置在启动时以重配置模式启动。这允许在设置默认选项外，设置网络配置、root 密码、时区、语言、鼠标和键盘选项。 |

| Option Name | graphical |
| --- | --- |
| Description | 如果未设置，图形 命令为默认值。安装将以全图形化方式继续。 |
| Options | `--non-interactive` 在完全非交互模式下执行安装。此模式在需要用户交互时将终止安装。 |
| Option Name | group |
|| --- | --- |
| Description | 此选项在系统上创建一个用户组。 |
| Options | - `--name=` 是必须的，用于设置组名。<br>- `--gid=` 是可选参数，将设置组的 GID。 |
| Option Name | halt |
| --- | --- |
| Description | 如果使用，系统将在安装完成后 halt（停止）。在未设置其他方法的情况下，这是默认的完成方法。其他完成方法包括 poweroff（关机）、reboot（重启）和 shutdown（关闭）。 |
| Options | 无 |
| Option Name | logging |
| --- | --- |
| Description | 这对于排查 PXE 安装有用。它控制安装程序在安装期间的日志。它不会配置被安装系统的日志。 |
| Options | - `--host=` 日志发送到的 syslog 主机。<br>- `--port=` 远程 syslog主机上用于使用的端口。如果未设置，则使用默认端口 (UDP 514)。 |

- `--level=` 指定发送到设备 tty3 的消息最小级别。无论该级别如何，所有消息都会发送到日志主机和文件。有效值为 critical, debug, error, info 和 warning。

| Syntax | logging [--host=host] [--port=port] [--level=critical|debug|error|info] |

| Option Name | poweroff |
| --- | --- |
| Description | 使用时，安装完成后将系统执行关机并断电。 |
| Options | 无 |

| Option Name | reboot |
| --- | --- |
| Description | 安装完成后重启系统。 |
| Options | `--eject` 在重启之前弹出启动介质（DVD、USB 等）。 |

| Option Name | repo |
| --- | --- |
| Description | 启用额外的 DNF/YUM 源。每个仓库需要单独的一行。 |
| Options | `--name=` 分配并设置仓库名称和 URL。如果名称与现有仓库冲突，则将被忽略。格式为 `--name=repo [--baseurl=url|--mirrorlist=url|--metalink=url] [options]`。可以将额外的选项添加到 URL 中。作为警告，仓库文件中不支持使用变量。但是，您可以使用 `$releasever` 和 `$basearch`：

- `--baseurl`: 仓库的 URL
- `--mirrorlist`: 仓库的镜像列表
- `--metalink`: 带有 metalink 的仓库 URL

- `--proxy=[protocol://][username[:password]@host[:port]` 设置仓库的代理。
- `--noverifys` 禁用 HTTPS 服务器的验证。 |

| Option Name | selinux |
| --- | --- |
| Description | 用于配置 selinux 的初始策略和状态。默认策略为 enforcing。 |
| Options | - `--enforcing` 将 selinux 策略设置为 enforcing。这是默认设置。<br>- `--permissive` 将 selinux 策略设置为 permissive。这允许警告输出到控制台 syslog，但不执行策略。<br>- `--disabled` 禁用 selinux。 |
| Option Name | shutdown |
| --- | --- |
| Description 在安装完成后对系统执行 shutdown 命令。 |
| Options | |

| Option Name | keykey |
| --- | --- |
| Description | 这是带有 metalink 的仓库 URL。 |
| Options | |

| Option Name | config |
| --- | --- |
| Description | 允许设置在启动时以重配置模式启动。这允许在设置默认选项外，设置网络配置、root 密码、时区、语言、鼠标和键盘选项。 |
| Options | |

| Option Name | text |
| --- | --- |
| Description | 如果未设置，图形 命令为默认值。安装将以全图形化方式继续。 |
| Options | `--non-interactive` 在完全非交互模式下执行安装。此模式在需要用户交互时将终止安装。 |
| Option Name | url |
| --- | --- |
| Description | 使用时，安装完成后将系统执行关机并断电。 |
| Options | |

Linux 内核版本以源代码的形式分发，而基于 Linux 的各种发行版或操作系统通常会打包并分发它们自己的内核版本，并将其整合到各自的发布版本中。此外，想要直接在系统中编译并安装内核的用户可以访问这些源代码。下表显示了 Linux 7、8 和 9 的 Linux 主线发布版本。

| OS 版本 | RHCK 发布版本 | 最新 UEK 版本 |
| :--- | :--- | :--- |
| Linux 7 | Linux 3.x | UEK 6/Linux 5.4 |
| Linux 8 | Linux 4.x | UEK 7/Linux 5.15 |
| Linux 9 | Linux 5.14 | UEK 7/Linux 5.15 |

表 3.1 – 按发布版本提供的内核选项

# 内核基础 – UEK 和 RHCK

在全新安装 Oracle Linux 后，默认使用“不可破坏企业内核”（Unbreakable Enterprise Kernel，UEK）。但是，在某些情况下，你可能希望切换到红帽兼容内核（RHCK）。

在某些场景下，默认内核可能不是使用的正确版本：

- UEK 发布版本基于比 RHCK 版本更新的内核，后者是 Red Hat 服务器的标准。在 Oracle Linux 中，你可以选择使用 UEK，它提供了更更新的内核。
- 当前内核版本可能与你的特定硬件不兼容。UEK 系统可以在新硬件上启动，而旧的 RHCK 则不能。一个例子是 UEK 7，它支持 Microsoft Azure 网络适配器 (MANA)，而 UEK 6 则不支持。
- 假设系统安装了 UEK Beta 版或初步发布版。在这种情况下，需要监控 UEK，以确保只有在管理员有意且手动选择内核时才使用该内核。
- 用于 Linux 的 UEK 提供了许多优势，例如显著的性能提升和新功能。Linux 操作系统是一个模块化系统，内核与硬件交互，并代表应用程序控制资源访问调度。大多数应用程序运行在所谓的用户空间中，只有一组稳定的系统库会请求内核服务。例外是直接访问内核的应用程序，最常见安全应用程序。
- 安装 UEK 不会更改 glibc 等系统库，glibc 是几乎所有应用程序（包括 Oracle Database）都使用的接口。无论你运行带有 UEK 还是带有 RHCK 的 Oracle Linux，glibc 版本都是相同的。这不仅限于 glibc，也适用于 libssl、libc 和 libcrypt 等所有系统库。

## 注意

对于任何基线操作系统，可能都有多个版本的 UEK。UEK 版本的选择取决于应用程序团队，并且必须反映任何兼容性要求。

这些示例和类似的情况要求你在内核类型之间切换。在旧版本中，管理默认内核是通过配置 GRUB 引导加载程序完成的。然而，从 Oracle Linux 8 及更高版本开始，你应该使用 `grubby` 命令来控制和管理内核启动配置。`grubby` 是 GNU 项目提供的第 2 版本引导加载程序 (`GRUB 2`) 的一部分。`GRUB` 是市场上许多 Linux 发行版的默认引导加载程序。将其加载到内存后，它会将控制权交给运行的内核。

`GRUB 2` 是 Oracle Linux 上使用的默认引导加载程序，它可以加载许多不同的操作系统，包括 Microsoft Windows。

## 准备工作

让我们开始深入研究该过程以更好地理解它。

## 启动过程

你已经了解 Oracle Linux 启动选项如何帮助你排查系统启动时遇到的问题。在使用新硬件或云环境时，这些知识非常有益。

当 Oracle Linux 系统启动时，它会执行许多任务，这些任务取决于你的硬件用于处理系统启动的固件类型。它可能是统一扩展固件接口 (`UEFI`) 固件，或传统的 BIOS 固件。传统的基本输入输出系统 (`BIOS`) 固件是遗留的。`BIOS` 固件维护了可启动设备列表。系统中的互补氧化物半导体 (`CMOS`) 芯片存储了设置，当系统上电时，`BIOS` 启动过程使用 `UEFI` 固件来尝试加载的可启动设备。使用 `BIOS` 固件的系统。`UEFI` 启动过程是遗留的，尽管现代系统可能仍然使用 `BIOS` 启动，内核在 `UEFI` 固件上交互。`UEFI` 固件管理的是一个包含 `.efi` 文件的引导程序。`EFI` 系统分区 (`ESP`) 包含了可作为 `EFI` 应用程序。使用 `.efi` 文件可以对内核进行更多控制，这可以利用新的安全特性。一个新安全特性是安全启动（Secure Boot），将在本章中介绍。

## UEFI 启动序列

`UEFI` 硬件使用的以下启动序列：

1. 系统首先执行引导自检 (`POST`)，识别所有可能的启动设备。
2. `UEFI` 根据全局唯一标识 (`GUID`) 搜索 `GUID` 分区表 (`GPT`)，以确定 `ESP`。通过 `efibootmgr` 工具，可以在不使用默认情况下指定不同的顺序。
3. 启动管理器检查是否启用了安全启动。如果没有启用安全启动，启动管理器请求 `ESP` 上的 `GRUB 2` 加载器。否则，启动管理器请求引导程序的证书并对其进行验证。引导器将内核加载到内存中并创建一个临时的内存文件系统（`tmpfs`）。这将用于提取 `initramfs` 镜像的内容。`vmlinuz` 是可启动压缩 Linux 内核的名称。嵌入 Linux 内核并在启动早期加载的根文件被称为 `initramfs`。
4. 驱动模块从 `initramfs` 文件系统加载。这些模块对于访问根文件是必要的。
5. 系统从第一个进程 `systemd` 开始启动。
6. `systemd` 运行运行定义的任何其他进程。

## Legacy BIOS 序列

传统的 `BIOS` 硬件使用以下序列：

1. 系统首先执行引导自检 (`POST`)，识别系统配置、测试内存并识别所有可能的启动设备。
2. 一旦 `BIOS` 识别出启动设备，它就会读取设备的第一个扇区，即主引导记录 (`MBR`)。`MBR` 包含了引导加载器，这是一个负责加载操作系统的微程序。`MBR` 读取分区表以确定启动分区。此外，`MBR` 还包含指向引导加载器 `GRUB 2` 的指针。`GRUB` 可以在安装 `GRUB` 的设备或独立设备上运行。这对于在同一系统上同时启动 Linux 和 Windows 有帮助。
3. 引导加载器将 `vmlinux` 内核加载到内存中并创建一个临时的内存文件系统（`tmpfs`）。这将用于提取 `initramfs` 镜像的内容。
4. 驱动模块从 `initramfs` 文件系统加载。
5. 内核启动 `systemd` 进程。

## 如何操作...

既然我们已经讨论了基础知识，我们可以跳过所有无聊的部分，直接开始实操。
是时候边玩边学了！

我们可以做的第一件事之一是禁用系统中当前加载的内核。
以下命令将显示我们的 Linux 系统中安装并配置的所有内核（请以 root 身份运行）：

```
