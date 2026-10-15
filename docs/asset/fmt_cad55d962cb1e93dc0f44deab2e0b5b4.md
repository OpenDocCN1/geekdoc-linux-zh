
# 使用 SSH 和 Telnet 进行远程访问

## 本章内容

- 设置 Telnet 服务器
- Telnet 与 SSH 的对比
- 设置 SSH 服务器
- SSH 工具
- 远程 X
- 参考资料

能够远程控制系统是 Ubuntu 的一大亮点——你可以通过多种方式从任何 Linux 机器连接到另一台 Linux 机器。如果你只想快速查看某些内容，或者带宽有限，可以选择仅使用命令行；但你也可以直接连接到 X 服务器，获得完整的图形化控制能力。

了解可用的工具选择在很大程度上是一堂历史课。例如，Telnet 是早期通过命令行连接另一台计算机的方式，但后来已被 SSH 取代。这并不是说你应该完全忽略 Telnet；你需要知道如何使用它，以便在紧急情况下作为备选方案。不过，SSH 更受青睐，因为它更安全。本章将同时介绍这两种方式。

## 设置 Telnet 服务器

你可以在 Synaptic 中找到 Telnet 服务器安装包，位于 `telnetd` 包下。安装完成后，选择“管理，服务”并启用 Telnet。此时请记下你的 IP 地址（使用 sudo 运行 `ifconfig`）。

完成上述操作后，你现在可以启动另一台 Linux 机器并输入 `telnet <你的 IP>`。系统会提示你输入用户名和密码。整个过程看起来应该像这样：

```
[paul@sussannah ~]$ telnet 10.0.0.1
Trying 10.0.0.1...
Connected to 10.0.0.1 (10.0.0.1)
```

```
Escape character is '\'.

Welcome to Caitlin
Running Ubuntu

* All access is logged *

login: paul
Password:
Last login: Sat Jul 9 12:05:41 from 10.0.0.5
[paul@caitlin ~]$
```

### 提示

请注意，服务器的响应是“Welcome to Caitlin, Running Ubuntu”，这是一条自定义消息。你的机器可能会响应为 Ubuntu 及一些版本信息。这样做是不安全的：透露版本号从来都不是明智之举。事实上，即使是说“Ubuntu”也值得商榷。编辑 `/etc` 目录下的 `issue` 和 `issue.net` 文件来修改这些消息。

现在运行 `w` 命令，会显示你从外部 IP 地址连接。

## Telnet 与 SSH 的对比

虽然 Telnet 值得保留作为万无一失的最后手段，但 SSH 几乎在各个方面都更胜一筹。Telnet 速度很快，但不安全。它会将所有文本（包括你的密码）以明文形式发送，任何拥有合适工具的人都能读取。相比之下，SSH 会对所有通信进行加密，因此更耗费资源，但更安全——即使某个政府安全机构出于某种原因嗅探你的数据包，也很难破解加密。

Andy Green 在 fedora-list 邮件列表中发帖，完美地总结了 Telnet 的处境：“由于 Telnet 被普遍认为会助长不良行为，`telnetd` 服务默认并不启用。” 这句话很值得引以为戒：仅在万不得已时才使用 Telnet。

## 设置 SSH 服务器

如果尚未安装，可以通过 Synaptic 添加 `openssh-server` 包来安装 OpenSSH 服务器。如果你已禁用它，可以选择“系统，管理，服务”并勾选“远程 Shell 服务器”框来重新启用。你可能已经猜到了，`sshd` 就是 SSH 服务器守护进程的名称。

存在两种不同的 SSH 版本，称为 SSH1 和 SSH2。后者更新、更安全、功能更多，并且是 Ubuntu 中的默认版本。最好禁用对 SSH1 客户端的支持，以便旧客户端可以连接。这是在此行中 `/etc/ssh/sshd_config` 文件中设置的：

```
#Protocol 2,1
```

为了获得最大安全性，该行应读为：

```
Protocol 2
```

这去掉了注释符号（#），并告诉 `sshd` 你希望它只允许 SSH2 连接。保存文件并退出编辑器。下一步是告诉 `sshd` 重新读取其配置文件，通过执行以下命令：

```
kill -HUP `cat /var/run/sshd.pid`
```

如果返回 `cat: /var/run/sshd.pid: No such file or directory`，则表示你没有运行 `sshd`。下次启动它时，它会读取配置文件并仅使用 SSH2。

