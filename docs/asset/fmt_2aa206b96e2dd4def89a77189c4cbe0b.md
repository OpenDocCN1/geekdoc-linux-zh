
> 在运行任何 X11 配置工具之前，务必复制或备份任何运行正常的 `XFree86Config` 配置文件。

## 配置音频设备

大多数用户都希望配置一个与 Red Hat Linux 工作的声卡。音频支持通常在 Red Hat Linux 首次启动时配置（如果在安装过程中识别到声卡，则在安装期间配置）。本节向你展示如何基于文本的 `alsaconfig` 命令或图形化的 `redhat-config-sound` 客户端为 Red Hat 配置音频。

如果你无法使用 Red Hat 的软件为系统配置音频，可以转向高级 Linux 架构 (ALSA) 项目的软件 http://www.alsa-project.org。使用 RPM 包下载并安装 ALSA 驱动、库和工具，或根据网站上的说明编译并安装 ALSA。

使用替代音频软件可能会很有帮助。例如，在 VIA EP3 min-ITX 主板（使用 8233 VIA 音频芯片组）上运行 Red Hat 的用户将需要使用 ALSA 才能使用，因为内置驱动将无法工作。实现这一点的方法是下载以下源码包：

```
alsa-driver-0.9.0rc5.tar.bz2
alsa-lib-0.9.0rc5.tar.bz2
alsa-utils-0.9.0rc5.tar.bz2
```

应对这些压缩包进行解压：

```
# tar xjvf alsa*driver* ; tar xjvf alsa*lib*; tar xjvf alsa*utils*
```

接下来，导航到生成的 ALSA 驱动目录，然后配置、编译并安装驱动：

```
# cd alsa*driver* ; ./configure; make; make install
```

对 ALSA 软件库执行相同的操作，并编译安装 ALSA 工具软件。你可以使用 `insmod` 命令加载支持的内核模块来初始化并配置音频：

```
# modprobe snd-via82xx
# modprobe snd-pcm-oss
# modprobe snd-mixer-oss
# modprobe snd-seq-oss
```

这将初始化你的声卡（ALSA 编号为 0）。要使用音频，你应该使用 ALSA 的 `alsamixer` 命令取消声卡通道的静音。要使用音频，你应该使用 ALSA 的 `alsamixer` 命令取消声卡通道的静音。

> 注意
>
> 要使用音频，你应该使用 ALSA 的 `alsamixer` 命令取消声卡通道的静音。

这将初始化你的声卡（ALSA 编号为 0）。要使用音频，你应该使用 ALSA 的 `alsamixer` 命令取消声卡通道的静音。

```
# alsactl store
```

你的声卡状态将保存在文件 `/asound.state` 中。

### 使用加载模块启动音频

虽然声卡可以直接编译到内核中，但通常使用可加载内核模块来启动音频。这些模块通过 `/etc/modules.conf` 中的条目启用，类似于示例：

```
# THIS FILE IS WRITTEN BY SNDCONFIG
# PLEASE USE SNDCONFIG TO MODIFY
# TO CHANGE THIS FILE!
# 行开头不有空格
# 等 号周围不有空格
CARD=SB16
```

![](img/e862c5b60f9f55ef43a34453c49f252f_138_0.png)

图 4.5 `sndconfig` 命令可用于配置新的声卡。

> 注意
>
> 如果您的音频配置正常且您已经为 Red Hat 安装了多媒体支持，那么可以使用类似 `ogg123` 音频播放器播放 Brent Fox 的 Red Hat Linux Credits 主题来完成测试：
>
> # `ogg123 /usr/share/redhat-credits.ogg`

Red Hat 还包含一个图形化音频客户端，用于在 X 会话期间配置声卡。您可以通过点击桌面面板的“系统设置-声卡检测”菜单或项目，或者在终端窗口中使用以下命令来启动 `redhat-config-soundcard` 客户端：

```
$ redhat-config-soundcard &
```

按下回车后，系统将提示您输入 root 密码。输入密码并点击确定。`redhat-config-soundcard` 将尝试自动检测并配置您的声卡。随后您将看到一个对话框，可以使用它测试声卡设置，如图 4.6 所示。点击“播放声音”按钮即可听示例音频。

