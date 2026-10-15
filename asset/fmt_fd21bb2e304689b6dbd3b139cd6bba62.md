
```
SUBSSTEM="net", RUN+=/etc/sysconfig/network-scripts/net.hotplug
```

| udev 调用 | 说明 |
|---|---|
| `ata_id` | 返回 ATA 存储设备序列号的调用脚本 |
| `bluetooth_serial` | 蓝牙设备序列号的调用脚本 |
| `cdrom` | 返回 CD/DVD-ROM 设备序列号的调用脚本 |
| `scsi_id` | 返回 SCSI 存储设备序列号的调用脚本 |
| `path_id` | 为设备生成唯一路径名称的调用脚本 |
| `ata_id` | 返回 ATA 存储设备序列号的调用脚本 |
| `usb_id` | 返回 USB 设备序列号的调用脚本 |
| `vol_id` | 返回卷卷存储设备序列号的调用脚本 |
| `create_floppy_devices` | 创建软驱设备 |
| `rename_device` | 重命名设备 |
| `write_cd_rules` | 写入持久性 CD/DVD-RW/ROM 规则 |
| `write_net_rules` | 写入持久性网络设备规则 |

表 17-7: Udev 调用（脚本），`/lib/udev`

## 创建 udev 规则

如果你想创建自己的规则，可以将它们放在单独的规则文件中。（注：原文此处存在大量重复句子，翻译已按逻辑意图处理）

### 第17 章：设备 433

取决于是否先插入打印机，然后会被赋予一个唯一的符号名称 `canon-pr`，该名称将引用官方名称（无论官方名称为何）。保留官方名称 `libp0` 可以保留许多应用程序对设备的标准访问方式。

你使用 `/sys` 文件系统关于设备的信息来检测要通过符号链接引用的正确设备。唯一的 `/sys` 设备信息（如厂商序列号或厂商名称）可用于唯一引用设备。要获取这些信息，你需要查询 `/sys` 文件系统设备。你可以通过 `udevinfo` 命令来完成此操作。

首先，你需要知道设备在 `/sys` 文件系统中的位置。你插入设备后，系统会自动使用官方名称对其进行配置和命名。例如，插入 USB 打印机将为它创建一个 `/dev/usb/lp0` 设备名称。你可以使用该设备找到打印机信息在 `/sys` 中的位置。使用带有 `-q path` 选项的 `udevinfo` 命令查询 `/sys` 路径，并添加 `-n` 以及设备的完整路径来识别你正在搜索的设备。以下命令将显示名为 `lp0` 的设备的 `/sys` 路径。在这种情况下，设备位于路径下的类目录下。假设路径将为 s330。

```
udevinfo -q -n /dev/usb/lp0
/class/usb/lp0
```

一旦获得了设备的 `/sys` 路径，你就可以使用该路径显示有关它的信息。使用带有 `-n` 选项的 `udevinfo` 命令显示设备的所有信息，并使用 `-p` 选项在 `/sys` 文件系统中指定该设备。列表可能非常详细，因此你可能需要将输出管道到 `less` 或重定向到文件。

```
udevinfo -a -p /sys/class/usb/lp0 | less
BUS="usb"
ATTR(serial)="300HCR"
ATTR(manufacturer)="Canon"
ATTR(idproduct)="1074"
ATTR(product)="S330"
```

你可以在 udev 规则的 `ATTRS` 键中使用这些许多信息来识别设备。`ATTRS` 键（属性）用于获取有关设备的 `/sys` 信息。使用括号中引用的字段配合 `ATTRS` 键。然后你可以将该字段与某个值匹配，从而使用有效的字段值匹配来引用特定设备。一旦知道设备的 `/sys` 序列号，你就可以在 udev 规则的 `ATTRS` 键中使用它来唯一引用设备。以下键检查设备序列号字段 Canon 打印机的序列号：

```
ATTRS(serial)="300HCR"
```

可以为 Canon 打印机创建一个用户规则。在其他规则中，你可以使用 `/sys` 信息添加自己的符号链接来唯一标识打印机，并使用官方内核名称命名设备。前两个键，

### 第3部分：设备与文件系统 434

