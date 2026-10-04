
# 网络配置与无线设置

## 接口配置文件示例

```
iface wlan0 inet manual
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```

这些行分别对应 loopback 和 eth0 设备，并提供了关于它们管理的简单详情；在这种情况下，loopback 是自动管理的环回设备，eth0 设备通过 DHCP 分配 IP 地址。对于你的 wlan0 设备，可能存在一些现有的配置；如果存在，你应该通过在前面添加 `#` 将其注释掉，或者从文件中删除。你现在需要为 wlan0 无线设备添加一个新的配置，所以请将以下内容添加到配置现有内容的下方：

```
auto wlan0
iface wlan0 inet dhcp
wpa-ssid <Your WiFi SSID>
wpa-psk <Your WiFi password>
```

此区块表示你将拥有一个自动管理的 wlan0 设备，该设备通过 DHCP 获取连接。你还传递了 SSID 和 PSK。此配置适用于 WPA 和 WPA2 网络安全实现。完成后，是时候测试你的网络了，请继续运行以下命令，这将启动接口。这可能需要几秒钟，但你的输出应该类似于：

```
$ sudo ifdown wlan0
$ ifup wlan0
Internet Systems Consortium DHCP Client 4.2.2
Copyright 2004-2011 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/wlan0/90:94:e5:81:7a
Sending on LPF/wlan0/90:94:e5:81:7a
Sending on Socket/fallback
DHCPDISCOVER on wlan0 to 255.255.255.255 port 67 interval 8
DHCPDISCOVER on wlan0 to 255.255.255.255 port 67 interval 15
DHCPDISCOVER on wlan0 to 255.255.255.255 port 67 interval 9
DHCPREQUEST on wlan0 to 255.255.255.255 port 67
DHCPPOFFER from wlan0 to 10.0.0.1
DHCPACK from 10.0.0.1 -- renewal in 44671 seconds.
```

这一切表明该设备已连接到你的无线网络，并通过 DHCP 获取了 IP 地址，这恰恰是你不想使用 DHCP 而是想为你的 WiFi 适配器分配静态 IP 地址的情况。你只需要将接口行改为 `static` 而不是 `dhcp`，并添加 IP 地址、子网掩码和网关的详情。你的配置看起来像这样：

既然你现在已经在系统上成功配置了无线网络，可以重启 Pi 以检查无线适配器是否启动。如果没有，请返回并确保你在 NetworkManager 配置文件中设置了 `auto=false` 标志。

如果不起作用，请检查你的 SSID 和 WiFi 密码设置。你可以通过 `ifup wlan0` 是否可以启动无线适配器；如果连接和获取 IP 地址时出现问题，系统应该显示这些问题，让你有机会找出问题所在。最后，如果你仍然无法让它运行，请尝试移除任何其他连接的 USB 设备；它们会消耗掉 WiFi 适配器的宝贵电源。

命令行中可能对你有帮助的最后是 `iw` 系列命令：

- 你可以使用 `iwlist` 配合 `scan` 选项来获取附近无线热点的扫描信息。
- 或者你可以使用 `iwconfig` 获取有关你无线适配器的配置详情。

## 仅剩一根线

恭喜，你正在迈向全无线树莓派之旅！你已成功消除了对以太网线的需求，现在可以通过无线方式访问你的 Pi 了。现在应该只剩一根线了！（参见图 9-10。）

![](img/0e6e6125cff2ec21b011df8d1f7a8ec1_207_0.png)

图 9-10. 最后一根电源线

## 消除对电源的需求

对于树莓派对电源的需求，你几乎无事可以捷径；它需要电源，而且解决这个方法的方案有限的。到目前为止，最简单方便的方法是获取一个大型 USB 电池。这些电池现在随处可见，用于为人们经常携带的许多设备充电。这里的简单解决方案是将你的 Pi 连接到其中一个电池上使用，因为这种电池应该保证为 Pi 提供正确的功率输出——因为它们的设计就是为 USB 设备供电。在寻找为 Pi 供电的电池时，重要的是确保它们能提供全 1 安培功率，因为某些 USB 电池虽然可以充电，但电量不足以驱动 Pi。图 9-11 显示了最终的 WiFi。

![](img/0e6e6125cff2ec21b011df8d1f7a8ec1_207_1.png)

图 9-11. 终于实现了 WiPi！

市面上有一些结合充电电池和太阳能电池板的黑科技，可以让你走得更远，但那些已超出了本书的范围。

## 带电 USB 适配器

