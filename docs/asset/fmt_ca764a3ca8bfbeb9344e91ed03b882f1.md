...[/content]”中

## 示例

原文：

[content]
进入 /path/to/xxx 目录，找到 xxx.json。

在表达式 cvar = avar + bvar 中，加法运算符（+）将 avar 与 bvar 相加，得到它们的和 cvar

在 List.of(arg0, arg1, arg2) 中，List 接口的工厂方法 of() 接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用 cmd 命令：cmd arg0 arg1 arg2。

if (condVar > someVal) {console.log("xxx")}
[/content]

排版后：

[content]
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

## 以下是需要排版的文本

[content]
要以替代格式显示日期，请使用 `+FORMAT` 样式。除了使用正常格式化输出日期和时间外，您可以使其满足某些字符限制，例如用于文件命名。例如，要以 yyyy-dd-mm 格式显示日期，您应使用以下命令：

```
date +%Y-%d-%m
```

这将显示以下输出：

```
2004-09-09
```

如果您知道前面的代码，在创建新文件的同时以创建时间命名新文件就很简单了。要创建一个名为 `backup` 的新目录并在其前面加上当前日期（以便整齐排序），您应使用：

```
mkdir `date +%Y-%d-%m`_backup
```

> **注意** 务必使用反引号字符 (`)，而不是撇号 (')。反引号通常位于波浪号字符 (~) 相同的键上。

######## hwclock 命令

`hwclock` 影响硬件时钟，而不是系统时钟或时间。如果您已经花费了几个周期将系统时钟校准到精确时间，您需要确保这些时间值正确存储到硬件时钟中。

大多数关机过程包括将系统时间同步到硬件时钟，但以防万一，请按照此处示例正确设置。

```
hwclock -r
hwclock --sysync
hwclock --hctosys
```

第一个示例读取硬件时钟值并将其显示在控制台上。

第二个示例获取系统时间并将其写入硬件时钟。

第三个示例读取硬件时钟时间，并将系统时钟设置为该时间。

####### USB 设备

大多数通用串行总线 (USB) 设备在 2.2 版本的内核中已得到支持，并且在 2.4 和 2.6 内核中支持范围不断扩大。

USB 设备呈层次树状结构，包含一个控制器和一个根集线器。所有设备通信都通过 USB 总线进行，设备无法直接访问其他设备。

USB 1.0 规范允许连接 127 个设备，而插入到主集线器的其他集线器则占用 1 个设备的位置。USB 2.0 可能会出现在考试中，但不会涉及关于规范或特性的问题。你只会看到关于 USB 设备等的问题。

######## 控制器类型

主要有两种 USB 控制器类型：通用主机控制器接口 (UHCI) 和开放式主机控制器接口 (OHCI)。

通用主机控制器接口 (UHCI) 是英特尔 (Intel) 的规范，功能较简单，需要更多的软件和处理器周期。

开放式主机控制器接口 (OHCI) 是康柏 (Compaq) 的规范，对软件和处理器的依赖程度稍低。

######## USB 设备与 Linux

要在 Linux 下使用 USB 设备，需要以下驱动程序：

- usbscore.o

- usb-uhci.o, uhci.o 或 usb-ohci.o

如果 USB 核心和相应的规范驱动程序未运行，你可能需要使用 `insmod` 或 `modprobe` 插入正确的规范驱动程序使其运行。

检查 USB 驱动程序是否已正确加载的快速方法是运行 `lsmod` 并查看输出中是否显示它们。如果它们存在，并且其他设备依赖于它们，这将显示在最右侧的列中。

Linux 和 USB 之间的关系与其他操作系统和 USB 的关系不同。例如，Linux 系统上的每个对象都是文件，所有内容都组织在单一的路径层次结构下。这引出了下一个观点，即 USB 设备组织在 USB 设备文件系统下，该文件系统出现在 /proc 抽象文件系统之下。

USB 设备文件系统通常在系统初始化时挂载到 /proc/bus/usb。该目录始终包含两个名为 /drivers 和 /devices 的子目录。当设备连接到文件系统时，第一个设备编号为 001，然后是 002，依此类推。

####### USB 和存储设备

USB 存储设备（如可拆卸硬盘外壳）在系统配置中显示为 SCSI 设备，因为它们可以是任何类型的设备，而 SCSI 驱动程序提供了最灵活的选项集。

运行 mount 命令字符串并搜索输出中的字符 usb：

```bash
mount | grep usb
```

这将显示以下输出：

```bash
usbdevfs on /proc/bus/usb type usbdevfs (rw)
```

输出显示 USB 设备文件系统已挂载到预期位置。你可以用来查看 USB 设备的其他命令包括 scsi_info，它旨在枚举 SCSI 和 USB 设备。例如，如果大容量存储设备（如磁盘）位于 /dev/sda，你将使用以下命令：

```bash
scsi_info /dev/sda
```

此外，如果该设备是存储设备，你可以使用 fdisk -l 查看它映射到了哪个 /dev 文件。然后你可以手动映射它，或者将其作为 /etc/fstab 文件中的条目插入。

最后，对于偏好图形化界面的用户，你可以使用 usbview 命令，它以双窗格视图显示 USB 设备和配置。

####### 使用 usbmgr

`usbmgr` 命令加载或卸载必要的内核模块，并执行各种脚本以设置 USB 设备。内核配置必须已选择并编译了 USB 支持选项。根据发行版的不同，你应该编辑 /etc/rc.config 或 rc.sysinit 脚本，将 START_HOTPLUG 设置配置为 true。

usbmgr 配置文件由以下内容组成：

- `usbmgr.conf`——包含模块加载/卸载的数据

- `preload.conf`——包含启动时加载的内核模块

然而，如果在内核重新配置期间，你编译了所有 USB 驱动程序，`usbmgr` 命令将无事可做且是不必要的。如果你将频繁使用 USB 设备，请将所有内容编译进内核，以使加载速度更快并减少依赖项。

####### USB 设备和驱动程序

`drivers` 文件包含已加载驱动程序的列表，该列表因每个系统连接或加载的内容而异。要查看此文件的列表，请执行此示例命令：

```bash
more /proc/bus/usb/drivers
```

这将产生以下输出：

```text
hid
printer
hub
```

`devices` 文件则详细得多，它以每个设备一系列行的形式显示连接的设备信息：

```bash
cat /proc/bus/usb/devices
```

这将产生以下输出：

```text
T:  Bus=01 Lev=00 Prnt=00 Pnt=00  LMin=00
B:  Alloc=   0/900 us  (  0%),  #Int=  0,  #Iso=  0
D:  Ver= 1.00 Cls=09(hub  ) (Device Descriptor)
P:  Vendor=0000 ProdID=0000 (Continuation of D:)
S:  Product=USB UHCI Root Hub (Strings returned from device)
S:  SerialNumber=1000 (Continuation of S:)
```

> **注意** 考试中的 USB 内容主要在于了解 USB 与系统的关系（它是一个设备文件系统）以及它是如何构建的（作为根集线器下设备的层次结构）。务必查看所有提到的文件，并阅读 `/etc/hotplug` 和 `usbmgr` 的手册页 (man pages)。

####### 设置 SCSI

LPi 假设你拥有安装了 Linux 的服务器系统，并且 SCSI 是高性能和大吞吐量系统的首选存储设备。

在参加考试时，请记住 SCSI 总线类型决定了设备的密度（8 位或 16 位），例如

- **8 位 SCSI**—八个设备（0–7）

- **16 位 SCSI**—十六个设备（0–15）

每个设备都与一个数字相关联，该数字决定了访问 SCSI 总线的优先级。

SCSI ID 7 通常保留给控制器。这要追溯到只有 8 个 ID 可供选择的时代，当时控制器可以放置在任意一端；因此选择了 ID 7。既然现在有 16 个 ID 可供选择，你可以将控制器 ID 设为 15。然而，为了保持一致性，大多数系统管理员仍在使用 ID 7。

部分由于历史上 ID 7 是控制器，SCSI 设备的优先级顺序如下：

```text
7, 6, 5, 4, 3, 2, 1, 0, 15, 14, 13, 12, 11, 10, 9, 8
```

通常，主机适配器应具有最高优先级，这也是将控制器保留在 ID 7 的另一个原因。

Linux 使用设备标识符 `sd` 后跟一个或两个数字来定义每个 SCSI 逻辑单元号 (LUN) 或设备。例如，系统上的第一个 SCSI 设备应映射到 `/dev/sda`。你可以使用以下命令确定系统中可能的设备/LUN 的上限：

```bash
ls -1 /dev/sd* | wc -l
```

这将产生以下输出：

```text
2048
```

/proc 文件系统是存储 SCSI 设备信息的地方，位于 /proc/scsi/scsi 目录中。你可以使用以下命令查看设备和其他信息：

```bash
cat /proc/scsi/scsi
```

这将产生以下输出：
