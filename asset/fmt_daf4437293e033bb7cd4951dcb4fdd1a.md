
vend/prod 信息提供了关键。工程师在 Linux-USB 设备概览网站查询了 `0x047D` 和 `0x5003`，发现这就是 Kensington

摄像头使用 `se401` 驱动。在 USB 支持菜单中有一个用于 `se401` 的内核配置选项。在本节中，你将在 `tbdev1` 上执行以下步骤：

- 1. 为视频操作和 `se401` 配置内核。编译并安装内核，然后重启 `tbdev1`。
- 2. 连接 Kensington 摄像头。
- 3. 下载并编译一个名为 `vgrabjj` 的基于控制台的视频采集程序，并捕获一张视频静态图像。

> 提示
厂商和产品信息对标识了一个唯一的 USB 设备。设计通常授权给几家公司进行生产和销售。例如，两家公司可能提供基于相同硬件设计的 USB 摄像头。这些摄像头从电气角度来看是相同的，你可以使用相同的 USB 设备驱动程序。如果你无法通过名称找到 USB 设备的驱动信息，请使用厂商和产品信息对。

# 为视频操作和 se401 配置内核

要使用 Kensington 摄像头，你需要配置并重新构建支持视频和 `se401` 的内核。你需要遵循以下步骤：

- 1. 使用 `menuconfig` 配置视频和 `se401` 支持的内核
```
root@tbdev1[553]: cd /usr/src/linux
root@tbdev1[554]: make menuconfig
```

- 2. 你需要配置视频支持的内核选项。使用向上和向下箭头选择 `Multimedia devices` 项目并按回车。选择 `Video For Linux` 项目并按空格键，直到在 `<` 之间出现一个 `*` 字符（即 `<>`）。现在向下滚动到 `Video For Linux --->` 并按回车。在选了 `proc` 文件系统中的 V4L 信息 `NEW` 项后，使用空格键直到在 `[ ]` 之间出现一个 `*` 字符（即 `[!]`）。选择 `Exit` 并按回车。再次选择 `Exit` 并按回车。

- 3. 滚动到 `USB support` 项目并按回车。配置此额外的 USB 支持选项：`-> USB SE401 Camera support`。

使用左右箭头选择 `Exit`，然后按回车。这将返回主菜单。

- 4. 使用左右箭头选择 `Exit`，然后按回车。当询问是否保存内核配置时，选择 `Yes` 并按回车。

- 5. 使用此命令构建新内核：
```
root@tdbdev1[555]: make dep; make clean; make bzImage
```

- 6. 当内核编译完成后，将内核镜像拷贝到 `/boot` 目录并运行 `lilo`：
```
root@tdbdev1[556]: cp arch/i386/boot/bzImage /boot/usb/usbtest
root@tdbdev1[557]: lilo
Added Linux
Added usbtest
```

- 7. 重启并在 `lilo` 启动提示符处输入 `usbtest`。以 `root` 身份登录。

- 8. 使用此命令在 `/proc/bus/usb` 上挂载 `usbdevfs`：
```
root@tbbdev1[505]: mount -t usbdevfs usbdevfs /proc/bus/usb/
```

# 连接 Kensington 摄像头

按照以下步骤连接 Kensington 摄像头并检查内核提供的 USB 信息：

- 1. 插入摄像头并检查 `/proc/bus/usb/devices` 文件：
```
root@tbbdev1[506]: cat /proc/bus/usb/devices
S: Product=USB UHCI-alt Root Hub
S: SerialNumber=e000
S: Manufacturer=YAMAHA
S: Product=YAMAHA YST-350D Speaker
S: SerialNumber=Ser
C*: #Ifs 3 Cfg=#1 Atr=80 MxPwr=0mA
I: #If=0 Alt=0 #Eps=2 (audio) Sub-01 Prot=00 Driver=
P: Vendor=047d Atr=180 ProdID=5003 Rev=20.50
S: Product=VideoCAM
C*: #Ifs 1 Cfg=#1 Atr=80 MxPwr=500mA
```
这里有摄像头。

