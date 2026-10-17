
结果是一个列表，每行一个设置了 `SUID` 或 `SGID` 位的文件。列表中可能出现的程序包括 `su`、`ping`、`mount`、`passwd`、`umount` 和 `sudo`。这些程序都有进行这样配置的需求。

大多数系统都有额外的 `SUID` 和 `SGID` 程序，其中某些可能看起来微不足道。如果你对某个程序是否真的需要 `SUID` 或 `SGID` 状态有疑问，应该进一步调查。尝试使用你的包管理工具验证包的完整性，并根据情况对程序名 `SUID` 或 `SGID` 进行网络搜索。你也可以尝试像第 4 节所示，使用 `chmod` 更改程序的 `SUID` 状态，并查看在由普通用户运行时它是否仍能正常工作。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_964_0.png)

属于 `SUID` 或 `SGID` `root` 但不应该是这样的程序可能是系统被入侵的迹。攻击者可能会以此重新配置程序以便更容易制造麻烦。因此，如果你发现此类程序，请调查系统的整体完整性。

# 配置 `SSH`

过去，`Telnet` 是 Linux 和 Unix 系统上常用的远程文本模式登录协议。遗憾的是，`Telnet` 缺乏安全特性。因此，近年来 `SSH` 变得流行，现在是首选的远程登录工具。`SSH` 还可以处理类似于 `FTP` 的文件传输任务。出于这些原因，了解如何配置 `SSH` 会非常有帮助。这项要求了解 `SSH` 的通用知识以及 Linux 内部的 `SSH` 配置文件。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_966_0)

`SSH` 足够复杂，本章仅涵盖其基础知识。更多细节请参考 `OpenSSH` 的文档或相关主题书籍，例如由 Daniel J. Barrett、Richard Silverman 和 Robert G. Byrnes 编写的 `SSH, The Secure Shell: The Definitive Guide, Second Edition`（O'Reilly, 2005），或由 Michael W. Lucas 编写的 `SSH Mastery: OpenSSH, PuTTY, Tunnels and Keys`（CreateSpace, 2012）。

# 理解 `SSH` 基础

Linux 通过多个服务器支持远程登录访问，包括 `Telnet`、虚拟网络计算 (`VNC`) 甚至 `X`。遗憾的是，这些方法都有一个主要缺点：它们以未加密的形式在网络上传输数据。这意味着任何能够监控网络流量的人都可以轻松获取敏感数据，通常包括密码。（`VNC` 和其他少数协议加密密码，但不加密其他数据。）这种安全限制使得这些远程登录工具无法高效使用。如果使用远程访问工具意味着你要放弃敏感数据或危及整个计算机的安全，那么它不是一个非常有用的工具。

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_967_0.png)

使用这些非加密的远程访问工具自负风险。最好不要使用它们。

`SSH` 的设计通过对网络连接的所有部分采用强加密技术来堵这一潜在的重大安全漏洞。`SSH` 加密了密码交换和所有后续数据传输，使其成为一种更安全的远程访问协议。

除了加密外，`SSH` 还提供了文件传输功能以及隧道其他网络协议的能力。这一功能允许非加密协议通过 `SSH` 连接挂载其数据，从而将 `SSH` 的加密优势带给其他协议。

`SSH` 的主要缺点是加密和解密会消耗 CPU 时间。这一事实使得 `SSH` 连接比直接连接慢，并可能降低系统性能。如果你隧道了一个传输更多数据的协议，在使用 `SSH` 时可能会看到更明显的性能下降。然而，安全性的提高通常值得付出这轻微的性能代价。

Linux 有多个 `SSH` 服务器可用，但目前为止最受欢迎的是 `OpenSSH` 服务器 (`www.openssh.org`)。该程序是 `SSH` 协议最早的开源实现之一。`OpenSSH` 随大多数 Linux 发行版一起发布。

`OpenSSH` 可以通过 `xinetd` 超守护进程或通过启动脚本启动。大多数发行版在它们的 `SSH` 包中提供了合适的启动脚本。

如果你对配置执行了更改，可能需要向启动脚本传递 `reload` 或 `restart` 选项，例如 `etc/init.d/ssh reload`。（第 5 节更详细介绍了启动脚本。）无论如何启动，`OpenSSH` 服务器的二进制文件名为 `ssh`。

