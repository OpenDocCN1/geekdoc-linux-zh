
以及哪些主机被允许连接到运行在数据库上的 authsrv 程序。

```
authsrv:      permit hosts 127.0.0.1
authsrv:      permit hosts 128.83.155.45
authsrv:      database /var/adm/authsrv.db

# clients using the auth server
*: authserver 127.0.0.1 7777
```

默认情况下，只有本地主机能够连接到 authsrv 进程。对于此配置，本地主机以及主机 128.83.155.45 都被允许连接到 authsrv 服务器进程。此外，数据库位于 /var/adm/authsrv.db。要初始化数据库，请以 root 身份运行 authsrv 程序：

```
# ./authsrv
# authsrv# adduser admin "AuthSrv_Admin"
ok - user added initially disabled
authsrv# ena admin
enabled
authsrv# proto admin pass
changed
authsrv# pass admin "r8uT3&4M"
password changed
authsrv# superwiz admin
set wizard
authsrv# adduser ruser "Remote_User"
ok - user added initially disabled
authsrv# group ruser rgroup
ok - user added to group rgroup
authsrv# ena ruser
enabled
authsrv# proto ruser pass
changed
authsrv# pass ruser "L83A47!"
authsrv# list
user  group  longname      ok?  proto  last
.... .... .... .... .... ....
admin rgroup AuthSrv_Admin ena  passw never
ruser rgroup Remote_User   ena  passw never
authsrv# quit
#
```

## 配置 Telnet 代理

这里无法对 netperm-table 文件的配置进行全面讨论。相反，我们将以配置 telnet 代理 tn-gw 为例进行说明。在默认的 netperm-table 文件中，tn-gw 软件的配置如下：

```
# Example telnet gateway rules:
#
#----------------------------------------
tn-gw: denial-msg /usr/local/etc/tn-deny.txt
tn-gw: welcome-msg /usr/local/etc/tn-welcome.txt
tn-gw: help-msg /usr/local/etc/tn-help.txt
tn-gw: timeout 3600
tn-gw: permit-hosts YOURNET.* -passok -xok
# if this line is uncommented incoming traffic is permitted WITH
# authentication required
tn-gw: permit-hosts * -auth
```

如果管理员将远程访问运行 FWTK 的防火墙主机，可以添加一条特殊行，其限制比普通用户更严格：

```
netacl-sshd: permit-hosts YOUR_ADDR -exec /usr/local/sbin/sshd
```

YOUR_ADDR 是管理员将从其连接的机器的地址。

在 /etc/services 文件中，您需要为使用工具包软件启用的任何新服务添加端口定义条目。工具包的核心是 <service>-gw 程序，它们是系统的代理服务器。假设例如，您从外部向网络提供 telnet 访问。为了使用 TIS FWTK，您需要配置 tn-gw 程序，以便 inetd 在每次对防火墙进行 telnet 连接时启动它。然后，根据 netperm-table 中 tn-gw 部分的内容，FWTK 可能会允许或拒绝连接。inetd.conf 需要反映 FWTK 网关程序的使用。列表 26.1 显示了 telnet、ftp、secure shell 和 identd 通过防火墙代理的示例 inetd.conf。

### 列表 26.1 通过 TIS 防火墙工具包代理的示例 inetd.conf

```
#
# See "man 8 inetd" for more information.
#
# If you make changes to this file, either reboot your machine or send the
# inetd a HUP signal:
# Do a "ps x" as root and look up the pid of inetd. Then do a
# "kill -HUP <pid of inetd>".
# The inetd will re-read this file whenever it gets that signal.
#
```

### 列表 26.1 继续

```
# <service_name> <sock_type> <proto> <flags> <user> <server_path> <args>
#
#
# These are standard services.
ftp stream tcp nowait root /usr/local/etc/ftp-gw /usr/local/etc/ftp-gw
telnet stream tcp nowait root /usr/local/etc/tn-gw /usr/local/etc/tn-gw
ssh stream tcp nowait root /usr/local/etc/plug-gw plug-gw sshd
ssh-a stream tcp nowait root /usr/local/etc/netacl sshd
#
# Ident service is used for net authentication
auth stream tcp nowait root /usr/local/etc/plug-gw /usr/sbin/in.identd
#
# End of inetd.conf.
```

plug-gw 文件如下：

