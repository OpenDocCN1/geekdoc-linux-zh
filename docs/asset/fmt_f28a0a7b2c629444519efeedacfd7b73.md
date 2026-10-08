
TCP compression code copyright 1998 Regents of the University of California

PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.

PPP line discipline registered.

你应该能看到类似的行。如果没有，你必须重新编译内核以内置 PPP 支持，或者构建 PPP 模块并使用 `insmod` 命令加载驱动程序。你需要启用网络支持，特别是 TCP/IP。

你需要的另一个软件是位于 `/usr/sbin` 目录下的 `chat` 程序，它是 ppp 守护进程软件包的一部分。`chat` 程序用于拨号过程拨出并连接到你的 ISP 调制解调器。除了 `chat`，你还需要 `pppd` 守护进程，同样安装在 `/usr/sbin/` 目录下。如果安装了 `pppd`，你应该能在 `/etc` 目录下找到一个 ppp 目录，其中包含部分内容：

```
ls /etc
chap-secrets options ppp-on-dialer
connect-errors pp-secrets
ip-up pp-off
```

如果没有看到 `ppp-on` 或 `ppp-on-dialer` 文件，可以从 `/usr/doc/ppp-2.0-3f/scripts` 目录复制它们。

你在本小时将学习的设置需要你修改 `ppp-on` 文件，这是一个可执行脚本。接下来，你可能想检查 `/etc` 目录下是否存在 `resolve.conf` 文件。如果没有，别担心，它是一个包含一两行的简短文件。

最后，你可能想查看系统中是否有 `ifconfig`、`minicom`、`netstat`、`ping` 或 `route` 命令。你以后将需要这些工具对你的连接进行一些测试。

## 你从 ISP 需要的信息

要通过 ISP 使用 PPP 连接到，你显然应该先有一个 PPP 账户。当你注册服务时，你的 ISP 客户代表可能会假设你有一套 Windows 或 Macintosh 系统的设置和软件。如果你说“都不是。我正在使用 Linux”，而得到的回复是空白的眼神、电话那头的沉默或“什么是 Linux？”，不要惊慌！

你可能会幸运。随着 Linux 普及率提高，美国和世界其他许多 ISP 已经认可并支持 Linux 用户。如果你的 ISP 了解 Linux，请询问最低系统要求、任何设置指南或安装技巧。书中附的 CD-ROM 你所需软件的最新稳定版本，所以你再也不用担心。

假设你的 ISP 不了解 Linux，以下是你从 ISP 需要的信息：

- 你的账户信息：用户名（登录名）和密码，以便你可以登录 ISP 的计算机。
- 你的 ISP 的调制解调器拨号号码，以便你可以连接。
- 你的 ISP 是否为你分配静态互联网协议 `IP` 地址，还是动态分配你的 IP 地址（本小时的示例假设了地址，但向你展示了可以在哪里更改为静态 IP 地址）。
- 你的 ISP 主 DNS 和备用 DNS 的 IP 地址和名称。这些信息将进入 `/etc/resolv.conf` 文件（如在“编辑 resolv.conf 文件”节中所解释）。

这些地址将以 8 位数字的形式出现，看起来像：`205.198.114.1` 或 `205.198.114.20`。这些是 ISP 使用或维护的服务器地址（以及其他），用于主机名（例如 `sunsite.unc.edu`）翻译为数字 IP 地址，以便你可以连接、查询或其他世界各地的计算机和用户。本节不涉及 IP 划分机制的细节，本书将涵盖 Linux 下网络的所有方面。

- 你的 ISP 邮件服务器名称或 IP 地址，以便你可以发送邮件。
- 你的 ISP 新闻服务器名称或 IP 地址，以便你可以阅读新闻。你需要第 11 小节“配置电子邮件”。
- 最后，你的 ISP 新闻服务器名称或 IP 地址，以便你可以阅读新闻。你需要第 12 小节“配置新闻”。

## resolv.conf 文件

这是一个简单的过程。首先，确保你以 root 身份登录。然后，在 `/etc` 目录下查找名为 `resolv.conf` 的文件。如果存在，用你喜欢的文本编辑器打开并添加 ISP 的服务器。如果你的 ISP 只有一个，没关系；如果有多个，也没关系。使用以下格式：

```
nameserver 205.198.114.1
nameserver 205.198.114.20
```

关闭文件。就这些！

## 设置连接

我不会进入详细方法，因为我想为你概述最简单的方法并让你快速上网。在获取连接时，我建议查看 `ppp` 的手册页、`/usr/doc/` 下 Robert Hart 的 PPP-HOWTO、`/usr/doc/` 下 Al Longyear 的 PPP-FAQ，或者《Linux 管理员指南》中的相关章节。

你应该执行的第一件事是确保以 root 身份登录。然后，在 `/etc/ppp` 目录下查找名为 `ppp` 的文件。如果存在，创建一个副本（你可以任意命名）或将 `ppp` 重命名为 `ppp-on`。如果没有 `ppp`，请从 `/usr/doc/ppp-2.0-3/scripts` 目录复制它。10.1 显示了由 Al Longyear 编写的脚本部分。

