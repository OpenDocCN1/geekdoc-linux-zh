
要安装新卡，你的内核必须首先配置为支持它。大多数卡的支持以可动态加载到内核的模块形式提供。安装卡的支持通常只需加载包含其驱动程序的模块即可。例如，Sound Blaster 声卡的驱动程序位于模块`sb.o`中。加载此模块会使你的声卡可供 Linux 使用。大多数发行版会自动检测系统上安装的卡并加载所需的模块。如果你更换声卡，新卡会被 Kudzu 自动检测，调用`redhat-config-soundcard`来配置它。对于网卡，Kudzu 会调用`redhat-config-network`来执行配置。你也可以手动加载所需的模块，移除旧的冲突模块。本章后面的“Modules”部分描述了此过程。

系统上的以太网卡。用于引用该特定卡所用模块的别名，例如，3Com Etherlink XL 卡别名为`3c59x`网络模块，如果它是第一块以太网卡，其别名将为`eth0`。模块本身保存在内核的模块目录`/lib/modules`中，如上一节所述。

## 音频设备

在 Red Hat 上，你可以使用`redhat-config-soundcard`实用程序在 Linux 上安装大多数声卡。不同音频设备的列表在表 32-3 中提供。某些声卡可能需要更专业的支持。对于声卡，你可以通过列出`/dev/sndstat`文件的内容来了解当前的音频配置。你可以通过简单地将音频文件重定向到它来测试你的卡，如下所示：

```
cat sample.au > /dev/audio.
```

对于 2.4 内核，大多数 Linux 音频驱动程序作为 Open Sound System（OSS）的一部分开发，并作为 OSS/Free 免费分发。这些作为 Linux 发行版的一部分安装。OSS 设备驱动程序旨在为所有 Unix 平台，包括 Linux，提供统一的 API。它们支持 Sound Blaster 和 Windows Sound System 兼容的声卡（ISA 和 PCI）。OSS 也可以以象征性费用获得，并提供设备设置的配置界面。

高级 Linux 音频架构（ALSA）取代了 2.6 Linux 内核中的 OSS，旨在成为 OSS 的更好替代，同时保持与其兼容。ALSA 提供模块化音频驱动程序、API 和配置管理器。ALSA 是一个 GNU 项目，完全免费；其网站`www.alsa-project.org`包含广泛的文档、应用程序和驱动程序。目前可用的有 ALSA 音频驱动程序、ALSA 内核 API、用于支持应用程序开发的 ALSA 库，以及为驱动程序提供配置界面的 ALSA 管理器。ALSA 源自 Linux Ultra Sound Project。

Linux 音乐数字接口（MIDI）和 Sound Pages，目前位于`www.xdt.com/ar/linux-snd`，提供了指向 Linux 各种声卡音频驱动程序的 Web 和 FTP 站点的链接。它们还包括指向 Linux MIDI 和音频软件站点的链接。

### 表 32-3 声音设备

| Device | Description |
|---|---|
| `/dev/sndstat` | Sound driver status |
| `/dev/audio` | Audio output device |
| `/dev/dsp` | Sound sampling device |
| `/dev/mixer` | Control mixer on sound card |
| `/dev/music` | High-level sequencer |
| `/dev/sequencer` | Low-level sequencer |
| `/dev/midi` | Direct MIDI port |

## 视频、电视和 DVD 设备

用于电视、视频和 DVD 设备的设备名称列于表 32-4。已为 DVD 和电视解码器开发了驱动程序。mg4linux (`marvel.sourceforge.net`) 正在为 Matrox 多媒体卡（如 Marvel G200）开发视频支持。通用 ATI 电视和叠加软件（GATOS）(`gatos.sourceforge.net`) 已为 ATI 视频卡当前未支持的功能开发了驱动程序，特别是电视功能。BTTV 驱动项目已为 Booktree 视频芯片开发了驱动程序。Creative Labs 为 Creative 系列 DVD DXR2 解码器赞助了 Linux 驱动程序 (`opensource.creative.com`)。

### 表 32-4 视频设备

| 设备名称 | 设备类型 |
|---|---|
| `/dev/video` | 视频捕获接口 |
| `/dev/vfx` | 视频特效接口 |
| `/dev/vdec` | 视频编解码器接口 |
| `/dev/vout` | 视频输出接口 |
| `/dev/radio` | AM/FM 收音机设备 |
| `/dev/vtx` | 图文电视接口芯片 |
| `/dev/vbi` | 数据服务接口 |

