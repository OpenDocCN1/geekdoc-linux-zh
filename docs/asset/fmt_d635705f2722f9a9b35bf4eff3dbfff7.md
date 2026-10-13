
`vi` 代表 visual editor（视觉编辑器）。这个经典的 Unix 编辑程序包含了一套强大的功能，可用于查找和重复操作，以更快速地进行更改并生成文件。它丰富的功能带来了卓越的结果；然而，它像一把双刃剑，因为对于初学者来说，很难掌握。

`whoami` 命令 `whoami` 将确切告诉你你是谁。不是形而上学意义上的，而是指你在系统中的身份。某些安装命令可能会根据你是否是 root 用户而异。检查你的身份通常可以避免在程序似乎没有完全编译时的挫败感。

这些命令将为你导纵 Linux 文件系统提供极佳的基础。在与 Linux 打交道的过程中，你将需要使用这些命令，因此现在牢记它们是一个极好的主意。如果这些大部分命令对你来说是全新的，记住在本节开头做一个书签以备后后参考。完成后，你就可以准备进入下一节了。

## 理解 Linux 文件系统布局

文件系统布局经过了精心组织，以便对文件系统有基础了解的人能够快速方便地找到文件。虽然初看起来并不如此，但当你习惯了这种布局后，你就能穿过目录定位你所需的位置。严格的命名规范和文件存储位置使得 Linux 能够继续其开源开发，而不会干扰任何人。让我们看看根级目录及其包含的文件。这里还包含一些最重要的目录及其文件：

| 权限 | 所有者 | 组 | 大小 | 日期 | 名称 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| drwx-xr-x | 2 root | root | 4096 | Jan 11:37 | bin |

| drwxr-xr-x | 4 root | root | 1024 | Jan 8 16:41 | boot |

| drwxr-xr-x | 21 root | root | 118784 | Jan 9 10:19 | dev |

| drwxr-xr-x | 57 root | root | 4096 | Jan 13 04:02 | etc |

| drwxr-xr-x | 3 root | root | 4096 | Jan 9 10:15 | home |

| drwx-xr-x | 2 root | root | 4096 | Oct 7 07:16 | initrd |

```
drwxr-xr-x 9 root 4096 Jan 9 11:33 lib
drwx------ 2 root 16384 Jan 8 18:38 last+found
drwxr-xr-x 2 root 4096 Sep 8 14:11 misc
drwxr-xr-x 2 root 4096 Jan 9 10:19 mnt
drwxr-xr-x 2 root 4096 Oct 7 07:16 opt
dr-xr-xr- 49 root 4096 Jan 0 05:18 proc
drwx------ 13 root 4096 Jan 13 15:09 root
drwxr-xr-x 2 root 8192 Jan 9 11:37 sbin
drwxrwwt 6 root 4096 Jan 13 04:02 tmp
drwxr-xr-x 15 root 4096 Jan 8 16:40 usr
drwxr-xr-x 19 root 4096 Jan 8 16:49 var
```

这是安装 Fedora Core 后应该拥有的内容的精确表示。

### /bin

`/bin` 目录包含了 Linux 的所有基本二进制程序和命令。进入 `/bin` 目录并查看列表，你将看到上一节列出的大部分命令，除了内置于 Bash shell 的命令。当你在计算机上安装软件和软件包时，此目录会随着命令的增加而扩展。

### /boot

`/boot` 目录包含了引导程序和 Linux 内核的状态文件。进入此目录并看一看——这里内容太多了。这是 GRUB 文件所在的位置，位于 `/boot/grub`。

### /dev

`/dev` 目录包含了特殊设备。查看此目录将产生一些有趣的结果。这里的每一个文件都代表系统上的一个特定设备，无论是硬件（hardware）设备还是软件（soft）设备。大小通常位于此处；它被分为两部分。第一部分代表主设备号；传递给内核的设备驱动。第二部分代表次设备号并传递给内核以允许进一步选择设备。例如，查看磁盘文件。这些文件由 IDE 字符引导。你的第一个硬盘是 `hda`。如果你执行 `ls hda*`，你将看到列出的每个设备。注意第一个设备列，因为它是第三部分。

