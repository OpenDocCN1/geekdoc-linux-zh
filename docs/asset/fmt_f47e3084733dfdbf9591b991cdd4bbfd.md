
本节描述了打开电脑并出现登录提示时发生的过程。简而言之，内核被加载，第一个程序——即 `init`——被启动。随后，它负责系统的基本配置（文件系统的链接）以及启动许多守护进程（用于网络功能、打印机支持等）。

在大多数情况下，`LILO` 负责第一部分，即启动内核（参见第 183 页）。然而，内核也可以直接从启动磁盘加载并执行。`LILO` 可用于向内核传递各种参数（第 48 页）。在内核启动后，它暂时只能以只读方式访问根分区。

接下来的部分，即 `/sbin/init` 程序的执行，在很大程度上取决于计算机的配置。虽然几乎所有的发行版（`Slackware` 除外）都由 System V Init 进程引导（正如许多其他 Unix 系统中所使用的那样），但在细节上仍有许多差异，特别是哪些 `init` 文件位于哪些目录中，不同的运行级别（runlevels）分配了哪些数字或字母等。

作为结论，还有一个进一步的警告：如果你想修改涉及 `init` 进程的文件，必须极其小心！如果你运气不好，将再无法启动 `Linux`。这意味着你无法纠正自己的错误！（补救：首先，尝试在 `LILO` 中指定附加启动参数 `single` 或 `emergency` 以进入单用户模式，如果这不起作用，你必须使用安装磁盘启动系统，手动挂载根系统并执行修复。在大多数安装磁盘上没有（可用的）编辑器——至少确保你备份了所有修改的文件。）

千万不要尝试安装不同发行版的 Init-V 软件包！遗憾的是，每个 `Linux` 发行版使用的配置文件不同，由于这个原因，Init-V 软件包比任何其他软件包都更取决于发行版。

以下描述面向 `RedHat` 发行版。原则上，类似的程序适用于其他发行版，但某些文件位于不同的目录或具有不同的名称。此外，进程启动或执行顺序随发行版而异。为了方便识别，你将在附录中找到其他发行版 Init V 进程的一些提示。

在下文中，我们不断谈到脚本。脚本是由解释器执行的（通常是较小的）程序。对于本节讨论的所有脚本，解释器都是 `bash`。在 `Linux` 下，`bash` 被用作命令解释器（类似于 `DOS` 下的 `COMMAND.COM`）。这种对 `bash` 的交互式使用将在第 12 章描述。`bash` 编程入门可以在第 13 章找到。

### 运行级别

内核启动 `/sbin/init` 作为第一个程序。所有尚未评估的内核参数都会传递给它。通过这种方式，可以确保 `Linux` 以单用户模式启动。（细节可以在 `init` 的 man 页中找到。）

因此，`init` 是第一个运行的进程。所有后续进程都通过 `init` 的子进程直接或间接启动。（如果你执行 `pstree` 或 `ktop`，你将立即识别出 `init` 的主作用。）在关机时，`init` 是最后一个运行的进程，负责所有其他进程的有序终止。

运行级别（runlevel）的概念是理解 System V 机制的核心，你可以在不同的运行级别上操作计算机。正常情况是带网络的多用户模式（运行级别 3）。对于专门在 X 下运行的电脑，是扩展的运行级别 5（多用户、网络、自动启动 X `xdm`）。对于维护，有限制的模式，例如运行级别 2（无网络的多用户）或运行级别 1（单用户）。运行级别 0（停止）和 6（重启）留给关机。

## 126 LINUX 基础

![](img/b30873dd3d753687a59253fb9ad26a0b_153_0.png)

**图 5.1** 进程层次结构。

遗憾的是，`SuSE` 和 `Debian` 等不同发行版的数量略有不同。每个项目的含义记录在 `/etc/initab` 中。

在系统启动时，默认运行级别由 `/etc/initab` 中的 `initdefault` 行决定。`root` 也可以运行期间使用它更改运行级别（`x` 必须替换为指定运行级别的数字或字母）。例如，对于某些维护任务，切换到单用户模式是有意义的。运行级别也会通过 `shutdown` 和 `Ctrl+Alt+Del` 改变——`Linux` 运行级别 6 以关机。

## Inittab

启动时，`init` 通过 `/etc/inittab` 文件控制。`inittab` 条目遵循以下语法方案：

