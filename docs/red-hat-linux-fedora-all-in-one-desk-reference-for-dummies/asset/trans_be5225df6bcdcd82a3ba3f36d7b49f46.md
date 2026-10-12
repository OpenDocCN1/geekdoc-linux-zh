
对于这些设备，请查阅 /usr/src/linux*/Documentation/video4linux 目录中的文档。

## 文件系统

通过此类别的选项（见图 6-14），您可以为特定类型的文件系统打开支持。Linux 内核可以支持的文件系统种类之多会令您惊讶。表 6-1 列出了 Linux 可以支持的一些文件系统。您通常会构建一个内核，支持核心 Linux 文件系统（ext2 和 ext3）、CD-ROM 文件系统（ISO 9660 和 Joliet）以及 DOS/Windows 文件系统（MSDOS、FAT 和 VFAT）。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_536_0.png)

图 6-14：从此配置窗口打开特定文件系统的支持。

表 6-1 Linux 内核支持的一些文件系统

| 文件系统 | 描述 |
|---|---|
| Apple Macintosh | Macintosh HFS 文件系统（Linux 可以读取和写入 Macintosh 格式的软盘和硬盘）。 |
| Coda | 一种高级网络文件系统，与 NFS 类似，但更好地支持断开操作（例如笔记本电脑），并且具有更好的安全模型。 |
| Ext2 | 第二代扩展文件系统——Linux 当前的标准文件系统。 |
| Ext3 | 支持日志功能的 Ext2 文件系统——一种设施，可在崩溃后快速恢复磁盘。 |
| FAT | 指任何基于文件分配表（FAT）的文件系统（包括 MS-DOS 和 Windows 95 VFAT 文件系统）。 |
| HPFS | OS/2 HPFS 文件系统（Linux 只能读取 HPFS 文件）。 |
| ISO 9660 | CD-ROM 上使用的标准 ISO 9660 文件系统（这也被称为 High Sierra 文件系统，在某些 UNIX 工作站上称为 hsfs）。 |
| Joliet | Microsoft 对 ISO 9660 CD-ROM 文件系统的 Joliet 扩展，允许使用 Unicode 格式的长文件名。（Unicode 是新的 16 位字符代码，可以编码世界上几乎所有语言的字符。） |
| MSDOS | MS-DOS 文件系统。 |
| NFS | 用于在网络上共享其他系统上的文件和目录的网络文件系统。 |
| NTFS | NT 文件系统（NTFS）——Microsoft Windows NT 使用的文件系统（Linux 只能读取 NTFS 磁盘）。 |
| /proc | 一个虚拟文件系统，可通过它获取有关内核的信息。/proc 文件系统不存在于磁盘上；文件在访问时创建。 |
| ROM | 安装 Red Hat Linux 时在初始 RAM 磁盘（initrd）期间使用的非常小、只读的内存驻留文件系统。 |
| SMB | 使用服务器消息块（SMB）协议访问运行 Windows 95/98/NT/2000 的网络 PC 上的共享目录的文件系统。 |
| System V | SCO、Xenix 和 Coherent 变体 UNIX 在 Intel PC 上使用的文件系统。 |
| UDF | 用于某些 CD-ROM 和 DVD 的新文件系统。（例如，UDF 文件系统用于以数据包模式写入或由 DirectCD 等 UDF 工具写入的可重写 CD。） |
| UFS | BSD（伯克利软件发行版）变体 UNIX（例如 SunOS、FreeBSD、NetBSD 和 NeXTstep）使用的文件系统。 |
| VFAT | 具有长文件名的 Windows 95/98/NT/2000 文件系统。 |

## 声音

使用这组选项配置声卡支持。如果已安装声卡，请先对“声卡支持”选项回答 y 或 m。之后，您必须为 PC 中安装的声卡启用多个选项。您始终可以选择 m 以模块形式构建声音支持，需要时可加载。

## USB 支持

使用此类别的选项（图 6-15）配置通用串行总线（USB）的支持——一种内置于大多数新 PC 中的串行总线。USB 1.1 版本支持高达 12Mbps 的数据传输速率——每秒 1200 万位或每秒 1.5 兆字节——相比之下，标准串行端口（如 COM1）的传输速率为 115Kbps 或 0.115Mbps。您可以在 USB 总线上菊花链连接多达 127 个设备。总线还为设备供电，并且可以在 PC 运行期间连接或移除设备——这种功能通常称为热插拔。USB 2.0 版本（或简称为 USB 2.0 或 USB2）将数据传输速率提高到 480Mbps，略快于竞争的 IEEE 1394（FireWire）总线。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_538_0.png)

图 6-15
通过这些选项配置 USB 支持。

