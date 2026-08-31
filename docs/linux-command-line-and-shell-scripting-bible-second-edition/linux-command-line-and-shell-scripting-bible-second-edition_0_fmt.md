
# Linux 命令行与 Shell 脚本圣经（第二版）

![](img/calibre_cover.jpg)

# 第 15 章：脚本控制

# 第 16 章：创建函数

- `SZ`：如果进程被交换，所需的近似交换空间
- `WCHAN`：进程睡眠时的内核函数地址

注意 `CMD` 列中的变化。

如你所见，Unix 和 BSD 类型的参数之间存在大量的重叠。从其中一种类型获取的大部分信息也可以从另一种类型获取。大多数情况下，你选择参数类型是取决于你更习惯的格式（例如，如果你在学习 Linux 之前习惯于 BSD 环境）。

当你使用 BSD 风格的参数时，`ps` 命令会自动更改输出以模拟 BSD 格式。这里有一个使用 `l` 参数的示例：

```
$ ps l
F  UID  PID  PPID  PRI  NI  VSZ  RSS  WCHAN  STAT TTY       TIME  COMMAND
0   500  3081  3080  20    0  4692  1432  wait    Ss    pts/0     0:00  -bash
0   500  5104  3081  20    0  4468   844  -       R+    pts/0     0:00  ps l
$
```

注意，虽然许多输出列与我们使用的 Unix 风格参数相同，但有几列是不同的：

- `VSZ`：进程在内存中的大小（单位为 KB）
- `RSS`：进程已使用但未交换出的物理内存
- `STAT`：表示当前进程状态的两个字符的状态码

许多系统管理员喜欢 BSD 风格的 `l` 参数，因为它为进程生成了更详细的状态码（`STAT` 列）。与单字符的 Unix 风格输出相比，这双字符代码能更精确地定义进程中正在发生的具体情况。

第一个字符使用的值与 Unix 风格的 `S` 输出列相同，显示进程何时处于睡眠、运行或等待状态。第二个字符进一步定义了进程的状态：

- `<`：进程以高优先级运行。
- `N`：进程以低优先级运行。
- `L`：进程有页面锁定在内存中。
- `s`：进程是一个会话首。
- `l`：进程是多线程。
- `+`：进程正在前台运行。

从之前显示的简单示例中，你可以看到 `bash` 命令正在睡眠，但它是一个会话首（它是我会话中的主进程），而 `ps` 命令在系统上是在前台运行的。

## GNU 长参数

最后，GNU 开发者通过在参数组合中添加更多选项，对新的改进型 `ps` 命令融入了他们自己的见解。某些 GNU 长参数复制了现有的 Unix 或 BSD 风格参数，而另一些则提供了新功能。表 4.3 列出了可用的 GNU 长参数。

### 表 4.3：`ps` 命令 GNU 参数

| 参数 | 说明 |
| :--- | :--- |
| `--deselect` | 显示命令行中列出的进程以外的所有进程。 |
| `--Group` `grplist` | 显示组 ID 在 `grplist` 中的进程。 |
| `--User` `userlist` | 显示用户 ID 在 `userlist` 中的进程。 |
| `--group` `grplist` | 显示有效组 ID 在 `grplist` 中的进程。 |
| `--pid` `pidlist` | 显示进程 ID 在 `pidlist` 中的进程。 |
| `--ppid` `pidlist` | 显示父进程 ID 在 `pidlist` 中的进程。 |
| `--sid` `sidlist` | 显示会话 ID 在 `sidlist` 中的进程。 |
| `--tty` `ttylist` | 显示终端设备 ID 在 `ttylist` 中的进程。 |
| `--user` `userlist` | 显示有效用户 ID 在 `userlist` 中的进程。 |
| `--format` `format` | 仅显示格式中指定的列。 |
| `--context` | 显示额外的安全信息。 |
| `--cols` `n` | 将屏幕宽度设为 `n` 列。 |
| `--columns` `n` | 将屏幕宽度设为 `n` 列。 |
| `--cumulative` | 显示累计信息。 |
| `--forest` | 以树状结构显示进程。 |
| `--headers` | 显示表头。 |
| `--no-headers` | 不显示表头。 |
| `--lines` `n` | 将行数设为 `n` 行。 |
| `--rows` `n` | 将行数设为 `n` 行。 |
| `--sort` `order` | 用于排序输出的列。 |
| `--width` `n` | 将屏幕宽度设为 `n`。 |
| `--help` | 显示帮助信息。 |
| `--info` | 显示帮助信息。 |
| `--version` | 显示版本。 |

你可以将 GNU 参数与 Unix 或 BSD 参数结合使用以真正实现自定义。长参数的一个很酷的功能是 `--forest`：

```
0   500  3081  3080  20    0  4692  1432  wait    Ss    pts/0     0:00  -bash
0   500  5104  3081  20    0  4468   844  -       R+    pts/0     0:00  ps l
```

## 实时进程监控

`ps` 命令非常适合查找频繁交换入出的进程。`top` 命令可以解决这个问题。`top` 输出是系统运行时的快照。`top` 的第一部分显示系统信息。第一行显示当前时间、系统运行时间、登录用户数以及负载。

负载显示三个数字：1 分钟、5 分钟和 15 分钟的平均负载。数值越高，系统负载越大。1 分钟负载值对于突发活动来说高并不罕见。如果 15 分钟负载值很高，你的系统可能出了问题。

Linux 系统管理的技巧在于定义到底什么是高负载值。这取决于系统正常运行的内容以及硬件配置。对于一个系统可能是正常的，对于另一个系统可能是高的。通常，如果负载平均超过 2，情况就会变得繁忙。

第二行显示进程信息（`top` 中称为 tasks）：有多少进程正在运行、睡眠、停止或僵尸。

接下来显示通用 CPU 信息。`top` 显示将 CPU 利用率分为几类，取决于进程的所有者以及进程的状态（运行、空闲或等待）。

随后，有两行详细说明系统内存状态。第一行显示物理内存状态，包括总内存、已使用和空闲。第二行内存显示系统交换区域的状态（如果已安装）。

最后，下一个部分显示当前运行进程的详细列表，包含一些与 `ps` 命令输出类似的熟悉列：

- `PID`：进程 ID
- `USER`：进程所有者的用户名
- `PR`：进程优先级
- `NI`：进程 nice 值
- `VIRT`：进程使用的总虚拟内存
- `RES`：进程使用的物理内存
- `SHR`：进程与其他进程共享的内存
- `S`：进程状态（`D`=可中断睡眠、`R`=运行、`S`=睡眠、`T`=被跟踪或停止，或 `Z`=僵尸）
- `%CPU`：进程使用的 CPU 时间百分比
- `%MEM`：进程使用的可用物理内存份额
- `TIME+`：进程自启动以来使用的总 CPU 时间
- `COMMAND`：进程的命令行名称（启动的程序）

默认情况下，当你启动 `top` 时，它会根据 `%CPU` 值对进程进行排序。你可以在 `top` 运行时使用几个交互式命令之一来更改排序顺序。每个交互式命令都是你在 `top` 运行时可以按下的单个字符，用于改变程序的行为。这些命令在表 4.4 中显示。

### 表 4.4：常用交互式命令

| 命令 | 描述 |
| :--- | :--- |
| `1` | 切换单 CPU 和对称多处理器（SMP）状态。 |
| `b` | 切换表格中重要数字的粗体显示。 |
| `I` | 切换 Irix/Solaris 模式。 |
| `z` | 配置表格颜色。 |
| `l` | 切换负载平均信息行的显示。 |
| `t` | 切换 CPU 信息行的显示。 |
| `m` | 切换 MEM 和 SWAP 信息行的显示。 |
| `f` | 添加或移除不同的信息列。 |
| `o` | 更改信息列的显示顺序。 |
| `F` 或 `O` | 选择用于进程排序的字段（默认为 `%CPU`）。 |
| `<` 或 `>` | 将排序字段向左移动（`<`）或向右移动（`>`）。 |
| `r` | 切换正常或反向排序顺序。 |
| `h` | 切换线程的显示。 |
| `c` | 切换显示进程的命令名称或完整命令行（包括参数）。 |
| `i` | 切换空闲进程的显示。 |
| `S` | 切换累积 CPU 时间或相对 CPU 时间的显示。 |
| `x` | 切换排序字段的高亮显示。 |
| `y` | 切换运行任务的高亮显示。 |
| `z` | 切换颜色和单色模式。 |
| `b` | 切换 x 和 y 模式的粗体模式。 |
| `u` | 显示特定用户的进程。 |
| `n` 或 `#` | 设置要显示的进程数量。 |
| `k` | 杀死特定进程（仅限进程所有者或 root 用户）。 |
| `r` | 更改特定进程的优先级（`renice`）（仅限进程所有者或 root 用户）。 |
| `d` 或 `s` | 更改更新间隔（默认为三秒）。 |
| `W` | 将当前设置写入配置文件。 |
| `q` | 退出 `top` 命令。 |

## 停止进程

作为一名系统管理员，至关重要的一点是知道何时以及如何停止进程。有时进程会挂起，只需要轻轻“推”一下就能重新运行或停止。其他时候，进程会过度占用 CPU 并拒绝放弃。在这两种情况下，你都需要一个允许你控制进程的命令。Linux 遵循 Unix 的进程间通信方法。

在 Linux 中，进程之间通过信号（signals）进行通信。进程信号是一种预定义的消息，进程可以识别它并可能选择忽略或处理。开发者通过编程来控制进程如何处理信号。大多数编写良好的应用程序都具有接收并处理标准 Unix 进程信号的能力。这些信号在表 4.5 中显示。

### 表 4.5：Linux 进程信号

| 信号 | 名称 | 描述 |
| :--- | :--- | :--- |
| 1 | `HUP` | 挂断。 |
| 2 | `INT` | 中断。 |
| 3 | `QUIT` | 停止运行。 |
| 9 | `KILL` | 无条件终止。 |
| 11 | `SEGV` | 段错误。 |
| 15 | `TERM` | 在可能的情况下终止。 |
| 17 | `STOP` | 无条件停止，但不终止。 |
| 18 | `TSTP` | 停止或暂停，但在后台继续运行。 |
| 19 | `CONT` | 在 `STOP` 或 `TSTP` 后恢复执行。 |

Linux 中有两个命令允许你向运行中的进程发送进程信号。

### `kill` 命令

`kill` 命令允许你根据进程 ID（PID）向进程发送信号。默认情况下，`kill` 命令向命令行列出的所有 PID 发送 `TERM` 信号。遗憾的是，你只能使用进程 PID 而不是命令名称，这使得 `kill` 命令有时难以使用。

发送进程信号要求你必须是该进程的所有者，或者以 root 用户身份登录。

```
$ kill 3940
-bash: kill: (3940) - Operation not permitted
$
```

`TERM` 信号告诉进程请停止运行。遗憾的是，如果你有一个失控的进程，它很可能会忽略该请求。当你需要强制执行时，`-s` 参数允许你指定其他信号（使用名称或信号数字）。

通常接受的程序是先尝试 `TERM` 信号。如果进程忽略了它，则尝试 `INT` 或 `HUP` 信号。如果程序识别这些信号，它将尝试在关闭之前优雅地停止正在执行的操作。最强制的信号是 `KILL` 信号。当进程接收到信号时，它会立即停止。这可能会导致文件损坏。

正如以下示例所示，`kill` 命令没有相关的输出。

```
### kill -s HUP 3940
#
```

要查看命令是否有效，你必须执行另一个 `ps` 或 `top` 命令来查看问题进程是否停止。

### `killall` 命令

`killall` 命令是一种通过名称而非 PID 数字来停止进程的强大方法。`killall` 命令还允许你使用通配符字符，当系统出现故障时，它是一个非常有帮助的工具：

```
### killall http*
#
```

此示例将杀死所有以 `http` 开头的进程，例如 Apache Web 服务器的 `httpd` 服务。

> **注意**
>
> 以 root 用户身份登录时，使用 `killall` 命令要极其小心。很容易在使用通配符字符时意外停止重要的系统进程。这可能导致文件系统损坏。

## 监控磁盘空间

系统管理员的另一项重要任务是跟踪系统的磁盘使用情况。无论你运行的是简单的 Linux 桌面还是大型 Linux 服务器，你都需要知道为应用程序留了多少空间。

你可以使用一些命令行工具来帮助管理 Linux 系统上的介质环境。本节描述了你在执行系统管理职责期间可能会遇到的核心命令。

### 挂载介质

如第 3 章所述，Linux 文件系统将所有介质磁盘合并到一个虚拟目录中。在系统上使用新的介质磁盘之前，你需要将其放置在虚拟目录中。这项被称为挂载（mounting）。

在当今的光源桌面世界中，大多数 Linux 发行版都有自动挂载特定类型可移除介质的能力。可移除介质设备是指（显然）可以从 PC 移除的介质，例如光驱、软盘和 USB 闪存。

如果你使用的自动挂载和卸载可移除介质的发行版，你需要手动操作。本节描述了帮助你管理可移除介质设备的 Linux 命令行。

### `mount` 命令

奇怪的是，挂载介质的命令叫做 `mount`。默认情况下，`mount` 命令显示当前系统中挂载的介质设备列表：

```
$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type bfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/sdb1 on /media/disk type vfat
(rw,nosuid,nodev,uhelper=hal,shortname=lower,uid=503)
$
```

`mount` 命令提供了四项信息：

- 媒体设备的设备文件名
- 媒体挂载到虚拟目录的挂载点
- 文件系统类型
- 挂载媒体的访问状态

上一个示例中的最后一条是一个 USB 优存盘，GNOME 桌面自动将其挂载在 `/media/disk` 挂载点。`vfat` 文件系统类型显示它是在微软 Windows 电脑上格式化的。

要在虚拟目录中手动挂载媒体设备，你需要以 root 用户身份登录。以下是手动挂载媒体设备的基本命令：

```bash
mount -t type device directory
```

`type` 参数定义了磁盘格式化时所使用的文件系统类型。Linux 识别许多不同的文件系统类型。如果你与 Windows PC 共享可移动媒体设备，你最可能会遇到的类型有：

- `vfat`：Windows 长文件名文件系统。
- `ntfs`：用于 Windows NT、XP 和 Vista 的 Windows 高级文件系统。
- `iso9660`：标准 CD-ROM 文件系统。

大多数 USB 优存盘和软盘都使用 `vfat` 文件系统格式化。如果你需要挂载数据 CD，必须使用 `iso9660` 文件系统类型。

接下来两个参数定义了媒体设备设备文件的位置以及虚拟目录中挂载点的位置。例如，要手动将设备 `/dev/sdb1` 的 USB 优存盘挂载到位置 `/media/disk`，你会使用以下命令：

```bash
mount -t vfat /dev/sdb1 /media/disk
```

一旦媒体设备挂载到虚拟目录，root 用户将拥有该设备的完全权限，但其他用户的访问将受到限制。你可以使用目录权限（第 6 章讨论）来控制谁可以访问设备。

如果你需要使用 `mount` 命令的一些更高级的功能，可用参数见表 4.6。

### 表 4.6：`mount` 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `-a` | 挂载 `/etc/fstab` 文件中指定的所有文件系统。 |
| `-f` | 使 `mount` 命令模拟挂载设备，但不实际挂载。 |
| `-F` | 与 `-a` 参数配合使用时，同时挂载所有文件系统。 |
| `-v` | 详细模式，解释挂载设备所需的所有步骤。 |
| `-I` | 不使用 `/sbin/mount.filesystem` 下任何文件系统辅助文件。 |
| `-l` | 为 `ext2`、`ext3` 或 `XFS` 文件系统自动添加文件系统标签。 |
| `-n` | 挂载设备不在 `/etc/mstab` 挂载设备文件中注册。 |
| `-p` `num` | 用于加密挂载，从文件描述符 `num` 读取密码。 |
| `-s` | 忽略文件系统不支持的挂载选项。 |
| `-r` | 以只读模式挂载设备。 |
| `-w` | 以读写模式挂载设备（默认）。 |
| `-L` `label` | 使用指定的 `label` 挂载设备。 |
| `-U` `uuid` | 使用指定的 `uuid` 挂载设备。 |
| `-O` | 与 `-a` 参数配合使用时，限制应用的文件系统集。 |



| `-o` | 为文件系统添加特定选项。 |

`-o` 选项允许你使用逗号分隔的附加选项列表来挂载文件系统。常用的选项有：

* `ro`: 以只读模式挂载。
* `rw`: 以读写模式挂载。
* `user`: 允许普通用户挂载文件系统。
* `check=none`: 在不进行完整性检查的情况下挂载文件系统。
* `loop`: 挂载一个文件。

如今 Linux 中很流行的做法是将 CD 分发为 `.iso` 文件。`.iso` 文件是 CD 在单个文件中的完整镜像。大多数 CD 刻录软件软件包都可以根据 `.iso` 文件创建新 CD。`mount` 命令的一个功能是你可以直接将 `.iso` 文件挂载到你的 Linux 虚拟目录，而无需将其刻录到 CD。这是通过带有 `loop` 选项的 `-o` 参数实现的：

```bash
$ mkdir mnt
$ su
Password:
## mount -t iso9660 -o loop MEPIS-KDE4-LIVE-DVD_32.iso mnt
## ls -l mnt
total 16
-r--r--r-- 1 root root 702 2007-08-03 08:49 about
dr-xr-xr-x 3 root root 2048 2007-07-29 14:30 boot
-r--r--r-- 1 root root 2048 2007-08-09 22:36 boot.catalog
-r--r--r-- 1 root root 894 2004-01-23 13:22 cdrom.ico
-r--r--r-- 1 root root 5229 2006-07-07 18:07 MCWL
dr-xr-xr-x 2 root root 2048 2007-08-09 22:32 mespis
dr-xr-xr-x 2 root root 2048 2007-04-23 16:44 OSX
-r--r--r-- 1 root root 107 2007-08-09 22:36 version
## cd mnt/boot
## ls -l
total 4399
dr-xr-xr-x 2 root root 2048 2007-06-29 09:00 grub
-r--r--r-- 1 root root 239212 2007-07-29 12:53 initrd.gz
-r--r--r-- 1 root root 94760 2007-06-14 14:56 memtest
-r--r--r-- 1 root root 14704 2007-07-29 14:26 vmlinuz
```

`mount` 命令挂载 `.iso` CD 文件就像它是一个真正的 CD 一样，并允许我们在其文件系统中进行操作。

### umount 命令

要移除可移动设备，你不应该直接将其从系统中移除。相反，你应该总是先卸载它。

> 提示：Linux 不允许你弹出已挂载的 CD。如果你在从驱动器中弹出 CD 时遇到困难，很可能是 CD 仍然挂载在虚拟目录中。先卸载它，然后再尝试弹出。

用于卸载设备的命令是 `umount`（是的，命令里没有 "n"，这很让人混淆）。`umount` 命令的格式非常简单：`umount [directory|device]`。`umount` 命令允许你通过设备位置或挂载目录来定义媒体设备。如果有任何程序在设备上打开了文件，系统将不允许你卸载。

```bash
[root@testbox mnt]# umount /home/rich/mnt
umount: /home/rich/mnt: busy
umount: /home/rich/mnt: busy
[root@testbox mnt]# cd /home/rich
[root@testbox rich]# umount /home/rich/mnt
[root@testbox rich]# ls -l mnt
total 0
[root@testbox rich]#
```

在这个示例中，命令提示符仍在一个目录中，因此 `umount` 命令无法卸载该镜像文件。一旦命令提示符离开镜像文件，`umount` 命令就能卸载该镜像文件了。

### 使用 df 命令

有时你需要查看单个设备上有多少可用磁盘空间。`df` 命令允许你轻松地查看所有挂载磁盘的状况：

```bash
$ df
```

| Filesystem | 1K-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda2 | 18251068 | 7703964 | 9605024 | 45% | / |
| /dev/sda1 | 101086 | 18680 | 77187 | 20% | /boot |
| tmpfs | 119536 | 0 | 119536 | 0% | /dev/shm |
| /dev/sdb1 | 127462 | 11392 | 13570 | 90% | /media/disk |

```
$
```

`df` 命令显示包含数据的挂载文件系统。正如之前从 `mount` 命令所示，某些挂载设备用于内部系统目的。该命令显示：

* 设备位置
* 它能容纳多少 1024 字节块的数据
* 使用了多少 1024 字节块
* 可用多少 1024 字节块
* 使用空间的百分比
* 设备挂载点

`df` 命令有许多不同的命令行参数可用，但大多数你永远用不到。一个流行的参数是 `-h`，它以人类易读的格式显示磁盘空间，通常为 M（兆字节）或 G（吉字节）：

```bash
$ df -h
```

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sdb2 | 18G | 7.4G | 9.2G | 45% | / |
| /dev/sda1 | 99M | 19M | 76M | 20% | /boot |
| tmpfs | 119M | 0 | 119M | 0% | /dev/shm |
| /dev/sdb1 | 124G | 113G | 13G | 90% | /media/disk |

```bash
$ df -h
```

现在，你不再需要解码那些丑陋的块数字，所有的磁盘大小都用“正常”单位显示出来。`df` 命令在排查系统磁盘空间问题时价值极高。

> 注意
> > 请记住，Linux 系统始终有后台运行的进程在处理文件。`df` 命令的值反映了 Linux 系统在时间点认为的当前值。你可能有一个运行的进程创建或删除了文件，但尚未释放该文件。该值不会包含在可用空间的计算中。

## 使用 du 命令

通过 `df` 命令，可以很容易看到磁盘何时耗尽空间。对于系统管理员来说，下一个问题是知道当这种情况发生时该做什么。

另一个可以帮助你的有用命令是 `du` 命令。`du` 命令显示特定目录（默认是当前目录）的磁盘占用情况。这是判断系统上是否存在明显的磁盘大户的快速方法。

默认情况下，`du` 命令显示当前目录下的所有文件、目录和子目录，并显示每个文件或目录占用的磁盘块数。对于标准大小的目录，列表可能会非常长。以下是使用 `du` 命令的部分列表：

```bash
$ du
484     ./.gstreamer-0.10
8       ./Templates
8       ./Download
8       ./.ccache/7/0
24      ./.ccache/7
368     ./.ccache/a/d
384     ./.ccache/a
424     ./.ccache
8       ./Public
8       ./.gphpedit/plugins
32      ./.gphpedit
72      ./.gconfd
128     ./.nautilus/metafiles
384     ./.nautilus
72      ./.bittorrent/data/metainfo
20      ./.bittorrent/data/resume
144     ./.bittorrent/data
152     ./.bittorrent
8       ./Videos
8       ./Music
16      ./.config/gtk-2.0
40      ./.config
8       ./Documents
```

每行右侧的数字是每个文件或目录占用的磁盘块数。注意列表是从目录的底部开始，向上遍历该目录内包含的文件和子目录。

`du` 命令本身可能没什么用处。能看到每个单独的文件和目录占用多少磁盘空间是很好，但当你必须翻阅好几页的信息才能找到要找的内容时，它可能就毫无意义了。

你可以配合 `du` 命令使用几个命令行参数来让结果更具可读性：

* `-c`: 生成所有列出文件的总计和。
* `-h`: 以人类可读的格式打印大小，使用 `K` 表示字节，`M` 表示兆字节，`G` 表示千字节。
* `-s`: 对每个参数进行汇总。

系统管理员的下一步是使用一些文件处理命令来操作大量数据。这正是下一节涵盖的内容。

## 处理数据文件

当你有大量数据时，通常很难处理这些信息并使其变得有用。正如你在上一节中通过 `du` 命令看到的，在处理系统命令时，很容易产生数据过载。

Linux 系统提供了若干命令行工具来帮助你管理大量数据。本节涵盖了每个系统管理员——以及任何日常 Linux 用户——应该学会如何使用的基本命令，以便他们的生活更轻松。

### 排序数据

在处理大量数据时，一个非常实用的函数是 `sort` 命令。`sort` 命令顾如其名——排序数据。

默认情况下，`sort` 命令使用你为会话指定的语言的标准排序规则对文本文件中的数据行进行排序。

```bash
$ cat file1
one
two
three
four
five
$ sort file1
five
four
one
three
two
$
```

非常简单。然而，事情并不总是像看起来那么简单。看这个例子：

```bash
$ cat file2
1
2
100
45
3
10
$ sort file2
1
2
100
45
3
10
```

等等，上面的示例显示的是标准的字符串排序。让我们看看数值排序：

```bash
$ cat file2
1
2
100
45
3
10
$ sort -n file2
1
2
3
10
45
100
```

如果你期望数字按数值排序，那么你可能会失望。要解决这个问题，请使用 `-n` 参数。按逆序排序：

```bash
$ sort -rn file2
100
45
10
3
2
1
```

## sort 参数

| 单横线 | 双横线 | 描述 |
| :--- | :--- | :--- |
| `-b` | | 排序时忽略空行。 |
| `-C` | | 检查输入是否已经排序。 |
| `-c` | | 如果未排序则报告。 |
| `-d` | | 仅考虑字符进行排序。 |
| `-f` | | 忽略大小写。 |
| `-g` | | 通用数值排序。 |
| `-i` | | 忽略不可打印字符。 |
| `-k` | `--key=POS1[,POS2]` | 基于 `POS1` 排序，并在 `POS2` 结束。 |
| `-M` | | 按三字符名称的顺序排序。 |
| `-m` | | 合并两个已排序的数据文件。 |
| `-n` | | 按数值排序。 |
| `-o` | `-output=file` | 将结果写入指定的文件。 |
| `-R` | | 按键的随机哈希排序。 |
| | `--random-source=FILE` | 指定用于 `-R` 参数的随机字节的文件。 |
| `-r` | | 反转排序顺序（降序而非升序）。 |
| `-S` | `--buffer-size=SIZE` | 指定使用的内存量。 |
| `-s` | | 禁用最后的比较。 |
| `-T` | `--temporary-direction=DIR` | 指定存储临时工作文件的位置。 |
| `-t` | `--field-separator=SEP` | 指定用于区分键位置的字符。 |
| `-u` | `--unique` | 配合 `-c` 参数时，检查严格排序；无 `-c` 参数时，仅输出两个相似行中的第一次出现。 |
| `-z` | `--zero-terminated` | 使用 NULL 字符结束所有行而不是换行符。 |

`-k` 和 `-t` 参数在排序使用字段的数据（例如 `/etc/passwd` 文件）时非常方便。使用 `-t` 参数指定字段分隔符字符，使用 `-k` 参数指定根据哪个字段进行排序。例如，要根据数值 userid 对密码文件进行排序，只需这样做：

```bash
$ sort -t ':' -k 3 -n /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/etc/news:
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
```

现在数据已根据第三字段（即数值用户 ID uid 值）进行了完美排序。

`-n` 参数非常适合对数值输出排序，例如 `du` 命令的输出：

```bash
$ du -sh * | sort -nr
1008k   mrtg-2.9.29.tar.gz
972k    bldg1
888k    fbs2.pdf
760k    Printtest
680k    rsync-2.6.6.tar.gz
660k    code
516k    fig1001.tiff
496k    test
496k    php-common-4.0.4pl1-6mdk.i586.rpm
448k    MesaGLUT-6.5.1.tar.gz
400k    plp
```

注意，`-r` 选项也会按降序排列值，因此你可以轻松地看到目录中哪些文件占用了最大的空间。

> 注意
> 本示例中使用的管道命令 (|) 将 `du` 命令的输出重定向到 `sort` 命令。这将在第 10 章进行更详细的讨论。

### 搜索数据

在大文件中，你通常需要查找隐藏在文件中间的某行特定数据。与其手动滚动整个文件，不如让 `grep` 命令为你搜索。`grep` 命令的命令行格式为：

```bash
grep [options] pattern [file]
```

`grep` 命令在输入或你指定的文件中搜索包含匹配指定模式（pattern）字符的行。`grep` 的输出是包含匹配模式的行。

以下是使用“排序数据”部分中的 `file1` 文件使用 `grep` 命令的两个简单示例：

```bash
$ grep three file1
three
$ grep t file1
two
three
$
```

第一个示例在 `file1` 文件中搜索匹配模式 `three` 的文本。`grep` 命令产生包含匹配模式的行。下一个示例在 `file1` 文件中搜索匹配模式 `t` 的文本。在这种情况下，有行匹配指定的模式，并且它们都显示了出来。

由于 `grep` 命令非常流行，它在其生命周期内经历了许多开发变化。`grep` 命令中添加了许多功能。如果你查看 `grep` 命令的帮助页（man pages），你将会发现它是多功能强大。

如果你想反向搜索（输出不匹配模式的行），请使用 `-v` 参数：

```bash
$ grep -v t file1
one
four
five
$
```

如果你需要找到匹配模式所处的行号，请使用 `-n` 参数：

```bash
$ grep -n t file1
2:two
3:three
$
```

如果你只需要查看包含匹配模式的行数，请使用 `-c` 参数：

```bash
$ grep -c t file1
2
$
```

如果你需要指定多个匹配模式，请使用 `-e` 参数指定每个单独的模式：

```bash
$ grep -e t -e f file1
two
three
four
five
$
```

此示例输出了包含字符串 `t` 或字符串 `f` 的行。

默认情况下，`grep` 命令使用基础的 Unix 风格正则表达式来匹配模式。Unix 风格正则表达式使用特殊字符来定义如何查找匹配模式。

有关正则表达式的更详细解释，请参阅第 19 章。

这里有一个在 grep 搜索中使用正则表达式的简单示例：



### `grep` 与方括号

```bash
$ grep [tf] file1

two

three

four

five

$
```

正则表达式中的方括号表示 `grep` 应该查找包含 `t` 或 `f` 字符的匹配项。如果没有方括号，正则表达式将查找字符串 `tf`。

`egrep` 是 `grep` 的衍生版本，允许使用扩展正则表达式。

### `bzip2` 工具

`bzip2` 软件包较新，但它正在变得流行。`bzip2` 工具包括：

*   `bzip2` 用于压缩文件
*   `bzcat` 用于显示压缩文件的内容
*   `bunzip2` 用于解文件
*   `bzip2recover` 用于尝试恢复损坏的文件

默认情况下，`bzip2` 命令会压缩原始文件并将其替换为 `.bz2` 扩展，这表明我们使用了什么压缩技术来压缩它。

```bash
$ bzip2 myprog

$ ls -l myprog

-rw-r--r-- 1 root root 2378 Oct 25 12:00 myprog.bz2
```

等待，`myprog` 的原始大小为 4882 字节，经过 `bzip2` 压缩后现在是 2378 字节。此外，注意 `bzip2` 命令自动将原始文件重命名为 `.bz2` 扩展。

要解压缩文件，只需使用 `bunzip2` 命令：

```bash
$ bunzip2 myprog.bz2

$ ls -l myprog

-rw-r--r-- 1 root root 4882 Oct 25 12:00 myprog
```

如你所示，解压缩后的文件恢复到了原始大小。一旦压缩了文本文件，你就无法使用标准的 `cat`、`more` 或 `less` 命令查看数据。相反，你需要使用 `bzcat` 命令：

```bash
$ bzcat test.bz2

This is a test text file.

The quick brown fox jumps over the lazy dog.

This is the end of the test file.
```

`bzcat` 命令在不解压缩实际文件的情况下显示压缩文件内部的文本。

### `gzip` 工具

到目前为止，Linux 中最流行的文件压缩工具是 `gzip` 工具。`gzip` 软件包是 GNU 项目的产，目的是尝试创建原始 Unix `compress` 工具的免费版本。该软件包包含以下文件：

*   `gzip` 用于压缩文件
*   `gzcat` 用于显示压缩文本文件的内容
*   `gunzip` 用于解压缩文件

这些工具的工作方式与 `bzip2` 工具相同：

```bash
$ gzip myprog

$ ls -l my*

-rwxrwxr-x 1 rich rich 2197 2007-09-13 11:29 myprog.gz
```

`gzip` 命令用于压缩你在命令行上指定的文件。你也可以指定多个文件名，甚至使用通配符来同时压缩多个文件：

```bash
$ gzip my*

$ ls -l my*

-rwxr--r--    1 rich      rich           103 Sep  6 13:43 myprog.c.gz
-rwxr-xr-x    1 rich      rich          5178 Sep  6 13:43 myprog.gz
-rwxr--r--    1 rich      rich            59 Sep  6 13:46 myscript.gz
-rwxr--r--    1 rich      rich            60 Sep  6 13:44 myscript.gz
```

`gzip` 命令会压缩目录中匹配通配符模式的所有文件。

### `zip` 工具

`zip` 工具与 Phil Katz 为 MS-DOS 和 Windows 创建的流行的 PKZIP 软件包兼容。Linux `zip` 软件包中包含四个工具：

*   `zip` 创建一个包含所列文件和目录的压缩文件。
*   `zipcloak` 创建一个包含所列文件和目录的加密压缩文件。
*   `zipnote` 从 zip 文件中提取注释。
*   `zipsplit` 将一个 zip 文件分割成一组指定大小的较小文件（用于将大型 zip 文件拷贝到软磁盘上）。
*   `unzip` 从压缩的 zip 文件中提取文件和目录。

要查看 `zip` 工具的所有可用选项，只需在命令行中单独输入它即可：

```bash
$ zip
Copyright (C) 1990-2005 Info-ZIP
Type ‘zip "-L”’ for software license.
Zip 2.31 (March 8th 2005). Usage:
zip [-options] [-b path] [-t mmddyyyy] [-n suffixes] [zipfile list]
[-xi list]
   默认默认操作是从 list 中添加或替换 zipfile 条目，
   这可以包括特殊名称 - 来压缩标准输入。
   如果省略 zipfile 和 list，zip 将将 stdin 压缩到 stdout。

  -f freshen: only changed files  -u update: only changed or new files
  -d delete entries in zipfile    -m move into zipfile (delete files)
  -r recurse into directories      -j junk directory names
  -0 store only                   -l convert LF to CR LF
  -1 compress faster              -9 compress better
  -q quiet operation              -v verbose operation
  -c add one-line comments        -z add zipfile comment
  -@ read names from stdin        -o make file as old as latest entry
  -x exclude the following names  -i include only the following names
  -F fix zipfile (-FF try harder) -D do not add directory entries
  -A adjust self-extracting exe   -J junk zipfile prefix (unzipsfx)
  -T test zipfile integrity       -X exclude file attributes
  -y store symbolic links as the link instead of the referenced file
  -R PKZIP recursion (see manual)-e encrypt -n don't compress these suffixes
```

`zip` 工具的强大之处在于能够将整个目录的文件压缩成单个压缩文件。这使其成为归档目录结构的理想选择：

```bash
$ zip -r test test
```

此示例创建一个名为 `test.zip` 的 zip 文件，并递归遍历 `test` 目录，将找到每个文件和目录添加到 zip 文件中。注意输出，并不是 zip 文件中存储的所有文件都能被压缩。

> 注意：当你使用 `zip` 命令的递归功能时，文件存储在 zip 文件中的相同目录中。子目录中的文件将存储在 zip 文件中相同的子目录内。在提取文件时必须小心；`unzip` 命令将在新位置重建整个目录结构。当你有大量的子目录和文件时，这有时会令人困惑。

### 归档数据

虽然 `zip` 命令在将数据压缩并归档到单个文件中方面表现出色，但它不是 Unix 和 Linux 世界使用的标准工具。到目前为止，Unix 和 Linux 中最流行的归档工具是 `tar` 命令。`tar` 命令最初用于将文件写入带设备进行归档。然而，它也可以将输出写入文件，这已成为 Linux 中归档数据的流行方式。

以下是 `tar` 命令的格式：

```bash
tar function [options] object1 object2
```

`function` 参数定义了 `tar` 命令应该执行。

### `tar` 命令函数

| 函数 | 长名称 | 说明 |
| :--- | :--- | :--- |
| `-A` | `--concatenate` | 将现有归档文件合并到另一个现有 tar 归档文件中。 |
| `-c` | `--create` | 创建一个新的 tar 归档文件。 |
| `-d` | `--diff` |  tar 归档文件与文件系统的差异。 |
| `--delete` | 从现有归档文件中删除。 |
| `-r` | `--append` | 将文件添加到现有归档文件的末尾。 |
| `-t` | `--list` | 列出现有归档文件的内容。 |
| `-u` | `--update` | 将比现有归档同名文件更新的文件添加到现有归档文件中。 |
| `-x` | `--extract` | 从现有归档文件中提取文件。 |

每个函数使用选项来定义 `tar` 归档文件的特定行为。

### `tar` 命令选项

| 选项 |  |
| :--- | :--- |
| `-C` `dir` | 切换到指定的目录。 |
| `-f` `file` | 输出结果到文件（或设备）`file`。 |
| `-j` | 将输出重定向到 `bzip2` 命令进行压缩。 |
| `-p` | 保留所有文件权限。 |
| `-v` | 处理时列出文件。 |
| `-z` | 将输出重定向到 `gzip` 命令进行压缩。 |

这些选项通常组合在一起创建以下场景。首先，你想使用此命令创建一个归档文件：

```bash
tar -cvf test.tar test/ test2/
```

上述命令创建一个名为 `test.tar` 的归档文件，包含 `test` 目录和 `test2` 目录的内容。接下来，使用此命令：

```bash
tar -tf test.tar
```

列出（但不提取）tar 文件 `test.tar` 的内容。最后，使用此命令：

```bash
tar -xvf test.tar
```

提取 tar 文件 `test.tar` 的内容。如果 tar 文件是从目录结构创建的，则从当前目录开始重建整个目录结构。

如你所见，使用 `tar` 命令是创建整个目录结构归档文件的简单方法。这是 Linux 世界分发开源源代码的常用方法。

> 提示：如果你下载开源软件，通常会看到以 `.tgz` 结尾的文件。这些是 gzipped tar 文件，可以使用命令 `tar -zxvf` `filename.tgz` 进行提取。

### 总结

本章讨论了 Linux 系统管理员和程序员使用的一些更高级的 bash 命令。`ps` 和 `top` 命令对于确定系统状态至关重要，允许你看到哪些应用程序正在运行以及它们消耗多少资源。

在可移动介质盛行的今天，系统管理员的另一个热门话题是挂载存储设备。`mount` 命令允许你将物理存储设备挂载到 Linux 虚拟目录结构中。要移除该设备，请使用 `umount` 命令。

最后，本章讨论了用于处理数据的各种实用工具。`sort` 工具可以轻松地排序大型数据文件，帮助你组织数据，而 `grep` 工具则允许你快速扫描大型数据文件以查找特定信息。Linux 中提供了不同的文件压缩工具，包括 `bzip2`、`gzip` 和 `zip`。每种工具都允许你压缩大文件以帮助节省文件系统空间。Linux 的 `tar` 工具是一种将目录结构归档为单个文件的流行方法，该文件可以轻松地迁移到另一个系统。

下一章将讨论 Linux 环境变量。环境变量允许你从脚本访问系统信息，并为在脚本中存储数据提供了一种方便的方法。

## 第 5 章：使用 Linux 环境变量

### 本章内容

- 什么是环境变量？
- 设置环境变量
- 删除环境变量
- 默认 shell 环境变量
- 设置 `PATH` 环境变量
- 定位系统环境变量
- 变量数组
- 使用命令别名

Linux 环境变量有助于定义你的 Linux shell 体验。然而，对于新的 Linux 用户来说，这可能是一个令人困惑的话题。许多程序和脚本使用环境变量获取系统信息并存储临时数据和配置信息。Linux 系统中有许多设置环境变量的地方，了解这些位置至关重要。本章将带你进入 Linux 环境变量的世界，展示它们在哪里、如何使用它们，甚至如何创建你自己的环境变量。本章将以一个相关主题结束，即在 shell 会话中定义和使用别名。

### 什么是环境变量？

bash shell 使用了一种名为环境变量的特性来存储有关 shell 会话和工作环境的信息（因此得名环境变量）。该特性还允许你在内存中存储数据，任何从 shell 运行的程序或脚本都可以轻松访问。这是一种存储标识用户账户、系统、shell 或任何你需要存储的特征的持久数据的方便方法。

bash shell 中有两种类型的环境变量：

- 全局变量
- 局部变量

本节描述了每种环境变量，并展示了如何查看和使用它们。

> 注意
> 尽管 bash shell 使用的是特定的且一致的环境，但不同的 Linux 发行版通常会添加自己的环境变量。在本章中看到的环境变量示例可能与你特定发行版中提供的变量略有不同。如果你遇到了此处未涵盖的环境变量，请检查你的 Linux 发行版的文档。

### 全局环境变量

全局环境变量在 shell 会话中以及 shell 启动的任何子进程中均可见。局部变量仅在创建它的 shell 中可用。这使得全局环境变量在需要来自父进程信息的子进程应用程序中非常有用。

Linux 系统在你启动 bash 会话时会设置几个全局环境变量（有关那时启动了哪些变量的细节，请参见本章后面的“定位系统环境变量”部分）。系统环境变量始终使用大写字母，以区别于普通用户环境变量。

要查看全局环境变量，请使用 `printenv` 命令：

```bash
$ printenv

ORBIT_SOCKETDIR=/tmp/orbit-user
HOSTNAME=localhost.localdomain
IMSETTINGS_INTEGRATE_DESKTOP=yes
TERM=xterm
SHELL=/bin/bash
XDG_SESSION_COOKIE=787b3cf537971ef8462260960000006b-1284670942.440386-1012435051
HISTSIZE=1000
GTK_RC_FILES=/etc/gtk/gtkrc:/home/user/.gtkrc-1.2-gnome2
WINDOWID=29360131
GNOME_KEYRING_CONTROL=/tmp/keyring-Egjauk
IMSETTINGS_MODULE=none
USER=user
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:
bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43
...
SSH_AUTH_SOCK=/tmp/keyring-Egjauk/ssh
SESSION_MANAGER=local/unix:@/tmp/.ICE-unix/1331,unix/unix:/tmp/.ICE-unix/1331
USERNAME=user
DESKTOP_SESSION=gnome
MAIL=/var/spool/mail/user
PATH=/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:
/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin
QT_IM_MODULE=xim
PWD=/home/user/Documents
XMODIFIERS=@im=none
GDM_KEYBOARD_LAYOUT=us
LANG=en_US
IMSETTINGS_INTEGRATE_DESKTOP=yes
TERM=xterm
SHELL=/bin/bash
USER=user
...
```

### 局部环境变量

局部变量仅在创建它的 shell 中可用。这使得全局环境变量在需要来自父进程信息的子进程应用程序中非常有用。

```bash
HISTFILE=/home/user/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/home/user
HOSTNAME=localhost.localdomain
HOSTTYPE=i386
IFS=$'\t\n'
IMSETTINGS_INTEGRATE_DESKTOP=yes
IMSETTINGS_MODULE=none
LANG=en_US.utf8
LESSOPEN='|/usr/bin/lesspipe.sh %s'
LINES=24
LOGNAME=user
LS_COLORS='rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43...'
```



`MACHTYPE=i386-redhat-linux-gnu`

`MAIL=/var/spool/mail/user`

`MAILCHECK=60`

`OLDPWD=/home/user`

`OPTERR=1`

`OPTIND=1`

`ORBIT_SOCKETDIR=/tmp/orbit-user`

`OSTYPE=linux-gnu`

`PATH=/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin`

`PIPESTATUS=([0]="0")`

`PPID=1674`

`PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME%%.*}:${PWD/#$HOME/~}";}"; echo -ne "\007"'`

`PS1='[\u@\h \W]\$ '`

`PS2='> '`

`PS4='+ '`

`PWD=/home/user/Documents`

`QT_IM_MODULE=xim`

`SESSION_MANAGER=local/unix:@/tmp/.ICE-unix/1331,unix/unix:/tmp/.ICE-unix/1331`

`SHELL=/bin/bash`

`SHELLOPTS=braceexpand:emacs:hashall:histexpand:history:interactive-comments:monitor`

`SHLVL=2`

`SSH_ASKPASS=/usr/libexec/openssh/gnome-ssh-askpass`

`SSH_AUTH_SOCK=/tmp/keyring-Egjauk/ssh`

`TERM=xterm`

`UID=500`

`USER=user`

`USERNAME=user`

`WINDOWID=29360131`

`WINDOWPATH=1`

`XAUTHORITY=/var/run/gdm/auth-for-user-GIU7sE/database`

`XDG_SESSION_COOKIE=787b3cf537971ef8462260960000006b-1284670942.440386-1012435051`

`XMODIFIERS=@im=none`

`_=printenv`

`colors=/etc/DIR_COLORS`

```bash
__udisks ()
{
    local IFS='';
    local cur="${COMP_WORDS[COMP_CWORD]}"

    if [ "${COMP_WORDS[$(($COMP_CWORD - 1))]}" = "--show-info" ]; then
        COMPREPLY=($(compgen -W "$(udisks --enumerate-device-files)" -- $cur));
    else
        if [ "${COMP_WORDS[$(($COMP_CWORD - 1))]}" = "--inhibit-polling" ]; then
            ...
        fi;
    fi;
    fi
}
```

```bash
command_not_found_handle ()
{
    runcnf=1;
    retval=127;
    [ ! -S /var/run/dbus/system_bus_socket ] && runcnf=0;
    [ ! -x /usr/sbin/packagekitd ] && runcnf=0;

    if [ $runcnf -eq 1 ]; then
        /usr/libexec/pk-command-not-found $1;
        retval=$?;
    else
        echo "bash: $1: command not found";
    fi;

    return $retval
}
```

你会发现，通过`printenv`命令看到的所有全局环境变量出现在`set`命令的输出中。然而，现在又出现了许多额外的环境变量。这些是本地环境变量。

## 设置环境变量

你可以直接从`bash` shell 设置你自己的环境变量。本节将向你展示如何创建自己的环境变量，并从交互式 shell 或 shell 脚本中引用它们。

## 设置本地环境变量

一旦启动了`bash` shell（或启动了 shell 脚本），你就可以创建在 shell 进程中可见的局部变量。你可以通过等号将变量赋值为值，从而为环境变量分配数值或字符串值：

```bash
$ test=testing

$ echo $test

testing
```

这很简单！现在，每当你需要引用`test`环境变量的值时，只需通过名称`$test`进行引用即可。

如果你需要引用`test`环境变量的值，只需通过名称`$test`进行引用即可。

```bash
$ test=testing

$ echo $test

testing
```

如果你需要引用`test`环境变量的值，只需通过名称`$test`进行引用即可。

```bash
$ test=testing

$ echo $test

testing
```

如果你需要引用`test`环境变量的值，只需通过名称`$test`进行引用即可。

```bash
$ test=testing

$ echo $test

testing
```

`bash` shell 默认使用某些特定的环境变量来定义系统环境。你可以始终认为这些变量在你的 Linux 系统上已经设置好了。由于`bash` shell 是原始 Unix Bourne shell 的派生版本，它也包含了最初在那个 shell 中定义的环境变量。

表 5.1 显示了`bash` shell 与原始 Unix Bourne shell 兼容的环境变量。

### bash Shell Bourne 变量

| 变量 | 说明 |
| :--- | :--- |
| `CDPATH` | 一个用冒号分隔的目录列表，用作`cd`命令的搜索路径。 |
| `HOME` | 当前用户的家目录。 |
| `IFS` | 字符列表，用于 shell 分割文本字符串的字段分隔。 |
| `MAIL` | 当前用户邮箱的文件名。`bash` shell 会检查此文件以获取新邮件。 |
| `MAILPATH` | 一个用冒号分隔的多个当前用户邮箱的文件名列表。`bash` shell 会检查此列表中的每个文件是否有新邮件。 |
| `OPTARG` | 由`getopts`命令处理的最后一个选项参数的值。 |
| `OPTIND` | 由`getopts`命令处理的最后一个选项参数的索引值。 |
| `PATH` | 一个用冒号分隔的目录列表，shell 在其中查找命令。 |
| `PS1` | 主级 shell 命令行界面提示符字符串。 |
| `PS2` | 次级 shell 命令行界面提示符字符串。 |

到目前为止，列表中最重要的环境变量是`PATH`变量。当你在 shell 命令行界面 (CLI) 中输入命令时，shell 必须搜索系统以找到程序。`PATH`变量定义了它查找命令的目录。在我的 Linux 系统上，`PATH`变量如下：

```bash
$ echo $PATH

/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:/
/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin

$
```

这显示 shell 有六个查找命令的目录。`PATH`中的每个目录都用冒号分隔。`PATH`变量末尾没有指示目录列表结束的符号。你只需通过添加另一个冒号以及新目录即可向`PATH`添加其他目录。`PATH`还显示了它查找命令的顺序。

除了默认的 Bourne 环境变量外，`bash` shell 还提供了几个自己的变量，如表 5.2 所示。

### bash Shell 环境变量

| 变量 | 说明 |
| :--- | :--- |
| `BASH` | 执行当前`bash` shell 实例的完整路径。 |
| `BASH_ALIASES` | 当前设置的别名的关联数组。 |
| `BASH_ARGC` | 变量数组，包含传递给子程序或 shell 脚本的参数个数。 |
| `BASH_ARCV` | 变量数组，包含传递给子程序或 shell 脚本的参数。 |
| `BASH_CMDS` | shell 已执行的命令位置的关联数组。 |
| `BASH_COMMAND` | 当前正在执行或即将执行的 shell 命令。 |
| `BASH_ENV` | 如果设置时，每个 bash 脚本在运行之前都会尝试执行一个由该变量定义的启动文件。 |
| `BASH_EXECUTION_STRING` | 使用`bash -c`选项传递的命令。 |
| `BASH_LINENO` | 变量数组，包含当前执行的 shell 函数的源代码行号。 |
| `BASH_REMATCH` | 只读变量数组，包含用于正则表达式比较运算符`=∼`进行正向匹配的模式及其子模式。 |
| `BASH_SOURCE` | 变量数组，包含当前执行的 shell 函数的源代码文件名。 |
| `BASH_SUBSHELL` | 当前子 shell 环境的嵌套层级。初始值为 0。 |
| `BASH_VERSION` | 当前`bash` shell 实例的版本号。 |
| `BASH_VERSINFO` | 变量数组，包含当前`bash` shell 实例的各个主版本和次要版本号。 |
| `BASH_XTRACEFD` | 如果设置为有效的文件描述符 (0,1,2)，则可以将从`set -x`调试选项生成的跟踪输出重定向。这通常用于将跟踪输出分离到文件中。 |
| `BASHOPTS` | 当前启用的 bash shell 选项列表。 |
| `BASHPID` | 当前`bash`进程的进程进程 ID (PID)。 |
| `COLUMNS` | 包含当前`bash` shell 实例所使用的终端宽度。 |
| `COMP_CWORD` | 变量`COMP_WORDS`的索引，该变量包含当前光标位置。 |
| `COMP_LINE` | 当前命令行。 |
| `COMP_POINT` | 当前光标位置相对于当前命令起始部分的索引。 |
| `COMP_KEY` | 用于触发补全的最后一个键。 |
| `COMP_TYPE` | 代表补全类型的整数值。 |
| `WORDDBREAKS` | Readline 单词分隔符。 |
| `COMP_WORDS` | 命令行上各个单词的数组。 |
| `COMPREPLY` | 包含生成的可能补全代码的变量数组。 |
| `DIRSTACK` | 目录内容的数组。 |
| `EMACS` | 当设置为`t`时，表示 emacs 缓冲区已禁用。 |
| `EUID` | 用户的数值有效用户 ID。 |
| `FCEDIT` | `fc`使用的默认编辑器。 |
| `FIGNORE` | 在文件名扩展期间忽略的后缀列表，用冒号分隔。 |
| `FUNCNAME` | 当前执行函数的名称。 |
| `GLOBIGNORE` | 定义文件名扩展时要忽略的文件名集的模式列表，用冒号分隔。 |
| `GROUPS` | 包含用户所属组列表的变量数组。 |
| `histchars` | 最多三个字符，控制历史记录。 |
| `HISTCMD` | 当前命令的历史编号。 |
| `HISTCONTROL` | 控制哪些命令被输入到历史列表中。 |
| `HISTFILE` | 保存历史列表的文件名（默认为`.bash_history`）。 |
| `HISTFILESIZE` | 历史记录文件中保存的最大行数。 |
| `HISTIGNORE` | 用于决定哪些命令在历史文件中被忽略的模式列表，用冒号分隔。 |
| `HISTSIZE` | 历史记录文件中存储的最大命令数。 |
| `HOSTFILE` | 包含 shell 需要补全主机名时应读取的文件名。 |
| `HOSTNAME` | 当前的主机名。 |
| `HOSTTYPE` | 描述 bash shell 运行机器的字符串。 |
| `IGNOREEOF` | shell 在退出前必须接收的连续 EOF 字符数。如果此值不存在，默认值为 1。 |
| `INPUTRC` | Readline 初始化文件名（默认是`.inputrc`）。 |
| `LANG` | shell 的语言区域类别。 |
| `LC_ALL` | 覆盖`LANG`变量，定义一个语言区域。 |
| `LC_COLLATE` | 设置排序字符串值时使用的排序顺序。 |
| `LC_CTYPE` | 决定文件名扩展和模式匹配中使用的字符解释。 |
| `LC_MESSAGES` | 决定解释由美元符号引导的双引号字符串时使用的语言区域设置。 |
| `LC_NUMERIC` | 决定格式化数字时使用的语言区域设置。 |
| `LINENO` | 当前执行脚本中的行号。 |
| `LINES` | 定义终端上的可用行数。 |
| `MACHTYPE` | 一个以`cpu-company-system`格式定义系统类型的字符串。 |
| `MAILCHECK` | shell 检查新邮件的频率（秒，默认为 60）。 |
| `OLDPWD` | 在 shell 中使用的上一个工作目录。 |
| `OPTERR` | 如果设置为 1，bash shell 会显示`getopts`命令生成的错误。 |
| `OSTYPE` | 一个定义 shell 运行的操作系统的字符串。 |
| `PIPESTATUS` | 一个变量数组，包含前台进程中进程退出状态值列表。 |
| `POSIXLY_CORRECT` | 如果设置，bash 将以 POSIX 模式启动。 |
| `PPID` | bash shell 父进程的进程 ID (PID)。 |
| `PROMPT_COMMAND` | 如果设置，则在显示主提示符之前执行的命令。 |
| `PROMPT_DIRTRIM` | 整数，用于指定在使用`\w`和`\W`提示符字符串转义字符时显示的末尾目录数量。被移除的目录名将用一组省略号替换。 |
| `PS3` | `select`命令使用的提示符。 |
| `PS4` | 当使用 bash `-x`参数时，在回显命令行之前显示的提示符。 |
| `PWD` | 当前工作目录。 |
| `RANDOM` | 返回一个 0 到 32767 之间的随机数。为此变量赋值会为随机数生成器的种子。 |
| `REPLY` | `read`命令的默认变量。 |
| `SECONDS` | 自 shell 启动以来秒数。为此变量赋值会将计时器重置为该值。 |
| `SHELL` | bash shell 的完整路径。 |
| `SHELLOPTS` | 已启用的 bash shell 选项的冒号分隔列表。 |
| `SHLVL` | 表示 shell 级别，每启动一个新的 bash shell 加 1。 |
| `TIMEFORMAT` | 指定 shell 如何显示时间值的格式。 |
| `TMOUT` | `select`和`read`命令等待输入的时间（秒）。默认值 0 表示无限等待。 |
| `TMPDIR` | bash shell 创建临时文件使用的目录名。 |
| `UID` | 当前用户的数字真实用户 ID。 |

你可能会发现，当使用`set`命令时，并不是所有的默认环境变量都会显示。其原因是尽管这些是默认环境变量，但并非所有变量都必须包含值。

## 设置 PATH 环境变量

`PATH`环境变量在 Linux 系统上似乎引起的问题最多。它定义了 shell 在哪里查找你在命令行上输入的命令。如果它找不到该命令，它会产生一条错误消息：

```bash
$ myprog

-bash: myprog: command not found

$
```

问题在于，应用程序通常将它们的可执行程序放在不在`PATH`环境变量中的目录中。技巧是确保你的`PATH`环境变量包含了你应用程序所在的所有目录。

你可以将新的搜索目录添加到现有的`PATH`环境变量中，而无需从头构建。`PATH`中列出的各个目录由冒号分隔。你只需要引用原始`PATH`值并向字符串中添加任何新目录。它看起来像这样：

```bash
$ echo $PATH

/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:/
/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin

$ PATH=$PATH:/home/user/test

$ echo $PATH

/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:/
/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin:/home/user/test

$ myprog

The factorial of 5 is 120.

$
```

通过将目录添加到`PATH`环境变量中，你现在可以从虚拟目录结构的任何地方执行你的程序：

```bash
[user@localhost ~]$ cd /etc

[user@localhost etc]$ myprog

The factorial of 5 is 120

[user@localhost etc]$
```



程序员的一个常用技巧是在`PATH`环境变量中包含单点符号`.`。单点符号表示当前目录（见第 3 章）：

```bash
[user@localhost ~]$ PATH=$PATH:.
[user@localhost ~]$ cd test2
[user@localhost test2]$ myprog2
The factorial of 6 is 720
[user@localhost test2]$
```

在下一节中，你将看到如何在系统上对环境变量进行永久更改，以便你始终能够执行你的程序。

## 定位系统环境变量

Linux 系统使用环境变量在程序和脚本中标识自己。这为你的程序获取系统信息提供了一种方便的方法。技巧在于这些环境变量是如何设置的。

当你通过登录 Linux 系统来启动`bash` shell 时，默认情况下`bash`会检查几个文件以获取命令。这些文件被称为启动文件。`bash`处理的启动文件取决于你启动`bash` shell 的方法。启动`bash` shell 有三种方式：

- 作为登录时的默认登录 shell
- 作为非登录 shell 的交互式 shell
- 作为运行脚本的非交互式 shell

接下来的章节描述了`bash` shell 在这些启动方法中执行的启动文件。

### 登录 shell (Login Shell)

当你登录 Linux 系统时，`bash` shell 作为登录 shell 启动。登录 shell 会查找四个不同的启动文件来处理命令。以下是`bash`处理这些文件的顺序：

- `/etc/profile`
- `$HOME/.bash_profile`
- `$HOME/.bash_login`
- `$HOME/.profile`

`/etc/profile`文件是系统中`bash` shell 的主要默认启动文件。系统上的每个用户在登录时都会执行此启动文件。其他三个启动文件是针对每个用户特定的，并且可以根据每个用户的需求进行自定义。让我们仔细观察这些文件。

### `/etc/profile`文件

`/etc/profile`文件是 `bash` 的主要默认启动文件。每当你登录 Linux 系统时，`bash`都会执行`/etc/profile`启动文件中的命令。不同的 Linux 发行版在该文件中放置不同的命令。在当前 Linux 系统上，它看起来是这样的：

```bash
$ cat /etc/profile
## /etc/profile
### System wide environment and startup programs, for login setup
### Functions and aliases go in /etc/bashrc
# It's NOT a good idea to change this file unless you know what you
# are doing. Much better way is to create custom.sh shell script
# in /etc/profile.d/ to make custom changes. This will
# prevent merging in future.
... (省略部分内容)
pathmunge() {
  case $PATH in
    *:*)
      if [ "$2" = "after" ]; then
        PATH=$1
      else
        PATH=$PATH:$1
      fi
  esac
}
if [ -x /id ]; then
  if [ -z "$EUID" ]; then
    # ksh around
    EUID='id -u'
    UID='id -ru'
  fi
  USER="id -un"
  LOGNAME=$USER
  MAIL="/var/mail/$USER"
fi
## Path manipulation
if [ "$EUID" = "0" ]; then
  pathmunge /sbin
  pathmunge /usr/sbin
  pathmunge /usr/local/sbin
else
  pathmunge /usr/local/sbin after
  pathmunge /usr/sbin after
  pathmunge /sbin after
fi
HOSTNAME='/bin/hostname 2>/dev/null'
HISTSIZE=1000
if [ "$HISTCONTROL" = "ignorespace" ]; then
  export HISTCONTROL=ignoreboth
else
  export HISTCONTROL=ignoredups
fi
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL
for i in /etc/profile.d/*.sh; do
  if [ -r "$i" ]; then
    if [ "$PS1" ]; then
      . $i
    else
      . $i >/dev/null 2>&1
    fi
  fi
done
unset i
unset pathmunge
$
```

你在此文件中看到的大多数命令和脚本在第 10 章中会有更详细的介绍。现在需要注意的是在此启动文件中设置的环境变量。注意文件底部的`export`行：

```bash
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL
```

这确保了这些环境变量对于从登录 shell 产生的所有子进程都是的。

`profile`文件还使用了另一个复杂的特性。其中有一个`for`语句会遍历位于`/etc/profile.d`目录中的任何文件（`for`语句将在第 12 章中详细讨论）。这为 Linux 系统提供了一个放置特定应用程序启动文件的地方，这些文件会在你登录时由 shell 执行。在这个 Linux 系统上，`profile.d`目录下包含以下文件：

```bash
$ ls -l /etc/profile.d
total 72
-rw-r--r--. 1 root root 1133 Apr 28 10:43 colorls.csh
-rw-r--r--. 1 root root 1143 Apr 28 10:43 colorls.sh
-rw-r--r--. 1 root root 192 Sep 9 2004 glib2.csh
-rw-r--r--. 1 root root 192 Dec 12 2005 glib2.sh
-rw-r--r--. 1 root root 58 May 31 06:23 gnome-ssh-askpass.csh
-rw-r--r--. 1 root root 70 May 31 06:23 gnome-ssh-askpass.sh
-rw-r--r--. 1 root root 184 Aug 25 11:36 krb5-workstation.csh
-rw-r--r--. 1 root root 57 Aug 25 11:36 krb5-workstation.sh
-rw-r--r--. 1 root root 1741 Jun 24 15:20 lang.csh
-rw-r--r--. 1 root root 2706 Jun 24 15:20 lang.sh
-rw-r--r--. 1 root root 122 Feb 7 2007 less.csh
-rw-r--r--. 1 root root 108 Feb 7 2007 less.sh
-rw-r--r--. 1 root root 837 Sep 2 05:24 PackageKit.sh
-rw-r--r--. 1 root root 2142 Aug 10 16:41 udisks-bash-completion.sh
-rw-r--r--. 1 root root 74 Mar 25 19:24 vim.csh
-rw-r--r--. 1 root root 248 Mar 25 19:24 vim.sh
-rw-r--r--. 1 root root 161 Nov 27 2007 which2.csh
-rw-r--r--. 1 root root 169 Nov 27 2007 which2.sh
$
```

你会注意到这些文件大多与系统上的特定应用程序有关。大多数应用程序创建两个启动文件，一个用于`bash` shell（使用`.sh`扩展名），另一个用于 `c` shell（使用`.csh`扩展名）。

`lang.csh`和`lang.sh`文件尝试确定系统使用的默认语言字符集，并恰当地设置`LANG`环境变量。

### `$HOME`启动文件

剩下的三个启动文件都用于相同的功能——提供一个用户特定的启动文件，用于定义用户特定的环境变量。大多数 Linux 发行版仅使用这三个启动文件之一：

- `$HOME/.bash_profile`
- `$HOME/.bash_login`
- `$HOME/.profile`

注意这三个文件都以点开头，这意味着它们是隐藏文件（它们不会出现在普通的`ls`命令中）。因为它们位于用户的`HOME`目录中，每个用户都可以编辑这些文件并添加自己的环境变量，这些变量会在启动的每个 bash 会话中生效。此 Linux 系统包含以下`.bash_profile`文件：

```bash
cat .bash_profile
## .bash_profile
## Get the aliases and functions
if [ -f ~/.bashrc ]; then
    ~/.bashrc
fi
## User specific environment and startup programs
PATH=$PATH:$HOME/bin
export PATH
$
```

`.bash_profile`启动文件首先检查`HOME`目录下是否存在另一个名为`.bashrc`的启动文件（我们将在“交互式 shell”部分中讨论它）。如果存在，启动文件将执行其中的命令。接下来，启动文件会向`PATH`环境变量添加一个目录，为在你的`HOME`目录中放置可执行文件提供一个公共位置。

### 交互式 shell

如果你在没有登录系统的情况下启动了`bash` shell（例如在 CLI 提示符处输入`bash`），你启动的就是所谓的交互式 shell。交互式 shell 的行为不像登录 shell，但它仍然为你提供了一个 CLI 提示符来输入命令。如果`bash`作为交互式 shell 启动，它不会处理`/etc/profile`文件。相反，它会检查用户`HOME`目录下的`.bashrc`文件。在这个 Linux 发行版上，该文件看起来如下：

```bash
cat .bashrc
## .bashrc
### Source global definitions
if [ -f /etc/bashrc ]; then
    .etc/bashrc
fi
### User specific aliases and functions
$
```

`.bashrc`文件做两件事。首先，它检查`/etc`目录下的通用`bashrc`。其次，它为用户输入个人别名（稍后在“使用别名”部分讨论）和私有脚本函数（在第 16 章描述）提供了一个位置。通用的`/etc/bashrc`启动文件由系统中启动交互式 shell 的所有人运行。在这个 Linux 发行版上，它看起来如下：

```bash
cat /etc/bashrc
## /etc/bashrc
### System wide functions and aliases
### Environment stuff goes in /etc/profile
# It's NOT good idea to change this file unless you know what you are doing.
# Much better way is to create custom.sh shell script in
# /etc/profile.d/ to make custom changes to environment. This will
# prevent need for merging in future updates.
### By default, we want this to get set.
### Even for non-interactive, non-login shells.
### Current threshold for system reserved uid/gids is 200
# You could check uidgid reservation validity in
# /usr/share/doc/setup-*/uidgid file
if [ $UID -gt 199 ] && [ 'id -gn' = 'id-un' ]; then
    umask 002
else
    umask 022
fi
### are we an interactive shell?
if [ "$PS1" ]; then
    case $TERM in
xterm*)
        if [ -e /etc/sysconfig/bash-prompt-xterm ]; then
            PROMPT_COMMAND=/etc/sysconfig/bash-prompt-xterm
        else
            PROMPT_COMMAND=echo -ne "\033]${USER}@${HOSTNAME%%}:${PWD/#$HOME}/";\007"
        fi
        ;;
    screen)
        if [ -e /etc/sysconfig/bash-prompt-screen ]; then
            PROMPT_COMMAND=/etc/sysconfig/bash-prompt-screen
        else
            PROMPT_COMMAND=echo -ne "\033_${USER}@${HOSTNAME%%}:${PWD/#$HOME}/\033"
        fi
        ;;
    *)
        [ -e /etc/sysconfig/bash-prompt-default ] && PROMPT_COMMAND=/etc/sysconfig/bash-prompt-default
        ;;
    esac
    # Turn on winsize
    shopt -s winsize
    [ "$PS1" = "\w\$ ] && PS1="[@h \W]"
    # You might want to have tty in prompt (e.g. more virtual machines)
    # and console windows
    # If you want to do so, just add e.g.
    # if [ "$PS1" ]; then
    #   PS1="[@h:\1 \W]"
    # fi
    # to your custom modification shell script in /etc/profile.d/ directory
fi
if ! shopt -q login_shell; then # We're not a login shell
    # Need to redefine pathmunge, it's undefined at the end of /etc/profile
    pathmunge () {
        case ":${PATH}:" in
            *:"$1":*)
                ;;
            *)
                if [ "$2" = "after" ]; then
                    PATH=$PATH:$1
                else
                    PATH=$1:$PATH
                fi
            fi
        esac
    }
    # Only display echos from profile.d scripts if we are no login shell
    # and otherwise just process them to set env
    for i in /etc/profile.d/*.sh; do
        if [ -r "$i" ]; then
            if [ "$PS1" ]; then
                .$i
            else
                .$i >/dev/null 2>&1
            fi
        fi
    done
    unset i
    unset pathmunge
fi
### vim:ts=4:sw=4
```



默认文件设置了几个环境变量，但注意它并没有使用`export`命令将它们设置为全局变量。记住，交互式 shell 启动文件会在每次启动新的交互式 shell 时运行；因此，任何子 shell 都会自动执行交互式 shell 启动文件。

还会注意到`/etc/bashrc`文件也会执行位于`/etc/profile.d`目录下的特定应用程序启动文件。

### 非交互式 Shell

最后一种 shell 是非交互式 shell。这是系统为了执行 shell 脚本而启动的 shell。与之前的不同之处在于，它不需要担心 CLI 提示符。然而，你可能仍然希望每次在系统上启动脚本时运行某些特定的启动命令。

为了适应这种情况，bash shell 提供了`BASH_ENV`环境变量。当 shell 启动非交互式进程时，它会检查此环境变量以获取要执行启动文件名。如果存在，shell 将执行文件中的命令。在我们使用的 Linux 发行版中，默认没有设置此环境变量值。

### 变量数组

环境变量的一个非常酷的特性是它们可以当作数组使用。数组是可以包含多个值的变量。值可以单独引用，也可以作为整个数组整体引用。

要为环境变量设置多个值，只需将它们列在括号中，并用空格分隔每个值：

```bash
$ mytest=(one two three four five)
$
```

这没什么令人兴奋的。如果你尝试像显示普通环境变量一样显示数组，你会感到失望的：

```bash
$ echo $mytest
one
$
```

只出现了数组中的第一个值。要引用单个数组元素，必须使用数值索引值，该值代表它在数组中的位置。数值包含在方括号中：

```bash
$ echo ${mytest[2]}
three
$
```

> **注意**
>
> 环境变量数组的索引值从零开始。这通常会引起困惑。

要显示整个数组变量，你使用星号通配符作为索引值：

```bash
$ echo ${mytest[*]}
one two three four five
$
```

你也可以更改单个索引位置的值：

```bash
$ mytest[2]=seven
$ echo ${mytest[*]}
one two seven four five
$
```

你甚至可以使用`unset`命令删除数组中的单个值，但要小心，因为这很复杂。看这个例子：

```bash
$ unset mytest[2]
$ echo ${mytest[*]}
one two four five
$
$ echo ${mytest[2]}
$ echo ${mytest[3]}
four
$
```

这个示例使用`unset`命令删除索引值为 2 的值。当你显示数组时，其他索引值似乎向下移动了一位。然而，如果你专门显示索引值为 2 处的数据，你会发现该位置是空的。

最后，你可以通过在`unset`命令中使用数组名删除整个数组：

```bash
$ unset mytest
$ echo ${mytest[*]}
$
```

有时变量数组会让事情变得复杂，因此它们在 shell 编程中经常不使用。它们对其他环境的移植性不好，如果你为不同的 shell 进行大量的 shell 编程，这是一个缺点。bash 有几个使用数组的环境变量（例如`BASH_INFO`），但总的来说你不会经常遇到它们。

### 使用命令别名

虽然命令别名（alias）不是正式环境变量，但 shell 命令别名的行为非常相似。命令别名允许你为常用命令（以及它们的参数）创建一个别名，以帮助你最少地输入。

很可能，你的 Linux 发行版已经为你设置了一些命令别名。要查看活动别名列表，使用带有`-p`参数的`alias`命令：

```bash
$ alias -p
alias .='ls -d --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias vi='vim'
alias which='alias /usr/bin/which --tty-only --show-dot'
```

注意，在这个 Linux 发行版上，别名被用来覆盖标准的`ls`命令。它自动提供了`--color`参数，表示终端支持颜色。你可以通过`alias`命令创建自己的别名：

```bash
$ alias li='ls -il'
$ li
total 32
75 drwxr-xr-x 2 user user 4096 Sep 16 11 Desktop
79 drwxr-xr-x 2 user user 4096 Sep 20 15 Documents
76 drwxr-xr-x 2 user user 4096 Sep 15 30 Downloads
80 drwxr-xr-x 2 user user 4096 Sep 15 30 Music
81 drwxr-xr-x 2 user user 4096 Sep 15 30 Pictures
78 drwxr-xr-x 2 user user 4096 Sep 15 30 Public
77 drwxr-xr-x 2 user user 4096 Sep 15 30 Templates
82 drwxr-xr-x 2 user user 4096 Sep 15 30 Videos
$
```

一旦你定义了别名值，你就可以在 shell 的任何时候使用它，包括在 shell 脚本中。命令别名的作用就像本地环境变量。它们只在定义它们的 shell 进程中有效：

```bash
$ alias li='ls -il'
$ bash
$ li
bash: li: command not found
$
```

当然，现在你知道了解决该问题的方法。bash shell 在启动新的交互式 shell 时总是会读取`$HOME/.bashrc`启动文件。这是放置命令`alias`语句的好地方（正如`.bashrc`文件注释中所指出的）。

## 总结

本章研究了 Linux 环境变量的世界。全局环境变量可以从定义它的进程派生的任何子进程中访问。本地环境变量只能从定义它的进程中访问。

Linux 系统同时使用全局和本地环境变量来存储系统环境信息。你可以从 shell 命令行界面以及 shell 脚本内部访问这些信息。bash shell 使用了原始 Unix Bourne shell 中定义的系统环境变量，以及许多新的环境变量。`PATH`环境变量定义了 bash shell 查找可执行命令时所采用的搜索模式。你可以修改`PATH`环境变量来添加你自己的目录，甚至是当前目录符号，使运行你的程序变得更容易。

你也可以创建你自己的全局和本地环境变量以供自己使用。一旦你创建了环境变量，它在整个 shell 会话期间都是可访问的。

在 shell 启动时，有几个启动文件是 bash shell 启动时执行的。这些启动文件可以包含环境变量定义，以便为每个 bash 会话设置标准环境变量。当你登录 Linux 系统时，bash shell 会访问`/etc/profile`启动文件，还会为每个用户访问三个本地启动文件：`$HOME/.bash_profile`、`$HOME/.bash_login`和`$HOME/.profile`。用户可以自定义这些文件，包含他们自己使用的环境变量和启动脚本。

bash shell 还提供了环境变量数组。这些环境变量可以在单个变量中包含多个值。你可以通过引用索引值来单独访问值，也可以通过引用整个环境变量数组名来整体访问值。

最后，本章讨论了命令别名的使用。虽然命令别名不是环境变量，但它们的行为与环境变量非常相似。它们允许你为命令及其参数定义一个别名。你不需要输入长长的命令和参数，只需将其分配给一个简单的别名，并在 shell 会话的任何时候使用该别名即可。

# 理解 Linux 文件权限

## 本章内容

- 理解 Linux 安全
- 解码权限
- 组 Linux 组

任何系统如果没有某种形式的安全措施是不完整的。必须有一种机制来保护文件不受未经授权的查看或修改。Linux 系统遵循 Unix 的文件权限方法，根据每个文件和目录的一组安全设置，允许个人用户和组访问文件。本章将讨论如何使用 Linux 文件安全系统在必要时保护数据，并在需要时共享数据。

## Linux 安全

Linux 安全系统的核心是用户账户。每个访问 Linux 系统的个人都应该分配一个唯一的用户账户。用户对系统对象的权限取决于他们登录时使用的账户。

用户权限通过用户 ID（通常称为`UID`）进行跟踪，该 ID 在账户创建时被分配给账户。`UID`是一个数值，对每个用户都是唯一的。然而，你并不是使用`UID`登录 Linux 系统。相反，你使用的是登录名。登录名是一个 8 个字符或更少的数字字母字符串，用户用它登录系统（以及关联的密码）。

Linux 系统使用特殊文件和实用程序来跟踪和管理系统上的用户账户。在讨论文件权限之前，我们需要讨论 Linux 如何处理用户账户。本节描述了用户账户所需的文件和实用程序，以便你能够在处理文件权限时理解如何使用它们。

### `/etc/passwd`文件

Linux 系统使用一个特殊文件将登录名与对应的`UID`值匹配。这个文件就是`/etc/passwd`文件。`/etc/passwd`文件包含了关于用户的几条信息。以下是 Linux 系统上典型的`/etc/passwd`文件内容：

```text
cat /etc/passwd

root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
news:x:9:13:news:/etc/news:
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
rpm:x:37:37::/var/lib/rpm:/sbin/nologin
vcsa:x:69:69:virtual console memory owner:/dev:/sbin/nologin
mailnull:x:47:47::/var/spool/mqueue:/sbin/nologin
smmsp:x:51:51::/var/spool/mqueue:/sbin/nologin
apache:x:48:48:Apache:/var/www:/sbin/nologin
rpc:x:32:32:Rpcbind Daemon:/var/lib/rpcbind:/sbin/nologin
ntp:x:38:38::/etc/ntp:/sbin/nologin
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
avahi:x:70:70:Avahi daemon:/:/sbin/nologin
hsqldb:x:96:96::/var/lib/hsqldb:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
haldaemon:x:68:68:HAL daemon:/:/sbin/nologin
xfs:x:43:43:X Font Server:/etc/X11/fs:/sbin/nologin
gdm:x:42:42::/var/gdm:/sbin/nologin
rich:x:500:500:Rich Blum:/home/rich:/bin/bash
mama:x:501:501:Mama:/home/mama:/bin/bash
katie:x:502:502:katie:/home/katie:/bin/bash
jessica:x:503:503:Jessica:/home/jessica:/bin/bash
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
$
```

`root`用户账户始终被分配`0`。如你所见，`/etc/passwd`文件包含的不仅是登录名和`UID`。Linux 将 500 以下的 UID 预留给系统账户。`/etc/passwd`文件包含以下信息：

- 登录名
- 密码
- 数值`UID`
- 数值组 ID（`GID`）
- 用户的文本描述（注释字段）
- `HOME`目录的位置
- 默认 shell

`/etc/passwd`中的密码字段被设为`x`。在过去，`/etc/passwd`文件包含密码的加密版本。然而，由于许多程序需要访问它，这成了一个安全问题。随着可以轻松解密密码的软件出现，Linux 开发者需要重新考虑该策略。

现在，大多数 Linux 系统将`/etc/passwd`文件看作一个标准文本文件。你可以使用任何文本编辑器直接在`/etc/passwd`文件中手动执行用户管理功能（如添加、修改或删除用户账户）。然而，这是一种极其危险的做法。如果`/etc/passwd`文件损坏，系统将无法读取它，并阻止任何人（即使是 root 用户）登录。相反，使用标准的 Linux 用户管理实用程序更安全。

### `/etc/shadow`文件

`/etc/shadow`文件对 Linux 系统如何管理密码提供了更多的控制。只有 root 用户可以访问`/etc/shadow`文件，这使其比`/etc/passwd`文件更安全。

`/etc/shadow`文件为系统的每个用户账户提供一条记录。记录格式如下：

```text
rich:$1$.FfcK0ns$f1UgiyHQ25wrB/hykCn020:11627:0:99999:7::
```

每个`/etc/shadow`文件记录有九个字段：

- 与`/etc/passwd`文件中的登录名对应的登录名
- 加密密码
- 上次更改密码距离 1970 年 1 月 1 日起的天数
- 更改密码前的最少天数
- 必须更改密码前的天数
- 密码过期前警告用户更改密码的天数
- 密码过期后账户被禁用的天数
- 用户账户禁用的日期（存储为自 1970 年 1 月 1 日起的天数）
- 留供未来使用的字段

使用影子密码系统，Linux 系统对用户密码有许多更精细的控制。它可以控制用户更改密码的频率，以及在密码未更改时何时禁用该账户。

## 添加新用户

在 Linux 系统中添加新用户使用的主要工具是`useradd`。该命令提供了一种创建新用户账户并一次性设置用户`HOME`目录结构的简单方法。`useradd`命令使用系统默认值和命令行参数的组合来定义用户账户。要查看您的 Linux 发行版上使用的系统默认值，请输入带有`-D`参数的`useradd`命令：

```bash
## /usr/sbin/useradd -D

GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
#
```

> **注意**
>
> 某些 Linux 发行版将 Linux 用户和组工具放在`/usr/sbin`目录中，该目录可能不在您的`PATH`环境变量中。如果您的 Linux 发行版是这种情况，请将该目录添加到`PATH`中，或使用绝对路径运行它。

`-D`参数显示了当在创建新用户账户时未在命令行中指定时，`useradd`命令将使用的默认值。此示例显示了以下默认值：

- 新用户将被添加到组 ID 为 100 的公共组中。
- 新用户将在`/home/loginname`目录下创建一个`HOME`账户。
- 当密码过期时，账户不会被禁用。
- 新账户不会设置在指定日期过期。
- 新账户将使用 bash shell 作为默认 shell。
- 系统将`/etc/skel`目录的内容复制到用户的`HOME`目录中。
- 系统将在邮件目录中创建一个文件，供该用户账户接收邮件。

倒数第二个值很有趣。`useradd`命令允许管理员创建一个默认的`HOME`目录配置，然后将其作为模板来创建新用户的`HOME`目录。这允许您自动在每个新用户的`HOME`目录中放置系统的默认文件。在 Ubuntu Linux 系统中，`/etc/skel`目录包含以下文件：

```bash
$ ls -al /etc/skel

total 32
```



`drwxr-xr-x   2 root root  4096 2010-04-29 08:26 .`

`drwxr-xr-x 135 root root 12288 2010-09-23 18:49 ..`

`-rw-r--r--   1 root root   220 2010-04-18 21:51 .bash_logout`

`-rw-r--r--   1 root root   3103 2010-04-18 21:51 .bashrc`

`-rw-r--r--   1 root root   179 2010-03-26 08:31 examples.desktop`

`-rw-r--r--   1 root root   675 2010-04-18 21:51 .profile`

`$`

您应该在第 5 章中认识这些文件。这些是 bash shell 环境的标准启动文件。系统会自动将这些默认文件复制到您创建的每个用户的 `HOME` 目录中。

您通过使用默认系统参数创建新用户账户，然后查看新用户的 `HOME` 目录来测试这一点：

```bash
## useradd -m test
## ls -al /home/test
total 24
drwxr-xr-x   2 test test 4096 2010-09-23 19:01 .
drwxr-xr-x   4 root root 4096 2010-09-23 19:01 ..
-rw-r--r--   1 test test   220 2010-04-18 21:51 .bash_logout
-rw-r--r--   1 test test   3103 2010-04-18 21:51 .bashrc
-rw-r--r--   1 test test   179 2010-03-26 08:31 examples.desktop
-rw-r--r--   1 test test   675 2010-04-18 21:51 .profile
#
```

默认情况下，`useradd` 命令不会创建 `HOME` 目录，但 `-m` 命令行选项告诉它创建 `HOME` 目录。如示例所示，`useradd` 命令使用 `/etc/skel` 目录包含的文件创建了新的 `HOME` 目录。

> **注意**
> 要运行本章中的用户账户管理命令，您可能需要登录为特殊的 root 用户账户，或者使用 `sudo` 命令以 root 用户账户身份运行命令。

如果您想在创建新用户时覆盖默认值或行为，可以通过命令行参数来实现。这些参数列在表 6.1 中所示。

### 表 6.1: `useradd` 命令命令行参数

| 参数 | 描述 |
| :--- | :--- |
| `-c` `comment` | 在用户注释中添加文本。 |
| `-d` `home_dir` | 为主目录指定一个与默认不同的名称。 |
| `-e` `expire_date` | 指定账户过期的日期，格式为 YYYY-MM-DD。 |
| `-f` `inactive` | 密码过期后到账户禁用前的天数。 |
| `-g` `group` | 指定组名或 GID。 |
| `-G` `group` | 指定用户所属的一个或多个附加组。 |
| `-k` `skel` | 将 `/etc/skel` 目录的内容复制到用户的 `HOME` 目录中。 |
| `-m` | 创建主目录。 |
| `-M` | 不创建 `HOME` 目录。 |
| `-n` | 指定组名作为默认。 |
| `-r` | 创建系统账户 |
| `-p` `passwd` | 指定加密密码。 |
| `-s` `shell` | 指定默认 shell。 |
| `-u` `uid` | 为账户指定唯一的 UID。 |

如果您想在创建新用户时覆盖默认值或行为，可以使用命令行参数。这些参数列在表 6.2 中。

### 表 6.2: `useradd` 默认值

| 参数 | 描述 |
| :--- | :--- |
| `-b` `default_home` | 修改用户目录创建的位置。 |
| `-e` `expiration_date` | 修改新账户的过期日期。 |
| `-f` `inactive` | 修改密码过期后到禁用前的天数。 |
| `-g` `group` | 修改默认组名。 |
| `-s` `shell` | 修改默认 shell。 |

更改默认值的操作如下：

```bash
## useradd -D -s /bin/bash
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
#
```

现在，`useradd` 命令将使用 bash shell 作为您创建的所有用户账户的默认 shell。

## 删除用户

如果您想从系统中删除用户，需要的是 `userdel` 命令。默认情况下，`userdel` 命令仅从 `/etc/passwd` 文件中删除用户信息。它不会删除账户在系统中拥有的任何文件。

如果您使用 `-r` 参数，`userdel` 将删除用户的 `HOME` 目录以及用户的邮件目录。然而，系统中可能仍有其他删除用户账户拥有的文件。这在某些环境中可能会产生问题。

使用 `userdel` 命令删除现有用户账户的示例：

```bash
## /usr/sbin/userdel -r test
## ls -al /home/test
ls: 无法访问 home/test': 无此文件或目录
#
```

使用 `-r` 参数后，用户的旧 `/home/test` 目录不再存在。

> **警告**
> 在多用户环境中使用 `-r` 参数时要小心。您永远不知道用户是否在其 `HOME` 目录中存储了其他其他人或其他程序使用的重要文件。在删除用户的 `HOME` 目录之前，请务必进行检查！

Linux 提供了不同的工具来修改现有用户账户的信息。表 6.3 显示了这些工具。

### 用户账户修改工具

表 6.3 用户账户修改工具

| 命令 | 描述 |
| :--- | :--- |
| `usermod` | 编辑用户账户字段，并指定主组和从组的组成关系 |
| `passwd` | 更改现有用户的密码 |
| `chpasswd` | 读取包含用户名和密码对的文件并更新密码 |
| `chage` | 修改密码的过期日期 |
| `chfn` | 修改用户账户的注释信息 |
| `chsh` | 更改用户账户的默认 shell |

这些工具中的每一个都提供了用于更改用户账户信息的特定功能。接下来的章节将详细介绍这些工具。

### `usermod`

`usermod` 命令是用户账户修改工具中最功能强大的一个。它提供了更改 `/etc/passwd` 文件中大部分字段的选项。要实现这一点，你只需要使用与你想要更改的值相对应的命令行参数。这些参数与 `useradd` 参数大部分相同（例如使用 `-c` 更改注释字段，`-e` 更改过期日期，以及 `-g` 更改默认登录组）。不过，还有几个额外的参数可能非常有用：

* `-l` 更改用户账户的登录名称
* `-L` 锁定账户，使用户无法登录
* `-p` 更改账户的密码
* `-U` 解锁账户，使用户可以登录

`-L` 参数特别有用。使用它来锁定账户，这样用户在无需删除账户及其用户数据的情况下无法登录。要将账户恢复正常，只需使用 `-U` 参数即可。

### `passwd` 和 `chpasswd`

更改用户密码的快速方法是使用 `passwd` 命令：

```bash
## passwd test
Changing password for user test.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
#
```

如果你仅单独使用 `passwd` 命令，它将更改你自己的密码。系统中的任何用户都可以更改自己的密码，但只有 root 用户可以更改他人的密码。

`-e` 选项是一种强制用户在下次登录时更改密码的实用方法。这允许你将用户的密码设置为一个简单的值，然后强制他们更改为他们可以记住的更复杂的密码。

如果你需要对系统上的大量用户进行批量密码更改，`chpasswd` 命令可以成为救命稻草。`chpasswd` 命令自动从标准输入读取用户名和密码对（用冒号分隔），加密密码并将其设置到用户账户。你也可以使用重定向命令将 `userid:password` 对的文件重定向到命令中：

```bash
## chpasswd < users.txt
#
```

### `chsh`, `chfn` 和 `chage`

`chsh`、`chfn` 和 `chage` 工具专门用于特定的账户修改功能。`chsh` 命令允许你快速更改用户的默认登录 shell。你必须使用 shell 的完整路径，而不仅仅是 shell 名称：

```bash
## chsh -s /bin/csh test
Changing shell for test.
Shell changed.
#
```

`chfn` 命令提供了一种在 `/etc/passwd` 文件注释字段中存储信息的标准方法。`chfn` 命令并不是仅仅插入随机文本（如姓名或昵称），或者留空注释字段，而是使用 Unix `finger` 命令中使用的特定信息在注释字段中存储信息。`finger` 命令允许你轻松查找 Linux 系统上人员的信息：

```bash
# finger rich
Login: rich                        Name: Rich Blum
Directory: /home/rich             Shell: /bin/bash
On since Thu Sep 20 18:03 (EDT) on pts/0 from 192.168.1.2
No mail.
No Plan.
#
```

> **注意**
> 出于安全考虑，许多 Linux 系统管理员会在他们的系统上禁用 `finger` 命令。

如果你在不带任何参数的情况下使用 `chfn` 命令，它会询问你输入适当的值：

```bash
# finger rich
Login: rich                        Name: Rich Blum
Directory: /home/rich             Shell: /bin/bash
On since Thu Sep 20 18:03 (EDT) on pts/0 from 192.168.1.2
No mail.
No Plan.
#
```

`rich:x:500:`

`mama:x:501:`

`katie:x:502:`

`jessica:x:503:`

`mysql:x:27:`

`test:x:504:`

与 UID 类似，GID 也使用特殊的格式进行分配。用于系统账户的组被分配 500 以下的 GID，而用户组被分配从 500 开始的 GID。`/etc/group` 文件包含四个字段：

* 组名
* 组密码
* GID
* 属于该组的用户账户列表

组密码允许非组成员通过使用密码临时成为该组的成员。虽然这一功能并不算常用，但它确实存在。

你永远不应该通过编辑 `/etc/group` 文件来将用户添加到组中。相反，请使用 `usermod` 命令（在前面的“Linux 安全”章节中已讨论过）将用户账户添加到组中。在能够将用户添加到不同的组之前，你必须先创建这些组。

> **注意**
> 用户账户列表具有某种误导性。你会注意到列表中有几个组没有列出任何用户。这并不是因为它们没有成员。当一个用户账户在 `/etc/passwd` 文件中使用某个组作为默认组时，该用户账户不会作为成员出现在 `/etc/group` 文件中。多年来，这曾让多个系统管理员感到过困惑！

## 创建新组

`groupadd` 命令允许你在系统上创建新组：

```bash
## /usr/sbin/groupadd shared
## tail /etc/group
haldaemon:x:68:
xfs:x:43:
gdm:x:42:
rich:x:500:
mama:x:501:
katie:x:502:
jessica:x:503:
mysql:x:27:
test:x:504:
shared:x:505:
#
```

当你创建一个新组时，默认没有用户分配给它。`groupadd` 命令没有提供将用户账户添加到组的选项。相反，要添加新用户，请使用 `usermod` 命令：

```bash
## /usr/sbin/usermod -G shared rich
## /usr/sbin/usermod -G shared test
## tail /etc/group
haldaemon:x:68:
xfs:x:43:
gdm:x:42:
rich:x:500:
mama:x:501:
katie:x:502:
jessica:x:503:
mysql:x:27:
test:x:504:
shared:x:505:rich, test
#
```

`shared` 组现在有两个成员：test 和 rich。`usermod` 中的 `-G` 参数将新组添加到该用户账户的组列表中。

> **注意**
> 如果你更改了当前登录系统的账户的用户组，则用户必须注销并重新登录，组更改才会生效。

> **警告**
> 在为用户账户分配组时要小心。如果你使用 `-g` 参数，你指定的组名将替换该用户账户的默认组。`-G` 参数会将该组添加到用户所属的组列表中，同时保持默认组不变。

## 修改组

如你从 `/etc/group` 文件中所见，关于组的信息并不多供你修改。`groupmod` 命令允许你更改现有组的 GID（使用 `-g` 参数）或组名（使用 `-n` 参数）：

```bash
## /usr/sbin/groupmod -n sharing shared
## tail /etc/group
haldaemon:x:68:
xfs:x:43:
gdm:x:42:
rich:x:500:
mama:x:501:
katie:x:502:
jessica:x:503:
mysql:x:27:
test:x:504:
sharing:x:505:test,rich
#
```

在更改组名时，GID 和组成员保持不变，只有组名发生了。由于所有安全权限都是基于 GID 的，你可以随心所欲更改组名，而不会对文件安全产生不利影响。

## 解码文件权限

现在你已经了解了用户和组，是时候解码在使用 `ls` 命令时看到的那些晦涩的文件权限了。本节描述了如何破解这些权限以及它们从何而来。

### 使用文件权限符号

如果你还记得第 3 章的内容，`ls` 命令允许你查看 Linux 系统上文件、目录和设备的权限：

```bash
$ ls -l
total 68
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

输出中的第一个字符定义了文件类型：
* `-` 表示文件
* `d` 表示目录
* `l` 表示链接
* `c` 表示字符设备
* `b` 表示块设备
* `s` 表示符号链接
* `p` 表示套接字
* `f` 表示命名管道

之后，有三组字符。每组定义了访问权限：
* `r` 表示读
* `w` 表示写
* `x` 表示执行

破折号 `-` 表示权限被拒绝。这三组分别对应所有者、所属组和所有人。

例如：

```bash
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

```bash
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

```bash
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

```bash
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

```bash
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

```bash
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
```



`-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz`

`-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2`

`-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3`

例如：

```
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

在输出中，第一个字符定义了文件类型：
* `-` 表示文件
* `d` 表示目录
* `l` 表示链接
* `c` 表示字符设备
* `b` 表示块设备
* `s` 表示符号链接
* `p` 表示套接字
* `f` 表示命名管道

之后，有三组字符。每组定义了访问权限：
* `r` 表示读
* `w` 表示写
* `x` 表示执行

破折线 `-` 表示权限被拒绝。这三组分别对应所有者、所属组和所有人。

例如：

```
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

在输出中，`-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz`、`-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2`、`-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3`。

在输出中，第一个字符定义了文件类型：
* `-` 表示文件
* `d` 表示目录
* `l` 表示链接
* `c` 表示字符设备
* `b` 表示块设备
* `s` 表示符号链接
* `p` 表示套接字
* `f` 表示命名管道

之后，有三组字符。每组定义了访问权限：
* `r` 表示读
* `w` 表示写
* `x` 表示执行

破折线 `-` 表示权限被拒绝。这三组分别对应所有者、所属组和所有人。

例如：

```
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

在输出中，`-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz`、`-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2`、`-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3`。

在输出中，第一个字符定义了文件类型：
* `-` 表示文件
* `d` 表示目录
* `l` 表示链接
* `c` 表示字符设备
* `b` 表示块设备
* `s` 表示符号链接
* `p` 表示套接字
* `f` 表示命名管道

之后，有三组字符。每组定义了访问权限：
* `r` 表示读
* `w` 表示写
* `x` 表示执行

破折线 `-` 表示权限被拒绝。这三组分别对应所有者、所属组和所有人。

例如：

```
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

在输出中，`-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz`、`-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2`、`-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3`。

在输出中，第一个字符定义了文件类型：
* `-` 表示文件
* `d` 表示目录
* `l` 表示链接
* `c` 表示字符设备
* `b` 表示块设备
* `s` 表示符号链接
* `p` 表示套接字
* `f` 表示命名管道

之后，有三组字符。每组定义了访问权限：
* `r` 表示读
* `w` 表示写
* `x` 表示执行

破折线 `-` 表示权限被拒绝。这三组分别对应所有者、所属组和所有人。

例如：

```
-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2
-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3
```

在输出中，`-rw-rw-r-- 1 rich rich    50 2010-09-13 07:49 file1.gz`、`-rw-rw-r-- 1 rich rich    23 2010-09-13 07:50 file2`、`-rw-rw-r-- 1 rich rich    48 2010-09-13 07:56 file3`。

在输出中，第一个字符定义了文件类型：
* `-` 表示文件
* `d` 表示目录
* `l` 表示链接
* `c` 表示字符设备
* `b` 表示块设备
* `s` 表示符号链接
* `p` 表示套接字
* `f` 表示命名管道

之后，有三组字符。每组定义了访问权限：
* `r` 表示读
* `w` 表示写
* `x` 表示执行

破折线 `-` 表示权限被拒绝。这三组分别对应所有者、所属组和所有人。

### 默认权限

你可能在好奇这些权限从哪里来。答案是 `umask`。`umask` 命令设置了你创建的任何文件的默认权限：

```
$ touch newfile
$ ls -l newfile
-rw-r--r-- 1 rich rich    0 2023-10-27 10:00 newfile
```

`touch` 命令创建了具有 `-rw-r--r--` 权限的文件。`umask` 是 `0022`：

```
$ umask
0022
```

`umask` 命令的设置并不直观，尝试理解它是如何工作的会让事情变得更复杂。第一个数字代表一个称为 `sticky bit` 的特殊功能。我们将在本章“共享文件”部分详细讨论。

接下来三个数字代表 `umask` 对文件或目录的八进制值。要理解 `umask` 如何工作，你首先需要理解八进制模式。

八进制模式安全设置将三个 `rwx` 权限值转换为 3 位二进制值，由单个八进制值表示。在二进制表示中，每个位置是一个二进制位：
* `r` = 4
* `w` = 2
* `x` = 1

如果只有读权限设置，值将变为 `r--`，对应二进制值 100，指示八进制值为 4。表 6.5 显示了你可能会遇到的所有组合：

| 权限 | 二进制 | 八进制 |
|---|---|---|
| `rwx` | 111 | 7 |
| `rw-` | 110 | 6 |
| `r-x` | 101 | 5 |
| `r--` | 100 | 4 |
| `-wx` | 011 | 3 |
| `-w-` | 010 | 2 |
| `--x` | 001 | 1 |
| `---` | 000 | 0 |

`umask` 命令通过“掩码”默认权限来工作。目录的最大权限是 777，文件的最大权限是 666。`umask` 值从这些最大值中减去以确定实际权限。例如，如果 `umask` 为 `0022`：
* 目录：`777 - 0022 = 775` (`drwxrwxr-x`) 
* 文件：`666 - 0022 = 644` (`-rw-r--r--`)

既然你已经了解了八进制模式权限，`umask` 值就变得更加复杂了。我的 Linux 系统上默认的 `umask` 显示的八进制模式为 `0022`，但我创建的文件八进制模式权限却是 `644`。这是如何发生的呢？

`umask` 值仅仅是一个掩码（mask）。它掩盖掉你不想授予某个安全级别的权限。现在，我们需要深入研究一些八进制运算，以揭开剩余的故事。

`umask` 值从对象的完整权限集中被减去。文件的完整权限是模式 `666`（所有人具有读/写权限），但对于目录，它是 `777`（所有人具有读/写/执行权限）。

因此，在示例中，文件初始权限为 `666`，应用 `022` 的 `umask` 后，剩余的文件权限为 `644`。

`umask` 值通常设置在 `/etc/profile` 启动文件中（见第 5 章）。你可以使用 `umask` 命令指定不同的默认 `umask` 设置：

```
$ umask 026
$ touch newfile2
$ ls -l newfile2
-rw-r-----     1 rich      rich               0 Sep 20 19:46 newfile2
$
```

通过将 `umask` 值设置为 `026`，默认文件权限变为 `640`，因此新文件现在对组成员限制只读，系统上的其他所有人对该文件没有权限。

`umask` 值也适用于创建新目录：

```
$ mkdir newdir
$ ls -l
drwxr-x--x     2 rich      rich               4096 Sep 20 20:11 newdir/
$
```

因为目录的默认权限是 `777`，通过 `umask` 产生的权限与新文件不同。`026` `umask` 值从 `777` 中减去，留下 `751` 的目录权限设置。

## 修改安全设置

如果你已经创建了文件或目录，并需要更改其安全设置，Linux 中提供了几种不同的工具。本节将向你展示如何更改文件或目录现有权限、默认所有者以及默认组设置。

### 修改权限

`chmod` 命令允许你更改文件和目录的安全设置。`chmod` 命令的格式为：

```
chmod [options] mode file
```

`mode` 参数允许你使用八进制模式或符号模式来设置安全设置。八进制模式设置非常直观；只需使用你希望文件拥有的标准三位八进制代码即可：

```
$ chmod 760 newfile
$ ls -l newfile
-rwxrw----    1 rich      rich               0 Sep 20 19:16 newfile
$
```

八进制文件权限会自动应用到指定的文件。符号模式权限的实现起来没有那么简单。

`chmod` 命令没有使用三组三个字符构成的普通字符串，而是采用了不同的方法。以下是在符号模式下指定权限的格式：

```
[ugoa…][[+-=][rwxXstugo…]
```

这听起来非常有道理，不是吗？第一组字符定义了新权限适用于谁：

*   `u` 代表用户（user）
*   `g` 代表组（group）
*   `o` 代表其他（others，即所有人）
*   `a` 代表以上所有（all）

接下来，使用一个符号来表示你想向现有权限中添加权限（`+`）、从现有权限中减去权限（`-`）或将权限设置为该值（`=`）。

最后，第三个符号是用于设置的权限。你可能会注意到，这里比通常的 `rwx` 值多。额外的设置包括：

*   `X`：仅当对象为目录或其已具有执行权限时，才分配执行权限
*   `s`：在执行时设置 UID 或 GID
*   `t`：保存程序文本（sticky bit）
*   `u`：将权限设置为所有者的权限
*   `g`：将权限设置为组权限
*   `o`：将权限设置为其他人的权限

使用这些权限的如下：

```
$ chmod o+r newfile
$ ls -l newfile
-rwxrw-r--    1 rich      rich               0 Sep 20 19:16 newfile
$
```

`o+r` 条目向“所有人”安全级别已有的任何权限添加了读权限。

```
$ chmod u-x newfile
$ ls -l newfile
-rw-rw-r--    1 rich      rich               0 Sep 20 19:16 newfile
$
```

`u-x` 条目移除了用户已拥有的执行权限。注意，`ls` 命令的设置通过在文件名后添加星号来指示文件是否具有执行权限。

`options` 参数提供了一些额外功能来增强 `chmod` 命令的行为。`-R` 参数执行递归的文件和目录更改。你可以在指定的文件名中使用通配符字符，仅需一个命令即可更改多个文件的权限。

### 修改所有权

有时你需要更改文件的所有者，例如当某人离开组织，或者开发者创建的应用在生产环境中需要由系统账户所有。Linux 提供了两个命令来实现这一点。`chown` 命令方便地更改文件的所有者，而 `chgrp` 命令允许你更改文件的默认组。

`chown` 命令的格式为：

```
chown [options] owner[.group] file
```

你可以为文件的新所有者指定登录名或数字 UID：

```
# chown dan newfile
# ls -l newfile
-rw-rw-r--    1 dan      rich               0 Sep 20 19:16 newfile
#
```

简单。`chown` 命令还允许你同时更改文件的用户和组：

```
# chown dan.shared newfile
# ls -l newfile
-rw-rw-r--    1 dan      shared               0 Sep 20 19:16 newfile
#
```

如果你真的想玩得复杂一点，可以只更改文件的默认组：

```
# chown .rich newfile
# ls -l newfile
-rw-rw-r--    1 dan      rich               0 Sep 20 19:16 newfile
#
```

最后，如果你的 Linux 系统使用独立的组名，你可以通过一个条目同时更改两者：

```
# chown test.shared newfile
# ls -l newfile
-rw-rw-r--    1 test     shared               0 Sep 20 19:16 newfile
#
```

`chown` 命令使用了一些选项参数。`-R` 参数允许你进行递归更改。`-h` 参数还会更改任何符号链接文件的所有权。

> 注意
> 只有 root 用户才能更改文件的所有者。任何用户都可以更改文件的默认组，但该用户必须是文件要切换的目标组的成员。

`chgrp` 命令提供了一种简单的方法来仅更改文件或目录的默认组：

```
$ chgrp shared newfile
```



`$ ls -l newfile`

```
-rw-rw-r--    1 rich      shared               0 Sep 20 19:16 newfile
$
```

现在，共享组中的任何成员都可以写入文件。这是在 Linux 系统上共享文件的方法之一。

## 共享文件

和你可能已经发现的，创建组是在 Linux 系统共享文件访问的方法。然而，对于完整的文件共享环境，情况更为复杂。

正如你在“解码文件权限”部分看到的，当你创建一个新文件时，Linux 使用你默认的 `UID` 和 `GID` 为新文件分配权限。为了允许他人访问文件，你需要更改“所有人”安全组的权限，或者为文件分配包含其他用户的不同默认组。如果你要在几个人之间创建并共享文档，这在大型环境中可能会很麻烦。幸运的是，有一个简单的方法来解决这个问题。

Linux 为每个文件和目录额外存储了三位信息：

*   设置用户 ID (`SUID`)：当文件被用户执行时，该程序以文件所有者的权限运行。
*   组 ID (`SGID`)：对于文件，程序将以文件所在组的权限运行。对于目录，在目录中创建的新文件将使用该目录组作为默认组。
*   粘滞位 (The sticky bit)：进程结束后，文件仍将保留（粘滞）在内存中。

`SGID` 位对于共享文件至关重要。通过启用 `SGID` 位，你可以强制在共享目录中创建的所有新文件都属于该目录的组，而不是个人用户的默认组。

`SGID` 使用 `chmod` 命令进行设置。它被添加到标准三位八进制值的开头（使其成为四位八进制值），或者你也可以在符号模式下使用符号 `s`。

如果你使用八进制模式，你将需要了解位位的排列情况，如 `Table 6.6` 所示。

### Table 6.6 `chmod` SUID、SGID 和粘滞位的八进制值

| 二进制 | 八进制 | 描述 |
| :--- | :--- | :--- |
| 000 | 0 | 所有位均清零。 |
| 001 | 1 | 设置了粘滞位。 |
| 010 | 2 | 设置了 `SGID` 位。 |
| 011 | 3 | 设置了 `SGID` 和粘滞位。 |
| 100 | 4 | 设置了 `SUID` 位。 |
| 101 | 5 | 设置了 `SUID` 和粘滞位。 |
| 110 | 6 | 设置了 `SUID` 和 `SGID` 位。 |
| 111 | 7 | 所有位均设置。 |

因此，要创建一个始终为所有新文件设置目录组的共享目录，你只需要为该目录设置 `SGID` 位：

```bash
$ mkdir testdir

$ ls -l
drwxrwxr-x    2 rich      rich           4096 Sep 20 23:12 testdir/

$ chgrp shared testdir

$ chmod g+s testdir

$ ls -l
drwxrwsr-x    2 rich      shared         4096 Sep 20 23:12 testdir/

$ umask 002

$ cd testdir

$ touch testfile

$ ls -l
total 0
-rw-rw-r--    1 rich      shared           0 Sep 20 23:13 testfile
$
```

第一步是使用 `mkdir` 命令创建一个你想共享的目录。接下来，使用 `chgrp` 命令将目录的默认组更改为包含需要共享文件的成员的组。最后，为目录设置 `SGID` 位，以确保在目录中创建的任何文件都使用共享组作为默认组。

为了让此环境正常工作，所有组成员都需要设置其 `umask` 值，以确保文件对组成员可写。在前面的示例中，`umask` 被更改为 `002`，以便组对文件有写权限。

完成所有操作后，组中的任何成员都可以进入共享目录并创建一个新文件。如所预期，新文件使用了目录的默认组，而不是用户账户的默认组。

## 总结

本章介绍了特殊文件位：`SUID`、`SGID` 和粘滞位。我们讨论了如何使用 `chmod` 命令通过八进制或符号模式设置这些位。我们还探索了如何使用 `SGID` 位和 `umask` 设置共享目录。

*   文件名
*   文件大小
*   文件所有者
*   文件所属组
*   文件的访问权限
*   指向包含文件数据的每个磁盘块的指针

Linux 使用唯一编号（称为 inode 编号）来引用 inode 表中的每个 `inode`，该编号是在创建数据文件时由文件系统分配的。文件系统使用 inode 编号来识别文件，而无需使用完整的文件名和路径。

## ext2 文件系统

原始的 `ext` 文件系统存在相当多的局限性，例如将文件大小限制为 `2GB`。在 Linux 首次引入后不久，`ext` 文件系统被升级为第二种扩展文件系统，称为 `ext2`。

正如你所猜到的那样，`ext2` 文件系统是 `ext` 文件系统基础能力的扩展，但保持了相同的结构。`ext2` 文件系统扩展了 inode 表的格式，以跟踪系统上每个文件的额外信息。

`ext2` inode 表为文件添加了创建时间、修改和最后访问时间的时间戳值，以帮助系统管理员跟踪系统上的文件访问。`ext2` 文件系统还将允许的最大文件大小增加到 `2TB`（在随后的 `ext2` 版本中，这被增加到了 `32TB`），以适应数据库服务器常见的大文件。

除了扩展 inode 表，`ext2` 文件系统还更改了文件在数据块中的存储方式。`ext` 文件系统的一个常见问题是，当文件写入物理设备时，用于存储数据的块往往分散在整个设备中（称为碎片）。数据块的碎片会降低文件系统的性能，因为搜索存储设备以访问特定文件的所有块需要更长时间。

`ext2` 文件系统通过在保存文件时分组分配磁盘块来帮助减少碎片。通过对文件的数据块进行分组，文件系统无需在整个物理设备上搜索数据块来读取文件。

多年来，`ext2` 文件系统一直是 Linux 的许多 Linux 发行版使用的默认文件系统，但它也有自己的局限性。inode 表虽然是一项允许文件系统跟踪文件额外信息的优秀功能，但可能会导致对系统是致命的问题。每当文件系统存储或更新文件时，它必须用新信息修改 inode 表。问题在于，这种操作并不总是流畅的。

如果在文件存储和 inode 表更新之间，计算机系统发生了任何故障，两者就会不同步。`ext2` 文件系统因由于系统崩溃和停电极易损坏而闻名。即使文件数据已良好存储在物理设备上，如果 inode 表条目未完成，`ext2` 文件系统甚至不知道该文件的存在！

不久后，开发者们开始探索 Linux 文件系统的另一种途径。

## 日志文件系统 (Journaling Filesystems)

日志文件系统为 Linux 系统提供了新级别的安全保障。日志文件系统不是直接将数据写入存储设备然后更新 inode 表，而是先将文件更改写入临时文件（称为日志）中。在数据成功写入存储设备和 inode 表后，日志项会被删除。

如果系统在数据写入存储设备之前发生崩溃或遭遇停电，日志文件系统只需读取日志文件并处理任何剩余未提交的数据。

Linux 中常用的有三种不同的日志方法，每种方法都有不同的保护级别。这些如表 7.1 所示。

### 表 7.1 日志文件系统方法

| 方法 | 说明 |
| :--- | :--- |
| 数据模式 | inode 和文件数据都会记录日志。丢失数据风险低，但性能差。 |
| 顺序模式 | 仅将 inode 数据写入日志，但在文件数据成功写入存储设备之前不会将其删除。性能和安全性之间的良好折中。 |
| 回写模式 | 仅将 inode 数据写入日志，不控制文件数据的写入时机。丢失数据风险较高，但仍优于不使用日志。 |

数据模式日志方法是目前保护数据最安全的方法，但也是最慢的。所有写入存储设备的数据必须写入两次，一次写入日志，然后再次写入实际存储设备。这可能导致性能低下，特别是对于进行大量数据写入操作的系统。

多年来，Linux 中出现了几种日志文件系统。接下来的章节描述了目前常用的 Linux 日志文件系统。

## 扩展 Linux 日志文件系统

作为 Linux 项目一部分开发了 `ext` 和 `ext2` 文件系统的同一小组还创建了文件系统的日志版本。这些日志文件系统与 `ext2` 文件系统兼容，并且很容易在它们之间来转换。目前有两个基于 `ext2` 文件系统的独立日志文件系统。

### ext3 文件系统

`ext3` 文件系统于 2001 年添加到 Linux 内核中，直到最近一直是几乎所有 Linux 发行版的默认文件系统。它使用与 `ext2` 文件系统相同的 inode 表结构，但在每个存储设备上添加了一个日志文件，以记录写入存储设备的数据。

默认情况下，`ext3` 文件系统使用顺序日志方法，仅将 inode 信息写入日志文件，但在数据块成功写入存储设备之前不将其删除。你可以在创建文件系统时，通过简单的命令行选项将 `ext3` 文件系统使用的日志方法更改为数据或回写模式。

虽然 `ext3` 文件系统为 Linux 文件系统增加了基础的日志功能，但它仍然缺少一些功能。例如，`ext3` 文件系统不提供对误删文件的恢复功能，没有内置的数据压缩（尽管可以单独安装一个提供此功能的补丁），并且 `ext3` 文件系统不支持加密文件。由于这些原因，Linux 项目的开发者选择继续工作改进 `ext3` 文件系统。

### ext4 文件系统

扩展 `ext3` 文件系统的结果（正如你可能猜到的那样）是 `ext4` 文件系统。`ext4` 文件系统于 2008 年在 Linux 内核中正式支持，现在是大多数流行 Linux 发行版（如 Fedora 和 Ubuntu）的默认文件系统。

除了支持压缩和加密，`ext4` 文件系统还支持一种名为 `extents` 的功能。`extents` 以块的形式在存储设备上分配空间，并在 inode 表中仅存储起始块位置。通过不再列出所有用于存储文件数据的数据块，节省了 inode 表中的空间。

`ext4` 文件系统还整合了块预分配功能。如果你想为一个已知大小会增长的文件在存储设备上预留空间，使用 `ext4` 文件系统可以为该文件分配所有预期的块，而不仅仅是物理上存在的块。`ext4` 文件系统用零填充预留的数据块，并知道不会将它们分配给任何其他文件。

### Reiser 文件系统

2001 年，Hans Reiser 创建了 Linux 的第一个日志文件系统，称为 `ReiserFS`。`ReiserFS` 文件系统仅支持回写日志模式，仅将 inode 表数据写入日志文件。由于它只向日志写入 inode 表数据，`ReiserFS` 文件系统是 Linux 中最快的日志文件系统之一。

`ReiserFS` 文件系统整合了两个有趣的特性：你可以在文件系统处于活动状态时对其进行大小调整；它使用了一种名为“尾部填充”（tailpacking）的技术，该技术可以将一个文件的数据填充到另一个文件数据块的空隙中。活动文件系统缩放功能对于你需要扩展已创建的文件系统以容纳更多数据的情况非常有用。

> 警告
> 由于 Hans Reiser 的法律纠纷，`ReiserFS` 文件系统的状态尚存疑点。虽然 `ReiserFS` 项目是一个开源项目，但 Hans 曾是该项目的首席开发人员，目前已入狱。`ReiserFS` 文件系统最近没有进行任何开发，尚不清楚是否还会其他人接手该项目的开发工作。鉴于现在有了其他日志文件系统的替代方案，绝大多数新的 Linux 安装程序不再使用 `ReiserFS` 文件系统。然而，你仍然可能会遇到在使用该系统的现有 Linux 系统。

## 日志文件系统 (Journaled Filesystem)

可能是最古老的日志文件系统之一，日志文件系统（`JFS`）由 IBM 在 1990 年为其 AIX 版本的 Unix 开发。然而，直到第二个版本出现，它才被移植到 Linux 环境。

> 注意
> `JFS` 文件系统的第二个版本的 IBM 官方名称是 `JFS2`，但大多数 Linux 系统仅将其称为 `JFS`。

`JFS` 文件系统使用顺序日志方法，仅在日志中存储索引节点表（inode table）数据，但在实际文件数据写入存储设备之前，不会将其删除。这种方法是在 `ReiserFS` 的速度和数据模式日志方法的数据完整性之间取得的一种折中方案。

`JFS` 文件系统使用基于区（extent-based）的文件分配方法，为写入存储设备的每个文件分配一组块。这种方法可以减少存储设备上的碎片。

在 IBM 提供的 Linux 产品之外，`JFS` 文件系统并不流行，但在你的 Linux 之旅中，你可能会遇到它。

## XFS 文件系统

`XFS` 日志文件系统是另一个最初为商用 Unix 系统创建并最终进入 Linux 世界的文件系统。硅谷图形公司（`SGI`）于 1994 年为其商用 `IRIX` Unix 系统创建了 `XFS`。它于 2002 年发布到 Linux 环境供通用使用。

`XFS` 文件系统使用日志的回写模式（writeback mode），这种模式提供了高性能，但也引入了一定风险，因为实际数据并未存储在日志文件中。`XFS` 文件系统还允许对文件系统进行在线大小调整，与 `ReiserFS` 文件系统类似，不同之处 `XFS` 文件系统只能扩展而不能缩小。

## 与文件系统的操作

Linux 提供了几个不同的实用程序，使得从命令行操作文件系统变得更容易。你可以轻松地通过键盘添加新文件系统或更改现有的文件系统。本节将带你熟悉从命令行环境与文件系统交互的命令。

## 创建分区

开始之前，你需要在存储设备上创建一个分区以包含文件系统。该分区可以是整个磁盘，也可以是磁盘的子集，包含虚拟目录的一部分。

`fdisk` 工具用于帮助你对安装在系统上的任何存储设备进行分区组织。`fdisk` 命令是一个交互式程序，允许你输入命令来完成硬盘分区的各个步骤。

要启动 `fdisk` 命令，你需要指定想要分区的存储设备的设备名称：

```
$ sudo fdisk /dev/sdc
```

```
[sudo] password for rich:

Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x4beedc66.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)
WARNING: DOS-compatible mode is deprecated. It's strongly recommended
        To switch off the mode (command ‘c') and change display units to sectors (command ‘u’).

Command (m for help):
```

如果你是第一次对存储设备进行分区，`fdisk` 会给你一个警告，说明设备上没有分区表。

`fdisk` 交互式提示符使用单字母命令指示 `fdisk` 执行什么。表 7.2 显示了 `fdisk` 提示符处的可用命令。

### 表 7.2 命令

| 命令 | 说明 |
| :--- | :--- |
| `a` | 切换可启动标志 |
| `b` | 编辑磁盘标签 |
| `c` | 切换 DOS 兼容标志 |
| `d` | 删除分区 |
| `l` | 列出分区 |
| `m` | 显示帮助 |
| `n` | 添加新分区 |
| `o` | 创建 DOS 分区表 |
| `p` | 显示分区表 |
| `q` | 在不保存更改退出 |
| `s` | 修改分区系统 ID |
| `u` | 更改显示单位 |
| `v` | 验证分区表 |
| `w` | 将分区表写入磁盘 |
| `x` | 高级功能 |

虽然这个列表看起来很复杂，但在日常工作中你通常只会使用几个基本命令。

首先，你可以使用 `p` 命令显示存储设备的详情：

```
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368946688 bytes
255 heads, 63 sectors/track, 652 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x4beedc66

    Device Boot      Start          End      Blocks

Command (m for help):
```

输出结果显示存储设备上有 5368MB 的空间。存储设备详情下的列表显示了设备上是否存在分区。示例列表中没有显示任何分区，因此设备尚未进行分区。

接下来，你想在存储设备上创建一个新分区。使用 `n` 命令：

```
Command (m for help): n

Command action
    e   extended
    p   primary partition (1-4)
p

Partition number (1-4): 1

First cylinder (1-652, default 1): 1

Last cylinder, +cylinders or +size{K,M,G} (1-652, default 652): +2G

Command (m for help):
```



分区可以创建为主分区或扩展分区。主分区可以格式化为文件系统，而扩展分区只能包含主分区。设置扩展分区是因为单个设备只能四个分区。你可以通过创建多个扩展分区然后在扩展分区内创建主分区来扩展这一点。此示例创建一个主存储设备，将其分配为存储设备上的分区 1，然后为其分配 2GB 的存储设备空间。你可以再次使用 `p` 命令查看结果：

```
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368946688 bytes

255 heads, 63 sectors/track, 652 cylinders

Units = cylinders of 16065 * 512 = 8225280 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x4beedc66

    Device Boot      Start          End      Blocks    Id  System

/dev/sdc1               1            262    2104483+83  Linux

Command (m for help):
```

现在输出中存储设备上出现了一个分区（称为 `/dev/sdc1`）。`Id` 条目定义了 Linux 如何处理该分区。`fdisk` 允许你创建许多分区类型。使用 `l` 命令可以列出所有可用类型。默认类型是 83，它定义为 Linux 文件系统。如果你想为不同的文件系统（例如 Windows NTFS 分区）创建分区，只需选择不同的分区类型。

你可以重复此过程，将存储设备的剩余空间分配给另一个 Linux 分区。在创建好所需的分区后，使用 `w` 命令将更改保存到存储设备：

```
Command (m for help): w

The partition table has been altered!

Calling ioctl() to re-read partition table.

Syncing disks.

$
```

现在存储设备上已经有了分区，你可以准备好用 Linux 文件系统对其进行格式化了。

> 注意
> 有时创建新磁盘分区最困难的部分是尝试在 Linux 系统中寻找物理磁盘。Linux 使用标准格式为硬盘分配设备名称，但你需要熟悉该格式。对于较旧的 IDE 驱动器，Linux 使用 `/dev/hdx`，其中 `x` 是根据驱动器检测顺序指定的字母（第一个为 a，第二个为 b，以此类推）。对于较新的 SATA 驱动器和 SCSI 驱动器，Linux 都使用 `/dev/sdx`，其中 `x` 是根据驱动器检测顺序指定的字母（同样，第一个为 a，第二个为 b，以此类推）。在格式化分区之前，双重检查确保你引用的是正确的硬盘始终是一个好习惯！

## 创建文件系统

在分区上存储数据之前，你必须用文件系统对其进行格式化，以便 Linux 使用它。每种文件系统类型都有自己的命令行程序来格式化分区。表 7.3 列出了本章讨论的各种文件系统所用用的工具。

### 表 7.3 创建文件系统的命令行程序

| 工具 | 用途 |
| :--- | :--- |
| `mke2fs` | 创建 ext 文件系统。 |
| `mkfs.ext3` | 创建 ext3 文件系统。 |
| `mkfs.ext4` | 创建 ext4 文件系统。 |
| `mkreiserfs` | 创建 ReiserFS 文件系统。 |
| `jfs_mkfs` | 创建 JFS 文件系统。 |
| `mkfs.xfs` | 创建 XFS 文件系统。 |

每个文件系统命令都有许多命令行选项，允许你自定义文件系统在分区中的创建方式。要查看所有可用的命令行选项，请使用 `man` 命令显示文件系统命令的手页（参见第 2 章）。所有的文件系统命令都允许你仅通过简单的无带选项命令来创建默认文件系统：

```
$ sudo mkfs.ext4 /dev/sdc1

[sudo] password for rich:

mke2fs 1.41.11 (14-Mar-2010)

Filesystem label=

OS type: Linux

Block size=4096 (log=2)

Fragment size=4096 (log=2)

Stride=0 blocks, Stripe width=0 blocks

131648 inodes, 526120 blocks

26306 blocks (5.00%) reserved for the super user

First data block=0

Maximum filesystem blocks=541065216

17 block groups

32768 blocks per group, 32768 fragments per group

7744 inodes per group

Superblock backups stored on blocks:

      32768, 98304, 163840, 229376, 294912

Writing inode tables: done

Creating journal (16384 blocks): done

Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 34 mounts or 180 days, whichever comes first. Use tune2fs -c or -i to override.

$
```

新文件系统使用了 `ext4` 文件系统类型，这是 Linux 中的带日志功能文件系统。请注意，创建过程的一部分是创建新的日志。

在你为分区创建文件系统后，下一步将其挂载到虚拟目录中的挂载点，这样你就可以在新文件系统中存储数据了。你可以在虚拟目录中任何需要额外空间挂载新文件系统。

```
$ sudo mkdir /mnt/testing

$ sudo mount -t ext4 /dev/sdb1 /mnt/testing

$ ls -al /mnt/testing

total 24

drwxr-xr-x 3 root root  4096 2010-09-25 19:25 .

drwxr-xr-x 3 root root  4096 2010-09-25 19:38 ..

drwx------ 2 root root 16384 2010-09-25 19:25 lost+found

$
```

`mkdir` 命令在虚拟目录中创建挂载点，而 `mount` 命令将新的硬盘分区添加到挂载点。现在你可以在新分区上保存新文件和文件夹了！

> 警告
> 这种挂载文件系统的方法只是临时挂载。当你重启 Linux 系统时，文件系统不会自动挂载。要强迫 Linux 在启动时自动挂载新文件系统，请将新文件系统添加到 `/etc/fstab` 文件。

本章展示了如何处理包含在物理存储设备中的文件系统。Linux 还提供了几种不同的方法来为文件系统创建逻辑存储设备。下一节将介绍你如何为你的文件系统使用逻辑存储设备。

## 如果出现问题

即使使用了高级的日志文件系统，如果意外断电，或者某个异常应用程序在文件访问期间锁定了系统，情况也可能变得糟糕。幸运的是，有一些命令行工具可以帮助你尝试将文件系统恢复正常。

每个文件系统都有自己的用于与文件系统交互的恢复命令。这可能会变得复杂，因为 Linux 环境中可用的文件系统越来越多，导致你必须了解许多单独的命令。幸运的是，有一个通用的前端程序，它可以确定存储设备上的文件系统，并根据该文件系统使用相应的文件系统恢复命令。

`fsck` 命令用于检查并修复任何类型的 Linux 文件系统，包括本章之前讨论的所有类型 ext、ReiserFS、JFS 和 XFS。命令的格式为：

```
fsck options filesystem
```

你可以在命令行中列出多个要检查的文件系统。可以使用设备名、虚拟目录中的挂载点或分配给文件系统的特殊 UUID 值来引用文件系统。

`fsck` 命令使用 `/etc/fstab` 文件来自动确定系统中通常挂载的存储设备的文件系统。如果存储设备没有通常挂载（例如你在新存储设备上创建了文件系统），你需要使用 `-t` 命令行选项指定文件系统类型。表 7.4 列出了其他可用的命令行选项。

### 表 7.4 fsck 命令行选项

| 选项 | 说明 |
| :--- | :--- |
| `-a` | 检测到错误时自动修复文件系统。 |
| `-A` | 检查 `/etc/fstab` 文件列出的所有文件系统。 |
| `-C` | 为支持该功能的文件系统显示进度条（仅 `ext2` 和 `ext3`）。 |
| `-N` | 不运行检查，仅显示将执行哪些检查。 |
| `-r` | 发现错误时提示进行修复。 |
| `-R` | 使用 `-A` 选项时跳过根文件系统。 |
| `-s` | 如果检查多个文件系统，则逐个执行检查。 |
| `-t` | 指定要检查的文件系统类型。 |
| `-T` | 在启动时不显示页头信息。 |
| `-V` | 在检查期间产生详细输出。 |
| `-y` | 检测到错误时自动修复文件系统。 |

你可能会注意到某些命令行选项是冗余的。这是尝试为多个命令实现通用前端时产生的问题之一。某些单独的文件系统修复命令具有可以使用的额外选项。如果你需要进行更高级的错误检查，你需要检查各个文件系统修复工具的帮助页（man pages），以查看是否有针对特定文件系统的扩展选项。

> 警告
> 你可以仅在未挂载的文件系统上运行 `fsck` 命令。对于大多数文件系统，你只需要卸载该文件系统进行检查，然后在完成后重新挂载即可。然而，由于根文件系统包含了所有的核心 Linux 命令和日志文件，你无法在运行中的系统上卸载它。

> 这正是使用 Linux LiveCD 派上用场的时候！只需使用 LiveCD 启动系统，然后在根文件系统上运行 `fsck` 命令即可！

# 逻辑卷管理器 (Logical Volume Managers)

如果你使用硬盘上的标准分区来创建文件系统，那么尝试为现有文件系统添加额外空间可能是相当痛苦的体验。你只能在同一物理硬盘的可用空间范围内扩展分区。如果该硬盘上没有更多可用空间，你就只能更换一个更大的硬盘，并手动将现有文件系统移动到新硬盘上。

非常有用的方法是：通过从另一个硬盘添加分区到现有文件系统，来动态地为现有文件系统添加更多空间。Linux 逻辑卷管理器（`LVM`）软件包允许你实现这一点。它提供了一种简单的方法，让你可以在 Linux 系统上操纵磁盘空间，而无需重新构建整个文件系统。

## 逻辑卷管理布局

逻辑卷管理的核心的核心在于它如何处理安装在系统上的物理硬盘分区。在逻辑卷管理领域，硬盘被称为物理卷（`PV`）。每个 `PV` 映射到硬盘上的一个特定物理分区。

多个 `PV` 元素被组合在一起创建一个卷组（`VG`）。逻辑卷管理系统将 `VG` 视为物理硬盘，但实际上 `VG` 可能由分布在多个硬盘上的多个物理分区组成。`VG` 提供创建一个逻辑分区的平台，这些逻辑分区实际上包含了文件系统。

结构中的最后一层是逻辑卷（`LV`）。`LV` 为 Linux 创建文件系统提供了分区环境，就 Linux 而言，它的作用类似于物理硬盘分区。Linux 系统对待 `LV` 就像对待物理分区一样。你可以使用任何标准 Linux 文件系统来格式化 `LV`，然后将其挂载到 Linux 虚拟目录的挂载点。

图 7.1 显示了典型的 Linux 逻辑卷管理环境的基础布局。

图 7.1 逻辑卷管理环境

![](img/00066.jpg)

[图 7.1]中所示的卷组跨越三个独立的物理硬盘，涵盖五个独立的物理分区。卷组内部有两个独立的逻辑卷。Linux 系统对待每个逻辑卷就像对待物理分区一样。每个逻辑卷都可以格式化为 `ext4` 文件系统，然后挂载到虚拟目录中的特定位置。

注意[图 7.1]，第三块物理硬盘有一个未使用的分区。使用逻辑卷管理，你可以在稍后轻松地将此未使用的分区分配给现有的卷组，然后使用它来创建新的逻辑卷，或者在需要更多空间时将其添加以扩展现有的逻辑卷之一。

同样，如果你向系统添加了新硬盘，本地卷管理系统允许你将其添加到现有的卷组中，然后为一个现有的逻辑卷创建更多空间，或者启动一个新的逻辑卷进行挂载。这是一种处理扩展文件系统好得多的方法！

## Linux 中的 LVM

Linux `LVM` 由 Heinz Mauelshagen 开发并于 1998 年发布给 Linux 社区。它允许你使用简单的命令行在 Linux 中管理完整的逻辑卷管理环境。

有两个版本的 Linux `LVM` 可用：

* `LVM1`：1998 年发布的原始 `LVM` 软件包，仅在 2.4 Linux 内核中可用。它只提供基本的逻辑卷管理功能。
* `LVM2`：`LVM` 的更新版本，适用于 2.6 Linux 内核。它在标准 `LVM1` 功能的基础上提供了额外功能。

大多数使用 2.6 内核版本的现代 Linux 发行版都提供了对 `LVM2` 的支持。除了标准的逻辑卷管理功能外，`LVM2` 还提供了其他可以在 Linux 系统使用的优秀功能。

### 快照 (Snapshots)

原始的 Linux `LVM` 允许你在逻辑卷激活状态下将现有逻辑卷复制到另一个设备上。此功能被称为快照。快照对于备份由于高可用性要求而无法锁定的重要数据非常好。传统的备份方法通常在文件复制到备份介质时会锁定文件。快照允许你在执行复制的同时继续运行关键任务的 Web 或数据库服务器。遗憾的是，`LVM1` 仅允许你创建只读快照。一旦创建了快照，你就无法向其写入数据。

`LVM2` 允许你为活动中的逻辑卷创建读写快照。通过读写副本，你可以移除原始逻辑卷并将快照作为替换。此功能对于快速故障转移（fail-overs），或者对于测试修改数据的应用程序非常有用，如果发生故障，数据可能需要恢复）。

### 条带化 (Striping)

`LVM2` 提供的另一个有趣功能是条带化。通过条带化，逻辑卷跨越多个物理硬盘创建。当 Linux `LVM` 向逻辑卷写入文件时，文件中的数据块将分散在多个硬盘上。每个连续的数据块被写入下一块硬盘。

条带化有助于提高磁盘性能，因为 Linux 可以同时向多个硬盘写入一个文件的多个数据块，而无需等待单个硬盘移动读写头到不同位置。这种改进也适用于顺序访问的文件，因为 `LVM` 可以同时从多个硬盘读取数据。

> 警告
> `LVM` 条带化不等同于 RAID 条带化。`LVM` 条带化不提供用于校验项（parity entry），因此无法创建容错环境。事实上，`LVM` 条带化可能会增加由于硬盘故障导致文件丢失的可能性。单个磁盘故障可能导致多个逻辑卷无法访问。

### 镜像 (Mirroring)

仅仅因为使用 `LVM` 安装了文件系统，并不意味着文件系统仍然不会出现问题。就像物理分区一样，`LVM` 逻辑卷也受到断电和磁盘崩溃的影响。一旦文件系统损坏，始终存在无法恢复它的可能。

`LVM` 快照过程提供了一些心理安慰，让你知道可以在任何时候创建逻辑卷的备份副本，但对于某些环境来说，这可能还不够。具有大量数据变化的系统（例如数据库服务器）自上次快照以来可能存储了成千上万条记录。

解决此问题的方案是 `LVM` 镜像。镜像是逻辑卷的完整副本，并实时更新。当你创建镜像逻辑卷时，`LVM` 会将原始逻辑卷同步到镜像副本。取决于原始逻辑卷的大小，这可能需要一些时间才能完成。

一旦原始同步完成，`LVM` 会对文件系统的每个写入过程执行两次写入——一次写入主逻辑卷，另写入镜像副本。正如你所料的，这个过程确实会减慢系统的写入性能。然而，如果原始逻辑卷由于某种原因发生损坏，你手中就会有一个完整且最新的副本！

## 使用 Linux LVM

现在你已经了解了 Linux LVM 的功能，本节将讨论如何实现它来帮助组织你系统上的磁盘空间。Linux LVM 软件包仅提供了命令行程序，用于创建和管理逻辑卷管理系统中的所有组件。某些 Linux 发行版包含了这些命令行命令的图形化前端，但为了完全控制你的 LVM 环境，最好最好习惯于直接使用命令操作。

## 定义物理卷 (Physical Volumes)

该过程的第一步是将硬盘上的物理分区转换为 Linux LVM 使用的物理卷区（physical volume extents）。我们的朋友 `fdisk` 命令将在此处提供帮助。在创建基础 Linux 分区后，你需要使用 `t` 命令更改分区类型：

```
Command (m for help): t

Selected partition 1

Hex code (type L to list codes): 8e

Changed system type of partition 1 to 8e (Linux LVM)

Command (m for help): p

Disk /dev/sdc: 2147 MB, 2147992064 bytes

255 heads, 63 sectors/track, 261 cylinders

Units = cylinders of 16065 * 512 = 8225280 bytes

Disk identifier: 0x4bc26133

Device Boot      Start           End         Blocks    Id  System

/dev/sdc1             1          261     2096451   8e  Linux LVM

Command (m for help):
```



`8e`分区类型表示该分区将作为 Linux LVM 系统的一部分，而不是直接作为文件系统，正如你之前看到的`83`分区类型那样。

下一步是使用该分区创建实际物理卷。这是通过`pvcreate`命令完成的：

```
$ sudo pvcreate /dev/sdc1

  Physical volume "/dev/sdc1" successfully created

$
```

`pvcreate`命令定义了用于 PV 的物理卷。它简单地将该分区标记为 Linux LVM 系统中的物理卷。如果你想查看在此的进度，可以使用`pvdisplay`命令显示你已创建的物理卷列表。

## 创建卷组 (Volume Groups)

该过程的下一步是根据物理卷创建一个或多个卷组。对于系统需要创建多少个卷组，没有固定的规则——你可以将所有可用的物理卷添加到单个卷组，也可以通过组合不同的物理卷创建多个卷组。

要从命令行创建卷组，你需要使用`vgcreate`命令。`vgcreate`命令需要几个命令行参数来定义卷组名称，以及你用于创建卷组的物理卷名称：

```
$ sudo vgcreate Vol1 /dev/sdc1

  Volume group "Vol1" successfully created

$
```

输出的内容没那么令人兴奋！如果你想查看有关新创建卷组的细节，可以使用`vgdisplay`命令：

```
$ sudo vgdisplay

  --- Volume group ---

  VG Name             Vol1

  System ID            

  Format              lvm2

  Metadata Areas       1

  Metadata Sequence No  1

  VG Access            read/write

  VG Status            resizable

  MAX LV              0

  Cur LV              0

  Open LV              0

  Max PV              0

  Cur PV              1

  Act PV              1

  VG Size              2.00 GB

  PE Size              4.00 MB

  Total PE             511

  Alloc PE / Size      0 / 0   

  Free  PE / Size      511 / 2.00 GB

  VG UUID             CyilHZ-Y840-8TUn-Wvti-4S6Q-bHHT-C113I0

$
```

此示例创建了一个名为`Vol1`的卷组，使用了在`/dev/sdc1`分区上创建的物理卷。

现在你已经有一个或多个卷组，可以创建逻辑卷了。

## 创建逻辑卷 (Logical Volumes)

逻辑卷是 Linux 系统用于模拟物理分区并存放文件系统的结构。Linux 系统处理逻辑卷就像处理物理分区一样，允许你在逻辑卷中定义文件系统，并将文件系统挂载到虚拟目录中。

要创建逻辑卷，请使用`lvcreate`命令。虽然你可以不使用选项完成，但`lvcreate`命令至少需要一些：

```
Fragment size=4096 (log=2)

130816 inodes, 523264 blocks

26163 blocks (5.00%) reserved for the super user

First data block=0

Maximum filesystem blocks=536870912

16 block groups

32768 blocks per group, 32768 fragments per group

8176 inodes per group

Superblock backups stored on blocks:

    32768, 98304, 163840, 229376, 294912

Writing inode tables: done

Creating journal (8192 blocks): done

Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 21 mounts or 180 days, whichever comes first. Use `tune2fs -c` or `-i` to override.

$
```

创建新文件系统后，你可以使用标准的 Linux `mount`命令将卷挂载到虚拟目录中，就像对待物理分区一样。唯一的区别在于，你使用了一个标识逻辑卷的特殊路径：

```
$ sudo mount /dev/Vol1/lvtest test

$ cd test

$ ls -al

total 24

drwxr-xr-x. 3 root root 4096 2010-09-17 17:36 .

drwx------. 33 rich rich 4096 2010-09-17 17:37 ..

drwx------. 2 root root 16384 2010-09-17 17:36 lost+found
```

注意，`mkfs.ext4`和`mount`命令中使用的路径稍显奇怪。它没有使用物理分区路径，而是使用了卷组名称加上逻辑卷名称。一旦挂载文件系统，你就可以在虚拟目录中访问该新区域。

## 修改 LVM

由于使用 Linux LVM 的好处是可以动态修改文件系统，因此你可能会有某些工具允许你执行此操作。Linux 中提供了一些工具，允许你修改现有的逻辑卷管理配置。

如果你没有用于管理 Linux LVM 环境的高级图形界面，也不必绝望。在本章中，你已经看到了一些 Linux LVM 命令行程序的实际应用。在安装 LVM 后，你还可以使用许多其他命令行程序来管理 LVM 设置。表 7.6 列出了 Linux LVM 软件包中提供的常用命令。

### 表 7.6 Linux LVM 命令

| 命令 | 功能 |
| :--- | :--- |
| `vgchange` | 激活和停用卷组 |
| `vgremove` | 移除卷组 |
| `vgextend` | 向卷组中添加物理卷 |
| `vgreduce` | 从卷组中移除物理卷 |
| `lvexend` | 增加逻辑卷的大小 |
| `lvreduce` | 减小逻辑卷的大小 |

通过这些命令行程序，你对自己的 Linux LVM 环境拥有完全控制权。

> **警告**
> 在手动增加或减小逻辑卷大时要小心。存储在逻辑卷中的文件系统需要手动修复以处理大小的变化。大多数文件系统都包含了用于重新格式化文件系统的命令行程序，例如用于 ext2 和 ext3 文件系统的`resize2fs`程序。

## 总结

在 Linux 中处理存储设备需要你了解一些文件系统。了解如何从命令行创建和操作文件系统，在你操作 Linux 系统时会非常有帮助。本章讨论了如何从 Linux 命令行处理文件系统。

Linux 系统与 Windows 的不同在于，它支持许多不同的存储文件文件夹的方法。每种文件系统方法都有不同的特性，使其适用于不同的场景。此外，每种文件系统方法使用不同的命令与存储设备进行交互。

在存储设备上安装文件系统之前，你必须先准备设备。使用`fdisk`命令对存储设备进行分区，以便为文件系统做好准备。当你对存储设备进行分区时，必须定义文件系统的类型。

---

# 第 8 章：安装软件

## 本章内容

*   安装软件
*   使用 Debian 包
*   使用 Red Hat 包

在 Linux 的早期，安装软件可能是一种痛苦的经历。坦率地说，Linux 开发者通过将软件打包成更易安装的预构建包，让我们的生活变得更轻松。然而，在安装软件方面我们仍然需要做一些工作，特别是如果你想从命令行进行此操作。

## 软件包管理入门

在深入 Linux 软件包管理世界之前，本章首先介绍一些基础知识。每种主要的 Linux 发行版都使用某种形式的`软件包管理系统`（PMS）来控制软件应用程序和库的安装。PMS 利用数据库来跟踪以下信息：

*   Linux 系统上安装了哪些软件包
*   每个软件包安装了哪些文件
*   每个软件包的版本

软件包存储在称为“仓库”（repositories）的服务器上，并通过运行在你本地 Linux 系统上的 PMS 工具跨越网络访问。你可以使用 PMS 工具搜索新的软件包，甚至对系统中已有的软件包进行更新。

一个软件软件包通常具有依赖关系，或者必须先安装其他软件包才能使该软件正常运行。PMS 工具会检测这些依赖关系，并在安装所需的程序包之前，提议安装任何额外需要的软件包。

PMS 的缺点是没有统一的标准。虽然书中到目前为止讨论的所有 bash shell 命令无论你使用哪种 Linux 发行版都能工作，但对于软件包管理来说，并非如此。

在不同的 Linux 发行版之间，PMS 工具及其相关命令有巨大差异。Linux 世界中常用的两种主要 PMS 基础工具是`dpkg`和`rpm`。

基于 Debian 的发行版（如 Ubuntu 和 Linux Mint）在其 PMS 工具的底层使用`dpkg`命令。该命令直接与 Linux 系统上的 PMS 交互，用于安装、管理和删除软件包。

基于 Red Hat 的发行版（如 Fedora、openSUSE 和 Mandriva）在其 PMS 的底层使用`rpm`命令。与`dpkg`命令类似，`rpm`命令可以列出已安装软件包、安装新软件包并删除现有的软件。

请注意，这两个命令是各自软件包管理系统（PMS）的核心，而不是整个 PMS 本身。许多使用`dpkg`或`rpm`方法的 Linux 发行版在这些命令的基础上构建了额外的特殊 PMS 工具，以帮助你的工作变得更加轻松。接下来的章节将介绍你在流行的 Linux 发行版中会遇到的各种 PMS 工具命令。

## 基于 Debian 的系统

`dpkg`命令是 Debian 系 PMS 工具的核心。该 PMS 包含的其他工具还包括：

* `apt-get`
* `apt-cache`
* `aptitude`

到目前为止，最常用的命令行工具是`aptitude`，这有其原因。`aptitude`工具本质上是`apt`工具和`dpkg`的前端。如果说`dpkg`是一个 PMS 工具，那么`aptitude`就是一个完整的软件包管理系统。

在命令行中使用`aptitude`命令将帮助你避免常见的软件安装问题，例如缺少软件依赖项、系统环境不稳定以及大量不必要的麻烦。本节将介绍如何从 Linux 命令行使用`aptitude`工具。

### 使用 aptitude 管理软件包

Linux 系统管理员经常面临的一项任务是确定系统中已经安装了哪些软件包。坦率地说，`aptitude`拥有一个实用的交互界面，让这项任务变得非常简单。

在 shell 提示符处输入`aptitude`并按回车。你将进入 aptitude 的全屏模式，如图 8.1 所示。

图 8.1 aptitude 主窗口

![](img/00026.jpg)

使用方向键移动菜单。选择菜单选项`Installed Packages`查看已安装的软件包。你会看到几组软件包，例如编辑器等。每组后面都有一个数字，表示该组包含软件包的数量。

使用方向键高亮一组并按回车查看软件包的每个子组。你将看到单个软件包的名称及其版本号。在单个软件包上按回车获取非常详细的信息，例如软件包的描述、主页、大小、维护者等。

查看完已安装的软件包后，按`q`退出显示。然后你可以回到方向键并使用回车切换软件包及其子组的打开或关闭。全部完成后，只需连续按多次`q`直到弹出屏幕“Really quit Aptitude?”（确定退出 Aptitude 吗？）。

已经熟悉系统中的软件包并想快速显示特定软件包的详细信息，无需进入 aptitude 的交互界面。你可以在命令行中将`aptitude`作为单命令使用：

`aptitude show package_name`

这是一个显示软件包`grub2-theme-mint`信息的示例：

```
$ aptitude show grub2-theme-mint

Package: grub2-theme-mint

New: yes

State: installed

Automatically installed: no

Version: 1.0.3

Priority: optional

Section: misc

Maintainer: Clement Lefebvre <root@linuxmint.com>

Uncompressed Size: 442k

Description: Grub2 theme for Linux Mint

 Grub2 theme for Linux Mint

$
```

> 注意
> `aptitude show`命令并不表示该软件包已安装在系统中。它仅显示来自软件仓库的详细软件包信息。

你无法通过`aptitude`获取的一个细节是特定软件包相关的文件列表。要获取此列表，你需要使用`dpkg`工具本身：

`dpkg -L package_name`

这是一个使用`dpkg`列出作为`grub2-theme-mint`软件包一部分安装的所有文件的示例：

```
$ dpkg -L grub2-theme-mint

/.

/boot

/boot/boot

/boot/boot/grub

/boot/boot/grub/linuxmint.png

/boot/grub

/boot/grub/linuxmint.png

/usr

/usr/share

/usr/share/doc

/usr/share/doc/grub2-theme-mint

/usr/share/doc/grub2-theme-mint/changelog.gz

/usr/share/doc/grub2-theme-mint/copyright

/etc

/etc/grub.d

/etc/grub.d/06_mint_theme

$
```

你也可以反过来操作——查找特定文件属于哪个软件包：

`dpkg --search absolute_file_name`

请注意，你需要使用绝对文件引用才能使其生效：

```
$ dpkg --search /boot/grub/linuxmint.png

grub2-theme-mint: /boot/grub/linuxmint.png

$
```

输出显示`linuxmint.png`文件作为`grub2-theme-mint`软件包的一部分安装的。

### 使用 aptitude 安装软件软件包

现在你已经更了解如何列出系统上的软件包信息，本节将介绍软件包的安装过程。首先，你需要确定要安装的软件包名称。如何找到特定的软件软件包？使用带有搜索选项的`aptitude`命令：

`aptitude search package_name`

搜索选项的巧妙之处在于，你不需要`package_name`周围插入通配符。通配符是隐含的。这是一个使用`aptitude`查找`wine`软件软件包的示例：

```
$ aptitude search wine

p   gnome-wine-icon-theme          - red variation of the GNOME- ...

v   libkwineffects1-api              - 

p   libkwineffects1a                 - library used by effects...

p   q4wine                           - Qt4 GUI for wine (W.I.N.E) 

p   shiki-wine-theme                - red variation of the Shiki- ...

p   wine                             - Microsoft Windows Compatibility ...

p   wine-dev                        - Microsoft Windows Compatibility ...

p   wine-gecko                      - Microsoft Windows Compatibility ...

p   wine1.0                          - Microsoft Windows Compatibility ...

p   wine1.0-dev                     - Microsoft Windows Compatibility ...

p   wine-gecko                      - Microsoft Windows Compatibility ...

... (为了简洁起见已省略，遵循提供的文本)
```



（注：提供的源文本在搜索输出中有一些重复行；我按照要求保留了命令和变量的格式逻辑）。

注意每个名称之前之前是`p`或`i`。如果你看到`u`，意味着该软件包目前已安装。如果你看到`p`，意味着它是可用的。从输出中可以看出，此系统没有`wine`，但该软件包是可用的。

使用`aptitude`从仓库安装软件包非常简单：

```
aptitude install package_name
```

一旦你从搜索中找到软件包名称，只需使用安装选项将其接入`aptitude`命令即可：

```
$ sudo aptitude install wine
```

```
* 启动 Winbind 进程 winbind
[ OK ]
Setting up wine (1.2-0ubuntu5) ...
Setting up gnome-exe-thumbnailer (0.6-0ubuntu1) ...
Processing triggers for libc-bin ...
ldconfig deferred processing now taking place
$
```

> 注意事项
> > 在上述列表的`aptitude`命令之前，使用了`sudo`命令。`sudo`命令允许你以 root 用户身份运行命令。你可以使用`sudo`命令来执行管理任务，例如安装软件。

要检查安装是否处理正常，只需再次使用`search`选项即可。这次，你应该会在`wine`软件包前面看到列出的`i u`标记，这表示它已经安装。

你可能还会注意到，有些额外的包前面也有`i u`。这是因为`aptitude`自动为我们解析了任何必要的软件包依赖关系，并安装了所需的额外库和软件包。这是许多包管理系统中包含的一个非常很棒的功能。

## 使用 aptitude 更新软件

虽然`aptitude`帮助你避免在安装软件时出现问题，但尝试协调具有依赖关系的多个包更新可能会变得棘手。要安全地更新系统中仓库中任何新版本的所有软件包，请使用`safe-upgrade`选项：

```
aptitude safe-upgrade
```

注意，此命令没有接受软件包名称作为参数。这是因为`safe-upgrade`选项会将所有已的软件包升级到仓库中提供的最新版本，这对于系统的稳定性更加安全。

以下是运行`aptitude safe-update`命令的示例输出：

```
$
$ sudo aptitude safe-upgrade
The following packages will be upgraded:
  evolution evolution-common evolution-plugins gsfonts libevolution
  xserver-xorg-video-geode
6 packages upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 9,312kB of archives. After unpacking 0B will be used.
Do you want to continue? [Y/n/?] Y
Get:1 http://us.archive.ubuntu.com/ubuntu/ maverick/main
  libevolution i386 2.30.3-1ubuntu4 [2,096kB]
...
Preparing to replace xserver-xorg-video-geode 2.11.9-2
(using .../xserver-xorg-video-geode_2.11.9-3_i386.deb) ...
Unpacking replacement xserver-xorg-video-geode ...
Processing triggers for man-db ...
Processing triggers for desktop-file-utils ...
Processing triggers for python-gmenu ...
...
Current status: 0 updates [-6].
$
```

还有一些不那么保守的软件升级选项可以可以使用：

- `aptitude full-upgrade`
- `aptitude dist-upgrade`

这些选项执行相同的任务，将所有软件包升级到最新版本。它们与`safe-upgrade`的区别在于它们不会检查与包之间的依赖关系。整个包依赖问题可能会变得非常糟糕。如果你不完全确定各种包的依赖关系，请坚持使用`safe-upgrade`选项。

> 注意事项
> > 显然，运行`aptitude`的`safe-upgrade`选项是你应该经常做的事情，以保持你的系统处于最新。然而，在全新的安装发行版后运行它尤为重要。通常情况下，自发行版最后一次完整发布以来发布了大量的安全补丁和更新。

## 使用 aptitude 卸载软件

使用`aptitude`移除软件包与安装和升级它们一样简单。你唯一需要做的真实选择是，之后是否保留软件的数据和配置文件。

要移除一个软件包，但保留数据和配置文件，请使用`aptitude`的`remove`选项。要移除一个软件包以及相关的数据和配置文件，请使用`purge`选项：

```
$ sudo aptitude purge wine
[sudo] password for user:
The following packages will be REMOVED:  
  cabextract{u} esound-clients{u} esound-common{u} gnome-exe-thumbnailer{u}
  icoutils{u} imagemagick{u} libaudio2{u} libaudiofile0{u} libcdt4{u}
  libesd0{u} libgraph4{u} libgvc5{u} libilmbase6{u} libmagickcore3-extra{u}
  libmpg123-0{u} libnetpbm10{u} libopenal1{u} libopenexr6{u}
  libpathplan4{u} libxdot4{u} netpbm{u} ttf-mscorefonts-installer{u}
  ttf-symbol-replacement{u} winbind{u} wine{p} wine1.2{u} wine1.2-gecko{u}
0 packages upgraded, 0 newly installed, 27 to remove and 6 not upgraded.
Need to get 0B of archives. After unpacking 121MB will be freed.
Do you want to continue? [Y/n/?] Y
(Reading database ... 120968 files and directories currently installed.)
Removing ttf-mscorefonts-installer ...
...
Processing triggers for fontconfig ...
Processing triggers for ureadhead ...
Processing triggers for python-support ...
$
```

要查看包是否已移除，你可以再次使用`aptitude search`选项。如果你在包前面看到`c`，意味着软件已移除，但配置文件尚未被清除。`p`表示配置文件也已清除。

## aptitude 仓库

`aptitude`的默认仓库位置在你安装 Linux 发行版时为你设置的。在许多情况下，你永远不需要添加/删除软件仓库。此外，`aptitude`只从这些仓库拉取软件。

> 提示
> Linux 发行版开发者努力确保添加到仓库的软件包版本之间不会产生冲突。通常从仓库升级或安装软件包是安全的。

以下是来自 Ubuntu 系统的`sources.list`示例：

```
$
$ cat /etc/apt/sources.list
# deb cdrom:[Ubuntu 10.10_Maverick_Meerkat_Alpha i386 (20100921)]/ main restricted
# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade
# to newer versions of the distribution.
deb http://us.archive.ubuntu.com/ubuntu/ maverick main restricted
deb-src http://us.archive.ubuntu.com/ubuntu/ maverick main restricted
# Major fix updates produced after the final release of the
# distribution.
deb http://us.archive.ubuntu.com/ubuntu/ maverick-updates restricted
deb-src http://us.archive.ubuntu.com/ubuntu/ maverick-updates restricted
...
# This 软件不是 Ubuntu 的一部分，而是由想要提供
# 最新软件的第三方开发者提供的。
deb http://extras.ubuntu.com/ubuntu/ maverick main
deb-src http://extras.ubuntu.com/ubuntu/ maverick main
deb http://security.ubuntu.com/ubuntu/ maverick-security main restricted
deb-src http://security.ubuntu.com/ubuntu/ maverick-security main restricted
deb http://security.ubuntu.com/ubuntu/ maverick-security universe
deb-src http://security.ubuntu.com/ubuntu/ maverick-security universe
...
$
```

首先，注意该文件充满了有用的注释和警告。指定的仓库源使用以下结构：

```
deb (or deb-src) address distribution_name package_type_list
```

`deb`或`deb-src`值表示软件包类型。`deb`值表示它是编译后程序的源，而`deb-src`值则表示它是源代码的源。

`address`条目是软件仓库的 Web 地址。`distribution_name`条目是该特定软件仓库发行版本的名称。在示例中，发行名称为`maverick`。这并不意味着你正在运行的发行版就是 Ubuntu 的 Maverick Meercat；它只是意味着 Linux 发行版正在使用 Ubuntu Maverick Meercat 仓库！例如，在 Linux Mint 的`sources.list`文件中，你将看到 Linux Mint 和 Ubuntu 软件仓库的混合。

最后，`package_type_list`条目可能包含多个单词，表示仓库中包含什么类型的软件包。例如，你可能会看到如`main`、`restricted`、`universe`或`partner`等值。

当你需要向源文件添加软件仓库时，你可以尝试自己操作，但这很可能会导致问题。通常，软件仓库网站或各种软件包开发者网站会提供一行完全匹配的文本，你可以从他们的网站复制并粘贴到你的`sources.list`文件中。最好的方法是选择更安全的路径直接复制/粘贴。

前端界面`aptitude`为处理基于 Debian 的`dpkg`工具提供了智能的命令行选项。现在是时候查看基于 Red Hat 的发行版的`rpm`工具及其各种前端界面了。

## 基于 Red Hat 的系统

与基于 Debian 的发行版一样，基于 Red Hat 的系统也有几种不同的前端工具可用。常见的有：

- `yum`: 用于 Red Hat 和 Fedora
- `urpm`: 用于 Mandriva
- `zypper`: 用于 openSUSE

这些前端界面都基于`rpm`命令行工具。接下来的章节将讨论如何使用这些各种基于`rpm`的工具管理软件包。重点将放在`yum`上，但也会包含`zypper`和`urpm`的信息。

### 列出已安装的软件包

要查找你的系统中当前安装了哪些内容，在 shell 提示符下输入以下命令：

```
yum list installed
```

信息可能会在屏幕上飞闪而，因此最好将已安装的软件列表重定向到文件中。然后你可以使用`more`或`less`命令（或 GUI 编辑器）以受控的方式查看列表。

```
yum list installed > installed_software
```

要列出你的 openSUSE 或 Mandriva 发行版上已安装的软件包，请参见表 8.1 中的命令。遗憾的是，Mandriva 中使用的`urpm`工具无法生成当前的安装软件列表。因此，你需要回到底`rpm`工具。

**表 8.1 如何使用 zypper 和 urpm 列出已安装软件**

| 发行版 | 前端工具 | 命令 |
| :--- | :--- | :--- |
| Mandriva | `urpm` | `rpm -qa > installed_software` |
| openSUSE | `zypper` | `zipper search -I > installed_software` |

要查找特定软件包的详细信息，`yum`真的非常出色。它不仅能给你关于软件包的非常详细描述，通过另一个简单的命令，你查看该软件包是否已安装：

```
# yum list xterm 
Loaded plugins: langpacks, presto, refresh-packagekit
Adding en_US to language list
Available Packages
xterm.i686 261-2.fc14 fedora 
#
# yum list installed xterm 
Loaded plugins: refresh-packagekit
Error: No matching Packages to list
#
```

使用`urpm`和`zypper`列出详细软件软件包信息的命令在表 8.2 中。你可以使用`zypper`命令上的`info`选项从仓库中获取更详细的软件包信息。

**表 8.2 如何使用 zypper 和 urpm 查看各种软件包细节**

| 细节类型 | 前端工具 | 命令 |
| :--- | :--- | :--- |
| 软件包信息 | `urpm` | `urpmq -i package_name` |
| 已安装? | `urpm` | `rpm -q package_name` |
| 软件包信息 | `zypper` | `zypper search -s package_name` |
| 已安装? | `zypper` | 相同，但在 Status 列中查找`i` |

最后，如果你需要找到文件系统上的特定文件是由哪个软件包提供的，多功能的`yum`也能做到！只需输入命令：

```
yum provides file_name
```

这里是一个尝试查找哪个软件提供了配置文件`/etc/yum.conf`的示例：

```
#
# yum provides /etc/yum.conf 
Loaded plugins: langpacks, presto, refresh-packagekit
Adding en_US to language list
yum-3.2.28-5.fc14.noarch : RPM installer/updater
Repo : fedora
Matched from: 
Filename : /etc/yum.conf
yum-3.2.28-5.fc14.noarch : RPM installer/updater
Repo : installed
Matched from: 
Other : Provides-match: /etc/yum.conf
#
```

`yum`检查了两个独立的仓库：fedora 和 installed。从这两个处得出的答案都是：`yum`软件包提供了这个文件！

### 使用 yum 安装软件

使用`yum`安装软件包非常简单。以下是从仓库安装软件包、其所有需要的库和软件包依赖项的基本命令：

```
yum install package_name
```

这里是安装 xterm 软件包的示例：

```
$ su -
Password: 
# yum install xterm
Loaded plugins: langpacks, presto, refresh-packagekit
Adding en_US to language list
fedora/metalink | 20 kB 00:00
fedora | 4.3 kB 00:00
fedora/primary_db | 11 MB 01:57
updates/metalink | 16 kB 00:00
updates | 4.7 kB 00:00
updates/primary_db | 11 MB 01:57
```



Updating metadata:

```text
Checking cache: ok
Metadata is expired.
Updating metadata: 01:57
fedora/metalink | 20 kB 00:00
fedora | 4.3 kB 00:00
fedora/primary_db | 11 MB 01:57
updates/metalink | 16 kB 00:00
updates | 4.7 kB 00:00
updates/primary_db | 11 MB 01:57
xterm.i686 261-2.fc14 installed
Complete!
```

#

> **注意**
> 在上述列表的 `yum` 命令之前，使用了 `su -` 命令来切换到 root 用户。`#` 表示你正以 root 身份登录。你应该只临时切换到 root 以运行管理任务，例如安装和更新。`sudo` 命令也是另一个选项。

你也可以手动下载 `rpm` 安装文件并使用 `yum` 将其安装。这被称为本地安装。基本命令是：

```bash
yum localinstall package_name.rpm
```

你可以开始发现 `yum` 的优势之一是它使用了非常符合逻辑且易用的命令。

**表 8.3** 如何使用 `zypper` 和 `urpm` 安装软件

| 前端工具 | 命令 |
| :--- | :--- |
| `urpm` | `urpmi package_name` |
| `zypper` | `zypper install package_name` |

### 使用 yum 更新软件

在大多数 Linux 发行版中，当你工作在 GUI 中时，你会得到那些漂亮的通知图标提示你需要更新。在命令行处，这需要多一些工作。

要查看已安装软件包的所有可用更新列表，输入以下命令：

```bash
yum list updates
```

对此命令没有响应通常是一件好事，因为这意味着你没有需要更新的内容！但是，如果你确实发现某个特定的软件包需要更新，请输入以下命令：

```bash
yum update package_name
```

如果你想更新更新列表中的所有软件包，只需输入以下命令：

```bash
bash update
```

**表 8.4** 如何使用 `zypper` & `urpm` 更新软件

当使用 `urpm` 时，仓库数据库会自动刷新，同时软件包也会被更新。

| 前端工具 | 命令 |
| :--- | :--- |
| `urpm` | `urpmi --auto-update --update` |
| `zypper` | `zypper update` |

## 使用 yum 卸载软件

`yum` 工具也提供了一种简单的方法来卸载你系统上不再需要的软件。与 `aptitude` 一样，你需要选择是否保留软件包的数据和配置文件。

如果只想删除软件包并保留任何配置和数据数据文件，请使用以下命令：

`yum remove package_name`

如果要卸载软件及其所有文件，请使用 `erase` 选项：

`yum erase package_name`

你会发现，在表 8.5 中，使用 `urpm` 和 `zypper` 卸载软件同样简单。这两个工具的功能都与 `yum` 的 `erase` 选项相似。

**表 8.5** 如何使用 `zypper` 和 `urpm` 卸载软件

| 前端工具 | 命令 |
| :--- | :--- |
| `urpm` | `urpme package_name` |
| `zypper` | `zypper remove package_name` |

虽然使用 PMS 软件包让生活轻松得多，但并非总是一风顺。偶尔也会出问题。幸运的是，有解决办法。

## 处理损坏的依赖关系

有时，当多个软件包被加载时，一个软件包的软件依赖可能会被另一个软件包的安装所覆盖。这被称为依赖关系损坏。

如果在你的系统上发生了这种情况，请先尝试以下命令：

`yum clean all`

然后尝试在 `yum` 命令中使用 `update` 选项。有时，只需清理任何位置的文件就能有所帮助。

如果这不能解决问题，请尝试以下命令：

`yum deplist package_name`

此命令显示该软件包的所有库依赖项以及提供这些依赖项的软件包。一旦你知道了软件包所需的库，就可以安装它们。这里有一个确定 `xterm` 软件包依赖项的示例：

```text
# yum deplist xterm

Loaded plugins: langpacks, presto, refresh-packagekit
Adding en_US to language list
Finding dependencies:
package: xterm.i686 261-2.fc14
dependency: libutempter.so.0
provider: libutempter.i686 1.1.5-4.fc12
dependency: rtld(GNU_HASH)
provider: glibc.i686 2.12.90-17
provider: glibc.i686 2.12.90-21
dependency: libc.so.6(GLIBC_2.4)
provider: glibc.i686 2.12.90-17
provider: glibc.i686 2.12.90-21
...
dependency: /bin/sh
provider: bash.i686 4.1.7-3.fc14
dependency: libICE.so.6
provider: libICE.i686 1.0.6-2.fc13
dependency: libXmu.so.6
provider: libXmu.i686 1.0.5-2-fc13
dependency: libc.so.6(GLIBC_2.3)
provider: glibc.i686 2.12.90-17
provider: glibc.i686 2.12.90-21
dependency: libXaw.so.7
provider: libXaw.i686 1.0.6-4-fc12
dependency: libX11.so.6
provider: libX11.i686 1.3.4-3-fc14
dependency: libc.so.6(GLIBC_2.2)
provider: glibc.i686 2.12.90-17
provider: glibc.i686 2.12.90-21
#
```

如果这仍然不能解决你的问题，你还有最后一个工具：

`yum update --skip-broken`

`--skip-broken` 选项允许你忽略具有损坏依赖关系的软件包，并更新其他软件包。这可能无法帮助损坏的包，但至少你可以更新系统中剩余的软件包！

在表 8.6 中，列出了使用 `urpm` 和 `zypper` 损坏依赖关系的尝试命令。对于 `zypper`，只有一个命令可以验证并修复损坏的依赖关系。对于 `urpm`，如果 `clean` 选项不起作用，你可以跳过冲突包的更新。要做到这一点，你必须将冲突包的名称添加到 `/etc/urpmi/skip.list` 文件中。

**表 8.6** `zypper` 和 `urpm` 的损坏依赖关系

| 前端工具 | 命令 |
| :--- | :--- |
| `urpm` | `urpmi --clean` |
| `zypper` | `zypper verify` |

## Yum 仓库

与 `aptitude` 系统一样，`yum` 在安装时就配置了软件仓库。对于大多数用途来说，这些预装的仓库将完全满足你的需求。但当你需要从不同的仓库安装软件时，这里有一些你需要了解的内容。

> **提示**
> 高明的系统管理员会坚持使用经过批准的仓库。经过批准的仓库是指发行发行官方网站认可的仓库。如果你开始添加未批准的仓库，你就会失去稳定性的保证。而且你会进入依赖关系损坏的领域。

要查看你当前从哪些仓库获取软件，输入以下命令：

`yum repolist`

如果你没有找到获取软件所需的仓库，那么你就需要进行一些配置文件编辑。`yum` 仓库定义文件位于 `/etc/yum.repos.d`。你需要添加正确的 URL 并获取任何必要的加密密钥的权限。

如 [rpmfusion.org](http://rpmfusion.org) 这样良好的仓库网站会列出使用它们所需的所有步骤。有时，这些仓库网站会提供 `rpm` 文件，你可以使用 `yum localinstall` 命令进行下载并安装。`rpm` 文件的安装将为你完成所有的仓库设置工作。这可真方便了！

`urpm` 将其仓库称为 media。查看 `urpm` media 和 `zypper` 仓库的命令在表 8.7 中。你会发现，在这两个前端工具中，你不需要编辑配置文件。相反，要添加 media 或仓库，你只需要输入命令即可。

**表 8.7** `zypper` 和 `urpm` 仓库

| 操作 | 前端工具 | 命令 |
| :--- | :--- | :--- |
| 显示仓库 | `urpm` | `urpmq --list-media` |
| 添加仓库 | `urpm` | `urpmi.addmedia path_name` |
| 显示仓库 | `zypper` | `zypper repos` |
| 添加仓库 | `zipper` | `zypper addrepo path_name` |

`sysstat-9.1.5/sysstat-9.1.5.lsm`
`sysstat-9.1.5/cifsiostat.c`
`sysstat-9.1.5/nfsiostat.h`
`sysstat-9.1.5/cifsiostat.h`
`sysstat-9.1.5/sysstat-9.1.5.spec`

## 安装 sysstat

现在 tar 包已经解压，文件已整齐地放置在名为 `sysstat-9.1.5` 的目录中，你可以进入该目录并继续操作。

首先，使用 `cd` 命令进入新目录，然后列出目录的内容：

```bash
$ cd sysstat-9.1.5
$ ls
```

```text
activity.c      INSTALL      prf_stats.h  sysconfig.in
build           ioconf.c     pr_stats.c    sysstat-9.1.5.lsm
CHANGES         ioconf.h     pr_stats.h    sysstat-9.1.5.spec
cifsiostat.c    iostat.c     rd_stats.c    sysstat.cron.daily.in
cifsiostat.h    iostat.h     rd_stats.h    sysstat.crond.in
common.c        Makefile.in   README        sysstat.cron.hourly.in
common.h        man           sa1.in        sysstat.in
configure        mpstat.c      sa2.in        sysstat.ioconf
configure.in    mpstat.h     sa_common.c    sysstat.sysconfig.in
contrib         nfsiostat.c   sadc.c        TODO
COPYING         nfsiostat.h   sadf.c        version.in
CREDITS         nls           sadf.h        xml
crontab.sample  pidstat.c     sa.h
FAQ             pidstat.h     sar.c
iconfig          prf_stats.c   sa_wrap.c
```

在列出的目录列表中，你通常应该看到一个 `README` 或 `AAAREADME` 文件。阅读这个文件非常重要。文件中包含你完成软件安装所需的实际指令。

遵循 `README` 文件中的建议，下一步是为你的系统执行 `configure sysstat`。这会检查你的 Linux 系统，以确保它具有适当的库依赖，以及用于编译源代码的正确编译器：

```bash
# ./configure
```

```text
Check programs:
.
checking for gcc... gcc
checking for C compiler default output name... a.out
checking whether the C compiler works... yes
...
checking for ANSI C header files... (cached) yes
checking for dirent.h that defines DIR... yes
checking for library containing opendir... none required
checking for ctype.h usability... yes
checking for ctype.h presence... yes
checking for ctype.h... yes
checking for errno.h usability... yes
...
Check library functions:
.
checking for strchr... yes
checking for strcspn... yes
checking for strspn... yes
checking for strstr... yes
checking for sensors support... yes
...
Check configuration:
...
config.status: creating Makefile
    Sysstat version:           9.1.5
    Installation prefix:      /usr/local
    rc directory:             /etc/rc
    Init directory:           /etc/rc.d/init.d
    Configuration directory:   /etc/sysconfig
    Man pages directory:      /usr/local/man
    Compiler:                 gcc
    Compiler flags:           -g -O2
```

如果发生任何错误，`configure` 步骤将显示一条解释缺失内容的错误消息。

下一阶段是使用 `make` 命令构建各种二进制文件。`make` 命令编译源代码，然后通过链接器创建该软件包的最终可执行文件。与 `configure` 命令一样，`make` 命令在编译和链接所有源代码的过程中会产生大量输出：

```bash
# make
...
gcc -o nfsiostat -g -O2 -Wall -strict-prototypes -pipe-O2 nfsiostat.o librdstats.a libsyscom.a -s
gcc -o cifsiostat.o -c -g -O2 -Wall -strict-prototypes -pipe
-O2 -DSA_DIR="/var/log/sa"
-DSA_PATH="/usr/local/lib/sa" cifsiostat.c
gcc -o cifsiostat -g -O2 -Wall -strict-prototypes -pipe
-O2 cifsiostat.o librdstats.a libsyscom.a -s
```

当 `make` 完成后，你将在目录中获得实际的 `sysstat` 软件程序！然而，从该目录运行它并不方便。相反，你希望将其安装到 Linux 系统上的公共位置。要做到这一点，你需要以 root 用户身份登录（如果你的 Linux 发行版偏好使用 `sudo` 命令），然后使用 `make` 命令的 `install` 选项：

```bash
# make install
mkdir -p /usr/local/man/man1
mkdir -p /usr/local/man8
rm -f /usr/local/man8/sa1.8
install -m 644 -g man/sa1.8 /usr/local/man8
rm -f /usr/local/man8/sa2.8
install -m 644 -g man/sa2.8 /usr/local/man8
rm -f /usr/local/man8/sadc.8
install -m 644 -g man/sadc.8 /usr/local/man8
rm -f /usr/local/man1/sar.1
...
install -m 644 sysstat.sysconfig /etc/sysconfig/sysstat
install -m 644 CHANGES /usr/local/share/doc/sysstat-9.1.5
install -m 644 COPYING /usr/local/share/doc/sysstat-9.1.5
install -m 644 CREDITS /usr/local/share/doc/sysstat-9.1.5
install -m 644 README /usr/local/share/doc/sysstat-9.1.5
install -m 644 FAQ /usr/local/share/doc/sysstat-9.1.5
```



现在 `sysstat` 软件包已经安装在`/usr/local/share/doc/sysstat-9.1.5`

## 总结

本章讨论了如何通过软件包管理系统（PMS）在命令行界面下安装、更新或移除软件。虽然大多数 Linux 发行版使用图形界面进行软件包管理，但也可以从命令行进行操作。

基于 Debian 的发行版使用`dpkg`工具与命令行进行交互。`aptitude`是`dpkg`工具的一个命令行界面。

基于 Red Hat 的发行版基于`rpm`工具，但使用了不同的命令行工具。Red Hat 和 Fedora 使用`yum`管理软件包。openSUSE 发行版使用`zypper`管理软件包，而 Mandriva 发行版使用`urpm`。

本章最后讨论了如何安装仅提供源代码的软件包。`tar`命令允许你从 tar 包中解压源代码，然后通过`configure`和`make`构建可执行程序。

下一章将查看可用的编辑器。当你准备开始编写脚本时，了解哪些编辑器将非常有帮助！

# 第 9 章：编辑器

## 本章内容

*   使用 vim 编辑器
*   理解 emacs
*   熟悉 KDE
*   使用 GNOME 编辑器

在开始你的脚本生涯之前，你需要学会使用 Linux 中的至少一种文本编辑器。你对如何使用搜索、剪切和粘贴等高级功能越熟悉，你开发脚本的速度就越快。

### vim 编辑器

如果你在命令行模式下工作，可能想熟悉一种在 Linux 控制台中运行的文本编辑器。`vi`编辑器是 Unix 系统上的原始编辑器。它使用控制台图形模式模拟文本编辑窗口，允许你查看文件行、在文件内移动以及插入、编辑和替换文本。

虽然它可能是最复杂的编辑器（至少在那些讨厌它的人看来），但它提供的许多功能使其成为几十年来 Unix 管理员的基石。

当 GNU 项目将`vi`编辑器移植到开源世界时，他们选择对其进行改进。由于它不再像 Unix 世界中原始的`vi`编辑器那样，开发者也将其重命名为改进版的 vi，即`vim`。

为了方便起见，几乎所有的 Linux 发行版都会创建一个名为`vi`（参见第 5 章）的别名，它指向`vim`程序：

```bash
$ alias vi
alias vi='vim'
$
```

本节将带你了解如何使用`vim`编辑器编辑你的文本 shell 脚本文件。

## vim 基础

`vim`编辑器在内存缓冲区中对数据进行操作。要启动`vim`编辑器，只需输入`vim`命令（如果有别名则输入`vi`）以及你想要编辑的文件名即可：

```bash
$ vim myprog.c
```

如果你在启动`vim`时没有提供文件名，或者该文件不存在，`vim`将打开一个新的缓冲区区域进行编辑。如果你在命令行中指定了一个存在的文件，`vim`将将文件的整个内容读取到缓冲区区域，然后就可以进行编辑，如图 9.1 所示。

图 9.1 vim 主窗口

![](img/00031.jpg)

`vim`编辑器会检测会话的终端类型（参见第 2 章），并使用全屏模式利用整个控制台窗口作为编辑器区域。

初始`vim`编辑窗口显示文件内容（如果有）以及窗口底部的消息行。如果文件内容没有占据整个屏幕，`vim`会在不属于文件的行处放置波浪号`~`（如图 9.1 所示）。

*   插入模式 (Insert mode)

当你首次打开一个文件进行编辑（或开始创建一个新文件）时，`vim`编辑器进入普通模式。在普通模式下，`vim`编辑器按键解释为命令（稍后会详细介绍）。

在插入模式下，`vim`将你输入的每个键都插入到缓冲区当前的光标位置。进入插入模式，按下`i`键。要退出插入模式并返回普通模式，按下键盘上的`Escape`键。

在普通模式下，你可以使用方向键在文本区域中移动光标（只要`vim`正确检测了你的终端类型）。如果你恰好处于一个没有定义方向键的不稳定终端连接上，也并非完全无可施。`vim`命令中包含了移动光标的命令：

*   `h` 向左移动一个字符
*   `j` 向下移动一行（文本中的下一行）
*   `k` 向上移动一行（文本中的上一行）
*   `l` 向右移动一个字符

在大段文本文件中逐行移动可能会很枯燥。幸运的是，`vim`提供了几个命令来帮助加速：

*   `PageDown`（或`Ctrl+F`）向前移动一屏数据
*   `PageUp`（或`Ctrl+B`）向后移动一屏数据
*   `G` 移动到缓冲区的最后一行
*   `num G` 移动到缓冲区中的第`num`行
*   `gg` 移动到缓冲区的第一行

`vim`编辑器在普通模式下有一个特殊功能，称为命令行模式。命令行模式提供了一个交互式命令行，你可以在其中输入额外的命令来控制`vim`的操作。要进入命令行模式，在普通模式下按下冒号键。光标移动到消息行，会出现一个冒号，等待你输入命令。

在命令行模式下，有几个将缓冲区保存到文件并退出`vim`的命令：

*   `q` 如果缓冲区数据没有任何更改，则退出
*   `q!` 退出并丢弃对缓冲区数据的任何更改
*   `w filename` 以不同的文件名保存文件
*   `wq` 将缓冲区数据保存到文件并退出

在看到几个基础的`vim`命令后，你可能就能理解为什么有些人极度讨厌`vim`编辑器了。要充分利用`vim`，你必须了解许多涩的命令。然而，一旦你掌握了几个基础`vim`命令，你就可以直接从命令行编辑文件，无论你处于什么种环境。此外，一旦你习惯了输入命令，同时输入数据和编辑命令似乎就像是本能一样，而要跳回使用鼠标反而变得很奇怪！

### 编辑数据

在插入模式下，你可以向缓冲区插入数据；但有时，你在将数据输入缓冲区后需要添加或删除数据。在普通模式下，`vim`编辑器提供了几个用于编辑缓冲区中数据的命令。表 9.1 列出了一些`vim`的常用编辑命令。

表 9.1 vim 编辑命令

| 命令 | 说明 |
| :--- | :--- |
| `x` | 删除当前光标位置的字符。 |
| `dd` | 删除当前光标所在的行。 |
| `dw` | 删除当前光标所在的单词。 |
| `d$` | 从当前光标位置删除到行末尾。 |
| `J` | 删除当前光标所在行尾的换行符（合并行）。 |
| `u` | 撤销上一个编辑命令。 |
| `a` | 在当前光标位置后追加数据。 |
| `A` | 在当前光标所在行的末尾追加数据。 |
| `r char` | 将当前光标位置的单个字符替换为`char`。 |
| `R text` | 用`text`覆盖当前光标位置的数据，直到按下`Escape`。 |

某些编辑命令还允许你使用数字修饰符来指定执行命令的次数。例如，命令`2x`从当前光标位置开始删除两个字符，命令`5dd`从当前光标所在行开始删除五行。

> 注意
> 在`vim`编辑器中尝试使用 PC 键盘的 Backspace（退格键）或 Delete（删除键）时要小心。`vim`编辑器通常会将 Delete 键识别为`x`命令的功能，即删除光标位置的字符。

## 复制与粘贴

现代编辑器的一个标准功能是剪切或复制数据，然后粘贴到其他地方。`vim`编辑器提供了实现这种方法。

剪切和粘贴相对简单。你已经学习了表 9.1 中可以删除数据的命令。然而，当`vim`删除数据时，它实际上将其存储在一个单独的寄存器中。你可以通过`p`命令来检索这些数据。

例如，你可以使用`dd`命令删除一行文本，然后将光标移动到缓冲区中你想放置它的位置，然后使用`p`命令。`p`命令在光标行之后插入文本。

复制文本稍微复杂一点。`vim`中的复制命令是`y`（代表 yank，即抓取）。你对`y`使用与`d`命令相同的第二个字符（`yw`复制一个单词，`y$`复制到行末）。在你复制文本后，将光标移动到你想放置文本的位置，并使用`p`命令。复制的文本现在出现在该位置。

复制的困难之处在于，由于你没有影响被复制的文本，因此你看不到发生了什么。在将内容粘贴到某处之前，你永远无法确定自己复制了什么。但`vim`有另一个功能可以帮助你复制。

可视模式在你移动光标时会高亮文本。你使用可视模式来选择要复制（yank）以供粘贴的文本。要进入可视模式，将光标移动到你想开始复制的位置，然后按下`v`。你会发现光标位置的文本现在被高亮了。接下来，移动光标覆盖你想要复制的文本（你甚至可以向下移动行来复制多行文本）。随着光标的移动，vim 会高亮剪贴板区域的文本。当你覆盖了想要复制的文本后，按下`y`键激活复制命令。现在文本已经进入了寄存器，你只需将光标移动到你想粘贴的地方，并使用`p`命令即可。

## 搜索与替换

你可以使用 vim 搜索命令轻松地查找缓冲区中的数据。要输入搜索字符串，按下正斜杠（`/`）键。光标会移动消息行，vim 会显示一个正斜杠。输入你想查找的文本，然后按回车键。vim 编辑器会响应三种操作之一：

- 如果单词出现在当前光标位置之后，它将跳转到该文本出现的第一个位置。
- 如果单词没有出现在当前光标位置之后，它将从文件末尾绕回到文件中该文本出现的第一个位置（并用消息提示）。
- 产生一条错误信息，说明文件中未找到该文本。

要继续搜索同一个单词，请按下正斜杠字符然后按回车键，或者你可以使用`n`键（下一个）。

替换命令允许你快速地将文本中的一个单词替换（替换）为另一个单词。要使用替换命令，你必须处于命令行模式。替换命令的格式为：

```bash
:s/old/new/
```

vim 编辑器会跳转到文本`old`的第一次出现处并将其替换为文本`new`。你可以对替换命令进行一些修改，以替换文本的多个出现处：

- `:s/old/new/g` 替换行内所有的`old`出现处
- `:'n,ms/old/new/g` 替换行号`n`和`m`之间所有的`old`出现
- `:%s/old/new/g` 替换整个文件中所有的`old`出现
- `:%s/old/new/gc` 替换整个文件中所有的`old`出现，但在每次替换前进行提示

正如你所见，对于命令行文本编辑器来说，vim 包含了许多高级特性。因为每个 Linux 发行版都包含了它，所以至少了解 vim 编辑器的基础知识是一个好主意，这样无论你身在何处或可以使用什么工具，都可以编辑脚本。

## emacs 编辑器

emacs 编辑器是一个极其流行的编辑器，它甚至在 Unix 出现之前就已经。开发者们非常喜欢它，将其移植到了 Unix 环境，现在它又被移植到了 Linux 环境。emacs 编辑器最初是一个控制台编辑器，类似于 vi，但它已经迁移到了图形化世界。

emacs 编辑器仍然提供原始的控制台模式编辑器，但现在它还拥有使用图形 X Windows 窗口在图形环境中编辑文本的能力。通常，当你从命令行启动 emacs 编辑器时，编辑器将判断你是否有可用的 X Window 会话并以图形模式启动。如果没有，它将在控制台模式启动。

本节将同时描述控制台模式和图形模式的 emacs 编辑器，以便在你想（或需要）时知道如何使用其中一种。

## 在控制台上使用 emacs

控制台模式版本的 emacs 是另一个使用大量按键命令来执行编辑功能的编辑器。emacs 编辑器使用涉及 Control 键（PC 键盘上的 Ctrl 键）和 Meta 键的组合。在大多数 PC 终端模拟器包中，Meta 键映射到 PC 的 Alt 键。emacs 官方文档将 Ctrl 键缩写为`C-`，将 Meta 键缩写为`M-`。因此，如果你输入`C-x`组合键，文档显示`C-x`。本章也将这样做，以免引起困惑。

### emacs 基础

要从命令行使用 emacs 编辑文件，输入：

```bash
emacs myprog.c
```



emacs 控制台模式窗口出现，并带有简短的介绍和帮助屏幕。不要担心；只要你按下任意键，emacs 就会将文件加载到活动缓冲区并显示文本，如图 9.2。

你会注意到控制台模式窗口顶部显示了一个典型的菜单栏。遗憾的是，你无法在控制台模式下使用菜单栏，只能在图形模式下使用。

> 注意
> > 如果你有图形桌面，但倾向于在控制台模式使用 emacs 而不是 X Windows 模式，请在命令行使用 `-nw` 选项。

与 vim 编辑器不同（你必须进出插入模式来切换输入命令和插入文本），emacs 编辑器只有一个模式。如果你输入可打印字符，emacs 会在当前光标位置插入它。如果你输入命令，emacs 就会执行该命令。

要在缓冲区区域移动光标，你可以使用方向键以及 PageUp 和 PageDown 键，前提是 emacs 正确识别了你的终端模拟器。如果没有，则有专门的命令移动光标：

- `C-p` 向上移动一行（文本中的上一行）。
- `C-b` 向左（向后）移动一个字符。
- `C-f` 向右（向前）移动一个字符。
- `C-n` 向下移动一行（文本中的下一行）。

还有让光标在文本中进行长距离跳转的命令：

- `M-f` 向右（向前）移动到下一个单词。
- `M-b` 向左（向后）移动到上一个单词。
- `C-a` 移动到行首。
- `C-e` 移动到行尾。
- `M-a` 移动到当前句子的开头。
- `M-e` 移动到当前句子的结尾。
- `M-v` 向后移动一屏数据。
- `C-v` 向移动一屏数据。
- `M-<` 移动到文本的第一行。
- `M->` 移动到文本的最后一行。

你应该学会几个命令用于将编辑器缓冲区保存回文件并退出 emacs：

- `C-x C-s` 将当前缓冲区保存到文件。
- `C-z` 退出 emacs 但保持它在会话中运行，以便你可以返回。
- `C-x C-c` 退出 emacs 并停止程序。

你会发现这些功能中的两个需要两个组合键命令。`C-x` 命令被称为扩展命令。这提供了另一整套完整的命令可以操作。

## 编辑数据

emacs 编辑器在缓冲区中插入和删除文本方面非常健壮。要插入文本，只需将光标移动到你想插入文本的位置并开始输入。要删除文本，emacs 使用 Backspace 键删除当前光标位置之前的字符，使用 Delete 键删除当前光标位置的字符。

emacs 编辑器还有用于杀死（kill）文本的命令。删除文本和杀死文本的区别在于，当你杀死文本时，emacs 会将其放在一个临时区域，你可以在那里检索它（参见“复制与粘贴”部分）。被删除的文本将永久消失。

缓冲区中有几个杀死文本的命令：

- `M-Backspace` 杀死当前光标位置之前的单词
- `M-d` 杀死当前光标位置之后的单词
- `C-k` 杀死从当前光标位置到行尾的内容
- `M-k` 杀死从当前光标位置到句尾的内容

emacs 编辑器还包含一种酷的批量删除（kill）文本的方法。只需将光标移动到你想删除区域的开头，然后按下 `C-@` 或 `C-Spacebar` 键。接着将光标移动到你想删除区域的末尾，按下 `C-w` 命令键。这两个位置之间的所有文本都会被删除。

如果你在删除文本时不小心操作失误，可以使用 `C-u` 命令撤销这次删除命令，并将数据恢复到删除前的状态。

## 复制与粘贴

你已经学会了如何从 emacs 缓冲区区域剪切数据；现在是时候看看如何将其粘贴到其他地方了。遗憾的是，如果你使用 vim 编辑器，那么在用 emacs 编辑器时，这个过程可能会让你感到困惑。

不幸的巧合的是，在 emacs 中粘贴数据被称为 yanking（拉取）。在 vim 编辑器中，复制也被称为 yanking，这如果你恰好同时使用这两个编辑器，将会是一件很难记忆的事情。

使用其中一个 kill 命令删除数据后，将光标移动到你想粘贴数据的位置，并使用 `C-y` 命令。这会将文本从临时区域拉出并粘贴到当前光标位置。`C-y` 命令拉取上一次 kill 命令的文本。如果你执行了多次 kill 命令，可以使用 `M-y` 命令在它们之间循环切换。

要复制文本，只需将其拉回你删除它时所在的相同位置，然后移动到新位置并再次使用 `C-y` 命令。你可以根据需要无限次地拉回文本。

## 搜索与替换

在 emacs 编辑器中搜索文本是通过使用 `C-s` 和 `C-r` 命令完成的。`C-s` 命令从当前光标位置到缓冲区区域末尾执行正向搜索，而 `C-r` 命令则从当前光标位置到缓冲区开头执行反向搜索。

当你输入任意 `C-s` 或 `C-r` 命令时，底行会出现一个提示符，询问你想要搜索的文本。emacs 可以执行两种类型的搜索。

在**增量搜索**（incremental search）中，emacs 编辑器会在你输入单词时以实时模式执行文本搜索。当你输入第一个字母时，它会高亮缓冲区中该字母出现的所有出现处。当你输入第二个字母时，它会高亮文本中该字母组合出现的所有处，依此类推，直到你完成要搜索的文本。

在**非增量搜索**（non-incremental search）中，在输入 `C-s` 或 `C-r` 命令后按下回车键。这将搜索查询锁定在底行区域，允许你在搜索之前完整输入搜索文本。

要将现有文本字符串替换为新的文本字符串，你必须使用 `M-x` 命令。该命令需要一个文本命令以及参数。

文本命令是 `replace-string`。输入命令后按下回车键，emacs 将询问你现有的文本字符串。输入完成后再次按下回车，emacs 将询问你新的替换文本字符串。

## 在 emacs 中使用缓冲区

emacs 编辑器允许通过多个缓冲区区域同时编辑多个文件。你可以将文件加载到缓冲区，并在编辑过程中切换缓冲区。

在 emacs 运行时向缓冲区加载新文件时，请使用 `C-x C-f` 键组合。这是 emacs 的“查找文件”（Find a File）模式。它会将你带到窗口的底行，允许你输入想要开始编辑的文件名。如果你不知道文件的名称或位置，只需按下回车键。这会在编辑窗口中弹出一个文件浏览器，如图 9.3 emacs 查找文件模式浏览器。

![](img/00003.jpg)

从这里，你可以浏览到想要编辑的文件。要向上移动目录级，进入双点条目并按下回车键。要向下进入目录，进入目录项并按下回车键。当你找到了想要编辑的文件，只需按下回车键，emacs 就会将其加载到新的缓冲区区域。

你可以通过按下 `C-x C-b` 扩展命令组合来列出活动缓冲区区域。emacs 编辑器会分割编辑器窗口，并在底部窗口显示缓冲区列表。除了你的主编辑缓冲区外，emacs 总是提供两个缓冲区：

*   一个名为 `scratch` 的草稿区域
*   一个名为 `Messages` 的消息区域

草稿区域允许你输入 LISP 编程命令，也可以给自己写笔记。消息区域显示 emacs 在运行期间产生的消息。如果在使用 emacs 时发生任何错误，它们将出现在消息区域中。

在窗口中切换到不同缓冲区区域有两种方法：

*   `C-x o`：切换到缓冲区列表窗口。使用方向键移动到你想要的缓冲区并按下回车键。
*   `C-x b`：输入你想切换到的缓冲区区域名称。

当你选择切换到缓冲区列表窗口选项时，emacs 将新窗口区域打开该缓冲区。emacs 编辑器允许在单个会话中打开多个窗口。下一节将讨论如何在 emacs 中管理多个窗口。

## 在控制台模式 emacs 中使用窗口

控制台模式 emacs 编辑器是在图形窗口概念出现很多年前就开发的。然而，它在那个时代是非常先进的，因为它可以在主 emacs 窗口内支持多个编辑窗口。

你可以使用以下两个命令之一将 emacs 编辑窗口拆分为多个窗口：

*   `C-x 2` 将窗口水平拆分为两个窗口。
*   `C-x 3` 将窗口垂直拆分为两个窗口。

要从一个窗口移动到另一个窗口，请使用 `C-x o` 命令。你会注意到，当你创建一个新窗口时，emacs 会在新窗口中使用原始窗口的缓冲区区域。一旦你进入新窗口，就可以使用 `C-x C-f` 命令加载新文件，或使用其中一个命令在新窗口中切换到不同的缓冲区区域。

要关闭窗口，移动到那里并使用 `C-x 0`（数字 0）命令。如果你想关闭当前窗口以外的所有窗口，请使用 `C-x 1`（数字 1）命令。

## 在 X Windows 中使用 emacs

如果你在 X Windows 环境（如 KDE 或 GNOME 桌面）中使用 emacs，它将以图形模式启动，如图 9.4 所示。

图 9.4 emacs 图形窗口

![](img/00006.jpg)

如果你已经在控制台模式下用过 emacs，你应该对 X Windows 模式熟悉。所有的快捷命令都可以作为菜单项可用。emacs 菜单栏包含以下项：

*   File（文件）：允许在窗口中打开文件、创建新窗口、关闭窗口、保存缓冲区和打印缓冲区。
*   Edit（编辑）：允许剪切和复制选中文本到剪贴板、将剪贴板数据粘贴到当前光标位置、搜索文本以及替换文本。
*   Options（选项）：提供更多 emacs 功能设置，如高亮、自动换行、光标类型和字体设置。
*   Buffers（缓冲区）：列出可用缓冲区并允许在其之间轻松切换。
*   Tools（工具）：访问 emacs 的高级功能，如命令行界面访问、拼写检查、文件间对比（diff）、发送电子邮件、日历和计算器。
*   Help（帮助）：提供在线 emacs 手册以获取特定 emacs 函数的帮助。

除了普通的图形化 emacs 菜单栏项目外，编辑器缓冲区中通常还有一个针对特定文件类型的单独项目。图 9.4 显示了打开一个 C 程序，因此 emacs 提供了一个 C 菜单项，允许对 C 语法高亮进行高级设置，并允许从命令行提示编译、运行和调试代码。

图形化 emacs 窗口是一个旧控制应用程序向图形世界迁移的示例。现在，许多 Linux 发行版提供了图形化桌面（即使对于不需要它们的服务器），图形化编辑器变得越来越常见。两种流行的 Linux 桌面环境（KDE 和 GNOME）也为各自的环境提供了特定的图形化文本编辑器，本文的其余部分将介绍它们。

## KDE 编辑器家族

如果你使用的是使用 KDE 桌面的 Linux 发行版（参见第 1 章），在文本编辑器方面你有几个选择。KDE 项目官方支持两个不同的文本编辑器：

* `KWrite`: 一个单屏文本编辑包
* `Kate`: 一个功能全、多窗口的文本编辑包

这两个编辑器都是包含许多高级功能的图形化文本编辑器。`Kate` 编辑器提供了更高级的功能，以及在标准文本编辑器中不常见的额外便利。本节描述了每种编辑器，并展示了一些你可以用来帮助编辑 shell 脚本的功能。

## KWrite 编辑器

KDE 环境的基础编辑器是 `KWrite`。它提供了简单的类似文字处理风格的文本编辑，并支持代码语法高亮和编辑。默认的 `KWrite` 编辑窗口如图 9.5 所示。

图 9.5 默认的 KWrite 窗口编辑 shell 脚本程序

![](img/00007.jpg)

从图 9.5 中看不出来，但 `KWrite` 编辑器识别多种类型的编程语言，并使用颜色编码区分常量、函数和注释。此外，注意 `for` 循环有一个连接起始和大括号的图标。这被称为折叠标记。通过点击该图标，你可以将函数折叠为单行。在处理大型应用程序时这是一个非常棒的功能。

`KWrite` 编辑窗口提供了完整的剪切和粘贴功能。要使用 `KWrite` 编辑文件，你可以使用鼠标或使用命令行：

```bash
$ kwrite
```



`kwrite` 命令有几个你可以用于自定义的参数：

* `--stdin`
* `--encoding`
* `--line`
* `--column`

菜单栏包含以下内容：

* `File`：用于加载、保存、打印、导出
* `Edit`：用于撤销、重做、剪切、复制、粘贴、全选、取消选择、覆盖模式、查找、查找下一个、查找上一个
* `View`：管理外观
* `Tools`：管理特殊功能
* `Settings`：用于配置编辑器

`Edit` 菜单项提供了处理文本所需的所有必要命令。表 9.2 描述了这些项目。

### 表 9.2 编辑菜单

| 项目 | 描述 |
| :--- | :--- |
| `Undo` | 撤销上次操作 |
| `Redo` | 撤销上一次撤销 |
| `Cut` | 删除选中文本并放入剪贴板 |
| `Copy` | 复制选中文本 |
| `Paste` | 插入剪贴板当前内容 |
| `Select All` | 选择编辑器中所有文本 |
| `Deselect` | 取消当前任何文本的选中 |
| `Overwrite Mode` | 在插入模式和覆盖模式之间切换 |
| `Find` | 产生查找对话框 |
| `Find Next` | 重复上一次向前查找 |
| `Find Previous` | 重复上一次向后查找 |
| `Replace` | 产生替换对话框 |
| `Find Selected` | 查找下一个出现处 |
| `Find Selected Backwards` | 查找上一个出现处 |
| `Go to` |  |

`Find` 功能有两种模式：普通模式（可以执行简单搜索）和高级搜索（你可以在其中进行高级搜索）。你通过查找部分中的箭头在两种模式之间切换，如图图 9.6 所示。

### 图 9.6 查找部分

![](img/00009.jpg)

`Tools` 菜单栏为处理文本提供了几个实用的功能。表 9.3 描述了 `KWrite` 中提供的工具。

### 表 9.3 KWrite 工具

| 工具 | 描述 |
| :--- | :--- |
| `Read Only Mode` | 锁定文本以便进行任何更改 |
| `Encoding` | 设置文本使用的字符集编码 |
| `Spelling` | 在文本开始处启动检查检查程序 |
| `Spelling (from cursor)` | 从当前光标位置启动检查检查程序 |
| `Spellcheck Selection` | 仅对选中的文本部分启动检查检查程序 |
| `Indent` | 增加段落缩进一级 |
| `Unindent` | 减少段落缩进一级 |
| `Clean Indentation` | 将所有段落缩进恢复原始设置 |
| `Align` | 强制当前行或选行返回默认缩进设置 |
| `Uppercase` | 将选中文本设为大写 |
| `Lowercase` | 将选中文本设为小写 |
| `Capitalize` | 将选中文本的首字母大大写 |
| `Join Lines` | 将选行合并为一行 |
| 换行文档 (Word Wrap Document) | 在文本中启用换行。如果某行超出了编辑器窗口边缘，该行将在下一行继续 |

有很多简单的文本编辑器工具可以使用！

`Settings`（设置）菜单包含 `Configure Editor`（配置编辑器）对话框，如图 9.7 所示。

### 图 9.7 KWrite 配置编辑器对话框

![](img/00011.jpg)

`Configuration`（配置）对话框使用左侧的图标供你选择想要在 `KWrite` 中配置的功能。当你选择其中一个图标时，对话框的右侧会显示该功能的配置设置。

`Appearance`（外观）功能允许你设置若干项功能，用于控制文本在文本编辑器窗口中的显示方式。你可以从这里启用换行、行号（对程序员非常有用）和文件夹标记。通过 `Fonts & Colors`（字体与颜色）功能，你可以自定义编辑器的完整配色方案，确定程序代码中每类文本采用的颜色。

## Kate 编辑器

`Kate` 编辑器是 KDE 项目的旗舰编辑器。它使用了与 `KWrite` 应用相同的文本编辑器（因此大部分功能都是相同的），但它将许多其他功能集成到了一个包中。

当你启动 `Kate` 编辑器时，首先会注意到编辑器并没有启动！相反，你会看到一个对话框，如图 9.8 所示。

### 图 9.8 Kate 会话对话框

![](img/00016.jpg)

`Kate` 编辑器通过会话（sessions）处理文件。你可以在一个会话中打开多个文件，也可以保存多个会话。启动 `Kate` 时，它会让你选择返回哪个会话。当你关闭 `Kate` 会话时，它会记住你打开过的文档，并在下次启动 `Kate` 时显示它们。这允许你通过为每个项目使用独立的工作区，轻松地管理多个项目的文件。

选择会话后，你将看到 `Kate` 编辑器的主窗口，如图 9.9 所示。

### 图 9.9 Kate 主编辑窗口

![](img/00018.jpg)

左侧框架显示当前会话中打开的文档。你只需点击文档名称即可在文档间切换。要编辑新文件，点击左侧的 `Filesystem Browser`（文件系统浏览器）标签。左侧框架现在是一个完整的图形化文件系统浏览器，允许你通过图形界面浏览并定位文件。

`Kate` 编辑器的一个强大功能是内置的终端窗口，如图 9.10 所示。

### 图 9.10 Kate 内置终端窗口

![](img/00023.jpg)

文本编辑器窗口底部的终端标签会启动 `Kate` 内置的终端模拟器（使用 KDE 的 `Konsole` 终端模拟器）。此功能将水平拆分当前编辑窗口，创建一个运行着 `Konsole` 的新窗口。你现在可以输入命令、启动程序或检查系统设置，而无需离开编辑器！要关闭终端窗口，只需在命令提示符处输入 `exit`。

正如你从终端功能中看到的，`Kate` 也支持多窗口。`Window`（窗口）菜单栏项提供了以下选项：

* 使用当前会话创建一个新的 `Kate` 窗口
* 垂直拆分当前窗口以创建一个新窗口
* 水平拆分当前窗口以创建一个新窗口
* 关闭当前窗口

要在 `Kate` 中设置配置选项，请选择 `Settings` 菜单栏项下的 `Configure Kate` 项。将出现如图 9.11 所示的 `Configuration` 对话框。

### 图 9.11 Kate 配置设置对话框

![](img/00024.jpg)

你会注意到 `Editor`（编辑器）设置区域与 `KWrite` 完全相同。这是因为这两个编辑器共享同一个文本编辑器引擎。`Application`（应用程序）设置区域允许你配置 `Kate` 项目的设置，例如控制会话（如图 9.11 所示）、文档列表和文件浏览器。`Kate` 还支持外部插件应用程序，可以在此处激活它们。

## GNOME 编辑器

如果你在运行 GNOME 桌面环境的 Linux 系统上工作，你也可以使用一个图形化文本编辑器。`gedit` 文本编辑器是一个基础文本编辑器，为了增加趣味性，它加入了一些高级功能。本节将带你了解 `gedit` 的功能，并演示如何使用它进行 Shell 脚本编程。

### 启动 `gedit`

大多数 GNOME 桌面环境在 `Accessories Panel`（辅助面板）菜单项中包含 `gedit`。如果你在那里没有找到 `gedit`，可以从命令行提示符启动它：

```bash
$ gedit factorial.sh myprog.c
```

当你使用多个文件启动 `gedit` 时，它会将所有文件加载到单独的缓冲区，并将每个文件作为标签页在主编辑器窗口内显示，如图 9.12 所示。

### 图 9.12 gedit 主编辑器窗口

![](img/00065.jpg)

`gedit` 主编辑器窗口的左侧框架显示你当前正在编辑的文档。右侧显示包含缓冲区文本的标签窗口。将鼠标指针悬停在每个标签上时，会出现一个对话框，显示文件的完整路径、MIME 类型以及它使用的字符集编码。

### gedit 基本功能

除了编辑器窗口外，`gedit` 还使用了菜单栏和工具栏，允许你设置功能并配置设置。工具栏提供了快速访问菜单项。可选菜单项有：

* `File`（文件）：用于处理新文件、保存现有文件和打印文件
* `Edit`（编辑）：用于操作活动缓冲区区域文本并设置编辑器偏好
* `View`（视图）：用于设置在窗口中显示的编辑器功能以及设置文本高亮模式
* `Search`（搜索）：用于在活动编辑器缓冲区区域查找并替换文本
* `Tools`（工具）：用于访问安装在 `gedit` 中的插件工具
* `Documents`（文档）：用于管理缓冲区区域打开的文件
* `Help`（帮助）：用于访问完整的 `gedit` 手册

这里没什么太让人意外的。`File` 菜单提供了 `Open Location`（打开位置）选项，允许你使用万维网中常用的标准统一资源标识符（URI）格式从网络打开文件。该格式识别了访问文件时使用的协议（如 `HTTP` 或 `FTP`）、文件所在的服务器以及服务器上访问该文件的完整路径。

`Edit` 菜单包含标准的剪切、复制和粘贴功能，还有一个方便的功能，允许你以多种不同的格式在文本中输入日期和时间。`Search` 菜单提供了标准的查找功能，产生一个对话框，可以在其中输入要查找的文本，并可以选择查找的工作方式（区分大小写、全词以及搜索方向）。它还提供了增量搜索功能，该功能以实时模式工作，在你输入单词字符时查找文本。

## 设置偏好

`Edit` 菜单包含 `Preferences`（偏好）项，产生 `gedit` 偏好对话框，如图 9.13 所示。

### 图 9.13 gedit 偏好对话框

![](img/00004.jpg)

在这里你通自定义 `gedit` 编辑器的操作。`Preferences` 对话框包含五个标签区域，用于设置编辑器的功能和行为。

### 视图

`View` 标签提供了 `gedit` 在编辑器窗口中显示文本的选项：

* **文本换行 (Text Wrapping)**：决定如何处理编辑器中的长行文本。启用文本换行选项会将长行折叠到编辑器的下一行。“不跨两行拆分 (Do Not Split Words Over Two Lines)”选项防止在长单词中自动插入连字符，以免它们被拆分到两行。
* **行号 (Line Numbers)**：在编辑器窗口的左侧边缘显示行号。
* **当前行 (Current Line)**：高亮光标所在的行，方便你轻松找到光标位置。
* **右边距 (Right Margin)**：启用右边距并允许你设置编辑器窗口的列数。默认值为 80 列。
* **括号匹配 (Bracket Matching)**：启用后将高亮编程代码中的括号对，允许你轻松匹配 `if-then` 语句、`for` 和 `while` 循环以及其他使用括号的代码元素。

行号和括号匹配功能为程序员提供了一个普通文本编辑器不常见的代码调试环境。

### 编辑器 (Editor)

`Editor` 标签页提供了 `gedit` 编辑器处理制表符和缩进的选项，以及文件的保存方式：

* **制表符停止 (Tab Stops)**：设置按下 `Tab` 键时跳过的空格数。默认值为八个。此功能还包含一个复选框，勾选后将插入空格而非制表符跳转。
* **自动缩进 (Automatic Indentation)**：启用后，`gedit` 会自动对文本中的段落和代码元素（如 `if-then` 语句和循环）进行缩进。
* **文件保存 (File Saving)**：提供了两个保存功能：在编辑窗口中打开文件时是否创建备份副本，以及是否在预设间隔内自动保存文件。

自动保存功能是确保更改定期保存的好方法，可以防止因崩溃或停电导致的灾难。

### 字体与颜色 (Font & Colors)

`Font & Colors` 标签页允许你配置（意不意外地）两个项目：

* **字体 (Font)**：允许你选择 `Monospace 10` 作为默认字体，或从对话框中选择自定义的字体和字体大小。
* **配色方案 (Color Scheme)**：允许你选择用于文本、背景、选中文本和选择颜色的默认配色方案，或为每个类别选择自定义颜色。

`gedit` 的默认颜色通常与桌面选择的标准 GNOME 桌面主题匹配。这些颜色将更改以匹配你为桌面选择方案。

### 插件 (Plug-ins)

`Plugins` 标签页提供了对 `gedit` 中用插件的控制。插件是独立的程序，可以与 `gedit` 交互提供额外功能。`Plugins` 标签页见图 9.14。

### 图 9.14 `gedit` 插件偏好设置

![](img/00059.jpg)

`gedit` 有多个插件可用，但并非所有插件都默认安装。表 9.4 描述了目前 `gedit` 中可用的插件。

### 表 9.4 `gedit` 插件

| 插件 | 描述 |
| :--- | :--- |
| `Change Case` | 更改选中文本的大小写 |
| `Document Statistics` | 报告单词、行数、字符和非空格字符的数量 |
| `External Tools` | 在编辑器中提供一个 shell 环境以执行命令和脚本 |
| `File Browser Pane` | 提供一个简单的文件浏览器，使选择文件进行编辑更加容易 |
| `Insert Date/Time` | 在当前光标位置插入多种格式的当前日期和时间 |
| `Modelines` | 在编辑器窗口底部提供 emacs 风格的消息行 |
| `Python Console` | 在编辑器窗口底部提供一个交互式控制台，用于使用 Python 语言输入命令 |
| `Quick Open` | 直接在 `gedit` 编辑窗口中打开文件 |
| `Snippets` | 允许你存储常用的文本片段，以便在文本任何地方轻松检索 |
| `Sort` | 快速排序整个文件或选中文本 |
| `Spell Checker` | 为文本文件提供字典拼写检查 |
| `Tag List` | 提供一个常用字符串列表，你可以轻松地将其输入文本中 |

已启用的插件会在名称旁边的复选框中显示勾选。某些插件（例如 `External Tools` 插件）是默认启用的。

到目前为止，你已经了解如何使用 shell 的命令行界面（CLI）提示符来输入命令并查看命令结果。shell 脚本的关键在于能够输入多个命令并处理每个命令的结果，甚至可能将一个命令的结果传递给另一个命令。shell 允许你将命令组合成单个步骤。

如果你想一起运行两个命令，可以在同一行提示符上输入它们，并用分号隔开：

```bash
$ date ; who

Mon Feb 21 15:36:09 EST 2011

Christine tty2           2011-02-21 15:26

Samantha tty3           2011-02-21 15:26

Timothy  tty1           2011-02-21 15:26

user     tty7           2011-02-19 14:03 (:0)

user     pts/0          2011-02-21 15:21 (:0.0)

$
```

恭喜，你刚刚写了一个 shell 脚本！这个简单的脚本只使用了两个 `bash` shell 命令。`date` 命令首先运行，显示当前的日期和时间，然后是 `who` 命令的输出，显示当前谁登录了系统。使用这种技术，你可以根据需要连接任意数量的命令，最多可达到命令行字符数 255 个字符的限制。

虽然这种技术对于小型脚本来说没问题，但它有一个主要的缺点：每次想运行它时，都必须在命令提示符上输入整个命令。与其手动在命令行中输入命令，你不如将命令组合到一个简单的文本文件中。当你需要运行命令时，只需运行该文本文件即可。

## 创建脚本文件

要将 shell 命令存放在文本文件中，你首先需要使用文本编辑器（参见第 9 章）创建一个文件，然后将命令输入到文件中。

在创建 shell 脚本文件时，你必须在文件的第一行指定你正在使用的 shell。其格式如下：

```bash
#!//bin/bash
```

在普通的 shell 脚本行中，井号（`#`）用作注释行。shell 脚本中的注释行不会被 shell 处理。然而，shell 脚本文件的第一行是一个特殊情况，井号后跟感叹号告诉 shell 在什么 shell 环境下运行脚本（是的，你可以使用 `bash` shell 并使用另一个 shell 运行你的脚本）。

在指定 shell 后，命令被输入到文件的每一行，并跟一个回车。如前所述，可以使用井号添加注释。示例所示：

```bash
#!/bin/bash

# 此脚本显示日期和当前登录的用户

date

who
```

就只有这些了。如果你想这样做，可以使用分号并将两个命令放在同一行，但在 shell 脚本中，你可以将命令列在不同的行上。shell 将按照它们在文件中出现的顺序来处理命令。

另外请注意，文件中还包含了一行以井符号开头并添加注释的行。以井符号开头的行（第一行 `#!` 除外）不会被 shell 解释。这是为你脚本中发生的情况留留注释的极佳方法，这样当你两年后回来时，就能轻松地记起你做了什么。

将此脚本保存为名为 `test1` 的文件，你就几乎就绪了。在运行新的 shell 脚本文件之前，还有几件事需要处理。

如果你现在尝试运行该文件，你会有些失望地看到这个：

```bash
$ test1

bash: test1: command not found

$
```

要跨越第一个障碍是让 `bash` shell 找到你的脚本文件。如果你还记得第 5 章，shell 使用一个名为 `PATH` 的环境变量来查找命令。快速查看 `PATH` 环境变量就可以发现我们的问题：

```bash
$ echo $PATH

/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin $
```



`PATH` 环境变量被设置为仅在少数几个目录中查找命令。为了让 shell 找到`test1`脚本，我们需要做两件事之一：

* 将我们 shell 脚本文件所在的目录添加到`PATH`环境变量中。
* 在提示符中使用绝对或相对路径来引用我们的 shell 脚本文件。

> **提示**
> 某些 Linux 发行版会将`$HOME/bin`目录添加到`PATH`环境变量。这在每个用户的`HOME`目录中创建一个空间，用于存放 shell 可以找到并执行的文件。

对于本示例，我们将使用第二种方法告诉 shell 脚本文件的具体位置。记住，要引用当前目录下的文件，你可以在 shell 中使用点操作符：

```
$ ./test1
bash: ./test1: Permission denied
$
```

现在 shell 顺利找到了 shell 脚本文件，但还有另一个问题。shell 指出你没有执行该文件的权限。快速查看文件权限就可以看出发生了什么：

```
$ ls -l test1
-rw-r--r--    1 user      user           73 Sep 24 19:56 test1
$
```

当创建新的`test1`文件时，`umask`值决定了新文件的默认权限设置。由于`umask`变量设置为 022（参见第 6 章），系统创建文件时仅为文件所有者赋予了读/写权限。

下一步是使用`chmod`命令赋予文件所有者执行文件的权限（参见第 6 章）：

```
$ chmod u+x test1
$ ./test1
Mon Feb 21 15:38:19 EST 2011
Christine tty2           2011-02-21 15:26
Samantha tty3           2011-02-21 15:26
Timothy  tty1           2011-02-21 15:26
user     tty7           2011-02-19 14:03 (:0)
user     pts/0          2011-02-21 15:21 (:0.0)
$
```

## 显示消息

大多数 shell 命令都会产生自己的输出。然而，有时你可能想在脚本中添加自己的文本。你可以通过`echo`命令来实现这一点。`echo`命令可以显示简单的字符串。但是，如果你在字符串内部使用引号，有时可能会变得棘手。

你可以使用双引号或单引号来界定字符串。如果你在字符串内部使用它们，你需要使用一种类型和另一种类型来界定：

```
$ echo "This is a test"
$ echo ‘scripting is easy’
```

现在所有的引号在输出中都正常显示了。你可以在 shell 脚本中任何需要显示的地方添加`echo`语句：

```
$ cat test1
#!/bin/bash
# 此脚本显示日期和当前登录的用户
echo The time and date are:
date
echo "Let's see who's logged into the system:"
who
```

当你运行此脚本时，它产生以下内容：

```
$ ./test1
The time and date are:
Mon Feb 21 15:41:13 EST 2011
Let's see who's logged into the system:
Christine tty2           2011-02-21 15:26
Samantha tty3           2011-02-21 15:26
Timothy  tty1           2011-02-21 15:26
user     tty7           2011-02-19 14:03 (:0)
user     pts/0          2011-02-21 15:21 (:0.0)
$
```

这看起来很不错，但如果你想在命令输出的同一行`echo`文本字符串呢？你可以为`echo`语句使用`-n`参数来实现这一点。只需将第一个`echo`语句行改为如下：

```
echo -n "The time and date are: "
```

你需要在字符串周围使用引号，以确保输出的字符串末尾有一个空格。命令的输出从字符串输出停止的地方恰好开始。现在的输出看起来像所示：

```
$ ./test1
The time and date are: Mon Feb 21 15:42:23 EST 2011
Let's see who's logged into the system:
Christine tty2           2011-02-21 15:26
Samantha tty3           2011-02-21 15:26
Timothy  tty1           2011-02-21 15:26
user     tty7           2011-02-19 14:03 (:0)
user     pts/0          2011-02-21 15:21 (:0.0)
$
```

完美！`echo`命令是 shell 脚本中与用户交互的关键部分。你会发现在自己在很多情况下都会使用它，特别是当你想显示脚本变量的值时。让我们接下来来看这一点。

## 使用变量

仅仅在 shell 脚本中运行单个命令是有用的，但它也有其局限性。通常你希望在 shell 命令中加入其他数据来处理信息。你可以通过使用变量来实现。变量允许你在 shell 脚本临时存储信息，供脚本中的其他命令使用。本节将介绍如何在 shell 脚本中使用变量。

### 环境变量

你已经看到一种 Linux 变量在运行了。第 5 章描述了 Linux 系统中可用的环境变量。你也可以从 shell 脚本访问这些值。

shell 维护着用于跟踪特定系统信息的环境变量，例如系统名称、登录系统的用户名、用户的系统 ID（称为`UID`）、用户的默认主目录以及 shell 查找程序时使用的搜索路径。你可以使用`set`命令显示可用活动环境变量的完整列表：

```
$ set
BASH=/bin/bash
...
HOME=/home/Samantha
HOSTNAME=localhost.localdomain
HOSTTYPE=i386
IFS=$‘ \t\n’
IMSETTINGS_INTEGRATE_DESKTOP=yes
IMSETTINGS_MODULE=none
LANG=en_US.utf8
LESSOPEN=‘|/usr/bin/lesspipe.sh %s’
LINES=24
LOGNAME=Samantha
...
```

你可以通过在环境变量名称前加上美元符号`$`来在脚本内部调用这些环境变量。下面的脚本演示了这一点：

```bash
$ cat test2
#!/bin/bash
# display user information from the system.
echo “User info for userid: $USER”
echo UID: $UID
echo HOME: $HOME
$
```

`$USER`、`$UID`和`$HOME`环境变量用于显示有关登录用户的相关信息。输出应该类似于：

```
$chmod u+x test2
$ ./test2
User info for userid: Samantha
UID: 1001
HOME: /home/Samantha
$ $
```

注意，当运行脚本时，`echo`命令中的环境变量会被替换为它们当前的值。另外请注意，我们能够在第一个字符串的双引号内放置`$USER`变量，且 shell 脚本仍然能够识别出我们的意思。然而，使用这种方法也有一个缺点。看看这个例子中发生的情况：

```
$ echo “The cost of the item is $15”
The cost of the item is 5
```

这显然不是预期的。每当脚本在引号内看到美元符号时，它都会认为你正在引用一个变量。在这个例子中，脚本尝试显示变量`$1`（它是未定义的），然后是数字`5`。要显示实际的美元符号，必须在它前面加上一个反斜杠字符：

```
$ echo “The cost of the item is \$15”
The cost of the item is $15
```

这样好多了。反斜杠允许 shell 脚本将美元符号解释为实际的美元符号而不是变量。下一节将介绍如何在脚本中创建自己的变量。

> **注意**
> 你可能还会看到使用`${variable}`格式引用的变量。变量名周围额外的括号通常用于帮助从美元符号中识别变量名。

### 用户变量

除了环境变量，shell 脚本还允许你在脚本内部设置和使用自己的变量。设置变量允许你临时存储数据并在整个脚本中使用它，使得 shell 脚本更像一个真正的计算机程序。

用户变量可以是任何最多 20 个字母、数字或下划线字符的文本字符串。用户变量区分大小写，因此变量`Var1`与变量`var1`不同。这个小规则经常让初学者脚本编程师陷入麻烦。

使用等号`=`给用户变量赋值。变量、等号和值之间不能出现空格（这是初学者另一个容易出错的地方）。以下是给用户变量赋值的几个示例：

```
var1=10
var2=-57
var3=testing
var4=“still more testing”
```

shell 脚本会自动确定用于变量值的数据类型。在 shell 脚本内部定义的变量在整个脚本的生命周期内都会保持其值，但在脚本完成后会被删除。

就像系统变量一样，用户变量可以使用美元符号进行引用：

```bash
$ cat test3
#!/bin/bash
# testing variables
days=10
guest="Katie”
echo “$guest checked in $days days ago”
days=5
guest="Jessica”
echo “$guest checked in $days days ago”
$
```

运行脚本会产生以下输出：

```
$ chmod u+x test3
$ ./test3
Katie checked in 10 days ago
Jessica checked in 5 days ago
$
```

每当引用变量时，它都会产生当前赋值给它的值。记住，在引用变量值时使用美元符号，但在引用变量并为其赋值时，不使用美元符号。这里有一个我意思的例子：

```bash
$ cat test4
#!/bin/bash
# assigning a variable value to another variable
value1=10
value2=$value1
echo The resulting value is $value2
$
```

当你在赋值语句中使用`value1`变量的值时，必须仍然使用美元符号。这段代码产生以下输出：

```
$ chmod u+x test4
$ ./test4
The resulting value is 10
$
```

如果你忘记了美元符号，并将`value2`赋值行写成如下：

```
value2=value1
```

你将得到以下输出：

```
$ ./test4
The resulting value is value1
$
```

没有美元符号，shell 会将变量名解释为普通文本字符串，这很可能不是你想要的。

### 反引号（Backtick）

shell 脚本最有用的特性之一是那个不起道的引号字符，在 Linux 世界中通常被称为反引号（`` ` ``）。注意——这不是你习惯用于字符串的普通引号。由于它在 shell 脚本中并不经常使用，你可能甚至不知道在键盘的哪里找到它。你应该习惯一下它，因为它是许多 shell 脚本的关键组件。提示：在美式键盘上，它通常与波浪符号（`~`）在同一个键上。

反引号允许你将 shell 命令的输出赋值给变量。虽然这看起来没什么，但它是脚本编程中的一个主要构建模块。

你必须用反引号包裹整个命令行行：

```
testing=`date`
```

shell 会运行反引号内的命令并将输出赋值给变量。这里有一个使用普通 shell 命令输出创建变量的示例：

```bash
$ cat test5
#!/bin/bash
# using the backtick character
testing=`date`
echo “The date and time are: ” $testing
$
```

变量`testing`接收来自`date`命令的输出，并在`echo`语句中使用它进行显示。运行 shell 脚本产生以下输出：

```
$ chmod u+x test5
$ ./test5
The date and time are:  Mon Jan 31 20:23:25 EDT 2011
$
```

在这个例子中并没有那么有趣了（你完全可以简单地将命令放在`echo`语句中），但一旦你将命令输出捕获到变量中，你就可以对其进行任何操作。

这里有一个常用的示例，展示了如何使用反引号获取当前日期并用它在脚本创建一个唯一文件名：

```bash
#!/bin/bash
# 将 /usr/bin 列表拷贝到日志文件
today=`date +%y%m%d`
ls /usr/bin -al > log.$today
```

`today`变量被赋值为格式化后的日期命令的输出。这是一种用于日志文件名提取日期信息的常用技术。`+%y%m%d`格式指示`date`命令以两位数的年份、月份和日期显示日期：

```bash
$ date +%y%m%d
110131
$
```

脚本将值赋给变量，然后将其作为文件名的一部分使用。文件本身包含了重定向输出（稍后在“输入和输出重定向”章节中讨论）的目录列表。运行脚本后，你应该会在目录中看到新文件：

```text
-rw-r--r--    1 user      user           769 Jan 31 10:15 log.110131
```

日志文件出现在目录中，文件名使用了`$today`变量的值。日志文件的内容是`/usr/bin`目录的列表。如果第二天运行脚本，日志文件名将`log.110201`，从而为新的一天创建一个新文件。

## 输入和输出重定向

有时希望保存命令的输出，而不仅仅是将其显示在显示器上。bash shell 提供了不同的运算符，允许你将命令的输出`重定向`到其他位置（例如文件）。重定向可以用于输入，也可以用于输出，将文件重定向到命令作为输入。本节介绍了在 shell 脚本中使用重定向时需要的操作。

### 输出重定向

最基本的重定向是将命令的输出发送到文件。bash shell 使用大于号（`>`）来实现此操作：

```bash
command > outputfile
```

原本会显示在显示器上的命令内容现在被存储在指定的输出文件中：

```bash
$ date > test6
$ ls -l test6
-rw-r--r--    1 user      user             29 Feb 10 17:56 test6
$ cat test6
Thu Feb 10 17:56:58 EDT 2011
$
```

重定向运算符创建了文件`test6`（使用默认的`umask`设置）并将`date`命令的输出重定向到`test6`文件。如果输出文件已存在，重定向运算符将用新数据覆盖现有文件：

```bash
$ who > test6
$ cat test6
user      pts/0    Feb 10 17:55
$
```

现在`test6`文件的内容包含了`who`命令的输出。

有时，你可能不需要覆盖文件内容，而是将命令的输出追加到现有文件中，例如当你正在创建一个日志文件来记录系统上的操作时。在这种情况下，你可以使用双大于号（`>>`）来追加数据：

```bash
$ date >> test6
$ cat test6
user      pts/0    Feb 10 17:55
Thu Feb 10 18:02:14 EDT 2011
$
```

`test6`文件仍然包含之前处理的`who`命令的原始数据——现在它还包含了`date`命令的新输出。

### 输入重定向

输入重定向是输出重定向的反方向。输入重定向不是获取命令输出并重定向到文件，而是获取文件内容并重定向到命令。

输入重定向符号是小于号（`<`）：

```bash
command < inputfile
```

记住此点的简单方法是：命令始终列在命令行最前面，而重定向符号“指向”数据流的方向。小于号表示数据从输入文件流向命令。

这是一个使用`wc`命令进行输入重定向的示例：

```bash
$ wc < test6
      2       11       60
$
```



`wc` 命令提供数据中文本的计数。默认情况下，它产生三个值：

*   文本中的行数
*   文本中的单词数
*   文本中的字节数

通过将文本文件重定向到`wc`命令，你可以快速统计文件的行数、单词和字节数。示例显示`test6`文件中有 2 行、11 个单词和 60 个字节。

还有另一种输入重定向方法，称为“内联输入重定向”。这种方法允许你在命令行上指定输入重定向的数据，而不是在文件中指定。初看起来这可能有些奇怪，但这种过程有几个应用（例如稍后在“执行数学运算”章节中所示）。

内联输入重定向符号是双小于号（`<<`）。在此之外，你必须在命令行中指定输入重定向的数据。

不要将管道（piping）认为是接连运行两个命令。Linux 系统实际上是同时运行这两个命令，并在系统内部将它们连接起来。当第一个命令产生输出时，它会立即发送到第二个命令。这不需要使用中间文件或缓冲区来传输数据。

现在，使用管道你可以轻松将`rpm`命令的输出直接`pipe`到`sort`命令以生成结果：

```bash
$ rpm -qa | sort
```

```text
abrt-1.1.14-1-fc14.i686
abrt-addon-ccpp-1.1.14-1-fc14.i686
abrt-addon-kerneloops-1.1.14-1-fc14.i686
abrt-addon-python-1.1.14-1-fc14.i686
abrt-desktop-1.1.14-1-fc14.i686
abrt-gui-1.1.14-1-fc14.i686
abrt-libs-1.1.14-1-fc14.i686
abrt-plugin-bugzilla-1.1.14-1-fc14.i686
abrt-plugin-logger-1.1.14-1-fc14.i686
abrt-plugin-runapp-1.1.14-1-fc14.i686
acl-2.2.49-8-fc14.i686
...
```

除非你是一个（快速）读者，否则可能跟不上该命令生成的输出。因为管道功能是实时的，只要`rpm`命令产生数据，`sort`命令就开始忙于排序它。当`rpm`命令完成输出时，`sort`命令已经完成了排序并在显示器上显示。

命令中管道的数量没有限制。你可以继续将命令的输出管道到其他命令以完善你的操作。在这种情况下，由于`sort`命令的输出速度非常快，你可以使用分页命令（如`less`或`more`）来强制输出在每屏停止：

```bash
$ rpm -qa | sort | more
```

这条命令运行`rpm`命令，将其输出管道到`sort`命令，然后将该输出管道到`more`命令进行显示，每屏信息停止。这让你在继续之前暂停并阅读显示内容，如图 10.1 使用管道将数据发送到 more 命令![](img/0006.jpg)

为了更高级的操作，你可以配合重定向使用管道将输出保存到文件：

```bash
$ rpm -qa | sort > rpm.list
$ more rpm.list
```

```text
abrt-1.1.14-1-fc14.i686
abrt-addon-ccpp-1.1.14-1-fc14.i686
abrt-addon-kerneloops-1.1.14-1-fc14.i686
abrt-addon-python-1.1.14-1-fc14.i686
abrt-desktop-1.1.14-1-fc14.i686
abrt-gui-1.1.14-1-fc14.i686
abrt-libs-1.1.14-1-fc14.i686
abrt-plugin-bugzilla-1.1.14-1-fc14.i686
abrt-plugin-logger-1.1.14-1-fc14.i686
abrt-plugin-runapp-1.1.14-1-fc14.i686
acl-2.2.49-8-fc14.i686
...
```

如预期的，`rpm.list`文件中的数据已经排序好了！

管道流行的用法之一是将产生长输出的命令管道到`more`命令。这在使用`ls`命令时非常常见，如图 10.2 所示。

图 10.2 使用 more 命令配合 ls 命令![](img/00017.jpg)

`ls -l`命令产生目录下所有文件的详细列表。对于包含大量文件的目录，可以通过管道输出到`more`命令强制输出在每屏停止。

## 执行数学运算

任何编程语言的另一个关键特性是操作数字。遗憾的是，对于脚本来说，这个过程有点笨拙。在脚本中有两种不同的方法执行数学操作。

### expr 命令

最初，Bourne shell 提供了一个用于处理数学表达式的特殊命令。`expr`允许从命令行处理表达式，但它非常笨拙：

```bash
$ expr 1 + 5
6
```

`expr`命令识别几种不同的数学和字符串运算符，如表 10.1 所示。

表 10.1 expr 运算符

| 运算符 | 说明 |
| :--- | :--- |
| `ARG1 \| ARG2` | 如果两个参数都不为空或零，则返回`ARG2`。 |
| `ARG1 & ARG2` | 如果两个参数都不为空或零，则返回 0。 |
| `ARG1 < ARG2` | 如果`ARG1`小于`ARG2`，则返回 1。 |
| `ARG1 <= ARG2` | 如果`ARG1`小于或等于`ARG2`，则返回 1。 |
| `ARG1 = ARG2` | 如果`ARG1`等于`ARG2`，则返回 1。 |
| `ARG1 != ARG2` | 如果`ARG1`不等于`ARG2`，则返回 1。 |
| `ARG1 >= ARG2` | 如果`ARG1`大于或等于`ARG2`，则返回 1。 |
| `ARG1 > ARG2` | 如果`ARG1`大于`ARG2`，则返回 1。 |
| `ARG1 + ARG2` | 返回`ARG1`和`ARG2`的和。 |
| `ARG1 - ARG2` | 返回`ARG1`和`ARG2`的差。 |
| `ARG1 * ARG2` | 返回`ARG1`和`ARG2`的乘积。 |
| `ARG1 / ARG2` | 返回`ARG1`除以`ARG2`的商。 |
| `ARG1 % ARG2` | 返回`ARG1`除以`ARG2`的余数。 |
| `ARG1 \| ARG2` | 返回`ARG1`和`ARG2`的按位或。 |
| `ARG1 & ARG2` | 返回`ARG1`和`ARG2`的按位与。 |
| `ARG1 ^ ARG2` | 返回`ARG1`和`ARG2`的按位异或。 |
| `ARG1 << ARG2` | 返回`ARG1`向左移动`ARG2`位。 |
| `ARG1 >> ARG2` | 返回`ARG1`向右移动`ARG2`位。 |

### 使用括号

bash shell 包含了`expr`命令以保持与 Bourne shell 的兼容；然而，它也提供了一种更简单的方法来执行数学表达式。在 bash 中，给变量赋值数学值时，你可以使用美元符号和方括号来封装数学表达式（`$[ operation ]`）：

```bash
$ var1=$[1 + 5]
$ echo $var1
6
$ var2 =[$var1 * 2]
$ echo $var2
12
```

使用括号让 shell 数学比使用`expr`命令简单得多。这种技术也适用于脚本：

```bash
$ cat test7
#!/bin/bash
var1=100
var2=50
var3=45
var4=$[$var1 * ($var2 - $var3)]
echo The final result is $var4
```

运行此脚本产生输出：

```bash
$ chmod u+x test7
$ ./test7
The final result is 500
```

此外，请注意，在使用方括号方法计算方程时，你不需要担心乘法符号或其他任何字符会被 shell 误解。shell 知道它不是通配符，因为它位于方括号内部。

在 bash shell 脚本中执行数学运算有一个很大的局限性。请看这个例子：

```bash
$ cat test8
#!/bin/bash
var1=100
var2=45
var3=$[$var1 / $var2]
echo The final result is $var3
$
```

现在运行它看看会发生什么：

```bash
$ chmod u+x test8
$ ./test8
The final result is 2
$
```

bash shell 的数学运算符仅支持整数算术。如果你正尝试进行任何现实世界的数学计算，这是一个巨大的局限性。

> 注意
>
> > z shell (zsh) 提供了完整的浮点算术运算。如果你在 shell 脚本中需要浮点计算，可以考虑查看 z shell（在第 22 章讨论）。

## 浮点数解决方案

有多种方法可以克服 bash 的整数限制。最流行的解决方案是使用 bash 内置的计算器，名为`bc`。

### bc 基础

bash 计算器实际上是一种编程语言，它允许你在命令行输入浮点数表达式，然后解释这些表达式、计算它们并返回结果。bash 计算器识别：

* 数字（整数和浮点数）
* 变量（简单变量和数组）
* 注释（以 # 号开头的行或 C 语言的`/* */`成对符号）
* 表达式
* 编程语句（如`if-then`语句）
* 函数

你可以使用`bc`命令从 shell 提示符访问 bash 计算器：

```bash
$ bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type ‘warranty’.
12 * 5.4
64.8
3.156 * (3 + 5)
25.248
quit
$
```

示例首先输入表达式`12 * 5.4`。bash 计算器返回答案。随后输入计算器的每个表达式都会被求值并显示结果。要退出 bash 计算器，必须输入`quit`。

浮点算术由一个名为`scale`的内置变量控制。你必须将此值设置为答案中所需的的小位数，否则你无法得到想要的结果：

```bash
$ bc -q
3.44 / 5
0
scale=4
3.44 / 5
.6880
quit
$
```

`scale`变量的默认值为零。在设置`scale`值之前，bash 计算器提供保留零位小数的答案。当你将`scale`变量值设置为四后，bash 计算器将显示四位小数的答案。`-q`命令行参数会抑制 bash 计算器的冗欢迎信息。

除了普通数字，bash 计算器还能理解变量：

```bash
$ bc -q
var1=10
var1 * 4
40
var2 = var1 / 5
print var2
2
quit
$
```

一旦定义了变量值，你就可以在整个 bash 计算器会话中使用该变量。`print`语句允许你打印变量和数字。

### 在脚本中使用 bc

现在你可能想知道 bash 计算器如何帮助你在 shell 脚本中进行浮点运算。你还记得你的朋友反引号字符吗？是的，你可以使用反引号运行`bc`命令并将输出赋值给变量！使用它的基本格式是：

`variable='echo "options; expression" | bc'`

第一部分`options`允许你设置变量。如果你需要设置多个变量，请使用分号将它们分开。`expression`参数定义了使用`bc`求值的数学表达式。这里有一个在脚本中执行此操作的示例：

```bash
$ cat test9
#!/bin/bash
var1='echo "scale=4; 3.44 / 5" | bc'
echo The answer is $var1
$
```

此示例将`scale`变量设置为四小数，然后为表达式指定了特定的计算。运行此脚本会产生以下输出：

```bash
$ chmod u+x test9
$ ./test9
The answer is .6880
$
```

这太酷了！你并不局限于在表达式值中使用数字。你还可以使用 shell 脚本中定义的变量：

```bash
$ cat test10
#!/bin/bash
var1=100
var2=45
var3='echo "scale=4; $var1 / $var2" | bc'
echo The answer for this is $var3
$
```

脚本定义了两个变量，这些变量在发送到`bc`命令的表达式中使用。记得使用美元符号`$`表示变量的值而不是变量本身。该脚本的输出如下：

```bash
$ ./test10
The answer for this is 2.2222
$
```

当然，一旦将值赋值给变量，该变量就可以在另一个计算中使用：

```bash
$ cat test11
#!/bin/bash
var1=20
var2=3.14159
var3='echo "scale=4; $var1 * $var1" | bc'
var4='echo "scale=4; $var3 * $var2" | bc'
echo The final result is $var4
$
```

这种方法对于短计算非常良好，但有时你需要处理更复杂的数字。如果你有不仅仅几个计算，尝试在同一行上列出多个表达式会变得很混乱。

这个问题有一个解决方案。`bc`命令识别输入重定向，允许你将文件重定向到`bc`命令进行处理。然而这也会变得混乱，因为你需要将表达式存储在文件中。

最好的方法是使用输入重定向，它允许直接从命令行重定向数据。在 shell 脚本中，我们将输出赋值给变量：

`variable='bc << EOF
options
statements
expressions
EOF'`

`EOF`字符串表示内联数据的开始和结束。记得仍然需要反引号将`bc`的输出赋值给变量。这里在脚本中使用此方法的示例：

```bash
$ cat test12
#!/bin/bash
var1=10.46
var2=43.67
var3=33.2
var4=71
var5='bc << EOF
scale = 4
a1 = ($var1 * $var2)
b1 = ($var3 * $var4)
a1 + b1
EOF'
echo The final answer for this is $var5
$
```

在脚本中将每个选项和表达式单独放在一行会让代码更整洁、更易读。

## 退出脚本

到目前为止，在我们的示例脚本中，我们结束得相当粗略。当我们完成最后一个命令时，直接结束了脚本。我们有更优雅的方式来完成任务。

每个在 shell 中运行的命令都使用一个`exit status`（退出状态）来告知 shell 它已完成。退出状态是一个 0 到 255 之间的整数值，由命令在运行结束时传递给 shell。你可以捕获此值并在脚本中使用它。

### 检查退出状态

Linux 提供了特殊变量`$?`，它存储了上一个执行命令的退出状态值。你必须在想要检查的命令之后立即查看或使用`$?`变量。它会变变为 shell 执行的最后一个命令的退出状态：

```bash
$ date
Sat Jan 15 10:01:30 EDT 2011
$ echo $?
0
$
```

按照惯例，成功完成的命令退出状态为零。如果命令带错误完成，则会将一个正整数值赋予退出状态中：

```
$ asdfg
-bash: asdfg: command not found
$ echo $?
127
$
```

无效命令返回的退出状态为`127`。Linux 的错误退出状态码并没有太多的标准。不过，你可以使用一些指南，如表 10.2 所示。

### 表 10.2 Linux 退出状态码

| 代码 | 说明 |
| :--- | :--- |
| 0 | 命令成功完成 |
| 1 | 通用未知错误 |
| 2 | Shell 命令误用 |
| 126 | 命令无法执行 |
| 127 | 未找到命令 |
| 128 | 无效的退出参数 |
| 128+x | Linux 信号 x 致命错误 |
| 130 | 命令通过 Ctrl+C 终止 |
| 255 | 退出状态超出范围 |

退出状态值`126`表示用户没有设置执行该命令的适当权限：

```
$ ./myprog.c
-bash: ./myprog.c: Permission denied
$ echo $?
126
$
```

你遇到的另一个常见错误是在向命令提供无效参数时发生的：

```
$ date %t
date: invalid date ‘%t’
$ echo $?
1
$
```

这会产生通用的退出状态码 1，表示命令中发生了未知错误。

## exit 命令

默认情况下，你的 shell 脚本将以脚本中最后一个命令的退出状态退出：

```
$ ./test6
The result is 2
$ echo $?
0
$
```

你可以更改它以返回你自己的退出状态码。`exit`命令允许你在脚本结束时指定一个退出状态：

```
$ cat test13
#!/bin/bash
# testing the exit status
var1=10
var2=30
var3=$[ $var1 + $var2 ]
echo The answer is $var3
exit 5
$
```

当你检查脚本的退出状态时，将得到作为`exit`命令参数使用的值：

```
$ chmod u+x test13
$ ./test13
The answer is 40
$ echo $?
5
$
```

你也可以在`exit`命令的参数中使用变量：



```
$ cat test14
#!/bin/bash
# testing the exit status
var1=10
var2=30
var3=$[ $var1 + $var2 ]
exit $var3
$
```

当你运行此命令时，它会产生以下退出状态：

```
$ chmod u+x test14
$ ./test14
$ echo $?
40
$
```

然而，你应该在使用此功能时要小心，因为退出状态码只能到到`255`。请看这个例子中发生了什么：

```
$ cat test14b
#!/bin/bash
# testing the exit status
var1=10
var2=30
var3=$[ $var1 * $var2 ]
echo The value is $var3
exit $var3
$
```

现在当你运行它时，你会得到以下：

```
$ ./test14b
The value is 300
$ echo $?
44
$
```

退出状态码被缩小以适应`0`到`255`的范围。shell通过使用模运算来实现这一点。一个值的“模”是除法后的余数。结果数字是指定数字除以`256`的余数。在`300`（结果值）的情况下，余数为`44`，这就是显示的退出状态码。

在第11章，你将看到如何使用`if-then`语句检查命令返回的错误状态，以判断命令是否成功。

## 总结

bash shell脚本允许你将命令组合成脚本。创建脚本最基本的方法是使用分号分隔命令行上的多个命令。shell会按顺序执行每个命令，并在显示器上显示每个命令的输出。

你也可以创建一个shell脚本文件，将多个命令放在文件中让shell按顺序执行。shell脚本文件必须定义用于运行脚本的shell。这是通过脚本文件的第一行实现的，使用`#!`符号，后跟shell的完整路径。

在shell脚本中，你可以通过在变量前使用美元符号来引用环境变量的值。你也可以定义供脚本内部使用的自定义变量，并使用反引号字符赋值甚至赋值命令的输出。通过在变量名前前放置美元符号，可以在脚本中使用变量值。

bash shell允许你从标准行为中重定向命令的输入和输出。你可以使用大于符号后跟捕捉输出的文件名，将任何命令的输出从显示器显示重定向到文件。你可以使用两个大于符号将输出数据追加到现有文件中。小于符号用于将输入重定向到命令。你可以将输入从文件重定向到命令。

Linux`pipe`命令（竖线符号）允许你将一个命令的输出直接重定向到另一个命令的输入。Linux系统同时运行这两个命令，在不使用任何重定向文件的情况下将第一个命令的输出发送到第二个命令的输入。

bash shell提供了几种在你的脚本中执行数学运算的方法。`expr`命令是执行整数运算的简单方法。在bash shell中，你还可以通过将方程包含在方括号中并在前面加上美元符号来执行基础数学计算。要执行浮点运算，你需要利用`bc`计算器命令，从内联数据重定向输入并将输出存储在用户变量中

最后，本章讨论了如何在shell脚本中使用退出状态。在shell中运行的每个命令都会产生一个退出状态。退出状态是一个`0`到`255`之间的整数值，表示命令是否成功完成，如果没有，原因是什么。退出状态`0`表示命令成功完成。你可以在shell脚本中使用`exit`命令来声明特定的退出状态。

# 第 11 章：使用结构化命令

### 本章

*   使用`if-then`语句

*   `if-then-else`语句

*   嵌套`if`

*   `test`命令

*   复合条件测试

*   高级`if-then`特性

*   `case`命令

*   管理用户账户

### 使用 if-then 语句

最基本的结构化命令类型是`if-then`语句。`if-then`语句具有以下格式：

```
if command
then
commands
fi
```

如果你在其他编程语言中使用`if-then`语句，这种格式可能会让你有些困惑。在其他编程语言中，`if`语句后面的对象是一个被求值为`TRUE`（真）或`FALSE`（假）的等式。但这并不是bash shell`if`语句的工作方式。

bash shell `if`语句运行在`if`行上定义的命令。如果命令的退出状态（参见第10章）为`0`（表示命令成功完成），则执行`then`部分列出的命令。如果命令的退出状态为任何其他值，则不执行`then`部分的命令，bash shell将继续执行脚本中的下一个命令。

这里有一个简单的示例来演示这个概念：

```bash
$ cat test1
#!/bin/bash
# testing the if statement
if date
then
    echo "it worked"
fi
```

该脚本在`if`行上使用了`date`命令。如果命令成功完成，`echo`语句将显示该文本字符串。当你从命令行运行此脚本时，将得到以下结果：

```bash
$ ./test1
Sat Jan 23 14:09:24 EDT 2011
it worked
$
```

shell执行了`if`行上列出的`date`命令。由于退出状态为`0`，它还执行了`then`部分列出的`echo`语句。

另一个示例：

```bash
$ cat test2
#!/bin/bash
# testing a bad command
if asdfg
then
    echo "it did not work"
fi
echo "we are outside of the if statement"
$
$ ./test2
./test2: line 3: asdfg: command not found
we are outside of the if statement
$
```

在这个示例中，我们故意在`if`语句行中使用了一个无法运行的命令。因为这是一个错误的命令，它会产生一个非零的退出状态，bash shell跳过了`then`部分的`echo`语句。同样注意，在`if`语句中运行命令时产生的错误信息仍然出现在脚本的输出中。在某些情况下，你可能不希望发生这种情况。第14章讨论了如何避免这种情况。

`then`部分并不局限于一个命令。你可以像在shell脚本的其他部分一样列出命令。bash shell将这些命令视为一个块，当`if`语句行中的命令返回零退出状态时执行执行所有命令，或者当命令返回非零退出状态时跳过所有命令：

```bash
$ cat test3
#!/bin/bash
# testing multiple commands in the then section
testuser=rich
if grep $testuser /etc/passwd
then
    echo The bash files for user $testuser are:
    ls -a /home/$testuser/.b*
fi
```

`if`语句行使用`grep`命令来搜索`/etc/passwd`文件，以检查特定的用户名是否正被系统使用。如果存在该登录名的用户，脚本将显示一些文本，然后列出用户`HOME`目录下的bash文件：

```bash
$ ./test3
rich:x:500:500:Rich Blum:/home/rich:/bin/bash
The files for user rich are:
/home/rich/.bash_history  /home/rich/.bash_profile
/home/rich/.bash_logout   home/rich/.bashrc
$
```

然而，如果你将`testuser`变量设置为系统上不存在的用户，则什么都不会发生：

```bash
$ ./test3
$
```

这并没有什么特别有趣的。如果我们能显示一条小消息，说明在系统中未找到该用户名，那就好了。嗯，我们可以使用`if-then`语句的另一个功能来实现这一点。

> 注意

> 你可能会在某些脚本中看到`if-then`语句的另一种形式：

> ```bash
> if command; then
> commands
> fi
> ```

> 通过在待求值的命令末尾加上分号，你可以将`then`语句包含在同一行中，这看起来更像其他编程语言中处理`if-then`语句的方式。

## if-then-else 语句

在`if-then`语句中，你对于命令是否成功只有一种选择。如果命令返回非零退出状态码，bash shell只是移动到脚本中的下一个命令。在这种情况下，如果能够执行另一组命令就太好了。而这正是`if-then-else`语句的用途。

`if-then-else`语句在语句中提供了另一组命令：

```bash
if command
then
commands
else
commands
fi
```

当`if`语句行中的命令返回退出状态码`0`时，执行`then`部分列出的命令，就像在普通的`if-then`语句中一样。当`if`语句行中的命令返回非零退出状态码时，bash shell执行`else`部分的命令。

现在你可以修改测试脚本使其如下所示：

```bash
$ cat test4
#!/bin/bash
# testing the else section
testuser=badtest
if grep $testuser /etc/passwd
then
    echo The files for user $testuser are:
    ls -a /home/$testuser/.b*
else
    echo "The user name $testuser does not exist on this system"
fi
$
$ ./test4
The user name badtest does not exist on this system
$
```

这样更对用户友好。与`then`部分一样，`else`部分也可以包含多个命令。`fi`语句界定了`else`部分的结束。

## 嵌套 if

有时你必须在脚本代码中检查几种情况。与其编写单独的`if-then`语句，你可以使用`else`部分的替代版本，称为`elif`。

`elif`使用另一个`if-then`继续接在`else`部分：

```bash
if command1
then
commands
elif command2
then
commands
fi
```

`elif`语句行提供了另一个待求值的命令，类似于`if`语句。如果来自`elif`的退出状态为`0`，bash将执行`then`部分。

你可以连续将`elif`语句连接在一起，创建一个`if-then-elif`：

```bash
if command1
then
commands set1
elif command2
then
commands set2
elif command3
then
commands set3
elif command4
then
commands set4
fi
```

每个命令块的执行取决于哪个命令返回了零退出状态。请记住，bash shell会按顺序执行`if`语句，只有第一个返回零退出状态的语句会导致`then`部分被执行。在后面的“case命令”章节中，你将看到如何使用`case`命令而不是需要嵌套大量的`if-then`语句。

## test 命令

到目前为止，你在`if`语句行中看到的都是普通的shell命令。你可能认为`if-then`语句是否具有评估命令退出状态之外的任何条件的能力。

答案是否定的。但是，bash shell中有一个实用的工具，可以帮助你使用`if-then`语句评估其他内容。

`test`命令提供了一种在`if-then`语句中测试不同条件的方法。如果`test`命令列出的条件求值为真，则`test`命令以零退出状态退出，使得`if-then`语句的行为与其他编程语言中的`if-then`语句非常相似。如果条件为假，`test`命令以`1`退出，这会导致`if-then`语句失败。

`test`命令的格式非常简单：

```bash
test condition
```

在`if-then`语句中使用时，`test`命令如下：

```bash
if test condition
then
commands
fi
```

bash shell提供了另一种在`if-then`语句中声明`test`命令的方法：

```bash
if [ condition ]
then
commands
fi
```

方括号定义了`test`命令中使用的条件。请注意：你必须在第一个括号之后有一个空格，在最后一个括号之前也有一个空格，否则你将收到错误信息。

`test`命令可以评估三类条件：

*   数值比较

*   字符串比较

*   文件比较

接下来的章节将描述如何在你的`if-then`语句中使用这些类别的测试。

## 数值比较

使用`test`命令最常用的方法是对两个数值进行比较。表11.1显示了用于测试两个值时使用的条件参数列表。

表 11.1 test 命令：数值比较

| 比较 | 说明 |

| :--- | :--- |

| `n1 -eq n2` | 检查`n1`是否等于`n2`。 |

| `n1 -ge n2` | 检查`n1`是否大于或等于`n2`。 |

| `n1 -gt n2` | 检查`n1`是否大于`n2`。 |

| `n1 -le n2` | 检查`n1`是否小于或等于`n2`。 |

| `n1 -lt n2` | 检查`n1`是否小于`n2`。 |

| `n1 -ne n2` | 检查`n1`是否不等于`n2`。 |

数值测试条件可以用于评估数字和变量。这里是一个示例：

```bash
$ cat test5
#!/bin/bash
# using numeric test comparisons
val1=10
val2=11
if [ $val1 -gt 5 ]
then
    echo "The test value $val1 is greater than 5"
fi
if [ $val1 -eq $val2 ]
then
    echo "The values are equal"
else
    echo "The values are different"
fi
```

第一个测试条件：

```bash
if [ $val1 -gt 5 ]
```

测试变量`val1`的值是否大于`5`。第二个测试条件：

```bash
if [ $val1 -eq $val2 ]
```

测试变量`val1`的值是否等于变量`val2`的值。运行脚本并观察结果：

```bash
$ ./test5
The test value 10 is greater than 5
The values are different
$
```

两个数值测试条件都按照预期通过了评估。

然而，数值测试条件存在局限性。尝试这个脚本：

```bash
$ cat test6
#!/bin/bash
# testing floating point numbers
val1=' echo "scale=4; 10 / 3 " | bc'
echo "The test value is $val1"
if [ $val1 -gt 3 ]
then
    echo "The result is larger than 3"
fi
$
$ ./test6
The test value is 3.3333
./test6: line 5: : 3.3333: integer expression expected
$
```

这个示例使用bash计算器产生一个浮点值，并将其存储在变量`val1`中。接下来，它使用`test`命令评估该值。这里显然出现了问题。

在第10章中，你学习了如何欺骗bash shell处理浮点值；但这个脚本仍然存在问题。`test`命令无法处理存储在变量`val1`中的浮点值。

请记住，bash shell能够处理的数字只有整数。当你使用bash计算器时，你只是欺骗shell将浮点值作为字符串值存储在变量中。如果你只需要使用`echo`语句显示结果，这运行得良好，但在以数值为导向的函数（例如我们的数值测试条件）中这不起作用。结论是，你无法在`test`命令中使用浮点值。

## 字符串比较

`test`命令还允许你对字符串值进行比较。正如你所看到的，对字符串进行比较可能会变得复杂。表11.2显示了你可以用于评估两个字符串值的比较函数。

表 11.2 test 命令：字符串比较

| 比较 | 说明 |

| :--- | :--- |

| `str1 = str2` | 检查`str1`是否与字符串`str2`相同。 |

| `str1 != str2` | 检查`str1`是否不等于`str2`。 |

| `str1 < str2` | 检查`str1`是否小于`str2`。 |

| `str1 > str2` | 检查`str1`是否大于`str2`。 |

| `-n str1` | 检查`str1`的长度是否大于零。 |

| `-z str1` | 检查`str1`的长度是否为零。 |

接下来的章节描述了各种不同的字符串比较。

### 字符串相等

对于字符串来说，相等和不等的条件是非常显而易见的。判断两个字符串值是否相同很容易：



```bash
$cat test7
#!/bin/bash
# testing string equality
testuser=rich
if [ $USER = $testuser ]
then
    echo "Welcome $testuser"
fi
$
$ ./test7
Welcome rich
$
```

此外，使用不等于字符串比较，可以让你判断两个字符串的值是否相同：

```bash
$ cat test8
#!/bin/bash
# testing string equality
testuser=baduser
if [ $USER != $testuser ]
then
    echo "This is not $testuser"
else
    echo "Welcome $testuser"
fi
$
$ ./test8
This is not baduser
$
```

`test`比较在比较字符串的相等性时会考虑所有的标点符号和大小写。

## 字符串顺序

尝试确定一个字符串是否小于或大于另一个字符串是事情开始变得复杂的地方。当 shell 程序员尝试使用`test`命令的大于或小于功能时，经常有两个问题困扰着他们：

- 大于和小于符号必须进行转义，否则 shell 将它们用作重定向符号。
- 大于和小于的顺序与`sort`命令中使用的顺序不同。

第一个问题在编写脚本时可能会导致一个未察觉的问题。这里是初学者 shell 程序员有时会遇到的一个典型示例：

```bash
$ cat badtest
#!/bin/bash
# mis-using string comparisons
val1=baseball
val2=hockey
if [ $val1 > $val2 ]
then
    echo "$val1 is greater than $val2"
else
    echo "$val1 is less than $val2"
fi
$
$ ./badtest
baseball is greater than hockey
$ ls -l hockey
-rw-r--r-- 1 rich Sep 30 19:08 hockey
$
```

在脚本中使用大于符号没有产生错误，但结果是错误的。脚本将大于符号解释为输出重定向。因此，它创建了一个名为`hockey`的文件。因为重定向成功，`test`命令返回零退出代码，`if`认为操作执行了！

要解决这个问题，你需要正确转义大于符号：

```bash
$ cat test9
#!/bin/bash
# mis-using string comparisons
val1=baseball
val2=hockey
if [ $val1 \> $val2 ]
then
    echo "$val1 is greater than $val2"
else
    echo "$val1 is less than $val2"
fi
$
$ ./test9
baseball is less than hockey
$
```

现在的答案更符合你对字符串比较的预期。

第二个问题更为微妙，除非你处理大写和小写字母，否则你可能不会遇到它。`sort`命令处理大写字母的方式与`test`命令考虑相反。让我们在脚本中测试这个功能：

```bash
$ cat test9b
#!/bin/bash
# testing string sort order
val1=Testing
val2=testing
if [ $val1 \> $val2 ]
then
    echo "$val1 is greater than $val2"
else
    echo "$val1 is less than $val2"
fi
$
$ ./test9b
Testing is less than testing
$
sort testfile
testing
Testing
$
```

在`test`命令中，大写字母被认为其值小于小写字母。然而，当你将相同的字符串放入文件中并使用`sort`命令时，小写字母会先出现。这是由于每个命令所使用的排序技术不同。`test`命令使用标准的 ASCII 排序，利用每个字符的 ASCII 数值来确定排序顺序。`sort`命令则使用系统区域（locale）语言设置定义的排序顺序。对于英语，区域设置规定在排序顺序中小写字母在大写字母之前。

> **注意**
>
> 请注意，`test`命令使用标准的数学比较符号进行字符串比较，并使用文本代码进行数值比较。这是一个微妙的特性，许多程序员经常会弄反它。如果你使用数学比较符号来处理数值，shell 会将其解释为字符串值，并可能产生错误的结果。

## 字符串长度

在尝试评估变量是否包含数据时，`-n`和`-z`比较非常有用：

```bash
$ cat test10
#!/bin/bash
# testing string length
val1=testing
val2=''
if [ -n $val1 ]
then
    echo "The string '$val1' is not empty"
else
    echo "The string '$val1' is empty"
fi
if [ -z $val2 ]
then
    echo "The string '$val2' is empty"
else
    echo "The string '$val2' is not empty"
fi
if [ -z $val3 ]
then
    echo "The string '$val3' is empty"
else
    echo "The string '$val3' is not empty"
fi
$ 
$ ./test10
The string 'testing' is not empty
The string '' is empty
The string '' is empty
$
```

此示例创建了两个变量。`val1`变量包含一个字符串，`val2`变量被创建为空字符串。如下所示进行了相应的比较：

`if [ -n $val1 ]`确定`val1`变量长度是否不为零，确实如此，因此处理了`then`部分：

`if [ -z $var2 ]`确定`val2`变量长度是否为零，确实如此，因此处理了`then`部分：

`if [ -z $val3 ]`确定`val3`变量长度是否为零。该变量在 shell 脚本从未定义，因此即使它没有被定义，也表示字符串长度为零。

> **注意**
>
> 空变量和未初始化的变量会对你的 shell 脚本测试产生灾难性的影响。如果你不确定变量的内容，在将其用于数值或字符串比较之前，最好先使用`-n`或`-z`测试变量是否包含值。

## 文件比较

最后一类`test`比较可能是 shell 脚本编写中最强大且最常用的比较。`test`命令允许你测试 Linux 文件系统上文件和目录的状态。表 11.3 列出了这些比较方法。

### 表 11.3 test 命令的文件比较

| 比较操作符 | 描述 |
| :--- | :--- |
| `-d file` | 检查`file`是否存在且是一个目录。 |
| `-e file` | 检查`file`是否存在。 |
| `-f file` | 检查`file`是否存在且是一个文件。 |
| `-r file` | 检查`file`是否存在且可读。 |
| `-s file` | 检查`file`是否存在且不为空。 |
| `-w file` | 检查`file`是否存在且可写。 |
| `-x file` | 检查`file`是否存在且可执行。 |
| `-O file` | 检查`file`是否存在并属于当前用户。 |
| `-G file` | 检查`file`是否存在且默认组是否与当前用户相同。 |
| `file1 -nt file2` | 检查`file1`是否比`file2`新。 |
| `file1 -ot file2` | 检查`file1`是否比`file2`旧。 |

这些条件让你能够在 shell 脚本中检查文件系统中的文件，并且它们通常被用于访问文件的脚本中。由于它们被频繁使用，让我们逐一查看每一个。

### 检查目录

`-d`测试检查指定的路径在系统中是否以目录的形式存在。如果你尝试向某个目录写入文件，或者在尝试切换目录之前，这通常是一个很好的做法：

```bash
$ cat test11
#!/bin/bash
# look before you leap
if [ -d $HOME ]
then
    echo "Your HOME directory exists"
    cd $HOME
    ls -a
else
    echo "There is a problem with your HOME directory"
fi
$ 
$ ./test11
"Your HOME directory exists"
.      Documents       .gvfs           .pulse-cookie
..      Downloads      .ICEauthority    .recently-used.xbel
.aptitude               .esd_auth      .local         
.sudo_as_admin_successful
.bash_history      examples        .desktop    .mozilla      Templates
.bash_logout          .fontconfig    Music      test11
.bashrc               .gconf        .nautilus  Videos
.cache               .gconfd        .openoffice.org        
.xsession-errors
.config               .gksu.lock   Pictures      .gnome-session
.gnome-session.profile
.xsession-errors.old
```

### 检查对象是否存在

`-e`比较允许你检查文件或目录是否存在。在尝试使用文件之前，你应该检查它：

```bash
$ cat test12
#!/bin/bash
# checking if file exists
if [ -e $file ]
then
    echo "The file exists"
else
    echo "The file does not exist"
fi
```

### 检查文件

`-e`比较同时适用于文件和目录。为了确保对象是一个文件，你必须使用`-f`比较：

```bash
$ cat test13
#!/bin/bash
# check if it is a file
if [ -e $HOME ]
then
    echo "The object exists, is it a file?"
    if [ -f $HOME ]
    then
        echo "Yes, it is a file!"
    else
        echo "No, it is not a file!"
        if [ -f $HOME/.bash_history ]
        then
            echo "But this is a file!"
        fi
    fi
else
    echo "Sorry, the object does not exist"
fi
```

### 你能读取吗？

在尝试从文件中读取数据之前，先测试你是否可以读取该文件通常是一个好主意。你通过`-r`比较来实现这一点：

```bash
$ cat test14
#!/bin/bash
# testing if you can read a file
```

`pwfile=/etc/shadow`

```bash
# first, test if the file exists, and is a file
if [ -f $pwfile ]
then
    # now test if you can read it
    if [ -r $pwfile ]
    then
        tail $pwfile
    else
        echo "Sorry, I am unable to read the $pwfile file"
    fi
else
    echo "Sorry, the file $file does not exist"
fi
```

```bash
$ ./test14
Sorry, I am unable to read the /etc/shadow file
$
```

`/etc/shadow`文件包含系统用户的加密密码，因此系统上的普通用户无法读取。`-r`比较判断我没有对该文件的读取权限，因此测试命令失败，bash 终端执行了`if-then`语句的`else`部分。

### 检查空文件

你应该使用`-s`比较来检查文件是否为空，特别是当你尝试删除一个文件时。要小心，因为当`-s`比较成功时，表示文件中包含数据：

```bash
$ cat test15
#!/bin/bash
# testing if a file is empty
file=t15test
touch $file
if [ -s $file ]
then
    echo "The $file file exists and has data in it"
else
    echo "The $file exists and is empty"
fi
date > $file
if [ -s $file ]
then
    echo "The $file file has data in it"
else
    echo "The $file is still empty"
fi
```

```bash
$ ./test15
The t15test exists and is empty
The t15test file has data in it
$
```

`touch`命令创建文件但不会向其中放入任何数据。在我们使用`date`命令并将输出重定向到文件后，`-s`比较指示文件中存在数据。

### 检查你是否可以写入文件

`-w`比较判断你是否有权限写入文件：

```bash
$ cat test16
#!/bin/bash
# checking if a file is writeable
logfile=$HOME/t16test
touch $logfile
chmod u-w $logfile
now='date +Y%m%d-%H%M'
if [ -w $logfile ]
then
    echo "The program ran at: $now" > $logfile
    echo "The first attempt succeeded"
else
    echo "The first attempt failed"
fi
chmod u+w $logfile
if [ -w $logfile ]
then
    echo "The program ran at: $now" > $logfile
    echo "The second attempt succeeded"
else
    echo "The second attempt failed"
fi
```

```bash
$ ./test16
The first attempt failed
The second attempt succeeded
$ cat $HOME/t16test
The program ran at: 20110124-1602
$
```

这是一个不错的 shell 脚本！首先，它在你的`$HOME`目录下定义了一个日志文件，将其文件名存储在`logfile`中，创建该文件，然后移除用户的写入权限。接下来，它创建了变量`now`并使用`date`命令存储时间戳。在完成这一切之后，它检查你是否有对日志文件的写入权限（你刚刚删除了该权限）。因为你没有写入权限，你应该看到失败的消息。之后，脚本再次使用`chmod`命令为用户重新授予写入权限，并尝试写入文件。这次写入成功了。

### 检查你是否可以运行文件

`-x`比较是判断你是否对某个文件具有执行权限的方便方法。虽然对于大多数命令可能不需要，但如果你在 shell 中运行很多脚本，它就会派上用场：

```bash
$ cat test17
#!/bin/bash
# testing file execution
if [ -x test16 ]
then
    echo "You can run the script: "
./test16
else
    echo "Sorry, you are unable to execute the script"
fi
```

```bash
$ ./test17
You can run the script:
The first attempt failed
The second attempt succeeded
$ chmod u-x test16
$ ./test17
Sorry, you are unable to execute the script
$
```

这个示例 shell 脚本使用`-x`比较来测试你是否有权限执行`test16`脚本。如果是，它就会运行脚本（注意，即使在 shell 脚本中，你也必须为执行不在你的`$PATH`中的脚本提供正确的路径）。在第一次运行`test16`脚本后更改它的权限并再次尝试。这次，`-x`比较失败了，因为你没有对`test16`脚本的执行权限。

### 所有权

`-O`比较允许你轻松测试自己是否是文件的所有者：



```bash
$ cat test18
#!/bin/bash
# check file ownership
if [ -O /etc/passwd ]
then
    echo “You are the owner of the /etc/passwd file”
else
    echo “Sorry, you are not the owner of the /etc/passwd file”
fi
```

```bash
$ ./test18
Sorry, you are not the owner of the /etc/passwd file
$ su
Password:
$
# ./test18
You are the owner of the /etc/passwd file
#
```

脚本使用 `-O` 比较来测试运行脚本的用户是否为`/etc/passwd`文件的所有者。脚本第一次在普通用户账户下运行时失败。第二次，我们使用`su`命令变成`root`用户，测试成功了。

### 检查默认组成员身份

`-G`比较检查文件的默认组，如果该组与用户的默认组匹配，则测试成功。这可能会有点困惑，因为`-G`比较只检查默认组，而不检查用户所属的所有组。这里有一个示例：

```bash
$ cat test19
#!/bin/bash
# check file group test
if [ -G $HOME/testing ]
then
    echo “You are in the same group as the file”
else
    echo “The file is not owned by your group”
fi
```

```bash
$ ls -l $HOME/testing
-rw-rw-r-- 1 rich rich 58 2011-01-30 15:51 /home/rich/testing
$
$ ./test19
You are in the same group as the file
$
$ chgrp rich $HOME/testing
$ ./test19
The file is not owned by your group
```

第一次运行脚本时，`$HOME/testing`属于`rich`组，`-G`比较成功。

### 检查日期

最后一组比较处理两个文件的创建时间。这在编写脚本时非常有用。有时你不想安装一个较旧的文件。`-nt`比较判断文件是否较新。如果文件较新，它将有更的创建时间。`-ot`比较判断文件是否较旧。如果文件较旧，它将有更早的创建时间：

```bash
$ cat test20
#!/bin/bash
# testing file dates
if [ ./test19 -nt ./test18 ]
then
    echo “The test19 file is newer than test18”
else
    echo “The test18 file is newer than test19”
fi
if [ ./test17 -ot ./test19 ]
then
    echo “The test17 file is older than the test19 file”
fi
```

```bash
$ ./test20
The test19 file is newer than test18
The test17 file is older than the test19 file
$
$ ls -l test17 test18 test19
-rwxrw-r-- 1 rich rich 167 2011-01-30 16:31 test17
-rwxrw-r-- 1 rich rich 185 2011-01-30 17:46 test18
```

文件路径是相对于你运行脚本的目录的。如果你检查的文件可以移动，这就会产生问题。另一个问题是，这两个比较都没有先检查文件是否存在。尝试这个测试：

```bash
$ cat test21
#!/bin/bash
# testing file dates
if [ ./badfile1 -nt ./badfile2 ]
then
    echo “The badfile1 file is newer than badfile2”
else
    echo “The badfile2 file is newer than badfile1”
fi
```

```bash
$ ./test21
The badfile2 file is newer than badfile1
$
```

这个小示例演示了如果文件不存在，`-nt`比较将返回一个失败的条件。在尝试在`-nt`或`-ot`比较中使用文件之前，务必确保这些文件存在。

## 复合条件测试

`if-then`语句允许你使用布尔逻辑来组合测试。你可以使用两种布尔运算符：

* `[ condition1 ] && [ condition2 ]`

* `[ condition1 ] || [ condition2 ]`

第一个布尔操作使用`AND`（与）布尔运算符组合两个条件。只有同时满足两个条件时，`then`部分才会执行。

第二个布尔操作使用`OR`（或）布尔运算符组合两个条件。如果任一条件为真，就会执行`then`部分。

```bash
$ cat test22
#!/bin/bash
# testing compound comparisons
if [ -d $HOME ] && [ -w $HOME/testing ]
then
    echo "The file exists and you can write to it"
else
    echo "I cannot write to the file"
fi
$ 
$ ./test22
I cannot write to the file
$ touch $HOME/testing
$ 
$ ./test22
The file exists and you can write to it
$
```

使用`AND`布尔运算符时，必须满足两个比较条件。第一个比较检查用户的`$HOME`目录是否存在。第二个比较检查用户的`$HOME`目录下是否存在一个名为`testing`的文件，以及该用户对该文件是否有写权限。如果这两个比较中的任何一个失败，`if`语句将失败，shell将会执行`else`部分。如果两个比较都成功，`if`语句将成功，shell将会执行`then`部分。

## 高级 if-then 特性

bash shell 最近新增了两个功能，它们提供了你可以在`if-then`语句中使用的高级特性：

* 用于数学表达式的双重圆括号

* 用于高级字符串处理函数的双中括号

接下来的章节将详细介绍这些特性的。

### 使用双重圆括号

双重圆括号命令允许你在比较中引入高级的数学公式。`test`命令在比较中只允许简单的算术运算。双重圆括号提供了更多数学符号，使用过其他编程语言的程序员可能对这些符号很熟悉。双重圆括号命令的格式为：

`(( expression ))`

表达式项可以是任何数学赋值或比较表达式。除了`test`命令使用的标准数学运算符外，还列出了可以在双重圆括号命令中使用的额外运算符。

#### 双重圆括号符号

| 符号 |  |

| :--- | :--- |

| `val++` | 后自增 |

| `val--` | 后自减 |

| `++val` | 前自增 |

| `--val` | 前自减 |

| `!` | 逻辑取反 |

| `~` | 位取反 |

| `**` | 幂运算 |

| `<<` | 左移 |

| `>>` | 右移 |

| `&` | 位与 `AND` |

| `\|` | 位或 `OR` |

| `&&` | 逻辑 `AND` |

| `\|\|` | 逻辑 `OR` |

你可以在`if`语句中使用双重圆括号命令，也可以作为赋值的普通命令使用：

```bash
$ cat test23
#!/bin/bash
# using double parenthesis
val1=10
if (( val1 ** 2 > 90 ))
then
    (( val2 = val1 ** 2 ))
    echo "The square of $val1 is $val2"
fi
$ 
$ ./test23
The square of 10 is 100
$
```

注意，你不需要在表达式中转义大于号符号。这是双重圆括号命令提供的另一个功能。

### 使用双中括号

双中括号命令提供了字符串比较的高级功能。双中括号的格式为：

`[[ expression ]]`

双中括号表达式使用了`test`命令中的标准字符串比较。然而，它提供了一个`test`命令不具备的特性：模式匹配。在模式匹配中，你可以定义一个正则表达式与字符串值进行匹配：

```bash
$ cat test24
#!/bin/bash
# using pattern matching
if [[ $USER == r* ]]
then
    echo "Hello $USER"
else
    echo "I do not know you"
fi
$ 
$ ./test24
Hello rich
$
```

双中括号命令匹配`$USER`环境变量，以检查它是否以字母`r`开头。如果是，则比较成功，shell将执行`then`部分。

### case 命令

你经常发现自己试图评估变量的值，在一组可能的值中寻找特定值。在这种情况下，你不得不编写一个冗长的`if-then-else`语句，如下所示：

```bash
$ cat test25
#!/bin/bash
# looking for a possible value
if [ $USER = "rich" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit"
elif [ $USER = "barbara" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit"
elif [ $USER = "testing" ]
then
    echo "Special testing account"
elif [ $USER = "jessica" ]
then
    echo "Do not forget to logout when you're done"
else
    echo "Sorry, you are not allowed here"
fi
$ 
$ ./test25
Welcome rich
Please enjoy your visit
$
```

`elif`语句继续`if-then`检查，为单个比较变量寻找特定值。你不需要编写所有的`elif`语句来继续检查同一个变量值，而是可以使用`case`命令。`case`命令以列表形式的形式检查单个变量的多个值：

```bash
case variable in
pattern1 | pattern2) commands1;;
pattern3) commands2;;
*) default commands;;
esac
```

`case`命令将指定的变量与模式进行比较。如果变量匹配模式，shell将执行命令。你可以在同一行列出多个模式，使用竖线运算符分隔每个模式。星号符号是用于不匹配值的通配符。这里有一个将`if-then-else`程序转换为使用`case`命令的示例：

```bash
$ cat test26
#!/bin/bash
# using the case command
case $USER in
rich | barbara)
    echo "Welcome, $USER"
    echo "Please enjoy your visit";;
testing)
    echo "Special testing account";;
jessica)
    echo "Do not forget to log off when you're done";;
*)
    echo "Sorry, you are not allowed here";;
esac
$ 
$ ./test26
Welcome rich
Please enjoy your visit
$
```

## 总结

结构化命令允许你更改 shell 脚本的执行流。最基本的结构化命令是`if-then`语句。该语句允许你评估一个命令，并根据所评估命令的结果执行其他命令。

你可以扩展`if-then`语句，包含一组当指定的命令失败时 bash shell 也会执行的命令。`if-then-else`语句允许仅在被评估的命令返回非零退出状态码时执行命令。

在大多数脚本中，你想要的不是执行一个命令，而是评估一个条件，例如数值、字符串内容，或者文件或目录的状态。`test`命令为你提供了一种简单的方法来评估所有这些条件。如果条件为真，`test`命令为`if-then`语句产生一个零退出状态码；如果条件为假，`test`命令则为`if-then`语句产生一个非零退出状态码。

方括号`[]`是一个特殊的 bash 命令，它是`test`命令的同义词。你可以在`if-then`语句用方括号括起测试条件，以对数值、字符串和文件条件进行测试。

双括号`(( ))`命令允许你使用额外的运算符执行高级数学评估，而双方括号`[[ ]]`命令则允许你执行高级的字符串模式匹配评估。

最后，本章讨论了`case`命令，它是执行多个`if-then-else`命令的简写方式，用于检查单个变量的值是否与一组值匹配。

下一章将通过检查 shell 循环命令继续对结构化命令的讨论。`for`和`while`命令允许你创建循环，在指定时间内对命令进行迭代。

# 读累了记得休息一会哦~

**公众号：古德猫宁李**

* 电子书搜索下载

* 书单分享

* 书友学习交流

**网站：**[沉金书屋 https://www.chenjin5.com](https://www.chenjin5.com)

* 电子书搜索下载

* 电子书打包资源分享

* 学习资源分享

# 第 12 章：更多结构化命令

## 本章内容

* 使用`for`语句循环

* 使用`until`语句迭代

* 使用`while`语句

* 组合循环

* 重定向循环输出

在上一章中，你看到了如何通过检查命令输出和变量值来控制 shell 脚本程序的流程。在本章中，我们将继续查看控制 shell 脚本流程的结构化命令。你将看到如何执行重复过程，即循环遍历一组命令，直到满足指定的条件为止。本章将讨论并演示`for`、`while`和`until`等 bash shell 循环命令。

## for 命令

遍历一系列命令是一种常见的编程实践。你通常需要重复执行一组命令，直到满足特定条件，例如处理目录中的所有文件、系统中的所有用户或文本文件中的所有行。

bash shell 提供了`for`命令，允许你创建一个遍历一系列值的循环。每次迭代都会使用系列中的一个值来执行一组定义的命令。以下是 bash shell`for`命令的基本格式：

```bash
for var in list
do
commands
done
```

你需要在`list`参数中提供用于迭代的系列值。这里有多种不同的方法可以让你指定列表中的值。

在每次迭代中，变量`var`包含列表中的当前值。第一次迭代使用列表中的第一个项，第二次迭代使用第二个项，依此类推，直到列表中的所有项都被使用完毕。

在`do`和`done`语句之间输入的命令可以是一条或多个标准的 bash shell 命令。在命令内部，变量`$var`包含当前迭代中列表项的条目值。

> **注意**

> 如果你愿意，可以将`do`语句与`for`语句放在同一行，但必须使用分号将其与列表项隔开：`for var in list; do`。

我们提到过有多种不同的方法可以指定列表中的值。接下来的章节将展示这些不同的方法。

### 读取列表中的值

`for`命令最基本的用法是遍历在`for`命令本身内部定义的值列表：

```bash
$ cat test1
#!/bin/bash
# basic for command
for test in Alabama Alaska Arizona Arkansas California Colorado
do
    echo The next state is $test
done
$ ./test1
The next state is Alabama
The next state is Alaska
The next state is Arizona
The next state is Arkansas
The next state is California
The next state is Colorado
$
```

每当`for`命令遍历所提供的值列表时，它都会将列表中的下一个值赋值给`$test`变量。`$test`变量可以像其他脚本变量一样在`for`命令语句中使用。在最后一次迭代之后，`$test`变量在 shell 脚本的剩余部分仍然保持有效。它保留了最后一次迭代的值（除非更改了它的值）：



```bash
$ cat test1b
#!/bin/bash
# testing the for variable after the looping
for test in Alabama Alaska Arizona Arkansas California Colorado
do
    echo "The next state is $test"
done
echo "The last state we visited was $test"
test=Connecticut
echo "Wait, now we're visiting $test"
$ ./test1b
The next state is Alabama
The next state is Alaska
The next state is Arizona
The next state is Arkansas
The next state is California
The next state is Colorado
The last state we visited was Colorado
Wait, now we're visiting Connecticut
$
```

`$test` 变量保留了它的值，并且允许我们像其他变量一样在 `for` 命令循环之外更改它的值并使用它。

### 读取列表中的复杂值

`for` 循环并不总是看起来那么简单。有时你会遇到会导致问题的数据。这里有一个关于 shell 脚本编写人员可能遇到问题的经典示例：

```bash
$ cat badtest1
#!/bin/bash
# another example of how not to use the for command
for test in I don't know if this'll work
do
    echo "word:$test"
done
$ ./badtest1
word:I
word:dont know if thisll
word:work
$
```

哎，这真疼。shell 看到了列表值中的单引号，并尝试使用它们来定义单个数据值，这在过程中真的搞乱了一切。

解决这个问题有两种方法：

- 使用转义字符（反斜杠 `\`）来转义单引号。
- 使用双引号定义包含单引号的值。

这两种解决方案都不完美，但每一种都能帮助解决问题：

```bash
$ cat test2
#!/bin/bash
# another example of how not to use the for command
for test in I\'t know if "this'll"
do
    echo "word:$test"
done
$ ./test2
word:I
word:don't
word:know
word:if
word:this'll
$
```

在第一个问题值中，你添加了反斜杠来转义单引号。在第二个问题值中，你用双引号括起了 `this'll` 值。两种方法都能很好地区分值。

你可能遇到的另一个问题是多单词值。记住，`for` 循环假设每个值是用空格分隔的。如果你有包含空格的数据值，将会遇到另一个问题：

```bash
$ cat badtest2
#!/bin/bash
# another example of how not to use the for command
for test in Nevada New Hampshire Mexico New York North Carolina
do
    echo "Now going to $test"
done
$ ./badtest
Now going to Nevada
Now going to New
Now going to Hampshire
Now going to New
Now going to Mexico
Now going to New
Now going to York
Now going to North
Now going to Carolina
$
```

哎，那不是我们想要的。`for` 命令用空格分隔列表中的每个值。如果单个数据值包含空格，你必须使用双引号来处理：

```bash
$ cat test3
#!/bin/bash
# an example of how to properly define values
for test in Nevada "New Hampshire" "New Mexico" "New York"
do
    echo "Now going to $test"
done
$ ./test3
Now going to Nevada
Now going to New Hampshire
Now going to New Mexico
Now going to New York
$
```

现在 `for` 命令可以正确地区分不同的值。此外，请注意，当你在值周围使用双引号时，shell 不会将双引号作为值的一部分。

## 从变量中读取列表

在 shell 脚本中，经常发生的情况是将一个存储在变量中的值列表，然后需要对该列表进行迭代。你也可以使用 `for` 命令来实现：

```bash
$ cat test4
#!/bin/bash
# using a variable to hold the list
list="Alabama Alaska Arizona Arkansas Colorado"
list=$list" Connecticut"
for state in $list
do
    echo "Have you ever visited $state?"
done
$ ./test4
Have you ever visited Alabama?
Have ever visited Alaska?
Have you ever visited Arizona?
Have you ever visited Arkansas?
Have you ever visited Colorado?
Have you ever visited Connecticut?
```

变量 `$list` 包含了用于迭代的标准文本值列表。请注意，代码还使用了另一个赋值语句向 `$list` 变量包含的现有列表添加（或拼接）项。这是向存储在变量中的现有文本字符串末尾添加文本的常用方法。

## 从命令中读取值

生成列表值的另一种方法是使用命令的输出。你使用反引号执行任何产生输出的命令，然后在 `for` 命令中使用该命令的输出：

```bash
$ cat test5
#!/bin/bash
# reading values from a file
file="states"
for state in `cat $file`
do
    echo "Visit beautiful $state"
done
$ cat states
Alabama
Alaska
Arizona
Arkansas
Colorado
Connecticut
Delaware
Florida
Georgia
$ ./test5
Visit beautiful Alabama
Visit beautiful Alaska
Visit beautiful Arizona
Visit beautiful Arkansas
Visit beautiful Colorado
Visit beautiful Connecticut
Visit beautiful Delaware
Visit beautiful Florida
Visit beautiful Georgia
$
```

此示例使用了反引号包裹的 `cat` 命令来显示 `states` 文件的内容。你会发现 `states` 文件中的每个州都占一行，而不是用空格分隔。`for` 命令仍然一次行遍历 `cat` 命令的输出，假设每个州都单独成行。然而，这并没有解决数据中包含空格的问题。如果你列出一个包含空格的州，`for` 命令仍然会将每个单词视为一个单独的值。这有其原因，我们将在下一节中讨论。

> **注意**
>
> `test5` 代码示例直接使用文件名（不带路径）将其赋值给变量。这要求该文件与脚本位于同一目录下。如果不是如此，你需要使用完整路径（绝对路径或相对路径）来引用文件位置。

## 修改字段分隔符

这个问题的原因是特殊的环境变量 `IFS`，称为内部字段分隔符。`IFS` 环境变量定义了 bash shell 用作字段分隔符的字符列表。默认情况下，bash shell 将以下字符考虑作字段分隔符：

- 空格
- 制表符
- 换行符

如果 bash shell 在数据中看到这些字符之一，它将认为你正在开始列表中的新数据字段。在处理可能包含空格的数据（如文件名）时，正如你在之前的脚本示例中看到的，这可能会非常困扰。

为了解决这个问题，你可以临时更改 shell 脚本中的 `IFS` 环境变量值，以限制 bash shell 识别为字段分隔符的字符。然而，这种方法有点奇怪。例如，如果你想将 `IFS` 值更改为仅识别换行符，你需要这样做：

`IFS=$'\n'`

在脚本中添加此语句告诉 bash shell 忽略数据值中的空格和制表符。将此应用于之前的脚本将得到以下结果：

```bash
$ cat test5b
#!/bin/bash
# reading values from a file
file="states"
IFS=$'\n'
for state in `cat $file`
do
    echo "Visit beautiful $state"
done
$ ./test5b
Visit beautiful Alabama
Visit beautiful Alaska
Visit beautiful Arizona
Visit beautiful Arkansas
Visit beautiful Colorado
Visit beautiful Connecticut
Visit beautiful Delaware
Visit beautiful Florida
Visit beautiful Georgia
Visit beautiful New York
Visit beautiful New Hampshire
Visit beautiful North Carolina
$
```

现在，shell 脚本能够使用列表中的包含空格的值了。

> **警告**
>
> 在编写长脚本时，可能会在某处更改了 `IFS` 值，然后忘记了它，并假设脚本的其他地方使用的是默认值。一种安全的做法是在更改 `IFS` 之前保存原始值，然后恢复它。

## 使用通配符读取目录

最后，你可以使用 `for` 命令自动遍历目录。为了做到这一点，你必须使用通配符。文件通配（File globbing）是产生匹配指定通配符的文件名的过程。

```bash
$ cat test6
#!/bin/bash
# iterate through a directory
for file in /home/rich/test/*
do
    if [ -d "$file" ]
    then
        echo "$file is a directory"
    elif [ -f "$file" ]
    then
        echo "$file is a file"
    fi
done
$ ./test6
/home/rich/test/dir1 is a directory
/home/rich/test/myprog.c is a file
/home/rich/test/myprog is a file
/home/rich/test/myscript is a file
/home/rich/test/newdir is a directory
/home/rich/test/newfile is a file
/home/rich/test/newfile2 is a file
/home/rich/test/testdir is a directory
/home/rich/test/testing is a file
/home/rich/test/testprog.c is a file
$
```

`for` 命令遍历 `/home/rich/test/*` 列出的结果。该代码使用 `test` 命令（使用方括号方法）测试每个条目，以检查它是目录（使用 `-d` 参数）还是文件（使用 `-f` 参数）（请参见第 11 章）。

注意在此示例中，我们在 `if` 语句测试中做了不同的操作：

`if [ -d "$file" ]`

在 Linux 中，包含空格的目录和文件名是完全合法的。为了适应这种情况，你应该将 `$file` 变量括在双引号中。如果不这样做，当你遇到包含空格的目录或文件名时，将会得到错误：

`./test6: line 6: [: too many arguments`

```text
./test6: line 9: [: too many arguments
```

bash shell 将额外的单词解释为 `test` 命令内部的参数，从而导致错误。

你也可以通过在 `for` 命令中列出一系列目录通配符，在同一个 `for` 语句中结合目录搜索方法和列表方法：

```bash
$ cat test7

#!/bin/bash

# 遍历多个目录

for file in /home/rich/.b* /home/rich/badtest
do
    if [ -d "$file" ]
    then
        echo "$file is a directory"
    elif [ -f "$file" ]
    then
        echo "$file is a file"
    else
        echo "$file doesn't exist"
    fi
done

$ ./test7

/home/rich/.backup.timestamp is a file
/home/rich/.bash_history is a file
/home/rich/.bash_logout is a file
/home/rich/.bash_profile is a file
/home/rich/.bashrc is a file
/home/rich/badtest doesn't exist

$
```

`for` 语句首先使用文件通配符（globbing）遍历由通配符字符生成的文件列表；然后遍历列表中的下一个文件。你可以组合列表中的任意数量的通配符项进行遍历。

> **注意**
>
> 注意，你可以在列表中输入任何内容。即使文件或目录不存在，`for` 语句也会尝试处理你放置在列表中的任何内容。这在处理文件和目录时可能会成为一个问题。你无法知道自己是否正在尝试遍历一个不存在的目录：在尝试处理每个文件或目录之前，对其进行测试总是一个好主意。

# C 风格的 for 命令

如果你用 C 语言进行过任何编程，你可能会对 bash shell 使用 `for` 命令的方式感到惊讶。在 C 语言中，`for` 循环通常定义一个变量，并在每次迭代中自动修改该变量。通常，程序员使用此变量作为计数器，并在每次迭代中将计数器加一或减一。bash 的 `for` 命令也可以提供这种功能。本节向你展示如何在 bash shell 脚本中使用 C 风格的 `for` 命令。

## C 语言 for 命令

C 语言的 `for` 命令有一种特定方法来指定变量、一个为了持续迭代必须保持为真的条件，以及一种每次迭代都修改变量的方法。当指定的条件变为假时，`for` 循环停止。条件等式使用标准数学符号定义。例如，考虑以下 C 语言代码：

```c
for (i = 0; i < 10; i++)
{
    printf("The next number is %d\n", i);
}
```

这段代码产生了一个简单的迭代循环，变量 `i` 被用作计数器。第一部分为变量分配了默认值。中间部分定义了循环迭代的条件。当定义的条件变为假时，`for` 循环停止迭代。最后部分定义了迭代过程。每次迭代后，都会执行最后部分定义的表达式。在这个示例中，`i` 变量在每次迭代后加 1。

bash shell 也支持一种类似于 C 风格 `for` 循环的版本，尽管它确实有一些细微的差异，包括一些会让 shell 脚本程序员感到困惑的地方。这里是 C 风格 bash `for` 循环的基本格式：

```bash
for ((
    variable assignment ;
    condition ;
    iteration process
))
```

C 风格 `for` 循环的格式会让 bash shell 脚本程序员感到很困惑，因为它使用了 C 风格的变量引用而不是 shell 风格的变量引用。这里是 C 风格 `for` 命令的样子：

```bash
for (( a = 1; a < 10; a++ ))
```

注意有几点并不符合标准的 bash shell `for` 方法：

- 变量值的赋值可以包含空格。
- 条件中的变量前面没有美元符号 `$`。
- 迭代过程的等式没有使用 `expr` 命令格式。

shell 开发者创建这种格式是为了更接近 C 风格的 `for` 命令。虽然这对 C 程序员来说很棒，但它会让甚至是专家级的 shell 程序员也不知所措。在脚本中使用 C 风格的 `for` 循环时要小心。

这是一个在 bash shell 程序中使用 C 风格 `for` 命令的示例：

```bash
$ cat test8

#!/bin/bash

# 测试 C 风格的 for 循环

for (( i=1; i <= 10; i++ ))
do
    echo "The next number is $i"
done
```

```bash
$ ./test8
The next number is 1
The next number is 2
The next number is 3
The next number is 4
The next number is 5
```



The next number is 6

The next number is 7

The next number is 8

The next number is 9

The next number is 10

$

`for` 循环使用 `for` 循环中定义的变量（此示例中的字母 `i`）遍历命令。在每次迭代中，变量 `$i` 包含在 `for` 循环中分配的值。每次迭代后，循环迭代过程被应用于变量，在此示例中，它会将变量加 1。

## 使用多个变量

（注：此处原文后续存在大量重复内容，已按要求不再重复输出。）

在某种有点奇怪的情况下，`while` 命令允许你在此 `while` 语句行上定义多个测试命令。只有最后一个测试命令的退出状态被用于判断循环何时何时停止。如果你不小心，这可能会导致一些有趣的结果。这里有一个示例：

```bash
$ cat test11

!/bin/bash

# 测试多命令 while 循环

var1=10

while echo $var1
      [ $var1 -ge 0 ]
do
    echo “循环内部”
    var1=$[ var1 - 1 ]
done

$ ./test11

10

循环内部

9

循环内部

8

循环内部

7

循环内部

6

循环内部

5

循环内部

4

循环内部

3

循环内部

2

循环内部

1

循环内部

0

循环内部

-1

$
```

注意这个示例中发生了什么。`while` 语句中定义了两个测试命令：

```bash
while echo $var1
      [ $var1 -ge 0 ]
```

第一个测试仅仅显示了 `var1` 变量的当前值。第二个测试使用中括号来确定 `var1` 变量的值。在循环内部，`echo` 语句显示了一条消息，表示循环正在处理。注意运行该示例时输出是如何结束的：

```text
循环内部

-1

$
```

`while` 循环在 `var1` 变量等于 0 时执行了 `echo` 语句，然后减少了 `var1` 变量的值。接着执行了测试命令，由于 `var1` 现在小于 0，`while` 循环终止。这表明在多命令 `while` 语句中，在最后一个测试命令失败之前，所有的测试命令都会执行。注意这一点。另一个需要注意的是如何指定多个测试命令。注意每个测试命令都是单独成行！

## `until` 命令

`until` 命令的作用与 `while` 命令完全相反。`until` 命令要求指定一个通常产生非零退出状态的测试命令。只要测试命令的退出状态是非零，bash shell 就会执行列出的命令。一旦测试命令返回零状态，循环停止。

正如你预期的那样，`until` 命令的格式是：

```bash
until test
commands
do
other commands
done
```

与 `while` 命令类似，`until` 命令语句中也可以有多个测试命令。只有最后一个命令的退出状态决定 bash shell 是否执行其他命令。

以下是使用 `until` 命令的示例：

```bash
$ cat test12

!/bin/bash

# 使用 until 命令

var1=100

until [ $var1 -eq 0 ]
do
    echo $var1
    var1=$[ var1 - 25 ]
done

$ ./test12

100

75

50

25

$
```

这个示例测试 `var1` 变量以确定 `until` 循环何时停止。一旦变量的值等于零，`until` 命令停止循环。当 `until` 命令使用多个测试命令时，适用于 `while` 命令相同的注意事项：

```bash
$ cat test13

!/bin/bash

# 使用 until 命令

var1=100

until echo $var1
      [ $var1 -eq 0 ]
do
    echo 循环内部: $var1
    var1=$[ var1 - 25 ]
done

$ ./test13

100

循环内部: 100

75

循环内部: 75

50

循环内部: 50

25

循环内部: 25

0

$
```

shell 执行指定的测试命令，仅当最后一个命令为真时停止。

## 嵌套循环

循环语句可以在内部使用任何其他类型的命令，包括其他循环命令。这被称为嵌套循环。使用嵌套循环时应小心，因为你在迭代中执行迭代，这会增加命令运行的次数。不注意这一点可能会导致脚本出现问题。

这是一个嵌套 `for` 循环的简单示例：

```bash
$ cat test14

!/bin/bash

# 嵌套 for 循环

for (( a = 1; a <= 3; a++ ))
do
    echo "开始循环 $a:"
    for (( b = 1; b <= 3; b++ ))
    do
        echo "  循环内部: $b"
    done
done

$ ./test14

开始循环 1:

  循环内部: 1

  循环内部: 2

  循环内部: 3

开始循环 2:

  循环内部: 1

  循环内部: 2

  循环内部: 3

开始循环 3:

  循环内部: 1

  循环内部: 2

  循环内部: 3

$
```

嵌套循环（也称为内循环）在外层循环的每次迭代中遍历其值。注意，两个循环的 `do` 和 `done` 命令没有区别。bash shell 在执行第一个 `done` 命令时，它指的是内循环而不是外层循环。

当你混合循环时也是如此，例如将 `for` 循环放在 `while` 循环内部：

```bash
$ cat test15

!/bin/bash

# 将 for 循环放在 while 循环内部

var1=5

while [ $var1 -ge 0 ]
do
    echo "外部循环: $var1"
    for (( var2 = 1; var2 < 3; var2++ ))
    do
        var3=$[ var1 * $var2 ]
        echo "  循环内部: $var1 * $var2 = $var3"
    done
    var1=$[ var1 - 1 ]
done

$ ./test15

外部循环: 5

  循环内部: 5 * 1 = 5

  循环内部: 5 * 2 = 10

外部循环: 4

  循环内部: 4 * 1 = 4

  循环内部: 4 * 2 = 8

外部循环: 3

  循环内部: 3 * 1 = 3

  循环内部: 3 * 2 = 6

外部循环: 2

  循环内部: 2 * 1 = 2

  循环内部: 2 * 2 = 4

外部循环: 1

  循环内部: 1 * 1 = 1

  循环内部: 1 * 2 = 2

外部循环: 0

$
```

再次，shell 能够区分内部 `for` 循环的 `do` 和 `done` 命令与外部 `while` 循环的。如果你真的想测试你的大脑，甚至可以结合 `until` 和 `while` 循环：

```bash
$ cat test16

!/bin/bash

# 使用 until 和 while 循环

var1=3

until [ $var1 -eq 0 ]
do
    echo "外部循环: $var1"
    var2=1
    while [ $var2 -lt 5 ]
    do
        var3='echo "scale=4; $var1 / $var2" | bc'
        echo "  循环内部: $var1 / $var2 = $var3"
        var2=$[ var2 + 1 ]
    done
    var1=$[ var1 - 1 ]
done

$ ./test16

外部循环: 3

  循环内部: 3 / 1 = 3.0000

  循环内部: 3 / 2 = 1.5000

  循环内部: 3 / 3 = 1.0000

  循环内部: 3 / 4 = .7500

外部循环: 2

  循环内部: 2 / 1 = 2.0000

  循环内部: 2 / 2 = 1.0000

  循环内部: 2 / 3 = .6666

  循环内部: 2 / 4 = .5000

外部循环: 1

  循环内部: 1 / 1 = 1.0000

  循环内部: 1 / 2 = .5000

  循环内部: 1 / 3 = .3333

  循环内部: 1 / 4 = .2500

$
```

## 遍历文件数据

通常，你需要遍历存储在文件中的项目。这需要结合涵盖过的两种技术：

- 使用嵌套循环
- 更改 `IFS` 环境变量

通过更改 `IFS` 环境变量，你可以强制 `for` 命令将文件中的每一行视为作为一个独立的项目进行处理，即使数据中包含空格也是如此。一旦你提取了文件中的某一行，你可能需要再次循环来提取其中包含的数据。

这种操作的经典示例是处理 `/etc/passwd` 文件中的数据。这需要逐行遍历 `/etc/passwd` 文件，然后将 `IFS` 变量的值改为冒号（`:`），这样就可以分离出每行中的各个组件。

以下是实现此操作的示例：

```bash
#!/bin/bash

# changing the IFS value

IFS.OLD=$IFS

IFS=$'\n'

for entry in `cat /etc/passwd`
do
    echo "Values in $entry –"
    IFS=:
    for value in $entry
    do
        echo "    $value"
    done
done

$
```

此脚本使用了两个不同的 `IFS` 值来解析数据。第一个 `IFS` 值解析 `/etc/passwd` 文件中的单独行。接下来的内部 `for` 循环将 `IFS` 值改为冒号，这允许你解析 `/etc/passwd` 行中的各个值。

当你运行此脚本时，你将得到类似下面的输出：

```text
Values in rich:x:501:501:Rich Blum:/home/rich:/bin/bash -

    rich

    x

    501

    501

    Rich Blum

    /home/rich

    /bin/bash

Values in katie:x:502:502:Katie Blum:/home/katie:/bin/bash -

    katie

    x

    506

    509

    Katie Blum

    /home/katie

    /bin/bash
```

内部循环解析 `/etc/passwd` 条目中的每个单独值。这也是处理逗号分隔数据的极佳方法，这是导入表格数据的常用方法。

# 控制循环

你可能会认为，一旦开始循环，你就必须一直持续，直到循环完成所有迭代。事实并非如此。有几个命令可以帮助我们控制循环内部发生的情况：

- `break` 命令
- `continue` 命令

每个命令在控制循环操作方面有不同的用途。以下章节描述了你可以如何使用这些命令来控制循环的操作。

## `break` 命令

`break` 命令是退出正在运行循环的简单方法。你可以使用 `break` 命令退出任何类型的循环，包括 `while` 和 `until` 循环。在几种情况下你可以使用 `break` 命令。本节将展示这些所有方法。

### 退出单个循环

当 shell 执行 `break` 命令时，它尝试跳出当前处理的循环：

```bash
$ cat test17

#!/bin/bash

# breaking out of a for loop

for var1 in 1 2 3 4 5 6 7 8 9 10
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration number: $var1"
done

echo "The for loop is completed"

$ ./test17

Iteration number: 1

Iteration number: 2

Iteration number: 3

Iteration number: 4

The for loop is completed

$
```

`for` 循环通常应该遍历列表指定的所有值。然而，当 `if-then` 条件被满足时，shell 执行了 `break` 命令，停止了 `for` 循环。这种技术也适用于 `while` 和 `until` 循环：

```bash
$ cat test18

#!/bin/bash

# breaking out of a while loop

var1=1

while [ $var1 -lt 10 ]
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration: $var1"
    var1=$[ var1 + 1 ]
done

echo "The while loop is completed"

$ ./test18

Iteration: 1

Iteration: 2

Iteration: 3

Iteration: 4

The while loop is completed

$
```

当满足 `if-then` 条件时，`while` 循环终止，并执行了 `break` 命令。

### 退出内部循环

当你处理多个循环时，`break` 命令会自动终止你所在的最内层循环：

```bash
$ cat test19

#!/bin/bash

# breaking out of an inner loop

for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 100; b++ ))
    do
        if [ $b -eq 5 ]
        then
            break
        fi
        echo "    Inner loop: $b"
    done
done

$ ./test19

Outer loop: 1

    Inner loop: 1

    Inner loop: 2

    Inner loop: 3

    Inner loop: 4

Outer loop: 2

    Inner loop: 1

    Inner loop: 2

    Inner loop: 3

    Inner loop: 4

Outer loop: 3

    Inner loop: 1

    Inner loop: 2

    Inner loop: 3

    Inner loop: 4
```

### 退出外部循环

有时你可能处于内部循环中，但需要停止外部循环。`break` 命令包含一个参数 `break n`，其中 `n` 表示要退出的循环层级。默认情况下，`n` 为 1，表示退出当前循环。如果你将 `n` 设置为 2，`break` 命令将停止下一层级：

```bash
$ cat test20

#!/bin/bash

# breaking out of an outer loop

for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 100; b++ ))
    do
        if [ $b -eq 5 ]
        then
            break 2
        fi
        echo "    Inner loop: $b"
    done
done
```

## `continue` 命令

`continue` 命令是一种提前停止循环内命令执行但不终止循环的方法。这允许你在循环内部设置条件。这是一个在 `for` 循环中使用 `continue` 的简单示例：

```bash
$ cat test21

#!/bin/bash

# using the continue command

for var1 in 1 2 3 4 5 6 7 8 9 10
do
    if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
    then
        continue
    fi
    echo "Iteration number: $var1"
done

$ ./test21

Iteration number: 1

Iteration number: 2

Iteration number: 3

Iteration number: 4

Iteration number: 5

Iteration number: 10

Iteration number: 11

Iteration number: 12

Iteration number: 13
```

当满足 `if-then` 语句的条件（值大于 5 且小于 10）时，shell 执行 `continue` 命令，跳过循环中的后续命令，但保持循环继续。当 `if-then` 条件不再满足时，情况就会恢复正常。

你可以在 `while` 和 `until` 循环中使用 `continue`，但要极度小心你的操作。记住，当 shell 执行 `continue` 命令时，它会跳过剩余的命令。如果你在这些命令之一中递增测试条件，就会发生糟糕的事情：

```bash
$ cat badtest3

#!/bin/bash
```



# 在 `while` 循环中错误使用 `continue` 命令

```
var1=0

while echo "iteration: $var1"; [ $var1 -lt 15 ]

do

    if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]

    then

        continue

    fi

    echo "    Inside iteration number: $var1"

    var1=$[ $var1 + 1 ]

done
```

```
$ ./badtest3 | more

while iteration: 0

    Inside iteration number: 0

while iteration: 1

    Inside iteration number: 1

while iteration: 2

    Inside iteration number: 2

while iteration: 3

    Inside iteration number: 3

while iteration: 4

    Inside iteration number: 4

while iteration: 5

while iteration: 10

while iteration: 11

while iteration: 12

while iteration: 13
```

```
Inside iteration number: 4

while iteration: 5

Inside iteration number: 5

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

while iteration: 6

$
```

你可能需要确保将此脚本的输出重定向到`more`命令，这样你就可以停止它。在满足`if-then`条件之前，一切似乎运行正常，直到 shell 执行了`continue`命令。当 shell 执行`continue`命令时，它会跳过`while`循环中剩余的命令。遗憾的是，在`while`测试命令中测试的`$var1`计数变量正是在那里递增的。这意味着正如从持续显示的输出中看到的，该变量并没有递增。

与`break`命令一样，`continue`命令允许你通过命令行参数指定要继续哪种层级的循环：

```
continue n
```

其中`n`定义了要继续的循环层级。这里有一个继续外层`for`循环的示例：

```bash
$ cat test22

#!/bin/bash

# continuing an outer loop

for (( a = 1; a <= 5; a++ ))

do

    echo "Iteration $a:"

    for (( b = 1; b < 3; b++ ))

    do

        if [ $a -gt 2 ] && [ $a -lt 4 ]

        then

            continue 2

        fi

        var3=$[ $a * $b ]

        echo "    The result of $a * $b is $var3"

    done

done

$ ./test22

Iteration 1:

    The result of 1 * 1 is 1

    The result of 1 * 2 is 2

Iteration 2:

    The result of 2 * 1 is 2

    The result of 2 * 2 is 4

Iteration 3:

Iteration 4:

    The result of 4 * 1 is 4

    The result of 4 * 2 is 8

Iteration 5:

    The result of 5 * 1 is 5

    The result of 5 * 2 is 10

$
```

###  `if-then` 语句

```
if [ $a -gt 2 ] && [ $a -lt 4 ]

then

    continue 2

fi
```

使用`continue`命令来停止循环内部命令的执行，但继续外层循环。注意脚本输出，值为 3 的迭代没有处理任何内部语句，因为`continue`命令停止了处理。

### 处理循环的输出

最后，你可以通过管道（pipe）或重定向 shell 脚本中循环的输出。你可以通过在`done`命令的末尾添加处理命令来实现这一点：

```
for file in /home*

do

    if [ -d "$file" ]

    then

        echo "$file is a directory"

    elif

        echo "$file is a file"

    fi

done > output.txt
```

shell 不会在显示器上显示结果，而是将`for`命令的结果重定向到文件`output.txt`。请考虑以下将`for`命令的输出重定向到文件的示例：

```bash
$ cat test23

#!/bin/bash

# redirecting the for output to a file

for (( a = 1; a < 10; a++ ))

do

    echo "The number is $a"

done > test23.txt

$ ./test23

The command is finished.

$ cat test23.txt

The number is 1

The number is 2

The number is 3

The number is 4

The number is 5

The number is 6

The number is 7

The number is 8

The number is 9

$
```

shell 创建了`test23.txt`文件并将`for`命令的输出仅重定向到该文件。shell 会像往常一样显示`for`命令之后的`echo`语句。这种技术同样适用于将循环的输出管道到另一个命令：

```bash
$ cat test24

#!/bin/bash

# piping a loop to another command

for state in "North Dakota" Connecticut Alabama Tennessee

do

    echo "$state is the next place to go"

done | sort

echo "This completes our travels"

$ ./test24

Alabama is the next place to go

Connecticut is the next place to go

Illinois is the next place to go

North Dakota is the next place to go

Tennessee is the next place to go

This completes our travels

$
```

州值在`for`命令列表中并不是按特定顺序列出的。`for`命令的输出被管道传输到`sort`命令，这将改变`for`命令输出的顺序。运行脚本确实显示输出在脚本内部已经过正确排序。

### 总结

循环是编程中不可或缺的一部分。bash shell 提供了三种不同的循环命令，你可以在脚本中使用它们。`for`命令允许你遍历值列表，这些值可以在命令行中提供，也可以包含在变量中，或者通过使用文件通配符（file globbing）从通配符字符提取文件名和目录名。

`while`命令提供了一种基于命令状态进行循环的方法，可以使用普通命令或`test`命令（后者允许你测试变量条件）。只要命令（或条件）产生零退出状态，`while`循环就会继续迭代指定的命令集。

`until`命令也提供了一种迭代命令的方法，但它的迭代基于命令（或条件）产生非零退出状态。此功能允许你设置一个在迭代停止前必须满足的条件。

你可以在 shell 脚本中组合循环，产生多层循环。bash shell 提供了`continue`和`break`命令。

`bash` shell 会将一组称为“位置参数”（positional parameters）的特殊变量分配给命令行中输入的所有参数。这甚至包括 shell 执行的程序名称。位置参数变量是标准数字，其中`$0`是程序名称，`$1`是第一个参数，`$2`是第二个参数，以此此类推，直到`$9`是第九个参数。

这里是在 shell 脚本中使用一个命令行参数的简单示例：

```bash
$ cat test1

#!/bin/bash

# using one command line parameter

factorial=1

for (( number = 1; number <= $1 ; number++ ))

do

    factorial=$[ $factorial * $number ]

done

echo The factorial of $1 is $factorial

$ 

$ ./test1 5

The factorial of 5 is 120

$
```

你可以像使用 shell 脚本中的其他变量一样使用`$1`变量。shell 脚本会自动将命令行参数的值赋值给变量；你不需要对其进行任何操作。

如果你需要输入更多的命令行参数，每个参数在命令行上必须用空格分隔：

```bash
$ cat test2

#!/bin/bash

# testing two command line parameters

total=$[ $1 * $2 ]

echo The first parameter is $1.

echo The second parameter is $2.

echo The total value is $total.

$ 

$ ./test2 2 5

The first parameter is 2.

The second parameter is 5.

The total value is 10.

$
```

shell 会将每个参数分配给相应的变量。

### 使用字符串参数

在这个示例中，使用的命令行参数都是数值。你也可以在命令行中使用文本字符串：

```bash
$ cat test3

#!/bin/bash

# testing string parameters

echo Hello $1, glad to meet you.

$ 

$ ./test3 Rich

Hello Rich, glad to meet you.

$
```

shell 将输入命令行的字符串值传递给脚本。但是，如果你尝试对包含空格的文本字符串进行此操作，你就会遇到问题：

```bash
$ ./test3 Rich Blum

Hello Rich, glad to meet you.

$
```

请记住每个参数都是用空格分隔的，因此 shell 将空格解释为仅分隔两个值。要将包含空格的字符串作为参数值，你必须使用引号（单引号或双引号）：

```bash
$ ./test3 'Rich Blum'

Hello Rich Blum, glad to meet you.

$ 

$ ./test3 "Rich Blum"

Hello Rich Blum, glad to meet you.

$
```

> **注意**
> 当你传递文本字符串作为参数时使用的引号并不是数据的一部分。它们只是界定了数据的开始和结束。

### 处理多个数字参数

如果你的脚本需要超过九个命令行参数，你可以继续，但变量名称会略有变化。在第九个变量之后，你必须在变量数字周围使用大括号，例如`${10}`。这是一个相关的示例：

```bash
$ cat test4

#!/bin/bash

# handling lots of parameters

total=$[ ${10} * ${11} ]

echo The tenth parameter is ${10}

echo The eleventh parameter is ${11}

echo The total is $total

$ 

$ ./test4 1 2 3 4 5 6 7 8 9 10 11 12

The tenth parameter is 10

The eleventh parameter is 11

The total is 110

$
```

这种技术允许你向脚本中添加你可能需要的任意命令行参数。

### 读取程序名称

你可以使用`$0`参数来确定 shell 从命令行启动的程序名称。如果你编写一个具有多个功能的实用程序，这会非常有用。然而，有一个小问题是你处理的。看这个简单示例中发生了什么：

```bash
$ cat test5

#!/bin/bash

# testing the $0 parameter

echo The command entered is: $0

$ 

$ ./test5

The command entered is: ./test5

$ 

$ /home/rich/test5

The command entered is: /home/rich/test5

$
```

当传递给`$0`变量的实际字符串是整个脚本路径时，整个路径将用于程序，而不仅仅是程序名称。

如果你想写一个根据命令行运行的脚本名称来执行不同函数的脚本，你必须做一些工作。你能够剥离从命令行运行脚本时使用的任何路径。

幸运的是，有一个非常有用的命令可以为你实现这一点。`basename`命令只返回不带路径的程序名。让我们修改示例脚本看看它是如何工作的：

```bash
$ cat test5b

#!/bin/bash

# using basename with the $0 parameter

name='basename $0'

echo The command entered is: $name

$ 

$ ./test5b

The command entered is: test5b

$ 

$ /home/rich/test5b

The command entered is: test5b

$
```

现在好多了。你现在可以使用这种技术来编写根据使用的脚本名称执行不同函数的脚本。这里有一个简单的示例来演示这一点：

```bash
$ cat test6

#!/bin/bash

# testing a multi-function script

name='basename $0'

if [ $name = "addem" ]

then

    total=$[ $1 + $2 ]

elif [ $name = "multem" ]

then

    total=$[ $1 * $2 ]

fi

echo The calculated value is $total

$ 

$ chmod u+x test6

$ cp test6 addem

$ ln -s test6 multem

$ ls -l

-rwxr--r--     1 rich      rich
```

### 测试参数

在使用参数时需要小心。如果脚本假设有数据但实际上没有，你很可能会得到错误。在使用之前检查你的参数始终是一个好主意：

```bash
$ cat test7

#!/bin/bash

# testing parameters before use

if [ -n "$1" ]

then

    echo Hello $1, glad to meet you.

else

    echo "Sorry, you did not identify yourself."

fi

$ 

$ ./test7 Rich

Hello Rich, glad to meet you.

$ 

$ ./test7

Sorry, you did not identify yourself.

$
```

### 特殊参数变量

bash shell 中有一些特殊变量用于跟踪命令行参数。本节描述了它们是什么以及如何使用它们。

#### 参数计数

正如上一节所示，在使用之前验证命令行参数通常是一个好主意。对于使用多个命令行参数的脚本，这会变得非常麻烦。与其测试每个参数，你只需要计算命令行上输入了多少参数。bash shell 提供了一个特殊变量为此目的。

特殊变量`$#`包含了运行脚本时的命令行参数数量。你可以像使用普通变量一样在脚本的任何地方使用这个特殊变量：

```bash
$ cat test8

#!/bin/bash

# getting the number of parameters

echo There were $# parameters supplied.

$ 

$ ./test8

There were 0 parameters supplied.

$ 

$ ./test8 1 2 3 4 5

There were 5 parameters supplied.

$ 

$ ./test8 1 2 3 4 5 6 7 8 9 10

There were 10 parameters supplied.

$ 

$ ./test8 "Rich Blum"
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

---

[content]
```
There were 1 parameters supplied.
```

现在你可以在尝试使用这些参数之前，测试存在的参数数量：

```bash
$ cat test9
#!/bin/bash

# testing parameters

if [ $# -ne 2 ]
then
   echo Usage: test9 a b
else
   total=$[ $1 + $2 ]
   echo The total is $total
fi
```

```bash
$ ./test9
Usage: test9 a b
$ ./test9 10
Usage: test9 a b
$ ./test9 10 15
The total is 25
$ ./test9 10 15 20
Usage: test9 a b
```

`if-then`语句使用`test`命令对命令行上提供的参数数量进行数值测试。如果参数数量不正确，你可以打印一条错误信息，显示脚本的正确用法。

这个变量还提供了一种获取命令行最后一个参数的酷方法，而不需要知道使用了多少个参数。然而，你需要使用一点小技巧才能做到。

如果你仔细思考，你可能会认为因为`$#`变量包含了参数数量的值，那么使用变量`${$#}`就会代表最后一个命令行参数变量。试一下看看会发生什么：

```bash
$ cat badtest1
#!/bin/bash

# testing grabbing last parameter

echo The last parameter was ${$#}
```

```bash
$ ./badtest1 10
The last parameter was 15354
```

哇，这里发生了什么？显然，发生了一些错误。事实证明，你不能在大括号中使用美元符号。相反，你必须将美元符号替换为感叹号。这很奇怪，但它确实有效：

```bash
$ cat test10
#!/bin/bash

# grabbing the last parameter

params=$#
echo The last parameter is $params
echo The last parameter is ${!#}
```

```bash
$ ./test10 1 2 3 4 5
The last parameter is 5
The last parameter is 5
$ ./test10
The last parameter is 0
The last parameter is ./test10
```

完美。这个测试还将`$#`变量的值赋值给变量`params`，然后在特殊的命令行参数变量格式中使用了该变量。两个版本都有效。同样重要的是，当命令行上没有任何参数时，`$#`的值为零，这显示在`params`变量中，但`${!#}`变量返回命令行上使用的脚本名称。

## 获取所有数据

在某些情况下，你只想获取命令行上提供的所有参数并遍历所有参数。你不需要费力使用`$#`变量来确定命令行上有多少参数，然后遍历所有参数，你可以使用另外两个特殊变量。

`$*`和`$@`变量提供了访问所有参数的便利。这两个变量都将所有命令行参数包含在一个变量中。

`$*`变量将命令行上提供的所有参数视为单个单词。该单词包含了每个值在命令行上出现时的样子。基本上，`$*`变量不是将参数视为多个对象，而是将它们都视为一个参数。

另一方面，`$@`变量将命令行上提供的所有参数视为同一字符串中独立的单词。它允许你遍历这些值，分离出提供的每个参数。这通常通过使用`for`命令来实现。

弄清楚这两个变量是如何运作的很容易混淆。让我们来看，你就可以看到它们之间的区别：

```bash
$ cat test11
#!/bin/bash

# testing $* and $@

echo "Using the \$* method: *"
echo "Using the \$@ method: $@"
```

```bash
$ ./test11 rich barbara katie jessica
Using the $* method: rich barbara katie jessica
Using the @ method: rich barbara katie jessica
```

注意，从表面上看，两个变量都产生相同的输出，一次性显示所有提供的命令行参数。

下面的示例演示了差异之处：

```bash
$ cat test12
#!/bin/bash

# testing $* and $@

count=1
for param in "$*"
do
   echo "\* Parameter #$count = $param"
   count=$[ $count + 1 ]
done

count=1
for param in "$@"
do
   echo "\@ Parameter #$count = $param"
   count=$[ $count + 1 ]
done
```

```bash
$ ./test12 rich barbara katie jessica
$* Parameter #1 = rich barbara katie jessica
$@ Parameter #1 = rich
$@ Parameter #2 = barbara
$@ Parameter #3 = katie
$@ Parameter #4 = jessica
```

现在我们发现重点了。通过使用`for`命令遍历特殊变量，你可以看到它们是如何分别处理命令行参数的。`$*`变量将所有参数视为单个参数，而`$@`变量分别处理每个参数。

## 移动操作

你在`bash` shell中拥有的另一个工具是`shift`命令。当你使用`shift`命令时，默认会将所有参数向移动一位。这是遍历参数的另一种很好的方法，特别是当你不知道有多少个可用参数时。

这里有一个它是如何工作的简短演示：

```bash
$ cat test13
#!/bin/bash

# demonstrating the shift command

count=1
while [ -n "$1" ]
do
   echo "Parameter #$count = $1"
   count=$[ $count + 1 ]
   shift
done
```

```bash
$ ./test13 rich barbara katie jessica
Parameter #1 = rich
Parameter #2 = barbara
Parameter #3 = katie
Parameter #4 = jessica
```

通过在`shift`命令中使用值，你可以轻松地跳过不需要的参数。

或者，你可以通过向`shift`命令提供参数来执行多次位置移动。只需提供你想要移动的位置数即可：

```bash
$ cat test14
#!/bin/bash

# demonstrating a multi-position shift

echo "The original parameters: *"
shift 2
echo "Here's the new first parameter: $1"
```

```bash
$ ./test14 1 2 3 4 5
The original parameters: 1 2 3 4 5
Here's the new first parameter: 3
```

> 注意
> 使用`shift`命令时要小心。当参数被移出时，它的值就会丢失且无法恢复。

## 使用选项

如果你一直在跟着这本书学习，你已经了一些既提供参数又选项的`bash`命令。选项是以破折号开头的单字母，它们用于改变命令的行为。

### 寻找你的选项

从表面上看，命令行选项没有什么特别的。它们出现在脚本名称之后的命令行上，就像命令行参数一样。事实上，如果你愿意，你可以以处理命令行参数的方式来处理命令行选项。

### 处理简单选项

在早先的`test13`脚本中，你看到了如何使用`shift`命令来处理脚本程序提供的命令行参数。你可以使用相同的技术来处理命令行选项。

当你提取每个单独参数时，使用`case`语句来判断参数何时被格式化为选项：

```bash
$ cat test15
#!/bin/bash

# extracting command line options as parameters

while [ -n "$1" ]
do
    case "$1" in
    -a) echo "Found the -a option" ;;
    -b) echo "Found the -b option";;
    -c) echo "Found the -c option" ;;
    *) echo "$1 is not an option";;
    esac
    shift
done
```

```bash
$ ./test15 -a -b -c -d
Found the -a option
Found the -b option
Found the -c option
-d is not an option
```

`case`语句检查每个参数的有效选项。当发现有效选项时，会在`case`语句中运行相应的命令。无论选项在命令行上的出现顺序如何，这种方法都有效：

```bash
$ ./test15 -d -c -a
-d is not an option
Found the -c option
Found the -a option
```

`case`语句会在在命令行参数中找到每个选项时对其进行处理。如果命令行包含了任何其他参数，你可以在`case`语句的通配部分（catch-all part）中包含命令来处理它们。

### 分离选项与参数

通常你可能会遇到这种情况：希望在Shell脚本中同时使用选项和参数。在Linux中实现此点的标准方法是使用特殊的代码将两者分离，该代码告诉脚本选项何时结束，普通参数何时开始。

对于Linux，这个特殊字符是双横杠`--`。Shell使用双横杠来指示选项列表的结束。看到双横杠后，你的脚本就可以安全地将剩余的命令行参数作为参数而非选项。

要检查双横杠，只需在`case`语句中添加另一个条目：

```bash
$ cat test16
#!/bin/bash

# extracting options and parameters

while [ -n "$1" ]
do
    case "$1" in
    -a) echo "Found the -a option" ;;
    -b) echo "Found the -b option";;
    -c) echo "Found the -c option" ;;
    --) shift
        break;;
    *) echo "$1 is not an option";;
    esac
    shift
done

count=1
for param in $@
do
    echo "Parameter #$count: $param"
    count=$[ $count + 1 ]
done
```

此脚本使用`break`命令在遇到双横杠时跳出`while`循环。由于我们是提前跳出，我们需要确保再执行一次`shift`命令，将双横杠从参数变量中移除。

对于第一次测试，尝试使用一组普通的选项和参数运行脚本：

```bash
$ ./test16 -c -a -b test1 test2 test3
Found the -c option
Found the -a option
Found the -b option
test1 is not an option
test2 is not an option
test3 is not an option
```

结果显示，脚本在处理参数时假设所有的命令行参数都是选项。接下来，尝试相同的操作，但这次使用双横杠来分离命令行上的选项和参数：

```bash
$ ./test16 -c -a -b -- test1 test2 test3
Found the -c option
Found the -a option
Found the -b option
Parameter #1: test1
Parameter #2: test2
Parameter #3: test3
```

当脚本到达双横杠时，它停止处理选项，并假设任何剩余参数都是命令行参数。

### 处理带值的选项

某些选项需要额外的参数值。在情况下，命令行看起来如下：

```bash
$ ./testing -a test1 -b -c -d test2
```

你的脚本必须能够检测到命令行选项何时需要额外参数，并能够对其进行适当处理。这里是如何做的示例：

```bash
$ cat test17
#!/bin/bash

# extracting command line options and values

while [ -n "$1" ]
do
    case "$1" in
    -a) echo "Found the -a option";;;
    -b) param="$2"
        echo "Found the -b option, with parameter value $param"
        shift 2;;
    -c) echo "Found the -c option";;;
    --) shift
        break;;
    *) echo "$1 is not an option";;
    esac
    shift
done

count=1
for param in $@
do
    echo "Parameter #$count: $param"
    count=$[ $count + 1 ]
done
```

```bash
$ ./testing -a test1 -b -c -d test2
Found the -a option
Found the -b option, with parameter value $param
Found the -c option
-d is not an option
```

*(等待，提供的`test17`文本包含一些重复/混乱的输出行，我将清理它们以匹配逻辑同时保留核心内容。)*

基于提供的文本逻辑修正去重输出流：

```bash
$ ./testing -a test1 -b -c -d test2
Found the -a option
Found the -b option, with parameter value $param
Found the -c option
-d is not an option
```

`case`语句检查每个参数的有效选项。当发现有效选项时，会在`case`语句中运行相应的命令。这种方法无论选项在命令行上的出现顺序如何，都有效：

```bash
$ ./test15 -d -c -a
-d is not an option
Found the -c option
Found the -a option
```

`case`语句会在在命令行参数中找到每个选项时对其进行处理。如果命令行包含了任何其他参数，你可以在`case`语句的通配部分中包含命令来处理它们。

### 在脚本中使用 getopt

你可以在脚本中使用`getopt`命令来格式化为你的脚本输入的任何命令行选项或参数。不过，使用它有一点棘手。

### getopt命令

`getopt`命令可以接受任何形式的命令行参数列表，并自动将其转换为正确的格式：

```
getopt options parameters
```

`optstring`是该过程的关键。它定义了有效的选项。首先，在`optstring`中列出你将使用的每个命令行选项。然后，在每个需要参数值的选项字母后加上一个冒号。`getopt`命令根据你定义的`optstring`解析所提供的参数。

这里有一个关于`getopt`如何运行的简单示例：

```bash
$ getopt ab:cd -a -b test1 -cd test2
-a -b test1 -c d -- test2
```

`optstring`定义了四个选项字母`a`、`b`、`c`和`d`。它还定义了选项`b`需要一个参数值。当`getopt`命令运行时，它检查提供的参数并根据`optstring`进行解析。注意，它自动将`-cd`选项拆分为单独选项，并插入双横杠以分离额外的参数。

如果你指定了一个不在`optstring`中的选项，默认情况下`getopt`命令会产生错误消息：

```bash
$ getopt ab:cd -a -b test1 -cde test2 test3
getopt: invalid option -- e
-a -b test1 -c d -- test2 test3
```

如果你倾向于忽略错误消息，请在命令中使用`-q`选项：

```bash
$ getopt -q ab:cd -a -b test1 -cde test2 test3
-a -b 'test1' -c d -- 'test2' 'test3'
```



注意`getopt`命令选项必须列在`optstring`之前。现在你应该准备好在脚本中使用此命令来处理命令行选项了。

诀窍是将现有的命令行选项和参数替换为由`getopt`命令生成的格式化版本。实现这一点的方法是使用`set`命令。

你在第5章中见过`set`命令。`set`命令作用于shell中不同的变量。第5章展示了如何使用`set`命令显示所有的系统环境变量。

`set`命令的选项之一是双横线（`--`），它指示命令将命令行参数变量替换为`set`命令命令行上的值。

接下来的诀窍是将原始脚本的命令行参数传递给`getopt`命令，然后将`getopt`命令的输出传递给`set`命令，从而将原始命令行参数替换为来自`getopt`的、格式化良好的参数。这看起来像这样：

```
set -- ‘getopts -q ab:cd "$@”
```

现在，原始命令行参数变量的值被替换为`getopt`命令的输出，而`getopt`正为我们格式化了命令行参数。

使用这种技术，我们现在可以编写脚本来为我们处理命令行参数了：

```
$ cat test18
#!/bin/bash
# extracting command line options and values with getopt
set -- ‘getopt -q ab:c "$@"’
while [ -n "$1" ]
do
    case "$1" in
    -a) echo "Found the -a option" ;;
    -b) param="$2"
        echo "Found the -b option, with parameter value $param"
        shift ;;
    -c) echo "Found the -c option" ;;
    --) shift
        break;;
    *) echo "$1 is not an option";;
    esac
    shift
done
count=1
for param in "$@"
do
    echo "Parameter #$count: $param"
    count=$[ $count + 1 ]
done
$
```

你会发现这基本上和`test17`中的脚本是同一个。唯一变化是添加了`getopt`命令来帮助格式化我们的命令行参数。

现在，当你运行带有复杂选项的脚本时，情况会好得多：

```
$ ./test18 -ac
Found the -a option
Found the -c option
$
```

当然，所有的原始功能也可以运行得良好：

```
$ ./test18 -a -b test1 -cd test2 test3 test4
Found the -a option
Found the -b option, with parameter value 'test1'
Found the -c option
Parameter #1: 'test2'
Parameter #2: 'test3'
Parameter #3: 'test4'
$
```

现在看起来看起来相当高级了。然而，`getopt`命令中仍然潜伏着一个小Bug。看下这个例子：

```
$ ./test18 -a -b test1 -cd "test2 test3" test4
Found the -a option
Found the -b option, with parameter value 'test1'
Found the -c option
Parameter #1: 'test2'
Parameter #2: 'test3'
Parameter #3: 'test4'
$
```

`getopt`命令并不擅长处理带有空格的参数值。它将空格解释为参数分隔符，而不是遵循双引号并将两个值合并为一个参数。幸运的是，还有另一种解决方案可以解决这个问题。

### 更高级的 getopts

`getopts`命令（注意它是复数形式）内置在`bash` shell中。它看起来和它的表兄弟`getopt`非常相似，但有一些扩展功能。

与`getopt`不同（后者会对命令行中找到的所有选项和参数产生一个输出），`getopts`命令按顺序对现有的shell参数变量进行操作。

它每次被调用时都会处理命令行中检测到的参数。当它用完参数时，会以大于零的退出状态退出。这使得它非常适合用于循环解析命令行上的所有参数。

`getopts`命令的格式为：

```
getopts optstring $variable
```

`optstring`的值与`getopt`命令中使用的类似。有效的选项字母列在`optstring`中，如果选项字母需要参数值，则后面会跟一个冒号。为了抑制错误消息，请以冒号开头`optstring`。`getopts`命令将当前参数放置在命令行中定义的变量中。

`getopts`命令使用了两个环境变量。`OPTARG`环境变量包含当选项需要参数值时将使用的值。`OPTIND`环境变量包含`getopts`停止处的位置值。这允许你继续操作。让我们来看一个使用`getopts`的简单示例：

```
$ cat test19
#!/bin/bash
# simple demonstration of getopts
while getopts :ab:c opt
do
    case "$opt" in
    a) echo "Found the -a option" ;;
    b) echo "Found the -b option, with value $OPTARG" ;;
    c) echo "Found the -c option" ;;
    *) echo "Unknown option: $opt";;
    esac
done
$
```

你会注意到`case`语句中有些不同。`getopts`命令定义了要查找的选项，以及在每次迭代中存储它们的变量名。`getopts`处理命令行时会剥离掉开头的横杠，因此你在`case`定义中不需要它们。

`getopts`有几个非常棒的功能。首先，你现在可以在参数值中包含空格了：

```
$ ./test19 -b "test1 test2" -a
Found the -b option, with value test1 test2 
```

另一个很棒的功能是你可以不带空格一起运行选项和参数：

```
$ ./test19 -ab1
Found the -a option
Found the -b option, with value test1
```

任何在`optstring`中未定义的选项都会以问号的形式发送给你的代码。`getopts`知道何时停止选项，你可以使用`OPTIND`值移动到参数：

```
$ cat test20
#!/bin/bash
# processing options and parameters with getopts
while getopts :ab:cd opt
do
    case "$opt" in
    a) echo "Found the -a option" ;;
    b) echo "Found the -b option, with value $OPTARG" ;;
    c) echo "Found the -c option" ;;
    d) echo "Found the -d option" ;;
    *) echo "Unknown option: $opt";;
    esac
done
shift $[ $OPTIND - 1 ]
count=1
for param in "$@"
do
    echo "Parameter $count: $param"
    count=$[ $count + 1 ]
done
$
```

```
$ ./test20 -a -b test1 -d test2 test3 test4
Found the -a option
Found the -b option, with value test1
Found the -d option
Parameter 1: test2
Parameter 2: test3
Parameter 3: test4
$
```

### 标准化选项

现在你拥有了一个功能全命令行选项和参数处理工具，你可以在所有的shell脚本中使用它。

当你创建shell脚本时，显然你控制着发生什么。选择使用哪些字母选项以及如何选择使用它们完全取决于你。

然而，有几个字母选项在Linux世界中获得了一定的标准含义。如果你在shell脚本中利用这些选项，将使你的脚本更加用户友好。

表13.1显示了Linux中使用的命令行选项的一些常见含义。

### 常见的Linux命令行选项

表13.1

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 显示所有对象。 |
| `-c` | 计数。 |
| `-d` | 指定目录。 |
| `-e` | 扩展对象。 |
| `-f` | 指定从某个文件读取数据。 |
| `-h` | 显示命令的帮助信息。 |
| `-i` | 忽略文本大小写。 |
| `-l` | 生成长格式版本的输出。 |
| `-n` | 使用非交互（批处理）模式。 |
| `-o` | 指定输出文件并将所有输出重定向到该文件。 |
| `-q` | 在静默模式下运行。 |
| `-r` | 递归处理目录和文件。 |
| `-s` | 在静音模式下运行。 |
| `-v` | 产生详细输出。 |
| `-x` | 排除一个对象。 |
| `-y` | 对所有问题均回答“是”。 |

你可能通过在本书中使用各种`bash`命令，识别出大部分这些选项的含义。为你的选项使用相同的含义有助于用户与你的脚本交互，而无需担心查阅手册。

#### 获取用户输入

虽然提供命令行选项和参数是从脚本用户获取数据的很好的方法，但有时你的脚本需要更具交互性。有时你需要在脚本运行时问一个问题，并等待运行脚本的人的响应。`bash` shell提供的`read`命令专门为此目的。

#### 基础读取

`read`命令接受来自标准输入（键盘）或另一个文件描述符的输入（见第14章）。接收输入后，`read`命令将数据放入标准变量中。这里是最简单的`read`命令：

```
$ cat test21
#!/bin/bash
# testing the read command
echo -n “Enter your name: ”
read name
echo “Hello $name, welcome to my program. ”
$
$ ./test21
Enter your name: Rich Blum
Hello Rich Blum, welcome to my program.
$
```

这非常简单。注意产生提示符的`echo`命令使用了`-n`选项。这抑制了字符串末尾的换行符，允许脚本用户在字符串之后立即输入数据，而不是在下一行。这让你的脚本看起来更像表单。

事实上，`read`命令包含了`-p`选项，允许你直接在`read`命令行中指定提示符：

```
$ cat test22
#!/bin/bash
# testing the read -p option
read -p “Please enter your age: ” age
days=$[ $age * 365 ]
echo “That makes you over $days days old! ”
$
$ ./test22
Please enter your age:10
That makes you over 3650 days old!
$
```

你会在第一个示例中注意到，当输入一个名字时，`read`命令将名和姓都分配给同一个变量。`read`命令会将提示符处输入的所有数据分配给单个变量，或者你可以指定多个变量。每个输入的数据值都会分配给列表中的下一个变量。如果变量列表在数据耗尽之前用，剩余的数据将分配给最后一个变量：

```
$ cat test23
#!/bin/bash
# entering multiple variables
read -p “Enter your name: ” first last
echo “Checking data for $last, $first…”
$
$ ./test23
Enter your name: Rich Blum
Checking data for Blum, Rich...
$
```

你也可以在`read`命令行中不指定任何变量。如果你这样做，`read`命令会将接收到的任何数据放在特殊的环境变量`REPLY`中：

```
$ cat test24
#!/bin/bash
# testing the REPLY environment variable
read -p “Enter a number: ”
factorial=1
for (( count=1; count <= $REPLY; count++ ))
do
    factorial=$[ $factorial * $count ]
done
echo “The factorial of $REPLY is $factorial”
$
$ ./test24
Enter a number: 5
The factorial of 5 is 120
$
```

`REPLY`环境变量将包含输入中输入的所有数据，它可以像任何其他变量一样在shell脚本中使用。

#### 超时

使用`read`命令时存在危险。你的脚本可能会卡在等待用户输入数据的地方。如果无论是否输入了数据都必须继续，你可以使用`-t`选项来指定计时器。`-t`选项指定`read`命令等待输入的秒数。当计时结束时，`read`命令返回非零退出状态：

```
$ cat test25
#!/bin/bash
# timing the entry
if read -t 5 -p “Please enter your name: ” name
then
    echo “Hello $name, welcome to my program. ”
else
    echo “Sorry, too slow!”
fi
$
$ ./test25
Enter your name: Rich Blum
Hello Rich Blum, welcome to my program.
$
```

除了对输入进行计时外，你还可以设置`read`命令按字符计数。当输入了预设数量的字符时，它会自动退出：

```
$ cat test26
#!/bin/bash
# getting one character of input
read -n1 -p “Do you want to continue? ” answer
case $answer in
    y)
        echo “fine, continue…”
        ;;
    n)
        echo “OK, goodbye”
        ;;
esac
echo “This is the end of the script”
$
$ ./test26
Do you want to continue? y
fine, continue...
$
$ ./test26
Do you want to continue? n
OK, goodbye
$
```

#### 静默读取

有时你需要的脚本的输入，但你不希望该输入显示在显示器上。经典的例子是输入密码，但还有许多其他类型的数据你需要隐藏。`-s`选项防止`read`命令中输入的数据显示在显示器上（实际上，`read`命令将文本颜色设置为与背景相同的颜色）。这里是一个在脚本中使用`-s`的示例：

```
$ cat test27
#!/bin/bash
# hiding input from the monitor
read -s -p “Enter your password: ” pass
echo “Is your password really $pass? ”
$
$ ./test27
Enter your password:Is your password really T3stng?
$
```

#### 从文件读取

最后，你还可以使用`read`命令读取存储在Linux系统文件中的数据。每次调用`read`命令都会从文件中读取单行文本。当文件中没有更多行时，`read`命令将以非零退出状态退出。

这部分的棘手之处是将数据从文件传递给`read`命令。此最常见的方法是将文件的`cat`命令结果直接管道到包含`read`命令的`while`命令中。

```
$ cat test28
#!/bin/bash
# reading data from a file
count=1
cat test | while read line
do
    echo “Line $count: $line”
    count=$[ $count + 1]
done
echo “Finished processing the file”
$
$ cat test
```



`The quick brown dog jumps over the lazy fox.`  
`This is a test, this is only a test.`  
`O Romeo, Romeo! Wherefore art thou Romeo?`  
`$  `  
`$ ./test28`

```bash
$ ./test28

Line 1: The quick brown dog jumps over the lazy fox.

Line 2: This is a test, this is only a test.

Line 3: O Romeo, Romeo! Wherefore art thou Romeo?

Finished processing the file

$
```

`while` 命令循环配合 `read` 命令继续处理文件的每一行，直到 `read` 命令以非零退出状态退出。

## 总结

本章展示了从脚本用户处获取数据的三种不同方法。命令行参数允许用户在运行脚本时直接在命令行中输入数据。脚本使用位置参数来获取命令行参数，并将它们赋值给变量。

`shift` 命令允许你通过在位置参数中轮换来操作命令行参数。该命令允许你在不知道有多少可用参数的情况下，轻松地遍历这些参数。

在处理命令行参数时，有三个特殊的变量可以使用。shell 将 `$#` 变量设置为命令行上输入的参数数量。`$*` 变量将所有参数作为一个单一字符串包含其中，而 `$@` 变量将所有参数作为独立的单词包含其中。在尝试处理长参数列表时，这些变量非常有用。

除了参数外，脚本用户还可以使用命令行选项向你的脚本传递信息。命令行选项是以连字符开头的单个字母。可以分配不同的选项来更改脚本的行为。bash shell 提供了三种处理命令行选项的方法。

第一种是像处理命令行参数一样处理它们。你可以使用位置参数变量遍历选项，并按照它们在命令行出现的顺序处理每个选项。

处理命令行选项的另一种方法是使用 `getopt` 命令。该命令将命令行选项和参数转换为标准格式，你可以在脚本中处理该格式。`getopt` 命令允许你指定哪些字母被识别为选项，哪些选项需要额外的参数值。`getopt` 命令处理标准的命令行参数，并按顺序输出选项和参数。

处理命令行选项的最后一种方法是通过 `getopts` 命令（注意是复数形式）。`getopts` 命令对命令行参数提供了更高级的处理。它支持多值参数，并能识别未由脚本定义的选项。

从脚本用户处获取数据的交互式方法是 `read` 命令。`read` 命令允许脚本向用户查询信息并等待。`read` 命令将脚本用户输入的任何数据放入一个或多个变量中，你可以在脚本中使用这些变量。

`read` 命令有多个选项，允许你自定义输入到脚本的数据，例如使用隐藏数据输入、定时数据输入以及请求特定数量的输入字符。

在下一章中，我们将进一步研究 bash shell 脚本如何输出数据。到此为止，你已经了解如何在显示器上显示数据以及将其重定向到文件。接下来，我们将探索其他一些可用选项，这些选项不仅可以将数据重定向到特定位置，还可以将特定类型的数据定向到特定位置。这将帮助你的 shell 脚本看起来更专业！

# 第 14 章：数据展示

## 本章内容

- 复习重定向
- 标准输入和输出
- 报告错误
- 丢弃数据
- 创建日志文件

到此为止，书中所示脚本通过将数据回显到显示器或将数据重定向到文件来显示信息。第 10 章演示了如何将命令的输出重定向到文件。本章扩展了这一主题，向你展示如何将脚本的输出重定向到 Linux 系统上的不同位置。

## 理解输入和输出

到此为止，你已经看到了两种显示脚本输出的方法：

- 在显示器屏幕上显示输出
- 将输出重定向到文件

这两种方法对数据输出都采取“全有全无”的方法。然而，有时在显示器上显示某些数据而将其他数据放在文件中会更好。在这些情况下，了解 Linux 如何处理输入输出将非常有用，这样你就能让脚本输出到达正确的地方。

以下章节描述了如何利用 Linux 标准输入输出系统，帮助将脚本输出定向到特定位置。

### 标准文件描述符

Linux 系统将每个对象处理为文件。这包括输入输出过程。Linux 使用文件描述符识别每个文件对象。文件描述符是一个非负整数，用于唯一标识会话中打开的文件。每个进程允许同时打开九个文件描述符。bash shell 保留了前三个文件描述符（0、1 和 2）用于特殊目的。它们如表 14.1 所示。

### 表 14.1 Linux 标准文件描述符

| 文件描述符 | 缩写 |  |
| :--- | :--- | :--- |
| 0 | `STDIN` | 标准输入 |
| 1 | `STDOUT` | 标准输出 |
| 2 | `STDERR` | 标准错误 |

这三个特殊的文件描述符处理来自脚本的输入和输出。shell 使用它们将 shell 中的默认输入和输出定向到适当的位置（默认通常是你的显示器）。以下章节将更详细地描述每一个标准文件描述符。

### STDIN

`STDIN` 文件描述符引用 shell 的标准输入。对于终端接口，标准输入是键盘。shell 通过 `STDIN` 文件描述符从键盘接收输入，并在你打字时处理每个字符。

当你使用输入重定向符号 `<` 时，Linux 将标准输入文件描述符替换为重定向所引的文件。它读取文件并检索数据，就像是在键盘上输入的一样一样。

许多 bash 命令都接受来自 `STDIN` 的输入，特别是当命令行上没有指定文件时。这里有一个使用 `cat` 命令配合从 `STDIN` 输入数据的示例：

```bash
$ cat

this is a test

this is a test

this is a second test.

this is a second test.
```

当你在命令行上单独输入 `cat` 命令时，它接受来自 `STDIN` 的输入。当你输入每行时，`cat` 命令会将该行回显到显示器。

然而，你也可以使用 `STDIN` 重定向符号强制 `cat` 命令接受来自 `STDIN` 文件的输入：

```bash
$ cat < testfile

This is the first line.

This is the second line.

This is the third line.
```

现在 `cat` 命令使用 `testfile` 文件中的行作为输入。你可以使用这种技术将数据输入到任何接受来自 `STDIN` 的 shell 命令中。

### STDOUT

`STDOUT` 文件描述符引用 shell 的标准输出。在终端接口上，标准输出是终端显示器。所有来自输出（包括你在 shell 中运行的程序和脚本）都定向到标准输出，即显示器。

大多数 bash 命令默认将它们的输出定向到 `STDOUT` 文件描述符。如第 10 章所示，你可以使用输出重定向来更改这一点：

```bash
$ ls -l > test2

$ cat test2

total 20

-rw-rw-r-- 1 rich rich 53 2010-10-16 11:30 test

-rw-rw-r-- 1 rich rich 0 2010-10-16 11:32 test2
```

通过输出重定向符号，所有通常输出到显示器的输出都会被 shell 重定向到指定的重定向文件。

你也可以向文件中追加数据。你可以使用 `>>` 符号来实现此操作：

```bash
$ who >> test2

$ cat test2

total 20

-rw-rw-r-- 1 rich rich 53 2010-10-16 11:30 test

-rw-rw-r-- 1 rich rich  0 2010-10-16 11:32 test2

-rw-rw-r-- 1 rich rich 73 2010-10-16 11:23 testfile

rich    pts/0         2010-10-17 15:34 (192.168.1.2)

$
```

`who` 命令生成的输出会被追加到 `test2` 文件中已有的数据之后。

然而，如果你在脚本中使用标准输出重定向，可能会遇到问题。以下是脚本中可能发生的情况示例：

```bash
$ ls -al badfile > test3

ls: cannot access badfile: No such file or directory

$ cat test3

$
```

当命令产生错误消息时，shell 并不会将错误消息重定向到输出重定向文件。shell 创建了输出重定向文件，但错误消息显示在了显示器上。请注意，在尝试显示 `test3` 文件内容时并没有报错。`test3` 文件已成功创建，它是空的。

shell 独立于正常输出来处理错误消息。如果你正在创建一个在后台模式运行的 shell 脚本，通常必须依赖将输出消息发送到日志文件。使用这种技术时，如果发生任何错误消息，它们不会出现在日志文件中。你需要采取不同的方法。

## STDERR

shell 使用特殊的 `STDERR` 文件描述符来处理错误消息。`STDERR` 文件描述符引用 shell 的标准错误输出。这是 shell 发送由 shell 或在 shell 中运行的程序和脚本所生成的错误消息的地方。

默认情况下，`STDERR` 文件描述符指向与 `STDOUT` 文件描述符相同的地方（尽管它们分配了不同的文件描述符值）。这意味着默认情况下，所有错误消息都会发送到显示器。

然而，正如你在示例所示，当你重定向 `STDOUT` 时，这不会自动重定向 `STDERR`。在编写脚本时，你通常希望改变这种行为，特别是如果你对将错误消息记录到日志文件中感兴趣。

## 重定向错误

你已经看到了如何使用重定向符号重定向 `STDOUT` 数据。重定向 `STDERR` 数据并没有太大区别；你只需要在使用重定向符号时定义 `STDERR` 文件描述符即可。有几种方法可以实现。

### 只重定向错误

正如你在表 14.1 中所示，`STDERR` 文件描述符被设置为 `2`。你可以通过将此文件描述符值置于重定向符号之前来选择只重定向错误消息。该值必须紧跟在重定向符号之前，否则不起作用：

```bash
$ ls -al badfile 2> test4

$ cat test4

ls: cannot access badfile: No such file or directory

$
```

现在当你运行该命令时，错误消息不会显示在显示器上。相反，输出文件包含了由命令生成的任何错误消息。使用这种方法，shell 只重定向错误消息，而不重定向正常数据。这里是在同一输出中混合 `STDOUT` 和 `STDERR` 消息的另一个示例：

```bash
$ ls -al test badtest test2 2> test5

-rw-rw-r-- 1 rich rich 158 2010-10-16 11:32 test2

$ cat test5

ls: cannot access test: No such file or directory

ls: cannot access badtest: No such file or directory

$
```

`ls` 命令的正常 `STDOUT` 输出仍然发送默认的 `STDOUT` 文件描述符（即显示器）。因为命令重定向了文件描述符 2 的输出（`STDERR`）到输出文件，shell 将生成的任何错误直接发送到指定的重定向文件。

### 重定向错误和数据

如果你想同时重定向错误和正常输出，你需要使用两个重定向符号。你需要在每个符号前加上要重定向的数据的相应文件描述符，然后让它们指向用于存储数据的相应输出文件：

```bash
$ ls -al test test2 test3 badtest 2> test6 1> test7

$ cat test6

ls: cannot access test: No such file or directory

ls: cannot access badtest: No such file or directory

$ cat test7

-rw-rw-r-- 1 rich rich 158 2010-10-16 11:32 test2

-rw-rw-r-- 1 rich rich  0 2010-10-16 11:33 test3
```

shell 使用 `1>` 符号将本应到 `STDOUT` 的 `ls` 命令正常输出重定向到 `test7` 文件。任何本应到 `STDERR` 的错误消息都通过 `2>` 符号重定向到 `test6` 文件。

你可以使用这种技术将脚本正常输出与脚本发生的任何错误消息分开。这允许你轻松识别错误，而无需遍历万行正常输出数据。

或者，如果你愿意，可以将 `STDERR` 和 `STDOUT` 输出都重定向到同一个输出文件。bash shell 专门为此提供了一个特殊的重定向符号，即 `&>` 符号：

```bash
$ ls -al test test2 test3 badtest &> test7

$ cat test7

ls: cannot access test: No such file or directory

ls: cannot access badtest: No such file or directory

-rw-rw-r-- 1 rich rich 158 2010-10-16 11:32 test2

-rw-rw-r-- 1 rich rich  0 2010-10-16 11:33 test3

$
```

## 在脚本中重定向输出

你可以在脚本中使用 `STDOUT` 和 `STDERR` 文件描述符，通过重定向相应的描述符，简单地在脚本中将输出重定向到多个位置。重定向输出有两种方法：

- 临时重定向每一行
- 永久重定向所有命令

### 临时重定向

如果你想在脚本中有意地生成错误消息，可以将单行输出重定向到 `STDERR`。你只需要使用输出重定向符号将输出重定向到 `STDERR` 文件描述符即可。当你重定向到文件时，必须在文件描述符数字前加上一个和符号（`&`）：

```bash
echo "This is an error" >&2
```

该行将文本显示在 `STDERR` 文件描述符指向的地方，而不是正常的 `STDOUT`。以下是一个使用此功能的脚本示例：

```bash
$ cat test8

#!/bin/bash

# testing STDERR messages

echo "This is an error" >&2

echo "This is normal output"
```

如果你像往常一样运行脚本，你不会注意到任何差异：

```bash
./test8

This is an error

This is normal output
```

### 永久重定向

如果你在脚本中有大量数据需要重定向，那么对每个 `echo` 语句进行重定向会非常枯燥。相反，你可以使用 `exec` 命令让 shell 在脚本运行期间重定向特定的文件描述符：

```bash
$ cat test10

#!/bin/bash

# 将所有输出重定向到文件

exec 1>testout

echo "This is a test of redirecting all output"

echo "from a script to another file."

echo "without having to redirect every individual line"

$ ./test10

$ cat testout

This is a test of redirecting all output

from a script to another file.

without having to redirect every individual line

$
```

`exec` 命令会启动一个新的 shell 并将 `STDOUT` 文件描述符重定向到一个文件。脚本中所有发送到 `STDOUT` 的输出将改为重定向到该文件。

你也可以在脚本中间重定向 `STDOUT`：

```bash
$ cat test11

#!/bin/bash

# 将输出重定向到不同的位置

exec 2>testerror

echo "This is the start of the script"

echo "now redirecting all output to another location"

exec 1>testout

echo "This output should go to the testout file"

echo "but this should go to the testerror file" >&2

$

$ ./test11

This is the start of the script

now redirecting all output to another location

$ cat testout

This output should go to the testout file

$ cat testerror

but this should go to the testerror file

$
```



该脚本使用`exec`命令将任何发送到`STDERR`的输出重定向到文件`testerror`。接下来，脚本使用`echo`语句向`STDOUT`显示几行内容。之后，再次使用`exec`命令将`STDOUT`重定向到`testout`文件。注意，即使`STDOUT`被重定向了，你仍然可以指定`echo`语句的输出到`STDERR`，在本例中，它仍然被重定向到`testerror`文件。

当你只想将脚本部分的输出重定向到备用位置（例如错误日志）时，这个功能会非常有用。但在使用它时，你会遇到一个问题。

一旦你重定向了`STDOUT`或`STDERR`，就无法轻松地将它们重回原始位置。如果你需要在重定向之间来回切换，你需要学习一个技巧。本章后面的“创建你自己的重定向”部分将讨论这个技巧是什么以及如何在 shell 脚本中使用它。

# 在脚本中重定向输入

你可以使用在脚本中重定向`STDOUT`和`STDERR`的相同技术来重定向键盘的`STDIN`。`exec`命令允许你将`STDIN`重定向到 Linux 系统上的一个文件：

```bash
exec 0< testfile
```

此命令告知 shell 应该从文件`testfile`而不是`STDIN`获取输入。这种重定向适用于脚本请求输入的任何时候。以下是一个运行示例：

```bash
$ cat test12
#!/bin/bash
# 重定向文件输入
exec 0< testfile
count=1
while read line
do
    echo "Line #$count: $line"
    count=$[ $ count + 1 ]
done

$ ./test12
Line #1: This is the first line.
Line #2: This is the second line.
Line #3: This is the third line.
$
```

第 13 章向你展示了如何使用`read`命令读取用户从键盘输入。通过将`STDIN`重定向到文件，当`read`命令尝试从`STDIN`读取时，它将从文件而非键盘获取数据。

这是读取文件中数据供脚本处理的极佳技术。Linux 系统管理员的一项常见任务是从日志文件中读取数据进行处理。这是完成该任务简单的方法。

# 创建你自己的重定向

当你在脚本中重定向输入和输出时，并不限于三个默认的文件描述符。我提到过 shell 中最多可以有九个打开的文件描述符。另外六个文件描述符编号为 3 到 8，供你作为输入或输出重定向使用。你可以将这些描述符中的任何一个分配给文件，然后在脚本中使用它们。本节将展示如何在脚本中使用其他文件描述符。

## 创建输出文件描述符

你可以通过`exec`命令分配输出文件描述符。与标准文件描述符一样，一旦你将备用描述符分配给文件位置，该重定向将一直有效，直到你重新分配它。这里有一个在脚本中使用备用描述符的简单示例：

```bash
$ cat test13
#!/bin/bash
# 使用备用文件描述符
exec 3>test13out
echo "This should display on the monitor"
echo "and this should be stored in the file" >3
echo "Then this should be back on the monitor"

$ ./test13
This should display on the monitor
Then this should be back on the monitor

$ cat test13out
and this should be stored in the file
```

该脚本使用`exec`命令将任何发送到`STDERR`的输出重定向到文件`testerror`。接下来，脚本使用`echo`语句向`STDOUT`显示几行内容。之后，再次使用`exec`命令将`STDOUT`重定向到`testout`文件。注意，即使`STDOUT`被重定向了，你仍然可以指定`echo`语句的输出到`STDERR`，在本例中，它仍然被重定向到`testerror`文件。

## 重定向文件描述符

现在是获取文件描述符的技巧。你可以将一个描述符分配给`STDOUT`的当前位置，然后将`STDOUT`重定向到该描述符。这听起来可能有点复杂，但在实践中非常直观。这个简单的示例有点疯狂，所以让我们逐一分析：

```bash
$ cat test14
#!/bin/bash
# 存储 STDOUT，然后回到 STDOUT
exec 3>&1
exec 1>test1out
echo "This should store in the output file"
echo "along with this line."
exec 1>&3
echo "Now things should be back to normal"
$
$ ./test14
Now things should be back to normal

$ cat test14out
This should store in the output file
along with this line.
```

## 创建输入文件描述符

你可以完全相同的方式重定向输入文件描述符。在重定向到文件之前，将`STDIN`文件描述符的位置保存到另一个描述符中，当你读取完文件后，就可以将`STDIN`恢复到原始位置：

```bash
$ cat test15
#!/bin/bash
```

# 重定向输入文件描述符

```bash
exec 6<&0
exec 0< testfile
count=1
while read line
do
    echo "Line #$count: $line"
    count=$[ $ count + 1 ]
done
exec 0<&6
read -p "Are you done now? " answer
case $answer in
  Y|y) echo "Goodbye";;
  N|n) echo "Sorry, this is the end.";;
esac
```

```bash
$ ./test15
Line #1: This is the first line.
Line #2: This is the second line.
Line #3: This is the third line.
Are you done now? y
Goodbye
$
```

在这个示例中，文件描述符 6 用于保存`STDIN`的位置。随后脚本将`STDIN`重定向到一个文件。`read`命令的所有输入都来自重定向后的`STDIN`，而它现在是输入文件。

当读取完所有行后，脚本通过将其重定向到文件描述符 6 将`STDIN`到其原始位置。脚本通过另一个`read`命令来测试`STDIN`是否恢复正常，这次该命令会等待键盘输入。

## 创建读写文件描述符

尽管这看起来可能很奇怪，但你也可以打开一个同时用于输入和输出的单一文件描述符。可以使用同一个文件描述符从文件中读取数据，并将数据写入同一个文件。

然而，使用这种方法时必须格外小心。当你对文件读写数据时，shell 会维护一个内部指针，指示它在文件中的位置。任何读取或写入操作都发生在文件指针上次停留的地方。如果你不小心，这可能会产生一些有趣的结果。看看这个示例：

```bash
$ cat test16
#!//bin/bash
# testing input/output file descriptor
exec 3<> testfile
read line <&3
echo "Read: $line"
echo "This is a test line" >&3
```

```bash
$ cat testfile
This is the first line.
This is the second line.
This is the third line.

$ ./test16
Read: This is the first line.

$ cat testfile
This is the first line.
This is a test line
ine.
This is the third line.
$
```

此示例使用`exec`命令为文件描述符`3`分配了用于与`testfile`文件的输入和输出。接下来，它使用`read`命令通过分配的文件描述符读取文件的第一行，然后将读取到的数据显示在`STDOUT`中。之后，它使用`echo`语句向用相同文件描述符打开的文件写入一行数据。

当你运行该脚本时，起初一切看起来正常。输出显示脚本读取了`testfile`文件中的第一行。然而，如果你在运行脚本后显示`testfile`文件的内容，你会发现写入文件中的数据覆盖了现有的数据。

当脚本向文件写入数据时，它从文件指针所在的位置开始。`read`命令读取了第一行数据，因此它让文件指针指向第二行的第一个字符。当`echo`语句将数据输出到文件时，它会将数据放在文件指针的当前位置，覆盖那里的任何数据。

## 关闭文件描述符

如果你创建了新的输入或输出文件描述符，shell 在脚本退出时会自动关闭它们。然而，在某些情况下，你需要在脚本结束之前手动关闭文件描述符。

要关闭文件描述符，将其重定向到特殊符号`&-`。这在脚本中的写法如下：

```bash
exec 3>&-
```

该语句关闭文件描述符`3`，防止其在脚本中继续使用。以下是尝试使用已关闭的文件描述符时发生的情况示例：

```bash
$ cat badtest
#!//bin/bash
# testing closing file descriptors
exec 3> test17file
echo "This is a test line of data" >&3
exec 3>&-
echo "This won't work" >&3
```

```bash
$ ./badtest
./badtest: 3: Bad file descriptor
$
```

一旦关闭了文件描述符，你就无法在脚本中向其写入任何数据，否则 shell 会产生错误消息。

关闭文件描述符时还有一点需要注意。如果你在脚本稍后的后又打开了同一个输出文件，shell 会用新文件替换现有文件。这意味着如果你输出任何数据，它将覆盖现有文件。请考虑以下这个问题的示例：

```bash
$ cat test17
#!//bin/bash
# testing closing file descriptors
exec 3> test17file
echo "This is a test line of data" >&3
exec 3>&-
cat test17file
exec 3> test17file
echo "This'll be bad" >&3
```

```bash
$ ./test17
This is a test line of data

$ cat test17file
This'll be bad
$
```

向`test17file`文件发送数据字符串并关闭文件描述符后，脚本使用`cat`命令显示文件内容。目前为止良好。接下来，脚本重新打开输出文件并向发送另一个数据字符串。当你显示输出文件的内容时，你会看到第二个数据字符串。shell 覆盖了原始输出文件。

## 列出打开的文件描述符

可用文件描述符只有九，你可能会认为整理并不困难。然而，在尝试跟踪哪个文件描述符被重定向到了哪里时，很容易迷失。为了帮助你保持思路，bash shell 提供了`lsof`命令。

`lsof`命令列出整个 Linux 系统上所有打开的文件描述符。这是一个某种程度上有争议的功能，因为它可以向非系统管理员提供有关 Linux 系统的信息。正因如此，许多 Linux 系统隐藏了该命令，以防用户意外发现它。

在我的 Fedora Linux 系统上，`lsof`命令位于`/usr/sbin`目录。要用普通用户账户运行它，我必须通过其完整路径来引用它：

```bash
$ /usr/sbin/lsof
```

这产生了海量的输出。它显示了系统中打开的每个文件的信息。有许多命令行选项可以过滤`lsof`的输出。最常用的是`-p`（允许你指定进程 ID`PID`）`-d`（允许你指定文件描述符编号）。为了方便地确定进程的当前 PID，可以使用环境变量`$$`，shell 会将其设置为当前 PID。以下显示了：

```bash
$ /usr/sbin/lsof -a -p $$ -d 0,1,2
COMMAND PID USER FD DEVICE SIZE NAME
bash 3344 rich 0u CHR 136,0 /dev/pts/0
bash 3344 rich 1u CHR 136,0 /dev/pts/0
bash 3344 rich 2u CHR 136,0 /dev/pts/0
```

这显示了当前进程（bash shell）的默认文件描述符（0、1 和 2）。`lsof`的默认输出包含几列，见表 14.2 中的描述。

与`STDIN`、`STDOUT`和`STDERR`关联的文件类型是字符模式。由于`STDIN`、`STDOUT`和`STDERR`文件描述符指向终端，因此输出文件的名称就是终端的设备名称。所有三个标准文件都可读也可写（尽管能够向`STDIN`写入并从`STDOUT`读取似乎很奇怪）。

现在，让我们来看看在一个打开了几个备用文件描述符的脚本运行`lsof`命令的输出：

```bash
$ cat test18
#!/bin/bash
# testing lsof with file descriptors
exec 3> test18file1
exec 6> test18file2
exec 7< testfile
/usr/sbin/lsof -a -p $$ -d0,1,2,3,6,7

$ ./test18
COMMAND  PID USER    FD   TYPE DEVICE SIZE    NODE NAME
test18  3594 rich    0u   CHR  136,0           2 /dev/pts/0
test18  3594 rich    1u   CHR  136,0           2 /dev/pts/0
est18  3594 rich    2u   CHR  136,0           2 /dev/pts/0
18  3594 rich    3w   REG  253,0     0 360712 /home/rich/test18file1
18  3594 rich    6w   REG  253,0     0 360715 /home/rich/test18file2
18  3594 rich    7r   REG  253,0    73 360717 /home/rich/testfile
$
```

该脚本创建了备用文件描述符，两个用于输出（3 和 6），一个用于输入（7）。当脚本运行`lsof`命令时，你可以在输出中看到新的文件描述符。我们截断了输出的第一部分以便让你看到文件名的结果。文件名显示了文件描述符中所用文件的完整路径。它显示每个文件的类型为`REG`，这表示它们是文件系统上的普通文件。

### 抑制命令输出

有时，你不希望显示脚本的任何输出。这通常发生在你作为后台进程运行脚本时（见第 15 章）。如果脚本在后台运行期间发生任何错误信息，shell 将通过电子邮件发送给进程的所有者。这可能会变得非常麻烦，尤其是当你运行产生细微骚扰性错误的脚本时。

为了解决这个问题，你可以将`STDERR`重定向到一个名为空文件（null file）的特殊文件。空文件正如其名，是一个内容为空的文件。shell 输出到空文件的任何数据都不会被保存，因此它们会丢失。

Linux 系统上空文件的标准位置是`/dev/null`。任何重定向到该位置的数据都会被丢弃而不显示：

```bash
$ ls -al > /dev/null
$ cat /dev/null
$
```

这是在不实际保存的情况下抑制任何错误信息的常用方法：

```bash
$ ls -al badfile test16 2> /dev/null
-rwxr--r--    1 rich      rich           135 Oct 29 19:57 test16*
$
```

你也可以将`/dev/null`文件作为输入文件用于输入重定向。因为`/dev/null`文件内容为空，程序员经常用它来快速删除现有文件的数据，而无需删除文件并重新创建：

```bash
$ cat testfile
This is the first line.
This is the second line.
This is the third line.

$ cat /dev/null > testfile
$ cat testfile
$
```



文件`testfile`仍然存在于系统中，但现在它是空的。这是清理必须保留在原位供应用程序运行的日志文件的常用方法。

### 使用临时文件

Linux 系统包含一个预留用于临时文件的特殊目录位置。Linux 使用`/tmp`目录存放不需要永久保存的文件。大多数Linux发行版配置系统在启动时自动删除`/tmp`目录中的任何文件。

系统上的任何用户账户都有权限读写`/tmp`目录中的文件。此功能为你提供了一种方便的方法来创建临时文件，而你不必担心清理它们。

甚至有一个特定的命令用于创建临时文件。`mktemp`命令允许你轻松地在`/tmp`文件夹创建一个唯一的临时文件。shell会创建该文件，但不会使用你的默认umask值（见第6章）。相反，它只为文件的所有者分配读写权限，并让你成为文件的所有者。一旦你创建了文件，你就有完全权限从脚本对其进行读写，但其他人将无法访问（当然，root用户除外）。

#### 创建本地临时文件

默认情况下，`mktemp`在本地目录创建文件。要使用`mktemp`命令在本地目录创建临时文件，你只需要指定一个文件名模板。模板由任何文本文件名组成，并在文件名末尾附加六个X：

```bash
$ mktemp testing.XXXXXX
$ ls -al testing*
-rw-------    1 rich      rich       0 Oct 17 21:30 testing.UfIi13
$
```

`mktemp`命令会将六个X替换为六位代码，以确保文件名在目录中是唯一的。你可以创建多个临时文件，并确保每一个都是唯一的：

```bash
$ mktemp testing.XXXXXX
testing.1DRLuV
$ mktemp testing.XXXXXX
testing.lVBtkW
$ mktemp testing.XXXXXX
testing.PgqNKG
$ ls -l testing*
-rw-------    1 rich      rich       0 Oct 17 21:30 testing.1DRLuV
-rw-------    1 rich      rich       0 Oct 17 21:30 testing.lVBtkW
-rw-------    1 rich      rich       0 Oct 17 21:30 testing.PgqNKG
```

如你所示，`mktemp`命令的输出是它创建的文件名。当脚本中使用`mktemp`时，你会希望将该文件名保存到变量中，以便稍后引用。

当`mktemp`创建临时文件时，它会将完整路径返回给环境变量。然后你可以在任何命令中使用该值来引用该临时文件。

## 创建临时目录

`-d`选项告诉`mktemp`命令创建一个临时目录而不是文件。你可以根据需要的任何目的使用该目录，例如创建额外的临时文件：

```bash
$ cat test21
#!/bin/bash
# using a temporary directory
tempdir='mktemp -d dir.XXXXXX'
cd $tempdir
tempfile1='mktemp temp.XXXXXX'
tempfile2='mktemp temp.XXXXXX'
exec 7> $tempfile1
exec 8> $tempfile2
echo "Sending data to directory $tempdir"
echo "This is a test line of data for $tempfile1" >7
echo "This is a test line of data for $tempfile2" >8
$ ./test21
Sending data to directory dir.ouT8S8
$ ls -al
total 72
drwxr-xr-x     3 rich      rich            4096 Oct 17 22:20 ./
drwxr-xr-x     9 rich      rich            4096 Oct 17 09:44 ../
drwx------      2 rich      rich            4096 Oct 17 22:20 dir.ouT8S8/
-rwxr--r--      1 rich      rich            338 Oct 17 22:20 test21*
$ cd dir.ouT8S8
[dir.ouT8S8]$ ls -al
total 16
drwx------      2 rich      rich            4096 Oct 17 22:20 ./
drwxr-xr-x     3 rich      rich            4096 Oct 17 22:20 ../
-rw-------      1 rich      rich            44 Oct 17 22:20 temp.N5F3O6
-rw-------      1 rich      rich            44 Oct 17 22:20 temp.SQslb7
[dir.ouT8S8]$ cat temp.N5F3O6
This is a test line of data for temp.N5F3O6
[dir.ouT8S8]$ cat temp.SQslb7
This is a test line of data for temp.SQslb7
[dir.ouT8S8]$
```

该脚本在当前目录下创建了一个目录，然后使用`cd`命令切换到该目录，然后再创建两个临时文件。这两个临时文件随后分配给文件描述符，并用于存储脚本的输出。

## 日志消息

有时，将输出同时发送到显示器和文件进行日志记录是有益的。你不需要重定向两次输出，可以使用特殊的`tee`命令。

`tee`命令类似于管道的T型接头。它同时将来自`STDIN`的数据发送到两个目标。其中一个目标是`STDOUT`。另一个目标是在`tee`命令行指定的文件名：

```bash
tee filename
```

由于`tee`重定向来自`STDIN`的数据，你可以结合管道命令使用它来重定向任何命令的输出：

```bash
$ date | tee testfile
Sun Oct 17 18:56:21 EDT 2010
$ cat testfile
Sun Oct 17 18:56:21 EDT 2010
$
```

输出会出现在`STDOUT`中，并写入指定的文件中。请注意：默认情况下，`tee`命令在每次使用时都会覆盖输出文件：

```bash
$ who | tee testfile
rich      pts/0      2010-10-17 18:41 (192.168.1.2)
$ cat testfile
rich      pts/0      2010-10-17 18:41 (192.168.1.2)
$
```

如果你想向文件中追加数据，必须使用`-a`选项：

```bash
$ date | tee -a testfile
Sun Oct 17 18:58:05 EDT 2010
$ cat testfile
```

系统和应用程序可以生成超过30个Linux信号。[表15.1]列出了你在Linux编程中会遇到的最常见的Linux系统信号。

### Linux信号

| 信号 | 值 | 描述 |
| :--- | :--- | :--- |
| `1` | `SIGHUP` | 挂起进程。 |
| `2` | `SIGINT` | 中断进程。 |
| `3` | `SIGQUIT` | 停止进程。 |
| `9` | `SIGKILL` | 无条件终止进程。 |
| `15` | `SIGTERM` | 在可能的情况下终止进程。 |
| `17` | `SIGSTOP` | 无条件停止但不终止进程。 |
| `18` | `SIGTSTP` | 停止或暂停进程，但不终止。 |
| `19` | `SIGCONT` | 继续运行已停止的进程。 |

默认情况下，`bash` shell会忽略其收到的任何`SIGQUIT (3)`和`SIGTERM (15)`信号（这样做是为了防止交互式shell不被意外终止）。然而，`bash` shell会处理其收到的任何`SIGHUP (1)`和`SIGINT (2)`信号。

如果`bash` shell接收到`SIGHUP`信号，将会退出。但在退出之前，它会将`SIGHUP`信号传递给shell启动的任何进程（例如你的shell脚本）。对于`SIGINT`信号，shell只会被中断。Linux内核会停止为shell提供CPU处理时间。当这种情况发生时，shell会将`SIGINT`信号传递给shell启动的任何进程以通知它们该情况。

shell将这些信号传递给你的shell脚本程序进行处理。然而，shell脚本的默认行为是忽略信号，这会对脚本的运行产生不利影响。为了避免这种情况，你可以编写脚本来识别信号并执行命令，为脚本应对信号带来的后果做好准备。

#### 生成信号

`bash` shell允许你使用键盘上的键组合生成两个基本的Linux信号。如果你需要停止或暂停运行异常的程序，此功能将非常有用。

#### 中断进程

`Ctrl+C`键组合会生成`SIGINT`信号，并将其发送到shell中当前运行的任何进程。你可以通过运行一个需要很长时间才能完成的命令并按下`Ctrl+C`键组合来测试这一点：

```
$ sleep 100
^C
$
```

`Ctrl+C`键组合仅仅是停止shell中运行的当前进程。`sleep`命令暂停操作指定的秒数。通常，在计时器过期之前命令提示符不会返回。通过在计时器过期前按下`Ctrl+C`键组合，你可以导致`sleep`命令提前终止。

#### 暂停进程

与其终止进程，你可以在它正在执行任何操作的中间将其暂停。有时这可能是危险的（例如，如果脚本对关键系统文件打开了文件锁），但通常它允许你在不实际终止进程的情况下查看脚本正在执行的内容。

`Ctrl+Z`键组合会生成`SIGTSTP`信号，停止shell中运行的任何进程。停止进程与终止进程不同，因为停止进程会让程序仍然留在内存中，并能够从停止的地方继续运行。在稍后的“作业控制”部分中，你将学习如何重启一个已停止的进程。

当你使用`Ctrl+Z`键组合时，shell会通知你进程已停止：

```
$ sleep 100
^Z
[1]+ Stopped             sleep 100
$
```

方括号中的数字是shell分配的作业号。shell将shell中运行的每个进程称为作业，并为每个作业分配一个唯一的作业号。它为第一个启动的进程分配作业号1，第二个作业分配作业号2，依此类推。

如果你在shell会话中有一个已停止的作业，当你尝试退出shell时，`bash`会警告你：

```
$ exit
logout
There are stopped jobs.
$
```

你可以使用`ps`命令查看停止的作业：

```
$ ps au
USER PID    %CPU  %MEM   VSZ  RSS TTY     STAT  START    TIME COMMAND
rich 20560  0.0  1.2  2688  1624 pts/0   S     05:15   0:00 -bash
rich 20605  0.2  0.4  1564   552 pts/0   T     05:22   0:00 sleep 100
rich 20606  0.0  0.5  2584  740 pts/0   R     05:22   0:00 ps au
$
```

在`STAT`列中，`ps`命令将停止作业的状态显示为`T`。这表示该命令正在被追踪或已停止。

如果你真的想在停止的作业仍然活动的情况下退出shell，只需再次输入`exit`命令。shell将退出，并终止停止的作业。或者，既然你已经知道了停止作业的`PID`，你可以使用`kill`命令发送`SIGKILL`信号来终止它：

```
$ kill -9 20605
$
[1]+ Killed             sleep 100
```

```bash
$ ./test2
Loop #1
Loop #2
^Cbyebye
$
```

当使用`Ctrl+C`键组合发送`SIGINT`信号时，脚本将会退出（因为该信号未列在trap陷列表中），但在脚本退出之前，shell会执行`trap`命令。

## 移除陷(Trap)

你可以使用破折号`-`作为命令来移除一组trap，并列出你想要恢复正常行为的信号列表：

```bash
$ cat test3
#!/bin/bash
# 移除已设置的trap
trap "echo byebye" EXIT
count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 3
    count=$[ $ count + 1 ]
done
trap - EXIT
echo "I just removed the trap"
$
$ ./test3
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
I just removed the trap
$
```

一旦信号trap被移除，脚本将忽略这些信号。然而，如果在移除trap之前接收到信号，脚本将按照`trap`命令对其进行处理：

```bash
$ ./test3
Loop #1
Loop #2
^Cbyebye
$
```

在示例中，使用了`Ctrl+C`键组合提前终止了脚本。因为脚本在移除trap之前就被终止了，所以脚本执行了trap中指定的命令。

## 在后台模式下运行脚本

有时，直接从命令行界面运行shell脚本是不方便的。某些脚本可能需要很长时间来处理，你可能不希望一直占用命令行界面等待。在脚本运行期间，你无法在终端会话中进行任何其他操作。幸运的是，这个问题有一个简单的解决方法。

当你使用`ps`命令时，你会看到Linux系统上运行着许多不同的进程。显然，并不是所有的进程都运行在你的终端显示器上。这被称为后台运行进程。在后台模式下，进程的运行不会关联终端会话的`STDIN`、`STDOUT`和`STDERR`（见第14章）。

你也可以在shell脚本中利用这一特性，让它们在后台运行而不会锁定终端会话。接下来的章节描述了如何在你的Linux系统上以后台模式运行脚本。

### 在后台运行

在后台模式下运行shell脚本是一件很容易的事。要在命令行界面以后台模式运行shell脚本，只需在命令后放置一个安符符号`&`：

```bash
$ ./test1 &
[1] 1976
$ This is a test program
Loop #1
Loop #2
ls /home/user/Desktop
gnome-screenshot.desktop konsole.desktop     virtualbox.desktop
gnome-terminal.desktop     ksnapshot.desktop
$ Loop #3
Loop #4
...
$
```

当你在命令后放置安符符号时，它会将命令与bash shell隔离开，并作为系统上一个独立的后台进程运行。首先显示的行是：

`[1] 1976`

方括号中的数字是shell分配给后台进程的作业号。下一个数字是Linux系统分配给进程的进程ID（`PID`）。Linux系统上运行的每个进程都必须有一个唯一的`PID`。

一旦系统显示了这些项目，一个新的命令行界面提示符就会出现。你返回到了shell，而你执行的命令在后台模式下安全运行。

此时，你可以在提示符处输入新命令（如示例所示）。然而，当后台进程仍在运行时，它仍然使用你的终端显示器作为`STDOUT`和`STDERR`消息输出。你会从示例中发现`test1`脚本的输出与从shell运行的任何其他命令输出交替出现。

当后台进程完成时，它会在终端上显示一条消息：

```bash
[1]+ Done             ./test1
```

这显示了作业号和作业状态（`Done`），以及启动该作业时使用的命令。

### 运行多个后台作业

你可以从命令行提示符同时启动任意数量的后台作业：

```bash
$
$ ./test1 &
[3] 2174
$ This is Test Program 1
$ ./test2 &
[4] 2176
$ I am Test Program 2
$ ./test3 &
[5] 2178
$ Well this is Test Program
$ ./test4 &
[6] 2180
$ This is Test Program 4
$
```

每当你启动一个新作业时，Linux系统都会为其分配一个新的作业号和`PID`。你可以通过`ps`命令看到所有脚本都在运行：

```bash
$ ps au
USER      PID %CPU %MEM    VSZ  RSS TTY  STAT START TIME COMMAND
...
user      1826  0.0  0.3    6704  3408 pts/0  Ss    14:07 0:00 bash
```



`user 2174 0.0 0.1 4860 1076 pts/0 S 15:23 0:00 /bin/bash ./test1`

`user 2175 0.0 0.0 3884 504 pts/0 S 15:23 0:00 /bin/bash ./test2`

`user 2176 0.0 0.1 4860 1078 pts/0 S 15:23 0:00 sleep 300`

`user 2177 0.0 0.0 3884 504 pts/0 S 15:23 0:00 /bin/bash ./test3`

`user 2178 0.0 0.0 3884 504 pts/0 S 15:23 0:00 /bin/bash ./test4`

`user 2179 0.0 0.0 3884 504 pts/0 S 15:23 0:00 sleep 300`

`user 2180 0.0 0.0 3884 504 pts/0 S 15:23 0:00 sleep 300`

`user 2181 0.0 0.0 3884 504 pts/0 S 15:23 0:00 sleep 300`

### 退出终端

使用后台进程时必须小心。如果终端退出，后台进程也会退出。你还有其他需要做的事。

### 无控制台运行脚本

有时你可能想从终端启动 shell 脚本并让它在后台运行直到完成，即使你注销。你可以通过使用`nohup`命令来实现。

`nohup`命令运行命令并阻塞任何`SIGHUP`信号。这防止了进程在你退出终端时终止。

`nohup`命令的格式如下：

```bash
$ nohup ./test1 &
[1] 1831
$ nohup: ignoring input and appending output to ‘nohup.out’
$
```

和普通后台进程一样，shell 为命令分配作业号和`PID`。区别在于当你使用`nohup`命令时，脚本会忽略由终端会话发送的`SIGHUP`信号。

由于`nohup`命令将进程与终端分离，进程失去了`STDOUT`和`STDERR`输出链接。为了适应命令生成的任何输出，`nohup`命令会自动将`STDOUT`和`STDERR`重定向到名为`nohup.out`的文件中。`nohup.out`文件包含了通常发送到终端显示器的所有输出。在进程完成后，你可以查看`nohup.out`文件的结果：

```bash
$ cat nohup.out
This is a test program
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Loop #6
Loop #7
Loop #8
Loop #9
Loop #10
This is the end of the test program
$
```

输出出现在`nohup.out`文件中，就像该进程在命令行运行一样！

> 如果你使用`nohup`运行另一个命令，输出将追加到现有的`nohup.out`文件中。在同一目录下运行多个命令时要小心，因为所有输出都将发送到同一个`nohup.out`文件，这可能会导致混乱。

## 任务控制

在本章的前面的部分，你已经学习了如何使用组合键来停止 shell 中运行的任务。停止任务后，Linux 系统允许你杀死它或重启它。你可以使用`kill`命令来杀死进程。重启已停止的进程则需要向它发送一个`SIGCONT`信号。

启动、停止、杀死和恢复任务的功能被称为任务控制（job control）。通过任务控制，你可以完全控制进程在 shell 环境中的运行方式。

本节描述了用于查看和控制 shell 中运行任务的命令。

## 查看任务

任务控制的关键命令是`jobs`命令。`jobs`命令允许你查看 shell 正在处理的当前任务：

```bash
$ cat test4
#!/bin/bash
# testing job control
echo “This is a test program $$”
count=1
while [ $count -le 10 ]
do
    echo “Loop #$count”
    sleep 10
    count=$[ $ count + 1 ]
done
echo “This is the end of the test program”
$ 
$ ./test4
This is a test program 29011
Loop #1
^Z
[1]+ Stopped              ./test4
$ 
$ ./test4 > test4out &
[2] 28861
$
$ jobs
[1]+ Stopped              ./test4
[2]- Running             ./test4 >test4out &
$
```

脚本使用`$$`变量来显示 Linux 系统分配给脚本的 PID（进程 ID）；然后它进入一个循环，每次迭代睡眠 10 秒。在示例中，第一个脚本从命令行界面启动，然后使用`Ctrl+Z`组合键停止。接着，使用`&`符号作为后台进程启动了另一个任务。为了方便起，该脚本的输出被重定向到一个文件中，这样它就不会显示在屏幕上。

在启动这两个任务后，我们使用`jobs`命令查看分配给 shell 的任务。`jobs`命令会显示已停止和正在运行的任务，以及它们的任务号和任务中使用的命令。

`jobs`命令使用了几个不同的命令行参数，如表 15.2 所示。

### 表 15.2 jobs 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `-l` | 列出进程的 PID 及其任务号。 |
| `-n` | 列出自上次 shell 通知以来状态发生变化的任务。 |
| `-p` | 仅列出任务的 PID。 |
| `-r` | 仅列出运行的任务。 |
| `-s` | 仅列出停止的任务。 |

你可能注意`jobs`命令输出中的加号 (+) 和减号 (-)。带有加号的任务被视为默认任务。如果命令行中中没有指定任务号，那么任何任务控制命令都会引用该带加号的任务。带有减号的任务将在当前默认任务处理完毕后成为默认任务。无论 shell 中运行了多少个任务，任何时候都只有一个带加号的任务和一个带减号的任务。

以下是一个示例，展示了当默认任务被移除时，队列中的下一个任务如何接管默认状态：

```bash
$ ./test4
This is a test program 29075
Loop #1
^Z
[1]+ Stopped              ./test4
$ 
$ ./test4
This is a test program 29090
Loop #1
^Z
[2]+ Stopped              ./test4
$ 
$ ./test4
This is a test program 29105
Loop #1
^Z
[3]+ Stopped              ./test4
$ 
$ jobs -l
[1] 29075 Stopped              ./test4
[2]- 29090 Stopped              ./test4
[3]+ 29105 Stopped              ./test4
$ 
$ kill -9 29105
$ 
$ jobs -l
[1]- 29075 Stopped              ./test4
[2]+ 29090 Stopped              ./test4
$
```

在这个示例中，启动了三个独立的进程并停止了它们。`jobs`命令列表显示了这三个进程及其状态。注意，默认进程（带有加号的那个）是最后启动的。随后执行了`kill`命令来停止默认进程。在下一次`jobs`列表中，带有减号的任务变成了默认任务。

## 重启已停止的任务

在任务控制下，你可以将任何停止的任务作为后台进程或前台进程重启。前台进程会占用终端，因此请注意。要在后台模式下重启任务，请使用`bg`命令配合任务号：

```bash
$ bg 2
[2]+ Running ./test4 > test4out &
$ jobs
[1]+ Stopped              ./test4
[2]- Running             ./test4 >test4out &
```

要在前台模式下重启任务，请使用`fg`命令：

```bash
$ fg 1
[1]+ ./test4
```

## nice 命令

`nice`命令允许你在启动命令时设置调度优先级。要让命令以较低优先级运行，请使用`nice`的`-n`选项指定一个新的优先级级别：

```bash
$ nice -n 10 ./test4 > test4out &
[1] 29476
$ ps al
  F  UID  PID  PPID  PRI  NI  CHAN  STAT TTY          TIME COMMAND
100  501  29459  29458  12    0  wait4  S   pts/0          0:00 -bash
000  501  29476  29459  15   10  wait4  SN   pts/0          0:00 /bin/bash 
000  501  29490  29476  15   10  nanosl SN   pts/0          0:00 sleep 10
000  501  29491  29459  14    0  -      R   pts/0          0:00 ps al
$
```

`nice`命令会导致脚本以较低的优先级运行。然而，如果你尝试增加其中一个命令的优先级，可能会大吃：

```bash
$ nice -n -10 ./test4 > test4out &
[1] 29501
$ nice: cannot set priority: Permission denied
```

```bash
[1]+ Exit 1 nice -n -10 ./test4 >test4out
$
```

`nice`命令防止普通系统用户提高其命令的优先级。这是一项安全功能，防止用户将其所有命令都以高优先级启动。

## renice 命令

有时你可能想要更改系统中已经在运行命令命令优先级。这正是`renice`命令的作用。它允许你指定正在运行进程的`PID`来更改其优先级：

```bash
$ ./test4 > test4out &
[1] 29504
$ ps al
  F    UID    PID  PPID  PRI  NI WCHAN  STAT TTY          TIME COMMAND
100   501 29459  29458   12    0  wait4   S    pts/0      0:00  -bash
000   501 29504  29459    9    0  wait4   S    pts/0      0:00  /bin/bash .
000   501 29518  29504    9    0  nanosl  S    pts/0      0:00  sleep 10
000   501 29519  29459   14    0  -       R    pts/0      0:00  ps al
$ renice 10 -p 29504
29504: old priority 0, new priority 10
$ ps al
  F    UID    PID  PPID  PRI  NI WCHAN  STAT TTY          TIME COMMAND
100   501 29459  29458   16    0  wait4   S    pts/0      0:00  -bash
000   501 29504  29459   14   10  wait4   SN    pts/0      0:00  /bin/bash .
000   501 29535  29504    9    0  nanosl  S    pts/0      0:00  sleep 10
000   501 29537  29459   14    0  -       R    pts/0      0:00  ps al
$
```

`renice`命令会自动更新运行中进程的调度优先级。与`nice`命令一样，`renice`命令也有一些局限性：

* 你只能对你拥有的进程进行`renice`。
* 你只能将进程`renice`为较低的优先级。
* root 用户可以将任何进程`renice`为任何优先级。

如果你想完全控制运行运行的进程，你必须以`root`账户登录或使用`sudo`命令。

## 像时钟一样运行

我确信，当你开始编写脚本时，会遇到这样一种情况：你希望在预设时间运行脚本，通常是在你不在场的时候。Linux 系统提供了几种在预选时间运行脚本的方法：`at`命令和`cron`表。每种方法都使用不同的技术来调度运行脚本的时间和频率。接下来的章节将描述这些每种方法。

### 使用 at 命令调度作业

`at`命令允许你指定 Linux 系统运行脚本的时间。`at`命令将作业提交到队列中，并带有 shell 何时运行该作业的指示。`at`守护进程`atd`在后台运行并检查作业队列是否有待运行的作业。大多数 Linux 发行版在启动时会自动启动此守护进程。

`atd`守护进程检查系统上的特殊目录（通常为`/var/spool/at`）是否有使用`at`命令提交的作业。默认情况下，`atd`进程每 60 秒检查一次该目录。当存在作业时，`atd`会检查作业设置的运行时间。如果时间与当前时间匹配，`atd`将运行该作业。

接下来的章节将描述如何使用`at`命令提交作业运行以及如何管理作业。

### at 命令格式

基本的`at`命令格式非常简单：

`at [-f <filename>] time`

默认情况下，`at`命令将输入从`STDIN`提交到队列。你可以使用`-f`参数指定读取命令的文件（你的脚本文件）。

时间参数指定了你希望 Linux 系统何时运行作业。在指定时间方面你可以非常有创意。`at`命令识别许多不同的时间格式：

* 标准的小时和分钟，例如 10:15
* ~A.M./~PM 指示，例如 10:15P.M.
* 特定的具名时间，如 now, noon, midnight, 或 teatime (4P.M.)

如果你指定了一个已经过去的时间，`at`命令将在次日的该时间运行作业。

除了指定运行作业的时间外，你还可以包含特定的日期，使用几种不同的日期格式：

* 标准的日期格式，例如 MMDDYY，`MM/DD/YY`
* 文本日期，例如 Jul 4 或 Dec 25，包含或不包含年份
* 你还可以指定一个时间增量：
    * Now + 25 minutes
    * 10:15 + 7 days

当你使用`at`命令时，作业会被提交到队列中。作业队列持有由`at`提交待处理的作业。共有 26 个不同的队列可用。作业队列使用小字母`a`到`z`进行引用。几年前，`batch`命令是另一种允许脚本在以后运行的方法。`batch`命令的独特之处在于，你可以调度脚本在系统负载较低时运行。如今，`batch`命令简单来说就是`/usr/bin/batch`，它调用`at`并将作业提交到`b`队列。`b`队列的优先级较低（`nice`值较高）。如果你想以更高的优先级运行作业，可以使用`-q`指定不同的队列。

### 获取输出

当`at`作业运行时，没有显示器与其一同运行。相反，Linux 系统使用提交作业的用户的电子邮件地址。任何到`STDOUT`或`STDERR`的输出都会发送给该用户。这里有一个使用`at`命令调度作业的简单示例：

```bash
$ cat <<EOF | at 10:15 PM
#!/bin/bash
echo "This is a test job"
EOF
job 1 scheduled for Thu Oct 26 22:15:00 2023
```

当作业完成时，系统会生成电子邮件。如果脚本没有产生任何输出，则不生成电子邮件。

### 列出等待作业

`atq`命令允许你查看系统中等待处理的作业：

```bash
$ atq
61  Mon Oct 26 15:20:00 2023 a
58  Mon Oct 26 15:05:00 2023 a
59  Mon Oct 26 15:10:00 2023 a
60  Mon Oct 26 15:15:00 2023 a
```

`atq`列表显示作业编号、系统运行作业的日期和时间以及作业所在的队列。

### 删除作业

要删除作业，使用`atrm`命令后接作业编号：

```bash
$ atrm 61
```

一旦你知道了任务队列中哪些待执行任务的信息，就可以使用`atrm`命令来删除待执行任务：

```bash
$
$ atq
59      Mon Oct 18 15:10:00 2010 a user
60      Mon Oct 18 15:15:00 2010 a user
$
$ atrm 59
$
$ atq
60      Mon Oct 18 15:15:00 2010 a user
$
```



只需指定你想要删除的任务编号即可。你只能删除由自己提交执行的任务，而无法删除他人提交的任务。

# 调度常规脚本

使用`at`命令调度脚本在预设时间运行是非常棒的，但如果你需要该脚本每天运行、每周一次或每月运行一次怎么办？与其不断地提交`at`任务，你可以使用 Linux 系统的另一个功能。

Linux 系统使用`cron`程序来允许你调度需要定期运行的任务。`cron`程序在后台运行，并检查特殊的表（称为 cron 表），以查找计划运行的任务。

## cron 表

`cron`表使用特殊的格式来允许你指定任务应何时运行。`cron`表的格式为：

`min hour dayofmonth month dayofweek command`

`cron`表允许你将条目指定为特定值、范围（例如 1–5）或通配符（星号 *）。例如，如果你想在每天的 10:15 运行命令，你会使用`cron`表条目：

`15 10 * * * command`

在`dayofmonth`、`month`和`dayofweek`字段使用的通配符表示`cron`将在每月的每天 10:15 执行该命令。要指定在每周一的下午 4:15 运行命令，你将使用以下命令：

`15 16 * * 1 command`

你可以将`dayofweek`条目指定为三字符文本值（mon, tue, wed, thu, fri, sat, sun）或数值，其中 0 代表星期日，6 代表星期六。

这是另一个例子：要在每月第一天的中午 12 点执行命令，你将使用以下格式：

`00 12 1 * * command`

`dayofmonth`条目指定该月的日期值（1–31）。

> 注意
> 敏锐的读者可能会想，你如何能够设置命令在每月的最后一天执行，因为你无法将`dayofmonth`值覆盖所有月份。这个问题一直困扰着 Linux 和 Unix 程序员，并产生了许多不同的解决方案。一种常见的方法是添加一个`if-then`语句，使用`date`命令检查明天日期是否为 01：
> `00 12 * * * if [‘date +d -d tomorrow' = 01 ] ; then ; command`
> 这将在每天中午 12 点检查是否是月的最后一天，如果是，`cron`将运行命令。

命令列表必须指定运行的命令或 shell 脚本的完整路径。你可以像普通命令行一样添加任何喜欢的命令行参数或重定向符号：

`15 10 * * * /home/rich/test4 > test4out`

`cron`程序使用提交任务的用户账户运行脚本。因此，你必须拥有相应的权限来访问命令列表中指定的命令和输出文件。

## 构建 cron 表

每个系统用户（包括 root 用户）都可以拥有自己的`cron`表来运行调度任务。Linux 提供了`crontab`命令来处理`cron`表。要列出现有`cron`表，使用`-l`参数：

```bash
$ crontab -l
no crontab for rich
$
```

默认情况下，每个用户的`cron`表文件不存在。要向你的`cron`表添加条目，请使用`-e`参数。当你这样做时，`crontab`命令会启动文本编辑器（见第 9 章）并打开现有的`cron`表（如果不存在则打开空文件）。

## cron 目录

当你创建一个对执行时间要求不精确的脚本时，使用一个预配置的`cron`脚本目录更容易。有四个基本目录：每（hourly）、每日（daily）、每月（monthly）和每周（weekly）。

```bash
$
$ ls /etc/cron.*ly
/etc/cron.daily:
anacron      aptitude          exim4-base           man-db           sysstat
apt          bsdmainutils      logrotate           popularity-contest
apport                dpkg  mlocate    standard 

/etc/cron.hourly:
/etc/cron.monthly:
anacron
/etc/cron.weekly:
anacron  apt-xapian-index  man-db
$
```

因此，如果你有一个需要每天运行一次的脚本，只需将其复制到 daily 目录，`cron`每天都会执行它。

## anacron 程序

`cron`程序唯一的问题是假设你的 Linux 系统是 24 小时、7 天运行的。除非你在服务器环境中运行 Linux，否则这并不一定。

如果 Linux 系统在`crontab`计划运行任务时处于状态，则任务将不会运行。`cron`程序不会在系统重启后追溯运行错过的任务。为了解决这个问题，许多 Linux 发行版还包含了`anacron`程序。

如果`anacron`确定某个任务错过了计划运行时间，它将尽快运行该任务。这意味着如果你的 Linux 系统关闭了几天，当它重新启动时，任何在关机期间计划运行的任务都会执行。

这一功能通常用于执行例行维护的脚本。如果脚本在应该运行时系统总是关闭的，日志文件将永远不会修剪并可能会增长到不可接受的大小。有了`anacron`，你可以确保日志文件每次系统启动都会修剪。

`anacron`程序使用时间戳来确定任务是否已运行。每个`cron`目录都有一个时间戳文件，位于`/var/spool/anacron`：

```bash
$
$ sudo cat /var/spool/anacron.monthly
20101123
$
```

`anacron`程序了自己的表（通常位于`/etc/anacab`）来检查任务目录：

```bash
$
$ cat /etc/anacab
# /etc/anacab: configuration file for anacron
# See anacron(8) and anacab(5) for details.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# These 替换 cron 的条目
1 5 cron.daily nice run-parts --report /etc/cron.daily
7 10 cron.weekly nice run-parts --report /etc/cron.weekly
@monthly 15 cron.monthly nice run-parts --report /etc/cron.monthly
```

`anacron`表的基本格式与`cron`表略有不同：

> period delay identifier command

`period`条目定义了任务运行的频率，以天为单位。`anacron`程序使用此条目检查任务的时间戳文件。`delay`条目指定了系统启动后多少分钟内`anacron`程序应运行错过的脚本。`command`条目包含`run-parts`程序和一个`cron`脚本目录名。`identifier`条目是一个唯一的非空字符字符串——例如，`cron-weekly`。它用于在日志消息和错误电子邮件中唯一标识该任务。

注意，`anacron`不运行位于`/etc/cron.hourly`中的脚本。这是因为`anacron`程序不处理执行时间要求少于日的脚本。

启动 shell 脚本的最后一种方法是让你的脚本在 Linux 系统启动时或每当用户启动新的 bash shell 会话时自动运行。在启动时启动脚本通常预留给执行系统功能的特殊脚本，例如配置网络接口或启动服务器进程。然而，如果你是一个 Linux 系统管理员，你可能需要在每次 Linux 系统启动时执行某项功能，例如重置自定义日志文件或启动自定义应用程序。

在每当用户启动新的 bash shell 时运行脚本的能力（即使只是在当特定用户启动 bash shell 时）也可能非常有用。在某些情况下，你可能想要为某个 shell 会话设置 shell 特性，或者只需确保某个文件已设置完毕。

本节介绍了如何配置你的 Linux 系统，以便在系统启动时或每次启动新 bash shell 时运行你的脚本。

# 在系统启动时启动你的脚本

在让你的 shell 脚本在启动时运行之前，你需要稍微了解 Linux 启动过程的工作原理。Linux 使用特定的顺序来在启动时启动脚本，了解这一过程可以帮助你的脚本以你预想要的方式运行。

## 启动过程

当你开启 Linux 系统后，Linux 内核会加载到内存并运行。它做的第一件事是启动 UNIX System V init 进程或 Upstart init 进程，具体取决于你的发行版及其版本。该进程随后负责启动 Linux 系统上的所有其他进程。

### System V init 进程

作为启动过程的一部分，System V init 进程会读取`/etc/inittab`文件。`inittab`文件列出了系统的运行级别（run level）。不同的 Linux 运行级别会启动不同的程序和脚本。[表 15.3] 列出了基于 Red Hat 的发行版的 Linux 运行级别。

[表 15.3] Linux 运行级别——基于 Red Hat 的发行版

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 停机 (Halt) |
| 1 | 单用户模式 |
| 2 | 多用户模式，通常不支持网络 |
| 3 | 全多用户模式，带网络 |
| 4 | 用户定义 |
| 5 | 多用户模式，带网络和图形 X Window 会话 |
| 6 | 重启 (Reboot) |

Linux 发行版通常使用[表 15.3]中列出的运行级别来对系统上启动的服务进行更细粒度的控制。然而，基于 Debian 的发行版（如 Ubuntu 和 Linux Mint）并不区分运行级别 2 到 5 的差异，如[表 15.4]所示。

[表 15.4] Linux 运行级别——基于 Debian 的发行版

| 运行级别 | 描述 |
| :--- | :--- |
| 0 | 停机 (Halt) |
| 1 | 单用户模式 |
| 2 - 5 | 多用户模式，带网络和图形 X Window 会话 |
| 6 | 重启 (Reboot) |

Ubuntu 发行版甚至没有用于设置运行级别的`/etc/inittab`文件。默认情况下，Ubuntu 进入运行级别 2。如果你想更改默认运行级别，则必须在 Ubuntu 发行版上创建一个`/etc/inittab`文件。

每个运行级别都定义了 System V init 进程启动或停止哪些脚本。这些启动脚本是 shell 脚本用于启动应用程序并为它们的运行提供必要的环境变量。

在基于 System V init 的启动过程中，情况开始变得有些模糊，主要是因为不同的 Linux 发行版将启动脚本放在略有不同的位置。有些发行版将启动脚本放在`/etc/rc#.d`目录，其中 # 代表运行级别。另一些使用`/etc/init.d`目录，还有的使用`/etc/init.d/rc.d`目录。通常，快速查看你的`/etc`目录结构就可以很容易判断你的发行版使用什么格式。

### Upstart init 进程

Upstart init 进程是管理服务进程的新兴标准，许多 Linux 发行版现在正转向它。Upstart 并不关注系统运行级别，而是关注事件，例如系统启动。在 Upstart 中，系统启动被称为启动事件。

根据你的发行版及其版本，Upstart 使用位于`/etc/event.d`或`/etc/init`目录下的文件来启动进程。为了保持后兼容性，许多 Upstart 实现仍然调用来自`/etc/init.d`和/或`/etc/rc#.d`的旧 System V init 脚本。

目前 Upstart init 进程标准仍在高度进化中。对于你创建并希望在系统启动事件期间启动的脚本，使用旧的 System V init 进程方法是稳妥的。这种方法将在下一节中描述。

## 定义你的脚本

最好不要修改 Linux 发行版中单个启动脚本文件。发行版通常提供工具在你添加服务器应用程序时自动构建这些脚本，手动更改这些脚本可能会导致问题。

相反，大多数 Linux 发行版提供了一个本地启动文件，专门允许系统管理员输入在启动时运行的脚本。当然，该文件的名称和位置在不同的 Linux 发行版中不同。[表 15.5]标识了五种流行的 Linux 发行版启动文件的位置。

[表 15.5] Linux 本地启动文件位置

| 发行版 | 文件位置 |
| :--- | :--- |
| debian | `/etc/init.d/rc.local` |
| Fedora | `/etc/rc.d/rc.local` |
| Mandriva | `/etc/rc.local` |
| openSuse | `/etc/init.d/boot.local` |
| Ubuntu | `/etc/rc.local` |

在本地启动文件中，你可以指定特定的命令和语句，也可以输入任何你想启动时运行的脚本。记住，如果你使用脚本，需要指定脚本的完整路径，以便系统在启动时能找到它。

> 注意
> 不同的 Linux 发行版在启动过程中的不同点执行本地启动脚本。有时脚本会在网络支持等功能启动之前运行。请查阅你特定的 Linux 发行版文档，以确定本地启动脚本在你的发行版何时运行。

## 使用新 Shell 启动

每个用户的家目录都包含两个 bash shell 用于自动启动脚本和设置环境变量的文件：

* `.bash_profile` 文件
* `.bashrc` 文件

当由于新登录导致运行新 shell 时，bash shell 会运行`.bash_profile`文件。将任何你想在登录时运行的脚本放在此文件中。

bash shell 在每次启动新 shell 时都会运行`.bashrc`文件。你可以通过在家目录下的`.bashrc`文件中添加一个简单的`echo`语句然后启动新 shell 来测试这一点：

```bash
$ bash
This is a new shell!!
$
```



对于系统上的每个用户，大多数 Linux 发行版都提供了 `/etc/bashrc` 文件（注意 `bashrc` 文件名前面没有点）。当系统上的任何用户启动新的 bash shell 时，bash shell 都会执行该文件中的语句。

## 总结

Linux 系统允许你通过信号来控制你的 shell 脚本。bash shell 接受信号并传递给在 shell 进程下的任何进程。Linux 信号允许你轻松杀死异常进程或临时暂停长时间运行的进程。

你可以在脚本中使用 `trap` 语句来捕获信号并执行命令。此功能提供了一种简单的方法，来控制用户是否可以在你的脚本运行时中断它。

默认情况下，当你在终端会话 shell 中运行脚本时，交互式 shell 会挂起，直到脚本执行完成。你可以在命令名后添加一个符号（`&`）来使脚本或命令在后台模式运行。当你以后台模式运行脚本或命令时，交互式 shell 会返回，允许你继续输入更多命令。使用这种方法运行的任何后台进程仍然与终端会话绑定。如果你退出终端会话，后台进程也会退出。

为了防止这种情况的发生，请使用 `nohup` 命令。该命令会拦截任何发送给命令并旨在停止其运行的信号——例如当你退出终端会话时。这使得脚本即使在你退出终端会话后也能继续在后台运行。

当你将进程移动到后台模式时，你仍然可以控制它的发生情况。`jobs` 命令允许你查看从 shell 会话启动的进程。一旦你知道了后台进程的任务 ID（job ID），可以使用 `kill` 命令向进程发送 Linux 信号，或使用 `fg` 命令将进程带回 shell 会话的前台。你可以通过使用 `Ctrl+Z` 键组合挂起正在运行的前台进程，然后使用 `bg` 命令将其放回后台模式。

`nice` 和 `renice` 命令允许你更改进程的优先级级别。通过赋予进程较低的优先级，你允许 CPU 为其分配较少的时间。这在运行可能消耗大量 CPU 时间的长进程时非常有用。

除了控制运行中的进程外，你还可以确定进程在系统上的启动时间。与其其直接从命令行界面提示符运行脚本，不如调度该进程在其他时间运行。有几种不同的方法可以实现这一点。`at` 命令允许你在预设时间运行一次脚本。`cron` 程序提供了一个可以按定期计划的时间间隔运行脚本的接口。

最后，Linux 系统提供了脚本文件供你调度脚本在系统启动时或每当用户启动新的 bash shell 时运行。不同的发行版有不同的文件，允许你列出每次系统启动时都启动的脚本。这允许系统管理员在启动时运行特殊的脚本进行系统维护。。同样地，`.bash_profile` 和 `.bashrc` 文件位于每个用户的家目录下，为放置随新 shell 运行的脚本和命令提供了位置。`.bash_profile` 文件在用户每次登录系统时运行脚本，而 `.bashrc` 文件在每个新的 shell 实例上运行脚本。

在下一章中，我们将查看如何编写脚本函数。脚本函数允许你编写一次代码块，然后在脚本的多个位置使用它们。

# 第三部分：高级 Shell 脚本

## 本部分

* 第 16 章：创建函数
* 第 17 章：为图形桌面编写脚本
* 第 18 章：引入 `sed` 和 `gawk`
* 第 19 章：正则表达式
* 第 20 章：高级 `sed`
* 第 21 章：高级 `gawk`
* 第 22 章：使用替代 Shell

# 第 16 章：创建函数

## 本章

* 基础脚本函数
* 返回值
* 在函数中使用变量
* 数组和变量函数
* 函数递归
* 创建库
* 在命令行上使用函数

在编写 shell 脚本时，你经常会发现自己在多个地方使用相同的代码。如果只是一个小代码段，通常不是什么问题。然而，在 shell 脚本中多次重写大段代码可能会很疲惫。bash shell 提供了一种支持用户定义函数的方法来提供帮助。你可以将你的 shell 脚本代码封装到一个函数中，然后在脚本的任何地方按需要多次使用它。本章将引导你完成创建自己的 shell 脚本函数的过程，并演示如何在 shell 脚本应用程序中使用它们。

## 基础脚本函数

当你开始编写更复杂的 shell 脚本时，你会发现自己在复用执行特定任务的代码部分。有时它是一些简单的内容，例如显示文本消息和从脚本用户处获取答案。其他时候，它是脚本中作为较大过程的一部分被多次使用的复杂计算。

在这些每种情况下，在脚本中反复编写相同的代码块都会变得很疲惫。如果只需要写一次该代码块，然后可以在脚本的任何地方引用该代码块而无需重写它，那就太好了。

bash shell 提供了一个允许你执行此操作的功能。函数是你为其分配了名称的脚本代码块，然后在代码的任何地方复用它。每当你需要在脚本中使用该代码块时，只需使用你分配给它的函数名（这称为调用函数）。本节描述了如何在 shell 脚本中创建和使用函数。

### 创建函数

在 bash shell 脚本中，可以使用两种格式来创建函数。第一种格式使用关键字 `function` 以及你分配给代码块的函数名：

```bash
function name {
  commands
}
```

`name` 属性定义了分配给函数的唯一名称。你在脚本中定义的每个函数都必须分配一个唯一的名称。

`commands` 是组成你函数的一个或多个 bash shell 命令。当你调用函数时，bash shell 会按照命令在函数中出现的顺序执行每条命令，就像在普通脚本中一样。

在 bash shell 脚本中定义函数的第二种格式更符合其他编程语言中函数的定义方式：

```bash
name() {
  commands
}
```

函数名后的空括号表示你正在定义一个函数。这种格式的命名规则与原始 shell 脚本函数格式相同。

### 使用函数

要在你的脚本中使用函数，请在一行中指定函数名，就像指定任何其他 shell 命令一样：

```bash
$ cat test1
#!/bin/bash

# 在脚本中使用函数
function func1 {
    echo "This is an example of a function"
}

count=1

while [ $count -le 5 ]
do
  func1
  count=$[ $count + 1 ]
done

echo "This is the end of the loop"

func1

echo "Now this is the end of the script"

$ 
$ ./test1
This is an example of a function
This is an example of a function
This is an example of a function
This is an example of a function
This is an example of a function
This is the end of the loop
This is an example of a function
Now this is the end of the script
$
```

每当你引用 `func1` 函数名时，bash shell 都会返回 `func1 function` 定义并执行你在那里定义的任何命令。

函数定义不必是 shell 脚本中的第一个内容，但要小心。如果你尝试在定义函数之前使用它，你将收到错误消息：

```bash
$ cat test2
#!/bin/bash

# 使用位于脚本中间的函数
count=1

echo "This line comes before the function definition"

function func1 {
    echo "This is an example of a function"
}

while [ $count -le 5 ]
do
  func1
  count=$[ $count + 1 ]
done

echo "This is the end of the loop"

func2

echo "Now this is the end of the script"

function func2 {
    echo "This is an example of a function"
}

$ 
$ ./test2
This line comes before the function definition
```

```bash
./test2: func2: command not found
Now this is the end of the script
$
```

第一个函数 `func1` 是在脚本中的几条语句之后定义的，这是完全没有问题的。当脚本中使用 `func1` 函数时，shell 知道去哪里找到它。

然而，脚本在定义 `func2` 函数之前就尝试使用它。由于 `func2` 函数没有被定义，当脚本运行到使用它的地方时，它产生了一条错误信息。

你还需要注意你的函数名称。记住，每个函数名称必须是唯一的，否则你就会遇到问题。如果你重新定义一个函数，新定义将覆盖原始函数定义，不会产生任何错误信息：

```bash
$ cat test3
#!/bin/bash

# testing using a duplicate function name
function func1 {
echo “This is the first definition of the function name”
}

func1

function func1 {
    echo “This is a repeat of the same function name”
}

func1

echo “This is the end of the script”

$ 
$ ./test3
This is the first definition of the function name
This is a repeat of the same function name
This is the end of the script
$
```

`func1` 函数的原始定义运行正常，但在第二次定义 `func1` 函数之后，任何后续对该函数的调用都将使用第二个定义。

## 返回值

`bash` shell 将函数视为微型脚本，拥有完整的退出状态（参见第 10 节）。你有三种不同的方法可以为你的函数生成退出状态。

### 默认退出状态

默认情况下，函数的退出状态是函数中最后一个命令返回的退出状态。在函数执行完毕后，你使用标准变量 `$?` 来确定函数的退出状态：

```bash
$ cat test4
#!/bin/bash

# testing the exit status of a function
func1() {
    echo “trying to display a non-existent file”
    ls -l badfile
}

echo “testing the function: ”

func1

echo “The exit status is: $?”

$ 
$ ./test4
testing the function:
trying to display a non-existent file
ls: badfile: No such file or directory
The exit status is: 1
$
```

函数的退出状态为 1，是因为函数中的最后一个命令执行失败了。然而，你无法知道函数中的其他任何命令是否成功完成。请看这个例子：

```bash
$ cat test4b
#!/bin/bash

# testing the exit status of a function
func1() {
    ls -l badfile
    echo “This was a test of a bad command”
}

echo “testing the function:”

func1

echo “The exit status is: $?”

$ 
$ ./test4b
testing the function:
ls: badfile: No such file or directory
This was a test of a bad command
The exit status is: 0
$
```

这一次，因为函数以一个成功执行的 `echo` 语句结束，所以函数的退出状态为 0，尽管函数中的一个命令失败了。使用函数的默认退出状态可能是一种危险的做法。幸运的是，我们还有其他几种解决方案。

### 使用 `return` 命令

`bash` shell 使用 `return` 命令以特定的退出状态退出函数。`return` 命令允许你指定一个单一整数值来定义函数的退出状态，这为你提供了一种以编程方式设置函数退出状态的方便方法：

```bash
$ cat test5
#!/bin/bash

# using the return command in a function
function dbl {
    read -p “Enter a value: ” value
    echo “doubling the value”
    return $[ $value * 2 ]
}

dbl

echo “The new value is $?”

$
```

`dbl` 函数将用户输入的 `$value` 变量中包含的值翻倍。然后它使用 `return` 命令返回结果，脚本通过 `$?` 变量显示该结果。

然而，当你使用这种技术从函数返回数值时必须小心。请记住以下两点以避免问题：

* 记住在函数完成后立即获取返回值。
* 记住退出状态必须在 0 到 255 的范围范围内。

如果你在通过 `$?` 变量获取函数返回值之前执行了任何其他命令，那么函数的返回值将会丢失。记住 `$?` 变量返回的是上一个执行的命令的退出状态。

第二个问题定义了使用此返回值技术的局限性。由于退出状态必须小于 256，因此你的函数结果必须产生一个小于 256 的整数值。任何大于该值的数都会返回错误值：

```bash
$ ./test5
Enter a value: 200
doubling the value
The new value is 1
$
```

如果你需要返回较大的整数值或字符串值，就无法使用这种返回值技术。相反，你需要使用下一节中演示另一种方法。

### 使用函数输出

就像你可以将命令的输出到 shell 变量一样，你也可以将函数的输出到 shell 变量。你可以使用这种技术返回任何类型的输出。以下是一个示例：

```bash
$ cat test5b
#!/bin/bash

# using the echo to return a value
function dbl {
    read -p “Enter a value: ” value
    echo “doubling the value”
    echo $[ $value * 2 ]
}

result=$(dbl)

echo “The new value is $result”

$ 
$ ./test5b
Enter a value: 100
doubling the value
The new value is 200
$
```

`dbl` 函数现在使用 `echo` 语句显示计算结果。脚本捕获的是 `dbl` 函数的输出，而不是查看退出状态。

这个例子展示了一个微妙的技巧。你会注意到 `dbl` 函数实际上输出了两条消息。`read` 命令输出了一条向用户查询数值的短消息。bash shell 脚本足够聪明，不会将其视为标准输出（STDOUT）的一部分，并忽略了它。如果你使用 `echo` 语句向用户产生这条查询消息，它也将连同输出一起被 shell 变量捕获。

> 注意：使用这种技术，你还可以返回浮点数和字符串值，这使其成为一种从函数返回数值的极其灵活的方法。

## 在函数中使用变量

你可能已经注意到上一节的 `test5` 示例中我们在函数内部使用了一个名为 `$value` 的变量来存储它处理的值。当你在函数中使用变量时，需要对定义和处理它们的方式有些小心。这是 shell 脚本中问题的常见原因。本节将介绍在 shell 脚本函数内部和外部处理变量的技巧。

### 向函数传递参数

正如我们早早在“返回值”一节中提到的，`bash` shell 将函数视为微型脚本。这意味着你可以像对待普通脚本一样向函数传递参数（参见第 13 节）。

函数可以使用标准的参数环境变量来表示从命令行传递给函数的任何参数。例如，函数的名称定义在 `$0` 变量中，而命令行上的任何参数使用 `$1`、`$2` 等变量定义。你还可以使用特殊变量 `$#` 来确定传递给函数的参数个数。

在脚本中指定函数时，你必须在与函数的同一行提供参数：

```bash
func1 $value1 10
```

该函数随后可以使用参数环境变量来检索参数值。这里有一个使用此方法向函数传递值的示例：

```bash
$ cat test6
#!/bin/bash

# passing parameters to a function
function addem {
    if [ $# -eq 0 ] || [ $# -gt 2 ]
    then
      echo -1
    elif [ $# -eq 1 ]
    then
      echo $[ $1 + $1 ]
    else
      echo $[ $1 + $2 ]
    fi
}

echo -n "Adding 10 and 15: "
value='addem 10 15'
echo $value

echo -n "Let's try adding just one number: "
value='addem 10'
echo $value

echo -n "Now trying adding no numbers: "
value='addem'
```



`echo $value`

`echo -n "Finally, try adding three numbers: "`

`value='addem 10 15 20'`

`echo $value`

`$`

`$ ./test6`

`Adding 10 and 15: 25`

`Let's try adding just one number: 20`

`Now trying adding no numbers: -1`

`Finally, try adding three numbers: -1`

`$`

```
`test6` 脚本中的 `addem` 函数首先检查脚本传递给它的参数数量。如果没有参数，或者参数数量超过两个，`addem` 将返回值 `-1`。如果只有一个参数，`addem` 将将该参数与其自身相加得到结果。如果有两个参数，`addem` 将将它们相加得到结果。
```

由于函数使用特殊的参数环境变量来获取其自身的参数值，因此它无法直接从脚本的命令行访问脚本参数值。下面的示例将会失败：

```bash
$ cat badtest1
#!/bin/bash
# trying to access script parameters inside a function
function badfunc1 {
    echo $[ $1 * $2 ]
}
if [ $# -eq 2 ]
then
    value='badfunc1'
    echo "The result is $value"
else
    echo "Usage: badtest1 a b"
fi
$ 
$ ./badtest1
Usage: badtest1 a b
$ ./badtest1 10 15
./badtest1: * : syntax error: operand expected (error token is "*")
The result is
$
```

尽管函数使用了 `$1` 和 `$2` 变量，但它们与脚本主部分可用的 `$1` 和 `$2` 变量不同。相反，如果你想在函数中使用这些值，你必须在调用函数时手动传递它们：

```bash
$ cat test7
#!/bin/bash
# trying to access script parameters inside a function
function func7 {
    echo $[ $1 * $2 ]
}
if [ $# -eq 2 ]
then
    value='func7 $1 $2'
    echo "The result is $value"
else
    echo "Usage: badtest1 a b"
fi
$ 
$ ./test7
Usage: badtest1 a b
$ ./test7 10 15
The result is 150
$
```

通过向函数传递 `$1` 和 `$2` 变量，它们就会变成可供函数使用的变量，就像任何其他参数一样。

# 在函数中处理变量

引起 shell 脚本程序员问题的问题之一是变量的作用域。作用域是变量可见的地方。在函数中定义的变量的作用域可能与普通变量不同。也就是说，它们可以对脚本的其他部分隐藏。

函数使用两种类型的变量：
* 全局
* 局域

接下来的章节描述了如何在函数中使用这两种类型的变量。

## 全局变量

全局变量是在 shell 脚本任何地方都有效的变量。如果你在脚本的主部分定义了一个全局变量，可以在函数内部检索它的值。同样地，如果你在函数内部定义了一个全局变量，可以在脚本的主部分检索它的值。

默认情况下，你在脚本中定义的任何变量都是全局变量。在函数外部定义的变量可以在函数内部正常访问：

```bash
$ cat test8
#!/bin/bash
# using a global variable to pass a value
function dbl {
    value=$[ $value * 2 ]
}
read -p "Enter a value: " value
dbl
echo "The new value is: $value"
$ 
$ ./test8
Enter a value: 450
The new value is: 900
$
```

`$value` 变量定义在函数外部。当调用 `dbl` 函数时，它的值在函数内部仍然有效。在函数内部为变量分配新值可能是一种危险的做法，特别是当你打算在不同的脚本中使用函数时。这要求你了解使用了哪些变量。这里有一个关于情况可能如何发展的示例：

```bash
$ cat badtest2
#!/bin/bash
# demonstrating a bad use of variables
function func1 {
    temp=$[ $value + 5 ]
    result=$[ $temp * 2 ]
}
temp=4
value=6
func1
echo "The result is $result"
if [ $temp -gt $value ]
then
    echo "larger"
else
    echo "smaller"
fi
$ 
$ ./badtest2
The result is 22
temp is larger
$
```

## 局域变量

与其使用全局变量，函数中使用的任何变量都可以声明为局域（local）。要做到这一点，可以在变量声明前使用 `local` 关键字。你也可以在赋值值时使用 `local`。`local` 关键字确保变量被限制在函数内部。这可以使你的变量与脚本分开。这里有一个示例：

```bash
$ cat test9
#!/bin/bash
# demonstrating the local keyword
function func1 {
    local temp
    temp=$[ $value + 5 ]
    result=$[ $temp * 2 ]
}
temp=4
value=6
func1
echo "The result is $result"
if [ $temp -gt $value ]
then
    echo "larger"
else
    echo "smaller"
fi
$ 
$ ./test9
The result is 22
temp is smaller
$
```

# 数组变量和函数

第 5 章讨论了使用数组允许单个变量持有多个值的高级方法。在函数中使用数组值有点复杂，并且有一些考虑事项。本节描述了一种可以实现该操作的技术。

## 向函数传递数组

将数组变量传递给脚本函数可能会令人困惑。如果你尝试将数组变量作为单个参数传递，它将不起作用：

```bash
$ cat badtest3
#!/bin/bash
# trying to pass an array variable
function testit {
    echo "The parameters are: $@"
    thisarray=$1
    echo "The received array is ${thisarray[*]}"
}
myarray=(1 2 3 4 5)
echo "The original array is: ${myarray[*]}"
testit $myarray
$ 
$ ./badtest3
The original array is: 1 2 3 4 5
The parameters are: 1
./badtest3: thisarray[*]: bad array subscript
The received array is
$
```

如果你尝试将数组变量作为参数，函数只会获取数组的第一个值。要解决这个问题，你必须将数组变量分解为它的独立值，然后将这些值作为函数参数。在函数内部，你可以将所有参数重新组合成一个新的数组变量。以下是这种操作的示例：

```bash
$ cat test10
#!/bin/bash
# array variable to function test
function testit {
    local newarray
    newarray=(echo "$@")
}
echo “The new array value is: ${newarray[*]}"
}
myarray=(1 2 3 4 5)
echo “The original array is ${myarray[*]}"
testit ${myarray[*]}
$
$ ./test10
The original array is 1 2 3 4 5
The new array value is: 1 2 3 4 5
$
```

该脚本使用 `$myarray` 变量来保存所有的数组值，并将它们全部放置在命令行中传递给函数。然后，函数从命令行参数重新构建数组变量。进入函数后，可以像使用其他数组一样使用它：

```bash
$ cat test11
#!/bin/bash
# adding values in an array
function addarray {
    local sum=0
    local newarray
    newarray=(‘echo “$@”`)
    for value in ${newarray[*]}
    do
        sum=$[ $sum + $value ]   done
    echo $sum
}
myarray=(1 2 3 4 5)
echo “The original array is: ${myarray[*]}"
arg1=‘echo ${myarray[*]}‘
result=‘addarray $arg1‘
echo “The result is $result”
$
$ ./test11
The original array is: 1 2 3 4 5
The result is 15
$
```

`addarray` 函数遍历数组值并将它们相加。你可以在 `myarray` 数组变量中放入任意数量的值，`addarray` 函数将对它们进行求加。

### 从函数返回数组

从函数将数组变量传回 Shell 脚本使用了类似的技术。函数使用 `echo` 语句按照正确的顺序输出单个数组值，然后脚本必须将它们重新组装成一个新的数组变量：

```bash
$ cat test12
#!/bin/bash
# returning an array value
function arraydblr {
    local origarray
    local newarray
    local elements
    local i
    origarray=(‘echo “$@”`)
    newarray=(‘echo “$@”`)
    elements=$[ $# - 1 ]
    for (( i = 0; i <= $elements; i++ ))
    {
        newarray[$i]=$[ ${origarray[$i]} * 2 ]
    }
    echo ${newarray[*]}
}
myarray=(1 2 3 4 5)
echo “The original array is: ${myarray[*]}"
arg1=‘echo ${myarray[*]}‘
result=(‘arraydblr $arg1‘)
echo “The new array is: ${result[*]}”
$
$ ./test12
The original array is: 1 2 3 4 5
The new array is: 2 4 6 8 10
```

该脚本使用 `$arg1` 变量将数组值传递给 `arraydblr` 函数。`arraydblr` 函数将数组重新组装成一个新的数组变量，并为输出数组变量创建一个副本。然后它遍历单个数组变量值，将每个值翻倍，并将其放入函数中的数组变量副本中。

随后，`arraydblr` 函数使用 `echo` 语句输出数组变量的各个值。脚本使用 `arraydblr` 函数的输出重新组装一个带有这些值的新数组变量。

### 函数递归

局部函数变量提供的一个特性是自包含性。自包含的函数不使用函数之外的任何资源，脚本通过命令行传递给它的变量除外。

这一特性使得函数可以递归调用，这意味着函数通过调用自己来获得答案。通常，递归函数有一个基值，它最终会迭代到该基值。许多高级数学算法使用递归来反复将复杂方程降级，直到达到基值定义的水平。

递归算法的经典例子是计算阶乘。一个数的阶乘是前面的数字与该数的乘积。因此，要找到 5 的阶乘，你需要执行以下方程：

`5! = 1 * 2 * 3 * 4 * 5 = 120`

使用递归，方程被简化为以下格式：

`x! = x * (x-1)!`

用英文表述为 `x` 的阶乘等于 `x` 乘以 `x-1` 的阶乘。这可以通过简单的递归脚本来实现：

```bash
function factorial {
    if [ $1 -eq 1 ]
    then
        echo 1
    else
        local temp=$[ $1 - 1 ]
        local result=‘factorial $temp‘
        echo $[ $result * $1 ]
    fi
}
```

阶乘函数使用自己来计算阶乘值：

```bash
$ cat test13
#!/bin/bash
# using recursion
function factorial {
    if [ $1 -eq 1 ]
    then
        echo 1
    else
        local temp=$[ $1 - 1 ]
        local result=‘factorial $temp‘
        echo $[ $result * $1 ]
    fi
}
read -p “Enter value: ” value
result=‘factorial $value‘
echo “The factorial of $value is: $result”
$
$ ./test13
Enter value: 5
The factorial of 5 is: 120
$
```

### 创建库

很容易看出函数如何帮助减少脚本中的打字量，但如果你恰好在脚本之间使用了同一个函数呢？如果你必须在每个脚本中定义相同的函数，这将是非常挑战性的。第一步是创建一个所需的库文件。这是一个名为 `myfuncs` 的简单库文件，它定义了三个函数：

```bash
$ cat myfuncs
# shell functions
function addem {
    echo $[ $1 + $2 ]
}
function multem {
    echo $[ $1 * $2 ]
}
function divem {
    if [ $2 -ne 0 ]
    then
        echo $[ $1 / $2 ]
    else
        echo -1
    fi
}
```

问题在于 Shell 的作用域。与环境变量一样，Shell 函数仅在定义它们的会话中有效。如果你运行 `myfuncs` 脚本，Shell 会创建一个新的 Shell，当你尝试运行另一个使用这些函数的脚本时，它们将不可用。

使用函数库的关键是 `source` 命令。`source` 命令在当前 Shell 中执行命令，而不是创建一个新的 Shell。你使用 `source` 命令在你的 Shell 脚本中运行该库文件。这使得函数对脚本可用。

`source` 命令有一个快捷别名，称为点操作符。要在要在 Shell 脚本中加载 `myfuncs` 库文件，你只需要添加以下行：

`. ./myfuncs`

此示例假设 `myfuncs` 库文件与 Shell 脚本位于相同的目录下。如果不是，你需要使用适当的路径来访问该文件。这是一个使用 `myfuncs` 库创建脚本示例：

```bash
$ cat test14
#!/bin/bash
# using functions defined in a library file
. ./myfuncs
value1=10
value2=5
result1=‘addem $value1 $value2‘
result2=‘multem $value1 $value2‘
result3=‘divem $value1 $value2‘
echo “The result of adding them is: $result1”
echo “The result of multiplying them is: $result2”
echo “The result of dividing them is: $result3”
$
$ ./test14
The result of adding them is: 15
The result of multiplying them is: 50
The result of dividing them is: 2
$
```



该脚本成功使用了`myfuncs`库文件中定义的函数。

# 在命令行上使用函数

你可以使用脚本函数来创建一些相当复杂的操作。有时，如果能够直接在命令行界面提示符中使用这些函数会非常有用。

就像你可以在 shell 脚本中使用脚本函数作为命令一样，你也可以在命令行界面将脚本函数作为命令。这是一个非常实用的功能，因为一旦你在 shell 中定义了函数，你就可以在系统的任何目录下使用它；你不必担心脚本是否在你的`PATH`环境变量中。诀窍在于让 shell 识别该函数。有几种方法可以实现。

## 在命令行上创建函数

由于 shell 会在你输入命令时对其进行解释，因此你可以直接在命令行上定义函数。有两种方法可以实现。

第一种方法在一行内定义整个函数：

```bash
$ function divem { echo $[ $1 / $2 ]; }
$ divem 100 5
20
$
```

当你在命令行上定义函数时，必须记住在每个命令的末尾包含分号，这样 shell 才知道在何处分隔命令：

```bash
$ function doubleit { read -p "Enter value: " value; echo $[ $value * 2 ]; }
$
$ doubleit
Enter value: 20
40
$
```

另一种方法是使用多行来定义函数。这样做时，bash shell 会使用次提示符提示你输入更多命令。使用这种方法，你不需要在每个命令的末尾放置分号；只需按回车键即可：

```bash
$ function multem {
> echo $[ $1 * $2 ]
> }
$ multem 2 5
10
$
```

当你使用函数末尾的大括号时，shell 就知道你已经完成了函数的定义。

> **注意**
> 在命令行上创建函数时要极度小心。如果你使用的函数名称与内置命令或其他命令重名，该函数将覆盖原始命令。

## 在 .bashrc 文件中定义函数

直接在命令行上定义 shell 函数的明显缺点是，当你退出 shell 时，你的函数就会消失。对于复杂的函数，这可能会变成一个问题。

更简单的方法是将函数定义在一个地方，每次你启动新的 shell 时，shell 都会重新加载它。

最好的位置是`.bashrc`文件。bash shell 每次启动时都会在你的家目录下查找此文件，无论是交互式启动，还是作为从现有 shell 启动新 shell 的结果。

### 直接定义函数

你可以直接在家目录下的`.bashrc`文件中定义函数。大多数 Linux 发行版已经在`.bashrc`文件中定义了一些内容，因此请小心不要删除它们。只需将你的函数添加到现有文件的末尾即可。这是一个这样做的示例：

```bash
$ cat .bashrc
.bashrc
### Source global definitions
if [ -r /etc/bashrc ]; then
    .etc/bashrc
fi
function add {
    echo $[ $1 + $2 ]
}
$
```

在下一次启动新的 bash shell 之前，函数才会生效。在此之后，你可以在系统的任何地方使用该函数。

### 引入函数文件

就像在 shell 脚本中一样，你可以使用`source`命令（或其别名点运算符`.`）将现有库文件中的函数添加到你的`.bashrc`脚本中：

```bash
$ cat .bashrc
.bashrc
### Source global definitions
if [ -r /etc/bashrc ]; then
    .etc/bashrc
fi
.home/rich/libraries/myfuncs
```

确保你包含了正确的路径，以便 bash shell 找到该库文件。当你下次启动 shell 时，库中的所有函数都可以在命令行界面上直接使用：

```bash
$ add 10 5
15
$ mult 10 5
50
$ dive 10 5
2
$
```

更好的是，shell 还会将任何定义的函数传递给子进程，因此你的函数自动适用于你运行的任何 shell 脚本。你可以编写一个使用这些函数但没有定义或引入它们的脚本来测试这一点：

```bash
$ cat test1
#!/bin/bash
# using a function defined in the .bashrc file
value1=10
value2=5
result1=$(add $value1 $value2)
result2=$(mult $value1 $value2)
result3=$(dive $value1 $value2)
echo "The result of adding them is: $result1"
echo "The result of multiplying them is: $result2"
echo "The result of dividing them is: $result3"
$
./test1
The result of adding them is: 15
The result of multiplying them is: 50
The result of dividing them is: 2
$
```

即使没有引入库文件，这些函数在 shell 脚本中也能运行良好。

## 总结

Shell 脚本函数允许你将脚本中反复出现的脚本代码放在一个地方。你不需要重写代码块，而是创建一个包含该代码块的函数，然后只需在脚本中引用函数名即可。当 bash shell 看到脚本中使用函数名时，它就会跳转到函数代码块。

你甚至可以创建可以返回值的脚本函数。这允许你创建与脚本交互的函数，返回数值和字符数据。脚本函数可以通过使用函数中最后一个命令的退出状态，或使用`return`命令来返回数值数据。`return`命令允许你根据函数的结果程序化地将函数的退出状态设置为特定值。

函数还可以使用标准的`echo`语句返回值。你可以像处理任何其他 shell 命令一样，使用反引号字符来捕获输出数据。这使得你能够从函数返回任何类型的数据，包括字符串和浮点数。

你可以在函数中使用 shell 变量，为变量赋值并从现有变量获取值。这允许你从主脚本向脚本函数传递任何类型的数据。函数还允许你定义局部变量，这些变量仅在函数代码块内部可用。局部变量允许你创建与主 shell 中使用的变量或进程独立的函数。

函数还可以调用其他函数，包括自身。当函数调用自身时，被称为递归。递归函数通常有一个基准值，作为函数的终止值。函数继续以递减的参数值调用自身，直到达到基准值。

如果你在 shell 脚本中使用许多函数，可以创建脚本函数的库文件。可以通过`source`命令（或其别名点运算符`.`）在任何 shell 文件中包含库文件。这被称为引入库文件。shell 不会运行库文件，而是让运行脚本的 shell 可以使用这些函数。

# 创建文本菜单

创建交互式 shell 脚本最常见的方法是利用菜单。为客户提供各种选项的选择有助于引导他们准确了解脚本可以做什么和不能做什么。

菜单脚本通常会清除显示区域，然后显示可用选项列表。客户可以通过按下分配给每个选项的相关字母或数字来选择选项。图 17.1 显示了一个示例菜单的布局。

图 17.1 从 shell 脚本中显示菜单

![](img/00013.jpg)

shell 脚本菜单的核心是`case`命令（参见第 11 章）。`case`命令根据客户从菜单中选择的字符执行特定的命令。

接下来的章节将引导你完成基于菜单的 shell 脚本时应该遵循的步骤。

## 创建菜单布局

创建菜单的第一步显然是确定你想在菜单中显示哪些元素，并按照你想要的方式对其进行布局。

在创建菜单之前，通常清除显示器内容是一个好主意。这让你能够在一个干净的环境中显示菜单，而不会受到文本的干扰。

`clear`命令使用你终端会话的`terminfo`数据（参见第 2 章）来清除显示器上出现的任何文本。执行`clear`命令后，你可以使用`echo`命令显示你的菜单元素。

默认情况下，`echo`命令只能显示可打印的文本字符。在创建菜单项时，使用不可打印项（如制表符和换行符）通常很有帮助。若要在你的`echo`命令中包含这些字符，你必须使用`-e`选项。因此，命令：

```
echo -e "1.\tDisplay disk space"
```

将产生输出行：

```
1         Display disk space
```

这极大地有助于格式化菜单项的布局。只需几个`echo`命令，你就可以创建一个看起来合理的菜单：

```
clear
echo
echo -e "\t\t\tSys Admin Menu\n"
echo -e "\t1. Display disk space"
echo -e "\t2. Display logged on users"
echo -e "\t3. Display memory usage"
echo -e "\t0. Exit menu\n\n"
echo –en "\t\nEnter option: "
```

最后一行的`-en`选项会在不在末尾添加换行符的情况下显示该行。这使得菜单看起来更专业，因为光标将停留在行尾等待客户的输入。

创建菜单的最后部分是从客户处获取输入。这是通过使用`read`命令完成的（参见第 13 章）。由于我们预期单字符输入，良好的做法是在`read`命令中使用`-n`选项来仅获取一个字符。这允许客户输入数字而无需按回车键：

```
read -n 1 option
```

接下来，你将创建菜单函数。

## 创建菜单函数

将 shell 脚本菜单选项作为一组独立的函数来创建会更容易。这允许你创建一个简单、且易于遵循的`case`命令。

要做到这一点，你需要为每个菜单选项创建单独的 shell 函数。创建菜单 shell 脚本的第一步是确定让脚本执行哪些函数，并将它们作为单独的函数在代码中布局。

为尚未实现的函数创建“存根函数”（stub functions）是一种常见做法。存根函数是一个尚未包含任何命令的函数，或者可能只包含一个指示最终应该放置内容的`echo`语句：

```
function diskspace {
    clear
    echo "This is where the diskspace commands will go"
}
```

这使得你的菜单在你处理各个函数时能够顺畅运行。你不需要为菜单运行编写所有函数的代码。你会发现函数是从`clear`命令开头的。这让你可以在没有菜单的情况下在干净的显示器上启动函数。

shell 菜单中有帮助的一点是将菜单布局创建为一个函数：

```
function menu {
    clear
    echo
    echo -e "\t\t\tSys Admin Menu\n"
    echo -e "\t1. Display disk space"
    echo -e "\t2. Display logged on users"
    echo -e "\t3. Display memory usage"
    echo -e "\t0. Exit program\n\n"
    echo -en "\t\nEnter option: "
    read -n 1 option
}
```

这让你能够通过调用`menu`函数随时地重新显示菜单。

## 添加菜单逻辑

现在你有了菜单布局和函数，你需要的是创建编程逻辑将它们整合起来。如所述，这需要`case`命令。`case`命令应该根据从菜单选择的字符调用相应的函数。使用默认`case`字符（星号`*`）来捕捉任何错误输入始终是一个好主意。

以下代码说明了在典型菜单中使用`case`命令：

```
menu
case $option in
0)
    break;;
1)
    diskspace;;
2)
    whoseon;;
3)
    memusage;;
*)
    clear
    echo "Sorry, wrong selection";;
esac
```

此代码使用`menu`函数来清除显示器屏幕并显示菜单。`menu`函数中的`read`命令会暂停，直到客户在键盘上击一个字符。一旦完成，`case`命令就会接管。`case`命令根据返回的字符调用相应的函数。在函数完成后，`case`命令退出。

## 整合在一起

现在你已经看到了了构成 shell 脚本菜单的所有部分，让我们把它们整合在一起，看看它们是如何相互协作的。这是一个完整的菜单脚本示例：

```bash
$cat menu1
#!/bin/bash
# simple script menu
function diskspace {
    clear
    df -k
}
function whoseon {
    clear
    who
}
function memusage {
    clear
    cat /proc/meminfo
}
function menu {
    clear
    echo
    echo -e "\t\t\tSys Admin Menu\n"
    echo -e "\t1. Display disk space"
    echo -e "\t2. Display logged on users"
    echo -e "\t3. Display memory usage"
    echo -e "\t0. Exit program\n\n"
    echo -en "\t\nEnter option: "
    read -n 1 option
}
while [ 1 ]
do
    menu
    case $option in
0)
        break;;
1)
        diskspace;;
2)
        whoseon;;
3)
        memusage;;
*)
        clear
        echo "Sorry, wrong selection";;
esac
    echo -en "\n\n\t\t\tHit any key to continue"
    read -n 1 line
done
clear
```

此菜单创建了三个函数，使用常用命令获取 Linux 系统管理信息。它使用`while`循环不断循环菜单，直到客户选择选项 0，该选项使用`break`命令跳出`while`循环。

# 使用 select 命令

你可能已经注意到，创建文本菜单的挑战在于创建菜单布局并获取你输入的答案。bash shell 为你提供了一个实用的工具，可以自动完成所有这些工作。

`select`命令允许你从单行命令行创建一个菜单，然后获取输入的答案并对其进行自动处理。`select`命令的格式如下：

```bash
select variable in list
do
    commands
done
```

`list`参数是一个由空格分隔的文本项列表，用于构建菜单。`select`命令将列表中的每个项显示为编号选项，然后显示一个由`PS3`环境变量定义的特殊提示符，供用户选择。

这里有一个`select`命令运行的简单示例：

```bash
$ cat smenu1
#!/bin/bash
# using select in the menu
function diskspace {
  clear
  df -k
}
function whoseon {
  clear
  who
}
function memusage {
  clear
  cat /proc/meminfo
}
PS3="Enter option: "
select option in "Display disk space" "Display logged on users"
"Display memory usage" "Exit program"
do
    case $option in
    "Exit program")
        break ;;
    "Display disk space")
        diskspace ;;
    "Display logged on users")
        whoseon ;;
    "Display memory usage")
        memusage ;;
    *)
        clear
        echo "Sorry, wrong selection";;
    esac
done
clear
$
```

当你运行该程序时，它会自动生成以下菜单：

```bash
$ ./smenu1
1) Display disk space        3) Display memory usage
2) Display logged on users  4) Exit program
Enter option:
```



使用 `select` 命令时，请记住存储在变量中的值是整个文本字符串，而不是与菜单项关联的数字。文本字符串值才是你在 `case` 语句中需要比较的内容。

# 操作 Windows

使用文本菜单是向正确方向迈的一步，但我们的交互式脚本仍然有很多缺失，特别是当我们试图将其与图形化的 Windows 世界进行比较时。幸运的是，开源世界中有些非常有才华的人帮助了我们。

`dialog` 软件包是一个非常实用的小工具，最初由 Savio Lam 创建，目前由 Thomas E. Dickey 维护。该软件包使用 ANSI 转义控制代码在文本环境中重建了标准的 Windows 对话框。你可以轻松地将其整合到脚本中。

> **注意**
>
> 并不是所有 Linux 发行版都安装了 `dialog` 包。如果没有安装，可以使用以下命令进行安装：

```bash
sudo apt-get install dialog
```

## dialog 软件包

`dialog` 命令提供了各种组件，用于在脚本中创建交互界面。

| 组件 | 描述 |
| :--- | :--- |
| `calendar` | 提供日历 |
| `checklist` | 允许多项选择 |
| `form` | 允许表单输入 |
| `select` | 允许选择列表 |
| `gauge` | 显示进度条 |
| `infobox` | 显示消息 |
| `inputbox` | 询问用户输入 |
| `menu` | 显示菜单列表 |
| `msgbox` | 显示消息 |
| `pause` | 暂停执行直到用户输入 |
| `password` | 隐藏用户输入 |
| `passwordform` | 允许密码输入 |
| `radiolist` | 允许选择一个选项 |
| `tail` | 显示文本内容 |
| `tailbg` | 显示带有背景颜色的文本 |
| `textbox` | 询问文本输入 |
| `timebox` | 提供时间选择 |
| `yesno` | 询问是/否问题 |

### msgbox 组件

`msgbox` 组件是最常见的对话框类型。它在窗口中显示消息并等待用户点击 OK。使用它需要遵循以下格式：

```bash
dialog --msgbox text height width
```

`text` 参数是任何你想放在窗口中的字符串。`dialog` 命令将根据你创建的 `height` 和 `width` 参数自动对文本进行换行以适应指定的大小。如果你想在窗口顶部放置标题，还可以使用 `--title` 参数。这里是使用 `msgbox` 的示例：

```bash
$ dialog --title "Testing" --msgbox "This is a test" 10 20
```

输入此命令后，消息框将出现在你正在使用的终端模拟器屏幕上。图 17.2 显示了它的样子。

图 17.2 在 `dialog` 命令中使用 `msgbox` 组件

![](img/00020.jpg)

### yesno 组件

`yesno` 组件比 `msgbox` 组件更进一步，允许用户回答窗口中显示的是/否问题。它在窗口底部生成两个按钮，一个用于是，另一个用于否。用户可以使用鼠标、Tab 键或键盘方向键在按钮之间切换。要选择该按钮，用户可以按下空格键或回车键。

```bash
$ echo $?

1

$
```

这会产生图 17.3 所示的小部件。

图 17.3 在 `dialog` 命令中使用 `yesno` 部件

![](img/00030.jpg)

`dialog` 命令的退出状态取决于用户选择了哪个按钮。如果选择了 No（否）按钮，退出状态为 `1`；如果选择了 Yes（是）按钮，退出状态为 `0`。

### 输入 inputbox 部件

`inputbox` 部件为用户提供了一个简单的文本框区域用于输入文本字符串。`dialog` 命令将文本字符串的值发送到 `STDERR`。你必须将其重定向以获取答案。图 17.4 展示了 `inputbox` 部件的样子。

图 17.4 inputbox 部件

![](img/00025.jpg)

如你在图 17.4 中所示，`inputbox` 提供了两个按钮：OK 和 Cancel。如果选择了 Cancel（取消）按钮，命令的退出状态为 `1`；否则，退出状态将为 `0`：

```bash
$ dialog --inputbox "Enter your age:" 10 20 2>age.txt

$ echo $?

0

$ cat age.txt

12$
```

你会注意到，当使用 `cat` 命令显示文本文件内容时，值之后没有换行符。这允许你轻松地将文件内容重定向到 shell 脚本中的变量，以提取用户输入的字符串。

### 文本 textbox 部件

`textbox` 部件是在窗口中显示大量信息的极佳方法。它产生一个滚动的窗口，包含参数中指定的文件的文本：

```bash
$ dialog --textbox /etc/passwd 15 45
```

`/etc/passwd` 文件的内容显示在滚动的文本窗口中，如图 17.5 所示。

图 17.5 textbox 部件

![](img/00036.jpg)

你可以使用方向键在文本文件中向左、右以及向上向下滚动。窗口底部的行显示你正在查看的文件中的百分比位置。`textbox` 仅包含一个 Exit（退出）按钮，选择该按钮即可退出部件。

### 菜单 menu 部件

`menu` 部件允许你创建一个在本章之前创建的文本菜单的窗口版本。你只需要为每个项目提供一个选择标签和文本即可：

```bash
$ dialog --menu "Sys Admin Menu" 20 30 10 1 "Display disk space" \
2 "Display users" 3 "Display memory usage" 4 "Exit" 2> test.txt
```

第一个参数定义了菜单标题。接下来两个参数定义了窗口的高度和宽度，而第三个参数定义了同时在窗口中显示的菜单项数量。如果有更多菜单项，你可以使用方向键进行滚动。

在这些参数之后，你必须添加菜单项对。第一个元素是用于选择菜单项的标签。每个标签对于每个菜单项都应该是唯一的，并且可以通过按下键盘上相应的键来选择。第二个元素是菜单中使用的文本。图 17.6 展示了示例命令产生的菜单。

图 17.6 带有菜单项的菜单部件

![](img/00061.jpg)

如果用户通过按下标签对应的键选择菜单项，该菜单项会被高亮但未被选中。只有使用鼠标或 Enter 键选择 OK 按钮才会完成选择。`dialog` 命令将选中的菜单项文本发送到 `STDERR`，你可以根据需要对其重定向。

### 文件选择 fselect 部件

`dialog` 命令提供了几个花哨内置部件。在处理文件名时，`fselect` 部件非常方便。你不需要强制用户输入文件名，而是可以使用 `fselect` 部件浏览到文件位置并选择文件，如图 17.7 所示。

图 17.7 fselect 部件

![](img/00064.jpg)

`fselect` 部件格式如下：

```bash
$ dialog --fselect "Select a file" $HOME/ 10 20 2>file
```

`$HOME/` 是 `fselect` 部件的起始位置。你可以输入文本框自定义：

```bash
$ dialog --inputbox "Enter your age:" 10 20 2>age.txt
```

第一个参数是 `fselect` 窗口的标题。在右侧显示列表。

## dialog 选项

除了标准部件外，你还可以自定义 `dialog` 的许多选项。你已经看到了 `--title` 参数的作用。

许多选项可以自定义窗口的显示。可以使用 `dialog` 的可用选项。

表 17.2 命令选项

| 选项 | 说明 |
| :--- | :--- |
| `--add-widget` | 除非按下 Cancel 按钮。 |
| `--aspect` `ratio` | 指定窗口的宽高比。 |
| `--backtitle` `title` | 显示顶部的标题。 |
| `--begin` `x y` | 指定左上角的起始位置。 |
| `--cancel-label` `label` | Cancel 按钮的替代标签。 |
| `--clear` | 使用默认背景颜色清除。 |
| `--colors` | 在文本中嵌入 ANSI 颜色。 |
| `--cr-wrap` | 允许文本中的换行符。 |
| `--create-rc` `file` | 将示例配置导出到。 |
| `--defaultno` | 设置 yes/no 对的默认。 |
| `--default-item` `string` | 设置选择框、表单或菜单中的默认项。 |
| `--exit-label` `label` | Exit 按钮的替代标签。 |
| `--extra-button` | 在 OK 和 Cancel 按钮之间显示额外按钮。 |
| `--extra-label` `label` | 额外按钮的替代标签。 |
| `--help` | 显示 `dialog` 命令帮助消息。 |
| `--help-button` | 在 OK 和 Cancel 按钮之后显示帮助按钮。 |
| `--help-label` `label` | 帮助按钮的替代标签。 |
| `--help-status` | 在选择帮助按钮后写入选择框、列表框或表单信息。 |
| `--ignore` | 忽略 `dialog` 不识别的选项。 |
| `--input-fd` `fd` | 指定除 `STDIN` 外的替代文件描述符。 |
| `--insecure` | 密码部件时显示星号。 |
| `--item-help` | 在选择框、列表框或菜单的每个标签屏幕底部添加帮助列。 |
| `--keep-window` | 不清除屏幕上的旧部件。 |
| `--max-input` `size` | 指定输入的最大字符串大小。默认为 2048。 |
| `--nocancel` | 取消 Cancel 按钮。 |
| `--no-collapse` | 不将对话文本中的制表符转换为空格。 |
| `--no-kill` | 将 `tailboxbg` 放入后台并禁用进程的 `SIGHUP`。 |
| `--no-label` `label` | No 按钮的替代标签。 |
| `--no-shadow` | 不为窗口显示阴影。 |
| `--ok-label` `label` | OK 按钮的替代标签。 |
| `--output-fd` `fd` | 指定除 `STDERR` 外的替代输出文件描述符。 |
| `--print-maxsize` | 输出允许的 `dialog` 窗口的最大大小。 |
| `--print-size` | 将每个对话框的大小打印到输出中。 |
| `--print-version` | 将对话版本打印到输出中。 |
| `--separate-output` | 逐行输出复选列表组件的结果，不加引号。 |
| `--separator` `string` | 指定一个用于分隔每个组件输出的字符串。 |
| `--separate-widget` `string` | 指定一个用于分隔每个组件输出的字符串。 |
| `--shadow` | 在每个窗口的右侧和下方绘制阴影。 |
| `--single-quoted` | 如果复选列表需要则使用单引号。 |
| `--sleep` `sec` | 在处理对话框后延迟指定的秒数。 |
| `--stderr` | 将输出发送到 `STDERR`（这是默认行为）。 |
| `--stdout` | 将输出发送到 `STDOUT`。 |
| `--tab-correct` | 将制表符转换为空格。 |
| `--tab-len` `n` | 指定制表符占用的空格数（默认值为 8）。 |
| `--timeout` `sec` | 指定在没有用户输入的情况下，多少秒后以错误代码退出。 |
| `--title` `title` | 指定对话框窗口的标题。 |
| `--trim` | 对话框文本前面的空格和换行符。 |
| `--visit-items` | 修改对话框中的制表位以包含项目列表。 |
| `--yes-label` `label` | 为“是 (Yes)”按钮指定备用标签。 |

`--backtitle` 选项是通过脚本为菜单创建一个通用标题的方便方法。如果你为每个对话框窗口指定了它，它将贯穿整个应用程序，为你的脚本营造专业外观。

从表 17.2 中可以看出，你可以覆盖对话框窗口中的任何按钮标签。此功能允许你创建几乎所需的任何窗口场景。

## 在脚本中使用 dialog 命令

在脚本中使用 `dialog` 命令非常轻而易举。你只需要记住两点：

- 如果有“取消 (Cancel)”或“否 (No)”按钮可用，请检查 `dialog` 命令的退出状态。
- 重定向 `STDERR` 以获取输出值。

如果你遵循这两个规则，你很快就能拥有一个看起来专业的交互式脚本。这里有一个使用 `dialog` 组件来重现我们在本节之前创建的系统管理员菜单的示例：

```bash
cat menu3
#!/bin/bash
# 使用 dialog 创建菜单
temp='mktemp -t test.XXXXXX'
temp2='mktemp -t test2.XXXXXX'

function diskspace {
    df -k > $temp
    dialog --textbox $temp 20 60
}

function whoseon {
    who > $temp
    dialog --textbox $temp 20 50
}

function memusage {
    cat /proc/meminfo > $temp
    dialog --textbox $temp 20 50
}

while [ 1 ]
do
  dialog --menu “Sys Admin Menu” 20 30 10 1 “Display disk space” 2 \
  “Display users” 3 “Display memory usage” 0 “Exit” 2> $temp2

  if [ $? -eq 1 ]
  then
    break
  fi

selection='cat $temp2'

case $selection in
1)
    diskspace ;;
2)
    whoseon ;;
3)
    memusage ;;
0)
    break ;;
*)
    dialog --msgbox “Sorry, invalid selection” 10 30
esac
done

rm -f $temp 2> /dev/null
rm -f $temp2 2> /dev/null
```

该脚本使用带有常量真值的 `while` 循环来创建一个无限循环菜单对话框。这意味着在执行每个函数后，脚本都会返回到显示菜单。

`menu` 对话框包含一个取消按钮，因此脚本会检查 `dialog` 命令的退出状态，以防用户按下取消按钮退出。由于它在 `while` 循环中，退出变得就像使用 `break` 命令跳出 `while` 循环一样简单。

脚本使用 `mktemp` 命令创建了两个临时文件来存储 `dialog` 命令的数据。第一个文件 `$temp` 用于存储 `df` 和 `meminfo` 命令的输出，以便它们可以在 `textbox` 对话框中显示（参见图 17.8）。第二个临时文件 `$temp2` 用于存储来自主菜单对话框的选值。

图 17.8 使用 textbox 对话框选项显示的 `meminfo` 命令输出

![](img/00069.jpg)

现在这看起来开始像一个你可以向别人展示的真实应用程序了！

## 获取图形界面

如果你正在为你的交互式脚本寻找更多图形化效果，你可以更进一步。KDE 和 GNOME 桌面环境（参见第 1 章）都扩展了 `dialog` 命令的想法，并包含了为各自环境生成 X Windows 图形窗口组件的命令。

本节描述了 `kdialog` 和 `zenity` 包，它们分别为 KDE 和 GNOME 桌面提供图形化窗口组件。

### KDE 环境

KDE 图形环境默认包含 `kdialog` 包。`kdialog` 包使用 `kdialog` 命令在你的 KDE 桌面中生成标准窗口，类似于 `dialog` 风格的组件。然而，这些窗口并没有笨重的感觉，而是与你其他的 KDE 应用程序窗口融在一起！这允许你直接从 shell 脚本产生 Windows 级的用户界面！

> **注意**
>
> 仅仅你的 Linux 发行版使用了 KDE 桌面并不意味着它默认安装了 `kdialog` 包。你可能需要从发行版存储库手动安装它。

### kdialog 组件

与 `dialog` 命令一样，`kdialog` 命令使用命令行选项来指定使用什么类型的窗口组件。以下是 `kdialog` 命令的格式：

`kdialog display-options window-options arguments`

`window-options` 选项允许你指定使用什么类型的窗口组件。可用选项如表 17.3 所示。

表 17.3 kdialog 窗口选项

| 选项 | 描述 |
| :--- | :--- |
| `--checklist` `title [tag item status]` | 复选列表菜单，状态指定项目是否被勾选。 |
| `--error` `text` | 错误消息框。 |
| `--inputbox` `text [init]` | 输入文本框。你可以使用 `init` 值指定默认值。 |
| `--menu` `title [tag item]` | 菜单选择框标题和由标签标识的项目列表。 |
| `--msgbox` `text` | 带有指定文本的简单消息框。 |
| `--password` `text` | 隐藏用户输入的密码输入框。 |



| `--radiolist` `title [tag item status]` | 单选列表菜单，状态指定项目是否被选中。 |

| `--separate-output` | 为复选列表和单选列表菜单分行返回项目。 |

| `--sorry` `text` | 抱歉消息框。 |

| `--textbox` `file [width] [height]` | 显示 `file` 内容的文本框，也可以由 `width` 和 `height` 指定。 |

| `--title` `title` | 指定对话框窗口标题栏的标题。 |

| `--warningyesno` `text` | 带有“是”和“否”按钮的警告消息框。 |

| `--warningcontinuecancel` `text` | 带有“继续”和“取消”按钮的警告消息框。 |

| `--warningyesnocancel` `text` | 带有“是”、“否”和“取消”按钮的警告消息框。 |

| `--yesno` `text` | 带有“是”和“否”按钮的问题框。 |

| `--yesnocancel` `text` | 带有“是”、“否”和“取消”按钮的问题框。 |

从表 17.3 可以看出，所有的标准对话框类型都涵盖了。然而，当你使用 `kdialog` 窗口组件时，它作为 KDE 桌面上的独立窗口出现，而不是在终端模拟器会话内部！

`checklist` 和 `radiolist` 组件允许你定义列表中的单个项目以及它们是否默认被选中：

```bash
$ kdialog --checklist “我需要的物品” 1 “牙刷” on 2 “牙膏” \
  off 3 “梳子” on 4 “去味剂” off 5 “拖鞋” off
```

生成的复选列表窗口显示在图 17.9 中。

图 17.9 一个 `kdialog` 检查列表对话框

![](img/00071.jpg)

被指定为“开启”的项目在检查列表中会被高亮显示。要选择或取消选择检查列表中的项目，只需点击它。如果你选择 OK 按钮，`kdialog` 将将标签值发送到 `STDOUT`：

`“1” “3” “5”`

`$`

当你按下回车键时，`kdialog` 框会带有选择的内容出现。当你点击 OK 或取消按钮时，`kdialog` 命令会将每个标签作为字符串值返回到 `STDOUT`（这些你在输出中看到的 `“1”`、`“3”` 和 `“5”` 值）。你的脚本必须能够解析结果值并将其与原始值匹配。

### 使用 kdialog

你可以像使用 `dialog` 控件一样，在 shell 脚本中使用 `kdialog` 窗口控件。主要的区别在于，`kdialog` 窗口控件使用 `STDOUT` 输出值，而不是 `STDERR`。

这里有一个脚本，将之前创建的系统管理员菜单转换为 KDE：

```bash
$ cat menu4
#!/bin/bash
# 使用 kdialog 创建菜单
temp=‘mktemp -t temp.XXXXXX‘
temp2=‘mktemp -t temp2.XXXXXX‘
function diskspace {
    df -k > $temp
    kdialog --textbox $temp 1000 10
}
function whoseon {
    who > $temp
    kdialog --textbox $temp 500 10
}
function memusage {
    cat /proc/meminfo > $temp
    kdialog --textbox $temp 300 500
}
while [ 1 ]
do
kdialog --menu “Sys Admin Menu” "1" "Display diskspace" "2" "Display users" "3" "Display memory usage" "0" "Exit" > $temp2
if [ $? -eq 1 ]
then
    break
fi
selection=‘cat $temp2‘
case $selection in
1)
    diskspace ;;
2)
    whoseon ;;
3)
    memusage ;;
0)
    break ;;
*)
    kdialog --msgbox “Sorry, invalid selection”
esac
done
$
```

使用 `kdialog` 命令和使用 `dialog` 命令的脚本之间没有太大区别。生成的主菜单见图 17.10。

图 17.10 使用 `kdialog` 的系统管理员菜单脚本

![](img/00027.jpg)

现在，你的简单 shell 脚本看起来就像一个真正的 KDE 应用程序了！现在你的交互式脚本可以做的事情已经没有限制了。

### GNOME 环境

GNOME 图形环境支持两个可以生成标准窗口的流行包：

* `gdialog`

* `zenity`

到目前为止，`zenity` 是大多数 GNOME 桌面 Linux 发行版中最常见的软件包（它在 Ubuntu 和 Fedora 中都是默认安装的）。本节描述了 `zenity` 的功能，并演示了如何在 shell 脚本中使用它。

### zenity 控件

正如你所预料的，`zenity` 允许你通过命令行选项创建不同的窗口控件。表 17.4 显示了 `zenity` 可以产生的不同控件。

表 17.4 zenity 窗口控件

| 选项 | 描述 |

| :--- | :--- |

| `--calendar` | 显示整月日历。 |

| `--entry` | 显示文本输入对话框。 |

| `--error` | 显示错误消息对话框。 |

| `--file-selection` | 显示完整路径和文件名的对话框。 |

| `--info` | 显示信息对话框。 |

| `--list` | 显示检查列表或单选列表对话框。 |

| `--notification` | 显示通知图标。 |

| `--progress` | 显示进度条对话框。 |

| `--question` | 显示是/否问题对话框。 |

| `--scale` | 显示比例尺对话框。 |

| `--text-info` | 显示包含文本的文本框。 |

| `--warning` | 显示警告对话框。 |

`zenity` 命令行程序的工作方式与 `kdialog` 和 `dialog` 程序略有不同。许多控件类型是使用命令行上的额外选项定义的，而不是作为选项的参数。

`zenity` 命令确实提供了一些非常酷的高级对话框。`calendar` 选项产生一个整月日历，如图 17.11 所示。

图 17.11 zenity 日历对话框

![](img/00019.jpg)

当你从日历中选择日期时，`zenity` 命令会将值返回到 `STDOUT`，就像 `kdialog` 一样：

```bash
$ zenity --calendar
12/25/2011
$
```

`zenity` 中另一个很酷的窗口是文件选择选项，如图 17.12 所示。

图 17.12 zenity 文件选择对话框

![](img/00037.jpg)

你可以使用对话框浏览到系统上的任何目录位置（只要你有查看该目录的权限）并选择一个文件。当你选择一个文件时，`zenity` 命令会返回完整的文件和路径：

```bash
$ zenity --file-selection
/home/ubuntu/menu5
$
```

有了这些工具供你使用，你的 shell 脚本创作将是无限制的！

### 在脚本中使用 zenity

正如你所预期的，`zenity` 在 shell 脚本中表现良好。遗憾的是，`zenity` 选择不遵循 `dialog` 和 `kdialog` 使用的选项规范，因此将任何现有交互式脚本转换为 `zenity` 可能会很有挑战。

在将系统管理员菜单从 `kdialog` 转换为 `zenity` 时，我们发现必须对控件定义进行大量的处理：

```bash
$ cat menu5
#!/bin/bash
# 使用 zenity 创建菜单
temp=‘mktemp -t temp.XXXXXX‘
temp2=‘mktemp -t temp2.XXXXXX‘
function diskspace {
    df -k > $temp
    zenity --textbox $temp 750 10
}
function whoseon {
    who > $temp
    zenity --textbox $temp 500 10
}
function memusage {
    cat /proc/meminfo > $temp
    zenity --textbox $temp 300 500
}
while [ 1 ]
do
zenity --list --radiolist --title “Sys Admin Menu” --column "Select" --column "Menu Item" "Display diskspace" "Display users" "Display memory usage" "Exit" > $temp2
if [ $? -eq 1 ]
then
    break
fi
selection=‘cat $temp2‘
case $selection in
(“Display diskspace”)
    diskspace ;;
(“Display users”)
    whoseon ;;
(“Display memory usage”)
    memusage ;;
Exit)
    break ;;
*)
    zenity --info “Sorry, invalid selection”
esac
done
$
```

由于 `zenity` 不支持菜单窗口，我们使用单选列表类型作为主菜单，如图 17.13 所示。

单选列表使用两列，每列都有标题。第一列包含用于选择的单选按钮。第二列是项目文本。单选列表也没有为项目使用标签。当你选择一个项目时，项目的完整文本将返回到 `STDOUT`。这让 `case` 命令的生活变得稍微有趣了一些。你必须在 `case` 选项中使用项目的完整文本。如果文本中有任何空格，你需要在文本周围加上引号。

使用 `zenity` 包，你可以为 GNOME 桌面上的交互式 shell 脚本添加 Windows 风格。

### 总结

交互式 shell 脚本有枯燥无味的声誉。你可以通过使用大多数 Linux 系统上提供的不同技术和工具来改变这一点。首先，你可以通过 `case` 命令和 shell 脚本函数为你的交互式脚本创建菜单系统。

`case` 命令允许你使用标准的 `echo` 命令绘制菜单，并使用 `read` 命令读取用户的响应。随后，`case` 命令会根据输入的值选择合适的 shell 脚本函数。

`dialog` 程序提供了几个预构建的文本小部件，用于在基于文本的终端模拟器上创建类似 Windows 的对象。你可以使用 `dialog` 程序创建用于显示文本、输入文本以及选择文件和日期的对话框。这有助于让你的 shell 脚本更加生动。

如果你在图形化的 X Windows 环境中运行 shell 脚本，你可以在交互式脚本中使用更多的工具。对于 KDE 桌面，有一个 `kdialog` 程序。该程序提供了简单的命令，用于为所有基本的窗口功能创建窗口小部件。对于 GNOME 桌面，有 `gdialog` 和 `zenity` 程序。这些程序提供的窗口小部件可以像真实的 Windows 应用程序一样融入到 GNOME 桌面中。

下一章将深入探讨编辑和操作文本数据文件的主题。通常，shell 脚本最大的用途之一围绕着解析和显示日志文件、错误文件等文本文件中的数据。Linux 环境包含了两个非常有用的工具 `sed` 和 `gawk`，用于在 shell 脚本中处理文本数据。下一章将向你介绍这些工具，并展示如何使用它们的基础。

# 第 18 章

## 介绍 sed 和 gawk

## 本章内容

* 文本操作

* sed 编辑器基础

到目前为止，人们使用 shell 脚本最常见的功能之一就是处理文本文件。从检查日志文件、读取配置文件到处理数据元素，shell 脚本可以帮助自动化处理文本文件中包含的任何类型数据的枯燥任务。然而，仅用 shell 脚本命令来尝试操作文本文件的内容可能会有些笨拙。如果你在 shell 脚本中执行任何类型的数据操作，你将希望熟悉 Linux 中提供的 `sed` 和 `gawk` 工具。这些工具可以极大简化你需要执行的任何数据处理任务。

## 文本操作

第 9 章向你展示了如何使用 Linux 环境中提供的不同编辑器程序来编辑文本文件。这些编辑器允许你通过简单的命令或鼠标点击来轻松操作文本文件中包含的内容。

然而，在某些情况下，你会发现自己想要即时操作文本文件中的文本，而无需调出一个完整的交互式文本编辑器。在这些情况下，拥有一个简单的命令行编辑器将很有用，它可以自动格式化、插入、修改或删除文本元素。

Linux 系统提供了两个常用的工具来完成此任务。本节描述了 Linux 世界中最常用的两种命令行编辑器：`sed` 和 `gawk`。

## sed 编辑器

`sed` 编辑器被称为流编辑器（stream editor），与普通的交互式文本编辑器不同。在交互式文本编辑器（如 `vim`）中，你交互式地使用键盘命令来插入、删除或替换数据中的文本。流编辑器则根据你提前提供的一组规则对数据流进行编辑，这些规则是在编辑器处理数据之前提供的。

`sed` 编辑器根据你输入的命令行或存储在命令文本文件中的命令来操作数据流中的数据。它每次从输入中读取一行数据，将该数据与提供的编辑器命令匹配，按照命令指定的更改流中的数据，然后将新数据输出到 `STDOUT`。当流编辑器对一行数据匹配完所有命令后，它会读取下一行数据并重复该过程。当流编辑器处理完流中的所有行后，它就会终止。

由于命令是按行顺序应用的，`sed` 编辑器只需要对数据流进行一次扫描即可完成编辑。这使得 `sed` 编辑器比交互式编辑器快得多，并允许你快速对文件中的数据进行更改。

使用 `sed` 命令的格式为：

```
sed options script file
```

选项参数允许你自定义 `sed` 命令的行为，包含了表 18.1 所示的选项。

### 表 18.1 sed 命令选项

| 选项 | 描述 |

| :--- | :--- |

| `-e script` | 将脚本中指定的命令添加到处理输入时运行的命令中。 |

| `-f file` | 将文件中指定的命令添加到处理输入时运行的命令中。 |

| `-n` | 不为每个命令产生输出，而是等待 `print` 命令。 |

`script` 参数指定了一个应用于流数据的单个命令。如果需要多个命令，你必须使用 `-e` 选项在命令行中指定它们，或使用 `-f` 选项在单独的文件中指定它们。有许多命令可用于操作数据。我们将在本章稍晚些时候检查 `sed` 编辑器使用的一些基础命令，然后在第 20 章查看一些更高级的命令。

### 在命令行中定义编辑器命令

默认情况下，`sed` 编辑器将指定的命令应用到 `STDIN` 输入流。这允许你直接将数据管道到 `sed` 编辑器进行处理。这里有一个演示如何操作的快速示例：

```
$ echo "This is a test" | sed 's/test/big test/'
This is a big test
$
```

此示例使用了 `sed` 编辑器中的 `s` 命令。`s` 命令将正斜杠之间指定的第一个文本字符串模式替换为第二个文本字符串。在这个示例中，单词 `big test` 替换了单词 `test`。

当你运行这个示例时，结果应该几乎瞬间显示。这就是使用 `sed` 编辑器的威力所在。你可以在仅启动某些交互式编辑器所需花费的大致相同的时间内，对数据进行多次编辑。

当然，这个简单的测试只编辑了一行数据。在编辑完整的数据文件时，你应该也会得到同样快速的结果：

```
$ cat data1
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
$ sed 's/dog/cat/' data1
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
$
```

`sed` 命令执行并几乎瞬间返回数据。在处理每行数据时，结果就会显示出来。在 `sed` 编辑器完成整个文件的处理之前，你就开始看到结果。

需要注意的是，`sed` 编辑器不会修改文本文件本身的数据。它只将修改后的文本发送到 `STDOUT`。如果你查看文本文件，它仍然包含原始数据：

```
$ cat data1
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
```

### 在命令行中使用多个编辑器命令

若要从 `sed` 命令行执行多个命令，只需使用 `-e` 选项。



使用`sed`编辑器执行替换命令：

```
$ sed -e 's/brown/green/; s/dog/cat/' data1
The quick green fox jumps over the lazy cat.
The quick green fox jumps over the lazy cat.
The quick green fox jumps over the lazy cat.
The quick green fox jumps over the lazy cat.
$
```

两个命令都应用到文件中的每行数据。命令必须用分号分隔，且命令结束与分号之间不应有空格。

与其使用分号来分隔命令，你可以使用`bash` shell中的次级提示符。只需输入第一个单引号来开启脚本，`bash`就会继续提示你输入更多命令，直到你输入结束单引号：

```bash
$ sed -e '
> s/brown/green/
> s/fox/elephant/
> s/dog/cat/' data1
The quick green elephant jumps over the lazy cat.
The quick green elephant jumps over the lazy cat.
The quick green elephant jumps over the lazy cat.
The quick green elephant jumps over the lazy cat.
$
```

你必须记住在闭合单引号出现的同一行上完成命令。一旦`bash` shell检测到闭合单引号，它就会处理该命令。一旦开始执行，`sed`命令就会将你指定的每个命令应用到文本文件的每一行数据。

## 从文件中读取编辑器命令

最后，如果你有很多`sed`命令需要处理，通常将它们存储在单独的文件中会更简单。使用`-f`选项在`sed`命令中指定文件：

```bash
$ cat script1
s/brown/green/
s/fox/elephant/
s/dog/cat/
$
$ sed -f script1 data1
The quick green elephant jumps over the lazy cat.
The quick green elephant jumps over the lazy cat.
The quick green elephant jumps over the lazy cat.
The quick green elephant jumps over the lazy cat.
$
```

在这种情况下，你不需要在每个命令后加分号。`sed`编辑器知道每行都包含一个独立的命令。与在命令行上输入命令一样，`sed`编辑器从指定文件中读取命令，并将它们应用到数据文件的每一行。

我们将在"`sed`编辑器基础"部分中查看其他一些`sed`编辑器命令，这些命令在处理数据时非常有用。在此之前，让我们快速查看另一个Linux数据编辑器。

## The gawk 程序

虽然`sed`编辑器是即时修改文本文件的有用工具，但它也有其局限性。通常你需要一个更高级的工具来处理文件中的数据，一个能够提供更像编程环境的环境，允许你修改和重组文件中的数据。这就是`gawk`大显身手的地方。

`gawk`程序是Unix中原始`awk`程序的GNU版本。`gawk`程序通过提供编程语言而非仅仅是编辑器命令，将流编辑推向了更深一步。在`gawk`编程语言中，你可以：

* 定义变量来存储数据。
* 使用算术和字符串操作符对数据进行操作。
* 使用结构化编程概念（如`if-then`语句和循环）为你的数据处理添加逻辑。
* 通过提取数据文件中的数据元素并以另一种顺序重新定位，生成格式化报告。

`gawk`程序的报告生成能力通常用于从大型文本文件中提取数据元素，并将其格式化为可读的报告。一个完美的例子就是格式化日志文件。试图仔细查看日志文件的每一行可能会困难。`gawk`程序允许你从日志文件中过滤出你所需的数据元素，然后以更容易阅读重要数据的方式进行格式化。

### gawk 命令格式

`gawk`程序的基本格式如下：

`gawk options file`

表18.2显示了`gawk`程序提供的选项。

### gawk 选项

| 选项 | 说明 |
| :--- | :--- |
| `-F fs` | 指定用于界定行数据字段的文件分隔符。 |
| `-f file` | 指定要读取程序的文件。 |
| `-v var=value` | 定义`gawk`程序中使用的变量和默认值。 |
| `-mf N` | 指定处理的最大字段数。 |
| `-mr N` | 指定数据文件中最大的记录大小。 |
| `-W keyword` | 为`gawk`指定兼容模式或警告级别。 |

命令行选项提供了一种用于自定义`gawk`程序功能的简单方法。在探索`gawk`的过程中，我们将更深入地查看这些内容。`gawk`的威力在于程序脚本。你可以编写脚本来读取文本行内的数据，然后处理并显示这些数据，以创建任何类型的输出。

### 从命令行读取程序脚本

`gawk`程序脚本通过大括号的开启和关闭来定义。你必须将脚本命令放在两个大括号之间。由于`gawk`命令行假设脚本是一个字符串，因此你还必须将脚本封装在引号中。以下是在命令行上指定简单`gawk`程序的示例：

```bash
$ gawk '{print "Hello John!"}'
```

程序脚本定义了一个单独的命令：`print`命令。`print`命令的作用正如其名：它将文本打印到`STDOUT`。如果你尝试运行此命令，你可能会有些失望，因为立即不会发生任何事情。因为命令行中没有定义文件名，`gawk`程序从`STDIN`获取数据。当你运行程序时，它只是在等待通过`STDIN`输入文本。

如果你输入一行文本并按回车键，`gawk`就会通过程序脚本运行文本：

```bash
$ gawk '{print "Hello John!"}'
This is a test
Hello John!
hello
Hello John!
This is another test
Hello John!
$
```

与`sed`编辑器一样，`gawk`程序会对数据流中的每行文本执行程序脚本。由于程序脚本被设置为显示固定的文本字符串，无论你在数据流中输入什么文本，你都会得到相同的文本输出。要终止`gawk`程序，你必须信号数据流已结束。`bash` shell提供了一个组合键来生成文件结束（EOF）字符。`Ctrl+D`键组合在`bash`中生成一个EOF字符。使用该键组合可以终止`gawk`程序并返回命令界面提示符。

### 使用数据字段变量

`gawk`的主要功能之一是处理文本文件中数据的能力。它通过自动为行中的每个数据元素分配变量来实现。默认情况下，`gawk`为在文本行中检测到的每个数据字段分配以下变量：

* `$0`代表整行文本。
* `$1`代表文本行中的第一个数据字段。
* `$2`代表文本行中的第二个数据字段。
* `$n`代表文本行的第`n`个数据字段。

文本中的每个数据字段是通过字段分隔符确定的。当`gawk`读取文本时，它使用定义的字段分隔符界定每个数据字段。`gawk`的默认字段分隔符是任何空白字符（例如制表符或空格字符）。

以下是一个`gawk`程序示例，它读取文本文件并仅显示第一个数据字段值：

```bash
$ cat data3
One line of test text.
Two lines of test text.
Three lines of test text.
$
$ gawk '{print $1}' data3
One
Two
Three
$
```

该程序使用字段变量`$1`显示每行文本的第一个数据字段。如果你正在读取使用不同字段分隔符的文件，可以使用`-F`选项来指定它：

```bash
$ gawk -F: '{print $1}' /etc/passwd
root
daemon
bin
sys
sync
games
man
lp
mail
...
```

这个短程序显示了系统密码文件的第一个数据字段。因为`/etc/passwd`文件使用冒号分隔数据字段，如果你想分离出每个数据元素，必须在`gawk`选项中将其指定为字段分隔符。

## 在程序脚本中使用多个命令

如果一个编程语言只能执行一条命令，那么它将非常没有用处。`gawk`编程语言允许你将多个命令组合成一个普通的程序。要在命令行指定的程序脚本中使用多个命令，只需在每个命令之间放置一个分号即可：

```bash
$ echo "My name is Rich" | gawk '{$4="Christine"; print $0}'
My name is Christine
$
```

第一个命令为`$4`字段变量赋值了一个值。第二个命令随后打印整个数据字段。从输出中可以看出，`gawk`程序将原始文本中的第四个数据字段替换为了新值。

你还可以使用次级提示符（secondary prompt）逐行输入你的程序脚本命令：

```bash
$ gawk '{
> $4="testing"
> print $0 }'
This is not a good test.
This is not testing good test.
$
```

打开单引号后，`bash` shell会提供次级提示符来提示你输入更多数据。你可以逐行添加命令，直到你输入闭合的单引号为止。要退出程序，只需按下`Ctrl+D`组合键来发送数据结束信号。

### 从文件中读取程序

与`sed`编辑器一样，`gawk`编辑器允许你将程序存储在文件中并在命令行引用它们：

```bash
$ cat script2
{ print $1 "'s home directory is " $6 }
$
$ gawk -F: -f script2 /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
...
Samantha's home directory is /home/Samantha
Timothy's home directory is /home/Timothy
Christine's home directory is /home/Christine
$
```

`script2`程序脚本再次使用`print`命令来打印`/etc/passwd`文件的家目录数据字段（字段变量`$6`）和用户ID数据字段（字段变量`$1`）。

你可以在程序文件中指定多个命令。要这样做，只需将每个命令放在单独的一行即可。不需要使用分号：

```bash
$ cat script3
{
text = "'s home directory is "
print $1 text $6
}
$
$ gawk -F: -f script3 /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
...
Samantha's home directory is /home/Samantha
Timothy's home directory is /home/Timothy
Christine's home directory is /home/Christine
$
```

`script3`程序脚本定义了一个变量来存储`print`命令中使用的文本字符串。你会发现，`gawk`程序在引用变量值时并不像shell脚本那样使用美元符号。

### 在处理数据之前运行脚本

`gawk`程序还允许你指定程序脚本运行的机制。默认情况下，`gawk`会从输入中读取一行文本，然后对该行文本中的数据执行程序脚本。有时，你可能需要在处理数据之前运行脚本，例如为报告创建一个表头部分。`BEGIN`关键字用于实现这一点。它强制`gawk`在读取数据之前，执行`BEGIN`关键字之后指定的程序脚本：

```bash
$ gawk 'BEGIN {print "Hello World!"}'
Hello World!
$
```

这一次，`print`命令在读取任何数据之前显示了文本。然而，在显示文本后，它会迅速退出，而不会等待任何数据。

这是因为`BEGIN`关键字仅在处理任何数据之前应用于指定的脚本。如果你想用普通的程序脚本处理数据，你必须使用另一个脚本部分定义程序：

```bash
$ cat data4
Line 1
Line 2
Line 3
$
$ gawk 'BEGIN { print "The data4 File Contents:" } { print $0 }' data4
The data4 File Contents:
Line 1
Line 2
Line 3
$
```

现在，在`gawk`执行`BEGIN`脚本之后，它会使用第二个脚本来处理任何文件数据。这样做时要小心——注意两个脚本在`gawk`命令行上仍然被视为一个文本字符串。你需要相应地放置单引号。

### 在处理数据之后运行脚本

与`BEGIN`关键字一样，`END`关键字允许你指定一个`gawk`在读取数据后执行的程序脚本：

```bash
$ gawk 'BEGIN { print "The data4 File Contents:" } { print $0 } END { print "End of File" }' data4
The data4 File Contents:
Line 1
Line 2
Line 3
End of File
$
```

当`gawk`程序完成打印文件内容后，它会执行`END`脚本中的命令。这是一个非常好的技巧，可以在处理所有普通数据后为报告添加页脚数据。

你可以将所有元素组合成一个良好的程序脚本文件，以便从简单的数据文件中创建一个完整的报告：

```bash
$ cat script4
BEGIN {
print "The latest list of users and shells"
print " Userid       Shell"
print "--------      -------"
FS=":"
}
{
print $1      "" $7
}
END {
print "This concludes the listing"
}
$
```

该脚本使用`BEGIN`脚本为报告创建表头。它还定义了一个名为`FS`的特殊变量。这是定义字段分隔符的另一种方法。这样，你就不需要依赖脚本的用户在命令行选项中定义字段分隔符了。

以下是运行此`gawk`程序脚本的某些截断的输出：

```bash
$ gawk -f script4 /etc/passwd
The latest list of users and shells
 Userid       Shell
--------      -------
root        /bin/bash
daemon      /bin/sh
bin         /bin/sh
...
Samantha    /bin/bash
Timothy     /bin/sh
Christine    /bin/sh
This concludes the listing
$
```

正如预期的，`BEGIN`脚本创建了头部，程序脚本处理了来自`/etc/passwd`的信息，`END`脚本产生了脚注。这让你初步体验到了使用`gawk`脚本的威力。

### sed 基础

成功使用`sed`编辑器的关键在于了解它的命令和格式，这些可以帮助你自定义文本。本节介绍了你可以包含在脚本中开始使用`sed`的基础命令。

### 替换选项

你已经看到了如何使用`s`命令替换行中的文本。然而，`substitute`命令还有一些额外的选项，可以让你的工作更轻松。

### 替换标记

`substitute`命令在替换字符串中的匹配模式时有一个注意事项。观察这个例子发生了什么：

```bash
$ cat data5
This is a test of the test script.
This is the second test of the test script.
$
$ sed 's/test/trial/' data5
This is a trial of the test script.
This is the second trial of the test script.
$
```

`substitute`命令在替换多行文本方面运行良好，但默认情况下，它只替换每行中的第一次出现。要让`substitute`命令处理不同的出现位置，你必须使用替换标记。替换标记设置在替换命令字符串之后：

`s/pattern/replacement/flags`

共有四种替换标记可用：

- 数字，指示要替换新文本的模式出现次数。
- `g`——表示对现有文本的所有出现处都进行新文本。
- `p`——表示打印原始行的内容。
- `w`文件——将替换结果写入文件。

在第一种替换类型中，你可以指定`sed`编辑器为匹配模式的哪一次替换新文本：

```bash
$ sed 's/test/trial/2' data5
This is a test of the trial script.
This is the second test of the trial script.
$
```

由于指定了`2`作为替换标志，`sed`编辑器只会替换每行中第二次出现的模式。`g`替换标志允许你替换文本中该模式的每一次出现：

```bash
$ sed 's/test/trial/g' data5
This is a trial of the trial script.
This is the second trial of the trial script.
$
```

`p`替换标志会在替换命令中打印包含匹配模式的行。这通常与`-n sed`选项配合使用。



```bash
$ cat data6
This is a test line.
This is a different line.
$

$ sed -n 's/test/trial/p' data5
This is a trial line.
$
```

`-n` 选项会抑制 `sed` 编辑器的输出。然而，`p` 替换标志会输出任何被修改过的行。两者结合使用时，只会输出被替换命令修改过的行。

`w` 替换标志产生相同的输出，但会将输出存储在指定的文件中：

```bash
$ sed 's/test/trial/w test' data6
This is a trial line.
This is a different line.
$

$ cat test
This is a trial line.
$
```

`sed` 编辑器的普通输出显示在 `STDOUT` 中，但只有包含匹配模式的行会被存储在指定的输出文件中。

## 替换字符

有时会在文本字符串中遇到在替换模式中不易使用的字符。Linux 世界中一个常见的例子就是正斜杠 `/`。

在文件中替换路径名可能会变得很笨拙。例如，如果你想将 `/etc/passwd` 文件中的 bash shell 替换为 c shell，你必须这样操作：

```bash
$ sed 's/\/bin\/bash/\/bin\/csh/' /etc/passwd
```

由于正斜杠被用作字符串分隔符，如果它出现在模式文本中，你必须使用反斜杠来对其进行转义。这通常会导致混淆和错误。

为了解决这个问题，`sed` 编辑器允许你在替换命令中选择不同的字符作为字符串分隔符：

```bash
$ sed 's!/bin/bash!/bin/csh!' /etc/passwd
```

在这个示例中，感叹号 `!` 被用作字符串分隔符，使得路径名更易阅读和理解。

## 使用地址

默认情况下，你在 `sed` 编辑器中使用的命令适用于文本数据的所有行。如果你只想对特定的行或一组行应用命令，则必须使用行地址（line addressing）。

`sed` 编辑器中有两种行地址的格式：

- 数字行范围
- 用于过滤掉某行的文本模式

这两种形式都使用相同的格式来指定地址：

`[address]command`

你还可以为特定地址将多个命令组合在一起：

```bash
address {
    command1
    command2
    command3
}
```

`sed` 编辑器将你指定的每个命令仅应用于匹配指定地址的行。本节演示了如何在你的 `sed` 脚本中同时使用这两种地址技术。

### 数字行地址

使用数字行地址时，你通过行在文本流中的位置来引用行。`sed` 编辑器将文本流中的第一行分配为行号 1，并对每个新行顺序递增。

你在命令中指定的地址可以是单个行号，也可以是由起始行号、逗号和结束行号指定的行范围。这里有一个指定应用 `sed` 命令的行号的示例：

```bash
$ sed '2s/dog/cat/' data1
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
$
```

`sed` 编辑器根据指定的地址仅修改了第二行的文本。这是另一个示例，这次使用了行地址范围：

```bash
$ sed '2,3s/dog/cat/' data1
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy dog
$
```

如果你想对从文本中某处开始但持续到文本结束的一组行应用命令，你可以使用特殊地址——美元符号 `$`：

```bash
$ sed '2,$s/dog/cat/' data1
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy cat
The quick brown fox jumps over the lazy cat
$
```

由于你可能不知道文本中有多少行数据，美元符号通常非常有用。

### 使用文本模式过滤器

限制命令应用行的另一种方法要稍微复杂一些。`sed` 编辑器允许你指定一个文本模式，并用于过滤命令的行。其格式为：

`/pattern/command`

你必须将指定的模式封装在正斜杠中。`sed` 编辑器仅对包含你指定的文本模式的行应用命令。

例如，如果你只想为用户 Samantha 更改默认 shell，你会使用 `sed` 命令：

```bash
$ grep Samantha /etc/passwd
Samantha:x:1001:1002:Samantha,4,,:/home/Samantha:/bin/bash
$

$ sed '/Samantha/s/bash/csh/' /etc/passwd
root:x:0:0:root:/root:/bin/bash
...
Samantha:x:1001:1002:Samantha,4,,:/home/Samantha:/bin/csh
Timothy:x:1002:1005::/home/Timothy:/bin/sh
Christine:x:1003:1006::/home/Christine:/bin/sh
$
```

该命令仅应用于具有匹配文本模式的行。虽然使用固定文本模式对于过滤特定值（如 `userid` 示例）可能有用，但它的功能范围相当有限。`sed` 编辑器在文本模式中使用了一种名为“正则表达式”（regular expressions）的特性，允许你创建非常复杂的模式。

正则表达式允许你创建高级的文本模式匹配公式来匹配各种数据。这些公式结合了一系列通配符、特殊字符和固定文本字符，产生一个可以匹配任何文本的简洁模式。正则表达式是 shell 编程中令人生畏的部分之一，第 19 章将非常详细地介绍它们。

### 命令分组

如果你需要在单行上执行多个命令，请使用大括号 `{}` 将命令组合起来。`sed` 编辑器将处理地址行上列出的每个命令：

```bash
$ sed '2{
    s/fox/elephant/
    s/dog/cat/
}' data1
The quick brown fox jumps over the lazy dog
The quick brown elephant jumps over the lazy cat
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
$
```

两个命令都会针对该地址进行处理。当然，你也可以在分组命令之前指定一个地址范围：

```bash
$ sed '3,${
    s/brown/green/
    s/lazy/active/
}' data1
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick green fox jumps over the active dog
The quick green fox jumps over the active dog
$
```

`sed` 编辑器将所有命令应用于地址范围内的所有行。

## 删除行

文本替换命令并不是 `sed` 编辑器中唯一的可用命令。如果你需要删除文本流中的特定文本行，有一个 `delete` 命令。

`delete` 命令 `d` 的作用顾如其名。它将删除任何匹配所提供的地址方案的文本行。使用 `delete` 命令要小心，因为如果你忘记包含地址方案，流中的所有行都将被删除：

```bash
$ cat data1
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
$ sed 'd' data1
$
```

`delete` 命令在与指定的地址结合使用时显然是最有用的。这允许你从数据流中删除特定的文本行，可以通过行号：

```bash
$ sed '3d' data7
This is line number 1.
This is line number 2.
This is line number 4.
$
```

或者通过特定的行范围：

```bash
$ sed '2,3d' data7
This is line number 1.
This is line number 4.
$
```

或者使用特殊的结束符字符：

```bash
$ sed '3,$d' data7
This is line number 1.
This is line number 2.
$
```

`sed` 编辑器的模式匹配功能也适用于 `delete` 命令：

```bash
$ sed '/number 1/d' data7
This is line number 2.
This is line number 3.
This is line number 4.
$
```

`sed` 编辑器会删除包含你指定的模式文本的行。

> **注意**
>
> 请记住，`sed` 编辑器不会修改原始文件。你删除的任何行只会从 `sed` 编辑器的输出中消失。原始文件仍然包含这些“已删除”的行。

你也可以使用两个文本模式来删除范围，但这样做时要小心。你指定的第一个模式会“开启”行删除，而第二个模式会“关闭”行删除。`sed` 编辑器会删除两个指定行之间的任何行（包括指定的行）：

```bash
$ sed '/1/,/3/d' data6
This is line number 4.
$
```

此外，你需要加小心，因为每当 `sed` 编辑器在数据流中检测到起始模式，删除功能就会“开启”。这可能会产生意想不到的结果：

```bash
$ cat data8
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is line number 1 again.
This is text you want to keep.
This is the last line in the file.
$

$ sed '/1/,/3/d' data7
This is line number 4.
$
```

包含数字 1 的行的第二次出现再次触发了 `delete` 命令，删除了数据流中的剩余所有行，因为停止模式没有被识别。当然，如果你指定的停止模式在文本中从未出现过，就会发生另一个明显的问题：

```bash
$ sed '/1/,/5/d' data8
$
```

由于删除功能在第一次模式匹配时已“开启”，但从未找到结束模式匹配，整个数据流都被删除了。

## 插入和追加文本

正如你预期的，像任何其他编辑器一样，`sed` 编辑器允许你向数据流插入和追加文本行。这两个操作之间的区别可能会令人困惑：

- `insert` 命令（`i`）在指定行之前添加一个新行。
- `append` 命令（`a`）在指定行之后添加一个新行。

这两个命令令人困惑的地方在于它们的格式。你不能在单行命令行上使用这些命令。你必须单独另起一行指定要插入或追加的行。此操作格式为：

```bash
sed '[[address]]command\
new line'
```

`new line` 中的文本会出现在你指定的 `sed` 编辑器输出位置。记住，当你使用 `insert` 命令时，文本出现在数据流文本之前：

```bash
$ echo "Test Line 2" | sed 'i\Test Line 1'
Test Line 1
Test Line 2
$
```

当你使用 `append` 命令时，文本出现在数据流文本之后：

```bash
$ echo "Test Line 2" | sed 'a\Test Line 1'
Test Line 2
Test Line 1
$
```

当你从命令行界面提示符使用 `sed` 编辑器时，你会收到输入新行数据的辅助提示。你必须在这一行完成 `sed` 编辑器命令。一旦你输入结束的单引号，bash shell 就会处理该命令：

```bash
$ echo "Test Line 2" | sed 'i\
> Test Line 1'
Test Line 1
Test Line 2
$
```

这对于在数据流文本之前或之后添加文本非常有效，但在数据流内部添加文本呢？

要在数据流行内部插入或追加数据，你必须使用地址来告诉 `sed` 编辑器你想让数据出现在哪里。在使用这些命令时，你只能指定单行地址。你可以匹配行号或文本模式，但不能使用地址范围。这是符合逻辑的，因为你只能在单行之前或之后插入或追加，而不能针对范围。

以下是在数据流第 3 行之前插入新行的示例：

```bash
$ sed '3i\
> This is an inserted line.' data7
This is line number 1.
This is line number 2.
This is an inserted line.
This is line number 3.
This is line number 4.
$
```

以下是在数据流第 3 行之后追加新行的示例：

```bash
$ sed '3a\
> This is an appended line.' data7
This is line number 1.
This is line number 2.
This is line number 3.
This is an appended line.
This is line number 4.
$
```

这使用的过程与 `insert` 命令相同；它只是新文本行放置在指定的行号之后。如果你有一个多行数据流，并想在数据流末尾追加新行文本，只需使用美元符号，它代表最后一行数据：

```bash
$ sed '$a\
> This is a new line of text.' data7
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is a new line of text.
$
```

如果你想在数据流开头添加新行，也适用相同的原理。要插入或追加多行文本，你必须在每一行都使用反斜杠，直到你想插入或追加的最后一行：

```bash
$ sed '1i\
> This is one line\
> This is another line.' data7
This is one line.
This is another line.
This is line number 1.
This is line number 2.
This is another line.
```

## 修改行

`change` 命令允许你修改整行的内容。它的工作方式与 `insert` 和 `append` 命令相同，即你必须将新行与 `sed` 命令分开指定：

```bash
$ sed '3c\
> This is a changed line.' data7
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

在这个示例中，`sed` 编辑器修改了第 3 行的文本。你也可以使用文本模式作为地址：

```bash
$ sed '/number 3/c\
> This is a changed line.' data7
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

文本模式 `change` 命令会修改数据流中匹配的任何行：

```bash
$ sed '/number 1/c\
> This is a changed line.' data8
This is a changed line.
This is line number 2.
This is line number 3.
This is line number 4.
This is a changed line.
This is another line.
This is the last line in the file.
$
```

你可以在 `change` 命令中使用地址范围，但结果可能不是你所预期的：

```bash
$ sed '2,3c\
> This is a new line of text.' data7
This is line number 1.
This is a new line of text.
This is line number 4.
$
```

`sed` 编辑器并没有修改这两行，而是使用单行文本来替换这两行。

## `transform` 命令

`transform` 命令（`y`）是 `sed` 编辑器中唯一针对单个字符的命令。`transform` 命令使用的格式为：



`[address]y/inchars/outchars/`

`transform` 命令执行`inchars`和`outchars`值之间一对一的映射。`inchars`中的第一个字符被转换为`outchars`中的第一个字符。`inchars`中的第二个字符被转换为`outchars`中的第二个字符。这种映射一直持续到指定字符的长度。如果`inchars`和`outchars`的长度不同，`sed`编辑器将产生错误信息。

使用`transform`命令的一个简单示例是：

```bash
$ sed 'y/123/789/' data8
This is line number 7.
This is line number 8.
This is line number 9.
This is line number 4.
This is line number 7 again.
This is yet another line.
This is the last line in the file.
$
```

从输出中可以看出，`inchars`模式中指定字符的每个实例都被替换为`outchars`模式中相同位置的字符。

`transform`命令是一个全局命令；也就是说，它会自动对文本行中找到的任何字符进行转换，而不考虑其出现的次数：

```bash
$ echo "This 1 is a test of 1 try." | sed 'y/123/456/'
This 4 is a test of 4 try.
$
```

`sed`编辑器转换了文本行中两个匹配的字符 1。你无法将转换限制为字符的特定出现次数。

# 打印回顾

“更多替换选项”部分向你展示了如何在替换命令中使用`p`标志来显示`sed`编辑器更改的行。还有三个命令也可以用于从数据流中打印信息：

- 小写`p`命令，用于打印文本行
- 等号（`=`）命令，用于打印行号
- `l`（小写 L）命令，用于列出一行

接下来的章节将查看`sed`编辑器中这三个打印命令的每一个。

## 打印行

与`substitution`命令中的`p`标志一样，`p`命令在`sed`编辑器的输出中打印一行。单单独使用它时并没什么特别的：

```bash
$ echo "this is a test" | sed 'p'
this is a test
this is a test
$
```

它所做的只是打印你已经知道存在的数据文本。`print`命令最常用的用途是打印包含来自文本模式匹配文本的行：

```bash
$ sed -n '/number 3/p' data7
This is line number 3.
$
```

通过在命令行上使用`-n`选项，你可以抑制所有其他行，只打印包含匹配文本模式的行。

你也可以将此作为快速打印数据流中部分行集的方法：

```bash
$ sed -n '2,3p' data7
This is line number 2.
This is line number 3.
$
```

当你需要在行被修改之前查看它时（例如使用`substitution`或`change`命令），你也可以使用`print`命令。你可以创建一个在更改前显示该行的脚本：

```bash
$ sed -n '/3/{
p
s/line/test/p
}' data7
This is line number 3.
This is test number 3.
$
```

此`sed`编辑器命令搜索包含数字 3 的行，然后执行两个命令。首先，脚本使用`p`命令打印行的原始版本；然后它使用`s`命令替换文本，并带有`p`标志打印结果文本。输出显示了原始行文本和新行文本。

## 打印行号

`equal sign`命令用于打印数据流中当前行的行号。行号是通过通过使用数据流中的换行符来确定的。每当数据流中出现换行符时，`sed`编辑器就会认为它结束了一行文本：

```bash
$ sed = data1
1
The quick brown fox jumps over the lazy dog.
2
The quick brown fox jumps over the lazy dog.
3
The quick brown fox jumps over the lazy dog.
4
The quick brown fox jumps over the lazy dog.
$
```

`sed`编辑器在实际的文本行之前打印行号。如果你在数据流中搜索特定的文本模式，`equal sign`命令就会非常有用：

```bash
$ sed -n '/number 4/{
=
p
}' data7
4
This is line number 4.
$
```

通过使用`-n`选项，你可以让`sed`编辑器仅显示包含匹配文本模式的行的行号和文本。

## 列行

`list`命令（`l`）允许你打印数据流中的文本和不可打印的 ASCII 字符。任何不可打印字符都使用其八进制值（前反斜杠）或常用不可打印字符的标准 C 风格命名法（例如用于制表符的`\t`）显示：

```bash
$ cat data9
This     line      tabs.
$
$ sed -n 'l' data9
This\tline\tcontains\ttabs.$
$
```

制表符的位置使用`\t`命名显示。行尾的美元符号表示换行符。如果你有一个包含转义字符的数据流，`list`命令将使用八进制代码显示它：

```bash
$ cat data10
This line contains an escape character
$
$ sed -n 'l' data10
This line contains an escape character \033[44m$
$
```

`data10`文本文件包含一个更改显示颜色的转义控制代码（见第 17 章）。当你使用`cat`命令显示文本时，你看不到转义代码。然而，使用`list`命令，你可以看到。`033`是转义的八进制值。

# 使用 sed 操作文件

`substitution`命令包含允许你处理文件的标志。

## 写入文件

`w`命令用于写入文件。`w`的格式为：

`[address]w filename`

`filename`参数可以是相对或绝对路径，在任何情况下，运行`sed`的人员必须具有写入权限。地址可以是任何类型的`sed`地址，例如：

```bash
$ sed '1,2w test' data7
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
$
$ cat test
This is line number 1.
This is line number 2.
$
```

当然，如果你希望这些行显示在`STDOUT`上，可以使用`sed`的`-n`选项。如果你需要从主文件创建一个数据文件，这是一个非常棒的工具，例如：

```bash
$ cat data11
Blum, Katie, Chicago, IL
Mullen, Riley, West Lafayette, IN
Snell, Haley, Ft. Wayne, IN
Woenker, Matthew, Springfield, IL
Wisecarver, Emma, Grant Park, IL
$
$ sed -n '/IN/w INcustomers' data11
$
$ cat INcustomers
Mullen, Riley, West Lafayette, IN
Snell, Haley, Ft. Wayne, IN
$
```

`sed`编辑器将包含文本模式的数据行写入目标文件。

## 从文件读取数据

你已经见过如何从`sed`命令行向数据流插入和追加文本。`read`命令（`r`）允许你插入单独文件中的数据。

`read`命令的格式为：

`[address]r filename`

`filename`参数指定包含数据的绝对或相对路径。你不能为`read`命令使用地址范围。你只能指定单个行号或文本模式地址。`sed`编辑器会在地址之后插入文件的文本。

```bash
$ cat data12
This is an added line.
This is the second added line.
$
$ sed '3r data12' data7
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
$
```

```text
这是第 3 行。
这是一条添加的行。
这是第二个添加的行。
这是第 4 行。
$
```

`sed`编辑器会将数据文件中所有的文本行插入到数据流中。在使用文本模式地址时，该技术同样适用：

```bash
$ sed ‘number 2/r data12’ data7
```

这是第 1 行。

这是第 2 行。

这是一条添加的行。

这是第二个添加的行。

这是第 3 行。

这是第 4 行。

$

如果你想在数据流的末尾添加文本，只需使用美元符号地址符号即可：

```bash
$ sed ‘$r data12’ data7
```

这是第 1 行。

这是第 2 行。

这是第 3 行。

这是第 4 行。

这是一条添加的行。

这是第二个添加的行。

$

`read`命令的一个很酷的用法是将其与`delete`命令结合使用，将文件中的占位符替换为另一个文件的数据。例如，假设你有一个存储在文本文件中的格式信函，内容如下：

```bash
$ cat letter
```

是否是以下人员：

LIST

请前往办公室。

$

该格式信函使用了通用的占位符`LIST`来代替人员列表。要在占位符之后插入人员列表，你只需要使用`read`命令。然而，这在输出中仍然保留了该占位符文本。要删除它，只需使用`delete`命令。结果如下所示：

```bash
$ sed ‘/LIST/{
> r data11
> d
>}’ letter
```

是否是以下人员：

Blum, Katie      Chicago, IL

Mullen, Riley    West Lafayette, IN

Snell, Haley      Ft. Wayne, IN

Woenker, Matthew      Springfield, IL

Wisecarver, Emma      Grant Park, IL

请前往办公室。

$

现在，占位符文本已被替换为数据文件中的姓名列表。

## 总结

虽然 shell 脚本可以独立完成很多工作，但仅通过 shell 脚本处理数据通常很困难。Linux 提供了两个实用的工具来帮助处理文本数据。`sed`编辑器是一个流编辑器，它可以在读取数据时快速地进行处理。你必须为`sed`编辑器提供一组编辑命令，由它将其应用于数据。

`gawk`程序是 GNU 组织的一个工具，它模仿并扩展了 Unix `awk`程序的功能。`gawk`程序包含一种内置编程语言，你可以用它编写脚本来处理和分析数据。你可以使用`gawk`程序从大型数据文件中提取数据元素，并以你所需的几乎任何格式输出它们。这使得处理大型日志文件变得轻而易举，也可以从数据文件中创建自定义报告。

使用`sed`和`gawk`程序的一个关键要素是学会使用正则表达式。正则表达式是创建自定义过滤器以提取和操作文本文件中数据的关键。本章将探讨经常被误解的正则表达式世界，向你展示如何构建处理所有类型数据的正则表达式。

# 第 19 章：正则表达式

## 本章内容

- 定义正则表达式
- 基础知识
- 扩展我们的模式
- 创建表达式

在 shell 脚本中成功使用`sed`编辑器和`gawk`程序的关键在于你对正则表达式的熟练程度。这并不总是易事，因为试图从大量数据中过滤特定数据可能会（而且通常确实）变得复杂。本章描述了如何在`sed`编辑器和`gawk`程序中创建正则表达式，以过滤出你所需的数据。

## 什么是正则表达式？

理解正则表达式的第一步是准确定义它们到底是什么。本节解释了什么是正则表达式，并描述了 Linux 如何使用正则表达式。

定义

正则表达式是你定义的模式模板，Linux 工具使用它来过滤文本。Linux 工具（如`sed`编辑器或`gawk`程序）在数据流入工具时，会将正则表达式模式与数据进行匹配。如果数据匹配模式，则被接受处理。如果数据不匹配模式，则被拒绝。这在图 19.1 中所示。

[图 19.1] 数据与正则表达式模式匹配

![](img/00044.jpg)

正则表达式模式利用通配符字符来表示数据流中的一个或多个字符。在 Linux 中有许多地方你可以指定通配符字符来表示你未知的数据。你已经见过在 Linux `ls`命令中使用通配符来列出文件和目录的示例（参见第 3 章）。

星号通配符字符允许你仅列出符合特定标准的文件。例如：

```bash
$ ls -al da*
-rw-r--r--  1 rich      rich              45 Nov 26 12:42 data
-rw-r--r--  1 rich      rich              25 Dec  4 12:40 data.tst
-rw-r--r--  1 rich      rich              180 Nov 26 12:42 data1
-rw-r--r--  1 rich      rich              45 Nov 26 12:42 data2
-rw-r--r--  1 rich      rich              73 Nov 27 12:31 data3
-rw-r--r--  1 rich      rich              79 Nov 28 14:01 data4
-rw-r--r--  1 rich      rich              187 Dec  4 09:45 datest
$
```

`da*`参数指示`ls`命令仅列出以`da`开头的文件。文件名中`da`之后可以是任意数量的字符（包括没有）。`ls`命令读取目录中所有文件的信息，但只显示匹配通配符的文件。

正则表达式模式的工作原理类似。正则表达式模式包含文本或特殊字符，为`sed`编辑器和`gawk`程序在匹配数据时遵循的模板。可以在正则表达式中使用不同的特殊字符来定义过滤数据的模式。

### 正则表达式的类型

使用正则表达式最大的问题是并没有某一套标准。Linux 环境中的许多不同的应用程序使用不同类型的正则表达式。这些包括多样化的应用程序，如编程语言（Java, Perl 和 Python）、Linux 工具（如`sed`编辑器、`gawk`程序和`grep`工具）以及主流应用程序（如 MySQL 和 PostgreSQL 数据库服务器）。

正则表达式是通过正则表达式引擎实现的。正则表达式引擎是解释正则表达式模式并使用这些模式匹配文本的底层软件。

在 Linux 世界，有两种常用的正则表达式引擎：

- POSIX 基础正则表达式 (BRE) 引擎
- POSIX 扩展正则表达式 (ERE) 引擎

大多数 Linux 工具至少符合 POSIX BRE 引擎规范，识别它定义的所有模式符号。遗憾的是，某些工具（如`sed`编辑器）仅符合 BRE 引擎规范的子集。这是由于速度限制，因为`sed`编辑器试图尽可能快地处理数据流中的文本。

POSIX ERE 引擎通常出现在依赖正则表达式进行文本过滤的编程语言中。它提供了高级模式符号，以及用于常见模式的特殊符号，例如匹配数字、单词和字母数字字符。`gawk`程序使用 ERE 引擎来处理其正则表达式模式。

由于实现正则表达式有许多不同的方法，很难对所有可能的正则表达式给出一个单一且简洁的描述。接下来的章节将讨论最常见的正则表达式，并演示如何在`sed`编辑器和`gawk`程序中使用它们。

## 定义 BRE 模式

最基本的 BRE（基本正则表达式）模式是匹配数据流中的文本字符。本节将演示你如何在正则表达式模式中定义文本，以及你预期会得到什么样的结果。

### 普通文本

第 18 章演示了如何在`sed`编辑器和`gawk`程序中使用标准文本字符串来过滤数据。这里有一个示例可以帮你重温记忆：

```
$ echo “This is a test” | sed -n '/test/p’
This is a test
$ echo “This is a test” | sed -n '/trial/p’
$
$ echo “This is a test” | gawk '/test/{print $0}’
This is a test
$ echo “This is a test” | gawk '/trial/{print $0}’
$
```

第一个模式定义了一个单词 true `test`。`sed`编辑器和`gawk`程序脚本分别使用各自版本的`print`命令来打印任何匹配正则表达式模式的行。因为`echo`语句的文本字符串中包含“test”一词，所以数据流文本匹配了定义的正则表达式模式，`sed`编辑器显示了该行。

第二个模式同样定义了一个单词，这次是单词“trial”。由于`echo`语句的文本字符串不包含该单词，因此正则表达式模式不匹配，所以`sed`编辑器和`gawk`程序都没有打印该行。

你可能已经注意到，正则表达式并不关心模式出现在数据流的什么位置。它也不关心模式出现了多少次。只要正则表达式可以匹配文本字符串中的任何位置，它就会将字符串传递给正在使用它的 Linux 实用工具。

关键是将正则表达式模式与数据流文本进行匹配。需要记住，正则表达式对匹配模式是非常挑剔的。要记住的第一条规则是，正则表达式模式是区分大小大小的。这意味着它们只会匹配字符大小写完全正确的模式。



```
$ echo “This is a test” | sed -n '/this/p'
$
$ echo “This is a test” | sed -n '/This/p'
This is a test
$
```

第一次尝试匹配失败，是因为文本字符串中的单词“this”没有以全小写形式出现；而在第二次尝试中，模式使用了大写字母，因此运行良好。

你不需要将正则表达式限制在整个单词上。如果定义的文本出现在数据流的任何地方，正则表达式都将匹配以下内容：

```
$ echo “The books are expensive” | sed -n '/book/p'
The books are expensive
$
```

尽管数据流中的文本是`books`，但流中的数据包含了正则表达式`book`，因此正则表达式模式匹配了该数据。当然，如果你尝试相反的操作，正则表达式将失败：

```
$ echo “The book is expensive” | sed -n '/books/p'
$
```

由于完整的正则表达式文本没有出现在数据流中，匹配失败，`sed`编辑器没有显示该文本。

你也不必将正则表达式限制在单个单词上。你还可以在文本字符串中包含空格和数字：

```
$ echo “This is line number 1” | sed -n '/ber 1/p'
This is line number 1
$
```

空格在正则表达式中的处理方式与其他任何其他字符相同：

```
$ echo “This is line number1” | sed -n '/ber 1/p'
$
```

如果你在正则表达式中定义了一个空格，它必须在数据流中出现。你甚至可以创建一个匹配多个连续空格的正则表达式模式：

```
$ cat data1
This is a normal line of text.
This is  a line with too many spaces.
$ sed -n '/  /p' data1
This is  a line with too many spaces.
$
```

单词间带有两个空格的行匹配了正则表达式模式。这是捕捉文本文件中空格问题的极佳方法！

## 特殊字符

当你在正则表达式模式中使用文本字符串时，有些点你需要注意。在正则表达式中定义文本字符时，有少数例外情况。正则表达式模式为某些字符分配了特殊含义。如果你尝试在文本模式中使用这些字符，将无法得到你预期的结果。

正则表达式识别的特殊字符有：

`.*[]ˆ${}\+?|()`

随着章节的进行，你将发现这些特殊字符在正则表达式中具体的用途。但目前，只需记住，你不能在文本模式中单独使用这些字符即可。

如果你想将其中一个特殊字符作为文本字符使用，你需要对其进行转义。当转义特殊字符时，你在它前面添加一个特殊字符，以指示正则表达式引擎将下一个字符视为普通的文本字符。执行此操作的特殊字符是反斜杠（`\`）。

例如，如果你想在文本中搜索美元符号，只需在它前面加一个反斜杠：

```
$ cat data2
The cost is $00
$ sed -n '/\$/' data2
The cost is $00
```

由于反斜杠是一个特殊字符，如果你需要在正则表达式中使用它，则需要对其进行转义：

```
$ echo “\is a special character” | sed -n '/\\/'
\is a special character
```

最后，虽然斜杠`/`不是特殊字符，但如果你在`sed`编辑器或`gawk`程序的正则表达式中使用它，将会得到一个错误：

```
$ echo “3 /2” | sed -n '///'
sed: -e expression, char
```

要使用斜杠，你需要对其进行转义：

```
$ echo “3 /2” | sed -n '\/\'
3 /2
```

现在`sed`编辑器可以正确解释正则表达式了，一切正常。

## 锚字符

如“普通文本”部分所示，默认情况下，当你指定正则表达式模式时，如果模式出现在数据流的任何地方，它将被匹配。有两个特殊字符可以将模式锚定在行的开头或结尾。

### 从开头开始

脱字符字符（`ˆ`）定义了一个从行首开始的模式。如果模式位于行首以外的位置，正则表达式将失败。

要使用脱字符字符，你必须将其放在正则表达式中指定的模式之前：

```
$ echo “The book store” | sed -n '/book/p'
$
$ echo “Books are great” | sed -n '/Book/p'
Books are great
$
```

脱字符锚根据换行符，在每个新行的开头检查模式：

```
$ cat data3
This is a test line.
this is another test line.
A line that tests this feature.
Yet more testing of this
$ sed -n '/this/p' data3
this is another test line.
$
```

只要模式出现在新行的开头，脱字符锚就能捕捉到它。

如果你将脱字符字符放在模式开头以外的任何位置，它将作为一个普通字符而不是特殊字符运行：

```
$ echo “This ˆ is a test” | sed -n '/s ˆ/p'
This ˆ is a test
$
```

由于脱字符字符列在正则表达式模式的最后，`sed`编辑器将其作为普通字符来匹配文本。

> **注意**
> > 如果你需要仅使用脱字符来指定正则表达式模式，则不需要用斜杠对其进行转义。但是，如果你在模式中先指定脱字符，随后是额外的文本，则你需要在脱字符之前使用转义字符。

## 寻找结尾

在行首查找模式的相反操作是在行尾查找模式。美元符号（`$`）特殊字符定义了结束锚点。在文本模式后添加此特殊字符，表示该数据行必须以该文本模式结尾：

```
$ echo “This is a good book” | sed -n '/book$/p'
This is a good book
```

```
$ echo “This book is good” | sed -n '/book$/p'
$
```

结尾文本模式的问题在于，你必须仔细注意你正在查找的是什么：

```
$ echo “There are a lot of good books” | sed -n '/book$/p'
$
```

在行尾将单词“book”变为复数，意味着它不再匹配该正则表达式模式，尽管`book`存在于数据流中。文本模式必须是该行中的最后内容，模式才能匹配成功。

## 组合锚点

在几种常见的情况下，你可以在同一行中同时使用起始和结束锚点。在第一种情况下，假设你想查找一行仅包含特定文本模式的数据行：

```
$ cat data4
this is a test of using both anchors
I said this is a test
this is a test
I'm sure this is a test.
$ sed -n '/ˆthis is a test$/p' data4
this is a test
$
```

`sed`编辑器会忽略除指定文本外包含其他文本的行。

第二种情况初看起来可能有点奇怪，但极其有用。通过在没有任何文本的模式中组合两个锚点，你可以从数据流中过滤掉空行。考虑这个示例：

```
$ cat data5
This is one test line.
This is another test line.
$ sed '/ˆ$/d' data5
This is one test line.
This is another test line.
$
```

定义的正则表达式模式查找在行首和行尾之间没有任何内容的行。因为空行在两个换行符之间不包含文本，所以它们匹配该正则表达式。`sed`编辑器使用`d`删除命令来删除匹配该模式的行，从而移除文本中的所有空行。这是从文档中删除空行的有效方法。

## 点字符

点特殊字符`.`用于匹配换行符以外的任何单个字符。然而，点字符必须匹配一个字符；如果点所在的位置没有字符，则模式将失败。

让我们来看在正则表达式模式中使用点字符的几个示例：

```
$ cat data6
This is a test of a line.
The cat is sleeping.
That is a very nice hat.
This test is at line four.
at ten o'clock we'll go home.
$ sed -n '/.at/p' data6
The cat is sleeping.
That is a very nice hat.
This test is at line four.
$
```

你应该能够推断出为什么第一行失败了，以及为什么第二行和第三行通过了。第四行有点狡猾。注意，我们匹配了`at`，但它前面没有字符来匹配点字符。啊，其实有的！在正则表达式中，空格被算作字符，所以`at`前面的空格匹配了模式。第五行证明了这一点，它将`at`放在行首，导致无法匹配模式。

## 字符类

点特殊字符对于匹配任意字符的字符位置非常有用，但如果你想限制匹配哪些字符呢？这在正则表达式中被称为“字符类”。

你可以定义一个字符类，该类可以匹配文本模式中的某个位置。如果字符类中的任意一个字符出现在数据流中，它就会匹配该模式。

要定义字符类，你使用方括号`[]`。方括号应包含你想包含在类中的任何字符。然后你可以像使用任何其他通配符一样，在模式中使用整个类。这起初可能需要一点时间适应，但一旦掌握，它就能产生一些非常惊人的结果。

以下是创建一个字符类的示例：

```
$ sed -n '/[ch]at/p' data6
The cat is sleeping.
That is a very nice hat.
$
```

使用与点特殊字符示例相同的数据文件，我们得到了不同的结果。这次，我们成功过滤掉了只包含单词`at`的那行。匹配此模式的唯一单词是`cat`和`hat`。同样注意，以`at`开头的行也没有匹配。字符类中必须有一个字符来匹配相应的位置。

如果你不确定字符是大写还是小写，字符类大有用处：

```
$ echo “Yes” | sed -n '/[Yy]es/p'
Yes
$ echo “yes” | sed -n '/[Yy]es/p'
yes
$
```

你可以在一个表达式中使用多个字符类：

```
$ echo “Yes” | sed -n '/[Yy][Ee][Ss]/p'
Yes
$ echo “yEs” | sed -n '/[Yy][Ee][Ss]/p'
yEs
$ echo “yeS” | sed -n '/[Yy][Ee][Ss]/p'
yeS
$
```

该正则表达式使用了三个字符类，涵盖了所有三个字符位置的大写和小写。

字符类并不一定非只包含字母；你也可以在它们中使用数字：

```
$ cat data7
This line doesn't contain a number.
This line has 1 number.
This line a 2.
This line has 4.
$ sed -n '/[0-3]/' data7
This line has 1 number.
This line a 2.
```

正则表达式匹配包含0、1、2的任何行。你可以组合字符类来检查格式正确的数字，例如电话号码。然而，当你尝试匹配特定格式时，你必须小心。这里有一个邮编错误的示例：

```
$ cat data8
60633
46201
22301
22203
$ sed -n '/^[0-9]\{5\}$/p' data8
60633
46201
22301
22203
```

这可能不是你想要的结果。它成功过滤掉了太短的数字。但是，尽管我们定义了五个，它仍然通过了六位数。记住，正则表达式模式可以出现在文本的任何地方。模式之外总会有额外的字符。如果你想确保只匹配五个数字，你需要对它们进行界定，就像在本示例中这样显示它们位于行首和行尾：

```
$ sed -n '/^[0-9]\{5\}$/p' data8
60633
46201
22301
22203
```

现在这样好多了！在本章的晚些部分，我们将介绍如何进一步简化这一点。

字符类的一个流行用途是解析可能拼写错误的单词，例如从用户表单输入的数据。你可以轻松创建可以接受数据中常见拼写错误的正则表达式：

```
$ cat data9
I need to have some maintenence on my car.
I'll pay that in a seperate invoice.
After I pay for the maintenance my car will be as good as new.
$ sed -n '/maint[ea]n[ae]nce/p;/sep[ea]r[ae]te/p' data9
I need to have some maintenence on my car.
I'll pay that in a seperate invoice.
After I pay for the maintenance my car will be as good as new.
```

此示例中的两个`sed`打印命令利用正则表达式字符类来帮助捕捉文本中拼写错误的单词，maintenence和separate。相同的正则表达式模式也匹配了拼写正确的“maintenance”。

在正则表达式模式中，你也可以反转字符类的效果。与其寻找包含在类中的字符，不如寻找任何**不在**该类中的字符。要做到这一点，只需在字符类范围的开头放置一个脱字符字符`^`即可：

```
$ sed -n '/[ˆch]at/p' data6
This test is at line two.
$
```

通过否定字符类，正则表达式模式可以匹配任何不是`c`也不是`h`的字符，连同文本模式一起匹配。由于空格字符符合这一类别，因此它通过了模式匹配。然而，即使使用了否定操作，字符类仍然必须匹配一个字符，因此行首开头为`at`的行仍然无法匹配该模式。

## 使用范围

你可能已经注意到，当我之前展示邮政编码示例时，在每个字符类中列出所有可能的数字显得有些笨拙。幸运的是，你可以使用快捷方法，这样就不需要那样做了。

你可以通过连字符`-`符号在字符类内部使用字符范围。只需指定范围内的第一个字符、一个连字符，然后是范围内的最后一个字符。根据Linux系统所使用的字符集（参见第2章），正则表达式将包含指定字符范围内的任何字符。

现在，你可以通过指定数字范围来简化邮政编码示例：

```
$ sed -n '/^[0-9][0-9][0-9][0-9][0-9]$/p' data8
60633
46201
45902
$
```

这节省了大量的输入工作！每个字符类将匹配从`0`到`9`的任何数字。如果数据中任何地方出现字母，模式将失败：

```
$ echo “a8392” | sed -n '/^[0-9][0-9][0-9][0-9][0-9]$/p'
$
$ echo “1839a” | sed -n '/^[0-9][0-9][0-9][0-9][0-9]$/p'
$
$ echo “18a92” | sed -n '/^[0-9][0-9][0-9][0-9][0-9]$/p'
$
```

相同的技巧也适用于字母：

```
$ sed -n '/[c-h]at/p' data6
The cat is sleeping.
That is a very nice hat.
$
```

新模式`[c-h]at`匹配首字母在字母`c`和字母`h`之间的单词。在这种情况下，仅包含单词`at`的行未能匹配该模式。

你还可以在单个字符类中指定多个不连续的范围：

```
$ sed -n '/[a-ch-m]at/p' data6
The cat is sleeping.
That is a very nice hat.
$
```

该字符类允许`a`到`c`以及`h`到`m`的范围出现在`at`文本之前。此范围将拒绝任何在`d`和`g`之间的字母：

```
$ echo “I'm getting too fat.” | sed -n '/[a-ch-m]at/p'
$
```

此模式拒绝了`fat`文本，因为它不在指定的范围内。

## 特殊字符类

除了定义你自己的字符类外，BRE（基本正则表达式）还包含你可以用于匹配特定类型字符的特殊字符类。表19.1描述了你可以使用的BRE特殊字符。

### 表19.1 BRE特殊字符类

| 类 |  |
| :--- | :--- |
| `[[:alpha:]]` | 匹配任何字母，大写或小写。 |
| `[[:alnum:]]` | 匹配任何字母数字0–9, A–Z或a–z。 |
| `[[:blank:]]` | 匹配空格或制表符。 |
| `[[:digit:]]` | 匹配从0到9的数字。 |
| `[[:lower:]]` | 匹配任何小写字母a–z。 |
| `[[:print:]]` | 匹配任何打印字符。 |
| `[[:punct:]]` | 匹配标点符号。 |



| `[[:space:]]` | 匹配任何空白字符：空格、制表符、换行、FF、VT、CR。 |

| `[[:upper:]]` | 匹配任何大写字母 A–Z。 |

你可以像在正则表达式模式中使用普通字符类一样使用这些特殊字符类：

```bash
$ echo “abc” | sed -n ‘/[[:digit:]]/p’
$

$ echo “abc” | sed -n ‘/[[:alpha:]]/p’
abc

$ echo “abc123” | sed -n ‘/[[:digit:]]/p’
abc123

$ echo “This is, a test” | sed -n ‘/[[:punct:]]/p’
This is, a test

$ echo “This is a test” | sed -n ‘/[[:punct:]]/p’
$
```

使用特殊字符类是定义范围的一种简单方法。你不需要使用范围`[0–9]`，而只需要使用`[[:digit:]]`。

## 星号

在字符后放置星号表示该字符在文本中必须出现零次多次才能匹配该模式：

```bash
$ echo “ik” | sed -n ‘/ie*k/p’
ik

$ echo “iek” | sed -n ‘/ie*k/p’
iek

$ echo “ieek” | sed -n ‘/ie*k/p’
ieek

$ echo “ieeek” | sed -n ‘/ie*k/p’
ieeek

$ echo “ieeeek” | sed -n ‘/ie*k/p’
ieeeek
$
```

该模式符号通常用于处理具有常见拼写错误或语言拼写变化的单词。例如，如果你需要编写一个可能用于美式或英式英语的脚本，你可以写：

```bash
$ echo “I'm getting a color” | sed -n ‘/colou*r/p’
color
```

```bash
$ echo “I'm getting a colour” | sed -n ‘/colou*r/p’
colour
```

模式中的`u*`表示`u`可能出现也可能不出现。同样，如果你知道一个单词经常被拼错，你可以通过星号来适应它：

```bash
$ echo “I'm getting too fat.” | sed -n ‘/fa*t/p’
fat
```

只要`a`和`e`字符在`b`和`t`之间的任何组合中出现（包括完全不出现），模式匹配。如果出现了定义类之外的任何字符，模式将失败。

## 扩展正则表达式

POSIX ERE 模式包含一些 Linux 应用程序和工具使用的额外符号。`gawk`程序识别 ERE 模式，但`sed`编辑器不识别。

> 注意：请记住，`sed`编辑器和`gawk`程序之间的正则表达式引擎是有差异的。`gawk`程序可以使用大多数扩展正则表达式模式符号，并可以提供`sed`编辑器不具备的某些额外过滤功能。然而，由于这一点，它在处理数据流时通常较慢。

本节描述了你可以在`gawk`程序脚本中使用的更常见的 ERE 模式符号。

## 问号

问号与星号类似，但略有不同。问号表示前一个字符可以出现零次或一次，但仅此而已。它不匹配该字符的重复出现：

```bash
$ echo “bt” | gawk ‘/be?t/{print $0}’
bt

$ echo “bet” | gawk ‘/be?t/{print $0}’
bet

$ echo “beet” | gawk ‘/be?t/{print $0}’
$
```

如果字符`e`没有出现在文本中，或者只要它在文本中只出现一次，模式就会匹配。

与星号`*`一样，你可以将问号`?`符号配合字符类使用：

```bash
$ echo “bt” | gawk '/b[ae]?t/{print $0}'
```
`bt`

```bash
$ echo “bat” | gawk '/b[ae]?t/{print $0}'
```
`bat`

```bash
$ echo “bot” | gawk '/b[ae]?t/{print $0}'
```
`$`

```bash
$ echo “bet” | gawk '/b[ae]?t/{print $0}'
```
`bet`

```bash
$ echo “baet” | gawk '/b[ae]?t/{print $0}'
```
`$`

```bash
$ echo “beat” | gawk '/b[ae]?t/{print $0}'
```
`$`

```bash
$ echo “beet” | gawk '/b[ae]?t/{print $0}'
```
`$`

如果字符类中出现零或一个字符，模式匹配通过。然而，如果两个字符都出现，或者其中一个字符出现两次，模式匹配将失败。

## 加号

加号`+`是另一个模式符号，与星号`*`类似，但与问号`?`有不同。加号`+`表示前面的字符可以出现一次或多次，但必须至少出现一次。如果该字符不存在，则模式不匹配：

```bash
$ echo “beeet” | gawk '/be+t/{print $0}'
```
`beeet`

```bash
$ echo “beet” | gawk '/be+t/{print $0}'
```
`beet`

```bash
$ echo “bet” | gawk '/be+t/{print $0}'
```
`bet`

```bash
$ echo “bt” | gawk '/be+t/{print $0}'
```
`$`

如果字符`e`不存在，则模式匹配将失败。加号也可以配合字符类使用，方式与星号`*`和问号`?`相同：

```bash
$ echo “bt” | gawk '/b[ae]+t/{print $0}'
```
`$`

```bash
$ echo “bat” | gawk '/b[ae]+t/{print $0}'
```
`bat`

```bash
$ echo “bet” | gawk '/b[ae]+t/{print $0}'
```
`bet`

```bash
$ echo “beat” | gawk '/b[ae]+t/{print $0}'
```
`beat`

```bash
$ echo “beet” | gawk '/b[ae]+t/{print $0}'
```
`beet`

```bash
$ echo “beeat” | gawk '/b[ae]+t/{print $0}'
```
`beeat`

`$`

这一次，如果字符类中定义的任意一个字符出现，文本将匹配指定的模式。

## 使用大括号

大括号`{}`在 ERE 中可用，允许你对可重复的正则表达式指定限制。这通常被称为区间（interval）。你可以用两种格式表示区间：

- `m` - 正则表达式恰好出现`m`次。
- `m,n` - 正则表达式出现至少`m`次，但不超过`n`次。

此功能允许你精细调整允许字符（或字符类）在模式中出现的次数。

> 注意
> 默认情况下，`gawk`程序不识别正则表达式区间。你必须为`gawk`程序指定`--re-interval`命令行选项，使其能够识别正则表达式区间。

这里是一个使用单值区间的示例：

```bash
$ echo “bt” | gawk --re-interval '/be{1}t/{print $0}'
```
`$`

```bash
$ echo “bet” | gawk --re-interval '/be{1}t/{print $0}'
```
`bet`

```bash
$ echo “beet” | gawk --re-interval '/be{1}t/{print $0}'
```
`$`

通过指定为 1 的区间，你限制了字符出现的次数，以便字符串能够匹配模式。如果字符出现次数更多，则模式匹配将失败。

在很多时候，指定上限和下限非常有用：

```bash
$ echo “bt” | gawk --re-interval '/be{1,2}t/{print $0}'
```
`$`

```bash
$ echo “bet” | gawk --re-interval '/be{1,2}t/{print $0}'
```
`bet`

```bash
$ echo “beet” | gawk --re-interval '/be{1,2}t/{print $0}'
```
`beet`

```bash
$ echo “beeet” | gawk --re-interval '/be{1,2}t/{print $0}'
```
`$`

在这个示例中，字符`e`可以出现一次或两次，模式匹配匹配能通过；否则，模式匹配将失败。

区间模式匹配也适用于字符类：

```bash
$ echo “bt” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`$`

```bash
$ echo “bat” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`bat`

```bash
$ echo “bet” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`bet`

```bash
$ echo “beat” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`beat`

```bash
$ echo “beet” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`beet`

```bash
$ echo “beeat” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`beeat`

`$`

```bash
$ echo “baeet” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`$`

```bash
$ echo “baeaet” | gawk --re-interval '/b[ae]{1,2}t/{print $0}'
```
`$`

该正则表达式模式如果文本模式中恰好出现一次或两次字母`a`或`e`，则将进行匹配；但如果在任何组合中出现更多，则将失败。

## 管道符号

管道符号`|`允许你指定两个或多个模式，正则表达式引擎在检查数据流时会在逻辑`OR`公式中使用这些模式。如果任何模式匹配数据流文本，则文本将通过。如果没有任何模式匹配，则数据流文本将失败。

使用管道符号的格式为：

`expr1|expr2|...`

这是一个示例：

```bash
$ echo “The cat is” | gawk '/cat|dog/{print $0}'
```
`The cat is`

```bash
$ echo “The dog is” | gawk '/cat|dog/{print $0}'
```
`The dog is`

```bash
$ echo “The bird is” | gawk '/cat|dog/{print $0}'
```
`$`

如果字符`e`不存在，则模式匹配将失败。加号也可以配合字符类使用，方式与星号`*`和问号`?`相同。

（注：由于提供的文本存在大量重复和混乱内容，以上翻译已根据核心逻辑进行了提取并保持格式。）

```bash
mypath='echo $PATH | sed 's/:/ /g''

for directory in $mypath

do

  ...

done
```

一旦你获得了每个目录，就可以使用`ls`命令列出每个目录中的每个文件，并使用另一个`for`语句遍历每个文件，同时为每个文件增加计数器。

脚本的最终版本如下：

```bash
$ cat countfiles

#!/bin/bash

# count number of files in your PATH

mypath='echo $PATH | sed 's/:/ /g''

count=0

for directory in $mypath

do

    check='ls $directory'

    for item in $check

    do

        count=$[ $count + 1 ]

    done

  echo "$directory - $count"

  count=0

done

$ ./countfiles

/usr/local/bin - 79

/bin - 86

/usr/bin - 1502

/usr/X11R6/bin - 175

/usr/games - 2

/usr/java/j2sdk1.4.1_01/bin - 27

$
```

现在我们开始看到正则表达式背后的力量了！

## 验证电话号码

上一个示例展示了如何将简单的正则表达式与`sed`结合，替换数据流中的字符以处理数据。正则表达式通常用于验证数据，以确保数据符合脚本的正确格式。

常见的数据验证应用是检查电话号码。通常，数据输入表单会要求填写电话号码，而客户往往无法输入格式正确的电话号码。在美国，有几种显示电话号码的常用方式：

* `(123)456-7890`
* `(123) 456-7890`
* `123-456-7890`
* `123.456.7890`

这使得客户在表单中输入电话号码时有了四种可能性。正则表达式必须足够健壮，能够处理任何情况。

在构建正则表达式时，最好从左侧开始，并构建你的模式来匹配你可能会遇到的字符。在这个示例中，电话号码中可能也可能没有左括号。可以使用以下模式进行匹配：

`^\(?`

脱字符`^`用于指示数据的开头。由于左括号是一个特殊字符，你必须对其进行转义才能作为普通字符使用。问号`?`表示左括号在匹配的数据中可能出现也可能不出现。

接下来是三位区号。在美国，区号以数字 2 开始（没有以 0 或 1 开头的区号），可以到 9。匹配区号，你需要使用以下模式：

`[2-9][0-9]{2}`

这要求第一个字符是 2 到 9 之间的数字，后面跟着任意两个数字。在区号之后，右括号可能存在也可能不存在：

`\)?`

在区号之后，可以有一个空格、没有空格、连字符或点。你可以使用字符组配合管道符号对它们进行分组：

`(||-|\.)`

第一个管道符号紧紧跟在左括号后面，用于匹配没有空格的情况。你必须对点使用转义字符；否则它将被解释为匹配任何字符。

接下来是三位的电话交换机号码。这里没有特殊要求：

`[0-9]{3}`

在电话交换机号码之后，你必须匹配一个空格、连字符或点（这一次你不需要担心匹配没有空格的情况，因为电话交换机号码和数字其余部分之间至少有一个空格）：

`( ||-|\.)`

然后为了完成最后，你必须匹配字符串末尾的四位本地扩展号：

`[0-9]{4}$`

将整个模式组合在一起，结果如下：

`^\(?[2-9][0-9]{2}\)?(||-|\.)[0-9]{3}( ||-|\.)[0-9]{4}$`

你可以在`gawk`程序中使用这个正则表达式模式来过滤掉格式错误的电话号码。你现在只需要使用正则表达式在`gawk`程序中创建一个简单的脚本，然后通过该脚本过滤你的电话列表。记住，当你在`gawk`程序中使用正则表达式范围时，你必须使用`--re-interval`命令行选项，否则你将无法得到正确的结果。

这里是脚本：

```bash
$ cat isphone

#!/bin/bash

# script to filter out bad phone numbers

gawk --re-interval '/^\\(?[2-9][0-9]{2}\)?(||-|\.)[0-9]{3}( ||-|\.)[0-9]{4}/{print $0}'

$
```

虽然从这个列表中看不出来，但`gawk`命令在 shell 脚本中是单行的。你可以随后将电话号码重定向到脚本进行处理：

```bash
$ echo "317-555-1234" | ./isphone

317-555-1234

$ echo "000-555-1234" | ./isphone

$
```

或者，你可以将整个电话号码文件重定向到脚本以过滤掉无效的：

```bash
$ cat phonelist

000-000-0000

123-456-7890

212-555-1234

(317)555-1234

(202) 555-9876

33523

1234567890

234.123.4567

$ cat phonelist | ./isphone

212-555-1234

(317)555-1234

(202) 555-9876

234.123.4567

$
```



只有匹配正则表达式模式的有效电话号码才会出现。

## 解析电子邮件地址

在当今，电子邮件地址已成为一种至关重要的通信形式。验证电子邮件地址对脚本编写者已变成了一项挑战，因为创建电子邮件地址有无数种。电子邮件的基本格式是：

`username@hostname`

`username` 值可以使用任何字母数字字符，以及几个特殊字符：

- 点
- 连字符
- 加号
- 下划线

这些字符可以以任何组合的形式出现在有效的电子邮件用户 ID 中。电子邮件地址的 `hostname` 部分由一个或多个域名和一个服务器名称组成。服务器和域名也必须遵循严格的命名规则，仅允许字母数字字符以及以下特殊字符：

- 点
- 下划线

服务器名和域名之间都用点分隔，先指定服务器名，接着指定任何子域名，最后是不带尾部点的顶级域名。

曾几何时，顶级域名的数量相当有限，正则表达式模式构建者试图将它们全部添加到模式中进行验证。遗憾的是，随着互联网的增长，可能的顶级域名也随之增加。这种技术不再是一个可行的解决方案了。

让我们从左侧开始构建正则表达式模式。我们知道用户名中可以有多个有效字符。这应该很容易：

`^([a-zA-Z0-9_\.\.]+@`

此分组指定了用户名中允许的字符，并用加号表示必须至少有一个字符。下一个字符显然将是 `@` 符号，这并不意外。

`hostname` 模式使用了相同的技术来匹配服务器名和子域名：

`([a-zA-Z0-9_\.-]+)`

此模式匹配文本：

- `server`
- `server.subdomain`
- `server.subdomain.subdomain`

顶级域名有特殊的规则。顶级域名仅由字母组成，且长度不能少于两个字符（用于国家代码）且不能超过五个字符。以下是顶级域名的正则表达式模式：

`\.([a-zA-Z]{2,5})$`

将整个模式组合在一起，结果如下：

`^([a-zA-Z0-9_\.\.]+]+@([a-zA-Z0-9_\.-]+)\.([a-zA-Z]{2,5})$`

此模式将从数据列表中过滤掉格式不正确的电子邮件地址。现在你可以创建你的脚本来实现该正则表达式：

```bash
$ echo "rich@here.now" | ./isemail

rich@here.now

$ echo "rich@here.now." | ./isemail

$

$ echo "rich@here.n" | ./isemail

$

$ echo "rich@here-now" | ./isemail

$
```

## 总结

如果你在 shell 脚本中处理数据文件，那么你就需要熟悉正则表达式。正则表达式在 Linux 节点、编程语言以及使用正则表达式引擎的应用程序中实现。Linux 世界中有许多不同的正则表达式引擎。最流行的两个是 POSIX 基础正则表达式（BRE）引擎和 POSIX 扩展正则表达式（ERE）引擎。`sed` 编辑器主要符合 `BRE` 引擎，而 `gawk` 程序利用了 `ERE` 引擎中的大多数功能。

正则表达式定义了一个模式模板，用于过滤数据流中的文本。该模式由标准文本字符和特殊字符组合。特殊字符被正则表达式引擎用于匹配一个或多个字符的序列，类似于其他应用程序中通配符的工作方式。

通过组合字符和特殊字符，你可以定义一个模式来匹配几乎任何类型的数据。然后，你可以使用 `sed` 编辑器或 `gawk` 程序从较大的数据流中过滤出特定数据，或者对从数据输入应用程序接收的数据进行验证。

下一章将深入探讨如何使用 `sed` 编辑器进行高级文本处理。`sed` 编辑器提供了许多高级功能，使其在处理大型数据流和过滤你所需的内容时非常有用。

# 第 20 章：高级 sed

## 本章内容

- 多行命令
- 留存空间（hold space）
- 取反命令
- 改变流程
- 模式替换
- 在脚本中使用 `sed`
- 创建 `sed` 工具

第 18 章向你展示了如何使用 `sed` 编辑器的基础操作来处理数据流中的文本。基础 `sed` 编辑器命令能够处理大多数日常文本编辑需求。本章将介绍 `sed` 编辑器提供的更高级的功能。这些功能你可能不会经常使用，但当你需要它们时，知道它们的存在以及如何使用它们是非常有的。

## 多行命令

在使用基础 `sed` 编辑器命令时，你可能注意到一个局限性。所有的 `sed` 编辑器命令都在单行数据上执行操作。当 `sed` 编辑器读取数据流时，它根据换行符的存在将数据划分为若干行。`sed` 编辑器一次处理一行数据，在某行文本上执行定义的脚本命令，然后移动到下一行并重复该过程。

有时，你需要对跨越多行的数据执行操作。当你尝试查找或替换某个短语时，情况尤为如此。

例如，如果你在数据中查找短语 `Linux System Administrators Group`，该短语很有可能在短语中的任何单词之间被拆分成两行。如果你使用普通的 `sed` 编辑器命令处理文本，将无法检测到该短语是如何拆分的。

幸运的是，`sed` 编辑器的设计者考虑到了这种情况并设计了一种解决方案。`sed` 编辑器包含了三个用于处理多行文本的特殊命令：

- `N`：将数据流中的下一行添加以创建一个用于处理的多行组。
- `D`：删除多行组中的单行。
- `P`：打印多行组中的单行。

接下来的章节将更详细地检查这些多行命令，并演示你如何在脚本中使用它们。

## `next` 命令

在检查多行 `next` 命令之前，你首先需要查看单行版本的 `next` 命令是如何工作的。一旦你了解了该命令的作用，理解多行版本 `next` 命令的运行机制就会容易得多。

### 单行 `next` 命令

小写 `n` 命令告诉 `sed` 编辑器移动到数据流中的下一行文本，而不返回命令的开头。请记住，通常情况下，`sed` 编辑器会在移动到数据流中的下一行文本之前，处理该行上的所有定义命令。单行 `next` 命令改变了这种流程。

这听起来有些复杂，有时确实如此。在这个示例中，你有一个包含五行的数据文件，其中两行是空的。目标是移除标题行之后的空行，但保留最后一行之前的空行。如果你写一个 `sed` 脚本来删除空行，你将删除两个空行：

```bash
$ cat data1

This is the header line.

This is a data line.

This is the last line.

$

$ sed ‘/^$/d’ data1

This is the header line.

This is a data line.

This is the last line.

$
```

由于你想删除的行是空的，因此你没有可以搜索的文本来唯一标识该行。解决方案是使用 `n` 命令。在接下来的示例中，脚本查找包含 `header` 单词的唯一行。一旦脚本识别出该行，`n` 命令将 `sed` 编辑器移动到下一行文本，即空行。

```bash
$ sed ‘/header/{n ; d}’ data1

This is the header line.

This is a data line.

This is the last line.

$
```

此时，`sed` 编辑器继续处理命令列表，使用 `d` 命令删除该空行。当 `sed` 编辑器到达命令脚本的结尾时，它从数据流读取下一行文本并从命令脚本的顶部开始处理命令。`sed` 编辑器没有找到另一个包含 `header` 单词的行；因此不再删除后续行。

### 合并文本行

现在你已经看到了单行 `next` 命令，可以查看多行版本。单行 `next` 命令将数据流中的下一行文本移动到 `sed` 编辑器的处理空间（称为模式空间，pattern space）。多行版本的 `next` 命令（使用大写 `N`）将下一行文本添加到模式空间中已有的文本中。

这种操作的效果是将数据流中的两行文本合并到同一个模式空间中。文本行之间仍然由换行符分隔，但 `sed` 编辑器现在可以将这两行文本视为一行。

以下是 `N` 命令如何运行的演示：

```bash
$ cat data2

This is the header line.

This is the first data line.

This is the second data line.

This is the last line.

$

$ sed ‘/first/{ N ; s/\n/ / }’ data2

This is the header line.

This is the first data line. This is the second data line.

This is the last line.

$
```

`sed` 编辑器脚本搜索包含单词“first”的文本行。当它找到该行时，它使用 `N` 命令将下一行与该行合并。然后它使用替换命令（`s`）将换行符替换为空格。结果是文本文件中的两行在 `sed` 编辑器的输出中显示为一行。

如果你正在搜索一个可能在数据文件中被拆分成两行的文本短语，这具有实际应用。这里有一个例子：

```bash
$ cat data3

The first meeting of the Linux System

Administrator's group will be held on Tuesday.

All System Administrators should attend this meeting.

Thank you for your attendance.

$

$ sed ‘s/System Administrator/Desktop User/’ data3

The first meeting of the Linux SystemAdministrator's group will be held on Tuesday.

All Desktop Users should attend this meeting.

Thank you for your attendance.

$
```

替换命令在文本文件中查找特定的双单词短语 `System Administrator`。在短语出现的单行中，一切都是正常的；替换命令可以替换文本。但在短语被拆分在两行之间，替换命令无法识别匹配模式。

`N` 命令有助于解决这个问题：


```bash
$ sed 'N ; s/System.Administrator/Desktop User/' data3

The first meeting of the Linux Desktop User's group will be held on Tuesday.

All Desktop Users should attend this meeting.

Thank you for your attendance.

$
```

通过使用 `N` 命令将下一行与找到第一个单词所在的行合并，你可以检测到短语中是否发生了换行。

注意，`substitution`（替换）命令在“System”和“Administration”之间使用了通配符模式（`.`），用以同时匹配空格和换行情况。然而，当它匹配到换行符时，会将其从字符串中删除，导致两行合并为的一行。这可能并不是你完全想要的结果。

为了解决这个问题，你可以在 `sed` 编辑脚本中使用两个 `substitution` 命令：一个用于匹配多行情况，另一个用于匹配单行情况：

```bash
$ sed '

> N

> s/System\nAdministrator/Desktop\nUser/

> s/System Administrator/Desktop User/

' data3

The first meeting of the Linux Desktop

User's group will be held on Tuesday.

All Desktop Users should attend this meeting.

Thank you for your attendance.

$
```

第一个 `substitution` 命令专门查找两个搜索单词之间的换行符，并将其包含在替换字符串中。这允许你在新文本相同位置添加换行符。

然而，该脚本仍然存在一个微妙的问题。脚本在执行 `sed` 编辑命令之前，总是会将下一行文本读取到模式空间（pattern space）。当它到达最后一行文本时，没有下一行文本可以读取，因此 `N` 命令会导致 `sed` 编辑器停止。如果匹配的文本位于数据流的最后一行，命令将无法捕获匹配数据：

```bash
$ cat data4

The first meeting of the Linux System

Administrator's group will be held on Tuesday.

All System Administrators should attend this meeting.

$

$ sed '

> N

> s/System\nAdministrator/Desktop\nUser/

> s/System Administrator/Desktop User/

' data4

The first meeting of the Linux Desktop

User's group will be held on Tuesday.

All System Administrators should attend this meeting.

$
```

由于 `System Administrator` 文本出现在数据流的最后一行，`N` 命令漏过了它，因为没有另一行可以读取到模式空间进行合并。你可以通过将单行命令移动到 `N` 命令之前，并让多行命令仅出现在 `N` 命令之后来轻松解决这个问题，如下所示：

```bash
$ sed '

> s/System Administrator/Desktop User/

> N

> s/System\nAdministrator/Desktop\nUser/

' data4

The first meeting of the Linux Desktop

User's group will be held on Tuesday.

All Desktop Users should attend this meeting.

$
```

现在，在单行中查找短语的 `substitution` 命令在数据流的最后一行也能正常工作，而多行 `substitution` 命令则涵盖了数据流中间出现的情况。

## 多行删除命令

第 18 章引入了单行 `delete` 命令（`d`）。`sed` 编辑器使用它来删除模式空间中的当前行。然而，在使用 `N` 命令工作时，使用单行 `delete` 命令必须非常小心：

```bash
$ sed 'N ; /System\nAdministrator/d' data4

All System Administrators should attend this meeting.

$
```

`delete` 命令在不同的行中查找 `System` 和 `Administrator` 单词，然后删除了模式空间中的两行。这可能并不是你初衷想要的。

`sed` 编辑器提供了多行 `delete` 命令（`D`），它只删除模式空间中的第一行。它删除了包括换行符在内的所有字符：

```bash
$ sed 'N ; /System\nAdministrator/d' data4

Administrator's group will be held on Tuesday.

All System Administrators should attend this meeting.

$
```

由 `N` 命令添加到模式空间的第二行文本保持完好。如果你需要移除出现在你找到数据字符串的行之前的行文本，这就会非常有用。

这里有一个移除出现在数据流第一行之前的空白空行的示例：

```bash
$ cat data5

This is the header line.

This is a data line.

This is the last line.

$

$ sed '/^$/{N ; /header/D}' data5

This is the header line.

This is a data line.

This is the last line.

$
```

此 `sed` 编辑器脚本查找空行，然后使用 `N` 命令将下一行文本添加到模式空间中。如果新的模式空间内容包含 `header` 单词，`D` 命令会移除模式空间中的第一行。如果没有 `N` 和 `D` 命令的组合，就不可能在不移除其他所有空的情况下移除第一个空。

## 多行打印命令

现在，你可能已经明白了单行和多行版本命令之间的区别。多行打印命令（`P`）也采用了相同的技术。它只打印多行模式空间中的第一行。这包含了模式空间中换行符之前的所有字符。它的用法与单行 `p` 命令非常相似，用于在你使用 `-n` 选项抑制脚本输出时显示文本。

```bash
$ sed -n 'N ; /System\nAdministrator/P' data3

The first meeting of the Linux System

$
```



当发生多行匹配时，`P`命令只打印模式空间中的第一行。多行`P`命令的力量在与`N`和`D`命令结合时发挥作用。`D`命令有一个独特的特性，它会强制`sed`编辑器返回脚本开头并在相同的模式空间上重复命令（它不会从数据流中读取新行）。通过在命令脚本中包含`N`命令，你可以有效地逐步通过模式空间，将多行结合。接下来，通过使用`P`命令你可以打印第一行，然后使用`D`命令删除第一行并返回开头。一旦你回到脚本开头，`N`命令就会读取下一行文本并重新开始过程。这个循环一直持续到数据流的结束。

## 留存空间 (Hold Space)

模式空间是一个活动缓冲区区域，用于存放`sed`编辑器在处理命令时所检查的文本。然而，它不是`sed`编辑器中用于存储文本的空间。

`sed`编辑器利用另一个称为留存空间的缓冲区区域。你可以在处理模式空间中的其他行时，使用留存空间来临时存放文本行。与操作留存空间相关的五个命令，如表 20.1 所示。

### 表 20.1 sed 编辑器留存空间命令

| 命令 | 说明 |
| :--- | :--- |
| `h` | 将模式空间复制到留存空间。 |
| `H` | 将模式空间追加到留存空间。 |
| `g` | 将留存空间复制到模式空间。 |
| `G` | 将留存空间追加到模式空间。 |
| `x` | 交换模式空间和留存空间的内容。 |

这些命令允许你将文本从模式空间复制到留存空间。这释放了模式空间以便加载另一个字符串进行处理。

通常在使用`h`或`H`命令将字符串移动到留存空间之后，你最终会想要使用`g`、`G`或`x`命令将存储的字符串移回模式空间（否则你一开始就不会在意保存它们）。

由于有两个缓冲区区域，尝试确定某行文本位于哪个缓冲区区域有时会令人困惑。这里有一个简短的示例，演示了如何使用`h`和`g`命令在`sed`编辑器的缓冲区空间之间来移动数据：

```
$ cat data2

This is the header line.

This is the first data line.

This is the second data line.

This is the last line.

$ 
```

```
$ sed -n ‘/first/{
> h
> p
> n
> p
> g
> p
> } data2
This is the first data line.
This is the second data line.
This is the first data line.
$
```

请逐步查看上述代码示例：

1. `sed`脚本在地址中使用正则表达式来过滤包含单词`first`单词的行。
2. 当出现包含`first`单词的行时，`h`命令将该行放置在保持空间（hold space）中。
3. `p`命令打印模式空间（pattern space）的内容，此时仍第一行数据。
4. `n`命令从数据流中获取下一行（`This is the second data line`）并将其放入模式空间中。
5. `p`命令打印模式空间的内容，此时是第二行数据。
6. `g`命令将保持空间的内容（`This is the first data line`）放回模式空间，替换当前文本。
7. `p`命令打印模式空间当前的内容，此时已变回第一行数据。

通过使用保持空间来调整文本行的顺序，你可以强制让第一行数据在输出中出现在第二行数据之后。如果你直接删掉第一个`p`命令，就可以反向顺序输出这两行：

```
$ sed -n ‘/first/{
> h
> n
> p
> g
> p
> } data2
This is the second data line.
This is the first data line.
$
```

这是一个有用功能的开始。你可以使用这种技术创建一个`sed`脚本来反转整个文本文件的行顺序！然而，要做到这一点，你需要了解`sed`编辑器的否定功能（negating feature），这正是下一节的重点。

## 否定命令

第 18 章展示了`sed`编辑器将命令应用于数据流中的每行文本，或者应用于由单个地址或地址范围专门指出的行。你也可以配置命令，使其不应用于数据流中的特定地址或地址范围。

感叹号命令（`!`）用于否定一个命令。这意味着在命令通常会被激活的情况下，它并不会被激活。这里有一个演示此功能的示例：

```
$ sed -n ‘/header/!p’ data2
This is the first data line.
This is the second data line.
This is the last line.
$
```

正常的`p`命令只会打印`data2`文件中包含单词`header`的那行。通过添加感叹号，文件中除了包含地址中引用的文本的行外，所有行都将被打印出来。

在几个应用场景中，使用感叹号非常有用。回想在本章较早，“后续命令”部分展示过一种情况：`sed`编辑器命令不会在数据流的最后一行文本上操作，因为它后面没有行了。你可以使用感叹号来解决那个问题：

```
$ sed ‘N; s/System.Administrator/Desktop User/’ data4
The first meeting of the Linux Desktop User's group will be held on Tuesday
All System Administrators should attend this meeting.
$ 
$ sed ‘!N; s/System.Administrator/Desktop User/’ data4
The first meeting of the Linux Desktop User's group will be held on Tuesday
All Desktop Users should attend this meeting.
$ 
```

这个示例展示了配合`N`命令使用的感叹号，以及特殊地址`$`。`$`代表数据流中的最后一行文本，因此当`sed`编辑器到达最后一行时，它不会执行`N`命令。但对于所有其他行，它都会执行该命令。

使用这种技术，你可以反转数据流中文本行的顺序。要反转文本流中出现的行顺序（先显示最后一行，最后显示第一行），你需要使用保持空间进行一些“花式操作”。

你需要的处理的模式如下：

1. 将一行放入模式空间中。
2. 将该行从模式空间移动到保持空间。
3. 将下一行文本放入模式空间中。
4. 将保持空间追加到模式空间中。
5. 将模式空间中的所有内容放入保持空间中。
6–9. 重复步骤 3 到 5，直到你将所有行按反序放入保持空间中。
10. 获取这些行并打印它们。

图 20.1 详细描绘了它的样子。

图 20.1 使用保持空间反转文本文件的顺序

![](img/00014.jpg)

使用这种技术时，你不希望在处理行时就打印它们。这意味着要为`sed`使用`-n`命令行选项。下一步需要确定的是如何将保持空间的文本追加到模式空间的文本中。这是通过使用`G`命令实现的。唯一的问题是，你不想将保持空间追加到处理的第一行文本上。这通过使用感叹号命令可以轻松解决：

```
1!G
```

下一步是将新的模式空间（带有追加的反转行文本的文本行）放入保持空间中。这非常简单，只需使用`h`命令即可。

当你将整个数据流以反转顺序放在模式空间中时，你只需要打印结果即可。当你到达数据流的最后一行时，你就知道整个数据流已经在模式空间中了。要打印结果，只需使用以下命令：

```
$p
```

这些就是你创建行反转`sed`脚本所需的全部组件。现在在测试运行中尝试一下吧：

```
$ cat data2
This is the header line.
This is the first data line.
This is the second data line.
This is the last line.
$ 
$ sed -n ‘{1!G;h;$p}’ data2
This is the last line.
This is the second data line.
This is the first data line.
This is the header line.
$
```

`sed`编辑器的运行符合预期。脚本的输出反转了文本文件中原始行。这证明了在脚本中使用保持空间的力量。它提供了一种在脚本输出中操作行顺序的简便方法。

> 注意
> 
> > 如果你好奇的话，有一个 Linux 命令可以执行反转文本文件的功能。`tac`命令以反序显示文本文件。你可能注意到这个命令的名字很巧妙，因为它执行的是`cat`命令的反向功能。

## 改变流程

通常，`sed`编辑器从脚本顶部开始向脚本末尾处理命令（`D`命令除外，它强制`sed`编辑器返回脚本开头而不读取新的文本行）。`sed`编辑器提供了一种改变命令脚本流程的方法，产生类似于结构化编程环境的结果。

## 分支（Branching）

在上一节中，你看到了如何使用感叹号命令来否定命令对某行文本的影响。`sed`编辑器提供了一种根据地址、地址模式或地址范围来否定整个命令块的方法。这允许你仅对数据流中的特定子集执行一组命令。

`branch`命令的格式为：

`[``address``]b [``label``]`

`address`参数决定了哪些行触发`branch`命令。`label`参数定义了跳转的位置。如果没有`label`参数，`branch`命令将执行到脚本末尾。

```
$ sed '{2,3b ; s/This is/Is this/;s/line./test?/}' data2
Is this the header test?
This is the first data line.
This is the second data line.
Is this the last test?
$
```

`branch`命令会跳过数据流中第二行和第三行的`substitution`（替换）命令。

与其跳转到脚本的末尾，你可以为`branch`命令定义一个跳转到的标签（label）。标签以冒号开头，长度最多为七个字符：

```
:label2
```

要指定标签，只需将其添加在`b`命令之后即可。使用标签允许你跳过匹配`branch`模式的命令，但仍然处理脚本中的其他命令：

```
$ sed '{/first/b jump1 ; s/This is the/No jump on/ 
> :jump1 
> s/This is the/Jump here on/}' data2
No jump on header line
Jump here on first data line
No jump on second data line
No jump on last line
$
```

`branch`命令指定：如果行中出现匹配文本“first”，程序应跳转到标记为`jump1`的脚本行。如果`branch`命令模式没有匹配，`sed`编辑器将继续处理脚本中的命令，包括`branch`标签之后的命令。（因此，所有三个`substitution`命令都会在不匹配`branch`模式的行上处理。）

如果行匹配`branch`模式，`sed`编辑器将跳转到`branch`标签行。因此，只有最后一个`substitution`命令会被执行。

示例显示了跳转到`sed`脚本中更靠处的标签。你也可以`branch`到脚本中较早出现的标签，从而创建一个循环效果：

```
$ echo “This, is, a, test, to, remove, commas. ” | sed -n '{
> :start
> s/,//1p
> b start
> }
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
```

脚本的每次迭代都会删除文本字符串中的第一个逗号并打印该字符串。这个脚本有一个缺陷：它永远不会结束。这种情况创建了一个无限循环，不断寻找逗号，直到你通过发送`Ctrl+C`组合键信号来手动停止它。

为了防止这个问题，你应该为`branch`命令指定一个要查找的地址模式。如果模式不存在，跳转应该停止：

```
$ echo “This, is, a, test, to, remove, commas. ” | sed -n '{
> :start
> s/,//1p
> /,/b start
> }
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
$
```

现在，`branch`命令仅在行中存在逗号时才进行跳转。在删除最后一个逗号后，`branch`命令将不再执行，允许脚本正常结束。

### 测试

与`branch`命令类似，`test`命令（`t`）也用于修改`sed`编辑器脚本的流程。`test`命令不是根据地址跳转到标签，而是根据`substitution`命令的结果跳转到标签。

如果`substitution`命令成功匹配了模式，`test`命令将跳转到指定的标签。如果`substitution`命令没有匹配模式，则`test`命令不会跳转。

`test`命令使用与`branch`命令相同的格式：

```
[address]t[label]
```

与`branch`命令一样，如果你不指定标签，如果测试成功，`sed`将跳转到脚本末尾。`test`命令提供了一种在文本上执行基础`if-then`语句的便捷方法。例如，如果你在执行了另一个替换后就不需要进行替换，`test`命令可以提供帮助：

```
$ sed '{ 
> s/first/matched
> t
> s/This is the/No match on/ 
 }' data2
No match on header line
This is the matched line
No match on second data line
No match on last line
$
```

第一个`substitution`命令查找模式`first`。如果它匹配行中的模式，它将替换文本，并且`test`命令将跳过后续的`substitution`命令。如果第一个`substitution`命令没有匹配模式，则处理第二个`substitution`命令。

使用`test`命令，你可以清理你尝试使用`branch`命令时创建的循环：

```
$ echo “This, is, a, test, to, remove, commas. ” | sed -n '{
> :start
> s/,//1p
> t start
> }
This is, a, test, to, remove, commas.
This is a, test, to, remove, commas.
This is a test, to, remove, commas.
This is a test to, remove, commas.
This is a test to remove, commas.
This is a test to remove commas.
$
```

当没有更多可以执行的替换时，`test`命令将不会跳转，并继续执行脚本的剩余部分。

### 模式替换

你已经看到了如何在`sed`命令中使用模式来替换数据流中的文本。然而，在使用通配符字符时，很难确切知道哪些文本会匹配模式。

例如，假设你想在行中匹配到的单词周围加上双引号。如果你只是在模式中寻找一个单词进行匹配，这非常简单：

```
$ echo “The cat sleeps in his hat.” | sed 's/cat/“cat”/'
The cat sleeps in hat.
```

但如果你在模式中使用通配符（`.`）来匹配多个单词呢？

```
$ echo “The cat sleeps in his hat.” | sed 's/.at/“.at”/g'
The “.at” sleeps in his “.
```

`substitution`字符串使用了点通配符来匹配字母字母“at”。遗憾的是，替换字符串并没有匹配该单词的值。

### 符号

`sed`编辑器为你提供了一个解决方案。符号（`&`）用于表示`substitution`命令中的匹配模式。对于匹配定义的任何文本，你可以在替换模式中使用符号来调用它。这允许你操作匹配的任何单词：

```
$ echo “The cat sleeps in his hat.” | sed 's/.at/“&”/g'
The “cat” sleeps in his “hat”.
```




当模式匹配`cat`时，“cat”出现在替换单词中。当匹配`hat`时，“hat”出现在替换单词中。

### 替换单个单词

符号检索匹配`substitution`命令中指定模式的整个字符串。有时你只想检索字符串的子集。你也可以这样做，但有点复杂。

`sed`编辑器使用括号在替换模式中定义子字符串组件。然后，你可以在替换模式中使用特殊字符引用每个子字符串组件。替换字符由反斜杠和一个数字组成。数字指示子字符串组件的位置。`sed`编辑器为第一个组件分配字符`\1`，第二个组件分配`\2`，以此类推。

> 注意：在`substitution`命令中使用括号时，必须转义将其识别为分组字符而不是普通括号。这与转义其他特殊字符的操作相反。

看看这个在`sed`编辑器脚本中使用此功能的示例：

```bash
$ echo “The System Administrator manual” | sed 's/\(System\) Administrator/\1 User/'

The System User manual
```

如果你需要用一个单词替换一个短语，而该单词是该短语的一个子字符串，但该子字符串恰好使用了通配符字符，那么使用子字符串组件将是救星：

```bash
$ echo “That furry cat is pretty” | sed ‘s/furry \(.at\)/\1/’
```

```text
That cat is pretty
```

```bash
$ echo “That furry hat is pretty” | sed ‘s/furry \(.at\)/\1/’
```

```text
That hat is pretty
```

在这种情况下，你不能使用安培符号`&`，因为它会替换整个匹配模式。子字符串组件提供了答案，允许你只选择模式中的某部分作为替换模式。

当你需要在两个或多个子字符串组件之间插入文本时，这个功能会特别有用。这里有一个使用子字符串组件在长数字中插入逗号的脚本：

```bash
$ echo “1234567” | sed '{
:start
s/\(.*[0-9]\)\([0-9]\{3\}\)/\1,\2/
t start
}'
```

```text
1,234,567
```

该脚本将匹配模式划分为两个组件：

```text
.*[0-9]
[0-9]{3}
```

此模式寻找两个子字符串。第一个子字符串是任意数量的字符，以数字结尾。第二个子字符串是一连续的三个数字（请参阅第 19 章获取有关如何在正则表达式中使用大括号的信息）。如果在文本中找到此模式，替换文本将会在两个组件之间放置一个逗号，每个组件由其组件位置进行标识。脚本使用`test`命令遍历数字，直到所有逗号都已就位。

## 在脚本中使用`sed`

现在你已经了解了`sed`编辑器的各个部分，是时候将它们整合起来并用在你的`shell`脚本中了。本节将演示在使用`bash` shell 脚本中的`sed`编辑器时，你应该了解的一些特性。

### 使用包装器

你可能已经注意到，尝试实现一个`sed`编辑器脚本可能是麻烦的，特别是当脚本很长时。与其在每次使用它时都重新输入整个脚本，你不如将`sed`编辑器命令放置在一个`shell`脚本包装器中。包装器充当`sed`编辑器脚本和命令行之间的中间人。

一旦进入`shell`脚本，你就可以使用普通的`shell`变量和参数配合你的`sed`编辑器脚本。这里有一个使用命令行参数变量作为`sed`脚本输入的示例：

```bash
$ cat reverse

#!/bin/bash

# 用于反转行的 sed 编辑器脚本 shell 包装器

sed -n '{
1!G
h
$p
}' $1
```

名为`reverse`的`shell`脚本使用`sed`编辑器脚本来反转数据流中的文本行。它使用`shell`参数`$1`从命令行中获取第一个参数，该参数应该是要反转的文件名：

```bash
$ ./reverse data2

This is the last line.

This is the second data line.

This is the first data line.

This is the header line.
```

现在你可以轻松地在任何文件上使用`sed`编辑器脚本，而不需要不断重新输入整个命令行。

### 重定向`sed`输出

默认情况下，`sed`编辑器将脚本结果输出到`STDOUT`。你可以在`shell`脚本中使用所有标准方法来重定向`sed`编辑器的输出。

你可以使用反引号将`sed`编辑器命令的输出重定向到变量，以便在脚本后续使用。以下是一个使用`sed`脚本为数值计算结果添加逗号的示例：

```bash
$ cat fact

#!/bin/bash

# 在阶乘答案中为数字添加逗号

factorial=1
counter=1
number=$1

while [ $counter -le $number ]
do
    factorial=$[ $factorial * $counter ]
    counter=$[ $counter + 1 ]
done

result=`echo $factorial | sed '{
:start
s/\(.*[0-9]\)\([0-9]\{3\}\)/\1,\2/
t start
}'`

echo "The result is $result"
```

```bash
$ ./fact 20

The result is 2,432,902,008,176,640,000
```

在使用完普通的阶乘计算脚本后，该脚本的结果被作为`sed`编辑器脚本的输入，后者添加逗号。该值随后被用于`echo`语句以产生结果。

## 创建`sed`实用程序

正如本章目前为止提供的简短示例所示，使用`sed`编辑器可以完成许多酷的数据格式化工作。本节展示了一些用于执行常见数据处理函数的常用`sed`编辑器脚本。

### 行间空行

正如你在本章中看到的这些简短示例，你可以使用`sed`编辑器完成许多酷的数据格式化任务。为了开始，请看下面这个简单的`sed`脚本，它在文本文件的行之间插入空行：

```bash
$ sed 'G' data2

This is the header line.

This is the first data line.

This is the second data line.

This is the last line.
```

这非常简单！这个技巧的关键在于保持空间（hold space）。`G`命令会将保持空间的内容附加到当前行。当你启动编辑器时，保持空间包含一个空行。你可能已经注意到这个脚本会在文件末尾添加一个空行。如果你想消除这个，可以使用取反符号`!`和行尾符号`$`：

```bash
$ sed '!G' data2

This is the header line.

This is the first data line.

This is the second data line.

This is the last line.
```

要把行间距更进一步，如果文本文件已经有了空行，但你想让所有行翻倍呢？如果你使用之前的脚本，你会得到过多的行：

```bash
$ sed 'G' data6

This is line one.

This is line two.

This is line three.

This is line four.
```

```bash
$ cat data6
```

现在你在原来的空行处有了三个空行。解决这个问题的方案是先删除数据流中的任何空行，然后使用`G`命令插入新行。为了删除现有的行，你只需要配合匹配空行的模式使用`d`命令：`/$/`。此模式使用了符号`^`和行尾标签`$`。

```bash
$ sed '/$/d;$G' data6

This is line one.

This is line two.

This is line three.

This is line four.
```

### 为文件中的行进行编号

上一章（第 18 章）向你展示了如何使用等号`=`显示数据流中行的行号：

```bash
$ sed = data2

1
This is the header line.
2
This is the first data line.
3
This is the second data line.
4
This is the last line.
```

这读起来有点不方便，因为行号在数据流中实际行的上方。更好的解决方案是将行号与文本放在同一行。现在你已经学会了如何使用`N`命令合并行，在`sed`编辑器脚本中使用这些信息应该不难。然而，这个实用工具的技巧在于，你不能在同一个脚本中组合这两个命令。

一旦你获得了等号命令的输出，你可以将其输出管道到另一个`sed`编辑器脚本，该脚本使用`N`命令合并这两行。你还需要使用`substitution`命令将换行符替换为空格或制表符。以下是最终解决方案的样式所示：

```bash
$ sed = data2 | sed 'N; s/\n/ /'

1 This is the header line.
2 This is the first data line.
3 This is the second data line.
4 This is the last line.
```

现在看起来好多了。在编写程序时，你需要查看错误信息中使用的行号，这是一个非常实用的辅助工具。

## 打印最后几行

到目前为止，你已经看到如何使用`p`命令打印数据流中的所有行，或者只打印匹配特定模式的行。如果你只需要处理长列表（例如日志文件）的最后几行，该怎么办呢？

美元符号`$`代表数据流的最后一行，因此可以很容易地只显示最后一行：

```bash
$ sed -n ‘$p’ data2

This is the last line.
```

现在，你如何使用美元符号`$`在数据流末尾显示固定数量的行呢？答案是创建一个滚动窗口。

滚动窗口是通过使用`N`命令将文本行组合，并在模式空间（pattern space）中检查文本块的常用方法。`N`命令将下一行文本附加到模式空间中已有的文本。一旦你在模式空间中获得了一个包含 10 行文本的块，就可以使用美元符号检查你是否处于数据流的末尾。如果不在末尾，则继续向模式空间添加更多行，同时删除原始行（记住`D`命令，它会删除模式空间中的第一行）。

通过循环`N`和`D`命令，你向模式空间中的行块添加新行，同时删除旧行。`branch`命令是该循环的完美选择。要结束循环，只需识别最后一行并使用`q`命令退出即可。

这里是最终的`sed`编辑器脚本的样式：

```bash
$ sed ‘{
:start
$q
N
11,$D
b start
}’ /etc/passwd

user:x:1000:1000:user,,,:/home/user:/bin/bash
polkituser:x:113:121:PolicyKit,,,:/var/run/PolicyKit:/bin/false
sshd:x:114:65534::/var/run/sshd:/usr/sbin/nologin
Samantha:x:1001:1002:Samantha,4,,:/home/Samantha:/bin/bash
Debian-exim:x:115:124::/var/spool/exim4:/bin/false
usbmux:x:116:46:usbmux daemon,,,:/home/usbmux:/bin/false
rtkit:x:117:125:RealtimeKit,,,:/proc:/bin/false
Timothy:x:1002:1005::/home/Timothy:/bin/sh
Christine:x:1003:1006::/home/Christine:/bin/sh
kdm:x:118:65534::/home/kdm:/bin/false
```

脚本首先检查该行是否为数据流的最后一行。如果是，`quit`命令将停止循环。`N`命令将下一行附加到模式空间中的当前行。`11,$D`命令表示如果当前行在第 10 行之后，则删除模式空间中的第一行。这在模式空间中创建了滑动窗口的效果。

## 删除行

`sed`编辑器的另一个实用工具是删除数据流中不需要的空行。从数据流中删除所有空行很容易，但有选择地删除空行需要一点技巧。本节将向你展示几个简单的`sed`脚本，可以帮助你从数据中删除不需要的空行。

### 删除连续的空行

数据文件中出现额外的空行可能会很困扰。通常情况下，你的数据文件包含空行，但有时缺少某行数据会导致产生过多的空行（正如你之前在双倍间距示例中看到的）。

删除连续空行的最简单方法是使用范围地址检查数据流。第 18 章向你展示了如何在地址中使用范围，包括如何将模式包含在地址范围中。`sed`编辑器会对在指定地址范围内匹配模式的所有行执行命令。

删除连续空行的关键是创建一个包含一个非空行和一个空行的地址范围。如果`sed`编辑器遇到这个范围，它就不应该删除该行。然而，对于不匹配该范围的行（连续的两个或多个空行），它应该删除这些行。

这里是实现此操作的脚本：

```bash
/./,/^$/!d
```

范围是从`/./`到`/^$/`。范围中的起始地址匹配包含至少一个字符的任何行。范围中的结束地址匹配空行。此范围内的行不会被删除。

这里是脚本的运行实例：

```bash
$ cat data6

This is the first line.

This is the second line.

This is the third line.

This is the fourth line.

$ sed '/./,/^$/!d' data6

This is the first line.

This is the second line.

This is the third line.

This is the fourth line.
```

无论文件中的数据行之间出现多少空行，输出都只在行之间保留一个空行。

### 删除开头的空行

数据文件开头包含多个空行也是一件困扰的事。通常在尝试将数据从文本文件导入数据库时，空行会创建空记录，从而影响任何使用这些数据的计算。

从数据流的顶部删除空行并不是一项困难的任务。这里是实现该功能的脚本：

```bash
/./,$!d
```

脚本使用地址范围来确定哪些行被删除。范围从包含字符的行开始，一直到数据流的末尾。此范围内的任何行都不会从输出中删除。这意味着第一个包含字符的行之前的任何行都会被删除。

看看这个简单脚本的运行实例：

```bash
$ cat data7

This is the first line.

This is the second line.

$ sed '/./,$!d' data7

This is the first line.

This is the second line.
```

测试文件在数据行之前有两个空行。脚本成功删除了两个开头的空行，同时保持了数据内部空行的完好。

### 删除结尾的空行

遗憾的是，删除结尾的空行并没有删除开头空行那么简单。就像打印数据流的结尾一样，删除数据流末尾的空行需要技巧和循环。

在我们开始讨论之前，让我们看看脚本的样子：

```bash
sed '{
:start
/^\n*$/{$d; N; b start}
}'
```

初看起来这看起来可能有点奇怪。注意普通脚本括号内部还有括号。这允许你在整个命令脚本中将命令组合在一起。命令组适用于指定的地址模式。地址模式匹配任何仅包含换行符的行。当找到这样的行时，如果它是最后一行，`delete`命令将将其删除。如果不是最后一行，`N`命令将下一行附加到其后，`branch`命令将循环到开头重新开始。

这里是脚本的运行实例：

```bash
$ cat data8

This is the first line.

This is the second line.

$ sed '{
:start
/^\n*$/{$d; N; b start}
}' data8

This is the first line.

This is the second line.
```

脚本成功删除了文本文件结尾的空行。

## HTML 标签

在当今时代，从网站下载文本以保存或作为应用程序中的数据并不稀奇。然而，有时当你从网站下载文本时，你也会获得用于格式化数据的 HTML 标签。当你只想看到数据时，这可能会成为一个问题。

标准的 HTML 网页包含几种不同类型的 HTML 标签，用于识别正确显示页面信息所需的格式特征。这里是一个 HTML 文件的示例：

```bash
$ cat data9

<html>

<head>

<title>This is the page title</title>

</head>

<body>

<p>

This is the <b>>first</b> line in the Web page. This should provide

some <i>useful</i> information for us to use in our shell script.

</p>

</body>

</html>
```

HTML 标签通过小于号和大于符号识别。大多数 HTML 标签都是成对出现的。一个标签开始格式化过程（例如，`<b>`用于加粗），另一个标签停止格式化过程（例如，`</b>`取消加粗）。

移除 HTML 标签会产生一个问题，如果你不小心的话。乍一看，你可能会认为移除 HTML 标签的方法只是寻找一个以小于符号（`<`）开头、以大于符号（`>`）结尾且符号之间有数据的文本字符串：

```bash
s/<.*>//g
```




遗憾的是，这个命令会导致意外之外的后果：

```bash
$ sed ‘s/<.*>//g’ data9

This is the line in the Web page. This should provide

some information for us to use in our shell script.

$
```

注意，标题文本丢失了，还有加粗和斜体的文本也丢失了。`sed` 编辑器字面上解释了该脚本，意味着小于号和大于号之间的任何文本，包括其他的小于号和大于号！每当文本被包裹在 HTML 标签中（例如 `<b>first</b></b>`）时，`sed` 脚本都会删除整个文本。

解决这个问题的办法是让 `sed` 编辑器忽略原始标签之间任何嵌入的大于号。要做到这一点，你可以创建一个否定大于号的字符类。这会将脚本更改为：

```bash
s/<[^>]*>//g
```

该脚本现在可以正常工作了，显示出你需要从网页 HTML 代码中看到的数据：

```bash
$ sed ‘s/<[^>]*>//g’ data9

This is the page title

This is the first line in the Web page. This should provide

some useful information for us to use in our shell script.

$
```

这好多了。为了进一步整洁内容，你可以添加一个 `delete` 命令来消除那些烦人的空行：

```bash
$ sed ‘s/<[^>]*>//g;^$/d’ data9

This is the page title

This is the first line in the Web page. This should provide

some useful information for us to use in our shell script.

$
```

现在看起来紧凑得多；只剩下你需要看到的数据。

## 总结

`sed` 编辑器提供了一些高级功能，允许你处理跨行的文本模式。本章向你展示了如何使用 `next` 命令获取数据流中的下一行并将其放入模式空间（pattern space）。一旦进入模式空间，你就可以执行复杂的 `substitution`（替换）命令来替换跨多行文本的短语。

多行 `delete` 命令允许你在模式空间包含两个或更多行时删除第一行。这是遍历数据流中多行的方便方法。同样，多行 `print` 命令允许你在模式空间包含两个或更多行文本时只打印第一行。多行命令的组合允许你遍历数据流并创建一个多行替换系统。

接下来，本章讨论了保持空间（hold space）。保持空间允许你在处理更多行文本时留出一行文本。你可以随时取回保持空间的内容，并替换模式空间中的文本，或将保持空间的内容附加到模式空间的文本之后。使用保持空间允许你对数据流进行排序，反转文本行在数据中出现的顺序。

本章还讨论了 `sed` 编辑器的流程控制命令。`branch` 命令提供了一种改变脚本中 `sed` 编辑器命令正常流的方法，从而在特定条件下创建循环或跳过命令。`test` 命令为你的 `sed` 编辑器命令脚本提供了一种 `if-then` 类型的语句。`test` 命令仅在先前的 `substitution` 命令成功替换了行中的文本时，才进行分支。

本章以讨论如何在 shell 脚本中使用 `sed` 脚本结束。对于大型 `sed` 脚本，一种常用技术是将脚本放在 shell 包装器中。你可以在 `sed` 脚本中使用命令行参数变量来传递 shell 命令行值。这创建了一种直接从命令行甚至从其他 shell 脚本中利用你的 `sed` 编辑器脚本的简单方法。

下一章将深入探索 `gawk` 的世界。`gawk` 程序支持许多高级编程语言的特性。你只需使用 `gawk` 就可以创建一些相当复杂的数据处理和报告程序。本章将描述各种编程特性，并演示如何使用它们从简单数据生成你自己的花哨报告。

# 第 21 章：高级 gawk

## 本章内容

- 重新审查 `gawk`
- 在 `gawk` 中使用变量
- 使用结构化命令
- 格式化你的输出
- 与函数一起

第 18 章介绍了 `gawk` 程序，并演示了使用它从原始数据文件生成格式化报告的基础。本章将更深入地探讨自定义 `gawk` 以生成报告。`gawk` 程序是一门完整的编程语言，提供了允许你编写高级程序来处理数据的功能。如果你是从其他编程语言跳入 shell 脚本世界的，那么你应该会对 `gawk` 感到如家。在本章中，你将看到如何使用 `gawk` 来处理几乎任何数据格式化任务。

## 使用变量

任何编程语言的一项重要功能都是使用变量存储和取回值。`gawk` 语言支持两种类型的变量：

- 内置变量
- 用户定义变量

许多内置变量可供 `gawk` 使用。内置变量包含了处理数据字段和记录的信息。你也可以在 `gawk` 程序中创建自己的变量。

### 内置变量

`gawk` 程序使用内置变量来引用特定的特性。本节描述了供 `gawk` 使用的内置变量并演示如何使用它们。

### 字段和记录分隔符

第 18 章演示了 `gawk` 中的一种内置变量——字段变量。字段变量允许你使用美元符号和字段在记录中的数值位置来引用数据字段。因此，要引用记录中的第一个字段，使用 `$1`。引用第二个字段，使用 `$2`，以此此类推。

数据字段由字段分隔符界定。默认情况下，字段分隔符是空白字符，如空格或制表符。第 18 章展示了如何通过命令行使用 `-F` 参数，或在 `gawk` 程序内部使用特殊的 `FS` 内置变量更改字段分隔符。

`FS` 内置变量属于一组内置变量，这些变量控制 `gawk` 如何处理输入和输出数据中的字段和记录。表 21.1 列出了该组中的内置变量。

#### 表 21.1 gawk 数据字段和记录变量

| 变量 | 说明 |
| :--- | :--- |
| `FIELDWIDTHS` | 定义每个数据字段精确宽度（以空格）的数字列表 |
| `FS` | 输入字段分隔符 |
| `RS` | 输入记录分隔符 |
| `OFS` | 输出字段分隔符 |
| `ORS` | 输出记录分隔符 |

`FS` 和 `OFS` 变量定义了你的 `gawk` 程序如何处理数据流中的字段。你已经见过如何使用 `FS` 变量来定义分隔记录字段的字符。`OFS` 变量执行相同的功能，但它是通过 `print` 命令用于输出。

默认情况下，`gawk` 将 `OFS` 变量设置为空格格，因此当你使用命令：

```awk
print $1,$2,$3
```

你看到的输出为：

```text
field1 field2 field3
```

你可以在以下示例中看到这一点：

```bash
$ cat data1

data11,data12,data13,data14,data15

data21,data22,data23,data24,data25

data31,data32,data33,data34,data35
```

```bash
$ gawk ‘BEGIN{FS=",”} {print $1,$2,$3}' data1
```

```text
data11 data12 data13

data21 data22 data23

data31 data32 data33
```

`print` 命令会自动将 `OFS` 变量的值置于输出中每个数据字段之间。通过设置 `OFS` 变量，你可以使用任何字符串来分隔输出中的数据字段：

```bash
$ gawk ‘BEGIN{FS=",”; OFS="-"} {print $1,$2,$3}' data1
```

```text
data11-data12-data13

data21-data22-data23

data31-data32-data33
```

```bash
$ gawk ‘BEGIN{FS=",”; OFS="--"} {print $1,$2,$3}' data1
```

```text
data11--data12--data13

data21--data22--data23

data31--data32--data33
```

```bash
$ gawk ‘BEGIN{FS=",”; OFS="<-->"} {print $1,$2,$3}' data1
```

```text
data11<-->data12<-->data13

data21<-->data22<-->data23

data31<-->data32<-->data33
```

`FIELDWIDTHS` 变量允许你在不使用字段分隔符的情况下读取记录。在某些应用程序中，数据并不是使用字段分隔符，而是放在记录中的特定列中。在这种情况下，你必须设置 `FIELDWIDTHS` 变量以匹配记录中数据的布局。

一旦你设置了 `FIELDWIDTHS` 变量，`gawk` 就会忽略 `FS` 并根据提供的字段宽度计算数据字段。这里是一个使用字段宽度而不是字段分隔符的示例：

```bash
$ cat data1b
```

```text
1005.3247596.37

115-2.349194.00

05810.1298100.1
```

```bash
$ gawk ‘BEGIN{FIELDWIDTHS="3 5 2 5"}{print $1,$2,$3,$4}' data1b
```

```text
100 5.324 75 96.37

115 -2.34 91 94.00

058 10.12 98 100.1
```

`FIELDWIDTHS` 变量定义了四个数据字段，`gawk` 据此解析数据记录。每条记录中的数字字符串根据定义的字段宽度值进行拆分。

> **注意**
>
> 必须记住，一旦你设置了 `FIELDWIDTHS` 变量，这些值就必须保持不变。这种方法无法处理变长度的数据字段。

`RS` 和 `ORS` 变量定义了你的 `gawk` 程序如何处理数据流中的记录。默认情况下，`gawk` 将 `RS` 和 `ORS` 变量设置为换行符。默认的 `RS` 变量值表示输入数据流中的每行文本都是一个新记录。

有时，你会遇到数据字段跨越数据流中的多行的情况。这种情况的一个经典例子是包含地址和电话号码的数据，每个各占一行：

```text
Riley Mullen

123 Main Street

Chicago, IL 60601

(312)555-1234
```

如果你尝试使用默认的 `FS` 和 `RS` 变量值来读取这些数据，`gawk` 将把每一行视为一个独立的记录，并将记录中的每个空格解释为字段分隔符。这并不是你想要的。

要解决解决，，你需要将 `FS` 变量设置为换行符。这表示数据流中的每一行都是一个独立的字段，且行上的所有数据都属于该数据字段。然而，当你这样做时，并不知道新记录从哪里开始。

要解决这个问题，将 `RS` 变量设置为空字符串，然后在数据流中的数据记录之间留一个空行。`gawk` 程序将把每个空行解释为记录分隔符。

以下是使用这种技术的示例：

```bash
$ cat data2

Riley Mullen

123 Main Street

Chicago, IL  60601

(312)555-1234

Frank Williams

456 Oak Street

Indianapolis, IN  46201

(317)555-9876

Haley Snell

4231 Elm Street

Detroit, MI
```

```bash
$ gawk ‘BEGIN{FS="\n"; RS=""} {print $1,$4}' data2
```

```text
Riley Mullen

Frank Williams

Haley Snell
```

完美——`gawk` 程序将文件中的每一行解释为数据字段，并将空行解释为记录分隔符。

### 数据变量

除了字段和记录分隔符变量外，`gawk` 还提供了其他内置变量，帮助你了解数据情况并从 shell 环境中提取信息。

#### gawk 内置变量

| 变量 | 描述 |
| :--- | :--- |
| `ARGC` | 命令行参数的数量。 |
| `ARGIND` | 当前处理的文件在 `ARGV` 中的索引。 |
| `ARGV` | 命令行参数数组。 |
| `CONVFMT` | 数字的转换格式（参见 `printf` 语句）。默认值为 `%g`。 |
| `ENVIRON` | shell 环境变量及其值的关联数组。 |
| `ERRNO` | 在读取或关闭输入文件时发生错误时的系统错误。 |
| `FILENAME` | 用于 `gawk` 程序输入的数据文件名为。 |
| `FNR` | 数据文件中的当前记录号。 |
| `IGNORECASE` | 如果设置为非零值，则忽略 `gawk` 命令中使用的字符串的大小写写。 |
| `NF` | 文件中数据字段的总数。 |
| `NR` | 已处理的输入记录数。 |
| `OFMT` | 数字的输出格式。默认为 `%g`。 |
| `RLENGTH` | `match` 函数中匹配到的子字符串的长度。 |
| `RSTART` | `match` 函数中匹配到的子字符串的起始索引。 |

你应该能在你的 shell 脚本中识别这些变量中的几个。`ARGC` 和 `ARGV` 变量允许你从 shell 中检索命令行参数的数量及其值。然而，这可能有点复杂，因为 `gawk` 不将程序脚本视为命令行的一部分：

```bash
$ gawk ‘BEGIN{print ARGC,ARGV[1]}’ data1
```

```text
2 data1
```

`ARGC` 变量表示命令行上有两个参数。这包括 `gawk` 命令和 `data1` 参数（记住，程序脚本不算参数）。`ARGV` 数组从索引 0 开始，代表命令。第一个数组值是 `gawk` 命令后的第一个命令行参数。

> **注意**
>
> 注意，与 shell 变量不同，在脚本中引用 `gawk` 变量时，不需要在变量名前添加美元符号。

`ENVIRON` 变量对你来说可能有点奇怪。它使用关联数组来检索 shell 环境变量。关联数组使用文本而不是数值作为数组索引。文本是 shell 环境变量。数组的值是 shell 环境变量的值。以下是这种技术的示例：

```bash
$ gawk ‘

BEGIN{

print ENVIRON["HOME"]

print ENVIRON["PATH"]

}’
```

```text
/home/rich

/usr/local/bin:/bin:/usr/bin:/usr/X11R6/bin
```

`ENVIRON["HOME"]` 变量从 shell 中检索 `HOME` 环境变量值。同样，`ENVIRON["PATH"]` 变量检索 `PATH` 环境变量值。你可以使用这种技术从 shell 中检索任何环境变量值并用于你的 `gawk` 程序。

`FNR`、`NF` 和 `NR` 变量在跟踪 `gawk` 程序中的数据字段和记录时非常有用。有时你处于一种不知道记录中具体有多少个数据字段的情况。`NF` 变量允许你指定记录中的最后一个数据字段，而无需知道它的位置：

```bash
$ gawk ‘BEGIN{FS=":"; OFS=":"} {print $1,$NF}' /etc/passwd
```

```text
rich:/bin/bash

testy:/bin/csh

mark:/bin/bash

dan:/bin/bash

mike:/bin/bash

test:/bin/bash
```

`NF` 变量包含数据文件中最后一个数据字段的数值。你可以通过在其前面添加美元符号将其作为数据字段变量使用。

`FNR` 和 `NR` 变量彼此相似但略有不同。`FNR` 变量包含当前数据文件中处理的记录数。`NR` 变量包含已处理的记录总数。让我们来看几个示例来观察这种差异：

```bash
$ gawk ‘BEGIN{FS=,”}{print $1,“FNR=”FNR}’ data1 data1
```

```text
data11 FNR=1

data21 FNR=2

data31 FNR=3

data11 FNR=1

data21 FNR=2

data31 FNR=3
```

在这个示例中，`gawk` 程序命令行定义了两个输入文件。（它指定了两次同一个输入文件）。脚本打印第一个数据字段的值以及 `FNR` 变量的当前值。请注意，当 `gawk` 程序处理第二个数据文件时，`FNR` 的值被重置回 1。

现在，让我们添加 `NR` 变量看看会产生什么：

```bash
$ gawk ‘

BEGIN {FS=,”}

{print $1,”FNR=”FNR,”NR=”NR}

END{print “There were”,NR,”records processed”’ data1 data1
```

```text
data11 FNR=1 NR=1

data21 FNR=2 NR=2

data31 FNR=3 NR=3

data11 FNR=1 NR=4

data21 FNR=2 NR=5

data31 FNR=3 NR=6

There were 6 records processed
```



当`gawk`处理第二个数据文件时，`FNR`变量的值被重置了，但`NR`变量的计数一直持续到第二个数据文件。结论是，如果你只使用一个数据文件作为输入，`FNR`和`NR`的值将是相同的。如果你使用多个数据文件作为输入，`FNR`的值会在每个数据文件处重置，而`NR`的值将对所有数据文件进行计数。

> **注意**
> 你会发现在使用`gawk`时，`gawk`脚本往往会比你的 shell 脚本其他部分还要大。在本章的示例中，为了简单起见，我们直接从命令行运行`gawk`脚本，使用了 shell 的多行功能。在 shell 脚本中使用`gawk`时，你应该将不同的`gawk`命令放在单独的行。这将让你更容易阅读和遵循，而不是尝试将所有内容都挤在 shell 脚本的一行中。此外，如果你发现自己在不同的 shell 脚本中使用相同的`gawk`脚本，记住你可以将`gawk`脚本保存在单独的文件中并使用`-f`参数引用它（参见第 18 章）。

## 用户定义变量

就像任何其他自尊的编程语言一样，`gawk`允许你定义自己的变量并在程序代码中使用。`gawk`用户定义的变量名可以是任意数量的字母、数字和下划线，但不能与数字开头。同样重要的是记住，`gawk`变量名是区分大小写的。

### 在脚本中为赋值

在`gawk`程序中为变量赋值与在 shell 脚本中赋值类似，使用赋值语句：

```bash
$ gawk '
BEGIN{
testing="This is a test"
print testing
}'
```

输出：
```
This is a test
```

`print`语句的输出是`testing`变量的当前值。与 shell 脚本变量一样，`gawk`变量可以持有数值值或文本值：

```bash
$ gawk '
BEGIN{
testing="This is a test"
print testing
testing=45
print testing
}'
```

输出：
```
This is a test
45
```

在这个示例中，`testing`变量的值从文本值变为数值值。

赋值语句还可以包含用于处理数值的数学算法：

```bash
$ gawk 'BEGIN{x=4; x= x * 2 + 3; print x}'
```

输出：
```
11
```

从这个示例可以看出，`gawk`编程语言包含了处理数值的标准数学运算符。这些运算符包括取余符号（`%`）和幂符号（使用`^`或`**`）。

### 在命令行上赋值

你也可以使用`gawk`命令行为`gawk`程序中的变量赋值。这允许你在普通代码之外设置值，动态更改值。这里有一个使用命令行变量显示文件中特定数据字段的示例：

```bash
$ cat script1
BEGIN{FS=","}
{print $n}

$ gawk -f script1 n=2 data1
```

输出：
```
data12
data22
```

`gawk -f script1 n=2 data1`命令允许你从命令行将变量`n`设置为`2`。这允许你在普通代码之外设置值，动态更改值。

## 使用数组

许多编程语言提供了数组来在单个变量中存储值。`gawk`提供了数组功能。关联数组与数值数组的区别在于，索引可以是任何字符串。

### 定义数组变量

你可以使用赋值语句定义数组变量。数组的格式为：
`var[index] = element`
其中`var`是变量名，`index`是数组索引，`element`是数据元素。这里是一些数组变量的示例：

```bash
$ gawk 'BEGIN{
capital["Illinois"] = "Springfield"
print capital["Illinois"]
}'
```

输出：
```
Springfield
```

当你引用数组变量时，必须包含索引值以检索数据元素。这对于数值数据也有效：

```bash
$ gawk 'BEGIN{
var[1] = 3
var[2] = 4
total = var[1] + var[2]
print total
}'
```

输出：
```
7
```

### 遍历数组变量

数组变量的问题在于，你可能无法知道索引值。与使用顺序数字作为索引值的数值数组不同，关联数组的索引可以是任何内容。

如果你需要在`gawk`中遍历关联数组，可以使用`for`语句的特殊格式：

```bash
for (var in array)
{
    statements
}
```

`for`语句循环语句，每次将关联数组的下一个索引赋值给变量`var`。记住，变量是索引的值，而不是数据元素的值。你可以通过将变量作为数组索引来轻松提取数据元素值：

```bash
$ gawk 'BEGIN{
var["a"] = 1
var["g"] = 2
var["m"] = 3
var["u"] = 4
for (test in var)
{
    print "Index:", test, " - Value:", var[test]
}
}'
```

输出：
```
Index: u - Value: 4
Index: m - Value: 3
Index: a - Value: 1
Index: g - Value: 2
```

注意，索引值并不是按特定顺序返回的，但它们每个都引用了相应的数据元素值。这一点非常重要，因为你不能保证返回值的顺序是相同的，只能确保索引和数据值相互匹配。

## 删除数组变量

从关联数组中删除数组索引需要一个特殊的命令：

`delete array[index]`

`delete`命令会从数组中删除关联索引值和关联的数据元素值：

```bash
$ gawk 'BEGIN{
var["a"] = 1
var["g"] = 2
for (test in var)
{
    print "Index:",test," - Value:",var[test]
}
delete var["g"]
print "---"
for (test in var)
    print "Index:",test," - Value:",var[test]
}'
```

输出：
```
Index: a - Value: 1
Index: g - Value: 2
---
Index: a - Value: 1
```

一旦从关联数组中删除了索引值，你就无法再次检索它。

## 使用模式

`gawk`程序支持多种类型的匹配模式来过滤数据记录，这与`sed`编辑器非常相似。第 18 章已经展示了两个特殊模式的应用。`BEGIN`和`END`关键字是特殊模式，它们在读取数据流数据之前或之后执行语句。同样，你也可以创建其他模式，当数据流中出现匹配数据时执行语句。

本节演示了如何在`gawk`脚本中使用匹配模式来限制程序脚本适用的记录范围。

### 正则表达式

第 19 章展示了如何使用正则表达式作为匹配模式。你可以使用基础正则表达式（BRE）或扩展正则表达式（ERE）来过滤程序脚本应用于数据流中的哪些行。

当使用正则表达式时，该正则表达式必须出现在其所控制的程序脚本的左大括号之前：

```bash
$ gawk 'BEGIN{FS=","} /11/{print $1}' data1
data11
$
```

正则表达式`/11/`匹配数据字段中任何位置包含字符串`11`的记录。`gawk`程序会将定义的正则表达式与记录中的所有数据字段进行匹配，包括字段分隔符字符：

```bash
$ gawk 'BEGIN{FS=","} /,d/{print $1}' data1
data11
data21
data31
$
```

此示例匹配了正则表达式中用作字段分隔符的逗号。这并不总是好事。它可能会导致匹配特定字段数据的问题，因为该数据也可能出现在另一个字段中。如果你需要将正则表达式匹配特定的数据实例，应该使用匹配运算符。

### 匹配运算符

匹配运算符允许将正则表达式限制在记录的特定数据字段。匹配运算符是波浪符号（`~`）。你指定匹配运算符、数据字段变量以及要匹配的正则表达式：

```bash
$1 ~ /^data/
```

变量`$1`表示记录中的第一个数据字段。该表达式过滤出第一个数据字段以文本`data`开头的记录。以下是一个在`gawk`程序脚本中使用匹配运算符的示例：

```bash
$ gawk 'BEGIN{FS=","} $2 ~ /^data2/{print $0}' data1
data21,data22,data23,data24,data25
$
```

匹配运算符将第二个数据字段与正则表达式`/^data2/`进行比较，该正则表示字符串以文本`data2`开头。

这是一个强大的工具，通常用于`gawk`程序脚本在数据文件中搜索特定数据元素：

```bash
$ gawk -F: '$1 ~ /rich/{print $1,$NF}' /etc/passwd
rich /bin/bash
$
```

此示例在第一个数据字段中搜索文本`rich`。当在记录中找到该模式时，它会打印记录的第一个和最后一个数据字段的值。

你也可以通过`!`符号来取反正则表达式匹配：

```bash
$1 !~ /expression/
```

如果记录中没有找到正则表达式，则程序脚本将应用于该记录数据：

```bash
$ gawk -F: '$1 !~ /rich/{print $1,$NF}' /etc/passwd
root /bin/bash
daemon /bin/sh
bin /bin/sh
sys /bin/sh
--- output truncated ---
$
```

在这个示例中，`gawk`程序脚本打印了`/etc/passwd`文件中所有不匹配用户名`rich`的条目的用户 ID 和 shell！

### 数学表达式

除了正则表达式之外，你还可以在匹配模式中使用数学表达式。在匹配数据字段中的数值值时，这个功能非常有用。例如，如果你想显示所有属于`root`用户组（组 ID 0）的系统用户，可以使用此脚本：

```bash
$ gawk -F: '$4 == 0{print $1}' /etc/passwd
root
sync
shutdown
halt
operator
$
```

该脚本检查第四个数据字段包含值`0`的记录。在这个 Linux 系统上，有五个用户属于`root`用户组。

你可以使用任何标准的数学比较表达式：

- `x == y`：值`x`等于`y`。
- `x <= y`：值`x`小于或等于`y`。
- `x < y`：值`x`小于`y`。
- `x >= y`：值`x`大于或等于`y`。
- `x > y`：值`x`大于`y`。

你也可以使用带有文本数据的表达式，但必须小心。与正则表达式不同，表达式是精确匹配。数据必须与模式完全匹配：

```bash
$ gawk -F, '$1 == "data"{print $1}' data1
$
$ gawk -F, '$1 == "data11"{print $1}' data1
data11
$
```

第一次测试没有匹配到任何记录，因为在任何记录中第一个数据字段的值都不是`data`。第二次测试匹配了一个值为`data11`的记录。

## 结构化命令

`gawk`编程语言支持常见的结构化编程命令。本节描述了这些命令中的每一个，并演示了如何在`gawk`编程环境中使用它们。

### if 语句

`gawk`编程语言支持标准的`if-then-else`格式的`if`语句。你必须为`if`语句定义一个条件并括在括号内。如果条件求值为`TRUE`，则紧执行`if`语句后面的语句。如果条件求值为`FALSE`，则跳过该语句。这可以使用以下格式：

```bash
if (condition)
    statement1
```

或者你可以将其放在一行上，如下：

```bash
if (condition) statement1
```

这是一个演示该格式的简单示例：

```bash
$ cat data4
10
5
13
50
34

$ gawk '{if ($1 > 20) print $1}' data4
50
34
$
```

并不太复杂。如果你需要在`if`语句中执行多个语句，必须用大括号将其括起来：

```bash
$ gawk '{
if ($1 > 20)
{
    x = $1 * 2
    print x
}
}' data4
100
68
```

注意不要将`if`语句的大括号与用于开始和结束程序的括号搞混。`gawk`程序可以检测到缺失的大括号，如果你弄错了，它会产生错误消息：

```bash
$ gawk '{
if ($1 > 20)
{
    x = $1 * 2
    print x
}
}' data4
gawk: cmd.line:7: (END OF FILE)
gawk: cmd.line:7: parse error
$
```

`gawk`的`if`语句支持`else`子句，允许在`if`语句条件失败时执行一个或多个语句。这里是使用`else`子句的示例：

```bash
$ gawk '{
if ($1 > 20)
{
    x = $1 * 2
    print x
} else
{
    x = $1 / 2
    print x
}
}' data4
5
2.5
6.5
100
68
$
```

你可以在单行使用`else`子句，但必须在`if`语句部分之后使用分号：

```bash
if (condition) statement1; else statement2
```

这是使用单行格式的相同示例：

```bash
$ gawk '{if ($1 > 20) print $1 * 2; else print $1 / 2}' data4
5
2.5
6.5
100
68
$
```

这种格式更紧凑，但可能更难跟。

### while 语句

`while`语句为`gawk`程序提供了基础的循环功能。以下是`while`语句的格式：

```bash
while (condition)
{
  statements
}
```

`while`循环允许你对一组数据进行迭代，并检查一个用于停止迭代的条件。如果你在每个记录中有多个必须在计算中使用数据值，这种方法非常有用：

```bash
$ cat data5
130 120 135
160 113 140
145 170 215

$ gawk '{
  total = 0
  i = 1
  while (i < 4)
  {
    total += $i
    i++
  }
  avg = total / 3
  print "Average:",avg
}' data5
Average: 128.333
Average: 137.667
Average: 176.667
$
```

`while`语句遍历记录中的数据字段，将每个值累加到`total`变量中，然后增加计数器变量`i`。当计数器值等于 4 时，`while`条件变为`FALSE`，循环终止，并执行脚本中的下一条语句。该语句计算平均值；然后打印平均值。此过程会对数据文件中的每个记录重复。

`gawk`编程语言支持在`while`循环中使用`break`和`continue`语句，允许你跳出循环中间部分：

```bash
$ gawk '{
  total = 0
  i = 1
  while (i < 4)
  {
    total += $i
    if (i == 2)
      break
    i++
  }
  avg = total / 2
  print "The average of the first two data elements is:",avg
}' data5
The average of the first two data elements is: 125
The average of the first two data elements is: 136.5
The average of the first two data elements is: 157.5
$
```

`break`语句用于在变量`i`的值为 2 时跳出`while`循环。

### do-while 语句

`do-while`语句与`while`语句类似，但会在检查条件语句之前执行语句。以下是`do-while`语句的格式：

```bash
do
{
  statements
} while (condition)
```

这种格式保证了语句在评估条件之前至少执行一次。当你需要在评估条件之前执行某些语句时，这非常有用：

```bash
$ gawk '{
  total = 0
  i = 1
  do
  {
    total += $i
    i++
  } while (total < 150)
  print total
}' data5
250
160
315
$
```



脚本从每个记录中读取数据字段并对其求和，直到累积值达到 150。如果第一个数据字段超过 150（如第二个记录所示），脚本保证在评估条件之前至少读取第一个数据字段。

### for 语句

`for` 语句是许多编程语言中用于循环的常用方法。`gawk` 编程语言支持 C 风格的 `for` 循环：

```
for(variable assignment; condition; iteration process)
```

这通过在一个语句中组合多个功能，简化了循环：

```bash
$ gawk '{
  total = 0
  for (i = 1; i < 4; i++)
  {
    total += $i
  }
  avg = total / 3
  print "Average:",avg
}' data5
Average: 128.333
Average: 137.667
Average: 176.667
$
```

### 格式化打印

你可能注意到 `print` 语句对输出的控制非常有限。解决方案是使用 `printf`。`printf` 命令使用一个格式字符串后跟多个参数。`printf` 命令不会自动添加换行，因此你必须自己包含换行符。

以下是 `printf` 的格式：

```
printf(format string, arg1, arg2, ...)
```

`format string` 包含了定义参数显示方式的格式说明符。每个说明符都以 `%` 开头，后面跟着几个字符。

#### 控制字母

| 控制字母 | 描述 |
| :--- | :--- |
| `c` | 显示一个字符。 |
| `d` | 显示一个整数。 |
| `i` | 显示一个整数（与 `d` 相同）。 |
| `e` | 显示科学计数法。 |
| `f` | 显示浮点数。 |
| `g` | 显示科学计数法或浮点数，较短者优先。 |
| `o` | 显示八进制值。 |
| `s` | 显示一个字符串。 |
| `x` | 显示十六进制值。 |
| `X` | 使用大写字母显示十六进制值。 |

除了控制字母，还可以使用修饰符进行更多控制：

- `width`：指定输出最小宽度的数值值。如果输出较短，`printf` 会用空格填充。如果输出长于 `width`，则会覆盖 `width` 值。
- `prec`：一个数值值，指定浮点数小数点右侧位数，或字符串中的最大字符数。
- `-`（负号）：负号表示使用左对齐而不是右对齐。

#### `printf` 示例

以下展示了如何使用 `printf` 格式化输出：

```bash
$ gawk '{
  total = 0
  for (i = 1; i < 4; i++)
  {
    total += $i
  }
  avg = total / 3
  print "Average:",avg
}' data5
Average: 128.333
Average: 137.667
Average: 176.667
$
```

结合 `width` 和格式说明符使用 `printf`：

```bash
$ gawk '{
  total = 0
  i = 1
  while (i < 4)
  {
    total += $i
    i++
  }
  avg = total / 3
  printf "Average: %10.3f\n", avg
}' data5
Average:   128.333
Average:   137.667
Average:   176.667
$
```

使用 `printf` 显示科学计数法：

```bash
$ gawk '{
  total = 0
  i = 1
  while (i < 4)
  {
    total += $i
    i++
  }
  avg = total / 3
  printf "Average: %.3e\n", avg
}' data5
Average: 1.283e+02
Average: 1.377e+02
Average: 1.767e+02
$
```

每个 `printf` 输出都显示在同一行。为了能够结束行，`END` 部分会打印一个换行符。

接下来，让我们使用一个修饰符来格式化第一个字符串值：

```bash
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%16s  %s\n", $1, $4}' data2
```

```
   Riley Mullen  (312)555-1234
  Frank Williams  (317)555-9876
      Haley Snell  (313)555-4938
$
```

通过添加 `16` 修饰符值，我们强制第一个字符串的输出使用 16 个空格。默认情况下，`printf` 命令使用右对齐将数据放置在格式空间中。要将其变为左对齐，只需在修饰符前添加一个负号：

```bash
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%-16s  %s\n", $1, $4}' data2
```

```
Riley Mullen      (312)555-1234
Frank Williams    (317)555-9876
Haley Snell        (313)555-4938
$
```

现在看起来非常专业了！

`printf` 命令在处理浮点数值时也非常好用。通过为变量指定格式，你可以让输出看起来更加均匀：

```bash
$ gawk '{
> total = 0
> for (i = 1; i < 4; i++)
> {
>     total += $i
> }
> avg = total / 3
> printf "Average: %5.1f\n",avg
> }' data5
Average: 128.3
Average: 137.7
Average: 176.7
$
```

通过使用 `%5.1f` 格式说明符，你可以强制 `printf` 命令将浮点数保留一位小数。

### 内置函数

`gawk` 编程语言提供了许多内置函数，可以执行常见的数学、字符串甚至时间函数。你可以在 `gawk` 程序中使用这些函数，帮助减少脚本中的编码需求。本节将带你介绍 `gawk` 中提供的各种内置函数。

### 数学函数

如果你用过任何语言进行编程，你可能已经熟悉在代码中使用内置函数来执行常见的数学函数。`gawk` 编程语言不会让那些寻求高级数学功能的人失望。

[表 21.4] 显示了 `gawk` 中提供的数学内置函数。

#### 表 21.4 gawk 数学函数

| 函数 | 说明 |
| :--- | :--- |
| `atan2(x, y)` | `x / y` 的反正切，`x` 和 `y` 以弧度为单位。 |
| `cos(x)` | `x` 的余弦，`x` 以弧度为单位。 |
| `exp(x)` | `x` 的指数。 |
| `int(x)` | `x` 的整数部分，向 0 截断。 |
| `log(x)` | `x` 的自然对数。 |
| `rand()` | 大于 0 且 1 的随机浮点数。 |
| `sin(x)` | `x` 的正弦，`x` 以弧度为单位。 |
| `sqrt(x)` | `x` 的平方根。 |
| `srand(x)` | 指定计算随机数的种子值。 |

虽然 `gawk` 没有详尽的数学函数列表，但它确实提供了标准数学处理所需的某些元素。`int()` 函数产生值的整数部分，但它不会对值进行四舍五入。它的行为类似于其他编程语言中的地板函数（floor function）。它产生的是该值与 0 之间最接近的整数。

这意味着值 `5.6` 的 `int()` 函数将返回 `5`，而值 `-5.6` 的 `int()` 函数将返回 `-5`。

`rand()` 函数非常适合创建随机数，但你需要使用一些技巧来获取有意义的值。`rand()` 函数返回一个 0 到 1 之间的随机数（不包括 1）。要获取更大的值，你需要对返回的值进行扩展。产生较大数的常用方法是使用 `int()` 函数：

```bash
x = int(rand() * 100)
```

`gawk` 编程语言还提供了一些位运算。这些在处理二进制数据时非常有用：

- `and(x, y)`: 位与操作。
- `or(x, y)`: 位或操作。
- `xor(x, y)`: 位异或操作。
- `compl(x)`: 位非操作。
- `lshift(x, n)`: 位左移。
- `rshift(x, n)`: 位右移。

### 字符串函数

`gawk` 编程语言还提供了几个用于处理字符串的函数：

| 函数 | 说明 |
| :--- | :--- |
| `asort(s)` | 根据元素值对数组 `s` 排序。生成的索引指示排序。或者，排序后的数组存储在 `d` 中。 |
| `asorti(s)` | 根据索引值对数组 `s` 排序。生成的索引指示排序。或者，排序后的数组存储在 `d` 中。 |
| `gensub(r, s, h, t)` | 在变量 `$0` 或目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果 `h` 是以 `g` 或 `G` 开头的字符串，则将匹配文本替换为 `s`。如果 `h` 是数字，它代表替换第几次出现的 `r`。 |
| `gsub(r, s, t)` | 在变量 `$0` 或目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果找到，全局替换字符串 `s`。 |
| `index(s, t)` | 返回字符串 `t` 在字符串 `s` 中的索引，如果未找到则返回 0。 |
| `length(s)` | 返回字符串 `s` 的长度，如果没有指定，则返回 `$0` 的长度。 |
| `match(s, r, a)` | 返回正则表达式 `r` 在字符串 `s` 中出现的索引。如果指定了数组 `a`，它包含 `s` 中匹配的部分。 |
| `split(s, a, r)` | 使用 `FS` 字符或提供的正则表达式 `r` 将 `s` 拆分到数组 `a`。返回字段数。 |
| `sprintf(format, variables)` | 使用提供的 `format` 和 `variables` 返回一个与 `printf` 输出相似的字符串。 |
| `sub(r, s, t)` | 在变量 `$0` 或目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果找到，则替换第一次出现的为字符串 `s`。 |
| `substr(s, i, n)` | 返回 `s` 从索引 `i` 开始的第 `n` 个字符子串。如果没有提供 `n`，则使用 `s` 的剩余部分。 |
| `tolower(s)` | 将 `s` 中的所有字符转换为小写。 |
| `toupper(s)` | 将 `s` 中的所有字符转换为大写。 |

某些字符串函数相对自显易懂：

```bash
$ gawk 'BEGIN{x = "testing"; print toupper(x); print length(x) }'
```

```
TESTING
7
$
```

然而，某些字符串函数可能会变得相当复杂。`asort` 和 `asorti` 函数是新的 `gawk` 函数，允许你根据数据元素值（`asort`）或索引值（`asorti`）对数组变量进行排序。这里是使用 `asort` 的示例：

```bash
$ gawk 'BEGIN{
> var["a"] = 1
> var["g"] = 2
> var["m"] = 3
> var["u"] = 4
> asort(var, test)
> for (i in test)
>     print "Index:",i, " - value:",test[i]
 }'
```

```
Index: 4  - value: 4
Index: 1  - value: 1
Index: 2  - value: 2
Index: 3  - value: 3
$
```

新数组 `test` 包含了原始数组新排序后的数据元素，但索引值现在已更改为数值，指示了正确的排序顺序。

`split` 函数是将数据字段推入数组以进行进一步处理的好方法：

```bash
$ gawk 'BEGIN{ FS=","}{
> split($0, var)
> print var[1], var[5]
 }' data1
```

```
data11 data15
data21 data25
data31 data35
$
```

新数组使用顺序数字作为数组索引，从索引值 1 开始第一个字段。

### 时间函数

`gawk` 编程语言包含几个可以帮助你处理时间值的函数，见 表 21.6。

表 21.6 gawk 时间函数

| 函数 | 描述 |
| :--- | :--- |
| `mktime(datespec)` | 将以 `YYYY MM DD HH MM SS [DST]` 格式指定的日期转换为时间戳。 |
| `strftime(format [, timestamp])` | 将当前时间的时间戳（或如果提供了时间戳）格式化为指定的日期和时间，使用 `date()` shell 函数的格式。 |
| `systime()` | 返回当前时间的时间戳。 |

在处理包含你需要比较的日期的日志文件时，经常使用时间函数。通过将日期的文本表示转换为 Unix 时间（自 1970 年 1 月 1 日午夜以来的秒数），你可以轻松地比较日期。

以下是在 `gawk` 程序中使用时间函数的示例：

```bash
$ gawk 'BEGIN{
> date = systime()
> day = strftime("%A, %B %d, %Y", date)
> print day
 }'
```

```
Friday, December 28, 2010
$
```

此示例使用 `systime` 函数从系统获取当前的 Unix 时间戳，然后使用 `strftime` 函数使用 `date` shell 命令的日期格式字符将其转换为人类可读的格式。

### 自定义函数

你不局限于仅使用 `gawk` 提供的内置函数。你可以创建自己的函数并在 `gawk` 程序中使用它们。本节将向你展示如何在 `gawk` 程序中定义和使用自定义函数。

#### 定义函数

要定义你自己的函数，必须使用 `function` 关键字：

```awk
function name([variables])
{
    statements
}
```

函数名必须唯一标识你的函数。你可以从调用的 `gawk` 程序向函数传递一个或多个变量：

```awk
function printthird()
{
    print $3
}
```

此函数将打印记录中的第三个数据字段。

函数还可以使用 `return` 语句返回值：

```awk
return value
```

该值可以是一个变量，也可以是一个求值为该值的表达式：

```awk
function myrand(limit)
{
    return int(limit * rand())
}
```

你可以将函数返回的值赋值给 `gawk` 程序中的变量：

```awk
x = myrand(100)
```

变量将包含函数返回的值。

#### 使用你的函数

当你定义一个函数时，它必须在定义任何编程部分（包括 `BEGIN` 部分）之前单独出现。这初看起来可能有点奇怪，但它有助于将函数代码与 `gawk` 程序的其余部分分开：

```bash
$ gawk '
> function myprint()
> {
>     printf "%-16s - %s\n", $1, $4
> }
> BEGIN{FS="\n"; RS=""}
> {
>     myprint()
> }' data2
```



```text
Riley Mullen      - (312)555-1234
Frank Williams    - (317)555-9876
Haley Snell       - (313)555-4955

$
```

此示例使用`systime`函数从系统获取当前的 Unix 时间戳，然后使用`strftime`函数，使用`date` shell 命令的日期格式字符将其转换为人类可读的格式。

> 注：由于原文中存在大量重复内容，译文已根据要求去除了重复部分，保留了核心逻辑结构。

下一章将稍微调整一下方向。它将检查你在 Linux 脚本编写过程中可能会遇到的其他几种 shell 环境（shell）。虽然`bash` shell 是 Linux 中最常用的 shell，但它并不是唯一的。了解一些其他可用的 shell 以及它们与`bash` shell 的区别是有帮助的。

# 读累了记得休息一会哦~

**公众号：古德猫宁李**

- 电子书搜索下载
- 书单分享
- 书友学习交流

**网站：**[沉金书屋](https://www.chenjin5.com)

- 电子书搜索下载
- 电子书打包资源分享
- 学习资源分享

# 第 22 章：使用替代性 Shell

## 本章内容

- 了解`dash` shell
- 在`dash` shell 中编程
- 介绍`zsh` shell
- 为`zsh`编写脚本

虽然`bash` shell 是 Linux 发行版中广泛使用的 shell，但它并不是唯一的。现在你已经了解了标准的 Linux`bash` shell 以及你用它能做什么，是时候检查一下 Linux 世界中其他几种 shell 了。本章描述了你在 Linux 之旅中可能会遇到的另外两种 shell，以及它们与`bash` shell 的区别。

## 什么是 dash Shell？

Debian`dash` shell 有着有趣的历史。它是`ash` shell 的直接后代，`ash`是 Unix 系统上原始 Bourne shell 的简单副本（请参见第 1 章）。Kenneth Almquist 为 Unix 系统创建了一个小型的 Bourne shell 版本，并称之为 Almquist shell，后来缩短为`ash`。这个原始版本的`ash` shell 极其小巧且运行快速，但缺乏许多高级功能（例如命令行编辑或历史记录功能），使得它很难作为交互式 shell 使用。

NetBSD Unix 操作系统采用了`ash` shell，并且至今仍将其作为默认 shell 使用。NetBSD 开发者通过添加若干个新功能对`ash` shell 进行了定制，使其更接近 Bourne shell。这些新功能包括使用`emacs`和`vi`编辑器命令进行命令行编辑，以及用于召回之前输入命令的`history`命令。这个版本的`ash` shell 也被 FreeBSD 操作系统作为默认登录 shell 使用。

Debian Linux 发行版在其版本中创建了自己的`ash` shell 版本（称为`Debian ash`或`dash`）。在大多数情况下，`dash`复制了 NetBSD 版本`ash` shell 的功能，提供了高级的命令行编辑能力。

然而，为了增加 shell 的复杂性，`dash` shell 实际上并不是许多基于 Debian 的 Linux 发行版中的默认 shell。由于`bash` shell 在 Linux 中的流行，绝大多数基于 Debian 的 Linux 发行版使用`bash` shell 作为正常的登录 shell，而仅将`dash` shell 作为安装脚本的快速启动 shell，用于安装发行版文件。

例外是流行的 Ubuntu 发行版。这经常困扰 shell 脚本程序员，并导致在 Linux 环境中运行 shell 脚本时出现大量问题。Ubuntu Linux 发行版使用`bash` shell 作为默认交互式 shell，但将`dash` shell 作为默认的`/bin/sh` shell。这一“特性”真的困扰了 shell 脚本程序员。

正如你在第 10 章看到的，每个 shell 脚本都必须以一行声明脚本所用 shell 的代码开头。在我们的`bash`脚本中，我们一直使用：

```bash
#!/bin/bash
```

这告诉 shell 使用位于`/bin/bash`的 shell 程序来执行脚本。在 Unix 世界中，默认 shell 一直是`/bin/sh`。许多熟悉 Unix 环境的 shell 程序员会将此复制到他们的 Linux shell 脚本中：

```bash
#!/bin/sh
```

在大多数 Linux 发行版中，`/bin/sh`文件指向`/bin/bash` shell 程序的符号链接（参见第 3 章）。这允许你轻松地将为 Unix Bourne shell 设计的 shell 脚本移植到 Linux 环境，而无需修改它们。

遗憾的是，Ubuntu Linux 发行版将`/bin/sh`文件链接到了`/bin/dash` shell 程序。由于`dash` shell 只包含了原始 Bourne shell 中命令的子集，这可能会（通常也是）导致某些 shell 脚本无法正常工作。

下一节将带你了解`dash` shell 的基础以及它与`bash` shell 的区别。如果你编写可能需要在 Ubuntu 环境下运行的 bash 脚本，了解这一点尤为重要。

## dash Shell 特性

虽然`bash` shell 和`dash` shell 都是模仿 Bourne shell 设计的，但它们之间存在差异。本节将带你了解 Debian`dash` shell 中的功能，以便在我们深入研究 shell 脚本功能之前让你熟悉`dash` shell 的工作原理。

## dash 命令行参数

`dash` shell 使用命令行参数来控制其行为。[表 22.1] 列出了命令行参数并描述了每个参数的作用。

### 表 22.1：dash 命令行参数

| 参数 | 说明 |
| :--- | :--- |
| `-a` | 导出所有分配给 shell 的变量。 |
| `-c` | 从指定的命令字符串读取命令。 |
| `-e` | 如果不是交互模式，当任何未测试的命令失败时立即退出。 |
| `-f` | 显示路径通配符。 |
| `-n` | 如果不是交互模式，读取命令但不执行。 |
| `-u` | 当尝试扩展未设置的变量时，向`STDERR`写入错误信息。 |
| `-v` | 在读取时将输入写入`STDERR`。 |
| `-x` | 在执行每个命令时将该命令写入`STDERR`。 |
| `-I` | 在交互模式下忽略输入中的 EOF 字符。 |
| `-i` | 强制 shell 在交互模式下运行。 |
| `-m` | 开启作业控制（交互模式下默认启用）。 |
| `-s` | 从`STDIN`读取命令（在无文件参数时的默认行为）。 |
| `-E` | 启用`emacs`命令行编辑器。 |
| `-V` | 启用`vi`命令行编辑器。 |

Debian 在原始的`ash` shell 命令行参数列表中仅添加了几个额外的命令行参数。`-E`和`-V`命令行参数开启了`dash` shell 的特殊命令行编辑功能。

`-E`命令行参数允许你使用`emacs`编辑器命令来编辑命令行文本（参见第 9 章）。你可以使用`Ctrl`和`Meta`键组合使用所有的`emacs`命令来操纵单行文本。

`-V`命令行参数允许你使用`vi`编辑器命令来编辑命令行文本（再次，参见第 9 章）。此功能允许你通过`Esc`键在命令行上的普通模式和 vi 编辑器模式之间切换。当你处于 vi 编辑器模式时，可以使用所有的标准`vi`编辑器命令（例如使用`x`删除字符，使用`i`插入文本）。一旦完成命令行编辑，你必须再次按下`Esc`键退出 vi 编辑器模式。

## dash 环境变量

`dash` shell 使用许多默认环境变量来跟踪信息，你也可以创建自己的环境变量。本节描述了这些环境变量以及`dash`如何处理它们。

### 默认环境变量

[表 22.2] 显示了默认的`dash`环境变量并描述了它们的用途。

### 表 22.2：dash shell 环境变量

| 变量 | 描述 |
| :--- | :--- |
| `CDPATH` | `cd`命令使用的搜索路径。 |
| `HISTSIZE` | 存储在历史文件中的行数。 |
| `HOME` | 用户默认登录目录。 |
| `IFS` | 输入字段分隔符。默认值是`空格`、`制表符`和`换行符`。 |
| `MAIL` | 用户邮箱文件名。 |
| `MAILCHECK` | 检查邮箱文件是否有新邮件的频率。 |
| `MAILPATH` | 一个由冒号分隔的多个邮箱文件名列表。如果设置，此值将覆盖`MAIL`环境变量。 |
| `OLDPWD` | 上一个工作目录的值。 |
| `PATH` | 可执行文件的默认搜索路径。 |
| `PPID` | 当前 shell 的父进程的进程 ID（PID）。 |
| `PS1` | 主 shell 命令行界面提示符。 |
| `PS2` | 次级 shell 命令行界面提示符。 |
| `PS4` | 当启用执行跟踪时，在每行之前打印的字符。 |
| `PWD` | 当前工作目录的值。 |
| `TERM` | shell 的默认终端设置。 |

你应该注意，`dash`环境变量与`bash`中使用的环境变量非常相似（参见第 5 节）。这并非偶然。请记住，`dash` shell 和`bash` shell 都是 Bourne 壳（Bourne shell）的扩展，因此它们都包含了它的许多特性。然而，由于追求简洁，`dash` shell 包含的环境变量远少于`bash` shell。在`ash` shell 环境下创建 shell 脚本时，你需要考虑到这一点。

`dash` shell 使用`set`命令来显示环境变量：

```bash
$ set
COLORTERM=''
DESKTOP_SESSION='default'
DISPLAY=':0.0'
DM_CONTROL='/var/run/xdmctl'
GS_LIB='/home/atest/.fonts'
HOME='/home/atest'
IFS=' 	
'
KDEROOTHOME='/root/.kde'
KDE_FULL_SESSION='true'
KDE_MULTIHEAD='false'
KONSOLE_DCOP='DCOPRef(konsole-5293,konsole)'
KONSOLE_DCOP_SESSION='DCOPRef(konsole-5293,session-1)'
LANG='en_US'
LANGUAGE='en'
LC_ALL='en_US'
LOGNAME='atest'
OPTIND='1'
PATH='/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'
PPID='5293'
PS1='$  '
PS2='>  '
PS4='+  '
PWD='/home/atest'
SESSION_MANAGER='local/testbox:/tmp/.ICE-unix/5051'
SHELL='/bin/dash'
SHLVL='1'
TERM='xterm'
USER='atest'
XCURSOR_THEME='default'
_='ash'
$
```

你的默认`dash` shell 环境很可能不同，因为不同的 Linux 发行版在登录时分配不同的默认环境变量。

### 位置参数

除了默认环境变量外，`dash` shell 还为命令行中定义的任何参数分配特殊变量。以下是`dash` shell 可用的位置参数变量：

- `$0`：shell 的名称
- `$n`：第 n 个位置参数
- `$*`：包含所有参数内容的单个值，由`IFS`环境变量中的第一个字符分隔，如果`IFS`未定义则用空格分隔
- `$@`：展开为由所有命令行参数组成的多个参数
- `$#`：位置参数的数量
- `$?`：最近一次命令的退出状态
- `$-`：当前的选项标志
- `$$`：当前 shell 的进程 ID（PID）
- `$!`：最近一次后台命令的进程 ID（PID）

所有的`dash`位置参数都模拟了`bash` shell 中可用的相同位置参数。你可以像在`bash` shell 中一样，在你的 shell 脚本中使用每个位置参数。

### 用户定义的环境变量

`dash` shell 还允许你设置自己的环境变量。与`bash`一样，你可以通过赋值语句（`assign` statement）在命令行上定义新的环境变量：

```bash
$ testing=10
$ echo $testing
10
$
```

默认情况下，环境变量只在定义它们的 shell 会话中可见。要让一个环境变量在子 shell 或进程中可见，你必须使用`export`命令：

```bash
$ testing=10 ; export testing
$ dash
$ echo $testing
10
$
```

如果没有`export`命令，用户定义的环境变量只在当前 shell 或进程中可见。

> **注意**
>
> `dash`变量和`bash`变量之间有一个巨大的区别。`dash` shell 不支持变量数组。这个微小的特性为高级 shell 脚本编写者带来了各种问题。

### dash 内置命令

与`bash` shell 一样，`dash` shell 包含一组它能够识别的内置命令。你可以直接从命令行界面使用这些命令，也可以将它们整合到你的 shell 脚本中。[表 22.3] 列出了`dash` shell 内置命令。

#### 表 22.3：dash shell 内置命令

| 命令 | 说明 |
| :--- | :--- |
| `alias` | 创建别名字符串来表示文本字符串。 |
| `bg` | 在后台模式下继续指定的作业。 |
| `cd` | 切换到指定的目录。 |
| `echo` | 显示字符串和环境变量。 |
| `eval` | 用空格连接所有参数。 |
| `exec` | 用指定的命令替换 shell 进程。 |
| `exit` | 终止 shell 进程。 |
| `export` | 导出指定的环境变量供所有子 shell 使用。 |
| `fc` | 列出、编辑或重新执行之前在命令行上输入的命令。 |
| `fg` | 在前台模式下继续指定的作业。 |
| `getopts` | 从参数列表中获取选项和参数。 |
| `hash` | 维护并检索最近命令及其位置的哈希表。 |
| `pwd` | 显示当前工作目录的值。 |
| `read` | 从`STDIN`读取一行并将值赋值给变量。 |
| `readonly` | 从`STDIN`读取一行到不可更改的变量中。 |
| `printf` | 使用格式化字符串显示文本和变量。 |
| `set` | 列出或设置选项标志和环境变量。 |
| `shift` | 将位置参数向后移动指定的次数。 |
| `test` | 评估表达式，为真则返回 0，为假则返回 1。 |
| `times` | 显示 shell 及所有 shell 进程的累计用户和系统时间。 |
| `trap` | 当 shell 接收到指定信号时解析并执行操作。 |
| `type` | 解析指定的名称并显示解析结果（别名、内置、命令、关键字）。 |
| `ulimit` | 查询或设置进程的限制。 |
| `umask` | 设置默认文件和目录权限的值。 |
| `unalias` | 移除指定的别名。 |
| `unset` | 从导出的变量中移除指定的变量或选项标志。 |
| `wait` | 等待指定的作业完成并返回退出状态。 |

你可能已经在`bash` shell 中识别出所有这些内置命令了。`dash` shell 支持与`bash` shell 许多相同的内置命令。你会发现，没有用于命令历史文件的命令，也没有用于目录栈的命令。`dash` shell 不支持这些特性。

### 在 dash 中编写脚本

遗憾的是，`dash` shell 并不识别`bash` shell 的所有脚本功能。为`bash`环境编写的 shell 脚本在`dash` shell 中运行时通常会失败，给 shell 脚本编程人员带来各种困扰。本节描述了为了让你的 shell 脚本在`dash` shell 环境中正常运行而需要注意的差异。

#### 创建 dash 脚本

你现在可能猜到了，为`dash` shell 创建 shell 脚本与为`bash` shell 创建 shell 脚本非常相似。你应该始终在脚本中指定要使用的 shell，以确保脚本以正确的 shell 运行。

你在 shell 的第一行这样做：

```bash
#!/bin/dash
```



你也可以在这一行指定 shell 命令行参数，正如之前在“dash 命令行参数”节中演示的那样。

### 不起作用的内容

遗憾的是，由于`dash` shell 仅是 Bourne shell 特性的子集，bash shell 脚本中的某些内容在`dash` shell 中无法工作。这些内容通常被称为 bashisms（bash 特性）。本节简要总结了你可能习惯在 bash shell 脚本中使用、但在 dash shell 环境下无法工作的 bash shell 特性。

## 使用算术运算

第 10 章展示了在 bash 脚本中表示数学运算的三种方法：

*   使用`expr`命令：`expr operation`
*   使用方括号：`$[ operation ]`
*   使用双括号：`$(( operation ))`

dash shell 支持`expr`命令和双括号方法，但不支持方括号方法。如果你有大量使用方括号的数学运算，这可能会一个问题：

```bash
$ cat test5
#!/bin/dash
# testing mathematical operations
value1=10
value2=15
value3=$[ $value1 * $value2 ]
echo “The answer is $value3”
$ ./test5
./test5: 7: value1: not found
The answer is
$
```

在 dash shell 脚本中执行数学运算的正确格式是使用双括号方法：

```bash
$ cat test5b
#!/bin/dash
# testing mathematical operations
value1=10
value2=15
value3=$(( $value1 * $value2 ))
echo “The answer is $value3”
$ ./test5b
The answer is 150
$
```

现在 shell 可以正常执行计算了。

### test 命令

虽然 dash shell 支持`test`命令，但你必须小心如何使用它。bash shell 版本的`test`命令与 dash shell 版本略有不同。

bash shell`test`命令允许你使用双等号（`==`）来测试两个字符串是否相等。这是为了适应其他编程语言中使用这种格式的程序员而增加的功能：

```bash
$ cat test6
#!/bin/bash
# testing the == comparison
test1=abcdef
test2=abcdef
if [ $test1 == $test2 ]
then
    echo “They're the same!”
else
    echo “They're different”
fi
$ ./test6
They're the same!
$
```

这很简单。然而，如果你在 dash shell 环境中运行此脚本，你将得到一个不受欢迎的结果：

```bash
$ ./test6
[: ==: unexpected operator
They're different
$
```

dash shell 中提供的`test`命令不识别用于文本比较的`==`符号。相反，它只识别`=`符号。如果你将文本比较符号更改为单个等号，那么在 bash 和 dash shell 环境中一切都会正常：

```bash
$ cat test7
#!/bin/dash
# testing the = comparison
test1=abcdef
test2=abcdef
if [ $test1 = $test2 ]
then
    echo “They're the same!”
else
    echo “They're different”
fi
$ ./test7
They're the same!
$
```

这个小 bash 特性让许多 shell 程序员为此感到了数小时的沮丧！

### echo 语句选项

简单的`echo`语句也是 dash shell 程序员的另一个沮丧来源。它在 dash 和 bash shell 中的行为并不相同。

在 bash shell 中，如果你想在输出中显示特殊字符，必须使用`-e`命令行参数：

```bash
echo -e “This line contains\ta special character”
```

`echo`语句包含表示制表符的特殊字符`\t`。如果没有`-e`命令行参数，bash 版本的`echo`语句会忽略特殊字符。这里有一个在 bash shell 中演示此点的测试：

```bash
$ cat test8
#!/bin/bash
# testing echo commands
echo “This is a normal test”
echo “This test uses a\tspecial character”
echo -e “This test uses a\tspecial character”
echo -n “Does this work: ”
read test
echo “This is the end of the test”
$ ./test8
This is a normal test
This test uses a\tspecial character
This test uses a  special character
Does this work: N
This is the end of the test
$
```

没有使用`-e`命令行参数的`echo`语句将`\t`字符作为普通文本显示，因此为了获取制表符，必须使用`-e`命令行参数。

在 dash shell 中，情况有点不同。dash shell 中的`echo`语句会自动识别并显示特殊字符。由于由于，没有`-e`命令行参数。如果你尝试在 dash 环境中运行相同的脚本，你会得到以下输出：

```bash
$ ./test8
This is a simple test
This line uses a         special character
-e This line uses a      special character
Does this work: N
This is the end of the test
$
```

如从输出所示，dash shell 版本的`echo`命令在没有`-e`命令行参数的情况下也能很好地识别行中的特殊字符，但对于包含`-e`命令行参数的行行，它会产生困惑并将`-e`视为普通文本显示。

遗憾的是，这个问题没有简单的解决方案。如果你必须编写可以在 bash 和 dash shell 环境中共同运行的脚本，最佳解决方案是使用`printf`命令显示文本。该命令在两种 shell 环境中的工作方式相同，并且可以正常显示特殊字符。

### function 命令

第 16 章向你展示了如何在 shell 脚本中定义自己的函数。bash shell 支持两种定义函数的方法。第一种方法是使用`function`语句：

```bash
function name {
commands
}
```

`name`属性分配给函数的唯一名称。脚本中定义的每个函数必须分配一个唯一名称。`commands`是组成函数的一个或多个 shell 命令。当你调用函数时，bash shell 会按照这些命令在函数中出现的顺序执行它们，就像在普通脚本一样。

bash shell 中定义函数的第二种格式更符合其他语言中函数的定义方式：

```bash
name() {
commands
}
```

名称后面的空括号表示你正在定义一个函数。dash shell 不`function`语句。如果你尝试在 dash 中运行为 bash 设计的函数，将得到一个错误：

```bash
$ cat test9
#!/bin/dash
# testing functions
function func1 {
    echo “This is an example of a function”
}
func1
$ ./test9
./test9: 4: Syntax error: "(" unexpected
$
```

dash shell 没有将函数代码分配给函数，而是执行了函数内部的代码。

如果你正在编写可能在 dash 环境中使用的脚本，请务必使用定义函数的定义方法：

```bash
$ cat test10
#!/bin/dash
# testing functions
func1() {
    echo “This is an example of a function”
}
count=1
while [ $count -le 5 ]
do
    func1
    count=$(( $count + 1 ))
done
echo “This is the end of the test”
$ ./test10
This is an example of a function
This is an example of a function
This is an example of a function
This is an example of a function
This is an example of a function
This is the end of the loop
This is an example of a function
This is the end of the test
$
```

现在 dash shell 正常识别了脚本中定义的函数，并能够在脚本中使用它。

## zsh Shell

另一个你可能会遇到的流行 shell 是 Z shell（称为 zsh）。zsh shell 是由 Paul Falstad 开发的开源 Unix shell。它吸收了所有现有 shell 的想法，并添加了许多独特的功能，创建一个为程序员设计的全功能高级 shell。

以下是使 zsh shell 独特的特性：

*   改进的 shell 选项处理
*   shell 兼容模式

### 可加载模块

在所有这些特性中，可加载模块是 shell 设计中最高级的特性。正如你在`bash`和`dash` shell 中看到的，每个 shell 都包含一组内置命令，这些命令不需要外部实用程序即可直接使用。内置命令的优点是执行速度快。shell 在运行命令之前不需要将实用程序加载到内存中；内置命令已经存在于 shell 内存中，随时待命。

`zsh` shell 提供了一组核心内置命令，并具备添加额外命令模块的能力。每个命令模块都为特定场景（如网络支持和高级数学函数）提供一组额外的内置命令。你可以只添加你认为在特定情况下所需要的模块。

这一特性提供了一种极佳的方法，既可以在需要 shell 占用空间较小且命令较少的情况下来限制`zsh` shell 的大小，也可以在需要更快执行速度的情况下扩展可用内置命令的数量。

## zsh Shell 的组成

本节将带你了解`zsh` shell 的基础知识，展示可用的（或通过安装模块添加的）内置命令，以及`zsh` shell 使用的命令行参数和环境变量。

### Shell 选项

大多数 shell 使用命令行参数来定义行为。`zsh` shell 使用`set`来自定义行为。

### 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| `-c` | 执行指定的命令。 |
| `-i` | 以交互模式启动。 |
| `-s` | 从`STDIN`执行。 |
| `-p` | 强制以用户身份运行。 |
| `-r` | 限制用户。 |
| `-t` | 执行单个命令。 |

### Shell 模拟

以下选项分为几类：

- **切换目录**: `cd`
- **补全**:
- **扩展与通配符**:
- **历史记录**: `echo`
- **初始化**:
- **输入/输出**:
- **作业控制**:
- **提示符**:
- **脚本**: `while`, `do`, `done`
- **陷阱 (Traps)**:
- **扩展与通配符**: `和`*`
- **zle** (编辑器)
- **别名 (Aliases)**:
- **Shell 状态**: `zle`

### 初始化

有几个选项用于处理 shell 的启动特性：

- `all_export`: 所有参数和变量都会导出到子 shell 进程。
- `global_export`: 导出到环境的参数不会变为函数的局部。
- `global_rcs`: 如果未设置，`zsh` shell 不运行全局启动文件，但仍会运行本地启动文件。
- `rcs`: 如果未设置，zsh shell 会运行`/etc/zshenv`启动文件，但不运行其他。

初始化选项允许你指定在 shell 环境中运行哪些（如果有）`zsh` shell 启动文件。你也可以在启动文件中设置这些值，以限制 shell 执行哪些文件。

### 脚本与函数

脚本和函数选项允许你自定义`zsh` shell 中的脚本编写环境。这是设置函数在 shell 中执行方式的一种方便方法。

- `c_bases`: 使用 C 格式 (`0xdddd`) 而不是 shell 格式 (`16#dddd`) 显示十六进制。
- `err_exit`: 如果命令以非零状态码退出，则执行`ZERR`陷阱中的命令并退出。
- `err_return`: 如果命令具有非零状态码，则立即从封装函数返回。
- `eval_lineno`: 如果设置，使用`eval`内置命令评估的表达式的行号将与 shell 环境的其他部分分开跟踪。
- `exec`: 执行命令。如果未设置此选项，则读取命令并报告错误，但不执行这些命令。
- `function_argzero`: 将`$0`设置为函数或脚本的名称。
- `local_options`: 如果设置，当 shell 函数返回时，将恢复在函数之前设置的所有选项。
- `local_traps`: 如果设置，当在函数内部设置信号陷获（trap）时，在函数退出时将恢复陷获的先前的状态。
- `multios`: 当尝试进行多次重定向时，执行隐式的`tee`或`cat`命令。
- `octal_zeroes`: 将任何以零开头的整数字符串解释为八进制数。
- `typeset_silent`: 如果未设置，使用`typeset`配合参数名将显示参数的当前值。
- `verbose`: 显示 shell 读取的 shell 输入行。
- `xtrace`: 在 shell 执行命令时，显示命令及其参数。

zsh shell 允许你自定义在退出 shell 中定义的函数时发生的大许多功能。

### 内置命令

zsh shell 的独特之处在于，它允许你扩展 shell 中可用的内置命令。这为许多不同的应用程序提供了丰富的、快速的工具。

本节描述了核心内置命令，以及在编写时可用的各种模块。

### 核心内置命令

zsh shell 的核心包含了你在其他 shell 中常见的各种内置命令。表 22.5 描述了供你使用的的内置命令。

**表 22.5 zsh 核心内置命令**

| 命令 | 描述 |
| :--- | :--- |
| `alias` | 为命令和参数定义别名。 |
| `autoload` | 将 shell 函数预加载到内存中以便更快地访问。 |
| `bg` | 在后台模式下执行作业。 |
| `bindkey` | 将组合键绑定到命令。 |
| `builtin` | 执行指定的内置命令，而不是同名的可执行文件。 |
| `bye` | 与`exit`相同。 |
| `cd` | 更改当前工作目录。 |
| `chdir` | 更改当前工作目录。 |
| `command` | 将指定的命令作为外部文件执行，而不是函数或内置命令。 |
| `declare` | 设置变量的数据类型（同于`typeset`）。 |
| `dirs` | 显示目录栈的内容。 |
| `disable` | 临时禁用指定的哈希表元素。 |
| `disown` | 从作业表中移除指定的作业。 |
| `echo` | 显示变量和文本。 |
| `emulate` | 设置 zsh 模拟另一个 shell，例如 Bourne、Korn 或 C shell。 |
| `enable` | 启用指定的哈希表元素。 |
| `eval` | 在当前 shell 进程中执行指定的命令和参数。 |
| `exec` | 执行指定的命令和参数并替换当前的 shell 进程。 |
| `exit` | 退出 shell。 |
| `export` | 将变量导出到环境变量。 |
| `false` | 返回非零退出状态。 |
| `fc` | 列出或编辑历史。 |
| `fg` | 将作业置于前台。 |
| `float` | 声明浮点变量。 |
| `functions` | 列出定义的函数。 |
| `getopts` | 解析行选项。 |
| `hash` | 重建哈希表。 |
| `history` | 列出或操作历史。 |
| `integer` | 声明整数变量。 |
| `jobs` | 列出活动作业。 |
| `kill` | 向进程发送信号。 |
| `let` | 执行算术运算。 |
| `limit` | 设置或显示资源限制。 |
| `local` | 在函数内定义变量。 |
| `log` | 显示登录历史。 |
| `logout` | 与`exit`相同，但用于登录 shell。 |
| `popd` | 更改目录并从栈弹出。 |
| `print` | 显示文本。 |



| `printf` | 打印格式化字符串。 |
| `pushd` | 更改目录并推入栈。 |
| `pwd` | 显示当前工作目录。 |
| `read` | 将输入读取到变量。 |
| `readonly` | 声明只读变量。 |
| `rehash` | 重建哈希表。 |
| `set` | 设置选项或参数。 |
| `setopt` | 设置 shell 选项。 |
| `shift` | 移动位置参数。 |
| `source` | 在当前 shell 中执行文件内容。 |
| `suspend` | 挂起 shell。 |
| `test` | 如果条件为真则返回 0。 |
| `times` | 显示用户系统时间。 |
| `trap` | 处理信号。 |
| `true` | 返回零退出状态。 |
| `ttyctl` | 控制终端设置。 |
| `type` | 显示命令如何被解释。 |
| `typeset` | 设置或显示变量的属性。 |
| `ulimit` | 设置或显示资源限制。 |
| `umask` | 设置默认文件权限。 |
| `unalias` | 移除别名。 |
| `unfunction` | 移除函数。 |
| `unhash` | 从哈希表中移除命令。 |
| `unlimit` | 移除资源限制。 |
| `unset` | 移除变量。 |
| `unsetopt` | 移除 shell 选项。 |
| `wait` | 等待作业完成。 |
| `whence` | 显示命令如何被解释。 |
| `where` | 查找命令的路径。 |
| `which` | 显示命令的路径。 |
| `zcompile` | 编译函数或脚本。 |
| `zmodload` | 加载 zsh 模块。 |

zsh shell 在提供内置命令方面绝非弱！你应该能对应的 bash 命令识别出大部分命令。zsh shell 内置命令最重要的特性是模块。

## 附加模块

有一个长长的模块列表为 zsh shell 提供额外的内置命令，随着资源丰富的程序员创建新模块，这个列表在不断增长。表 22.6 显示了编写时可用的模块。

| 模块 | 描述 |
| :--- | :--- |
| `zsh/cap` | POSIX 兼容命令 |
| `zsh/clone` | 将运行中的 shell 克隆到另一个终端的命令 |
| `zsh/compctl` | 控制命令补全的命令 |
| `zsh/complete` | 命令行补全命令 |
| `zsh/complist` | 命令行补全列表扩展的命令 |
| `zsh/computil` | 用于命令行补全的实用命令 |
| `zsh/datetime` | 额外的日期和时间命令及变量 |
| `zsh/deltochar` | 模拟 emacs 功能的行编辑器函数 |
| `zsh/files` | 基础文件处理命令 |
| `zsh/mapfile` | 通过关联数组访问外部文件 |
| `zsh/mathfunc` | 额外的科学函数 |
| `zsh/parameter` | 通过关联数组访问命令哈希表 |
| `zsh/pcre` | 扩展正则表达式库 |
| `zsh/sched` | 用于定时命令执行的调度命令 |
| `zsh/net/socket` | Unix 域套接字支持 |
| `zsh/stat` | 访问 stat 系统调用以提供系统统计信息 |
| `zsh/system` | 各种底层系统功能的接口 |
| `zsh/net/tcp` | 访问 TCP 套接字 |
| `zsh/termcap` | `termcap` 数据库的接口 |
| `zsh/terminfo` | `terminfo` 数据库的接口 |
| `zsh/zftp` | 专用的 FTP 客户端命令 |
| `zsh/zle` | zshell 行编辑器 |
| `zsh/zleparameter` | 使用变量修改 `zle` |
| `zsh/zprof` | 允许对 shell 函数进行性能分析 |
| `zsh/zpty` | 在伪终端启动命令 |
| `zsh/zselect` | 文件描述符就绪时阻塞并返回 |
| `zsh/zutil` | 各种 shell 程序 |

zsh shell 模块涵盖了广泛的主题，从提供简单的命令行编辑功能到高级网络功能。zsh shell 的设计理念是提供一个基础的最小 shell 环境，并让你根据完成编程任务的需要添加相应的组件。

## 查看、添加和移除模块

`zmodload` 命令是 zsh 模块的接口。你使用此命令在 zsh shell 会话中查看、添加和移除模块。

在不带任何命令行参数的情况下使用 `zmodload` 命令，会显示当前在 zsh shell 中已安装的模块：

```
% zmodload
zsh/zutil
zsh/complete
zsh/main
zsh/terminfo
zsh/zle
zsh/parameter
%
```

不同的 zsh shell 实现默认包含不同的模块。要添加新模块，只需在 `zmodload` 命令行中指定模块名称即可：

```
% zmodload zsh/zftp
%
```

没有任何输出输出表示模块已加载。你可以执行另一个 `zmodload` 命令，新模块应该出现在已安装模块的列表中。

一旦加载了模块，与模块关联的命令就可以作为内置命令可用：

```
% zftp open myhost.com rich testing1
欢迎来到 myhost FTP 服务器。
% zftp cd test
% zftp dir
01-21-11 11:21PM    120823 test1
01-21-11 11:23PM    118432 test2
% zftp get test1 > test1.txt
% zftp close
%
```

`zftp` 命令允许你直接从 zsh shell 命令行进行完整的 FTP 会话！你可以将这些命令整合到 zsh shell 脚本中，直接从脚本执行文件传输。

要移除已安装的模块，请使用 `-u` 参数配合模块名：

```
% zmodload -u zsh/zftp
% zftp
zsh: command not found: zftp
%
```

> 注意
> > 将 `zmodload` 命令放置在 `$HOME/.zshrc` 启动文件中是一种常见做法，这样你喜欢的函数在 zsh shell 启动时会自动加载。

## 使用 zsh 编写脚本

zsh shell 的主要目的是为 shell 程序员提供一个高级的编程环境。考虑到这一点，zsh shell 提供了许多让 shell 脚本变得更容易的功能，这并不意外。

### 数学运算

正如你所预期的，zsh shell 允许你轻松地执行数学函数。过去，Korn shell 通过提供对浮点数的支持在支持数学运算方面领先。而 zsh shell 在所有的数学运算中都对浮点数提供了完全支持！

### 执行计算

zsh shell 支持两种执行数学运算的方法：

- `let` 命令
- 双括号

当你使用 `let` 命令时，应该将操作括在双引号中以允许空格：

```
% let value1=" 4 * 5.1 / 3.2 "
% echo $value1
6.3749999999999991
%
```

注意，使用浮点数会引入精度问题。为了解决这个问题，使用 `printf` 命令始终是一个好主意，并指定所需的十精度以正确显示答案：

```
% printf "%6.3f\n" $value1
6.375
%
```

现在好多了！

第二种方法是使用双括号。这种方法结合了两种定义数学运算的技术：

```
% value1=$(( 4 * 5.1 ))
% (( value2 = 4 * 5.1 ))
% printf "%6.3f\n" $value1 $value2
20.400
20.400
%
```

注意，你可以将双括号放在仅限操作周围（前面加美元符号），也可以放在整个赋值语句周围。两种方法都会产生相同的结果。

如果你不使用 `typeset` 命令来声明变量的数据类型，zsh shell 会尝试分配数据类型。看这里这个：

```
% value=10
% value2=$(( 10 / 3 ))
% echo $value2
3.3333333333333335
```

（注：此处保留了原始文本中关于计算示例的逻辑。）

与 bash shell 函数（参见第 16 节）一样，你可以在 shell 脚本中定义函数，然后使用全局变量或向函数传递参数。这里有一个使用全局变量的示例：

```bash
% cat test3
#!/bin/zsh
# testing functions in zsh
dbl() {
    value=$(( $value * 2 ))
    return $value
}
value=10
dbl
echo The answer is $?
% ./test3
The answer is 20
%
```

你并不需要将函数放在你的 shell 脚本中。zsh shell 允许你在单独的文件定义函数，当 zsh 尝试解析函数名时可以访问这些文件。

zsh shell 通过 `fpath` 环境变量来查找函数。你可以将函数文件存储在该路径下的任何目录中。以下是典型 Linux 工作站上 `fpath` 的取值：

```bash
% echo $fpath
/usr/local/share/zsh/site-functions
/usr/share/zsh/4.2.5/functions/Completion
/usr/share/zsh/4.2.5/functions/Completion/AIX
/usr/share/zsh/4.2.5/functions/Completion/BSD
/usr/share/zsh/4.2.5/functions/Completion/Base
/usr/share/zsh/4.2.5/functions/Completion/Cygwin
/usr/share/zsh/4.2.5/functions/Completion/Darwin
/usr/share/zsh/4.2.5/functions/Completion/Debian
/usr/share/zsh/4.2.5/functions/Completion/Linux
/usr/share/zsh/4.2.5/functions/Completion/Mandrake
/usr/share/zsh/4.2.5/functions/Completion/Redhat
/usr/share/zsh/4.2.5/functions/Completion/Unix
/usr/share/zsh/4.2.5/functions/Completion/X
/usr/share/zsh/4.2.5/functions/Completion/Zsh
/usr/share/zsh/4.2.5/functions/MIME
/usr/share/zsh/4.2.5/functions/Misc
/usr/share/zsh/4.2.5/functions/Prompts
/usr/share/zsh/4.2.5/functions/TCP
/usr/share/zsh/4.2.5/functions/Zftp
/usr/share/zsh/4.2.5/functions/Zle
%
```

如你所见，zsh shell 有许多地方会搜索函数名。在该系统中，你可以将我的函数放在 `/usr/local/share/zsh/site-functions` 目录下，zsh shell 将能够解析它们。

然而，在 zsh shell 解析函数之前，你必须使用 `autoload` 命令。该命令将函数加载到内存中供 shell 。这是一个独立函数的示例：

```bash
% cat dbl
#!/bin/zsh
# a function to double a value
dbl() {
    value=$(( $1 * 2 ))
    return $value
}
% cp dbl /usr/local/share/zsh/site-functions
%
```

取决于你的 Linux 系统的配置情况，你可能需要作为 root 用户（或使用 `sudo` 命令）才能将文件复制到 zsh 库中。现在，函数已经在文件中创建并存储在 `fpath` 中的目录中了。但是，如果你尝试使用它，在将其加载到内存之前，你会收到错误消息：

```bash
% dbl 5
zsh: command not found: dbl
% autoload dbl
dbl 5
```

这同样适用于 shell 脚本。如果你有一个需要使用的函数，你需要使用 `autoload` 命令来确保它可用：

```bash
% cat test4
#!/bin/zsh
# testing an external function
autoload dbl
dbl 5
echo The answer is $?
% ./test4
The answer is 10
%
```

zsh shell 的另一个有趣功能是 `zcompile` 命令。该命令处理函数文件并为 shell 创建一个“编译”后的版本。这并不是你在其他语言中常见的种类型的编译。然而，它将函数放入了一种二进制格式，使 zsh shell 能够更快地加载它。当你运行 `zcompile` 命令时，它会创建一个 `.zwc` 版本的函数文件。当 `autoload` 命令在 `fpath` 中查找它时，它将看到 `.zwc` 版本并加载它而不是文本文件。

## 总结

本章讨论了你可能会遇到的两种替代 Linux shell。bash 是作为 Debian 发行版的一部分开发的，主要用于 Ubuntu Linux 发行版中。它是 Bourne shell 的较小版本，因此支持的功能没有 bash shell 那么多，这可能会给脚本编写带来麻烦。zsh shell 经常出现在编程环境中，因为它为 shell 程序员提供了许多酷炫的功能。它使用可加载模块来加载单独的库，这使得使用高级函数像运行命令行一样简单！从复杂算法到 FTP 和 HTTP 等网络应用，有许多不同函数都有可加载的模块。本书的下一节将深入探讨你可能在 Linux 环境中运行的一些脚本应用程序。下节将如何将两个最流行的数据库包整合到系统中。

## 第 IV 部分：高级脚本主题

- 第 23 节：使用数据库
- 第 24 节：使用 Web
- 第 25 节：使用 e-mail
- 第 26 节：编写脚本工具
- 第 27 节：高级脚本

## 第 23 节：使用数据库

在本节中

- 介绍 MySQL
- 介绍 PostgreSQL
- 创建数据库对象
- 编写数据库脚本

shell 脚本的一个问题是持久化数据。你可以在 shell 变量中存储所有信息，但在脚本结束后，变量就消失了。有时你希望你的脚本能够存储以后可以使用的数据。在过去，在脚本中存储和检索数据意味着创建文件、读取文件、解析数据并保存回文件。搜索数据意味着读取文件的每一条记录。如今数据库非常流行，让 shell 脚本处理数据变得非常简单。Linux 世界最流行的两个开源数据库是 MySQL 和 PostgreSQL。本节向你介绍如何在 Linux 系统上运行这些数据库，并花时间教你如何在命令行中使用它们。

### MySQL 数据库

目前 Linux 环境中最流行的数据库是 MySQL。作为 Linux-Apache-MySQL-PHP (LAMP) 服务器环境的一部分，许多 Web 服务器使用它来托管在线商店、博客和应用程序。本节描述了如何在 Linux 环境中安装 MySQL 数据库，以及如何创建脚本所需的数据库对象。

### 安装 MySQL

在 Linux 系统上安装 MySQL 曾经相当，但现在 Linux 发行版经常使用自动化软件安装程序（参见第 8 节）。这些程序不仅可以让你轻松从网络存储库下载并安装新软件，还可以自动检查已安装软件包的更新并进行安装。

[图 23.1] 展示了 Ubuntu 发行版中的添加软件功能。

[图 23.1] 在 Ubuntu Linux 系统上安装 MySQL

![](img/0049.jpg)

你只需要选择 `mysql-server` 选项，Synaptic 包管理器就会下载并安装完整的 MySQL 服务器（以及客户端）软件。没有更简单的方法了。

openSUSE Linux 发行版也使用先进的软件管理系统。[图 23.2] 显示了软件管理窗口，你可以根据软件选择软件包或搜索特定软件包。

[图 23.2] 在 openSUSE Linux 系统上安装 MySQL

![](img/0062.jpg)

再次，您可以选择 MySQL 软件选项来下载并安装所需的软件包。

如果您正在使用不支持自动软件加载的 Linux 发行版，或者您只是想获得最新、最强大的 MySQL 服务器版本，可以直接从 MySQL 网站（[www.mysql.com](http://www.mysql.com)）下载安装文件并自行安装。

MySQL 网站包含了针对特定 Linux 发行版的预构建二进制包（使用 Red Hat RPM 软件包格式或 Debian DEB 软件包格式）以及源码包。预构建的二进制包更易安装，因此，如果您的 Linux 系统有可用的二进制包，请尝试使用它。如果您在为你的 Linux 发行版安装二进制包或源码包时需要帮助，请回阅第第 8 章。

> 注意
> > 如果您选择手动下载并安装 MySQL（无论是预构建的二进制包还是源码下载），您将需要进行一些额外的工作来配置 MySQL 服务器，而 Linux 发行版安装包将安装一个预配置好的设置，您几乎无需承担任何工作！

## MySQL 客户端界面

访问 MySQL 数据库的门户是 `mysql` 命令行界面程序。本节描述了 `mysql` 客户端程序，并展示了如何使用它与数据库进行交互。

### 连接到服务器



`mysql`客户端程序允许您使用任何用户账户和密码连接到网络上任何位置的 MySQL 服务器。默认情况下，如果您在命令行中不带任何参数输入`mysql`程序，它将尝试连接到运行在同一 Linux 系统上的 MySQL 服务器，并使用 Linux 登录用户名。

很可能，这并不是您想要连接数据库的方式。有很多命令行参数允许您不仅可以控制连接到哪个 MySQL 服务器，还可以控制`mysql`界面的行为。表 23.1 显示了您可以在`mysql`程序中使用的命令行参数。

### 表 23.1 的 mysql 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| `-A` | 禁用自动重哈。 |
| `-b` | 禁用错误后的蜂鸣声。 |
| `-B` | 不使用历史文件。 |
| `-C` | 压缩在客户端和服务器之间发送的所有信息。 |
| `-D` | 指定要使用的数据库。 |
| `-e` | 执行指定的语句并退出。 |
| `-E` | 垂直显示查询输出，每行一个数据字段。 |
| `-f` | 发生 SQL 错误时继续。 |
| `-G` | 启用命名`mysql`命令。 |
| `-h` | 指定 MySQL 服务器主机名（默认是 localhost）。 |
| `-H` | 以 HTML 代码显示查询输出。 |
| `-i` | 忽略函数名后的空格。 |
| `-N` | 不在结果中显示列名。 |
| `-o` | 忽略命令行中指定的默认数据库以外的其它语句。 |
| `-p` | 提示输入用户账户密码。 |
| `-P` | 指定用于网络连接的 TCP 端口号。 |
| `-q` | 不缓存每个查询结果。 |
| `-r` | 在不进行转义转换的情况下列列。 |
| `-s` | 使用静默模式。 |
| `-S` | 指定连接 localhost 的 socket。 |
| `-t` | 以表格形式显示输出。 |
| `-T` | 程序退出时显示调试信息、内存和 CPU 统计数据。 |
| `-u` | 指定用作登录的用户账户。 |
| `-U` | 仅允许指定键值的`UPDATE`和`DELETE`语句。 |
| `-v` | 使用详细模式。 |
| `-w` | 如果无法建立连接，则等待并重试。 |
| `-X` | 以 XHTML 代码显示查询输出。 |

如您所见，有很多命令行选项可以修改您登录到 MySQL 服务器的方式。

默认情况下，`mysql`客户端程序尝试使用您的 Linux 登录名登录 MySQL 服务器。如果该名称没有在 MySQL 中配置为用户账户，您将需要使用`-u`参数来指定登录的名称：

```bash
$ mysql -u root -p
```

```text
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 39
Server version: 5.1.49-1ubuntu8.1 (Ubuntu)
Copyright (c) 2000, 2010, Oracle and/or its affiliates. All rights reserved.
This software comes with ABSOLUTELY NO WARRANTY. This is free software, and you are welcome to modify and redistribute it under the GPL v2 license
Type ‘help;’ or \h for help. Type \c to clear the current input statement.
mysql>
```

`-p`参数告诉`mysql`程序提示输入与用户账户关联的密码。`mysql`程序尝试使用您的 Linux 登录名登录 MySQL 服务器。一旦登录到服务器，就可以开始输入命令。

## mysql 命令

`mysql`程序使用两种类型的命令：

* 特殊`mysql`命令
* 标准 SQL 语句

`mysql`程序使用自己的一套命令让您可以轻松控制环境并获取有关 MySQL 服务器的信息。表 23.2 显示了这些命令。

### 表 23.2 mysql 命令

| 命令 | 快捷键 | 描述 |
| :--- | :--- | :--- |
| `?` | `\?` | 帮助。 |
| `clear` | `\c` | 清除命令。 |
| `connect` | `\r` | 连接数据库。 |
| `delimiter` | `\d` | 设置分隔符。 |
| `edit` | `\e` | 编辑命令。 |
| `echo` | `\G` | 将命令发送服务器。 |
| `exit` | `\q` | 退出程序。 |
| `go` | `\g` | 将命令发送服务器。 |
| `help` | `\h` | 显示帮助。 |
| `nopager` | `\n` | 禁用分页器。 |
| `note` | `\t` | 将输出到文件。 |
| `pager` | `\P` | 设置分页器程序。 |
| `print` | `\p` | 打印命令。 |
| `prompt` | `\R` | 更改`mysql`提示符。 |
| `quit` | `\q` | 退出程序。 |
| `rehash` | `\#` | 重建表。 |
| `source` | `\` | 执行文件中的 SQL 脚本。 |
| `status` | `\s` | 获取状态。 |
| `system` | `\!` | 执行 shell 命令。 |
| `tee` | `\T` | 追加输出到文件。 |
| `use` | `\u` | 使用另一个数据库。 |
| `charset` | `\C` | 更改字符集。 |
| `warnings` | `\W` | 语句后显示警告。 |
| `nowarning` | `\w` | 语句后不显示警告。 |

您可以在`mysql`提示符处直接使用完整命令或快捷键：

```text
mysql> \s
--------------
mysql Ver 4.12 Distrib 5.0 for redhat-linux (i86) using readline 5.0
Connection id: 1
Current database:
Current user: root@localhost
SSL: Not in use
Current pager: stdout
Using outfile: ''
Using delimiter: ;
Server version: 5.1.49-1ubuntu8.1 (Ubuntu)
Protocol version: 10
Connection: Localhost via UNIX socket
Server characterset: latin1
Db characterset: latin1
Client characterset: latin1
Conn. characterset: latin1
UNIX socket: /var/lib/mysql/mysql.sock
Uptime: 4 hours 15 min 24 sec
Threads: 1 Questions: 53 Slow queries: 0 Opens: 23 Flush tables: 1 Open tables: 17 Queries per second avg: 0.003
mysql>
```

`mysql`程序实现了 MySQL 服务器支持的所有标准结构化查询语言 (SQL) 命令。本章的“创建 MySQL 数据库对象”部分将更详细地讨论这一点。

`mysql`程序实现的一个不常用的 SQL 命令是`SHOW`命令。使用该命令，你可以提取有关 MySQL 服务器的信息，例如已创建的数据库和表：

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
+--------------------+
2 rows in set (0.04 sec)
mysql> USE mysql;
Database changed
mysql> SHOW TABLES;
+---------------------------+
| Tables_in_mysql     |
+---------------------------+
| columns_priv        |
| db                  |
| func                |
| help_category       |
| help_keyword        |
| help_relation       |
| help_topic          |
| host                |
| proc                |
| procs_priv          |
| tables_priv         |
| time_zone           |
| time_zone_leap_second|
| time_zone_name      |
| time_zone_transition|
| time_zone_transition_type|
| user                |
+---------------------------+
17 rows in set (0.00 sec)
mysql>
```

在这个示例中，我们使用`SHOW` SQL 命令显示 MySQL 服务器上当前配置的数据库，然后使用`USE` SQL 命令连接到单个数据库。你的`mysql`会话一次只能连接到一个数据库。

你会注意到，在每个命令之后我们都添加了分号。分号向`mysql`程序表示命令的结束。如果你不使用分号，它会提示输入更多数据：

```sql
mysql> SHOW
   -> DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
+--------------------+
2 rows in set (0.00 sec)
mysql>
```

这个功能在你处理长命令时会非常有用。你可以在一行中输入命令的一部分并按回车键，然后在下一行继续输入。你可以一直持续下去，直到你需要的行数，直到你使用分号表示命令结束。

> Note
> 在本章中，我们使用大写字母表示 SQL 命令。这已成为编写 SQL 命令的常用方法，但`mysql`程序允许你使用大写或小写来指定 SQL 命令。

## 创建 MySQL 数据库对象

在编写 shell 脚本与数据库交互之前，你需要一些数据库对象来工作。至少，你希望拥有以下内容：

* 一个用于存储应用程序数据的唯一数据库
* 一个用于从脚本访问数据库的唯一用户账户
* 一个或多个用于组织数据数据的数据表

你使用`mysql`程序构建所有这些对象。`mysql`程序直接与 MySQL 服务器交互，使用 SQL 命令创建和修改每个对象。

你可以使用`mysql`程序向 MySQL 服务器发送任何类型的 SQL 命令。本节将引导你学习为 shell 脚本构建基础数据库对象所需的各种 SQL 语句。

### 创建数据库

MySQL 服务器将数据组织成数据库。数据库通常包含单个应用程序的数据，将其与其他使用数据库服务器的应用程序隔离开。为每个 shell 应用程序创建一个独立的数据库有助于消除混淆和数据混乱。

创建新数据库所需的 SQL 语句是：

```sql
CREATE DATABASE `name`;
```

这非常简单。当然，你必须拥有在 MySQL 服务器上创建新数据库的相应权限。最简单的方法是以 root 用户账户身份登录：

```bash
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 39
Server version: 5.1.49-1ubuntu8.1 (Ubuntu)
Copyright (c) 2000, 2010, Oracle and/or affiliates. All rights reserved.
This software comes with ABSOLUTELY NO WARRANTY. This is free software, and you are welcome to modify and redistribute it under the GPL v2 license
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.02 sec)
mysql>
```

你可以使用`SHOW`命令检查新数据库是否已创建：

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
+--------------------+
2 rows in set (0.04 sec)
mysql>
```

在这个示例中，我们使用`SHOW` SQL 命令显示 MySQL 服务器上当前配置的数据库，然后使用`USE` SQL 命令连接到单个数据库。你的`mysql`会话一次只能连接到一个数据库。

```sql
mysql> USE test;
Database changed
mysql> SHOW TABLES;
+--------------------+
| Empty set |
mysql>
```

`SHOW TABLES`命令允许你查看是否存在表。Empty set 表示还没有可以操作的表。

### 创建用户

到为止，你已经了解了如何使用`root`账户连接到服务器。对于普通应用程序使用`root`账户是非常危险的。如果发生泄露，有人知道了 root 账户的密码，你的系统可能会发生各种糟糕的事情。

为了防止这种情况，创建一个仅具有数据库权限的独立用户是明智的。你通过`GRANT`语句来实现：

```sql
mysql> GRANT SELECT,INSERT,DELETE,UPDATE ON test.* TO test IDENTIFIED BY 'test';
Query OK, 0 rows affected (0.35 sec)
mysql>
```

你可以直接从`mysql`程序测试新用户账户：

```bash
$ mysql test -u test -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 40
Server version: 5.1.49-1ubuntu8.1 (Ubuntu)
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

## PostgreSQL 数据库

PostgreSQL 数据库最初是一个学术项目，展示了如何将先进数据库技术整合到功能性的数据库服务器中。多年来，PostgreSQL 已经进化为 Linux 环境中最先进的开源数据库服务器之一。

本节将引导你完成安装并运行 PostgreSQL 数据库服务器，然后设置一个用于 Shell 脚本的用户账户和数据库。

### 安装 PostgreSQL

与 MySQL 类似，你可以通过系统的自动化软件安装系统安装 PostgreSQL 数据库服务器包，也可以通过从 PostgreSQL 网站（[www.postgresql.org](http://www.postgresql.org)）手动下载进行安装。

要使用你 Linux 发行版的自动化软件安装，请遵循本章稍前“安装 MySQL”部分列出的相同步骤。与 MySQL 类似，PostgreSQL 的下载区域包含了适用于多种 Linux 发行版的预构建包，以及一个源码包。同样，请查阅第 8 章，以确定你的 Linux 发行版是否使用了 PostgreSQL 二进制包支持的包管理系统。如果不支持，你需要下载 PostgreSQL 源码包并在你的 Linux 系统上进行手动编译。这可能是一个有趣的项目。

> 注意
> 编译源码包要求你的 Linux 系统中已加载了 C 软件开发软件包。如今这对于服务器来说是非常普遍的，但如果你使用的是桌面级 Linux 发行版，可能没有加载。请参阅各个 Linux 发行版的文档，了解有关软件编译以及编译 C 源代码项目所需的软件软件包的信息。

一旦安装了 PostgreSQL 数据库服务器，登录 PostgreSQL 服务器的方法与 MySQL 服务器略有不同。如果你还记得，MySQL 服务器维护着自己的内部用户数据库，可以授予用户访问数据库对象的权限。虽然 PostgreSQL 也具有这种能力，但大多数 PostgreSQL 实现（包括默认源码安装）利用现有的 Linux 系统用户账户来验证 PostgreSQL 用户。



虽然这有时会让人困惑，但它为控制 PostgreSQL 用户账户提供了一种简洁高效的方式。你只需要确保每个 PostgreSQL 用户在 Linux 系统上都有有效的账户，而无需担心另一套完全独立的用户账户。

PostgreSQL 的另一个主要区别是，其管理员账户被称为`postgres`，而不是`root`。由于这一要求，当你在 Linux 系统上安装 PostgreSQL 时，必须存在名为`postgres`的 Linux 用户账户。

下一节将介绍如何使用`postgres`账户访问 PostgreSQL 服务器。

# PostgreSQL 命令行界面

PostgreSQL 命令行客户端程序称为`psql`。该程序提供了对 PostgreSQL 服务器中配置的数据库对象的完全访问。本节描述了`psql`命令并展示了如何使用它与你的 PostgreSQL 服务器进行交互。

## 连接到服务器

`psql`客户端程序提供了 PostgreSQL 服务器的命令行界面。正如你所预期的，它使用命令行参数来控制客户端界面启用的功能。每个选项都使用长名称或短名称格式。表 23.3 显示了可用的命令行参数。

表 23.3 psql 命令行参数

| 短名称 | 长名称 | 描述 |
| :--- | :--- | :--- |
| `-a` | `--echo-all` | 在输出中显示从脚本文件中处理的所有 SQL 行。 |
| `-A` | `--no-align` | 将输出格式设置为未对齐模式。数据不以格式化表格显示。 |
| `-c` | `--command` | 执行指定的 SQL 语句并退出。 |
| `-d` | `--dbname` | 指定要连接的数据库。 |
| `-e` | `--echo-queries` | 在屏幕显示所有查询。 |
| `-E` | `--echo-hidden` | 在屏幕显示隐藏的 psql 元命令。 |
| `-f` | `--file` | 从指定的文件执行 SQL 命令并退出。 |
| `-F` | `--field-separator` | 在未对齐模式下指定用于分隔列数据的字符。默认是逗号。 |
| `-h` | `--host` | 指定远程 PostgreSQL 服务器的 IP 地址或主机名。 |
| `-l` | `--list` | 显示服务器上可用数据库列表并退出。 |
| `-o` | `--output` | 将查询输出重定向到指定的文件。 |
| `-p` | `--post` | 指定要连接的 PostgreSQL 服务器 TCP 端口。 |
| `-P` | `--pset` | 将指定的表格打印选项设置为指定值。 |
| `-q` | `--quiet` | 静默模式，不显示输出消息。 |
| `-R` | `--record-separator` | 使用指定的字符作为记录分隔符。默认是换行符。 |
| `-s` | `--single-step` | 在每个 SQL 查询后提示继续或取消。 |
| `-S` | `--single-line` | 指定用回车键定义 SQL 查询的结束而不是分号。 |
| `-t` | `--tuples-only` | 表格输出中的列标题和页脚。 |
| `-T` | `--table-attr` | 在 HTML 模式下使用指定的 HTML 表格标签。 |
| `-U` | `--username` | 使用指定的用户名连接到 PostgreSQL 服务器。 |
| `-v` | `--variable` | 将指定的变量设置为指定的值。 |
| `-V` | `--version` | 显示 psql 版本号并退出。 |
| `-W` | `--password` | 强制提示密码。 |
| `-x` | `--expanded` | 启用扩展表格输出以显示记录的其他信息。 |
| `-X` | `--nopsqlrc` | 不处理 psql 启动文件。 |
| `-?` | `--help` | 显示 psql 命令行帮助并退出。 |

如上一节所述，PostgreSQL 的管理员账户名为`postgres`。由于 PostgreSQL 使用 Linux 用户账户验证用户，你必须以`postgres`Linux 账户登录，才能以`postgres`用户身份访问 PostgreSQL 服务器。

为了解决这个问题，你可以使用`sudo`命令以`postgres`用户账户身份运行`psql`命令行程序。

```bash
$ sudo -u postgres psql
[sudo password for rich]:
psql (8.4.5)
Type "help" for help.
postgres=#
```

默认的`psql`提示符表示你连接的数据库。提示符中的井号 (`#`) 表示你正以管理员用户账户登录。你现在准备好输入一些命令来与 PostgreSQL 服务器进行交互了。

## psql 命令

与`mysql`程序类似，`psql`程序使用两种不同类型的命令：

* 标准 SQL 语句
* PostgreSQL 元命令

PostgreSQL 元命令允许你轻松提取有关数据库环境的信息，以及用于`psql`会话的功能。元命令由反斜杠`\`表示。有许多针对各种不同设置和功能的 PostgreSQL 元命令，但没有理由立即就开始担心它们。最常用的有：

* `\l` 列出可用数据库
* `\c` 连接到数据库
* `\dt` 列出数据库中的表
* `\du` 列出 PostgreSQL 用户
* `\z` 列出表权限
* `\?` 列出所有元命令
* `\h` 列出所有 SQL 命令
* `\q` 退出数据库

如果你需要找到某个元命令，只需输入`\?`元命令。你将看到一个列表，以及所有可用元命令的解释。

要测试元命令，请使用`\l`元命令列出可用数据库：

```sql
postgres=# \l
List of databases
   Name  | Owner  | Encoding | Collation  |   Ctype   |   Access
-----------+----------+----------+------------+------------+----------
 postgres | postgres | UTF8      | en_US.utf8 | en_US.utf8 | 
 template0 | postgres | UTF8      | en_US.utf8 | en_US.utf8 | =c/postgres
 template1 | postgres | UTF8      | en_US.utf8 | en_US.utf8 | =c/postgres
(3 rows)
postgres=#
```

该列表显示了服务器上可用的数据库以及它们的特性（我们截断了`Access`列的条目，使其能够适应页面宽度）。这些是 PostgreSQL 服务器提供的默认数据库。`postgres`数据库维护着服务器的所有系统数据。`template0`和`template1`数据库提供了默认数据库模板，供你将在创建新数据库时进行复制。

你现在已经准备好在`postgresql`中处理你自己的数据了。

# 创建 PostgreSQL 数据库对象

本节将引导你完成创建数据库以及用于访问数据库的用户账户的过程。你会发现，虽然 PostgreSQL 中的某些工作与 MySQL 完全相同，但某些工作又完全不同。

## 创建数据库对象

创建数据库是与 MySQL 相同的操作之一。请记住以`postgres`管理账户身份登录以创建新数据库：

```bash
$ sudo –u postgres psql
psql (8.4.5)
Type "help" for help.
postgres=# CREATE DATABASE test;
CREATE DATABASE
postgres=#
```

创建数据库后，使用元命令`\l`查看它是否出现在列表中，然后使用元命令`\c`连接到该数据库：

```bash
postgres=# \l
List of databases
    Name    | Owner  | Encoding | Collation  |   Ctype     |   Access
-----------+----------+----------+------------+------------+----------
  postgres  | postgres | UTF8      | en_US.utf8  | en_US.utf8  |
  template0 | postgres | UTF8      | en_US.utf8  | en_US.utf8  | =c/postgres
  template1 | postgres | UTF8      | en_US.utf8  | en_US.utf8  | =c/postgres
  test      | postgres | UTF8      | en_US.utf8  | en_US.utf8  |
(4 rows)
postgres=# \c test
psql (8.4.5)
You are now connected to database "test".
test=#
```

当你连接到`test`数据库时，`psql`提示符会变为显示新的数据库名称。当你准备好创建数据库对象时，这是一个很好的提醒，让你能轻松判断自己处于系统中的位置。

> 注意
> 
> PostgreSQL 为数据库增加了另一层名为模式（schema）的控制。一个数据库可以包含多个模式，每个模式包含多个表。这允许你针对特定的应用程序或用户对数据库进行细分。
> 
> 默认情况下，每个数据库都包含一个名为`public`的模式。如果你只有一个应用程序使用该数据库，那么只使用`public`模式就可以了。如果你想玩得高级一点，可以创建新的模式。在本例中，表将使用`public`模式。

## 创建用户账户

创建新数据库后，下一步是创建一个供 shell 脚本访问数据库的用户账户。正如你所看到的，PostgreSQL 中的用户账户与 MySQL 有显著不同。

PostgreSQL 中的用户账户被称为`Login Roles`（登录角色）。PostgreSQL 服务器将`Login Roles`与 Linux 系统用户账户相匹配。由于由于，创建用于访问 PostgreSQL 数据库的 shell 脚本`Login Roles`有常用方法：

- 创建一个特殊的 Linux 账户并配有匹配的 PostgreSQL`Login Role`来运行所有的 shell 脚本。
- 为每个需要运行 shell 脚本访问数据库的 Linux 用户创建 PostgreSQL 账户。

对于本例，让我们选择第二种方法，创建一个与我们的 Linux 系统账户匹配的 PostgreSQL 账户。这样，你就可以直接从 Linux 用户账户运行访问 PostgreSQL 数据库的 shell 脚本。

首先，你必须创建`Login Role`：

```bash
test=# CREATE ROLE rich login;
CREATE ROLE
test=#
```

这足够简单了。如果没有`login`参数，该角色将不允许登录 PostgreSQL 服务器，但可以被分配权限。这种类型的角色被称为组角色（group role）。如果你在一个拥有大量用户和表的大型环境中工作，组角色将非常有用。你不需要不断跟踪哪个用户对哪些表拥有何种类型的权限，只需为特定类型的表访问创建组角色，然后将登录角色分配给相应的组角色即可。

对于简单的 shell 脚本编写，你可能不需要担心创建组角色，直接将权限分配给登录角色即可。这正是我们在本例中将做的。

然而，PostgreSQL 处理权限的方式与 MySQL 的不同。它不允许你对数据库中的所有对象授予整体权限并将其过滤到表级。相反，你需要为你创建的每个单独的表授予权限。虽然这有点麻烦，但它确实有助于执行严格的安全策略。你必须推迟分配权限，直到你创建了表。这是我们流程中的下一个步骤。

# 操作表

现在你已经运行了 MySQL 或 PostgreSQL 服务器，并创建了新数据库和一个访问用户账户，是时候开始处理数据了！幸运的是，`mysql`和`psql`程序都使用标准 SQL 来创建和管理数据表。本节将引导你学习在两种环境中创建表、插入和删除数据以及查询现有数据所需的 SQL。

## 创建表

MySQL 和 PostgreSQL 服务器都被认为是关系型数据库。在关系型数据库中，数据通过数据字段、记录和表进行组织。数据字段是单一信息，例如员工的姓或薪水。记录是相关数据字段的集合，例如员工 ID、姓、名、地址和工资。每条记录表示一组数据字段。

表包含所有相关数据的记录。因此，你将有一个名为`Employees`的表，存储了每个员工的记录。

要在数据库中创建新表，你需要使用`CREATE TABLE`SQL 命令：

```bash
$ mysql test -u root -p
Enter password:
mysql> CREATE TABLE employees (
  -> empid int not null,
  -> lastname varchar(30),
  -> firstname varchar(30),
  -> salary float,
  -> primary key (empid));
Query OK, 0 rows affected (0.14 sec)
mysql>
```

首先注意，为了创建新表，我们需要使用`root`用户账户登录 MySQL，因为`test`用户没有创建新表的权限。接下来，注意我们在`mysql`命令行中指明了`test`数据库。如果我们没有这样做，就需要使用`USE`SQL 命令来连接到`test`数据库。

> 警告
> 
> 在创建表之前，确保你处于正确的数据库中至关重要。此外，请确保你使用的是管理账户（MySQL 使用`root`，PostgreSQL 使用`postgres`）登录以创建表。

表中的每个数据字段都使用数据类型定义。MySQL 和 PostgreSQL 数据库支持许多不同的数据类型。表 23.4 显示了你可能需要的一些常用数据类型。

| 数据类型 | 说明 |
| :--- | :--- |
| char | 固定长度的字符串值 |
| varchar | 可变长度的字符串值 |
| int | 整数值 |
| float | 浮点值 |
| Boolean | 布尔真/假值 |
| Date | YYYY-MM-DD 格式的日期值 |
| Time | HH:mm:ss 格式的时间值 |
| Timestamp | 日期和时间组合值 |
| Text | 长字符串值 |
| BLOB | 大型二进制值，如图像或视频剪 |

`empid`数据字段还指定了数据约束。数据约束限制了你创建有效记录时可以输入类型。`not null`数据约束表示每条记录必须指定`empid`值。

最后，`primary key`（主键）定义了一个唯一标识每条记录的数据字段。这意味着表中的每条数据记录必须有一个唯一的`empid`值。

创建新表后，你可以使用相应的命令来确保它已创建。在`mysql`中，它是`show tables`命令：

```
mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| employees      |
+----------------+
1 row in set (0.00 sec)
mysql>
```

在`psql`中，它是`\dt`元命令：

```
test=# \dt
           List of relations
Schema  |  Name    | Type  |  Owner
--------+-----------+-------+----------
public  | employees | table | postgres
(1 row)
test=#
```

正如你可能从本章之前的“创建 PostgreSQL 数据库对象”部分中所记得的，在 PostgreSQL 中，你需要在表级分配权限。现在你已经有一个表了，需要赋予你的登录角色（Login Role）访问它的权限：

```
$ sudo -u postgres psql
psql (8.4.5)
Type "help" for help.
postgres=# \c test
psql (8.4.5)
You are now connected to database "test".
test=# GRANT SELECT, INSERT, DELETE, UPDATE ON public.employees TO rich;
GRANT
test=#
```

指定表的格式必须包含模式（schema）名称，默认模式为`public`。此外，请记住以`postgres`登录角色执行此命令，并连接到 test 数据库。

表创建完成后，你现在准备好开始保存数据了。下一节将介绍如何进行操作。

# 插入和删除数据

意料之之中，你使用`INSERT`SQL 命令向表中插入新的数据记录。每个`INSERT`命令都必须指定数据字段的值，以便`MySQL`或`PostgreSQL`能够能够接受该记录。

`INSERT`SQL 命令的格式为：

`INSERT INTO table VALUES (...)`

这些值是每个数据字段值的列表，并用逗号分隔：

```
$ mysql test -u test -p
Enter password:
mysql> INSERT INTO employees VALUES (1, 'Blum', 'Rich', 25000.00);
Query OK, 1 row affected (0.35 sec)
```

或者在`PostgreSQL`中：



```bash
$ psql test
psql (8.4.5)
Type “help” for help.
test=> INSERT INTO employees VALUES (1, ‘Blum’, ‘Rich’, 25000.00);
INSERT 0 1
test=>
```

`MySQL` 示例使用 `-u` 命令行提示符登录到 `MySQL` 中创建的 `test` 用户账户。`PostgreSQL` 示例使用了当前的 Linux 用户账户，因此直接使用了创建的 `rich` 用户账户。

`INSERT` 命令将你指定的数据值推送到表的数据字段。如果你尝试添加另一个与 `empid` 数据字段值重复的记录，将收到错误消息：

```text
mysql> INSERT INTO employees VALUES (1, ‘Blum’, ‘Barbara’, 45000.00);
ERROR 1062 (23000): Duplicate entry ‘1’ for key 1
```

但是，如果你将 `empid` 值更改为唯一值，一切应该都是正常的：

```text
mysql> INSERT INTO employees VALUES (2, ‘Blum’, ‘Barbara’, 45000.00);
Query OK, 1 row affected (0.00 sec)
```

现在你的表里应该有两个数据记录了。

如果你需要从表中删除数据，可以使用 `DELETE` SQL 命令。然而，你对它需要非常小心。

基础的 `DELETE` 命令格式为：

```sql
DELETE FROM table;
```

其中 `table` 指定要从中删除记录的表。这个命令正有一个小问题：它会移除表中的所有记录。

为了仅指定单个记录或一组记录进行删除，你必须使用 `WHERE` 子句。`WHERE` 子句允许你创建一个过滤器来识别要移除哪些记录。你可以像这样使用 `WHERE` 子句：

```sql
DELETE FROM employees WHERE empid = 2;
```

这会将删除过程限制在所有 `empid` 值为 2 的记录。当你执行此命令时，`mysql` 程序会返回一条消息，指示匹配过滤器的记录数量：

```text
mysql> DELETE FROM employees WHERE empid = 2;
Query OK, 1 row affected (0.29 sec)
```

如预期，只有一条记录匹配过滤器并被删除了。

# 查询数据

一旦你将所有数据都存入数据库，就可以开始运行报告来提取信息了。

所有查询工作的核心工具是 SQL `SELECT` 命令。`SELECT` 命令功能非常强大，但多功能也伴随着复杂性。

`SELECT` 语句的基础格式为：

```sql
SELECT datafields FROM table
```

`datafields` 参数是你希望查询返回的数据字段名列表，并用逗号分隔。默认情况下，`SELECT` 命令返回表中所有的记录：

```text
mysql> SELECT * FROM employees;
+-------+----------+-----------+-------+
| empid | lastname | firstname | salary |
+-------+----------+-----------+-------+
| 1     | Blum     | Rich      | 25000.00|
| 2     | Blum     | Barbara  | 45000.00|
+-------+----------+-----------+-------+
```

你可以使用更多修饰符来定义结果。以下是常用修饰符列表：

- `WHERE`：显示满足条件的记录
- `ORDER BY`：按指定顺序显示记录
- `LIMIT`：仅显示记录子集

`WHERE` 子句是最常用的 `SELECT` 修饰符。这里有一个使用 `WHERE` 的示例：

```text
mysql> SELECT * FROM employees WHERE salary > 40000;
+-------+----------+-----------+-------+
| empid | lastname | firstname | salary |
+-------+----------+-----------+-------+
| 2     | Blum     | Barbara  | 45000.00|
+-------+----------+-----------+-------+
```

# 在你的脚本中使用数据库

现在你可以看到在 shell 脚本中添加数据库访问的力量了！下一节描述了使用 shell 脚本与数据库交互时需要的操作。

## 连接数据库

显然，为了连接数据库，你需要在 shell 脚本以某种方式利用 `mysql` 或 `psql` 程序。这个过程并不复杂，但有几点你需要注意。

### 寻找程序

你需要完成的第一个障碍是弄清楚 `mysql` 和 `psql` 命令行客户端程序在 Linux 系统上的位置。Linux 安装的一个缺点是，不同的 Linux 发行版通常将软件包放在不同的位置。

幸运的是，有 `which` 命令。`which` 命令告诉你，如果 shell 尝试从命令行运行某个命令，会在哪里找到它：

```text
$ which mysql
/usr/bin/mysql
$ which psql
/usr/bin/psql
```

处理这些信息的简单方法是将其赋值给环境变量，然后在当你需要引用相应的程序时，在 shell 脚本中使用它：

```bash
MYSQL=$(which mysql)
```

```bash
PSQL=$(which psql)
```

### 登录服务器

找到客户端程序的位置后，你就可以在脚本中使用它们来访问数据库服务器。对于 PostgreSQL 服务器，这很简单：

```bash
$ cat ptest1
#!/bin/bash
# test connecting to the PostgreSQL server
PSQL=$(which psql)
$PSQL test
```

```text
$ ./ptest1
psql (8.4.5)
Type “help” for help.
test=>
```

由于脚本是从 Linux 用户账户运行的，且存在一个同名的 PostgreSQL 账户，你只需要在 `psql` 命令行指定要连接的数据库名称即可。`ptest1` 脚本连接到了 `test` 数据库并让你处于该数据库内部的 `psql` 提示符。

如果你在 MySQL 中为 shell 脚本创建了特殊的用户账户，你需要在 `mysql` 命令行指定该账户：

```bash
$ cat mtest1
#!/bin/bash
# test connecting to the MySQL server
MYSQL='which mysql'
$MYSQL test -u test -p
$ ./mtest1
Enter password:
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A
Welcome to the MySQL monitor.  Commands with ; or \g.
Your MySQL connection id is 43
Server version: 5.1.49-1ubuntu8.1 (Ubuntu)
Copyright (c) 2000, 2010, Oracle and/or its affiliates. All rights reserved.
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL v2 license
Type ‘help;’ or ‘\h’ for help. Type ‘\c’ to clear the current input statement.
mysql
```

这可以运行，但对于非交互式脚本来说并不理想。`-p` 命令行参数导致 `mysql` 暂停并询问密码。你可以通过在命令行中包含密码来解决这个问题：

```bash
$MYSQL test -u test -ptest
```

然而，这并不是一个好主意。任何访问你脚本的人都会知道你数据库的用户账户和密码。

为了解决这个问题，你可以使用 `mysql` 程序使用的特殊配置文件。`mysql` 程序使用 `$HOME/.my.cnf` 文件来读取特殊的启动命令和设置。这些设置之一就是由用户账户启动的 `mysql` 会话的默认密码。

要在文件中设置默认密码，只需创建以下内容：

```bash
$ cat .my.cnf
[client]
password = test
$ chmod 400 .my.cnf
$
```

`chmod` 命令用于限制 `.my.cnf` 文件，使得只有你可以查看它。你现在可以从命令行进行测试：

```bash
$ mysql -u test
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A
Welcome to the MySQL monitor.  Commands with ; or \g.
Your MySQL connection id is 4
Server version: 5.1.49-1ubuntu8.1 (Ubuntu)
Copyright (c) 2000, 2010, Oracle and/or its affiliates. All rights reserved.
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL v2 license
Type ‘help;’ or ‘\h’ for help. Type ‘\c’ to the current input statement.
mysql
```

完美！现在你不需要在命令行中包含密码了。

## 发送到服务器

在建立与服务器的连接后，你将希望发送命令与数据库进行交互。这种方法有两种：

- 发送单个命令并退出。
- 发送多条命令。

要发送单个命令，你必须将命令作为 `mysql` 或 `psql` 命令行的一部分。对于 `mysql` 命令，你使用 `-e` 参数来实现此：

```bash
$ cat mtest2
#!/bin/bash
# send a command to the MySQL server
MYSQL='which mysql'
$MYSQL test -u test -e 'select* from employees'
$ ./mtest2
+-------+----------+-----------+
| empid | lastname | firstname |
+-------+----------+-----------+
| 1     | Blum     | Rich      |
| 2     | Blum     | Barbara   |
| 3     | Blum     | Katie Jane|
| 4     | Blum     | Jessica  |
+-------+----------+-----------+ (Wait, the original text had)
```

对于 `psql` 命令，你使用 `-c` 参数来实现此：

```bash
$ cat ptest2
#!/bin/bash
# send a command to the PostgreSQL server
PSQL='which psql'
$PSQL test -c 'select* from employees'
$ ./ptest2
empid | lastname | firstname | salary
-------+----------+----------
| 1    | Blum     | Rich      | 25000
| 2    | Blum     | Barbara   | 45000
| 3    | Blum     | Katie Jane| 34500
| 4    | Blum     | Jessica  | 52340
(4 rows)
$
```

数据库服务器将 SQL 命令的结果返回给 shell 脚本，脚本在 `STDOUT` 中显示它们。

如果你需要发送多条 SQL 命令，可以使用文件重定向（见第 14 章）。要重定向 shell 脚本中的行，你必须定义一个文件结束字符串（EOF）。文件结束字符串表示重定向数据的开始和结束。

以下是一个定义文件结束字符串并包含数据的示例：

```bash
$ cat mtest3
#!/bin/bash
# sending multiple commands to MySQL
MYSQL='which mysql'
$MYSQL test -u test <<EOF
show tables;
select* from employees where salary > 40000;
EOF
$ ./mtest3
Tables_in_test
employees
empid    lastname    firstname    salary
2       Blum        Barbara      45000
4       Blum        Jessica     52340
$
```

shell 将 `EOF` 分隔符之间的所有内容重定向到 `mysql` 命令，该命令会像你在提示符处手动输入一样执行这些行。使用这种方法，你可以向 MySQL 服务器发送任意数量的命令。然而，你会注意到，每个命令的输出之间没有分隔。在下一节“格式化数据”中，你将看到如何解决这个问题。

> **注意**
>
> 你还应该注意到，当你使用重定向输入方法时，`mysql` 程序更改了默认输出样式。`mysql` 程序没有在数据周围创建 ASCII 符号框，而是检测到输入是重定向的，因此只返回了原始数据。同样的技术也适用于 `psql` 程序：

```bash
$ cat ptest3
#!/bin/bash
# sending multiple commands to PostgreSQL
PSQL='which psql'
$PSQL test <<EOF
dt
select* from employees where salary > 4000;
EOF
$ ./ptest3
List of relations
Schema | Name | Type | Owner
-------+------+------+------
public | employees | table| postgres (1 row)
empid | lastname | firstname | salary
-------+--------------------------
| 2   | Blum     | Barbara   | 45000
| 4   | Blum     | Jessica  | 52340
$
```

`psql` 按你指定的顺序将每个命令的输出直接显示到 `STDOUT`。

当然，你并不局限于从表中检索数据。你可以在脚本中使用任何类型的 SQL 命令，例如 `INSERT` 语句：

```bash
$ cat mtest4
#!/bin/bash
# send data to the table in the MySQL database
MYSQL='which mysql'
if [ $# -ne 4 ]
then
  echo "Usage: mtest4 empid lastname firstname salary"
else
  statement="INSERT INTO employees VALUES ($1, '$2', '$3', $4)"
  $MYSQL test -u test <<EOF
  $statement
EOF
  if [ $? -eq 0 ]
  then
    echo "Data successfully added"
  else
    echo "Problem adding data"
  fi
fi
$ ./mtest4
Usage: mtest4 empid lastname firstname salary
$ ./mtest4 5 Blum Jasper 100000
Data successfully added
$
$ ./mtest4 5 Blum Jasper 100000
ERROR 1062 (23000) at line 1: Duplicate entry '5' for key 1
Problem adding data
$
```

此示例演示了使用这种技术的几点。当你指定文件结束字符串时，它必须是该行上的唯一内容，且该行必须以该字符串开头。如果我们对 `EOF` 进行缩进以匹配 if-then 的缩进，它将无法工作。

在 `INSERT` 语句中，请注意文本值周围有单引号，而整个 `INSERT` 语句周围有双引号。务记不要将用于字符串值的单引号与用于定义脚本变量文本的双引号混淆。

此外，请我们我们如何使用特殊变量 `$?` 来测试 `mysql` 程序的退出状态。这可以帮助你判断命令是否执行失败。

仅仅将命令的输出发送到 `STDOUT` 并不是管理和处理数据最简单的方法。下一节将向你展示一些技巧，可以帮助你的脚本捕获从数据库检索的数据。

## 数据格式化



`mysql`和`psql`命令的标准输出并不非常便于进行数据检索。如果你需要对检索到的数据进行实际操作，你就需要进行一些高级的数据处理。本节描述了你可以使用的一些技巧，以帮助从数据库报告中提取数据。

## 将输出赋值给变量

捕获数据库数据的第一步是将`mysql`和`psql`命令的输出重定向到环境变量中。这允许你在其他命令中使用输出信息。例如所示：

```
$ cat mtest5
```

```bash
#!/bin/bash
# 将 SQL 输出重定向到变量
MYSQL='which mysql'
dbs='$MYSQL test -u test -Bse 'show databases''
for db in $dbs
do
  echo $db
done
```

```bash
$ ./mtest5
```

```
information_schema
test
```

这里在`mysql`程序命令行中有两个额外的参数。`-B`参数指定`mysql`程序以批处理模式运行，并与`-s`（静默）参数结合使用，可以抑制列标题和格式化符号。

通过将`mysql`命令的输出重定向到变量，此示例能够逐个遍历每个返回记录的数值。

## 使用格式化标签

在上一个示例中，你看到在`mysql`程序命令行中添加`-B`和`-s`参数允许你抑制输出标题信息，这样你就能得到数据。还有其他几个你可以使用的参数，可以让你的工作变得更轻松。

为网页生成数据是现今非常流行的事情。`mysql`和`psql`程序都提供了使用 HTML 格式显示输出的选项。在两者中，都是通过使用命令行参数`-H`来启用：

```
$ psql test -H -c 'select * from employees where empid = 1'
```

```html
<table border="1">
<tr>
  <th align="center">empid</th>
  <th align="center">lastname</th>
  <th align="center">firstname</th>
  <th align="center">salary</th>
</tr>
<tr valign="top">
  <td align="right">1</td>
  <td align="left">Blum</td>
  <td align="left">Rich</td>
  <td align="right">25000</td>
</tr>
</table>
<p>(1 row)<br />
</p>
```

```
$
```

`mysql`程序支持另一种流行的格式，称为可扩展标记语言 (XML)。这种语言使用类似 HTML 的标签来标识数据名称和值。

对于`mysql`程序，你使用命令行参数`-X`来实现：

```
$ mysql test -u test -X -e 'select * from employees where empid = 1'
```

```xml
<?xml version="1.0"?>
<resultset statement="select * from employees">
<row>
    <field name="empid">1</field>
    <field name="lastname">Blum</field>
    <field name="firstname">Rich</field>
    <field name="salary">25000</field>
</row>
</resultset>
```

```
$
```




使用 `XML`，你可以轻松地识别单行数据以及每个记录中的单个数据值。

## 总结

本章讨论了通过 shell 脚本从数据库中保存、修改和检索数据的能力。你可以从 shell 脚本直接访问 MySQL 和 PostgreSQL 服务器。

在安装 MySQL 和 PostgreSQL 服务器后，你可以使用各自的客户端程序从命令行或 shell 脚本访问服务器。`mysql` 客户端程序提供了 MySQL 服务器的命令行界面。你可以从 shell 脚本向服务器发送 SQL 命令以及自定义 MySQL 命令，然后检索结果。

`psql` 客户端程序对 PostgreSQL 服务器的操作相同。有许多命令行参数你可以使用，来帮助以正确的方式格式化你的数据。

两个客户端程序都允许你向服务器发送单个命令，或使用输入重定向发送批量命令。程序通常将服务器的输出数据发送到 `STDOUT`，但你可以将输出重定向到变量并在 shell 脚本中使用该信息。

下一章将研究万维网。让你的 shell 脚本与互联网上的网站建立接口是一项复杂的任务，但一旦你掌握了它，全世界都任由你检索数据。

# 第 24 章：使用 Web

## 本章内容

- 使用 `Lynx` 浏览
- 使用 `cURL` 探索
- 在 `zsh` 中进行客户端/服务器编程

当你考虑到 shell 脚本编程时，最后想到的往往是互联网。命令行世界对于华丽的图形化互联网世界来说往往很陌生。然而，有几种不同的工具你可以轻松地在 shell 脚本中使用，以访问 Web 上的内容以及其他网络设备的内容。本章将带你了解三种让 shell 脚本与网络世界交互的流行方法。

## `Lynx` 程序

`Lynx` 程序几乎与互联网本身一样老，它于 1992 年由堪萨斯大学的学生创建，作为一个基于文本的浏览器。因为它是基于文本的，`Lynx` 程序允许直接从终端会话浏览网站，用 HTML 文本标签替换网页上的华丽图形。这允许你从几乎任何类型的 Linux 终端上网。图 24.1 显示了 Lynx 屏幕的示例。

图 24.1 使用 `Lynx` 查看网页

![](img/00070.jpg)

`Lynx` 使用标准键盘键在网页上进行导航。链接以高亮文本的形式出现在网页中。使用向右箭头键可以跟随链接跳转到下一个网页。

你可能在想如何在 shell 脚本中使用图形化文本程序。`Lynx` 程序还提供了一个功能，可以将网页的文本内容导出到 `STDOUT`。这个功能对于挖掘网页中包含的数据非常有帮助。本节描述了如何在 shell 脚本中使用 `Lynx` 程序从互联网网站中提取数据。

### 安装 `Lynx`

尽管 `Lynx` 程序已经有些老了，但它仍在活跃开发。在本书期间，`Lynx` 的最新版本是 2.8.8，它于 2010 年 6 月发布，新版本正在开发中。由于它在 shell 脚本程序员中非常受欢迎，许多 Linux 发行版在默认安装中就包含了 `Lynx`。

如果你使用的发行版没有提供 `Lynx`，请检查你发行版的包。你很可能在那里找到并进行安装。

如果你的发行版没有包含 `lynx` 包，或者你想要最新版本，可以从 [lynx.isc.org](http://lynx.isc.org) 网站下载并自行编译（假设你已经在 Linux 系统上安装了 C 开发库）。有关如何编译和安装源码发行包的信息，请参见第 8 章。

> **注意**
>
> `Lynx` 程序在 Linux 中使用 `curses` 图形库。大多数发行版默认安装了该库。如果你的发行版没有，在尝试编译 Lynx 之前，请咨询特定发行版关于安装 curses 库的说明。

下一节将描述如何从命令行使用 `lynx` 命令。

## `lynx` 命令行

`lynx` 命令行在从远程网站检索信息方面极其功能强大。当你通过浏览器查看网页时，你看到的只是传输到你浏览器的部分信息。网页由三类数据元素组成：

- HTTP 头部（headers）
- Cookies
- HTML 内容

### HTTP 头部

HTTP 头部提供了有关连接中发送的数据类型、发送数据的服务器以及连接中所使用的安全类型等相关信息。如果你正在发送特殊类型的数据（例如视频或音频片段），服务器会在 HTTP 头部中识别出这些内容。`Lynx` 程序允许你查看在网页会话中发送的所有 HTTP 头部。

如果你进行过任何类型的网络浏览，无疑你对网页 cookie 并不陌生。网站使用 cookie 来存储有关你访问网站的数据以备将来使用。每个单独的 cookie 都可以存储信息，但只能访问其自身设置的信息。`lynx` 命令提供了选项，允许你查看 Web 服务器发送的 cookie，并可以拒绝或接受从服务器发送的特定 cookie。

### HTML 内容

`Lynx` 程序允许你以三种不同的格式查看网页的实际 HTML 内容：

- 在终端会话中使用 `curses` 图形库以文本图形形式显示
- 作为文本文件，转储网页的原始数据
- 作为文本文件，转储网页的原始 HTML 源代码

对于 shell 脚本来说，查看原始数据或 HTML 源代码是一个金矿。一旦捕获了从网站检索的数据，你就可以轻松提取出单个信息。

### `Lynx` 命令用法

如你所见，`Lynx` 程序的功能极其多变。然而，多功能性也伴随着复杂性，特别是在涉及到命令行参数时。`Lynx` 程序是你会在 Linux 世界中遇到的较复杂的程序之一。

`lynx` 命令的基本格式为：

```text
lynx options URL
```

其中 `URL` 是你想要连接的 HTTP 或 HTTPS 目标地址，`options` 是一个或多个修改 `Lynx` 在与远程网站交互时行为的选项。对于 `Lynx` 所需的任何类型的 Web 交互，都有相应的选项。表 24.1 显示了你可以配合 `lynx` 命令一并使用的所有可用命令行参数。

#### 表 24.1 `lynx` 命令参数

| 参数 | 说明 |
| :--- | :--- |
| `-` | 从标准输入（`STDIN`）接收选项和参数。 |
| `-accept_all_cookies` | 如果开启 `Set-Cookie` 处理，则无需提示直接接受 cookie。默认设置为 `off`。 |
| `-anonymous` | 为匿名账户应用限制。 |
| `-assume_charset=name` | 未指定字符集的文档时使用的默认字符集。 |
| `-assume_local_charset=name` | 本地文件的默认字符集。 |
| `-assume_unrec_charset=name` | 使用替代未识别字符集时使用的默认字符集。 |
| `-auth=id:pw` | 受保护文档的身份验证信息。 |
| `-base` | 为 `-source` 转储的文本/HTML 输出前加上请求 URL 注释和 BASE 标签。 |
| `-bibhost=URL` | 本地 bibp 服务器 URL（默认为 `http://bibhost/`）。 |
| `-book` | 使用书签页作为起始页。默认设置为 `off`。 |
| `-buried_news` | 切换对新闻文章中埋藏引用的扫描。默认设置为 `on`。 |
| `-cache=n` | 内存中缓存的文档数量。 |
| `-case` | 开启区分大小的用户搜索。默认设置为 `off`。 |
| `-center` | 切换 HTML `<table>` 标签中的居中对齐。默认设置为 `off`。 |
| `-cfg=filename` | 指定除 `lynx.cfg` 以外的配置文件。 |
| `-child` | 在起始文件上按左箭头退出，并禁用保存到磁盘。 |
| `-cmd_log=filename` | 将按键命令记录到指定文件。 |
| `-cmd_script=filename` | 从指定文件读取按键命令。 |
| `-connect_timeout=n` | 设置连接超时（秒）。默认为 18,000 秒。 |
| `-cookie_file=filename` | 指定用于读取 cookie 的文件。 |
| `-cookie_save_file=filename` | 指定用于存储 cookie 的文件。 |
| `-cookies` | 切换 `Set-Cookie` 头部处理。默认设置为 `on`。 |
| `-core` | 切换在致命错误时强制核心转储（core dumps）。默认设置为 `off`。 |
| `-crawl` | 配合 `-traversal`，使用 `-dump` 将每个页面输出到文件，格式与 `-traversal` 相同，但输出到标准输出（`STDOUT`）。 |
| `-curses_pads` | 使用 curses pad 特性支持左/右移动。默认设置为 `on`。 |
| `-debug_partial` | 显示带有 MessageSecs 延迟的增量显示阶段。默认设置为 `off`。 |
| `-delay=n` | 设置 statusline 消息的延迟（秒）。默认设置为 `0.000`。 |
| `-display=display` | 为 X Window 程序设置显示变量。 |
| `-display_charset=name` | 终端输出的字符集。 |
| `-dont_wrap_pre` | 当设置 `-dump` 和 `-crawl` 时，不在 `<pre>` 区域内对文本换行。在交互会话中标记换行的行。默认设置为 `on`。 |
| `-dump` | 将第一个 URL 转储到 `STDOUT` 并退出。 |
| `-editor=editor` | 使用指定的编辑器开启编辑模式。 |
| `-emacskeys` | 开启类似 Emacs 的按键移动。默认设置为 `off`。 |
| `-enable_scrollback` | 切换与滚动回键的兼容性。默认设置为 `off`。 |
| `-error_file=filename` | 将 HTTP 状态码写入指定文件。 |
| `-exec` | 开启本地程序执行。 |
| `-force_empty_hrefless_a` | 强制让没有 `href` 属性的 `<a>` 元素为空。默认设置为 `off`。 |
| `-force_html` | 强制将第一个文档解释为 HTML。默认设置为 `off`。 |
| `-force_secure` | 要求 SSL cookie 具有安全标记。默认设置为 `off`。 |
| `-forms_options` | 使用基于表单选项菜单。默认设置为 `on`。 |
| `-from` | 开启 From 头的传输。默认设置为 `on`。 |
| `-ftp` | 禁用 FTP 访问。默认设置为 `off`。 |
| `-get_data` | 从 `STDIN` 读取 GET 表单的数据，以 `---` 结束。 |
| `-head` | 发送 `HEAD` 请求。默认设置为 `off`。 |
| `-help` | 打印用法信息。 |
| `-hiddenlinks=option` | 指定如何处理隐藏链接。`Option` 可以是 `merge`、`listonly` 或 `ignore`。 |
| `-historical` | 使用 `>` 代替 `-->` 作为注释终止符。默认设置为 `off`。 |
| `-homepage=URL` | 设置独立主页。 |
| `-image_links` | 启用所有图像的链接。默认设置为 `off`。 |
| `-index=URL` | 设置索引文件名。 |
| `-ismap` | 当存在客户端 MAP 时包含 ISMAP 链接。默认设置为 `off`。 |
| `-link=n` | 设置 `-crawl` 生成的 `lnk#.dat` 文件的起始计数。默认值为 `0`。 |
| `-localhost` | 禁用指向远程主机的 URL。默认设置为 `off`。 |
| `-locexec` | 仅开启本地文件的本地程序执行。默认设置为 `off`。 |
| `-mime_header` | 包含 MIME 头部并强制源码。 |
| `-minimal` | 使用极简模式代替有效的注释解析。默认设置为 `off`。 |
| `-nested_tables` | 使用嵌套表格逻辑。默认设置为 `off`。 |
| `-newschunksize=n` | 设置分块新闻列表中的文章数量。 |
| `-newsmaxchunk=n` | 设置新闻列表分块前的最大文章数量。 |
| `-nobold` | 禁用视频粗体属性。 |
| `-nobrowse` | 禁用目录浏览。 |
| `-nocc` | 禁用邮件发送时的自复制副本提示。默认设置为 `off`。 |
| `-nocolor` | 禁用颜色支持。 |
| `-noexec` | 禁用本地程序执行。默认设置为 `on`。 |
| `-nofilerferer` | 禁用文件 URL 传输 `Referer` 头部。默认设置为 `on`。 |
| `-nolist` | 禁用转储中的链接列表功能。默认设置为 `off`。 |
| `-nolog` | 禁用向文档所有者发送错误消息。默认设置为 `on`。 |
| `-nonrestarting_sigwinch` | 使窗口大小变化处理程序不重新启动。默认设置为 `off`。 |
| `-nopause` | 禁用状态行消息的强制暂停。 |
| `-noprint` | 禁用某些打印功能，例如 `-restrictions=print`。默认设置为 `off`。 |
| `-noredir` | 不跟随 `Location:` 重定向。默认设置为 `off`。 |
| `-noreferer` | 禁用传输 `Referer` 头部。默认设置为 `off`。 |
| `-noreverse` | 禁用反转视频属性。 |
| `-nostatus` | 禁用杂信息消息。默认设置为 `off`。 |
| `-nounderline` | 禁用下划线视频属性。 |
| `-number_fields` | 强制对链接以及表单输入字段编号。默认设置为 `off`。 |
| `-number_links` | 强制对链接编号。默认设置为 `off`。 |
| `-partial` | 在下载时显示部分页面。默认设置为 `on`。 |
| `-partial_thres=n` | 设置在用部分显示逻辑重绘显示之前渲染的行数。默认设置为 `-1`，即禁用此功能。 |
| `-pauth=id:pw` | 为受保护代理服务器设置认证信息。 |
| `-popup` | 通过弹出窗口处理单选 `SELECT` 选项，而不是单选按钮列表。默认设置为 `off`。 |
| `-post_data` | 从 `STDIN` 读取 POST 表单的数据，以 `---` 结束。 |
| `-preparsed` | 在 `-source` 和源码视图中显示解析后的文本/HTML MIME 类型，以直观展示 Lynx 如何处理无效的 HTML。默认设置为 `off`。 |
| `-prettysrc` | 在源码视图中使用语法高亮和超链接处理。默认设置为 `off`。 |
| `-print` | 启用打印功能，与 `-noprint` 相反。默认设置为 `on`。 |
| `-pseudo_inlines` | 为没有 ALT 字符串的内联元素使用伪 ALT。默认设置为 `on`。 |
| `-raw` | 启动字符集使用 8 位字符翻译默认设置或 CJK 模式。默认设置为 `off`。 |
| `-realm` | 限制在起始领域内访问 URL。默认设置为 `off`。 |
| `-reload` | 刷新代理服务器上的缓存（仅影响第一个文档）。默认设置为 `off`。 |
| `-restrictions=options` | 设置限制选项。使用不带参数的 `-restrictions` 查看列表。 |
| `-resubmit_posts` | 当其返回的文档通过 `PREV_DOC` 命令或从历史列表被请求时，强制对方法为 `POST` 的表单进行重新提交（不使用缓存）。默认设置为 `off`。 |
| `-rlogin` | 禁用 `rlogin` 功能。默认设置为 `off`。 |
| `-selective` | 需要 `.www_browsable` 文件才能浏览目录。 |
| `-short_url` | 在状态行中启用对长 URL 开头和结尾的检查。默认设置为 `off`。 |
| `-show_cursor` | 设置为 `off` 时隐藏右下角的光标，否则显示光标。默认设置为 `on`。 |
| `-show_rate` | 显示传输速率。默认设置为 `on`。 |
| `-soft_dquotes` | 使用旧版 Netscape 和 Mosaic 的 bug，该 bug 将 `>` 视为双引号和标签的共同终止符。默认设置为 `off`。 |
| `-source` | 将第一个 URL 的源码导出到 `STDOUT` 并退出。 |
| `-stack_dump` | 禁用 SIGINT 清理处理程序。默认设置为 `off`。 |
| `-startfile_ok` | 允许配合 `-validate` 使用非 HTTP 起始页和首页。默认设置为 `off`。 |
| `-stdin` | 从 `STDIN` 读取 startfile。默认设置为 `off`。 |
| `-tagsoup` | 使用 TagSoup 而不是 SortaSGML 解析器。默认设置为 `off`。 |
| `-telnet` | 禁用 Telnet 会话。默认设置为 `off`。 |
| `-term=term` | 指定要模拟的终端类型。 |
| `-tlog` | 为当前会话使用 Lynx 追踪日志。默认设置为 `on`。 |
| `-tna` | 使用文本字段激活模式。默认设置为 `off`。 |
| `-trace` | 使用 Lynx 追踪模式。默认设置为 `off`。 |
| `-trace_mask` | 自定义 Lynx 追踪模式。默认设置为 `0`。 |
| `-traversal` | 遍历从 startfile 产生的所有 HTTP 链接。 |
| `-trim_input_fields` | 修剪表单中的输入文本/文本区域字段。默认设置为 `off`。 |
| `-underline_links` | 为链接使用下划线/粗体属性。默认设置为 `off`。 |
| `-underscore` | 在导出中使用下划线格式。 |
| `-use_mouse` | 启用鼠标支持。默认设置为 `off`。 |
| `-useragent=Name` | 设置备用的 Lynx User-Agent 头部。 |
| `-validate` | 接受 `http` URL（用于验证），意味着比 `-anonymous` 更多限制，但允许 `http` 和 `https` 的重定向。默认设置为 `off`。 |
| `-verbose` | 使用带有这些图像文件名的 `[LINK]`、`[IMAGE]` 和 `[INLINE]` 注释。默认设置为 `on`。 |
| `-version` | 显示 Lynx 版本信息。 |
| `-vikeys` | 启用类似 vi 的键移动。默认设置为 `off`。 |
| `-width=n` | 设置用于导出格式化的屏幕宽度。默认值为 80 列。 |
| `-with_backspaces` | 如果使用 `-dump` 或 `-crawl` 参数，则在输出中产生退格键。默认设置为 `off`。 |

如你所见，你可以直接从命令行控制几乎任何类型的 HTTP 或 HTML 设置。例如，如果你想使用 HTTP POST 方法向 Web 表单发布数据，只需在 `-post-data` 参数中包含你的数据。如果你想将网站收到的 cookie 存储在特殊位置，可以使用 `-cookie_save_file` 参数。

许多命令行参数定义了你在浏览网页时控制 `Lynx` 的行为。与其在每次使用时都输入这些参数，`Lynx` 提供了一个通用配置文件来定义基础行为。下一节将讨论该文件。

## `Lynx` 配置文件

虽然这看起来像是在浪费时间，但它是保护客户免受互联网危险的一项重要功能。代理服务器可以过滤不适当的内容和恶意代码，甚至可以检测用于网络数据钓鱼计划的网站（伪装成他人以获取客户数据的流氓服务器）。代理服务器还可以帮助减少互联网带宽的使用，因为它们缓存常用的 Web 页面并将其返回给客户端，而不是重新下载原始页面。

用于定义代理服务器的配置参数有：

```text
http_proxy:http://some.server.dom:port/
https_proxy:http://some.server.dom:port/
ftp_proxy:http://some.server.dom:port/
gopher_proxy:http://some.server.dom:port/
news_proxy:http://some.server.dom:port/
newspost_proxy:http://some.server.dom:port/
newsreply_proxy:http://some.server.dom:port/
snews_proxy:http://some.server.dom:port/
snewspost_proxy:http://some.server.dom:port/
snewsreply_proxy:http://some.server.dom:port/
nntp_proxy:http://some.server.dom:port/
wais_proxy:http://some.server.dom:port/
finger_proxy:http://some.server.dom:port/
cso_proxy:http://some.server.dom:port/
no_proxy:host.domain.dom
```

你可以为 `Lynx` 支持的任何网络协议定义不同的代理服务器。`NO_PROXY` 参数是一个由逗号分隔的列表，包含了你希望直接访问而不使用代理服务器的网站。这些通常是不需要过滤的内部网站。

## `Lynx` 环境变量

从丰富的命令行选项和配置文件参数可以看出，`Lynx` 程序是高度自定义的。然而，自定义并不仅于此。你可以使用环境变量覆盖许多配置文件参数。如果你在一个无法访问 `lynx.cfg` 配置文件的环境中工作，可以通过设置本地环境变量来覆盖某些默认参数。表 24.2 列出了在受限环境中使用 `Lynx` 时可能需要的更常用的 `Lynx` 环境变量。

### 表 24.2 `Lynx` 环境变量

| 变量 | 说明 |
| :--- | :--- |
| `LYNX_CFG` | 指定备用配置文件的位置。 |
| `LYNX_LSS` | 指定默认 Lynx 字符样式表的位置。 |
| `LYNX_SAVE_SPACE` | 指定保存文件到磁盘的位置。 |
| `NNTPSERVER` | 指定用于检索和发布 USENET 新闻的服务器。 |
| `PROTOCOL_PROXY` | 覆盖指定协议的代理服务器。 |
| `SSL_CERT_DIR` | 指定包含访问信任站点所需的信任证书的目录。 |
| `SSL_CERT_FILE` | 指定包含你的信任证书的文件。 |
| `WWW_HOME` | 定义 Lynx 启动时使用的默认 URL。 |

在使用 `Lynx` 程序之前，你就像设置任何其他环境变量一样设置这些环境变量：

```bash



```bash
$ http_proxy=http://myproxy.com:8080

$ lynx
```

要指定代理服务器，你必须提供协议、服务器名称以及与代理服务器通信的端口。如果你需要设置此变量，最好将其包含在 shell 的常用启动文件中（例如 bash shell 的 `.bashrc` 文件），这样你就不需要每次都输入它了。

## 从 Lynx 获取数据

当你在 shell 脚本中使用 Lynx 时，你可能正尝试从 Web 页面获取特定的某部分或多部分信息。实现此目标的技术被称为屏幕抓取（screen scraping）。在屏幕抓取中，你正试图程序化地在图形界面的特定位置寻找数据，以便捕获并在 shell 脚本中使用。

使用 `lynx` 执行屏幕抓取的简单方法是使用 `-dump` 选项。该选项不会尝试在终端屏幕上显示 Web 页面。相反，它将 Web 页面的文本数据直接显示到 `STDOUT`：

```bash
$ lynx -dump http://localhost/RecipeCenter/
```

```text
Recipe Center

          “就像妈妈做的一样”

欢迎

    [1]首页

    [2]登录发布

    [3]免费注册

      _________________________________________________________

    [4]发布新食
```

每个链接通过标签数字识别，Lynx 在网页数据之后会显示所有标签引用的列表。

一旦你获取了网页的所有文本数据，你可能知道我们要从工具箱中取出哪些工具来开始提取数据了。没错，就是我们的老朋友 `sed` 和 `gawk` 程序（见第 18 章）。

首先，让我们找到一些有趣的数据来收集。Yahoo! 天气网页是查找世界上任何地方当前天气状况的绝佳来源。每个位置使用单独的 URL 来显示该城市的天气信息（你可以通过普通浏览器访问该网站并输入你的城市信息来找到你城市的特定 URL）。用于查找伊利诺伊州芝加哥市天气的 `lynx` 命令是：

```bash
lynx -dump http://weather.yahoo.com/united-states/illinois/chicago-2379574/
```

此命令从网页中导出了大量数据。第一步是找到你需要的精确信息。为了实现这一点，将 `lynx` 命令的输出重定向文件，然后在文件中搜索你的数据。在执行了上述命令后，我们在输出文件中发现了以下文本：

```text
截至东部时间下午 1:54 的当前状况

大部分多云

    体感温度:

          32 °F

    气压:

          30.13 英寸正在上升

湿度:

          50%

能见度:

          10 英里

露点:

          15 °F

风力:

          西风 10 英里
```

这就是你需要的关于当前天气全部信息了。这个输出只有一个小问题。你会发现数字在标题下方的一行中。尝试只提取单个数字将很困难。第 18 章讨论了如何处理这种情况。

```bash
echo The current temp outside is: $temp

$ ./weather

Current conditions: Mostly Cloudy

The current temp outside is: 32 °F

$
```

该天气脚本会连接到所需城市的 Yahoo! 天气网页，将网页保存到临时文件，提取相应的文本，删除临时文件，然后显示天气信息。这种做法的妙之处在于，一旦你从网站上提取了数据，就可以对它进行任何操作，例如创建一个温度表。然后，你可以创建一个 `cron` 任务（参见第 15 节），让它每天运行一次以跟踪每日温度。

> **注意**
>
> 互联网是一个动态变化的地方。如果你花费了几个小时来确定网页上数据的精确位置，结果发现它在几周后移动了位置，导致你的脚本崩溃，这并不请不要感到意外。事实上，当你读到这本书时，这个示例可能已经无法工作了。重要的是学会从网页上提取数据的流程，然后你就可以将该原理应用于任何情况。

# cURL 程序

Lynx 的流行催生另一个类似的产品，称为 `cURL`。`cURL` 程序允许你使用指定的 URL 从命令行自动传输文件。它目前支持 URL 中指定的 FTP、FTPS、HTTP、HTTPS、SCP、SFTP、TFTP、telnet、DICT、LDAP、LDAPS 和 FILE 协议。

虽然 `cURL` 本身不是作为浏览器浏览器，但它允许你通过简单的命令，直接从命令行或你的 shell 脚本中无人地发送或检索数据。这为你的 shell 脚本工具箱提供了一个非常棒的工具。

本节将带你了解如何在 shell 脚本中安装和使用 `cURL`。

> **注意**
>
> 还有一种名为 `curl` 的编程语言，由 Sumisho Computer System Corporation 所有并销售。请不要将 `cURL` 与 `curl` 编程语言混淆。

# 安装 cURL

随着用性的日益提高，许多 Linux 发行版默认都安装了 `cURL`。在 Ubuntu 中，你必须从软件仓库手动安装它。只需使用此命令即可：

```bash
$ sudo apt-get install curl
```

如果你的 Linux 发行版没有 `cURL`，或者你只想使用最新版本，可以从 `curl.haxx.se` 网站下载源代码并在你的 Linux 系统上进行编译。

再次强调，标准的免责声明仍然适用；你必须在 Linux 系统上安装 C 开发库才能使其工作。

下一节将描述如何从命令行使用 `curl` 程序。

# 使用 cURL 进行探索

默认情况下，`cURL` 将整个网页的完整 HTML 代码返回到 `STDOUT`：

```text
$ curl http://www.google.com

<!doctype html><<html><head><meta http-equiv="content-type" content="text/html; charset=ISO-8859-1">><title>Google</title>

[ listing truncated ]
```

与 Lynx 程序一样，你可以使用标准的 shell 脚本技术从导出的网页中提取单个数据元素。

我们喜欢使用 `cURL` 来批量下载文件。现如今，我们似乎在不断地下载最新的 Linux 发行版 ISO 文件。因为 ISO 文件非常大，我们需要开始下载并在下载时时离开电脑。一旦我们知道了 ISO 文件的 URL，就可以就可以使用 `cURL` 创建一个简单的 shell 脚本来自动化该过程：

```bash
$ cat downld

#!/bin/bash

# download latest cURL file automatically

curl -s -o /home/rich/curl-7.18.0.tar.gz http://curl.haxx.se/download/curl-7-18.0.tar.gz

$
```

`-s` 命令行选项将 `curl` 置于静默模式，不向 `STDOUT` 发送任何数据。`-o` 命令行选项将输出重定向到一个文件名。虽然你从列表中看不出来，但脚本中的 `curl` 命令是单行的。这个简单的脚本只是直接从 `cURL` 网站下载文件。你现在可以使用 `at` 或 `cron` 命令（参见第 15 节）调度下载，在晚上你不使用电脑或网络时进行。

# 使用 zsh 进行网络操作

第 22 节描述了 `zsh` shell 中可用的所有功能。`zsh` shell 是一种适用于 Linux 和 Unix 环境的较新 shell。`zsh` shell 的功能之一是插件模块。与其尝试将许多功能整合到 `zsh` 核心中，`zsh` 使用了专用模块，这样你可以根据需要选择加载的命令。其中一个模块就是 TCP 模块。

`zsh` shell 中的 TCP 模块直接从命令行提供了一些惊人的网络能力。你可以直接从命令行（或 shell 脚本）与另一个网络设备创建一个 TCP 网络会话。本节讨论了 `zsh` TCP 模块的功能，并展示了一个你可以使用 `zsh` shell 脚本构建的简单客户端/服务器应用程序。

## TCP 模块

`zsh` shell 使用模块为核心 `zsh` 添加额外功能。每个模块都包含专门用于特定领域的内置命令。TCP 模块为大量的网络功能提供了内置命令。

要在 `zsh` shell 中安装 TCP 模块，请执行以下操作：

```zsh
% zmodload zsh/net/tcp

%
```

这就是在 shell 中安装模块库的全部工作！如果你在 shell 脚本中使用 TCP 模块，请记住在脚本中包含此行。该模块仅适用于当前 shell。

一旦加载了 TCP 模块，你就可以使用 `ztcp` 命令。`ztcp` 命令的格式为：

```text
ztcp [-acflLtv] [-d fd] [[args]]
```

可用的命令行选项有：

- `-a`：接受新连接。
- `-c`：关闭现有连接。
- `-d`：为连接使用指定的文件描述符。
- `-f`：强制关闭连接。
- `-l`：打开一个新的 socket 进行监听。
- `-L`：列出当前连接的 socket。
- `-t`：如果没有挂起的连接则退出。
- `-v`：显示有关连接的详细信息。

`ztcp` 命令使用文件描述符与打开的 TCP 连接进行交互。默认情况下，`zsh` 使用环境变量 `$RESULT` 引用文件描述符。你只需要向 `$RESULT` 变量指定的文件描述符发送数据，TCP 模块将其转发到远程主机。同样，如果远程主机向你发送任何数据，你只需要从 `$RESULT` 变量指定的文件描述符中读取它。网络编程没有这更简单了！

## 客户端/服务器范式

在深入使用 `zsh` shell 创建客户端/服务器程序之前，了解客户端和服务器程序具体是如何运行是一个很好的主意。显然，它们在数据连接和传输中承担着不同的责任。

服务器程序监听网络上来自客户端的请求。客户端向服务器发起连接请求。一旦服务器接受了连接请求，每个设备就可以通过双向通信通道发送和接收数据了。这一过程在图 24.2 中所示。

**图 24.2 客户端/服务器通信图**

![](img/00028.jpg)

如从图 24.2 中所示，服务器在与客户端通信之前必须执行两个功能。首先，它必须设置一个特定的 TCP 端口来监听传入的请求。当连接请求进来时，它必须接受连接。

客户端的责任要简单得多。它所需要的尝试连接到服务器正在监听的特定 TCP 端口。如果服务器接受了连接，双向通信即可可用，就可以发送数据。

一旦服务器和客户端之间建立了连接，在两个设备之间就必须使用某种通信过程（或规则）。如果两个设备都尝试同时监听消息，它们将发生死锁，什么也不会发生。同样，如果它们都尝试同时发送消息，也将无法完成任何操作。

作为网络编程员，你的工作是决定你的客户端程序和服务器程序必须遵循的协议规则。

# 使用 zsh 进行客户端/服务器编程

为了演示使用 `ztcp` 创建客户端/服务器程序，让我们建立一个简单的网络应用程序。我们将创建的服务器程序将在 TCP 端口 `5150` 上监听连接请求。当连接请求进来时，服务器将接受它，然后向客户端发送一条欢迎消息。

随后，服务器程序将等待接收客户端的消息。如果它收到了消息，服务器将显示该消息，并将相同的消息发回客户端。发送消息后，服务器将循环回来监听另一个消息。此循环将一直持续，直到服务器接收到包含文本 `exit` 的消息。发生这种情况时，服务器将终止会话。

我们将创建的客户端程序将向服务器的 TCP 端口 `5150` 发送连接请求。连接建立，客户端需要接收服务器的欢迎消息。

接收消息后，客户端会显示它，然后询问用户要发送到服务器的数据。从用户获取消息后，客户端程序将将其发送到服务器并等待接收返回的消息。如果消息返回，客户端将显示该消息并循环回来请求用户提供另一个消息。此循环将一直持续，直到用户输入文本 `exit`。发生这种情况时，客户端将退出文本发送给服务器，然后终止会话。

接下来的章节将展示服务器和客户端程序。

## 服务器程序

以下是服务器程序的代码：

```zsh
% cat server

#!/bin/zsh

# zsh TCP server script

zmodload zsh/net/tcp

ztcp -l 5150

fd=$REPLY

echo “Waiting for a client…”

ztcp -a $fd

clientfd=$REPLY

echo “client connected”

echo “Welcome to my server” > $clientfd

while [ 1 ]

do

    read line < $clientfd

    if [[ $line = “exit” ]]

    then

      break

    else

      echo Received: $line

      echo $line > $clientfd

    fi

done

echo “Client disconnected session”

ztcp -c $fd

ztcp -c $clientfd

%
```

服务器程序遵循图 24.2 所示的客户端/服务器范式。它首先使用 `-l` 参数在指定的端口 `5150` 上监听。`$RESULT` 包含 Linux 系统返回的用于识别连接的文件描述符。服务器使用 `-a` 参数接受新的连接请求。此命令会等待新的连接请求进来（称为阻塞）。除非接受了连接请求，否则脚本不会继续。

每个客户端连接都使用与监听端口文件描述符不同的文件描述符。这允许你在需要时维护多个客户端连接（在这个简单的练习中我们没有这样做）。

在接受连接后，服务器将欢迎消息重定向到客户端的文件描述符：

```zsh
echo “Welcome to my server” > $clientfd
```

`zsh` shell TCP 模块处理了所有确保数据发送到远程客户端的机制。

接下来，服务器程序进入一个无限循环。它使用 `read` 命令等待从客户端返回数据：

```zsh
read line < $clientfd
```

此命令也会阻塞脚本的执行，直到收到来自客户端的数据。如果客户端丢失了网络连接，这可能会是一坏。为了防止这个问题，你可以在 `read line` 中使用 `-t` 选项指定超时值（秒）。如果服务器在超时时间内没有从客户端接收数据，它将继续执行。

如果服务器收到了客户端的数据，它将在 `STDOUT` 上显示数据，然后将其发回客户端。如果数据等于文本字符串 `exit`，服务器将退出循环，并使用 `ztcp` 中的 `-c` 参数关闭客户端的文件描述符和监听端口的文件描述符。如果你希望服务器监听另一个连接，在关闭客户端文件描述符后，你可以循环回来等待接受新连接。

## 客户端程序

以下是客户端程序的代码：

```zsh
% cat server

#!/bin/zsh

# zsh TCP server script

zmodload zsh/net/tcp

ztcp -l 5150

fd=$REPLY

echo “Waiting for a client…”

ztcp -a $fd

clientfd=$REPLY

echo “client connected”

echo “Welcome to my server” > $clientfd

while [ 1 ]

do

    read line < $clientfd

    if [[ $line = “exit” ]]

    then

      break

    else

      echo Received: $line

      echo $line > $clientfd

    fi

done

echo “Client disconnected session”

ztcp -c $fd

ztcp -c $clientfd

%
```

以下是客户端的代码：

```zsh
% cat server

#!/bin/zsh

# zsh TCP server script

zmodload zsh/net/tcp

ztcp -l 5150

fd=$REPLY

echo “Waiting for a client…”

ztcp -a $fd

clientfd=$REPLY

echo “client connected”

echo “Welcome to my server” > $clientfd

while [ 1 ]

do

    read line < $clientfd

    if [[ $line = “exit” ]]

    then

      break

    else

      echo Received: $line

      echo $line > $clientfd

    fi

done

echo “Client disconnected session”

ztcp -c $fd

ztcp -c $clientfd

%
```



等等，重新检查源文本：“客户端程序”部分在提示中提供的文本中实际上再次列出了服务器代码。我将完全遵循提示的文本，但应用格式规则。

实际上，仔细查看提示中的“待格式化文本”，“客户端程序”章节确实以“以下是客户端的代码：”开头，随后是服务器代码块。

客户端程序将向服务器的 TCP 端口`5150`发送连接请求。连接建立后，客户端需要接收服务器的欢迎消息。

接收消息后，客户端显示它，然后询问用户要发送到服务器的数据。从用户处获取消息后，客户端程序将将其发送到服务器并等待接收返回的消息。如果消息返回，客户端显示该消息并循环回来请求用户提供另一个消息。此循环将一直持续，直到用户输入文本`exit`。发生这种情况时，客户端将退出文本发送给服务器，然后终止会话。

## 运行程序

你可以在不同的 Linux 系统上运行这些程序，也可以在同一系统的终端会话中运行。你必须先启动服务器，以便它能够监听连接：

```
./server
Waiting for a client...
```

然后你可以启动客户端：

```
./client

Welcome to my server
Enter text: test
Sending test to remote host...
Received: test
```

当客户端连接时，你将在服务器上看到：

```
client connected
Received: test
```

这将一直持续，直到用户在客户端输入`exit`：

```
Enter text: exit
Sending exit to remote host...
```

你应该看到服务器自动退出：

```
Client disconnected session
```

## 总结

本章介绍了 shell 脚本与交互的世界。执行该操作最流行的工具之一是 Lynx。`Lynx`是一个命令行程序，可以在会话中使用文本模式显示网站信息。除了该功能外，`Lynx`还提供了从网站检索原始数据的方法，并将其显示在`STDOUT`。你可以使用`Lynx`从网站提取数据，并使用`sed`和`gawk`等标准 Linux 文本工具对其进行解析。

`curl`程序是与互联网进行交互时的另一个非常有用的工具。`curl`程序还允许你从网站转储数据，并提供了一种轻松脚本下载不同类型文件的方法。

最后，本章展示了如何使用`zsh` shell 的`TCP`模块编写你自己的网络程序。`zsh` shell 提供了一种在位于网络不同系统的 shell 脚本之间进行通信的方法。

在下一章中，我们将探讨如何在 shell 脚本中利用电子邮件。通常当你使用 shell 脚本实现流程自动化时，如果能收到一条消息指示过程是成功还是失败了，将非常好。通过了解如何使用系统上安装的电子邮件软件，你可以轻松地向世界上任何人发送自动化的消息。

# 第 25 章：使用电子邮件

## 本章内容
* 电子邮件与 Linux
* 搭建电子邮件服务器
* 发送简单消息
* 在 Mutt 中使用附件

随着电子邮件的普及，如今几乎每个人都有一个电子邮箱地址。正因如此，人们往往期望通过电子邮件接收数据，而不是查看文件或打印件。这在 shell 脚本世界中也大无相同。如果你从 shell 脚本中生成了任何种类型的报告，很可能在某个时刻，你会被要求将结果通过电子邮件发送给某人。本章将向你展示如何配置你的 Linux 系统以支持直接从 shell 脚本发送电子邮件。它还将向你展示如何确保你的 Linux 系统可以发送向出的邮件消息，以及如何确保你拥有一个可以从命令行执行此操作的邮件客户端。不过，本章将简要概述 Linux 处理电子邮件的一般方式。

## Linux 电子邮件基础
有时在 shell 脚本中使用电子邮件，最困难的部分是理解 Linux 中的电子邮件系统到底是如何工作的。了解哪些软件包执行特定的任务，对于将邮件从你的 shell 脚本发送到你的收件箱至关重要。本节将带你了解 Linux 系统如何使用电子邮件的基础知识，以及在使用它之前需要准备好的配置。

### Linux 中的电子邮件
Unix 操作系统的主要目标之一是软件模块化。Unix 开发者没有创建一个一个处理某项功能所需所有部分的单体程序，而是创建了许多较小的程序，每个程序负责处理系统总功能的一个较小部分。

这种哲学被应用于 Unix 中使用的电子邮件系统的实现，并被继承到了 Linux 环境。在 Linux 中，电子邮件功能被分为不同的部分，每个部分分配给不同的程序。图 25.1 显示了大多数开源电子邮件软件如何在 Linux 环境中将电子邮件功能模块化。

图 25.1 Linux 模块化电子邮件环境

![](img/00008.jpg)

正如你在图 25.1 中所示，在 Linux 环境中，电子邮件过程通常分为三个功能：
* 邮件传输代理 (MTA)
* 邮件投递代理 (MDA)
* 邮件用户代理 (MUA)

这三个功能之间的边界往往是模糊的。某些电子邮件软件包将 MDA 和 MTA 功能结合，而另一些则结合了 MDA 和 MUA 功能。接下来的章节将更详细地描述这些基础电子邮件组件以及它们在 Linux 系统中如何实现。

### 邮件传输代理 (MTA)
MTA 软件是 Linux 电子邮件系统的核心。它负责处理系统中的入站和出邮件消息。对于每条出站邮件消息，MTA 必须确定收件人地址的目标。如果目标主机是本地系统，MTA 可以直接投递到本地邮箱，也可以将消息传递给本地 MDA 进行投递。

然而，如果目标主机是远程邮件服务器，MTA 必须与远程主机上的 MTA 软件建立通信链接以传输消息。MTA 软件包使用两种常用方法将邮件投递到远程主机：
* 直接投递
* 代理投递

如果你的 Linux 系统直接连接到互联网，它通常可以直接将目标为远程主机收件人的消息直接投递到远程主机。MTA 软件使用域名系统 (DNS) 来解析目标主机，并使用简单邮件传输协议 (SMTP) 将消息投递到远程主机。

> 注意
> 邮件箱的原始 Unix 位置是`/var/spool/mail`。大多数 Linux 发行版都使用这种命名约定；但也有少数 Linux 发行版使用的是`/var/mail`。

如果你的系统确实使用特殊的 MDA 程序来处理入站邮件消息，那么很可能就是流行的`Procmail`程序。`Procmail`允许每个用户创建自定义的配置文件，以定义邮件过滤器、自动回复目标以及独立的邮件信箱。

# 邮件用户代理 (MUA)

到目前为止，我们追踪了邮件从远程主机到本地主机，再到单个用户信箱的流量。该过程的下一步是允许单个用户查看他们的电子邮件。

Linux 邮件模型为每个用户使用一个本地信箱文件或目录来存放该用户的邮件。`MUA`程序的作用是为用户提供一种与其信箱交互以读取消息的方法。

需要注意的是，`MUAs`并不接收消息；它们只显示已经存在信箱中的消息。许多`MUA`程序还提供创建独立邮件文件夹的能力，以便用户可以将邮件从默认信箱（通常称为`Inbox`）移动到单独文件夹中进行组织。

大多数`MUA`程序还提供发送消息的能力。这部分稍微有点模糊，因为正如你所看到的，发送电子邮件消息是`MTA`程序的工作。

为了执行此功能，大多数`MUA`程序利用了`SMTP`中的智能主机（smart host）功能。可以是`MUA`程序自动将消息投递给本地`MTA`程序进行发送，或者你必须在`MUA`配置中定义一个远程智能主机以便其发送消息。

多年来，Linux 平台提供了许多不同的开源`MUA`程序。以下章节描述了你在 Linux 中会遇到的一些流行的`MUA`程序。

## Mailx

`Mailx`程序是 Linux 环境中最常用的命令行`MUA`程序。在所有安装版本中，`Mailx`程序都会连同可执行文件`mail`一起安装，这表明它是`mail`程序的替代品，而不是一个独立的程序。

> 注意
> 像 Ubuntu 和 openSUSE 这种面向图形桌面的 Linux 发行版默认不安装命令行`Mailx`程序。你需要作为邮件客户端包的一部分（见第 8 章）手动安装它。然而，你必须小心，因为并不是所有的 Linux 邮件包都是一样的。对于 Ubuntu，该包名为`mailutils`，它使用的是 GNU`Mailutils`包而不是`Mailx`。它提供了相同的功能，但命令行参数略有不同。

`Mailx`程序允许用户从命令行访问其信箱以读取存储的消息，并向其他邮件用户发送消息。以下是一个`Mailx`会话示例。

```
$ mail

"/var/mail/rich": 2 messages 2 new

>N    1 Rich Blum           Dec  9 10:07  13/579   Test message

 N    2 Rich Blum           Dec  9 10:08  13/593   This is another test

? 1

Return-Path: <rich@rich-Parallels-Virtual-Platform>

X-Original-To: rich@rich-Parallels-Virtual-Platform

Delivered-To: rich@rich-Parallels-Virtual-Platform

Received: by rich-Parallels-Virtual-Platform (Postfix, from userid 1000)

       id 5C03F2606CF; Thu,  9 Dec 2010 10:07:48 -0500 (EST)

To: <rich@rich-Parallels-Virtual-Platform>

Subject: Test message

X-Mailer: mail (GNU Mailutils 2.1)

Message-Id: <20101209150748.5C03F2606CF@rich-Parallels-Virtual-Platform>

Date: Thu,  9 Dec 2010 10:07:48 -0500 (EST)

From: rich@rich-Parallels-Virtual-Platform (Rich Blum)

This is a test message

? d

? q

Held 1 message in /var/mail/rich

$ 
```

第一行显示在不带命令行选项的情况下执行了`Mailx`程序。默认情况下，这允许用户检查其信箱中的消息。在输入`mail`命令后，会显示用户信箱中所有消息的摘要。`Mailx`程序只能读取`/var/mail`格式或`$HOME/mail`格式的消息。它无法处理`Maildir`邮件文件夹格式的消息。

每个用户都有一个包含其所有消息的独立文件。对于某些 Linux 发行版，在用户账户接收消息之前，信箱文件是不存在的。文件名通常是用户的系统登录名，位于系统信箱目录中。因此，用户名`rich`的所有消息都存储在 Linux 系统的`/var/mail/rich`文件中。当用户收到新消息时，它们会被追加到文件的末尾。

你也可以使用`mail`命令行程序发送邮件消息：

```
$ mail barbara

Cc:

Subject: This is a test sent to Barbara

Hello Barbara -

This is a test message I'm sending from the command line.

$ 
```

## 设置你的服务器

在开始向世界发送你的自动化电子邮件消息之前，你需要确保你的 Linux 系统运行着一个 MTA 包，并且其配置是完全的。这本身并不是一项轻易的任务，但幸运的是，某些 Linux 发行版提供了一些基本工具来帮助你。

本节将带你了解 Linux 中最常用的两种邮件 MTA 程序：`sendmail`和`Postfix`的基础知识。虽然已有专门的书介绍了如何正确配置这些包中的每一个，但我们只需查看基础知识，以了解如何让邮件离开 Linux 系统并进入你的收件箱。

# sendmail

`sendmail`MTA 软件包是互联网邮件服务器使用的最流行的开源 MTA 软件包之一。在过去，它曾饱受后门和安全漏洞故事的困扰；然而，它已经经过了重写，不仅消除了安全漏洞，还整合了许多新的 MTA 特性，例如垃圾邮件控制。新版本的`sendmail`程序已被证明既安全又多功能。

## sendmail 程序的组成

主可执行程序称为`sendmail`。它通常在后台模式下运行，监听来自远程邮件服务器的 SMTP 连接，并转发本地用户的出站邮件。

除了主`sendmail`程序外，还有一个配置文件和若干张表，它们用于包含在处理入站和出站邮件消息时需要的信息。表 25.1 列出了标准`sendmail`安装中使用的所有部分。

### 表 25.1 sendmail 配置文件

| 文件 | 描述 |
| :--- | :--- |
| `sendmail.cf` | 控制`sendmail`程序行为的文本文件。 |
| `sendmail.cw` | 文本文件，包含`sendmail`程序将接收邮件的域名列表。 |
| `sendmail.ct` | 文本文件，包含可以控制`sendmail`操作的信任用户列表。 |
| `aliases` | 二进制文件，包含有效本地邮件地址列表，这些地址可以将邮件重定向到另一个用户、文件或程序。 |
| `newaliases` | 可执行程序，从文本文件创建新的`aliases`数据库文件。 |
| `mailq` | 可执行程序，检查邮件队列并打印任何消息。 |
| `mqueue` | 用于存储等待交付的邮件的目录。 |
| `mailertable` | 用于指定特定域名路由路径的文本文件。 |
| `domaintable` | 用于将旧域名映射到新域名的文本文件。 |
| `virtusertable` | 用于将用户和域名映射到备用地址的文本文件。 |
| `relay-domains` | 文本文件，列出允许通过`sendmail`程序中继消息的特定主机。 |
| `access` | 文本文件，列出允许或拒绝接收来自特定域名的消息。 |

除非你正在为公司或互联网服务提供商运行主邮件服务器，否则你需要关心的只有`sendmail.cf`配置文件。事实上，许多使用`sendmail`的 Linux 发行版会自动为你创建并配置一个核心`sendmail.cf`配置文件，它在大多数简单应用程序中都能正常工作。

## sendmail.cf 文件

`sendmail`程序需要被告知在服务器接收消息时如何处理它们。作为一种 MTA，`sendmail`处理入站邮件并将其重定向到另一个邮件包，可以在远程系统，也可以在本地系统。配置文件用于指导`sendmail`如何操作目标邮件地址，以决定在哪里以及如何转发消息。配置文件的默认位置是`/etc/mail/sendmail.cf`。

`sendmail.cf`文件由规则集组成，这些规则集解析入站邮件消息并确定采取的操作。每个规则集都用于识别特定的邮件格式并指示`sendmail`如何处理该消息。

当`sendmail`程序接收到消息时，它解析邮件头并将消息通过各种规则集，以确定对消息采取的操作。`sendmail`配置文件包含了允许`sendmail`处理许多不同格式邮件的规则。从 SMTP 主机接收的邮件与从本地用户接收的邮件具有不同的头字段。`sendmail`程序必须知道如何处理任何邮件情况。

规则在配置文件中还定义了辅助函数。你可以定义三种不同类型的辅助函数：

* **类（Classes）**：定义常用的短语，用于帮助规则集识别某些类型的消息。
* **宏（Macros）**：设置值，以简化配置文件中长字符串的输入。
* **选项（Options）**：用于设置`sendmail`程序运行的参数。

配置文件由一系列类、宏、选项和规则集组成。每个函数在配置文件中被定义为单行文本。

配置文件中的每行都以一个字符开头，该字符定义了该行的操作。以空格或制表符开头的行是上一一个操作行的延续。以井号（`#`）开头的行表示注释，不会被`sendmail`处理。

文本行开头的操作定义了该行的用途。表 25.2 显示了标准的`sendmail`操作及其含义。

### 表 25.2 sendmail 配置文件行

| 配置行 | 描述 |
| :--- | :--- |
| `C` | 定义文本类 |
| `D` | 定义宏 |
| `F` | 定义包含文本类的文件 |
| `H` | 定义头字段和操作 |
| `K` | 定义包含搜索文本的数据库 |
| `M` | 定义邮件传输器 (mailers) |
| `O` | 定义`sendmail`选项 |
| `P` | 定义`sendmail`优先级值 |
| `R` | 定义解析地址的规则集 |
| `S` | 定义规则集组 |

正如我们提到的，你可能不需要从头开始编写`sendmail.cf`配置文件；Linux 发行版应该会为你创建一个标准的模板文件。很可能，你唯一需要担心的只是如果你必须使用智能主机（smart host）来为你转发邮件。`DS`配置行控制此功能：

```
DSmyisp.com
```



在`DS`标签之后添加智能主机的主机名即可。

# Postfix

Postfix 软件包迅速成为 Unix 和 Linux 系统流行的邮件包之一。Postfix 由 Wietse Venema 开发，旨在为标准的 Unix 类型服务器提供替代的 MTA。Postfix 软件能够将任何 Unix 或 Linux 系统转变为功能完整的邮件服务器。

MTA 包负责管理进入或离开邮件服务器的消息。Postfix 通过使用多个模块化程序和邮件队列系统来实现这种消息跟踪。每个程序通过各种邮件队列处理消息，直到其交付到最终目的地。如果在邮件传输期间邮件服务器发生崩溃，Postfix 可以确定消息最后成功放置的队列，并尝试继续处理消息。

## Postfix 系统的组成

Postfix 系统由多个邮件队列目录和可执行程序组成，所有程序相互交互以提供邮件服务。

Postfix 包利用一个始终作为后台进程的主程序。主程序允许 Postfix 启动扫描邮件队列中的新消息并将其发送到目的地的程序。

主程序根据需要启动额外的辅助程序。这些程序可以被配置为在使用后保持运行一段时间。这允许主程序在需要时重用正在运行的辅助程序，从而节省处理时间。在设定的时间限制后，辅助程序会静默停止。

主程序用于控制 Postfix 的整体运行。[表 25.3] 显示了 Postfix 用于传输邮件消息的辅助程序。

### 表 25.3 Postfix 辅助程序

| 程序 | 描述 |
| :--- | :--- |
| `bounce` | 为退回邮件在退回邮件队列中发布日志并将退回邮件返回给发件者 |
| `cleanup` | 处理入站邮件头并将消息放入入站队列 |

## Postfix 队列

Postfix 使用多个不同的队列来管理处理过程中的电子邮件消息。每个队列包含处于不同状态的消息。表 25.4 列出了 Postfix 使用的队列。

| 队列 | 描述 |
| :--- | :--- |
| `mail` | 等待处理的来自本地用户的新消息。 |
| `incoming` | 等待处理的或来自远程主机的新消息。 |
| `active` | 准备好进行投递的消息。 |
| `deferred` | 初始投递失败并等待下一次尝试的消息。 |
| `flush` | 目标为远程主机的消息，这些主机将连接到邮件服务器来获取它们。 |
| `mail` | 如果 Postfix 系统随时关闭，消息将保留在它们最后所在的队列中。当 Postfix 重启时，它将自动从队列开始处理消息。这是 Postfix 的一个优秀特性，使其成为可用最稳健的电子邮件系统之一！ |

## 配置文件

Postfix 系统的一个至关重要的部分是配置文件。Postfix 使用三个独立的配置文件，允许你设置用于指导 Postfix 如何处理消息的参数。与其他 MTA 程序不同，可以在 Postfix 服务器运行时更改配置信息，并发出命令让 Postfix 载入新信息，而无需完全停止邮件服务器。

这三个配置文件通常存储在公共 Postfix 目录中。通常，该目录的默认位置是`/etc/postfix`。通常，所有用户都有查看配置文件的权限，而只有 root 用户有更改文件内值的权限。当然，出于安全考虑，可以对此进行修改。表 25.5 列出了配置文件。

### 表 25.5 Postfix 配置文件

| 文件 | 描述 |
| :--- | :--- |
| `install.cf` | 包含安装 Postfix 时使用的安装参数信息。`install.cf` 配置文件允许你检索 Postfix 软件首次安装到系统上时使用的安装参数。这提供了一种简单的方法，来确定设置中哪些功能可用或不可用。 |
| `main.cf` | 包含 Postfix 程序在处理消息时使用的参数。 |
| `master.cf` | 包含 Postfix 主程序在运行核心程序时使用的参数。 |

`master.cf` 配置文件控制 Postfix 核心程序的行为。每个程序都单独列在一行，并带有控制其操作的参数。这是一个带有默认设置的示例`master.cf`文件：

```
#==================================

# service type unpriv root wakeup maxproc command + args

#             (yes)  (yes)  (yes)  (never) (50)

#==================================

smtp     inet  n  -  n  -  -  smtpd

pickup   fifo  n  -  n  60  1   pickup

cleanup  unix  -  -  n  -  0   cleanup

qmgr     fifo  n  -  n  300 1   qmgr

rewrite  unix  -  -  n  -  -  trivial-rewrite

bounce   unix  -  -  n  -  0   bounce

defer    unix  -  -  n  -  0   defer
```

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 指定额外的 SMTP 头部行。 |
| `-b` | 向消息中添加 BCC（密送）收件人。 |
| `-c` | 向消息中添加 CC（抄送）收件人。 |
| `-e` | 如果消息为空，则不发送。 |
| `-i` | 忽略 TTY 中断信号。 |
| `-I` | 强制 Mailx 在交互模式下运行。 |
| `-n` | 不读取`/etc/mail.rc`启动文件。 |
| `-s` | 指定主题（Subject）。 |
| `-v` | 在终端上显示投送详情。 |

正如从表 25.6 所示，你几乎可以通过命令行参数创建整个电子邮件。你唯一需要添加的是消息正文。

要做到这一点，你需要将文本重定向到`mail`命令。这里有一个直接从命令行创建并发送电子邮件的简单示例：

```
$ echo "This is a test message" | mail -s "Test message" rich
```

Mailx 程序将来自`echo`命令的文本作为消息正文。这为你从 shell 脚本发送消息提供了一种方便的方法。这里有一个快速示例：

```bash
$ cat factmail

#!/bin/bash

# 发送阶乘结果

MAIL='which mail'

factorial=1

counter=1

read -p "Enter the number: " value

while [ $counter -le $value ]

do

    factorial=$[$factorial * $counter]

    counter=$[$counter + 1]

done

echo The factorial of $value is $factorial | mail -s "Factorial answer" $USER

echo "The result has been mailed to you."
```

此脚本并没有假设 Mailx 程序位于标准位置。它使用`which`命令来确定`mail`程序的具体位置。

在计算完阶乘函数的结果后，shell 脚本使用`mail`命令将消息发送到用户定义的`$USER`环境变量，该变量应该是执行脚本的人。

```bash
$ ./factmail

Enter the number: 5

The result has been mailed to you.

$
```

你只需要检查你的邮箱以查看答案是否送达：

```bash
$ mail

"/var/mail/rich": 1 message 1 new

>N    1 Rich Blum             Thu Dec  9 10:32  13/586   Factorial answer

?

Return-Path: <rich@rich-Parallels-Virtual-Platform>

X-Original-To: rich@rich-Parallels-Virtual-Platform>

Delivered-To: rich@rich-Parallels-Virtual-Platform

Received: by rich-Parallels-Virtual-Platform (Postfix, from userid 1000)

        id B4A2A260081; Thu,  9 Dec 2010 10:32:24 -0500 (EST)

Subject: Factorial answer

To: <rich@rich-Parallels-Virtual-Platform>

X-Mailer: mail (GNU Mailutils 2.1)

Message-Id: <20101209153224.B4A2A260081@rich-Parallels-Virtual-Platform>

Date: Thu,  9 Dec 2010 10:32:24 -0500 (EST)

From: rich@rich-Parallels-Virtual-Platform (Rich Blum)

The factorial of 5 is 120

?
```

在消息正文中仅发送一行文本并不总是方便的。通常，你可能需要将整个输出作为电子邮件消息。在这些情况下，你始终可以将文本重定向到临时文件，然后使用`cat`命令并将输出重定向到`mail`程序。

这里是一个在电子邮件消息中发送较多数据的示例：

```bash
$ cat diskmail

#!/bin/bash

# 在电子邮件中发送当前磁盘统计信息

date='date +m/%d/%Y'

MAIL='which mail'

TEMP='mktemp tmp.XXXXXX'

df -k > $TEMP

cat $TEMP | $MAIL -s "Disk stats for $date" $1

rm -f $TEMP
```

`diskmail`程序使用`date`命令获取当前日期（带有一些特殊格式），找到 Mailx 程序的路径，然后创建一个临时文件。之后，它使用`df`命令显示当前的磁盘空间统计信息（见第 4 章），并将输出重定向到临时文件。

然后它将临时文件重定向到`mail`命令，使用第一个命令行参数作为目标地址，并在主题头中使用当前日期。当你运行脚本时，你不会在命令行输出上看到任何内容：

```bash
$ ./diskmail rich
```

但如果你检查你的邮箱，你应该能看到送出的消息：

```bash
$ mail

"/var/mail/rich": 1 message 1 new

>N    1 Rich Blum             Thu Dec  9 10:35  19/1020   Disk stats for 12/09/2010

?

Return-Path: <rich@rich-Parallels-Virtual-Platform>

X-Original-To: rich@rich-Parallels-Virtual-Platform>

Delivered-To: rich@rich-Parallels-Virtual-Platform>

Received: by rich-Parallels-Virtual-Platform (Postfix, from userid 1000)

        id 3671B260081; Thu,  9 Dec 2010 10:35:39 -0500 (EST)

Subject: Disk stats for 12/09/2010

To: <rich@rich-Parallels-Virtual-Platform>

X-Mailer: mail (GNU Mailutils 2.1)

Message-Id: <20101209153539.3671B260081@rich-Parallels-Virtual-Platform>

Date: Thu,  9 Dec 2010 10:35:39 -0500 (EST)

From: rich@rich-Parallels-Virtual-Platform (Rich Blum)

Filesystem     Blocks      Used Available Use% Mounted on

/dev/sda1      63315876 25955124 37360752  41% /
```

| 选项 | 描述 |
| :--- | :--- |
| `-F muttrc` | 指定一个初始化文件进行读取，而不是`$HOME/.muttrc`。 |
| `-h` | 显示帮助文本。 |
| `-H draft` | 指定一个包含头信息和正文的草稿文件用于发送消息。 |
| `-i include` | 指定一个包含在消息正文中的文件。 |
| `-m type` | 指定默认邮箱类型。 |
| `-n` | 忽略系统配置文件。 |
| `-p` | 恢复已推迟的消息。 |
| `-Q query` | 查询配置变量的值。查询会在所有配置文件解析完毕且命令行给出的任何命令执行后执行。 |
| `-R` | 以只读模式打开邮箱。 |
| `-s subject` | 指定消息的主题。 |
| `-v` | 显示 Mutt 版本号和编译时定义。 |
| `-x` | 模拟 Mailx 的组合模式。 |
| `-y` | 从列出`mailboxes`命令指定的所有邮箱开始。 |
| `-z` | 与`-f`同时使用，如果邮箱中没有消息，则不启动。 |
| `-Z` | 打开`mailboxes`命令指定的包含新邮件的第一个邮箱。 |

通过无数种命令行参数，你可以直接从命令行自定义你的电子邮件消息，这正是你在 shell 脚本中想要做的。

与`Mailx`程序一样，`Mutt`程序中有一点是你无法在命令行上指定的，那就是消息的正文文本。如果你不将文本重定向到`Mutt`程序，它将以文本图形模式启动，并打开一个编辑器窗口供你输入消息正文。

对于 shell 脚本来说这不是一件好事，因此你总是希望重定向某种类型的文本作为消息正文，即使你正在使用附件选项来指定要附加的文件。下一节将演示如何这样做。

### 使用 Mutt

现在你准备好在 shell 脚本中使用`Mutt`程序了。要在你的 shell 脚本中创建基础的`mutt`命令，你需要包含指定消息主题、附件文件以及消息所有收件人的命令行选项：

```
mutt -s Subject -a file -- recipients
```

`recipients`列表是一个用空格分隔的电子邮箱地址列表。如果你想附加多个文件，可以在`-a`选项之后列出用空格分隔的文件；`--`符号用于将文件名与收件地址列表隔离开。`file`参数必须是绝对路径，或者是从运行`mutt`命令的当前工作目录相对路径。

`mutt`命令还有另一个陷阱。如果你没有重定向消息正文文本，Mutt 将自动进入全屏模式，让你在编辑器窗口中输入文本。这可能不是你想要的，所以请确保为消息正文重定向一些文本：

```
echo "Here's the log file" | mutt -s file -a /var/log/messages
```



此命令将系统日志文件作为附件发送到本地系统上的邮箱地址 `rich`。请注意，你还必须拥有访问要附加文件的相应权限。图 25.5 显示了 Evolution 邮件客户端中收到的电子邮件。注意消息包含了来自 `echo` 语句的正文文本，以及一个单独的附件图标。你可以直接从 KMail 客户端保存附件文件。

> 注意
> 如果查看附件文件名，你会发现 Mutt 使用附件文件的基名（basename）作为名称。使用临时文件时要小心，因为 Mutt 将使用临时文件名作为附件。使用更具描述性的名称来保存临时文件会比使用临时名称要好。

## 总结

本章讨论了如何在 shell 脚本中整合电子邮件。定期向客户发送电子邮件报告是 shell 脚本中可以提供的一个很棒的功能。

在使用命令行发送电子邮件消息之前，你需要了解电子邮件在 Linux 环境中如何工作，以及你需要安装和配置哪些应用程序。Linux 邮件环境由三个元素组成：邮件传输代理（MTA）程序、邮件传递代理（MDA）程序（通常是 MTA 程序的一部分）以及邮件用户代理（MUA）程序。

MTA 程序负责为 Linux 系统收发邮件消息。它必须知道如何将传入的邮件传递给正确的用户邮箱，以及如何发送发往远程邮件服务器用户的出站邮件。通常，MTA 程序会使用代理服务器（也称为智能主机）来完成投递。它将任何发往远程服务器用户的消息转发给智能主机进行投递。它可以依靠智能主机自行完成投递。

MDA 程序负责确保发往本地用户的邮件进入正确的本地邮箱。有时此功能由 MTA 程序直接执行。但是，如果你需要高级的邮件投递功能（例如离开通知或垃圾邮件过滤），你可以配置 MTA 程序将消息传递给 MDA 程序，后者通常内置了这些功能。

MUA 程序允许单个系统用户访问其邮箱中的消息，并将出站消息传递给 MTA 进行投递。这些程序范围从简单的命令行程序（如 `Mailx` 和 `Mutt`）到精美的图形化程序（如 `KMail` 和 `Evolution`）。

从 shell 脚本发送电子邮件最简单的方法是使用 `Mailx` 程序。该程序允许你在命令行上指定主题头和一个或多个收件人。你通过将文本重定向到 `Mailx` 程序来创建消息正文。你可以使用 `echo` 命令处理单行文本，或使用 `cat` 命令将文件内容重定向到邮件消息。

`Mutt` 程序是一个更高级的命令行 MUA 程序，它提供了为邮件消息附加文件的能力，而不是在消息正文中包含文本。这允许你附加大型文本文件，客户可以轻松将其保存到磁盘，并在其他程序（如表格或文字处理软件包）中检查。

本书的最后两章涵盖了 shell 脚本的重要部分：编写脚本管理函数。如果你是 Linux 系统管理员，很可能会遇到想要定期监控系统功能状态的情况。通过创建一个 shell 脚本并将其放在 `cron` 任务中，你可以轻松监控 Linux 系统中发生的情况。

## 第 26 章：编写脚本工具

在本章中：
- 监控磁盘空间
- 执行备份
- 管理用户账户

没有地方比为 Linux 系统管理员编写脚本工具的 shell 脚本编程更有用了。典型的 Linux 系统管理员每天有许多需要完成的工作，从监控磁盘空间到备份重要文件再到管理用户账户。shell 脚本工具可以让系统管理员的生活变得简单得多！本章演示了在 `bash` shell 中编写脚本工具的一些能力。

### 监控磁盘空间

多用户 Linux 系统最大的问题之一是可用磁盘空间量。在某些情况下（例如文件共享服务器），仅仅因为一个粗心的用户，磁盘空间就可能立即填满。

此 shell 脚本工具可以帮助你确定指定目录中占用磁盘空间排名前十的项目。它会生成带有日期戳的报告，允许你监控磁盘空间消耗趋势。

#### 所需的函数

你需要使用的第一个工具是 `du` 命令（参见第 4 章）。该命令显示单个文件和目录的磁盘使用情况。`-s` 选项允许你在目录层级汇总总量。这在计算单个用户使用的总磁盘空间时非常有用。以下是使用 `du` 命令对 `/home` 目录下每个用户的 `$HOME` 目录进行汇总示例：

```
$ du -s /home/*
6174428      /home/consultant
4740           /home/Development
4740           /home/Production
3860           /home/Samantha
7916           /home/Timothy
140376116      /home/user
$
```

`-s` 选项对于用户的 `$HOME` 目录很好，但如果我们想查看像 `/var/log` 等系统目录的磁盘占用情况怎么办？

```
$ du -s /var/log/*
4           /var/log/alternatives.log
44          /var/log/alternatives.log.1
4           /var/log/apparmor
176         /var/log/apt
0           /var/log/aptitude
4           /var/log/aptitude.1.gz
4           /var/log/aptitude.2.gz
4           /var/log/aptitude.3.gz
4           /var/log/aptitude.4.gz
4           /var/log/aptitude.5.gz
160         /var/log/auth.log
...
$
```

列表很快变得过于详细。`-S` 选项在这里更符合我们的需求，它能为每个目录和子目录单独提供总计。这允许你快速定位问题区域：

```
$ du -S /var/log
176      /var/log/apt
52       /var/log/exim4
1048     /var/log/dist-upgrade/20101011-1337
6148     /var/log/dist-upgrade
1248     /var/log/installer
228      /var/log/gdm
4        /var/log/news
4        /var/log/samba/cores/winbindd
4        /var/log/samba/cores
16       /var/log/samba
4        /var/log/unattended-upgrades
4        /var/log/sysstat
4        /var/log/speech-dispatcher
108      /var/log/ConsoleKit
64       /var/log/cups
4        /var/log/apparmor
12       /var/log/fsck
4844     /var/log
$
```

由于我们感兴趣的是占用最大磁盘空间块的目录，你需要对 `du` 生成的列表使用 `sort` 命令（参见第 4 章）：

```
$ du -S /var/log | sort -rn
6148    /var/log/dist-upgrade
4864    /var/log
1248    /var/log/installer
1048    /var/log/dist-upgrade/20101011-1337
228     /var/log/gdm
176     /var/log/apt
108     /var/log/ConsoleKit
64      /var/log/cups
52      /var/log/exim4
16      /var/log/samba
12      /var/log/fsck
4       /var/log/unattended-upgrades
4       /var/log/sysstat
4       /var/log/speech-dispatcher
4       /var/log/samba/cores/winbindd
4       /var/log/samba/cores
4       /var/log/news
4       /var/log/apparmor
$
```

`-n` 选项允许你进行数值排序。`-r` 选项将最大的数字列在前。这对于寻找最大的占用者非常完美。`sed` 编辑器（参见第 18 和第 20 章）将使列表更加清晰。为了聚焦前十名磁盘占用者，当到达第 1 行时，`sed` 被设置为删除列表的剩余部分。下一步是为每行添加行号。第 18 章已向了如何通过向 `sed` 命令添加等号 `=` 来实现这一点。为了让这些行号与磁盘空间在同一行，正如我们在第 20 章中做的那样，使用 `N` 命令合并文本行。`sed` 命令如下：

```bash
sed '{1,$D}' | sed 'N; /'
```

现在可以使用 `awk` 命令清理输出（参见第 21 章）。来自 `sed` 编辑器的输出被传递给 `awk` 命令，然后使用 `printf` 函数打印出来。

```bash
awk '{printf $1 ":\t" $2 "\t" $3 "\n"}'
```

在行号之后添加了一个冒号（`:`），并在每行输出的各个字段之间放置了制表符（`\t`）。这产生了一个格式整齐的前十名磁盘空间占用者列表。

```
$ du -S /var/log | sort -rn | sed '{1,$D}' | sed 'N; /' | awk '{printf $1 ":\t" $2 "\t" $3 "\n"}'
1:   6148    /var/log/dist-upgrade
2:   4864    /var/log
3:   1248    /var/log/installer
4:   1048    /var/log/dist-upgrade/20101011-1337
5:   228     /var/log/gdm
6:   176     /var/log/apt
7:   108     /var/log/ConsoleKit
8:   64      /var/log/cups
9:   52      /var/log/exim4
10:  16      /var/log/samba
$
```

现在你已经入门了！下一步是使用这些信息创建脚本。

#### 创建脚本

为了节省时间和精力，脚本为多个指定目录创建报告。使用一个名为 `CHECK_DIRECTORIES` 的变量来实现这一点。对于我们的目的，该变量被设置为仅两个目录：

```bash
CHECK_DIRECTORIES="/var/log /home"
```

脚本包含一个 `for` 循环，对变量列出的每个目录执行 `du` 命令。这种技术用于（参见第 12 章）读取和处理列表中的值。每当 `for` 循环遍历变量 `CHECK_DIRECTORIES` 中的值列表时，它会将列表中的下一个值赋值给 `DIR_CHECK` 变量：

```bash
for DIR_CHECK in $CHECK_DIRECTORIES
do
  ...
  du -S $DIR_CHECK
  ...
done
```

为了便于快速识别，使用 `date` 命令在报告的文件名添加了日期戳。使用 `exec` 命令（参见第 14 章），脚本将其输出重定向到带有日期戳的报告文件：

```bash
DATE=$(date '+%m%d%y')
exec > disk_space_$DATE.rpt
```

现在，为了产生格式良好的报告，脚本使用 `echo` 命令放入几个报告标题：

```bash
echo "Top Ten Disk Usage"
echo "for $CHECK_DIRECTORIES Directories"
```

让我们来看看整个脚本是如何组合的：

```bash
#!/bin/bash
#
# Big_Users - 查找各种目录的大磁盘占用者
###############################################
# Parameters for Script
# 
CHECK_DIRECTORIES="/var/log /home"   # 要检查的目录
# 
############## Main Script #################################
#
DATE=$(date '+%m%d%y')              #报告文件的日期
# 
exec > disk_space_$DATE.rpt         #报告标准输出
#
echo "Top Ten Disk Usage"           # 报告标题
echo "for $CHECK_DIRECTORIES Directories"
for DIR_CHECK in $CHECK_DIRECTORIES #循环目录
do
  echo ""
  echo "The $DIR_CHECK:"           # 每个目录的标题
  # 创建占用者列表
  du -S $DIR_CHECK | sed '{1,$D}' | sed 'N; /' | awk '{printf $1 ":\t" $2 "\t" $3 "\n"}'
done                                #循环结束
```

就这样。这是一个为你选择的目录创建日期戳报告的简单 shell 脚本。

#### 运行脚本

在让 `Big_Users` 脚本自动运行之前，你想手动测试几次，以确保它的运行符合预期：

```
$
$ ./Big_Users
$
$ cat disk_space_012311.rpt
Top Ten Disk Usage
for /var/log /home Directories
The /var/log:
1:   6148    /var/log/dist-upgrade
2:   4864    /var/log
3:   1248    /var/log/installer
4:   1048    /var/log/dist-upgrade/20101011-1337
5:   176     /var/log/apt
6:   108     /var/log/ConsoleKit
7:   64      /var/log/cups
8:   52      /var/log/exim4
9:   16      /var/log/samba
10:  12      /var/log/fsck
```

`/home` 目录：

```
1:        92365332 /home/user/.VirtualBox/HardDisks
2:        18659720 /home/user/Downloads
3:        17626092 /home/user/archive
4:        6174408 /home/Timothy/Junk/More_Junk
5:        6174408 /home/Timothy/Junk
6:        6174408 /home/consultant/Work
7:        6174408 /home/consultant/Downloads
8:        3227768 /home/user/vmware/Mandriva
9:        3212464 /home/user/vmware/Fedora
10:         104632 /home/user/vmplayer
```

```
$
```

成功了！现在你可以设置 shell 脚本根据需要自动执行。你可以使用 `cron` 表来实现此功能（参见第 15 章）。

> 注意
> 当运行包含需要 root 权限的 bash shell 命令的脚本时，你需要使用 `su` 或 `sudo` 命令。否则，脚本将产生意想不到的结果。

运行此脚本的频率取决于你的文件服务器的活跃程度。要每周运行一次脚本，请向你的 `cron` 表添加以下条目：

```
15 7 * * 1 /home/user/Big_Users
```

该条目会在每周一早上 7:15 运行 shell 脚本。现在，你可以在周一早上第一时间喝着咖啡，查看你的每周磁盘占用报告了。

### 执行备份

无论你是在商业环境中负责 Linux 系统，还是仅仅在家里使用，数据丢失都可能是灾难性的。为了防止糟糕情况的发生，定期备份是一个好主意。

然而，良好的主意和实际可行性往往是两回事。尝试安排备份计划来存储重要文件可能是一项挑战。这也是 shell 脚本经常大显身手的领域。

本节演示了使用 shell 脚本备份 Linux 系统数据的两种不同方法。

#### 归档数据文件

如果你正在使用 Linux 系统处理重要项目，可以创建一个 shell 脚本来自动对特定目录创建快照。在配置文件中指定这些目录允许你在特定项目发生变化时更改它们。这将有助于避免从主存档文件中进行耗时的恢复过程。

本节将向你展示如何创建一个自动化 shell 脚本，对指定的目录创建快照，并保留数据过去版本的存档。

##### 所需函数

Linux 世界中归档数据的核心工具是 `tar` 命令（参见第 4 章）。`tar` 命令用于将整个目录归档为单个文件。这是一个使用 `tar` 命令创建工作目录归档文件的示例：

```
$ tar -cf archive.tar /home/user/backup_test
tar: Removing leading ‘/’ from member names
$
```



`tar` 命令会返回一条警告信息，说明它正在从路径中删除起始的正斜杠，将其从绝对路径转换为相对路径（参见第 3 章）。这允许你在文件系统的任何位置提取这些 `tar` 归档文件。你可能想在脚本中消除这条信息。可以通过将 `STDERR` 重定向到 `/dev/null` 文件来实现（参见第 14 章）：

```
$ tar -cf archive.tar /home/user/backup_test 2>/dev/null
$
```

由于 `tar` 归档文件可能会占用大量磁盘空间，因此压缩文件是一个好主意。你可以通过简单添加 `-z` 选项来实现。这将 `tar` 归档文件压缩为 gzipped `tar` 文件，称为 tarball。请确保使用正确的文件扩展名表示该文件是 tarball。使用 `.tar.gz` 或 `.tgz` 都可以。这是一个创建工作目录 tarball 的示例：

```
$ tar -zcf archive.tar.gz /home/user/backup_test 2>/dev/null
$
```

现在你已经完成了归档脚本的主要组件。

与其为每个想要备份的新目录或文件修改或创建新的存档脚本，你可以使用配置文件。配置文件应该包含你想包含在存档中的每个目录或文件：

```
$ cat Files_To_Backup
/home/user/Downloads
/home/user/Documents/CLandSS_V2
/home/Samantha/Documents
/home/Does_not_exist
/home/Timothy/Junk
/home/consultant/Work
$
```

> **注意**
>
> 如果你使用的是包含图形桌面的 Linux 发行版，请小心归档整个`$HOME`目录。虽然这看起来很好，但`$HOME`目录包含许多与图形桌面相关的配置和临时文件。这将创建一个比你预期的大得多的存档文件。选择一个存储工作文件的子目录，并在归档配置文件中使用该子目录。

你可以让脚本读取配置文件并将每个目录或文件的名称添加到存档列表中。要做到这一点，请使用简单的`read`命令（参见第 13 章）从文件中读取每条记录。但与我们在第 13 章中那样将`cat`命令通过到`while`循环不同，此脚本将使用`exec`命令重定向`STDINPUT`（参见第 14 章）。它看起来如下：

```
exec < $CONFIG_FILE
read FILE_NAME
```

注意，归档配置文件以及从文件中读取的每条记录都使用了变量。只要`read`命令在配置文件中找到新记录进行读取，它就会在`?`变量中返回退出 0 表示成功（参见第 10 章）。你可以将其用作`while`循环中的测试，以读取配置文件中的所有记录：

```
while [ $? -eq 0 ]
do
  ...
read FILE_NAME
```

`Daily_Archive` 脚本会自动在指定位置创建一个归档，并使用当前日期来唯一标识文件。以下是脚本该部分的代码：

```bash
DATE='date +y%m%d'

#
# 设置归档文件名
#
FILE=archive$DATE.tar.gz
#
# 设置配置文件和目标文件
#
CONFIG_FILE=/home/user/archive/Files_To_Backup
DESTINATION=/home/user/archive/$FILE
```

`DESTINATION` 变量附加了归档文件的完整路径。`CONFIG_FILE` 变量指向包含要归档文件的归档配置文件。如果需要，这两者都可以轻松更改为备用目录和文件。

整合在一起，`Daily_Archive` 脚本现在看起来如下：

```bash
#!/bin/bash
#
# Daily_Archive - 归档指定的文件和目录
###############################################
#
# 获取当前日期
#
DATE='date +y%m%d'

#
# 设置归档文件名
#
FILE=archive$DATE.tar.gz
#
# 设置配置文件和目标文件
#
CONFIG_FILE=/home/user/archive/Files_To_Backup
DESTINATION=/home/user/archive/$FILE
######### 主脚本 ##########
#
# 检查备份配置文件是否存在
#
if [ -f $CONFIG_FILE ]   # 确保配置文件仍然存在。 
then                # 如果存在，则什么都不做继续执行。  
      echo
else                # 如果不存在，发出错误并退出脚本。
      echo
      echo "CONFIG_FILE 不存在。"
      echo "由于缺少文件，备份完成" 
      echo
      exit
fi
#
# 构建所有待备份的文件名 
#
FILE_NO=1    # 从配置文件的第 1 行开始。 
exec < $CONFIG_FILE    # 将标准输入重定向到配置文件名
#
read FILE_NAME      # 读取第一条记录 
#
while [ $? -eq 0 ]    # 创建要归档的文件列表。 
do
    # 确保文件或目录存在。
    if [ -f $FILE_NAME -o $FILE_NAME ]
    then
        # 如果文件存在，将其名称添加到列表。
        FILE_LIST="FILE_LIST $FILE_NAME"
    else
        # 如果文件不存在，发出警告
        echo
        echo "FILE_NAME 不存在。"
        echo "显然，我不会将其包含在此归档中。"
        echo "它列在配置文件的 $FILE_NO 行。"
        echo "正在继续构建归档列表..." 
        echo
    fi
#
    FILE_NO=$[$FILE_NO + 1] # 行号/文件数加 1。 
    read FILE_NAME      # 读取下一条记录。 
done
#
#######################################
#
# 备份文件并压缩归档
#
tar -czf $DESTINATION $FILE_LIST 2> /dev/null
```

### 运行每日归档脚本

测试 `Daily_Archive` 脚本非常简单：

```bash
$ ./Daily_Archive
/home/Does_not_exist, 不存在。 
显然，我不会将其包含在此归档中。 
它列在配置文件的第 4 行。 
正在继续构建归档列表... 
```

你可以看到脚本捕获了一个不存在的目录`/home/Does_not_exist`。它让你知道该错误目录位于配置文件的第几行，然后继续创建列表并归档数据。数据现在已安全地归档在 tarball 文件中。

### 创建每小时归档脚本

如果你处于文件变化快速的高并发生产环境中，每日归档可能并不理想。如果你想将归档频率增加到每小时一次，你需要考虑另一个因素。

当每小时备份文件并尝试使用`date`命令为每个文件名添加时间戳时，情况会很快变得糟糕。在筛选具有此类文件名的文件目录是非常枯燥的：

`archive0102110233.tar.gz`

与其将所有归档文件放在同一个文件夹中，不如为你的归档文件创建一个目录层次结构。这种原则是：归档目录包含每年每个月的目录，使用月份数字作为目录名。每个月的目录又包含该月每一天的文件夹（使用日期的数值作为目录名）。这允许你只需为单个归档文件标记时间戳，然后将其放在相应的日期和月份目录中。

现在有一个新挑战要解决。脚本必须自动创建各个月份和日期目录，并且知道如果它们已经存在，则不需要创建。

如果你查阅`mkdir`的命令行（参见第 3 章），你会发现`-p`命令行选项。此选项允许你在单个命令中创建目录和子目录；此外，额外的好处是如果目录已存在，它不会产生错误信息。完美！

我们现在准备好创建 `Hourly_Archive` 脚本了。这是脚本的上部分：

```bash
#!/bin/bash
#
# Hourly_Archive - 每小时创建一个归档
#############################
#
# 设置配置文件
#
CONFIG_FILE=/home/user/archive/hourly/Files_To_Backup
#
# 设置基础归目标位置
#
BASEDEST=/home/user/archive/hourly
#
# 获取当前日期、月份和时间
#
DAY='date +d'
MONTH='date +m'
TIME='date +%M'
#
# 创建归档目标目录
#
mkdir -p $BASEDEST/$MONTH/$DAY
#
# 构建归档目标文件名
#
DESTINATION=$BASEDEST/$MONTH/$DAY/archive$TIME.tar.gz
#
########## 主脚本 #####
...
```

一旦脚本到达 `Hourly_Archive` 的“主脚本”部分，该脚本与 `Daily_Archive` 脚本完全相同。大部分工作已经完成了！`Hourly_Archive` 从`date`命令中获取日期和月份值，以及用于唯一标识归档文件的时间戳。然后它使用这些信息创建当天的归档目录（如果已存在则静默退出）。最后，脚本使用`tar`命令创建归档并将其压缩为 tarball。

### 运行每小时归档脚本

与 `Daily_Archive` 脚本一样，在将其放入`cron`表之前测试 `Hourly_Archive` 脚本是一个好主意：

```bash
$ cat /home/user/archive/hourly/Files_To_Backup
/home/Development/Simulation_Logs
/home/Production/Machine_Errors
$
$ ./Hourly_Archive
$
$ ls /home/user/archive/hourly/01/02
archive1601.tar.gz
$
$ ./Hourly_Archive
$ ls /home/user/archive/hourly/01/02
archive1601.tar.gz archive1602.tar.gz
$
```

脚本第一次运行正常，创建了相应的月份和日期目录，然后创建了归档文件。为了测试，再次运行它以查看是否会对现有目录产生问题。脚本再次运行正常并创建了第二个归档文件。它现在可以用于`cron`表了。

### 管理用户账户

用户账户不仅仅是添加、修改和删除账户。你还需要考虑安全问题、保留工作的需求以及准确管理账户。这是一项耗时的任务。这是另一个编写脚本工具真正节省时间的实例！

### 需要的函数

删除账户是账户管理中更复杂的任务。在删除账户时，至少需要四个独立操作：

1. 获取要删除的正确账户名称。
2. 杀死系统中当前运行的属于该账户的所有进程。
3. 确定系统中所有属于该账户的文件。
4. 删除该用户账户。

很容易漏掉某一个步骤。本节中的 Shell 脚本工具将帮助你避免犯此类错误。

## 获取正确的账户名

删除账户过程的第一步是最重要的，即获取要删除的正确账户名。由于这是一个交互式脚本，你可以使用`read`命令（参见第 13 章）来获取账户名。如果脚本用户离开了并让问题悬挂在那里，你可以使用`read`命令的`-t`选项，在给脚本用户 60 秒时间回答问题后超时：

```bash
echo "Please enter the username of the user "
echo -e "account you wish to delete from system: \c"
read -t 60 ANSWER
```

由于中断是生活的一部分，最好给用户三次回答问题的机会。为了实现这一点，请使用`while`循环（参见第 12 章）并配合`-z`选项来测试`ANSWER`变量是否为空。当脚本第一次进入`while`循环时，`ANSWER`变量长度为零，因为问题会被放在循环的末端：

```bash
while [ -z "$ANSWER" ]
do
  ...
echo "Please enter the username of the user "
echo -e "account you wish to delete from system: \c"
read -t 60 ANSWER
done
```

现在你需要一种方法与脚本用户通信，告知第一次问题超时的情况、还有一次回答问题的机会等等。`case`语句（参见第 11 章）是可以在此处完美工作的结构化命令。通过使用递增的 `ASK_COUNT` 变量，你可以设置不同的消息与脚本用户通信。该部分的代码如下：

```bash
case $ASK_COUNT in
2)
      echo
      echo "Please answer the question."
      echo
;;
3)
      echo
      echo "One last try...please answer the question."
      echo
;;
4)
      echo
      echo "Since you refuse to answer the question..."
      echo "exiting."
      echo
      exit
;;
esac
```

现在脚本已经拥有了请求用户删除账户所需的所有结构。此脚本中有几个问题你需要提问，仅仅问一个问题就已经写了大量代码！因此，让我们这段代码转换为一个函数（参见第 16 章），以便在你的 `Delete_User` 脚本的多个位置使用它。

你首先做的第一件事是声明函数名 `get_answer`。接下来，使用`unset`命令（参见第 5 章）清除脚本用户之前提供的任何回答。执行这些操作的代码如下：

```bash
function get_answer{
unset ANSWER
```

你在原始代码中需要更改另一个项目是对向脚本用户的实际问题。脚本不会每次都问同一个问题，所以让我们创建两个变量 `LINE1` 和 `LINE2` 来处理问题所在行：

```bash
echo $LINE1
echo -e $LINE2 \c
```

然而，并不是每个问题都有两行。有些只有一行。使用`if`结构（参见第 1 章）来协助解决这个问题。该函数将测试 `LINE2` 是否为空，如果为空，则仅使用 `LINE1`：

```bash
if [ -n "$LINE2" ]
then
  echo $LINE1
  echo -e $LINE2 \c
else
  echo -e $LINE1 \c
fi
```

最后，我们的函数需要通过清除 `LINE1` 和 `LINE2` 变量来自我清理。因此，函数现在看起来是：

```bash
function get_answer{
unset ANSWER
ASK_COUNT=0
while [ -z "$ANSWER" ]
do
  ASK_COUNT=$[ ASK_COUNT + 1 ]
  case $ASK_COUNT in
  2)
      echo ...
  esac
  echo
  if [ -n "$LINE2" ]
  then      #打印 2 行
    echo $LINE1
    echo -e $LINE2 \c
  else      #打印 1 行
    echo -e $LINE1 \c
  fi
  read -t 60 ANSWER
done
unset LINE1
unset LINE2
} # get_answer 函数结束
```

要询问脚本用户要删除哪个账户，你需要设置几个变量然后调用 `get_answer` 函数。使用新函数使脚本代码变得简单得多：

```bash
LINE1="Please enter the username of the user "
LINE2="account you wish to delete from system:"
get_answer
USER_ACCOUNT=$ANSWER
```

由于可能存在拼写错误，你希望验证输入的账户名。因为我们已经有了代码来处理提问：

```bash
LINE1="Is $USER_ACCOUNT the user "
LINE2="you wish to delete from system? y/n"
get_answer
```

一旦提问，脚本需要处理回答。变量 `ANSWER` 携带用户对问题的回答。如果用户回答“是”，你就获得了要删除账户。可以使用`case`语句（参见第 1 章）来处理回答。确保代码处理输入“是”的情况：

```bash
case $ANSWER in
y|yes|yEs|yS|yES ) 
;;
*)
  echo "the account, $USER_ACCOUNT, is not "
  echo "the one you wish to delete, we are leaving the script..."
  exit
;;
esac
```

脚本多次需要处理用户的是/否回答。因此，创建一个函数来处理这项任务是合理的。只需要对前面的代码进行少量修改。简单地声明函数名并将 `EXIT_LINE1` 和 `EXIT_LINE2` 变量添加到 `case` 语句中。结合最后的变量清理，这些将产生 `process_answer` 函数：

```bash
function process_answer{
case $ANSWER in
y|yes|yEs|yS|yES ) 
;;
*)
  echo $EXIT_LINE1
  echo $EXIT_LINE2
  exit
;;
esac
unset EXIT_LINE1
unset EXIT_LINE2
} # process_answer 函数结束
```

简单的函数调用现在将处理回答：



```bash
EXIT_LINE1=“Because the account, $USER_ACCOUNT, is not ”
EXIT_LINE2=“the one you wish to delete, we are leaving the script...”
process_answer
```

用户给了我们要删除的账户并进行了验证。现在是双检查该账户是否存在于系统的良好时间。此外，向脚本用户显示完整的账户记录以检查这真的是要删除的账户。为了完成这些操作，使用变量`USER_ACCOUNT_RECORD`，并设置为对`/etc/passwd`文件的`grep`（参见第 4 章）搜索结果。`-w`选项允许在该特定用户账户的账户记录中进行精确词匹配：

```bash
USER_ACCOUNT_RECORD=$(cat /etc/passwd | grep -w $USER_ACCOUNT)
```

如果在`/etc/passwd`中没有找到任何用户账户记录，这意味着该账户已经被删除或从未存在过。在任何情况下，你都需要让脚本用户知道并退出脚本。`grep`命令的退出状态将在此帮助我们。如果没有找到账户记录，`?`变量将被设置为 1：

```bash
if [ $? -eq 1 ]
then
  echo “Account, $USER_ACCOUNT, not found. ”
  echo “Leaving the script...”
  exit
fi
```

```bash
echo "I found this record:"
echo $USER_ACCOUNT_RECORD
echo
#
LINE1="Is this the correct User Account? [y/n]"
get_answer
#
EXIT_LINE1="Because the account, $USER_ACCOUNT, is not"
EXIT_LINE2="the one you wish to delete, we are leaving the script..."
process_answer
```

# 账户进程

到目前为止，你已经获取并验证了要删除的用户账户正确名称。为了从系统中移除该用户账户，该账户不能拥有任何当前运行的进程。因此，你的下一步是找到并杀掉这些进程。这将变得有点复杂！

查找用户进程将是简单的一部分。在这里，脚本可以使用`ps`命令（参见第 4 章）和`-u`选项来定位任何由该账户拥有的进程。如果确实存在任何进程，它们将显示给脚本用户。

```bash
ps -u $USER_ACCOUNT
```

你可以使用`ps`命令的退出状态和`case`结构来确定下一步采取的措施：

```bash
case $? in
1)
    echo "There are no processes for this account currently running."
    echo
;;
0)
    unset ANSWER
    LINE1="Would you like me to kill the process(es)? [y/n]"
    get_answer
...
esac
```

如果退出状态返回 1，则系统中没有属于该用户账户的运行进程。然而，如果退出状态返回 0，则系统上运行着该该账户的进程。在这种情况下，脚本需要询问脚本用户他们是否想要杀掉这些进程。你可以通过使用`get_answer`函数完成此任务。

你可能认为脚本的下一步操作是调用`process_answer`函数。遗憾的是，下一个项目对于`process_answer`来说太复杂了。你需要嵌入另一个`case`语句来处理脚本用户的回答。`case`语句的第一部分看起来与我们的`process_answer`函数非常相似：

```bash
case $ANSWER in
    y|Y|YES|yes|Yes|yEs|yeS|YEs|yES ) # 如果用户回答 "yes"，
                                       #杀掉用户账户进程。
...
;;
*)   # 如果用户回答 "yes" 以外的任何内容，则不杀死。
    echo
    echo "Will not kill the process(s)"
    echo
;;
esac
```

如你所见，`case`语句本身并没有特别有趣的地方。有趣的地方在于`case`语句中的 "yes" 部分。在这里，需要杀掉用户账户进程。要这样做，重新执行`ps`命令，这次将输出发送到临时报告文件而不是屏幕。

```bash
ps -u $USER_ACCOUNT > $USER_ACCOUNT_Running_Process.rpt
```

你可以使用`exec`命令和`while`循环来读取报告文件，类似于我们在`Daily_Archive`脚本中读取备份配置文件的方法。

```bash
exec < $USER_ACCOUNT_Running_Process.rpt
read USER_PROCESS_REC
while [ $? -eq 0 ]
do
...
    read USER_PROCESS_REC
done
```

在`while`循环内部，使用`cut`命令从每个运行进程的状态记录中提取进程 ID (PID)。一旦获得 PID，就使用`kill`命令（参见第 4 章）配合`-9`选项无条件地终止进程。

```bash
USER_PID=$(echo $USER_PROCESS_REC | cut -d " " -f1)
kill -9 $USER_PID
echo "Killed process $USER_PID"
```

现在任何用户账户拥有的进程都被杀掉，脚本可以移动到下一步，查找该用户账户的所有文件。

# 查找账户文件

当用户账户从系统中删除时，归档属于该账户的所有文件是一个良好的习惯。除了这种做法之外，移除文件或将它们的所有权分配给另一个账户也很重要。如果你删除的账户用户 ID 为 1003，而你没有移除或重新分配这些文件，那么下一个创建的用户 ID 为 1003 的账户将拥有这些文件！你可以看到在这种情况下可能发生的安全灾难。

`Delete_User`脚本不会为你完成所有这些，但它会创建一个报告，该报告可以在`Daily_Archive`脚本中作为备份配置文件使用。你可以利用报告来帮助移除或重新分配文件。

要查找用户文件，你可以使用`find`命令。`find`命令使用`-u`选项搜索整个文件系统，这将精确找到任何用户账户拥有的文件。命令如下：

```bash
find / -user $USER_ACCOUNT > $REPORT_FILE
```

与处理用户账户进程相比，这非常简单！在`Delete_User`脚本的下一步，实际上移除用户账户，操作变得更简单。

# 移除账户

在从系统中移除用户账户时，稍微谨慎一点总是好主意。因此，你应该再次询问脚本用户是否想要移除该账户。

```bash
LINE1="Do you wish to remove User_Account's account? [y/n]"
get_answer
#
EXIT_LINE1="Since you do not wish to remove the account,"
EXIT_LINE2="$USER_ACCOUNT at this time, exiting the script..."
process_answer
```

最后，我们达到了脚本的主要目的，实际上从系统中删除该用户。在这里你可以使用`userdel`命令（参见第 6 章）：

```bash
userdel $USER_ACCOUNT
```

现在我们已经收集了所有的部分，准备好它们组合成一个完整的、实用的工具了。

# 创建脚本

记住`Delete_User`脚本与脚本用户具有高度交互性。因此，包含大量的文字以让用户了解脚本执行过程中的发生情况非常重要。在脚本顶部，声明了两个函数`get_answer`和`process_answer`。然后脚本进入了移除用户的四个步骤：获取用户名；查找并杀掉用户进程；创建用户所有文件的报告；以及实际移除用户。这里是完整的`Delete_User`脚本：

```bash
#!/bin/bash
# Delete_User - 自动完成移除账户的 4 个步骤
###############################################
# Functions
#####################################
function get_answer {
    unset ANSWER
    ASK_COUNT=0
    while [ -z "$ANSWER" ] # 当没有给出回答时，继续询问
    do
        ASK_COUNT=$[ASK_COUNT + 1] # 如果用户在规定时间内没有给出回答
        case $ASK_COUNT in
            2)
                echo
                echo "Please answer the question."
                ;;
            3)
                echo
                echo "One last try...please the question."
                ;;
            4)
                echo
                echo "Since you refuse to answer the question... exiting program."
                exit
                ;;
        esac
        echo
        if [ -n "$LINE2" ]; then # 打印 2 行
            echo $LINE1
            echo -e "$LINE2 \c"
        else # 打印 1 行
            echo -e "$LINE1 \c"
        fi
        # 允许 60 秒回答，超时
        read -t 60 ANSWER
    done
    # 简单的变量清理
    unset LINE1
    unset LINE2
} # get_answer 函数 结束

#####################################
function process_answer {
    case $ANSWER in
        y|Y|YES|yes|Yes|yEs|yeS|YEs|yES ) # 如果用户回答 "yes"，什么都不做。
            ;;
        *) # 如果用户回答 "yes" 以外的任何内容，退出脚本
            echo
            echo $EXIT_LINE1
            echo $EXIT_LINE2
            echo
            exit
            ;;
    esac
}
```

`} #End of process_answer function`

#

##############################################

# 函数定义结束

############## 主脚本 #####################

# 获取要检查的用户账户名称

echo "步骤 #1 - 确定要删除的用户账户名称 "

echo

LINE1="请输入您想要从系统中删除的用户 "

LINE2="账户名："

`get_answer`

`USER_ACCOUNT=$ANSWER`

# 向脚本执行者再次确认是否为正确的的用户账户

LINE1="账户 $USER_ACCOUNT 是您想要 "

LINE2="从系统中删除的账户吗？ [y/n]"

`get_answer`

# 调用 process_answer 函数：

#     如果用户回答的不是“yes（是）”，则退出脚本

EXIT_LINE1="因为账户 $USER_ACCOUNT 不是 "

EXIT_LINE2="您想要删除的那个，我们正在退出脚本..."

`process_answer`

################################################################

# 检查 USER_ACCOUNT 是否确实是系统上的一个账户

`USER_ACCOUNT_RECORD=$(cat /etc/passwd | grep -w $USER_ACCOUNT)`

if [ $? -eq 1 ]; # 如果未找到该账户，则退出脚本

then

    echo

    echo "未找到账户，$USER_ACCOUNT。"

    echo "正在退出脚本..."

    echo

    exit

fi

echo

echo "我找到了这条记录："

echo $USER_ACCOUNT_RECORD

echo

#

LINE1="这是正确的的用户账户吗？ [y/n]"

`get_answer`

# # 调用 process_answer 函数：

#       如果用户回答的不是“yes（是）”，则退出脚本

EXIT_LINE1="因为账户 $USER_ACCOUNT 不是 "

EXIT_LINE2="您想要删除的那个，我们正在退出脚本..."

`process_answer`

##################################################################

# 查找任何属于该用户账户的运行进程

echo

echo "步骤 #2 - 查找系统中属于该用户账户的进程"

echo "$USER_ACCOUNT 正在运行以下进程： "

echo

# ps -u $USER_ACCOUNT #列出运行的用户进程。

case $? in

1) # 该账户没有正在运行的进程

    #

    echo "该账户当前没有运行的进程。"

    echo

;;

0) # 该账户有正在运行的进程。

    # 询问脚本执行者是否希望我们杀死这些进程。

    #

    unset ANSWER

    LINE1="您想让我杀掉这些进程（们）吗？ [y/n]"

    `get_answer`

    #

    case $ANSWER in

        y|YES|Yes|yEs|Y|ES) # 如果用户回答“yes”，

            # 杀死账户进程。

            #

            echo

            # 信号时清理文件

            trap "rm $USER_ACCOUNT_Process.rpt" TERM SIG QUIT

            # 列出运行的进程

            ps -u $USER_ACCOUNT > $USER_ACCOUNT_Process.rpt

            # 生成报告输入

            exec < $USER_ACCOUNT_Process.rpt

            # 第一条记录将为空

            read USER_PROCESS_REC

            while [ $? -eq 0 ]

            do

                # 获取 PID

                USER_PID=$(echo $USER_PROCESS_REC | cut -d " " -f1)

                kill -9 $USER_PID

                echo "已杀死进程 $USER_PID"

                read USER_PROCESS_REC

            done

            #

            echo

            rm $USER_ACCOUNT_Process.rpt # 临时报告。

            ;;

        *) # 如果用户回答的不是“yes”，则不杀死。

            echo

            echo "不会杀死这些进程（们）"

            echo

            ;;

    esac

;;

esac

#################################################

# 创建所有属于该用户账户的文件报告

echo

echo "步骤 #3 - 查找系统中属于该用户账户的文件"

echo

echo "正在创建 $USER_ACCOUNT 拥的所有文件报告。"

echo

echo "建议您备份/存档这些文件，"

echo "然后执行以下两个操作之一："

echo "  1) 删除文件"

echo "  2) 将文件的所有权更改为当前用户账户。"

echo

echo "请等待。这可能需要一些时间..."

#

`REPORT_DATE=$(date +%y%m%d')`

`REPORT_FILE=$USER_ACCOUNT"_Files"$REPORT_DATE".rpt`

#

`find / -user $USER_ACCOUNT > $REPORT_FILE 2>/dev/null`

#

echo

echo "报告已完成。"

echo "报告名称：   $REPORT_FILE"

echo "报告位置：   'pwd'"

echo

####################################

# 用户账户

echo



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



快照报告对于让你了解系统的整体健康状况非常有帮助。然而，这种类型的报告无法让你看到性能和资源使用随时间演变的各种趋势。因此，让我们来看一组脚本，它们将为你提供这类信息。

# 系统统计报告

任何 Linux 系统的核心统计数据都是 CPU 和内存使用情况。如果这些值开始失控，问题会很快出现。本节将演示如何编写脚本，以帮助你在一段时间内监控并跟踪 Linux 系统的 CPU 和内存使用情况。

## 所需的函数

第一个脚本的目的是将性能用量统计数据收集到一个数据文件中以供日后使用。因此，你需要确切地确定想通过脚本收集哪些数据，以及使用哪些命令。

对于此脚本，我们将再次使用`uptime`命令。但这次，我们不是获取系统运行的时间，而是获取系统上的用户数量。用户数量直接影响 CPU 和内存的使用。通过`sed`，我们将在`uptime`命令的输出文本中搜索“users”一词。在当前行中找到该词后，让`sed`直接删除该行的剩余文本，包括“users”一词。这将留下你需要的统计数据——系统用户数——作为该行的最后一个项目。要获取最后一个数据项，你可以使用`gawk`变量`NF`。整个命令行及其输出看起来如下：

```bash
$ uptime | sed 's/users.*$//' | gawk '{print $NF}'
4
```

系统负载是另一个可以从`uptime`命令输出中解析出的良好统计数据。系统负载显示了系统中 CPU 的平均忙程度。平均负载为`1`意味着单个 CPU 一直处于忙状态。然而，如果你的系统中有两个 CPU，这意味着每个 CPU 的忙程度仅为 50%。`uptime`命令提供的系统负载是最后分钟、最后五分钟和最后十五分钟的平均值。我们将获取最后十五分钟的平均系统负载统计数据，它方便地位于输出文本行的末尾：

```bash
$ uptime | gawk '{print $NF}'
0.19
```

另一个提取系统信息的强大命令是`vmstat`。这里是`vmstat`命令的输出示例：

```bash
$ vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
r b    swpd   free  buff  cache   si  so      bi  bo    in  cs    us sy id wa
0 0   11328  42608 165444  502500   0   0      1   2     68  10    1  0 99  0
```

当你第一次运行`vmstat`命令时，它显示自上次重启以来的平均值。要获取当前统计数据，你必须带命令行参数运行`vmstat`命令：

```bash
$ vmstat 1 2
procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
r b    swpd   free  buff  cache   si  so      bi  bo    in  cs    us sy id wa
0 0   11328  43112 165452  502444   0   0      1   2     68  10    1  0 99  0
0 0   11328  40540 165452 505064   0   0      0   0     58 177    1  1 98  0
```

第二行包含 Linux 系统的当前统计数据。如你所示，`vmstat`命令的输出有些晦涩。[表 27.1]解释了每个符号的含义。

### 表 27.1 `vmstat` 输出符号

| 符号 | 描述 |
| :--- | :--- |
| `r` | 等待 CPU 时间的进程数 |
| `b` | 处于不可中断睡眠状态的进程数 |
| `swpd` | 使用的虚拟内存（单位：MB） |
| `free` | 未使用的物理内存量（单位：MB） |
| `buff` | 用作缓冲区内存内存（单位：MB） |
| `cache` | 用作缓存空间的内存（单位：MB） |
| `si` | 从磁盘交换入的内存（单位：MB） |
| `so` | 交换到磁盘的内存（单位：MB） |
| `bi` | 从块设备接收的块数 |
| `bo` | 发送到块设备的块数 |
| `in` | 每秒 CPU 中断数 |
| `cs` | 每秒 CPU 上下文切换数 |
| `us` | 运行非内核代码的 CPU 时间百分比 |
| `sy` | 运行内核代码的 CPU 时间百分比 |
| `id` | 空闲的 CPU 时间百分比 |
| `wa` | 等待 I/O 的 CPU 时间百分比 |

这些是大量信息。空闲内存和 CPU 空闲时间百分比统计数据将满足我们这里的需求。

你可能已经注意到`vmstat`命令的输出包含了表头信息，你显然不想在数据中包含这些内容。要解决这个问题，请使用`sed`命令仅显示包含数值的行：

```bash
$ vmstat 1 2 | sed -n '[0-9]/p'
1 0 11328 38524 165476 506548 0 0 1 2 68 10 1 0 99 0
0 0 11328 35820 165476 509528 0 0 0 0 82 160 1 1 98 0
```

这样好多了，但现在你只需要第二行数据。再次调用`sed`即可解决该问题：

```bash
$ vmstat 1 2 | sed -n '[0-9]/p' | sed -n '2p'
0 0 11328 36060 165484 509560 0 0 0 0 58 177 1 1 98 0
```

（等等，示例输出显示为`0 0 11328 36060...`，遵循上述逻辑）。

最后，你可能为每条记录标记一个时间戳，以指示获取统计数据的时间。只需使用`date`命令并指定你需要的格式即可。

```bash
$ date +%m/%d/%Y %H:%M:%S
12/09/2010 13:55:31
```

## 创建采集脚本

一旦所有函数都就绪，这个用于采集数据的脚本就会非常简单。它的样子如下：

```bash
#!/bin/bash
# Capture_Stats - 收集系统统计
######################
# 设置脚本变量
#
REPORT_FILE=/home/user/Documents/capstats.csv
DATE=$(date +%m/%d/%Y)
TIME=$(date +%H:%M:%S)
##########################################
# 收集性能
#
USERS=$(uptime | sed 's/users.*$//' | gawk '{print $NF}')
LOAD=$(uptime | gawk '{print $NF}')
FREE=$(vmstat 1 2 | sed -n '[0-9]/p' | sed -n '2p' | gawk '{print $4}')
IDLE=$(vmstat 1 2 | sed -n '[0-9]/p' | sed -n '2p' | gawk '{print $15}')
#########################################
# 将统计数据发送到报告文件
#
echo "$DATE,$TIME,$USERS,$LOAD,$FREE,$IDLE" >> $REPORT_FILE
#
```

在创建脚本后，在从你的`cron`表中定期运行之前，你应该先在命令行中对其测试：

```bash
$ cat capstats.csv
12/09/2010,9:06:50,2,0.29,645988,99
12/09/2010,9:07:55,2,0.28,620252,100
```

`12/09/2010, 9:40:51,3,0.37,474740,100`

`12/10/2010,14:36:46,3,0.30,46640,98`

`12/12/2010, 7:16:26,4,0.25,27308,98`

`12/12/2010,13:28:53,4,0.42,58832,100`

接下来的脚本将根据 CSV 数据生成报告并通过电子邮件发送给相关个人。由于报告脚本是一个独立的脚本，你可以让`cron`以与`Capture_Stats`脚本不同的时间表运行它。这让你在报告之前捕获多少数据量上具有灵活性。

## 生成报告脚本

现在你已经有了一个充满原始数据的文件，可以开始编写用于生成精美报告的脚本了。处理此任务的最佳工具是`gawk`命令。

`gawk`命令将允许你从 CSV 文件中提取原始数据并以任何想要的方式呈现。首先，在命令行中进行测试，使用由`Capture_Stats`脚本创建的新`capstats.csv`文件：

```bash
$ cat capstats.csv | gawk -F, '{printf "%s %s - %s\n", $1, $2, $4}'
12/09/2010 9:06:50 - .29
12/09/2010 9:07:55 - .28
12/09/2010 9:40:51 - .37
12/10/2010 14:36:46 - .30
12/12/2010 7:16:26 - .25
12/12/2010 13:28:53 - .42
```

你需要使用`gawk`命令的`-F`选项将逗号定义为数据中的字段分隔符。之后，你可以使用`printf`功能检索每个数据字段并按你需要的方式显示。

对于报告，我们将使用 HTML 格式。HTML 使用简单的标签来界定网页中的数据。然而，HTML 不仅用于网页，你经常会在邮件消息中发现它。取决于你的邮件工具（见第 25 章），你可能会看到嵌入的 HTML 文档。更好的解决方案创建一个 HTML 报告并作为邮件附件。

使用 HTML 创建报告允许你生成格式良好的报告。显示报告程序将完成所有的格式工作。你只需要插入适当的 HTML 标签来格式化数据。在 HTML 中显示表格风格数据最简单的方法是使用`<table>`标签。表格标签允许你创建行和单元格，这些在 HTML 中被称为“划分”。使用`<tr>`标签定义行的开始，使用`</tr>`标签定义行的结束。同样，使用`<td>`和`</td>`标签定义单元格。

完整的 HTML 表格所示：

```html
<html>
<body>
  <h2>Report title</h2>
  <table border="1">
    <tr>
      <td>Date</td><td>Time</td><td>Users</td>
      <td>Load</td><td>Free Memory</td><td>Idle</td>
    </tr>
    <tr>
      <td>12/09/2010</td><td>1:00</td><td>4</td>
      <td>0.26</td><td>57.06</td><td>87</td>
    </tr>
  </table>
</body>
</html>
```

每条数据记录都是`<tr>...</tr>`对的一部分。每个数据字段都在自己的`<td>...</td>`对中。当你在浏览器中显示 HTML 报告时，浏览器会为你创建表格，如图 27.2 所示。

对于脚本，你只需要使用`echo`命令生成 HTML 头部，使用`gawk`命令生成数据，然后再次使用`echo`命令关闭表格。这是`Report_Stats`脚本，它将生成报告并发送：

```bash
#!/bin/bash
# Report_Stats - 从捕获的状态生成报告
# 设置变量
REPORT_FILE=/home/user/capstats.csv
TEMP_FILE=/home/user/capstats.html
# 日期
DATE=$(date +%m/%d/%Y)
# 邮件
MAIL=mutt
MAIL_TO=user
# 创建报告头部
echo "<html><body><h2>Report for $DATE</h2>" > $TEMP_FILE
echo "<table border='1'>" >> $TEMP_FILE
echo "<tr><td>Date</td><td>Time</td><td>Users</td>" >> $TEMP_FILE
echo "<td>Load</td><td>Free Memory</td><td>Idle</td></tr>" >> $TEMP_FILE
# 将性能状态放入报告
cat $REPORT_FILE | gawk -F, '{
  printf "<tr><td>%s</td><td>%s</td><td>%s</td>", $1, $2, $3;
  printf "<td>%s</td><td>%s</td><td>%s</td></tr>\n", $4, $5, $6;
}' >> $TEMP_FILE
echo "</table></body></html>" >> $TEMP_FILE
# 发送性能报告并清理
$MAIL -a $TEMP_FILE -s "Performance Report $DATE" -- $MAIL_TO < /dev/null
rm -f $TEMP_FILE
```

我们使用`mutt`来发送性能报告，但你可以将其更改为本地邮件客户端。临时 HTML 报告的文件也可以修改以更好地符合你的需求。

> **注意**

> 大多数邮件客户端可以通过文件扩展名自动检测附件类型。由于由于原因，你应该以`.html`结束报告文件名。

### 运行脚本

创建`Report_Stats`脚本后，从命令行中进行测试运行并看看发生了什么：

```bash
$ ./Report_Stats
```

嗯，这并不有趣。现在的真正测试是查看你的邮件消息，最好使用如 KMail 或 Evolution 等图形化邮件客户端。图 27.3 展示了如何从 Evolution 邮件客户端查看消息。注意数据是如何使用 HTML 表格进行整齐格式化的，就像在浏览器中查看时一样！

# 问题跟踪数据库

每个系统都不可避免地遇到意外。然而，对问题的分析将允许你做出更改，以尽量减少未来意外的困难。拥有一份关于如何解决问题的记录也有帮助，以防问题再次发生。当你与一个可以记录所经历的问题/解决方案的团队合作工作时，会有更大的收益。问题/解决方案的信息可以更方便地在团队成员之间传播。

在本节中，我们将带你建立基础问题跟踪数据库的过程。此外，我们还将帮助你创建几个高级脚本来记录、更新和审查问题及解决方案。

## 创建数据库

规划数据库结构是创建问题跟踪数据库最重要的部分。你需要确定你想要跟踪什么类型的信息，以及谁有权访问和使用存储在数据库中的数据。

此数据库的主要目的是记录问题及其如何修复，以便你利用这些信息更快速地解决未来的类似问题。为了实现这一目的，你应该跟踪以下信息：

- 报告问题的日期
- 修复问题的日期
- 问题的描述及其症状
- 对问题解决方案的描述

我们将使用`mysql`（见第 23 章）作为问题跟踪数据库的数据库系统。首先，创建一个空数据库：

```bash
$ mysql -u root -p
Enter password:
```

`欢迎使用 MySQL 监控器。命令以 ; 或 \g 结束。`

`...`

```mysql
mysql> CREATE DATABASE Problem_Trek;
Query OK, 1 row affected (0.02 sec)
mysql>
```

创建一个空数据库后，现在可以添加表了。我们将创建一个名为`problem_logger`的表，包含四个字段来存储问题信息。此外，你还需要一个字段`id_number`来作为数据库的主键。[表 27.2]显示了所需的五个字段。

### 表 27.2 `Problem_Logger` 表的字段

| 字段名称 | 数据类型 |
| :--- | :--- |
| `id_number` | integer |
| `report_date` | date |
| `fixed_date` | date |
| `prob_symptoms` | text |
| `prob_solutions` | text |

在`mysql`中创建此表非常简单：

```mysql
mysql> USE Problem_Trek;
Database changed
mysql>
mysql> CREATE TABLE problem_logger (
->  id_number int not null,
->  report_date Date,
->  fixed_date Date,
->  prob_symptoms text,
->  prob_solutions text,
->  primary key (id_number));
Query OK, 0 rows affected (0.04 sec)
mysql>
```

注意，下发`USE`命令是为了确保我们在正确的数据库中创建新表。让我们使用`DESCRIBE`命令再次查看新的`problem_logger`表。这是显示已添加到表中的字段的一种非常清晰的方法：



```mysql
mysql> DESCRIBE problem_logger;
+----------------+---------+------+-----+---------+-------+
| Field           | Type    | Null | Key | Default | Extra |
+----------------+---------+------+-----+---------+-------+
| id_number       | int(11) | NO   | PRI | NULL    |       |
| report_date     | date    | YES |     | NULL    |       |
| fixed_date      | date    | YES |     | NULL    |       |
| prob_symptoms   | text    | YES |     | NULL    |       |
| prob_solutions  | text    | YES |     | NULL    |       |
+----------------+---------+------+-----+---------+-------+
5 rows in set (0.01 sec)
mysql>
```

到目前为止，我们必须使用`root`账户创建数据库和表。现在这些步骤已经完成，你的工作不再需要`root`账户。正如你在第 23 章中学到的，在脚本中使用`root`账户不是良好的做法。因此，你需要为数据库添加一个具有适当权限的新账户。该账户将供脚本用于访问`Problem_Trek`数据库：

```mysql
mysql> GRANT SELECT,INSERT,UPDATE ON Problem_Trek.* TO cbres IDENTIFIED BY 'test_password';
Query OK, 0 rows affected (0.03 sec)
mysql>
```

一旦你为数据库添加了新用户账户，请务必进行测试：

```bash
mysql Problem_Trek -u cbres -p
Enter password:
```

新账户运行得完美！现在，再过一步，你就可以开始为我们的数据库编写所需的函数了。使用你喜欢的文本编辑器创建一个特殊的配置文件`~/.my.cnf`，其中包含你为用户账户设置的密码。这将允许脚本访问`mysql`而无需在内部包含密码。

```bash
cat ~/.my.cnf
[client]
password=test_password
```

并且不要将其限制为仅供访问：

```bash
chmod 400 ~/.my.cnf
```

现在`Problem_Trek`数据库已经创建，并已设置了适当的访问权限。你准备好开始编写数据库脚本了。

## 记录问题

跟踪问题的第一步是记录它的症状。因为使用`mysql`命令记录问题可能会耗时，我们将通过在其周围封装一个易用的脚本来简化这一过程。要将问题信息放入你的`problem_logger`表以向表中插入一条新记录，你需要执行这些命令：

```bash
mysql Problem_Trek -u cbres -p
Enter password:
```

```mysql
mysql> INSERT INTO problem_logger VALUES (
->  101211322,
->  20101211,
->  0,
->  "When trying to run script Capture_Stats, getting message: bash:./Capture_Stats: Permission denied", "");
Query OK, 1 row affected (0.02 sec)
mysql>
```

这非常简单。你可以使用`SELECT`命令查看你刚刚放入表的记录。通过在`WHERE`中指定新记录的 ID 编号，只会显示插入的记录：

```mysql
mysql> SELECT * FROM problem_logger WHERE id_number=101211322;
+-----------+-------------+------------+---------------+---------------++
| id_number | report_date | fixed_date | prob_symptoms | prob_solutions |
+-----------+-------------+------------+---------------+---------------++
| 101211322 | 2010-12-11 | 0000-00-00 | When trying to run script Capture_Stats, getting message: bash:./Capture_Stats: Permission denied | |
+-----------+-------------+------------+---------------+---------------++
1 row in set (0.00 sec)
mysql>
```

虽然你可以看到插入的记录，但在这种格式下很难阅读数据。为了让记录更易读，你可以在命令末尾添加`\G`而不是分号（`;`）：

```mysql
mysql> SELECT * FROM problem_logger WHERE id_number=101211322\G
*************************** 1.row *****************
id_number: 101211322
report_date: 2010-12-11
fixed_date: 0000-00-00
prob_symptoms: When trying to run script Capture_Stats, getting message: bash:./Capture_Stats: Permission denied
prob_solutions: 
```

## 创建脚本

在第 23 章中，你学习了使用`which`命令在你的特定系统上查找`mysql`命令，然后将其分配给环境变量。你可以更进一步，为`mysql`添加数据库名称和用户账户：

```bash
#
MYSQL=$(which mysql) "Problem_Trek -u cbres"
#
```

### 所需函数

`Record_Problem`是一个交互式脚本。为了保持简单，你可以通过提问来获取所需信息。随着脚本获取答案，它会将这些答案分配给不同的变量。一旦收集了所有数据，你就可以使用变量名配合`INSERT`命令将信息输入数据库。这样一来，脚本用户就可以完全忽略那些必要的`mysql`命令了：

```bash
ID_NUMBER=$(date +%y%m%d%H%M)
#
```

由于此脚本仅用于记录问题，你可能还没有关于`FIXED_DATE`和`PROB_SOLUTIONS`变量的数据。因此，在向表中插入记录之前，请将这两个变量都设置为适当的空值：

```bash
#
# 现在将修复日期和问题解决方案设置为空
FIXED_DATE=0
PROB_SOLUTIONS=""
#
```

为了显示问题记录添加成功，请向脚本添加一个`SELECT`语句。为了防止显示整个数据库的内容，`WHERE`命令将使用`ID_NUMBER`变量仅选择刚刚添加的记录：

```
SELECT * FROM problem_logger WHERE id_number=$ID_NUMBER\G
```

将所有部分组合在一起将得到如下脚本：

```bash
#!/bin/bash
#
# Record_Problem - 在数据库中记录问题
######################################################
# 确定 mysql 位置并存入变量
#
MYSQL=‘which mysql‘“ Problem_Trek -u cbres”
#
#############################################
# 创建记录 ID 和报告日期 
#
ID_NUMBER=‘date +%y%m%d%H%M‘
#
REPORT_DATE=‘date +%Y%m%d‘
#
#############################################
# 获取要放入表格的信息
#
echo
echo -e “简要描述问题及其症状: \c”
#
read ANSWER
PROB_SYMPTOMS=$ANSWER
#
# 暂时将固定日期和问题解决方案设为空值
FIXED_DATE=0
PROB_SOLUTIONS=""”
#
##############################################
# 将获取的信息插入表格
#
#
echo
echo “问题记录如下:”
echo
$MYSQL <<EOF
INSERT INTO problem_logger VALUES (
  $ID_NUMBER,
  $REPORT_DATE,
  $FIXED_DATE,
  "$PROB_SYMPTOMS",
  "$PROB_SOLUTIONS");
SELECT * FROM problem_logger WHERE id_number=$ID_NUMBER\G
EOF
#
##############################################
```

现在测试`Record_Problem`脚本并查看它是否已就绪：

```
$ ./Record_Problem 
简要描述问题及其症状: 
运行 yum 安装软件并
收到‘not found’消息。 
问题记录如下: 
*************************** 1. row **************************** 
id_number: 1012111510 
report_date: 2010-12-11 
fixed_date: 0000-00-00 
prob_symptoms: 
运行 yum 安装软件并收到‘not found’消息。 
prob_solutions: 
$ 
```

运行得非常棒！你可以看到，使用这样的脚本记录问题比尝试使用单独的`mysql`命令进行插入要容易得多。

现在你已经有了一种记录问题的方法，你需要一种更新记录的方法。让我们开始创建`Update_Problem`脚本。

## 更新问题

跟踪问题的下一步是记录问题的解决方案。在本节创建的脚本将允许将这些信息添加到问题记录中。

### 必要的函数

使用`mysql`更新记录非常简单。一旦获取了所有必要的数据，只需使用`mysql UPDATE`命令即可：

```
UPDATE problem_logger SET 
      prob_solutions="$PROB_SOLUTIONS", 
      fixed_date=$FIXED_DATE 
      WHERE id_number=$ID_NUMBER;
```

这非常简单。然而，组合`Update_Problem`脚本比仅仅使用`UPDATE`函数要复杂一点。

### 创建脚本

与之前的脚本一样，我们希望让脚本用户尽可能方便。为了实现这一目标，需要添加几个功能。

`Problem_Trek`数据库的主键`id_number`用于标识要更新的记录。如果已知 ID 数字，可以将其作为参数传递给脚本（参见第 13 章）。你只需要检查该参数并将其分配给变量`ID_NUMBER`。如果没有作为参数传递 ID 数字，脚本将提示输入：

```bash
if [ $# -eq 0 ]  #检查是否传递了 id 数字
then          #如果未传递，则询问。
#
...
  echo
  echo “你想要更新的问题”
  echo -e “ID 数字是?: \c”
  read ANSWER
  ID_NUMBER=$ANSWER
else
  ID_NUMBER=$1
fi
```

但是，询问问题 ID 数字有一点不公平。没有多少人能在脑海中记住一个 10 位的数字来标识他们正在解决的特定问题。因此，你应该提供数据库中各种未解决问题的列表，让脚本用户更容易操作。

首先，检查是否存在未解决的记录。`fixed_date`和`prob_solutions`字段将为空。如果这两个字段中的任何一个，就需要更新记录；通过`SELECT`，你可以在`WHERE`语句中使用`OR`命令搜索这两个字段。实现此操作的代码如下：

```bash
RECORDS_EXIST='$MYSQL -Bse ‘SELECT id_number FROM problem_logger 
WHERE fixed_date="0000-00-00” OR prob_solutions=""’‘
```

注意命令的输出被赋值给变量`RECORDS_EXIST`。为了实现这一点，`mysql`命令必须使用`-Bse`选项。它们允许命令以批量（一次性）执行然后退出。如果`RECORDS_EXIST`变量包含数据，则存在需要更新的记录。使用以下操作将其显示在屏幕上：

```bash
#
  if [ “RECORDS_EXIST” != "" ]
  then
  echo
  echo “以下记录需要更新...”
  $MYSQL  <<EOF
    SELECT id_number, report_date, prob_symptoms 
          FROM problem_logger 
          fixed_date="0000-00-00” 
OR
EOF
```

这将提供一个不错的未完成记录列表。从列表中选择 ID 数字比尝试记住数字要容易得多。现在你可以组合出一个易于使用的整个脚本。它看起来应该类似于：

```bash
#!/bin/bash
#
# Update_Problem - 更新数据库中的记录
######################################
# 确定 mysql 位置并设置变量
#
MYSQL=‘which mysql‘“ Problem_Trek -u cbres”
#
#############################################
# 获取 ID 
#
if [ $# -eq 0 ]  #检查是否传递了 id 数字
then          #如果未传递，则询问。
#
# 检查是否存在记录。
  RECORDS_EXIST='$MYSQL -Bse ‘SELECT id_number FROM problem_logger 
WHERE fixed_date="0000-00-00” OR prob_solutions=""’‘
#
  if [ “RECORDS_EXIST” != "" ]
  then
  echo
  echo “以下记录需要更新...”
  $MYSQL  <<EOF
    SELECT id_number, report_date, prob_symptoms 
          FROM problem_logger 
          fixed_date="0000-00-00” 
OR
EOF
  fi
# 这提供了一个不错的未完成记录列表。选择 ID 数字。
  echo
  echo “你想要更新的问题”
  echo -e “ID 数字是?: \c”
  read ANSWER
  ID_NUMBER=$ANSWER
else
  ID_NUMBER=$1
fi
#############################
# 获取解决方案（即修复日期）
#
echo
echo -e “今天解决问题了吗？(y/n) \c”
read ANSWER
case $ANSWER in
y|Y|yes|Yes|yS|YEs|yES )
#
  FIXED_DATE=‘date +%Y%m%d‘
;;
*)
# 如果答案不是 yes，则询问日期
  echo
  echo -e “解决日期是？[YYYYMMDD] \c”
  read ANSWER
  FIXED_DATE=$ANSWER
;;
esac
#
##############################################
# 更新问题记录
#
#
echo
echo “问题记录更新如下:”
echo
$MYSQL <<EOF
UPDATE problem_logger SET 
      prob_solutions="$PROB_SOLUTIONS", 
      fixed_date=$FIXED_DATE 
      WHERE id_number=$ID_NUMBER;
SELECT * FROM problem_logger WHERE id_number=$ID_NUMBER\G
EOF
#
```

测试此脚本并查看它的性能如何。

```
$ ./Update_Problem 
以下记录需要更新... 
*************************** 1. row **************************** 
```

`id_number: 1012111624`

`report_date: 2010-12-11`

`prob_symptoms: 运行 yum 安装软件时获取‘not found’ 消息。`

你想要更新的问题 ID 号是多少？`1012111624`

今天解决问题了吗？(y/n) y 

简要描述问题解决方案：网络服务宕了。

执行了命令：`service network restart`

问题记录更新如下：

*************************** 1. row ****************************

`id_number: 1012111624`

`report_date: 2010-12-11`



`fixed_date: 2010-12-11`

`prob_symptoms: 运行 yum 安装软件时获取‘not found’ 消息。`

`prob_solutions: 网络服务宕机。`

执行了命令：`service network restart`

这运行非常好，而且使用非常简单。

## 补充

现在，为了让脚本用户操作更加方便，让我们修改 `Record_Problem` 脚本，在需要时调用 `Update_Problem`。有时候当你很忙时，“批量”记录问题会更方便。在原始 `Record_Problem` 脚本的最后面，你可以添加以下代码：

```bash
# 检查现在想要输入解决方案
#
echo
echo -e "你现在有解决方案了吗？(y/n) \c"
read ANSWER
#
case $ANSWER in
  y|Y|YES|yes|Yes|yEs|yeS|YEs|yES )
    ./$HOME/scripts/Update_Problem $ID_NUMBER
##
    ;;
  *)
    # 如果回答不是 yes，直接退出脚本
    ;;
esac
##############################################
```

现在让我们测试一下这个修改，看看它是否有效：

`$ ./Record_Problem`

简要描述问题及其症状：

将脚本从 Fedora 移动到 Ubuntu 后无法正常工作。

问题记录如下：

*************************** 1. row ****************************

`id_number: 1012111631`

`report_date: 2010-12-11`

`fixed_date: 0000-00-00`

`prob_symptoms: 将脚本从 Fedora 移动到 Ubuntu 后无法正常工作。`

`prob_solutions:`

你现在有解决方案了吗？(y/n) y

今天解决问题了吗？(y/n) y

简要描述问题解决方案：

在脚本顶部添加了 `#!/bin/bash`。这是必要的因为 Ubuntu 的默认 shell 是 `dash`。

问题记录更新如下：

*************************** 1. row ****************************

`id_number: 1012111631`

`report_date: 2010-12-11`

`fixed_date: 2010-12-11`

`prob_symptoms: 将脚本从 Fedora 移动到 Ubuntu 后无法正常工作。`

`prob_solutions: 在脚本顶部添加了 `#!/bin/bash`。这是必要的因为 Ubuntu 的默认 shell 是 `dash.`

这运行得非常完美。现在你已经非常方便地在 `Problem_Trek` 数据库中记录和更新记录了。

## 查找问题

拥有像 `Problem_Trek` 这样的数据库的真正之处在于回顾记录。查看过去的问题及其解决方案将让你能够快速解决重复问题并发现趋势。

### 必须的函数

为了在表中查找记录进行回顾，你可以再次使用 `SELECT` 命令。我们在本章之前已经使用过它，用于查看 `problem_logger` 表中新添加的记录等目的：

```sql
SELECT * FROM problem_logger WHERE id_number=$ID_NUMBER\G
```

对于 `Find_Problem` 脚本，需要对之前使用的 `SELECT` 命令进行微调。为了能够轻松找到旧问题，脚本会要求输入关键词。因此，如果你记得你有关于 `yum` 的问题，就会输入关键词“yum”。要在数据库中搜索包含该关键词的记录，请在脚本的 `SELECT` 语句中添加 `LIKE`。代码类似于：

```sql
mysql> SELECT * FROM problem_logger WHERE prob_symptoms LIKE 'yum'\G
```

`Empty (0 sec)`。 等，这没起作用！这是因为需要通配符。要在 `prob_symptoms` 字段中找到“yum”这个词，需要在两边都添加通配符。实际上，你是在告诉 `mysql` 寻找一个 `prob_symptoms` 字段包含单词“yum”的记录。使用的通配符是 `%`。因此，你的代码应该像：

```sql
mysql> SELECT * FROM problem_logger WHERE prob_symptoms LIKE '%yum%'\G
```

*************************** 1. row *****************

`id_number: 1012111624`

`report_date: 2010-12-11`

`fixed_date: 2010-12-11`

`prob_symptoms: 运行 yum 安装软件时获取‘not found’ 消息。`

`prob_solutions: 网络服务宕机。`

执行了命令：`service network restart`

1 row (0 sec)

你可能希望 `SELECT` 命令也能搜索 `prob_solutions` 字段以及 `prob_symptoms` 字段，这将允许更彻底的搜索：

```sql
mysql> SELECT * FROM problem_logger WHERE prob_symptoms LIKE '%yum%' OR prob_solutions LIKE '%yum%'\G
```

*************************** 1. row *****************

注意：如果你担心大小写敏感，不用担心。默认情况下，`mysql` 会忽略大小写，所以你可以输入关键词“yum”或“YUM”。为了对 `Problem_Trek` 数据库进行有效搜索，应该允许使用多个关键词。`LIKE` 命令无法兼顾多个。但是，你可以使用正则表达式 `REGEXP`。`REGEXP` 的优点之一是它会搜索整个字段——不需要通配符。要搜索多个关键词，在它们之间放置一个管道符 `|`。因此，代码现在看起来像：

```sql
mysql> SELECT * FROM problem_logger WHERE prob_symptoms REGEXP 'yum|dash'\G
```

*************************** 1. row ****************************

### 创建脚本

最好在调用脚本时允许关键词作为参数传递。然而，你不知道可能会传递多少个关键词。可能是五个，可能是一个，也可能没有！这实际上是一个很容易解决的困境。使用 `if` 测试检查是否传递了任何关键词。如果是，使用 `$@` 一次性获取所有关键词（见第 13 章）。如果没有传递关键词，脚本将需要它们。完成此任务的代码如下：

```bash
# 获取关键词(s)
#
if [ -n "$1" ]; # 检查是否传递了关键词
then             # 获取所有传递的关键词
  KEYWORDS=$@ # 获取所有参数作为独立的单词，相同的字符串
else # 关键词(s) 未传递。询问它们。
  echo
  echo "你想搜索哪些关键词？"
  echo -e "请用空格分隔单词: \c"
  read ANSWER
  KEYWORDS=$ANSWER
fi
```

一旦你有了关键词，下一步就是构建搜索语句。请记住，在每对关键词之间需要放置逻辑或 `or (|)`，以便 `REGEXP` 能够正确搜索它们。这可以通过 `sed` 轻松实现。`KEYWORDS` 数组变量中的每个空格都可以替换为 `|`。

```bash
KEYWORDS=`echo $KEYWORDS | sed 's/ /|/g'`
```

现在脚本看起来像这样：

```bash
#!/bin/bash
#
# Find_Problem - 使用关键字查找问题记录
######################################################
# 确定 sql 位置并设置变量
#
MYSQL=`which mysql`" Problem_Trek -u cbres"
#
#############################################
# 获取关键词(s)
#
if [ -n "$1" ]      # 检查是否传递了关键词
then               # 获取所有传递的关键词
#
      KEYWORDS=$@    # 获取所有参数作为独立的单词，保持字符串相同
#
else               # 未传递关键词。询问用户。
      echo
      echo "您想搜索哪些关键词?"
      echo -e "请用空格分隔单词: \c"
      read ANSWER
      KEYWORDS=$ANSWER
fi
#
##############################################
# 查找问题记录
#
echo
echo "使用关键词 $KEYWORDS 找到了以下内容:"
echo
#
KEYWORDS=`echo $KEYWORDS | sed 's/ /|/g'`
# 
$MYSQL <<EOF
SELECT * FROM problem_logger WHERE
    prob_symptoms REGEXP '($KEYWORDS)'
    OR
    prob_solutions REGEXP '($KEYWORDS)'
EOF
#
```

当然，下一步是测试你的新脚本。由于多关键词问题一直是关注的焦点，让我们先尝试在命令行中传递多个关键词：

```bash
$ ./Find_Problem yum dash
```

使用关键词 yum dash 找到了以下内容：yum dash 

*************************** 1. row ***************** 

`id_number: 1012111624` 

...

`prob_solutions: 在脚本顶部添加了 #!/bin/bash`。

这是必要的，因为 Ubuntu 的默认 shell 是 dash。

现在，让我们测试不带任何参数运行脚本。相反，我们将让脚本询问我们关键词。

```bash
$ ./Find_Problem
```

您想搜索哪些关键词? 

请用空格分隔单词: Ubuntu  

使用关键词 Ubuntu 找到了以下内容：Ubuntu 

*************************** 1. row *******************

`id_number: 1012111631` 

...

`prob_solutions: 在脚本顶部添加了 #!/bin/bash`。

这是必要的，因为 Ubuntu 的默认 shell 是 dash。

两次测试都运行得没有任何问题。现在，在 `Problem_Trek` 数据库中查找问题记录将变得简单。

有了这三个脚本——`Record_Problem`、`Update_Problem` 和 `Find_Problem`，你可以开始创建自己的问题数据库。我们希望你创建这些脚本花费的时间，将通过解决和避免问题所节省的时间倍倍给你。

## 总结

在本章中，我们回顾了一些可以放入 shell 脚本的更高级的功能。用户经常忽略 shell 脚本在特定系统管理任务中的有用之处，因为脚本需要高级功能才能正常运行。

本章演示了如何使用 shell 性能工具（如 `uptime`、`df` 和 `free`）来收集系统性能和资源使用的快照。使用 `sed` 和 `gawk` 从命令输出中提取了所需信息，包含了它们的一些更高级的能力。在根据信息创建报告后，通过电子邮件客户端发送给指定的用户账户。

下一节介绍了如何使用 `uptime` 和 `vmstat` 创建一个更高级的性能监控脚本。数据从这些工具中收集并存储。

## 附录 A

### bash 快速指南

在本附录中，我们提供了关于以下内容的简明指南：

*   shell 内部
*   内置命令
*   环境变量

#### 内置命令

shell 直接包含了许多常用命令。

| 命令 | 描述 |
| :--- | :--- |
| `alias` | 为指定的命令定义别名。 |
| `bg` | 在后台模式下恢复作业。 |
| `bind` | 将键盘序列绑定到 readline 函数。 |
| `break` | 退出 `for`、`while`、`select` 或 `until` 循环。 |
| `builtin` | 执行指定的 shell 内置命令。 |
| `cd` | 将当前目录更改指定的目录。 |
| `caller` | 返回任何活动子程序调用的上下文。 |
| `command` | 在不进行正常 shell 查找的情况下执行指定的命令。 |
| `compgen` | 为指定的单词生成可能的补全匹配。 |
| `complete` | 显示指定的单词将如何完成。 |
| `continue` | 恢复 `for`、`while`、`select` 或 `until` 循环的下一次迭代。 |
| `declare` | 声明变量或变量类型。 |
| `dirs` | 显示当前记忆的目录列表。 |
| `disown` | 从进程作业表中移除指定的作业。 |
| `echo` | 将指定的字符串显示到 STDOUT。 |
| `enable` | 启用或禁用指定的内建 shell 命令。 |
| `eval` | 将指定的参数合并为单个命令，然后执行该命令。 |
| `exec` | 用指定的命令替换 shell 进程。 |
| `exit` | 强制 shell 以指定的退出状态退出。 |
| `export` | 设置指定的变量，使其子 shell 进程可用。 |
| `fc` | 从历史列表中选择命令列表。 |
| `fg` | 在前台模式下恢复作业。 |
| `getopts` | 解析指定的各种参数。 |
| `hash` | Find 并记住指定的命令的完整路径。 |
| `help` | 显示帮助文件。 |
| `history` | 显示命令历史。 |
| `jobs` | 列出活动作业。 |
| `kill` | 向指定的进程 ID (PID) 发送系统信号。 |
| `let` | 求值数学表达式中的每个参数。 |
| `local` | 在函数中创建局部范围的变量。 |
| `logout` | 退出登录 shell。 |
| `popd` | 从目录栈中移除项。 |
| `printf` | 使用格式化字符串显示文本。 |
| `pushd` | 将目录添加到目录栈。 |
| `pwd` | 显示当前工作目录的路径。 |
| `read` | 从 STDIN 读取一行数据并将其赋值给变量。 |
| `readonly` | 从 STDIN 读取一行数据并赋值给不可更改的变量。 |
| `return` | 强制函数退出，并返回一个可供调用脚本获取的值。 |
| `set` | 设置并显示环境变量和 shell 属性。 |
| `shift` | 将位置参数向下移动一位。 |
| `shopt` | 切换控制可选 shell 行为的变量值。 |
| `suspend` | 挂起 shell 的执行，直到收到 `SIGCONT` 信号。 |
| `test` | 根据指定的条件返回 0 或 1 的退出状态。 |
| `times` | 显示累积的用户和系统时间。 |
| `trap` | 如果收到指定的系统信号，则执行指定的命令。 |
| `type` | 显示指定的单词用作命令时将如何被解释。 |
| `ulimit` | 为系统用户设置指定资源的限制。 |
| `umask` | 设置新创建的文件和目录的默认权限。 |
| `unalias` | Remove 指定的别名。 |
| `unset` | Remove 指定的环境变量或 shell 属性。 |
| `wait` | 等待指定的进程完成，并返回退出状态。 |

内置命令比外部命令具有更高的性能，但添加到 shell 中的内置命令越多，它消耗的内存就越多（其中包含许多你可能永远用不到命令）。`bash` shell 还包含为 shell 提供扩展功能的外部命令。这些内容将在 bash 命令部分进行讨论。

## bash 命令

除了内置命令外，`bash` shell 还利用外部命令来允许你在文件系统中移动，并操作文件和目录。[表 A.2] 显示了在 `bash` shell 中工作时可能想要使用的常用外部命令。

### 表 A.2 bash Shell 外部命令

| 命令 | 描述 |
| :--- | :--- |
| `bzip2` | 使用 Burrows-Wheeler 块排序文本压缩算法和霍曼编码进行压缩。 |
| `cat` | 列出指定文件的内容。 |
| `chage` | 更改指定用户账户的密码过期日期。 |
| `chfn` | 更改指定用户账户的注释信息。 |
| `chgrp` | 更改指定文件或目录的默认组。 |
| `chmod` | 更改指定文件或目录的安全权限。 |
| `chown` | 更改指定文件或目录的默认所有者。 |
| `chpasswd` | 读取用户名密码文件并更新密码。 |
| `chsh` | 更改指定用户的默认 shell。 |
| `compress` |  Unix 文件压缩工具。 |
| `cp` | 将指定文件复制到另一个位置。 |
| `date` | 以各种格式显示日期。 |
| `df` | 显示所有挂载设备的当前磁盘空间统计信息。 |
| `du` | 显示指定路径的磁盘使用统计信息。 |
| `file` | 查看指定文件的类型。 |
| `find` | 对文件进行递归搜索。 |
| `finger` | 显示 Linux 系统或远程系统中用户账户的信息。 |



| 命令 | 描述 |
| :--- | :--- |
| `free` | 检查系统的可用和已用内存。 |
| `grep` | 在文件中搜索指定的文本字符串。 |
| `groupadd` | 创建新的系统组。 |
| `groupmod` | 修改现有的系统组。 |
| `gzip` | GNU 项目使用 Lempel-Ziv 压缩的工具。 |
| `head` | 显示指定文件内容的开头部分。 |
| `kill` | 向运行中的进程发送信号。 |
| `less` | 查看文件内容。 |
| `link` | 创建链接。 |
| `ls` | 列出目录。 |
| `mkdir` | 创建目录。 |
| `more` | 查看文件内容。 |
| `mount` | 挂载设备。 |
| `mv` | 移动或重命名。 |
| `nice` | 更改命令的优先级。 |
| `passwd` | 更改密码。 |
| `ps` | 显示活动进程。 |
| `pwd` | 显示当前目录。 |
| `renice` | 更改进程的优先级。 |
| `rm` | 删除文件。 |
| `rmdir` | 删除目录。 |
| `sort` | 组织数据。 |
| `stat` | 查看文件统计信息。 |
| `sudo` | 以 `root` 用户运行。 |
| `tail` | 显示文件的尾部分。 |
| `tar` | 归档数据。 |
| `touch` | 创建空文件。 |
| `top` | 显示系统使用情况。 |
| `umount` | 卸载设备。 |
| `uptime` | 显示系统运行的时间。 |
| `useradd` | 创建新用户。 |
| `userdel` | 删除用户。 |
| `usermod` | 修改用户。 |
| `vmstat` | 生成详细报告。 |
| `which` | 找到可执行文件的位置。 |
| `zip` | 压缩文件。 |

你可以使用这些命令完成所需的任何任务。

## 环境变量

`bash` shell 还利用许多环境变量。虽然环境变量不是命令，但它们经常影响命令的运行，因此了解环境变量非常重要。[表 A.3] 显示了 `bash` shell 中可用的默认环境变量。

### 表 A.3：`bash` Shell 环境变量

| 变量 | 描述 |
| :--- | :--- |
| `$*` | 包含所有命令行参数作为一个单一文本值。 |
| `$@` | 包含所有命令行参数作为独立的文本值。 |
| `$#` | 命令行参数的数量。 |
| `$?` | 最近一次使用的进程的退出状态。 |
| `$-` | 命令行选项标记。 |
| `$$` | 当前 shell 的进程 ID (PID)。 |
| `$!` | 最近执行的后台进程的 PID。 |
| `$0` | 从命令行中输入的命令名称。 |
| `$_` | shell 的绝对路径。 |
| `BASH` | 用于调用 shell 的完整文件名。 |
| `BASH_ARGC` | 当前子程序中的参数个数。 |
| `BASH_ARGV` | 包含所有已指定的命令行参数的数组。 |
| `BASH_COMMAND` | 当前正在执行的命令名称。 |
| `BASH_ENV` | 设置时，每个 `bash` 脚本在运行前都会尝试执行由此变量定义的启动文件。 |
| `BASH_EXECUTION_STRING` | 用于 `-c` 命令行选项的命令。 |
| `BASH_LINENO` | 包含脚本中每个命令行号的数组。 |
| `BASH_REMATCH` | 包含匹配指定正则表达式的文本元素的数组。 |
| `BASH_SOURCE` | 包含 shell 中声明函数的源文件名的数组。 |
| `BASH_SUBSHELL` | 当前 shell 派生的子 shell 数量。 |
| `BASH_VERSION` | 当前 `bash` shell 实例的版本号。 |
| `BASH_VERSINFO` | 一个变量数组，包含当前 `bash` shell 实例的各个主版本和次版本号。 |
| `COLUMNS` | 包含当前 `bash` shell 实例所使用的终端宽度。 |
| `COMP_CWORD` | 变量 `COMP_WORDS` 的索引，包含当前光标位置。 |
| `COMP_LINE` | 当前的命令行。 |
| `COMP_POINT` | 当前光标位置相对于当前命令起始位置的索引。 |
| `COM_WORDBREAKS` | 执行单词补全时用单词分隔符的字符集。 |
| `COMP_WORDS` | 一个变量数组，包含当前命令行上的每一个单词。 |
| `COMPREPLY` | 一个变量数组，包含由 shell 函数生成的可能的补全代码。 |
| `DIRSTACK` | 一个变量数组，包含目录栈的当前内容。 |
| `EUID` | 当前用户的有效用户 ID。 |
| `FCEDIT` | `fc` 命令使用的默认编辑器。 |
| `FIGNORE` | 执行文件名补全时要忽略的后缀列表，用冒号分隔。 |
| `FUNCNAME` | 当前执行的 shell 函数名。 |
| `GLOBIGNORE` | 定义文件名扩展时要忽略的文件名集的模式列表，用冒号分隔。 |
| `GROUPS` | 一个变量数组，包含当前用户所属的组列表。 |
| `histchars` | 控制历史扩展的最多三个字符。 |
| `HISTCMD` | 当前命令的历史行号。 |
| `HISTCONTROL` | 控制哪些命令会被输入到 shell 历史列表中。 |
| `HISTFILE` | 用于保存 shell 历史列表的文件名（默认为 `.bash_history`）。 |
| `HISTFILESIZE` | 历史文件中保存的最大行数。 |
| `HISTIGNORE` | 用于决定哪些命令被忽略在历史文件中的模式列表，用冒号分隔。 |
| `HISTSIZE` | 历史文件中存储的最大命令数。 |
| `HOSTFILE` | 包含 shell 需要补全主机名时应该读取的文件名。 |
| `HOSTNAME` | 当前的主机名。 |
| `HOSTTYPE` | 描述运行 `bash` shell 机器的字符串。 |
| `IGNOREEOF` | shell 之前必须接收的连续 EOF 字符数。如果此值不存在，默认值为 1。 |
| `INPUTRC` | readline 初始化文件名（默认为 `.inputrc`）。 |
| `LANG` | shell 的本地区域类别。 |
| `LC_ALL` | 覆盖 `LANG` 变量，定义本地区域类别。 |
| `LC_COLLATE` | 设置排序字符串值时使用的排序规则。 |
| `LC_CTYPE` | 决定文件名扩展和模式匹配中使用的字符解释。 |
| `LC_MESSAGES` | 决定解释以美元符号开头的双引号字符串时使用的本地区域设置。 |
| `LC_NUMERIC` | 决定格式化数字时使用的本地区域设置。 |
| `LINENO` | 当前执行脚本中的行号。 |
| `LINES` | 定义终端可用行数。 |
| `MACHTYPE` | 以 `cpu`-`company`-`system` 格式定义系统类型的字符串。 |
| `MAILCHECK` | shell 检查新邮件的频率（秒为单位，默认为 60）。 |
| `OLDPWD` | shell 中使用的上一个工作目录。 |
| `OPTERR` | 如果设置为 1，`bash` shell 会显示 `getopts` 命令生成的错误。 |
| `OSTYPE` | 定义 shell 运行操作系统的字符串。 |
| `PIPESTATUS` | 一个变量数组，包含前台进程的退出状态值列表。 |
| `POSIXLY_CORRECT` | 如果设置，`bash` 以 POSIX 模式启动。 |
| `PPID` | `bash` shell 父进程的进程 ID (PID)。 |
| `PROMPT_COMMAND` | 如果设置，在显示主提示符之前执行的命令。 |
| `PS1` | 主命令行提示符字符串。 |
| `PS2` | 次级命令行提示符字符串。 |
| `PS3` | `select` 命令使用的提示符。 |
| `PS4` | 使用 `bash` `-x` 参数时，在命令行回显之前显示的提示符。 |
| `PWD` | 当前工作目录。 |
| `RANDOM` | 返回 0 到 32767 之间的随机数。给此变量赋值会为随机数生成器种子。 |
| `REPLY` | `read` 命令的默认变量。 |
| `SECONDS` | 自 shell 启动以来的秒数。赋值会将计时器重置为该值。 |
| `SHELLOPTS` | 已启 `bash` shell 选项列表，用冒号分隔。 |
| `SHLVL` | 表示 shell 层级，每启动一个新的 `bash` shell 就会加 1。 |
| `TIMEFORMAT` | 指定 shell 如何显示时间的格式。 |
| `TMOUT` | shell 等待的时间（秒为单位）。 |
| `UID` | 当前用户的有效用户 ID。 |

# 附录 B：`sed` 和 `gawk` 快速指南

## `sed` 编辑器

`sed` 编辑器可以处理数据。它从输入读取一行数据，并将该数据与提供的编辑器命令进行匹配，更改流中的数据然后输出新数据。

### 启动 `sed` 编辑器

使用 `sed` 的格式为：

`sed options script`

`options` 参数允许你自定义 `sed` 命令的行为，包括表 B.1 所示的选项。

### 表 B.1：`sed` 命令选项

| 选项 | 描述 |
| :--- | :--- |
| `-e` `script` | 在处理输入时，将 `script` 中指定的命令添加到命令列表中。 |
| `-f` `file` | 在处理输入时，将文件 `file` 中指定的命令添加到命令列表中。 |
| `-n` | 不为每个命令产生输出，而是等待 `print` 命令。 |

`script` 参数指定了应用于数据流的单个命令。如果需要多个命令，你必须使用 `-e` 选项在命令行中指定它们，或使用 `-f` 选项在单独的文件中指定它们。

## `sed` 命令

`sed` 编辑器脚本包含了 `sed` 对输入中每行数据进行处理的命令。本节描述了你可能想要使用的一些常用 `sed` 命令。

### 替换

`s` 命令替换输入流中的文本。`s` 命令的格式为：

`s/pattern/replacement/flags`

`pattern` 是要替换的文本，`replacement` 是 `sed` 将插入到该位置的新文本。

`flags` 参数控制替换的发生方式。共有四种类型的替换标志可用：

- 一个数字，表示要替换的模式出现次数。
- `g`：表示替换文本的所有出现处。
- `p`：表示打印原始行的内容。
- `w` `file`：表示将替换结果写入文件。

在第一种替换中，你可以指定 `sed` 编辑器应该替换匹配模式的几次出现处。例如，你使用 `2` 来仅替换模式的第二次出现处。

### 定址（Addressing）

默认情况下，你在 `sed` 编辑器中使用的命令适用于文本数据的所有行。如果你只想将命令应用于特定的某行或一组行，则必须使用行定址。

`sed` 编辑器中有两种行定址的格式：

- 数字行范围
- 过滤出某行的文本模式

这两种形式在指定地址时使用相同的格式：

`[address]command`

使用数字行定址时，你通过行在文本流中的位置来引用行。`sed` 编辑器将文本流中的第一行分配为行号一，并对每个新行顺序递增。

```bash
$ sed ‘2,3s/dog/cat/’ data1
```

另一种限制命令应用行的方法稍微复杂一些。`sed` 编辑器允许你指定一个文本模式，并用它为命令过滤行。其格式为：

`/pattern/command`

你必须用正斜杠将你指定的 `pattern` 括起来。`sed` 编辑器仅对包含你指定的文本模式的行应用命令。

```bash
$ sed ‘/rich/s/bash/csh/’ /etc/passwd
```

此过滤器会找到包含文本 `rich` 的行，并将文本 `bash` 替换为 `csh`。

你还可以将多个命令组合到特定的地址中：

```bash
address {
command1
command2
command3
}
```

`sed` 编辑器将你指定的每个命令仅应用于匹配指定地址的行。`sed` 编辑器将处理地址行上列出的每个命令：

```bash
$ sed ‘2{
> s/fox/elephant/
> s/dog/cat/
> }’ data1
```

`sed` 编辑器将每个替换操作都应用于数据文件中的第二行。

### 删除行（Deleting Lines）

删除命令 `d` 的作用几乎如其名。它会删除任何匹配所提供地址方案的文本行。使用删除命令时要小心，因为如果你忘记包含地址方案，流中的所有行都将被删除：

```bash
$ sed ‘d’ data1
```

删除命令在与指定地址结合使用时显然最有用。这允许你从数据流中删除特定的文本行，可以通过行号：

```bash
$ sed ‘3d’ data6
```

或者通过一个特定的行范围：

```bash
$ sed ‘2,3d’ data6
```

`sed` 编辑器的模式匹配功能也适用于删除命令：

```bash
$ sed ‘/number 1/d’ data6
```

只有匹配指定文本的行会被从流中删除。

### 插入和追加文本（Inserting and Appending Text）

正如你预期的，像任何其他编辑器一样，`sed` 编辑器允许你向数据流插入和追加文本行。这两个操作之间的区别可能会引起混惑：

- 插入命令（`i`）在指定行之前添加新行。
- 追加命令（`a`）在指定行之后添加新行。

这两个命令的格式可能会引起混惑：你不能在单行命令上使用这些命令。你必须在单独的一行中指定要插入或追加的行。此操作的格式为：

```bash
sed ‘[address]command\
new line’
```

`new line` 中的文本将出现在 `sed` 编辑器输出的指定位置。记住，当你使用插入命令时，文本出现在数据流文本之前：

```bash
$ echo “testing” | sed ‘i\
> This is a test’
This is a test
testing
$
```

当你使用追加命令时，文本出现在数据流文本之后：

```bash
$ echo “testing” | sed ‘a\
> This is a test’
testing
This is a test
$
```

这允许你在普通文本的末尾插入文本。

### 修改行（Changing Lines）

更改命令允许你更改数据流中整行文本的内容。它的工作方式与插入和追加命令相同，即你必须将新行与 `sed` 命令的其他部分分开单独指定：

```bash
$ sed ‘3c\
> This is a changed line of text.’ data6
```

反斜杠字符用于指示脚本中的新行数据。

### 转换命令（Transform Command）

转换命令（`y`）是 `sed` 编辑器中唯一对单个字符操作的命令。转换命令使用以下格式：

`[address]y/inchars/outchars/`

转换命令对 `inchars` 和 `outchars` 的值进行一对一的映射。`inchars` 中的第一个字符转换为 `outchars` 中的第一个字符。`inchars` 中的第二个字符转换为 `outchars` 中的第二个字符。这种映射持续到指定字符的整个长度。如果 `inchars` 和 `outchars` 长度不同，`sed` 编辑器将产生错误消息。

### 打印行（Printing Lines）

与替换命令中的 `p` 标志类似，`p` 命令在 `sed` 编辑器输出中打印一行。打印命令最常用的用途是打印包含来自文本模式匹配文本的行：

```bash
$ sed -n ‘number 3/p’ data6
This is line number 3.
$
```

`print` 命令允许你从输入流中过滤出特定的数据行。

### 写入文件（Writing to a File）

`w` 命令用于将行写入。`w` 命令的格式为：

`[address]w filename`

`filename` 可以指定为相对路径或绝对路径，但无论哪种，`sed` 编辑器必须对该文件具有写权限。

### 从文件读取（Reading from a File）

你已经看到如何向数据流插入和追加文本。读取命令（`r`）允许你插入包含在单独文件中的数据。读取命令的格式：

`[address]r filename`

`filename` 指定绝对或相对路径。你不能对读取命令使用地址范围。你只能指定单个行号或文本模式。`sed` 编辑器会在地址之后插入来自文件的文本。

```bash
$ sed ‘1,2 test’ data6
```

输出文件 `test` 仅包含来自输入流的最前两行。

## `gawk` 程序

`gawk` 程序是 Unix 中原始 `awk` 程序的 GNU 版本。`awk` 程序通过提供编程语言而非仅是编辑器命令，比 `sed` 编辑器更进一步。本节描述了 `gawk` 程序的基础，作为其功能的快速参考。

### 命令格式

`gawk` 程序的基本格式如下：

`gawk options program file`

### `gawk` 选项

| 选项 | 描述 |
| :--- | :--- |
| `-F` `fs` | 指定文件分隔符用于划分行中的数据字段。 |
| `-f` `file` | 指定用于读取程序的文件名。 |
| `-v` `var=value` | 在 `gawk` 程序中定义变量和默认值。 |
| `-mf` `N` | 指定数据文件中处理的最大字段数。 |
| `-mr` `N` | 指定数据文件中最大记录的大小。 |



| `-W` `keyword` | 为 `gawk` 指定兼容模式或警告级别。使用 `help` 选项列出所有可用关键字。 |

命令行选项提供了一种自定义 `gawk` 程序功能的简便方法。

# 使用 `gawk`

你可以直接从命令行使用 `gawk`，也可以在你的 shell 脚本中使用。本节演示了如何使用 `gawk` 程序以及如何为 `gawk` 输入供其处理的脚本。

## 从命令行读取程序脚本

一个 `gawk` 程序脚本由一对左括号和右括号定义。你必须将脚本命令放置在两个括号之间。由于 `gawk` 命令行假设脚本是一个单一文本字符串，因此你还必须用单引号将你的脚本括起来。这里有一个在命令行上指定的简单 `gawk` 程序脚本的示例：

```bash
$ gawk '{print $1}'
```

该脚本将显示输入流中每行的第一个数据字段。

## 在程序脚本中使用多个命令

如果一种编程语言只能执行一个命令，那么这种语言将变得大大没用处。`gawk` 编程语言允许你将多个命令组合成一个正常的程序。若要在在命令行指定的程序脚本中使用多个命令，只需在每个命令之间放置一个分号即可：

```bash
$ echo "My name is Rich" | gawk '{$4="Dave"; print $0}'
My name is Dave
$
```

该脚本执行了两个命令：首先，它将第四个数据字段替换为不同的值；然后它显示流中的整条数据行。

## 从文件读取程序

与 `sed` 编辑器一样，`gawk` 编辑器允许你将程序存储在文件中，并在命令行中引用它们：

```bash
$ cat script2
{ print $5 ' userid is ' $1 }
$ gawk -F: -f script2 /etc/passwd
```

`gawk` 程序会在输入流数据上处理文件中指定的所有命令。

## 在处理数据之前运行脚本

`gawk` 程序还允许你指定程序脚本运行的时机。默认情况下，`gawk` 从输入中读取一行文本，然后对该行文本中的数据执行程序脚本。有时，你可能需要在处理数据之前运行脚本，例如为报告创建一个表头部分。要做到这一点，你可以使用 `BEGIN` 关键字。这会强制 `gawk` 在读取数据之前执行 `BEGIN` 关键字之后指定的程序脚本：

```bash
$ gawk 'BEGIN {print "This is a test report"}'
This is a test report
$
```

你可以在 `BEGIN` 部分中放置任何类型的 `gawk` 命令，例如为变量分配默认值的命令。

## 在处理数据后运行脚本

与 `BEGIN` 关键字类似，`END` 关键字允许你指定一个 `gawk` 在读取数据后执行的程序脚本：

```bash
$ gawk 'BEGIN {print "Hello World!"} {print $0} END {print "byebye"}'
Hello World!
This is a test
This is a test
This is another test.
This is another test.
byebye
$
```

`gawk` 程序首先执行 `BEGIN` 部分的代码，然后处理输入流中的任何数据，最后执行 `END` 部分的代码。

# `gawk` 变量

`gawk` 程序不仅仅是一个编辑器；它是一个完整的编程环境。因此，有许多与 `gawk` 相关的命令和功能。本节展示了在使用 `gawk` 进行编程时需要了解的主要功能。

## 内置变量

`gawk` 程序使用内置变量来引用程序数据中的特定功能。本节描述了你可以在 `gawk` 程序中使用的 `gawk` 内置变量，并演示了如何使用它们。

`gawk` 程序将数据定义为记录（records）和数据字段（fields）。记录是一行数据（默认以换行符分隔），数据字段是行内一个独立的数据元素（默认以空白字符，如空格或制表符分隔）。

`gawk` 程序使用数据字段变量来引用每个记录中的数据元素。[表 B.3] 描述了这些变量。

### 表 B.3

| 变量 | 描述 |
| :--- | :--- |
| `$0` | 整个记录 |
| `$1` | 第一个字段 |
| `$2` | 第二个字段 |
| `$n` | 第 n 个字段 |
| `FIELDWIDTHS` | 定义字段宽度 |
| `FS` | 输入字段符 |
| `RS` | 输入记录符 |
| `OFS` | 输出字段符 |
| `ORS` | 输出记录符 |

除了字段和记录分隔符外，`gawk` 还提供了其他内置变量来帮助你了解情况。表 B.4 显示了更多内置变量。

### 表 B.4 `gawk` 内置变量

| 变量 | 描述 |
| :--- | :--- |
| `ARGC` | 命令行参数的数量 |
| `ARGIND` | 当前参数的索引 |
| `ARGV` | 命令行参数数组 |
| `CONVFMT` | 数字转换格式 |
| `ENVIRON` | 环境关联数组 |
| `ERRNO` | 发生错误时的系统错误 |
| `FILENAME` | 输入的文件名 |
| `FNR` | 当前记录行号 |
| `IGNORECASE` | 设置为非零值时忽略大小写 |
| `NF` | 字段总数 |
| `NR` | 处理的记录数 |
| `OFMT` | 数字输出格式 |
| `RLENGTH` | 匹配子串的长度 |
| `RSTART` | 匹配子串的起始索引 |

你可以在程序脚本的任何地方使用这些内置变量，包括 `BEGIN` 和 `END` 部分。

## 在脚本中变量赋值

在 `gawk` 程序中为变量赋值类似于在 shell 脚本中——使用赋值语句：

```bash
$ gawk '
> BEGIN{
> testing="This is a test"
> print testing
> }
This is a test
$
```

一旦为变量赋值，你就可以在 `gawk` 脚本的任何地方使用它。

## 在命令行中变量赋值

你还可以使用 `gawk` 命令行为变量赋值。这允许你在代码之外设置值，从而动态更改值。这里有一个使用命令行变量显示文件中特定数据字段的示例：

```bash
$ cat script1
BEGIN{FS=","}
{print $n}
$ gawk -f script1 n=2 data1
$ gawk -f script1 n=3 data1
```

这一特性是处理 shell 脚本数据的极佳方法。

# `gawk` 程序功能

`gawk` 程序的某些功能对于处理数据非常方便，允许你创建可以解析任何类型文本文件的 `gawk` 脚本，包括日志文件。

## 正则表达式

你可以使用基础正则表达式 (BRE) 或扩展正则表达式 (ERE) 来过滤数据流中哪些行适用于程序脚本。

在使用正则表达式时，正则表达式必须出现在它所控制的程序脚本的左括号之前：

```bash
$ gawk 'BEGIN{FS=","} /test/{print $1}' data1
This is a test
$
```

## 匹配运算符

匹配运算符允许你将正则表达式限制到记录中的特定数据字段。匹配运算符是波浪号（`~`）。你指定匹配运算符、数据字段变量以及要匹配的正则表达式：

```text
$1 ~ /^data/
```

该表达式过滤第一个数据字段以文本 data 开头的记录。

除了正则表达式外，你还可以在匹配模式中使用数学表达式。此功能在匹配数据字段中的数值时非常有用。例如，如果你想显示所有属于 root 用户组（组 ID 0）的系统用户，可以使用此脚本：

```bash
gawk -F: ‘$4 == 0{print $1} /etc/passwd
```

此脚本会显示第四个数据字段包含 0 的所有行的第一个数据字段。

# 结构化命令

`gawk` 程序支持以下结构化命令：

## `if-then-else` 语句

```bash
if (condition) statement1; else statement2
```

## `while` 语句

```bash
while (condition)
{
  statements
}
```

## `do-while` 语句

```bash
do {
  statements
} while (condition)
```

## `for` 语句

```bash
for(variableassignment; condition; iteration process)
```

这为 `gawk` 脚本程序员提供了丰富的编程机会。你可以编写出功能足以媲拟任何高级语言程序的 `gawk` 程序。

# 索引

## 符号与数字

- `:`（冒号）
- `/etc/passwd`
- `IFS`
- `.`（点）
- `BRE`
- 正则表达式
- 相对文件路径
- `..`（双点），相对文件路径
- `;`（分号）
- `do`
- 函数
- `IFS`
- `mysql`
- `sed`
- shell 脚本
- `&`（安符）
- 后模式
- 双括号符号
- `sed`
- `STDERR`
- `&&`（双安符）
- 双括号符号
- `PID`
- `*`（星号）
- `BRE`
- `case`
- 可执行文件
- 过滤字符串
- `ls`
- 正则表达式
- `**`（双星号），双括号符号
- `\`（反斜杠）
- `for`
- bash 提示符字符
- `list`
- 正则表达式
- `sed`
- `sem`
- shell 脚本
- `substitution`
- `` ` ``（反引号）
- `bc`
- shell 脚本
- `ˆ`（脱字符符号）
- 锚点字符
- 正则表达式
- `sed`
- `{}`（花括号），ERE
- `$`（美元符号）
- bash shell
- 环境变量
- `sed`
- 用户变量
- `$$`（双美元符号）
- bash shell
- dash shell
- `=`（等号）
- 磁盘空间监控
- 环境变量
- 文件权限
- `print`
- 用户变量
- `!`（感叹号）
- 双括号符号
- `sed`
- `substitution`
- `>`（大于符号）
- BSD 风格参数
- 输出重定向
- `sed`
- `>>`（双大于符号）
- 输出重定向
- 统计报告
- `#`（井号）
- `<`（小于符号）
- 输入重定向
- `sed`
- `<<`（双小于符号）
- 双括号符号
- 内联输入重定向
- `-`（减号/连字符号）
- `BRE`
- 文件权限
- 格式指定符
- `--`（双减号/连字符号）
- `Mutt`
- `shift`
- `-?`（减号/连字符号问号），`psql`
- `---`（三减号/连字符号），权限代码
- `|`（管道符号）
- 双括号符号
- `ERE`
- 正则表达式
- `sort`
- `||`（双管道符号），双括号符号
- `+`（加号）
- BSD 风格参数
- `ERE`
- 文件权限
- 正则表达式
- `?`（问号）
- `ERE`
- 过滤字符串
- `mysql`
- `read`
- 正则表达式
- 用户账户
- `“”`（双引号）
- `for`
- `IFS`
- 位置参数
- `''`（单引号）
- shell 脚本
- `substitution`
- `[]`（中括号），后模式
- bash shell
- `gawk`
- 数学
- 函数
- `~`（波浪号）
- 双括号符号
- `gawk`
- 数值
- `+%y%m%d`（日期格式）
- `()`（括号）
- 退出状态
- 函数
- 正则表达式
- `substitution`
- `(())`（双括号）
- bash shell
- `if-then`
- `zsh`
- `\!`
- bash 提示符字符
- `mysql`
- `\#`
- bash 提示符字符
- `\$`，bash 提示符字符
- `\?`
- `mysql`
- `psql`
- `\@`，bash 提示符字符
- `\[`，bash 提示符字符
- `\]`，bash 提示符字符
- `$!`
- bash shell
- dash shell
- `$#`
- bash shell
- 位置参数
- dash shell
- `$*`
- bash shell
- 位置参数
- dash shell
- `$-`，dash shell
- `$?`
- bash shell
- dash shell
- 退出状态
- `mysql`
- `$@`
- bash shell
- 位置参数
- dash shell
- `$_`，bash shell
- `$>`，`STDERR`
- `$0`
- bash shell
- dash shell
- `gawk`
- `zsh`
- `1`
- 退出状态
- 信号
- `$1`，`gawk`
- `2`
- 退出状态
- 信号
- `$2`，`gawk`
- `3`，信号
- `9`，信号
- `15`，信号
- `17`，信号
- `18`，信号
- `19`，信号
- `126`，退出状态
- `127`，退出状态
- `128`，退出状态
- `128+x`，退出状态
- `130`，退出状态
- `132`，退出状态

## 内置函数与变量

### 内置函数，`gawk`

### 内置变量，`gawk`

- `bunzip2`
- `-buried_news`
- `bye`
- `bzcat`
- `bzip2`
- `bzip2recover`

## C

- `C`
- `sendmail`
- `c`
- `aptitude`
- 字符设备权限
- `fdisk`
- 格式指定符
- `optstring`
- `-C`
- `fsck`
- `lvcreate`
- `mysql`
- `sort`
- `-c`
- dash shell
- `exit`
- `lvcreate`
- Mailx
- Mutt
- 选项
- `psql`
- `sort`
- `tar`
- TCP 模块
- `C-@`
- `\C`
- `\c`
- `-c bytes`
- `-C cmdlist`
- `-c comment`
- `-C dir`

### C 语言

- `-c string`
- `C-a`
- `cache`
- `-cache`
- `calendar`
- `--calendar`
- `caller`
- 调用函数
- `--cancel-label`
- 大写
- `case`
- 命令行参数
- `getopts`
- 菜单
- 用户账户
- `zsh`
- `-case`
- 大小写敏感性
- `cat`
- bash shell
- `inputbox`
- `read`
- `zsh`
- `C-b`
- `c_bases`
- `cd`
- bash shell
- dash shell
- `zsh`
- `CDPATH`
- `C-e`
- `-center`
- `C-f`
- `-cfg`
- `chage`
- 修改
- 更改大小写
- 更改配置文件
- `char`
- 字符编码
- 字符
- 锚点
- ANSI
- 类
- 设备
- 文件
- 权限
- 转义
- 范围
- 特殊
- `charset`
- `chdir`
- `--check`
- `CHECK_DIRECTORIES`
- `checklist`
- `--checklist`
- `check=none`
- `--check=quiet`
- `chfn`
- `chgrp`
- `-child`
- `chmod`
- bash shell
- 权限
- `chown`
- `chpasswd`
- `chsh`
- `--chunksize`
- `C-k`
- `--classify`
- 清理缩进
- `cleanup`
- `clear`
- `--clear`
- 清除回滚并重置
- CLI。参见命令行接口
- 客户端/服务器范式
- `cm`
- `CMD`
- `-cmd`
- `-cmd_log`
- `-cmd_script`
- `C-n`
- 颜色
- 颜色方案
- `--colors`
- `--color=when`
- `--cols` `n`
- `cols#80`
- `--column`
- `COLUMNS`
- `--columns` `n`
- COM 端口
- `COMMAND`
- `command`
- `--command`
- 命令。另请参见特定命令
- 别名
- bash shell
- C 语言
- 组，`sed`
- 值
- 命令行接口 (CLI)
- bash shell
- 函数
- `gawk`
- MySQL
- PostgreSQL
- 变量
- 命令行参数
- bash shell
- `case`
- `chage`
- dash shell
- GNOME
- Konsole
- `ls`
- `lynx`
- 选项
- `tail`
- `test`
- `useradd`
- `while`
- xterm
- `zsh`
- `commands`
- `COMP_CWORD`
- `compgen`
- `COMP_KEY`
- `compl()`
- `complete`
- `COMP_LINE`
- `COMP_POINT`
- `COMPREPLY`
- 压缩
- `COMP_TYPE`
- `COMP_WORDBREAKS`
- `COMP_WORDS`
- `COM_WORDBREAKS`
- `--concatenate`
- 条件
- `CONFIG_FILE`
- `configure`
- 配置编辑器
- `configure sysstat`
- 连接



`_connect_timeout`

`CONT`

`--context`

继续

`--continuous`

控制代码

> 终端仿真

> terminfo 数据库

`CONVFMT`

`_cookie_file`

`_cookies`

`_cookie_save`

复制

复制并粘贴

> `emacs`

> `vim`

另存为 HTML

`-core`

核心发行版

`corutils`

`cos()`

计数参数

`cp`

`C-p`

`%CPU`

cr

`C-r`

`-crawl`

`--create`

`--create-rc`

`cron`

> `Delete_User`

> 统计报告

`crontab`

`--cr-wrap`

cs

`C-s`

`csh_junkie_history`

`csh_junkie_loops`

`csh_junkie_quotes`

`csh_nullcmd`

`C-Spacebar`

csr

`cub`

`cub1`

`cud`

`cud1`

`cuf`

`cuf1`

`--cumulative`

cup

cURL

`curl`

当前行

`-curses_pads`

剪

`cuu`

`cuul`

`C-v`

`C-x 2`

`C-x 3`

`C-x b`

`C-x C-b`

`C-x C-c`

`C-x C-f`

`C-x C-s`

`C-x o`

`C-y`

`C-z`

D

`D`, `sendmail`

`d`

> 目录权限

> `fdisk`

> 格式指定符

> `optstring`

> `sed`

`D$`

`-D`

> Mutt

> `mysql`

> useradd

`-d`

> `chage`

> `cp`

> `if`

`mktemp`

`psql`

> `sort`

> `tar`

`\d`

`-d file`

`-d home _dir`

`da*`

每日归档

dash shell

> 内置命令

> 命令行参数

> `echo`

> 环境变量

> 位置参数

> shell 脚本

> `test`

> 用户定义环境

data

> 存档

> 压缩

> 约束

> `emacs`

> 字段

> 文件

`-a`

> bash shell

> 格式

> 输入

> 文件描述符

> 输出

> 文件描述符

> 变量

> 演示

> 排序

> 数据库

`DATE`

date

`

`

-value`

`--dbname`

`dd`

Debian

> 本地启动位置

> `MySQL`

> PMS

> 运行级别

`deb-src`

`-debug_partial`

Digital Equipment Corporation (DEC)

`declare`

`--default-item`

`--defaultno`

deferred

`-delay`

`DELETE`

delete

> bash shell

> 目录

> `read`

> `sed`

`--delete`

Delete_User

分隔符

依赖

> 损坏

`--dereference`

`DESCRIBE`

Deselect

`--deselect`

桌面环境

`DESTINATION`

`/dev`

设备

> 名字

> 权限

`/dev/null`

`/sdcl`

`/sdx`

`df`

`dialog`

dialog package

Dickey, Thomas.

`--dictionary-order`

`--diff`

digiKam

`[:digit:]]`

Digital Equipment Corporation (DEC)

目录

> `for`

> bash shell

> `cron`

> 删除

> 文件，计数

> `ls`

> 权限

> 临时

> 虚拟

> 通配符

`--directory`

`dirs`

`DIRSTACK`

disable

`--disable-factory`

磁盘空间监控

> bash shell

`diskmail`

`DISKS_TO_MONITOR`

`disown`

`-display`

`-display_charset`

发行版

> 核心

> LiveCD

> 专用

`distrubition_name`

`do`

文档统计

命令

dolphin

域名系统 (DNS)

`domaintable`

`done`

`-dont_wrap_pre`

双字节字符

`do-while`

`dpkg`

拖放

`\dt`

`du`

`\du`

哑终端（dumb terminals）

`-dump`

`dw`

dyne:bolic

E

`e`

> 格式指定符

`-E`

> `chage`

> dash shell

> `mysql`

> `psql`

`-e`

> dash shell

> 文件比较

> Mailx

> Mutt

> `mysql`

> 选项

> `psql`

`\e`

`-e command`

`-e expiration _date`

`-e expire _date`

`-e file`

`-e script`

`echo`

> bash shell

> dash shell

> 磁盘空间监控

> 文件描述符

> Mailx

> 菜单

`-n`

> `STDERR`

> `while`

> zsh

`--echo-all`

`--echo-hidden`

`--echo-queries`

`ed`

edit

编辑命令

> `emacs`

> gedit

> KWrite

编辑菜单栏

> GNOME 终端仿真

> Konsole

`_editor`

编辑器

> `emacs`

> GNOME

> KDE

> `vim`

`-ef`

`ego`

`egrep`

8 位控制

`el`

`elif`

`ell`

`EMACS`

`emacs`

> 缓冲区

> 控制台模式

> 复制并粘贴

> 数据

> 图形窗口

> 菜单栏

> 搜索和替换

> X Windows

`-emacskeys`

e-mail

> 解析，正则表达式

> `STDERR`

> `STDOUT`

`empid`

仿真

`-en`

`enable`

`-enable_scrollback`

`enacs`

编码

`--encoding`

`END`

结束文件

文件结束符 (`EOF`)

`--entry`

`ENVIRON`

环境变量

> 数组

> bash shell

> Bourne shell

> 命令别名

> dash shell

> 默认值

> 全局

> 本地

> 查找

> Lynx

> 移除

> 设置

> shell 脚本

`EOF`。参见文件结束符

epiphany

`equal sign`（...不对，原文是 equal sign，即等号）

`equal sign`

ERE. 参见 POSIX 扩展正则表达式引擎

`err_exit`

`ERRNO`

错误

`--error`

`-error_files`

`err_return`

`--escape`

转义字符

`/etc`

`/etc/apt/sources.list`

`/etc/bashrc`

`/etc/fstab`

`/etc/group`

`/etc/init.d`

`/etc/init.d/boot.local`

`/etc/init.d/rc.local`

`/etc/rcX.d`

`/etc/inittab`

`/etc/passwd`

> `:`（冒号）

> `chfn`

> `IFS`

`/etc/profile`

`etc/rc#`

`/etc/rc.d/rc.local`

`/etc/rc.local`

`/etc/rc.d`

`/etc/shadow`

`/etc/skel`

`/etc/urpmi/skip.list`

`EUID`

`eval`

`eval_lineno`

evince

Evolution

`exec`

> `date`

> 文件描述符

> `STDINPUT`

> `STDOUT`

> `while`

> zsh

`-exec`

可执行文件

`exit`

> bash shell

> `-c`

> dash shell

> `mysql`

> zsh

退出状态

> `dialog`

> dialog 小组件

`--exit-label`

`exp()`

`--expanded`

`export`

`expr`

`(EXPRESSION)`

`ext`

`ext2`

`ext3`

`ext4`

扩展命令

扩展文件系统

可扩展标记语言 (XML)

extents

`--extents`

外部工具

`--extract`

F

`F`

`f`

`-F`

> `mount`

> Mutt

> `psql`

`-f`

> `cp`

> dash shell

> 文件比较

> `funclib`

> `gawk`

> `if`

> `mount`

> Mutt

> `mysql`

> 选项

> `psql`

> `sort`

> TCP 模块

`-f` 文件

> `sed`

`-F fs`

`-f` 不活跃

`-f inactive_days`

`false`

FAT16

FAT32

`fb font`

`fc`

`FCEDIT`

`FD`

`fdisk`

Fedora

> `ext4`

### 本地启动文件位置

`yum`

`fg`

`fg color`

`fgrep`

### 字段分隔符

`IFS`

`OFS`

`--field-separator`

`FIELDWIDTHS`

`FIGNORE`

`file`

### bash shell

### Mutt

`$file`

`--file`

文件。另见特定文件类型

### 块设备

### 字符设备

### 比较

`test`

### 复制，bash shell

### 创建，bash shell

### 删除，bash shell

### 描述符

### 选择

`-d`

### 数据输入

### 数据输出

`echo`

`exec`

`read`

### 重定向

### 快速照报告

`STDIN`

`STDOUT`

`gawk`

### 通配符

### 信息，bash shell

### 链接，bash shell

### 列表

### 过滤

### 循环

### 网络设备

### 权限

### 解码

### 默认值

### 组

### 所有权

### 符号

### 重命名，bash shell

`sed`

### 共享

### 查看，bash shell

文件浏览器面板

`file` 命令

`emacs`

### gedit

### KWrite

文件菜单栏

GNOME 终端仿真

Konsole

文件保存

`file1 -nt`

`file1 -ot2`

`FILE_LIST`

`FILENAME`

`FILE_NO`

路径

`--file-selection`

文件系统

### 创建

### 日志记录

### 管理

### 内核

LVM

### 导航，bash shell

### 分区

`--file-type`

### 过滤

`find`

查找下一个

查找上一个

查找已选

反向查找已选

`Find_Problem`

`finger`

`FIXED_DATE`

`fixed_date`

`float`

浮点解决方案

`flush`

`fluxox`

`fn`

`FNR`

折叠标记

字体

`for`

### bash shell

`break`

### C 语言

### 目录

`do`

`done`

`gawk`

### 组

`IFS`

`find`

`sort`

### 变量

### 通配符

`zsh`

`-force_empty`

`hrefl_a`

`force_secure`

`force_html`

`--forest`

`from`

`--format`

格式占位符

格式字符串

`forms_options`

`fpath`

碎片

`free`

`-from`

`FS`

`fsck`

`fselect`

`-ftp`

`funclib`

`FUNAME`

函数

### 数组变量

### 库

### 菜单

### 参数

### 递归

### shell 脚本

### 值

`zsh`

功能键

`functionargzero`

`fvwm`

fvwm95

`fw font`

`G`

`grep`

组

### 权限

### 正则表达式

### 角色

`sed`

### SGID

`VG`

`--Group` 列表

`--group` 列表

`groupadd`

`--group-directories-first`

`groupmod`

`GROUPS`

`grub2-theme-mint`

`gsub()`

`gunzip`

`gzcat`

`gzip`

H

`H`

`sed`

### sendmail

`h`

`sed`

`vim`

`-H`

### Mutt

`mysql`

`-h`

Mutt

`mysql`

选项

`psql`

`\H`

`\h`

硬盘。另见磁盘空间监控

硬链接

硬件管理

`hash`

`hc color`

`head`

`-head`

`--headers`

`height`

`help`

`-help`

`--help`

帮助命令

帮助菜单栏

`--help-button`

`--help-label`

`--help-status`

隐藏文件

`-hiddenlinks`

隐藏 VT 窗口

`--hide-menubar`

`histchars`

`HISTCMD`

`HISTCONTROL`

`HISTFILE`

`HISTFILESIZE`

`HISTIGNORE`

`-historical`

`history`

`HISTSIZE`

保留空间

`HOME`

`useradd`

`userdel`

home

`$HOME`

### 磁盘空间监控

### 临时文件

`/home`

`$HOME/bin`

`$HOME/mail`

`$HOME/.my.cnf`

`-homepage`

`$HOME/.zshrc`

`--host`

`HOSTFILE`

`HOSTNAME`

`HOSTTYPE`

`Hourly_Archie`

`hpfs`

`ht`

HTML

`sed`

### 统计报告

`hts`

HTTP 头部

`--human-readable`

`H`

`--interval`

字符串函数

结构化命令

时间函数

自定义函数

`printf`

自定义变量

变量

`while`

僵尸进程

gcalc-tool

`gdialog`

gedit

`--general-numeric-sort`

`gensub()`

Gentoo

`--geometry=`

`get_answer`

`get_data`

`getln`

`getopts`

`GLOBIGNORE`

GNOME。另见 GNU 网络模型环境

gnome-nettool

gnome-panel

gnome-terminal

长参数

GNU 网络模型环境 (GNOME)

应用程序

命令行参数

编辑器

电子邮件

图形窗口

终端仿真

菜单栏

标签页

Ubuntu

GNU 工具

`go`

跳转到行

`GRANT`

`grant`

图形

块模式

缓冲

颜色

终端仿真

矢量

图形桌面

图形化控制台

图形窗口

GNOME

KDE

菜单

`grep`

组

权限

正则表达式

角色

`sed`

SGID

VG

`--Group` 列表

`--group` 列表

`groupadd`

`--group-directories-first`

`groupmod`

`GROUPS`

`grub2-theme-mint`

`gsub()`

`gunzip`

`gzcat`

`gzip`

H

`H`

`sed`

sendmail

`h`

`sed`

`vim`

`-H`

Mutt

`mysql`

`-h`

Mutt

`mysql`

options

`psql`

`\H`

`\h`

硬盘。另见磁盘空间监控

硬链接

硬件管理

`hash`

`hc color`

`head`

`-head`

`--headers`

`height`

`help`

`-help`

`--help`

帮助命令

帮助菜单栏

`--help-button`

`--help-label`

`--help-status`

隐藏文件

`-hiddenlinks`

隐藏 VT 窗口

`--hide-menubar`

`histchars`

`HISTCMD`

`HISTCONTROL`

`HISTFILE`

`HISTFILESIZE`

`HISTIGNORE`

`-historical`

`history`

`HISTSIZE`

保留空间

`HOME`

`useradd`

`userdel`

home



`$HOME`

`local installation`

`local variables`

`-localhost`

`local_options`

`local_traps`

`-locexec`

`log()`

`log`

日志到文件

`logfiles`

日志消息

### 逻辑卷管理器 (LVM)

> 文件系统管理

> 镜像

> 修改

> 照照

> 条带

逻辑卷

`login`

登录角色

login shell

`logout`

`loop`

循环。另参见特定的循环操作符

> 控制

> 文件

> 嵌套

> 输出处理

`[[:lower:]]`

小写

`ls`

> `*` (星号)

> bash shell

> 命令行参数

> 目录

> 过滤

> 正则表达式

> `STDOUT`

`--ls`

`LS_COLORS`

`lshift()`

`lsof`

`lvcreate`

`lvdisplay`

`lvextend`

LVM。另参见逻辑卷管理器

LVM1

LVM2

`lvreduce`

`lvtest`

### Lynx

> 环境变量

> 输出捕获

`lynx`

`LYNX_CFG`

`LYNX_LSS`

`LYNX_SAVE_SPACE`

M

`M`, sendmail

`m`

> `fdisk`

> 正则表达式区间

`-M`

> `sort`

> `useradd`

`-m`

> `chage`

> dash shell

> `lvcreate`

> Mutt

> `sort`

> `useradd`

`M-<`

`M->`

`M-a`

`MACHTYPE`

`MAIL`

`mail`

邮件传输代理 (MDA)

邮件传输代理 (MTA)

邮件用户代理 (MUA)

`MAILCHECK`

Maildir 格式的邮箱

`maildrop`

# 读累了记得休息一会哦~

**公众号：古德猫宁李**

* 电子书搜索下载

* 书单分享

* 书友学习交流

**网站：**[沉金书屋 https://www.chenjin5.com](https://www.chenjin5.com)

* 电子书搜索下载

* 电子书打包资源分享

* 学习资源分享

`mailertable`

`MAILPATH`

`mailq`

`MAIL_TO`

Mailx

`main.cf`

`make`

`man`

Mandriva

`master.cf`

`match()`

`match STRING REGEXP`

匹配操作符

math

> `gawk`

> shell 脚本

> zsh

Mauelagen, Heinz

`maverick`

Maverick Mercat

`--max-input`

`mb`

`M-b`

退格

`M-d`

空格

`M-e`

media

`/media`

`%MEM`

`MemFree`

`meminfo`

memory

> 管理

> 页面

`MemTotal`

> 菜单

`while`

`while`

> 菜单

`--menu`

menus

> 函数

> 脚本

> 图形化窗口

> `select`

menu bar

> `emacs`

> GNOME 终端

> Konsole

`--merge`

messages

> area

> IMAP

> 日志

> shell 脚本

messages

Meta 发送

Escape 键

`M-f`

`-mf`

`-mf N`

`-mime_header`

`--minimal`

`minix`

`--minor`

Mint

镜像

`M-k`

`mkdir`

`mk2fs`

`mkefs`

`mkfs.ext3`

`mkfs.ext4`

`mkfs.xfs`

`kreiserfs`

`mktemp`

`mktemp -d`

`mktime()`

`m.n`

`/mnt`

mode

mode table

Modelines

modules

> 内核

> zsh

modulo

monitoring

> 磁盘空间

> bash 脚本

> 进程

> program

> 实时进程

> Windows

`--month-sort`

`more`

mount

`mount`

> bash 脚本

> 硬盘

mount points

挂载介质

moving

`mqueue`

`-mr N`

`ms color`

`msdos`

`msgbox`

`--msgbox`

`msgr`

multios

multios

multiple commands

> `gawk`

> shell 脚本

`while`

多个变量，`for`

Mutt

`mutt`

`mv`

`M-v`

`$myarray`

`myfuncs`

`myprint()`

`mypro?`

`myprog`

MySQL

> CLI

`mysql`

> `$?`

> `-e`

`mysql INSERT`

`mysql UPDATE`

N

`sed`

`n`

> `fdisk`

> 网络设备权限

> `sed`

`$n`

> dash shell

> `gawk`

`-N`

> `fsck`

> `mysql`

`-n`

> 磁盘空间监控

> `echo`

> jobs

> `lvcreate`

> Mailx

> `mount`

> Mutt

> 选项

> `print`

> `read`

> `sed`

> `sort`

> 替换

> `useradd`

`\n`

`-n lines`

`N` namelist

`-n` namelist

`-n str1`

`n1 eq n2`

`n1 ge n2`

`n1 -le n2`

`n1 -ne n2`

`n1-gt n2`

`n1-lt n2`

`NAME`

`name`

`--name`

`name name`

`--name name`

nautilus

`ncp`

嵌套循环

`-nested_tables`

network

> 设备

> 文件

> 权限

> zsh

网络文件系统

`[New File]`

`newaliases`

`-newschunksize`

`-newsmaxchunk`

`next`

`NF`

`nfs`

`nftfs`

`NI`

`nice`

`\nnn`

`NNTPSERVER`

`--no-align`

`-nobold`

`-nobrowse`

`--nocancel`

`-nocc`

`--noclose`

`--no-collapse`

`-nocolor`

`NODE`

nodes

`-noexec`

`-nofilerferer`

`--noframe`

`--no-group`

`--headers`

`--noost`

nohup

`--noresize`

`--nokill`

`--nolabel`

`--nolist`

`--nolog`

`--nopage`

`--noprint`

`--noquery`

`--noreverse`

`----noroot`

`--noroute`

`--nosub`

`--notext`

`--notype`

`--nouser`

`--nowait`

`--noarg`

`--nofail`

`--nowidth`

`--nowrap`

`--wrap`

`--nobar`

`--notime`

`--note`

`--notop`

`--notout`

`--notump`

`--now`

`print`

打印窗口

`printenv`

`printf`

`--print-maxsize`

`--print-size`

problem-logger

问题跟踪数据库

`Problem_Trek`

`prob_solutions`

`prob_symptoms`

`proc`

process ID (PID)

> `&&`

> `while`

process ID (`PID`)

`process_answer`

processes

> 监控

> 实时

> 信号

> 停止

> 用户帐户

> 虚拟内存

> 僵

`/proc/meminfo`

`--profile file`

profiles

`--profiles`

程序监控

程序快捷键

`--progress`

`prompt`

`PROMPT_COMMAND`

`PROMPT_DIRTRIM`

`PROTOCOL_PROXY`

`ps`

`PS1`

`PS2`

`PS3`

`PS4`

`--pset`

`-pseudo_inlines`

`psql`

公共模式

`[[:punct:]]`

Puppy Linux

`pushd`

`pushln`

PV。另参见物理卷

`pvcreate`

`pvdisplay`

`PWD`

`pwd`

> bash shell

> dash shell

> zsh

Python 控制台

Q

`q`

> `fdisk`

> `vim`

`q!`

`-Q`

`-q`

> `mysql`

> 选项

> `psql`

`\q`

> `mysql`

> `psql`

`-qa`

`qmgr`

`--question`

快速打开

`--quiet`

`QUIT`

`quit`

> `sem`

> `vmstat`

`-R`

> `chown`

> `cp`

> `fsck`

> `lvcreate`

Mutt

> `psql`

> `sort`

`-r`

> `cp`

文件比较

> `fsck`

> `gawk`

> `jobs`

> `lvcreate`

> `mount`

> `mysql`

options

> `tar`

> `useradd`

> `userdel`

zsh

`r--`

`\R`

`\r`

`r` 字符

`-r file`

`R` 文本

`radiolist`

`--radiolist`

`rand()`

`RANDOM`

`--random-sort`

`--random-source=`FILE`

`-raw`

`rc`

`rcs`

`read`

> `?` (问号)

> bash shell

> `cat`

> dash shell

> 删除

> 文件描述符

> `if-then`

> 菜单

> `-n`

> `-p`

> 管道

> `-s`

> `sed`

> `STDIN`

> `-t`

用户账户

值

> `while`

zsh

只读模式

`--readahead`

`README`

`READNULLCMD`

`readonly`

> bash shell

> dash shell

> zsh

读/写文件描述符

`-realm`

实时进程监控

`recipients`

`Record_Problem`

记录

`--record-separator`

`RECORDS_EXIST`

递归

`--recursive`

Red Hat (红帽)

> 运行级别

> `yum`

红帽软件包管理 (RPM)

> MySQL

重定向到打印机

重做

重绘窗口

`REG`

`REGEXP`

`--regionsize`

正则表达式

> `*` (星号)

> 大小写敏感性

> 统计目录文件

> 电子邮件解析

> 引擎

> `gawk`

> 组

> 手机号码验证

> `sed`

> 通配符

`rehash`

`--re-interval`

Reiser, Hans

`ReiserFS`

相对路径

`relay-domains`

`-reload`

可移动媒体

`renice`

重复键

替换

`replace-string`

`REPLY`

`report_date`

`REPORT_FILE`

仓库

> `aptitude`

> `urpm`

> 版本

> `yum`

> `zypper`

`RES`

`-restrictions`

`-resubmit_posts`

`$result`

`return`

返回键

`rev`

反转

`--reverse`

`ri`

`rich`

右边距

`RLENGTH`

`-rlogin`

`rm`

`rmacs`

`rmam`

`rmdir`

`rmkx`

`rmso`

`rmul`

`ro`

`--role+`

滚动窗口

`root`

> 文件所有者

> MySQL

> `problem-solver`

> `test`

`/root`

根驱动

`--rows` n

RPM。详见红帽软件包管理

`rpm`

`rpmfusion.org`

`rpm.list`

`RS`

`rs2`

`rshift()`

RSS

`RSTART`

运行级别

> Debian

> init 进程

> Red Hat

`rv`

`rw`

`rwx`

`r-x`

S

`S`

> `sendmail`

`s`

> `fdisk`

格式说明符

`-S`

> `cp`

> `mount`

> `mysql`

> `psql`

> `sort`

`-s`

> `cp`

> dash shell

> 磁盘空间监控

> 文件比较

> `fsck`

> `jobs`

> `lvcreate`

Mailx

Mutt

> `mysql`

options

> `psql`

> `read`

软链接

> `sort`

> `STDOUT`

zsh

`\s`

`-s file`

`-s sec`

`-s sesslist`

`-s shell`

`safe-upgrade`

`sb`

`/sbin`

`sc`

`--scale`

schema

`--schema name`

空白区域

屏幕抓取

script。详见 shell 脚本

> 启动

滚动锁定

滚动区域

回滚缓冲区

回滚菜单栏

`sda`

搜索数据

`search`

搜索并替换

搜索并替换

搜索命令

`SECONDS`

安全键盘

安全

> 更改设置

`sed`

> `&` (安符)

> `!` (感叹号)

> 高级命令

> `append`

> `branch`

> `change`

> 更改流

> 命令

> 组

> 多个

> 否定

> `d`

> 删除

> 磁盘空间监控

> 双倍行距

> 等号

> 文件

> 保持空间

> HTML

> `insert`

> 路径地址

> `list`

> `-n`

> `next`

> 行数计数

> 数字路径地址

> `p`

> `print`

> 打印最后一行

快速指南

> `r`

> `read`

> 正则表达式

> `reverse`

> shell 脚本

> `STDIN`

> `STDOUT`

> `substitution`

> `t`

> `test`

> 功能

`SEGV`

`SELECT`

`select`

> 菜单

`select`

> zsh

全选

`selective`

`sem`

> `a`

> `\` (斜杠)

> `d`

> `i`

> `p`

> `r`

> `w`

> `y`

`sendmail`

`sendmail.cf`

`sendmail.ct`

`sendmail.cw`

`--output`

`--separator`

`set`

> bash shell

> dash shell

> `getopt`

> zsh

`setopt`

Settings

`set`

`id`

> `shadow`

> `shadow`

> `shadow`

`sh`

stub functions (存存占位函数)

stub functions

`sub`

`substitution`

> 转义字符

> `N`

> `sed`

`substr()`

`substr POS LENGTH`

`sudo`

SUID. 设置用户 ID

`suspend`

`SW`

交换空间

交换出

`SwapTotal`

切换到 Tek 窗口

`swpd`

`sy`

Synaptic Package Manager

`sysstat`

system

system accounts

System V init process

`systime()`

`sysv`

`SZ`

T

`T`

> `fdisk`

> `sed`

`-T`

> `fsck`

> `mysql`

> `psql`

> `sort`

`-t`

> 文件系统

> `fsck`

> `mysql`

> `psql`

> `read`

> `sort`

> `tar`

> TCP module

> zsh

`\T`

`\t`

`t. --title=`

`-T title`

`t` ttylist

`-t` ttylist

`--tab`

Tab Stops (制表符)

tabbed windows (标签页窗口)

`--tab-correct`

`<table>`

tables (表格)

> `cron`

> databases

`--table-attr`

`--tab-len`

tabs, GNOME terminal emulation (标签，GNOME 终端仿真)



Tabs menu bar (标签菜单栏)

`--tab-with-profile=`

`tac`

Tag List (标签列表)

`tags`

`-tagsoup`

`tail`

`tailbox`

`tailboxbg`

`tar`

tasks (任务)

`tb`

`tbc`

TCP module

`tcsh`

`tee`

Tektronix

`-telnet`

`$temp`

`$tempfile`

temporary directories (临时目录)

temporary files (临时文件)

> `$HOME`

`--temporary-direction=`DIR`

`$tempt`

`TERM`

`-term`

Termcap 功能键

terminal emulation (终端仿真)

> control codes (控制代码)

> GNOME

> graphics (图形)

> keyboard (键盘)

> Konsole

> Linux Console (Linux 控制台)

> shell

> terminfo database

# 终端菜单栏

terminfo 数据库

### 控制代码

`test`

### bash shell

### 命令行参数

### dash shell

## 文件比较

### `if-then`

## 数值比较

### `root`

### `sed`

### `sort`

## 字符串比较

### zsh

`$test`

`test command`

`testerror`

`testfile`

### 文本

`Text`

`text`

文本模式过滤器

文本虚拟控制

文本换行 (Text Wrapping)

`textbox`

`--textbox`

`--text-info`

### 时间

`TIME`

`Time`

`TIME+`

时间函数

`timebox`

`TIMEFORMAT`

`--timeout`

`times`

时间戳 (Timestamp)

`--title`

`-tlog`

`TMOUT`

`/tmp`

`TMPDIR`

`-tna`

`+` `TOKEN`

`tolower()`

tomboy

### 工具命令

`top`

Torvalds, Linus

`totem`

`touch`

`touch top`

`toupper()`

`-trace`

`-trace_mask`

`transform`

`trap`

`traps_async`

`-traversal`

`--trim`

`-trim_input_fields`

`trivialrewrite`

`true`

TrueType 字体

`TSTP`

TTY

`--tty` `ttylist`

`ttyctl`

`ttyS`

`--tuples-only`

`TYPE`

`type`

`--type type`

`--types`

`typeset`

`typeset_silent`

### U

`u`

### `fdisk`

### 用户权限

### `vim`

`-U`

### `mysql`

### `psql`

### `usermod`

`-u`

### `cp`

### dash shell

### `find`

### `mysql`

### `sort`

### `tar`

### zsh

`\u`

`-u` `uid`

`U` 用户列表

`-U` 用户列表

`-u` 用户列表

`-U` `uuid`

Ubuntu

### `/etc/init.d`

### `ext4`

### GNOME

### 本地启动文件位置

### Maverick Mercat

### MySQL

UCE. 参见未请求的商业邮件

`ufs`

`UID`. 参见用户 ID

`$UID`

`ulimit`

`umask`

`umount`

`umsdos`

`unalias`

`-underline_links`

`-underscore`

撤销 (Undo)

`unfunction`

`unhash`

Unicode 字符

统一资源标识符 (URI)

取消缩进 (Unindent)

`--unique`

Unix 风格参数

`unlimit`

`unmount`

`unset`

### bash shell

### dash shell

### zsh

`unsetopt`

未请求的商业邮件 (UCE)

`until`

### `break`

### `continue`

### `while`

`unzip`

`Update_Problem`

`[[:upper:]]`

大写

Upstart 启动进程

`uptime`

URI. 参见统一资源标识符

`urpm`

### Mandriva

### 软件库

`urpme package_name`

`urpmi --auto-update --update`

`urpmi --clean`

`urpmi package_name`

`urpmi.addmedia path_name`

`urpmq --list-media`

`us`

`USE`

`use`

`--use-factory`

`-use_mouse`

`USER`

`user`

`$USER`

用户

### 账户

### 进程

### 添加

### 修改

### 权限

### 移除

用户 ID (`UID`)

### bash shell

`--User` 用户列表

`--user` 用户列表

用户变量

`USER_ACCOUNT_RECORD`

`useradd`

`-useragent`

用户定义变量

用户定义函数

用户定义变量

`userdel`

`userid`

`usermod`

`--username`

`/usr`

`/usr/sbin`

UTF-8 字体

UTF-8 标题

GNU

### `sed`

### 脚本

`u-x`

### V

`V`

`v`

### `fdisk`

`-V`

### dash shell

### `fsck`

### `psql`

`-v`

### `cp`

### dash shell

### `gawk`

### Mailx

### `mount`

### Mutt

### `mysql`

### options

### `psql`

### `tar`

### TCP module

`\V`

`v`

`-v var=value`

`val++`

`++val`

`val--`

`--val`

`-validate`

`$value`

`values`

### commands

### options

### `read`

`/var`

`varchar`

`--variable`

### variables

### `for`

### arrays

### CLI

### dash shell

### data fields

### data output

### functions

### global

### lists

### local

### shell scripts

### user

`var/mail`

`/var/mail`

vector graphics

`verbose`

virtual consoles

virtual directory

File System (VFS)

virtual memory

`virtusable`

`--visit`

visual mode

`vmstat`

volume groups (VG)

VSZ

VT commands

VT features

VT menu

VT options

`--vt sz`

`vt#3`

VT220 keyboard

### W

`W`

`w`

### `fdisk`

### `sed`

### `sem`

### substitution

`-W`

### `chage`

### `gawk`

### `mount`

### `psql`

`-w`

### file comparison

### `mysql`

`-w-`, permission code

`\W`

### `mysql`

`\w`

### `mysql`

`-w file`

`w` `filename`

`-W keyword`

`wa`

wait

### bash shell

### dash shell

### zsh

`--warning`

`--warningcancel`

warnings

`--warningno`

`--warningnocancel`

`wc`

`WCHAN`

`whence`

`WHERE`

`where`

`which`

### bash shell

### Mailx

### zsh

`while`

### `break`

### command line parameters

### `continue`

### `echo`

### `exec`

### `gawk`

### `getopts`

### menus

### multiple commands

PID

### `read`

### `until`

### user accounts

### zsh

`who`

widget

widgets

### dialog package

### `kdialog`

### `zenity`

width

`-width`

`--width` n

wildcards

### `aptitude`

### directories

### regular expressions

### `rm`

`--window`

windows. 参见图形窗口

### rolling

### tabbed

`--window-with-profile=`

`-with_backspaces`

Word Wrap Document

`--workdir dir`

`--working-directory=`

`wq`

wrappers

Writeback mode

`WWW_HOME`

`-wx`

### X

`X`

### format specifier

`x`

### `fdisk`

### format specifier

### `sed`

### `vim`

`-X`, `psql`

`-x`

### `cp`

### dash shell

### file comparison

### Mutt

### `mysql`

### options

### `psql`

### `tar`

`--x`, permission code

`x < y`

`x <= y`

`x == y`

`x > y`

X event commands

`-x file`

X Windows

### `emacs`

### virtual consoles

`x >=y`

Xandros

`xen1`

xfce

XFree86

`XFS`

XFS 文件系统

XML. 参见可扩展标记语言

`xon`

`xor()`

X.org

xterm

### command line parameters

### keyboard settings

### main menu

### output capturing

### VT options menu

### X event commands

`xtrace`

### Y

`y`

### `sem`

`-y`

### `fsck`

### Mutt

### options

`--yes-label`

`yesno`

`--yesno`

`--yesnocancel`

`+%y%m%d`

`yum`

### Fedora

### Red Hat

### repositories

`yum localinstall`

### Z

`Z`

`z`

`-Z`

### `lvcreate`

### Mutt

`-z`

### `ANSWER`

### Mutt

### `sort`

### `tar`

### `test` string 比较

`\z`

z shell (zsh)

### built-in commands

### command line parameters

### functions

### mathematical operations

### modules

### options

### shell scripts

### structured commands

`-z str1`

`zcompile`

`zenity`

`--zero`

`--zero-terminated`

`zftp`

`zip`

`zipcloak`

`zipnote`

`zipsplit`

`zmodload`

### `$HOME/.zshrc`

### zsh

zombie 进程

`--zoom=`

zsh.参见 z shell

`zsh`

`zsh/cap`

`zsh/clone`

`zsh/compctl`

`zsh/complete`

`zsh/complist`

`zsh/computil`

`zsh/datetime`

`zsh/deltochar`

`zsh/files`

`zsh/mapfile`

`zsh/mathfunc`

`zsh/net/socket`

`zsh/net/tcp`

`zsh/parameter`

`zsh/pcre`

`zsh/sched`

`zsh/stat`

`zsh/system`

`zsh/termcap`

`zsh/terminfo`

`zsh/zftp`

`zsh/zle`

`zsh/zleparameter`

`zsh/zprof`

`zsh/zpty`

`zsh/zselect`

`zsh/zutil`

`ztcp`

`zypper`

### openSUSE

###  repositories

`zypper addrepo path_name`

`zypper install package_name`

`zypper remove_package_name`

`zypper repos`

`zypper update`

`zypper verify`
