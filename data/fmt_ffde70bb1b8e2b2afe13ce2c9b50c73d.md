
UP BROAD LOOPBACK RUNNING MTU:3584 Metric:1

RX packets: 1620 errors:0 dropped:0 overflows:0

TX packets: 1620 errors:0 dropped:0 overflows:0

eth0 Link encap:10Mbps Ethernet HWaddr 00:00:09:85:AC:55

net addr:199.1.2.10 Bcast:199.1.2.255 Mask:255.255.255.0

UP BROADCAST MULTICAST MTU:1500 Metric:1

RX packets: 0 errors:0 dropped:0 overflows:0

TX packets: 0 errors:0 dropped:0 overflows:0

Interrupt:12 Base address:0x310

eth1 Link encap:10Mbps Ethernet HWaddr 00:00:09:80:1E:D7

net addr:192.168.2.1 Bcast:192.168.2.255 Mask:255.255.255.0

UP BROADCAST MULTICAST MTU:1500 Metric:1

RX packets: 0 errors:0 dropped:0 overflows:0

TX packets: 0 errors:0 dropped:0 overflows:0

Interrupt:15 Base address:0x30

你的路由表应该像这样：

```
#route -n

Kernel routing table

Destination Gateway Mask Flags MSS Window Use Iface

199.1.2.0 * 255.255.255.0 U 1500 0 15 eth0

192.168.2.0 * 255.255.255.0 U 1500 0 0 eth1

127.0.0.0 * 255.0.0.0 U 3584 0 2 lo

* * 0 1500 0 72 eth0
```

`199.1.2.0` 是预留的，我们将在示例中使用它。`192.168.2.0` 是私有网络。`199.1.2.1` 是你的代理/网关 IP 地址。

## 7. 安装 TIS 服务器

```
/sbin/ipfwadam -A out -i -S 0.0.0.0/0 -D 196.1.2.0/24
/sbin/ipfwadam -A in -i 196.1.2.0/24 -D 0.0.0.0/0
/sbin/ipfwadam -A in -i -S 0.0.0.0/0 -D 196.1.2.0/24
```

如果你只需要一个过滤防火墙，那么可以到此为止了。祝你愉快 :-

## 7 安装 TIS 代理服务器

### 7.1 获取软件

TIS FWTK 可以在 `ftp://ftp.tis.com` 获取。
不要犯像我犯过的那个错误。当你从 TIS ftp 下载文件时，请**阅读** README 文件。TIS 的 fwtk 被锁定在他们系统中一个隐藏目录中。TIS 要求你向 `ftp-request@tis.com` 发送邮件，正文只需包含 `SEND` 一个单词即可获取该隐藏目录名称。邮件不需要主题，随后他们会发给你目录名称（有效期 12 小时）以便你下载源码。

在我写这些内容时，他们正在发布 FWTK 的 2.0 (beta) 版本。这个版本看起来编译良好（除了所有例外情况），并且在我这里运行正常。这是我在这里编译的版本。等最终代码准备就绪，我会更新 HOWTO。

要安装 FWTK，请在你的 `/usr/src` 中创建一个 `fwtk-2.0` 目录。将你的 FWTK 副本 (`fwtk-2.0.tar.gz`) 到该目录并解压：`tar -xzf fwtk-2.0.tar.gz`。

FWTK 不代理 SSL 文档，但有一个由 Jean-Christophe Touvet 编写的插件。它可以在 `ftp://ftp.edelweb.com/pub/contrib/fwtk/ssl-gw.tar.Z` 获取。Touvet 不支持此项。

我使用的是一个修改过的版本，它包含了 Eric Wedel 编写的对 Netsecure 服务器的访问。它可以在 `/fdi/meridian-data.com/ftp/fwtk/ssl/ssl-gw-2.tar.Z` 获取。

在示例中，我将使用 Eric Wedel 的版本。
要安装它，只需在你的 `/usr/src/fwtk-2.0` 中创建一个 `ssl-gw` 目录并将文件放入其中。

当我安装它时，它需要进行一些更改才能与工具包的其他部分一起编译。
第一个更改是 `ssl-gw.c` 文件。它没有包含一个必要的头文件。

```c
#if defined(__linux)
#include <sys/ioctl.h>
#endif
```

其次，它没有制作 Makefile。我从网关目录复制了一个，并将网关名称替换为 `ssl-gw`。

### 7.2 编译 TIS FWTK

FWTK 2.0 版本的编译比旧版本容易得多。我仍然发现了一些在 BETA 版本能够干净编译之前需要更改的地方。希望这些更改会在最终版本中完成。

