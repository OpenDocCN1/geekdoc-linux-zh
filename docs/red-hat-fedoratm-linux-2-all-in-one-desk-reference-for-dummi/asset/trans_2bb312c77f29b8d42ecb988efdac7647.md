
## 482 管理可加载驱动程序模块

### 使用 udev 进行持久设备命名

Linux 内核 2.6 基于以下特性，引入了一种处理设备的新方法：

-   **sysfs**：2.6 内核提供了 sysfs 文件系统，它挂载在文件系统的 `/sys` 目录下。sysfs 文件系统展示了系统中的所有设备以及每个设备的详细信息。这些信息包括设备在总线上的位置、名称和序列号等属性，以及设备的主设备号和次设备号。
-   `/sbin/hotplug`：每当设备被添加或移除时，都会调用此程序。随后它可以执行处理该设备所需的一切操作。
-   `/sbin/udev`：此程序负责基于设备特性（如序列号、总线上的设备编号）或基于通过文本文件 `/etc/udev/udev.rules` 设置的一组规则而由用户分配的名称，对动态命名的设备进行管理。

目前，2.6 内核同时包含 `udev` 和旧的静态 `/dev` 设备目录。`udev` 程序的配置文件是 `/etc/udev/udev.conf`。根据该配置文件中的设置，`udev` 会自动在 `/udev` 目录中创建设备节点。只有编辑了 `/etc/udev/udev.conf` 中的 `udev_root*="/udev/*"` 这一行，`udev` 才能开始管理 `/dev` 目录中的设备节点。现阶段，只需了解 `udev` 的存在即可，但在未来某个内核版本中，它可能会成为 Linux 中动态管理设备的唯一方式。

![](img/9f89727199836b0f871f1745838aa8b2_508_0.png)

### 管理可加载驱动程序模块

要使用任何设备，Linux 内核必须包含相应的驱动程序。如果驱动程序代码以*单体*程序的形式链接到内核中（即形式为单个大型文件的程序），那么添加新驱动程序就意味着需要重新编译内核以包含新的驱动程序代码。重新编译内核意味着你必须在启动新内核并重启 PC 后，才能使用新的设备驱动程序。幸运的是，Linux 内核采用了模块化设计，从而免除了重启的麻烦。Linux 设备驱动程序可以创建为模块形式，内核可以在无需重启 PC 的情况下加载和卸载这些模块。

驱动程序模块是更广泛的软件模块类别——可加载内核模块（Loadable Kernel Modules）的一种。其他类型的内核模块包括支持新类型文件系统的代码、网络协议模块，以及解释不同格式可执行文件的模块。

![](img/9f89727199836b0f871f1745838aa8b2_508_1.png)

## 加载和卸载模块

你可以通过使用一组命令来管理可加载的设备驱动程序模块。使用其中一些命令需要以 root 身份登录。表 5-1 总结了一些常用的模块命令。

**表 5-1 管理内核模块的命令**

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `insmod` | 将模块插入内核 |
| `rmmod` | 从内核中移除模块 |
| `depmod` | 确定模块之间的相互依赖关系 |
| `ksyms` | 显示符号列表以及定义该符号的模块名称 |
| `lsmod` | 列出当前已加载的所有模块 |
| `modinfo` | 显示关于内核模块的信息 |
| `modprobe` | 智能地插入或移除单个模块或一组模块（例如，如果模块 A 需要 B，那么当要求加载 A 时，modprobe 会自动加载 B） |

如果你必须使用这些命令中的任何一个，请登录为 root，或在终端窗口中输入 `su -` 以成为 root。

要查看当前已加载的模块，请输入：

```bash
lsmod
```

你会看到模块列表。例如，这是我在一台运行 Fedora Core 的笔记本电脑上的列表：

```text
Module             Size  Used by
hid                50580  0
ntfs               78924  1
ide_cd             32644  0
snd_mixer_oss      14336  1
snd_intel8x0       30120  1
snd_ac97_codec     53768  1
snd_pcm            84744  1
snd_timer          25604  1
gameport           4352   1
snd_page_alloc     9092   2
snd_mpu401_uart    7680   1
snd_rawmidi        21792  1
snd_seq_device     6792   1
snd                44516  8
snd_mixer_oss,snd_intel8x0,snd_ac97_codec,snd_pcm,snd_timer,snd_mpu401_uart,snd_rawmidi,snd_seq_device
```

| 模块 | 大小 | 引用计数 | 依赖 |
| :--- | :--- | :--- | :--- |
| soundcore | 8032 | 2 | snd |
| nls_utf8 | 2048 | 1 | |
| cifs | 145280 | 2 | |
| ipv6 | 211200 | 10 | |
| lp | 9452 | 0 | |
| autofs | 17536 | 0 | |
| orinoco_cs | 7816 | 1 | |
| orinoco | 45196 | 1 | orinoco_cs |
| hermes | 7040 | 2 | orinoco_cs,orinoco |
| ds | 10628 | 3 | orinoco_cs |
| venta_socket | 12928 | 1 | |
| pcmcia_core | 52964 | 3 | orinoco_cs,ds,venta_socket |
| ipt_REJECT | 5248 | 1 | |
| ipt_state | 1920 | 6 | |
| ip_conntrack | 25008 | 1 | ipt_state |
| iptable_filter | 2560 | 1 | |
| ip_tables | 13952 | 3 | |
| 3c59x | 33192 | 0 | |
| o8c1394 | 31896 | 0 | |
| ieee1394 | 286776 | 1 | o8c1394 |
| sd_mod | 13216 | 0 | |
| parport_pc | 20928 | 1 | |
| parport | 36808 | 2 | lp,parport_pc |
| microcode | 5792 | 0 | |
| floppy | 54192 | 0 | |
| sg | 28448 | 0 | |
| sr_mod | 13988 | 0 | |
| cdrom | 29852 | 2 | ide_cd,sr_mod |
| usb_storage | 59360 | 0 | |
| scsi_mod | 102332 | 4 | sd_mod,sg,sr_mod,usb_storage |
| uhci_hcd | 35740 | 0 | |
| usbscore | 92724 | 5 | hid,usb_storage,uhci_hcd |
| button | 5016 | 0 | |
| battery | 7436 | 0 | |
| asus_acpi | 8984 | 0 | |
| ac | 3980 | 0 | |
| ext3 | 94760 | 2 | |
| jbd | 65432 | 1 | ext3 |

