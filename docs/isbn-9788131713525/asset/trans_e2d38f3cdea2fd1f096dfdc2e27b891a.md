

-   oldconfig—使用提供的 `.config` 作为基础来更新当前配置
-   randconfig—生成一个新配置，对所有选项随机给出答案
-   defconfig—生成一个新配置，对所有选项采用默认答案
-   allmodconfig—生成一个新配置，尽可能地将所有选项设置为模块
-   allyesconfig—生成一个新配置，接受所有选项（均为 yes）
-   allnoconfig—生成一个最小化的新配置

上述前四个 makefile 配置目标都会调用某种形式的配置编辑器，正如列表中所描述的那样。由于篇幅限制，本章及其他章节的讨论将仅聚焦于基于 GTK 的图形前端。请注意，你可以使用任意你喜欢的配置编辑器，并得到相同的结果。

通过在内核顶层目录下输入命令 `make gconfig` 来启动配置编辑器。图 4-2 展示了当运行 `gconfig` 时向开发人员呈现的顶层配置菜单。从这里开始，可以访问每一个可用的配置参数，以生成自定义的内核配置。

![](img/7a1144833e62564667e7dd9eb4c9f03d_114_0.png)

### 图 4-2
顶层内核配置

如前所述，你可以使用任意你喜欢的配置编辑器，例如 `make xconfig` 或 `make menuconfig`。

当退出配置编辑器时，系统会提示你是否保存更改。如果你选择保存更改，全局配置文件 `.config` 将被更新（如果该文件尚不存在，则会被创建）。这个 `.config` 文件（前文已介绍）通过顶层 makefile 驱动内核构建。你会注意到，在这个 makefile 中，`.config` 文件是通过 `#include` 语句直接读取的。

大多数内核软件模块也通过 `.config` 文件间接读取配置，方法如下。在构建过程中，`.config` 文件会被处理成一个位于 `../include/linux` 目录下的 C 头文件，名为 `autoconf.h`。这是一个自动生成的文件，绝不应直接编辑，因为每次运行配置编辑器时所做的编辑都会丢失。许多内核源文件使用 `#include` 预处理器指令直接包含此文件。列表 4-6 复现了该头文件中与上文 USB 示例相对应的部分。请注意，对于列表 4-5 中 `.config` 文件片段中的每一项，都会在 `autoconf.h` 中创建一个对应的条目。这就是内核源码树中的源文件引用内核配置的方式。

### 列表 4-6

```c
/* Linux autoconf.h */
/*
 * USB support
 */
#define CONFIG_USB_MODULE 1
#undef CONFIG_USB_DEBUG

/*
 * Miscellaneous USB options
 */
#define CONFIG_USB_DEVICEFS 1
#undef CONFIG_USB_BANDWIDTH
#undef CONFIG_USB_DYNAMIC_MINORS

/*
 * USB Host Controller Drivers
 */
#define CONFIG_USB_EHCI_HCD_MODULE 1
#undef CONFIG_USB_EHCI_SPLIT_ISO
#undef CONFIG_USB_EHCI_ROOT_HUB_TT
#define CONFIG_USB_OHCI_HCD_MODULE 1
#define CONFIG_USB_UHCI_HCD_MODULE 1
```

如果你还没有这样做过，请在你的内核源码顶层目录中执行 `make gconfig`，并在这个配置工具中四处看看，以了解 Linux 开发人员可用的众多子章节和配置选项。只要你不显式保存更改，这些更改在退出配置编辑器时就会丢失。许多配置参数包含有用的说明文本，这有助于你理解不同的配置选项。

### 4.3.3 Makefile 目标

如果你在顶层 Linux 源码目录下输入 `make help`，你会看到一个可以从源码树生成的目标列表。`make` 最常见的用法是不指定任何目标。这将生成内核 ELF 文件 `vmlinux` 以及你所选架构的默认二进制映像（例如，x86 的 `bzImage`）。不指定目标运行 `make` 还会构建配置中指定的所有设备驱动程序模块（内核可加载模块）。

许多架构和机器类型需要特定的针对架构和所用引导加载程序的二进制目标。其中一个更常见的架构特定目标是 `zImage`。在许多架构中，这是可以在目标嵌入式系统上加载和运行的默认目标映像。新手常犯的一个错误是指定 `bzImage` 作为 `make` 目标。`bzImage` 目标特定于 x86/PC 架构。与流行误解相反，`bzImage` 并不是一个经 bzip2 压缩的映像。它是一个大的 `zImage`。无需深入探讨传统 PC 架构的细节，只需知道 `bzImage` 仅适用于具有行业标准 PC 风格 BIOS 的 PC 兼容机器即可。

