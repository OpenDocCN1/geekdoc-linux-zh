
# 336 使用 Linux 上网

FTP 允许在通过互联网连接的计算机之间传输二进制文件。显而易见，FTP 是与远端同事交换数据的实用方法。然而，FTP 的如此流行归功于匿名 FTP：许多属于大学和互联网提供商的服务器向所有用户开放所谓的 FTP 存档访问。与普通 FTP 不同，它不会被拦截。

当你需要文件时，不知道它存储在哪个服务器上，你可以在以下地址搜索：

`http://ftpsearch.com/`

# ftp 命令

FTP 会话通过 `ftp` 命令启动。由于文件要从/到当前目录传输，你应该首先使用 `cd` 进入所需的目录。在调用 `ftp` 时，需要指定 FTP 服务器所需的互联网地址。

在建立连接并输入用户名和密码后，你就准备好了；你可以使用与 Linux 下含义相同的 `cd`、`pwd` 和 `ls` 命令在 FTP 存档中穿行。为了将文件从 FTP 存档传输到计算机当前目录，执行 `get`。文件名保持不变。相反，你可以使用 `put` 将当前目录的文件传输到 FTP 存档中。（显然，这只有在你拥有该目录写入权限时才可行。对于匿名 FTP，这通常限于名为 `/public/incoming` 的单个目录）。

在传输文件之前，你必须先用二进制切换到模式。在文本模式下，FTP 将文件解释为文本并尝试将其转换为当前计算机的格式。二进制文件通过这种转换将失效。（幸运的是，大多数 FTP 服务器都配置为二进制为默认设置。）

FTP 会话通过 `quit` 或 `bye` 命令终止。下表总结了在 FTP 会话期间可以执行的最重要命令：

| 命令 | 说明 |
| :--- | :--- |
| `?` | 列出所有 FTP 命令 |
| `!` | 允许执行 shell 命令 |
| `ascii` | 切换到文本模式 |
| `binary` | 切换到二进制模式 |
| `bye` | 终止 FTP |
| `cd` | 进入指定的目录 |
| `close` | 与 FTP 服务器的连接 |
| `get` | 从 FTP 存档传输文件到当前目录 |
| `help` | 显示指定命令的简要介绍 |
| `ls` | 显示文件列表 |
| `mget *.pattern` | 从 FTP 存档传输所有匹配的文件到当前目录 |

## 文件传输协议 (FTP) 337

- `open` 与主机建立连接（如果首次尝试失败）
- `put file` 将文件从当前存档传输到 FTP 存档
- `quit` 终止 FTP
- `user` 允许新登录（如果首次尝试失败）

## 示例

以下示例展示了如何从 FTP 服务器 `ftp.redhat.com` 拷贝 PPP 软件包 2。由于空间限制，屏幕上显示的一些文本和目录仅显示了部分。为了提高可读性，所有接收到的文本相对于用户输入都缩进了几个字符。

![](img/b30873dd3d753687a59253fb9ad26a0b_364_0.png)

尽管文本经过了精简，但示例显示在 FTP 会话期间会显示大量的文本。因此，请尝试在 X shell 窗口或 Emacs 的 shell 模式下工作，在这些环境下你可以滚动查看已显示的文本会话。FTP 会话中无法使用 `less` 命令。

```
user$ ftp.redhat.com.
Connected to speedy.redhat.com.
Please use a mirror if possible
```

| FTP站点 | 目录 |
| :--- | :--- |
| `ftp.gwdg.` | `/linux/install/redhat` |
| ... | |

`speedy.redhat.com` FTP 服务器 (Version-2.4.2-academ[BETA-9])(1)

Feb 29 15:50:44 EST 1996) ready.

Name (`ftp.redhat.com:kofler`): anonymous

331 Guest login ok，请发送您的完整电子邮件地址作为密码。

Password: > kofler@ftp.at

欢迎来到 Red Hat Software Linux 存档。

当前有 72 个用户在使用 ftp 存档。

访登录允许，受限制。

远程系统类型为 Unix。

正在使用二进制模式传输文件。

```
ftp> ls
---
dwxfxxr-xr 3 root root       1024 May 24 20:26 mirrors
dwxfxxr-xr 5 506 506      1024 May 21 14:23 pnp
dwx--x--x 3 root root       1024 May 27 17:10 private
dwxfxxr-xr 15 root root       1024 Jun 5 16:16 pub
dr-xr-xr-x 3 root root       1024 Sep 9 1994 usr
```

## 338 使用 Linux 接入互联网

```
ftp> cd pub
请阅读 README 文件
该文件最后修改于 1996年3月15日周五 17:30:04 - 83天前
ftp> ls

drwxr-xr-x 10 504 504 1024 Jun 5 21:08 contrib
drwxr-xr-x 2 root root 1024 May 31 21:07 current
drwxr-xr-x 7 root root 1024 May 9 18:38 devel

ftp> cd contrib/RPMS
ftp> ls *

-rw-rw-r-- 15 504 504 19428 Mar 1 01:17 portmap-3.0-1.1386.rpm
-rw-rw-r-- 1504 504 707936 Feb 8 22:02 postgres95-1.0-2.1386.rpm
-rw-rw-r-- 1504 504 81095 May 28 00:02 ppp-2.2.of-1.1386.rpm
-rw-rw-r-- 1504 504 82548 May 17 22:55 privtool-0.96-1.1386.rpm
-rw-rw-r-- 1504 504 11003 Apr 3 22:24 prometer-1.1-1386.rpm
```

```
ftp> get ppp-2.2.of-1.1386.rpm
PORT 命令成功。
正在打开 BINARY 模式连接传输 -2.2.of-11386.rpm (81095 字节)。
传输完成。
81095 字节耗时 28.3 秒 (2.8 KB/sec)
ftp> bye
```

为了尽可能减少传输的数据，FTP 服务器上的文件通常使用 `compress` 或 `gzip` 进行压缩。唯一的例外是较小的文本文件。传输完成后，必须使用 `gunzip` 或 `compress` 来解压文件。

## 现代 FTP 客户端

使用 `Netscape`、`gftp`（GNOME FTP 客户端）、`gmc` 和 `kfm` 程序访问匿名 FTP 服务器比使用 `ftp` 命令简单得多：你只需指定 FTP 服务器的地址而不是 WWW 地址。请使用正确的语法（此处是 RedHat FTP 服务器的示例）：
