

此配置将主机设置为从名称服务器。如果主名称服务器宕机，该从服务器将接管其活动。请比较以下代码：

```text
zone " "."in" {
    type hint;
    file "root.cache";
};
```

这定义了根名称服务器缓存。root.cache 文件保存了顶级域名的地址转换记录。

```text
zone "0.0.127.in-addr.arpa" in {
    type master;
    file "named.local";
};
```

这定义了本地主机网络。它始终是 127.0.0.0 网络。

## 配置 Linux 主机

当网卡已安装且驱动支持已启用（你需要重新编译内核）后，你需要配置网络。要配置网络配置文件，请运行 `/sbin/netconfig`。这将执行一个脚本，提示你输入相关信息。请确保你已从网络管理员处获取以下关键信息：

- IP 地址（如果需要）
- 主要名称服务器
- 次要名称服务器
- 网关
- 域名
- 主机名
- 子网掩码（也称为子网掩码）

运行 `/sbin/netconfig`。按 Enter 键开始网络配置，如图 11-1 所示。

![](img/8ad518fddafc7f5e73715a2604b61d50_371_0.png)

将出现以下提示。请按照建议输入信息。

1. 对于 ENTER HOSTNAME，输入你的主机名（全部使用小写字母），然后按 Enter 键。见图 11-2。

![](img/8ad518fddafc7f5e73715a2604b61d50_371_1.png)

2. 对于 ENTER DOMAIN NAME，输入 `company.com` 然后按 Enter 键。（见图 11-3。）请将 `company` 替换为你实际的公司名称。

![](img/8ad518fddafc7f5e73715a2604b61d50_371_2.png)

3. 对于 LOOPBACK ONLY，按 Tab 键直到选中 No，然后按 Enter 键。（见图 11-4。）

![](img/8ad518fddafc7f5e73715a2604b61d50_372_0.png)

4. 对于 ENTER LOCAL IP ADDRESS，输入你的 IP 地址，然后按 Enter 键。如果你的网络使用 DHCP 而不是静态地址，你可以输入 "1.1.1.1"。（见图 11-5。）

![](img/8ad518fddafc7f5e73715a2604b61d50_372_1.png)

5. 对于 ENTER GATEWAY ADDRESS，输入你的网关地址，然后按 Enter 键。（见图 11-6。）

![](img/8ad518fddafc7f5e73715a2604b61d50_372_2.png)

6. 对于 ENTER NETMASK，输入你的子网掩码，然后按 Enter 键。它的样子类似于 255.255.255.0 或 255.255.248.0。（见图 11-7。）

![](img/8ad518fddafc7f5e73715a2604b61d50_373_0.png)

图 11-7：设置你的子网掩码

7. 对于 USE A NAMESERVER，按 Enter 键将其默认设为 YES；否则你会对输入 IP 地址感到厌倦。（见图 11-8。）

![](img/8ad518fddafc7f5e73715a2604b61d50_373_1.png)

图 11-8：设置你的名称服务器

8. 对于 SELECT NAMESERVER，输入你的名称服务器 IP 地址（不是名称），然后按 Enter 键。（见图 11-9。）

![](img/8ad518fddafc7f5e73715a2604b61d50_373_2.png)

图 11-9：查看最终屏幕

9. 在最终屏幕上按 Return 或 Enter 键，至此你的主机配置已完成。请务必重新启动系统以充分利用你的网络功能（如果不重启，它们将无法生效）。

## 检查网络守护进程

网络守护进程多种多样：`telnetd`、`sshd`、`ftpd`、`tftpd`。当某个应用程序的套接字打开时，守护进程驻留在该应用程序的套接字上并等待连接。当该应用程序的套接字关闭时，守护进程停止运行。

守护进程不会独立运行，它们由 inetd 控制，inetd 是一个超级守护进程。inetd 的配置文件可以影响哪些应用程序和协议可以运行，甚至可以启用某些应用程序的日志记录。因此，你可以将 inetd 视为套接字管理器。

当 inetd 运行时，它会读取配置文件。如果你更新了此文件，请向 inetd 发送挂起信号（`kill –HUP <processid>`）。这将导致 inetd 重新读取 `/etc/inetd.conf` 文件。

注意 `/etc/inetd.conf` 的权限：

```text
$ ls –l /etc/inetd.conf
-rw-r-r-- 1 root root 4998 Oct 15 1997 /etc/inetd.conf
```

你绝不应该让此文件的权限高于 644！这可以防止用户向 `/etc/inetd.conf` 文件写入数据。

`/etc/inetd.conf` 中的条目格式如下：

```text
service_name sock_type proto flags user server_path args
```

FTP 是所有语法用法的很好的例子。

```text
Ftp stream tcp nowait root /usr/sbin/tcpd wu.ftp –l –i –a
```

在这里，FTP 被定义为一个服务（如在 `/etc/services` 文件中所示）。它使用数据流（你还会看到 dgram，它是 datagram 的缩写，用于 UDP 数据包）。它使用 TCP 作为传输协议，信息通过流传输——它也可以是数据报以及多种其他数据包。nowait 意味着协议不会等待释放套接字（这只适用于数据报数据包），并且 ftpd 以 root 用户身份运行。