我之前提到过，如果你给 Pi 的 USB 施加过大负载，可能会导致它崩溃，因为它自带的电源有限。解决方案是获取一个带电 USB 集线器。这些带电集线器通常有一个输出连接和多个输入连接，还有一个用于供电的市电连接。其原理是人们很少使用 USB 的全部数据传输量，但会耗尽电源，因此通过市电电源为 USB 设备补充电源，是为人们的设备提供更多灵活性的好方法。如果你发现连接设备时 Pi 自动关机了，那么很有可能需要像这样的设备来帮助分担负载（参见图 9-12）。

![](img/0e6e6125cff2ec21b011df8d1f7a8ec1_208_0.png)

图 9-12. 带电集线器的作用

# 第 10 章 树莓派

## 所需材料

- 1x 树莓派
- 1x USB 线（用于电源）
- 1x 以太网
- 1x 摄像头
- 1x SD 卡

## 启动日志分析

```
1.998581 Waiting for root device /dev/mmcblk0p2...
0.071268 mmc0: new boot SD card at address 7d37
0.079917 mmcblk0:7d37 SD02G 1.88 GIB
0.208723 mmcblk0:p1 p2
1.332278 EXT4-fs (mmcblk0p2): mounted filesystem with ordered data mode. Opts: (null)
2.154275 VFS: Mounted root (filesystem) on 179:2.
2.155272 Free init memory: 200K
2.187333 usb-1: new high speed USB device number 2 using dc_otg
2.418045 usb-1: new USB device, idvendor=0424, idproduct=9512
2.427750 usb-1: new USB device strings: Mfr=0, Prod=0, SerialNumber=0
2.436808 usb-1:1.1.0: USB hub bound
2.445041 usb-1:1.1.0: 3 ports detected
2.727674 usb-1: new high speed USB device 3 using dc_otg
2.837059 usb-1: new USB device, idvendor=0424, idproduct=ec00
2.857413 usb-1: new USB device strings: Mfr=0, Prod=0, SerialNumber=0
2.878965 smsc95xs:1.1.1.0: ethno: register 'smsc95xs' at usb-bcm2708-usb_1.1, smsc95xs
2.942985 smsc95xs:1.1.1.0: ethno
USB 2.0 Ethernet, b27:eb:aa64:a6
11.006171 EXT4-fs (/mmcblk0p2): re-mounted. Opts: (null)
11.429660 ### snd_bcm2835_alsa_probe c5c88e0############# PROB FOR bcm2835 ALSA device(0):1###########
11.442869 Creating...
11.448269 Creating device/chip
11.457711 Adding controls
1.460340 bcm2835 ALSA card CREATED!
11.475463 ### BCM2835 ALSA driver init OK ####
11.487786
19.483739 smsc95xs:1.1.0.0: eth: link up, 100Mbps, full-duplex, lpa 0x45E1
24.673222 Adding swap on /var/swap. Priority:-1 extents:1 across:102396k S
```

如你所见，`dmesg` 的输出并不令人振奋，而且难以理解。这些信息依赖于对 `dmesg` 系统如何运作的理解。首先是方括号 `[ ]` 中的数值。这是一个计时器值，记录了自系统启动以来经过的时间。这是跟踪系统中事件发生顺序、以及将近期事件与过去发生的事件区分开来的好方法。

接下来的内容本身显然毫无用，但它们共同构成了一幅非常有趣的画面，展示了我的树莓派上到底发生了什么。让我们从第一行开始：等待设备 `/dev/mmcblk0p2`。前几行是：系统正在等待某些东西，但 `/dev/mmcblk0p2` 是什么？嗯，第一个线索是 Linux 操作系统列出了我们知道的所有设备 `/dev/mmcblk0p2`，它看起来像是一个字符串，但实际上是一系列异常。我们正在等待 SD 卡。第二到第四行是我们正在等待的内容，顺序如下：

- `mmcblk` 表示存储设备
- `blk` 表示第一个逻辑设备
- `p2` 表示该设备的根分区

接下来的两行是将该设备上的文件系统挂载到该设备上并设置为可读。继续向下看，你可以看到树莓派设备的注册（8-15）、以太网口（16-17），最后是一个高级音频架构（ALSA）设备，即音频端口（19-25）。既然你理解了为什么我们没有连接摄像头，我想让你查看 `dmesg` 的输出。尽管去连接你的摄像头并再次运行 `dmesg`。这是我们新连接的摄像头的输出：

```
[1869.79323] usb 1-2: high speed USB number 4 using dc_otg
[1869.147691] usb 1-2: New USB device, idvendor=0424, idproduct=081d
[1869.147736] usb 1-2: New device strings: Mfr=0, Prod=0, SerialNumber=0
[1869.147758] usb 1-2: Serial Number: 86fac4
[1869.314171] usb 1-2: Linux video interface: v2.0
[1869.336421] UVC: Found UVC 1.0 device <046d:08d>
[1869.336421] UVC: Input: Camera (046d:08d) as /devices/bcm2708/usb1/1-1/1.2
[1869.402280] uscore: registered interface uvcvideo
[1869.402299] USB Class driver (UVC)
[1869.406093] uscore: registered interface snd-audio
```

