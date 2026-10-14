
- 根文件系统位于 LVM 上
- 根文件系统是加密的（`linuxrc` 会要求输入密码）
- 根文件系统位于 PCMCIA 适配器上的 SCSI 硬盘上。

## 更多信息

```text
/usr/src/linux/Documentation/ramdisk.txt
/usr/src/linux/Documentation/initrd.txt
the man page for initrd (man 4 initrd)
```

## linuxrc

`linuxrc` 在内核启动期间启动，通常作为 Linux 系统安装的前奏，在“实际”启动开始之前（当然，内核必须首先正确配置）。这样，您可以启动一个小型的模块化内核，并从软盘加载所需的少量驱动模块。

如果需要，`linuxrc` 会协助加载相关驱动。不过，`YaST2` 的自动硬件检测通常相当可靠。

您也可以将 `linuxrc` 用作已安装系统的启动工具。您甚至可以启动一个完全独立的基于 RAM 磁盘的救援系统，例如，当您的硬盘发生严重问题或您只是忘记了 root 密码时。更多相关内容请参见下面的第 285 页*SuSE 救援系统*一节。

### 主菜单

选择语言和键盘后，您将进入 `linuxrc` 的主菜单（参见第 34 页的图 3.2）。通常，`linuxrc` 用于启动 Linux。进入启动菜单以开始安装（“开始安装 / 系统”）。

### 设置 / 首选项

请指定关于“语言”、“屏幕”（彩色/单色）、“键盘布局”和“调试（专家）”的设置。

### 系统信息

在“系统信息”（下一页的图 11.1）中，除了内核消息外，还可以检查许多其他信息，例如 PCI 卡的 I/O 地址或 Linux 识别出的主内存大小。

您可以在“系统信息”中查看一些系统信息。在这里，可以检查已使用的中断、已使用的 I/O 端口、主内存以及 Linux 检测到的 PCI 设备。

接下来的几行显示了连接到 (E)IDE 控制器的硬盘和 CD-ROM 如何宣布它们的启动。在这种情况下，您不需要加载额外的模块：

```text
hda: ST32140A, 2015MB w/128kB Cache, LBA, CHS=1023/64/63
hdb: CD-ROM CDU-51G, ATAPI CD-ROM drive
Partition check:
 hda: hda1 hda2 hda3 < hda5 >
```

![](img/a4b6c994843f3fbd688003f4cabfa48f_293_0.png)

*图 11.1：系统信息*

如果您启动的内核已经编译了 SCSI 驱动，那么您也不需要将该 SCSI 驱动作为模块。加载 SCSI 适配器和连接设备时的典型提示信息可能如下所示：

```text
scsi : 1 host.
Started kswapd v 1.4.2.2
scsi0 : SCSI host 0 accepting period 100ns offset 8 10.00MHz FAST SCSI-II
scsi0 : setting target 0 to period 100ns offset 8 10.00MHz FAST SCSI-II
  Vendor: QUANTUM  Model: VP3210S       Rev: 811H
  Type:   Direct-Access                    ANSI SCSI revision: 02
Detected scsi disk sda at scsi0, channel 0, id 0, lun 0
scsi0 : setting target 2 to period 248ns offset 8 4.03MHz synchronous SCSI
scsi0 : setting target 2 to period 248ns offset 8 4.03MHz synchronous SCSI
  Vendor: TOSHIBA  Model: CD-ROM XM-3401TA  Rev: 0283
  Type:   CD-ROM                         ANSI SCSI revision: 02
scsi2 : detected 1 SCSI disk total.
SCSI device sda: hdwr sector=512 bytes. Sectors=4308352 [2103 MB] [2.1 GB]
Partition check:
 sda: sda1 sda2 sda3 sda4 < sda5 sda6 sda7 sda8 >
```

### 加载模块

选择您需要哪些种类的模块。如果您通过磁盘启动，`linuxrc` 必须读取相应的数据并显示在列表中。

如果您从 CD 或 DOS（通过 `loadlin`）启动，这些模块已经在 `linuxrc` 中设置好了。这省去了繁琐的加载过程，但需要额外的内存。

![](img/a4b6c994843f3fbd688003f4cabfa48f_294_0.png)

