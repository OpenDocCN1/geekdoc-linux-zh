
这意味着 `known_hosts` 文件的第一行包含违规密钥。删除文件中的此行，`ssh` 程序即可接受来自远程系统的新的认证凭据。

除了在远程系统上开启 shell 会话外，`ssh` 还允许我们能够在远程系统上执行命令。例如，要在远程主机 `remote-sys` 上执行 `free` 命令并将结果显示在本地系统，我们使用：

```
~me@linuxbox ~$ ssh remote-sys free
password:
```

| total | used | shared | cached |
| :--- | :--- | :--- | :--- |
| Mem: 775536 | 507184 | 0 | 110068 154596 |
| -/+ buffers/cache: 242520 | 533010 | | |
| Swap: 0 | 157285 | | |

```
~me@linuxbox ~$
```

这种技术可以用于更有趣的方式，例如下面的示例，其中我们在远程系统上执行 `ls` 并将输出重定向到本地系统上的文件：

```
me@linuxbox ~$ ssh remote-sys 'ls * > dirlist.txt'
me@remote-sys~$ password:

me@linuxbox ~$ ssh remote-sys 'ls * > dirlist.txt'
me@remote-sys~$ password:
```

注意命令中的单引号。同样，如果我们想将输出放在本地系统，可以使用重定向操作符。

```
me@linuxbox ~$ ssh remote-sys 'ls * > dirlist.txt'
```

## 使用 SSH 隧道

当你通过 `ssh` 建立连接时，发生的一部分是在本地和远程系统之间创建一个加密隧道。最常见的用途是虚拟专用网络（VPN）。然而，也可以在远程系统上运行图形应用程序并显示在本地。在某些系统中，你可能需要使用 `-Y` 而不是 `-X`。这是一个示例会话：

```
@linuxux ~$ ssh -X remote-sys
me@remote-sys's password:
Last login: Mon Sep 10 13:23:11 2018
@remote-sys~$
```

## scp 和 sftp

OpenSSH 包还包含了两个可以使用 SSH 隧道复制文件的程序。第一个 `scp`（安全复制）用法类似于熟悉的 `cp` 程序来复制文件。最显著的区别是源或目标路径可以使用远程主机名称引导，后跟一个冒号。例如，如果我们想从远程系统的家目录复制 `document.txt` 到本地系统的当前目录，我们可以这样做：

```
@linuxux ~$ scp remote-sys:document.txt
remote-sys's password:
document.txt 100% 5.5KB/s 00:00
```

与 `ssh` 一样，如果所需的远程帐户与本地系统不匹配，可以在远程主机名的开头加上用户名。

```
@remote-sys:document.txt
```

第二个 SSH 文件复制程序是 `sftp`，正如名称所示，它是 `ftp` 程序的替代品。`sftp` 的工作与我们之前使用的程序类似，但它不是以明文传输一切，而是使用加密隧道。`sftp` 相比传统的 `ftp` 优势在于不需要在远程主机上运行 FTP 服务器。只需要 SSH 服务器。这意味着任何通过 SSH 客户端连接的远程机器都可以用作类似 FTP 的服务器。这是一个示例会话：

```
@linuxux ~$ sftp remote-sys
Connecting to remote-sys...
remote-sys's password:
sftp> ls
ubuntu-8.04-desktop-i386.iso
sftp> cd ubuntu-8.04-desktop-i386.iso
sftp> get ubuntu-8.04-desktop-i386.iso ubuntu-8.04-desktop-i386.iso
Fetching /home/me/ubuntu-8.04-desktop-i386.iso 100% 699MB/s 01:35
sftp> bye
```

SFTP 协议被许多 Linux 发行版中的图形化文件管理器支持。使用 GNOME 还是 KDE，我们都可以在地址栏中输入以 `sftp://` 开头的 URI，并对运行 SSH 服务器的远程系统上的文件进行操作。

# Windows 上的 SSH 客户端？

假设你正坐在一台 Windows 电脑前，但你需要登录你的 Linux 服务器并完成一些实际工作；你该怎么办？当然，为你的 Windows 机器下载一个 SSH 客户端程序。这类程序有很多。其中最受欢迎的可能是由 Simon Tatham 及其团队开发的 PuTTY。PuTTY 程序显示一个终端窗口，并允许 Windows 用户在远程主机上打开 SSH（或 telnet）会话。该程序还提供了 scp 和 sftp 程序的对应程序。

PuTTY 可以在 `www.chiark.greenend.org.uk/~sgtatham/putty/` 获得。

## 总结

在本章中，我们调查了大多数 Linux 系统上可见的网络工具领域。由于 Linux 在服务器和网络设备中被广泛使用，通过安装额外的软件可以添加更多工具。但即使只有基础工具集，也可以执行许多实用的网络相关任务。

# 17

## 搜索文件

当我们漫游自己的 Linux 系统时，有一点变得显而易见：典型的 Linux 系统有大量文件！这引发了一个问题：“我们如何找到东西？”我们已经知道 Linux 文件系统根据从的一代类 Unix 系统传递给下一代的约定进行了良好的组织，但文件的巨大数量可能会带来一个令人生畏的问题。

在本章中，我们将介绍两个用于在系统中查找文件的工具。

- `locate` 按名称查找文件
- `find` 在目录层次结构中搜索文件

我们还将查看经常与文件搜索命令配合使用的命令，用于处理生成的文件列表。

- `xargs` 从标准输入构建并执行命令行

此外，我们还将介绍两个命令来协助我们的探索。

- `touch` 修改文件时间
- `stat` 显示文件或文件系统状态

## locate—最简单的查找方法

`locate` 程序对路径名进行快速数据库搜索，然后输出每个匹配给定子字符串的名称。例如，假设我们要找到所有以 zip 开头的程序。由于我们正在寻找程序，可以假设包含程序的目录名会以 `bin/` 结尾。因此，我们可以尝试这样使用 locate 来查找文件：

```bash
[linuxux ~] locate bin/zip
```

`locate` 将搜索其路径名数据库并输出任何包含字符串 `bin/zip` 的条目。

```bash
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zsplit
```

如果搜索要求没有那么简单，我们可以结合 `locate` 和其他工具（如 `grep`）设计更有趣的搜索。

```bash
[linuxux ~] locate zip | grep bin
/bin/bunzip2
/bin/bzip2
/bin/bzip2recover
/bin/gunzip
/bin/gzip
/usr/bin/funzip
/usr/bin/gpg-zip
/usr/bin/preunzip
/usr/bin/prezip
/usr/bin/prezip-bin
/usr/bin/unzip
/usr/bin/unzipsfx
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zsplit
```

`locate` 程序已经存在多年，有几种常用的变体。在现代 Linux 发行版中最常见的两种是 `solace` 和 `locate`，尽管它们通常通过名为 `locate` 的符号链接访问。不同版本的 `locate` 具有重叠的选项。某些版本包含正则表达式匹配（我们将在第 19 章中介绍）和通配符支持。检查 `locate` 的主页以确定安装的是哪个版本的 `locate`。

### locate 数据库从哪里来？

你可能会注意到，在某些发行版中，`locate` 在系统安装后无法工作，但如果你第二天再次尝试，它就能正常运行。这是为什么？`locate` 数据库是由另一个名为 `updated` 的程序创建的。通常，它作为 cron 任务定期运行，即 cron 守护进程按定期执行的任务。大多数配备了 `locate` 的系统会在一天后运行。由于数据库不是持续更新的，你会发现当使用 `locate` 时，非常新的文件不会显示。为了克服这个问题，可以在提示符处成为超级用户并手动运行 `updated` 程序。

## find—费力的文件查找方法