不出所料，模块列表取决于系统中安装的设备类型。

第一列按从后到前的顺序列出模块名称。因此，列表中的第一个模块是最后加载的。Size 列显示模块在 PC 内存中占用的字节数。其余各列显示关于每个模块的其他信息，例如当前有多少应用程序正在使用该模块，以及需要该模块的其他模块的名称。

`lsmod` 显示的列表包括所有类型的 Linux 内核模块，而不仅仅是设备驱动程序。例如，最后两个模块 — `jbd` 和 `ext3` — 都是 EXT3 文件系统（Linux 最新的文件系统）的一部分。

-   **记住**：除了 `lsmod`，另一个常用的模块命令是 `modprobe`。当你需要手动加载或移除一个或多个模块时，请使用 `modprobe`。`modprobe` 最好的地方在于，你无需担心模块是否需要其他模块才能工作。`modprobe` 命令会自动加载任何模块所需的其他模块。例如，在我的系统中，我可以使用以下命令手动加载声音驱动程序：

    ```bash
    modprobe sound-slot-0
    ```

    此命令会促使 `modprobe` 加载使声音工作所需的所有内容。

-   **提示**：你可以使用带有 `-r` 选项的 `modprobe` 来移除模块。例如，要移除声音模块，我使用以下命令：

    ```bash
    modprobe -r sound-slot-0
    ```

    此命令会移除 `modprobe sound-slot-0` 命令所加载的所有模块。

## 使用 /etc/modprobe.conf 文件

当我使用模块名称 `sound-slot-0` 时，`modprobe` 命令是如何知道它需要加载 `snd-intel8x0` 驱动程序模块的？答案就在 `/etc/modprobe.conf` 配置文件中。该文件包含一行，告诉 `modprobe` 当看到模块名称 `sound-slot-0` 时加载什么。

要查看 `/etc/modprobe.conf` 的内容，请输入：

```bash
cat /etc/modprobe.conf
```

在我的一台 Fedora Core PC 上，该文件包含以下行：

```text
alias eth0 3c59x
alias usb-controller uhci-hcd
alias sound-slot-0 snd-intel8x0
```

每一行以关键字 `alias` 开头的行都为实际的驱动程序模块定义了一个标准名称。例如，第一行将 `3c59x` 定义为别名 `eth0`（代表第一块以太网卡）的实际驱动程序名称。类似地，第三行将 `snd-intel8x0` 定义为使用名称 `sound-slot-0` 时要加载的模块。

*modprobe* 命令查阅 /etc/modprobe.conf 文件，将别名转换为驱动程序模块的真实名称，并执行其他任务，例如获取驱动程序模块的参数。例如，你可以插入以 *options* 关键字开头的行，以提供驱动程序可能需要的参数值。

例如，要将以太网驱动程序的调试级别参数设置为 5（该参数会在 /var/log/messages 中生成大量信息），我在 /etc/modprobe.conf 文件中添加以下行：

```text
options 3c59x debug=5
```

该行指定 *5* 为 *3c59x* 模块中名为 *debug* 的参数的值。

如果你想知道某个模块接受的参数名称，请使用 *modinfo* 命令。例如，要查看 *3c59x* 驱动程序模块的信息，我输入：

```bash
modinfo 3c59x | more
```

从输出的结果中，我可以看出 *debug* 是设置调试级别的参数名称。

不幸的是，*modinfo* 命令显示的信息可能有些晦涩难懂。唯一的安慰是，你通常只需使用图形实用程序来配置设备，该实用程序会自动处理向配置文件（如 /etc/modprobe.conf）中添加所需内容。

## 管理 USB 设备

Fedora Core 内置了对通用串行总线（USB）的支持——这是一种逐渐取代 PC 串行端口和并行端口功能，以及键盘和鼠标端口功能的串行总线。如今，许多 PC 外设——如鼠标、键盘、打印机、CD 刻录机、扫描仪、调制解调器、数码相机、存储卡等——都设计为通过 USB 端口连接到 PC。

USB 版本 1.1 支持高达 12 Mbps 的数据传输速率——即每秒 1200 万位或每秒 1.5MB——相比之下，标准串行端口的传输速率为 115 Kbps 或 0.115 Mbps。你可以在单个 USB 总线上菊花链连接多达 127 个设备。该总线还为设备提供电源，并且可以在 PC 运行时连接或移除设备——这种功能通常被称为*热插拔*或*热交换*。USB 版本 2.0（或 USB 2.0 或

![](img/9f89727199836b0f871f1745838aa8b2_512_0.png)

