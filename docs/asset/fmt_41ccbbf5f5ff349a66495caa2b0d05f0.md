
现在是时候在你的计算机上安装 TurboLinux 了。本章将向你展示如何使用多种安装选项来安装 TurboLinux。如果你在阅读本章时正在进行安装，你将会在结束时能够进入 TurboLinux——好运保佑。如果你拥有标准的 PC 硬件，你至少应该有一个可以运行的 TurboLinux 版本。在随后的章节中，你将学习如何配置 TurboLinux 与非必需硬件（如扫描仪、打印机等）协同工作。让我们开始吧！

- 选择你的安装方法
- 安装前预热
- 开始安装
- 重启

> **提示**：如果你正在安装 TurboLinux，我能给你的最佳建议是花点时间，按照书中列出的要求做好必要的准备，并仔细阅读说明。不要盲目点击“确定”按钮。

## 选择你的安装方法

本节涵盖了你可以安装 TurboLinux 的方法。

### 启动 TurboLinux CD

最简的安装方法之一是直接从 TurboLinux CD-ROM 启动。如果你的硬件支持，书中附带的 Linux CD-ROM 和标准的 TurboLinux set 都是可启动的。大多数 PC 都支持从 CD-ROM 驱动器启动。如果你计算机上已经有了现有的操作系统，你需要确保 PC 在检查硬盘以查找可启动磁盘之前先检查 CD-ROM。你可以通过查看 BIOS 设置来检查这一点。

通常情况下，你可以在启动过程中按 F2、Delete 或空格键来检查 BIOS 设置。当计算机启动时，寻找屏幕上显示要按哪个键来编辑 BIOS 设置的提示。如果这是你的安装选择，你只需要将光盘放入 CD-ROM 驱动器并启动计算机。TurboLinux 安装程序将启动。你可以跳过本节的其余部分，直接进入“安装前预热”部分。如果你在启动期间无法从 CD-ROM 启动，且你拥有有一个可以识别 CD-ROM 驱动器的操作系统，请以 DOS 模式启动并 `cd` 到 CD-ROM 驱动器。切换到 `dosutils` 目录并运行 `boot` 命令。如果不起无效，请在下一节创建 TurboLinux 软盘。

## 从软盘启动

如果你选择的是从 CD-ROM 启动以外的方法，你需要创建启动软盘。这些启动软盘会加载 Linux 内核和访问你硬件所需的驱动程序——安装程序会自动启动。根据你的硬件和安装方法，你需要创建一到四张软盘。创建启动软盘非常简单。在 CD-ROM 上有一个目录，包含了软盘的原始磁盘镜像。大多数操作系统都有一个将原始磁盘镜像拷贝到软盘的工具。TurboLinux CD-ROM 附带了一个适用于 DOS 和 Windows 9 的名为 `rewrite` 的工具。

## 选择磁盘镜像

如果你选择的是从 CD-ROM 启动以外的方法，你需要创建启动软盘。这些启动软盘会加载 Linux 内核和访问你硬件所需的驱动程序——安装程序会自动启动。根据你的硬件和安装方法，你需要创建一到四张软盘。

根据你的计算机系统及其组件，你需要创建一个或多个安装软盘。你至少需要创建 `boot.img` 启动磁盘。`boot.img` 包含了大多数以太网和 SCSI 适配器的驱动程序。你可能还需要 `extrawh.img` 硬件磁盘，它包含了其他以太网、SCSI 和 PCMCIA 设备的支持。如果你需要从 FTP 服务器或 Windows 网络安装 TurboLinux，必须使用辅助磁盘 `supp.img`。如果你有一个并行端口 IDE CD-ROM 需要安装，你需要从 `extra2.img` 创建软盘。由于软盘很便宜，你应该考虑至少创建 `boot.img`、`extrawh.img` 和 `supp.img`。

## 如何写入磁盘镜像

以下指令告诉你如何使用随 TurboLinux CD-ROM 提供的 `rewrite` 工具创建镜像。在 CD-ROM 的 `dosutils` 目录中有四个批处理文件：`mkboot.bat`、`mkehw.bat`、`mke2.bat` 和 `mksupp.bat`。这些批处理文件分别创建 boot、extrahw、extra2 和 supp 磁盘。如果由于原因批处理文件无效，或者你需要从提供的镜像创建额外的软盘，可以使用下面的指令。

