

![](img/ec25e59d75726b7041242a56d3376832_593_0.png)

这是该模块中较为基础的场景之一。请务必抽出时间完成练习并理解这些概念，然后再继续前进。

## 20.1.1.1 练习

- 连接到你的专用 Linux 实验室客户端，并以 root 身份从 `/root/port_forwarding_and_tunneling/` 目录运行 `clear_rules.sh` 脚本。
- 尝试复现上述场景中所涵盖的端口转发技术。

## 20.2 SSH 隧道

SSH 协议<sup>591</sup> 是用于隧道和端口转发最受欢迎的协议之一。<sup>592</sup> 这是因为它具有在 SSH 协议内创建加密隧道的能力，而该协议支持双向通信通道。SSH 协议的这一晦涩功能对渗透测试人员和管理员都有深远的影响。

### 20.2.1 SSH 本地端口转发

SSH 本地端口转发允许我们将本地端口通过 SSH 作为传输协议隧道到远程服务器。这种技术的效果类似于 rinetd 端口转发，但也有一些不同之处。

<sup>591</sup> (SSH Communications Security, 2018), https://www.ssh.com/ssh/protocol/

<sup>592</sup> (Trackets Blog, 2017), https://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html

![](img/ec25e59d75726b7041242a56d3376832_594_0.png)

让我们考虑另一个场景。在一次评估中，我们通过远程漏洞攻陷了一个基于 Linux 的目标，将权限提升至 root，并获取了该机器上 root 和 student 用户的密码。这个被攻陷的机器似乎没有出站流量过滤，并且只暴露了 SSH（端口 22）、RDP（端口 3389）和存在漏洞的服务端口，这些端口在防火墙中也是被允许的。

在对被攻陷的 Linux 客户端进行枚举后，我们发现除了连接到当前网络（10.11.0.x）外，它还有一个似乎连接到不同网络（192.168.1.x）的网络接口。在这个内部子网中，我们识别出一台 Windows Server 2016 机器，该机器有可用的网络共享。

为了在我们的实验室环境中模拟这种配置，我们将运行专用 Linux 客户端上的 `ssh_local_port_forwarding.sh` 脚本：

```bash
root@debian:~# cat /root/port_forwarding_and_tunneling/ssh_local_port_forwarding.sh
#!/bin/bash

# Clear iptables rules
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
iptables -X

# SSH Scenario
iptables -F
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 3389 -m state --state NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 8080 -m state --state NEW -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
root@debian:~# /root/port_forwarding_and_tunneling/ssh_local_port_forwarding.sh
```

> 列表 632 - ssh_local_port_forwarding.sh 脚本的内容

在这种情况下，我们可以将所需的攻击和枚举工具移动到被攻陷的 Linux 机器上，然后尝试与 2016 服务器上的共享进行交互，但这既不够优雅也不具备可扩展性。相反，我们希望从基于互联网的连接通过我们的 Kali 攻击机器，透过这个被攻陷的 Linux 客户端进行跳转（pivoting），与这个新目标进行交互。这样，当我们与目标交互时，就可以访问我们 Kali 攻击机器上的所有工具。

这需要一些端口转发的魔法，我们将使用 ssh 客户端的本地端口转发功能（通过 `ssh -L` 调用）来协助实现。

语法如下：

```bash
ssh -N -L [bind_address:]port:host:hostport [username@address]
```

> 列表 633 - 使用 SSH 进行本地端口转发的命令原型

查阅 ssh 客户端的手册（`man ssh`），我们注意到 -L 参数指定了将转发到远程地址和端口的本地主机端口。

在我们的场景中，我们希望将我们 Kali 机器上的端口 **445**（无 NetBIOS 的微软网络）转发到 Windows Server 2016 目标上的端口 **445**。当我们这样做时，指向我们 Kali 机器的任何微软文件共享查询都将被转发到我们 Windows Server 2016 目标。鉴于防火墙正在阻止 TCP 端口 **445** 上的流量，这似乎是不可能的，但这个端口转发是通过 SSH 会话隧道到我们 Linux 目标端口 **22** 的，该端口是防火墙允许的。简而言之，请求将到达我们 Kali 机器的端口 **445**，通过 SSH 会话转发，然后传递到我们 Windows Server 2016 目标上的端口 **445**。