## 模块

Linux 内核采用模块来支持不同的操作系统功能，包括对各种设备（如声卡和网卡）的支持。在许多情况下，您可以选择将对设备的支持实现为模块，或直接编译为内置内核功能，这需要您重建内核（参见第 33 章）。更安全、更稳健的解决方案是使用模块。模块是 Linux 内核的组件，可根据需要加载。要为新设备添加支持，您现在只需指示内核加载该设备的模块。在某些情况下，您可能只需要重新编译该模块即可为您的设备提供支持。使用模块的额外优点是减少了内核程序的大小，同时使系统更稳定。内核只能在需要时将模块加载到内存中。如果模块失败，只有该模块停止运行，而不会影响整个系统。例如，用于调制解调器的 PPP 网络接口的模块仅在您连接到 ISP 时才需要使用。

## 内核模块工具

系统所需的模块通常在安装期间确定，基于您提供的配置信息类型以及 Kudzu 执行的自动检测。例如，如果您的系统使用在安装期间指定类型的以太网卡，系统将加载该卡的模块。但是，您可以手动控制要为系统加载哪些模块。实际上，这使您可以按您想要的方式自定义内核。您可以使用多个命令、配置工具和守护进程来管理内核模块。2.4 Linux 内核包含内核模块加载器（Kmod），它具有在需要时自动加载模块的能力。内核中也必须启用内核模块加载支持，尽管这通常被认为是标准配置的一部分，并且包含在 Red Hat 发行版中。此外，还有多个工具可让您在必须时手动加载和卸载模块。内核模块加载器使用某些内核命令来执行加载或卸载模块的任务。`modprobe`命令是一个通用命令，用于调用`insmod`加载模块和`rmmod`卸载它们。这些命令列于表 32-5。特定模块的选项、通用配置，甚至特定模块加载都可以在`/etc/modules.conf`文件中指定。您可以使用此文件自动加载和配置模块。您也可以在启动提示符或`grub.conf`中指定要加载的模块（参见第 27 章）。

### 表 32-5 内核模块命令

| 命令 | 描述 |
|---|---|
| `lsmod` | 列出当前已加载的模块。 |
| `insmod` | 将模块加载到内核中。不检查依赖关系。 |
| `rmmod` | 卸载当前已加载的模块。不检查依赖关系。 |
| `modinfo` | 显示有关模块的信息：`-a`（作者），`-d`（描述），`-p`（模块参数），`-f`（模块文件名），`-v`（模块版本）。 |
| `depmod` | 创建依赖文件，列出指定模块可能依赖的所有其他模块。 |
| `modprobe` | 加载模块及其可能需要的任何依赖模块。使用`depmod`生成的依赖列表文件：`-r`（卸载模块），`-l`（列出模块） |

## 模块文件和目录

模块的文件名扩展名为`.o`。内核模块位于`/lib/modules/version`目录中，其中`version`是当前内核的版本号。2.4.22-1 内核的目录是`/lib/modules/2.4.22-1`。随着您在系统上安装新内核，将为它们生成新的模块目录。访问当前内核目录的一种方法是使用`uname -r`命令生成内核版本号。该命令需要反引号。

```
cd /lib/modules/`uname -r`
```

在此目录中，内核的模块位于`/kernel`目录中。在`/kernel`目录中包含多个子目录，包括保存诸如声卡驱动程序或视频驱动程序等模块的`/drivers`目录。这些子目录用于对模块进行分类，使其更易于定位。例如，`kernel/drivers/net`目录保存以太网卡的模块，而`kernel/drivers/sound`目录包含声卡模块。

## 使用 `/etc/modules.conf` 管理模块

如前所述，有多个命令可用于管理模块。`lsmod`命令列出当前已加载到内核中的模块，而`modinfo`则提供特定模块的信息。虽然你可以使用`insmod`和`rmmod`命令直接加载或卸载模块，但应仅对这些任务使用`modprobe`。 （请参阅表 33-5 中的内核模块命令。）然而，通常给定模块需要其他模块被加载。例如，Sound Blaster 声卡的模块`sb.o`需要`sound.o`模块也被加载。

## depmod 命令
