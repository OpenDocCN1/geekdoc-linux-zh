
图 B-3 显示了在 Windows 桌面的 QEMU 窗口中显示的 Small Linux 示例：

图 B-3 使用 QEMU 在 Windows XP 中测试 linux。

# 附录 B 构建、测试和刻录 ISO

## 使用 VMware 测试 ISO 镜像

`VMware Player` (`www.vmware.com/products/player`) 是一款流行的工具，你可以用它代替 QEMU 在电脑桌面上测试 ISO 镜像。该播放器免费下载，允许你启动虚拟机并在窗口中运行一个完全独立的操作系统。由于它可以在 Windows、Linux 和其他基于 PC 的系统中运行，因此你无需重启即可测试 ISO 镜像。

你可以从 `www.vmware.com/download/player` 下载 VMware Player。由于 VMware Player 不是开源软件，因此无法与 Linux 发行版一起发布。让它运行起来可能有点复杂。对于 Fedora Core，我使用了描述让其工作：`http://www.vmware.com/go/2006/livecd-player-virtual-machine.html`。在 VMware 运行后，下一个技巧是在虚拟机中播放 CD。来自 VMware.com 的任何一个小软件都可以帮助你将 livecd iso 复制到某个目录，通过在解压 `Generic-LiveCD-Virtual-Machine` 后，可以从该目录启动：

```
vmplayer Generic-LiveCD-Virtual-Machine.vmx
```

如果你切换到另一个现场 CD（将新的一个复制为 iso），请确保将 VMware 偏好（`Player → Preferences`）设置为在关闭时关闭虚拟机。否则，关闭旧 CD 将仅仅是挂起，因此下次启动 VMware 时它会重新打开。图 B-4 显示了我使用上述 VMware 软件在播放器窗口中运行制作的现场 CD 的启动屏幕。

## 使用 cdrecord 或 K3b 刻录 ISO 镜像

当你完成一个 ISO 镜像后，可以使用许多 Linux 和 Windows 工具将该 ISO 镜像刻录到 CD 或 DVD。本节介绍了每个主流 Linux 发行版都提供的两种流行的 CD 和 DVD 刻录工具：`cdrecord` 和 `K3b`。

### 使用 cdrecord 刻录 CD 和 DVD

`cdrecord` 命令是一个易用工具，你可以用它将镜像刻录到 CD 或 DVD。通过支持 ATA 数据包接口 (`ATA Packet Interface`)，`cdrecord` 可以与 IDE 驱动器工作，使用 ATAPI 标准。图 B-4 使用 VMware Player 在 Windows 上启动 CD。

`cdrecord` 命令是一个易用工具，你可以用它将镜像刻录到 CD 或 DVD。每个 Linux 发行版（包括 Red Hat Linux 和 SuSE）都包含 `cdrecord`。

使用默认设置（在 `/etc/cdrecord.conf` 中），默认驱动器是 `/dev/cdrom`。如果你的 ISO 镜像在当前目录并命名为 `livecd.iso`，你需要向驱动器插入一张空白 CD 并执行以下：

```
cdrecord livecd.iso
```

在上述示例中，当 `cdrecord` 完成，你可以弹出 CD 或 DVD。如果这不起作用，或者你想对过程有更多控制，可以使用许多选项。

在继续之前，你可以通过多种方式获取可写驱动器的信息。如果你有多个 CD 或 DVD 驱动器，可能需要指定你想写入的是哪一个。可以使用设备名称（例如 `/dev/cdrom`）来指示驱动器。要确定可写 CD 和 DVD 的设备名称，可以使用如下 `scanbus` 选项：

```
cdrecord -scanbus
```

```
cdrecord-clone 2.01 (i686-linux-gnu)
Copyright (C) 1995-2004 Jörg Schilling
scsideo: 'ATA'
devname: 'ATA'
scsibus: target 2 lun: 2
Linux sg version: 3.5.27
Using libscg version '0.8'.
scsibus:
0,0 100 'LITE-ON DVDRW SOHW-1633S' Removable CD-ROM
1,1 101
1,2 102
1,3 103
1,4 104
1,5 105
1,6 106
1,7 107
```

