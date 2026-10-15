
```
$ ls -l /var/www/example.net
lrwxrwxrwx 1 root root 26 2009-04-09 19:11 /var/www/example.net -> /home/kyle/example.net
```

## 硬链接

硬链接与符号链接相似，不同在于符号链接指向另一个文件，而硬链接本身就是该文件。如果你想理解硬链接，了解什么是 `inode`（索引节点）会有帮助。你在分区上创建的每个文件将其数据存储在 `inode` 中。与分区上的任何其他 `inode` 相比，每个 `inode` 都有一个唯一的编号，`inode` 内部包含了如文件权限、文件所有者以及指向文件实际数据的指针等信息。当你在中创建文件时，该目录实际上包含了文件的名称和它的 `inode` 编号。当你访问该文件时，你会被引导到该 `inode` 并读取其数据。在硬链接的情况下，在分区上创建的第二个文件指向同一个 `inode`。由于硬链接与原始文件共享相同的 `inode`，从所有意义上说，它就是那个文件；两者具有相同的权限并像普通文件一样运行。与符号链接不同，如果你为文件创建硬链接，你可以删除原始文件，而硬链接仍然有效。

那么，为什么要使用一种链接而不是另一种呢？当你需要在文件系统的两个位置引用同一个文件（例如，一张大图片或其他文件）时，硬链接非常有用。你会发现，某些备份软件会使用硬链接，这样如果两个服务器具有相同的文件，备份只需要存储一次该文件。不过，你不能对目录使用硬链接。其次，硬链接仅在相同的文件系统中工作，所以如果你有一个根分区和一个独立分区，你就无法在它们之间创建硬链接。创建硬链接，只需使用不带 `-s` 的 `ln` 命令。因此，如果我想从 `/home/kyle/isos/` 获取一个占用大量空间的服务器副本，我可以输入：

```
$ ln /home/kyle/isos/ubuntu-08.04-server-i386.iso /home/kyle/Desktop/ubuntu-08.04-server-i386.iso
```

这个硬链接看起来和原始文件没有区别：

```
$ ls -l /home/kyle/isos/ubuntu-08.04-server-i386.iso
-rw-r---- 2 kyle 5847232 2008-10-08 20:26 /home/kyle/isos/ubuntu-08.04-server-i386.iso
```

## 设备文件

除了 `u`（用户）、`g`（组）和 `o`（其他）之外，`chmod` 命令还接受 `a`（所有）类别。例如，如果你想移除所有用户、组和其他用户的执行权限，你可以输入：

```
$ chmod a-x c.sh
$ ls -l c.sh
-rw-r-- 1 kyle admin 52 2009-04-04 15:13 c.sh
```

要撤销我刚刚执行的操作，我只需将其更改为 `a+`：

```
$ chmod a+x c.sh
$ ls -l c.sh
-rwr-xr-x 1 kyle admin 52 2009-04-04 15:13 c.sh
```

## Linux 文件类型

大多数使用电脑一段时间的人对两种最常见的文件类型都很熟悉：普通文件和目录。然而，在 Linux 系统上，从硬盘到其他物理设备的所有内容都表示为一个文件。虽然初级管理员可能不会经常处理命名管道或套接字文件，但有三种文件类型是你会遇到并使用的：符号链接、硬链接和设备文件。

## 符号链接

符号链接（`symlinks`）是一种指向另一个文件的特殊小文件。如果你有 Windows 背景，符号链接可能会让你联想到 Windows 快捷方式文件。当你对符号链接进行操作时（例如用另一个程序打开它或向其写入内容），数据实际上会流向原始文件。

那么，为什么要使用符号链接呢？管理员经常在多个位置需要同一组文件时会使用链接。如果你想与新的 Linux 用户共享系统目录或其他文件，这非常方便——你只需要在用户的家目录中创建一个该目录的符号链接即可。当配置文件的名称发生变化但你仍然希望旧名称出现时，你也会看到管理员使用符号链接。

要创建符号链接，请使用 `ln` 命令配合 `-s` 参数，后跟你想要链接的文件以及要创建的符号链接的路径。例如，如果我想将我的网站存储在主目录 `/home/kyle/example.net/` 下（那里可能有更多空间），但仍然显示在 `/var/www/` 下（因为这是管理员使用的标准），我可以创建一个符号链接：

