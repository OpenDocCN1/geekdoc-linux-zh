
下面的章节练习让你在环境中练习使用 `rcp` 命令。

## EXERCISE 11.20

使用 `rcp` 命令将文件从你的机器复制到网络上的另一台机器。你使用了什么命令？它做了什么？

## 11.8.10 Secure Shell and Related Commands

源自 BSD 的 `r` 命令（`rsh`、`rcp`、`rlogin` 等）是不安全的，`telnet` 也是如此。Secure Shell（`SSH`）是它们的现代替代品，消除了对 `.rhosts` 和 `hosts.equiv` 文件的需求，并且可以通过加密密钥对用户进行身份验证；它还提高了其他基于 TCP/IP 的应用程序的安全性，例如 X Windows 转发，该转发通过 SSH 加密连接透明地“隧道传输”它们。处理安全连接协议的程序称为 Secure Shell daemon，`sshd`。

`rsh` 命令的安全版本称为 `ssh`。`rsh` 和其他 UNIX `r` 命令以明文（有时称为纯文本）与远程主机通信，而 `ssh` 使用强加密来传输数据，包括命令、密码和文件。每当你的数据传输到你的网络时，`ssh` 会自动对其进行加密，并在数据到达预期接收者时自动解密。结果是透明加密——即发送方和接收方都不知道加密/解密过程。

由于这些原因，`ssh` 已成为 LAN 或 Internet 中安全终端连接的事实标准。例如，`ssh`、`scp` 和 `sftp` 使用的加密会话可以防止任何人在嗅探数据包时理解正在进行的通信。此外，`ssh` 中使用的身份验证方法可以防止任何类型的欺骗，例如 IP 地址欺骗。

`SSH` 版本 2 是 PC-BSD 和 Solaris 的默认协议。它有三个组件：

- `1.` `SSH Transfer Protocol`: Handles server identification, encryption algorithm and key encryption, and manages the channel between client and server

- `2.` `SSH` 认证协议：验证客户端机器上用户登录角色的有效性

- `3.` `SSH` 通道协议：处理远程 shell 会话、端口转发或 X11 转发的加密通道和逻辑连接状态

以下小节假定 `ssh` 服务已在不仅你的客户端本地计算机上，而且在远程服务器主机上默认安装并已启动。我们不提供如何获取或安装 `ssh` 客户端或服务器程序的细节，但我们提供了如何对 `sshd` 守护进程进行初步配置以及如何在 PC-BSD 和 Solaris 上启动/重启守护进程的说明。

默认情况下，`sshd` 在我们的 PC-BSD 和 Solaris 系统上均已启用并启动，要使用本节所示的 `ssh` 命令，我们只需让本地客户端机器和远程服务器机器上的守护进程最初交换加密密钥，如以下示例会话所示。

有关 `ssh`、`scp` 和 `sftp` 命令的更完整描述，请参阅这些命令的手册页。

## 11.8.10.1 ssh 的初步配置以及如何启动/重启 sshd 守护进程

以下小节给出了 PC-BSD 和 Solaris 上 `ssh` 的初步配置信息，并展示了如果守护进程未在默认情况下启动，或因某种原因已停止，如何启动或重启守护进程。

### 1. PC-BSD 上 ssh 的配置

如果你不想在使用 `ssh` 时输入密码，并且使用 RSA 或 DSA 密钥进行身份验证，可以在运行其他应用程序之前运行 `ssh-agent` 命令。X 用户通常通过他们的 `.xsession` 或 `.xinitrc` 文件来执行此操作。有关详细信息，请参阅 `ssh-agent` 的手册页。

#### a. 使用 `ssh-keygen` 命令生成密钥对并将其放置在你的 `$HOME/.ssh` 目录中。你的公钥是 `$HOME/.ssh/id_dsa.pub` 或 `$HOME/.ssh/id_rsa.pub`，具体取决于你分别使用 DSA 或 RSA 进行身份验证。

#### b. 将你的公钥发送给为你设置提交者权限的人员，以便将其放入 `/etc/ssh-keys/` 中的你的登录项中。默认情况下，在我们的 PC-BSD 和 Solaris 机器上，这些密钥已自动生成并存储。

