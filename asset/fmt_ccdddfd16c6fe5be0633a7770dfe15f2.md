
## 19.4.1 内核事件与模块自动加载

以下是列表 19-7 的内核事件：

```
KERNEL add /devices/platform/musb_hdrc/usb1/1-1 (usb)
KERNEL add /devices/platform/musb_hdrc/usb1/1-1:1.0 (usb)
KERNEL add /class/endpoint/usbdevv1.2_ep1 (usb_endpoint)
KERNEL add /class/usb_device/usbdevv1.2 (usb_device)
KERNEL add /class/endpoint/usbdevv1.2_ep0 (usb_endpoint)
KERNEL add /module/hid (module)
KERNEL add /bus/hid (bus)
KERNEL add /module/mousehid (module)
KERNEL add /bus/hid/generic-usb (drivers)
KERNEL add /devices/platform/musb_hdrc/usb1/1-1/1.0/0003:047D:1035:0001 (hid)
KERNEL add /class/input/mouse0 (input)
KERNEL add /bus/hid/generic-usb (drivers)
KERNEL add /module/mousehid (module)
```

当模块被编译并放置在你的系统中时，`depmod` 工具会收集所有这些字符串并构建 `modules.alias` 文件，供 `modprobe` 引用。查看你 Linux 上的 `modules.alias` 文件，然后查看任何近期 Linux 内核的 `drivers` 子目录，你就可以匹配这些条目。这就是 `udev` 通过 `MODALIAS` 导致模块自动加载的原理。在列表 19-4 的示例规则中，包含 `modprobe` 指令的第二行直接表示以下内容：如果 `DEVICE` 环境变量未设置，且作为内核事件传递进的 `MODALIAS` 环境变量中有文本，则通过 `MODALIAS` 触发 `modprobe` 来加载该模块。任何模块依赖（例如我们示例中的 `hid`）也会被加载。这是 `udev` 的一个非常强大的特性。

## 19.4.2 典型的 udev 规则配置

如所述，控制嵌入式 Linux 上 `udev` 行为的规则集是系统设计人员或嵌入式 Linux 发行版的责任。在某些情况下，包提供者会为其特定功能添加规则。你最近使用的 Linux 发行版提供了一个很好的遵循示例。列表 19-9 显示了在 Moblin 发行版近期快照中找到默认规则列表。

### 列表 19-9 来自 Moblin 发行版的默认 udev 规则

```
$ ls -1 /Moblin/lib/udev/rules.
total 60
-rw-r--r-- root root 652 2009-05-10 04:02 10-moblin.rules
-rw-r--r-- root root 348 2009-05-10 04:02 40-alsa.rules
-rw-r--r-- root root 172 2009-05-10 04:02 50-firmware.rules
-rw-r---- root root 4548 2009-05-10 04:02 50-udev-default.rules
-rw-r---- root root 141 2009-05-10 04:02 60-cdrom-id.rules
-rw-r---- root root 715 2009-05-10 04:02 60-persistent-serial.rules
-rw-r---- root root 1518 2009-05-10 04:02 60-persistent-storage-tape.rules
-rw-r---- root root 708 2009-05-10 04:02 60-persistent-v41.rules
-rw-r---- root root 525 2009-05-10 04:02 61-persistent-storage-add.rules
-rw-r---- root root 390 2009-05-10 04:02 75-cd-aliases-generator.rules
-rw-r---- root root 2430 2009-05-10 04:02 75-persistent-net-generator.rules
-rw-r---- root root 137 2009-05-10 04:02 79-fstab.import.rules
-rw-r---- root root 779 2009-05-10 04:02 80-drivers.rules
-rw-r---- root root 234 2009-05-10 04:02 95-udev-late.rules
```

注意规则文件的分组情况。以类似于 System V initscripts 的方式，使用数字来固定读取顺序。规则文件的处理顺序与列表 19-9 相同。其中一些规则值得深入研究。