```
$ ln -s /home/kyle/example.net /var/www/example.net
```

当你使用 `ln` 命令配合 `-l` 参数查看符号链接时，你可以通过它指向源文件或目录的箭头轻松判断出这是一个符号链接。请注意，如果你删除了符号链接指向的文件，符号链接文件仍然存在于系统中，但数据将丢失。

```
$ ls -l /var/www/example.net
lrwxrwxrwx 1 root root 26 2009-04-09 19:11 /var/www/example.net -> /home/kyle/example.net
```

## At and Cron

随着你越来越熟悉 Linux 和从命令行运行程序，最终你会发现你需要在你不在时运行某个程序。例如，你可能会设置一个备份系统的脚本，但你希望它在凌晨 2 点没有人在使用这些系统时运行。Linux 包含了两个不同的服务，`at` 和 `cron`，允许在预定义时间运行程序。当你想要让程序在特定时间运行且通常只运行一次时，使用 `at`。当你想要定期运行程序（例如每天一次或每小时运行一次）时，使用 `cron`。

### At

要使用 `at`，首先在终端中输入 `at` 命令，后跟想要运行该命令的时间。`at` 可以接受多种格式的时间和日期，但请务必不要混淆 AM 和 PM。你甚至可以 subst- 使用像“tomorrow”（明天）这样的词汇来指定具体的日期。一旦你按下回车键，你将进入一个交互式 shell：

```
$ at 9pm
```

```
warning: commands will be executed using /bin/sh
```

```
at>
```

在这个 shell 内部，你可以输入所有想要运行的命令，就像在终端中一样。如果你想运行多个命令，只需在每个命令后后按回车键，即可进入下一个 `at>` 提示符。当你输入完所有想要在该时间运行的命令后，在空空的 `at>` 提示符处按 `Ctrl-D`，任务就会被入队。

```
$ at 9pm
```

```
warning: commands will be executed using /bin/sh
```

```
at>
```

```
at> /usr/Local/bin/my_backup_script
```

```
at> <EOT>
```

```
job 1 at Sat Apr 17 21:00:00 2010
```

一旦命令被入队，你可以使用 `at` 命令查看你所有的入队任务。输出将列出任务编号、执行时间以及执行该任务的用户（即最初运行 `at` 命令的用户）：

```
$ atq
```

+   1 Sat Apr 17 21:00:00 2010 a Kyle

如果你想从队列中删除一个任务，只需使用 `atrm` 命令并在后面加上要删除的任务编号即可：

```
$ atrm 1
```

### Cron

在大多数情况下，你会发现自己并不想使用 `at`，而是想定期运行命令。为了这一目的，你将使用 `cron`。`cron` 是一个在你的 Linux 系统后台运行的守护进程。每个用户和系统本身都有一个 cron 表（称为 `crontab`），其中列出了他们想要运行的任务以及任务运行的频率。

系统级的 `crontab` 位于 `/etc/crontab`，它是了解 `cron` 语法的好去处：

```
$ cat /etc/crontab
```

```
# /etc/crontab-system-wide crontab
# unlike any other crontab, you don't have to run the 'crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.
```

```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr:/usr/sbin:/bin
```

```
# h dom mon dow dow user
```

```
* * * * * command
17 * * * * root test -x /usr/sbin/anacron ||
( cd ) & run-parts -report /etc/cron.hourly
```

```
25 6 * * * root test -x /usr/sbin/anacron ||
( cd ) & run-parts -report /etc/cron.daily
```

```
47 6 * * * root test -x /usr/sbin/anacron ||
( cd ) & run-parts -report /etc/cron.weekly
```

```
52 6 * * * root test -x /usr/sbin/anacron ||
( cd ) & run-parts -report /etc/cron.monthly
```

此文件中的每个 `crontab` 条目都以几个字段开头，告诉 `cron` 何时运行该条目。然后，条目指定了由哪个用户执行命令（这些示例中为 `root`），最后列出要运行的命令。让我们来看其中几行，看看语法是如何工作的：

```
25 6 * * * root test -x /usr/sbin/anacron ||
( cd ) & run-parts -report /etc/cron.daily
```
