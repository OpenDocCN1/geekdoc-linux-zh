
## 添加 Zip 驱动器

有许多版本的 Zip 驱动器。大多数类型的 Zip 驱动器都支持 Linux，但某些（如 USB 版本）仍在等待 Linux 驱动程序的开发。查看 `Zip Drive Mini-HOWTO` 获取你型号的驱动信息。

Zip 驱动器是可移动硬盘的廉价替代方案，尽管目前的格式将存储容量限制在小于 250MB。如果你需要更大的可移动驱动器，可以考虑 Iomega 或 Syquest 的其他驱动器。SCSI 版本的 Zip 驱动器支持，因为它被视为任何其他 SCSI 设备（检查 `Hardware-HOWTO` 页面以查看你的 SCSI 适配器是否受支持）。并行端口 Zip 驱动器也支持，只要你或者

# 第二部分
## 第8章 添加 Zip 驱动器

重新编译内核或使用可加载软件模块。`Zip-plus` 和 `Zip250` 需要不同的加载模块，而 ATAPI 版本则使用标准的 ATAPI 驱动程序，将其视为一个大型软驱器。

有关 Iomega Zip 驱动器的更多信息，请使用您常用的 浏览器访问以下网站：
`http://www.omega.com`

+ 另另
- 关于重新编译 Linux 内核的详情，请参第 545 页。
- 关于在 Linux 内核中使用模块的详情，请参第 535 页。

![](img/b916e6553833e904f268fdbef0cc11e9_152_0.png)

# 在安装 Zip 驱动器之前

尽管大多数 Linux 发行版都带有支持 Zip 驱动器所需的驱动程序和文件系统工具，但在安装之前，您必须确保以下条件：

- 对于大多数 Zip 驱动器，内核必须编译了 SCSI 支持，或者作为可加载模块可用。
- 并口驱动器要求并行打印机支持不要被编译到 Linux 内核中，而应该作为可加载模块可用。`ppa` 驱动程序需要在打印机的 `1p` 模块之前加载。
- 手头应该有一个 Grant Guenther 的 `Zip Drive Mini-HOWTO` 页面的副本。该文档包含了内核配置和驱动程序自定义的技术细节，并提供了最新驱动器的索引。使用它来查找与您的 Zip 驱动器版本匹配的规格。检查您发行版的文档，以查看 HOWTO 可能安装在系统的哪个位置。要获取最新的 HOWTO 集合，请将您的 Web 浏览器指向 Linux 文档项目：`http://www.linuxdoc.org`。

+ 另另
- 安装硬盘请参阅第 119 页。

# 第二部分 配置您的系统
## 第8章 添加磁带和 Zip 驱动器

### 文件系统：Windows 用户使用 vfat
具有 Windows 分区的 Linux 用户可能希望对 DOS 格式的 Zip 磁盘使用 `vfat` 文件系统类型。通过对复制到 Zip 磁盘的 Linux 或 Windows 文件使用 32 字符文件名，您将受益。

# Zip 磁盘的弹出、密码保护和读写保护

使用 `ziptool` 命令利用 Zip 驱动器的一些独特功能，例如读写保护或密码保护。`ziptool` 的其他功能还包括：

- 弹出未挂载的 Zip 磁盘。
- 报告未挂载 Zip 磁盘的读写保护。
- 切换未挂载 Zip 磁盘的读写保护。
- 启用或禁用未挂载且启写的 Zip 磁盘的密码保护。

获取 `ziptool` 程序的副本，请检查您的发行版或浏览以下网站：

`http://www.novia.net/~segura/ziptool/`

有许多名为 `ziptool` 的不同 Zip 驱动器文件工具。如果您的版本与我在这里讨论的不同，请务必检查该版本的主页或其他文档。使用 `ziptool` 时，请指定一个选项，后跟设备卷名（`/dev/sda`），而不是设备分区名（`/dev/sda4`）。

### 弹出 Zip 磁盘

1. 使用 `umount` 命令后跟 Zip 磁盘挂载点的路径来卸载 Zip 磁盘：
   - `umount /mnt/zip`
2. 要弹出磁盘，使用 `ziptool` 的 `-e` 选项：
   - `ziptool -e /dev/sda`

使用此 `ziptool` 选项物理弹出 Zip 磁盘。

### 为 Zip 磁盘设置密码

