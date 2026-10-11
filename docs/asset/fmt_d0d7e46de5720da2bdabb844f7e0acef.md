
```bash
# ssh user0@172.168.1.1
主主机 '172.168.1.1' (172.168.1.1) 的真实性无法确认。
RSA 密钥指纹为
5a:29:fd:c7:ef:5a:3d:4f:b1:99:05:f1:5f:ac:46:cb。
确定要继续连接吗？(yes/no)?n
警告：已将主机 '172.168.1.1' (RSA) 永久添加到主机列表。
user0@172.168.1.1 password:
最后登录：Jun 3 06:22:12 2010 来自自 172.168.1.20
user0@RHEL01~$
```

根据登录提示，你可以判断出你登录的主机与你登录的身份不同。在这种情况下，你可以看到你以 `user0` 的身份登录到了 `RHEL01`。当你在远程主机上完成工作后，可以使用 `exit` 命令返回本地系统或关闭连接。

由于 SSH 只是系统管理员的一项常用工具，我推荐两个产品。如果你使用 Windows 客户端（笔记本电脑/桌面式电脑）并想通过 SSH 连接到 Linux 服务器，可以下载并使用 PuTTY（免费）或 SecureCRT（收费，但更好）。如果你已经在 Linux 上，可以直接使用系统内置的 shell，尽管有很多免费工具可以帮助你轻松地管理 SSH 连接。

## 防火墙和 SELinux 配置

在涉及 Linux 远程管理时，SSH 是标准。因为 Red Hat 默认安装了 SSH，并且已经有一条防火墙规则供你开始远程管理，因此你不需要创建任何额外的规则。不过，按照良好的习惯，你应该验证该规则是否确实生效。

由于 SSH 使用 TCP 端口 22 进行远程访问，你应该从 `/etc/sysconfig/iptables` 中查询任何规则：

```bash
# /etc/sysconfig/iptables | grep 22
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
```

在防火墙规则生效的情况下，你还需要查看 SELinux 对 SSH 服务的限制。

- **步骤 1.** 查询与 SSH 相关的布尔值（Boolean values）：

```bash
# getseboolean -a | grep ssh
allow_ssh_keysgen -> off
sftpd_write_ssh_home -> off
ssh_sysadmn_login -> off
```

> **考试技巧**
> 
> `sftpd_write_ssh_home` 布尔值是 RHEL6 新引入的，且 `run_ssh_inetd` 已删除。

你只需要更改这里的选项之一。在本章后面的部分，我们将讨论通过使用公钥和私钥基于基于安全性，这需要开启第一个布尔值。

- **步骤 2.** 启用所需的布尔值：

```bash
# setseboolean -P allow_ssh_keysgen=1
```

- **步骤 3.** 验证值是否已更改：

```bash
# getseboolean -a | grep ssh
allow_ssh_keysgen -> on
sftpd_write_ssh_home -> off
ssh_sysadmn_login -> off
```

此时，SSH 的防火墙和 SELinux 要求已处理完毕。SSH 不需要许多更改即可直接工作，但随着你学习的深入，你将遇到需要对防火墙规则和 SELinux 进行多处更改的服务。

## SSH 安全

在安全方面，SSH 有许多不同的选项。首先，让我们来看一些主机安全。在设置 SSH 服务时，你可以利用 TCP Wrappers 服务提供额外保护。假设你只想允许来自 `172.168.1.0/24` 网络连接到 `RHEL01` 主机。

步骤 1. 使用 TCP Wrappers 限制可以连接服务器的主机：

```bash
# echo "sshd:172.168.1.1" >> /etc/hosts.allow
# echo "ALL: ALL" >> /etc/hosts.deny
```

这允许 `172.168.1.0/24` 网络内的所有客户端进行连接。

以确保我们没有添加您预期的额外键。

## 第 13 章：远程访问 317

当公钥就绪后，你还需要调整 SSH 服务器（RHEL01）上的主配置，以允许通过公钥/私钥进行验证。

- 步骤 3。在 `sshd_config` 文件中，更改以下选项：

