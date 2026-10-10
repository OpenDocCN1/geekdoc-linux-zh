

`PATH` 命令中指定的目录，如果命令不在这些目录中的任何一个里，系统将返回“命令未找到”的消息。通常，如果用户创建了命令，应将其放置在用户主目录的 bin 目录中（例如，`/home/syngress/bin`）或其他方便的位置，并且 `PATH` 变量会检查以确保该目录已被引用。`PATH` 变量包含由冒号分隔的目录列表，如下所示：

```
echo $PATH
/bin:/usr/bin:/usr/local/bin
```

由于其中不包含你的本地 bin 目录，你需要将其添加到该变量中。可以通过执行以下命令修改 `PATH` 变量以包含该目录：

```
PATH=$PATH:$HOME/bin
```

如果 `PATH` 已经像之前那样定义过，对于用户 syngress 再次执行命令将产生以下结果：

```
echo $PATH
/bin:/usr/bin:/usr/local/bin:/home/syngress/bin
```

### 编辑器

`EDITOR` 变量定义了用户首选的文本编辑器。文本编辑器的种类和数量庞大，每个用户都有自己的最爱（以及不喜欢！）。一些常见的编辑器包括 `ed`、`vi`、`vim` 和 `emacs`。如上所述，设置环境变量可以通过在命令行上设置或插入到 _.bashrc_ 脚本中来实现。

如果未设置该变量，命令 `echo $EDITOR` 将返回一个空行。要将默认编辑器设置为 `vim`，请使用 `EDITOR=vim` 或 `EDITOR=/usr/bin/vim`。

理想情况下，使用完整的路径名（特别是在 _.bashrc_ 脚本中）会更好，以确保变量被正确定义。如果 `PATH` 变量被更改或未定义 /usr/bin 目录，系统将找不到编辑器并导致错误。vi 文本编辑器的使用方法在第 6 章中有定义。

### 终端

`TERM` 变量用于设置正在使用的终端类型，当使用面向屏幕的程序（如文本编辑器）时，这一点尤为重要。该变量在系统安装期间会自动设置，但如果用户远程访问系统，可能需要对其进行修改。当使用 KDE 安装 Linux 时，`TERM` 变量将被设置为值 `xterm`。

也可以使用 `tset` 命令设置该变量，该命令常用于用户的登录脚本中，以便让他们选择正在登录的终端类型。

## PAGER

`PAGER` 变量控制输出到屏幕的内容，例如 `man` 命令。这允许以受控的方式显示输出。`PAGER` 的典型值是 `more` 和 `less`。虽然这两者相似，但 `less` 具有额外功能（例如使用 b 键向后滚动），因此它是作为默认值更优选的选项。

## HOME

`HOME` 变量在每次登录系统时都会被设置，并将其设置为 /home/username（其中 username 是你的登录名）。这不应更改，因为许多程序使用此变量来在你的个人主目录中创建或查找文件。此外，快捷方式 `~` 引用 `HOME` 变量，如果修改了该变量，将返回错误结果。

## PRINTER

`PRINTER` 变量定义默认打印机。如果没有定义打印机，该值将被设置为 `NULL`。该变量主要用于命令行程序进行打印。设置该变量并不意味着不需要在系统上安装打印机。使用 `PRINTER` 变量允许系统管理员根据用户的位置为用户设置特定的打印机。

## 练习 5.1：配置用户环境

在这个练习中，你将修改 profile 中默认的 `PAGER` 变量设置。

- 1. 将目录更改到你的主目录。
- 2. 执行 `more .bashrc` 命令查看你当前的环境设置。你会看到 `PAGER` 变量被设置为 `more`。
- 3. 输入命令 `echo $PAGER`，它显示值 `more`。
- 4. 使用你喜欢的编辑器，将以下行添加到 .bashrc 文件中：
    `export PAGER=less`
- 5. 当用户下次注销并重新登录时，这将把值从 `more` 更改为 `less`。

## 设备管理

Linux 系统中的设备管理至关重要，乍一看，对于正在熟悉 Linux 的 Microsoft Windows 用户来说，它似乎更加复杂。管理设备通常不止一种方法，而且通常除了图形用户界面（GUI）之外，还可以使用命令行。以下部分将列出一些系统管理员在日常工作中可能会使用的常见命令和主要目录。

### *lsusb*

*lsub* 将列出系统上的所有 USB 总线，并显示连接到它们的任何设备的信息。*-v* 和 *-vv* 选项将提供详细输出；然而，这仅在调试时需要，因为输出确实非常详细，*-vv* 选项会输出周边组件互连（PCI）设备可以显示的所有信息。此命令有助于查看哪些 USB 设备正在工作以及连接的设备类型。

