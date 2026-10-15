
`service-name` 条目是 `/etc/services` 文件中有效服务的名称。对于“内部”服务（下文将讨论），服务名称必须是服务的官方名称（即 `/etc/services` 中的第一个条目）。当用于指定基于 Sun-RPC 的服务时，此字段是 `/etc/rpc` 文件中的有效 RPC 服务名称。“/” 右侧的部分是 RPC 版本号。

## 立即解决方案

这可以仅仅是一个单数字参数或版本范围。范围由低版本到高版本界定 - 例如 `rusers/1-3`。

`socket-type` 应该是 `"stream"`,`"dgram"`,`"raw"`,`"rdcm"` 或 `"sepacket"` 之一，取决于套接字是流式、数据报（datagram）、可靠投递的消息还是顺序包套接字。

`protocol` 必须是 `/etc/protocols` 中给出的有效协议。示例可能是 `"tcp"` 或 `"udp"`。基于 RPC 的服务通过 `"rpc/tcp"` 或 `"rpc/udp"` 服务类型指定。

`wait/nowait` 条目仅适用于数据报套接字（其他套接字在此空间应有 `"nowait"` 条目）。如果数据报服务器连接到其对端，释放了套接字以便 `inetd` 能在该套接字上接收后续消息，则称为“多线程”服务器，并应使用 `"nowait"` 条目。对于处理所有入站数据报并最终超时的数据报服务器，该服务器被称为“单线程”服务器并应使用 `Wait` 服务器。`Com-sat(8)` (`biff(1)`) 和 `talkd(8)` 都是此类类型数据报服务器的示例。`Tcpfd(8)` 是例外；它是一个建立伪连接的数据报服务器。它必须列为 `"Wait"` 以避免竞态条件；服务器读取第一个包，创建一个新套接字，然后派生（`fork`）并退出 `inetd` 以检查新的服务请求以生成新服务器。可选的 `"max"` 后缀（通过点与 `"Wait"` 或 `"nowait"` 分隔）指定了 `inetd` 可能生成的最大服务器实例数量。如果省略，`"max"` 默认认为 40。

![](img/166cd29830b01a9e3eceb33240be1bcf_170_0.png)

`user` 条目应包含运行服务器的用户名称。这允许服务器获得比 `root` 更低的权限。可以通过在用户名后添加一个点并跟上组名来指定可选的组名。这允许服务器以与密码文件中指定的不同的（主）组 ID 运行。如果指定了组且用户不是 `root`，与用户相关的辅助组仍会被设置。

`server-program` 条目应包含要执行的程序的路径，当在套接字上发现请求时，由 `inetd` 执行该程序。如果 `inetd` 内部提供此服务，则此条目应为 `"internal"`。

`server program arguments` 应该像通常一样，以 `argv(0)` 开始，即程序的名称。如果服务是在内部提供的，则用 `"internal"` 一词代替此条目。

`inetd` 通过其内部的例程提供几个“简单”服务。这些服务是 `"echo"`,`"discard"`,`"chargen"`（字符生成器）、`"daytime"`（人类可读时间）和 `"time"`（机器可读时间，格式为自 1900 年 1 月 1 日午夜以来的秒数）。所有这些服务都是基于 `tcp` 的。`inetd` 在接收到挂断信号 `SIGHUP` 时重新读取其配置文件。当重新读取配置文件时，可以添加、删除或修改服务。`inetd` 创建 `/etc/inetd.pid` 文件，其中包含进程标识。

另参

- `comsat(8)`, `fingerd(8)`, `ftpd(8)`, `rexec(8)`, `rlogind(8)`, `rshd(8)`, `telnetd(8)`, `tfpfd(8)`

历史

`inetd` 命令出现在 4.3BSD。对基于 Sun-RPC 服务支持模仿 SunOS 4.1。

## 使用 inetd 启动 smbd 和 nmbd

启用 Samba 的第一步是确保 SMB 或 NetBIOS 服务在 `/etc/services` 文件中有相应的条目。取决于是否存在，你需要在 `/etc/services` 中添加以下内容：

```
sm 139/tcp

netbios 137/udp
```

然后，你需要确保设置了适当的服务。通过向你的 `/etc/inetd.conf` 添加行来实现：

```
smbd nowait /usr/local/samba/bin/smbd

nmbd wait /usr/local/samba/bin/nmbd
```

