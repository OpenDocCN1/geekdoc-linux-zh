
08/30/00  06:40    <DIR>               sv

08/30/00  06:40        14 File(s)    5,431,781 bytes

                                              0 free

TEAM Ling - 现场、信息丰富、免费且正版！

## 定制和升级 Linux

### 第 2

从 `\dosutils` 目录运行 `rawrite` 实用程序并将 `boot.img` 文件传输到软盘上：

```
G:\dosutils\rewrite

Enter disk image source file: boot.img

Enter target diskette drive: a:

Please insert a formatted diskette drive into A: and press -ENTER-: <CR>
```

结果将是一个可启动的软盘，其中包含以下文件，你可以使用它来启动系统并启动安装过程：

```
Volume in drive A LINUX BOOT

Volume Serial Number is 2410-07EF

Directory of A:\

08/30/00 06:39 5,860 LDLINUX.SYS

08/30/00 06:39 425 SYSLINUX.CFG

08/30/00 06:39 4,807 TEM.IMG

08/30/00 06:39 789,543 INITRD.IMG

08/30/00 06:39 600,265 VMLINUZ

08/30/00 06:39 751 BOOT.IMG

08/30/00 06:39 655 EXPER.MSG

08/30/00 06:39 859 GENERAL.MSG

08/30/00 06:39 860 PARAM.MSG

08/30/00 06:39 500 RESCUE.MSG

08/30/00 06:39 545 SNAKE.MSG

11 File(s) 1,405,074 bytes

49,964 bytes free
```

## 从 UNIX 系统创建安装启动盘

在基于 UNIX 的环境中，你可以使用 `dd` 工具创建软盘。首先，你需要挂载 CD-ROM 以进入 `images` 目录，`boot.img` 文件就在那里。`dd` 工具是一个 UNIX 实用，因此它不在 CD 上。

将 CD 放入 CD-ROM 驱动器，挂载 CD-ROM 并列出 `images` 目录的内容。你需要的启动文件是 `boot.img`。你的 `images` 目录列表可能不完全相同，但应该与以下所示。当你运行 `dd` 时，将提供 `boot.img` 文件作为参数传输到启动盘。请按照以下指令从 UNIX 系统创建启动磁盘：

TEAM LinG - 现场、信息丰富、免费且正版！

## 从 CD-ROM 安装 Linux

### 第 1

将 Red Hat CD 放入 CD-ROM 驱动器。切换到 `/images` 目录并列出内容：

```
08/30/00  06:40    <DIR>               .

08/30/00  06:44    <DIR>               .

08/30/00  06:48                    485 TRANS.TBL

08/30/00  06:39            1,474,560 boot.img

08/30/00  06:39            1,474,560 bootnet.img

08/30/00  06:40    <DIR>               de

08/30/00  06:40            860,110 drivers.img

08/30/00  06:40    <DIR>               es

08/30/00  06:40    <DIR>               fr

08/30/00  06:40    <DIR>               it

08/30/00  06:39            147,456 paride.img

08/30/00  06:39            1,474,560 pcmcia.img

08/30/00  06:40    <DIR>               pxeboot

08/30/00  06:40    <DIR>               sv

08/30/00  06:40        14 File(s)    5,431,781 bytes

                                              0 free
```

Red Hat CD 放入 CD-ROM 驱动器。切换到 `/images` 目录并列出内容：

```
08/30/00 06:40 Red Hat Linux_7.0 (i)

login:

08/30/00 06:40 Jun 7 11:48:36

password:

08/30/00 06:40 mount /dev/hdc

08/30/00 06:40 mount /dev/cdrom

08/30/00 06:40 mount /mnt/cdrom

08/30/00 06:40 cd /mnt/cdrom

08/30/00 06:40 ls -l

total 63

-drwxr-xr-x 2 root root 4096 Jun 30 .

-drwxr-xr-x 2 root root 4096 Jun 30 ..

-rw-r--r-- 1 root root 485 Jun 30

-rw-r--r-- 1 root root 1474560 Jun 30

-rw-r--r-- 1 root root 1474560 Jun 30

-drwxr-xr-x 2 root root 4096 Jun 30 de

-rw-r--r-- 1 root root 860110 Jun 30

-drwxr-xr-x 2 root root 4096 Jun 30 es

... (省略部分以保持简洁)

-rw-r--r-- 1 root root 4096 Jun 30 sv
```

### 第 2

切换到 `/mnt/cdrom` 目录并列出内容以确认 `boot.img` 存在：

