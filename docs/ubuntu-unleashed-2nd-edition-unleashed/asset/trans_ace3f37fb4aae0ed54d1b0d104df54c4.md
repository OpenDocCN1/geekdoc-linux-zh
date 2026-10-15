

欢迎使用 Caitlin
运行 Ubuntu

* 所有访问均已记录 *

login: paul
Password:
上次登录：Sat Jul 9 12:05:41 from 10.0.0.5
[paul@caitlin ~]$

## 提示

请注意，服务器响应的是 Welcome to Caitlin, running Ubuntu，这是一个自定义消息。你的机器很可能会响应 Ubuntu 以及一些版本信息。这是不安全的：泄露版本号从来都不是明智之举。事实上，甚至说出 Ubuntu 也是值得怀疑的。编辑你 /etc 目录下的 issue 和 issue.net 文件以更改这些消息。

现在运行 w 命令，你会看到自己是从外部 IP 地址连接的。

## Telnet 与 SSH

尽管 Telnet 作为最后的保底、最后的手段选项值得保留，但 SSH 在几乎所有方面都更胜一筹。Telnet 速度快但也不安全。它以明文发送你的所有文本，包括你的密码，任何拥有正确工具的人都可以读取。另一方面，SSH 会加密你的所有通信，因此资源消耗更大但安全——即使某个政府安全机构出于某种原因嗅探你的数据包，也很难破解加密。

> Andy Green 在 fedora-list 邮件列表中的帖子完美地总结了 Telnet 的情况，他说：“由于 Telnet 被普遍认为助长邪恶，telnetd 服务默认未启用。” 值得采纳这个提示：仅在最后手段时才使用 Telnet。

## 设置 SSH 服务器

如果尚未安装，可以通过 Synaptic 添加 openssh-server 包来安装 OpenSSH 服务器。如果你已禁用它，可以通过选择 System、Administration、Services 并选中 Remote Shell Server 复选框来重新启用它。正如你可能已经猜到的那样，sshd 是 SSH 服务器守护进程的名称。

存在两个不同版本的 SSH，称为 SSH1 和 SSH2。后者更新、更安全、功能更多，并且是 Ubuntu 中的默认设置。最好禁用对 SSH1 客户端的支持，以便旧客户端可以连接。这在 /etc/ssh/sshd_config 文件的这一行中设置：

```
#Protocol 2,1
```

为了最大化安全性，该行应读为：

```
Protocol 2
```

这去掉了注释符号（#）并告诉 sshd 你希望它只允许 SSH2 连接。保存文件并退出编辑器。下一步是告诉 sshd 重新读取其配置文件，通过执行以下命令：

```
kill -HUP `cat /var/run/sshd.pid`
```

如果返回 cat: /var/run/sshd.pid: No such file or directory，则表示你没有运行 sshd。下次启动它时，它会读取配置文件并仅使用 SSH2。

你可以通过尝试以 SSH1 模式连接到你的 SSH 服务器来测试此更改。从同一台机器，输入以下内容：

```
ssh -1 localhost
```

-1 开关强制 SSH1 模式。如果你成功强制了 SSH2 协议，你应该会收到消息 Protocol major versions differ: 1 vs. 2。

## SSH 工具

令许多人惊讶的是，OpenSSH 实际上包含一套工具。我们已经看到了 ssh，即连接到其他机器的安全 shell 命令，以及 sshd，即接受传入 SSH 连接的 SSH 服务器守护进程。然而，还有 sftp，即 ftp 的替代品，以及 scp，即 rcp 的替代品。

你应该已经熟悉 ftp 命令，因为它是处理 FTP 文件传输的最低公分母系统。就像 Telnet 一样，ftp 也不安全：它以明文形式在网络上传输你的数据，任何人都可以嗅探你的数据包来获取用户名和密码。SSH 替代品 sftp 将 FTP 流量置于 SSH 链接之上，从而确保其安全。

rcp 命令可能对你来说是新的，主要是因为它现在很少被使用。在它鼎盛时期，rcp 是将单个文件复制到另一台服务器的主要方式。与 ftp 一样，scp 通过简单地将数据通过安全的 SSH 连接传输来取代 rcp。sftp 和 scp 之间的区别在于，前者允许你复制多个文件，而后者只发送一个。

## 使用 scp 在机器之间复制单个文件

scp 命令最基本的使用是将文件从当前机器复制到远程机器。你可以使用以下命令执行此操作：

```
scp test.txt 10.0.0.1:
```