Linux 子系统找到了 Kensington VideoCAM 并加载了 `se401` 驱动。`se401` 设备需要配置 Video For Linux。该子系统创建了一个 `/proc/video` 项。如果你探索该目录，会发现这些项：
```
root@tbbdev1[515]: cd /proc/video/
root@tbbdev1[516]: ls
dev/se401/
root@tbbdev1[517]: cat /proc/video/video0
name: Kensington VideoCAM
type: VID_TYPE_CAPTURE
hardware: 0x1e
root@tbbdev1[518]: cat /proc/video/se401/video0
driver_version: 0.23
model: Kensington VideoCAM
use: no
streaming: no
button: no
button pressed: no
num_frames: 2
Sizes: 168x120 200x152 176x144 32x240 352x288 600x300 640x480 704x576 800x600
Frames total: 0
Frames read: 0
Packets dropped: 0
Decoding Errors: 0
```
摄像头！

- 2. 从摄像头获取图像。首先，你需要检查 `/dev` 目录下的 `video` 和 `video1` 设备。如果它们不存在，你需要创建它们：
```
root@tbbdev1[521]: ls
root@tbbdev1[521]: mknod -m 644 /dev/video0 b 0 0
root@tbbdev1[521]: ln -s /dev/video /dev/video1
root@tbbdev1[527]: ls
lrw-rw- 1 root Oct 7 20:42 /dev/video -> /dev/video1
crw-r-- 1 root Oct 7 20:42 /dev/video0
```

# 下载和编译控制台视频采集器

如果你使用 `cat /dev/video`，RGB 图像流将充满屏幕字符。这对你没有帮助。你可以使用一个名为 `vgrabjj` (`http://vgrabjj.ge.de`) 的程序将 RGB 流转换为 JPEG 图像。`vgrabjj` 允许你定期采集图像、在图像上叠加时间戳并以 JPEG 格式保存。以下是下载、编译和运行 `vgrabjj` 的步骤：

## 第8章 USB 接口

1. 获取 `vgrabjj` 的最新源码并在 `tbdev1` 上编译：
```
root@tbbdev1[51]: wget http://vgrabjj.gecius.dev/vgrabjj/vgrabjj-latest.tar.gz
root@tbbdev1[52]: tar xvf vgrabjj-latest.tar.gz
root@tbbdev1[53]: cd vgrabjj-0.7.4/
root@tbbdev1[54]: ./configure
```
`lines removed`
`checking for jpeg_set_defaults in -ljpeg... no`
`configure error: *** jpeg library not found!`
请安装相应的库

你可以看到 `tbdev1` 缺少一些库。`vgrabjj` 需要这些库及其头文件：`libjpeg`, `libpng`, `freetype`。你需要在 `tbdev1` 上安装它们并重新运行 `vgrabjj configure`：

```
root@tbbdev1[550]: apt-install libjpeg62-dev

root@tbbdev1[551]: apt-install libpng2-dev

root@tbbdev1[552]: apt-install freetype2-dev

root@tbbdev1[553]: ../configure

root@tbbdev1[556]: make

gcc -DHAVE_CONFIG_H -I. -I. -g -O2 -Wall -c vgrabjj.c

gcc -DHAVE_CONFIG_H -I. -I. -g -O2 -Wall -c font.c

gcc -DHAVE_CONFIG_H -I. -I. -g -O2 -Wall -c ccvt_c.c

gcc -O2 -Wall -o vgrabjj
```

2. 运行 `vgrabjj` 查看获取的结果：
```
root@tbbdev1[558]: vgrabjj -f /tmp/a.jpg -e
Reading image from /dev/video
root@tbbdev1[559]: ls /tmp/a.jpg
-rw-r--r-- 1 root Oct 7 20:42 /tmp/a.jpg
```

3. `vgrabjj` 程序有许多功能，如时间戳、图像叠加和间隔。表 8.1 详细解释了这些命令行参数。

| 命令行选项 | 说明 |
|---|---|
| `-e` | 启用时间戳 |
| `-i vga` | 将图像大小设为 640×480 |
| `-f` | 写入输出文件而不是标准输出 |
| `-p` | 定义叠加格式 |
| `-T` | 设置叠加大小 |
| `-a` | 设置叠加在图像上的对齐 |
| `-m` | 设置叠加与原始图像的混合 |
| `-1 30` | 告诉 `vgrabjj` 守护进程并每 30 秒写入一张图像 |

# 为 SCSI 操作和 SDDR-09 使用配置内核

要使用 SanDisk（闪迪）USB SmartMedia 读卡器，你需要配置并重新编译支持 SCSI 和 SDDR-09 的内核。请按照以下步骤配置并编译内核：