`SUBSYSTEM`、`ATTRS` 指定特定的打印机。在这种情况下，使用打印机的序列号来唯一标识它。`NAME` 键将使用官方内核名称为打印机命名，并始终使用 `%k` 代码引用。由于是 USB 打印机，其设备文件将放置在 `usb` 子目录 `/dev/usb` 下。然后 `SYMLINK` 键定义了要使用的唯一符号名称 `/dev/usb` 目录下的 `canon-pr`。

```
SUBSYSTEM="usb", ATTRS="300HCR", NAME="usb/%k", SYMLINK="usb/canon-pr";
```

规则是实时动态应用的。要运行新规则，只需插入你的 USB 打印机（或拔出并重新插入）。你将看到设备文件自动生成。

## 权限与所有者字段：MODE, GROUP, OWNER

附加字段为设备提供了所有权权限属性。`MODE` 字段用于指定权限，`OWNER` 用于指定拥有设备的用户（通常是 root 用户）。`GROUP` 字段允许将设备添加到可以控制访问的组中。

`MODE` 字段是一个八进制权限设置，与文件权限相同。通常将其设置为 660，即所有者和组的读写权限。支持使用 `*`、`?` 和 `[]` 运算符进行模式匹配。以下示例将鼠标设备设置为所有者读/写和组读权限，0640：

```
KERNEL="mouse[mice|event*], NAME="input/%k", MODE="0640"
```

软盘设备 (`fd`) 条目指定了一个软盘组。

```
KERNEL="fd[0-9]*", GROUP="floppy"
```

并行设备 (`parport`) 被分配给 `lp` 组。

```
KERNEL="parport[0-9]*", GROUP="lp"
```

磁带设备 (`pt` 和 `nt`) 使用 `disk` 组。

```
KERNEL="ct[0-9]*|nt[0-9]*", GROUP="disk"
```

默认设置将 `OWNER` 和 `GROUP` 设置为 root，并具有所有者读写权限 (600)。

```
KERNEL="*", OWNER="root" GROUP="root", MODE="0600"
```

## 硬件抽象层：HAL

硬件抽象层 (`HAL`) 的目的是抽象应用程序访问设备的过程。应用程序不需要了解设备，即使是它的符号名称也不需要。它只需要请求某种类型的设备，然后由像 HAL 这样的服务提供可用资源。有了 HAL，设备实现对应用程序是隐藏的。

HAL 通过使用 D-BUS（设备总线）结构让桌面和应用程序能够轻松使用设备。设备由应用程序可以轻松访问的对象进行管理。D-BUS 服务由 HAL 守护进程 `haldaemon` 提供。与设备进行交互。

### 第17 章：设备 435

HAL 是 `www.frektop.org` 的软件项目。请访问 `http://frektop.org`（搜索 HAL）查看最新的 HAL 规范，获取 HAL 如何工作的详细说明。文档非常详尽。还可以下载并安装 `hal-docs`。在 `/usr/share/doc/hal/` 目录下，你会找到详细的文档 (`spec-hal-spec`) 以及通用概述。使用你的浏览器读取 `hal-spec.html`（版本号 0.5.12 会随 HAL 更新而变化）。

```
The HAL 和工具 36

HAL 守护进程由 `haldaemon` 进程运行。HAL 守护进程提供的所有设备信息可以使用 HAL 工具显示，例如使用 `ihal` 列出 HAL 设备，使用 `hal-get-property` 显示设备的属性。`hal-get-property` 使用 `--udi` 选项获取设备的唯一标识符并使用 `--key` 选项指定属性名称。

`hal-get-property` 使用 `--udi` 和 `--key` 选项。可以使用 `--string`、`--bool`、`--int` 等选项设置值，并使用 `--trislist` 等选项配合 `--remove` 选项删除属性。

`hal-find-by-property` 允许你提供模式来搜索 HAL 设备属性字段。`--key` 选项根据名称搜索。匹配设备的 UID 将输出。`hal-find-by-capability` 允许你根据设备能力搜索 HAL 设备。`--capability` 选项允许你提供模式进行搜索。匹配设备的 UID 将被显示。

对于移动介质，HAL 将继续轮询设备以便在插入或连接时快速检测。如果设备配置损坏，可能会导致问题，因为会增加管理设备的开销。如果你在使用移动介质遇到困难，可以使用 `hal-disable-polling` 轮询。`--udi` 选项引用设备。你也可以使用 `--enable-polling` 选项恢复轮询。
```

`file://usr/share/doc/hal-0.5.12/spec/hal-spec.html`