这些行有什么用？首先，你可以看到 `dmesg` 中该特定条目的时间差异，这代表了启动所需的时间。接下来，前四行代表 USB 端口插入了一个新设备；此外，第一行代表用于此设备的 `dwc_otg`。第五行显示 `uvcvideo` 注册了 USB 类（UVC）设备。最后，我们还可以看到麦克风也注册为最后行的 `snd-audio` 设备。通过这一点，我们可以看到摄像头已经连接并与操作系统注册了驱动程序。

既然设备已经注册，我们需要一种方法来引用它，以便应用程序可以使用。现在 `dmesg` 输出立即指定了我们添加的设备，让我们看看是否匹配。让我们列出 `/dev` 的内容（见图 10-2）。

```
$ udev info -q -a -n /dev/video0
P: /devices/platform/bcm2708_usb/usb1/1-1/1.2:1.2:1.2:video4linux/video0
N: video0
S: v1/by-id-usb-046d.081d.86274C0-video-index0
S: v1/by-path-platform-bcm2708_usb-0:1.2:1.2-video-index0
E: DEVLINKS=/dev/by-id-usb-046d-081d_86274C0-video-index0
E: /dev/by-path-platform-bcm2708_usb-0:1.2:1.2-video-index0
E: DEVNAME=dev/video0
E: DEVPATH=/devices/platform/bcm2708_usb/usb1/1-1/1.2:1.2:1.2:video4linux/video0
E: ID_BUS=usb
E: ID_MODEL=081d
E: ID_MODEL_ENC=081d
E: ID_PATH=platform-bcm2708_usb-0:1.2:1.2
E: ID_TAG=platform-bcm2708_usb-0:1.2:1.2
E: ID_REVISION=001
E: ID_SERIAL=046d.081d.86274C0
E: ID_SERIAL_SHORT=86274C0
E: ID_TYPE=video
E: ID_DRIVER=uvcvideo
E: ID_INTERFACES=0
E: ID_INTERFACE_NUM=0
E: ID_VAL_CAPABILITIES
E: ID_VAL_PRODUCT=Camera (046d:081d)
E: ID_VAL_VERSION=2
E: ID_VENDOR=046d
E: ID_VENDOR_ENC=046d
E: ID_VENDOR_ID=046d
E: MAJOR=8
E: MINOR=0
E: SUBSYSTEM=video4linux
E: TAGS=udev
E: USB_LOG=3
E: USB_INITIALIZED=1
```

好的，这看起来有点吓人。正如我确定你现在猜到的，我们只是要求 `udev` 系统为我们提供与设备名称 `/dev/video0` 相关的所有查询，我们实际上只需要查看前几行。第一行的输出就是我们在 `dmesg` 中看到的标识符！事实上，这里的大部分信息都是 `dmesg` 中某处引用的数据。好的，我们认为这是对的——但我们如何判断呢？`udev`，具体来说是 `dev` 管理 Linux 内核的设备管理器。它知道设备注册在哪里，以便被应用程序访问。在 Debian（以及树莓派）中，可以使用 `udev` 命令访问 `udev` 的内部工作机制。

图 10-2. `/dev` 目录的内容

这里是一些设备。我们可以快速排除掉：所有 `tty` 设备、所有 `ram` 设备（因为它们是树莓派的内存）、所有 `loop` 设备（因为它们是 SD 卡），以及所有 `video` 设备（因为它们是虚拟控制台）。仍然有一些，最好的就是 `video0`。对于摄像头，它注册为视频设备，不是吗？

## 故障排除

如果摄像头在 `dmesg` 中注册时出现问题（与我的情况不同），可能需要安装驱动程序。如果我的摄像头没有列出，那是对的。

好的，这看起来有点吓人。事实上，这里的大部分信息都是在 `dmesg` 中某处引用的数据。好的，现在 `dmesg` 输出立即指定设备，让我们看看它是匹配的。

## 树莓派 SPI

摄像头上的灯在动作时亮起！开始挥手和移动，因为你想让它捕捉到你！

- [1] 变化: 3374 - 噪声水平: 15
- [1] 变化: 3198 - 噪声水平: 15
- [1] 变化: 3011 - 噪声水平: 15
- [1] 变化: 2922 - 噪声水平: 15
- [1] 变化: 2555 - 噪声水平: 15
- [1] 变化: 2390 - 噪声水平: 15
- [1] 变化: 2491 - 噪声水平: 15
- [1] 变化: 2874 - 噪声水平: 15
- [1] 变化: 2817 - 噪声水平: 15
