
![](img/a6a91935f07f13d62210d3016f91c5fc_49_0.png)

```erlang
echo_server(Port) ->
    {Socket, Client} = gen_tcp:accept(gen_tcp:listen(Port, [])),
    gen_tcp:send(Socket, ["Hello, " ~p!\n", Client], [0]),
    echo_loop(Socket).
```

上图显示了实现 `Echo` 服务器（回显服务器）的代码。

当 `Echo` 服务器在屏幕上运行时，它会监听连接，并接收消息以及其他调试信息。

现在是查看 `Echo` 服务运行情况了。

我们将使用两个窗口以便你可以测试 `TCP` 服务器和客户端。在第一个窗口中，让我们开始使用端口 `8002`：

```erlang
33 >> echo_server(8002);
```

接下来，你将在第二个窗口中启动 `TCP` 客户端：

```erlang
9 >> echo_client("localhost", 8002, "HI!");
Socket: {port:8002};
Sent: {ok,131,0.7,32,105,33}
Recv: "HelloHI!"
nok
```

`Echo` 服务器将打印以下内容：

```erlang
Got - "HI"
ok
```

该过程的结果验证了消息已发回，并在其前面加上了 `"Hello "`。由于 `gen_tcp:listen` 函数具有 `active(false)` 参数，服务器进程在客户端连接后会终止；因此，如果你想让它持续运行，请重启。

## 在 `Erlang` 中创建 `UDP` 客户端

为了增加趣味性，我们将使用 `UDP` 开发 `Echo` 客户端。你可以在图 5 中看到 `UDP` 客户端的 `Echo` 代码，它与 `TCP` 版本非常相似。

`Echo` 服务器的实现有一个显著区别。过程如下：客户端发送数据并从服务器接收返回。之后，`UDP` 连接会自动关闭，因为 `UDP` 是无状态协议。与 `TCP` 不同，`UDP` 是无连接的。

简单来说，`UDP` 不关心数据包是否被接收或是否存在丢失；`TCP` 则对每个发送的数据包都有确认。此外，如果 `TCP` 没有收到

![](img/a6a91935f07f13d62210d3016f91c5fc_49_1.png)

`net` 网络工具（也作为 `nc` 执行）可以帮助你测试连接，并且在 `TCP/IP` 网络上开发应用程序时非常有用。该工具的好处是可以在没有 `root` 权限的情况下操作。它既作为客户端也可以作为服务器。使用带有 `-u` 选项的命令对于绑定端口非常有用，这意味着我们可以测试 `UDP`。默认情况下 `net` 使用 `TCP`，但使用 `-u` 选项后它充当 `UDP` 服务器。该选项告诉你仅使用 `IPv6` 地址。

```erlang
echo_client(Host, Port, Message) ->
    {Socket, Server} = gen_udp:connect(Host, Port, []);
    gen_udp:send(Socket, Message, 0);
    {ok, Reply} = gen_udp:recv(Socket, 1024);
    Reply.
```

上述 `UDP` 客户端与 `TCP` 客户端有某些相似之处，虽然看起来像 `TCP`，但速度比可靠性更重要。在这种情况下，当数据被拆分为单个数据包时，`UDP` 可能是更好的选择。`Echo` 服务就是这样一个例子。

![](img/a6a91935f07f13d62210d3016f91c5fc_49_2.png)

```erlang
echo_server(Port) ->
    {Socket, Address} = gen_udp:bind(Port, [], active(false));
    echo_loop(Socket).
```

```erlang
echo_loop(Socket) ->
    {ok, Message, Address} = gen_udp:recv(Socket, 1024);
    gen_udp:send(Socket, Message, 0);
    echo_loop(Socket).
```

上述是使用 `UDP` 协议的 `Echo` 服务器。在 `Erlang` 中创建 `UDP` 服务器

