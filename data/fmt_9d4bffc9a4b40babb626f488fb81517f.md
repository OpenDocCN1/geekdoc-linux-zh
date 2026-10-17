
# Project Trailblazer USB Hardware 217

## dev/se401/

```
root@tbdev1[517]: cat /proc/video/dev/video0
name : Kensington VideoCAM 67016
type : VID_TYPE_CAPTURE
hardware : 0x1e
```

```
root@tbdev1[518]: cat /proc/video/se401/video
driver_version : 0.23
model : Kensington VideoCAM 67016
inuse : no
streaming : no
button state : no
button pressed : no
num_frames : 2
Sizes : 160x120 200x152 176x144
-320x240 352x288 400x300 640x480 704x576 800x600
Frames total : 0
Frames read : 0
Packets dropped : 0
Errors : 0
```

### 2. 从摄像头获取图像

首先，你需要检查 `/dev/` 中的这些 `video` 和 `video0` 条目。如果没有，你需要创建它们：

```
root@tbdev1[521]: ls -l /dev*
root@tbdev1[522]: mknod -m 644 /dev/video0
root@tbdev1[521]: ln -s video0 /dev/video
root@tbdev1[527]: ls -l /dev
lrwxrwxrwx 1 root Oct 7 42 -> video0
crw-r-- 1 root Oct 7 video
```

## 下载并编译控制台捕获器

