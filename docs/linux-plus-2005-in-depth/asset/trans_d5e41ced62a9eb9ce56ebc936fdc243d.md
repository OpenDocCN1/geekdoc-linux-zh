

FIPS 可以从互联网上的 <http://www.iog.fhg.de/~achafel/fips/> 下载。你应该阅读随程序提供的 FIPS.doc 文件，并满足其中概述的要求。使用 FIPS 调整 Windows 分区大小所需步骤的一个示例列表如下：

- 1. 从要调整大小的 Windows 分区中删除任何旧的、不需要的、未使用的或不必要的文件，以腾出最大空间供 Linux 使用。
- 2. 使用诸如 DEFRAG 之类的磁盘碎片整理程序对要调整大小的 Windows 分区进行碎片整理。
- 3. 确保 Windows 分区上有足够的空闲空间来安装 Linux。
- 4. 运行程序以检查硬盘的完整性，并使用诸如 CHKDSK 或 SCANDISK 之类的程序识别任何坏扇区。备份 Windows 分区上的所有数据，以防 FIPS 过程中发生故障。
- 5. 获取或创建一个 DOS 或 Windows 9x 启动盘。将文件 FIPS.exe、ERRORS.txt 和 RESTORRB.exe 复制到启动盘上。
- 6. 使用上一步创建的启动盘启动系统。在 DOS 提示符下，输入 “fips” 以调用 FIPS 程序。
- 7. 在确定了有多少空闲空间后，FIPS 显示建议的分区划分。调整分区划分以符合所需的硬盘空间划分比例。在你指示 FIPS 可以分割分区后，它会提供创建硬盘上 MBR 的备份副本，扩展名为 .000。你将来可以使用 RESTORRB.exe 恢复此 MBR 备份副本。
- 8. FIPS 将原始 Windows 分区缩小，并从上一步原始 Windows 分区上的空闲空间创建一个新的分区。
- 9. 在原始 Windows 分区上运行 SCANDISK，以确保没有错误。
- 10. 运行 Linux 安装程序；当提示分区时，你可以安全地删除 FIPS 创建的第二个分区，并用 Linux 分区替换它。

如果 FIPS 过程成功完成，在使用 Windows 操作系统时可能存在的一个区别是：Windows 操作系统分配给驱动器（如 CD-ROM）的驱动器字母可能会改变，因为硬盘上现在有不同的分区结构。

## 使用 Windows 引导加载程序双启动 Linux

你可以选择使用 Windows 引导加载程序来加载 Linux 操作系统；只需在 Windows 引导加载程序配置中指定 GRUB 或 LILO 的位置即可。类似于 LILO 和 GRUB，随 Windows NT、Windows 2000、Windows XP 和 Windows Server 2003 提供的 NTLDR 引导加载程序可以在启动时显示一个屏幕，提示用户选择要启动的操作系统。因此，如果与 Linux 双启动的操作系统是 Windows NT、Windows 2000、Windows XP 或 Windows Server 2003，你可以使用 Windows NTLDR 引导加载程序来加载 LILO 或 GRUB。

你必须确保首先安装 Windows NT、Windows 2000、Windows XP 或 Windows Server 2003 并将其放置在系统的第一主活动分区上；NTLDR 引导加载程序默认放置在硬盘的 MBR 上。接下来，你可以安装 Linux 并指定 GRUB 安装在分区的第一扇区，而不是 MBR 上，如图 9-7 所示；否则，GRUB 将覆盖硬盘 MBR 上的 NTLDR。

![](img/09bf13b782f71165e17bb3839040c96a_359_0.png)

**图 9-7 配置 GRUB 驻留在 Linux 分区上**

Linux 成功安装后，再次使用第一张 Red Hat Fedora CD-ROM 启动你的电脑。在欢迎屏幕上，在启动提示符处输入 `linux rescue` 并按下 Enter。接下来，在“选择语言和键盘类型”屏幕上点击“确定”，在“设置网络”屏幕上选择“否”，并在“救援”屏幕上选择“继续”。当提示位于硬盘上的 Linux 安装系统的 root 文件系统已挂载到 `/mnt/sysimage` 时，点击“确定”，你将获得一个命令提示符。

接下来，你创建一个目录来挂载软盘（`mkdir /mnt/floppy`），在软驱中放入一个格式化为 FAT 文件系统的软盘，并挂载你的软盘（`mount -t vfat /dev/fd0 /mnt/floppy`）。

然后，你可以创建 GRUB 的可启动映像文件。假设 GRUB 安装到 / 分区（`dev/hda2`）的第一扇区，要在软盘设备上创建名为 `inboot.bin` 的 dev/hda2 第一扇区映像，你可以在命令提示符下执行以下命令：

