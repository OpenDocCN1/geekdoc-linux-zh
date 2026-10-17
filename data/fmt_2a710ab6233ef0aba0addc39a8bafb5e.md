
对于使用 `LILO` 作为启动加载器的系统，请参考下一页的示例 7.2。你可以在启动提示符处选择所需的配置。

示例 7.2：`/etc/lilo.conf`

```
boot = /dev/hda
change-rules
reset
read-only
menu-scheme = Wg:kw:Wg:Wg
prompt
timeout = 80
message = /boot/message
```

```
image = /boot/vmlinuz
label = home
root = /dev/hda6
initrd = /boot/initrd
append = "vga=0x317 hde=ide-scsi PROFILE=home"
```

```
image = /boot/vmlinuz
label = work
root = /dev/hda6
initrd = /boot/initrd
append = "vga=0x317 hde=ide-scsi PROFILE=work"
```

```
image = /boot/vmlinuz
label = road
root = /dev/hda6
initrd = /boot/initrd
append = "vga=0x317 hde=ide-scsi PROFILE=road"
```

### 7.2.8 故障排除

在大多数情况下，`SCPM` 运行顺畅。然而，也存在一些陷阱，在此处进行了描述。

`SCPM` 目前无法应对系统更新。困难在于，在系统更新时，存储在配置中的数据不会通过自动机制进行更新。`SCPM` 然后会检测到系统更新并拒绝工作。在这种情况下，你会收到包含“your operating system installation changed/is unknown, read man page!”的错误消息。在这种情况下，使用 `scpm -f enable` 重新初始化 `SCPM`。但是，你的配置将会丢失，你必须重新配置。

有时 `SCPM` 可能会在切换过程中发生停止工作。这可能是由某些外部影响引起的，例如用户中止、电源故障、其他类似问题，甚至是 `SCPM` 本身的错误。在这种情况下，下次启动 `SCPM` 时会显示“`SCPM` 已锁定”的错误消息。这是为了系统安全，因为其数据库中存储的数据可能与系统中的数据不同。要解决此问题，请从 `/var/lib/scpm/#LOCK` 删除锁文件，然后使用 `scpm-s reload` 更新数据库。完成此操作后，按正常程序继续。

更改已初始化 `SCPM` 的资源组配置没有问题。但在添加或删除组后，你必须运行 `scpm rebuild`。这将向所有配置添加新资源并移除被删除的资源。被删除的资源不会从系统中。如果同一资源在不同配置中有不同的设置，删除资源可能会导致严重问题。未被 `SCPM` 触过的当前配置不会受到影响。如果你使用 `YaST` 重新配置系统，重建过程将由 `YaST` 处理。
[/content]

[content]
## 7.3 IrDA — 红外数据协会

`IrDA`（红外数据协会）是一种用于红外无线通信的工业标准。今天销售的许多笔记本电脑都配备了兼容 `IrDA` 的收发器，与打印机、调制解调器、局域网或其他笔记本电脑等设备通信。传输速度范围从 2400 bps 到 4 Mbps。

`IrDA` 有两种操作模式。标准模式 `SIR` 通过串口接口访问红外端口。该模式适用于所有系统，并能够满足大多数需求。快速模式 `FIR` 需要特殊的驱动程序。由于缺乏适当的驱动程序，`FIR` 模式不支持所有的芯片类型。在计算机的 `BIOS` 中设置所需的 `IrDA` 模式。`BIOS` 还会显示 `BIOS` 模式下使用的是串口接口。

有关 `IrDA` 的信息可以在 Werner Heuser 编写的 `IrDA` how-to 中找到：http://tuxmobil.org/Infrared-HOWTO/Infrared-HOWTO.html。此外，请参考 Linux `IrDA` 项目网站：http://irda.sourceforge.net。

### 7.3.1 软件

必要的内核模块已包含在内核包中。`irda` 包提供了支持红外接口所需的辅助应用程序。安装该包后，可以在 `/usr/share/doc/packages/irda/README` 找到文档。

### 7.3.2 配置