在此示例中，只发现了一个 CD/DVD 刻录机，其 SCSI 地址为 1,0,0。这意味着 SCSI 总线 1、目标 0 和 LUN 0。因此使用 `dev=` 选项，可以在 `cdrecord` 命令行上将其标识为 `dev=1,0,0` 或 `dev=/cdrom`。

当没有速度选项时，`cdrecord` 会尝试使用它检测到的适用于该驱动器和介质的最大速度。有时这个值可能是不正确的，或者你可能会遇到写入错误并想自行更改速度。

已正确检测；你可能需要手动设置最大写入速度。要将速度设置为最低值，请使用 `speed=0`。

`cdrecord` 命令的其他常用选项包括详细输出 (`-v`) 和退出选项 (`-eject`)。如果你不熟悉正在使用的驱动器，可以使用 `-dummy` 选项进行测试。使用带有 `-dummy` 的 `cdrecord` 会执行 `cdrecord` 命令行上请求的所有动作，但不会启动激光，也不会意外刻录光盘。这个命令行示例包含了你描述的几个选项：

```
# cdrecord dev=/dev/cdrom1 speed=4 -eject -dummy mylivecd.iso
```

在刚刚的示例中，`cdrecord` 使用了第二个 CD 驱动器 (`/dev/cdrom1`) 和 4 倍速度（即音频速度的四倍）。随着记录的进行，将显示详细输出。当整个镜像刻录到 CD/DVD 后，光盘会自动退出。

你可以选择几种写入模式。1997 年之后的大多数驱动器都符合多媒体命令集 2 (`MMC-2`) 规范，因此它们应该至少支持所述的写入模式之一。请考虑以下示例：

> 在后文提到的情况下，如果你在开始刻录之前需要知道每个轨道的精确大小，可以在使用 `mkisofs` 命令创建 ISO 镜像时确定该大小。添加 `-print-size` 选项即可产生你需要的信息。

- `-sao` 一次会话（Session At Once）模式仅对支持此模式的 MMC 驱动器可用。要使用此模式，`cdrecord` 必须知道每个轨道的精确大小。这种模式有时被称为磁盘一次写入（Disk At Once，你可以使用 `-dao` 代替 `-sao`）。
- `-tao` 轨道一次写入（Track Once）模式是 `cdrecord` 的默认模式。如果你正在多次刻录，则需要此模式。
- `-raw` 某些固件不良的 CD 刻录机无法在 `-sao` 或 `-tao` 模式下工作。在这些情况下，你可能需要使用 `-raw` 写入模式。当指定 `-raw` 时，默认认为 `-raw96`。`-raw96` 模式使用 2448 字节扇区（由 2352 字节扇区和 96 字节原始 P-W 子通道数据组成）。其他原始方法包括 `-raw16`（2368 字节扇区大小，由 2352 字节扇区加 16 字节 P-Q 子通道数据组成）和 `-raw96p`（与 -raw9r 大小相同，仅用于少数 CD 刻录机）。在想要以原始模式写入时，大多数情况下应使用 `-raw96r` 或 `-raw16`。

如果你在使用可重写 CD 介质（这在反复测试 live CD 时是个好主意），可以使用 `cdrecord` 的 `blank` 选项来擦除你的 CD 重刻录。要擦空整块磁盘，请使用 `blank=all`、`blank=disc` 或 `blank=disk`。若要用更快速但不彻底的方法擦除磁盘，可以使用 `blank=fast` 或 `blank=minimal` 擦除 PMA、TOC 和 prepag。以下是完全擦除与 `/dev/cdrom` 关联磁盘的命令示例：

```
# cdrecord dev=/dev/cdrom blank=all
```