列表 4-7 包含了来自较新 Linux 内核的 `make help` 输出。你可以从列表中看到，顶层 Linux 内核 Makefile 中提供了许多目标。每个目标都附带其用途的简短描述。重要的是要认识到，即使是 `help` make 目标（如 `make help`）也是架构特定的。根据你在 `make` 调用时传入的架构不同，你会得到不同的架构特定目标列表。列表 4-7 说明了指定 ARM 架构的调用，你可以从 `make` 命令行中看到这一点。

### 列表 4-7

# Makefile 目标

```bash
$ make ARCH=arm help
Cleaning targets:
 clean - remove most generated files but keep the config
 mrproper - remove all generated files + config + various backup files

Configuration targets:
 config - Update current config utilising a line-oriented program
 menuconfig - Update current config utilising a menu based program
 xconfig - Update current config utilising a QT based front-end
 gconfig - Update current config utilising a GTK based front-end
 oldconfig - Update current config utilising a provided .config as base
 randconfig - New config with random answer to all options
 defconfig - New config with default answer to all options
 allmodconfig - New config selecting all modules when possible
 allyesconfig - New config where all options are accepted with yes
 allnoconfig - New minimal config

Other generic targets:
 all - Build all targets marked with [*]
 * vmlinux - Build the bare kernel
 modules - Build all modules
 modules_install - Install all modules
 dir/ - Build all files in dir and below
 dir/file.[o]s - Build specified target only
 -dir/file.ko - Build module including final link
 rpm - Build a kernel as an RPM package
 tags/TAGS - Generate tags file for editors
 cscope - Generate cscope index
 kernelrelease - Output the release version string

Static analysers
 buildcheck - List dangling references to vmlinux discarded sections and init sections from non-init sections
 checkstack - Generate a list of stack hops
 namespacecheck - Namespace analysis on compiled kernel

Kernel packaging:
 rpm-pkg - Build the kernel as an RPM package
 binrpm-pkg - Build an rpm package containing the compiled kernel and modules

- deb-pkg - Build the kernel as a deb package
- tar-pkg - Build the kernel as an uncompressed tarball
- targz-pkg - Build the kernel as a gzip compressed tarball
- tarbz2-pkg - Build the kernel as a bzip2 compressed tarball

Documentation targets:

- man - Linux kernel internal documentation in different formats:
  - xmldocs (XML DoCbook), pedocs (Postscript/PDF), pdfdocs (PDF)
  - htmldocs (HTM), man docs (pages, use installmandocs to install)

Architecture specific targets (arm):

- zImage - Compressed kernel image (arch/arm/boot/zImage)
- Image - Uncompressed kernel image (arch/arm/boot/Image)
- xipImage - XIP kernel image, if configured (arch/arm/boot/xipImage)
- bootpImage - Combined zImage and initial RAM disk

- install - Install initrd image via make variable INITRD=<path>
- zinstall - Install uncompressed kernel
- install - Install compressed kernel
  - Install using (your) ~/bin/installkernel or
  - (distribution) /sbin/installkernel or
  - Install to $(INSTALL_PATH) and run lilo

- assabet_defconfig - Build for assabet
- badge4_defconfig - Build for badge4
- bast_defconfig - Build for bast
- cerfcube_defconfig - Build for cerfcube
- clips7500_defconfig - Build for clips7500
- colli_defconfig - Build for colli
- corgi_defconfig - Build for corgi
- ebsa110_defconfig - Build for ebsa110
- edb7211_defconfig - Build for edb7211
- emx2611_defconfig - Build for emx2611
- ep80219_defconfig - Build for ep80219
- epax10d_h_defconfig - Build for epax10dH
- foodbridge_defconfig - Build for foodbridge
- fortunet_defconfig - Build for fortunet
- h3600_defconfig - Build for h3600
- h7201_defconfig - Build for h7201
- h7202_defconfig - Build for h7202
- hackkit_defconfig - Build for hackkit
- integrator_defconfig - Build for integrator
- igi1244_defconfig - Build for igi1244
- iq80321_defconfig - Build for iq80321
- iq80331_defconfig - Build for iq80331
- iq80332_defconfig - Build for iq80332
- ixdp2400_defconfig - Build for ixdp2400
- ixdp2401_defconfig - Build for ixdp2401
- ixdp2800_defconfig - Build for ixdp2800
- ixdp2801_defconfig - Build for ixdp2801
- ixp4xx_defconfig - Build for ixp4xx
- Jornada720_defconfig - Build for jornada720
- lart_defconfig - Build for lart
- lpd7a400_defconfig - Build for lpd7a400
- lpd7a404_defconfig - Build for lpd7a404
- lubbock_defconfig - Build for lubbock
```

