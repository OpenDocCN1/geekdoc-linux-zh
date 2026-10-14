

使用集群别名而不是某种不可预测的、基于接口的 IP 地址，该地址在某些情况下可能在通信的不同阶段来自不同的集群成员。最好让标识发送节点的 IP 地址保持一致且可预测。它还隐藏了响应（或请求）来自集群的事实。这是通过将 out_alias 属性应用于服务来实现的。

此服务属性对于允许使用 /etc/hosts.equiv 或 ~/.rhosts 文件在网络中多个节点上的帐户之间建立信任的 rlogin、rsh 和 rcp 服务特别有用。无需在这些文件中为每个集群成员放置一个条目，服务器（非集群成员）可以在文件中放置一个条目。该单个条目将包含集群别名。

以下示例使用 login 服务作为使用 out_alias 属性的服务的示例。删除该属性后，rlogin 活动需要密码。在删除 out_alias 属性之前，系统之间的信任是永久的，并且可以方便地无需密码登录。 不言而喻，你可能不希望在高度安全的计算环境中启用此信任。

```
 [sheridan]
# grep login /etc/clua_services
login                 513/tcp             in_multi,out_alias,static
```

从 login 行中删除 out_alias 并发出 “cluamgr -f” 命令以通知 CLUA 软件更改。

```
 [sheridan]
# grep login /etc/clua_services
login                 513/tcp             in_multi,static
```

```
# cluamgr -f
```

使用集群别名登录。注意没有请求密码。这通常表明客户端和服务器之间通过 /etc/hosts.equiv 文件或 ~/.rhosts 文件启用了信任。有关这些文件的更多信息，请参阅 hosts.equiv 或 rhosts 的参考页。

从客户端系统：

```
# rlogin babylon5
Last login: Tue Sep 3 00:41:34 EDT 2002 from babylon5.dec.com
"
```

```
# hostname
sheridan.dec.com
```

请注意，当登录请求由 molari 处理时，会提示输入密码信息。正如你将在下面看到的，/etc/hosts.equiv 文件和/或

`~/.rhosts` 文件包含的是集群别名而不是单个集群成员名称。只要 `out_alias` 属性应用于 `/etc/clua_services` 文件中的 login 服务，这就可以正常工作。

从客户端系统：

```
```text
# rlogin babylon5
Password:
Last login: Tue Sep  3 00:46:19 EDT 2002 from babylon5.dec.com
```
```

```
```text
# hostname
molari.dec.com
```
```

为了实现在从 `/etc/clua_services` 文件中删除 `out_alias` 属性之前启用的便捷信任，我们必须在 `~/.rhosts` 文件中为每个单独的集群成员输入一行。

```
```text
[ molari]
# cat /.rhosts
babylon5.dec.com
sheridan-ics0
molari-ics0
climach4
climach3
```
```

```
```text
[ molari]
# cat >> /.rhosts
molari
sheridan
```
```

```
```text
[ molari]
# cat /.rhosts
babylon5.dec.com
sheridan-ics0
molari-ics0
climach4
climach3
molari
sheridan
```
```

现在登录无需密码即可工作。

从客户端系统：

```
```text
# rlogin babylon5
Last login: Tue Sep  3 00:48:42 EDT 2002 from sheridan.dec.com
```
```

你可以将 out_alias 属性理解为传出流量将使用别名 IP 地址来标识网络上的发送节点。

## 16.10.7.6 The static Attribute

最终标志 static 使与端口号高于 512 的服务相关联的服务与其分配的端口号静态关联。端口号将不会被分配为动态端口。例如，一旦端口 540 与 uucp 关联（由 inetd 启动），该端口将只与 uucp 服务关联。

如前所述，如果你对 /etc/clua_services 文件进行更改，你将必须通过 "cluamgr -f" 命令强制重新读取该文件（在每个成员上）。如果更改涉及由 inetd 启动的服务，还必须使用 "kill -HUP" 命令重新启动 inetd（在每个成员上）。

## 16.11 CAA vs. CLUA

到目前为止，本章解释了当服务由 inetd 守护进程按需启动时会发生什么。还有其他网络服务在启动时启动，例如 NFS、DNS/BIND 和 NIS。这些服务通常通过 CAA 子系统控制（有关 CAA 示例，请参阅第 24 章）。CAA 设计用于管理一次在单个集群成员上运行的应用程序。将其与 CLUA 子系统形成对比，后者负责路由到集群别名的客户端连接请求。有时 CAA 和 CLUA 的概念似乎模糊不清，但如果你记住 CLUA 涉及集群别名路由决策，而 CAA 涉及启动、管理和故障转移应用程序，那么区别应该变得清晰。

CAA 在具有 in_single CLUA 属性的应用程序上最有用。CAA 将负责启动其控制下的应用程序，在必要时进行应用程序故障转移，并监控 CAA 控制的应用程序运行所需的任何资源的可用性。有关 CAA 的更多信息，请参阅第 23 章和第 24 章。

## 16.12 NFS and Aliases

NFS 是在启动时启动的网络服务的示例。因此，它不受 inetd 守护进程的控制。在集群中典型使用 NFS 作为高可用性 NFS 服务器。请记住，NFS 是一种软件机制，允许文件系统（或目录）通过远程挂载对网络中的客户端节点可访问。我们是否应该担心哪个集群成员实际充当 NFS 服务器？

在正常情况下，其中要服务的存储位于所有集群成员共享的总线上，哪个成员提供数据几乎没有区别。但想象一下，选择的集群成员执行 NFS 服务却没有直接访问要服务的存储所涉及的开销。这将需要在 CI 上产生额外的流量，以便访问要通过 NFS 提供的数据的 CFS 服务器。哎呀！这简直是系统资源的浪费。

