

# 设置 inetd

你通过 `/etc/inetd.d` 目录下的 `/etc/inetd.conf` 文件控制通过 inetd 启动的服务器。`/etc/inetd.conf` 文件由一系列行组成，每行对应一个服务器。典型的行如下所示：

```
ftp stream tcp nowait /usr/sbin/tcp /usr/sbin/in.ftpd -l
```

此示例以及随后的几个示例涉及 `in.ftpd`，这一个曾经非常流行的 FTP 服务器，但在许多系统中已被其他 FTP 服务器所取代。其中一些服务器无法从超级服务器（super server）运行。

与其使用单体式的 `/etc/inetd.conf` 文件，inetd 的版本允许你将配置拆分为 `/etc/inetd.d` 目录下的多个文件。这样做允许你通过添加或删除配置文件来轻松添加或删除服务器。例如，接下来的段落仅提到 `/etc/inetd.conf`，但描述同样适用于 `/etc/inetd.d` 中的文件。

`/etc/inetd.conf` 中的每行由一个或多个空格分隔的几个字段组成。
这些字段的含义如下：

- **服务名称 (Service Name)**：第一个字段（上例中的 `ftp`）是服务在 `/etc/inetd.services` 文件中显示的名称。
- **Socket 类型 (Socket Type)**：socket 条目定义了预期的连接类型——可靠的双向连接（stream）、开销较小但可靠性较低的连接（dgram）、到网络的低层连接（raw）或其他。不同类型具有很强的技术性；你在编辑此条目时，主要关注的应该是正确输入服务器文档中指定的值。
- **协议 (Protocol)**：这是使用的 TCP/IP 传输层协议，通常为 `tcp` 或 `udp`。
- **等待/不等待 (Wait/No Wait)**：对于 `dgram` socket 类型，此条目指定服务器是连接到客户端并等待（nowait`）还是处理所有数据包并超时（wait`）。使用其他 socket 类型的服务器在 inetd 中应使用 `nowait`。
- **用户 (User)**：这是运行服务器的用户名。`root` 和 `nobody` 是常见选择，但也可以是其他用户。作为一般原则，出于安全考虑，你应该尽可能使用低特权用户运行服务器。详情请咨询服务器文档。
- **服务器名称 (Server Name)**：这是服务器的文件名。在上例中，服务器指定为 `/usr/sbin/tcpd`，它是 TCP Wrappers 的二进制文件。正如稍后在“通过 TCP Wrappers 控制访问”部分描述的，该程序是一个安全工具，应该包含在通过 inetd 启动的程序列表中。
- **参数 (Parameters)**：服务器名称之后的所有内容都是传递给服务器的参数。如果你使用 TCP Wrappers，你在此字段中传递真实目标服务器的（例如 `/usr/sbin/in.ftpd`）及其参数。

哈希符号 (`#`) 是 `/etc/inetd.conf` 的注释符号。因此，如果某个服务器在 inetd 中运行而你想禁用它，可以在行首放置一个哈希标记。如果你想向 `inetd.conf` 添加一个服务器，你需要为它创建一个条目。大多数可以从 inetd 运行的服务器在其文档中都包含了示例条目。许多发行版带的 `inetd.conf` 文件也包含了常见服务器的条目，尽管其中许多被注释掉了；删除行首的哈希标记即可激活该服务器。

修改 `inetd.conf` 后，你必须重启 inetd 服务器。你通常可以通过启动脚本来重启它，如第 5 章“启动 Linux 和编辑文件”所描述。在大多数计算机上，输入类似于以下的内容即可生效：

```
# /init.d/inetd restart
```

或者，你可以使用 `reload` 参数而不是 `restart` 来告诉 inetd 重新加载其配置。`restart` 选项会关闭服务器然后重新启动。当你使用 `reload` 时，服务器永远停止运行；它会重新读取配置。
