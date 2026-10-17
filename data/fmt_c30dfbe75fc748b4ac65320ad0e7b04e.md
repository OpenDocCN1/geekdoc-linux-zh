
# `ln -s /dev/hdd /dev/cdrom`

如果你想播放音频 CD，你需要设置设备文件（实际文件，而不是指向它的符号链接）的权限允许所有用户读取，例如：

```bash
# chmod 666 /dev/hdd
# ls -l /dev
brw-rw-r-- 1 root disk 22, 64 Feb 4 1995 /dev/hdd
```

在启动 Linux 时，驱动程序会尝试确定合适的设备是否存在，通常通过探测地址来实现。许多驱动程序会在多个地址上进行自动探测，但由于配置差异、可能的设备冲突以及硬件限制，驱动程序有时需要帮助来识别地址和其他参数。大多数驱动程序支持内核命令行上的选项，可以交互式完成，或者更常见的是配置到你的启动加载器中。例如使用 LILO，你需要在 `/etc/lilo.conf` 文件中添加如下的 `append` 命令：

```conf
append = '*spbcd0x230,SoundBlaster*'
```

更多信息请参考 LILO 文档。

在下一节中，我将讨论各个设备驱动程序，包括设备文件、启动参数以及不同驱动程序的能力。你只需要阅读与你的驱动器类型相关的章节。README 文件通常位于 `/usr/src/linux/Documentation/cdrom` 目录下。

### 4.3.1 Spbcd 驱动程序

- 主要作者：Eberhard Moenberg (`emoenberg@gwdg.de`)
- 多会话支持：是（但并非所有驱动器）
- 多驱动器支持：是
- 可加载模块支持：是
- 读取音频帧：是（仅限 CR-562, CR-563, CD-200）
- 自动探测：是
- 设备文件：`/dev/spbcd`，主设备号 25
- 配置文件：`spbcd.conf`
- 内核配置选项：Matsushita/Panasonic CDROM support
- README 文件：`spbcd`

该驱动接受格式如下的内核命令行：

```
spbcd=<io-address>,interface-type
```

其中第一个参数是设备的基地址（例如 `0x230`），而 `<interface-type>` 是 "SoundBlaster, LaserMate," 或 "SPEA" 之一。参考第一个文件 `sbcd.h` 获取使用何种接口的提示。使用 `sbcd=0` 会禁用自动探测从而禁用驱动程序。

可以使用以下命令创建设备文件：

```bash
# mknod /dev/sbcd b 25 0
```

每个控制器支持多四个驱动器。第一个控制器上的后三个将使用从 1 到 3 的次设备号。如果你有多个控制器，请创建主设备号为 26、27 和 28 的设备，最少支持 4 个控制器（这总共有 16 个 CD-ROM 驱动器；对大多数用户足够）。

关于此设备的更多信息请参见 `sbcd`。

如果你最近购买了 CD-ROM 驱动器，不要假设它连接到了 SoundBlaster 卡或它应该使用此内核驱动程序。大多数由 Creative Labs 构建的 CD-ROM 驱动器现在都是 IDE/ATAPI 驱动器。请不要就关于使用 IDE 设备使用此驱动器的其他问题打扰作者。引用 README 文件的话：

`sbcd` 真的不用于任何 IDE/ATAPI 驱动器！
即使你有一个带有 IDE 接口的“原始”SoundBlaster 卡！
所以，如果你的端口地址是 `0x1F0`, `0x170`, `0x18`, `0x168` 或类似的，最好查看 README.ide。
我收到来自 IDE/ATAPI 驱动器用户的邮件——我真的无法回答他们所有人。所以，如果你的驱动器/接口信息表显示为 "IDE"（主、辅、三级、四级）且你 `CONFIG.SYS` 中的 DOS 驱动程序调用行使用的是低于 `0x230` 的地址：
别折磨我的最后一个神经——将你的接口跳线设置到地址 `0x170` 和 IRQ 15（即“辅助 IDE 配置”）。

### 4.3.2 Sonycd35 驱动程序

