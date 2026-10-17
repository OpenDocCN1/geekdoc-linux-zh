
## 配置目标

- `config`——使用行行的程序更新当前配置
- `menuconfig`——使用基于菜单的程序更新当前配置
- `xconfig`——使用基于 QT 的前端更新当前配置
- `gconfig`——使用基于 GTK 的前端更新当前配置
- `oldconfig`——使用提供的 `.config` 作为基础更新当前配置
- `silentconfig`——与 `oldconfig` 相同，对所有选项给出随机回答
- `randconfig`——对所有选项给出默认回答的新配置
- `almodconfig`——在可能的情况下选择模块的新配置
- `allyesconfig`——接受所有选项并选 yes 的新配置
- `allnoconfig`——新的最小配置

这些前四个文件配置目标调用了某种形式的配置编辑器，如列表所示。由于空间考虑，我们在本章和本书的其余部分中仅关注基于 GTK 的图形化前端。请注意，你可以使用任何你选择的配置编辑器并获得相同的结果。

你通过在内核顶层目录输入命令 `make gconfig` 来调用配置编辑器¹³。图 4-2 显示了运行 `gconfig` 时向开发者呈现的顶层配置菜单。从这里，你可以访问每个可用的配置参数来生成自定义的内核配置。

![](img/75da989fc023923ea1a768dd5ab686d4_116_0.png)

**图 4-2** 顶层内核配置

> ¹³ 如前所述，你可以使用任何你选择的配置编辑器，例如 `make xconfig` 或 `make menuconfig`。

当你退出配置编辑器时，系统会提示你保存更改。如果你选择保存更改，全局配置文件 `.config` 将被更新（如果不存在则创建）。之前介绍的 `.config` 文件通过顶层 Makefile 驱动内核构建。

大多数内核软件也通过 `.config` 文件间接读取配置。在构建过程中，`.config` 文件被处理为 `include/linux` 目录下的一个头文件 `autoconf.h`。该文件是自动生成的。如果你从未编辑过它，每次更改配置并启动新构建时，编辑都会丢失。许多内核文件使用 `#include` 直接包含此文件。列表 4-5 重现了该头文件中与 USB 支持相关的部分，方式如下：

```
gcc ... -include/linux/autoconf.h
```

这是各种内核模块访问内核配置的方式。

### 列表 4-5 Linux autoconf.h

```
$ cat include/linux/autoconf.h | grep CONFIG_USB
#define CONFIG_USB_ARCH_HAS_EHCI 1
#define CONFIG_USB_HID 1
#define CONFIG_USB_EHCI_BIG_ENDIAN 1
#define CONFIG_USB_EHCI_HAS_OHCI 1
#define CONFIG_USB_BIG_ENDIAN_MMIO 1
#define CONFIG_USB_STORAGE 1
#define CONFIG_USB_SUPPORT 1
#define CONFIG_USB_HCD 1
#define CONFIG_USB_DEVICE 1
#define CONFIG_USB_OHCI 1
#define CONFIG_USB_UHCI 1
#define CONFIG_USB_OHCI_LITTLE_ENDIAN 1
#define CONFIG_USB_ARCH_HAS_HCD 1
#define CONFIG_USB 1
```

如果你还没有这样做，在内核根目录下执行 `make config`，并研究此配置工具以查看开发者可以使用大量的配置选项。只要你不显式保存更改，当你退出配置编辑器时更改将会丢失¹许多配置参数包含帮助文本，可以增加你对各种配置选项的理解。

> > 更好的做法是为你的 `.config` 文件创建一个备份副本。

## 4.3.3 Makefile 目标

如果你在 Linux 根目录下输入 `make help`，你将看到一组从源码树生成的目标。`make` 最常用的用法是不指定目标。这会生成 ELF 文件 `vmlinux` 以及你选择架构的默认二进制镜像（例如 x86 的 `bImage`）。不指定目标还会构建所有设备驱动程序（内核可加载模块）。

许多架构和机器类型需要特定于架构和引导程序的二进制目标。常见的目标之一是 `Image`。在许多架构中，这是可以加载并运行的默认目标镜像。新手常犯的错误之一是指定 `bimage` 为目标。`bImage` 目标特定于 x86 架构。与流行说法不同，bimage 并不是 bzip2 压缩镜像。它是一个 zImage。不需要进入旧 PC 架构的细节，只需知道 bimage 适用于具有标准 PC BIOS 的兼容机器。

### 列表 4-6 Makefile 目标

```
$ make ARCH=arm help
```

#### 清理目标

