
`/etc/inet/hostname.interface` 文件是一个包含网络适配器主机名的文本文件。该文件与 `/etc/inet/hosts` 一起使用确定系统启动时分配哪个 IP 地址。例如，考虑一个有两个接口（`le0` 和 `le1`）的系统。必须使用两个 `hostname.interface` 文件——`/etc/inet/hostname.le0` 和 `/etc/inet/hostname.le1`。下一节介绍了这些文件如何配合 `/etc/inet/hosts` 和 `/etc/inet/netmasks` 配置系统的网络接口。

## 适配器如何配置

图 9.2 展示了配置文件、网络适配器及其网络地址之间的关系。

图 9.2. Network Adaptor Configuration 78b12ae14a18c2c115c2be90d0b.png

系统的网络适配器在启动时的配置如下（参见图 9.2）：

- 系统列出网络适配器并与 `/etc/inet/hostname.interface` 文件配对。主机名与 `/etc/inet/hosts` 文件中的 IP 地址配对。
- 每个接口的子网掩码来自 `/etc/inet/netmasks` 文件。

## 监听模式

监听模式（在本章之前定义）可以使用工具 `cpm`（检查监听模式）检测。`cpm` 可从 http://www.purdue.edu/tools/unix/ 获取。

## 运行 cpm

以下示例演示了 `cpm` 检测监听模式的接口。

- 1. 处于监听模式的接口

```
## cpm

3 network interfaces found:

lo0: Normal

le0: *** PROMISOUS MODE ***

le1: Normal

1 个处于监听模式。
```

- 2. 无接口处于监听模式

```
## cpm

3 network interfaces found:

lo0: Normal

le0: Normal

le1: Normal

0 个处于监听模式。
```

## 网络服务

网络服务是 Solaris 操作系统的一个逻辑部分，用于计算机之间特定类型信息的通信。配置了一个或多个服务的系统将同意与请求服务的计算机通信。

服务的示例包括：

- `telnet`——允许其他系统的用户登录本系统并启动 shell。
- `ftp`——允许其他系统的用户在本系统建立文件传输会话以获取或投放文件。
- `sendmail`——允许其他系统建立连接以发送和接收电子邮件。
- `ntp`——允许其他系统向本系统询问时间，以便两个系统同步时钟。
- `routed`——在工作站本身是路由器或工作站位于具有多个提供其他网络连接的复杂网络中促进路由信息的交换。

## 不需要的服务

Solaris 系统配备了各种网络服务，其中大多数已激活。对于每个系统（及其所有者）来说，禁用不需要的服务是有益的。请参考第 13 章有关禁用网络服务的信息。

## 网络服务编号

网络服务（也称为端口号）定义在互联网的意见请求 (`RFC` ) `1700` 中。有关 `RFC` 的更多信息，请参阅附录中的建议阅读部分。

## 网络服务配置

服务通过两个配置文件配置：`/etc/inet/services` 和 `/etc/inet/inetd.conf`。这两个文件共同工作，确定激活哪些网络服务以及如何配置它们。

`/etc/inet/services`

`/etc/inet/services` 文件将每个服务名称与端口号和端口类型配对。`/etc/services` 是 `/etc/inet/services` 的链接；存在 `/etc/services` 是为了与旧版本的 UNIX 兼容。`/etc/inet/services` 中的字段定义如下：

```
name port/protocol [aliases]
```

其中 `name` 是名称，`port` 是 IP 端口号，`protocol` 是使用的协议（传输控制协议 [TCP] 或用户数据协议 [UDP]），`aliases` 是服务的可选备名称列表。
以下是 `/etc/inet/services` 的部分：

```
#ident "@(#)services 1.1697/05/12 SMI" /* Svr4.0 1.8 */

#

## Network services, Internet site

#

tcpmux 1/tcp

echo 7/tcp

echo 7/udp

discard 9/tcp sink null

discard 9/udp sink null

systat 11/tcp users

daytime 13/tcp
```

`daytime 13/udp`
`netstat 15/tcp`
`chargen 19/tcp ttytest source`
`chargen 19/udp ttytest source`
`ftp-data 20/tcp`
`ftp 21/tcp`
`telnet 23/tcp`
`smtp 25/tcp mail`
`time 37/tcp timsimver`
`time 37/udp timsimver`
`name 42/udp nameserver`
`whois 43/tcp nickname # 通常用于 sri-nic`
...

## `/etc/inetd.conf`

`/etc/inetd.conf` 文件将每个服务（通过其名称）与系统提供的网络服务等效起来。`/etc/inetd.conf` 文件包含了启动该特定服务所需的配置特征。
`/etc/inetd.conf` 是指向 `/etc/inetd.conf` 的链接；存在 `/etc/inetd.conf` 是为了让系统级与旧版本的 UNIX 兼容。`/etc/inetd.conf` 中的字段定义如下：

`name protocol waitstatus user args`

其中，`name` 是服务的名称；`type` 是这些类型之一——`stream`,`dgram`,`raw`,`seqpacket`,或 `tli`；`protocol` 是 `/etc/inet/protocols` 中列出的协议类型之一；`waitstatus` 是 `wait` 或 `nowait`；运行路径的用户帐户是服务的完整路径名（`internal` 的值具有下文解释的特殊用途）；`args` 包含了所有程序参数（从 de第一个参数 `arg0` 开始，即程序名本身）。
这里是 `/etc/inetd.conf` 文件的部分内容。

```
#

#ident "(#)inetd.conf 13 98/06/02 SMI" /* svr4.0 1.5 */

#

# inetd(1M)的配置文件。请参见 inetd.conf(4)。

#

# 要重新配置运行中的 inetd 进程，请编辑此文件，然后

# 向 inetd 进程发送 SIGHUP 信号。

#

# 基于 socket 的 Internet 服务的语法：

## <service_name> <socket_type> <proto> <flags> <user> <path> <args>

#

# 基于 TLI 的 Internet 服务的语法：

## <service_name> tli <proto> <flags> <user> <path> <args>

#

# Ftp 和 telnet 是标准的 Internet 服务。

#

ftp stream tcp nowait root /usr/sbin/in.ftpd in.ftpd

telnet stream tcp nowait root /usr/sbin/in.telnet in.telnet

# Tnamed 服务过时的 I-116 名称服务器协议。
```
