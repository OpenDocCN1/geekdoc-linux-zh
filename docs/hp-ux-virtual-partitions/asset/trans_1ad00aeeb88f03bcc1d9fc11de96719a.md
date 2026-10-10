
接下来是在同一台已运行过 **ioscan** 的 Series 800 上运行 **lsdev** 的示例：

（在 Series 800 上）

```bash
$ /usr/sbin/lsdev
```

| 字符 | 块 | 驱动 | 类 |
| :--- | :--- | :--- | :--- |
| 0 | -1 | cn | pseudo |
| 1 | -1 | asio0 | tty |
| 3 | -1 | mm | pseudo |
| 16 | -1 | ptym | ptym |
| 17 | -1 | ptys | ptys |
| 28 | -1 | diag0 | diag |
| 46 | -1 | netdiag1 | unknown |
| 52 | -1 | lan2 | lan |
| 64 | 64 | lv | lvm |
| 69 | -1 | dev_config | pseudo |
| 72 | -1 | clone | pseudo |
| 73 | -1 | strlog | pseudo |
| 74 | -1 | sad | pseudo |
| 75 | -1 | telm | strtelm |
| 76 | -1 | tels | strtels |
| 77 | -1 | t1ctl1s | pseudo |
| 78 | -1 | t1cots | pseudo |
| 79 | -1 | t1cotsod | pseudo |
| 114 | -1 | ip | pseudo |
| 116 | -1 | echo | pseudo |
| 119 | -1 | dlpi | pseudo |
| 130 | -1 | rawip | pseudo |
| 136 | -1 | 1pr0 | unknown |
| 137 | -1 | udp | pseudo |
| 138 | -1 | stcpgmap | pseudo |
| 139 | -1 | nuls | pseudo |
| 140 | -1 | netga | pseudo |
| 141 | -1 | tun | pseudo |
| 142 | -1 | btlani3 | unknown |
| 143 | -1 | fddil3 | unknown |
| 144 | -1 | fddi0 | unknown |
| 156 | -1 | pttm | strpttm |
| 157 | -1 | ptm | strptys |
| 159 | -1 | ps2 | ps2 |
| 164 | -1 | pipedev | unknown |
| 168 | -1 | beep | graf_pseudo |
| 174 | -1 | framebuffer | graf_pseudo |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | pseudo |
| 193 | -1 | mux2 | tty |
| 203 | -1 | sctl | ctl |
| 205 | -1 | tape | tape |
| 207 | -1 | sy | pseudo |
| 216 | -1 | CentIF | ext_bus |
| 227 | -1 | kept | pseudo |
| 229 | -1 | ite | graf_pseudo |

最后，这里是在同一台已运行过第一个 **ioscan** 的 V-Class 服务器上运行 **lsdev** 的示例：

```bash
$ /usr/sbin/lsdev
                              (在 V-Class 上)
```

| 字符 | 块 | 驱动 | 类 |
| :--- | :--- | :--- | :--- |
| 0 | -1 | cn | pseudo |
| 3 | -1 | mm | pseudo |
| 16 | -1 | pty0m | pty0m |
| 17 | -1 | pty1e | pty1e |
| 27 | -1 | dmem | pseudo |
| 28 | -1 | diag0 | diag |
| 46 | -1 | netdiag1 | unknown |
| 64 | 64 | lv | lvm |
| 69 | -1 | dev_config | pseudo |
| 72 | -1 | clone | pseudo |
| 73 | -1 | strlog | pseudo |
| 74 | -1 | sad | pseudo |
| 75 | -1 | telm | strtelm |
| 76 | -1 | tels | strtels |
| 77 | -1 | ticlts | pseudo |
| 78 | -1 | tlcots | pseudo |
| 79 | -1 | tlcootad | pseudo |
| 114 | -1 | ip | pseudo |
| 115 | -1 | arp | pseudo |
| 116 | -1 | echo | pseudo |
| 119 | -1 | dlpi | pseudo |
| 130 | -1 | rawip | pseudo |
| 136 | -1 | tcp | pseudo |
| 137 | -1 | udp | pseudo |
| 138 | -1 | stopmap | pseudo |
| 139 | -1 | nuls | pseudo |
| 140 | -1 | netgq | pseudo |
| 141 | -1 | tun | pseudo |
| 142 | -1 | fddi4 | unknown |
| 143 | -1 | fc71_ctl | lan |
| 144 | -1 | fcgsc_lan | lan |
| 145 | -1 | lpr0 | unknown |
| 156 | -1 | ptm | strptym |
| 157 | -1 | pts | strptys |
| 164 | -1 | pipedev | unknown |
| 169 | -1 | conspl | tty |
| 170 | -1 | btlam6 | lan |
| 171 | -1 | fcp | fcp |
| 188 | 31 | sdisk | disk |
| 189 | -1 | klog | pseudo |
| 203 | -1 | sctl | ctl |
| 205 | -1 | stape | tape |
| 207 | -1 | sy | pseudo |
| 227 | -1 | kepd | pseudo |
| 232 | -1 | diag2 | diag |

从这三个 **lsdev** 输出中，你可以观察到设备方面的一些细微差异。例如，Series 700 具有音频和软盘等类别，Series 800 具有多路复用器，而 V-Class 具有 BaseTen 网卡。

你可以使用 **ioscan** 来显示特定外设的设备文件。回到那台连接了四个磁盘和一台 CD-ROM 的 Series 800，你可以发出以下 **ioscan** 命令来查看与*磁盘*相关的设备文件：

