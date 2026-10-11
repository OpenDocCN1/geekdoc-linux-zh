
```
# grep PermitRootLogin /etc/ssh/sshd_config

PermitRootLogin no
```

一旦你更改了 `sshd_config`，请重启 `sshd` 服务。从那时起，如果你使用 `ssh` 从远程客户端登录到系统，你必须以普通用户身份登录，并使用 `su` 或 `sudo` 变为 `root` 用户。

## 使用 SSH 客户端工具

已经创建了许多访问远程 Linux 系统的工具来利用 `ssh` 服务。最常用的工具是 `ssh` 命令，它可以用于远程登录、远程执行以及其他任务。如 `scp` 和 `rsync` 等命令可以在 `ssh` 客户端和服务器系统之间一次复制一个或多个文件。`sftp` 命令提供了一个类似 FTP 的接口，用于遍历远程文件系统并在系统之间交互式地获取和放置文件。

默认情况下，所有 SSH 相关的工具都使用标准的 Linux 用户名和密码进行身份验证，且均通过加密连接进行。SSH 还支持基于密钥的身份验证，用于配置客户端和 `ssh` 服务器之间的无密码身份验证（在本章稍后的“使用基于密钥（无密码）身份验证”节中描述）。

## 使用 ssh 进行远程登录

从另一台 Linux 计算机使用 `ssh` 命令，测试你是否能够登录到运行你 `ssh` 服务的 Linux 系统。`ssh` 命令是你将用于访问正在配置的服务器上的 shell 的命令之一。

尝试使用 `ssh` 命令从另一个 Linux 系统登录到你的 Linux 服务器。（如果你没有另一台系统，可以通过通过输入 `localhost` 代替 IP 地址并以本地用户登录来模拟这一点）。以下是远程登录到 `10.14.60.23` 上 `johndoe` 账户的示例：

```
$ johndoe@10.14.60.23

The authenticity of '10.14.60.23' (10.14.60.23) can't be established.

RSA key fingerprint is A4:28:35:89:6d:08:fa:99:1e:55:89

Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added '10.14.60.23' (RSA) to the list of known hosts

johndoe@10.14.60.23 password: ***********
```

如果你是第一次使用 `ssh` 命令登录到该远程系统，系统将要求你确认是否要连接。输入 `yes` 并按回车。在提示时，输入用户的密码。

当你在输入 `yes` 接受远程主机的公钥时。此时，远程主机的公钥将下载到客户端的 `~/.known_hosts` 文件中。这两个系统之间交换的数据可以使用 RSA 非对称加密进行加密和解密（参见第 23 章“高级 Linux 安全”）。

一旦你登录到远程系统，就可以开始输入 shell 命令。该连接的功能就像普通登录一样。唯一的区别是数据在网络上经过了加密。

当你完成后，输入 `exit` 退出远程连接。连接将关闭，你将返回到本地系统的命令提示符。（如果你在退出远程 shell 后本地 shell 没有返回，输入 `~` 通常可以恢复连接。）

```
$ exit

logout

Connection to 10.14.60.23 closed.

$
```

一旦你连接到服务器，你本地系统子目录 `~/.ssh/known_hosts` 中的文件就会存在。该文件包含了远程主机的公钥及其 IP 地址。你服务器的公钥和私钥存储在 `/etc/ssh` 目录中。

```
$ ls .ssh

known_hosts

$ cat .ssh/known_hosts

10.140.67.23 ssh-rsa

AAAB3NzaN3C2EAAAABiWAAAEQoyfJKylw2nhmpHE4YLPAAZY9ZHEDBE71
```

> 提示 在较旧版本的 Fedora 发行版中管理服务，请使用 `chkconfig` 命令来启动 `ssh` 服务并确保它在启动时启动。

修改 `netfilter/iptables` 防火墙设置以允许 `openssh-client` 访问 `22` 端口（防火墙内容见第 25 章“网络上的 Linux 安全防护”）。一旦服务启动运行且防火墙配置恰当，你就应该能够使用 `ssh` 客户端命令通过 `ssh` 服务器访问你的系统。

> 注意 最好配合 `ssh` 服务使用 TCP Wrapper。TCP Wrappers 见第 25 章“网络上的 Linux 安全防护”。

对 `ssh` 守护进程的任何进一步配置都可以在 `/etc/ssh/sshd_config` 文件中处理。至少将 `PermitRootLogin` 设置从 `yes` 改为 `no`。这将阻止任何人远程以 `root` 登录。

```
# grep PermitRootLogin /etc/ssh/sshd_config

PermitRootLogin no
```

一旦你更改了 `sshd_config`，请重启 `ssh` 服务。从那时起，如果你使用 `ssh` 从远程客户端登录到系统，你必须以普通用户身份登录，并使用 `su` 或 `sudo` 变为 `root` 用户。

## 第 13 章：理解服务器管理

你可以使用 `scp` 命令配合 `-r` 参数进行递归复制。与其传递文件，不如将目录名称传递给 `scp` 命令，文件系统中该点下的所有文件和目录都会复制到另一个系统。

```
$ scp johndoe@10.140.67.23:/usr/share/man/man/ /tmp/
```
