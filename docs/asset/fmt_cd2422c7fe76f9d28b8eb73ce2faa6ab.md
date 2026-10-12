
默认 udev 规则将使用为它们保留的官方符号名称为你的设备提供名称，例如打印机的 `lpn`，其中 `n` 是打印机编号。对于固定设备（如固定打印机），这通常足够了。但对于可移动设备（例如在不同时间连接到 USB 端口的 USB 打印机），名称可能无法指向同一台打印机。例如，如果你有两个 USB 打印机（一台 Epson 和一台 Canon），并且先连接 Epson 后连接 Canon，那么 Epson 将获得 `usb/lp0` 和 `usb/lp1` 的名称。然而，如果你先拔掉并重新连接 Canon，然后连接 Epson，那么 Canon 将获得 `usb/lp0` 的名称，而 Epson 将获得 `usb/lp1`。如果你希望始终拥有相同的名称（例如 Epson 为 `epson-pr`，Canon 为 `canon-pr`），你需要创建自己的规则来检测打印机并赋予它们自定义的符号名称。

有助于创建持久性名称的持久规则是使用 `66-input-persistent.rules` 和 `65-storage-persistent.rules`。关键是使用唯一标识符来识别它，然后使用官方名称命名，但赋予它一个唯一的名称。然后你可以使用相同的符号名称（如 `canon-pr`）始终引用那台未插入的打印机。在这个示例中，使用了 Canon 打印机序列号等信息来识别 Canon 打印机。随后是官方名称 `usb/lp0` 或 `usb/lp1`（取决于是否先插入了另一台打印机），然后赋予它一个唯一的符号名称 `canon-pr`，该名称将引用无论官方名称是什么的。保留官方名称（如 `lp0`）可以保留许多应用程序对设备的访问。

### 检测与命名

你使用关于设备的 `/sys` 文件系统信息通过符号链接来检测设备。唯一的 `/sys` 设备信息（如供应商名称或编号）被用于引用设备。要获取这些信息，你需要查询 `/sys` 文件系统。你通过 `udevinfo` 命令执行此操作。

首先你需要知道设备在 `/sys` 文件系统中的位置。你插入设备，系统将使用官方名称自动对其进行配置和命名。例如，插入 USB 打印机将为它创建一个 `dev/usb/lp0` 设备名称。你可以使用此名称找到 USB 打印机信息在 `/sys` 中的位置。使用带有 `-q path` 参数的 `udevinfo` 命令查询 `/sys` 路径，并带有设备完整路径的 `-n` 参数来识别你要搜索的设备。以下命令将显示打印机 `lp0` 的 `/sys` 路径。在这种情况下，是 `usb` 下的类目录。路径假设为 `/sys`。

```
udevinfo -q -n /dev/usb/lp0/class/usb/lp0
```

一旦获得了设备的 `/sys` 路径，可以使用它来显示相关信息。使用 `udevinfo` 命令配合 `-a` 选项显示设备信息，并使用 `-p` 选项指定其在 `/sys` 中的路径。输出非常详尽，你应该将输出重定向到 `less`。

```
udevinfo -a -p /sys/class/usb/lp0 | less
```

## 第 31 章：设备与模块

输出中的许多是所使用的总线信息，例如序列号、产品编号或制造商。某些设备使用不同的总线，信息可能会不同。在 udev 规则中设置键时确保使用总线信息。

```
BUS="usb"
ATTR(serial)="30HCR"
ATTR(manufacturer)="Canon"
ATTR(idproduct)="1074"
ATTR(product)="S30"
```

你可以在 udev 规则的 `ATTRS` 键中使用许多信息。`ATTRS`（属性）用于获取有关设备的 `/sys` 信息。你使用带有大括号的字段。你可以将该字段匹配一个值以引用特定设备。一旦知道了设备的 `/sys` 序列号，你可以在 udev 规则的 `ATTRS` 键中使用进行唯一引用。以下键检查 Canon 打印机的序列号：

```
ATTR(serial)="30HCR"
```

