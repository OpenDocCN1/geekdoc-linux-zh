
## cp /bin/bash /home/guest
## mv /home/guest/bash /home/guest/./.backdoor

接下来，你需要为该文件赋予 SUID 访问权限和 root 控制权。

## chmod 4755 /home/guest/./.backdoor
## chown root /home/guest/./.backdoor

现在，你可以运行 `.backdoor` 命令，从而获得你想要的 root 访问权限。你还可以搞出的另一个恶作剧是修改设备的权限，使其变为所有人可写。这将使你能够向该设备发送命令——并且这些命令将以 root 权限运行。

## 拒绝服务

拒绝服务（DoS）攻击旨在使主机或网络服务瘫痪。大多数针对特定网络端口的 UNIX 漏洞利用程序同样可以攻击 Linux 中类似的易受攻击点。其中一种简单的攻击——可能会击垮 Web 服务器——使用带有 flood 选项 (-f) 的 ping 命令：

## ping -f some.webserver.org 80

![](img/8ad518fddafc7f5e73715a2604b61d50_292_0.png)

### 早期的 Slackware 后门（续）

幸运的是，技术在进步。如今，你不会在任何新的 Slackware 发行版中找到 **sample_users.tgz**。当然，你可以使用 **adduser** 命令创建自己的示例用户（带有他们自己的密码保护）。只需小心你给它们起的名字。

这样做会向 **some.web-server.org** 的 **80** 端口发送大量 ICMP 数据包。这就像在一个房间里有一百人，每个人都在试图同时与你交谈。那么，你会怎么做？你会关闭监听，不听任何人的话。计算机也会做同样的事。它将关闭该端口；由于这是 Web 服务器守护进程，Web 服务器就会关闭。

![](img/8ad518fddafc7f5e73715a2604b61d50_293_0.png)

除非是对你自己的 Web 服务器进行测试，否则不要这样做。这种手段很容易被追踪，并且有人因此而入狱。

## 保护你的系统

在保护你的系统之前，你需要了解主机安全的三个基本方面：授权、认证和完整性。**授权** 是授予某人访问数据的权限。**认证** 是验证已授权用户的身份；*维护文件完整性* 是保持数据处于可用且可信的形式。表 9-1 展示了每一点的示例。

### 表 9-1 主机安全的基本方面

| 安全方面 | 定义 | 示例 |
| :--- | :--- | :--- |
| 授权 | 授予访问权限 | 用户名、名字、身份证号、权限 |
| 认证 | 验证已授权用户 | 密码、指纹、数字签名 |
| 完整性 | 保持数据可用且可信 | 检查文件变更、备份 |

即使你的 Slackware 系统上没有保存任何核机密，你也不希望被迫重新做所有辛苦工作来重新优化你的系统。如果有人入侵你的系统，你不希望陷入这种困境。你可能会因此失去工作，回答律师发来的法律问题，或者遭受其他糟糕的后果。

![](img/8ad518fddafc7f5e73715a2604b61d50_294_0.png)

> 第 8 章提供了关于账户管理的详细信息——不仅是用户账户，还包括系统中使用的服务和管理应用。作为朝这个方向迈出重要的一步，你可能需要回顾本章提到的不安全应用程序——并对它们进行加固。

黑客试图*获取你系统的 root 权限*——即在未询问你密码的情况下获得 root 访问权限。本节详细介绍了如何防止这种情况发生。

## 仅运行必要的守护进程

守护进程是脱离终端在后台运行的进程。根据守护进程的不同，它们很可能以 root 身份运行。由于守护进程在后台运行，当它们运行时你无法直接控制它们，因为它们不直接在终端中运行。

针对针对网络守护进程的程序漏洞的一种基本防御策略是：只运行你实际需要的网络服务和守护进程。作为评估的第一步，你可以通过运行 `ps` 来查看守护进程列表，如清单 9-1 所示。