```
-drwxr-xr-x 2 root root 4096 Jun 30 .

-drwxr-xr-x 2 root root 4096 Jun 30 ..

-rw-r--r-- 1 root root 485 Jun 30

-rw-r--r-- 1 root root 1474560 Jun 30

-rw-r--r-- 1 root root 1474560 Jun 30

-drwxr-xr-x 2 root root 4096 Jun 30 de

-rw-r--r-- 1 root root 860110 Jun 30

-drwxr-xr-x 2 root root 4096 Jun 30 es

...

-drwxr-xr-x 2 root root 4096 Jun 30 sv
```

TEAM Ling - 现场、信息丰富、免费且正版！

### 第 2

切换到 `/mnt/cdrom` 目录并列出内容以确认 `boot.img` 存在：

```
-drwxr-xr-x 2 root root 4096 Jun 30 .

-drwxr-xr-x 2 root root 4096 Jun 30 ..

-rw-r--r-- 1 root root 485 Jun 30

-rw-r--r-- 1 root root 1474560 Jun 30

-rw-r--r-- 1 root root 1474560 Jun 30

-drwxr-xr-x 2 root root 4096 Jun 30 de

-rw-r--r-- 1 root root 860110 Jun 30

-drwxr-xr-x 2 root root 4096 Jun 30 es

...

-drwxr-xr-x 2 root root 4096 Jun 30 sv
```

### 第 3

使用 `dd` 工具将 `boot.img` 文件传输到软盘：

```
[root@HostA images]# dd if=boot.img of=/dev/fd0

2880+0 records in

2880+0 records out
```

结果将是一个可启动的软盘，其中包含以下文件，你可以使用它来启动系统并启动安装过程。请注意，尽管我们使用了 `dd` 工具，但文件与 `rawrite` 创建的文件是相同的：

```
[root@HostA /root]# mount /dev/floppy

[root@HostA /root]# cd /mnt/floppy

[root@HostA floppy]# ls -l
```

## 定制与升级 Linux

插入您的 CD-ROM 并启动系统。如果启动过程中遇到困难，请阅读以下段落。如果系统启动没有问题，请继续执行第 1 。

## 在 IDE 系统上安装 Linux

在本节中，Linux 将安装在具有集成驱动器电子（IDE）架构的系统上。IDE 是一种 IBM PC 行业标准架构（ISA）。它通常比 SCSI 便宜，且配置更简单。我们为您绘制了硬盘配置图，供您研究分区和挂载点数据（图 3.1）。

需要连接到互联网的网络连接；因此，我们准备了一些 IP 地址。

## 启动问题判定

有时，Linux 似乎无法识别或从 IDE CD-ROM 启动。如果出现这种情况，您应该尝试确定 Linux 无法看到 IDE 设备的原因。可能是由于 BIOS 的局限性，导致它无法识别或读取 IDE 通道。如果系统之前在不同的操作系统下运行正常，那么很可能就是这种情况。解决方案是升级 BIOS 或创建一个软盘启动盘。我们建议您创建一个软盘启动盘，因为这样更容易。另一个可能是可能是系统配置不正确。如果您利用机会添加或移动了系统中的驱动器，通常会发生这种情况。检查所有驱动器和设备上的主/从跳线。如果驱动器串联在同一个 IDE 控制器上，则一个设备应配置为为主设备（master），另一个设备应为从设备设备（slave）。您需要查找 IDE 设备的文档以找到如何安排跳线，因为这些说明书因设备而异。

| 欢迎使用 Red Hat Linux 7.1！ |
| :--- |
| 在图形模式下安装或升级 Red Hat Linux，请按 <ENTER> 键 |
| 在文本模式下安装或升级 Red Hat Linux，输入：text <ENTER> |
| 要启用低分辨率模式，输入：lowers <ENTER>。 |
| 按 <F2> 获取有关低分辨率模式的信息。 |
| 要禁用帧缓冲区（framebuffer）模式，输入：nofb <ENTER>。 |
| 按 <F2> 获取有关禁用帧缓冲区模式的信息。 |
| 要启用专家模式，输入：expert <ENTER>。 |
| 按 <F3> 获取有关专家模式的信息。 |
| 要启用救援模式，输入：linux rescue <ENTER>。 |
| 按 <F5> 获取有关救援模式的信息。 |
| 如果您有驱动器盘，输入：linux dd <ENTER> |
| 使用下列出的功能键获取更多信息。 |
| [F1-主] [F2-通用] [F3-专家] [F4-内核] [F5-救援] |

图 3.1 IDE 磁盘配置。

另一个更有趣的问题是安装后 CD-ROM 不会自动加载。为了让系统正常运行，您可以在启动序列期间的 LILO 提示符处输入以下语句：

```
boot: linuxdx=cdrom
```

x 是 Linux 为驱动器指定的 IDE 字母。此字母取决于驱动器连接的 IDE 总线。这种情况下也可能在启动期间给您带来一些问题。请记下它，如果系统在安装后仍然无法启动，请重新检查您的布线和主/从配置。

