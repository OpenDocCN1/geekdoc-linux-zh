
```
log_on_success      = HOST PID USERID
```

你正在向 `/etc/xinetd.conf` 中 `defaults` 部分的 `log_on_success` 属性已指定的列表中添加值。同样地，你也可以覆盖服务配置中的默认值。假设你不想通过 syslog 记录，而是倾向于使用 `/var/log` 目录下的文件记录。你可以通过这种方式覆盖 `log_type` 设置：

```
log_type           = FILE /var/log/mynetdservice.log
```

此外，你可以根据需要添加新属性。例如，为了通过 `nice` 属性控制 FTP 服务器的优先级，你可以将其添加到配置中。完成的示例配置在列表 14-5 所示。

### 列表 14-5：`/etc/xinetd.d/ftpd`

```
service ftp
{
    socket_type    = stream
    wait           = no
    user           = root
    server        = /usr/sbin/in.ftpd
    server_args      = -1 -a
    log_on_success  += DURATION USERID
    nice              = 10
}
```

## 通过名称或 IP 地址控制访问

通过名称或 IP 地址控制某些访问是常见做法。以前可以使用名为 `tcpd` 的封装程序配合 `/etc/allow` 和 `/etc/deny` 文件来实现。现在，如果你想限制对服务的访问，可以使用 xinetd。例如，如果你想允许来自网络内部的访问，可以使用以下内容：

```
# 仅允许来自你的网络的访问
only_from = 192.168.1.0/24
```

当用户尝试从不在列表中的 IP 地址连接服务时，访问将被拒绝。如果你想允许特定主机的访问，可以在 `only_from` 属性中列出它们：

```
only_from = 192.168.1.10 192.168.1.11
```

# 第14 章：xinetd

## 每次仅 10 个连接

`instances` - 10

在这里，`xinetd` 会启动最多十个服务器来处理多个请求。如果连接请求数超过十个，超过十个的请求将被拒绝，直到至少有一个服务器退出。

## 限制日志文件大小

许多攻击者知道大多数服务都会写入访问日志条目。他们经常向写入大量日志条目的守护进程发送许多请求，以填满 `/var` 或其他分区的磁盘空间。因此，为服务设置最大日志大小是一个好主意。默认情况下，`xinetd` 使用 syslog 的 `daemon.info` 设施写入日志条目。你可以使用此属性更改 syslog 设施，如下：

```
log_type SYSLOG facility
```

使用 syslog 的 `authpriv.info` 设施请使用：

```
log_type SYSLOG authpriv.info
```

此外，`xinetd` 还可以写入你指定的日志。写入日志的 `log_type` 语法为：

```
log_type FILE /path/to/logfile [soft_limit [hard_limit]]
```

例如，将某个服务的日志文件 `/var/log/myservice.log` 限制为最多 10,485,760 字节 (10MB)，并在限制接近 8,388,608 字节 (8MB) 时在 syslog 中接收警告，则如下所示使用 `log_type` 属性：

```
log_type FILE /var/log/myservice.log 8388608 10485760
```

当日志达到 8MB 时，会在 syslog 中看到一条警条目；当日志文件达到 10MB 限制时，`xinetd` 会停止使用该日志文件的服务。

## 限制负载

你可以使用 `maxload` 属性来指定 `xinetd` 停止接受某个服务的系统负载。该属性具有以下语法：

```
max_load number
```

此数字指定了服务器停止接受连接的负载；负载值基于一分钟 CPU 负载平均值，如下例所示：

# 第三部分：系统安全

```
@Not under load
max_load = 2.9
```

当系统负载平均值高于 2.9 时，该服务将临时禁用，直到负载平均值降低。

> 要使用 `max_load` 属性，请使用 `-with-load-avrg` 选项编译 `xinetd`。

`nice` 属性设置由 `xinetd` 启动的服务器进程优先级，如下例：

```
Be low priority
nice - 15
```

这确保了由 `xinetd` 启动的服务优先级较低。

> 要设置高优先级，请使用较小的数字。最高优先级为 -20。

## 限制连接速率

此属性控制 `xinetd` 每秒为自定义服务启动多少个服务器。第一个数字（秒）指定频率（每秒连接数）。第二个数字（秒）指定了在达到服务器/秒限制后 `xinetd` 等待多长时间，如下例所示：

```
Only 5 connections per second
cps = 10 60
```

在这里，`xinetd` 最多启动 10 个服务器，如果达到此限制，将等待 60 秒。在等待期间，该服务对任何新客户端不可用。服务请求将被拒绝。

## 创建访问区分服务

有时，像 HTTP 或 FTP 这样的服务必须在服务器上运行时，能够根据访问请求的来源进行区分。这种区分允许对服务如何向终端用户可用进行严格控制。

例如，如果你有一个有两个接口的系统（`eth0` 连接到本地局域网，`eth1` 连接到互联网路由器），你可以为每个接口的 FTP 服务提供不同的限制 `set`。你可以限制公共（即 `eth1`）面向互联网的接口上的 FTP 服务，使其仅在系统管理员位于局域网的工作时间允许允许 FTP 连接；或者，当局域网用户请求时不受限制地运行 FTP 服务。当然，你不想让互联网用户在工作时间之后访问 FTP，但你希望加班的员工随时通过局域网访问服务器。你可以使用 `bind` 属性将 IP 地址绑定到服务。具有多个网络接口的系统拥有多个 IP 地址，此属性可以在同一机器的不同接口（即 IP 地址）上提供不同功能。列表 14-6：`/etc/xinetd.d/ftp-worldwide` 用于 FTP 服务的配置

### 列表 14-6：`/etc/xinetd.d/ftp-worldwide`

```
service ftp
{
  id              = ftp-worldwide
  wait            = no
  user            = root
  server          = /usr/sbin/inftpd
  server_args     = -1
  instances       = 10
  cps             = 5
  nice            = 10
  only_from       = 0.0.0/0
  bind            = 169.132.226.215
  access_times    = 08:00-17:00
}
```

上述配置的作用如下：

- `id` 字段为全球（互联网）的 FTP 服务设置名称 "`ftp-worldwide`"。

- 该服务绑定到 `eth1` 接口上的 IP 地址 (`169.132.226.215`)。因为 `only_from` 允许整个 IP 地址空间 (`0.0.0/0`) 访问。

- 使用 `access_times` 属性将访问限制在 08:00-17:00。

- 同时最多运行十个 FTP 实例。

- 每秒内最多启动五个服务器实例。

- 服务使用 `nice` 属性以低优先级 (10) 运行。

列表 14-7 显示了仅限局域网访问（即局域网）的 FTP 服务配置文件 `/etc/xinetd.d/ftp-office`

### 列表 14-7：`/etc/xinetd.d/ftp-office`

```
service ftp
{
  id = ftp-office
  socket_type = stream
  wait = no
  user = root
  server = /usr/sbin/in.ftpd
  server_args = -1
  only_from = 192.168.1.0/24
  bind = 192.168.1.215
}
```

私有 FTP 服务命名为 `ftp-office`（使用 `id` 属性），并绑定到 `192.168.1.0` 网络。该 C 类网络上的每个主机都可以访问此 FTP 服务。但外部服务器（例如互联网上的）无法访问此服务器。

## 重定向和转发

使用端口重定向可以将客户端指向服务器上的不同端口或将其转发到不同的系统。`redirect` 属性可以将客户端重定向或转发到不同的系统或本地系统的不同端口。`redirect` 属性具有以下语法：

```
redirect IP address or hostname port
```

# 第14 章：xinetd 343
