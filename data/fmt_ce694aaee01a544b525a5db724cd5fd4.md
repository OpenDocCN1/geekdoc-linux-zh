
如果多一个 man 页面章节都包含同一个单词的信息，而你对特定章节的手册页感兴趣，可以使用 `-S` 选项。因此，以下命令行显示了 `read` 系统调用的手册页，而不是 shell 命令 `read` 的手册页。

`man -S2 read`

命令 `man -S3 fopen fread strcmp` 会按顺序显示三个 C 库调用的 man：`fopen`、`fread` 和 `strcmp`。

要退出这些系统调用的显示，请输入 `<Ctrl-C>`。

使用 `man` 命令并配合 `-k` 选项输入命令，可以指定限制搜索的关键词。这等同于使用 `apropos` 命令。搜索将从系统中所有包含该关键词的 man 页面产生有用的 man 页头。例如，以下命令在我们的 Raspberry Pi OS 系统上产生了屏幕输出：

# `man -k password`

```text
chpasswd (8) - 批量模式更新组密码
chpasswd (8) - 批量模式更新密码
getpwent_r (3) - 重入地获取文件条目
getpwent_r (3) - 重入地获取文件条目
gpasswd (1) - 管理 /etc/group 和 /etc/shadow
openssl-passwd (1) - 计算密码哈值
pam_localuser (8) - 要求用户在 /etc/passwd 中
passwd (1) - 修改用户密码
exim4_passwd (5) - Debian exim4 软件包使用的文件
exim4_passwd_client (5) - Debian exim4 软件包使用的文件
passwd (1) - 修改用户密码
```

Wait, the:

```bash
$ password
``` (8) - 批量模式更新密码

`passwd` (5) - Debian exim4 软件包使用的文件

`passwd` (8) - 批量模式更新组密码

要获取任何命令的短描述，可以使用 `whatis` 命令。这类似于 `man` 命令。`whatis` 的通用语法如下：

# `whatis`

用途：搜索 whatis 数据库的摘要

输出：在屏幕上打印一行描述

以下是此方法的示例：

```bash
$ whatis ls
```

你也可以通过向 `whatis` 命令输入多个参数来获取多个命令的短描述。以下显示了这种用法：

```bash
$ whatis ls password
```

有很多主要的命令可以让初学者在使用 Raspberry Pi OS 时更高效。以下章节提供了这类命令的示例，分为系统设置、通用工具和通信命令。

### 0.3.1 检查系统设置

`where [options] filename`

用途：定位命令的二进制、源码和 man 文件

输出：首先去除提供名称的路径组件和扩展名，然后在屏幕上显示路径名

- 常用选项/功能：
- `-b` 仅搜索二进制文件
- `-s` 仅搜索源码

例如，如果你在命令行输入命令 `where bash`，你将看到 Bash shell 程序本身的路径列表如下：

```bash
$ where bash
bash /bin/bash /etc/bash.bashrc /usr/share/man/man1/bash.1.gz
```

注意，“内置”或内部命令的路径无法通过 `where` 命令找到。当你登录时，能够查看关于你的 userid、所登录的计算机或系统以及该计算机上的操作系统的有用。这些任务可以通过 `whoami` 命令完成，它会在屏幕上显示你的 userid。`whoami` 命令的通用语法如下：

用途：显示有效用户 ID

输出：在标准输出上显示你的有效用户 ID 名称

以下显示了我们在命令行输入此命令时，系统是如何响应的：

```bash
$ whoami
bob
$
```

以下章内练习让你有机会使用 `where`、`whoami` 以及另外两个重要的实用命令 `who` 和 `hostname` 来获取有关系统的重要信息。

- 使用 `where` 命令定位 Korn shell、Bourne shell、Bourne Again shell、C shell 和 Z shell 的二进制文件。这些程序中是否有任何在你的系统上不可用？
- 使用 `whoami` 命令查找你正在使用的系统用户名。然后使用 `who` 命令查看你的用户名是如何列出的，以及同一系统的其他用户列表。你通过 `who` 命令获得的每个用户列表在屏幕上显示什么？尝试识别与你用户名在同一行中的每个字段的信息。
- 使用 `hostname` 命令查找你登录的主机计算机。你能根据此列表判断出你使用的是台式计算机还是网络计算机系统吗？请解释你如何通过 `hostname` 命令提供的列表判断出区别。