你可以通过尝试以 SSH1 模式连接到你的 SSH 服务器来测试此更改。从同一台机器，输入以下内容：

```
ssh -1 localhost
```

`-1` 开关强制 SSH1 模式。如果你成功强制 SSH2 协议，你应该会收到消息 `Protocol major versions differ: 1 vs. 2`。

## The SSH Tools

令许多人惊讶的是，OpenSSH 实际上包含一套工具。我们已经看到了 `ssh`，即连接到其他机器的安全 shell 命令，以及 `sshd`，即接受传入 SSH 连接的 SSH 服务器守护进程。然而，还有 `sftp`，即 `ftp` 的替代品，以及 `scp`，即 `rcp` 的替代品。

你应该已经熟悉 `ftp` 命令，因为它是处理 FTP 文件传输的最低公分母系统。像 Telnet 一样，`ftp` 是不安全的：它以明文形式在网络上传输你的数据，任何人都可以嗅探你的数据包以挑选出用户名和密码。SSH 替代品 `sftp` 将 FTP 流量置于 SSH 链接之上，从而确保其安全。

`rcp` 命令可能对你来说是新的，主要是因为它现在很少被使用。在它那个时代，`rcp` 是将单个文件复制到另一台服务器的主要方式。与 `ftp` 一样，`scp` 通过简单地将数据通过安全的 SSH 连接传输来取代 `rcp`。`sftp` 和 `scp` 之间的区别在于，前者允许你复制多个文件，而后者只发送一个。

## Using scp to Copy Individual Files Between Machines

`scp` 命令最基本的使用是将文件从当前机器复制到远程机器。你可以用以下命令做到这一点：

```
scp test.txt 10.0.0.1:
```

第一个参数是你想要发送的文件名，第二个是你想要发送到的服务器。请注意 IP 地址末尾有一个冒号。这就是你可以指定文件要被复制的确切位置的地方。如果冒号后面什么都没有，如前一个示例中所示，`scp` 会将文件复制到你的主目录。与 SSH 一样，`scp` 会在复制之前提示你输入密码。

你可以重写之前的命令，以便将 `test.txt` 从本地机器复制并保存为服务器上的 `newtest.txt`：

```
scp test.txt 10.0.0.1:newtest.txt
```

或者，如果有一个目录你希望文件被保存，你可以这样指定：

```
scp test.txt 10.0.0.1:subdir/stuff/newtest.txt
```

到目前为止的三个命令都假设你在本地机器上的用户名与你在远程机器上的用户名相同。如果不是这种情况，你需要在远程地址前指定你的用户名，像这样：

```
scp test.txt jap@10.0.0.1:newtest.txt
```

你可以使用 `scp` 将远程文件复制到本地，只需将远程文件指定为源，将当前目录（`.`）指定为目标即可：

```
scp 10.0.0.1:remote.txt .
```

`scp` 命令名义上也能够从一台远程机器复制文件到另一台远程机器，但在 Ubuntu 中此功能尚未得到正确实现。如果发布了补丁——我们希望最终会有——正确的命令将是：

```
scp 10.0.0.1:test.txt 10.0.0.2:remotetest.txt
```

这会将 `test.txt` 从 `10.0.0.1` 复制到 `10.0.0.2` 上的 `remotetest.txt`。如果这有效，你将被要求输入两个服务器的密码。

## Using sftp to Copy Many Files Between Machines

`sftp` 是 `ftp` 和 `scp` 的混合体。连接到服务器使用与 `scp` 相同的语法——你只需指定一个 IP 地址以使用当前用户名连接，或者你可以使用 `username@ipaddress` 指定用户名。你可以 optionally 添加一个冒号和一个

目录操作与 `scp` 相同。连接后，命令与 `ftp` 相同：`cd`、`put`、`mput`、`get`、`quit` 等等。

在 `scp` 的其中一个示例中，我们将一个远程文件复制到本地。使用 `sftp` 也可以完成同样的操作，对话如下：

```
[paul@susannah ~]$ sftp 10.0.0.1
Connecting to 10.0.0.1...
paul@10.0.0.1's password:
sftp> get remote.txt
Fetching /home/paul/remote.txt to remote.txt
/home/paul/remote.txt    100%  23    0.0KB/s   00:00
sftp> quit
paul@susannah ~]$
```