`IrDA` 系统服务不会通过引导过程自动启动。使用 `YaST` 运行级别模块更改系统服务的设置。或者，使用 `chconfig`。每隔几秒，`IrDA` 就会发送一个“发现包”来检测附近的其他外围设备。这会消耗大量的电池电量。由于如此，`IrDA` 默认禁用的，应在需要时启动。使用 `cirda start` 手动激活，或使用 `cirda stop` 禁用。当接口激活时，所有所需的内核模块将自动加载。

`/etc/sysconfig/irda` 文件仅包含变量 `IRDA_PORT`。这是设置 `SIR` 模式下接口的地方。红外支持包中的脚本 `/etc/irda/drivers` 会设置此变量。

### 7.3.3 使用

数据可以发送到设备文件 `/dev/irplt0` 进行打印。设备 `/dev/irplt0` 的作用就像普通的 `/dev/lp0` 线缆接口，只不过打印数据是通过红外线无线发送的。带有红外接口的打印机就像连接到并行或串口的打印机一样安装。确保打印机在红外接口的可范围内，并且已启动红外支持。

与其他主机以及手机或其他类似设备的通信通过设备文件 `/dev/ircomm0` 进行。例如，西门子 S25 和诺基亚 6210 手机可以使用 `wvcdal` 应用通过红外接口拨接入互联网。只要相应应用程序的设备设置设置为 `/dev/ircomm0`，就可以与 Palm Pilot 同步数据。

只有支持打印机或 `IrCOMM` 协议的设备无需任何调整即可访问。支持 `IROBEX` 协议的设备（如 3Com Palm Pilot）可以使用 `irobexpalm` 和 `irobexceive` 等应用程序访问。参考有关此主题的 `IRHOWTO`。设备支持的协议列在 `iradump` 输出中设备名称后的括号内。局域网协议的支持仍处于“进行中”——它目前还不稳定，但在不久的将来一定会适用于 Linux。

### 7.3.4 故障排除

如果连接到红外端口的设备没有响应，使用命令 `iradump`（root root）检查计算机是否识别了另一个设备。当 Canon BJC-80 打印机在计算机可见时，会显示类似于示例 7.3 的内容：

示例 7.3：`iradump` 的输出

```
21:41:38.453239 xid:cmd 5b62bed5 > fffffff S=6 s=0 (14)
21:41:38.525167 xid:cmd 5b62bed5 > fffffff S=6 s=1 (14)
21:41:38.615139 xid:cmd 5b62bed5 > fffffff S=2 (14)
21:41:38.705170 xid:cmd 5b62bed5 > fffffff S=6 s=0 (14)
```

以下段落描述了用于蓝牙工作所需的主要工具。目前仅提供命令行程序。`Konqueror`（KDE 桌面）和 `Nautilus`（GNOME 桌面）的扩展正在开发中。此功能可能在编辑截止日期后实现。在这种情况下，URL `sdp://` 会显示本地蓝牙设备（物理上连接到主机）以及远程蓝牙设备（通过无线连接访问）。

## 注意

上述蓝牙应用程序的功能可以通过 `man <program_name>` 查看。

## 注意

某些命令只能以 root 权限执行。这包括用于测试远程设备连接的 `l2ping <device_address>` 命令。

## hcitool

`hcitool` 可检测本地和远程蓝牙设备。`hcitool dev` 命令应列出设备。每个检测到的本地设备都会生成一行格式为 `<interface_name> <device_address>` 的输出。

`hcitool name <device_address>` 用于确定设备的名称。如果检测到另一个设备，显示的类别和名称与 `/etc/bluetooth/hcid.conf` 文件中的信息对应。

## hciconfig

使用 `hciconfig` 获取本地设备的更多信息。搜索未物理连接到主机的远程设备，使用 `hcitool inq` 命令。每个检测到的设备都会显示三个值：设备地址、偏移和类别。设备地址非常重要，其他命令使用它来识别目标设备。偏移主要用于技术目的。类别以十六进制值编码。

174 7.4 蓝牙无线连接

## sdptool

`sdptool` 程序用于检查特定设备提供了哪些服务。`sdptool browse <device_address>` 命令返回所有服务。`sdptool search <service_code>` 命令用于搜索特定服务。如果一个设备提供该服务，程序将打印出设备的服务名称及简要描述。可以通过带参数的 `sdptool` 查看所有可能的服务。

## 7.4.5 示例

以下两个示例演示了蓝牙的一些功能。

### 主机之间的网络连接