```
#
# Secure Shell and identd gateway
#
plug-gw: -port ssh * -plug-to <ssh_server> -port ssh
plug-gw: -port 113 * -plug-to <mail_server> -port 113
```

netperm-table 中的 plug-gw 部分告诉防火墙将端口 22 上的连接转发到安全 shell 服务器的 ssh 端口（即端口 22）。对于 identd，任何 identd 连接都被发送到邮件服务器，因为它是最合乎逻辑的运行 identd 的位置。

现在让我们更仔细地看看 ssh-a 行。这是在防火墙机器上为管理安全 shell 预留的特殊端口。例如，sshd 通常在端口 22 上运行。但是，对于此示例，sshd 将在端口 38 上运行。为了使 inetd 理解这一点，/etc/services 文件需要条目：

```
ssh tcp/38   ssh # Administrative Secure Shell added.
```

设置代理服务器比简单的包过滤防火墙需要更多的工作。然而，代理服务器在使网络更易于访问并使防火墙对用户更易于忍受方面发挥了很大作用。现在我们已经讨论了如何在防火墙上设置代理服务，我们可以把注意力转向设置防火墙本身。

## 设置防火墙

在深入了解如何使用 Linux 机器设置防火墙之前，需要问一个问题：“我需要设置防火墙吗？”如果您想要设置防火墙的机器持续连接到互联网，答案是肯定的。如果您在家中有一个网络，只想伪装您的网络，答案很可能是肯定的。如果所讨论的机器不是持续连接到互联网并且不充当私有网络的网关角色，答案可能是否定的。尽管如此，在当今的互联网上，了解如何设置防火墙是一项必要的技能。入侵和攻击的数量每年都在增加。了解如何保护网络甚至单台机器是非常有价值的。

## 包过滤

每个防火墙基本上都是一个包过滤器。想法是选择性地控制数据的流向和/或来自网络。包过滤器允许或阻止数据包，通常在路由它们的同时进行，可以在路由器级别或主机级别实现。当在路由器中实现时，路由器不仅必须承担将数据包路由到其正确目的地的负担，还必须决定哪些数据包允许通过，哪些数据包被拒绝。

## 使用 Linux 进行包过滤

在 Linux 下，包过滤内置于内核中。过滤器的确切实现取决于您运行的是 2.2.X 内核还是 2.0.X 内核。包过滤首次引入 Linux 内核代码是在 1.3.X 内核中，过滤规则由 Jos Vos 编写的程序 ipfwadm 设置和操作。

当开发内核 2.1.102 发布时，许多人惊讶地发现他们的旧包过滤器不再工作。随着内核 2.1.103 的发布，变更被记录下来。名为 ipchains 的新程序可用，它可与新的包过滤代码一起工作。本节介绍如何使用 ipfwadm 和 ipchains 设置 Linux 包过滤器。始终最好参考随程序提供的文档以全面讨论其功能。此外，始终如一，如果您在手册页中找不到问题的答案，包过滤的内核源代码是权威的。

## 使用 ipfwadm 进行过滤

ipfwadm 最初由 X/OS Systems 的 Jos Vos 编写。构建的 RPM 可以在 ftp://ftp.xos.nl/pub/linux/ipfwadm/ipfwadm-2.3.0-1.i386.rpm 找到。

安装 ipfwadm：

```
# rpm -ivh ipfwadm-2.3.0-6.i386.rpm
ipfwadm ########################################
#
```

程序 ipfwadm 将安装在 /sbin 中。在使用 ipfwadm 之前，您必须重新编译内核以确保防火墙代码已内置。要编译包过滤代码，必须在内核配置中设置以下选项：

```
Code maturity level options ...>

[Y] Prompt for development and/or incomplete code/drivers

General Setup ...>

[Y] Networking support

Networking options ...>

[Y] Network firewalls
[Y] TCP/IP networking
[Y] IP: forwarding/gatewaying
[Y] IP: syn cookies
[Y] IP: firewalling
[Y] IP: firewall packet logging
[Y] IP: always defragment
[Y] IP: accounting
[Y] IP: Drop source routed frames

Network device support ...>

[Y] Network device support
<*> Dummy net driver support
[Y] Ethernet (10 or 100Mbit)
Select your particular network card
```

重新配置内核后，执行 make clean、make dep 和 make zImage。将新内核复制到 /boot 目录，编辑 /etc/lilo.conf 以包含新内核，然后重新启动。