1. 为 Zip 磁盘设置密码需要磁盘已插入 Zip 驱动器但未挂载。如果驱动器已挂载，请先用 `mount` 命令卸载磁盘。
2. 要检查磁盘状态并获取密码或读写状态的报告，请使用 `ziptool` 的 `-s`（status）选项：

```
# ziptool -s /dev/sda

ziptool: medium is not protected
```

3. 要为 Zip 磁盘设置密码并启用只读保护，请使用 `-rp` 选项，用法如下所示：

```
# ziptool -rp /dev/sda

Password: mypasswd

ziptool: medium is password write-protected.
```

要删除密码保护并允许向磁盘写入，请使用 `-rw`（读写）选项：

```
# ziptool -rw /dev/sda

Password: mypasswd

ziptool: medium is not protected.
```

> 记住您的 Zip 磁盘密码
如果您在用 `ziptool` 为 Zip 磁盘保护时忘记了密码，则必须在重新格式化之前才能再次用于存储（否则，它将变成咖啡桌上漂亮且昂贵的杯垫）。

### Zip 磁盘读写保护

1. 要将 Zip 磁盘设为写保护，请使用 `-ro`（只读）选项：
```
# ziptool -ro /dev/sda

ziptool: medium is write-protected.
```
2. 要切换读写保护，请使用 `-rw` 选项使用 `ziptool` 命令：
```
# ziptool -rw /dev/sda

ziptool: medium is not protected.
```

# 第章

## 启用 PC Card 设备

- 启用 PC Card 服务
- 使用 `cardmgr`
- 使用 `cardctl` 命令

### 启用 PCMCIA 服务
支持可加载模块的新内核内核为带有设备的笔记本电脑用户简化了生活，这些设备在插入时会自动加载和卸载。要使用 PCMCIA，您应该安装 `pcmmia` 软件包。请检查发行版文档。

+ 另另
- 关于 Linux 内核和模块，请参阅 535。
- 关于安装软件包，请参阅 483。

此软件包安装以下内容：
- `pmia` 配置文件和数据库，通常位于 `/etc/pcmmia`
- 包含可加载模块的目录，通常位于 `/lib/modules/kernel-version`
- 特定的启动脚本
- 各种文档文件

`cardmgr` 守护支持的一些卡包括：
- 以太网卡
- 令牌环适配器
- 无线网络适配器
- 调制解调器
- 内存卡
- SCSI 接口适配器
- ATA/IDE 光驱适配器
- 多功能卡
- ATA/IDE 驱动器
- 杂卡

### 我的 PC 卡 能用 Linux 吗？
阅读 `mia` 文档中的 `SUPPORTED.CARDS` 文件以确定 Linux 是否支持您的卡。如果您的卡在启动时未被识别，您仍然可以尝试配置它。某些旧笔记本电脑可能不支持某些“cardbus”PC 卡。请检查您的笔记本文档。

关于配置未识别卡的详情可以在 `PCMCIA-HOWTO` 页中找到（可能位于 `/usr/doc/HOWTO` 目录）。要获取最新版本的 PCMCIA-HOWTO、Linux PCMCIA 程序员指南或最新支持卡的列表，请浏览 David Hinds 的 Web 页面：

```
http://pccmia.sourceforge.org
```

### 确定您的 PCMCIA 控制器
为了设置 PC 卡服务，首先确定可用 PC 卡插槽的数量以及计算机安装的 PC 卡 控制器类型。使用 `probe` 命令报告插槽数量：

```
# probe

PCI bridge probe: Cirrus PD6729 found, 2 sockets.
```
使用 `probe` 命令的 `-m` 选项查找计算机使用的芯片类型：

```
# probe -m

i2365
```

### 启用 PC 卡服务
要为 Linux 启用 PC 卡服务，请确保以 root 用户身份登录。您还需要找到您的发行版存储 PCMCIA 配置的地方。在某些情况下，它可能在启动脚本中；或者是一个独立的文件。

## 第二部分 配置你的系统
## 第 9 章 启用 PC 卡设备

2. 使用你喜欢的文本编辑器打开 PCcmia 配置文件。输入单词 `PCCMIA=yes`（如果尚未存在）以及你电脑中使用的 PC 卡控制器类型（`PCIC`）（可以是 182365 或 tcie；请参见上方的 `probe -m` 输出）：
```
PCCMIA=yes

PCIC=182365

PCIC_OPTS=

CORE_OPTS=
```
