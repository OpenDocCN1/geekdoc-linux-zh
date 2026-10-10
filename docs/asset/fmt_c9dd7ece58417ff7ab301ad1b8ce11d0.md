
- `modinfo` 提供详细的模块数据。

关于模块，故障有时会触发内核消息。`dmesg` 命令的方便之处在于查看与当前事件相关的内核消息。在启动时，你的发行版可能会对内核环形缓冲区取快并将数据存储在文件中（通常为 `/var/log/dmesg`）。这两个缓冲区信息源帮助你跟踪模块问题。

环形缓冲区是内存中固定大小的数据结构。它不是环形的，而是像管子。在内核环形缓冲区中，随着新消息进入管子，旧消息向结构末尾移动，最旧的消息从管口流出（被删除）。

`dmesg` 工具将将当前内核环形缓冲区输出到 `STDOUT`。使用 `grep` 命令挖掘消息非常有帮助。这种方法的示例如列表 14.4 所示。

### 列表 14.4：使用 grep 使用 dmesg

```
$ dmesg | grep -i driver
-
[ 1.674321] e1000: Intel(R) PRO/1000 Network Driver - version 7.3221-k8-NAPI
[ 3.614747] cdrom: Uniform CD-ROM driver Revision: 3.20
-
[ 48.828793] tun: Universal TUN/TAP device driver, 1.6
[ 8768.969714] usbcore: registered new interface driver usb-storage
$
```

## 探索内核模块 401

你可以使用不同的搜索词来过滤 `dmesg` 工具的输出。例如，如果你只想查找有关 USB 设备问题的信息，可以管道执行 `dmesg -i usb` 命令。

`lsmod` 工具显示当前 Linux 内核中模块的状态。列表 14.5 显示了 openSUSE 发行版上的一个示例片段。

### 列表 14.5：使用 lsmod 显示模块状态

```
$ lsmod
Module Size Used by
af_packet 49152 4
[--]
bridge 172032 1 ebptable_broute
stp 16384 1 bridge
btrfs 1327104 1
scsi_dh_alua 20480 0
$
```

在 `lsmod` 的输出中，每个模块单独列成一行。第一列是模块名称。

注意列表 14.5 中的 `Used by`（使用者）列。该列中的数字表示当前使用该模块的进程或其他模块的数量。如果是另一个内核模块正在使用它，则会显示另一个模块的名称。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_456_0.png)

你可以通过查看 `/proc/modules` 文件的内容获取与 `lsmod` 工具显示的相同信息。然而，它的格式没有那么漂亮。

你可以通过 `modinfo` 工具找到有关特定内核模块的更详细信息。如列表 14.6 所示，这可能需要超级用户权限。

### 列表 14.6：使用 modinfo 显示详细模块信息

```
$ modinfo bridge
filename: /lib/modules/[-]/kernel/net/bridge/bridge.ko
alias: rtl-Link-bridge
version: 2.3
license: GPL
suserelease: openSUSE Leap 15.0
srcversion: D039BA7E5E769F636E31A8C
depends: stp,plc
retpoline: Y
intree: Y
vermagic: [-]SMP mod_unload modversions retpoline
$
```

## 安装内核模块

注意列表 14.6 中的内核模块文件名。内核模块文件通常具有 `.ko` 扩展。还要注意到模块的版本号也被显示出来了。如果你需要跟踪与特定模块相关的已知错误，这非常有帮助。

Linux 会在系统需要时自动加载模块。但是，通常你可能想要测试某个模块或尝试新的模块配置。为了做到这一点，你可能需要手动将模块安装到内核。这也被称为插入或加载到内核。在本节中，我们将查看一些可以帮助你将模块加载到内核的工具。它们如下：

- `insmod`
- `modprobe`
- `depmod`

`insmod` 工具允许你将单个模块插入到 Linux 内核中。遗憾的是，因为它非常基础，你必须为模块文件提供绝对目录引用。此外，该命令不会加载任何所需的模块依赖项。openSUSE 发行版上的示例片段如 14.7 所示。

