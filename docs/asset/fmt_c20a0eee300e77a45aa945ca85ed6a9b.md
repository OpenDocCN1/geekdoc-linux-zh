
# 移除补丁

`patchrm` 命令用于通过指定补丁编号作为命令行参数来移除或回退补丁。`patchadd` 命令支持的系统配置也受 `patchrm` 命令的支持。你还可以像之前描述的那样使用 `-C`、`-R` 和 `-S` 命令行参数。例如，要从名为 client5 的无盘客户端的可启动根镜像中移除补丁 110906-01，你可以使用以下 `patchrm` 命令：

```
patchrm -R /export/root/client5 110906-01
```

由于在安装过程中可以使用 `patchadd` 命令的 `-B` 命令行参数更改备份目录，因此 `patchrm` 命令也支持 `-B` 参数。

此外，你还可以使用 `-f` 命令行参数强制 `patchrm` 命令移除已被其他补丁覆盖的补丁。

只要满足以下条件，你就可以重新安装已安装的补丁，并将系统恢复到安装之前的状态：

## 练习题

### 第 1 题

以下哪些可以安装多个补丁？[多选]

- a. `patchadd -M /var/spool/patch 104567-03 106583-10 103276-04`
- b. 使用 `patchadd` 分别安装每个补丁。
- c. `patchadd -M /var/spool/patch patchlist`

答案 a、b 和 c 正确。所有答案都可以用于安装多个补丁。答案 a 中的命令安装了位于 `/var/spool/patch` 目录下的三个补丁。答案 c 中的命令使用了命名的补丁列表（patchlist），该列表包含要安装的补丁列表。当然，可以使用 `patchadd` 命令一次安装几个补丁（答案 b）。

### 第 2 题

以下哪些可以安装软件包？[多选]

- a. `admintool`
- b. `pkgtool`
- c. `pkgadd`
- d. `pkgrm`
- e. `pkginfo`

答案 a 和 c 正确。你可以使用 `admintool` 和 `pkgadd` 安装软件包。`pkgtool` 不存在。因此，答案 b 是错误的。`pkgrm` 用于移除软件包，而 `pkginfo` 用于显示有关软件包的信息。因此，答案 d 和 e 是错误的。

### 第 3 题

安装 Solaris 8 最常用的两种方法是哪些？[多选]

- a. 磁带
- b. CD-ROM
- c. 网络
- d. 软磁盘
- e. Web

答案 b 和 c 正确。Solaris 8 最常用的安装方式是通过 CD-ROM 或通过网络。磁带和软磁盘是有效的启动设备，但未用于安装。因此，答案 a 和 d 是错误的。答案 e Web 是不可行的。

### 第 4 题

以下哪项是软件包的默认生成池目录（spool directory）？

- a. `/var/spool`
- b. `/var/sadm/pkg`
- c. `/tmp`
- d. `/var/spool/pkg`

答案 d 正确。`/var/spool/pkg` 是软件包的默认生成池目录。系统生成目录是 `/var/spool`。因此，答案 a 是错误的。包含已安装软件包信息的目录是 `/var/sadm/pkg`。因此，答案 b 是错误的。临时目录是 `/tmp`。因此，答案 c 是错误的。

### 第 5 题

Solaris 8 无法安装在以下哪个上？

- a. Macintosh 系统
- b. Sun SPARC
- c. Intel Pentium
- d. AMD 或 Cyrix (Intel 兼容)

答案 a 正确。Solaris 8 无法安装在 Macintosh 系统上。Solaris 8 可以安装在 Sun SPARC、Intel Pentium 或 Intel 兼容设备（AMD 和 Cyrix）上。因此，答案 b、c 和 d 是错误的。

### 第 6 题

哪些命令会显示来自 SUNWast pkginfo 文件的指定信息？[多选]

- a. `pkginfo SUNWast`
- b. `pkginfo -l SUNWast`
- c. `display pkginfo SUNWast window`
- d. 在 Admintool Software 窗口中突出显示 SUNWast 并点击 Show Details（详情）。

