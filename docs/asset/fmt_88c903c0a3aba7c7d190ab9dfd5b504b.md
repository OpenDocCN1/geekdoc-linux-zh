
- 可选的 DeltaRPM 支持，通过 Presto（YUM 的增强功能）更新软件包，只需下载包中已修改的部分而不是整个包，从而显著减少下载量。安装 `yum-presto` 启用。YUM 的 Presto 插件 (PackageKit) 将使用 delta RPM 包代替完全替换。DeltaRPM 包要小得多，仅包含更改的数据，用于在你的系统上生成更新后的包版本，然后只需下载更新包中更改的数据。

- 可选的 Presto 支持，YUM 的增强功能通过通过下载包中已修改的部分而不是整个包来更新软件包，显著减少下载量。安装 `yum-presto` 启用。

- 默认虚拟网络客户端是 TigerVNC。

- 红色图形启动 (RHGB) 已被 Plymouth 取代，这是一种更精简、高效的快速图形启动，不需要 X 服务器支持。它依赖内核的内核模式设置 (KMS) 特性，该特性为基础图形提供直接支持。通过直接渲染管理器，可以使用各种图形。KMS 目前为 ATI 和 Intel 显卡提供支持。Nvidia 通常不支持 KMS，但使用 Nouveau 驱动可以启用支持。

http://fedaproject.org/wiki/Features/BetterStartup

- FirstAidKit 自动化工具恢复常见问题的操作。该工具具有易于添加的插件组件。FirstAidKit 旨在从救援 CD/DVD（安装 DVD）或 Live CD 在救援模式下运行，发现问题并建议修复该问题的插件。用户可以选择运行插件来修复问题。

http://fedaproject.org/wiki/Features/FirstAidKit

- 内核模式设置 (KMS) 提供了快速启动、快速用户切换和无缝 X 服务器切换（适用于 ATI 和 Intel 显卡，以及启用 Nouveau 驱动时）。

- 虚拟化支持外部存储访问。虚拟系统现在可以挂载和访问分区、LVM 卷和 SCSI 存储。还提供了直接 PCI 设备访问（图形除外）。

- 使用 sVirt 为虚拟主机支持 SELinux。

- sectool SELinux 工具对系统进行安全审计以检测入侵，包含 sectool 和 sectool-gui 软件包。

- RPM 4.7 基于 RPM 4.6 构建，提供更快的更新和改进的失败更新处理。RPM 4.6 是红帽包管理器 (RPM) 的重大重写。命令和界面保持不变。RPM 4.6 还支持一种新的压缩方法 LZMA (Lempel-Ziv-Markov chain-Algorithm)，用于更快的下载和节省空间。与 YUM 有更好的底层集成。

```
http://rpm.org/wiki/Releases/4.6.0
```

# 第一部分：系统管理

- 支持管理在线账户信息和访问。诸如 Google 这样的在线账户信息可以由 GConf 配合 GNOME Keyring 存储，也可以通过 http://online.gnome.org 提供的在线账户服务进行存储。目前支持在线桌面（针对 Google 和 Twitter），但很快可能会支持其他应用程序。

- MySQL 已升级到 5.0 版本，包含许多更改。

- OpenJDK 6（开源 JAVA）现已安装用于 Java 运行时环境服务。`java-gcj-collect` 集合仍然可用，并提供 Java 运行时环境的兼容性。

## 安装问题 (Anaconda)

- 针对桌面应用设计，现在提供了一种精简平台安装版，适用于空间少于 500MB 的小型安装，仅包含部分应用程序和服务。这为一个更不容易受到攻击的系统提供了一个快速安装方案。

- Anaconda 中的存储管理配置界面和设备已经过重写，以便更好地使用 RAID、LUKS 加密和 LVM 等存储管理设备。使用 `udev` 来检测设备块。

- 从在内存中运行或在 USB 驱动器上运行的 Live 镜像安装。

- 对于 IDE 驱动器，设备名称已废弃，并替换为 `sd`（PPC Fedora 版本除外）。IDE 驱动器不再标记为 `/dev/hdx`，而是作为 `/dev/sd`。

- Fedora 使用 `dmraid` 模块支持大多数主板 RAID 控制器。如果你的主板 RAID 不受支持，你可以使用 Linux 软件 RAID。

- 如果你的电脑有多个网络接口（NIC 或 PXE），它可能不会将 `eth0` 分配给第一个接口（请阅发布说明）。