### 2. 在 PC-BSD 上启动或重启 sshd

要确定 `sshd` 是否正在运行，或重启服务，运行以下命令序列：

```
% /etc/rc.d/sshd start

sshd already running? (pid=1523)
```

```
% /etc/rc.d/sshd restart

Stopping sshd.
Waiting for PIDS: 1523
Starting sshd.
%
```

启动 `ssh` 守护进程的另一种方法是，通过在 `/etc/rc.conf` 文件中添加以下行，在启动时自动启动 `sshd` 服务器：

```
sshd_enable="YES"
```

现在通过在命令行输入以下内容启动 `sshd` 服务器：

```
% /etc/rc.d/sshd start
```

### 1. Solaris 上 ssh 的配置

在本地客户端机器上，检查文件 `/etc/ssh_config` 和 `/etc/ssh/sshd_config`，分别是 `ssh` 的客户端和服务器端配置文件。这些文件中未被注释掉的行（即第一个字符不是 `#`），是你的 `ssh` 会话的配置设置，分别作为客户端和服务器。

### 2. 在 Solaris 上启动或重启 sshd

要启动远程服务器上的 `sshd`，如果它尚未运行，运行以下命令：

```
$ svcadm enable svc:/network/ssh:default
```

要重启远程服务器上的 `sshd`，输入以下内容：

```
$ svcadm restart svc:/network/ssh:default
```

## 11.8.10.2 ssh 命令

`ssh` 命令允许你执行基本上与 `telnet`、`rlogin` 和 `rsh` 命令相同的任务，但方式更安全。如果你机器名在远程主机上的 `/etc/host.equiv` 或 `/etc/shosts.equiv` 文件中找到，并且你的登录名在你的机器和远程机器上相同，则允许你登录到远程主机或在其上执行命令。如果你登录名在本地和远程主机上不同，并且你的本地机器名和其上的登录名包含在 `~/.rhosts` 或 `~/.shosts` 文件中，也允许你登录到远程主机。`ssh` 还使用额外的安全功能，包括公钥加密，在允许用户登录到远程机器之前对用户及其主机进行身份验证。我们仅描述 `ssh` 命令中一些相当基本的功能，这些功能用于远程登录、远程执行命令以及在客户端和服务器机器之间传输文件。以下是 `ssh` 命令的简要描述：

### SYNTAX

```
ssh [-option(s)] [-option argument(s)] [command]
```

Purpose: `ssh`（SSH 客户端）是一个用于登录远程机器并在远程机器上执行命令的程序。它旨在取代 `rlogin` 和 `rsh`，并在不安全的网络上为两台不被信任的主机之间提供安全的加密通信。

Output: 通过安全通道到网络或互联网上的主机的远程连接

### Common Options and Features:

- `-D [bind_address:]port` 指定本地“动态”应用级端口转发。这通过在本地端分配一个套接字来监听端口，可选择绑定到指定的 `bind_address`。

- `-L [bind_address:]port:host:hostport` 指定本地（客户端）主机的给定端口应转发到远程端的给定主机和端口。

- `-l login_name` 指定在远程机器上登录的用户名。这也可以在配置文件中按主机指定。

你可以使用 `ssh` 命令像使用 `rsh` 命令一样登录到远程主机或在远程主机上执行命令。例如，在以下会话中，从 PC-BSD 客户端机器开始，你在名为 `192.168.0.12` 的远程主机 `ssh` 服务器上启动一个 `ssh` 会话，使用默认用户名（在本例中与本地客户端机器上的用户名相同），然后退出远程主机：

```
% ssh 192.168.0.12

The authenticity of host '192.168.0.12 (192.168.0.12)' can't be established.
RSA key fingerprint is 37:a2:db:ce:97:17:ce:37:26:bf:58:9d:a2:ed:1c:0f.
No matching host key fingerprint found in DNS.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.0.12' (RSA) to the list of known hosts.
Password: xxxxx
Last login: Tue Sep 23 08:51:38 2014

OpenIndiana (powered by illumos) SunOS 5.11 oi_151a9

November 2013

$
...
```
