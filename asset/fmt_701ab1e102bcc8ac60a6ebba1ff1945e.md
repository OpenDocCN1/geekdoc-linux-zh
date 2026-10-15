
USB 服务（最可能最初由安装程序配置）在启动期间通过系统模块配置文件 `/etc/modules.conf` 中的条目启动：

```
alias usb-controller usb-uhci
```

# 第 4 章 安装后配置

在本示例中，PC 平台使用通用主机控制器接口 `uhci`，当 Red Hat Linux 启动时，将从 `/lib/modules/2.4-X/kernel/drivers/usb` 目录加载 `uhci.o` 内核模块。另一个常用的 USB 控制器是开放主机控制器接口 `ohci`，它需要加载 `uhci.o` 模块来启用 USB 服务。

如果你的指针设备不起，你可以使用 `dmesg` 命令查看 Linux 是否在启动过程中识别了该设备。这可以提供一些诊断信息，因为 Linux 或驱动程序（可能是某个模块）通常会输出诊断信息：

```
usb-uhci.c: USB UHCI at I/O 0xd800, IRQ 15
usb-uhci.c: Detected 2 ports
usb.c: new USB bus registered, assigned bus number 2
hub.c: USB hub found
hub.c: 2 ports detected
usb-uhci.c: v1.275: Universal Host Controller Interface driver
hub.c: USB device connect on bus/1, assigned device number 2
usb.c: USB device 2 (vendor/prod 0x1241/0x1122) is not claimed by any active driver.
usb.c: registered new driver hiddev
usb.c: registered new driver hid
input0: HID v1.000 Mouse [1241:1122] on usb1:2.0
hid-core.c: v1.8 Andras Gal, Vojtech Pavlovik <vojtech@use.cz>
hid-core.c: USB support
mice: PS/2 mouse device common for mice
```

在本示例中（你的输出可能不同），Red Hat Linux 识别了通用 USB 模块。USB 支持最初由 `usbcore.o` 模块启用。在本示例，通过加载 `uhci.o` 内核模块初始化并配置 USB 控制器接口，并加载如 `input.o` 和 `hid.o` 等模块来支持鼠标（或键盘）USB 设备。

你可以通过 `lsmod` 命令的输出查看加载了哪些模块。注意，根据你的计算机和模块版本，可能会看到不同的内存值：

```
### lsmod

mouseddev        4288  1
hid             18720 0 (unused)
input           3744  0 [mouseddev]
usb-uhci        21636 0 (unused)
usbcore        59072 1 [hid-uhci]
```

## 指针和键盘配置

可以看到，USB 设备支持（特别是指针设备）涉及正确加载模块链，而不是单个驱动程序。

> 提示
>
> 在启动或连接时，每个 USB 设备都会报告一对代表厂商和相关产品（型号）的数字。如果无法识别厂商和产品，可能会出现问题。更多信息请参见第 2 章“USB 设备”。

Red Hat Linux 安装程序通常识别并正确配置计算机的指针设备，但如果你安装了新设备，将重新配置系统以便使用。

使用 PS/2 指针设备时，文件 `/dev/mouse` 将指向 `/dev/psaux`；当使用 USB 指针设备时，`/dev/mouse` 将指向 `/dev/input/mice`。串口鼠标将使 `/dev/mouse` 指向特定的串口，可能是 `/dev/ttyS0`。`/dev/mouse` 文件是一个符号链接，为了方便许多 Linux 应用程序。对于程序来说，查找 `/dev/input/mice`、`/dev/psaux` 或 `/dev/tty0` 要方便得多。

USB 服务（最可能最初由安装程序配置）在启动期间通过系统模块配置文件 `/etc/modules.conf` 中的条目启动：

```
alias usb-controller usb-uhci
```

# 第 4 章 安装配置

在本示例中，PC 平台使用通用主机控制器接口 `uhci`，当 Red Hat Linux 启动时，将从 `/lib/modules/2.4-X/kernel/drivers/usb` 目录加载 `uhci.o` 内核模块。另一个常用的 USB 控制器是开放主机控制器接口 `ohci`，它需要加载 `uhci.o` 模块来启用 USB 服务。（注：原始文本说了两次 `uhci.o`，但上下文暗示应该是 `ohci.o`）。

如果你的指针设备不起，你可以使用 `dmesg` 命令查看 Linux 是否在启动过程中识别了该设备。这可以提供一些诊断信息，因为 Linux 或驱动程序（可能是某个模块）通常会输出诊断信息：

```
usb-uhci.c: USB UHCI at I/O 0xd800, IRQ 15
usb-uhci.c: Detected 2 ports
usb.c: new USB bus registered, assigned bus number 2
hub.c: USB hub found
hub.c: 2 ports detected
usb-uhci.c: v1.275: Universal Host Controller Interface driver
hub.c: USB device connect on bus/1, assigned device number 2
usb.c: USB device 2 (vendor/prod 0x1241/0x1122) is not claimed by any active driver.
usb.c: registered new driver hiddev
usb.c: registered new driver hid
input0: HID v1.000 Mouse [1241:1122] on usb1:2.0
hid-core.c: v1.8 Andras Gal, Vojtech Pavlovik <vojtech@use.cz>
hid-core.c: USB support
mice: PS/2 mouse device common for mice
```

在本示例中（你的输出可能不同），Red Hat Linux 识别了通用 USB 模块。USB 支持最初由 `usbcore.o` 模块启用。在本示例，通过加载 `uhci.o` 内核模块初始化并配置 USB 控制器接口，并加载如 `input.o` 和 `hid.o` 等模块来支持鼠标（或键盘）USB 设备。

你可以通过 `lsmod` 命令的输出查看加载了哪些模块。注意，根据你的计算机和模块版本，可能会看到不同的内存值：

```
### lsmod

mouseddev        4288  1
hid             18720 0 (unused)
input           3744  0 [mouseddev]
usb-uhci        21636 0 (unused)
usbcore        59072 1 [hid-uhci]
```

## 指针和键盘配置

可以看到，USB 设备支持（特别是指针设备）涉及正确加载模块链，而不是单个驱动程序。

> 提示
>
> 在启动或连接时，每个 USB 设备都会报告一对代表厂商和相关产品（型号）的数字。如果无法识别厂商和产品，可能会出现问题。更多信息请参见第 2 章“USB 设备”。

（注：提供的 OCR 文本包含重复部分，以上是基于逻辑流的清理后内容。）

# 配置显示图形

在初始安装 Red Hat Linux 之后，如果您添加或更改系统中使用的图形设备，必须对这些设备进行配置。对于 Red Hat 系统，添加或更改显示器可能像更换显示器或替换显示适配器一样简单。对于基于 Intel 的 PC，这可能意味着从使用主板内置显示适配器（如果可用）切换过来——通过在加速图形端口 `AGP` 或外设组件部件接口 `PCI` 槽中插入显卡——或添加第二个显示适配器以支持在 X 会话中使用多个显示器。

虽然显示器可以可以方便地断开连接或重新连接到运行中的 Red Hat Linux 系统，但插入或移除图形显示适配器将需要停机——这是学术、企业、公司或小微企业运营的噩梦。

## Red Hat Linux 与 KVM

键盘、视频和鼠标 `KVM` 硬件提供了使用单台显示器、键盘和指针快速切换各个计算机显示和控制台的能力。这为大型安装环境中的计算机提供了高效的组织和利用，并允许单个操作员执行系统管理任务，而无需物理性地移动到每台计算机前。
