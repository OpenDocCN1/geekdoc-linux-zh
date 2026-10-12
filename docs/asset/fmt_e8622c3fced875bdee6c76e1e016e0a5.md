
`server = /usr/sbin/tcpd`

这将导致`xinetd`启动`tcpd`守护进程，而不是服务守护进程本身。

5. 添加以下行：

`server_args = path_to_daemon`

这告诉`tcpd`守护进程随后运行所请求的网络守护进程。在此处显示的示例中，`/etc/xinetd.d/telnet`文件已被配置为在`TCP wrapper`中运行`vsftpd`守护进程：

```
service ftp
{
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/vsftpd
    server          = /usr/sbin/tcpd
    server_args
```

`log_on_success += DURATION USERID`

`log_on_failure += USERID`

`nice = 10`

`disable = no`

6. 保存文件并重启`xinetd`守护进程。

接下来，你需要创建访问控制。`tcpd`守护进程使用`/etc/hosts.allow`和`/etc/hosts.deny`文件来指定谁可以访问其所管理的服务。`/etc/hosts.allow`中的条目表示允许访问；而`/etc/hosts.deny`中的主机则不允许访问。这两个文件的语法如下：

`service: host_addresses`

控制访问的最佳策略是首先在`/etc/hosts.deny`文件中明确拒绝所有主机对该服务的访问。例如，若要拒绝所有主机访问`vsftpd`服务，你应创建如下条目：

`vsftpd: ALL`

接着，你需要配置`/etc/hosts.allow`文件以允许特定主机访问。以下示例中的条目授予 IP 地址为`192.168.1.10`和`192.168.1.102`的主机访问`vsftpd`服务的权限。

`vsftpd: 192.168.1.10, 192.168.1.102`

请注意，`hosts.deny`先于`hosts.allow`被读取和应用。这意味着`hosts.allow`中的任何指令都会优先于`hosts.deny`中任何冲突的指令。如果未经授权的主机尝试连接，该请求将会失败。

某些发行版使用`inetd`守护进程而非`xinetd`。这个守护进程的工作方式与`xinetd`非常相似。接下来，我们将学习它是如何工作的。

#### 配置 `inetd`

`inetd`守护进程是一个类似`xinetd`的超级守护进程，但它通常用于较旧的 Linux 发行版。与`xinetd`一样，`inetd`守护进程充当运行在 Linux 主机上的网络服务连接请求的中介。它接受来自客户端系统的连接请求，启动所需的服务，然后将来自客户端的请求转发给新启动的守护进程。当交易完成且来自客户端的连接终止时，该守护进程在 Linux 主机上停止运行。

正如我们在`xinetd`部分讨论的那样，以这种方式管理 Linux 主机上的网络服务既有优势也有劣势。其中关键的一点是它节省了系统内存和 CPU 资源。网络守护进程仅在需要时才启动。当不需要时，它会从内存中移除，直到再次被请求。然而，这种好处是以延迟为代价的。当客户端请求某项服务时，客户端必须等待一小段时间，以便加载必要的守护进程并建立连接。因此，`inetd`（以及`xinetd`）仅应用于管理系统中偶尔才需要的网络服务。

`inetd`守护进程通过`/etc/inetd.conf`文件进行配置。与`xinetd`守护进程不同，`inetd`管理的所有服务都在这个单一的配置文件中配置。该文件中的每一行配置由`inetd`管理的单一服务。`inetd.conf`中使用的语法如下所示：

`service_name socket_type protocol flags user executable arguments`

该行中每个参数的描述见下表 17-6。

以下是`inetd.conf`中针对`vsftpd`守护进程的一个示例条目：

`ftp stream tcp nowait ftp /usr/sbin/tcpd vsftpd`

请注意，在这个示例中，你可以像在`xinetd`中使用`TCP wrappers`一样在`inetd`中使用它们。在这个例子中，当客户端尝试与此 Linux 主机建立 FTP 连接时，`inetd`守护进程将启动`tcpd`守护进程，并将实际要启动的守护进程的名称（`vsftpd`）作为服务器参数传递给它。与`xinetd`一样，在`inetd`中使用`TCP wrappers`允许你使用`/etc/hosts.allow`和`/etc/hosts.deny`文件来控制对主机上运行的网络服务的访问。

| 配置参数 | 描述 |
| :--- | :--- |
| `service_name` | 指定要管理的服务名称，如`/etc/services`文件中所包含的那样。`/etc/services`文件将端口号和协议映射到特定的服务名称。`inetd.conf`中的`service_name`参数随后将这些服务名称之一映射到特定的守护进程。默认情况下，`inetd`在所有活动的网络接口上监听指定服务的请求。如果你想将对该服务的访问限制在单个接口上，请将该接口的 IP 地址添加到服务名称中（用冒号分隔）。例如，若要限制对 IP 地址为`192.168.1.10`的网络接口的`vsftpd`请求，应使用服务名称`192.168.1.10:vsftpd`。 |
| `socket_type` | 指定网络套接字的类型。对于大多数网络服务，此参数通常设置为值`stream`。 |
| `protocol` | 指定正在启动的守护进程所使用的协议，如在`/etc/protocols`中规定的。对于大多数服务，此参数通常设置为值`tcp`或`udp`。 |
| `flags` | 指定指定协议的相应标志。如果你指定了`tcp`协议，此参数可以使用值`nowait`。如果你指定了`udp`协议，此参数可以使用值`wait`。 |
| `user` | 指定服务将作为哪个用户和组运行。使用`user:group`的语法。 |
| `executable` | 指定`inetd`在收到对指定服务的连接请求时要运行的可执行文件名（包括完整路径）。 |
| `arguments` | 指定当`inetd`启动服务时传递给该服务的参数。 |

表 17-6 `inetd`配置文件参数

让我们在下面的练习中实践配置超级守护进程。

#### 练习 17-3: 配置 `xinetd`

在这个练习中，你将通过启用由这个超级守护进程管理的多个服务中的一个来练习使用`xinetd`。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_737_0.png)

> **注意** 此练习需要使用第二台 Linux 系统来测试你的配置。两台系统都需要连接到同一个网络段，并且配置正确以参与该网络段。此外，如果你的 Linux 发行版使用的是`inetd`而不是`xinetd`，你需要根据本章内容调整步骤。

你将通过`xinetd`在 Linux 主机上启用`time`服务。完成后，你的 Linux 主机可以作为一个时间提供者服务于时间客户端。请完成以下操作：

1. 启动你的 Linux 系统并以标准用户身份登录。
2. 打开一个终端会话。
3. 通过输入`su`并跟随你的`root`用户密码切换到你的`root`用户账户。
4. 在 shell 提示符下，使用`cd`命令切换到`/etc/xinetd.d`目录。
5. 在 shell 提示符下，输入`vi /time-udp`以打开`time`服务的`xinetd`配置文件。你应该看到类似于以下的配置设置：

```
service time
{
    type                = INTERNAL UNLISTED
    id                  = time-dgram
    socket_type         = dgram
    protocol            = udp
    user                = root
    wait                = yes
    disable             = no
    port                = 37
    FLAGS               = IPv6 IPv4
}
```

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_737_1.png)