答案 a、b 和 d 正确。你可以使用 `pkginfo SUNWast` 或 `pkginfo -l SUNWast` 命令显示来自 SUNWast pkginfo 文件的指定信息，或者在 Admintool Software 窗口中突出显示 SUNWast 并点击 Show Details。虽然答案 a 中的命令仅提供软件包类型和软件类型，但 pkginfo 文件是获取此类信息的唯一地方。答案 c 中的命令不存在。

### 第 7 题

以下哪些命令可以用于移除补丁？

- a. `rmpatch`
- b. `patchrm`
- c. `pkgrm -p`
- d. `patchadd -d`

答案 b 正确。你可以使用 `patchrm` 命令移除补丁。答案 a (`rmpatch`) 不是有效命令。`pkgrm` 命令用于移除软件包，且不存在 `-p` 命令行参数。因此，答案 c 是错误的。`patchadd -d` 命令用于在文件更新或替换之前不保存即添加补丁。因此，答案 d 是错误的。

### 第 8 题

以下哪些命令可以列出所有已安装补丁？[多选]

- a. `showrev -p`
- b. `patchinfo`
- c. `patchlist all`
- d. `patchadd`

答案 a 和 d 正确。你可以使用 `showrev -p` 和 `patchadd` 命令列出已安装补丁。答案 b 和 c 命令不存在。

### 第 9 题

在升级过程中，以下哪些可以作为备份？[多选]

- a. 未用磁盘
- b. 磁带
- c. 软磁盘
- d. CD-ROM

答案 a、b、c 和 d 正确。在升级期间，可以使用未使用磁盘、磁带或软磁盘作为备份，前提是空间足够。CD-ROM 如其名称所示只读。只读媒体不能用于备份。

### 第 10 题

在自定义安装期间可以选择以下哪些项？

- a. 文件系统
- b. 软件本地化 (localizations)
- c. 额外产品
- d. 系统区域 (locale)
- e. 软件组

答案 a、b、d 和 e 正确。软件本地化可以选择区域（如北美），系统区域进一步定义了语言（对于北美，你可以选择多种变体）。软件组和额外产品也可以选择。这些项仅在选择自定义安装时可用。

## 需要了解

- Solaris 8 Essential Reference (New Riders, Indianapolis, 2001), ISBN 0-7357-1007-4.
- Sun Microsystems, Solaris 8 Intel Platform Hardware Compatibility List. 打印版编号为 806-1054-11，可在 docs.sun.com 在线查看。
- Sun Microsystems, Solaris 8 Intel Platform Installation Guide. 打印版编号为 806-0956-10，可在 docs.sun.com 在线查看。
- Sun Microsystems, Solaris 8 SPARC Platform Installation Guide. 打印版编号为 806-0955-10，可在 docs.sun.com 在线查看。

# 第 4 章：系统的启动与关机

你需要理解的术语：

- OpenBoot
- 非易性 RAM (NVRAM)
- 设备别名 (Device aliases)
- 启动过程
- 内核模块
- init 程序
- 系统运行级别 (run levels)
- rc 脚本

## 你需要掌握的技术：

- 创建和删除设备别名
- 排除启动故障
- 修改系统运行级别
- 使用 rc 脚本添加系统服务

本章介绍了与系统启动和关机相关的主题。第一节介绍了 Sun SPARC 平台上系统固件的方面，包括 Boot PROM 目标。第二节总结了 SPARC 和 Intel x86 平台的启动过程。本节涵盖了启动过程测试目标。第三节描述了系统运行级别、不同运行级别下提供的服务以及如何在不同运行级别之间切换。还包含了如何在选定的运行级别下添加自定义服务的描述。本节包含初始化和关机测试目标。

## Boot PROM 固件 (OpenBoot)

系统的启动可编程只读存储器 (PROM) 用于存储在系统硬件完成上电自检 (POST) 后立即执行的固件。该固件被称为 OpenBoot，它是 Sun 系统的标准固件。OpenBoot 固件仅适用于 SPARC 平台，但在 Intel x86 平台上提供有限的功能。

