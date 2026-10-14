
检查你的 BIOS 设置以确定哪一个是正确的。如果你有支持的 IRDA 芯片组，在 (`IRDA_PORT`) 中找到对应内核模块的名称，例如 `IRDA_PORT`="toshoboe"。`FIR` 必须启用。

（实际上，处理提供的文本以使其没有 OCR 痕迹）：

## displaymanager 显示器管理器配置

...

`KDM_GREETSTRING`=""

以特殊方式接收系统的问候。

## gconf2 配置 gconf 守护进程

```bash
GCONF2_CONF_SOURCE="distribution"
```
为 `gconf` 守护进程选择默认配置源。确定用户从哪里获取 GNOME 桌面配置。如果设置为 `source`，将使用来自 GNOME2 源的默认设置。作为替代方案，选择 `distribution` 以使用发行版的默认设置。你也可以在此处指定其他源。

## hardware 硬件设置

```bash
DEVICES_FORCE_IDE_DMA_ON=""
```
为列出的 IDE 设备开启 DMA。

```bash
DEVICES_FORCE_IDE_DMA_OFF=""
```
为列出的 IDE 设备关闭 DMA。

## hotplug 配置热插拔服务

```bash
HOTPLUG_DEBUG="default"
```
此变量控制热插拔服务的输出量。
使用 `default`、`""` 或 `no` 时，它只向 `syslog` 打印少量的消息和错误。设置为 `off`，它将保持绝对安静。设置为 `verbose`（或 `yes`），它会打印一些额外的调试输出。设置为 `max`，它将把每一个细节都填满 `syslog`。

```bash
HOTPLUG_START_USB="yes"
```
启用或禁用 USB 热插拔事件处理。

> Note
> 在加载了 USB 输入设备时禁用 USB 热插拔将导致你的键盘无法使用。

```bash
HOTPLUG_USB_USE_USBMODULES="no"
```
启用或禁用使用 `/sbin/usbmodules`。默认不使用此功能。

```bash
HOTPLUG_USB_HOSTCONTROLLER_LIST="usb-uhci uhci usb-ohci ehci-hcd"
```
主机控制器驱动将按此顺序加载。

```bash
HOTPLUG_USB_STATIC_MODULES="evdev joydev"
```
指定在 USB 热插拔启动时加载的模块。主要是这些是不会创建热插拔事件的模块，例如输入设备。如果你使用旧的 Free86 USB，请添加 `mousedev` 和 `input`。

```bash
HOTPLUG_USB_MODULES_TO_UNLOAD="scanner"
```
这些模块将在 USB "remove" 事件时被卸载。对于某些设备，重新初始化硬件是有用的。

```bash
HOTPLUG_NET_MODULES="pegasus usnet cateth CD-Ether"
```
如果加载或卸载了这些模块中的一个，它将被视为网络设备，系统将为接下来的 "net event" 创建硬件描述。

```bash
HOTPLUG_USB_DELAY="3"
```
USB 栈将在后台加载一些驱动程序。在所需的驱动加载之前可能会运行其他层级脚本。

```bash
HOTPLUG_START_NET="yes"
```
启用或禁用 NET 热插拔事件处理。

### `HOTPLUG_NET_DEFAULT_HARDWARE`="1"

在未来的某一天，将会有方法获取特定网络接口背后硬件类型的信息。目前，还没有简单的方法获取这些信息。目前，我们使用以下变通方案：将硬件描述写入 USB 或 PCI 热插拔事件中，然后由 NET 事件读取。如果你同时插上多个设备，可能会导致竞态条件。如果变通方案失败，当调用 `[up,down]` 时将使用 `HOTPLUG_NET_DEFAULT_HARDWARE` 中的字符串。将其设置为你所使用的热插拔网卡类型：`pcmcia`, `usb` 或 `firewire`。

### `HOTPLUG_NET_TIMEOUT`="8"

指定等待 USB 或 PCI 事件提供的硬件描述的时间（秒）。如果此值等于 `0`，热插拔服务将不会等待硬件描述，并始终使用 (`HOTPLUG_NET_DEFAULT_HARDWARE`) 的值。这里的默认值是 `8`，因为某些 PCMCIA NIC 执行某些任务需要很长时间。

### `HOTPLUG_START_PCI`="yes"

启用或禁用 PCI 热插拔事件处理。

### `HOTPLUG_PCI_MODULES_NOT_TO_UNLOAD`=""

这些模块在 PCI "remove" 事件时不应被卸载，因为它们会带来很多麻烦。