```
id-code:runlevel:action:command
```

`init-code` 由两个字符组成，唯一标识该行。`run-level` 指定该条目对哪个运行级别有效。`action` 包含给 `init` 的指令。`command` 指定要启动哪个 `Linux` 命令或程序。

以下列表显示了最重要的 `action` 关键字（你可以通过 `man inittab` 获取完整描述）：

- `ctrlldel`：指定 `init` 如何响应 `Ctrl+Alt+Del`
- `default`：定义 `init` 的默认运行级别
- `once`：`init` 在切换到此运行级别时启动指定的命令
- `respawn`：`init` 在命令终止后重启该命令
- `sysinit`：`init` 在期间启动一次命令
- `wait`：`init` 等待命令终止

以下列表代表 `RedHat` 的简略 `inittab`：

```
# /etc/inittab for RedHat
init:0:init:/init
init:1:init:/sbin/init
init:2:init:/sbin/init
init:3:init:/sbin/init
init:4:init:/sbin/init
init:5:init:/sbin/init
init:6:reboot:/sbin/init
```

（注：由于原文中存在大量重复的 OCR 错误片段和乱码，此处已根据逻辑进行了整合并去除了冗余部分。）

如果你使用 ISA 即插用卡，你应该查看 `isapnp`、`pnpdump` 和 `isapnp.conf` 的 man 文档。

- 以读写模式挂载根分区。
- 挂载 `/proc` 目录。
- 为内核启动模块支持（仅适用于带有旧内核的发行版；自内核 2.2 版本起，此任务由内核组件节点负责）。
- 激活声卡、MIDI 模块。
- 激活 RAID 支持；如果 `/etc/fstab` 存在，则通过 `ifup` 创建其中列出的虚拟分区。另见第 157 页。
- 根据 `/etc/fstab` 检查需要挂载到文件系统的分区。
- 挂载分区（不包括 NFS 分区，因为网络服务尚不可）。
- 设置文本控制台的字符集（`/sbin/setsysfont`）。
- 激活整个文件系统的配额。
- 设置系统时间（考虑 `/etc/sysconfig/clock`）。
- 链接交换文件（根据 `/etc/fstab`）。
- 初始化串口接口（通过存在的 `/etc/rc.d/rc.serial`）。
- 如果找到 SCSI 驱动器，则激活相应的内核模块。
- 将内核消息存储在 `/var/log/dmesg` 中。
- 初始化随机数生成器。

## rc 文件

`init` 和 `initab` 负责控制 `init` 进程，实际工作由从 `/etc/rc.d/` 启动的众多 `rc` 脚本完成。`rc` 是新的运行级别 n。`rc` 首先处理 `/etc/rc.d/init.d/` 文件，其中执行了如 `daemon` 和 `killproc` 等宏。然后，在运行进程上执行所有 `rc.d/S*` 脚本。最后，所有 `S*` 都会为执行的运行级别启动新进程。

```
rc1: (single user)
K09keytable K20rwhod K60atd K70syslog S00single
K15gpm K30sendmail K60cron K95nfs S01kernel
K20nfs K50init K60ipld K96pcmcia S20random
K20usersd K55rooted K65portmap K97network
```

```
rc3: (multi-user with network)
K20usersd S10network S40atd S50init S80sendmail
```

下表显示了选特定运行级别执行的脚本文件，例如当切换到单用户模式时，各种网络服务、`cron` 和 `syslog` 会被停止。

`K20rwhod S15nfs S40cond S60lpd S85gpm K55routed S20random S40portmap S60nfs S99local S01kernel S30syslog S45pcmcia S75keytable`

准确来说，脚本文件实际上并不位于 `rc/` 目录中，该目录仅包含指向它们的链接。这样做的处是，某些脚本文件（例如用于启动/停止互联网守护进程的 `inet`）可以用于多个运行级别，并在必要时进行集中修改。

链接名称并不像它们看起来那么简单：首字母表示它是启动脚本还是停止脚本。`S` 和 `K` 链接通常指向同一个文件；脚本

脚本文件本身存储在 `/etc/rc.d/init.d` 中。这些程序首先从 `/etc/sysconfig` 中的文件读取配置信息。相应的程序——即网络守护进程、鼠标驱动程序等——被启动。

## Init 脚本