在 DOS、Windows 3.1 和 Windows 9x 中，你可以使用名为 `rewrite` 的命令行程序。按照以下步骤使用 `rewrite` 工具：

1. 将 TurboLinux CD-ROM 放入你的 CD-ROM 驱动器。
2. 切换到 CD-ROM 镜像目录，如果 F: 是你的 CD-ROM 驱动器：

```
F: cd images
```
3. 运行带有 TurboLinux CD-ROM 程序：

```
..\dosutils\rewrite
```
4. 输入要写入软盘的磁盘镜像，例如 `boot.img`。
5. 输入软盘驱动器，例如 A：

如果你使用的是 Windows NT，你需要使用兼容的工具。你可以考虑 `winimage`，`http://www.winimage.com`。

如果你已经在某个版本的 Linux，可以使用 `dd` 命令行工具：

1. 将 TurboLinux CD-ROM 放入你的 CD-ROM 驱动器并挂载它。
2. 切换到 CD-ROM 驱动器的镜像目录（例如 `/mnt/cdrom/images`）。
3. 输入 `dd if=<disk image> of=/dev/<floppy device>`，其中 `<disk image>` 是你想写入软盘的镜像。由于这是数据的原始写入，不要挂载软盘驱动器，`dd` 将直接写入设备。例如：

```
dd if=boot.img of=/dev/fd0
```
4. 等待 `dd` 命令完成且软盘驱动器指示熄灭。在此弹出软盘。

## 从 CD-ROM 安装

如果由于某种原因，你无法从 TurboLinux 安装 CD-ROM 启动，则必须从软盘启动。启动后，你应该能够将你的 CD-ROM 驱动器指定为安装介质。请确保你的 TurboLinux CD-ROM 已插入驱动器中。

## 从本地硬盘安装

如果你在硬盘上有 TurboLinux 安装文件，可以指定指向顶级目录的完整路径。顶级目录包含 `MDSUMUMS` 校验和文件以及 TurboLinux 主目录等其他文件和目录。该顶级目录应该与你从 TurboLinux 网站下载或从 CD-ROM 复制的 TurboLinux 发行版本镜像。由于你的硬盘尚未挂载，你必须指定硬盘路径。如果你在另一个操作系统中将 TurboLinux 下载到 `C:\TurboLinux` 下，那么在导入时安装目录时，我建议提供 `/dev/hd1/TurboLinux` 作为 TurboLinux 安装目录的完整路径。

> 你可以下载最新的 TurboLinux 工作站：`ftp://ftp.turbolinux.com/pub/turbolinux`。你还可以从同一个 `pub` 目录获取服务器版本、源码、更新和配套的 CD-ROM 镜像。

## 从 FTP 服务器安装

如果你有直接的网络连接，则可以通过网络或 Internet 从 FTP 服务器安装 TurboLinux。如果你可以访问 Internet，可以直接从 TurboLinux 的 FTP 站点安装 TurboLinux。你必须拥有计算机的相应网络信息，例如 IP 地址、子网掩码和网关 IP 地址。

有关网络属性的更多信息，请参阅第 17 章“网络（Networking）”。

如果你选择 FTP 安装方法，你需要额外的软盘以及指向 FTP 服务器的 URL——例如 `ftp://ftp.turbolinux.com/pub/turbolinux`。

> 你无法使用 PPP 或其他串行调制解调器进行 FTP 安装。你必须拥有直接的网络连接。

## 从 NFS 文件系统安装

如果你的计算机连接到局域网（LAN），且网络上还有另一台机器导出了 TurboLinux 的 NFS 导出目录，你可能可以使用 NFS 选项进行安装。与 FTP 安装选项类似，你需要为计算机提供 TCP/IP 设置，以及适当的 NFS 服务器和 NFS 挂载点。你可以从网络管理员或 NFS 服务器的负责人员处获取这些信息。

## 安装前的准备工作

你已经准备好安装 TurboLinux 了。那么，开始你需要什么呢？

- 安装工作表（Installation worksheet）
- 一台准备好安装 TurboLinux 的计算机
- TurboLinux 发行版的安装介质或网络位置
- 本书
