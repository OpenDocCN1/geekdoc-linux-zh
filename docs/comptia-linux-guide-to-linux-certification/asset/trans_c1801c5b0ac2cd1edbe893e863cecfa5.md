

不过，info 页面和手册页都用于查找文档，因为手册页自 Linux 诞生以来一直被使用，而在 UNIX 操作系统中已有二十多年的历史。以下是一个使用 info 实用工具查找 whoami 命令信息的示例：

```
[root@server1 root]# info whoami
```

随后，info 页面会以交互方式显示：

```
File: coreutils.info, Node: who invocation, Prev: users invocation,
Up: User information

20.6 'who' : Print who is currently logged in
================================================

'who' prints information about users who are currently logged on.
Synopsis:

who [OPTION] [FILE] [am i]

If given no non-option arguments, 'who' prints the following
information for each user currently logged on: login name, terminal line,
login time, and remote hostname or X display.

If given one non-option argument, 'who' uses that instead of a default
system-maintained file (often '/var/run/utmp' or '/var/run/utmp') as the
name of the file containing the record of users logged on. '/var/log/wtmp'
is commonly given as an argument to 'who' to look at who has previously
logged on.

If given two non-option arguments, 'who' prints only the entry for * bash:
(bash). The Bourne Again Shell. the hostname. Traditionally, the two
arguments given are 'am i', as in 'who am i'.

Time stamps are listed according to the time zone rules specified by the
'TZ' environment variable, or by the system default rules if 'TZ' is not
set. *Note Specifying the Time Zone with 'TZ': (libc)TZ Variable.

The program accepts the following options. Also see *Note Common
options::

'-a'
'--all'
Same as '-b -d --login -p -r -t -T -u'.

'-b'
'--boot'
Print the date and time of last system boot.

--zz-Info: (coreutils.info.gz) who invocation, 103 lines --Top-----
[root@server1 root]#_ 
```

![Image](img/c27875544958897d817484d558c208c8_98_0.png)

在 info 实用工具中，按 ? 键或 Ctrl+h 组合键可显示描述 info 用法的帮助屏幕。与 man 命令一样，你可以使用 q 键退出。

某些命令没有手册页或 info 页面。这些命令通常是 BASH shell 内置的函数。要查找这些命令的帮助信息，必须使用 help 命令，如下所示：

```
[root@server1 root]# help echo
echo: echo [-neE] [arg ...]

Write arguments to the standard output.

Display the ARGs on the standard output followed by a newline.

Options:

- -n do not append a newline
- -e enable interpretation of the following backslash escapes
- -E explicitly suppress interpretation of backslash escapes

'echo' interprets the following backslash-escaped characters:

- \a alert (bell)
- \b backspace
- \c suppress further output
- \e escape character
- \f form feed
- \n new line
- \r carriage return
- \t horizontal tab
- \v vertical tab
- \\ backslash
- \0nnn the character whose ASCII code is NNN (octal). NNN can be 0 to 3 octal digits
- \xHH the eight-bit character whose value is HH (hexadecimal). HH can be one or two hex digits

Exit Status:

Returns success unless a write error occurs.

[root@server1 root]#_
```

## 关闭 Linux 系统

由于操作系统负责将计算机内存中的数据写入计算机的磁盘驱动器，因此直接切断计算机电源可能会导致用户文件和系统文件损坏。因此，在关闭计算机硬件组件的电源之前，准备操作系统关闭是很重要的。为此，你可以发出 shutdown 命令，该命令可以在经过一定时间后停止或重启（重新启动）你的计算机。例如，要在 15 分钟后停止你的系统，可以输入：

```
[root@server1 root] # shutdown -H +15
```

这将产生类似于以下内容的输出：

```
Broadcast message from root@server1 (Wed 2014-09-17 15:36:48 EDT) :

The system is going down for power-off at Wed 2014-09-17 15:51:48 EDT!

Shutdown scheduled for Wed 2014-09-17 15:51:48 EDT, use `shutdown -c` to cancel.
```

请注意，在启动 shutdown 命令后，你将不会再收到命令提示符。因此，要停止关闭过程，只需按 Ctrl 和 c 键组合返回命令提示符，然后发出命令 `shutdown -c` 以取消关闭。

若要立即停止你的系统，可以输入：

```
[root@server1 root] # poweroff
```

shutdown 命令的其他示例及其说明如表 2-9 所示。

| 命令 | 描述 |
| :--- | :--- |
| `shutdown -H +4` | 四分钟后停止你的系统 |
| `shutdown -r +4` | 四分钟后重启你的系统 |
| `shutdown -H now` | 立即停止你的系统 |
| `shutdown -r now` | 立即重启你的系统 |
| `shutdown -c` | 取消已计划的关机 |
| `halt` | 立即停止你的系统 |
| `poweroff` | 立即停止你的系统并切断计算机电源 |
| `reboot` | 立即重启你的系统 |

**表 2-9 停止和重启 Linux 操作系统的命令**

## 本章总结

- 在安装之前，应使用 HCL（硬件兼容性列表）验证硬件要求。
- 可以通过从互联网下载 ISO 镜像来获取 Linux 安装介质，该镜像可以写入 DVD 或 USB 闪存盘，也可以直接供虚拟化软件使用。
- 典型的 Linux 安装会提示用户提供信息，例如语言、日期、时区、键盘布局、网络配置、用户账户配置和永久存储配置。
- 用户必须登录到终端并接收 shell 才能与 Linux 系统和内核进行交互。单个用户可以同时登录到多个不同的终端，无论是在本地还是通过网络。
- 无论你使用哪种类型的终端（图形界面或命令行），你都可以在 shell 提示符下输入命令、选项和参数来执行系统任务、获取命令帮助或关闭 Linux 系统。shell 区分大小写，并理解各种称为 shell 元字符的特殊字符，如果不希望使用其特殊含义，则应保护这些字符。

# 关键术语

**Advanced Technology Attachment (ATA)** 参见 并行高级技术附件。

**arguments** 出现在命令名称之后的文本，不以破折号（- 字符）开头，并指定命令正常运作所需的信息。

**authentication** 每个用户在获得系统用户界面访问权限之前，必须使用有效的用户名和密码进行登录的过程。

**B-tree Filesystem (BTRFS)** 一种实验性的 Linux 文件系统，包含高级功能，如存储池和文件系统快照。

**BASH shell** 也称为 Bourne Again Shell，这是 Linux 中的默认命令行接口。

**BIOS (Basic Input/Output System)** 计算机系统中包含用于在启动时初始化硬件组件的程序的部分。

**command** 存在于文件系统中的程序，在命令行输入时执行。

**ext2** 非日志记录型 Linux 文件系统。

**ext3** 日志记录型 Linux 文件系统。

**ext4** ext3 文件系统的改进版本，具有扩展的功能集和更好的性能。

**extended partition** 硬盘或 SSD 上的分区，可以进一步细分为称为逻辑驱动器的组件。

**filesystem** 硬盘或 SSD 分区格式化的方式，使数据能够驻留在物理介质上；常见的 Linux 文件系统包括 ext2、ext3、ext4、REISERFS 和 VFAT。

**GUID Partition Table (GPT)** 大硬盘（> 2TB）上分区外部的区域，用于存储分区信息和启动加载器。

**Hardware Compatibility List (HCL)** 经过测试并被认为与给定操作系统兼容的硬件组件列表。

**info pages** 通过输入 info 命令行实用工具可用的本地、易读的命令语法文档集。

**Integrated Drive Electronics (IDE)** 参见 并行高级技术附件。