OpenBoot 用于启动操作系统、运行诊断、修改存储在非易性 RAM (NVRAM) 中的启动相关参数并提供 Forth 解释器。

目前有两个版本的 OpenBoot：2.x 版本和 3.x 版本。OpenBoot 2.x 随着 SPARCstation 2 和 SPARCstation IPX 系统的引入。OpenBoot 3.x 是 OpenBoot 2.x 的增强版本；它基于电气电子工程师学会 (IEEE) 标准1275-1994《启动固件标准》。OpenBoot 3.x 用于 Sun 系列和新的 SPARC 平台。

OpenBoot 为系统控制台提供命令行界面。该命令行界面有两种模式：

- 受限监控器 (Restricted Monitor)——允许管理员启动操作系统、继续挂起的操作或启动 Forth 监控器。受限监控器的提示符为符号 `OK`。
- Forth 监控器 (Forth Monitor)——允许管理员启动操作系统、运行诊断并修改系统配置参数。Forth 监控器的提示符为单词 `ok`，通常称为 OpenBoot 提示符。

系统配置参数存储在系统的 NVRAM 中。这些参数决定了系统的初始配置和相关的通信特性，并在系统断电时保留其键值。

你可以使用 OpenBoot `printenv` 命令查看这些参数的值。要修改它们，请使用 OpenBoot `setenv` 命令。

## 重要 OpenBoot 命令

一些最重要的 OpenBoot 命令用于显示系统配置信息、执行硬件测试和控制系统启动。所有这些命令都在 Forth 监控器或 OpenBoot `ok` 提示符下输入。

表 4.1 列出了显示系统配置数据的 OpenBoot 命令，表 4.2 列出了用于执行基础硬件测试的 OpenBoot 命令。表 4.3 列出了你可以用于选择不同设备的 OpenBoot `boot` 命令的变体。

### 表 4.1：显示系统配置数据的 OpenBoot 命令

| 命令 | 描述 |
|---|---|
| `banner` | 显示启动 banner |
| `dealias` | 列出所有别名 |
| `.enet-addr` | 显示以太地址 |
| `.idprom` | 显示格式化的 ID PROM 内容 |
| `module-info` | 显示 CPU 速度 (仅限2.x) |
| `printenv` | 列出所有 NVRAM 参数和默认值 |
| `show-devs` | 列出所有已安装设备 |
| `.speed` | 显示 CPU 和总线速度 (仅限3.x) |
| `.traps` | 列出 SPARC trap 的类型 |
| `.version` | 显示 boot PROM 的版本和数据 |

### 表 4.2：执行硬件测试的 OpenBoot 命令

| 命令 | 描述 |
| --- | --- |
| `pcia-probe-list` | 测试外部件连接 (PCI) 总线 |
| `probe-scsi` | 测试内置的小型计算机接口 (SCSI) 总线连接的设备 |
| `probe-scsi-all` | 测试所有 SCSI 总线 |
| `test-all` | 测试一组已安装设备 |
| `test floppy` | 测试磁盘驱动器 |
| `test /memory` | 测试系统内存 |
| `test net` | 测试板载以太网接口 |
| `watch-clock` | 监控系统时钟 |
| `watch-net` | 监控网络连接 |

### 表 4.3：选择不同启动设备的 OpenBoot 命令

| 命令 | 描述 |
| --- | --- |
| `boot cdrom` | 从本地 CD-ROM 启动 |
| `boot disk` | 从默认硬盘启动 |
| `boot floppy` | 从磁盘驱动器启动 |
| `boot net` | 从网络启动 |
| `boot tape` | 从 SCSI 磁带机启动 |

`boot` 命令支持一些可能认为非常有用的选项。`-a` 选项请求交互式启动，以便 OpenBoot 提示输入信息。此外，`-s` 选项导致 OpenBoot 进入单用户模式而不是默认运行级别。当你从硬盘启动时，默认设备由 `boot-device` NVRAM 参数指定。在 OpenBoot 提示符下，使用以下命令显示默认设备：