# 第 4 章 安装后配置

![](img/e862c5b60f9f55ef43a34453c49f252f_139_0.png)

图 4.6 `redhat-config-soundcard` 客户端用于 X 会话期间为 Red Hat Linux 配置声卡。

## 检测和配置调制调器

美国已有超过七百万用户通过电缆或 DSL 服务连接互联网，但对许多用户来说，调制调器是使用点点协议（PPP）连接互联网提供商（ISP）的标准方式。调制调器的其他常见任务包括收发传真。如果您在初始安装 Red Hat 后添加或更改了调制调器，则需要配置调制调器以执行所有这些任务。

Red Hat 提供了多种工具，供您在笔记本电脑或 PC 中配置和使用内部或外部调制调器。第 15 章“互联网连接”包含了关于如何配置调制调器的 Red Hat Linux 连接互联网的详细信息。本节涵盖了如何配置 Red Hat Linux 使用串口（使用以前称为 RS232 标准，现在称为 EIA232）或 USB 来识别并配置调制调器。

### 配置串口调制调器

Linux 使用 `/dev/ttyUSB0` 到 `/dev/ttyUSBX` 表示串口，其中 X 的范围从 0 到 15。可以使用多端口卡或链式 USB 设备向系统中添加许多额外端口。PC 的集成串口通常在启动时被识别。要查看系统已识别的端口列表，请通过 `fgrep` 命令查看 `dmesg` 输出，如下：

```
# dmesg | grep tty
ttyS0 at 0x03f8 (irq 4) is 16550a
ttyS1 at 0x02f8 (irq 3) is 16550a
```

在此示例中，Linux 报告识别了两个端口。请注意，尽管内核输出如此，匹配 `ttyS0` 的设备是 `/dev/ttyS0`。PC 的外部调制调器可以连接（最可能使用 DB9 适配器）到任何一个端口。在 Red Hat Linux 下，几乎所有基于调制调器的软件都使用名为 `/dev/modem` 的符号链接指向目标设备。该链接默认创建的，但作为 root 用户，您可以使用 `ln` 命令手动创建此设备，如下：

```
# ln -s /dev/ttyS0 /dev/modem
```

在此示例中，`/dev/modem` 将指向第一个串口。

### 检测和配置调制调器

您也可以在初始安装 Red Hat Linux 后使用 Red Hat 的图形化 X 客户端配置调制调器。Red Hat 的 `redhat-config-network` 客户端（如图 4.7 所示）将尝试探测系统中可用的调制调器。如果没有找到调制调器，您可以手动输入调制调器数据。

![](img/e862c5b60f9f55ef43a34453c49f252f_140_0.png)

图 4.7 Red Hat Linux `redhat-config-network` 客户端将探测可用的调制调器。

KDE 提供了 `kmod` 客户端（如图 4.8 所示），当您设置新的点点协议（PPP）连接时，可以使用它查找并设置调制调器。点击 `kmod` 对话框中的“查询调制调器”按钮以搜索已安装的调制调器。

Red Hat Linux 为系统管理员提供了命令行诊断和串口配置工具。例如，要获取有关特定端口的更多信息，可以使用 `statserial` 命令配合指定的设备：

```
# statserial /dev/ttyS0
Device: /dev/ttyS0
```

| 信号名称 | 引脚 | 方向 | 状态 | 全称 |
|---|---|---|---|---|
| FG (25) | 1 | | | 框架地 |
| TxD | 2 | 3 | out | 发送数据 |
| RxD | 3 | 2 | in | 接收数据 |
| RTS | 4 | 7 | out | 请求发送 |
| CTS (25) | 5 | | | 准备发送 |
| DSR | 6 | | | 数据集就绪 |
| GND | 7 | | | 信号地 |
| DCD | 8 | | | 载波检测 |
| DTR | 9 | | | 终端就绪 |

![](img/e862c5b60f9f55ef43a34453c49f252f_139_0.png)

图 4.8 `kmod` 客户端可用于查找和设置调制调器。当您设置新的点点协议（PPP）连接时，可以使用它查找并设置调制调器。点击 `kmod` 对话框中的“查询调制调器”按钮以搜索已安装的调制调器。