`50-udev-default.rules` 规则文件是 `udev` 软件包的一部分（来自当前的 `udev` 快照），并由 `udev` 团队作为示例提供。事实证明，Moblin 版本与 `udev` 软件包中找到此默认版本非常接近。该规则文件为许多常见的 Linux 设备建立了一套默认值，包括作为 `tty`、`pty`、串口设备的字符设备，如 `/dev/null` 和 `/dev/zero` 等内存设备，以及任何 Linux 系统上找到的许多其他设备。

其他规则为特定类别的设备提供了发行版特定的属性和操作。在 Moblin 规则集中，这些包含了用于声设备的 ALSA 规则、CD-ROM 规则定义，以及多组旨在为类设备提供持久设备名称的规则。你可以在 `udev` 文档中找到更多细节，该文档在本章末尾引用。

关于 `udev` 规则的另一个值得提到的注释是：除非使用特定语法触发其他行为，否则 `udev` 规则是累积的。换句话说，你可能为单个设备拥有多条规则，跨越多个规则文件，每条规则匹配不同的属性。由这些规则定义的每个操作都会应用到相关的设备或子系统。例如，你可以将为设备命名的规则与应用权限的规则分开。最近的 Ubuntu 发行版在名为 `20-names.rules` 和 `40-basic-permissions.rules` 的规则文件中有一个此类构想的示例。

查看 `20-names.rules` 和 `40-basic-permissions.rules` 可以很容易地说明 `udev` 规则的“堆叠”性质。单个设备可以匹配多条规则，而这些规则共同定义了指定子系统或设备的操作。例如，考虑声学设备，如 `control0`（声卡接口）。`20-names.rules` 中的一条规则可能如下：

```
KERNEL="control[0-9]*", NAME="%s/%k"
```

这条规则简单地匹配名为 `control0`、`control1` 等内核设备，并分配设备名称 `/snd/%k`。在设备名称前加上 `%k` 指令 `udev` 在 `/dev` 下的名为 `snd` 的子目录下创建该设备节点。因此，你最终获得了 `/dev/snd/control0` 作为声卡的设备节点。下一条来自 `40-permissions.rules` 的规则可能如下：

```
KERNEL="control[0-9]*", MODE="0666"
```

当这条规则被 `udev` 扫描时，它基本上被连接到前面的规则之后，并导致创建的设备节点具有对所有（用户、组和其他）的读写权限。通过这种方式，Linux 发行版可以创建易于维护的清晰集合。在讨论中，你可以看到为类别（例如 `/dev` 下的子目录）分配设备名称的规则维护在一个规则文件中，而应用权限的规则维护在另一个规则文件中。

现在我们已经设置好了一切，是时候启动 udev 守护进程了。你可以在列表 19-10 中看到调用 `/sbin/udevd` 的那行。如果你研究过这个启动脚本，可能会好奇最后几个操作是做什么。

### 19.4.3.1 冷热拔处理

在内核启动过程中，许多子系统被初始化，许多设备被发现并注册，同时在 `/sys` 中生成相应的条目。在本章示例使用的 BeagleBoard 上，`/sys` 中报告了近 200 个设备，这些设备通常会由 udev 处理以便可能的设备创建或驱动程序加载。问题是，udev 在 init 运行一段时间后才会启动；因此，有近 200 个设备仍然没有被 udev 处理。这就是 udev 中存在触发机制的原因。

看看列表 19-10 脚本中的最后两条命令。`udevadm` 会通过回放内核事件并按正常方式处理，使 udev 处理 `/sys` 中的所有条目。为了在不占用书中后续 12 页的情况下说明这种处理的范围，我们将使用以下命令显示触发事件前后 `/dev` 中设备的计数：

```bash
root@beagle:-# find /dev -type c -o -type b -o -type 1 | wc -l 6
```

注意，此 `find` 命令找到的三个设备节点与列表 19-11 的内容完全匹配。我们初始的静态设备集恰好有三个字符设备三个符号链接，总共六个条目。列表 19-11 中的最后两个条目是我们在刚才的 `find` 命令过滤掉的目录。

在列表 19-10 的示例启动脚本中运行 `udevadm trigger` 命令后（这会导致 udev 回放所有内核事件），我们看到创建了 100 多个设备和 400 多个符号链接。以下命令序列演示了：