- `clean`——删除大部分生成文件，但保留配置和足够构建外部模块的内容
- `mrproper`——删除所有生成文件 + 配置 + 各种备份文件
- `distclean`——`mrproper` + 删除编辑器备份和补丁文件

#### 配置目标

- `config`——使用行的程序更新当前配置
- `menuconfig`——使用基于菜单的程序更新当前配置
- `xconfig`——使用基于 QT 的前端更新当前配置
- `gconfig`——使用基于 GTK 的前端更新当前配置
- `oldconfig`——使用提供的 `.config` 作为基础更新当前配置
- `silentoldconfig`——与 `oldconfig` 相同，但静默执行
- `randconfig`——对所有选项给出随机回答的新配置
- `defconfig`——对所有选项给出默认回答的新配置
- `allmodconfig`——在可能的情况下选择模块的新配置
- `allyesconfig`——接受所有选项并选 yes 的新配置
- `allnoconfig`——对所有选项回答 no 的新配置

#### 其他通用目标

- `all`——构建标记为 `[*]` 的所有目标
- `vmlinux`——构建裸内核
- `modules`——构建所有模块
- `modules_install`——将所有模块安装到 `INSTALL_MOD_PATH`（默认为 `/`）
- `firmware_install`——将固件安装到 `INSTALL_FW_PATH`（默认为 `$(INSTALL_MOD_PATH)/lib/firmware`）
- `dir/`——构建目录及子目录下的所有文件
- `dir/file.[ois]`——仅构建指定的目标
- `dir/file.ko`——构建包含链接的模块
- `prepare`——为构建外部模块准备
- `tags`——为文件编辑器生成标签
- `cscope`——生成 cscope 索引
- `kernelrelease`——输出发布版本字符串
- `kernelversion`——在 Makefile 中输出版本字符串

#### 静态分析工具

- `checkstack`——生成栈消耗户列表
- `namespacecheck`——对编译后的内核进行命名空间分析
- `versioncheck`——对 `version.h` 使用进行完整性检查
- `includecheck`——检查重复包含的头文件
- `export_report`——列出所有导出符号的用法
- `headers_check`——对导出的头文件进行完整性检查
- `headerdep`——检测头文件中的包含循环

#### 内核打包

- `rpm-pkg`——构建源码和二进制 RPM 内核包
- `binrpm-pkg`——仅构建二进制内核包
- `deb-pkg`——将内核构建为 deb 包
- `tar-pkg`——将内核构建为未压缩的 tar 包
- `targz-pkg`——将内核构建为 gzip 压缩的 tar 包
- `tarbz2-pkg`——将内核构建为 bzip2 压缩的 tar 包

#### 文档目标文件

不同格式的 Linux 内核内部文档：

- `htmldocs`——HTML
- `pdfdocs`——PDF
- `psdocs`——Postscript
- `xmldocs`——XML DocBook
- `mandocs`——man 手页（帮助手册）
- `installmandocs`——安装由 `mandocs` 生成的 man 手页
- `cleandocs`——清理所有生成的 DocBook 文件

#### 特定架构目标文件 (arm)

- `zImage`——压缩的内核镜像 (`arm/boot/zImage`)
- `Image`——未压缩的内核镜像 (`arm/boot/Image`)
- `xipImage`——XIP 内核镜像，如果已配置 (`arm/boot/xipImage`)
- `uImage`——U-Boot 封装镜像
- `bootImage`——镜像和初始 RAM 磁盘（通过变量 `INITRD=<path>` 提供 initrd）
- `install`——安装未压缩的内核
- `zinstall`——使用（你的）`/bin/installkernel` 或（发行版的）`/sbin/installkernel` 或安装到 `$(INSTALL_PATH)` 并运行 lilo

##### ARM 架构默认配置