如果你使用 `/dev/video`，RGB 流将填满屏幕。你可以使用一个名为 `vgrabbj` (http://vgrabbj.de) 的程序将 RGB 流转换为 JPEG 图像。`vgrabbj` 允许你定期捕获图像、在图像叠加时间戳并以 JPEG 格式保存。以下是下载、编译和运行 `vgrabbj` 的步骤：

### 1. 在 tbdev1 上获取 vgrabbj 的最新代码并进行编译

```
root@tbdev1[541]: wget http://vgrabbj.de/vgrabbj-latest.tar.gz
root@tbdev1[542]: tar xzvf vgrabbj-latest.tar.gz
root@tbdev1[543]: cd vgrabbj-0.7.4/
root@tbdev1[549]: ./configure
checking for jpeg_set_defaults in libjpeg: no
configure: error: *** please install the appropriate library
```

`tbdev1` 缺少库。`vgrabbj` 需要这些库和头文件：`libjpeg`、`libpng` 和 `freetype`。你需要在 `tbdev1` 上安装它们并重新运行 `vgrabbj` 配置：

```
root@tbdev1[550]: apt-get install libjpeg-dev
root@tbdev1[551]: apt-get install libpng-dev
root@tbdev1[552]: apt-get install freetype-dev
root@tbdev1[553]: ./configure
gcc -DHAVE_CONFIG_H -I. -I. -I. -g -O2 -Wall -c vgrabbj.c
gcc -DHAVE_CONFIG_H -I. -I. -I. -g -O2 -Wall -c font.c
gcc -DHAVE_CONFIG_H -I. -I. -I. -g -O2 -Wall -c ccvt_c.c
gcc -g -O2 -Wall -o vgrabbj vgrabbj.c ccvt_c.o -lz -ltf -lpng -lm
root@tbdev1[558]: ls -l vgrabbj
rwxr-xr-x 1 root 189463 Oct 7 21:23 vgrabbj
```

### 2. 运行 vgrabbj 查看结果

```
root@tbdev1[559]: vgrabbj -f /tmp/firstpicture.jpeg
Reading image from /dev/video
root@tbdev1[560]: ls -l /tmp/firstpicture.jpeg
-rw-r--r-- 1 root 60818 Oct 7 21:24 /tmp/firstpicture.jpeg
```

结果是 `/tmp` 目录下的一个 JPEG 文件。`tbdev1` 没有 JPEG 查看器或图形支持，因此你必须将 `/tmp/firstpicture.jpeg` 传输到另一台计算机进行查看。如图 8.1 所示。

### 3. vgrabbj 程序有许多功能

例如文本叠加、图像时间标记和自动捕帧间隔。此命令测试了 Project Trailblazer Lift 9 的设置：

```
vgrabbj -e -i vga -f /tmp/image.jpg
-p "Silverjack Lift 9 Top - %A, %D, %r"
-T 20 -a 5 -m 50 -l 30
```

表 8.1 详细解释了这些 `vgrabbj` 命令行参数。

![](img/6d9baeee8ddb96b5248c3d68b6bc0ecb_231_0.png)

**图 8.1** 从 Kensington VideoCAM Super-VGA USB 摄像头捕获的 `vgrabbj` 图像。

**表 8.1** `vgrabbj` 命令行选项

| 命令行选项 | 描述 |
| --- | --- |
| `-e` | 启用时间戳 |
| `-i vga` | 将图像大小设置为 640x480 |
| `-f` | 写入输出文件而不是标准输出 |
| `-p` | 定义叠加格式 |
| `-T` | 设置叠加大小 |
| `-a` | 设置叠加对齐方式 |
| `-m` | 设置叠加与原始图像的混合 |
| `-l 30` | 告诉 `vgrabbj` 成为守护进程并每 30 秒写入一次图像 |

## 使用 SCSI 操作和 SDDR-09 配置内核

要使用 SanDisk USB SmartMedia 读器，你将需要配置并重新编译内核的 SCSI 和 SDDR-09 支持。请按照以下步骤配置并编译内核：

### 使用 `menuconfig` 配置带有 SCSI 和 SDDR-09 的内核选项

```bash
root@tdedev1[553]: cd /usr/src/linux
root@tdedev1[554]: make menuconfig
```

使用向上和向下方向键配置内核选项，滚动到 `SCSI support` 项并按回车。选择 `SCSI support` 项并按空格键，直到 `< >` 之间出现 `*` 字符（即 `<*>`）。选择并配置这三个 SCSI 支持项：

* `<*>` SCSI support
* `<*>` SCSI disk support
* `<*>` SCSI generic support

选择 `Exit` 并按回车。SDDR-09 驱动被认为是新驱动。除非你为内核配置了开发驱动程序，否则你不会在 USB 支持菜单中看到它的选项。使用向上和向下方向键滚动到 `Code Maturity Level` 选项并按回车。选择 `Prompt for Development and/or Incomplete Code/Drivers` 项并按空格键，直到 `< >` 之间出现 `*` 字符。选择 `Exit` 并按回车。这将返回主菜单。

### 配置 USB 支持选项

使用向上和向下方向键滚动到 `USB support` 项并按回车。配置这些 USB 支持项：

* `<*>` USB Mass Storage support
* `<*>` SanDisk SDDR-09 (and other SmartMedia) support (NEW)

选择 `Exit` 并按回车。这将返回主菜单。SmartMedia 卡片使用 DOS FAT 文件系统。你需要配置内核对 DOS FAT 文件系统的支持。使用向上和向下方向键滚动到 `File Items` 项并按回车。配置这些文件系统项：

* `<*>` DOS FAT fs support
* `<*>` MSDOS fs support

选择 `Exit` 并按回车。这将返回主菜单。

### 后续步骤

6. 使用左右方向键选择 `Exit`，然后按回车。当系统询问是否保存内核配置时，选择 `Yes` 并按回车。

7. 使用此命令构建新内核：

```
root@tbdev1[555]: make dep; make clean; make bImage
```

8. 当内核构建完成后，将内核镜像拷贝到 `/boot` 目录并运行 `lilo`：

```
root@tbdev1[556]: cp arch/i386/boot/bzImage /boot/usbtest
root@tbdev1[557]: lilo
Added Linux *
Added usbtest
```

9. 重启并在启动提示符处使用 `usbtest`。以 root 身份登录。

10. 使用此命令挂载 `usdevfs` `/proc/bus/usb` 和 `usdevfs`：

```
root@tbdev1[501]: mount -t usdevfs usdevfs /proc/bus/usb/
```

## 连接 SanDisk USB SmartMedia 卡读器

按照以下步骤连接 SanDisk USB SmartMedia 卡读器，并检查内核提供的 USB 信息：

### 1. 插入 SanDisk 读器并检查 /proc/bus/usb/devices

```
root@tbdev1[508]: cat /proc/bus/usb/devices
S: Product=SanDisk UHCI-alt Root Hub
S: SerialNumber=e000
S: Manufacturer=YAMAHA
S: Product=YAMAHA YST-MS35D USB Speaker
S: SerialNumber=Ser 00 em
S: Manufacturer=SanDisk
S: Product=SSDOC
C: #Ifs=1 Attr=0 MxPwr=100mA
I: #=0 Alt=0 #EPS=3 Cl=ff(vendor). Sub=1 Prot=0 Driver=usb-storage
```

### 2. 子系统找到了 SanDisk 卡读器、USB SSDOC 及其对应的 usb-storage 驱动

`proc` 目录下有多个 SCSI 条目，存储日志也包含信息：

```
root@tbdev1[518]: cat /proc/scsi/scsi
Attached devices:
Host: scsi Channel: 00 Id: 00 Lun: 00
Vendor: SanDisk Model: ImageMate SDDR-0 Rev: 028
```

## Project Trailblazer USB 硬件 223

类型：直接访问 ANSI SCSI 版本: 02

```
root@tbdev1[519]: cat /proc/scsi/usb-storage-0/0
Host scsi0: usb-storage
Vendor: SanDisk
Product: USB SSDFC
Serial Number: None
Protocol: Transparent SCSI
Transport: EUSB/SDR09
GUID: 078102000000000000000000
Attached: 1
```

```
root@tbdev1[523]: tail /var/log/messages
Oct 8 00:13:01 tbdev1 kernel: hub.c: USB new device
connect on bus1/2, assigned device number 4
Oct 8 00:13:02 tbdev1 kernel: Manufacturer: SanDisk
Oct 8 00:13:02 tbdev1 kernel: Product: USB SSDFC
Oct 8 00:13:02 tbdev1 kernel: scsi0 : SCSI emulation
for USB Storage devices
Oct 8 00:13:02 tbdev1 kernel: Vendor: SanDisk Model:
Oct 8 00:13:02 tbdev1 kernel: Type:
Direct-Access ANSI revision: 02
Oct 8 00:13:02 tbdev1 kernel: Attached scsi
removable disk sda at scsi0, channel 0, id 0, lun 0
Oct 8 00:13:02 tbdev1 kernel: SCSI device
sda: 32768 512-byte sectors (17 MB)
Oct 8 00:13:02 tbdev1 kernel: sda: Write on
Oct 8 00:13:02 tbdev1 kernel: sda: -276    00:13:022dev1 kernel: /dev/sda1
```