如果操作正确，我们的隧道和转发设置将类似于图 298：

![](img/ec25e59d75726b7041242a56d3376832_595_0.png)

为了实现这一点，我们将从我们的 Kali Linux 攻击机器执行一个 ssh 命令。我们在技术上不会发出任何 ssh 命令（`-N`），但会设置端口转发（使用 `-L`），将本地机器上的端口 **445**（**9.0.0.0:445**）绑定到 Windows Server（**192.168.1.110:445**）上的端口 **445**，并通过我们原始 Linux 目标的会话来实现，登录用户为 student（**student@10.11.0.128**）：

```bash
kali@kali:~$ sudo ssh -N -L 9.0.0.0:445:192.168.1.110:445 student@10.11.0.128
student@10.11.0.128's password:
```

> 列表 634 - 将我们的 Kali Linux 机器上的 TCP 端口 445 转发到 Windows Server 2016 上的 TCP 端口 445

此时，任何传入到我们 Kali Linux 机器 TCP 端口 **445** 的连接都将被转发到通过我们被攻陷的 Linux 客户端连接到 192.168.1.110 IP 地址的 TCP 端口 **445**。

在测试之前，我们需要对我们的 Samba 配置文件做一个小改动，通过将该文件末尾添加 `"min protocol = SMB2"` 来将最低 SMB 版本设置为 SMBv2，如列表 635 所示。这是因为 Windows Server 2016 默认不再支持 SMBv1。

```bash
kali@kali:~$ sudo nano /etc/samba/smb.conf

kali@kali:~$ cat /etc/samba/smb.conf
...
Please note that you also need to set appropriate Unix permissions
# to the drivers directory for these users to have write rights in it
;
write list = root, @lpadmin

min protocol = SMB2

kali@kali:~$ sudo /etc/init.d/smbd restart
[ ok ] Restarting smbd (via systemctl): smbd.service.
```

*列表 635 - 将 Samba 更新为使用 SMBv2 通信*

最后，我们可以尝试列出 Windows Server 2016 机器上的远程共享，将请求指向我们的 Kali 机器。

我们将使用 smbclient 工具，提供 IP 地址或 NetBIOS 名称，在这种情况下是我们的本地机器（`-L 127.0.0.1`）和远程用户名（`-U Administrator`）。如果一切按计划进行，在我们输入远程密码后，该端口上的所有流量都将被重定向到 Windows 机器，并将显示可用的共享：

```bash
kali@kali:~# smbclient -L 127.0.0.1 -U Administrator
Unable to initialize messaging context
Enter WORKGROUP\Administrator's password:

Sharename    Type       Comment
---------    ----       -------
ADMIN$       Disk       Remote Admin
C$          Disk       Default share
Data         Disk
IPC$         IPC        Remote IPC
NETLOGON     Disk       Logon server share
SYSVOL       Disk       Logon server share
Reconnecting with SMB1 for workgroup listing.

Server     Comment
---------    -------

Workgroup    Master
---------    -------
```

*列表 636 - 通过本地端口转发列出 Windows Server 2016 机器上的网络共享*

不仅该命令成功了，而且由于这些流量通过 SSH 进行了隧道传输，整个事务都是加密的。我们可以使用这个端口转发设置继续通过 445 端口分析目标服务器，或者转发其他端口以进行额外的侦察。

### 20.2.1.1 练习

- 连接到你的专用 Linux 实验室客户端，并以 root 身份从 `/root/port_forwarding_and_tunneling/` 目录运行 `clear_rules.sh` 脚本。
- 以 root 身份从 `/root/port_forwarding_and_tunneling/` 目录运行 `ssh_local_port_forwarding.sh` 脚本。

