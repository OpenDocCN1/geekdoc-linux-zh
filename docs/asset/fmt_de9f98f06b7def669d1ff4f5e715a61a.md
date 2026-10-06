
`mount [option(s)] [-t type] remote_volume node`

`umount [option(s)] node`

### Finder 等效操作

通过选择“前往 (Go) ➤ 连接服务器 (Connect to Server)”来挂载网络卷。

## mount 命令选项概述

- `mount`: `mount` 命令用于挂载文件系统。
- `umount`: 命令用于卸载文件系统。

### 获取更多信息

在终端（Terminal）中输入 `man mount`、`man unmount`、`man type` 或 `man amount` 来显示帮助页面并了解更多。

## 使用 ssh 安全地登录远程计算机

如果你想在运行 Mac OS X 或其他基于 Unix 的系统的远程计算机上运行命令，你必须登录到该计算机上的用户账户。当你登录到远程计算机时，就像是在那台计算机的终端中打开了一个会话；距离远近没有任何影响。你可以从远程终端运行每一个命令，无论它运行的是什么操作系统（当然，如果它是不同的类 Unix 系统，你必须意识到命令之间的任何差异）。

但是，首先必须在主机上启用远程登录。在 Mac OS X 下，通过在“共享 (Sharing)”面板中勾选“远程登录 (Remote Login)”来实现。这允许用户使用 `ssh`（安全外壳）程序访问你的 Mac，该程序在网络上的两个主机之间提供安全的加密通信。此外，你不能有防火墙拦截 `22` 端口以使用这种登录方法。

`ssh` 命令非常简单。它的语法如下：

```
ssh username@host
```

`username` 是主机上用户账户的，`host` 是远程计算机的 IP 地址或主机名。

要登录 IP 地址为 `100.0.1.201` 的 Mac，运行以下命令：

```
Walden:~ kirk$ kirk@10.0.1.201
```

终端显示主机信息

主机 '10.0.1.201' 的真实性无法确认。RSA 密钥指纹为 58:35:46:c9:de:c6:81:17:d2:97:d1:83:f5:b6:9a:02。你确定要继续连接吗 (yes/no)？

## 实践：在远程 Mac 上使用图形应用程序

当你通过 `ssh` 登录到远程 Mac 时，你可以访问命令行，并可以从终端运行任何命令，就像你坐在那台计算机面前一样。然而，你无法对图形用户界面应用程序进行任何操作。

但你可以从命令行在远程 Mac 上打开应用程序。`open` 命令允许你实现这一点。假设你想在你网络上的某台 Mac 上打开 iTunes，以便将 MP3 文件与你的本地网络共享。使用 `ssh` 连接后，只需运行此命令：

```
$ open -a iTunes
```

你可以使用 `open` 命令从命令行打开任何你想要的图形化应用程序，尽管这并不总是有用；只有当应用程序一运行后就能独立执行某些操作，或者它能接受来自你正在使用的 Mac 的连接或命令时，这才有趣。关于使用 `open` 命令的更多信息，请参阅间插 5，“万能的 open 命令”。

输入 yes 允许访问或输入 no 停止连接。终端显示如下：

> 警告：已将 '10.0.1.201' (RSA) 永久地添加到已知主机列表。kirk@10.0.1.201 的密码：

输入你的密码，终端会显示打开新终端会话时看到的标准欢迎消息：

```
Last login: Fri Jun 13 12:17:42 2004 from 100.0.1.202

Welcome to Darwin!

Walden2$: kirkk
```

如你所示，提示符显示了我连接的计算机名称 (`Walden2`)，而最后登录 (`Last login`) 显示我连接到了 `100.0.1.202`。
默认情况下，`ssh` 连接到端口 `22`。如果由于任何原因你需要使用不同的端口连接，可以使用 `ssh` 的 `-p` 选项并指定你的端口号：

```
$ ssh -p 2000 kirkk@10.0.1.201
```

