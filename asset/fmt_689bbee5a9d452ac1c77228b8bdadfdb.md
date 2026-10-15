
所需的软件名为 HairyDairyMaid's Debrick Utility，同时适用于 Linux 和 Windows。Linux 的源代码和 Windows 的二进制文件包含在同一个包中，你可以在镜像站 `http://downloads.openwrt.org/utils` 找到它。你可以通过你选择的操作系统的 Web 浏览器下载 HairyDairyMaid's Debrick Utility（在本文简称为 debrick 工具）。你使用该 debrick 工具的 PC 必须有一个并行端口，以便连接 JTAG 线。

Windows 的安装非常简单。下载工具后，将可执行文件解压到任选的目录，并从命令行执行它。要在 Windows XP 下获取命令行，选择**开始 | 运行**，在**运行**对话框中输入 `cmd.exe` 然后点击**确定**。在新建的命令提示符窗口中，务必导航到解压 debrick 工具的正确目录。

在使用 Windows 版本的 debrick 工具之前，你需要加载一个输入/输出 Windows 驱动程序。在 debrick 工具目录中，你可以使用以下命令启动驱动加载实用程序：

```
loaddrv
```

这会创建一个新窗口。在 **Full pathname of driver** 字段中，你需要输入 `gevio.sys` 的完整路径，该文件也位于 debrick 工具目录中。在我们的示例中，`gevio.sys` 位于 `c:\hdm\`，如图 8.1 所示。输入完整路径后，点击**Start**。

> 提示 LoadDrv 程序似乎有细微缺陷。直觉上 Install 按钮应该允许你永久安装驱动程序，但它并不能。如果你想再次使用 JTAG 线，需要在重启后使用上述过程重启驱动。

![](img/41991837f74596e7c29a2498b6ec56e8_344_0.png)

# 第 8 章 • WRT54G 故障排除

## 图 8.1 LoadDrv 实用程序

![](img/41991837f74596e7c29a2498b6ec56e8_345_0.png)

在你选择的 Linux 环境下，需要在导航到下载工具的目录后解压 debrick 工具。你可以使用 `unzip` 解压：

```
unzip HairyDairyMaid_WRT54G_Debrick_Utility_v48.zip
```

一旦解压了实用程序，你需要切换到包含解压文件的新创建目录，然后使用以下命令进行编译：

```
make
```

> 注意
> 在 Linux 下，在 debrick 工具工作之前，你需要更改内核并行端口驱动程序。你需要卸载 `lp` 内核模块并加载 `ppdev` 内核模块。你可以通过这两条命令完成：

```
rmmod lp
insmod ppdev
```

一旦解压并构建了实用程序，你就可以将其连接到路由器。在 WRT54G 通电的情况下，将 JTAG 线的针连接器端连接路由器，确保记住引脚 1 位置。在 WRT54G 保持断电的情况下，将 25 脚连接器连接到 PC 的并行端口。

> 警告
> 请确保电路板上的引脚 1 与 JTAG 线的引脚 1 正确对齐。

# WRT54G 故障排除 • 第 8 章

在你成功连接电缆后（如图 8.2 所示），现在需要启动 debrick 工具。在命令行导航到 debrick 工具所在的正确目录。在 Windows 下，你可以执行以下命令测试电缆的功能：

```
C:\wrt54g.exe -probeonly
```

在 Linux 下，使用此命令：

```bash
./wrt54g -probeonly
```

## 图 8.2 已安装 JTAG 自动检测

![](img/41991837f74596e7c29a2498b6ec56e8_346_0.png)

为 WRT54G 上电并使用前面的命令启动 debrick 工具。执行后，debrick 工具将自动连接并识别 WRT54G 芯片组，如图 8.3 所示。

## 图 8.3 Debrick 工具自动检测

```
C:\windows\system32\cmd.exe wrt54g.exe -probeonly
C:\admin>wrt54g.exe -probeonly
=====================================
WRT54G/JTAG Debrick Utility v4.8
=====================================
Probing bus ... Done
Instruction Length set to 5
CPU Chip ID: 011111110111011101110111 (0x471017F)
Found a Broadcom BCM57682 Rev 1 CPU chip ***
JTAG IMPCODE             : 000000000000000000000000 (0x000000)
JTAG VERSION             : 1 or 2.0
JTAG ID Support          : YES

