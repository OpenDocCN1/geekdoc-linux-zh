
# 深度解析

## `Command_coreboot`

通用 / UMS 配置值 = `CMDS` 默认值位于你的主板目录 `src/mainboard/model.defs`

设备 / 原生图形初始化 = 启用（注意：并非所有系统都可用）

显示 / 帧缓冲区 = 禁用（文本模式图形的默认值，在 `coreboot` vs 中启用）

负载 / USB 2.0 调试支持 = 启用

通用驱动 / 启用（RAM 之前）使用调试 = 启用

通用驱动 / 令牌棒类型 = 任意或无

通用驱动 / 数字化器 = 存在

控制台 / 双控制台输出 = 启用

负载 / 文件名 = `payload`（如果你想要不同的负载，请更改此项）

**图 4：** 在带有集成显卡的机器上，要求固件的通用固件选项。使用 `coreboot`。

设备 / VGA 选项 = 禁用

设备 / PCI 设备上的 ROM = 禁用

最近，我使用了一个名为 `coreboot-configuration` 的图形化工具来处理设备变体。在你研究完特性并成功构建固件后，你会遇到一些问题。

**图 5：** 没有集成显卡的机器需要两个选项。

进入包含 `coreboot` 以及任何厂商或负载构建的目录（图 6）。在构建结束时，无论成功失败，都需要要求你在下一次尝试之前通过一些研究进行纠正。只有在一次失败后才出现过刷写成功。尽管如此，请务必小心，在尝试之前搜索流程，并备份你的文件。如果你按照上述说明操作，你将能够构建内核（即同一台电脑的其中一个）。在包含你固件的目录中，

## 刷写、拆解与移除

这些指令是从零开始刷写固件的。`coreboot` 作为一个操作系统正在飞速发展。越来越多的 Linux 硬件厂商正在让 `coreboot` 变得更易于获取。例如，System 76 显示了它的选项，包括查找硬件规格的脚本 (6)，以及比说明中显示的步骤多得多的更新。在这里，Ubuntu 自带了一个用于安装 `coreboot` 配置的工具，这与更新 Android 手机一样简单可能并不遥远。

现在，刷写自定义固件最简单的方法是使用 `flashrom` [7]，它是用于刷写以下内容的相同实用程序：

```
flashrom -i -w/coreboot
```

你可能需要在启动管理器中启动。如果该过程没有成功，请检查 `coreboot` 文档中关于其他刷写方法，以及作为更常用的：目前，编辑 `coreboot` 最简单的方法是重置闪存编程器。Star Labs 有：

```
bbqsystem76-pc=~/coreboot/ coreboot make
Updating git modules
HOSTCC
util/config.lex.py
HOSTCC
util/config.tab
HOSTCC
util/config/main
util/config (link)
mainboard/emulator/qemu-1440fx/devicree.cb
```

```
# No /to home-bb/coreboot/.config
build.auto.config 1611: override = assignment to symbol LAPIC ACCESS MODE
HOSTCC
nvartool/cl1/nvtool.o
nvartool/clipt/opts.o
HOSTCC
nvartool/cm0_level.o
HOSTCC
nvartool/charm.o
HOSTCC
nvartool/common.o
HOSTCC
nvartool/compute_checksum.o
HOSTCC
nvartool/newsetup
```

信息：https://coreboot.org/

[已支持] 方法：https://coreboot.org/status/boot-status.html

[`coreboot`] 文档：https://coreboot.org/HOWTO/kerneldev

[`Qemu`] 教程：https://coreboot.org/QEMU_Menu_Tutorial

[`Payloads`]：https://doc.coreboot.org/payload.html

[`System`] 文档：https://github.com/system/firmware-open-blob/flashing.md

[`flash`]:https://www.com/Flashrom

[`8 固件`]:https://doc.coreboot.org/tutorial/flashing/index.html

[`coreboot-configuration`]:https://support.starlabs.com/kb/guides-corebootconfiguration

**图 6：** 编译固件：仅刷写成功构建的文件。

2023年7月44日 | 第 272 期 | LINUX-MAGAZINE.COM

## 将你的想法变为现实！

这不是一本普通的电脑杂志！`MakerSpace` 专注于你可以用来构建属于自己的东西的技术。

如果你对电子产品感兴趣，但还没有时间或技能（目前），学习这些 Maker 项目可能是让你开始的最后推动力。

这期特别刊将帮助你深入研究：

- 树莓派
- `Arduino`
- 复古游戏
- 以及更多！

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_44_0.png)

# 深度解析

逆向工程蓝牙

逆向工程一个 `BLE` 钟

# 完美时间

当你所有的蓝牙钟显示的时间略有不同时，你会怎么办？通过逆向工程，你计划编写一个 `Python` 程序来同步你的时。作者：Koen Vervloesen

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_45_0.png)

我有一个 ThermoPro TP358，这是一个带有显示器的蓝牙低功耗 (BLE) 数字温度计。ThermoPro 显示温度、湿度和空气舒适度指数，以及时间和日期。它的显示对于即时反馈很好，但该设备允许你通过 Android 和 iOS 上的 App 读取其值并查看图表（图 1）。我的计划是弄清楚命令的含义，然后在可以全天运行的树莓派上实现同步命令。本文描述了我我是如何对 ThermoPro TP358 实现此，但你可以对任何 BLE 设备使用相同的步骤。此外，每当我连接到 App 时，它都会同步时间。

## 调查流量

有多种方法调查流量。如果你正在调查 Android 手机发送的 BLE 数据包，简单的方法是让手机记录，然后将日志传输到电脑并用 Wireshark 打开。作为更常用的：目前，编辑 `coreboot` 最简单的方法是重置闪存编程器。Star Labs 有：

## 深度解析

## 蓝牙逆向工程

它以值 `a5` 开始并以 `5a` 结束，因此这看起来像是一个包头和页脚。`5a` 之前的 `01` 看起来也不像，可能是页脚或其他内容。此外，`07` 始终保持为 `07`，看起来像是一天中的结束，而 `07` 变成了其他值。也许这些是秒，它们不在时钟显示范围内。

`ykr_hn_2085a_tlu66`。因此数据包中的后续行是应用对应的：

```
package/data/app/--9lh-Mj7iUbObZ26AIew=/com.humuro.ykr_hn_2085a_tlu66-dZE=lThVNbRa26Iqd=/app.com.humuro.ykr_hn_2085a_tlu66/
```

在解压目录内从命令行运行 `./bin/jadx-gui`。选择你下载的 `.apk` 文件。程序将向你显示类和层的树形结构，如下：

现在将 `apk` 文件从文件夹复制到你的：

```
adb pull data/app/--9lh-Mj7iUbObZ26AIew=/com.humuro.ykr_hn_2085a_tlu66-dZE=lThVNbRa26Iqd=/app.com.humuro.ykr_hn_2085a_tlu66/
```

并使用路径方法反编译第一个或最后一个字符。结果保存在你的电脑上作为。

如果获取 `apk` 文件不起作用，你可以从第三方 `apk` 反编译器下载，例如 `apk`:

遵循指纹操作。你现在已准备好搜索设置目标了。查看 Wireshark 中的蓝牙日志。你已经分析出了数据包中包含的值，但它在哪里呢？点击详情面板中的下拉菜单。查看 UUID 的方法是：