```bash
[root@server1 root]# cd /mnt/floppy
[root@server1 floppy]# dd if=/dev/hda2 bs=512 count=1 of=linboot.bin
1+0 records in
1+0 records out
[root@server1 floppy]# cd
[root@server1 root]# umount /mnt/floppy
[root@server1 root]# _
```

成功创建映像后，你可以通过在命令提示符下输入 `exit` 来重启电脑并启动到 Windows 操作系统。将 linboot.bin 文件复制到 C:\，并配置 NTLDR 配置文件（C:\\boot.ini）以包含一个可用于启动它的部分。下面是一个示例 `boot.ini` 文件：

```ini
[boot loader]
    timeout=30
    default=multi(0)disk(0)rdisk(0)partition(1)WINDOWS
[operating systems]
    multi(0)disk(0)rdisk(0)partition(1)WINDOWS="Microsoft Windows XP Professional" /fastdetect
```

上述 boot.ini 文件在 30 秒内（timeout=30）从第一个 IDE 硬盘控制器（multi(0)）上的第一块硬盘（disk(0)）上的第一个分区（partition(1)）启动默认的、标签为 "Microsoft Windows XP Professional" 的 Windows 操作系统。

要让 NTLDR 启动 Linux 操作系统，你必须指定之前创建的 linboot.bin 文件的路径，并指定要在 NTLDR 启动屏幕上显示的标签：

```ini
[boot loader]
    timeout=30
    default=multi(0)disk(0)rdisk(0)partition(1)WINDOWS
[operating systems]
    multi(0)disk(0)rdisk(0)partition(1)WINDOWS="Microsoft Windows XP Professional" /fastdetect
    C:\\linboot.bin="Red Hat Fedora Core 2"
```

当系统重启时，NTLDR 引导加载程序加载并显示一个操作系统列表供选择，其中包括 Linux，如图 9–8 所示。

> **注意**
> 安装后，如果你需要，可以将 LILO 安装到分区的第一扇区而不是 GRUB，并重新创建一个 NTLDR 可以使用的 linboot.bin 文件。

![](img/09bf13b782f71165e17bb3839040c96a_361_0.png)

## Linux 初始化

回想一下，当引导加载程序将 Linux 操作系统内核加载到内存后，内核恢复控制权并执行系统中第一个名为 init 的守护进程。init 守护进程随后使用其配置文件 /etc/inittab（init 表）来加载系统中提供系统服务的其他守护进程，最终允许用户登录并使用系统。此外，init 守护进程还负责在系统停止或重启时卸载加载到内存中的守护进程。

### 运行级别

因为在典型的 Linux 系统上，init 守护进程可能需要管理多个守护进程，所以 init 守护进程将系统划分为运行级别。运行级别定义了在一个特定系统上加载到内存中并由内核执行的守护进程的数量和类型。在任何时候，Linux 系统可能处于七个标准运行级别中的任何一个；这些运行级别在表 9-3 中定义。

| 运行级别 | 通用名称 | 描述 |
| :--- | :--- | :--- |
| 0 | 关机 | 一个内存中没有活动守护进程的系统，准备断电。 |
| 1, s, S, 单用户 | 单用户模式 | 一个只有足够守护进程的系统，允许一个用户登录并执行系统维护任务。进入单用户模式时，用户会自动以 root 用户身份登录系统。 |
| 2 | 多用户模式 | 一个启动了大多数守护进程的系统，允许多个用户登录并使用系统服务。在此运行级别中，除专门网络服务外，大多数常见网络服务也可用。 |
| 3 | 扩展多用户模式 | 具有与多用户模式相同功能的系统，但启动了所有额外的网络服务（例如，SNMP、NFS）。 |
| 4 | 未使用 | 通常不使用，但可以根据你的需求进行自定义。 |
| 5 | 图形模式 | 具有与扩展多用户模式相同功能的系统，但在 tty7 上启动了名为 GNOME 显示管理器（gdm）的图形登录程序，允许进行图形登录。 |
| 6 | 重启 | 一个用于重启系统的特殊运行级别。 |

![](img/09bf13b782f71165e17bb3839040c96a_362_0.png)

> **注意**
> 由于 init 守护进程负责启动和停止守护进程，从而更改运行级别，因此运行级别通常被称为 **init 状态**。

要查看系统的当前运行级别和以前的运行级别（如果系统启动以来运行级别已更改），你可以使用 **runlevel 命令**，如下面的输出所示：

```bash
[root@server1 root]# runlevel
N 5
[root@server1 root]# _
```

上述 runlevel 命令表明系统处于运行级别 5，并且进入此运行级别之前最近的运行级别是不存在的（N）。要在正在运行的系统上更改运行级别，你只需指定 **init 命令** 后跟新的运行级别；要从运行级别 5 更改为运行级别 1 以执行系统维护任务，你可以使用以下命令：

