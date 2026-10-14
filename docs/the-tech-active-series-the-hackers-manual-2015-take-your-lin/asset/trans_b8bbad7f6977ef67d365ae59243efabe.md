

## 如此 AWStats。如此多图表。非常全面。哇。

```
$ ssh-copy-id user@host
```

将 user 和 host 替换为你之前设置的用户和 VPS 地址。这会将你的公钥追加到远程主机上的文件 ~/.ssh/authorized_keys 中。如果你确实需要复制你的私钥，请确保其权限（600）得到保留，否则你会因不安全的做法而受到谴责。

现在测试你刚烘焙好的密钥。如果你保留了默认文件名，则不需要任何特殊语法，否则你将不得不使用 -i（身份文件）选项：
$ ssh user -i ~/.ssh/private_key user@host

如果一切按计划进行，你应该会被提示输入私钥的密码短语并被允许登录。完成之后，我们可以在服务器上的 sshd_config 中更改以下行以禁用密码认证、旧的 v1 协议以及除 user 之外的任何人登录，并可选择将端口从默认的 22 更改：
Port 2022
Protocol 2
PasswordAuthentication no
AllowUsers user

现在我们重启 SSH 服务器。如果你使用的是可靠的 Sysvinit 脚本，这只需成为 root 并运行命令
$ /etc/init.d/sshd restart
或对于 Systemd：

```
$ systemctl restart sshd
```

现在唯一能登录的人是拥有我们密钥文件的人。服务器现在也在不同的端口上运行，这可能会阻止一些脚本小子，但也意味着你必须相应地指向你的 SSH 客户端：
$ ssh user@host:2022

你可以使用 ssh-agent 在本地会话期间保持此密钥解锁，这是一个方便的省力设备，尽管它会带来一点隐私成本。这可以通过以下方式实现：
$ ssh-add ~/.ssh/private_key

如果你正在运行某种正规的桌面环境，或以其他方式弄清楚如何在你的系统上塞入 Gnome Keyring 之类的东西，那么你甚至可以在登录时自动解锁并将你的密钥加载到内存中。同样，这很方便但可能不安全。

值得考虑通过 SSH 连接显式为你或你的授权用户运行的任何服务进行隧道传输。例如，如果你正在运行 VNC 服务器，那么与其将其暴露给外部世界，不如将其配置为仅在本地回环地址上监听。VNC 的默认端口是 5900，因此当我们从本地机器 ssh 时，我们像这样将此端口转发到 5901：
$ ssh -L 5901:localhost:5900 user@host:2022

> “考虑通过 SSH 对你显式运行的服务进行隧道传输。”

冒号后的部分相对于远程机器——我们将其端口 5900 转发到我们的 5901。只要在服务器的 hosts 文件中正确设置了 localhost 别名，你现在就可以告诉 VNC 客户端连接到你本地机器的 5901 端口（或在 VNC 用语中为 display :1）。一切顺利的话，你应该有一个可用的 VNC 会话，并且会有那种模糊温暖的感觉，因为你所有的点击和按键都通过加密通道发送。

## 完全锁定

过滤传出数据包真的只适用于偏执狂，但如果锡箔帽要求如此，这里是你在大规则或 REJECT 规则之前可能想要允许的流量的快速总结。

| Loopback traffic | Similar to incoming rules, use -o -j ACCEPT |
| DNS | TCP and UDP on port 53. |
| NTP | UDP port 123 |
| HTTP(S) | TCP on ports 80 & 443 |
| FTP | TCP on port 21 (Active FTP will initiate an incoming connection from the server’s port 20, but our established/related rule on the INPUT chain should take care of that) |
| git | TCP 9418 |
| ping | ICMP use --icmp-type 8 (echo) as in incoming rules |

如果你真的想满足终极控制狂系统管理员的刻板印象，那么可以记录 iptables 拒绝的所有数据包，但这会很快导致日志文件过大和磁盘满，这对你来说会比有人扫描你的机器寻找不存在的 SMB 共享更成问题。

## 玩火(墙)

设置基于 iptables 的防火墙是我们下一个挑战。iptables 程序根据规则过滤数据包，这些规则存在于名为 filter 的表中，并分为三个链：INPUT 用于传入数据包，OUTPUT 用于传出数据包，FORWARD 用于更高级的路由，我们不予关心。同样，其他表管理 nat。每个链都有一个默认策略，通常是接受所有数据包。除了接受它们之外，我们还有目标 REJECT 来明确拒绝连接，以及 DROP 来静默忽略