在连接到另一台 Mac 时，你可以从终端运行命令，就像你坐在它面前一样。这对于故障排除或系统管理非常有用。假设你在某台 Mac 上有一个卡住的进程且无法强制退出它。你可以登录到 Mac 并使用 `top` 命令找到该进程，然后使用 `kill` 命令将其关闭（有关管理进程的更多信息，请参阅第 14 章，“管理程序和进程”）。

你也可以连接到远程计算机，再连接回你所在的计算机。这看起来可能很奇怪，但对于诊断网络问题很有用。看以下：

```
Walden$: kirkk ssh 10.0.1.201

kirk@10.0.1.201's password:

Last login: Fri Jun 13 12:23:03 2004 from 100.0.1.202

Welcome to Darwin!

Walden2$: kirkk ssh 10.0.1.202

kirk@10.0.1.202's password:

Last login: Fri Jun 13 12:16:15 2004 from 100.0.1.202

Welcome to Darwin!

Walden: ~kirk$
```

在这个示例中，我从 `Walden2` 连接，然后在同一个会话中打开了一个回到 `Walden` 的连接。如果我在一个方向遇到了网络问题——例如，从 `Walden2` 到 `Walden`——我可以运行 `Ping` 和 `Traceroute` 等工具来尝试解决它们。要结束会话，只需输入 `exit`。

## ssh 命令概述

### 命令语法

```
ssh username@host [command]
```

### Finder 等效操作

无。

## ssh 选项概述

- `ssh`: 与远程计算机创建一个安全的（加密的）shell 会话。
- `-p [port_number]`: 此选项告诉 `ssh` 命令使用指定的端口进行连接。

### 获取更多信息

在终端中输入 `man ssh` 来显示帮助页面并学习更多关于 `ssh` 的知识。

## 运行单个命令

通过 `ssh` 你还可以在远程计算机上运行单个命令。你不需要打开会话，只需告诉远程计算机执行命令并将其输出返回给你。这可以是你可以从终端运行的任何类型的命令。要查看远程计算机存在哪些用户账户，你可以运行：

```
$ kirk@10.0.1.201 password:

nobody

root

unknown

lp

postfix

www

mysql

sshd

cyrus

mailman

appserver

samuel

bach
```

## 使用 telnet 登录远程计算机

`Telnet` 协议（根据 RFC 854 中的原始规范）是一种较旧的协议，设计用于“允许一种终端设备和终端导向进程彼此相互交互的方法”。与 `SSH` 不同，`Telnet` 不是加密的，因此安全性低得多。在过去，`telnet` 用于公告板系统 (BBS)、游戏服务器以及其他不需要安全性的服务器。现在由于不安全已不再使用，但某些服务器仍通过 `Telnet` 提供服务。要通过 `Telnet` 连接服务器，使用以下语法：

```
$ telnet hostname
```

## telnet 命令概述

### 命令语法

```
telnet hostname [port]
```

### Finder 等效操作

无。

## telnet 选项概述

- `telnet`: `telnet` 命令与远程计算机创建一个 shell 会话。
- `port`: 指定端口号告诉 `telnet` 命令使用指定的端口而不是默认端口。

### 获取更多信息

在终端中输入 `man telnet` 来显示帮助页面并学习更多关于 `telnet` 的知识。这尝试通过默认 `Telnet` 端口 `23` 进行连接。如果你需要通过特定端口使用 `Telnet` 连接，请使用：

```
$ telnet hostname port
```

这是一个 `telnet` 会话开始的示例。在这个示例中，我使用特殊端口 `9696` 连接到 `nngs.cosmic.org` (NGS Go 服务器)：

```
$ telnet nngs.cosmic.org 9696

Trying 198.36.217.60...

Connected to nngs.cosmic.org.

Escape character is '^'.
```

Copyright 1995-2001 by Erik H. Riper, all rights reserved.

- 欢迎来到 Name Go 服务器！
- 很高兴来这里下棋或结朋友。