实际运行的守护进程是 wu.ftp，即 WUarchive FTP 守护进程。选项 –l（小写 L）启用日志记录选项。

请查看整个 `/etc/inetd.conf` 文件，如列表 11–1 所示。

### 列表 11–1：/etc/inetd.conf 文件

```text
# more /etc/inetd.conf
# See "man 8 inetd" for more information.
#
#
# If you make changes to this file, either reboot your machine or send the
# inetd a HUP signal:
# Do a "ps x" as root and look up the pid of inetd. Then do a
# "kill –HUP <pid of inetd>".
# The inetd will re-read this file whenever it gets that signal.
#
# <service_name> <sock_type> <proto> <flags> <user> <server_path> <args>
#

# The first 4 services are really only used for debugging purposes, so
# we comment them out since they can otherwise be used for some nasty
# denial-of-service attacks. If you need them, uncomment them.
# echo stream tcp nowait root internal
# echo dgram udp wait root internal
# discard stream tcp nowait root internal
# discard dgram udp wait root internal
# daytime stream tcp nowait root internal
# daytime dgram udp wait root internal
# chargen stream tcp nowait root internal
# chargen dgram udp wait root internal
time stream tcp nowait root internal
time dgram udp wait root internal
#
# These are standard services.
#
ftp stream tcp nowait root /usr/sbin/tcpd wu.ftp -1 -i -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
#

# Use this one instead if you want to snoop on telnet users (try to use this
# for ethical purposes, ok folks?):
# telnet stream tcp nowait root /usr/sbin/tcpd
/usr/sbin/in.telnetd
#

# This is generally unnecessary. The daemon provided by INN will handle the
# incoming NNTP connections.
# nntp stream tcp nowait root /usr/sbin/tcpd in.nttpd
#

# This is for BSD sendmail. NOTE: It's not a good idea to uncomment this
# one, since sendmail is already set up to run as a daemon in /etc/rc.d/rc.M.
# But, If you really want to run sendmail this way for some reason, you'll
# need to uncomment the smtp line following AND change the line in
/etc/rc.d/rc.M
# to run sendmail like this: /usr/sbin/sendmail -q30m
# ...otherwise the queue will not be processed.
# smtp stream tcp nowait root /usr/sbin/tcpd sendmail -bs

# The comsat daemon notifies the user of new mail when biff is set to y:
comsat dgram udp wait root /usr/sbin/tcpd in.comsat
#

# Shell, login, exec and talk are BSD protocols.
#
shell stream tcp nowait root /usr/sbin/tcpd in.rshd -L
login stream tcp nowait root /usr/sbin/tcpd in.rlogind
# exec stream tcp nowait root /usr/sbin/tcpd in.rexecd
# talk dgram udp wait root /usr/sbin/tcpd in.talkd
ntalk dgram udp wait root /usr/sbin/tcpd in.ntalkd
# 
# Kerberos authenticated services 
# 
# klogin stream tcp nowait root /usr/sbin/tcpd rlogind -k 
# eklogin stream tcp nowait root /usr/sbin/tcpd rlogind -k -x 
# kshell stream tcp nowait root /usr/sbin/tcpd rshd -k 
# 
# Services run ONLY on the Kerberos server 
# 
# krbupdase stream tcp nowait root /usr/sbin/tcpd registerd 
# kpasswd stream tcp nowait root /usr/sbin/tcpd kpasswd 
# Pop et al 
# 
pop2 stream tcp nowait root /usr/sbin/tcpd in.pop2d 
pop3 stream tcp nowait root /usr/sbin/tcpd in.pop3d 
# The ipop3d POP3 server is part of the Pine distribution. If you've 
# installed the Pine package, you may wish to switch to ipop3d by 
# commenting out the pop3 line above, and uncommenting the ipop3d line following.
#ipop3 stream tcp nowait root /usr/sbin/tcpd ipop3d 
imap2 stream tcp nowait root /usr/sbin/tcpd imapd 
# 
# The Internet UUCP service. 
# 
# uucp stream tcp nowait uucp /usr/sbin/tcpd /usr/lib/uucp/uucico -l 
# 
# Tftp service is provided primarily for booting. Most sites 
# run this only on machines acting as "boot servers." 
# 
# tftp dgram udp wait nobody /usr/sbin/tcpd in.tftp 
# bootps dgram udp wait root /usr/sbin/in.bootpd in.bootpd 
# 
# Finger, systat and netstat give out user information which may be 
# valuable to potential "system crackers." Many sites choose to disable 
# some or all of these services to improve security. 
# Try "telnet localhost systat" and "telnet localhost netstat" to see that 
# information yourself! 
#
finger stream tcp nowait nobody /usr/sbin/tcpd in.fingerd -w 
systat stream tcp nowait nobody /usr/sbin/tcpd /bin/ps -auwx 
netstat stream tcp nowait root /usr/sbin/tcpd /bin/netstat -a 
#
```