Red Hat Linux 为系统管理员提供了命令行诊断和串口配置工具。例如，要获取有关特定端口的更多信息，可以使用 `statserial` 命令配合指定的设备：

```
# statserial /dev/ttyS0
Device: /dev/ttyS0
```

按下回车键后，你会看到一个设置对话框。选择“串口配置”（Serial-Port Configuration）并按回车键。你将看到如图 4.9 所示的“配置设置”（Configuration Settings）对话框，可以使用它配置程序以连接外部调制调器。

![](img/e862c5b60f9f55ef43a34453c49f252f_143_0.png)

图 4.9 使用 minicom 的设置对话框配置程序以连接外部调制调器。

### 为笔记本配置无控制器调制调器

关于调制调器的其他问题涉及使用无控制器调制调器的 Red Hat 笔记本用户。这些调制调器使用专用软件模拟硬件调制调器。尽管发布了二进制驱动以启用这些设备，但这些设备仍然是 Linux 笔记本和桌面用户的痛苦。

你可能会找到对 Lucent（但不是 Lucent AMR）、Motorola SM56 型、IBM Wave 和 Conexant HSF（而非 HCF）控制器的支持。在本文编写时，尚未支持任何 3COM 或 U. Robotics 的无控制器调制调器。驱动程序链接和更多信息，请访问 http://www.linmodems.org Linux 调制调器网页。

## 在 Red Hat Linux 中配置电源管理

高级电源管理（APM）允许工作站和服务器在接收关闭指令时自动关闭。APM 通常由 Red Hat Linux 移动用户使用，通过使用智能存储单元电路、CPU“节流”（类似于但不同于 Intel 在 Pentium III 和 IV CPU 中内置的热节流）以及对显示器和硬盘的控制来延长电池使用时间。

大多数 PC 通过 BIOS 和硬件支持 APM。APM 支持经过配置后，会被整合到 Linux 内核中。

APM 信息在 `/proc/apm/` 文件中不断更新，如下所示：

```
# cat /proc/apm
1.14 1.12 0x03 0x01 0x03 0x09 100% 10800 sec
```

此示例提供了电池电量等信息，以及剩余的时间和百分比。示例从左到右依次是驱动程序版本、BIOS 版本、AC 状态、电池状态、电池状态、剩余寿命以及剩余秒数。一些 X1 客户端（如 `apm`、`apmload` 或 GkRell 客户端）会解析此文件并显示图标或图形电源 LED，以更易理解的方式呈现信息。这些客户端对笔记本用户特别有帮助。

所有 Red Hat 内核都支持 APM。然而，硬件问题或 APM 配置错误可能会导致某些硬件出现内核面板，从而导致无法启动 Linux。当发生这种情况时，你必须重新配置 APM 并编译安装一个新的 Linux 内核。（更多信息请参阅第 24 章。）

基础 Linux 内核 APM 选项包括：

- `CONFIG_APM_IGNORE_USER_SUSPEND`—不配置 APM 支持
- `CONFIG_APM_USER_SUSPEND`—忽略键盘挂起指令
- `CONFIG_APM_DO_ENABLE`—在启动时启用 APM
- `CONFIG_APM_CPU_IDLE`—不使用时让 CPU 进入空闲状态
- `CONFIG_APM_DISPLAY_BLANK`—启用显示器或 LCD 面板黑屏
- `CONFIG_APM_RTC_IS_GMT`—在使用 APM 期间允许中断（例如串口活动）
- `CONFIG_APM_REAL_MODE_POWER_OFF`—启用关机

Red Hat Linux 包含了几个与 APM 相关的命令——例如 `apm` 输出 APM 信息，`apsleep` 用于在特定时间挂起并唤醒硬件。Red Hat Linux 笔记本用户可以这样使用 `apm` 命令：

```
$ apm -v
APM BIOS 1.2 (kernel driver 1.16)
AC on-line, battery status high: 95%
```

![](img/e862c5b60f9f55ef43a34453c49f252f_144_0.png)

内核中整合的其他电源管理还包括对外设控制接口（PCI）设备的控制，以及对已启用显示器的显示电源管理信号（DPMS），这可以在预设后将设备置于低功耗状态来帮助节省成本。正如大多数精明的 Red Linux 系统管理员和用户所知，屏幕保护程序不再需要来保护设备免受图像“烧屏”。而且屏幕保护程序启用的密码保护仅提供有限的物理安全。

