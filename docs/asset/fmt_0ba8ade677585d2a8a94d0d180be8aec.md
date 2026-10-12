
`stop` 函数的操作类似于 `start` 函数的相反。首先，它输出一条消息指示 atd 正在停止。然后它调用函数 `pidfileofproc` 来查看 atd 是否有 PID 从而正在运行。如果是，则调用 `killproc` 函数杀死 atd，并将变量 `RETVAL` 设置为 3；否则，调用 `failure` 函数指示在尝试停止 atd 时失败。命名变量（与 `RETVAL` 不同）被设置为最近一次函数调用的值，该值将是 `killproc` 或 `failure` 的值。`killproc` 成功后返回 0，如果 `retval` 为 0，则意味着 atd 已成功停止。随后删除 `lockfile` 文件以指示进程不再运行。

```bash
restart() {
    stop
    start
}
```

```bash
reload() {
    restart
}
```

```bash
force_reload() {
    restart
}
```

`restart` 简单地分别调用 `stop` 和 `start` 两个函数。如果你修改了 atd 的配置文件，或者发现 atd 运行正常并希望重启，就会使用 `restart`。它也可以单独停止和启动。上面还展示了 `reload` 和 `force_reload`，两者都调用 `restart` 以提供相同的结果。这允许系统管理员使用 `restart`、`reload` 或 `force_reload` 中的任何一个来重启 atd。

```bash
rh_status() {
    status $prog
}
```

`rh_status` 函数似乎并没有实际作用；它仅仅调用了 `status` 并传递程序名称 `atd`。事实上，`rh_status` 是一种包装函数。我们使用 `rh_status` 是因为我们可能想直接或间接地通过另一个函数 `rh_status_q`（如下所示）调用它。由于在调用 `status` 时没有提供 `-l` 或 `-p` 选项，它将测试是否存在 PID，如果存在则输出“running”消息；否则，它将响应“dead”、“权限不足”或“stopped”消息。

```bash
rh_status_q() {
  rh_status >/dev/null 2>&1
}
```

此函数用于调用上述 `rh_status` 函数。符号 `>/dev/null 2>&1` 在系统管理脚本中很常见，表示将 `STDERR` 重定向到与 `STDOUT` 相同的输出位置。在从 `2>&1` 中，`2` 代表 `STDERR`，`>` 将 `STDERR` 的任何输出重定向到 `&1`，而 `&1` 表示“指向 `STDOUT` 的目的地”。在此之前，代码 `>/dev/null` 将 `rh_status` 的 `STDOUT` 和错误不输出到用户的终端窗口，而是发送到 `/dev/null`。

当我们调用 `status` 来查找服务状态时，为什么要防止输出在终端窗口中被看到呢？这是因为调用 `rh_status_q` 获取服务状态是为了不输出而是返回状态码。我们希望接收到一个 0，表示服务按预期运行。我们将看到，当想要获取服务状态时使用的是 `rh_status` 而不是 `rh_status_q`，而 `rh_status_q` 则用于启动或停止。

```bash
case "$1" in
  start)
    start
    ;;
  stop)
    stop
    ;;
  restart)
    restart
    ;;
  reload)
    reload
    ;;
  force_reload)
    force_reload
    ;;
  status)
    status
    ;;
  *)
    echo "Usage: $0 {start|stop|restart|reload|force_reload|status}"
    exit 1
    ;;
esac
```

## 系统初始化与服务 ■ 473

允许其他类型的消息通过。例如，如果你准备在这台 Linux 机器上实现一个 Web 服务器，你必须允许 HTTP 和可能还有 HTTPS 消息（图中未显示）。或者，如果你想建立 DNS 服务器，就会启用 DNS。

对于列表中的每个服务，我们还选择了与其相关的端口和协议。这些细节有助于完善防火墙规则。例如，SSH 使用端口 22 的 TCP 协议。如果你选择了 DNS 并应用更改，防火墙将生成一条规则，允许通过端口 53 的 TCP 和 UDP 消息。Conrack Helper 是 Connection Tracker Helper（连接跟踪器助手）的缩写。这些程序帮助跟踪各种类型的连接。例如，`amanda` 是用于跟踪 Amanda Backup 客户端的程序。