### 10.1. ppp-on 连接脚本。

```
TELEPHONE=555-1212
ACCOUNT=username
PASSWORD=password
LOCAL_IP=0.0.0.0
REMOTE_IP=0.0.0.0
# 连接的电话号码
# 登录账户名（如 'George Burns'）
# 此账户的密码（以及 'Gracie Allen'）
# 已知的本地 IP 地址。动态 = 0.0.0.0
# 如果所需的远程 IP 地址。通常为 0.0.0.0
```

```
DIALER_SCRIPT=/etc/ppp/ppp-on-dialer
exec /usr/sbin/ppp lock modem crts /dev/modem 57600 \
asyncmap 200A0000 escape FF SLOCK_IP:$REMOTE_IP \
noipfault netmask SNETMASK defaultroute connect \
DIALER_SCRIPT=$&
```

## 第 10 小时

你需要修改此脚本的几个部分。大部分情况下，你只需要进行几处更改。一些关键元素如下：

- `TELEPHONE`—在此处输入你的 ISP 调制解调器连接号。
- `ACCOUNT`—输入你的用户名或登录（通常由你的 ISP 分配）。
- `PASSWORD`—在此处输入你的密码（通常由你的 ISP 分配）。
- `DIALER_script`—你的拨号脚本程序的完整路径。`chat` 程序将为你完成拨号、连接和登录。如果你找不到这个名为 `ppp-on-dialer` 的脚本副本，请在 `/usr/doc/ppp-2.2/scripts` 目录下查找（列表 10.2 显示了 ppp-on-dialer 脚本）。注意，如果你的 ISP 计算机没有显示 `name:` 提示符，你必须更改此脚本中的 `login:` 和 `password:` 字符串，以与你 ISP 提供的内容匹配。

### 10.2. ppp-on-dialer 拨号脚本。

```
exec chat -v
TIMEOUT 3
ABORT '\nBUSY\r'
ABORT '\nNO ANSWER\r'
ABORT '\nRINGING\r\r\nRINGING\r\r\nAT'
'OK-+++c-OK' ATH0
TIMEOUT 30
OK ADDTSTEPHONE
CONNECT /\nlogin: SCOUNT
password: SPASSWORD
```

接下来，检查 `ppp-on` 脚本中的 ppp 命令，并将 `/dev/modem` 修改为你的调制解调器连接的设备。如果你愿意，可以使用第 9 小时“使用通信程序”中概述的方法，从调制解调器的串口端口到 `/dev/modem` 创建符号链接。这里有一个提示：如果你有一个 14.4 的调制解调器，使用 `19200` 作为数值；如果你有 28.8 或 33.6 的调制解调器，尝试 `57600`。你可能会连接到更快的速度，特别是使用较新的调制解调器时。

如果你的 ISP 分配 IP 地址（动态 IP 地址或每次登录都可能不同的地址），那么你就准备好了。但如果你必须连接到特定的（静态或固定）IP 地址，你需要从 ppp 命令中移除 `nodefault` 选项，并将 `REMOTE_IP` 字符串更改为 ISP 提供的 IP 地址（你可以在 ppp 命令中更改或在脚本上方的 `REMOTE_IP` 变量中更改）。

最后，确保 `ppp-on` 和 `ppp-on-dialer` 脚本是可执行的，可以通过 `ls -l` 检查或使用 `chmod` 程序进行修改：

```bash
# chmod +x /etc/ppp/ppp-on*
```

假设你的调制解调器已连接到电脑，电话线已连接到调制解调器，你现在可以尝试连接了。

## 启动和停止 PPP 连接

本节介绍了如何连接到你的 ISP 并启动 Internet 会话。有几种方法可以实现。你看到的第一个方法是最基础、最简单的方法，即使用 `minicom` 程序连接而不使用你刚刚创建的脚本。你将学习如何使用 PPP 连接脚本 `ppp-on`。

> 在第 9 小时讨论的 `minicom` 程序是一种通信程序。你可以使用它拨出连接到其他计算机或信息服务，例如公告板系统（BBS）。更多信息请参阅 `minicom` 手册页。

请稍候

### 使用 minicom 连接

使用 `minicom` 连接 ISP 有一个优势，因为你的账户和密码不会记录在 `/var/log` 目录下的系统日志中。你每次上网都可以使用 `minicom`，但你可能会觉得这个过程很麻烦。我向你展示这种方法是因为你可能会发现它对于验证你在 `ppp-on-dialer` 脚本中指定的登录和密码输入是否有效很有用。

以下是步骤。你可以这样做是因为 `minicom` 可以在退出时不重置你的调制解调器。你可以使用 `minicom` 拨号、连接然后退出，允许你使用 ppp 守护进程启动 PPP 会话。方法如下：

