
```
# rsh molari ps -A | grep tftp | grep -v grep
# rsh sheridan ps -A | grep tftp | grep -v grep
```

Try to get some tftp activity going using the cluster alias.

```
# tftp babylon5 -g /tftp/big1 /dev/null &
[1] 5118
```

```
# tftp babylon5 -g /tftp/big1 /dev/null &
[2] 5119
```

No luck because of the `in_noalias` service attribute.

```
# rsh molari ps -A | grep tftp | grep -v grep
# rsh sheridan ps -A | grep tftp | grep -v grep
```

Now try to get some tftp activity going using the actual cluster member names (not an alias).

```
# tftp molari -g /tftp/big1 /dev/null &
[1] 5139
```

The `tftpd` daemon started on molari because we used the actual member name. Our request, therefore, was not affected by the `in_noalias` attribute.

## 16.10.7.4 The in_nolocal Attribute

As you (hopefully) recall, a cluster alias provides an additional IP address through which access to cluster services may be gained. You may want to restrict access to a service such that the clients must use a cluster alias to get access to the service. Attaching the `in_nolocal` attribute to a service indicates that there should be no access to the service unless the alias is used. This means that use of any of the member’s local IP interface addresses (or node names) will not provide access to any service with the `in_nolocal` attribute.

The following example first shows successful client access to a service using a cluster alias, and then shows an unsuccessful attempt due to the `in_nolocal` attribute having been applied to the `tftp` service.

From the client system:

```
# rsh sheridan grep tftp /etc/clua_services
 tftp 69/udp in_multi;in_nolocal
```

Get some tftp activity going using the cluster alias. Works like a charm.

```
# tftp babylon5 -g /tftp/big1 /dev/null &
[1] 5182
```

```
# rsh molari ps -A | grep tftp | grep -v grep
1049867 ?? S 0:00.00 tftpd /tftp
```

Try to get some tftp activity going using a member name. No luck because of the `in_nolocal` attribute.

```
# tftp sheridan -g /tftp/big1 /dev/null &
[1] 5202
```

```
# rsh sheridan ps -A | grep tftp | grep -v grep
```

## 16.10.7.5 The out_alias Attribute

When communication takes place between nodes in a network, the nodes will identify themselves in the IP header with an IP address that is in use on the sending node. This would normally be the IP address associated with a local interface and not the IP address associated with a cluster alias. In the case where various authentication mechanisms may be in place, these mechanisms may function better if the sending node’s (actually a cluster member’s) IP address is the IP address associated with

```
# rsh molari ps -A | grep tftp | grep -v grep
1049745 ?? S 0:01.70 tftpd /tftp
```

使用集群别名而不是某种不可预测的、基于接口的 IP 地址，该地址在某些情况下可能在通信的不同阶段来自不同的集群成员。最好让标识发送节点的 IP 地址保持一致且可预测。它还隐藏了响应（或请求）来自集群的事实。这是通过将 `out_alias` 属性应用于服务来实现的。

此服务属性对于允许使用 `/etc/hosts.equiv` 或 `~/.rhosts` 文件在网络中多个节点上的帐户之间建立信任的 `rlogin`、`rsh` 和 `rcp` 服务特别有用。无需在这些文件中为每个集群成员放置一个条目，服务器（非集群成员）可以在文件中放置一个条目。该单个条目将包含集群别名。

以下示例使用 `login` 服务作为使用 `out_alias` 属性的服务的示例。删除该属性后，`rlogin` 活动需要密码。在删除 `out_alias` 属性之前，系统之间的信任是永久的，并且可以方便地无需密码登录。 不言而喻，你可能不希望在高度安全的计算环境中启用此信任。

```
 [sheridan]
# grep login /etc/clua_services
login                 513/tcp             in_multi,out_alias,static
```

从 `login` 行中删除 `out_alias` 并发出 `cluamgr -f` 命令以通知 CLUA 软件更改。

```
 [sheridan]
# grep login /etc/clua_services
login                 513/tcp             in_multi,static
```

```
# cluamgr -f
```

使用集群别名登录。注意没有请求密码。这通常表明客户端和服务器之间通过 `/etc/hosts.equiv` 文件或 `~/.rhosts` 文件启用了信任。有关这些文件的更多信息，请参阅 `hosts.equiv` 或 `rhosts` 的参考页。

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

请注意，当登录请求由 molari 处理时，会提示输入密码信息。正如你将在下面看到的，`/etc/hosts.equiv` 文件和/或 `~/.rhosts` 文件包含的是集群别名而不是单个集群成员名称。只要 `out_alias` 属性应用于 `/etc/clua_services` 文件中的 `login` 服务，这就可以正常工作。

从客户端系统：

```
# rlogin babylon5

Password:

Last login: Tue Sep  3 00:46:19 EDT 2002 from babylon5.dec.com

```
