
# 为此范围添加 `vbios_xe00` 语句，见下文。
# 如果 `DOSEMU` 无法正常启动，请在配置中
# 提前设置 `'allowvideaccess'`，例如花屏、
# 鸣叫或视频信息。
# - `CMOS` 设置中的 `C000-FFF` 视频必须禁用。

# 警告：在启用图形之前关闭 `BIOS` 影子！

# 如果设置为 `'off'` 且开启了图形导致无法启动
# 你的系统，可能需要将此设置为 `'on'`。
# 注意：可能会干扰某些板卡。
`allowvideaccess` `on`

# `100%` 兼容的标准 `VGA` 卡可以使用此项：
# `video { console graphics }`

# 如果你的 `VGA-BIOS` 位于 `E000`，这可能有效：
# `video { console graphics vbios_xe00 }`

# 板载 `1MB` 的 `Trident SVGA`
# `video { console graphics trident 1024 }`

# `Diamond SVGA`
# `video { console graphics diamond }`

# 板载 `1MB` 的 `ET4000 SVGA` 卡：
# `video { console graphics et4000 1024 }`

# 板载 `1MB` 的 `S3` 基 `SVGA` 卡：
# `video { console graphics s3 1024 }`

********************杂杂 *****************

# 快速开始：

# 对于 `'mathco'`，设置为 `'on'` 在 `DOSEMU` 期间启用协处理器。

# 这对 `1.0.3` 之前的内核有效。

# 对于 `'cpu'`，将其设置为你想让 `DOSEMU` 识别的 `CPU`。

# 对于 `'bootA/bootc'`，将其设置为你想使用的驱动器。

# 强烈建议从 `'bootA'` 开始让 `DOSEMU` 运行起来，

# 在配置 `DOSEMU` 期间识别硬盘。

`mathco` `on`    # 数协处理器有效值：`on` `off`

`cpu` `8036`    # `CPU` 仿真值：`8026` `8036` `8046`

`bootA`        # 启动有效值：`bootA` `bootc`

******************** 内存 *********************

# 快速开始：

# 这些是以 `KB` 为单位的内存参数。

# 如果 `DOSEMU` 运行时遇到磁盘交换，你应该

# 减少这些值。此外，`DPI` 仍然有些不稳定

#（截至 `1994` 年 `4` 月），注意 `DPI` 参数。

```
xms 1024          # XMS 大小（K），或 "off"
ems 1024          # EMS 大小（K），或 "off"
dpmi off          # DPI 大小（K），或 "off"。注意 DPI！
```

************************************

* 端口访问

# !!警告！！提供端口访问是一个安全问题，

# 某些部分非常危险。请跳过此部分，

# 除非你知道自己在做什么，否则不要动它。

# `ports { 0x388 0x239 }` # 用于 `SimEarth`

`ports { 0x21e 0x22e 0x23e 0x24e 0x25e 0x26e 0x27e 0x29e }` # 用于 `jill`

************************************

* 扬声器

`speaker` `native`     # 或 "`off`" 或 "`emulated`"

************************************

* 硬盘

# !!警告！！如果在不知道自己在做什么的情况下修改此部分，

# 可能会导致你的硬盘（`LINUX` 和 `DOS`）损坏！

# 快速开始：

# 最好的开始方法是使用软盘启动，并在配置中

# 设置 "`bootA`" 。在为 `DOSEMU` 设置此硬盘配置

# 期间保留软盘并进行测试就是这样。

# 如果你想让 `DOSEMU` 成为一个 `DOS` 分区，

# 更安全的方法是使用 "`partition`" 访问，因为 "`wholedisk`"

# 访问给了 `DOSEMU` 整个磁盘的写入权限，

# 包括该驱动器上的各种 `Linux` 分区！

# !!!重要 !!!

# 你不能在分区上安装 `LILO` 以便 `dosemu` 启动。

# 截至 `94/04/26`，`doublespace` 和 `stack 4.1` 可以在全盘或

# 分区访问下工作。据报道 `Stacker 4.0` 可以在

# 全盘访问下工作。如果你想在使用分区访问时使用

# 磁盘压缩，你需要使用 `dosemu` 自带的 "`mkpartition`" 命令

# 为 `dosemu` 创建一个分区表数据文件。

# 请阅读 "`doc`" 子目录下的文档以获取设置

# 真实硬盘访问的信息。

# "`image`" 指定硬盘镜像文件。

# "`partition`" 指定分区访问，带有设备和分区

```

# 列表 5.1 续

```

# 编号。

# "`wholedisk`" 指定对整个硬盘的完全访问。

# "`readonly`" 用于只读访问。建议在设置时使用。

#

# `$disk < Image /var/lib/dosemu/himage >`    # 我们使用磁盘镜像文件。

# `$disk ( partition /dev/hda1 1 readonly )`  # 第1个IDE上的第1个分区。

# `$disk ( partition /dev/sda2 1 readonly )`  # 第2个SCSI上的第1分区。

# `$disk ( wholisk /dev/hda )`                # 整个硬盘驱动单元

# ***************** DOSEMU 启动*****************

# 使用选项从指定文件启动，并在

# 启动后，`haveboot` 在 `autoexec.bat` 中执行。通知 `Ded`。

# 注意它遵循典型的软盘规范。要创建此文件请使用

# `dd if=/dev/fd0 of=/var/lib/dosemu/bdisk bs=16`

# `$bootdisk heads 2 sectors 18 tracks 80 threeinch /var/lib/dosemu/#bdisk`

# 指定 `CONFIG` 和 `AUTOEXEC` 文件的扩展名。如果

# 取消注释，扩展名将变为 `CONFIG.EMU` 和 `AUTOEXEC.EMU`。

# 注意：此功能可能会影响启动后的软盘命名。

# 如果你使用 `MSDOS 6.2`，你可能想要使用 `CONFIG.SYS` 菜单。

# `nEmuSys EMU`

# `EmuBat EMU`

**************** 软盘 ******

# 快速开始：

# 这部分相当简单。确保第一个 (`/dev/fd0`)

# 第二 (`/dev/fd1`) 软盘驱动器的尺寸正确，“`threeinch`”（三寸）

# 和/或“`fiveinch`”（五寸）。不过，可以使用软盘镜像。

# 为了安全起见，在启动 `DOSEMU` 之前，请拔掉所有物理软盘驱动器，

# 否则可能会软盘造成损坏！

#

# `floppy { device /dev/fd0 threeinch }`

# `floppy { device /dev/fd1 fiveinch }`

# `floppy { heads 2 sectors 18 tracks 80`

# `threeinch /var/lib/dosemu/diskimage }`

## 如果软盘速度非常重要，请考虑以下行。

# 然而，这会让软盘驱动器变得不稳定。

# 在软盘已受写保护的情况下最好使用。

# `nFastFloppy on`

***************** 打印机 ******************

# 快速开始：

# 打印机通过将打印数据管道到文件或通过 `unix`

# 命令 '`lpr`' 进行模拟。在运行起 `DOSEMU` 之前，

# 请不必费心调整此配置。

```
http://www.quecorp.com

# 在 Linux 下运行 DOS 程序
```

# `printer { options "%s" command "lpr" timeout 20 }`

# `printer { options "-p %s" command "lpr" timeout 10 }` # `prn` 格式

# `printer { file "lpt3" }`