```
acs5k_defconfig            - 为 acs5k 构建
acs5k_tiny_defconfig       - 为 acs5k_tiny 构建
afeb9260_defconfig         - 为 afeb9260 构建
am200epdkit_defconfig      - 为 am200epdevkit 构建
ams_delta_defconfig        - 为 ams_delta 构建
assabet_defconfig          - 为 assabet 构建
at91cap9ad_defconfig       - 为 at91cap9adk 构建
at91rm920dk_defconfig      - 为 at91rm9200dk 构建
at91rm920ek_defconfig      - 为 at91rm9200ek 构建
at91sam926ek_defconfig     - 为 at91sam926ek 构建
at91sam926ik_defconfig     - 为 at91sam926ik 构建
at91sam9263ek_defconfig    - 为 at91sam9263ek 构建
at91sam9g20k_defconfig     - 为 at91sam9g20k 构建
at91sam9rlek_defconfig     - 为 at91sam9rlek 构建
ateb920_defconfig          - 为 ateb9200 构建
badge4_defconfig           - 为 badge4 构建
cam60_defconfig            - 为 cam60 构建
carmeva_defconfig          - 为 carmeva 构建
cerfcube_defconfig         - 为 cerfcube 构建
cm_x220_defconfig          - 为 cm_x220 构建
cm_x300_defconfig          - 为 cm_x300 构建
colibri_pxa270_defconfig   - 为 colibri_pxa270 构建
colibri_pxa300_defconfig   - 为 colibri_pxa300 构建
collie_defconfig           - 为 collie 构建
corgi_defconfig            - 为 corgi 构建
csb337_defconfig           - 为 csb337 构建
csb637_defconfig           - 为 csb637 构建
davinci_all_defconfig      - 为 davinci_all 构建
ebsa110_defconfig          - 为 ebsa110 构建
ecbat91_defconfig          - 为 ecbat91 构建
edb7211_defconfig          - 为 edb7211 构建
em_x270_defconfig          - 为 em_x270 构建
ep93xx_defconfig           - 为 ep93xx 构建
eseries_pxa_defconfig      - 为 eseries_pxa 构建
ezx_defconfig              - 为 ezx 构建
footbridge_defconfig       - 为 footbridge 构建
fortunet_defconfig         - 为 fortunet 构建
h3600_defconfig            - 为 h3600 构建
h5000_defconfig            - 为 h5000 构建
h7201_defconfig            - 为 h7201 构建
h7202_defconfig            - 为 h7202 构建
hackkit_defconfig          - 为 hackkit 构建
integrator_defconfig       - 为 integrator 构建
iopl33xx_defconfig         - 为 iopl33xx 构建
iop32x_defconfig           - 为 iop32x 构建
iop33x_defconfig           - 为 iop33x 构建
ixp2000_defconfig          - 为 ixp2000 构建
ixp23xx_defconfig          - 为 ixp23xx 构建
ixp4xx_defconfig           - 为 ixp4xx 构建
jornada720_defconfig       - 为 jornada720 构建
kafa_defconfig             - 为 kafa 构建
kb9202_defconfig           - 为 kb9202 构建
kirkwood_defconfig         - 为 kirkwood 构建
ks8695_defconfig           - 为 ks8695 构建
lart_defconfig             - 为 lart 构建
littleton_defconfig        - 为 littleton 构建
loki_defconfig             - 为 loki 构建
ldp270_defconfig           - 为 ldp270 构建
ldp7a400_defconfig         - 为 ldp7a400 构建
ldp7a404_defconfig         - 为 ldp7a404 构建
lubbock_defconfig          - 为 lubbock 构建
lus1720_defconfig          - 为 lus1720 构建
magician_defconfig         - 为 magician 构建
mainstone_defconfig        - 为 mainstone 构建
msm_defconfig              - 为 msm 构建
mv78xx_defconfig           - 为 mv78xx 构建
mxlads_defconfig           - 为 mxlads 构建
mx1_defconfig              - 为 mx1 构建
mx27_defconfig             - 为 mx27 构建
mx31pdk_defconfig          - 为 mx31pdk 构建
mx3_defconfig              - 为 mx3 构建
n770_defconfig             - 为 n770 构建
neocore926_defconfig       - 为 neocore926 构建
onset_defconfig            - 为 onset 构建
netx_defconfig             - 为 netx 构建
ns99xx_defconfig           - 为 ns99xx 构建
omap_2430sp_defconfig      - 为 omap_2430sp 构建
omap_3430sp_defconfig      - 为 omap_3430sp 构建
omap3_beagle_defconfig     - 为 omap3_beagle 构建
omap3_pandora_defconfig    - 为 omap3_pandora 构建
omap_apollon_2420_defconfig - 为 omap_apollon_2420 构建
omap_generic_1510_defconfig - 为 omap_generic_1510 构建
omap_generic_1610_defconfig - 为 omap_generic_1610 构建
omap_generic_1710_defconfig - 为 omap_generic_1710 构建
omap_generic_2420_defconfig - 为 omap_generic_2420 构建
omap_h2_1610_defconfig     - 为 omap_h2_1610 构建
omap_h4_2420_defconfig     - 为 omap_h4_2420 构建
omap_innovator_1510_defconfig - 为 omap_innovator_1510 构建
omap_innovator_1610_defconfig - 为 omap_innovator_1610 构建
```