围棋发明于4000年前的，在韩国被称为“Bad”，在日本被称为“Go”，这种奇妙的游戏将简单的形式与深奥的策略结合在一起。现在你也可以在互联网上享受它。

我们欢迎你的邮件问题/建议：wgc@nngs.cosmic.org
请以客身份登录一个可能未被其他玩家使用的异常名称。

登录：

服务器要求登录；当你输入此登录并按回车后，它会要求密码。由于 Go 不需要任何特殊安全措施，这相对安全。但密码是以明文发送的，任何包嗅探都能轻松发现它。

## 使用 scp 远程复制文件

当你连接到远程计算机时，跨网络复制文件的方法取决于连接方式。如果你只是挂载了网络卷，你可以使用标准的复制命令 `cp` 和 `scp`；请参见第 5 章，“文件和目录操作”获取更多关于这些命令的信息。

要从挂载的网络卷复制文件到我的主目录，我只需运行此命令：

```
$ cp /Volumes/Files/Walden.txt ~/Walden.txt
```

无论卷位于何处，命令都是相同的。然而，如果你想安全地从网络卷复制文件，可以使用一个特殊命令 `scp (安全复制)`。但要使用此命令，你必须确保远程计算机已开启远程登录。

## 动手实践：启用 TELNET

当你在“共享”属性面板格中启用“远程登录”时，`ssh` 会开启。你可能也想在你的 Mac 上运行 `Telnet`，为其他人提供 `Telnet` 访问。（你仍然可以作为客户端运行 `Telnet` 连接到其他计算机，而无需在你的 Mac 上启用它。）

要启用服务，你必须以 root 身份编辑 `/etc/xinetd.d/telnet` 文件。你可以通过运行以下命令使用 Pico：

```
$ sudo /etc/xinetd.d/telnet
```

此文件包含 `Telnet` 服务的信息。要开启 `Telnet`，请将 `disable = yes` 改为 `disable = no`。

- `disable = yes`
- `socket_type = stream`
- `wait = no`
- `user = root`
- `server = /usr/libexec/telnet`
- `groups = yes`
- `flags = REUSE`

接下来，重启 `xinetd`：

```
$ sudo kill -HUP 'cat /var/run/xinetd.d/pid'
```

记住，`Telnet` 不是加密的，因此是不安全的。

你可以使用这里描述的相同技术，启用 `/etc/xinetd.d/` 目录下的其他服务。

`scp` 命令的语法与 `cp` 命令类似：

```
scp source destination
```

然而，由于 `scp` 是从一台计算机复制到另一台计算机，你需要在源或目的地中指定用户名和主机，取决于你登录的是哪台计算机：

```
scp [user@host]:source [user@host]destination
```

这里有一个 `scp` 命令的示例：

```
$ scp kirk@10.0.1.201:Walden.txt ~/Walden.txt

Walden.txt 100% *****************************| 567 KB 00:01
```

这从 `10.0.1.201` 上用户 `kirk` 的家目录复制 `Walden.txt` 文件到我当前登录计算机的家目录。在提示密码后，命令运行；星号行作为进度条。在行末尾，会显示复制的文件总大小和所需的时间。

`scp` 命令使用 `ssh` 创建加密连接，并同样发送加密的文件。如果你已经使用 `ssh` 登录到远程计算机，则需要以不同的方式运行命令：

```
$ scp Walden.txt kirk@10.0.1.202:~/Walden.txt

irk10.0.1.202's password:

Walden.txt 100% |********************************| 567 KB 00:00
```

在这种情况下，我实际上已经在远程计算机上并发起了 `ssh` 连接，因此我将文件发送到我物理所在的计算机，即 `10.0.1.202`。如果你想从一台计算机复制目录到另一台计算机，必须使用 `-r`（递归）选项。这里是一个示例：

