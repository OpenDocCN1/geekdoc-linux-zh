
然后重命名目录，例如重命名为“CD1”：

```
earth:/ # mv /suse-share/cdrom /suse-share/CD1
```

对其他光盘重复此过程。然后通过 NFS 导出 `/suse-share` 目录。更多信息请参见第 371 页的“NFS — Shared File Systems”。

## 为网络安装启动

将启动介质插入驱动器。启动盘的创建方法请参见第 21 页的“在 DOS 中创建启动盘”和第 22 页的“在 UNIX 类型系统中创建启动盘”。几短时间后将出现启动菜单。选择“Manual Installation”（手动安装）。你可以指定额外的内核参数。按 Enter 键确认选择。内核将加载，系统会提示你插入第一个模块磁盘。

过了一会儿后，`linuxrc` 将出现并要求你输入若干参数：

1. 在 `linuxrc` 中选择语言和键盘布局。
2. 选择“Kernel modules (hardware drivers)”（内核模块（硬件驱动程序））。
3. 加载系统所需的 IDE、RAID 或 SCSI 驱动程序。
4. 选择“Load network card modules”（加载网卡模块）并加载所需的网卡驱动程序（例如 `eepro100`）。
5. 选择“Load file system driver”（加载文件系统驱动程序）并加载所需的驱动程序（例如 `reinsfs`）。
6. 选择“Back”（返回）然后“Start installation / system”（开始安装 / 系统）。
7. 选择“Start installation/update”（开始安装/更新）。
8. 选择“Network”（网络）然后选择网络协议（例如 NFS）。
9. 选择要使用的网卡。
10. 指定 IP 地址和其他网络信息。
11. 指定提供安装数据的 NFS 服务器的 IP 地址。
12. 输入 NFS 共享的路径（例如 `/suse-share/CD1`）。

现在 `linuxrc` 将从网络源加载安装环境并启动 `YaST2`。按照《用户指南 (2003)》“Installation”（安装）章节中的描述继续安装。

### 故障排除

- 安装在实际启动之前已终止。“另一台”机器的安装目录没有以 exec 权限导出。请现在执行此操作。
- 服务器不识别要安装 SuSE Linux 的主机。在服务器的 `/etc/hosts` 文件中输入要安装主机的名称和 IP 地址。

## 提示与技巧

### 在 DOS 中创建启动盘

此操作需要一个经过格式化的 3.5 英寸软盘和一个可启动的 3.5 英寸软盘驱动器。

### 附加信息

CD 1 上的 `boot` 目录包含许多磁盘镜像。可以在适当工具的帮助下将镜像复制到磁盘。通过这种方式准备的软盘称为启动盘。

这些磁盘镜像还包括“loader”（加载器）、SYLINUX 和程序 `linuxrc`。SYLINUX 允许在启动过程中选择所需的内核，并在必要时为所使用的硬件指定参数。`linuxrc` 程序支持为你的硬件加载内核模块并随后启动安装。

#### 步骤

DOS 应用程序 `rawwrite.exe`（CD 1，目录 `\dosutils\rawwrite`）用于生成 SuSE 启动盘和模块磁盘。此操作需要一台运行 DOS（例如 FreeDOS）或 Windows 的机器。

以下描述的步骤适用于 Windows 环境：

1. 插入 SuSE Linux CD 1。
2. 打开 DOS 窗口（在开始菜单的“应用程序” ->“MS-DOS Prompt”下）。
3. 通过为 CD 驱动器提供正确的路径名称启动 `rawwrite.exe` 应用程序。以下示例在 Windows 目录下的 C 盘上进行，你的 CD 驱动器是 D:

```
C:\Windows> >dosutils\rawwrite
```

4. 启动程序后，它将提示你输入复制的文件源和目的地。启动盘镜像存储在 CD 1 的 `\boot` 目录下。文件简单命名为 `bootdisk`。记得包含 CD 的路径。

```
C:\Windows> d:\dosutils\rawwrite
```

```
RaWrite 1.2 -- Write disk file to raw floppy diskette
```

Enter source file name: d:\boot\bootdisk

Enter destination drive: a:
```

输入目标驱动器 `a:` 后，根据要求插入已格式化的磁盘，然后按 J。`rawwrite` 然后将显示复制进度。此过程可以通过 `Ctrl + C` 终止。

## 在 UNIX 类型系统中创建启动盘

这需要一个带有 CD-ROM 驱动器的 Unix 或 Linux 系统以及一个格式化的磁盘。

创建启动盘：

1. 如果需要，先格式化磁盘：
```
earth:~ # fdformat /dev/fd0
```
2. 挂载 CD 1，例如到 `/media/cdrom`：
```
earth:~ # mount -tiso960 /dev/cdrom/media/cdrom
```
3. 进入 CD 上的 `boot` 目录：
```
earth:~ # cd /media/cdrom/boot
```
4. 使用以下命令创建启动盘：
```
earth:~ # dd if=/media/cdrom/boot/bootdisk of=/dev/fd0 bs=8k
```

`boot` 目录中的 `README` 文件提供了有关软盘的详细信息。通过这种方法也可以创建其他镜像。如果你在安装期间需要 USB 或 SCSI 设备或 PCMCIA 卡，就需要这些镜像。如果你想启动文件系统，可能需要模块磁盘。

如果你要在安装期间使用自行编译的内核，过程会稍微复杂。在这种情况下，首先将默认镜像（`bootdisk`）写入软盘，然后用自己的内核覆盖实际内核（`linux`）（编译内核见第 262 页）：

```
earth:~ # dd if=/media/cdrom/boot/bootdisk of=/dev/fd0 bs=8k

earth:~ # mount -t msdos /dev/fd0 /mnt

earth:~ # cp /usr/src/linux/arch/i386/boot/vmlinux /mnt/linux

earth:~ # umount /mnt
```