清单 9-1: 查看守护进程
```bash
# ps -aux
USER         PID %CPU %MEM   SIZE  RSS TTY STAT START TIME COMMAND
bin          56  0.0  0.2   824   80 ?  S  Jul 15 0:00 (rpc.portmap)
root         1  0.0  0.4   824  140 ?  S  Jul 15 0:03 init [3]
root         2  0.0  0.0     0    0 ?  SW Jul 15 0:00 (kflushd)
root         3  0.0  0.0     0    0 ?  SW Jul 15 0:00 (kswapd)
root         4  0.0  0.0     0    0 ?  SW Jul 15 0:00 (nfslod)
root         5  0.0  0.0     0    0 ?  SW Jul 15 0:00 (nfslod)
root         6  0.0  0.0     0    0 ?  SW Jul 15 0:00 (nfslod)
root         7  0.0  0.0     0    0 ?  SW Jul 15 0:00 (nfslod)
root        13  0.0  0.2   800  68 ?  S  Jul 15 0:00 /sbin/update
root        51  0.0  0.6   836 188 ?  S  Jul 15 0:00 /usr/sbin/syslogd
root        54  0.0  0.7  1056 224 ?  S  Jul 15 0:00 /usr/sbin/klogd
root        58  0.0  0.3   824 100 ?  S  Jul 15 0:00 (inetd)
root        60  0.0  0.6  1028 192 ?  S  Jul 15 0:02 /usr/local/sbin/sshd
root        65  0.0  0.3   880 116 ?  S  Jul 15 0:00 /usr/sbin/rpc.mountd
root        67  0.0  0.3   900 120 ?  S  Jul 15 0:00 /usr/sbin/rpc.nfsd
root        69  0.0  0.6   824 196 ?  S  Jul 15 0:00 /usr/sbin/crond -110
root        75  0.0  0.8  1248 268 ?  S  Jul 15 0:00 (sendmail)
root        83  0.0  0.2   832  88 ?  S  Jul 15 0:00 gpm -t ms
root        85  0.0  0.2   816  68 2  S  Jul 15 0:00 (agetty)
root        86  0.0  0.2   816  68 3  S  Jul 15 0:00 (agetty)
root        87  0.0  0.2   816  64 4  S  Jul 15 0:00 (agetty)
root        88  0.0  0.1   816  44 5  S  Jul 15 0:00 (agetty)
root        89  0.0  0.1   816  48 6  S  Jul 15 0:00 (agetty)
root        98  0.0 17.5 10544 5400 ?  S  Jul 15 4:33 /usr/X11R6/bin/Xwrapp
root      4174  0.0  1.9  1156  608 p2 S  12:05 0:00 bash
root      4219  0.2  1.6   908  500 p2 S  12:14 0:00 /usr/sbin/pppd -detac
root      4266  0.0  1.2   868  384 p2 R  12:16 0:00 ps -aux
hobbes      84  0.0  0.8  1188  268 1  S  Jul 15 0:00 (tcsh)
hobbes      96  0.0  0.7  1104  216 1  S  Jul 15 0:00 (startx)
hobbes      97  0.0  0.6  1868  208 1  S  Jul 15 0:00 (xinit)
hobbes     101  0.0  0.6  1104  208 1  S  Jul 15 0:00 (xinitrc)
hobbes     103  0.0  2.1  1800  660 1  S  Jul 15 0:02 fwm2
hobbes     106  0.0  0.9  1540  300 1  S  Jul 15 0:00 /usr/X11R6/lib/X11/fv
hobbes     108  0.0  1.8  2164  572 1 SN  Jul 15 0:00 xload -nolabel -bg gr
hobbes     109  0.0  1.6  2124  508 1  S  Jul 15 0:00 xclock -bg #c3c3c3 -g
hobbes     110  0.0  0.8  1532  272 1  S  Jul 15 0:00 /usr/X11R6/lib/X11/fv
hobbes     123  0.0  3.0  2564  932 1  S  Jul 15 0:01 xterm -sb -sl 500 -j
hobbes     124  0.0  1.7  1244  548 p1 S  Jul 15 0:00 (tcsh) .
hobbes    3202  0.4 49.2 26356 15180 p1 S  01:33 2:51 netscape
hobbes    3203  0.0  5.5 12564  1720 p1 S  01:33 0:00 (netscape)
hobbes    3577  0.0  4.5  2556  1400 1  S  09:25 0:00 xterm -sb -sl 500 -j
hobbes    3578  0.0  2.1  1200   656 p0 S  09:25 0:00 -tcsh
hobbes    3597  0.0  3.0  1744   936 1  S  09:28 0:00 rxvt -font 10x20 -ls
hobbes    3598  0.0  2.2  1228   696 p2 S  09:28 0:00 -tcsh
```

守护进程包括 pppd, kflushd, kswapd, inetd, nfsd, mountd 和 sshd。还有很多其他守护进程可能正在运行。你运行的守护进程越多，你系统中运行的不受控制的进程就越多。从某种意义上说，这是好事，因为你不必担心监视它们。然而，你仍然需要担心维护。

如果某人正在运行 NFS 守护进程，而该进程存在广为人知的漏洞，这些漏洞可用于获取系统 root 权限。限制 NFS 可以访问的可信任主机数量；它太容易被伪造了。

表 9-2 展示了常见的守护进程。

## 扫描知名端口

黑客访问你系统的另一种常见方式是扫描端口。在 Linux 系统上表现良好的两个常见实用程序是 strobe 和 nmap。

## NMAP

nmap 扫描器是一种发现知名端口的便捷方式。它通过扫描 /etc/services 文件来实现这一点。你可以传递许多选项来查看你能发现什么。你可以使用不同的扫描类型（例如，通过发送不同类型的数据包）。nmap 扫描器在 Linux 和其他 UNIX 操作系统上运行良好。下表展示了执行 nmap -h 后显示的使用信息。表 9-3 列出了 nmap 选项。

