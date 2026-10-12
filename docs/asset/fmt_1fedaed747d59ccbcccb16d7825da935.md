
`gopher` `70/udp` `timserver`

```
uucic -l
```

```
#ftftp dgram udp wait root /usr/sbin/tcp in.tftpd

#bootps dgram udp wait root /usr/sbin/tcp bootpd

#cfinger stream tcp nowait root /usr/sbin/tcp in.cfigner

#systat tcp nowait guest /usr/sbin/tcp /bin/ps -auwxx

#netstat tcp nowait guest /usr/sbin/tcp /bin/netstat -f inet

#swat stream tcp nowait.400 root /usr/sbin/swat swat
```

`inetd` 文件中的注释以井号（`#`）开头。要启用某服务，请在对应条目的开头插入井号；要禁用该服务，请移除井号。例如，通过移除 `bootsps` 开头的 `#` 号来启用 BootP 服务器。同样，在 `finger` 条目的第一个字符前插入 `#` 号即可禁用 finger 协议。这将让你对 Linux 系统提供的服务拥有完全控制。

禁用未使用的服务是服务器安全的重要部分。不要运行你不需要的服务。每项服务都是黑客可能渗透的潜在漏洞。在我们的服务器上，我们提供了 `ftp`。显然，它不应该在示例配置中被注释掉。但我们的服务器并不提供 `gopher` 或 `pop-3` 服务。这些服务可以被注释掉而不会影响这台虚拟服务器的用户。在另一台服务器上，角色可能会反过来：`POP` 可能被启用，而 `FTP` 可能被禁用。启用哪些服务取决于服务器将提供哪些服务。

将控制网络服务的访问作为整体系统安全组成部分非常重要，这也是创建 `inetd` 的主要原因。扩展互联网服务守护进程（`xinetd`）执行与 `inetd` 相同的任务，但它提供了增强的安全特性。

### 配置 xinetd

`inetd` 的替代方案是扩展互联网服务守护进程（`xinetd`）。`xinetd` 在 `/etc/xinetd.conf` 中配置，它提供了与 `inetd.conf` 相同的信息。但 `xinetd` 不使用由其配置行相对位置决定的名称（位置参数，而是使用`属性-值对`。属性名能够清晰地标识每个参数的用途，值则用于配置该属性。例如，`inetd.conf` 中的第三字段包含传输协议的名称。在 `xinetd` 中，传输协议是通过 `protocol` 属性定义的，例如 `protocol = tcp`。`xinetd` 的功能比 `inetd` 多得多，因此配置 `xinetd` 的属性比 `inetd` 使用的七个位置参数更多。理解各种 `xinetd` 属性的最佳方法是查看一些真实的配置。列表 3.5 是 Red Hat 7.2 系统的 `xinetd.conf` 文件。

列表 3.5：`/etc/xinetd.conf`

```
$ cat /etc
```

`xinetd` 的简单配置文件

```
# 一些默认值并包含 /etc/xinetd.d/

defaults
{
  instances = 60
  log_type = SYSLOG authpriv
  log_on_success = HOST PID
  log_on_failure = 
)
cps = 25 30
includedir /etc/xinetd.d
```

以 `#` 开头的行是注释。`defaults` 语句是该文件的第一个条目。`defaults` 是可选的，但如果使用它，配置中只能出现一个 `defaults` 语句。使用此语句为各种属性设置默认值。将属性/值对列表包含在大括号中（属性/值对列表始终包含在大括号中）。列表 3.5 中的中的 `xinetd.conf` 文件定义了五个属性的默认值：

- `instances`：指定同时运行的某种类型服务的守护进程的最大数量。列表 3.5 将 `instances` 设置为 60，这意味着任何时候运行的 telnet 进程不会超过 60 个。即使从网络收到额外的 Telnet 服务请求，`xinetd` 也不会启动第 61 个实例。`instances` 的系统默认值允许所有类型的服务拥有无限数量的并发进程。`instances` 设置数值或关键字 `UNLIMITED`。

- `log_type`：定义日志记录的位置。该属性有两个可能的值：
    - `FILE pathname [soft_limit [hard_limit]]`：`FILE` 设置告诉 `xinetd` 将活动记录到由 `pathname` 标识的文件中。文件大小的上限使用 `soft_limit` 和 `hard_limit` 设置。当超过 `soft_limit` 时，`xinetd` 会发出有关文件的警告。当超过 `hard_limit` 时，`xinetd` 将停止向该文件记录消息。默认是对文件大小没有限制。
    - `SYSLOG syslog_facility [syslog_level]`：`SYSLOG` 设置告诉 `xinetd` 使用 `syslog` 守护进程记录活动。`syslog_facility` 必须是 `/etc/syslog.conf` 中定义的设施之一。如果使用 `syslog_level`，它必须是标准的 `syslog` 严重性值。参见列表 3.5 中的示例，告诉 `xinetd` 通过 `syslog` 记录活动并使用该设施。

- `log_on_success`：定义当成功连接到本地服务时记录的信息。列表 3.5 中的 `xinetd.conf` 文件记录了远程客户端的地址（HOST）和启动的守护进程进程 ID（PID）。还有其他几个可以记录的值。正确配置 `xinetd` 以记录网络活动将在第 12 章中介绍。

- `log_on_failure`：定义当尝试连接本地服务失败时记录的信息。列表 3.5 中的 `xinetd.conf` 文件记录了连接失败时的信息。正确配置 `xinetd` 以记录网络活动将在第 12 章。

- `cps`：定义每秒允许的连接数。如果超过此限制，`xinetd` 将停止接受该端口的连接。

在第 12 章中再次出现。

`log_on_failure` 定义了当尝试连接到 FTP 服务失败时记录的信息。同样，使用了 `+=` 语法将此处定义的数值添加到 `xinetd.conf` 文件默认语句中之前为 `log_on_failure` 定义的值上（参见列出列表 3.5）。这些设置会使 `xinetd` 记录客户端的地址以及登录失败的用户名。`xinetd` 的日志记录将在第 12 章中再次介绍。

`nice` 定义了 `xinetd` 在启动服务器程序时使用的 Nice 值。`nice` 命令设置了服务器程序的调度优先级。`nice` 命令以及许多其他系统管理工具已在 Vicki Stanfield 和 Rod Smith 编写的《Linux System Administration》（Sybase, 2001）书中有所介绍。

`disable` 告知该服务是否已被系统管理员禁用。如果将 `disable` 设置为 `no`，则启用该服务，当 `xinetd` 在此服务器的端口上接收到连接请求运行时运行服务。如果将 `disable` 设置为 `yes`，则该服务被禁用，`xinetd` 不会响应连接请求启动服务。默认情况下，如果配置中未包含该属性，则服务是启用的。

最后一个属性表明，系统管理员可以通过更改 `disable` 属性的值来控制 `xinetd` 启动的服务。这可以通过直接编辑 `xinetd.d` 目录下的配置文件来实现，但红帽（Red Hat）提供了一种简单的方法。第 2 章中用于控制启动脚本的 `chconfig` 命令也可以用于控制 `xinetd` 启动的服务。

列出列表 3.7：使用 `chconfig` 控制 `xinetd`

```
[root] # chconfig --list wu-ftpd
wu-ftpd	onton

[root] # grep disable /etc/xinetd.d/wu-ftpd
    disable = no

[root] # chconfig wu-ftpd off
[root] # chconfig --list wu-ftpd
wu-ftpd

off

[root] # grep disable /etc/xinetd.d/wu-ftpd
    disable = yes
```
