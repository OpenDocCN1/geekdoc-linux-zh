
## 附录

### 第五部分

### lpq
lpq 检查 lpd 用于在线打印机上打印文件所使用的假脱机区域，并报告指定作业或与该用户关联的所有作业的状态。如果未提供任何参数调用 lpq，它将报告当前打印队列中任何作业的情况。

### lpr
行式打印机命令使用假脱机守护程序在设施可用时打印指定的文件。如果没有提供文件名，则假设使用标准输入。以下是 lpr 命令的示例：

```
lpr /etc/hosts
```

### lprm
lprm 命令将打印作业从文档队列中移除。通过指定命令行上的作业编号来停止打印作业。以下示例停止打印作业 28（由 lpq 命令显示）：

```
# lprm 28
```

### ls
ls 命令列出目录的内容。输出格式通过选项进行操作。不带选项的 ls 命令以字母顺序列出所有可见文件（以点开头的文件是隐藏文件），并在窗口中填充尽可能多的列。与该命令一起使用的选项中最常见的用法可能是 -la 选项。a 表示列出所有文件（包括隐藏文件），l 表示将输出制作成长列表。以下是该命令的一个示例：

```
svr01:~$ ls -la
total 35
drwxr-xr-x   7  dptits  users         1024 Jul 21 00:19 .
drwxr-xr-x 140 root    root          3072 Jul 23 14:38 ..
-rw-r--r--   1  dptits  users          4541 Jul 23 23:33 .bash_history
-rw-r--r--   1  dptits  users           18 Sep 16 1996 .forward
-rw-r--r--   2  dptits  users          136 May 10 01:46 .htaccess
-rw-r--r--   1  dptits  users          164 Jun 30 1995 .kermrc
-rw-r--r--   1  dptits  users            34 Jun  6 1993 .less
-rw-r--r--   1  dptits  users          114 Nov 23 1993 .lessrc
-rw-r--r--   1  dptits  users            10 Jul 20 22:32 .profile
drwxr-xr-x   2  dptits  users          1024 Dec 20 1995 .term/
drwx------   2  dptits  users          1024 Dec 16 02:04 Mail/
drwxr-xr-x   2  dptits  users          1024 Feb 10 1996 cgi_src/
-rw-r--r--   1  dptits  users          1643 Dec 21 00:23 hi
-rwxr-xr-x   1  dptits  users           496 Jan  3 1997 quota*
drwxr-xr-x   2  dptits  users          1024 Jan  3 1997 passwd/
drwxrwxrwx   5  dptits  users          1024 May 14 20:29 public_html/
```

### lynx
lynx 浏览器是一个快速、紧凑且高效的纯文本 Web 浏览器，具有与其他 Web 浏览器几乎相同的所有功能。请在控制台的命令行或 X11 终端窗口中启动 lynx，并指定一个 Web 地址：

```
# lynx http://www.mcp.com
```

### mail
此程序提供用于发送、处理或读取邮件的简易界面，但在从命令行发送单行电子邮件消息时非常方便。您可能更喜欢使用 Pine 邮件程序。

### make
make 实用程序自动确定大型程序的哪些部分需要重新编译，然后发出重新编译所需的命令。

### makewhatis
makewhatis 命令构建 whatis 命令数据库，该数据库位于 /usr/man 目录中。请查阅 whatis 命令数据库以获取有关 whatis 命令数据库的更多信息。

### man
man 命令用于格式化和显示在线手册页。在以下示例中，我调用了描述手册页的手册页：

```
svr01:~$ man man
man(1)			man(1)

NAME
man - format and display the on-line manual pages
manpath - determine user's search path for man pages

SYNOPSIS
man [-adfhktwW] [-M system] [-P string] [-C config_file]
[-M path] [-P pager] [-S section_list] [section] name ...

DESCRIPTION
man formats and displays the on-line manual pages. This version knows about the MANPATH and PAGER environment variables, so you can have your own set(s) of personal man pages and choose whatever program you like to display the formatted pages. If section is specified, man only looks in that section of the manual. You may also specify the order to search the sections for entries and which pre-processors to run on the source files via command line options or environment variables. If name contains a / then it is first tried as a filename, so that you can do...
```

### mcopy
mcopy 命令是 mtools 软件包的一部分，它可以在无需先挂载磁盘的情况下将文件复制进或复制出 DOS 格式化的磁盘。

### mdel
此命令是 mtools 软件包的一部分，它可以在不挂载磁盘的情况下从 DOS 磁盘中删除文件。