USB 可以取代 PC 的串行和并行端口的功能，以及键盘和鼠标端口的功能。如今，许多 PC 外设——例如鼠标、键盘、打印机、扫描仪、调制解调器、数码相机等——设计为通过 USB 端口连接到 PC。

如果您的 PC 具有 USB 端口，请将 USB 支持选项设置为 y 或 m。然后您必须根据 PC 拥有的 USB 接口类型——UHCI（Intel）或 OHCI（Compaq 等）——对 UHCI 或 OHCI 选项回答 m。要确定 USB 接口的类型，输入 lspci 并在输出中查找 USB 控制器的制造商和型号。如果控制器由 Intel 生产，请使用 UHCI 驱动程序。

对于 USB 2.0 支持，您可以将 EHCI HCD（即主机控制器设备）选项设置为 y 或 m。

在选择 UHCI 或 OHCI 接口支持后，您必须为系统上的特定 USB 设备构建驱动模块。有关 USB 设备的更多信息，请查阅 /usr/src/linux*/Documentation/usb 目录中的文档——尤其是 usb-help.txt 文件中的链接。

## 内核调试

这组选项使您能够使用 SysRq 键（相当于在键盘上按下 Alt+PrintScreen）以在系统崩溃后立即获取重要的状态信息。如果您是期望调试内核的 Linux 开发人员，此信息很有用。大多数用户将这些选项设置为 No（因为大多数用户运行的是稳定的内核版本，并且不期望修复内核错误）。

## 构建内核

配置内核选项后，单击主配置窗口中的“保存并退出”按钮（参见图 6-1）。现在您必须构建内核。这涉及输入三条命令来执行三个任务。

使用单行命令行启动接下来的三个任务（您可以在同一行输入多个用分号分隔的命令），以便您可以输入该行；然后按 Enter，并休息一下。这部分需要一段时间。根据您的系统，制作新内核可能需要几分钟到一个多小时。

在单行输入以下内容以启动该过程：

```
make dep; make clean; make zImage
```

make dep 命令确定哪些文件已更改以及必须重新编译的内容。make clean 命令删除旧的、无用的文件（如旧的内核副本）。最后，make zImage 在名为 zImage 的压缩文件中创建新内核并将其放置在某个目录中。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_539_0.png)

如果您将太多功能链接到内核中（通过对许多配置选项回答 Yes），内核文件大小可能太大，无法在 PC 启动时使用的 640K 内存中容纳。此 640K 限制的存在是因为 Intel x86 处理器以实模式启动，只能访问 1MB 内存，其中 640K 可供程序使用。此限制是旧 MS-DOS 时代的遗留问题，仅在 PC 启动时 Linux 内核初始加载时适用。在这种情况下，make 命令会显示如下错误消息：

```
System is too big. Try using bzImage or modules.
```

如果您收到“System is too big”错误，请输入 make bzImage 以使用可能适合内存限制的另一种类型的压缩内核。否则，请再次进行 make config 步骤，通过为这些配置问题选择 No 来消除不必要的特性。对于您确实需要或可能想尝试的其他功能，请选择 m 以创建模块。虽然内核大小在启动时有限制，但内核在启动过程完成后可以加载所需的任意多个模块。

在构建内核时，您会在屏幕上看到大量消息。全部完成后，/usr/src/linux*/arch/i386/boot 目录中会出现一个名为 zImage 的压缩文件形式的新的内核。

要使用新内核，您必须将内核复制到 /boot 目录下并使用特定名称，并编辑 /etc/grub.conf 文件以设置 GRUB——引导加载程序。但是，在继续进行内核安装之前，您必须构建和安装模块。

## 构建和安装模块

如果在内核配置期间选择了任何模块，您必须构建模块并安装它们。按以下步骤执行这些任务：

- 1. 输入以下命令以构建模块：
  ```
  cd /usr/src/linux*
  make modules
  ```
  目录中当前的一组模块以您系统正在运行的 Linux 内核版本命名。例如，如果您的系统运行内核版本 2.4.20-20.1.2013.nptl，则模块位于以下目录中：
  ```
  /lib/modules/2.4.20-20.1.2013.nptl
  ```
- 2. 按如下方式将模块目录移动到新位置：
  ```
  mv /lib/modules/2.4.20-20.1.2013.nptl
      /lib/modules/2.4.20-20.1.2013.nptl-old
  ```
- 3. 使用以下命令安装新模块：
  ```
  make modules_install
  ```

现在您可以安装内核并使其可供 GRUB 启动。

## 安装新内核并设置 GRUB

Red Hat Linux 使用 GRUB 从磁盘加载 Linux 内核。配置文件 /etc/grub.conf 列出了 GRUB 运行的内核二进制文件。你