- 所有硬盘（包括 SATA 和 IDE）每块磁盘限制为 15 个分区（SCSI 设备规范），而不是 63 个（IDE 设备规范）。如果您的硬盘有超过 15 个分区，您应该将其迁移到 LVM 卷。

- 在安装过程中，通过 `ntfs-3g` 实现了 NTFS 支持。系统上的 NTFS 分区将被自动检测，并监控 `/media` 目录下的子目录。子目录名称将使用分区标签或磁盘名称。

- 修订后的文本模式安装程序。

## 升级问题

- 设备标记用于使用直接硬盘分区（而非 LVM）升级系统。内核现在处理 `hdev` 和 `sdx` 设备的方式与之前的版本不同。安装过程通过通过标签而非设备名称来识别驱动器，绕过了这个问题。这意味着所有驱动器在安装之前都必须标记。如果从之前的 Fedora 版本升级，请确保你的硬盘分区已全部标记。如果没有，请在升级前对其进行标记。除非所有磁盘都已标记，否则升级无法进行。

# 第一章：Fedora 11 介绍

- 如果你使用分区（之前 Fedora 安装的默认设置），你的设备已经标记好了。

- 使用以下块 ID 命令检查你的设备是否已经标记。每个设备都应该有一个 `LABEL` 字段：

```
/sbin/blkid
```

- 如果你添加了标签，请确保在 `/etc/fstab` 文件中对应的设备条目也添加该标签。

- 如果必须添加根设备标签，请务必在 `/etc/boot/grub.conf` 的内核行中添加标签条目。通常你的根设备可能已经标记了。默认情况下，之前的安装会为根设备分配标签 `/`。

- 确保通过重启来测试你的更改，确保所有内容都能正确挂载和启动。

- 升级时，务必备份你的 `/home` 和 `/etc` 目录（以及任何自定义包的 `/opt` 和 `/usr/local`）。

## Fedora ISO 镜像

Fedora 磁盘以一系列变体（spins）的形式发布，收集了不同用途的软件。包括桌面、工作站、服务器的标准 DVD 镜像，桌面 Live CD (GNOME Desktop)、Fedora KDE Live CD、Fedora Developer Live CD 以及电子实验室 (FEL) Live CD。普通的 Fedora DVD 变体包含工作站和服务器软件，但不是全集。变体是用 Pungi 创建的，你可以用它来开发自己的自定义变体。你可以在此处找到更多关于变体的信息：https://fedoraaproject.org/wiki/SIGs/Spins，那里也描述了自定义变体。

**Fedora Test Live CD：** Fedora GNOME 桌面 Live CD，适用于 i386 和 x86_64 版本。

**Fedora KDE Live CD：** KDE 桌面 Live CD，适用于 i386 和 x86_64 版本。

**Fedora 安装 DVD：** 包含更完整的软件选择的安装 DVD，适用于 i386 和 x86_64 版本。

### Fedora 自定义变体

自定义变体也可用，可以在 Fedora Projects Tracker 下载这些种子文件。

**Fedora Live Games 变体：** 可用的 Fedora 游戏变体。

**Fedora FEL 变体：** 电子实验室变体。

**Fedora Live Edu 变体：** 教育变体。

**Fedora BrOffice 变体：** 带有 OpenOffice 的巴西葡萄语变体。

**Fedora AOS 变体：** 用于构建虚拟设备的 JeOS 变体。

### Fedora XF 桌面变体：采用轻量级 XFCE 桌面，而非 GNOME 或 KDE。

### Fedora 特殊变体

此外还有几个特殊变体仍在开发中，目前已有版本。它们位于。这些包括 Omega 和 Sugar 变体。

**Omega：** 带有 RPM Fusion 完整多媒体解码器的变体（可以直接从 10 升级到 Fedora 11）。位于：

```
ftp.fedoraaproject.org
```

**Sugar：** 针对儿童的教育变体。

### 多媒体

包含了广泛的多媒体应用程序，例如视频播放器和电视查看，支持来自 http://rpmfusion.org 的各种多媒体程序和库。

关于热插设备的信息通过来自 freedktop.org 的硬件抽象层 (HAL) 提供给应用程序。这允许 GNOME 应用程序轻松地显示和管理移动设备。

### Fedora 标准功能

这里列了一些标准功能：

- 本版本包含 Thunderbird 邮件客户端。

- FreeIPA 使用 Web 界面集成审核、身份和策略管理。
