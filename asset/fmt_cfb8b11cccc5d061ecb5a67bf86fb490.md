
`source=kismet_drone,192.168.1.220:3501,drone2`

一旦你执行了这些更改，你就可以启动 Kismet 客户端（在你的 Kismet 服务器安装上或另一台独立的 PC 上），并通过网络连接到无人机。图 6.4 显示了一个示例。

## 图 6.4 连接到 Kismet 无人机的 Kismet

![](img/41991837f74596e7c29a2498b6ec56e8_256_0.png)

地下的随记……

# 在 WRT54G 上使用 Kismet 监测信号强度

你部署多个 Kismet 无人机的原因之一是监控非法接入点。非法接入点是可能安装在你环境中的无线接入点，它们是未经许可的，并且可能为你的网络提供未经授权的访问。

确定非法接入点位置的最佳方法之一，是确定 Kismet 无人机观察到的信号强度。遗憾的是，Broadcom 提供的闭源无线驱动程序并不提供可用的信号信息！这为使用 Kismet 无人机定位非法接入点制造了困难。

虽然仍然可以利用 Kismet 定位接入点，但过程会迅速变得复杂。至少，在 WRT54G 路由器上的 Kismet 无人机结合中央服务器，以及一台带有定向天线的笔记本电脑，是一种有效的方法。

继续

## 第 6 章 • 针对渗透测试者的 WRT54G

关于如何使用 Kismet、Kismet 无人机和 WRT54G 路由器定位非法接入点的更多信息，可以参考 SANS Reading Room 中的一篇论文，地址为：www.sans.org/reading_room/whitepapers/honors/1671.php。

# WRT54G 远程蓝牙扫描器

蓝牙扫描对于无线渗透测试人员来说日益重要，因为它用于蓝牙设备上。带有蓝牙的设备处理各种信息：手机有通话和电话录，键盘用于传输密码和财务信息，而蓝牙耳机则传输音频通信。这些类型的信息对攻击者来说非常有价值，而且蓝牙设备正通过空中传输这些信息。

蓝牙旨在作为一种短距离无线技术，范围在 1–100 米之间，取决于蓝牙设备的等级。这本应限制攻击者拦截传输的范围；然而，一组黑客已利用廉价硬件实现了超过一英里距离的蓝牙连接！蓝牙使用的 2.4GHz 频率与 Wi-Fi 相同，且两种技术在设计上是可以交换的。

> 注意：有关蓝牙的更多信息（包括协议信息、频率和距离信息），请查看 Wikipedia 词目：http://en.wikipedia.org/wiki/Bluetooth。你可以在 http://wifinite.org/bluetooth_stuff.html 和 www.smallnetbuilder.com/content/view 找到更多关于远程蓝牙连接的信息。由于 WRT54G 具有通用串行总（USB）端口，我们将在 WRT54G 上进行此攻击。我们将使用第三方 USB 适配器执行扫描。

# 关于蓝牙适配器

我们选择用于此次攻击的 USB 适配器是 Linksys USB100，如图 6.5 所示，它默认情况下可以通信达 100 米。该适配器具有外部天线；但它已被替换为根电缆和一个 RP-SMA 接口。我们还将适配器与一个 dB 全向天线连接。现在，由于模块化设计，我们可以根据需要从不同的天线中选择。img/41991837f74596e7c29a2498b6ec56e8_256_0.png

## 图 6.5 修改后的 Linksys 适配器

img/41991837f74596e7c29a2498b6ec56e8_256_0.png

> 提示：为了获取蓝牙的更多信息（包括协议信息、频率和距离信息），请检查 Wikipedia 词目：http://en.wikipedia.org/wiki/Bluetooth。你可以在 http://wifinite.org/bluetooth_stuff.html 和 www.smallnetbuilder.com/content/view 找到更多关于远程蓝牙连接的信息。由于 WRT54G 具有通用串行总（USB）端口，我们将在 WRT54G 上进行此攻击。我们将使用第三方 USB 适配器执行扫描。

（后略）

# 配置 USB 蓝牙适配器

