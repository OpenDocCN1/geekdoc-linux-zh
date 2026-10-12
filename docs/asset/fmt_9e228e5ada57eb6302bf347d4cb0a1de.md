
许多应用程序是面向连接的客户端—服务器模型，其中客户端向服务器发送连接请求，由服务器决定接受或拒绝该请求。如果服务器接受了请求，客户端和服务器将通过虚拟连接建立。从这一点起，客户端发送客户端请求，服务器向客户端发送响应。客户端与相应服务器之间的通信以及客户端与用户的交互，都由应用程序所提供的服务协议决定。图 11.7 显示了客户端—服务器软件模型的概述。

然后，当你运行如 `Firefox` 这样允许你浏览网页程序时，客户端运行的主机上会启动一个 `http` 客户端进程，尽管它可以设置为任何页面（包括空白页）。当你想要查看某个网站的网页时，你将拥有该页面的网站组织的统一资源定位符（`URL`）提供给客户端进程。对于显示主页，`URL` 具有：

```
http://host/page
```

其中 `host` 是具有你要显示的主页的的 `FDN` 或 `IP` 地址（在 `DDN` 中），`page` 是包含要显示页面的文件路径——例如 `cnn.com`、`www.stroustrup.com`、`mitadmissions.org/index.php` 以及 `http://profiles.stanford.edu/`。客户端尝试与网络上的 `http` 服务器进程建立连接。如果该网站有 `http` 服务器且没有设置密码等安全保护，则客户端和服务器之间将建立连接。然后服务器将网页发送给客户端，由客户端在屏幕上显示，任何音频或视频组件将发送到相应的设备上。请注意，如果你想通过浏览器访问 `https` 站点，可以将 `http` 替换为 `https`；如果你想通过安全外壳（`SSH`）协议进行远程登录，则可以替换为 `ssh`。

你可以使用相应的命令调用大多数 Internet 服务的客户端程序，例如用于 `SSH` 进程的 `ssh` 和用于 `FTP` 服务器的 `ftp`。这些命令允许指定一个域

![](img/2a18e06cd9c6395e451f26126ecba1fd_317_0.png)

图 11.7 客户端—服务器软件模型的描绘。

## Linux

在命令中使用运行服务器的主机主机名或 `IP` 地址作为参数。命令还允许将端口号作为参数。内置了这种灵活性的客户端软件是 `全参数化客户端`。从提供的灵活性角度来看，客户端非常重要。它们还允许通过在为人知的端口上运行更新的服务器软件并使用客户端与其连接来对其测试。第 11.8 节中讨论的 `telnet` 客户端是 `全参数化客户端` 的一个良好示例。

### 11.8 应用软件

在 `Linux` 主机网络上，提供了许多实现上述应用层协议的程序。在本文描述的最常用应用程序中，某些适用于 `Linux` 和基于 `Linux` 的系统，而另一些适用于 Internet 上的所有主机。

#### 11.8.1 显示主机名

基于网络的应用程序使用 `user@host` 地址格式来识别 Internet 网络上的用户。你可以使用 `hostname` 和 `uname` 命令来显示你所登录的主机名称。在某些系统上，主机名以短、简单的格式显示，而在另一些系统上，它以完整的 `FQDN` 格式显示。如果你识别了你所登录的网络上的主机，可以使用 `hostname -s` 命令显示短格式，它只是主机的名称（`FQDN` 格式中最左侧的部分）。你可以使用 `uname -n` 命令将你登录的计算机名称以 `FQDN` 格式显示。`uname -a` 命令显示关于主机的完整信息，包括其运行的操作系统和 `CPU` 的名称。以下是 `hostname` 和 `uname` 命令的一些示例。

```
$ hostname
Mint18
$ uname -n
Mint18
$ uname -a
Mint18 4.4.0-21-generic #37-Ubuntu SMP Mon Apr 18 18:33:37 UTC 2016 x86_64 x86_64 GNU/Linux $
```

你可以使用 `arch` 命令查找处理器架构。该命令输出的信息与 `uname -m` 相同，如下会话所示。

```
$ arch
x86_64
$ uname -m
x86_64 $
```

