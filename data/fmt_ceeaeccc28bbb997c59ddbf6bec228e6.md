
其中 `host` 可以是具有您要显示的首页的计算机的完全限定域名或 IP 地址（以 DDN 表示），`page` 是包含要显示页面的文件的路径名——例如，`http://cnn.com`、`http://www.stroustrup.com`、`http://mitadmissions.org/index.php` 和 `http://profiles.stanford.edu/russ-altman`。客户端尝试与 URL 对应的站点上的 `http` 服务器进程建立连接。如果站点正在运行 `http` 服务器并且没有诸如密码之类的安全保护，则在客户端和服务器之间建立连接。然后服务器将网页发送给客户端，客户端将其显示在屏幕上，任何音频或视频组件都会发送到相应的设备。请注意，如果您想通过浏览器访问 `ftp` 站点，可以用 `ftp` 替换 `http`，或者如果您想通过 Secure Shell（SSH）协议远程登录，可以用 `ssh` 替换。

您可以通过使用相应的命令来调用大多数互联网服务的大多数客户端程序，例如 `ssh` 用于 SSH 服务，`ftp` 用于 FTP 服务。其中大多数命令允许将服务器运行的主机的域名或 IP 地址作为命令的参数。一些命令还允许端口号作为参数。具有这种灵活性的客户端软件被称为完全参数化客户端。这类客户端在提供的灵活性方面很重要。它们还允许通过在不为人知的端口上运行更新的服务器软件并使用客户端联系它来测试更新的服务器软件。`telnet` 客户端是一个很好的完全参数化客户端的例子，在第 11.8 节中讨论。

## 11.8 应用软件

在 UNIX 主机的网络上，有许多实现刚才讨论的应用层协议的程序可用。在这里描述的最常用的应用程序中，其中一些仅在基于 UNIX 和 Linux 的系统上可用，而另一些则可供互联网上的所有主机使用。

TABLE 11.3 Popular Internet Services and Corresponding Protocols

| Service | Protocol |
|---|---|
| Electronic mail | SMTP (Simple Mail Transfer Protocol) |
| File transfer | FTP (File Transfer Protocol) |
| Remote login | SSH (Secure Shell) and TELNET |
| Web browsing | HTTP (Hyper Text Transfer Protocol) and HTTPS (HTTP Secure) |

![](img/02e070097d401d3bf7de4bf1c470b267_447_0.png)

FIGURE 11.7 Depiction of the client–server software model.

## 11.8.1 显示主机名

基于网络的应用程序使用 `user@host` 地址格式来在 Internet 上的网络中标识一个用户。你可以使用 `hostname` 和 `uname` 命令来显示你当前登录的主机的名称。在某些系统上，主机名以简短的简单名称格式显示，而在其他系统上则以长格式的 FQDN 显示。如果你必须识别你在网络上登录的主机，可以使用 `hostname -s` 命令来显示简短格式，它只是主机名，即 FQDN 格式中最左边的字符串。某些系统不允许你在使用 `-s` 选项，除非你是超级用户。你可以使用 `uname -n` 命令以 FQDN 格式显示你当前登录的计算机的主机名。`uname -a` 命令显示有关主机的完整信息，包括其运行的操作系统和 CPU 的名称。在 Solaris 上，你可以使用 `-X` 选项按行显示扩展信息，每行一项。以下是 Solaris 上 `hostname` 和 `uname` 命令的一些示例。

```
$ hostname

solarissrv

$ uname -n

solarissrv

$ uname -a

SunOS solarissrv 5.11 11.2 i86pc i386 i86pc

$ uname -X

System = SunOS

Node = solarissrv

Release = 5.11

KernelID = 11.2

Machine = i86pc

BusType = <unknown>

Serial = <unknown>

Users = <unknown>

OEM# = 0

Origin# = 1

NumCPU = 4

$
```

以下是 PC-BSD 上 `hostname` 和 `uname` 的示例运行。

```
% hostname

pcbsd-srv

% uname -n

pcbsd-srv

% uname -a

FreeBSD pcbsd-srv 10.0-RELEASE-p6 FreeBSD 10.0-RELEASE-p6 #0

acf484b(releng/10.0) : Mon Feb 24 15:14:38 EST 2014 root@avenger:/usr/obj/root/pcbsd-build-10.0-EDGE/git/freebsd/sys/GENERIC amd64

%
```

## 11.8.2 显示使用网络主机的用户列表

你可以使用 `rwho`（remote who，远程 who）命令来显示当前使用你网络上机器的用户的相关信息。此命令的输出类似于 `who` 命令的输出。输出行包含用户的登录名、用户登录的计算机和终端，以及登录的日期和时间。最后一个字段为空，表示用户当前正在终端上输入；否则，它显示用户上次在键盘上输入后的小时数和分钟数。你可以使用 `-a` 选项与 `rwho` 命令一起使用，以包含当前处于空闲状态的用户。以下会话显示了该命令的示例输出。

```
$ rwho | more

bobk      upibm7:ttyC4      Jul 26 12:03

dfrakes   upibm47:ttyp2     Jul 26 11:49

lulay     upsuni7:pts/0      Jul 26 10:17

oster     upsuni7:pts/2      Jul 26 12:28

sarwar    upibm7:ttyp2      Jul 26 11:15

$
```

你可以使用 `rusers`（remote users，远程用户）命令来显示登录到本地网络上的机器的用户的名称。当前使用某台机器的用户的登录名按每台机器一行显示。以下是该命令的简要说明。

### SYNTAX

```
rusers [options] [host_list]
```

Purpose: Display the login names of the users logged on to all the machines on your local network

Output: Information about the users logged on to the hosts on your local network, one line per machine

Commonly used options/features:

- `-a` Display a host name even if no user is using it
- `-l` Display the user information in a long format similar to that displayed by the `who` command

`rusers` 命令向网络上的所有主机广播查询，询问它们回复用户信息。它收集所有回复并按接收顺序显示信息。以下是该命令的简单运行示例。请注意，主机名显示在 16 个字符的字段中，这就是为什么名称中的 `edu` 部分没有完全显示。正如命令的输出所示，用户 `kent` 在 `upibm8.egr.up.edu` 主机上登录了两次，`sarwar` 登录到 `upsun29.egr.up.edu`，而用户 `kittyt` 和 `deborahs` 登录到 `upibm6.egr.up.edu`，其中 `kittyt` 登录了两次。

```
$ rusers  more

upibm48.egr.up.e  kent  kent
```

你可以通过将主机作为参数指定给 `rusers` 命令来显示登录到特定主机的用户名称。以下命令显示登录到 `upibm7` 主机的用户登录名。

```
$ rusers upibm7

upibm7.egr.up.edu upppp44 upppp upppp26 kathek khnguyen upppp14

leslie sarwar sarwar

$
```

如以下会话所示，你可以使用 `-a` 选项使用 `rusers` 命令，即使没有用户登录到这些主机，也显示主机名称。这样可以让你查出网络上所有主机的名称。

```
$ rusers -a | more

upsun12.egr.up.edu

...

upsun27.egr.up.edu

upibm48.egr.up.edu kent kent

upsun29.egr.up.edu sarwar

upsqnt.egr.up.edu

...
```