```bash
$ lsusb
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 005: ID 0204:6025 Chipsbank Microelectronics Co., Ltd
CBM2080 Flash drive controller
Bus 001 Device 003: ID 046d:c517 Logitech, Inc. LX710 Cordless Desktop
Laser
Bus 001 Device 002: ID 413c:0058 Dell Computer Corp. Port Replicator
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

### *lspci*

*lspci* 命令与 *lsub* 命令类似，不同之处在于它显示系统中所有 PCI 总线的信息以及连接到它的所有设备。此命令有助于了解系统中连接了哪些设备以及应为这些设备加载的实际驱动程序。此命令也可以与 *-x* 选项一起使用，以显示 PCI 配置的前 64 个字节，这对于查看加载的内容很有用。

```bash
$ lspci -x
00:00.0 Host bridge: Intel Corporation 82855PM Processor to I/O Controller (rev 03)
00: 86 80 40 33 06 01 90 20 03 00 00 06 00 00 00 00
10: 08 00 00 e0 00 00 00 00 00 00 00 00 00 00 00 00
20: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
30: 00 00 00 00 e4 00 00 00 00 00 00 00 00 00 00 00

00:01.0 PCI bridge: Intel Corporation 82855PM Processor to AGP Controller (rev 03)
00: 86 80 41 33 07 01 a0 00 03 00 04 06 00 20 01 00
10: 00 00 00 00 00 00 00 00 01 01 20 c0 c0 a0 22
20: 00 fc f0 fd 00 e8 f0 ef 00 00 00 00 00 00 00 00
30: 00 00 00 00 00 00 00 00 00 00 00 00 00 0c 00
```

此外，可以使用 -b 命令来显示各卡片看到的中断请求线（IRQ）地址。

```
$ lspci -b
00:00.0 Host bridge: Intel Corporation 82855PM Processor to I/O Controller (rev 03)
00:01.0 PCI bridge: Intel Corporation 82855PM Processor to AGP Controller (rev 03)
00:1d.0 USB Controller: Intel Corporation 82801DB/DBL/DBM (ICH4/ICH4-L/ICH4-M) USB UHCI Controller #1 (rev 01)
00:1d.1 USB Controller: Intel Corporation 82801DB/DBL/DBM (ICH4/ICH4-L/ICH4-M) USB UHCI Controller #2 (rev 01)
```

输出还可以以树状格式显示，当需要快速概览设备时，这很有用。

```
$ lspci -t
-[0000:00]--+-00.0
|\-
|    01.0-[0000:01]----00.0
|    1d.0
|    1d.1
|    1d.2
|    1d.7
|    |e.0-[0000:02-0a]----00.0
|    |     01.0
|    |     01.1
|    |     03.0
|    1f.0
|    1f.1
|    1f.5
|\-1f.6
```

### lsmod

`lsmod` 命令显示有关已加载模块的所有信息，格式为名称、大小、使用次数和引用模块列表。列表的一部分显示如下：

```
$ lsmod
  Module
nls_iso8859_1           3768   1
nls_cp437              5432   1
vfat                   9764   1
fat                   46376   1 vfat
usb_storage            86620   1
ip6t_LOG               6212   7
xt_tcpudp              2728   2
xt_pkttype             1560   3
ipt_LOG                5708   8
xt_LIMIT               2056  15
binfmt_misc            7872   1
snd_pcm_oss           43300   0
```

`lsmod` 命令从 /proc/modules 文件中获取数据，并以更容易被人类阅读的形式显示。

### /sys

/sys 目录包含所有与内核、固件和其他系统相关文件相关的文件。/sys 下有几个目录，以确保其结构组织良好。可以使用 `ls` 命令查看整体结构。

```
$ ls -l /sys
total 0
drwxr-xr-x   2 root root   0 2009-05-23 10:53 block
drwxr-xr-x  16 root root   0 2009-05-23 08:47 bus
drwxr-xr-x  39 root root   0 2009-05-23 08:47 class
drwxr-xr-x   4 root root   0 2009-05-23 10:56 dev
drwxr-xr-x  10 root root   0 2009-05-23 08:47 devices
drwxr-xr-x   5 root root   0 2009-05-23 08:47 firmware
drwxr-xr-x   3 root root   0 2009-05-23 08:47 fs
drwxr-xr-x   6 root root   0 2009-05-23 08:47 kernel
drwxr-xr-x 127 root root   0 2009-05-23 10:53 module
drwxr-xr-x   2 root root   0 2009-05-23 08:47 power
```

/sys 目录与下一节中描述的 /proc 目录相关。