### 列表 14.7：使用 insmod 向内核插入单个模块

```
$ lsmod | grep -i joydev

$ sudo insmod /lib/modules/-/kernel/drivers/input/joydev.ko
$
$ lsmod | grep -i joydev
joydev          24576 0
```

在 14.7 中，使用 `insmod` 命令检查系统是否存在模块名为 `joydev` 的已加载模块。没有找到。因此，`insmod` 命令使用其全名和目录位置将其插入内核。再次使用 `lsmod` 命令显示该模块确实已加载到内核。

`modprobe` 命令比 `insmod` 工具更易用，因为你可以通过模块名称指定模块。它还会加载插入的模块运行所需的任何额外模块（依赖项）。列表 14.8 显示了一个示例片段，它在 `modprobe` 命令上使用 `-v` ，在插入模块及其所有当前未加载的依赖项时显示更多信息。

### 列表 14.8：使用 modprobe 插入模块及其依赖项

```
$ sudo modprobe -v dm_mirror
insmod /lib/modules/-/kernel/drivers/md/dm-log.ko

insmod /lib/modules/[...]/kernel/drivers/md/dm-region-hash.ko

insmod /lib/modules/[...]/kernel/drivers/md/dm-mirror.ko

$ lsmod | grep -i dm_mirror

| dm_mirror | 28672 0 |

| dm_region_hash | 16384 1 dm_mirror |

| dm_log | 16384 2 dm_mirror,dm_region_hash |

| dm_mod | 139264 3 dm_mirror,dm_log,dm_multipath |

$ sudo modinfo dm_mirror

filename: /lib/modules/[...]/kernel/drivers/md/dm-mirror.ko

license: GPL

author: Joe Thornber

description: device-mapper mirror target

susereversion: openSUSE Leap 15.0

srcversion: A74B80C071D9A4F94E83

depends: dm-region-hash,dm-mod,dm-mod

retline: Y

intree: Y

vermagic: SMP mod_unload modversions retpoline

parm: resync_throttle=0

$
```

`dm_mirror` 模块允许卷管理器镜像逻辑卷。在列表 14.8 中，当使用 `modprobe` 命令加载此模块时，它还会加载另外两个模块，`dm_mirror` 模块正常工作需要它们。注意 `modprobe` 工具正在调用 `insmod` 工具执行插入。还要注意 `dm_mirror` 模块的名称略有不同，为 `dm-mirror.ko`，如 `modinfo` 工具的输出所示。

`modprobe` 使用 `modules.dep` 文件确定任何模块依赖。它通常位于 `/lib/modules/` 子目录下，如列表 14.9 所示。

### 列表 14.9：查看 modules.dep

```
$ ls /lib/modules/[...]/modules.dep
/lib/modules/[...]/modules.dep
$ grep -n mirror /lib/modules/[...]/modules.dep
kernel/drivers/md/dm-mirror.ko:
kernel/drivers/md/dm-region-hash.ko
kernel/drivers/md/dm-log.ko
kernel/drivers/md/dm-mod.ko
```

在列表 14.9 中，使用 `grep` 工具在 `modules.dep` 文件中搜索单词 `mirror`。要找到特定模块的依赖项，你可以在文件中定位模块名称。在冒号（`:`）之后，按全名列出模块的依赖项。对于 `dm_mirror (dm-mirror.ko)`，模块依赖是 `dm-region-hash`、`dm-log` 和 `dm-mod`。这与列表 14.8 中 `modinfo` 工具的输出一致。

你可以使用 `depmod` 命令扫描系统中任何未检测到的硬件。这对于排排除新设备的问题很有用。示例片段如 14.10 所示。

### 列表 14.10：使用 depmod 工具更新 modules.dep 文件

```
$ sudo depmod -v
[...]
/lib/modules/[]/kernel/sound/soc/intel/snd-hifi-platform.ko needs
snd_pcm_lib_preallocate_pages_for_all:
/lib/modules/[]/kernel/core/snd-pcm.ko
$
```