*图 11.2：加载模块*

`linuxrc` 提供了一个可用驱动列表。左边是模块名称，右边是对其用途的简要描述。对于某些组件，有多种驱动可供选择（甚至包括较新的 alpha 驱动）。

### 传递参数

找到合适的驱动后，用光标移动到它并按下 [Enter]。这将打开一个对话框，其中有一个区域可以为该模块添加额外参数。关于模块参数的更多信息，请参见第 255 页的 *modprobe 参数*一节。

请注意——与在内核提示符下输入参数（如 `MILO`、`SILO` 或 `SYSLINUX`）不同——同一模块的多个参数在这里必须用空格分隔。

在大多数情况下，不需要详细指定硬件。大多数驱动会自动找到它们的组件。只有在您有网卡或带有专有控制器卡的旧 CD-ROM 驱动器时，才需要指定参数。如有疑问，只需尝试按 [Enter]。识别和初始化某些硬件可能需要一些时间。切换到虚拟控制台 4（Alt + F4）可以让您在加载时查看内核消息。SCSI 驱动需要一段时间，因为它们必须等待每个设备加载完毕。

![](img/a4b6c994843f3fbd688003f4cabfa48f_295_0.png)

*图 11.3：SCSI 驱动选择*

这些消息由 `linuxrc` 显示，以便您可以验证一切是否顺利运行。如果失败，这些消息可能会提示原因。

### 开始安装 / 系统

一旦您通过模块设置了硬件支持，请进入“开始安装 / 系统”菜单。

从这里可以启动多种流程：“开始安装”（更新也是从此项启动）、“启动已安装的系统”（必须知道根分区）、“启动救援系统”（参见对面页的*SuSE 救援系统*一节）和“弹出 CD”。

“启动 Live-CD”仅在您使用“LiveEval CD”启动时可用。从 FTP 服务器下载 ISO 镜像（live-eval——变量 `VERSION`）：

ftp://ftp.suse.com/pub/suse/i386/

> **提示**
>
> 如果您想在不实际安装的情况下测试这台计算机或您可能想购买的笔记本电脑是否与 SuSE Linux 兼容，“启动 Live-CD” 这一项会非常有用——这样的测试应该在任何现代电脑商店都能毫无问题地进行。

对于安装（第 286 页的图 11.5），请为安装选择各种来源，救援系统也是如此（参见第 286 页的图 11.5）。

![](img/a4b6c994843f3fbd688003f4cabfa48f_296_0.png)

*图 11.4：输入要加载模块的参数*

### SuSE 救援系统

SuSE Linux 包含多个 Linux 救援系统，以便在紧急情况下，您硬盘上的 Linux 分区可以从“外部”访问：通过启动盘或从磁盘、CD、网络或 SuSE FTP 服务器加载的“救援”系统。还有一个可启动的 SuSE Linux CD（“LiveEval CD”）可用作救援系统。救援系统包含几个帮助程序，您可以用它们来解决无法访问的硬盘、配置错误的配置文件或其他类似问题带来的大麻烦。

救援系统的另一个方面是 `Parted`，用于修改分区大小。如果您不想利用 `YaST2` 中集成的调整大小工具，可以从救援系统内部启动该程序。有关 `Parted` 的信息可以在以下网址找到：

http://www.gnu.org/software/parted/

> **提示**
>
> 请始终在手边准备一张启动盘和救援盘，因为与紧急情况下无法访问系统或 CD-ROM 驱动器所浪费的时间和精力相比，创建和维护启动盘所需的一点点努力是微不足道的。

![](img/a4b6c994843f3fbd688003f4cabfa48f_297_0.png)

*图 11.5：在 linuxrc 中选择源介质*

## 准备工作

要设置救援系统，你需要两张无错误的磁盘：一张作为将来的启动盘，另一张用于存放小型根文件系统的压缩镜像。用于启动系统的镜像文件 `bootdisk` 和用于根文件系统的文件 `rescue` 可以在第一张 CD 的 `/disks` 目录中找到。有三种方法可以将根文件系统设置到磁盘上：

- 使用 `YaST`
- 在控制台中使用 Linux 命令