1. 运行 `minicom`。
2. 输入 `ATDT`，后面跟着你的 ISP 调制解调器号码。
3. 等待连接和 ISP 的提示，然后使用用户名和密码登录。注意登录和密码提示符是否不同。如果是，把它们记下来，这样你就有所需的信息来编辑 `ppp-on-dialer` 脚本中的 `chat` 程序选项了。
4. 按 `Ctrl+Q` 退出 `minicom` 而不重置调制解调器。
5. 在命令行输入以下内容：

```bash
# pppd -d detach /dev/modem &
```

几秒钟后，你就连接上了！（嗯，你应该先检查——然后验证）。

### 使用 ppp-on 脚本连接

使用 `ppp-on` 建立连接非常简单。命令将显示通过你的 PPP 接口接收和发送的字节数（数据包形式）。

### 停止 PPP 连接

命令将列出当前活动的网络接口。停止你的会话。

### 检查连接

你可以通过几种方式对连接进行诊断、故障排除或获取更多信息。你还可以检查系统日志，查看启动或断开期间发生的任何问题。

### 使用 ifconfig 命令

虽然位于 `/sbin` 目录下的 `ifconfig` 命令通常用于网络管理中的接口配置（该技能在书中未涵盖；请参考《Linux 网络指南》），但你可以使用 `ifconfig` 查看 PPP 连接的状态。

当你运行某些程序（例如新闻阅读器）时，这个命令可能有用，这些程序看起来可能“冻结”，但但实际上正在接收未显示在屏幕上的数据。

### 使用 netstat 命令

`netstat` 命令是检查网络活动、连接、路由表以及其他网络统计数据的权威命令。如果你对灵活列运行列表感兴趣，你会想尝试它。例如，你可以尝试（以下示例输出为简略）：

# 170

## netstat

活跃的 Internet 连接（不含服务器）

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 1 | | localhost:1644 | localhost:1322 | CLOSE_WAIT |
| tcp | 0 | | localhost:2579 | localhost:6000 | ESTABLISHED |
| tcp | 0 | | serial52.statnet.com:~4216 | megan.statnet.com:pop | ESTABLISHED |

活跃的 UNIX 域套接字（不含服务器）

| Proto | RefCnt | Flags | Type | State | I-Path |
| :--- | :--- | :--- | :--- | :--- | :--- |
| unix | 2 | [] | STREAM | CONNECTED | 417 |

```
unix 2 [] STREAM 419 /dev/log
unix 2 [] STREAM CONNECTED 1982
unix 2 [] STREAM 1983 /dev/log
```

`netstat` 命令有十多个命令行选项。更多信息请参阅 `netstat` 帮助页。

## 使用 ping 命令

`ping` 命令用于验证您的 ISP IP 地址是否有效，并测试你的 ISP 主机服务器的响应时间。`ping` 发送数据包并测量主机发送此类信息所需的时间——例如：

```
# statnet.com
PING stat.207.226.80.1: 64 data bytes
64 bytes from 207.226.80.1: icmp_seq=0 ttl=254 time=176.9 ms
64 bytes from 207.226.80.1: icmp_seq=1 ttl=254 time=180.0 ms
64 bytes from 207.226.80.1: icmp_seq=2 ttl=254 time=170.0 ms
64 bytes from 207.226.80.1: icmp_seq=3 ttl=254 time=170.0 ms
64 bytes from 207.226.80.1: icmp_seq=4 ttl=254 time=170.0 ms
64 bytes from 207.226.80.1: icmp_seq=5 ttl=254 time=170.0 ms
64 bytes from 207.226.80.1: icmp_seq=6 ttl=254 time=169.7 ms
```

statnet.com ping 统计

7 packets transmitted, 7 packets received, 0% packet loss

round-trip min/max = 169.7/172.3/180.0 ms

默认情况下，它会继续发送和接收信息，直到你按 Ctrl+C 停止。你还应该知道，`-f` 或 `flood` 对你的 ISP（或任何其他计算机）并不是什么好的做法，因为它会产生网络开销和不的网络流量。

## 使用 route 命令

`route` 命令用于为接口设置或删除网络路由，在查看你的 ppp0 接口发生的情况时也很有用。你可以尝试以下命令：

```
# /bin/route
```

| Kernel IP table | Genmask | Flags | Metric | Ref | Use | Interface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Destination Gateway | pm2.statnet.com | * | 255.255.255.255 | UM | 0 | 0 ppp |
| 127.0.0.0 | 255.0.0.0 | U | 0 | 0 | 2 lo |
| default | pm2.statnet.com | 0.0.0.0 | | | | pp

## 连接互联网

关于 `route` 命令的更多细节，请参阅你的帮助页。

## 读取系统日志

如果你想详细了解脚本执行执行时发生了什么，请查看你的系统日志、`messages` 文件或 `/var/log` 目录。尝试：

```
# less /var/log/messages
```

在 `ppp-script` 中寻找 ppp 守护进程的启动。注意你的拨号脚本使用了 `chat` 程序，它完成了大部分工作后退出，随后由 `ppp` 获取并设置网络 IP 地址。