### mdir
mdir 命令列显示 DOS 磁盘上的文件，并且是 mtools 磁盘驱动器支持软件包的一部分。

### mesg
mesg 实用程序由用户运行，用于控制其他用户对与标准错误输出关联的终端设备的写访问。如果允许写访问，则诸如 talk 和 write 之类的程序有权在终端上显示消息。默认情况下允许写访问。

### mformat
mformat 命令对具有 DOS 文件系统的软盘执行低级格式化。此命令是 mtools 软件包的一部分。

### mgetty
使用 mgetty 程序监控传入的登录，以设置终端速度、类型和其他参数。此命令是 mgetty+sendsfx 软件包的一部分。

### minicom
minicom 是一个串行通信程序。minicom 程序提供了一个易于使用的界面，带有菜单和自定义颜色，并且是一个功能强大、灵活的通信程序，用于拨号外发并与其他计算机连接。

### mkdir
mkdir 命令用于创建新目录。

### mk2fs
**mk2fs** 命令用于在指定的硬盘或其他设备（如软盘）上创建第二扩展 Linux 文件系统。此命令不会格式化新的文件系统，但会使其可供使用。**mk2fs** 还可以用于标记分区，并指定挂载点或目录，以便在挂载分区后可以访问该分区。

### mkfs
**mkfs** 用于在设备上构建 Linux 文件系统，通常是硬盘分区。该命令的语法为 **mkfs** *文件系统*，其中 *文件系统* 是设备名称（如 `/dev/hda1`）或文件系统的挂载点（例如，`/`、`/usr`、`/home`）。

### mkswap
**mkswap** 在设备（通常是磁盘分区）上设置 Linux 交换区。

设备通常具有以下形式：

```
/dev/hda[1-8]
/dev/hdb[1-8]
/dev/sda[1-8]
/dev/sdb[1-8]
```

### mlabel
**mlabel** 命令是 mtools 软件包的一部分，用于标记（命名）DOS 软盘。

### more
**more** 是一个用于一次一屏分页浏览文本的过滤器。与可以向上和向下分页浏览文本的 **less** 不同，此命令只能向下分页浏览文本。

### mount
**mount** 将 *specfile*（通常是设备名称）指定的文件系统附加到作为参数指定的目录。只有超级用户可以挂载文件。如果在不带参数的情况下运行 **mount** 命令，它将列出所有当前已挂载的文件系统。以下是 **mount** 命令的一个示例：

```
svr01:/home/dpitts$ mount
/dev/hda1 on / type ext2 (rw)
/dev/hda2 on /var/spool/mail type ext2 (rw,usrquota)
/dev/hda3 on /logs type ext2 (rw,usrquota)
/dev/hdc1 on /home type ext2 (rw,usrquota)
none on /proc type proc (rw)
```

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_992_0.png)

### mpage
`mpage` 命令在单张纸上格式化多个页面，从而节省资金并减少打印机消耗的树木数量。安装好打印机后，尝试按每页两张纸打印文档，如下所示：

```
# mpage -2 myfile.txt | lpr
```

### mt
`mt` 是磁带命令。您可以使用此命令在磁带驱动器中擦除、倒带或重新张紧磁带。您可以使用此命令执行近 40 种不同的操作。

### mv
`mv` 命令用于将对象从一个位置移动到另一个位置。如果最后一个参数指定了现有目录，则该命令将列表中的其余部分移动到该目录中。如果给出两个文件，则该命令将第一个文件移动到第二个文件中；它重命名了该文件。除非最后一个参数是目录，否则在此命令中使用两个以上参数是一个错误。

### netcfg
这是一个 Red Hat Linux 网络配置工具。`netcfg` 命令是一个 X11 客户端，用于配置 Linux 网络硬件、接口和服务。

### netstat
`netstat` 显示系统中 TCP、UDP、RAW 或 UNIX 套接字上网络连接的状态。`-r` 选项用于获取有关路由表的信息。以下是 `netstat` 命令的一个示例：

```
srv01:/home/dpitts$ netstat
Active Internet connections
Proto Recv-Q Send-Q Local Address Foreign Address (State)
tcp 0 16501 www.mk.net:www sd1b12119.san.net:3148 FIN_WAIT1
tcp 0 16501 auth02.m.k.net:www sd1b12119.san.net:3188 FIN_WAIT1
tcp 0 1 www.anglernnet.com:www ts88.ctcrap.com:1070 SYN_RECV
tcp 0 1 www.anglernnet.com:www ts88.ctcrap.com:1071 SYN_RECV
```

