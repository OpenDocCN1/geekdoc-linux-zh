
最后，文件的最后一行指定必须检查 `/etc/xinetd.d` 目录以查找包含更多配置信息的其他文件。这将导致 `xinetd` 读取该目录中的所有文件，并对其进行解析，就像它们是 `/etc/xinetd.conf` 文件的一部分一样。

## 属性及其含义

表 9-1 列出了 `/etc/xinetd.conf` 文件中支持的一些属性/变量名称。

## 第二部分 单机主机管理

| 变量 | 说明 |
|---|---|
| id | 此属性用于唯一标识一个服务。这非常有用，因为存在某些服务可以使用不同的协议，需要在配置文件中使用不同的条目进行描述。默认情况下，服务 ID 与服务名称相同。 |
| type | 可以使用以下值的任何组合：如果服务是远程过程调用 (RPC) 服务，则使用 `RPC`；如果此服务由 `xinetd` 提供，则使用 `INTERNAL`；如果此服务未列在 `/etc/services` 文件中，则使用 `UNLIST`。 |
| disable | 值为 `yes` 或 `no`。`yes` 表示该服务已定义但不可用。 |
| socket_type | 有效值为：`stream`，表示该服务是基于流的服务；`dgram`，表示该服务是基于数据报的；`raw`，表示该服务使用原始 IP 地址。`stream` 值指的是面向连接的 TCP 数据流（例如，Telnet 和 FTP）。`dgram` 值指的是数据报流（用户数据报协议 (UDP) 流）（例如，简易文件传输协议 (TFTP) 服务是基于数据报的协议）。TCP/IP 范围之外的其他协议不存在，但你很少遇到它们。 |
| protocol | 决定连接的协议类型（TCP 或 UDP）。 |
| wait | 如果设置为 `yes`，则意味着服务是单线程的，每次只会处理一个连接。如果设置为 `no`，则意味着服务是多线程的，通过多次运行适当的服务守护进程允许多个连接。 |
| user | 设置服务所属的用户。 |
| group | 设置服务所属的组。 |
| instances | 允许的最大实例数量。 |
| server | 指定服务的程序路径。 |
| server_args | 传递服务的参数。 |
| only_from | 指定允许访问服务的 IP 地址范围。 |

表 9-1 `/etc/xinetd.conf` 属性（继续）

| 变量 | 说明 |
|---|---|
| access | 指定允许访问服务的 IP 地址范围。可以使用：`allow`、`deny`、`global`、`local`、`wrap`、`match`。`all` 表示所有，`host` 表示主机，`from` 表示远程主机，`pass` 表示需要密码。`net` 表示网络，`mask` 表示子网掩码。`local` 表示本地，`global` 表示全局。`wrap` 表示使用 `/etc/tcpwrappers` 配置，`match` 表示匹配规则。 |
| port | 服务监听的端口号。 |
| protocol | 协议类型（TCP 或 UDP）。 |
| socket_type | 套接字类型（`stream`, `dgram` 或 `raw`）。 |
| wait | 是否为单线程。 |
| user | 运行的用户。 |
| group | 运行的组。 |
| instances | 最大实例数。 |
| server | 可执行程序。 |
| server_args | 程序参数。 |
| only_from | 允许的 IP 范围。 |

# 第 9 章 核心系统服务 185

## 示例：简单的 (echo) 服务

以由 `xinetd` 提供的 echo 服务为例，我们来看看最简单的 `xinetd` 条目之一。

```
# This is the configuration for the tcp/stream echo service
{
    disable = yes
    id = echo-stream
    type = INTERNAL
    wait = no
    socket_type = stream
}
```

如你所见，该条目是自而易见的。第一行的井号（`#`）表示它是注释，因此被忽略。服务名称是 `echo`，由于 `socket_type`（即 `stream`），我们知道这是一个 TCP 服务。`wait` 变量告诉我们可以运行多个 echo 进程。最后，类型为 `INTERNAL` 的属性表示由 `xinetd` 提供，换句话说，它不是由外部包提供的。

## 启用/禁用 echo 服务

