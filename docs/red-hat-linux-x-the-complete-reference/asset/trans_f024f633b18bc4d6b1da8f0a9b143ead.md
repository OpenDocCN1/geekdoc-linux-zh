
![](img/32a48d8db4c23e6e2eb70d1e5034c976_774_0.png)

# ABC Amber CHM 转换器试用版

请注册以移除此横幅。

[http://www.processestext.com/abcchm.html](http://www.processestext.com/abcchm.html)

## 视频、电视和 DVD 设备

用于电视、视频和 DVD 设备的设备名称列于表 32-4 中。DVD 和 TV 解码器的驱动程序已开发完成。mga4linux（[marvel.sourceforge.net](marvel.sourceforge.net)）正在为 Marvel G200 等 Matrox 多媒体卡开发视频支持。通用 ATI 电视和叠加软件（GATOS）（[gatos.sourceforge.net](gatos.sourceforge.net)）已为 ATI 视频卡当前不支持的功能，特别是电视功能，开发了驱动程序。BTTV 驱动项目开发了 Booktree 视频芯片的驱动程序。Creative Labs 赞助了 Creative 系列 DVD DXR2 解码器的 Linux 驱动程序（[opensource.creative.com](opensource.creative.com)）。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_775_0.png)

### 模块

Linux 内核采用模块机制来支持不同的操作系统功能，包括对各种设备（如声卡和网卡）的支持。在许多情况下，您可以选择将设备支持实现为模块，或者直接将其编译为内置内核功能，后者需要重新构建内核（参见第 33 章）。更安全且稳健的解决方案是使用模块。模块是 Linux 内核的组件，可按需加载。要为新设备添加支持，您现在只需指示内核加载该设备的模块即可。在某些情况下，您可能只需重新编译该模块即可提供对设备的支持。使用模块的额外优点在于减小内核程序的大小，并使系统更加稳定。内核只在需要时在内存中加载模块。如果某个模块失败，只有该模块停止运行，而不会影响整个系统。例如，用于调制解调器连接的 PPP 网络接口模块，只需在您连接到 ISP 时才需要使用。

### 内核模块工具

您的系统所需的模块通常在安装过程中确定，基于您提供的配置类型信息以及 Kudzu 执行的自动检测。例如，如果您的系统使用了一种您在安装期间指定类型的以太网卡，系统就会加载该卡的模块。然而，您可以手动控制为您的系统加载哪些模块。实际上，这允许您以任何想要的方式定制内核。您可以使用多个命令、配置工具和守护进程来管理内核模块。2.4 Linux 内核包含内核模块加载器（Kmod），它具有自动加载所需模块的能力。内核中必须启用内核模块加载支持，但这通常被视为标准配置的一部分，并包含在 Red Hat 发行版中。此外，多个工具允许您手动加载和卸载模块（如果必须的话）。内核模块加载器使用特定的内核命令来执行加载或卸载模块的任务。modprobe 命令是一个通用命令，它调用 insmod 来加载模块，调用 rmmod 来卸载它们。这些命令列于表 32-5 中。特定模块的选项、通用配置以及特定的模块加载可以在 /etc/modules.conf 文件中指定。您可以使用此文件自动加载和配置模块。您也可以在启动提示符或 grub.conf 中指定要加载的模块（参见第 27 章）。

表 32-4：视频设备

| 设备名称 | 设备类型 |
|---|---|
| /dev/video | 视频采集接口 |
| /dev/vfx | 视频特效接口 |
| /dev/codec | 视频编解码器接口 |
| /dev/vout | 视频输出接口 |
| /dev/radio | AM/FM 无线电设备 |
| /dev/vtx | 图文电视接口芯片 |
| /dev/vbi | 数据服务接口 |

### 模块文件和目录

模块文件名的扩展名为 .o。内核模块位于 /lib/modules/version 目录中，其中 version 是当前内核的版本号。2.4.22-1 内核的目录是 /lib/modules/2.4.22-1。当您在系统中安装新内核时，会为它们生成新的模块目录。访问当前内核目录的一种方法是使用 uname -r 命令生成内核版本号。此命令需要使用反引号。

```
cd /lib/modules/`uname -r`
```

在此目录中，内核模块位于 /kernel 目录中。/kernel 目录内有几个子目录，包括 /drivers 目录，该目录包含声卡驱动程序或视频驱动程序等模块的子目录。这些子目录有助于对模块进行分类，使其更容易查找。例如，kernel/drivers/net 目录包含以太网卡模块，kernel/drivers/sound 目录包含声卡模块。

表 32-5：内核模块命令

| 命令 | 描述 |
|---|---|
| lsmod | 列出当前加载的模块。 |
| insmod | 将模块加载到内核中。不检查依赖项。 |
| rmmod | 卸载当前加载的模块。不检查依赖项。 |
| modinfo | 显示关于模块的信息：-a（作者）、-d（描述）、-p（模块参数）、-f（模块文件名）、-v（模块版本）。 |
| depmod | 创建一个依赖项文件，列出指定模块可能依赖的所有其他模块。 |
| modprobe | 加载模块及其可能需要的任何依赖模块。使用 depmod 生成的依赖项列表文件：-r（卸载模块）、-l（列出模块） |

