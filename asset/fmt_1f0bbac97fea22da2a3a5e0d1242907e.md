
```
[paul@susannah~]$ $ telnet 10.0.0.1
Trying 10.0.0.1...
Connected to 10.0.0.1 (10.0.0.1)
Escape character is '^'

欢迎来到 Caitlin
正在运行 Fedora Core

* 所有访问均已记录 *

login: paul
Password:
上次登录时间：Sat Jul 9 12:05:41 来自 10.0.0.5
[paul@caitlin~]$
```

> 注意，服务器响应的是“Welcome to Caitlin, running Fedora Core”，这是一个自定义消息。你的机器可能会响应 Fedora Core 5 和你的内核版本。这是不安全的：泄露数字永远不是一个明智之举。事实上，直接说 Fedora 也是值得商榷的。通过编辑 `/etc` 目录下的 `issue` 和 `issue.net` 文件可以更改这些消息。

现在运行 `w` 命令将显示你正从外部 IP 地址连接。

# 设置 SSH 服务器

OpenSSH 服务器在 Fedora 中被设置为自动安装并运行，这意味着它可能已经在你的系统上工作了。然而，如果你禁用了它，可以通过选择“系统设置”、“服务器设置”、“服务”并勾选 `sshd` 框来重新启用它。正如你可能已经意识到的，`sshd` 是 SSH 服务器守护进程的。

SSH 有两个不同的版本：SSH1 和 SSH2。后者更新、更安全、功能更多，并且是 Fedora Core Linux 的默认设置。然而，对 SSH1 客户端的支持也默认保持开启，以便旧版客户端可以连接。由于它的安全性较低，如果你没有专门依赖 SSH1 的用户，你应该禁用 SSH1。

要做到这一点，请编辑 `/etc/ssh/sshd_config` 文件并查找此行：

```
#Protocol 2,1
```

编辑此行使其变为：

```
Protocol 2
```

这删除了注释符号 (`#`) 并告诉 `sshd` 你希望它只允许 SSH2 连接。保存文件并退出编辑器。下一步是执行执行此命令来告诉 `sshd` 重新读取其配置文件：

```
kill -HUP `/var/run/sshd.pid`
```

如果系统返回 `cat: /var/run/sshd.pid: No file or directory`，意味着你之前没有运行 `sshd`。当你下一次启动它时，它将会读取配置文件并仅使用 SSH2。

你可以通过尝试在 SSH1 模式下连接到你的 SSH 服务器来更改这一点。对于同一台机器，输入：

```bash
ssh -1 localhost
```

`-1` 强制使用 SSH1 模式。如果你成功强制使用了 SSH2 协议，你应该会收到 `Protocol major versions differ: 1 vs. 2` 的消息。

# SSH 工具

OpenSSH 由一组工具组成，这让很多人惊讶。你已经见过 `ssh`（用于连接到其他机器的客户端）以及 `sshd`（接受 SSH 连接的服务器守护进程）。然而，还有 `sftp`（替代 `ftp` 的工具）以及 `scp`（替代 `rcp` 的工具）。

你应该已经熟悉 `ftp` 命令，因为它在网络中用于传输数据。像 Telnet 一样，`ftp` 是不安全的：它以明文发送你的数据。通过 SSH，`scp` 将数据传输到安全连接。

## 使用 scp 在机器间复制单个文件

`scp` 最基本的用法是从当前机器复制文件到远程机器。你可以通过以下命令实现：

```bash
scp test.txt 10.0.0.1:
```

第一个参数是你想要发送的文件名，第二个是你想发送到的服务器。注意 IP 地址后面有一个冒号。这是你指定文件保存的确切位置。如果你在冒号后什么都不写（如上面的示例），`scp` 将文件复制到你的主目录。在复制之前，SSH 会提示你输入密码。

你可以重写之前的命令，以便从本地机器复制 `test.txt` 并在服务器上保存为 `newtest.txt`：

```bash
scp test.txt 10.0.0.1:newtest.txt
```

或者，如果你想将文件保存到某个目录，可以这样指定：

```bash
scp test.txt 10.0.0.1:subdir/stuff/newtest.txt
```