硬件监控由 `lm_sensors` 包支持，该包因早期版本导致 IBM ThinkPad 笔记本遭受永久性损坏而闻名。然而，管理桌面 PC 的系统管理员可以从应用程序受益，因为 `sensors` 命令利用了 `lm_sensors` 库的硬件监控功能。

你可以通过编辑（或根文件 `/etc/sensors.conf`，默认设置适用于你的计算机）来自定义 `sensors` 命令的输出。要启用传感器读取，使用 `sensors-detect` 命令确定加载哪些内核模块以启用传感器输出：

```
# /usr/bin/sensors-detect
此程序将帮助你确定最有效地需要加载哪些 I2C/SMBus 模块来运行 lm sensors。
你需要在执行 'make install'、'depmod -a' 并确保
/etc/conf.modules（或 '/etc/modules.conf'）包含适当的
模块路径后才能使用此工具的某些功能。阅读 doc/modules 获取更多信息。
此外，你可能是 'root' 权限，或者至少在某些时间拥有 /dev/i2c[-/-]* 文件。如果你还没有这些文件，可以使用 proc/mkdev/mkdev.sh 创建这些 /dev 文件。
如果你已经修复了内核并内置了驱动程序，在被要求加载某些模块时可以安全地回答 NO。在这种情况下，情况可能看起来混乱，但它们仍然可以工作。
```

> 如果是 IBM THINKPAD，现在立即按 CTRL-C！
>
> IBM Thinkpads 具有极其错误的 i2c/SMBus 实现，仅仅扫描总线就会导致你的 thinkpad 永久损坏！

我们可以从探测 (PCI) I2C 或 SMBus 适配器开始。

你不需要任何特殊权限。

现在要探测吗？(YES/NO):

输入 YES 并按回车开始（如果你是 IBM ThinkPad 笔记本，请不要这样做；请见 http://www.linux-thinkpad.org/）。该命令将开始对你的主板进行一系列探测并报告发现的结果。

## 重置日期和时间

Red Hat Linux 在安装期间询问你默认的时区设置，以及你的计算机硬件时钟是否设置为格林尼治标准时间（GMT）——更广为人知的 UTC，即协调世界时。

Linux 提供系统日期时间；你的计算机提供基于硬件时钟的时间。在许多情况下，两者可能会产生偏差。保持准确的时间不仅在单台工作站上很重要，在网络环境中也至关重要。备份、计划停机和其他网络范围内的活动需要精确协调。

Red Hat Linux 提供了多种可以在命令行或在 X 会话期间使用的日期和时间工具，包括以下：

- `date`—用于从命令行显示、设置或调整系统日期和时间
- `hwclock`—一个 root 用户命令，用于显示、设置、调整和同步硬件时钟与系统时钟
- `redhat-config`—一个图形化的日期、时间及网络时间配置工具

### 使用 date 命令

使用 `date` 命令显示或设置您的 Linux 系统时间。这要求您使用特定的数字序列来表示所需的日期和时间。要查看 Linux 系统认为的当前日期和时间，请如下所示使用 `date` 命令：

```
# date
Sun 22 15:53:19 EDT 2002
```

要调整您的系统时间（例如，设置为 2003 年 9 月 23 日上午 8 点），请使用命令行，格式如下（月、日、时、分和年）：

```
# date 092308002003
Tue Sep 23 08:00:00 EDT 2003
```

### 使用 hwclock 命令

使用 `hwclock` 显示或设置您的 Linux 系统时间、显示或设置 PC 的硬件时钟，或同步系统和硬件时间。要查看硬件日期和时间，如下所示使用 `--show` 选项 `hwclock`：

```
# hwclock --show
Sun Sep 22 03:59:58 PM EDT -0.71946 seconds
```

使用带有 `--set` 和 `--date` 选项 `hwclock` 手动设置硬件时钟：

```
# hwclock --set --date "09/23/03 08:00:00"
# hwclock --show
Tue Sep 23 08:00:08 AM EDT -0.151718 seconds
```