Issuing Processor / Peripheral Reset ... Done
Enabling Memory Writer ... Done
Halting Processor ... <Processor Entered Debug Mode> ... Done
Clearing Watchdog ... Done
```

如果 debrick 工具无法自动检测硬件，可以通过执行工具时在命令行指定 `-Ifc:<value>` 来强制使用指定的芯片组。要确定适用于芯片组的值，请不带任何命令行选项运行实用程序以显示内置帮助。内置帮助包含了所有支持的芯片组的值。

## 工具与陷阱

### 看门狗

在使用 debrick 工具进行所有 JTAG 操作期间，你都会看到关于“清除看门狗”（Clearing Watchdog）的输出。该看门狗是内置于 CFE 的保护机制（见第2 章），用于判断是否发生了对 CFE 的非预期访问（根据制造商，你的活动可能被认为是非预期的）。该看门狗被设置了一个内部定时器，当定时器触发时，看门狗会终止所有 JTAG 操作。

# WRT54G 故障排除 • 第 8 章

为了开始备份，你需要在执行 debrick 实用工具时添加一些命令行开关。首先，使用以下命令备份 CFE：

```
# wrt54g -backup:cfe
```

debrick 实用工具将连接到路由器，并开始将 CFE 的内容复制到 PC 上，文件命名为 `CFE.BIN.SAVED_<datestamp>_`，并与 debrick 实用工具位于同一目录下。完成后，它将通知你完成状态并返回命令行。使用以下命令备份你的 NVRAM：

```
# wrt54g -backup:nvram
```

同样，debrick 实用工具将连接到路由器，并开始将 NVRAM 的内容复制到 PC 上的文件中，命名为 `NVRAM.BIN.SAVED_<datestamp>_`，并与 debrick 实用工具位于同一目录下。完成后，它将通知你完成状态并返回命令行。

> 警告
> 在执行多个读取或写入闪存芯片的 debrick 实用工具命令之前，在命令之间重启路由器始终是一个好主意。这将确保路由器和 CFE 在每个命令下处于适当状态。

![](img/41991837f74596e7c29a2498b6ec56e8_348_0.png)

## 备份整个闪存芯片

尽管我们建议你跳过备份内核或整个闪存芯片的操作，但这是完全可行的。尽管在砖化的设备上备份整个闪存的用处尚疑，但它在其他情况下可能有用。

为了备份整个闪存芯片，你仍然可以使用 debrick 实用工具。要执行备份，请运行以下命令。

```
# wrt54g -backup:wholeflash
```

根据你正尝试备份的 WRT54G 型号闪存芯片的大小，此过程可能需要 6 到 24 小时才能完成！这是因为 JTAG 连接的带宽有限，且整个闪存芯片的尺寸很大。

除了时间限制外，你应该避免在砖化的路由器上备份整个闪存的另一个原因是，三个主要的闪存区域被合并在一个文件中，而不是分成独立的、易于恢复的文件。

# 第 8 章 • WRT54G 故障排除

使用其他工具将所有闪存备份镜像拆分为单独的文件，这很快就会变成一项低效的尝试。

一旦你完成了所有备份，就可以开始将路由器配置恢复到工作状态。你将从简单的问题开始，逐步处理更困难的问题。

你通过 JTAG 线缆可以修复的最简单问题涉及 NVRAM。通过将 NVRAM 变量设置为错误的设置并使路由器无法访问，将 WRT54G 变成“砖头”是非常容易的！在这个棘手的过程中，作者们通过错误地定义虚拟局域网（VLAN）分配，成功地把自己锁在了 WRT54G 之外，导致无法与路由器进行任何网际协议（IP）通信。使用以下命令清除 NVRAM 设置：

```
# wrt54g -erase:nvram
```

短段时间后，debrick 实用工具应该报告成功。如果这是你修复路由器所需的所有操作，重启后将把 WRT54G 恢复到默认配置。