- 主要作者：`ken@hal.com`
- 多会话支持：否
- 多驱动器支持：否
- 可加载模块支持：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/sonycd`，主设备号 24
- 配置文件：`sonycd.h`
- 内核配置选项：Sony CDROM support
- README 文件：`sonycd`

该驱动接受格式如下的内核命令行：

```
sonycd=<io-address>
```

其中第一个参数是设备的基地址（例如 `0x230`），而 `<interface-type>` 是 "PAS" 之一。

可以使用以下命令创建设备文件：

```bash
# mknod /dev/sonycd b 24 0
```

### 4.3.3 Cdu3a 驱动程序

- 主要作者：Corey Minyard (`minyard@cir.com`)
- 多会话支持：是
- 多驱动器支持：否
- 可加载模块支持：是
- 读取音频帧：是
- 自动探测：否
- 设备文件：`/dev/cdu3a`，主设备号 15
- 配置文件：`cdu3a.h`
- 内核配置选项：Sony CDU1A support
- README 文件：`cdu3a`

该驱动接受格式如下的内核命令行：

```
cdu3a=<io-address>,interrupt
```

其中第一个参数是设备的基地址（例如 `0x340`），而 `<interface-type>` 是中断号。

可以使用以下命令创建设备文件：

```bash
# mknod /dev/cdu3a b 15 0
```

### 4.3.4 Aztcd 驱动程序

- 主要作者：Werner Zimmermann (`zimmermann@rz.fht-esslingen.de`)
- 多会话支持：是
- 多驱动器支持：否
- 可加载模块支持：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/azctcd0`，主设备号 29
- 配置文件：`aztcd.h`
- 内核配置选项：Azctch/Orchid/Okano/Wearneas (non IDE) CDROM support
- README 文件：`aztcd`

该驱动接受格式如下的内核命令行：

```
azcd=<io-address>
```

其中参数是卡的 I/O 基地址（例如 `0x340`）。

可以使用以下命令创建设备文件：

```bash
# mknod /dev/azctcd0 b 29 0
```

# 788

注意，此驱动程序适用于 CDA268-01A。其他模型，包括 CDA268-031 和 CDA269-031SE，并非专有，应该使用 IDEC (ATAPI) 内核驱动。
有关此驱动程序的更多信息，请参 `azcd` 文件。

## 4.3.5 Gscd 驱动

- 主要作者：Oliver Raupach (`raupach@nwfs1.rz.fh-hannover.de`)
- 多会话支持：否
- 多驱动器支持：否
- 支持可加载模块：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/gscd0`，主设备号 16
- 配置文件：`gscd.h`
- 内核配置选项：Goldstar R420 CDROM support
- README 文件：`gscd`

该驱动程序接受如下形式内核命令行：

```
gscd=<io-address>
```

指定显卡的 I/O 基础地址（例如 `0x340`）。
可以使用以下命令创建设备文件：

```
# mknod /dev/gscd0 b 16 0
```

有关此驱动程序的更多信息，请参阅 `gscd` 文件和网站 (`http://linux.fz-hannover.de/~raupach`)。

## 4.3.6 Mcd 驱动

- 主要作者：Martin (`martin@bdsi.com`)
- 多会话支持：否
- 多驱动器支持：否
- 支持可加载模块：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/mcd`，主设备号 23
- 配置文件：`mcd.h`
- 内核配置选项：Standard Mitsumi CDROM support?
- README 文件：`mcd`

这是 Mitsumi 驱动的旧版驱动，已经存在一段时间。你可能想尝试新的 `mcdx` 驱动，它具有一些新功能，但可能稳定性较低。

该驱动程序接受如下形式内核命令行：

```
mcd=<io-address>,<irq>
```

指定显卡的 I/O 基础地址（例如 `0x340`）和使用的 IRQ 请求号。
可以使用以下命令创建设备文件：

```
# mknod /dev/mcd b 23 0
```

有关此驱动程序的更多信息，请参阅 `mcd` 文件。

## 4. 安装

## 4.3.7 Mcdx 驱动

- 主要作者：Heiko Schlittermann
- 多会话支持：是
- 多驱动器支持：是
- 支持可加载模块：是
- 读取音频帧：否（硬件不支持）
- 自动探测：否
- 设备文件：`/dev/mcd0`，主设备号 20
- 配置文件：`mcdx.h`
- 内核配置选项：Experimental Mitsumi support?
- README 文件：`mcdx`

这是一个用于 Mitsumi 的较新驱动。旧版且更稳定的 `mcdx` 驱动仍然可用。
该驱动程序接受如下形式命令行：

```
mcdx<io-address>,<irq>
```

指定显卡的 I/O 基础地址（例如 `0x340`）和 IRQ 请求号。
可以创建设备文件：

```
# mknod /dev/mcd0 32 20
```

如果你有一个 Mitsumi CD-ROM 驱动器，不要假设它应该使用此内核驱动。某些 Mitsumi 模型现在是 IDE/ATA 驱动器，应该使用 `ideck` 内核驱动。
有关此驱动程序的更多信息，请参阅 `mcdx` 文件。

## 4.3.8 Cm206 驱动

- 主要作者：David A. van Leeuwen (`david@tm.no`)。
- 多会话支持：是
- 多驱动器支持：否
- 支持可加载模块：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/cm206cd`，主设备号 32
- 配置文件：`cm206.h`
- 内核配置选项：Philips/LMS CM206 CDROM support?
- README 文件：`cm206`

