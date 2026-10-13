
### 11.1 文件系统结构

Linux 文件系统层次结构 (FHS) 是名称和位置的权威参考。在本节中，我们提供了标准的概述以及对未涵盖部分的描述。

完整标准可以在此处查看：

http://www.com/fhs/

#### 11.1.1 FHS 概述

这里提到的目录和文件是 FHS 指定的一个子集。请检查最新的 FHS 文档以获取最新的信息。

- `/dev`: `/dev` 目录包含代表连接设备的文件系统项。这些文件对于系统的运行至关重要。
- `/etc`: `/etc` 目录留给本地机器的配置文件。`etc` 中不应放置二进制文件。过去放在 `/etc` 中的二进制文件应该进入 `/sbin` 或可能的 `/bin`。
- X11 和 skel 目录应该是 `/etc` 的子目录：

`/etc`
  - X11
  - skel

`X11` 目录用于 X86config 等配置文件。`skel` 目录用于“骨架”用户，在首次创建用户时用于填充家目录。
- `/lib`: `/lib` 目录应该只包含执行 `/bin` 和 `/sbin` 中二进制文件所需的库。
- `/proc`: `/proc` 目录包含提取或向内核发送信息的特殊文件。它是使用 `cat` 命令访问操作系统信息的简单方法。
- `/sbin`: `/sbin` 目录用于 root 用户使用的执行文件，且仅包含启动系统、挂载 `/usr` 以及执行系统恢复操作所需的执行文件。标准规定：

> "`/sbin` 通常包含 `/bin` 中的二进制文件中对于启动系统至关文件。在 `/usr` 已挂载（当出现问题时）之后执行的任何内容都应该放置在 `/usr/sbin`。本地的系统管理二进制文件应该放在 `/usr/local/sbin.`"

至少，以下程序应位于 `/sbin` 中：

```
clock, getty, init, update, mkswap, swapon, swapoff, halt,
reboot, shutdown, fdisk, fsck.*, mkfs.*, lilo, arp, ifconfig,
route
```

### /usr 目录

`/usr` 目录用于整个站点范围内共享的文件。`/usr` 目录通常有自己的分区，并且应该能够以只读方式挂载。以下目录应该是 `/usr` 的子目录：

```
/usr
- X11
- bin
- dict
- doc
- etc
- games
- include
- info
- lib
- local
- man
- sbin
- share
- src
```

`X11` 目录用于 X 窗口系统（Red Hat Linux 上的 XFree86），`bin` 用于可执行文件，`doc` 用于非 man 页面文档，`etc` 用于站点范围内的配置文件，`include` 用于头文件，`info` 用于 GNU 文件，`lib` 用于库，`man` 用于 man 页面，`sbin` 用于系统管理二进制执行文件（那些不属于 `/sbin` 的文件），`src` 用于源代码。

### /usr/local 目录

FSSTND 规定道：

> "//usr/local 层级结构由系统管理员在本地安装软件时使用。当系统软件更新时，需要对其进行覆盖。它可能用于一组机器共享的程序和数据，但在 /usr 中未找到这些。"

`/usr/local` 目录的结构与 `/usr` 目录相似。它包含以下子目录，其用途与 `/usr` 目录中的目录相似：

```
/usr/local
- bin
- doc
- etc
- games
- include
- info
- lib
- man
- sbin
- src
```

### /var 目录

由于 FSSTND 要求能够以只读方式挂载 `/user`，因此任何写入日志文件或需要池（spool）或锁目录的程序，可能都会将它们写入 `/var` 数据中。FSSTND 规定 `/var` 用于：

> "可变数据文件。这包括池目录和文件、管理和日志数据文件，以及瞬态和临时文件。"

以下目录应该是 `/var` 的子目录：

```
/var
- log
- catman
- lib
- local
- named
- nis
- preserve
- run
- lock
- tmp
- spool
- at
- cron
- lpd
- mail
- message
- rwho
- small
- uucp
- news
```