### `HOTPLUG_START_IEEE1394`="yes"

启用或禁用 IEEE1394 (Firewire) 热插拔事件处理。

### `HOTPLUG_IEEE1394_MODULES_NOT_TO_UNLOAD`="eth1394"

如果加载或卸载了这些模块中的一个，设备设备被视为网络设备，并为接下来的事件创建一个硬件描述。

### `HOTPLUG_IEEE1394_MODULES_NOT_TO_UNLOAD`=""

这些模块在 IEEE1394 "remove" 事件时不应被卸载。

`irda` 是使用的红外接口，例如笔记本电脑。若要永久激活它，请运行 `insnerv /etc/init.d/irda`。

### `IRDA_PORT`="/dev/tty1"

目前，正常配置支持 UART (SIR) 模式。变量 (`IRDA_PORT`) 设置串口。检查你的 BIOS 设置以确定哪一个是正确的。如果你有支持的 IRDA 芯片组，在 (`IRDA_PORT`) 中找到对应内核模块的名称，例如 `IRDA_PORT`="toshoboe"。`FIR` 必须先在 BIOS 设置中启用。有时，你必须禁用串口，通过 `seterial /dev/ttyS<x>` 使用。

SUSE Linux 引导

SUSE Linux - 管理指南

313

（等待，OCR 文本有一些重复和布局。我将根据提供的文本进行清理。）

`KBD_TTY`="tty1 tty2 tty3 tty4 tty5 tty6 tty7 tty8 tty9

tty10 tty12 tty13 tty14 tty15 tty16 tty17 tty18 tty19

tty20"

将 (`NumLock`)、(`CapsLock`) 和 (`ScrollLock`) 限制在某些 TTY 上。一个以空格分隔的列表。`""` 表示全部。

`COMPOSETABLE`="clear winkeys shiftctrl latin.add"

要加载的组合键表。关于按键表的更多细节，请参 `/usr/share/packages/kbd/README.SU`。

用于语言和区域的语言设置。

`RC_LANG`="en_US"

设置用于区域的 LC 变量。这是本地用户的默认值，只要遵循了 (`RC_LC_*`) 变量。

`sysconfig` 变量有 (`RC_LC_ALL`)（覆盖 LC* 和 LANG），(`RC_LC_MESSAGES`)，(`RC_LC_TYPE`)，(`RC_LC_MONETARY`)，(`RC_LC_NUMERIC`)，(`RC_LC_TIME`)，以及 (`RC_LC_COLLATE`)。请参见第 290 页的 Local Adjustments —118N/L10n。

`ROOT_USES_LANG`="ctype"

`root` 是否应该使用区域设置？`ctype` 表示 `root` 仅使用 (`LC_TYPE`)。

`locate` 数据库允许快速找到系统上的文件。它在系统启动后不久就会进行更新，以防你的机器没有持续运行（请参见第 267 页的 `cron` 软件包）。

`RUN_UPDATED`="no"

是否应该每天更新一次 `locate` (`locate`) 数据库？可以通过以下变量对 `updateddb` 进行更详尽的配置。

`RUN_UPDATED_AS`="nobody"

指定使用 `updateddb` 的用户。出于安全考虑，默认值为 `nobody`。

`UPDATED_NETPATHS`=""

通常，`updateddb` 仅扫描硬盘，但也可以将网络路径包含在数据库中。如果你指定了目录，它们将会被扫描。

`UPDATED_PRUNEPATHS`="/mnt /media/cdrom /tmp /usr/tmp /var/tmp /var/spool /proc /media"

指定在每日运行 `updateddb` 运行时跳过的目录。

`UPDATED_NETUSER`=""

用于搜索网络的用户，默认为 `nobody`。

`UPDATEDB_PRUNEFS`=""

指定要从 `updateddb` 运行中排除的文件系统类型。

### mail 电子邮件设置

`FROM_HEADER`=""

为整个系统定义的 From: 行。如果为空 `""`，则使用 FQDN（完全限定域名）。请参见第 340 页的域名名系统。

`MAIL_CREATE_CONFIG`="yes"

如果不需要让 SysConfig 生成配置文件，请将此项设置为 `no`（例如，你想自己生成 `/etc/sendmail.cf`）。如果你想从 `/etc/sysconfig/sendmail` 中的参数生成 `sendmail` 配置 `/etc/sendmail.cf`，请使用 `yes`。

`SMTPD_LISTEN_REMOTE`="no"
