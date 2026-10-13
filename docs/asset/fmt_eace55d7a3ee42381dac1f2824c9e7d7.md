
```
ftp      stream tcp   nowait root       /usr/sbin/in.ftpd      in.ftpd -l
telnet   stream tcp   nowait root       /usr/sbin/in.telnet    in.telnet
shell    stream tcp   nowait root       /usr/sbin/in.rshd        in.rshd
login    stream tcp   nowait root       /usr/sbin/in.rlogind    in.rlogind
exec     stream tcp   nowait root       /usr/sbin/in.recedx     in.recedx
comsat   dgram udp   wait   root       /usr/sbin/in.comsat     in.comsat
talk     dgram udp   wait   root       /usr/sbin/in.talkd      in.talkd
uucpd   stream tcp   nowait root       /usr/sbin/in.uucpd      in.uucpd
finger   stream tcp   nowait nobody   /usr/sbin/in.fingerd   in.fingerd
```

以下配置禁用了 `/etc/inetd.conf` 中的 `ftp`、`telnet`、`shell`、`login`、`exec`、`comsat`、`talk` 和 `finger` 服务：

```
#ftp      stream tcp   nowait root       /usr/sbin/in.ftpd      in.ftpd -l
#telnet   stream tcp   nowait root       /usr/sbin/in.telnet    in.telnet
#shell    stream tcp   nowait root       /usr/sbin/in.rshd        in.rshd
#login    stream tcp   nowait root       /usr/sbin/in.rlogind    in.rlogind
#exec     stream tcp   nowait root       /usr/sbin/in.recedx     in.recedx
#comsat   dgram udp   wait   root       /usr/sbin/in.comsat     in.comsat
#talk     dgram udp   wait   root       /usr/sbin/in.talkd      in.talkd
#uucpd   stream tcp   nowait root       /usr/sbin/in.uucpd      in.uucpd
#finger   stream tcp   nowait nobody   /usr/sbin/in.fingerd   in.fingerd
```

同样，以下配置启用了 `/etc/services` 中的 `ftp`、`telnet`、`shell`、`login`、`exec`、`comsat`、`talk`、`uucpd` 和 `finger` 服务：

```
ftp              21/tcp
telnet           23/tcp
shell            514/tcp        cmd
login            513/tcp
exec             512/udp
biff             512/udp        comsat
talk             517/udp
uucpd           540/tcp        uucpd
finger   stream tcp   nobody   /usr/sbin/in.fingerd   in.fingerd
```

![](img/11bcccd1804574cca0c3018732958dd5_234_0.png)

## 206 第三部分：安全

同样，以下配置禁用了 `/etc/services` 中的 `ftp`、`telnet`、`shell`、`login`、`exec`、`comsat`、`talk`、`uucp` 和 `finger` 服务：

```
#ftp 21/tcp
#telnet 23/tcp
#shell 514/tcp cmd
#login 513/tcp
#exec 512/tcp
#biff 512/udp
#talk 517/udp
#uucp 540/tcp uucpd
#finger stream tcp nobody /usr/sbin/in.fingererd in.fingererd
```

别忘记，要启用这些功能需要 `inetd` 守护进程。

### 检查用户和组标识

用户概念是 Solaris 的核心——Solaris 系统上的所有进程和文件都“属于”某个特定的用户，并分配给特定的用户组。在建立有效的用户或组之前，系统上不可能存在任何数据或活动。作为 Solaris 管理员，管理用户和组是一项具有挑战性的活动——你将负责分配授予或拒绝给用户或用户组的所有权限，而这些权限中的许多都带有巨大的风险。例如，具有不适当权限级别的用户可能会以超级用户的身份执行不适当的命令，对你的系统造成破坏。

你可以使用 `id` 命令从终端会话中确定当前登录的用户是谁：

```
$ id
uid=1001 (natashia) gid=10(dialup)
```

输出显示当前登录的用户是 `natashia`，`UID=1001`，`GID=10`。

# 第 9 章：系统安全 209

```
root console Thul12pm 6 6 perl
natashia pts/12 Thullam 8:45 9 /usr/local/bin/tcsh
```

`w` 和 `ps` 命令是获取 Solaris 系统上当前使用模式概述的有用工具。另一个有命令是 `last`，它以顺序格式显示当前系统的历史使用模式：

```
$ last
natashia pts/4 hp Wed Apr 11 19:00 still logged in
root console :0 Tue Apr 20 10:11 still logged in
natashia pts/2 nec Tue Apr 19 19:17 - 19:24 (00:06)
natashia pts/6 austin Tue Apr 10 15:53 - 15:53 (00:00)
root console :0 Tue Apr 10 14:24 - 16:25 (02:01)
reboot system boot Thu Apr 10 14:04
natashia pts/5 hp Thu May 25 21:28 - 21:40 (00:01)
natashia pts/5 hp Thu May 25 22:22 - 21:37 (00:15)
natashia pts/5 10.64.18.1 Thu May 25 19:30 - 20:00 (00:30)
natashia pts/5 hp Thu Apr 19 19:18 - 19:29 (00:11)
root console :0 Thu Apr 5 19:27 - 22:05 (04:28)
reboot system boot Thu Apr 5 19:14
natashia pts/5 hp Fri Mar 3 16:54 - 18:26 (02:11)
natashia pts/5 hp Tue Apr 3 08:48 - 10:35 (01:47)
root console :0 Tue Apr 3 08:48 - 22:01 (13:15)
reboot system boot Thu Apr 3 08:45
root console :0 Fri Mar 30 18:54 - 19:27 (00:32)
reboot system boot Fri Mar 30 18:46
natashia pts/6 hp Tue Mar 27 20:46 - 21:51 (01:04)
root console :0 Tue Mar 27 19:50 - 21:51 (02:01)
reboot system boot Tue Mar 27 19:48
root console :0 Mon Mar 26 17:47 - 17:47 (00:04)
```

### 远程访问的安全

远程访问是现代多用户操作系统的标志，如 Solaris 及其前身系统 VAX/VMS。Solaris 服务器可以并发登录并交互式执行支持传输控制协议/网协议（TCP/IP）的 Solaris 服务器上的任何客户端，例如 Solaris、Windows 和 MacOS OS。