系统日志文件（如 `wtmp` 和 `lastlog`）存放在 `/var/log`。`/var/lib` 目录还包含 RPM 系统数据库。格式化的 man 页面存放在 `/var/catman`，日志文件存放在 `/var/lock`。`/var/spool` 目录具有各种存储数据文件的系统的子目录。

## 11.2 Red Hat 特殊文件位置

### 11.1.2 Red Hat Linux 中的 /usr/local

在 Red Hat 中，`/usr/local` 的预期用途与 FSSTND 规定的略有不同。FSSTND 规定 `/usr/local` 应该是你存放软件的地方，以确保这些软件免受系统软件升级的影响。由于来自 Red Hat 的系统程序已通过 RPM 系统和 GRPM 安全地处理，因此你不需要通过将文件放在 `/usr/local` 来保护它们。相反，我们建议你将 `/usr/local` 用于你本地机器上特有的软件。

例如，如果你通过来自 beavis 的只读 NFS 挂载了 `/usr`。如果你有一个想要安装的软件包或程序，但你不被允许写入 beavis，则你应该将其安装在 `/usr/local` 下。稍后，如果你成功说服了 beavis 的系统管理员从 `/usr` 安装该程序，你就可以从 `/usr/local` 卸载它。

除了 `/var/lib/rpm` 中与 RPM 系统相关的文件（第 9 章）外，还有两个预留给 Red Hat Linux 配置和操作的特殊位置。

控制面板及相关工具在 `/usr/lib/rhs` 中放置了大量内容。那里可能没有你想要编辑的内容。它大部分由小型脚本、位图和文本文件组成。

另一个位置 `/etc/sysconfig` 存储了配置信息。该目录下的文件主要用户是启动时运行的脚本。可以手动编辑这些内容，但使用适当的控制面板工具更好。

## 11.3 用户、组和用户私有组

管理用户和组在传统上是繁琐的。Red Hat Linux 有一些工具和规范，使得用户和组的管理变得更加简单、更有用。

管理用户和组最简单的方法是通过 Linuxconf（参见第 8 章）。不过，你可以使用 `adduser` 从命令行创建新用户。

### 11.3.1 标准用户

表 11.3.1 列出了安装过程设置的标准用户（本质上是 `/etc/passwd` 文件）。此表中的组 ID (GID) 是该用户的主组。有关组如何使用的详细信息，请参见第 11.3.3 节。

| 用户 | UID | GID | 主目录 | Shell |
|---|---|---|---|---|
| root | 0 | 0 | /root | |
| bin | 1 | 1 | /bin | |
| daemon | 2 | 2 | /sbin | |
| adm | 3 | 4 | /var/adm | |
| lp | 4 | 7 | /var/spool/lpd | |
| sync | 5 | 0 | /sbin | |
| shutdown | 6 | 0 | /sbin | |
| halt | 7 | 0 | /sbin | |
| mail | 8 | 12 | | |
| news | 9 | 13 | | |
| uucp | 10 | 14 | | |
| operator | 11 | 0 | | |
| games | 12 | 10 | | |
| gopher | 13 | 30 | | |
| ftp | 14 | 50 | | |
| nobody | 15 | 99 | | |

*(注：由于原文表格部分数据缺失或对应关系错位，此处根据原文结构进行对齐翻译)*

### 11.3.2 标准组

表 11.3.2 列出了安装过程设置的标准组（这本质上是 `/etc/group` 文件）。

| 组 | GID | 成员 |
|---|---|---|
| root | 0 | |
| bin | 1 | |
| daemon | 2 | |
| adm | 3 | |
| tty | 4 | |
| disk | 5 | |
| lp | 6 | |
| mem | 7 | |
| wheel | 8 | |
| mail | 9 | |
| news | 10 | |
| uucp | 11 | |
| man | 12 | |
| games | 13 | |
| gopher | 14 | |
| dip | 15 | |
| sys | 16 | |
| cd | 17 | |
| lp | 18 | |
| floppy | 19 | |
| users | 20 | |
| dial | 21 | |
| lp | 22 | |
| lp | 23 | |
| lp | 24 | |
