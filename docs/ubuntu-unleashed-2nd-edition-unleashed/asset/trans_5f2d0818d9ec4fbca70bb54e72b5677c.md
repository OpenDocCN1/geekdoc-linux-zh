

# USB 扫描仪成功难以捉摸

因为失败有时比成功更具教育意义，所以在本书的前几版中，我们尝试配置一个不受支持的 USB 扫描仪：Canon N650U。随着随 Ubuntu 发布的 SANE 版本的发布，该扫描仪现在已受支持，并且会被自动检测到！

然而，这里是我们手动用于在 Linux 中检测和配置该扫描仪的步骤，当它工作不正常时：

首先，连接扫描仪。对于此 USB 扫描仪，请查看以下输出：

```
$ sudo cat /proc/bus/usb/devices/
```

（我们在此截断了输出，仅显示扫描仪。您也可以使用 lsusb 命令。）

```
T:  Bus=01 Lev=01 Prnt=01 Port=00 Cnt=01 Dev#=  2 Spd=12 MxCh=
D:  Ver= 1.00 Cls=00(>ifc ) Sub=00 Prot=00 MxPS= 8 #Cfgs=  1
P:  Vendor=04a9 ProdID=2206 Rev= 1.00
S:  Manufacturer=Canon
S:  Product=CanoScan
C:  #Ifs= 1 Cfg#= 1 Atr=80 MxPwr=500mA
I:  If#= 0 Alt= 0 #EPs= 3 Cls=ff(vend.) Sub=00 Prot=ff Driver=(none)
E:  Ad=81(I) Atr=03(Int.) MxPS=  1 Ivl=16ms
E:  Ad=82(I) Atr=02(Bulk) MxPS= 64 Ivl=0ms
E:  Ad=03(O) Atr=02(Bulk) MxPS= 64 Ivl=0ms
```

第七行末尾的 Driver=(none) 告诉我们该设备未在查找表中找到。因为我们现在有了“魔术”厂商 ID 和设备 ID，所以我们可以尝试手动加载驱动程序

```
$ sudo /sbin/modprobe scanner vendor=0x04a9 product=0x2206
```

现在，之前 cat /proc/bus/usb 命令的输出告诉我们扫描仪设备驱动程序已与我们的扫描仪关联：

```
I:  If#= 0 Alt= 0 #EPs= 3 Cls=ff(vend.) Sub=00 Prot=ff Driver=usbscanner
```

并且 Kooka 和 Xsane 应用程序现在可以识别扫描仪。

## 使用图形格式

图像文件格式是为了满足特定的技术目的而开发的，例如无损压缩，即在不牺牲图像质量的情况下减小文件大小，或为了竞争原因满足对专有格式的需求。许多文件格式受一个或多个专利覆盖。例如，GIF 格式在开源社区中已不受欢迎，因为专利持有者最近才决定开始执行其专利权。

如果您想查看或操作图像，您需要识别文件格式以选择合适的工具来处理图像。文件扩展名是您判断的第一个指标

- **.bmp**—位图图形，常用于 Microsoft Windows
- **.cgm**—计算机图形元文件
- **.g3**—CCITT Group 3 传真图像
- **.gif**—CompuServe 图像交换格式
- **.ico**—Microsoft Windows 图标图像
- **.jpg**—联合图像专家组
- **.mng**—多图像网络图形图像
- **.pbm**—便携式位图文件格式
- **.pcx**—IBM Paintbrush
- **.pgm**—便携式灰度图文件格式
- **.png**—便携式网络图形
- **.pnm**—便携式任意图
- **.ppm**—便携式像素图文件格式
- **.rgb**—原始红、绿、蓝采样
- **.rs**—Sun 栅格图像
- **.svg**—可缩放矢量图形
- **.tif**—标记图像文件格式
- **.xbm**—X 位图图像
- **.xpm**—X 像素图图像，常用于 Linux 图标图像

图像文件扩展名的详尽列表可以在 ImageMagick 的 man 手册中找到，ImageMagick 是一个优秀的应用程序，随 Ubuntu 一起提供，您将在本章后面的部分了解更多相关信息。

> **TIP**
> 
> Ubuntu 包含数十种图形转换程序，并且几乎没有图形文件格式在使用 Linux 时无法被操作。这些命令可用于 Perl 脚本、shell 脚本或命令行管道，以支持许多类型的复杂格式转换和图像操作任务。请参阅 ppm、pbm、pnm 和 pgm 系列命令的 man 手册。另请参阅 convert 命令的 man 手册，该命令是随 ImageMagick 套件一起提供的功能极强的程序套件的一部分。

通常，您想要以某种方式操作的<|message|> 在您的图形应用程序或最终应用程序都无法使用的格式中。解决方案是将图像文件转换——有时需要经过几种格式。ImageMagick 的 convert 实用程序很有用，netpbm 工具家族也是如此。如果尚未安装，可以通过“系统设置”菜单中的“添加/删除软件”GUI 安装 ImageMagick；netpbm 工具默认始终已安装。

convert 实用程序在 ImageMagick 识别的图像格式之间进行转换。颜色深度和大小也可以在转换过程中进行操作。您可以使用 ImageMagick 来附加图像、为其添加边框、标签、旋转和着色，并执行其他非常适合脚本操作的操纵。与 ImageMagick 关联的命令包括 display、animate、identify 和 import。该应用程序支持超过 130 种不同的图像格式——（全部列在 ImageMagick 的 man 手册中）。

## 使用 ImageMagick 的 Identify 玩转

您可以使用 ImageMagick 的 identify 命令来识别图像文件的详细信息。用于 GRUB 启动加载器的欢迎闪屏图像位于 /boot/grub 中，是一张被 gzip 压缩的 .xpm 图像。如果您对该图像运行 identify，您会发现它是一张 640×480 xpm 图像，颜色深度为 16 位。这就是您构建自己的替换图像所需了解的全部信息。使用 GIMP 或其他图形工具，将您选择的图像裁剪或调整大小为 640×480 并将颜色深度更改为 16 位。将图像保存为 splash.xpm，然后 gzip 生成的文件。替换原始的 Red Hat 文件，您现在就拥有了一个自定义启动图像。identify 的使用帮助您复制原始图像的参数以符合 GRUB 的要求。

identify 命令可用于识别未知图像文件并确定它们是否已损坏。

netpbm 工具默认已安装，因为它们构成了图形格式操作的基础。每个图像格式的 man 手册都列出了相关的转换实用程序；这些实用程序的数量可以让您了解该格式的使用方式，并显示一种格式是如何建立在另一种格式之上的：

- ppm 的 man 手册，便携式像素图文件格式，列出了 47 个与 ppm 相关的转换实用程序。这是有道理的，因为 ppm，即便携式像素图，被认为是彩色图像文件的最低公分母。因此，它通常用作中间格式。

- pgm 的 man 手册，便携式灰度图文件格式，列出了 22 个转换实用程序。这是有道理的，因为 pgm 是灰度图像文件的最低公分母。

- ppm 的 man 手册，便携式任意图文件格式，列出了 31 个与其相关的转换实用程序。然而，PNM 没有关联的格式，因为它与 ppm、pgm 和 pbm 协同工作。