本节涵盖了使用 `UDP` 的 `Echo` 服务器的开发。代码用 `Erlang` 编写，你也可以在上面的图 6 中看到。我们的 `Echo` 服务器是一个被动式 `UDP` 服务器，使用逻辑/函数处理其连接。

首先，调用 `echo_server()` 并调用 `spawn()` 来在后台初始化服务器，这使得 `Erlang` shell 能够接收后续命令。因此，你可以如下所示启动 `UDP` 服务器：

```erlang
> net:echo_server(8000).
Socket:?Port=2071><66>.
```

接下来，我们启动在上一节中开发的 `Erlang` 客户端：

```erlang
> net:echo_client("localhost", 8000).
"Hello Hello!"
Cot:?Port<49>
:<This is Hello!>>
```

此时，`UDP` 服务器将打印以下行行：

```erlang
:"Hello Hello!"
```

因此，我们可以相信客户端和服务器的运行符合预期，且 `UDP` 服务的 `Erlang` 实现是正确的。

```erlang
{{127,0,0,1),(0,0,0),(255,0,0,0)}}
```

你也可以使用 `inet:getaddrs(Addr)` 获取相同的信息。图 7 显示了 `inet:getaddrs()` 函数更具分析性的输出——在 `Erlang` 中处理 `inet:getaddrs(Addr)` 的文本是一项困难的任务。你也可以用它来测试一个 `IP` 是否是有效的 `IP` 地址：

```erlang
> net:parse_address("192.168.1.200").
ok,((192,168,1,200)),
> net:parse_address("192.168.1.256").
error(invalid).
```

图 8 显示了一个名为 `dns.er` 的小型 `Erlang` 程序，它允许你使用 `inet:getaddr(Hostname)` 解析主机名。执行它将得到如下输出：

```erlang
-module(dns).

export([dns_resolve/1]).
dns_resolve(Hostname) ->
    Output = inet:getaddr(Hostname),
    format("~p~n", [Output]).
```

## 图 8

![](img/a6a91935f07f13d62210d3016f91c5fc_50_0.png)

图 7 显示了 `dns.er` 的 `Erlang` 代码，它包含单个函数：

- `1) dns_resolve("linux.user.co.uk")`
  `ok,(52,117,23,92))`

输出告诉我们 `linux.user.co.uk` 的 `IP` 是 `52.117.23.92`，可以通过 `host` 命令行进行验证：

```bash
$ host linux.user.co.uk
www.linux.co.uk has address 52.117.23.92
```

接下来的教程将开始讲解 `OTP`（开放电信平台），为了避免混淆，它不是指超时，而是指处理电信应用程序特征的软件。

正如你所见，`inet:getaddrs()` 函数提供了更详细的 `IP` 分析。与 `inet` 模块工作

在本节中，我们将展示如何使用 `inet` 模块。`TCP` 以下内容：

```erlang
> net:parse_address("192.168.1.200").
ok,((192,168,1,200)),
> net:parse_address("192.168.1.256").
error(invalid).
```

有原生的安全扫描功能。`Ubuntu` Server on `nmap`

| NMAP | Nmap 参考指南 |
|---|---|
| SWIFT | nmap 探索工具 /端口扫描器 |
| DESCRIPTION | "Nmap" 是用于网络发现和安全审计的开源工具。它支持许多操作系统。Nmap 使用原始 IP 包发送和接收信息，并确定主机开启了哪些服务（应用程序版本等）。Nmap 广泛用于安全审计、网络管理、配置审核计划以及主机或服务的运行监控。 |

## 资源

当我们在网络上设置 `Linux` 系统时，面临许多安全挑战，我们可能对保持系统安全感兴趣。在本教程中，我们将展示一个可行的解决方案。我们将涵盖安全 `Ubuntu` 服务器的各个方面。

- [nmap](https://nmap.org)
- [Ubuntu Server](https://ubuntu.com/server/Basic)

## 状态名称 | 概要描述

| 状态名称 | 概要描述 |
