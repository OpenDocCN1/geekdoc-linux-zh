
表 7-4 显示了用户主目录中最重要的文件：

| File | Description |
|---|---|
| `.profile` | 用户的私有登录脚本 |
| `.bashrc` | bash 的配置文件 |
| `.bash_history` | bash 中先前运行的命令列表 |

## 表 7-4

如果没有特殊设置，所有用户的主目录都位于 `/home` 目录下。用户的主目录也可以通过快捷方式 `~` 来寻址，因此 `~/.bashrc` 指的是用户主目录中的文件 `.bashrc`。

在许多情况下，/home 目录位于不同的分区上，甚至可能位于不同的计算机上（使用主目录的集中管理）。

## 库 (/lib)

许多程序使用特定的函数，这些函数也被其他程序使用。这种标准函数从实际程序中移除，存储在系统中，并在程序运行时才调用。它们被称为 *共享库*。

`/lib` 目录包含 `/bin` 和 `/sbin` 目录中程序使用的库。内核模块（未编译进内核的硬件驱动程序）位于 `/lib/modules/` 目录中。

你可以在 `/usr` 目录下找到额外的库。

## 可移动媒体的挂载点 (media/*)

SUSE Linux 在 `/media/` 目录中为可移动媒体创建目录。它为检测到的每种媒体创建一个单独的目录：

- `/media/floppy/`—为软盘驱动器创建。
- `/media/cdrom/`—为 CD-ROM 驱动器创建。
- `/media/cdrecorder`—为 CD 烧录机创建。
- `/media/dvd/`—为 DVD 驱动器创建。
- `/media/usbdisk/`—为 USB 闪存盘创建。
- `/media/medianame`—在插入带标签的可移动媒体后创建。

## 应用程序目录 (/opt)

已安装的程序可以将静态文件存储在 `/opt` 目录中。首先，创建一个以应用程序名称命名的目录。然后文件存储在该目录中。示例包括 GNOME (`/opt/gnome`) 和 KDE (`/opt/kde3`)。

## 管理员的主目录 (/root)

系统管理员的主目录不像普通用户那样位于 /home 下。最好，它应与根目录 “/” 位于同一分区。只有这样才能保证用户 root 总能无问题地登录并拥有自己的配置环境可用。

## 系统二进制文件 (/sbin)

/sbin 目录包含系统管理的重要程序。普通用户运行的程序也位于 /bin 中。

通常情况下，/sbin 目录中的程序也可以由普通用户运行，但仅用于显示配置值。配置的更改只能由用户 root 进行。

表 7-5 是 /sbin 目录中重要文件的概述。

| File | Description |
|---|---|
| `/sbin/SuSEconfig` | 启动 `/sbin/conf.d/` 目录中的 SuSEconfig 模块。 |
| `/sbin/conf.d/*` | 包含由 `/sbin/SuSEconfig` 调用的 SuSEconfig 系列脚本。它们用于配置整个系统、评估 `/etc/sysconfig/` 目录中配置文件中的条目并写入进一步的配置文件。 |
| `/sbin/yast` | SUSE Linux Enterprise Server 的管理工具。 |
| `/sbin/fdisk` | 修改分区。 |
| `/sbin/fsck*` | 检查文件系统（文件系统检查）。 |
| `/sbin/init` | 初始化系统。 |
| `/sbin/mkfs*` | 创建文件系统（格式化）。 |
| `/sbin/shutdown` | 关闭系统。 |

## 表 7-5

## 服务的数据目录 (/srv)

/srv 目录的子目录包含各种服务的数据。例如，Apache Web 服务器的文件位于 /srv/www/ 目录中，FTP 服务器文件位于 /srv/ftp/ 目录中。

## 临时区域 (/tmp)

各种程序创建临时文件，这些文件存储在 /tmp 中，直到被删除。

## /usr 下的层次结构

根据 FHS，/usr 目录代表第二层层次结构。（/usr 表示 *UNIX 特殊资源* 或 *UNIX 系统资源*。）

这里是所有应用程序、图形界面文件、额外库、本地安装程序以及包含文档的常用共享目录的所在地。请参阅表 7-6。

| Directory | Description |
|---|---|
| `/usr/X11R6/` | X Window System 的文件 |
| `/usr/bin/` | 几乎所有可执行程序 |
| `/usr/lib/` | 库 |
| `/usr/local/` | 不属于 SUSE Linux Enterprise Desktop 10 发行版的本地安装程序 |
| `/usr/sbin/` | 系统管理程序 |
| `/usr/share/doc/` | 文档 |
| `/usr/share/man/` | 手册页（命令说明） |
| `/usr/src/` | 所有程序和内核的源文件（如果已安装） |