用户规则可以使用 `/sys` 信息添加你自己的符号链接，以唯一标识打印机并使用其官方内核名称命名设备。前两个键 `BUS` 和 `ATTRS` 指定特定的打印机。在这种情况下，打印机的序列号被用于唯一标识它，使用 `%s` 代码引用。`NAME` 键将使用官方内核名称命名打印机。设备文件将放在 `usb%` 子目录下。`SYMLINK` 键定义了 `/dev/usb` 目录下使用的唯一名称 `canon-pr`。

```
BUS="usb", ATTRS(serial)="30HCR", NAME="usb/%k", SYMLINK="usb/canon-pr"
```

规则动态应用。要运行新规则，只需连接你的 USB 打印机（或拔掉重新连接）。你会看到设备文件自动创建。

### 权限字段：`MODE`, `GROUP`, `OWNER`

赋予不同设备文件的由 udev 规则中的权限规则决定。Red Hat、Fedora 类似的发行版中位于 `50-udev.rules` 文件，而在 Debian 和类似的发行版中位于 `40-permissions.rules` 文件。`MODE` 字段是一个八进制权限设置，与文件权限相同。通常设置为 `660`，即所有者和组的读写权限。支持使用 `*`、`?` 和 `[]` 运算符进行模式匹配。以下示例将音频设备的所有者和组设置为具有所有者和组的读写权限：

```
KERNEL="audio*", MODE="0660"
```

软盘设备项指定了一个 `floppy` 组。

```
KERNEL="fd[0-1]*", GROUP="floppy", MODE="0660"
```

USB 设备使用 `lp` 组，模式为 `660`。

```
KERNEL="usb/lp*", GROUP="lp", MODE="0660"
```

磁带设备使用 `disk` 组。

```
KERNEL="npt*", GROUP="disk", MODE="0660"
```

默认设置将所有者和组设为 `root`，并具有读写权限（`600`）。

```
KERNEL="*", OWNER="root", GROUP="root", MODE="0600"
```

## 硬件抽象层：HAL

硬件抽象层（HAL）的目的是抽象访问设备的过程。应用程序不应该了解任何设备或其符号名称。应用程序只需要请求特定类型的设备，然后由 HAL 作为服务提供可用资源。设备实现对应用程序隐藏了。

HAL 通过 D-BUS 结构使得桌面和应用程序能够轻松访问设备。设备由 HAL 进程 `haldaemon` 提供。与设备对象的交互由 freedesktop.org HAL 服务提供，该服务由 `/org/freedesktop/HAL/Manager` 管理。

HAL 是一个用于设备的信息服务。这些信息可以被专门程序用于维护设备配置文件。在管理可移动设备时情况如此。如 CD-ROM 光盘或 USB 读器等可移动设备由带有 HAL 信息的特殊调用（callouts）进行管理，用于检测此类项的插入。这可能会令人困惑。调用程序执行实际任务，但 HAL 提供设备信息。例如，虽然通过 `hal-call-system-mount` 挂载了设备，但选项和挂载点是在 HAL 设备信息文件中指定的，这些文件设置了存储管理策略。

HAL 对用于管理文件系统的 `/etc/fstab` 文件具有关键影响。在 `/etc/fstab` 文件中不再维护像 CD-ROM 类的可移动设备的条目。这些设备由 HAL 直接通过其存储调用程序进行管理，例如使用 `hal-storage-mount` 挂载设备，或使用 `hal-storage-eject` 移除设备。实际上，你现在必须使用 HAL 设备信息文件来管理你的可移动文件。

HAL 是 freedesktop.org 的一个软件项目，该项目专注于开源桌面工具。可以在 freedesktop.org 的 `software/HAL` 页面查看最新的 HAL 规范文档，以获取关于 HAL 如何工作的详细说明（参见 HAL 页面上的规范链接：Latest HAL Specification）。该文档非常详尽且完整。

### HAL 进程与 hal-device-manager (`hal-gnome`)

HAL 进程 `hal` 由 `haldaemon` 进程命名。HAL 为你所有设备提供的信息可以由 HAL 设备管理器显示。HAL 设备管理器是 `hal-gnome` 包的一部分。安装后，你可以从“系统 | 管理 | 硬件”项访问它。HAL 设备管理器命名为 `hal-device-manager`。