```bash
PasswordAuthentication no
PubKeyAuthentication yes
```

此更改防止用户使用公钥/私钥组合之外的其他方式登录。

- 步骤 4。重启 SSH 服务使设置生效：

```bash
# service sshd restart
Stopping sshd: [ OK ]
Starting sshd: [ OK ]
```

- 步骤 5。尝试从 Client02 主机以 `user01` 用户身份连接到 `RHEL01`，确保密钥认证工作正常：

```bash
# ssh user01@172.168.1.1
user01@172.168.1.1:password:
Last login: Thu Jun 3 06:22:22 2010 from 172.168.1.20
[user01@RHEL01 ~]$
```

## 端口转发

如前所述，端口转发允许你连接到中心网关，并在你的网络内部形成附加连接。这种能力通过强制所有连接流经中心网关来增加安全性，网关通常会进行审计以跟踪谁登录了。这种集中管理是通过使用端口转发实现的，每个连接建立到网关，然后转发到另一个地方。

语法：`ssh username@hostname -L local-port:remote-hostname:remote-port`

让我们来看一个示例。假设在 RHEL01 上，你想创建一个到 RHEL01 的端口转发，并允许 SSH 连接仅来自 RHEL01。你可以使用以下命令在 RHEL01 上使用初始隧道：

```bash
# ssh user01@172.168.1.2 -L 1234:172.168.1.2:22
```

在 RHEL01 上执行此命令后，你现在应该拥有一个转发到 RHEL02 的隧道。其他用户现在可以在 RHEL01 上本地使用 SSH，并被转发到 RHEL02。

另一个示例是将所有流量发送到特定站点：

```bash
# ssh -N -L 8080:localhost:80 <site>
```

红帽® 考试实战指南：RHCSA™ 和 RHCE® 指南与实验手册

`-N` 选项保持 SSH 连接不处于交互模式。现在，如果你设置浏览器使用代理连接到端口 8080 上的 `localhost`，你就能安全地访问命令中指定的站点。虽然端口转发对于测试或连接非常有用，但实际上世界上有很多很棒的程序，可以实现比仅使用命令行更易于的管理和隧道创建。

## VNC 服务器

对服务器进行远程访问很棒，但如果终端用户来电说她的系统出了问题，该怎么办呢？她很可能不仅仅是在使用 Shell，而且服务器已经乱套了。你不需要使用 SSH 来远程修复问题，因为总有一个替代方案：VNC。VNC 服务器允许你远程进入用户的系统并查看她的桌面。通过终端用户的桌面视图，你可以更轻松地排查她正在遇到的问题。设置 VNC 服务器并不困难，事实上，它有时会作为桌面包的一部分预安装。

- 步骤 1。在 RHEL02 上安装 `vnc-server` 软件包：

```bash
# yum install -y tigervnc-server
```

- 步骤 2。查询以确保包已安装：

```bash
# rpm -qa | grep tiger
tigervnc-server-1.0.90-0.2010115svn3945.el6.x86_64
```

> 迁移提示
> 
> RHEL6 可用的 VNC 包是 `tigervnc`。
> 
> RHEL5 及更早版本有一个名为 `vnc` 和 `vnc-server` 的不同包。
> 
> 考试提示
> 
> `vino` 包通过 Gnome 桌面管理器提供相同的功能。

在安装了包后，你需要在主文件中添加两行，告诉 VNC 服务器如何运行。

- 步骤 3。查看默认项：

```bash
# cat /etc/sysconfig/vncervers
# VNCSERVERS="2:myusername"
# VNCSERVERSARGS[2]="-geometry 800x600 -nolisten -nohtttp -localhostga"
```

## 第 13 章：远程访问

第一行定义允许登录系统的用户。

第二行列出了传递给 VNC 服务器的参数。

- `-geometry` 定义客户端连接时的查看器尺寸
- `-nolisten` 拒绝 VNC 服务器的 TCP 连接
- `-nohtttp` 拒绝 Web VNC 客户端
- `-localhost` 强制使用安全网关（端口转发）
