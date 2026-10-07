
该命令将返回一个明确允许或拒绝的访问列表，包括访问相关的守护进程（daemon）、访问相关的客户端（client）以及实际的访问判定。这是一个示例：

```
>>> Rule /etc/hosts.allow line 18:
daemons:  in.telnetd
clients: .ntrnet.net
access:  granted
```

另一个工具是 `tcpmatch` 实用程序，允许你对特定的守护进程和客户端进行测试。命令如下：

```
# tcpmatch in in.telnetd www.macrosoft.com
```

如果允许访问，命令将返回以下内容：

```
client:  hostname www.macroshaft.com
client:  address  117.4.137.45
server:  process   in.telnetd
access:  granted
```

如果主机被拒绝访问，响应将如下：

```
client:  hostname www.macroshaft.com
client:  address  117.4.137.45
server:  process   in.telnetd
matched: /etc/hosts.deny line 10
access:  denied
```

一旦用户获得了访问，TCP Wrappers 软件包为你的系统提供了相当的保护。然而，仅靠拒绝服务是不够的。

## xinetd

从 Red Hat 7.0 开始，`inetd` 不再默认安装。相反，它使用了更安全的扩展 Internet 服务守护进程 (`xinetd`)。其他发行版也在切换到 `xinetd`。`xinetd` 和 `inetd` 可以在系统中并发运行。事实上，`xinetd` 代码的作者建议运行 RPC 服务的管理员通过 `inetd` 运行。你可以使用你的 `inetd.conf` 为非 RPC 服务创建一个 `xinetd.conf`。

![](img/4fb617eb648f87def380ef5d92052d01_260_0.png)

## 第 7 章 安全

在 Red Hat 7.0 系统上，`/usr/sbin/inetdconvert` 是一个 Python 脚本，它能将你的 `inetd.conf` 文件转换为新 `/etc/inetd.d` 目录下的多个文件。使用此工具转换所有尚未转换服务的命令是：

```
# inetdconvert --convertremaining
```

一个用于将 `inetd.conf` 脚本转换为 `xinetd.conf` 文件的 Perl 脚本包含在 `xinetd` 软件包的其他版本中，位于与二进制文件相同的目录下。如果该脚本存在于你的系统中，它将位于 `/usr/sbin`，你可能需要使用以下命令运行它（假设可执行文件位于 `/usr/sbin`）：

```
# /usr/sbin/xconv.pl < /etc/xinetd.conf > /tmp/xinetd.conf
```

转换在 `/etc/xinetd.d` 目录下创建了几个文件。这些文件包含了由 `xinetd` 管理的服务的配置选项，因此你需要编辑这些文件来配置 `xinetd` 以按照你想要的方式处理这些服务。例如，列表 7.9 显示了 `/etc/xinetd.d/telnet` 文件，它配置了 Telnet 服务。

### 列表 7.9 /etc/xinetd.d/telnet 文件配置了 Telnet 服务，是单个服务 xinetd 文件的典型示例。

```
# default: on
# description: The telnet server serves telnet sessions, it uses \
# encrypted username/password pairs for authentication.
service telnet {
    flags = REUSE NAMEINARGS
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/in.telnetd
    log_on_failure += USERID
}
```

来自 `inetd.conf` 的条目处理 Telnet 服务实际上包含了大部分相同的信息：

```
telnet stream nowait root /usr/sbin/tcpd.telnetd
```

*(注：由于原始文本后半部分存在大量重复和 OCR 识别乱码（如 "What is different is the flags field?" 等），上述翻译已根据逻辑内容进行了整合处理。)*
