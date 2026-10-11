

## 示例 10-52 将服务绑定到特定地址

```text
defaults
(
    log_type      = SYSLOG local4 info
    log_on_success  = PID HOST EXIT DURATION
    log_on_failure  = HOST
    instances       = 8
)
service ftp
(
    id              = ftp
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    only_from       = 172.17.0.0 172.19.0.0/20
    bind            = 172.17.1.1 # widget
    log_on_success  += USERID
    log_on_failure  += USERID
    server          = /usr/sbin/in.ftpd
    server_args     = -l -a
)
service ftp
(
    id              = ftp_chroot
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    bind            = 24.170.1.218 # widget-srvr
    log_on_success  += USERID
    log_on_failure  += USERID
    access_times    = 8:30-11:30 13:00-18:00
    log_on_success  += USERID
    log_on_failure  += USERID
    server          = /usr/sbin/anon/in.ftpd
)
```

在每种情况下使用 **bind** 将允许仅发往该接口的数据包调用指定的守护进程。因此，我们可以通过执行 **ftp widget-srvr** 来访问匿名服务器。由于该服务没有访问控制，因此所有人都可以访问。然而，由于 **access_times** 属性的限制，访问仅在上午 8:30 至 11:30 以及下午 1:00 至 6:00 之间授予。

另一方面，执行 **ftp widget** 仅当客户端 IP 地址的前两个八位位组以 172.17 开头，或者请求来自 172.19.0.0 到 172.19.15.255 范围内的地址时才会成功，这是因为 **only_from** 属性的限制。

**使用 redirect 属性。** redirect 属性提供了一种通过服务器代理服务的方法。换言之，用户可以 telnet 到运行 xinetd 的特定服务器，该服务器会打开到另一个系统的连接。我们可以通过 */etc/xinetd.conf* 中示例 10-53 所示的条目来实现这一点。这里我们以 telnet 为例，但它可以用于任何 TCP 服务。flags 属性中的 REUSE 值是必需的。注意 bind 属性的使用。它具有以下效果。如果命令 `telnet 172.17.33.111`（或在本例中的 topcat）被使用，那么连接将直接建立到服务器本身（topcat）。然而，如果命令 `telnet 201.171.99.99` 被使用，那么连接将被转发到主机 172.17.1.1（foghorn）的 23 端口（telnet 端口）。示例 10-54 展示了最后一条命令的效果。嘿——foghorn 没有运行 Linux！没关系，这些其他 UNIX 变体也就再存在一小会儿了！

## 示例 10-53 /etc/xinetd.conf 中 redirect 和 bind 的使用

```text
service telnet
{
  socket_type = stream
  wait = no
  flags = REUSE
  user = root
  bind = 172.17.33.111
  server = /usr/sbin/in.telnetd
  log_on_success = PID HOST EXIT DURATION USERID
  log_on_failure = RECORD HOST
}

service telnet
{
  socket_type = stream
  protocol = tcp
  wait = no
  flags = REUSE
  user = root
  bind = 201.171.99.99
  redirect = 172.17.1.1 23
  log_on_success = PID HOST EXIT DURATION USERID
  log_on_failure = RECORD HOST
}
```

## 示例 10-54 redirect 的效果

```text
$ telnet 201.171.99.99
Trying 201.171.99.99...
Connected to 201.171.99.99.
Escape character is '^]'.

UNIX(r) System V Release 4.0 (foghorn)
login:
```

由于 Linux 支持每个物理接口最多 256 个逻辑接口，理论上你可以为系统中的每个物理地址代理多达 256 个不同的地址。

虽然 redirect 机制可能非常有用，但在实施时要谨慎。确保在代理服务器和最终系统上都发生日志记录。其他被认为更安全的代理实现方法在第 16 章第 488 页“通用防火墙参考资料”和“DMZ 资源”中引用的参考文献中有讨论。然而，在紧密控制的内部网络中，这种实现可能很方便。

## 集成 TCP_wrappers