- 1. 通过执行 `menuconfig` 配置具有 SCSI 和 SDDR-09 支持的内核
```
root@tbdev1[553]: cd /usr/src/linux
root@tbdev1[554]: make menuconfig
```

- 2. 你需要配置用于 SCSI 支持的内核选项。使用向上和向下箭头键滚动到 `SCSI support` 项目并按回车。选择 `SCSI support` 项目并按空格键，直到 `>` 之间出现一个 `*` 字符（即 `<>`）。选择并配置这三个 SCSI 支持项：
- `<*> SCSI support`
- `<*> SCSI disk support`
- `<*> SCSI generic support`

选择 `Exit`（退出）并按回车。这将带你回到主菜单。

- 3. 现在考虑 SDDR-09 驱动程序。除非你配置内核提示开发驱动程序，否则你不会在 `USB support` 项目中看到它的选项。使用向上和向下箭头键滚动到 `Code Maturity Level` 选项并按回车。选择 `Prompt for Development and/or Incomplete Code/Drivers` 项目并按空格键，直到 `<>` 之间出现一个 `*` 字符。选择 `Exit` 并按回车。这将带你回到主菜单。

- 4. 配置 USB 支持选项。使用向上和向下箭头键滚动到 `USB support` 项目并按回车。配置这些 USB 支持项：
- `<*> Mass Storage support`
- `[*] SanDisk SDDR-09 (and other SmartMedia) support (NEW)`

选择 `Exit` 并按回车。这将带你回到主菜单。

- 5. SmartMedia 卡使用 DOS FAT 文件系统。你需要配置内核以支持 DOS FAT 文件系统。使用向上和向下箭头键滚动到 `File Systems` 项目并按回车。配置这些文件系统项：
- `<*> DOS fs support`
- `<*> MSDOS fs support`

选择 `Exit` 并按回车。这将带你回到主菜单。

## 第 8 章 USB 接口

6. 使用左右方向键选择 `Exit`，然后按回车。当系统询问是否要保存内核配置时，选择 `Yes` 并按回车。

7. 使用此构建新内核：
```
root@tbdev1[555]: make dep; make clean; make bImage
```

8. 内核构建完成后，将内核镜像拷贝到 `/boot` 目录并运行 `lilo`
```
root@tbdev1[556]: cp arch/i386/boot/bzImage /boot/usbst
root@tbdev1[557]: lilo
Added Linux *
Added usbst
```

9. 重启并在 `lilo` 启动提示符处使用 `usbst`。以 `root` 身份登录。

10. 使用此命令在 `/proc/bus/usb` 上挂载 `usbdevfs`：
```
root@tbdev1[501]: mount -t usbdevfs usbdevfs /proc/bus/usb/
```

### 连接 SanDisk USB SmartMedia 读卡器

按照以下步骤检查 SanDisk USB SmartMedia 读卡器并检查内核提供的 USB 信息：

- 1. 插入 SmartMedia 读卡器并检查 `/proc/bus/usb/devices` 文件：
```
root@tbdev1[508]: cat /proc/bus/usb/devices
s: Product=USB UHCI-alt Root Hub
s: SerialNumber=e000
s: Manufacturer=YAMAHA
s: Product=YAMAHA YST-MS35D USB Speaker
s: SerialNumber=Ser 0 em
s: Manufacturer=SanDisk
s: Product=USB SSFDC
c*: #Ifs=1 Cfg=1 Atr-a0 MxPwr=10mA
i: If=# 0 Alt=0 #Eps=3 Cl=ff(vend.) Sub=01 Prot=01 Driver=usb-storage
```

- 2. 子系统找到了 SmartMedia 读卡器、USB SSDFC，并为它加载了 `usb-storage` 驱动程序。`proc` 目录现在有几个 SCSI 条目，系统日志文件也包含了相关信息：
```
root@tbdev1[518]: cat /proc/scsi/scsi
Attached devices:
Host: scsi Channel: 00 Id: 00 Lun: 00
Vendor: SanDisk Model: ImageMate SDDR-0 Rev: 0208
```
Project Trailblazer USB Hardware 223
Type: Direct-Access ANSI SCSI revision: 02

```
root@tbdev1[519]: cat /proc/scsi/usb-storage-0/0
Host scsi0: usb-storage
Vendor: SanDisk
Product: USB SSFDC
Serial Number: None
Protocol: Transparent SCSI
Transport: EUSB/SDRR09
GUID: 078102200000000
```
