
虽然这个警告看起来很微妙，但它告诉你有人删除了你 Linux 中的 `halt` 命令。从前几行可以推断出，我实际上将 `/sbin/halt` 重命名为 `/sbin/halt.bak`。

注意 对于 Red Hat Linux 9 的 Tripwire 包并不简单。有许多文件与 Red Hat Enterprise Linux 3 不同。但是，你至少可以设置基准日志，并根据此日志检测问题。

# 排除访问问题

安全可能过度。任何阻止用户使用所需服务的安全措施可能弊大于利。

如果你的用户需要某个服务，而你的安全措施阻止了该服务，你需要做出选择。你可以提供一个可以接受的替代方案，或者以某种方式放宽安全措施。有时，当问题实际上在于安全设置时，用户可能会告诉你某些功能无法工作。例如，`iptables` 的 `DROP` 可能会导致让用户感到困惑的输出。

# 过度安全

如果安全阻止了用户工作，那么它并没有帮助。但是，某些服务足够危险，你需要为用户提供替代方案。

例如，如果用户想通过 Telnet 连接到远程计算机，可能让他们学习第 18 节描述的安全 Shell（`SSH`）对你有利。你通常不希望用户在网络上以明文发送密码。

另一个例子是网络文件系统（`NFS`），细节详见第 22 节。`NFS` 需要访问多个 TCP/IP 服务：`nfs`、`portmap`、`rpc.mountd`，且 `nfs` 使用端口 `2049`；标准的 Red Enterprise Linux 防火墙还会拦截端口 `111`，这与 RPC 守护进程有关。

# 拒绝访问

当用户尝试访问被禁止的服务时，他们看到的取决于 `iptables`，特别是 `DROP` 或 `REJECT` 选项。例如，你可以实现以下规则之一，阻止 `192.168.0.0/24` 网络的用户通过安全 Shell（`SSH`）连接：

```
# iptables A INPUT -s 192.168.1.0/24 -p tcp --dport 22 -j DROP
# iptables A INPUT -s 192.168.1.0/24 -p tcp --dport 22 -j REJECT
```

端口 `22` 是 `SSH` 服务的 TCP/IP 端口。你可以在 `/etc/services` 中查找标准的 TCP/IP 端口。

现在对比 `192.168.1.0/24` 网络上的用户在尝试通过一个 `DROP` 请求的服务器连接时看到的：

```
# Enterprise3
Trying 192.168.1.13...
```

Trying 192.168.1.13...

telnet: Unable to connect to host: Connection refused