## 表 7-6

## 可变文件 (/var)

/var 目录及其子目录包含系统运行时可以修改的文件。

表 7-7 提供了 /var 下最重要的目录的概述。

| Directory | Description |
|---|---|
| `/var/lib/` | 可变库（如 locate 和 rpm 命令的数据库） |
| `/var/log/` | 大多数服务的日志文件 |
| `/var/run/` | 包含正在运行进程信息的文件 |
| `/var/spool/` | 队列目录（打印机、电子邮件） |
| `/var/lock/` | 锁定文件，用于防止设备被多次使用 |

## 表 7-7

## Windows 分区 (/windows)

如果 YaST 找到任何具有 Microsoft 文件系统的分区，它会自动创建一个 /windows 目录。该目录内部有以 Windows 驱动器字符（C、D 等）标记的子目录。

## 进程文件 (/proc)

Linux 通过 /proc 目录向用户提供进程信息。该目录不包含任何真实文件，因此不占用硬盘空间。

/proc 目录在被访问时动态生成（例如，使用 ls /proc）。它包含文件和目录。这些文件中的值可以像硬盘上的普通文件一样读取。一些值，例如内核参数，也可以通过写入相应文件来设置。对此虚拟文件系统的更改仅在系统运行时有效；重启后不会保留。

每个进程都有自己的目录。例如，init 进程始终具有进程号 1。因此有关它的信息位于 /proc/1/ 目录中。该目录包含以下文件：

```text
da10:~ # ls -l /proc/1
total 0
dr-xr-xr-x    3 root root 0 Apr 5 17:28 .
dr-xr-xr-x   62 root root 0 Mar 30 15:09 ..
dr-xr-xr-x    2 root root 0 Apr 5 17:36 attr
-r--r--r--    1 root root 0 Apr 5 17:36 auxv
-r--------    1 root root 0 Apr 5 17:28 cmdline
lrwxrwxrwx    1 root root 0 Apr 5 17:36 cwd -> /
-r--------    1 root root 0 Apr 5 17:36 delay
-r--------    1 root root 0 Apr 5 17:36 environ
lrwxrwxrwx    1 root root 0 Apr 5 17:28 exe -> /sbin/init
dr-x------    2 root root 0 Apr 5 17:36 fd
-rw-------    1 root root 0 Apr 5 17:36 map_base
-r--r--r--    1 root root 0 Apr 5 17:36 maps
-rw-------    1 root root 0 Apr 5 17:36 mem
-r--r--r--    1 root root 0 Apr 5 17:36 mounts
lrwxrwxrwx    1 root root 0 Apr 5 17:36 root -> /
-r--r--r--    1 root root 0 Apr 5 17:28 stat
-r--r--r--    1 root root 0 Apr 5 17:36 statm
-r--r--r--    1 root root 0 Apr 5 17:36 status
dr-xr-xr-x    3 root root 0 Apr 5 17:36 task
-r--r--r--    1 root root 0 Apr 5 17:36 wchan
da10:~ #
```

这些文件可以用 cat 命令查看。例如，文件 /proc/1/status 显示进程的状态，如下所示：

```text
da10:~ # cat /proc/1/status
Name: init
State: S (sleeping)
SleepAVG: 26%
Tgid: 1
Pid: 1
PPid: 0
TracerPid: 0
Uid: 0 0 0 0
Gid: 0 0 0 0
FDSize: 32
Groups:
VmSize: 588 kB
VmLck: 0 kB
VmRSS: 108 kB
VmData: 136 kB
VmStk: 8 kB
VmExe: 432 kB
VmLib: 0 kB
Threads: 1
SigPnd: 0000000000000000
ShdPnd: 0000000000000000
SigBlk: 0000000000000000
SigIgn: ffffffffff770d8fc
SigCgt: 00000000002882603
CapInh: 0000000000000000
CapPrm: 00000000ffffffff
CapEff: 00000000ffffffff
da10:~ #
```

在此示例中，列表显示了进程的名称（init）、其状态（sleeping）以及它属于哪个用户（Uid: 0 for root）。

除了每个单独进程的目录外，/proc 还包括包含系统状态信息的目录和文件。