“其他端口”（Other Ports）选项允许你添加在“信任服务”（Trusted Services）下列出的端口。例如，`telnet` 可通过端口 23 使用。你必须选择“其他端口”而不是“信任服务”。此外，你还可以打开非典型端口，例如为 HTTP 添加端口 8080。HTTP 请求默认使用端口 80。除了端口或端口范围外，你还需要指定给定端口的可接受协议。

“信任接口”（Trusted Interfaces）包括 `eth+` 设备（例如 `eth0`、`eth1`、`eth2` 等）、`ipp+` 设备、`isdn+`、`dpp+` 设备、`tun+` 和 `wan+` 设备。网络接口（Network interface）单独列出。默认是不选择这些中的。如果你有未列出的接口设备，也可以将你的接口添加到列表中。

对本地网络进行伪装（Masquerading），使主机显示为单一的 Internet 地址。如果开启伪装，则会启用端口转发。

端口转发（Port Forwarding）允许你指定转发规则。如果你的设备不是网络的终端用户，而是路由消息的设备（例如路由器、网关），你就会使用转发。转发允许消息从你的设备转发到另一个设备。端口转发是指定哪些消息应该传递以及允许的目标地址和端口的规则。例如，你可能指定从 `eth+` 端口 80 接收到的 TCP 消息可以转发到 IP 地址 `10.11.1.2`。如果收到的消息的目标地址中存在任何本地机器的 IP 地址，则不进行转发。

ICMP 过滤器（ICMP Filter）允许由故障排除程序作为 `ping` 发送的消息。选择包括目标不可达（destination unreachable）、参数问题（parameter problem）、重定向（redirect）和超时（time exceeded）。最后，自定义规则允许你输入自己的防火墙规则。这些规则使用 `iptables` 格式指定，我们将在第 12 章中解释。

## 11.6.2 kdump 配置工具

内核转储配置工具（Kernel Dump Configuration Tool）可以替代 `kdump` 配置文件 `kdump.conf`。当内核崩溃时会调用 `kdump` 服务，以便可以将内核崩溃原因的记录保存为核心转储（core dump）。通过防火墙，此 GUI 提供了更改 `kdump` 行为的方便方法。图 11.5 展示了内核转储配置工具的主窗口。从主面板开始，你的选项是启用/

# 474 操作系统概念与 Linux

![](img/c3d46558b4f2c37c3a715bd825868fef_501_0.png)

图 11.5 内核转储配置 GUI 工具。

禁用 `kdump` 服务并确定内核转储的大小。还有三个其他设置供选择：目标设置（Target settings）、过滤设置（Filtering settings）和专家设置（Expert settings）。

通过其他选项卡，你可以指定其他的 `kdump` 信息。在目标设置中，你指定内核转储的路径和文件名，它可以是本地文件系统的某处（如 `/var/crash`）、原始设备，或通过 NFS 或 SSH 访问的网络位置。过滤选项卡允许你通过指定过滤级别来确定转储多少数据。专家设置允许你更改内核（默认内核或自定义内核）以及启动内核的命令行规范。图 11.6 结合了这三个窗口。

![](img/c3d46558b4f2c37c3a715bd825868fef_501_1.png)

图 11.6 其他 Kdump GUI 设置。

## 11.7 通过配置文件配置服务

我们现在转到使用配置文件来配置服务。这种方法要求你编辑相应的服务配置文件。在许多情况下，给定的服务只有一个配置文件。但在某些情况下，可能有多个文件，例如配置文件和一个规则文件。这些文件大多数位于 `/etc` 下，尽管在许多情况下，它们位于 `/etc/sysconfig` 等子目录中，或者位于特定于服务的目录下。

这些文件中的条目因服务而异，但主要格式是列出带有值的指令（directives）。指令是使用保留术语的选项，可能像赋值语句，例如：

```
AUTOCREATE_SERVER_KEYS=YES
```

在 `ssh` 配置文件 `/etc/sysconfig/sshd` 中找到；或者它们可能以指令和参数（参数）的形式出现，如：

```
path /var/crash
```
