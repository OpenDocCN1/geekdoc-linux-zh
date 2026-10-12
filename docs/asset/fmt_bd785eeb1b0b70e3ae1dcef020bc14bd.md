
### 25.7. 故障排除

使用`ssh -v`获取关于连接的调试信息。

```
paul@debian5:~$ ssh -v bert@192.168.1.92
OpenSSH_4.3p2 Debian-8ubuntu, OpenSSL 0.9.8 05 Sep 2006
debug1: Reading configuration data /home/paul/.ssh/
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for *
debug1: Connecting to host 192.168.1.92 [192.168.1.92] port 22.
debug1: Connection established.
debug1: identity file /home/paul/.ssh/identity type -1
debug1: identity file /home/paul/.ssh/id_rsa type 1
debug1: identity file /home/paul/.ssh/id_dsa type -1
debug1: Remote protocol version 1.99, remote software version OpenSSH_3
debug1: match: OpenSSH_3.9p1 pat OpenSSH_3.*
debug1: Enabling compatibility mode for protocol 2.0
...
```

## 25.8. sshd

`ssh` 服务器称为 `sshd`，由 `openssh-server` 包提供。

```
root@ubuntu204~# dpkg -l openssh-server | tail -1 openssh-server 1:5.9p1-5ubuntu secure shell (SSH) server,...
```

## 25.10. ssh-agent

`sshd` 服务器使用的公钥位于 `/etc/ssh/` 且全局可读。私钥仅供 `root` 读。

```
root@ubuntu204~# ls -l /etc/ssh/ssh_host_*
-rw------- root root 668 Jun 7 2011 /etc/ssh/ssh_host_rsa_key
-rw-r--r-- root root 598 Jun 7 2011 /etc/ssh/ssh_host_rsa_key.pub
-rw------- root root 1679 Jun 7 2011 /etc/ssh/ssh_host_dsa_key
-rw-r--r-- root root 390 Jun 7 2011 /etc/ssh/ssh_host_dsa_key.pub
```

使用 `ssh-keygen` 生成密钥时，你可以选择输入密码短语来保护密钥访问。为了避免每次输入此密码短语，可以将密钥添加到 `ssh-agent`。大多数 Linux 发行版会在登录时自动启动 `ssh-agent`。

```
root@ubuntu204~# ps -ef | grep ssh-agent
2405 2365 0 08:13 00:00 /usr/bin/ssh-agent...
```

此截图显示了如何使用 `ssh-add` 列出当前添加到 `ssh-agent` 的密钥。

```
paul@debian::- ssh-add -L
ssh-rsa AAAAB3NzaC1yc2EAAAADAABABQQ9yZ6y+HpqW2z1T4DtkqMnMW8bWU/OPG33fUv1/NHouilmpe20df/u2u4mljfde/0/tTMGSBenYCR8CT9Yta
```

## 25.11. 练习：ssh

1. 在服务器上安装 `sshd`
2. 在 `ssh` 配置文件中验证仅允许协议版本 2
3. 使用 `ssh` 登录到服务器，显示当前目录然后退出服务器
4. 使用 `scp` 从你的电脑将文件复制到服务器
5. 使用 `scp` 从服务器将文件复制到你的电脑
6. （可选）为你的密钥设置密码短语，然后将此密钥添加到 `ssh-agent` 并测试你到服务器的无密码 `ssh`。

# 25.12. 解决方案：ssh

0. 确保你有两台 Linux 计算机的权限，或者与伙伴合作完成此练习。在本次练习中，我们将其中一台机器命名为服务器。
1. 在服务器上安装 `sshd`

```
apt-get install openssh-server (on Ubuntu/Debian)
yum -y install openssh-server (on CentOS/Fedora/Red Hat)
```

2. 在 `ssh` 配置文件中验证是否只允许协议版本 2。

```
grep Protocol /etc/ssh/ssh* -config
```

3. 使用 `ssh` 登录服务器，显示你的当前目录并退出服务器。

```
userclient$ ssh user@server-ip-address
user@server$ pwd
/home/user
user@server$ exit
```

4. 使用 `scp` 将文件从你的电脑拷贝到服务器。

```
scp localfile user@server:
```

5. 使用 `scp` 将文件从服务器拷贝到你的电脑。

```
scp user@server:/serverfile
```

6. （可选，仅当 Linux 安装了图形化界面 Linux 时有效）在服务器上安装 `xeyes` 包，并使用 `ssh` 在服务器上运行 `xeyes`，将其显示在你的客户端上。

```
on the server:
apt-get install xeyes
on the client:
ssh -X user@server-ip
xeyes
```

7. （可选，与上述相同）在 `firefox` 中创建一个书签，然后退出客户端和服务器上的 `firefox`。使用 `ssh -X` 在你的显示器上运行 `firefox`，但在你邻居的电脑上。你看到你的书签了吗？
8. 使用 `ssh-keygen` 创建一个无密码保护的密钥对。在你和邻居之间建立无密码 `ssh`（在你的客户端和服务器之间）。

参阅书籍 “setting up passwordless ssh” 中的解决方案。

9. 验证服务器密钥的权限是否正确；公钥对所有人可读，私钥仅限 `root` 访问。

```
ls -l /etc/ssh/ssh_host_* *
```

10. 验证 `ssh-agent` 是否正在运行。

```
ps fax | grep ssh-agent
```

11. （可选）用密码保护你的密钥对，然后将此密钥添加到 `ssh-agent` 并测试到服务器的免密 `ssh`。

```
man ssh-keygen
man ssh-agent
man ssh-add
```

# 第26章 NFS简介

网络文件系统（简单称为 `nfs`）自 80 年代以来让我们能够与网络上的其他计算机共享目录。

在本章中，我们将学习如何设置 `nfs` 服务器和 `nfs` 客户端。

# 26.1. NFS 协议版本

旧的 `nfs` 版本 2 和 3 虽然默认使用 `udp`，但它们可以使用 `tcp`。较新的 `nfs` 版本 4 提供了一个性能更好、安全性更高的指定协议。

`NFS` 版本 4 定义在 2000 年的 `rfc 3010` 和 2003 年的 `rfc 3530` 中，需要 `tcp`（端口 `2049`）。它在挂载共享时还支持 `Kerberos` 认证作为选项。

`NFS` 版本 2 和 3 仅验证主机。

# 26.2. rpcinfo

客户端使用 `rpc` 连接到服务器（在 Linux 上这可以通过 `portmap` 守护进程管理）。查看 `rpcinfo` 以查找运行的 `nfs` 及其服务。