在列表 14.10 中，`depmod` 工具扫描系统，确定任何所需的模块，检查模块的依赖关系，并更新相应的 `modules.dep` 文件。注意它还将其活动显示到标准输出（`STDOUT`）。

## 移除内核模块

移除 Linux 系统上不再使用的任何内核模块是一个好主意。如果你只需要移除（卸载）一个没有依赖项的模块，可以使用 `rmmod` 命令。示例如 14.11 所示。

### 列表 14.11：使用 rmmod 工具移除模块

```
$ lsmod | grep joydev
joydev          24576 0
$
$ sudo rmmod -v joydev
$
$ lsmod | grep joydev
$
```

注意列表 14.11 中，`rmmod` 工具理解模块名称，因此你不需要为模块文件提供绝对目录引用。一旦模块被卸载，`lsmod` 工具将不再显示该模块。

`modprobe` 工具对于移除具有一个或多个依赖项的模块有用。你只需要添加 `-r` 关，如果你想要详细信息，请包含 `-v` 开关，如列表 14.12 所示。

### 列表 14.12：使用 modprobe 移除模块及其依赖项

```
$ sudo modprobe -rv dm_mirror
rmmod dm_mirror
rmmod dm_region_hash
rmmod dm_log
$
```

在 14.12 中，`dm_mirror` 模块与其两个依赖项一起被卸载。注意如果模块没有加载，将看不到任何消息，只会得到命令行提示符。

## 总结

当内核模块失败或你需要测试新模块时，了解模块文件及其配置文件的位置至关重要。同样重要的是使用各种可用工具诊断问题。由于模块可以与内核动态链接，你应该理解如何使用正确的工具执行这些任务。你 Linux 工具箱中的这些额外工具可以帮助快速解决内核模块的问题。

## 考试要点

- 内核模块的位置。内核模块具有 `.ko` 扩展，通常位于 `/lib/modules/` 目录的目录下。每个特定的 Linux 内核版本都有子目录。某些发行版有额外的目录，例如 `/usr/lib/modules/`，它是 `/lib/modules/` 的硬链接。

- 区分模块配置文件的位置。旧的 Linux 发行版使用单个文件 `/etc/modules.conf` 作为它们的内核模块配置文件。更现代的发行版使用配置目录，可以是 `/etc/modprobe.d/`、`/etc/modules-load.d/`、`/lib/modprobe.d/`、`/usr/lib/modprobe.d/` 和/或 `/run/modprobe.d/` 目录。在配置目录下，模块配置文件具有 `.conf` 扩展。

- 总结故障排除工具。因为内核模块可能会失败，通常使用 `dmesg` 工具查看最近的内核消息，或翻阅 `/var/log/dmesg` 文件（可用）以查看启动内核问题。

`lsmod` 工具显示所有当前加载的模块以及其他模块的名称。`modinfo` 程序非常有用，因为它显示了模块的详细信息，包括它的依赖关系。

**比较安装内核模块的工具。** 低级 `insmod` 工具需要完整的文件名才能将模块插入内核，这可能非常麻烦。此外，`modprobe` 工具只需要模块名称。它搜索 `modules.dep` 文件来确定并加载任何依赖项。

**解释移除内核模块的工具。** `rmmod` 工具是一个底层工具。虽然它不需要完整的文件名即可从内核中卸载模块，可能会导致多余的模块。`modprobe` 工具使用 `-r` 选项会卸载模块并解除链接。

## 复习题

- 1. 关于内核模块，下列哪些正确？（多选）

  - A. 它是一个自包含驱动文件。

  - B. 它是编译进内核的。

  - C. 它允许根据需要添加功能。

  - D. 它可以在需要时被加载。

  - E. 它让内核保持轻量和灵活。

- 2. 模块文件存储在哪里？（多选）

  - A. `/lib/modules/kernel/` 目录

  - B. `/lib/modules/KernelVersion/` 目录

  - C. `/usr/lib/modules/kernel/` 目录

  - D. `/usr/lib/modules/KernelVersion/` 目录

  - E. `/lib/kernel/modules` 目录

