
250 2.1.0 Ok
RCPT TO: kyle@localhost
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: test
This is just a test
.
250 2.0.0 Ok: queued as 1ADD057CD0
quit
221 2.0.0 Bye
Connection closed by foreign host.

你输入的第一个命令是 HELO 后跟你希望系统识别你的名称。接下来输入 MAIL FROM: 后跟你希望邮件显示来自的电子邮件地址。之后输入 RCPT TO: 后跟你想要发送到的电子邮件地址。然后输入 DATA。此时之后你输入的所有内容都将被视为邮件正文。在我的示例中我添加了一个 Subject: 字段，但即使这也是可选的。继续输入你的消息，然后当你完成后，输入一个句点，然后再次按回车。最后输入 quit 以结束会话。

## 简单的 SSH 密钥共享

在 SSH 上设置密钥认证时令人烦恼的部分之一是必须将所有公钥移动到每个系统的 authorized_keys 文件中。多年来我会做一些花哨的 shell 脚本来复制密钥，但后来我发现 openssh 包中包含了一个名为 ssh-copy-id 的工具，专门用于此目的。要使用该程序，只需输入 ssh-copy-id 后跟你想要复制密钥到的远程服务器（以及可选的远程用户名）。例如，如果我想将我当前用户的密钥复制到名为 web1 的服务器，我可以输入：

```
$ ssh-copy-id web1
```

或者如果我想将密钥复制到名为 db4 的服务器上 kyle 用户的账户，我会输入：

```
$ ssh-copy-id kyle@db4
```

com.                 172800  IN  NS  J.GTLD-SERVERS.NET.
com.                 172800  IN  NS  A.GTLD-SERVERS.NET.
com.                 172800  IN  NS  M.GTLD-SERVERS.NET.
com.                 172800  IN  NS  G.GTLD-SERVERS.NET.
com.                 172800  IN  NS  E.GTLD-SERVERS.NET.
com.                 172800  IN  NS  I.GTLD-SERVERS.NET.
;; Received 504 bytes from 192.58.128.30#53(j.root-servers.net)
   in 110 ms

ubuntu.com.          172800  IN  NS  ns1.canonical.com.
ubuntu.com.          172800  IN  NS  ns2.canonical.com.
ubuntu.com.          172800  IN  NS  ns3.canonical.com.
;; Received 144 bytes from 192.41.162.30#53(L.GTLD-SERVERS.NET)
   in 91 ms

www.ubuntu.com.       600   IN  A   91.189.90.41
ubuntu.com.          172800  IN  NS  ns1.canonical.com.
ubuntu.com.          172800  IN  NS  ns2.canonical.com.
ubuntu.com.          172800  IN  NS  ns3.canonical.com.
;; Received 160 bytes from 91.189.94.173#53(ns1.canonical.com)
   in 151 ms

## 索引

- \ (反斜杠)
- 行 continuation 字符，93
- 在 sudoer 别名中，206
- % (百分号)
- 组名指示符，204
- Kickstart 部分指示符，106
- . (点)
- 当前目录的别名，20
- 软件包段分隔符，62–63
- 分区分隔符，94，96
- .. (点点)，当前目录上方目录的别名，20
- [ ] (方括号)
- 在 grep 搜索关键字中，477–478
- 在正则表达式中，458
- @ (at 符号)，Kickstart 任务指示符，106
- ^ (插入符号)，Ctrl 键符号，24
- # (井号)，注释指示符
- source.list 文件，72
- Upstart，31
- < (左尖括号)，重定向操作符，462–464
- ? (问号)，通配符，456
- > (右尖括号)，重定向操作符，462–464
- >> (右尖括号)，重定向操作符，462–464
- / (斜杠)，在 IRC 命令中，444
- | (竖线)，管道符号，458–459
- * (星号)
- 在 shell glob 中，208–209，457
- 在 traceroute 输出中，414
- 通配符，457
- ** (星号)，在 shell glob 中，208–209
- 1n 命令
- 创建硬链接，468
- 创建符号链接，467
- 450 命令，155
- 802.3ad 或 4 模式，366
- A
- A 时间，12
- a2dissite 脚本，139
- a2ensite 脚本，138
- aa-complain 程序，209
- aa-enforce 程序，209
- abort 命令，149
- 可访问性选项，4
- 账户选项，Kickstart，109
- 主/主集群，369
- 主/备份或 1 模式，365
- 主/备份策略，365
- 主/被动集群，369
- 自适应负载均衡，366
- 自适应传输负载均衡，366
- --add 命令，346
- 管理员。参见 系统管理员。
- 管理员 (Windows)。参见 Root 用户。
- 高级软件包工具 (APT)。参见 APT (高级软件包工具)。
- 警报升级，285–286
- 软件升级警报，64
- 别名
- 目录的别名，20
- 电子邮件用户，147，150
- 嵌套，21
- newaliases 命令，150
- sudo 命令，205–206
- 更新，150
- allow 命令，217
- Apache。另见 Web 服务器。
- a2dissite 脚本，139
- a2ensite 脚本，138