## 第3章 使用 Linux

每个列表项都有不同的设备号，属于该分区，或者在 `hda` 的情况下，指定整个硬盘。访问“文件”目录意味着某种设备而不是文件系统。这些设备中的可能会产生意外的影响。你可能需要的其他设备包括鼠标、CD-ROM、扫描仪和调制调器。任何媒体通常都可以通过 `mount` 命令挂载到特定的目录。例如，在 `/mnt` 下运行。

### /etc

`/etc` 目录包含了特定于你计算机的配置文件。大部分配置文件都存储在这里，并且需要多个文件的应用程序有自己的子目录。查看此目录的列表会因为其文件数量而让你惊讶。为了方便快速参考，我们已经对它们进行了分类，如表 3.1–3.3 所示。

#### 3.1 网络相关文件

| 文件 | 描述 |

| :--- | :--- |

| exports | 网络文件系统 (NFS) 服务器 |

| host.conf | hosts 配置 |

| hosts | 带 IP 地址的主机列表 |

| hosts.allow | 允许的 TCP wrapper |

| hosts.deny | 拒绝的 TCP wrapper |

| protocols | 带有描述的协议列表 |

| resolv.conf | 名称解析配置 |

| services | 带有端口的服务 |

#### 3.2 Shell 配置文件

| 文件 | 描述 |

| :--- | :--- |

| bashrc | 所有用户的默认配置 |

| csh.cshrc | C shell 配置文件 |

| csh.login | C shell 功能 |

| profile | Bash shell 配置文件 |

| shells | 系统所有 shell 的列表 |

#### 3.3 杂项系统文件

| 文件 | 描述 |

| :--- | :--- |

| passwd | 用户定义 |

| shadow | 带有 MD5 的影子密码文件 |

| group | 组定义 |

| gshadow | 影子文件 |

| aliases | 系统和邮件别名 |

| aliases.db | 系统和邮件别名 |

| crontab | 系统 cron 配置，包含按计划运行的命令列表 |

| fstab | 文件系统和挂载点列表 |

| inittab | init 进程配置 |

| motd | 今日消息 |

| mtab | 当前挂载的文件系统列表 |

| printcap | 打印机配置 |

| sysctl.conf | Fedora 的内核配置 |

| syslog.conf | 日志配置 |

| termcap | 终端类型描述 |

当你根据需要自定义服务器时，你将频繁使用其中的许多文件。第 4–7 章将深入系统各个方面的文件设置和配置。现在，只需熟悉一些名称以及每个文件所属内容的概概述。

除了此目录内的文件外，它们内部还有许多重要的子目录。让我们来看一些：

`etc/cron.d` 此目录存放由 `crontab` 运行的脚本。`crontab` 是一个由 `cron` 守护进程 (`crond`) 解析的文件，决定了脚本应何时运行。

`etc/cron.daily` 日常 cron 目录每天运行一次其中的任何脚本。你不需要为这里的脚本设置 `crontab` 条目。

`etc/cron.hourly` 类似于 `/etc/cron.daily` 目录，此目录不需要位于其中的脚本具有独立的 `crontab` 条目。唯一的区别是，正如其名称所示，脚本每小时运行一次。

`etc/cron.monthly` 此目录内的脚本也都不需要独立的 `crontab` 条目。唯一的区别是，正如其名称所示，脚本每月运行一次。

`etc/cron.weekly` 和它的所有兄弟目录一样，这些文件会自动运行。每周扩展意味着这些文件每周运行一次。

`etc/default` `/etc/default` 目录包含了默认的 `useradd` 文件（无双关）。该文件包含：

```
## useradd defaults
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

每次创建新用户时，这些值将被分配给该用户。在自定义系统时，你可能希望更改这些值。

`etc/httpd` 这是你的 Apache Web 服务器配置文件所在地。稍后的第 8 章“Apache Web 服务器：安装与配置”中会有更多介绍。

`etc/mail` 此目录包含了 `sendmail` 的配置文件，这是一个从你的系统发送邮件的程序。这里包含了与访问权限和用户的各种配置文件。