# 设置 `SSH` 选项

大多数情况下，`SSH` 在首次安装时工作得良好，因此你可能不需要对其配置进行任何更改。但是，如果你需要更改，这些主要通过 `SSH` 主配置文件 `etc/ssh/ssh_config` 处理。你也可以编辑一些额外的文件来限制对 `SSH` 服务器的访问，或更改 `SSH` 管理登录过程的方式

# 配置基础 `SSH` 特性

`etc/ssh/sshd_config` 文件主要包含：

![](img/f74c2c51e1985d4d3a6804ba2887d2f4_969_0.png)

```text
# Port
# 指 SSH 守护进程监听的端口。
# 默认值为 22。你可以将其更改为 1 到 65535 之间的任何端口。
# 更改端口有助于避免攻击。
Port 22

# Protocol
# 指守护进程支持的 SSH 协议。
# 默认值为 2。协议 1 是不安全的，不应使用。
Protocol 2

# HostKeys
# 指守护进程用于向客户端标识自己的主机密钥。
# 默认是 /etc/ssh/ 中所有的密钥。
HostKeys /etc/ssh/ssh_host_rsa_key /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_ecdsap256_key /etc/ssh/ssh_host_ed2519_key

# PubkeyAuthentication
# 指是否允许公钥认证。
# 默认值为 yes。
PubkeyAuthentication yes

# PasswordAuthentication
# 指是否允许基于密码的认证。
# 默认值为 yes。
PasswordAuthentication yes

# ChallengeResponseAuthentication
# 指是否允许挑战响应认证。
# 默认值为 no。
ChallengeResponseAuthentication no

# UsePAM
# 指是否使用可插认证模块。
# 默认值为 yes。
UsePAM yes

# PermitRootLogin
# 指是否允许 root 用户通过 SSH 登录。
# 默认值为 no。
PermitRootLogin no

# Subsystem
# 指守护进程支持的子系统。
# 默认值为 sftp。
Subsystem sftp internal
```

请确保**私**钥得到了妥善的保护；如果入侵者获取了这些密钥之一，入侵者就可以伪装你的系统。通常，这些文件应该具有 `0600 (-rw-------)` 权限并由 `root` 所有。然而，**公**钥文件（以 `.pub` 扩展名结尾的文件）应该对所有用户可读。

当你配置客户端系统时，可能想要考虑创建一个主机密钥的全局缓存。如前所述，`ssh` 程序会为每个单独的用户记录主机密钥。（它将这些密钥存储在 `~/.ssh/known_hosts` 文件中。）当你设置客户端时，可以填充一个全局的 `ssh_known_hosts` 文件，该文件通常存储在 `/etc` 或 `etc/ssh` 中。这样做可以确保公钥列表与你用于填充全局文件的源一样准确。它还消除了用户首次连接到你选择包含在全局文件中的主机时所弹出的确认消息。

你该如何创建这个文件呢？一种简单的方法是从已经连接到你想要包含的服务器的用户账户中拷贝该文件，如下所示：

```
$ sudo cp /home/rich/.ssh/known_hosts /etc/ssh_known_hosts
[sudo] password for Christine:
$
```

在过去，你可以在文本编辑器中查看 `SSH` 的已知主机文件，因为它是一个文本模式的文件。现在 `OpenSSH` `v4.0` 及更高版本支持对该文件的数据进行哈希处理。当启用此功能时，信息将经过哈希处理并存储。其原理是，你仍然能够验证你连接的 `SSH` 服务器，因为输入的主机名哈希值将与存储的主机名哈希值匹配。然而，如果攻击者偷了你的已知主机文件，攻击者将无法确定你曾连接过的计算机的身份。这种哈希处理一个不幸的副作用是，你无法判断它描述了哪些服务器。

## 控制 `SSH` 访问

你可以通过多种方式限制谁可以访问 `SSH` 服务器。最明显且基础的方法是通过密码验证。通常的 `SSH` 验证方法是使用用户名和密码，就像 `Telnet` 一样。`ssh` 客户端程序会自动发送用户名，或作为命令行的一部分发送用户名。因此，当你通过 `ssh` 登录时，你不会看到用户名提示，如下例所示：

```
$ ssh Christine@192.168.56.101
Christine@192.168.56.101's password:
Last Login: Wed Nov 12 10:20:36
$
```