将 TCP_wrappers 功能包含在 /etc/xinetd.conf 中非常简单，以至于除了它所代表的显著功能外，显得有些平淡无奇。TCP_wrappers 的所有功能都可以通过 xinetd 集成，就像通过 inetd 集成一样。示例 10-55 显示了一个使用 TCP_wrappers 为许多服务进行封装的示例 /etc/xinetd.conf 文件。只要将 /usr/sbin/in.tcpcd 设置为属性 server 的值，该服务就会被封装。还请注意，此类条目总是将 server_args 属性设置为要调用的守护进程（完全限定路径）。这是必须的！回想一下第 229 页“构建 xinetd”一节，我们将 xinetd 与 libwrap 一起编译。无论你是否使用 libwrap 编译，示例 10-55 中的配置文件都会按预期工作。使用 libwrap 编译的效果是仅引入 /etc/hosts.allow 和 /etc/hosts.deny 中找到的访问限制（不包括选项）。示例 10-55 中显示的内容提供了 TCP_wrappers 的完整功能集——横幅、spawn、twist 等。我们从第 194 页“TCP Wrappers”部分开始讨论的所有关于 TCP_wrappers 的内容，现在都适用于此处。

## 示例 10-55 在 /etc/xinetd.conf 中使用 TCP_wrappers

```text
defaults
{
    log_type
        = SYSLOG local4 info
    log_on_success
        = PID HOST EXIT DURATION
    log_on_failure
        = HOST
    instances
        = 8
}

service xadmin
{
    type
        = INTERNAL UNLISTED
    flags
        = REUSE
    socket_type
        = stream
    protocol
        = tcp
    port
        = 9967
    wait
        = no
    only_from
        = topcat
}

service ftp
{
    id
        = ftp
    socket_type
        = stream
    protocol
        = tcp
    wait
        = no
    user
        = root
    only_from
        = 172.17.0.0
    log_on_success
        += USERID
    log_on_failure
        += USERID
    access_times
        = 8:00-16:30
    server
        = /usr/sbin/tcpsd
    server_args
        = /usr/sbin/in.ftpd -l -a
}
```

**示例 10-55 在 /etc/xinetd.conf 中使用 TCP_wrappers（续）**

```text
service telnet
{
    socket_type     = stream
    wait            = no
    flags           = NAMEARGS REUSE
    user            = root
    bind            = 172.17.33.111
    server          = /usr/sbin/tcpd
    server_args     = /usr/sbin/in.telnetd
    log_on_success  = PID HOST EXIT DURATION USERID
    log_on_failure  = RECORD HOST
}

service telnet
{
    socket_type     = stream
    protocol        = tcp
    wait            = no
    flags           = REUSE
    user            = root
    bind            = 201.171.99.99
    redirect        = 172.17.1.1 23
    log_on_success  = PID HOST EXIT DURATION USERID
    log_on_failure  = RECORD HOST
}
...
<文件的其余部分省略>
...
```

## xinetd 守护进程

xinetd 守护进程接受多个参数。这些参数可以被特殊服务 default 中的属性覆盖，或者被一个或多个服务中的单个属性条目覆盖。然而，在此处给出的所有参数或其默认值控制 xinetd 本身的行为。例如，如果为 xinetd 指定了 **-s** 标志，那么它将记录所有状态转换消息，尽管 */etc/xinetd.conf* 文件为与服务相关的消息指定了其他日志位置。可用的参数列表见表 10.15。

应该注意，xinetd 报告的所有状态信息，如重新配置通知，始终出现在由 **-syslog** 或 **-filelog** 标志指定的日志文件中（-syslog 默认选择器为 daemon.info），无论 */etc/xinetd.conf* 中通过 default 或其他方式的设置如何。此外，如果你希望将 xinetd 的 PID 捕获到一个文件中，你可以这样做：

```text
xinetd -pid > /var/run/xinetd.pid 2>&1
```

如第 230 页示例 10-38 中给出的脚本所示。

## 可用于 xinetd 的信号

xinetd 守护进程还会根据发送的某些信号采取特殊操作。表 10.16 描述了它接受的每个信号的功能。请注意，每当添加新服务或 default 条目，或者当以下属性之一发生变化时，你都必须使用 SIGTERM（或更简单的 TERM）信号终止 xinetd。