- 3. 模块配置信息存储在哪里？（多选）

  - A. `/etc/modules` 文件

  - B. `/etc/modprobe.d/*.conf`

  - C. `/etc/modules.d/*.conf`

  - D. `/lib/modprobe.d/*.conf`

  - E. `/usr/lib/modprobe.d/*.conf`

- 4. 你需要确定已卸载 `xyz` 模块的依赖关系。使用哪个工具最合适？

  - A. `dmesg`

  - B. `insmod`

  - C. `lsmod`

  - D. `modprobe`

  - E. `modinfo`

- 5. 你需要安装包含所有所需依赖的 `xyz` 模块。你应该使用哪些工具？

  - A. `insmod`

  - B. `modinfo`

  - C. `modprobe`

  - D. `lsmod`

  - E. `depmod`

- 6. 当你在 Linux 系统上安装 USB 设备时，显示未检测到设备。下列哪个命令最适合排查这种情况？

  - A. `lsmod`

  - B. `modinfo`

  - C. `dmesg`

  - D. `depmod`

  - E. `insmod`

- 7. `modprobe` 工具使用 `____` 文件来确定任何依赖项。

  - A. `modules.dep`

  - B. `/lib/modules`

  - C. `/usr/lib/lib/modules`

  - D. `/etc/modprobe.d`

  - E. `/lib/modprobe.d`

- 8. 你需要将 `abc` 模块插入内核。它没有任何依赖项。使用哪个工具最合适？

  - A. `lsmod`

  - B. `modinfo`

  - C. `dmesg`

  - D. `depmod`

  - E. `insmod`

- 9. 你需要从内核中卸载 `abc` 模块。它没有任何依赖项。使用哪个工具最合适？

  - A. `insmod`

  - B. `unload`

  - C. `rmmod`

  - D. `modprobe`

  - E. `rm -f`

- 10. 你需要移除 `xyz` 模块及其所有的依赖项。使用哪个命令最合适？

  - A. `dmesg`

  - B. `modprobe -r`

  - C. `lsmod`

  - D. `paste`

  - E. `groupdel`

## 安全你的系统

第四部分

![](img/0c1e7d2699b9d354c8d2f84669d18d3_464_0.png)

### 第 15 章

#### 应用所有权和权限

- 目标 3.1：给定场景，应用或获取适当的用户和/组权限以及所有权。

![](img/0c1e7d2699b9d354c8d2f84669d18d3_466_0.png)

防止未经访问文件和目录是任何 Linux 管理员工作的主要部分。Linux 提供了几种不同的文件保护方法，这使得安全性变得有点复杂。本章深入研究 Linux 文件和目录安全，并演示如何在你的 Linux 系统上实现它。首先，它查看了 Linux 如何为文件和目录分配所有权。然后讨论了自 Linux 诞生以来就存在的基本文件和目录安全功能。随后，它检查了两种为系统文件和应用程序添加额外保护的新方法。简要概述了 Linux 如何处理处理系统所需的管理员权限。

#### 查看文件和目录权限

Linux 的核心安全功能是文件和目录权限。Linux 通过为每个文件和目录分配一个所有者并允许所有者设置基本安全设置以控制对该文件或目录的访问来实现这一点。以下章节将介绍 Linux 如何处理文件和目录权限。

#### 理解所有权

Linux 通过为每个文件和目录分配一个所有者，并允许所有者设置基本安全设置以控制对该文件或目录的访问。Linux 使用以下三层方法来保护文件和目录：

字体 `**所有者**`：在 Linux 系统中分配用户。

- `**组**`：Linux 系统也会为用户分配所属组。

- `**其他**`：对于既不是所有者也不属于该组的用户。

你可以通过向 `ls` 命令添加 `-l` 选项来查看文件或目录的所有者和组。

##### 15.1 查看文件或目录的所有者

```bash
ls -l
if (condVar > someVal) {console.log("xxx")}
```

`##` 图 15.1 `ls` 输出中显示的文件和目录权限
