
`service`、`socket_type`、`wait`、`user` 和 `server` 值均与 `inetd.conf` 中的值对应，不同之处 `server` 参数提供的路径没有调用 `tcpd` 封装程序。不使用封装程序是因为 `xinetd` 自身就提供了与 `wrapper` 类似的功能。

`xinetd` 提供了自身的日志记录和访问控制。尽管 `xinetd` 不调用 `tcpd`，但它除了 `xinetd.conf` 中定义的访问控制外，还会处理 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。这意味着为其他程序（如 `portmapper`）创建的 `hosts.allow` 和 `hosts.deny` 文件也可以为 `xinetd` 提供引导指导。

列表 12.2 中的 `log_on_success` 和 `log_on_failure` 行在连接成功或连接尝试失败时，会将远程用户的用户 ID 写入标准日志。`log_on_success` 行还会记录处理此次运行的服务器所持续的时间长度（`DURATION` 仅适用于 `log_on_success`）。`+=` 语法意味着为 `log_on_success` 和 `log_on_failure` 定义的值将加到已记录的其他值上。除了记录连接持续时间和远程用户的用户 ID 外，`log_on_success` 和 `log_on_failure` 还允许你记录以下内容：

-   `HOST` 远程主机的地址。与 `USERID` 类似，此值可同时用于成功和失败。
-   `PID` 启动处理连接的服务器的进程 ID。`PID` 仅适用于 `log_on_success`。
-   `EXIT` 连接终止时服务器的退出状态。`EXIT` 仅适用于 `log_on_failure`。
-   `ATTEMPT` 记录失败的连接尝试。`ATTEMPT` 仅适用于 `log_on_failure`。
-   `RECORD` 记录从远程服务器接收的连接信息。`RECORD` 仅适用于 `log_on_failure`。

列表 12.2 中的 `disable = no` 行意味着此服务已启用。要防止此服务运行，请将 `disable` 设置为 `yes`。如前所述，Red 允许你通过 `config` 命令设置 `disable` 参数。除了控制服务是否可用，`xinetd` 还提供了更细粒度的访问控制。`xinetd` 提供了三个访问控制属性：配置为接受来自某些主机的连接（类似于 `hosts.allow` 文件）；拒绝来自某些主机的连接（类似于 `hosts.deny` 文件）；以及仅在每天的特定时间接受连接。这些属性描述如下：

`only_from`: 此属性识别允许连接到服务的主机。可以使用数值地址定义主机。例如，`172.16.12.5` 定义一个特定主机，`172.16.12.0` 定义所有具有地址范围的主机。例如，`172.16.12.[3,6,8,23]` 定义四个不同的主机。网络名称必须在 `/etc/networks` 文件中定义。远程系统提供的 IP 地址映射到此规范主机名（canonical hostname）。域名名也可以定义主机，例如，`172.16.12.0`。主机名返回的反向查询（reverse lookup）必须在指定的域名内。注意，当使用域名时，它以关联的 IP 地址和掩码开头，例如，`172.16.12/25`。

`no_access`: 此属性定义拒绝访问服务的主机。定义主机的方法与之前描述 `only_from` 属性的方法相同。

`access_times`: 此属性定义服务可用的时间，使用的格式为 `hour:min`。小时范围为 0 到 23，分钟为 0 到 59。如果既没有指定 `only_from` 也没有指定 `no_access`，则允许所有人访问。如果两者都指定了，则应用精确匹配——例如：

```
no_access          = 172.16.12.255
only_from          = 172.16.12.0
```

示例中的 `only_from` 命令允许网络 `172.16.12.0` 上的所有系统访问服务。`no_access` 命令取消了该系统的访问。无论 `no_access` 属性是在 `only_from` 属性之前还是之后，工作方式都是相同的，因为精确匹配优先。列表 12.3 显示了带有某些访问控制的示例 Red 系统的 `/etc/xinetd.d/imap` 条目。

`tcpd` 封装可以保护由 `inetd` 或服务（如 `portmapper`）的服务。`hosts.allow` 和 `hosts.deny` 可以保护它启动的服务。其他服务（如 `dhcpcd`）在启动时启动。要控制由启动脚本启动且不读取 `tcpd` 配置文件的服务的访问，请使用 Linux IP 防火墙。

## 使用 iptables 控制访问

每个人都认为自己了解防火墙，直到涉及到细节。从大上来说，防火墙是一个保护本地网络免受全球网络攻击的系统。它是网络流量在进入或离开本地网络之前经过的哨兵。在最简单的情况下，防火墙是一个过滤不需要流量的路由器；而在最复杂的情况下，它是包含多个路由器和多个服务器的整个网络。

Linux 提供了创建简单防火墙所需的流量过滤工具。将 Linux 的功能与 `iptables` 的过滤功能相结合可以创建一个路由器。此外，更常见的是使用 `iptables` 过滤到达 Linux 服务器网卡的流量，这让 Linux 能够在服务器内部构建防火墙，为所有可能的网络服务提供访问控制。

## 使用 iptables 防火墙规则

Linux 内核将流量分为三组，并对每类流量应用不同的过滤规则：

-   **输入防火墙 (Input firewall)**：入站流量在接受之前通过输入防火墙规则测试。
-   **输出防火墙 (Output firewall)**：出站流量在发送之前通过输出防火墙规则测试。
-   **转发防火墙 (Forwarding firewall)**：通过 Linux 系统的转发流量通过转发防火墙规则测试。

### 列表 12.3: xinetd.conf 访问控制

```
# default: off
# description: IMAP 服务允许远程用户使用 IMAP
#              客户端（如 Mutt, fetchmail 或
#              Netscape Communicator）访问。
service imap
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/imap
    log_on_success += DURATION USERID
    log_on_failure += USERID
    disable         = no
    only_from       = 172.16.12.0
    no_access       = 172.16.12.231
    server          = /usr/sbin/in_logind
```