每个计算机用户执行的一个非常有用且常见的任务是在打印机上打印文本文件。这是通过本地或远程系统上配置的打印机实现的。第1章将详细介绍如何使用实用程序控制和管理打印机。

在 Raspberry Pi OS 系统上执行打印的常用命令是 `lpr` 和 `lp`。`lpr` 命令的一般语法如下：

`lpr [options] filename`

- 目的：发送文件到打印机
- 输出：将文件作为打印作业发送到打印队列
- 常用选项/功能：
    - `-P printer` 将输出发送到指定的打印机
    - `-c copies` 为每个命名文件生成指定数量的副本

以下 `lpr` 命令完成了在我们的系统中指定为 `spr` 的打印机上打印 `order.pdf` 文件。请记住，在选项（在此处为 `-P`）和选项参数（在此处为 `spr`）之间不需要空格。

```bash
$ lpr -Pspr order.pdf
$
```

接下来的 `lpr` 命令完成了在默认打印机上打印名为 `memo1` 的文件。

```bash
$ lpr memo1
$
```

以下多命令组合将 `man` 命令和 `lpr` 命令结合，并使用 Raspberry Pi OS 的管道 (`|`) 重定向字符将它们连接在一起，在名为 `hp1200` 的打印机上打印描述 `ls` 管道的帮助页。

```bash
$ man ls | lpr -Phpp1200
$
```

以下了如何使用 `lp` 命令执行打印任务。`lp` 命令的一般语法如下：

`lp [options][option arguments] file(s)`

**目的：** 在指定的系统打印机上提交文件打印，或更改挂起的打印作业

**输出：** 打印的文件或更改后的打印队列

**常用选项/功能：**

**-d destination** 打印到指定的目的地

**-n copies** 设置打印副本的数量。

在第一个命令中，要打印的文件名为 `file1`。在第二个命令中，要打印的文件名为 `sample` 和 `phones`。注意 `-d` 选项用于指定使用哪个打印机。`lp` 命令中指定副本数量的选项是 `-n`。

```bash
$ lp -d spr file1
request id is spr-983 (1 file(s))
$ lp -d spr -n 3 sample phones
request id is spr-984 (2 file(s))
$
```

- 描述并概述 Zettabyte 文件系统 (ZFS)
- 在系统管理背景下阐述 `zpool` 和 `zfs` 命令的使用
- 提供一份简要的 ZFS 命令和操作参考百科全
- 提供一个在 Bash Shell 脚本中使用 `zfs snapshot` 命令进行文件系统备份的完整示例
- 涵盖命令和原语：`zpool`, `zfs`

本章将详细介绍通常被称为 Zettabyte 文件系统 (ZFS) 的现代文件系统的实际操作机制。ZFS 具有以下属性：它可以在位级别进行自我纠错；它非常安全；它是一个卷管理器；并且它提供了自己的实时文件备份系统程序。它有时被称为“用户”文件系统，因为系统的普通特权用户可以通过输入命令来控制 ZFS 操作。我们将展示两个最重要的 ZFS 命令——`zpool` 和 `zfs` 的示例。

在本书的编写期间，ZFS 可以在基于 Debian Bookworm 的 Raspberry Pi OS 上轻松地安装。

在安装时或使用某些安装后程序，ZFS 无法轻松或可靠地作为根文件系统。此外，ZFS 无法在之前的基于 Bullseye 的 Raspberry Pi OS 上轻松或可靠地安装。

要在基于 Debian Bookworm 的 Raspberry Pi OS 上下载并安装 ZFS，我们使用了以下命令：

```bash
# sed -r 'i.BAK' s/^(.*)$/\dev/1/g' /etc/apt/sources.list
# apt update
# apt install linux-headers-arm64 zfsutils-linux-dkms zfs-zed
Output truncated...
```