### 使用 /etc/modules.conf 管理模块

如前所述，有几个命令可用于管理模块。lsmod 命令列出当前加载到内核中的模块，modinfo 提供关于特定模块的信息。虽然您可以使用 insmod 和 rmmod 命令直接加载或卸载模块，但对于这些任务，您应该仅使用 modprobe。（参见表 33-5 了解内核模块命令。）然而，通常给定模块需要加载其他模块。例如，Sound Blaster 声卡模块 sb.o 还需要加载 sound.o 模块。

### depmod 命令

而不是手动尝试确定给定模块依赖哪些模块，您使用 depmod 命令为您检测依赖项。depmod 命令生成一个列出给定模块依赖的所有模块的文件。depmod 命令生成分层列表，注明哪些模块应首先加载以及加载顺序。然后，要加载模块，您使用 modprobe 命令并使用该文件。modprobe 读取 depmod 生成的文件，并以正确的顺序加载任何依赖模块以及您想要的模块。在第一次使用 modprobe 之前，您需要执行一次带有 -a 选项的 depmod。输入 depmod -a 会创建所有模块依赖项的完整列表。此命令在当前内核版本的模块目录 /lib/modules/version 中创建一个名为 modules.dep 的文件。

```
depmod -a
```

### modprobe 命令

要手动安装模块，请使用 modprobe 命令和模块名称。您可以添加模块可能需要任何参数。以下命令安装 Sound Blaster 声卡模块，并带有 I/O、IRQ 和 DMA 值。modprobe 还支持使用 * 字符，使您能够使用模式选择多个模块。此示例使用了声卡常用的几个值。您应该使用为您系统中的声卡推荐使用的值。

```
modprobe sb io=0x220 irq=5 dma=1
```

要发现模块接受哪些参数，您可以使用带有 -p 选项的 modinfo 命令。

```
modinfo -p sb
```

您可以使用 -l 选项列出模块，使用 -t 选项在指定子目录中查找模块。在下一个示例中，用户列出了 sound 目录中的所有模块：

```
# modprobe -l -t sound
/lib/modules/2.4.22-1/kernel/drivers/sound/sb.o
/lib/modules/2.4.22-1/kernel/drivers/sound/sb_lib.o
/lib/modules/2.4.22-1/kernel/drivers/sound/sound.o
/lib/modules/2.4.22-1/kernel/drivers/sound/soundcore.o
```

modprobe 命令的选项放在 /etc/modules.conf 文件中。在此，您可以输入配置选项，如默认目录和别名。别名为模块提供简单名称。例如，以下条目使您能够引用 3c59x.o 以太网卡模块为 eth0（Kmod 自动检测 3Com 以太网卡并加载 3c59x 模块）：

```
alias eth0 3c59x
```

### insmod 命令

insmod 命令执行模块的实际加载。modprobe 和内核模块加载器都使用此命令来加载模块。虽然由于 modprobe 检查依赖项而更受推荐，但您可以使用 insmod 和 rmmod 命令单独加载或卸载特定模块。

insmod 命令接受模块名称作为其参数，rmmod 也是如此。名称可以是简单的基名称，如 sb.o 模块的 sb。您可以使用 -o 选项指定完整的模块文件名。其他有用的选项包括 -p 选项，它允许您首先探测您的系统，以查看模块是否可以成功加载，以及 -n 选项，它执行所有任务但不实际加载模块（空跑）。-v 选项（详细模式）列出发生的所有操作。在极少数需要强制加载模块的情况下，您可以使用 -f 选项。在下一个示例中，insmod 加载 sb.o 模块。

```
# insmod -v sb
```

### rmmod 命令

rmmod 命令执行模块的实际卸载。它是 modprobe 和内核模块加载器用于卸载模块的命令。只要模块没有被使用或其他模块所需，您就可以使用 rmmod 命令移除特定模块。您可以使用 -r 选项移除模块及其所有依赖模块。-a 选项移除所有未使用的模块。使用 -s 选项时，当 rmmod 卸载模块时，它会在持久数据目录中保存任何持久数据（参数），通常是 /var/lib/modules/persist。

### /etc/modules.conf 文件

请注意，/dev 目录中没有以太网设备的设备名称。这是因为设备名称实际上是 modules.conf 文件中定义的以太网网络模块的别名。如果您添加另一张相同类型的以太网卡，您将在 modules.conf 文件中为其放置一个别名。对于第二张以太网卡，您将使用设备名称 eth1 作为别名。这样，第二以太网设备就可以通过名称 eth1 被引用。一个 modules.conf 条目如下所示：

```
alias eth1 ne2k-pci
```