```
$ scp -r Texts kirk@10.0.1.202:~/Desktop/

kirk10.0.1.202's password:

A Week 100% |********************************| 655 KB 00:01

Cape Cod 100% |********************************| 422 KB 00:00

Civil_Disobedience.h 100% |********************************| 52310 00:00

Dispersion of Seeds 100% |********************************| 312 KB 00:00

Life_without_Principle 100% |********************************| 44883 00:00

Walden 100% |********************************| 567 KB 00:01

Walking.htm 100% |********************************| 69301 00:00
```

命令执行，并为每个文件显示一行，包含其进度、大小和所需的时间。

## 命令行操作

## scp 命令概述

### 命令语法

```
scp [user@host:]source [user@host:]destination
```

## FINDER 中的等效操作

复制到网络卷，尽管 `scp` 提供了安全的（加密）复制。

## SCP 选项概述

`scp` 命令通过 `ssh` 命令将文件复制到远程计算机。

- `-r` 此选项告诉 `scp` 命令复制目录及其所有内容。

### 获取更多信息

要显示帮助页并了解更多关于 `scp` 的信息，请在终端中输入 `man scp`。

## 动手实践：另一种远程复制文件的方法

还有另一种从远程计算机复制文件的方法，尽管它并不总是有用。记住，你可以在远程计算机上运行命令，可以通过发起 `ssh` 连接或通过 `ssh` 运行单行命令（onesliners）。如果你运行单行命令，且你的命令涉及输出重定向，你可以简单地将输出重定向到你正在工作的计算机上。

这里有一个使用 `cat` 读取文件并将输出重定向到你计算机的简单命令：

```
$ ssh kirk10.0.1.201 Walden.txt ~/Desktop/Walden.txt
```

## 命令行操作

## rsync 命令概述

### 命令语法

```
rsync [option(s)] [user@host:]source [user@host:]destination
```

## FINDER 等效功能

无。某些第三方备份程序具有类似的功能。

## RSYNC 选项概述

- `- rsync`: `rsync` 命令在源和目标之间之间同步目录及其内容。它可以在本地运行，也可以在本地计算机与远程计算机之间运行。
- `- ssh`: 此选项告诉 `rsync` 命令通过 `ssh` 建立安全连接。
- `-a`: 此选项告诉 `rsync` 命令使用一组默认值，以保留所有者、用户组、权限等信息。这等同于使用 `-vlogtp` 选项。
- `-v`: 此选项告诉 `rsync` 命令进入详细模式，并提供有关所复制内容的详细信息。
- `-z`: 此选项告诉 `rsync` 命令使用 `gzip` 压缩文件。
- `-delete`: 此选项告诉 `rsync` 命令删除目标中任何在源中不存在的文件。

### 获取更多信息

要显示手册并了解更多关于 `rsync` 的信息，请在 Terminal 中输入 `rsync`。`rsync` 命令非常强大，拥有数十个选项，允许你排除文件、删除文件、忽略目标中更新的文件、为复制的文件添加特定后缀等。前面的示例展示了使用 `rsync` 的基础知识；如果你计划使用该工具，访问 `rsync` 的 man 页面将非常有帮助。

在示例中，`rsync` 检查五个文件，将它们与目标进行比较，并仅复制新文件。但由于《自我之歌》的作者沃尔特·惠特（Walt Whitman）并没有住在康科德（Concord），因此这个文件不属于那里。如果我从源目录中删除了它，然后再次运行 `rsync` 并添加 `--delete` 选项，就会发生以下情况：

```
$ rsync -e ssh -avz --delete Concordians kirk@10.0.1.201:Public

rsync: open connection using ssh -l kirk 10.0.1.201 rsync -vlogtp --

--delete . Public

kirk@10.0.1.201's password:
```

```
rsync: building file list...

rsync: 4 files to consider.

deleting Concordians/Song_of_Myself.txt

Concordians/

wrote 181 bytes read 20 bytes 17.48 bytes/sec

total size is 638037 speedup is 3174.3
```
