
# 第 6 章 支持与常见问题

如果网络正常但无法加载网站，可能是 DNS 服务器有问题，它们负责将如 google.com 这样的域名转换为 IP 地址。要测试这一点，你需要一个 IP 地址。你可能会从 ISP 获得一些 IP 地址。或者，你可以使用另一台电脑找到一个 IP 进行测试。尝试 `ping` 该地址，如果有响应，说明是名称服务器问题。要解决这个问题，请在 DNS 选项卡中指定正确的名称服务器。

## 如何使用 SSH 跨网络传输文件？

安全 Shell (SSH) 是一种安全连接远程计算机的协议。要在客户端连接远程计算机，请点击 位置 > 连接到服务器，并选择 SSH 作为服务类型。在第一个字段输入主机名或 IP 地址。在第二个字段输入用户名。在第三个字段输入密码。点击连接。现在你已连接到远程计算机。

要传输文件，可以使用 `scp` 命令。例如，将文件从本地复制到远程计算机：

```
scp filename user@remote_host:/path/to/destination/
```

将文件从远程计算机复制到本地：

```
scp user@remote_host:/path/to/file /local/destination/
```

或者，可以使用 `sftp`，它提供了一个用于文件传输的交互式 shell。要启动，输入：

```
sftp user@remote_host
```

连接后，你可以使用 `put` 命令上传文件并使用 `get` 命令下载文件。

你使用的是哪种无线卡。要确定这一点，你需要安装 `gnome-device-manager` 软件包，然后运行“应用程序 > 系统工具 > 设备管理器”（如图 6-6 所示），并寻找你的无线卡。它可能会显示 Wireless 或802.11a、b 或 g，或者可能是 WLAN。

找到网卡类型后，你需要启用驱动程序。这可能涉及编译代码，也可以简单地启用 Ubuntu 中已有的驱动程序。请查看 Ubuntu 论坛或在 Google 上搜索此类信息。

确定网卡类型后，你现在需要建立连接，正如我们在问题开头所解释的那样。

更多信息，请参阅 `https://wiki.ubuntu.com/HardwareSupportComponentsWirelessNetworkCards`。

![](img/aa15f1f82061fdaf4ff1da575e3e1c52_251_0.png)

图 6-6 HAL 设备管理器是一个用于显示管理硬件（包括无线卡）信息的工具。

## 我的无线接入点需要使用 WPA 或 WPA-PSK

对于大多数网卡，使用 WPA 所需的只需连接到接入点。Network Manager 会检测 WPA 设置并完成其余工作。一些较旧的无线卡可能不支持 WPA。检查你的网卡是否列在 WPA Supplicant 网站（`http://hostap.epest.fi/wpa_supplicant`）。在 Ubuntu 下支持 WPA 的常见网卡包括各种 Broadcom（博通）、Atheros 和 Intel（英特）芯片组。

## 硬件

计算机可以使用许多不同的硬件，包括摄像头、网卡、硬盘、显卡、声卡等。为了让这些设备正常工作，Linux 内核需要加载驱动程序。与 Windows 等系统不同，你不需要安装设备自带的特殊驱动程序。相反，驱动程序应该已经包含在 Ubuntu 中并可以开箱即用。

当然，情况并非总是如此，有时硬件运行起来非常棘手。在本节中，我们将剖析一些与硬件相关的问题并尝试解决它们。

## Ubuntu 没有检测到我的旧声卡

许多旧设备不会被当前的 2.6 内核序列自动检测。这样做是为了避免硬件问题导致崩溃。遗憾的是，如果你有一张旧声卡，意味着你需要卷起袖子仔细研究才能让它运行。要做到这一点，你需要知道你的卡需要哪个内核模块然后加载该模块。为你的设备加载正确的模块不会导致系统崩溃，但加载错误的模块很可能会导致这种情况。你可能需要尝试不同的模块。

可以通过参考电脑的规格说明、检查 Windows 中的设备名称（如果适用）或打开电脑机箱查看声卡芯片来查找你拥有的声卡型号。你可以使用 Google 将芯片序列号与芯片组类型进行匹配。以下是设备及其相关内核模块列表（取自 `www.icewalkers.com/Linux/Howto/BootPrompt-HOWTO-8.html`）：

- `snd-dummy` = 虚拟声卡
- `snd-mpu401` = mpu401 UART
- `snd-mtpav` = MOTU Midi Timepiece
- `snd-serial` = Serial UART 16450/16550 MIDI
- `snd-virmidi` = 用于虚拟 rawmidi 设备的虚拟声卡
- `snd-ad1816a` = ADI SoundPort AD1816A
- `snd-ad1848` = AD1848/AD1847/CS4248 的通用驱动
- `snd-als100` = Avance Logic ALS100
- `snd-azt2320` = Aztec Systems AZT2320 (以及 2316)
- `snd-cmi8330` = C-Media 的 CM18330
- `snd-cs4231` = CS4231 芯片的通用驱动
- `snd-cs4232` = CS4232 芯片的通用驱动
- `snd-cs4236` = CS4235/6/7/8/9 芯片的通用驱动
- `snd-dt019x` = Diamond Technologies DT-019x
- `snd-es1688` = 通用 ESS AudioDrive ESx688
- `snd-es18xx` = 通用 ESS AudioDrive ES18xx
- `snd-gusclassic` = Gus Classic
- `snd-gusetreme` = Gus Extreme
- `snd-gusmax` = Gus Max
- `snd-interwave` = Interwave
- `snd-interwave-stb` = Interwave
- `snd-opl3sa2` = Yamaha OPL3SA2
- `snd-opti93x` = 基于 Opti 82c93x 的网卡
- `snd-opti92x-cs4231` = Opti 82c92x/CS4231
- `snd-opti92x-ad1848` = Opti 82c92x/AD1848
- `snd-cs9968` = ESS AudioDrive ES9968
- `snd-sb16` = SoundBlaster 16
- `snd-sbawe` = SoundBlaster 16 AWE
- `snd-sb816` = SoundBlaster 816

## 我的 USB 适配器未识别

## 插入 USB 盘后什么也没有发生

- 热插拔时挂载移动驱动器
- 插入时挂载移动介质
- 插入时浏览移动介质