驱动接受如下形式命令行：
```
cm206<io-address>,<interrupt>
```

其中第一个数字是显卡的 I/O 基础地址（例如 `0x340`）。第二个是中断通道。
可以创建设备文件：

```
# mknod /dev/cm206cd 32 0
```

有关此驱动程序的更多信息，请参阅 `cm206` 文件。

## 4.3.9 Optcdv 驱动

- 主要作者：Leo Spiekman (`spiekman@dutette.tudelft.nl`)
- 多会话支持：是
- 多驱动器支持：否
- 支持可加载模块：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/optcd0`，主设备号 17
- 配置文件：`optcd.h`
- 内核配置选项：Experimental Optics Storage ... CDROM support
- README 文件：`optcd`

驱动接受如下形式内核命令行：
```
optcd=<io-address>
```

以指定显卡的 I/O 基础地址（例如 `0x340`）。
可以使用以下命令创建设备文件：

```
# mknod /dev/optcd0 b 17 0
```

有关此驱动程序的更多信息，请参阅 `optcd` 文件。

## 4.3.10 Sjcd 驱动

- 主要作者：Vadim V. Model (`vadim@msk.ru`)
- 多会话支持：否
- 多驱动器支持：否
- 支持可加载模块：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/sjcd`，主设备号 18
- 配置文件：`sjcd.h`
- 内核配置选项：Experimental Sanyo CDROM support?
- README 文件：`sjcd`

驱动接受如下形式内核命令行：
```
sjcd=<io-address>,<interrupt>,<dma>
```

指示基础地址、中断和使用的 DMA 通道（例如 `sjcd=0x340,5`）。
可以创建设备文件：

```
# mknod /dev/sjcd b 18 0
```

有关此驱动程序的更多信息，请参阅 `sjcd` 文件。

## 4.3.11 SCSI 驱动

- 主要作者：David Giller
- 多会话支持：是（取决于驱动器）
- 多驱动器支持：是
- 支持可加载模块：是
- 读取音频帧：否
- 自动探测：是
- 设备文件：`/dev/scccd0`，主设备号 11
- 配置文件：`cdrom.h`
- 内核配置选项：SCSI CDROM support
- README 文件：无

内核命令行用于指定每个类型的 SCSI 控制器。请查看 SCSI HOWTO。
支持多个驱动器（取决于 SCSI 总线的限制）。创建从 11 开始的设备文件：

```
# mknod /dev/scccd0 b 11 0
# mknod /dev/scccd1 b 11 1
```

虽然驱动本身不支持读取音频帧，但某些 SCSI 驱动具有 `cdda`（使用通用 SCSI 接口）。

## 4.3.12 IDE 驱动

- 主要作者：Scott Snyder (`snyder@final.gov`)
- 多会话支持：是
- 多驱动支持：是
- 支持可加载模块：否
- 读取音频帧：是（在支持的驱动器上）
- 自动探测：是
- 设备文件：`/dev/hdb(a,b,c,d)`，主设备号 22
- 配置文件：`cdrom.h`
- 内核配置选项：Include support for IDE/ATAPI CDROM
- README 文件：`ide-cd`