如果你希望系统是安全的，可能只会运行少数服务——有些人甚至根本不运行 `xinetd`！启用或禁用服务只需要几步。例如，要启用一个服务，你需要在 `xinetd` 配置文件中启用它，重启 `xinetd` 服务，最后进行测试以确保行为符合预期。要禁用服务，只需相反操作即可。

注意 我们正在研究的是 echo 服务。该服务是 `xinetd` 内部的（也就是说它不是由外部守护进程提供的）。

让我们逐步启用 echo 服务：通过编辑 `/etc/xinetd.d/echo-stream` 文件并将 `disable` 变量更改为 `no`，如下文所示：

提示：在基于 Ubuntu 的系统上，echo 服务的配置文件是 `/etc/xinetd.d/echo`。

Ubuntu 更进了一步，将 UDP 和 TCP 版本的 echo 服务合并在一个文件中。

相比之下，Fedora 将 echo 服务的 UDP 和 TCP 连接分成了两个独立的文件：

`/etc/xinetd.d/echo-dgram` 和 `/etc/xinetd.d/echo-stream`。

保存你所做的的更改并退出编辑器。

- 3. 重启 `xinetd` 服务。在大多数 Linux 发行版中，你可以输入以下命令：

```
[master@server -]$ sudo service xinetd restart
```

在启用了 `systemd` 的现代发行版中，你也可以选择使用 `systemctl` 单元来重启 `xinetd` 服务，如下所示：

```
[master@fedora-server -]$ sudo systemctl restart xinetd.service
```

- 4. Telnet 连接到 echo 服务的端口（端口 7），查看索引是否正在运行：

```
[master@fedora-server -]$ telnet localhost 7
Connected to localhost.
Escape character is '^'.
Hello World
Hello World
```

如果 echo 服务已启用，你的输出应该与上述类似。

你可以在 Telnet 提示符处输入键盘上的任何字符，并观察该字符如何回显（重复）给你。在示例中你输入了 "Hello World"。如你所见，echo 服务是那些极其有用且救命的服务之一，用户和系统管理员无法离开它！)

同时，在键盘上按下 CTRL-] 断开连接，然后输入 `quit` 退出 Telnet 并返回 shell 提示符。

这次练习通过直接编辑 `xinetd` 配置文件来启用服务来实现。启用或禁用服务是一个简单的过程。然而，你应该轻松地回滚并通过测试来确保该服务确实是需要的（如果这正是你想要的）——因为防患于未总比事后后悔要好。一个事后“后悔”的例子是：你认为自己已经禁用了不安全的 Telnet 服务，但实际上它仍在运行！

> 提示：你可以通过 `chconfig` 工具使用 `xinetd` 快速启用或禁用服务，该工具在较旧的 GNU/Linux 发行版中随处可用（或可以安装）。例如，要禁用手动启用的 `echo-stream` 服务，只需执行以下命令：

```
# chkconfig echo-stream off
```

# 日志守护进程

当一次同时处理很多任务时，特别是对于与终端窗口断开连接的服务，需要一种标准的机制来记录特殊事件和消息。Linux 发行版传统上一直使用 `syslog` (`syslog`) 守护进程来提供此服务。然而，现代 Linux 发行版已将 `rsyslog` 包以及 `systemd` 的日志组件（称为 `systemd-journald` (`journald`)）标准化为处理日志相关函数的标准工具。

无论使用何种软件，其核心思想都是相同的，最终结果（收集系统日志）也大部分相同；新方法之间的主要区别在于其提供的额外功能set。在本节中，我们将重点关注 `rsyslog`。在适当的情况下，会偶尔引用 `syslog`。管理和配置 `rsyslog` 的方法与在 `syslog` 中进行的方式相似。`rsyslog` 守护进程与传统的 `syslog` 守护进程保持向后兼容，同时也提供了许多新功能。

## rsyslog

`rsyslog` 守护进程提供了一种执行记录的标准方法。许多其他平台的系统都采用兼容的守护进程，从而提供了通过网络进行跨平台记录的方法。这在大型异构环境中特别有价值，因为在其中需要集中收集日志条目以准确获取发生的情况。你可以将此日志设施系统等同于 Windows 中的事件查看器（Event Viewer）功能。