```
ok printenv boot-device
boot-device = disk
ok
```

根据需要更改默认设备。例如，要将默认设备更改为设备 disk2，使用以下命令。然后使用 `reset` 保存值并重启：

```
ok setenv boot-device disk2
```

## 设备别名 (Device Aliases)

OpenBoot 使用完整的设备路径来识别硬件，该路径代表设备类型及其在系统中的位置。设备路径由系统总线、地址和可能的驱动名称组成。以下是 SCSI 分区的完整设备名称示例：

```
/sbus1,0/SUN@8000/sd@3
```

更多关于设备名称的细节请参见第8章。由于设备名称通常很长且输入不便，OpenBoot 允许为完整设备分配别名；这种别名短且容易记忆。

## 创建设备别名

你有两种方法创建别名。第一种方法使用 `devalias` 命令。别名会在系统重启时丢失。第二种方法使用 `nvalias` 命令。别名存储在非易性内存中，直到你使用命令删除它们。两个命令都使用相同的语法。例如，在 OpenBoot 提示符下输入以下命令，将别名 disk2 指向设备 `/sbus/esp/sd@2` (SCSI 磁盘)：

```
ok devalias disk2 /sbus/esp/sd@2
ok nvalias disk2 /sbus/esp/sd@2
```

在 OpenBoot 环境中任何需要设备名称的地方，都可以用别名代替。非易性别名存储在 NVRAM 的一部分内存中。这部分内存被视为 `nvramrc` 参数。`nvramrc` 参数的内容是一个脚本。除了存储用户定义的命令外，该参数还用于设备驱动、分区代码或存储特定设备信息。如果 `use-nvramrc?` 参数设置为 `true`，则在系统启动期间执行脚本。使用 `nvalias` 命令定义的任何别名将被设置，然后在脚本后续部分使用或作为多个 OpenBoot 参数的值。

## 显示设备别名

你也可以使用 `devalias` 命令显示设备别名。如果你输入命令时不带命令行参数，将列出定义的设备别名。如果你将别名作为命令行参数，`devalias` 命令将仅显示该设备别名。以下示例显示了在 SPARC 2020 OpenBoot 提示符下使用 `devalias` 命令：

```
ok devalias
screen /iommu@f,e0000000/sbuf@f,e0010000/cgsix@2,0
ttyb /iommu@f,e0000000/sbuf@f,e0010000/zs@0,100000:b
ttya /iommu@f,e0000000/sbuf@f,e0010000/zs@0,100000:a
keyboard /iommu@f,e0000000/sbuf@f,e0010000/zs@0,0
floppy /iommu@f,e0000000/sbuf@f,e0010000/SUNW,fdtwo
scsi /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000
net-au /iommu@f,e0000000/sbuf@f,e0010000/le@f,c00000:au
net-tpe /iommu@f,e0000000/sbuf@f,e0010000/le@f,c00000:tpe
net /iommu@f,e0000000/sbuf@f,e0010000/le@f,c00000
disk /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/sd@3,0
cdrom /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/st@6,0
tape /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/st@4,0
tape1 /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/st@5,0
tape0 /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/st@4,0
disk3 /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/sd@3,0
disk2 /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/sd@2,0
disk1 /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/sd@1,0
disk0 /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/sd@0,0
```

```
ok devalias disk
disk /iommu@f,e0000000/sbuf@f,e0010000/espdma@f,400000/esp@f,800000/sd@3,0
ok
```

## 删除设备别名

由 `nvalias` 命令定义的别名存储在脚本中，并一直存在直到使用 `nvunalias` 命令将其删除，或者使用 `set-defaults` 命令将系统配置恢复到原始默认值。请注意，使用 `devalias` 命令定义的别名不会存储在脚本中，并在系统重启时会丢失。

要删除非易失性设备别名（存储在脚本中的别名）`disk2`，请在 OpenBoot 提示符下输入以下命令：

```
ok nvunalias disk2
```