为了修复它，通过开始修改 `/usr/src/fwtk/fwtk` 目录并复制 `Makefile.config linux` 文件，可以生成 `Makefile.config` 文件。

**不要运行 MAKE**。说明书中要求你运行它。如果你运行了，它会破坏每个目录中的 Makefile。
我有一个该问题的解决方法。问题在于 sed 脚本会添加一个 ' ' 并包含每个 Makefile 的该行。这个 sed 脚本是有效的。

```bash
sed 's/^/include[^\]*\ \(.*\)/include \1/' $name .proto > $name
```

接下来我们需要编辑 `Makefile.config` 文件。你可能需要做两个更改。
作者将源码目录设置为家目录。我们在 `/usr/src` 中编译代码，所以你应该更改 `FWKTSCDRID` 变量来修复它。

```
FWKTSCDRID=/usr/src/fwtk/fwtk
```

其次，至少 Linux 系统使用 gdbm 数据库。`Makefile.config` 使用的是 dbm。你可能需要更改此。我在 RedHat 3.0.3 上必须这么做。

```
DBMLIB=-1gdbm
```

最后一个修复在 x-gw 中。BETA 版本的 bug 在 `socket.c` 中。要修复它，请删除这些行代码。

```c
#ifdef SCM_RIGHTS /* 4.3BSD Reno and later */
      + sizeof(un_name->sun_len) + 1
#endif
```

如果你将 `ssl-gw` 添加到了你的 FWTK 源码目录，你需要将它添加到 Makefile 中的目录列表中。
`DIRS= smap smapd netac-pug-gw ftp-gw tn-gw login-gw http-gw x-gw ssl-gw`

现在运行 make。

### 7.3 安装 TIS FWTK

运行 `install`。
默认安装目录是 `/usr/local/etc`。你可以更改它（我没有改）到一个更安全的目录。我选择将该目录的访问权限改为 `chmod 700`。
现在剩下的工作就是配置防火墙。

### 7.4 配置 TIS FWTK

现在才真正开始。我们必须测试系统以调用这些新服务，并创建表格来控制它们。
我不会在这里重写 FWTK 手册。我会向你展示我发现的设置和问题。有三个文件这些这些：

- `/etc/services`：告诉系统哪些端口是开启的。
- `/etc/inetd.conf`：当有人敲击端口时告诉 inetd 程序。
- `/usr/local/etc/netmap-table`：告诉 FWTK 允许或拒绝服务。

为了让 FWTK运行，你应该从底部开始编辑这些文件。没有正确编辑 `inetd.conf` 或 `netmap-table` 会导致你的系统无法访问。

#### 7.4.1 netmap-table

该文件控制 FWTK 的服务。你应该考虑来自防火墙两侧的流量。网络外部的人应该在获得访问之前识别身份，但你网络内部的人可能被允许通过。防火墙使用一个名为 `auth` 的进程来保存用户 ID 和密码数据库。该行的正确设置是：

```
# Proxy configuration
# 认证服务器和客户端规则
authsrv   database /usr/local/etc/fw-auth
authsrv   permit-hosts *
authsrv   sleep 120
authsrv   true
# 使用认证服务器的应用程序
authsrv*:127.0.0.1
```

初始化数据库，切换到 root 并在 `/var/local/etc` 创建记录。这是一个示例。阅读 FWTK 文档学习如何添加用户和组。

```
# auth
authsrv   list
authsrv   disabled
authsrv   enabled
authsrv   changed
authsrv   never
authsrv   set
authsrv   list
user hostname                ok
D
```

telnet (`tn-gw`) 控制是直观的，你应该设置这些。例如，我允许私有网络的主机通过（`permit-hosts 196.1.2.* -passok`）。但任何其他用户必须输入他们的 ID 和密码来使用代理（`permit-hosts * -auth`）。我还允许其他系统 (`196.1.2.202`) 直接访问防火墙。所有的 in-telnet 节点都这样做。稍后我会解释这些。telnet timeout 应该保持短。

```
# telnet gateway rules:
tn-gw:denial-msg /usr/local/etc/tn-deny.txt
tn-gw:welcome-msg /usr/local/etc/tn-welcome.txt
tn-gw:help-msg /usr/local/etc/tn-help.txt
tn-gw:timeout 90
tn-gw:permit-hosts 196.1.2.* -passok -xok
tn-gw:permit-hosts -auth
# Only the Administrator can telnet directly to the Firewall via Port 24
netacl-in.telnet:permit-hosts 196.1.2.202 -exec /sbin/in.telnet
```

login-commands 工作方式与 telnet 相同。

