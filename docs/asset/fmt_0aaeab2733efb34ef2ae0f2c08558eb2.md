
# `/etc/services`

```
/etc/services:
# $id:services.v 1.13 2000/12/01 03:20:17 nalin Exp $
#
# Network services, Internet style
# 注意，目前 IANA 的策略是为 TCP 和 UDP 分配单个
# 熟知端口号；这里的大多数条目都有两个条目
# 即使该协议不支持 UDP 操作。
# 更新自 RFC 1700，“分配数字”（1994年10月）。并非所有端口
# 都包含在内，仅包含常用的端口。
# 每行描述一项服务，格式如下：
# service name    port/protocol [aliases...]      # comment
tcpmux           1/tcp                         # TCP port service multiplexer
tcpmux      1/udp          # TCP port service multiplexer
rje         5/tcp          # Remote Job Entry
rje         5/udp          # Remote Job Entry
echo        7/tcp
echo        7/udp
discard     9/tcp          sink null
discard     9/udp          sink null
systat     11/tcp         users
systat     11/udp         users
datime     13/tcp
datime     13/udp
qtdd       17/tcp         quote
qtdd       17/udp         quote
msp         18/tcp          # message send protocol
msp         18/udp          # message send protocol
chargen     19/tcp         ttytst source
chargen     19/udp         ttytst source
ftp-data    20/tcp
ftp-data    20/udp
ftp         21/tcp
ftp         21/udp
ssh         22/tcp          # SSH Remote Login Protocol
ssh         22/udp          # SSH Remote Login Protocol
telnet      23/tcp
telnet      23/udp
# 24 - private mail system
smtp        25/tcp         mail
```

文件的前 14 行只是注释（以每行开头的 `#` 字符识别）。在注释之后，您会注意到三列信息。最左侧的一列包含每个服务的名称。中间列定义了用于该服务的端口号和协议类型。最右侧字段可以包含服务的可选别名或别名列表。

例如，让我们检查文件片段中的最后一个条目。它描述了 `SMTP`（简单邮件传输）服务，这是用于在互联网上传递电子邮件的服务。中间列包含文本 `25/tcp`，它告诉我们 `SMTP` 协议使用端口 `25`，并使用传输控制协议（`TCP`）作为其协议。

那么，端口号到底是什么？它是一个为特定服务保留的唯一数字。它允许网络连接被正确路由到处理它的软件上。例如，当电子邮件从其他计算机投递到您的 Linux 盒机时，远程系统必须首先与您的系统建立网络连接。您的计算机接收连接请求，检查它，发现它被标记为端口 `25`，因此知道该连接应该交给处理电子邮件的程序（恰好是 `sendmail`）。

`www.unlimited.com` 上的额外内容

## 第三部分 管理 Red Hat Linux

静静运行在后台处理服务请求（如 `sendmail`）的程序被称为守护进程（`daemon`）。通常，守护进程在您的系统启动时自动启动，并一直运行到您的系统关闭。守护进程也可以由 `xinetd` 根据需要启动，`xinetd` 是一种特殊的守护进程，它监听大量的端口号，然后启动请求的进程。

我提到过 `SMTP` 使用 `TCP` 协议。某些服务使用 `UDP`，即用户数据报协议。对于 `TCP` 和 `UDP`（至少就此安全讨论而言），您真正需要知道的是它们提供了对通过网络连接发送的信息进行打包的两种方式。`TCP` 连接提供错误检测和丢失数据的重传。`UDP` 则不提供。

了解这些服务以及如何访问它们至关重要。

### 安全远程 shell 和登录

`UNIX` 在提供许多共享信息的方法有着悠久的历史。`Red Hat Linux` 遵循这一传统，提供了远程登录、数据传输和远程 shell 服务。尽管这些服务非常有用，但在使用不当时，它们也可能产生风险。这些有用但具有风险的功能之一是远程 shell 服务，它传统上运行在 `TCP` 上。

您如何让一个系统信任另一个系统？一种方法是在 `hosts.equiv` 文件中列出信任主机。通过在 `hosts.equiv` 中列出系统，您是在告诉您的计算机远程系统是信任的。

即使您没有 `hosts.equiv` 文件，单个用户也可以通过在其主目录下创建 `.hosts` 文件来启用其账户的远程 shell 访问。`.hosts` 文件与 `hosts.equiv` 文件基本相同，但它影响该用户而不是所有用户。其他使用 `hosts.equiv` 和 `.hosts` 文件建立信任的命令包括 `login`（远程登录）命令和 `rcp`（远程复制）命令。

参考第9章获取更多关于远程 shell 和其他网络服务的知识。

除非绝对需要远程 shell 或远程复制服务，否则我建议完全禁用它们。

### 禁用网络服务

远程 shell 服务只是 `xinetd` 端口映射处理的许多服务之一。`Xinetd` 是一个监听大量网络端口的守护进程。当连接到特定的端口号时，`xinetd` 会自动启动该服务的相应程序并处理该连接。配置文件 `/etc/xinetd.conf` 用于告诉 `xinetd` 监听哪些端口以及启动哪些程序。要禁用远程 shell 服务，请编辑 `xinetd.conf` 文件并查找类似下面的部分：

```
service shell
{
    socket_type      = stream
    wait             = no
    user             = root
    instances        = UNLIMITED
    flags            = IDONLY
    log_on_success   += USERID
    server           = /usr/sbin/in.rshd
}
```

## 504 第三部分 管理 Red Hat Linux

请注意，此示例的第一行将该服务标识为 "`shell`" 。这与 `/etc/services` 文件中列出的服务名完全匹配。要禁用 `shell` 服务，你只需简单地从 `xinetd.conf` 文件中删除该部分即可。更好的做法是，你可以在大括号 `{` 和 `}` 之间的某处添加 `disabled = yes` 这一行。因此，禁用 `shell` 服务的示例如下：

```bash
service shell {
  socket_type         = stream
  wait               = no
  user               = root
  instances          = UNLIMITED
  flags              = IDONLY
  log_on_success     += USERID
  server             = /usr/sbin/in.rhsd
  disabled           = yes
}
```

同样，你应该通过确保在 `/etc/xinetd.d/login` 文件中设置 `disabled=yes` 来禁用登录服务。

可以保持登录服务激活，但禁用 `/etc/host.equiv` 和 `.hosts` 文件的使用，从而要求登录始终提示密码。与其删除该部分或添加 "`disabled`" 行，不如找到 "`server = /usr/sbin/in.rhsd`" 行，并在末尾添加一个空格后跟 `-L`。

你需要向 `xinetd` 进程发送信号以重新加载其配置文件。最快的方法是重启 `xinetd` 服务。作为 `root` 用户，在 `shell` 中输入以下命令：

```bash
# /etc/init.d/xinetd restart
Stopping xinetd:   [ OK ]
Starting xinetd:   [ OK ]
```

这就是你禁用远程 shell 和远程登录服务的原因。如果有人尝试使用这些服务，他们将收到“Connection Refused”（拒绝连接）错误消息。

## 使用 TCP wrappers