## IDE 安装的故障排除

如果您在安装过程中遇到困难，请停止并研究您正在进行的操作。根据我们的经验，大多数问题涉及硬盘配置或硬件兼容性，其次是网卡和糟糕的驱动程序配置。

关于这个问题，通常是因为缺少关于跳线或终端设置（termination settings）的文档。如果您有一对 IDE 驱动器或一个硬盘加 CD-ROM 组合，通常是主/从配置问题。如果是正确的，请确保所有 IDE 设备之间相互兼容。换句话说，不要将旧的 IDE 技术与较新的增强型 IDE 技术混用。如果它们能协同工作，那么您很幸运。我们行业内有一句说法：“我们是运气好还是很聪明？”

网卡和驱动程序的组合也可能产生麻烦。我们认为，在过去的两年里，这个领域取得了巨大的进展。三年前，Linux 支持的网卡非常少——而现在有很多。较新的网卡是 PCI 的，因此是自配置的。当它工作正常时，太棒了。当然，这在您的系统中运行得成功完全取决于您安装的 BIOS。如果 BIOS 存在漏洞或过旧，那么这种情况可能会非常困难。不要忽略我们在第 1 章中告诉您的 DOS 实用程序。在检查网卡使用的 IRQ、I/O 端口和内存地址空间行为（无论是否为 PCI）之前，不要在不工作的网卡上花费大量时间。

注意以下糟糕的情况。您可以在系统内部固定网卡，但它不会响应 DHCP 服务器。这种情况通常是资源冲突，通常是内存空间。要检查这些问题，直接进入 `/proc` 目录并列出所有名为 `iomem`、`ioports`、`irq` 和 `net` 的文件内容。如果网络在这些文件中不存在，那么 `irq` 可能被设置为已被其他设备占用。如果您无法在内部固定网卡，那么驱动程序可能无法正常工作。如果网卡背部没有指示灯，那么可能是网卡本身的问题。我们建议不要在一个不工作的网卡上花费太多时间，直接去买一个。我买的最后一个 DLink 网卡不到 20 美元。您的时间比这值。可以通过 `driversguide.com` 找到很多驱动程序。

视频配置也是大问题——大到我们专门用了一个章节。请参考该章节。

## 逐步安装

我们的屏幕并不一定反映您系统上的实际情况。然而，它们将让您对安装所需的信息有一个良好的了解。我们将解释默认行为以及选择特定选项的理由。我们的目的是让您在执行操作时能够做出明智的决策。

### 第 1 步启动消息

如果您在第一个屏幕上不选择任何内容离开，安装程序将自动启动并默认到 GUI 安装模式。我们专门演示使用文本模式。

- 欢迎使用 Red Hat Linux 7.1！
- 在图形模式下安装或升级 Red Hat Linux。这是默认选项，它将启动 GUI 安装面板。请注意，此选择的视频失败率很高，因为它无法正确解释显卡和显示器。如果您选择此选项并失败，我们建议您立即重启并使用文本选项。
- 在文本模式下安装或升级 Red Hat Linux。出于实际考虑并为了方便大多数无图形系统的安装，请使用此选项。只是提醒一下——所有目标服务器的系统将具有图形支持。
- 启用专家模式。此选项不适合胆小的人，但有时是必要的——例如，当自动探测似乎无法正确发现您的设置时。这些对话框允许您为所有显卡设置（如 IRQ、I/O 和 DMA）提供必要信息。
- 启用救援模式。此功能允许您从 CD-ROM 启动系统。如果系统无法启动且您没有救援盘，此选项是最后的手段。如果您跳过了这一步，可以在安装完成后创建救援盘。

# 46 Linux 的定制与升级

安装过程中的一个步骤。要创建安装后救援盘，请进入 `/lib/modules` 目录并使用以下命令为您的系统创建一个定制的救援盘：

```bash
#cd /lib/modules
#mkbootdisk --device /dev/fd0 kernel_number
```

`kernel_number` 的格式为 `2.4.2-2`。当您选择想要安装的内核时，您将根据您当前运行的内核级别插入相应的版本号。您应该始终手头准备一个针对每个系统特定的救援盘。例如，使用内核级别为 `2.2.14-5` 的系统的救援盘来救援一个本应为内核级别为 `2.4.2-2` 的系统被认为是一种不良实践。任何系统的当前内核级别都可以通过观察登录提示符或使用 `uname -a` 命令和系统提示符来确定。

您还可以通过 Red Hat CD 创建救援盘，进入 `/images` 目录并执行以下命令：

```bash
G:\
G:\cd images
G:\>dd if=rescue.img of=/dev/fd0 bs=1440 count=1
```