```
# login gateway rules:
login-gw:    denial-msg      /usr/local/etc/login-deny.txt
login-gw:    welcome-msg    /usr/local/etc/login-welcome.txt
login-gw:    help-msg       /usr/local/etc/login-help.txt
login-gw:    timeout 90
login-gw:    permit-hosts 196.1.2.* -passok -xok
login-gw:    permit-hosts * -auth -xok
# Only the Administrator can connect directly to the Firewall via Port
netacl-ridlog:permit-hosts 196.1.2.202 -exec /usr/libexec/ridlog -a
```

你不应该让任何人直接访问你的防火墙，这包括 FTP，所以你不在防火墙上放置 FTP 服务器。

再次，`permit-hosts` 列表允许保护网络中的任何人访问 Internet，所有其他人都要进行身份验证。我在控制中包含了每个发送和接收文件的日志 (`-log str`)。

ftp timeout 控制掉坏连接的时间以及连接有活动时保持开启的时间。

```
# ftp gateway rules:
ftp-gw:    denial-msg      /usr/local/etc/ftp-deny.txt
ftp-gw:    welcome-msg    /usr/local/etc/ftp-welcome.txt
ftp-gw:    help-msg       /usr/local/etc/ftp-help.txt
ftp-gw:    timeout 300
ftp-gw:    permit-hosts 196.1.2.* -log (ret str)
ftp-gw:    permit-hosts * -auth
```

Web、组和基于浏览器的 ftp 由 `http-gw` 控制。前两行为 root 创建了一个目录。

```
# www and gopher gateway rules:
http-gw:    userid         root
http-gw:    directory      /jail
http-gw:    timeout 300
http-gw:    default-httpd  www.aft.nes
http-gw:    hosts          196.1.2.* -log (read write ftp)
```

ssl 实际上只是一个通过网关。我对它很放心。我允许保护网络内的任何人连接到任何服务器，除了地址 `172.0.0.*` 和 `192.1.1.*`，并且仅通过端口 443 到 563 。

```
# ssl gateway rules:
ssl-gw:    timeout 300
ssl-gw:    hosts          196.1.2.* -dest ( !127.0.0.* !192.1.1.*) *:443:563)
ssl-gw:    deny-hosts *
```

* NetNews Plugged gateway

## 7. 安装 TIPS 代理服务器

```
plug-gw: timeout 3600
plug-gw: port nntp 196.1.2.* -plug-to 199.5.175.22 -port nntp
plug-gw: port nntp 199.5.175.22 -plug-to 196.1.2.* -port nntp
```

finger 网关非常简单。受保护网络内部的任何人必须先登录，然后我们允许他们对他们使用 `finger` 程序。其他其他人将收到一条消息。

```
# 启用 finger 服务
netacl-finger:permit-hosts 196.1.2.* -exec /usr/libexec/fingerd
netacl-finger:permit-hosts * -exec /bin/cat /usr/local/etc/finger.txt
```

我还没有设置 Mail（邮件）和 X-windows 服务，因此没有包含相关示例。如果有人有可以运行的示例，请给我发送电子邮件。

### 7.4.2 inetd.conf 文件

这是一个完整的 `/inetd.conf` 文件。所有不需要的服务都已注释掉。我包含了整个文件，以展示如何关闭服务，以及如何设置新的防火墙服务。

```
#echo stream tcp nowait root internal
#echo dgram udp wait root internal
#discard stream tcp nowait root internal
#discard dgram udp wait root internal
#daytime stream tcp nowait root internal
#daytime dgram udp wait root internal
#chargen stream tcp nowait root internal
#chargen dgram udp wait root internal
# FTP 防墙网关
ftp-gw stream tcp nowait.400 root /usr/local/etc/ftp-gw ftp-gw
# 隧道防火墙网关
telnet stream tcp nowait root /usr/local/etc/tn-gw /usr/local/etc/tn-gw
# 本地 telnet 服务
telnet-a stream tcp nowait root /usr/local/etc/netacl/in.telnetd
# Gopher 防火墙网关
gopher stream tcp nowait.400 root /usr/local/etc/http-gw \
/usr/local/etc/http-gw
# WWW 防火墙网关
http stream tcp nowait.400 root /usr/local/etc/http-gw \\
# SSL 防火墙网关
ssl-gw stream tcp nowait root /usr/local/etc/ssl-gw ssl-gw
# Netnews 防火墙代理 (使用 plug-gw)
nntp stream tcp nowait root /usr/local/etc/plug-gw plug-gw nntp
#nntp stream tcp nowait root /usr/sbin/tcpd in.nntp
# SMTP (邮件) 防火墙网关
#smap stream tcp nowait root /usr/local/etc/smap
```
