
# 快速上手

使用以下行仅以文本视频启动，启动后当 `DOSEMU` 运行时，你设置更好的视频配置。

`video ( vga console )`      # 如果使用 VGA，请使用此行
`video ( cga console )`      # 如果使用 CGA，请使用此行
`video ( ega console )`      # 如果使用 EGA，请使用此行
`video ( mda console )`      # 如果使用 MDA，请使用此行

甚至更基础的，如在 `xterm` 或串口上，使用以下之一：

对于 `Xterm`
`video ( vga chunks 25 )`

对于 2400 波特率串口
`video ( vga chunks 200 )`

## 图形模式快速上手说明

如果你的 `VGA-BIOS` 位于 `E000-EFF`，关闭该地址范围的视频 `BIOS` 影子，并将语句 `vbios_seg exe000` 添加到正确的 `vbios-statement` 中，参见下示例。

如果 `DOSEMU` 无法正常启动，请在此配置文件的早期位置设置 `'allowvideodeportconn on'`，例如挂起、黑屏或蜂鸣声。

`CMOS` 设置中 `C000-CFFF` 的 `BIOS` 影子必须禁用。

*注意：在启用图形之前关闭 `BIOS` 影子！*

当此项设置为 `'off'` 且启用图形时，某些显卡串口可能需要将其设置为 `'on'`。

`allowvideodeportconn on`

100% 兼容的标准显卡可以使用此项：
`video ( vga console )`

如果你的 `VGA-BIOS` 位于 `E800`，这可能有效：
`video ( vga console vbios_seg exe000 )`

带有兆字节板的 `Trident SVGA`
`video ( vga console memsize 1024 )`

`Diamond SVGA`
`video ( vga console chipset )`

带有兆字节板的 `ET4000 SVGA`
`video ( vga console chipset et4000 memsize 1024 )`

带有兆字节板的 `S3` 核心显卡：
`video ( vga console chipset s3 memsize 1024 )`

![](img/c03a7f0ab2607b66fa9c0158.png)

# 第 5 章 运行应用程序

## 列表 5.1 续

杂项

### 快速上手

对于 `'math'`，在 `DOSEMU` 期间设置为 `'on'` 以启用协处理器。这对 1.0.3 版本有效。

对于 `'cpu'`，在 `DOSEMU` 期间设置为相应的 `CPU`。

对于 `'boota'`/`'bootc'`，将其设置为你想使用的启动器。在配置 `DOSEMU` 时使用 `'bootA'` 来识别硬盘。

处理器有效值：`on`
`CPU` 模拟值：`80286` `80386` `80486`
启动器有效值：`bootc`

内存

### 快速上手

这些是以字节为单位的内存参数。如果 `DOSEMU` 频繁发生磁盘交换，应减少这些值。同时 `DPMI` 尚不稳定（截至 1994 年 4 月），请小心使用。

`xms 1024` # 单位为 K，或 `"off"`
`ems 1024` # `EMS` 单位为 K，或 `"off"`
`dpmi` # 单位为 K，或 `"off"`。小心使用！

端口访问

!!警告!! 访问端口存在安全问题，且部分内容是危险的。除非你知道自己在做什么，否则请跳过此部分。

`ports {0x388 0x389 }`
`ports {0x21 0x22 0x23 0x24 0x25 0x26 0x27 0x29 }`

扬声器

`"speaker"` 行允许以下关键字：
`native` 让 `DOSEMU` 直接访问扬声器端口。
`emulated` 在终端启用简单的蜂鸣声。
`off` 禁用扬声器模拟。

`Speaker native` #或 `"off"` 或 `"emulated"`

硬盘

!!警告!! 如果你在不知道自己在做什么的情况下修改此部分，可能会导致你的硬盘（`LINUX` 和/`DOS`）损坏！

### 快速上手

最好的启动方法是使用软盘启动，并在配置中设置 `"boota"`。继续使用该软盘为 `DOSEMU` 配置此硬盘，并使用 `DIR` 之类的命令进行测试。

在 Linux 下运行 DOS 程序

如果你想让 `DOSEMU` 访问 `DOS` 分区，更安全的访问类型是 `"partition"` 访问，因为 `"wholedisk"` 访问赋予 `DOSEMU` 对整个物理磁盘的写入权限包括该驱动器上的任何 Linux 分区！

!!! 重要 !!!

你不能在分区上安装 `LILO` 以便 `dosemu` 启动。

截至 94/04/26，`doublespace` 和 `stacker 3.1` 可以在仅全或分区访问下工作。`Stacker 4.0` 报告可以在 `whole` 访问下工作，你需要使用 `dosemu` 自带的 `"mkpartition"` 命令为 `dosemu` 创建分区表数据文件。

请阅读 `"doc"` 子目录下的文档以获取有关如何设置真实硬盘访问的信息。

`"image"` 指定硬盘镜像文件。
`"partition"` 指定分区访问，带有设备和分区号。
`"wholedisk"` 指定对整个硬盘的完全访问。
`"readonly"` 用于只读访问。这是一个很好的设置建议。

`image /var/lib/dosemu/hdimage }` # 使用磁盘镜像文件。
`{ partition /dev/hd1 1 readonly }` # 第1 个 IDE 上的 #1 分区。
`{ partition /dev/sda2 1 readonly }` # 第2 个 SCSI 上的 #1 分区。
`{ disk wholedisk /dev/hda }` # 整个磁盘

**DOSEMU 启动** 使用以下选项从指定文件启动，启动后在 `autoexe.bat` 中执行 `bootoff`。感谢 `Ted`:-。

注意它遵循典型的规范。创建此文件使用
`dd if=/dev/fd0 of=/var/lib/dosemu/bdisk bs=16`

启动磁盘（2 扇区 18 轨道 80 英文件 `/var/lib/dosemu/bdisk`）

## 列表 5.1 继续

```
floppy { device /dev/fd0 threeinch }
floppy { device /dev/fd1 fiveinch }
# floppy { head 2 sectors 18 tracks 80 }
#   threeinch file /var/lib/dosemu/diskimage }
```

如果软磁盘速度非常重要，请取消以下行的注释。然而，这会让软磁盘驱动器变得有些不稳定。最好在软磁盘受写保护的情况下使用。

`#FloppyOn`

快速上手：
打印机是通过将打印数据通过管道到文件或通过 unix 命令 `"lpr"` 来模拟的。在运行 `DOSEMU` 之前，请不要费心调整此配置。

`printer { options "%s" "lpr" timeout 20 }`
`#printer ( options "-p %s" "lpr" timeout 10 }` # pr格式化
`printer { file "lpt3" }`