这是用于 ATAPI CD-ROM 的驱动。驱动接受内核命令行：
```
hdx=cyls,heads,sectors,rw,irq
hdx=cdrom
```

其中 `hdx` 可以是任何 `hda`。让 IDE 驱动识别你的 CD-ROM 可能很困难，特别是当你有超过两个设备或一个 IDE 控制器时。通常只需要向 LILO 传递正确的命令行选项。文件 (`/usr/src/linux/Documentation/ide-cd`) 解释了如何操作。

最近的 Linux 内核对多个 IDE 设备有更好的支持。升级可能会帮助。某些 IDE 控制器的硬件问题可以通过内核驱动来解决。你可能需要向驱动添加额外的参数来启用此。详情见文档。

## 4.4 启动 Linux 内核

现在使用新内核重启。注意类似下面的消息，表示驱动程序找到了 CD-ROM（消息取决于驱动器类型）：

```
hdd: CD-ROM DRIVE:2, ATAPI CDROM drive
```

如果引导信息滚动得太快，你应该可以使用 `dmesg` 或 `/var/adm/messages` 来检索它们。

如果找不到驱动器，则存在问题。请参见故障排除章节。

## 4.5 挂载、卸载和弹出设备

要挂载 CD-ROM，请将磁盘插入驱动器并以 root 身份运行 `mount` 命令（这假设你已如上面建议创建了设备文件的符号链接，并且存在空目录 `/mnt/cdrom`）：

```
# mount -t iso9660 -r /dev/cdrom /mnt/cdrom
```

现在可以在 `/mnt/cdrom` 目录下访问 CD 了。`mount` 命令还有其他你可能使用的选项；详情请参手页。

你可以在 `/etc/fstab` 中添加条目以便在 Linux 启动时挂载 CD-ROM，或指定挂载时使用的参数；请参见 `fstab(5)` 手页。

注意，播放音频 CD 不应尝试挂载它们。

要卸载 CD-ROM，请以 root 身份运行 `mount` 命令：

```
# mount /mnt/cdrom
```

只有在没有进程正在访问驱动器（包括其默认目录设置为挂载的驱动器）时，才能卸载磁盘。然后你可以弹出磁盘。大多数驱动器都有弹出按钮；还有一个独立的 `eject` 程序允许在软件控制下弹出 CD-ROM。

注意，你不应该在磁盘挂载时弹出（这可能也可能可能，取决于驱动器类型）。某些 CD-ROM 驱动可以在卸载时自动弹出 CD-ROM 并在挂载时插入光盘（你可以使用内核或软件命令关闭此功能）。

## 4.6 故障排除

如果在遵循 HOWTO 中的说明后仍然遇到问题，这里是需要检查的内容。检查按复杂度增加的顺序列出。如果检查失败，在移动到下一个阶段之前解决问题。

### 4.6.1 步骤 1：确保你运行的是编译的内核

你可以检查内核的时间戳以查看运行的是否编译了 CD-ROM 支持。你可以使用 `uname` 命令：

```
$ uname -a
Linux fizzbin 2.0.18 #1 Fri Sep 6 10:10:54 EDT 1996 586
```

或者显示 `/proc/version`：

```
$ /proc/version
Linux version 2.0.18 (root@fizzbin) (gcc version 2.7.2) #1
Fri Sep 6 10:10:54 EDT 1996
```

如果时间戳与你编译内核时不匹配，说明你运行的是旧内核。你真的重启了吗？如果你使用 LILO，你应该重新安装它（通常通过运行 `/sbin/lilo`）。如果从软盘启动，创建新的启动软盘并启动？

### 4.6.2 步骤 2：确保编译了正确的内核驱动

你可以通过查看 `/proc/devices` 查看驱动程序被编译在哪里：

```
$ /proc/devices
Character devices:
1 mem
2 pty
3 typ
4 ttyS
5 cua
7 vcs
```

首先寻找你的 CD-ROM 设备驱动程序。这些都是块设备，在这种情况下，我们可以看到主设备号为 22 的驱动确实存在。

还要确保 ISO-9660 文件系统已编译编译，通过查看 `/proc/filesystems`

## 4. 安装

```bash
% cat /proc/filesystems
ext2
msdos
```
