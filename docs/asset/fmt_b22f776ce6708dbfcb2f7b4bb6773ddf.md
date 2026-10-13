
# 在操作系统安装期间移除不必要的服务

在你的计算机上安装 Red Hat Linux 之前，决定你想在系统上运行什么。写下实现你的目标所需的服务。例如，如果你正在创建一个 Web 服务器系统，你可能不需要 POP 服务器或 NNTP 新闻服务器。列出你想要安装的服务器软件列表。Red Hat Linux 安装程序允许你选择单个软件包。花时间检查所有列表并只选择必要的包。有时安装程序会安装一个或多个你所选包的先决包。一旦你在安装过程中完成软件包选择，它会向你显示这些包的名称。写下这些包的名称。

在你安装了必要的包并首次启动系统后，你可以查看存储在 `/tmp` 中的安装日志，或者运行以下命令获取所有已安装包的完整列表：

```
rpm -qa > /tmp/all.packages
```

仔细检查 `/tmp/all.packages` 文件，检测任何你不记得安装过的包。如果某个包没有出现在你的先决列表中，你可能想使用以下命令获取更多关于该包的信息：

```
rpm -qi package_name
```

如果该包是不必要的，使用以下命令将其删除：

```
rpm -e package_name
```

# 第六部分：安全与监控

我不建议在将作为互联网服务器的计算机上安装以下类型的软件包：

- 任何与 X-Windows 以及 X-Windows 本身相关的包。
- 如果你计划提供实时音频/视频服务，除了 real-audio/video 服务器包以外的任何多媒体应用。
- 除必需的之外的任何解释器。我个人仅将 Perl 用于脚本编写，因此会安装其他脚本语言。
- 任何你不需要的服务器软件，例如 NFS、NIS、INN、POP2 或 3，或者你不需要的 Samba。
- 任何你不使用的文件编辑器。我只使用 vi，因此不会安装像 emacs 这样复杂的编辑器。当然，如果你是一个 emacs 粉丝，你会选择这个“巨兽”而不是 vi。我也没有安装各种 vi 的克隆版本。
- 任何你需要的客户端程序。例如，不要安装你认为你或你的用户不会使用的电子邮件客户端。

如你所见，主题是相同的——安装的越少，需要担心的越少。

现在让我们来看看如何增强各种网络服务的安全性。

## 安全 inetd-rd 运行的服务

`inetd` 守护进程被称为互联网“超级服务器”，因为它被用于提供许多流行的互联网服务器，如 FTP、Telnet、POP2/3 和 finger。`inetd` 守护进程通常在多用户启动过程的某点启动。在启动时，`inetd` 守护进程会读取 `/etc/inetd.conf` 配置，并监听 `/etc/services` 中列出的所有标准端口上的请求。当在某个端口接收到请求时，它会启动相应的服务来处理该请求。列表 18-2 显示了一个典型的 `/etc/inetd.conf` 文件。

```
Listing 18-2: 一个 /etc/inetd.conf 文件
#
# inetd.conf
# 此文件描述了通过 INET TCP/IP 超级服务器提供的服务。要要重新配置
# 运行中的 INET 进程，请编辑此文件，然后向
# INET 进程发送一个 SIGHUP 信号。
#
# 版本: @(#)/etc/inetd.conf 3.10 05/27/93
```

## 第 18 章：安全基础

作者：内容取自 BSD UNIX 4.3/TAHOE。

Fred N. van Kempen <waltje@uwalt.nl.mugnet.org>

由 Marc Ewing 修改于 RHS Linux <marc@redhat.com>

```
#n <service_name> <sock_type> <proto> <flags> <user> \
# <server_path> <args>
# Echo, discard, daytime, 和 chargen 主要
# 用于测试。
# 在更改后重新读取此文件，
# 只需执行 'killall -HUP inetd'
# BSD
#echo stream tcp nowait root internal
#echo dgram udp wait root internal
#discard stream tcp nowait root internal
#discard dgram udp wait root internal
#daytime stream tcp nowait root internal
#daytime dgram udp wait root internal
#chargen stream tcp nowait root internal
#chargen dgram udp wait root internal
# 这些是标准服务。
# ftp stream tcp nowait root /usr/sbin/tcpd in.fpd -1 -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
gopher stream tcp nowait root /usr/sbin/tcpd gn
# 不要取消注释，除非你*真的*知道自己在做什么。
# smtp 现在由 sendmail 守护进程处理，而不是 smtpd。
# 它并没有
# 从这里运行，它是在启动时从 /etc/rc.d/rc.# 启动的
#smtp stream tcp nowait root /usr/bin/smtp smtpd
#nntp stream tcp nowait root /usr/sbin/tcpd in.nntpd
# Shell, login, 和 exec 都是 BSD 协议。
shell stream tcp nowait root /usr/sbin/tcpd in.rshd
login stream tcp nowait root /usr/sbin/tcpd in.logind
exec stream tcp nowait root /usr/sbin/tcpd in.rexecd
talk dgram udp wait root /usr/sbin/tcpd in.talkd
talkd dgram udp wait root /usr/sbin/tcpd in.ntalkd
#dtalk stream tcp wait nobody /usr/sbin/tcpd in.dtalkd
#
# 所有的 pop 和 imap 邮件服务
#
pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
imap stream tcp nowait root /usr/sbin/tcpd imapd
#
# 互联网 UUCP 服务。
#
#uucp stream tcp wait uucp /usr/sbin/tcpd /usr/lib/uuc/uico -1
#
# Tftp 服务主要用于启动。大多数站点
# 仅在作为“启动服务器”的机器上运行此服务
# 除非你*需要*它，否则不要取消注释。
#
tftpd dgram udp wait root /usr/sbin/tcpd in.tftpd
#bootps dgram udp wait root /usr/sbin/tcpd bootpd
#
# Finger, systat 和 netstat 输出的用户信息
# 对潜在的“破解者”可能有价值。
# 许多站点选择禁用部分或全部
# 服务以提高安全性。
# finger 是 GNU finger，目前在
# RHS Linux 中
finger stream tcp nowait root /usr/sbin/tcpd in.finger
#fingerd stream tcp nowait root /usr/sbin/tcpd in.fingerd
#systat stream tcp nowait guest /usr/sbin/tcpd /bin/ps -aux
#netstat stream tcp nowait guest /usr/sbin/tcpd /bin/netstat -f
#
# Time 服务用于时钟同步。
#
time stream tcp nowait nobody /usr/sbin/tcpd in.timed
time dgram udp wait nobody /usr/sbin/tcpd in.timed
#
# 认证
#
auth stream tcp nowait nobody /usr/sbin/in.ident in.ident
linuxconf stream tcp wait root /bin/linuxconf -http
# inetd.conf 结束
```

许多其他 UNIX 文件中，`/etc/inetd.conf` 
`service_name` `sock_type` `proto` `flags` `user` `server_path` `args`

`service_name` 匹配 `/etc/services` 中指定的服务。让我们来看下面的例子：