（在 Series 800 上）

```bash
$ /usr/sbin/ioscan -fn -C disk
```

| 类 | I 硬件路径 | 驱动 | 软件状态 | 硬件类型 | 描述 |
| :---- | :--------- | :----- | :-------- | :------- | :---------- |
| disk | 0 10/0.3.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t3d0 | | /dev/rdisk/c0t3d0 | |
| disk | 1 10/0.4.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t4d0 | | /dev/rdisk/c0t4d0 |
| disk | 2 10/0.5.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t5d0 | | /dev/rdisk/c0t5d0 |
| disk | 3 10/0.6.0 | sdisk | CLAIMED | DEVICE | HP C2490WD |
|      |            | /dev/dsk/c0t6d0 | | /dev/rdisk/c0t6d0 |
| disk | 3 10/12/5/2.0 | sdisk | CLAIMED | DEVICE | CD-ROM |
|      |              | /dev/dsk/c1t2d0 | | /dev/rdisk/c1t2d0 |

从这个 **ioscan** 输出中，你可以看到所有与*磁盘*相关的设备文件，包括 CD-ROM。

你可以使用 **diskinfo** 命令来获取关于这些设备中某一个的更多信息。请指定你想要了解更多信息的字符设备，如下所示（使用 *-v* 选项提供详细信息可以获得更详尽的信息）。

```bash
$ diskinfo /dev/rdsk/c0t5d0
SCSI describe of /dev/rdsk/c0t5d0
    vendor: HP
    product id: C2490WD
    type: direct access
    size: 2082636 bytes
bytes per sector: 512
```

## 添加外设的示例

在本节中，我们将为一个磁带驱动器构建设备文件。第 9 章介绍了使用设备文件以及所有逻辑卷管理器（Logical Volume Manager）命令来添加磁盘设备的流程，你可能也会想看看这部分内容。在构建设备文件之前，让我们先查看 Series 700 上两个现有的设备文件，看看这些信息出现在哪里。第一个长列表是磁带驱动器的，第二个是磁盘的，两者都在前文的 Series 700 列表中出现过。

```bash
$ ll /dev/rmt/0m
(在 Series 700 上)
crw-rw-rw-  2 bin bin  205 0x003000 Feb 12 03:00 /dev/rmt/0m
```

```bash
$ ll /dev/dsk/c0t1d0
(在 Series 700 上)
brw-r-----  1 bin sys  31 0x001000 Feb 12 03:01 /dev/dsk/c0t1d0
```

磁带驱动器设备文件 **/dev/rmt/0m** 显示主设备号为 205，这与 `lsdev` 中字符设备驱动程序 *stape* 所示的主设备号相对应。磁盘驱动器设备文件 **/dev/dsk/c0t6d0** 显示主设备号为 31，这与 `lsdev` 中*块*设备驱动程序 *fsdisk* 相对应。由于磁带驱动器只需要一个字符设备文件，且没有块 *stape* 设备的主设备号（如 `lsdev` 中块列中的 - *I* 所示），因此该文件是磁带驱动器唯一的设备文件。另一方面，磁盘既可以作为块设备使用，也可以作为字符设备使用（也称为*原始设备*）。因此，我们应该看到一个字符设备文件 /dev/rdsk/c0t6d0，其主设备号为 188，如 `lsdev` 中 *fsdisk* 所示。

（在 Series 700 上）

```bash
$ ll /dev/rdsk/c0t6d0

crw-r----- 1 root sys 188 0x001000 Feb 12 03:01 /dev/rdsk/c0t6d0
```

现在，我们可以使用 `mksf` 命令为第二个磁带驱动器（这次位于 SCSI 地址 2）创建一个设备文件，并为位于 SCSI 地址 5 的磁盘驱动器创建一个磁盘设备文件。你可以以两种不同的方式运行 `mksf`。第一种 `mksf` 形式要求你包含较少具体的信息，例如次设备号。第二种形式要求你包含更多这些具体信息。这些参数中有一些仅适用于你使用的特定 `mksf` 形式。

- `-d`
    使用指定的设备驱动程序。可以使用 `lsdev` 命令获取设备驱动程序列表。
- `-C`
    指定的设备属于此类。类也可以通过 `lsdev` 命令获取。
- `-H`
    使用指定的硬件路径。硬件路径可以通过 `ioscan` 命令获取。
- `-m`
    提供设备的次设备号。
- `-r`
    创建字符设备，也称为原始设备文件。默认情况下创建块文件。
- `-v`
    使用详细输出，这会打印出每个创建的特殊文件的名称。

我们将为磁盘驱动器创建设备文件。需要创建块设备和字符设备文件。示例中的 0x005000 对应于磁盘驱动器上地址 5。这个号码用于块设备和字符设备文件中，对于创建的每个磁盘驱动器都是唯一的。

现在，我们可以使用以下 `mksf` 命令为位于 SCSI 地址 5 的磁盘创建一个块设备文件：

（在 Series 700 上）

```bash
$ /sbin/mksf -v -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/dsk/c0t5d0 b 31 0x005000
```

类似地，我们现在可以使用 `mksf` 的第二种形式为位于 SCSI 地址 5 的磁盘创建一个字符设备文件：

（在 Series 700 上）

```bash
$ /sbin/mksf -v -r -C disk -m 0x005000 /dev/dsk/c0t5d0
making /dev/rdsk/c0t5d0 c 188 0x005000
```