在插入并使用 USB 蓝牙适配器之前，你需要修改一些系统配置，因为其中一个模块在重启后不会自动安装，这是蓝牙适配器运行所必需的。你需要安装适当的驱动程序。首先，你需要安装通用的蓝牙内核模块以及 USB 蓝牙控制器（HCI）的内核模块，来自 OpenWrt 软件包树：

```
# ipkg install kmod-bluetooth kmod-bluetooth-hciusb
```

你还需要安装 `bluez` 软件包中的蓝牙工具。遗憾的是，`bluez` 软件包不在默认的 OpenWrt 回源树中。为了添加这些包，你需要更新 `/etc/ipkg.conf` 以包含额外的仓库：在 `/etc/ipkg.conf` 中添加如下 `src` 指令：

```
src backports http://downloads.openwrt.org/backports/0.9/
```

此额外的源提供了一个描述性名称（`backports`），并提供了包含 BlueZ 工具的新仓库位置。为了安装 BlueZ 工具，你需要确保更新了软件包数据库以添加来自新 `backports` 仓库的项：

```
## ipkg update
# ipkg install bluez-utils
```

# 渗透测试者的 WRT54G • 第 6 章

`hci_usb` 模块将通过 USB 端口或其与蓝牙适配器的依赖项初始化蓝牙 HCI。这种交互在蓝牙设备发现方面极其重要。为了完成 HCI 安装，你需要确保 HCI 守护进程已经启动，并且在 `/etc/init.d` 下的启动项中启动，通过创建一个包含如下内容的 `S70hid` 文件来实现：

```
#!/bin/sh

/usr/sbin/hcid
```

你还需要使用以下命令将 `S70hid` 设为可执行文件：
```
# chmod 755 S70hid
```

在完成所有这些步骤后，你应该对 WRTLS54GS 进行完全重启，以验证你的所有模块和守护进程已启动。执行 `insmod` 命令，输出应反映出你所有的新模块及其依赖项，如下代码所示，包括 `bluez`, `hci_usb`, `l2cap`, `rfcomm`, `sco`, `usb-hci` 和 `uscore`：

| 模块 (Module) | 大小 (Size) | 已用 (Used) | 污染 (Tainted) |
|---|---|---|---|
| usserial | 24140 | 0 | |
| hci_usb | 10520 | 1 | |
| usb-hci | 19236 | 0 | (unused) |
| uscore | 74792 | 1 | [uscore hci_usb usb-hci] |
| sco | 10196 | 0 | (unused) |
| rfcomm | 35128 | 0 | (unused) |
| l2cap | 18524 | 1 | [rfcomm] |
| bluez | 38936 | 3 | [hci_usb sco rfcomm l2cap] |
| wlcompat | 14896 | 0 | (unused) |
| wl | 423640 | 0 | (unused) |
| switch-robo | 4444 | 0 | [switch-robo] |
| diag | 3320 | 0 | (unused) |

## 使用 USB 蓝牙适配器发现设备

早些，你安装了 `bluez-utils` 包以使你的蓝牙设备能够在你的 WRTLS54GS 上工作。`bluez-utils` 包包含了一些对扫描蓝牙设备非常有用的实用工具。除了扫描工具外，还有一些利用蓝牙设备某些功能的其他工具，例如拨号上网、文件传输和语音通信。在这种情况下，我们主要感兴趣的是使用扫描工具进行渗透测试。

你需要执行的第一步是定位一些蓝牙设备。你可以使用 `bluez-utils` 包中包含的 `hcitool` 做到这一点。如下所示，你可以使用以下命令启动蓝牙设备扫描：

![](img/41991837f74596e7c29a2498b6ec56e8_260_0.png)

# 第 6 章 • 渗透测试者的 WRT54G

```
# hcitool scan
Scanning ...
00:0F:86:34:8C:0A      BlackBerry 7520
00:16:20:E8:A0:92      Z520a
00:16:CB:8F:29:0C      NORAD
```

在扫描输出中，我们得到了三个蓝牙设备的列表，其带有 MAC 地址（或 *haddr*）和设备名称。一旦你确定了 *haddr*，你就可以使用 *hcitool info* 获取有关该设备的更多信息，如下针对 NORAD 设备的简短输出：

```
# hcitool info 00:16:CB:8F:29:0C
Requesting information ...
BD Address: 00:16:CB:8F:29:0C
Device Name: NORAD
```