询问你的朋友和同学，关于他们最常用的两个网络服务。它们是哪些服务？哪一个最多？

#### 11.8.2 测试连接

你可以使用 `ping` 命令测试网络或特定主机的状态。如果 `ping` 命令在你的系统上不起，请使用 `ping` 查找其位置。以下是 `ping` 的简要描述。

##### 语法：`ping [options]`

`目的`：向主机发送 `IP` 数据报文以指示主机是否存活。

`常用选项`：

- `c`: 发送包的数量
- `f`: 每秒发送包的数量
- `s`: 发送包的大小
- `t`: 发送直到超时

你可以使用主机的 `IP` 地址来代替其主机名。例如，你可以使用 `ping 171.67.215.200` 而不是 `ping stanford.edu`，如下：

```
$ ping 171.67.215.200
PING 171.67.215.200 (171.67.215.200) 56(84) bytes of data.
64 bytes from 171.67.215.200: icmp_seq=1 ttl=231 time=617 ms
64 bytes from 171.67.215.200: icmp_seq=2 ttl=231 time=312 ms
64 bytes from 171.67.215.200: icmp_seq=3 ttl=231 time=437 ms
64 bytes from 171.67.215.200: icmp_seq=4 ttl=231 time=398 ms
64 bytes from 171.67.215.200: icmp_seq=5 ttl=231 time=438 ms
---
 171.67.215.200 ping statistics
5 packets transmitted, 5 received, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 31.828/41.048/67.665/92.43 ms
$
```

#### 11.8.3 显示用户信息

你使用 `finger` 命令显示本地或远程主机上的用户信息。显示的信息是从 `~/plan` 和 `~/project` 文件中提取的。默认情况下，你的 `Linux` `Mint` 系统没有安装 `finger` 命令。如果你的 `Linux` 系统没有提供 `finger`，请参阅附录 `A` 在你的系统中安装的说明。以下是该命令的简述。

```
语法：finger [options] [user-list]
用途：显示 user_list 中用户的信息；如果没有 user_list，命令将显示当前登录到指定主机的所有用户的状态报告
输出：从 ~/project 和 ~/plan 文件中提取的用户信息
常用选项/功能：
-m 将 user_list 仅匹配到登录名
-s 以短格式输出
```

以下会话展示了该命令最简单的用法，显示主机上用户 `bob` 的信息。

```
$ finger bob
Login: bob Name: Robert Koretsky
Directory: /home/bob Shell: /bin/bash
 Oct 15 20:21 (PDT) on pts/1 103.255.5.99
1 hour 39 minutes idle
once Sun Oct 15 21:53 (PDT) on pts/0 103.255.5.99
3 seconds idle
No mail.
No Plan.
$
```

你可以使用带有 `-s` 选项的 `finger` 命令以短格式显示命令的输出，并使用 `-m` 选项将 `user_list` 仅匹配到登录名。如果用户名为 `tree`（网络命令认为字母大小写相同），则 `finger -m` 命令显示的信息与 `finger birch` 相同。然而，如果用户的登录名为 `btree` 且系统中不存在登录名 `birch`，`finger` 命令将显示相应的消息通知你。

在不带任何参数运行时，`finger` 命令会返回当前登录到你机器的所有用户的状态。显示的信息量略有不同，取决于你的主机运行的 `Linux` 系统。以下命令运行在 `Linux-Networking` 和 `Internetworking` 上：

`finger`

| 登录名 (Login) | 姓名 (Name) | 终端 (T) | 空闲 (Idle) | 登录时间 (Login Time) | 办公室 (Office) | 电话 (Phone) |
|---|---|---|---|---|---|---|
| `bob` | `bob` | `tty8` | `12:37` | `Jul 25 17:53` | `(:)` | |
| `malik` | `Malik` | `tty8` | `86d` | `Jul 21 18:54` | `(:)` | |
| `root` | `root` | `tty1` | `2d` | `Jul 25 08:12` | | |
| `sarwar` | `Mansoor Swar` | `pts/1` | `1:42` | `Oct 15 20:21 (103.255.5.99)` | | |

$