`service-name` 条目是 `/etc/services` 文件中有效服务的名称。对于“内部”服务（下文将讨论），服务名称必须是服务的官方名称（即 `/etc/services` 中的第一个条目）。当用于指定基于 Sun-RPC 的服务时，此字段是 `/etc/rpc` 文件中的有效 RPC 服务名称。“/” 右侧的部分是 RPC 版本号。

这仅仅是一个单数字参数或版本范围。范围由低版本到高版本界定 - `"rusers/1-3"`。

`socket-type` 应该是 `"stream"`,`"dgram"`,`"raw"`,`"rdcm"` 或 `"sepacket"` 之一，取决于套接字是流式、数据报、可靠投递的消息还是顺序包套接字。

`protocol` 必须是 `/etc/protocols` 中给出的有效协议。示例可能是 `"tcp"` 或 `"udp"`。基于 RPC 的服务通过 `"rpc/tcp"` 或 `"rpc/udp"` 服务类型指定。

`wait/nowait` 条目仅适用于数据报套接字（其他套接字在此空间应有 `"nowait"` 条目）。如果数据报服务器连接到其对端，释放了套接字以便 `inetd` 能在该套接字上接收后续消息，则称为“多线程”服务器，并应使用 `"nowait"` 条目。对于处理所有入站数据报并最终超时的数据报服务器，该服务器被称为“单线程”服务器并应使用 `Wait` 服务器。`Com-sat(8)` (`biff(1)`) 和 `talkd(8)` 都是此类类型数据报服务器的示例。`Tcpfd(8)` 是例外；它是一个建立伪连接的数据报服务器。它必须列为 `"Wait"` 以避免竞态条件；服务器读取第一个包，创建一个新套接字，然后派生（`fork`）并退出 `inetd` 以检查新的服务请求以生成新服务器。可选的 `"max"` 后缀（通过点与 `"Wait"` 或 `"nowait"` 分隔）指定了 `inetd` 可能生成的最大服务器实例数量。如果省略，`"max"` 默认认为 40。

`user` 条目应包含运行服务器的用户名称。这允许服务器获得比 `root` 更低的权限。可以通过在用户名后添加一个点并跟上组名来指定可选的组名。这允许服务器以与密码文件中指定的不同的（主）组 ID 运行。如果指定了组且用户不是 `root`，与用户相关的辅助组仍会被设置。

`server-program` 条目应包含要执行的程序的路径，当在套接字上发现请求时，由 `inetd` 执行该程序。如果 `inetd` 内部提供此服务，则此条目应为 `"internal"`。

`server program arguments` 应该像通常一样，以 `argv(0)` 开始，即程序的名称。如果服务是在内部提供的，则用 `"internal"` 一词代替此条目。

`inetd` 通过其内部的例程提供几个“简单”服务。这些服务是 `"echo"`,`"discard"`,`"chargen"`（字符生成器）、`"daytime"`（人类可读时间）和 `"time"`（机器可读时间，格式为自 1900 年 1 月 1 日午夜以来的秒数）。所有这些服务都是基于 `tcp` 的。有关这些服务的详情，请咨询网络信息中心的适当 RFC。

`inetd` 在接收到挂断信号 `SIGHUP` 时重新读取其配置文件。当重新读取配置文件时，可以添加、删除或修改服务。`inetd` 创建 `/etc/inetd.pid` 文件，其中包含进程标识。

另参

- `comsat(8)`, `fingerd(8)`, `ftpd(8)`, `rexec(8)`, `rlogind(8)`, `rshd(8)`, `telnetd(8)`, `tfpfd(8)`

历史

`inetd` 命令出现在 4.3BSD。对基于 Sun-RPC 服务支持模仿了 SunOS 4.1。

## 以 sm 启动 smbd 和 nmbd

启用 Samba 的第一步是确保 SMB 或 NetBIOS 服务在 `/etc/services` 文件中有相应的条目。取决于是否存在，你需要在 `/etc/services` 中添加以下内容：

```
sm 139/tcp

netbios 137/udp
```

然后，你需要确保设置了适当的服务。通过向你的 `/etc/inetd.conf` 添加行来实现：

```
smbd nowait /usr/local/samba/bin/smbd

nmbd wait /usr/local/samba/bin/nmbd
```