```bash
root@beagle:-# udevadm trigger
root@beagle:-# udevadm settle
root@beagle:-# find /dev -type c -o -type b | wc -l 135
root@beagle:-# find /dev -type c -o -type b -o -type 1 | wc -l 410
```

现在 udev 已处理内核在启动期间发现的所有设备，我们发现了 132 个新设备节点，总共 135 个（包括我们静态集合中的原始三个）。加上符号链接，我们在 `/dev` 中现在共有 410 个引用设备的文件。这就是 dev 如何“后处理”内核在启动期间创建的设备。从现在起，只要 udev 守护进程运行，内核就会向 udev 报告任何添加或删除的设备，udev 会根据其设置的规则对其进行处理。

## 19.5 加载平台设备驱动程序

平台设备驱动程序可以使用 udev 轻松动态加载。udev 软件包中的默认规则可以安装到你的嵌入式系统中。该规则看起来类似于列表 19-4 中的第一个规则。为了方便起见，在此复制：

```
DRIVER!="?*", ENV(MODALIAS)="?*", RUN(ignore_error)+=/sbin/modprobe -b $env{MODALIAS}
```

该规则表示当满足以下条件运行时执行 `modprobe` 并将 `MODALIAS` 的值传递给 `modprobe`：MODALIAS 被驱动程序设置，而 DRIVER 环境变量未设置。只要你的驱动程序包含一个格式正确的 `MODULE_ALIAS` 宏，它就会被传递给 `modprobe` 并与 `depmod` 生成的 `modules.alias` 文件中收集的信息进行匹配。这在第 19.4.1 节中有详细解释。

例如，让我们看看 BeagleBoard 上 OMAP3530 Inventra 双角色 USB 控制器的平台驱动。列表 19-12 显示了来自近期 Linux 内核的 USB 主机驱动的几行。最后一行包含魔法代码，转换为 `modules.alias` 文件中的条目，`modprobe` 使用它来选择哪种驱动程序。

### 列表 19-12 musb_hdrc.c 部分

```c
#define MUSB_DRIVER_NAME "musb_hdrc"
const char musb_driver_name[] = MUSB_DRIVER_NAME;

MODULE_DESCRIPTION(DRIVER_INFO);
MODULE_AUTHOR(DRIVER_AUTHOR);
MODULE_LICENSE("GPL");
MODULE_ALIAS("platform:" MUSB_DRIVER_NAME);
```

`MODULE_ALIAS` 宏实际上创建了一个字符字符串（const char），并放置在设备驱动程序（模块）对象文件的特殊区域中。该字符串类似于环境变量，以 `alias="string"` 的形式存在。这个特殊区域被标记为 `.modinfo`，包含描述驱动程序各个方面的属性。你可以使用你交叉版本的 `readelf` 查看此节头。记得我们在第 13 章“开发工具”中涵盖过 `readelf` 的细节。可以使用以下命令查看 `.modinfo` 字符串：

```bash
$ armv7_vfp_le-readelf -e drivers/usb/musb/musb_hdrc.ko | grep modinfo
[11] .modinfo PROGBITS 00000000 0063dc 001ec 00 A 0 0 0
```

## 19.6 自定义 udev 行为

你的想象力可能是你使用 udev 能做的事情的极限。一方面，你可以在设备添加或删除时运行程序。例如，可以使用如下规则在有人插入 USB 存储设备时启动一个进程：

```
ACTION="add", KERNEL="sd[a-d][0-9]", RUN="/bin/myloader"
```

你的程序 `/bin/myloader` 处理这种情况。接下来，你的程序可以验证新安装设备的内容并启动任何所需的操作。这是 udev 上自动化安装新镜像的一种方法。如果你选择这种方法，可能是派生并分离 udev 父进程以完成并返回。这种操作可以避免在 udev 未来决定杀死看似耗时的子进程时出现意外。此外，考虑环境变量。当你的程序运行时，它继承了 udev 提供的最小环境。这可能无法满足你的需求。你可能需要为你的特殊处理器创建自己的环境以完成任务。

### 19.6.1 udev 自定义示例：USB 自动挂载

列表 19-13 展示了一组可以将 USB 驱动器自动挂载到你的嵌入式设备上的规则。

### 列表 19-13 自动挂载