到为止的三个命令都假设你在本地机器上的用户名与远程机器上的用户名相同。如果事实如此，你需要在远程地址之前指定用户名，如下：

```bash
scp test.txt japh@10.0.0.1:newtest.txt
```

你可以通过指定远程文件为源、当前目录 (`.`) 为目标，使用 `scp` 复制远程文件到本地：

```bash
scp 10.0.0.1:remote.txt
```

## 使用 sftp 在机器间复制多个文件

`sftp` 是 `ftp` 和 `scp` 的结合体。连接到服务器使用的语法与 `scp` 相同——你只需要指定 IP 地址来连接到你的当前用户名，或者可以使用 `username@ipaddress` 指定一个用户名。你可以像 `scp` 一样，可选地添加一个冒号和目录。连接成功后，使用的命令与 `ftp` 相同：`cd`、`put`、`mput`、`get`、`quit` 等。

在其中一个 `sftp` 示例中，我们可以通过以下对话使用 `sftp` 完成相同的操作：

```
[paul@susannah-$] sftp 10.0.0.1
Connecting to 10.0.0.1...
paul@10.0.0.1's password:
sftp> get remote.txt
Fetching /home/paul/remote.txt to remote.txt
/home/paul/remote.txt      100% 23 0.0KB/s 00:00
sftp> quit
paul@susannah-$
```

尽管由于许多系统不支持 SSH（特别是 Windows 系统），FTP 仍然占据着地位，但 SFTP 正在变得流行。除了它可以确保客户端和服务器之间所有通信的安全外，SFTP 流行是因为客户端和服务器之间的初始连接是通过 22 端口通过 `ssh` 守护进程建立的。使用 SFTP 的守护进程连接到标准的 `ssh` 守护进程，验证身份后，将其移交给 SFTP 服务器。这样做的好处是减少了攻击向量，因为只要 `ssh` 守护进程是安全的，无法无法访问 SFTP 服务器，也无法对其攻击。

## 使用 ssh-keygen 启用密钥登录

SSH 系统存在一个弱环节，而且不可避免地，这个环节就在用户身上。无论系统管理员在培训用户小心保管密码方面做出了多少努力，世界各地显示器上都贴着写有“password”字样的便利贴。诚然，它混合了字母和数字，但可以在一秒钟内通过暴力破解破解。暴力破解（Brute-forcing）是尝试每种可能的密码的方法，从可能的词汇（如 `password` 及其变体，或 `god`）开始，然后只是尝试随机字母（例如 `a`, `aa`, `ab`, `ac` 等）。

即使是强密码，也不超过 16 个字符；需要长时间才能暴力破解的密码仍然可能被破解。解决方案是使用基于密钥的登录，它为你的机器生成唯一的 1024 位私钥和公钥。这些密钥即使对于最快的计算机也需要一生才能破解，你可以用密码对其进行备份以防止他人使用它们。

创建 SSH 密钥通过 `ssh-keygen` 命令完成，如下：

```
ssh-keygen -t dsa
```

# 第 15 章 使用 SSH 进行远程访问

当提示你将密钥保存何处时按回车，并在要求输入时输入短语。这个短语只是用于保护密钥的密码——如果你愿意，可以留空，但这样做允许其他人在他们成功登录后，使用你的账户连接到远程机器。

密钥生成后（取决于机器速度，可能需要最多 30 秒），更改目录到 `~/.ssh` (`cd ~/.ssh`)，这是一个存储密钥并存放 ssh 主机列表的隐藏目录。你会看到 `id_rsa` 和 `id_rsa.pub` 文件。第一个是你的私钥，绝不应给出。第二个是你的公钥，可以安全分发。你需要将公钥复制到你想通过基于密钥的 SSH 连接的每台服务器上。

使用 `scp`，你可以将公钥复制到你的服务器，如下：

```
scp id_rsa.pub 10.0.0.1:
```

这将 `id_rsa.pub` 放置在你 `10.0.0.1` 上的家目录下。下一步是正常 SSH 登录 `10.0.0.1` 并将其设置为授权密钥。然后你可以以自己的身份 SSH 登录并输入

```
touch .ssh/authorized_keys
cat id_rsa.pub >> .ssh/authorized_keys
chmod 400 .ssh/authorized_keys
```
