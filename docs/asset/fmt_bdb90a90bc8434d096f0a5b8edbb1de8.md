
`ntalk` 示例包含了表 10-4 中列出的字段：

| 字段 | 条目描述 |
| --- | --- |
| disable | 使用 Yes 或 No。Yes 会导致服务不启动。 |
| socket_type | 使用 stream, dgram, raw 或 seqpacket |
| wait | 单线程应用程序设置为 Yes，多线程应用程序设置为 No。多线程应用程序会启动多个副本，例如 httpd。 |
| user | 运行服务器的帐户。永远不要使用 root |
| group | 运行服务器的组。 |
| server | 执行的程序。 |

## 第 10 章：系统管理与安全

### 练习 10-2

#### 配置 xinetd

在练习中，我们将使用 `xinetd` 启用 Telnet 服务。使用 `telnet localhost` 命令尝试建立 Telnet 会话。Telnet 在 Red Hat Linux 中默认是禁用的，因此你的尝试应该失败，除非你已经启用了 Telnet。

1. 编辑 `/etc/xinetd.d/telnet` 并将 `Disable` 的值从 `Yes` 改为 `No`。

2. 使用以下命令让 xinetd 重新读取其配置文件：
`kill -SIGUSR1 'cat /var/run/xinetd.pid'`

3. 现在尝试建立一个 Telnet 会话。你应该能够成功。

4. 恢复 Telnet 配置文件中 `Disable` 的值，并再次向 xinetd 发送 `SIGUSR1`。尝试再次使用 Telnet，假设你已经恢复了 `Yes` 设置，你不应该能够再次使用 Telnet。

### tcp_wrappers, /etc/hosts.allow, 和 /etc/hosts.deny

尽管你可以通过在 `/etc/xinetd.conf` 中注释掉或删除未使用的服务来获得某种程度的安全性，但仍然有人可能对你留开启的服务发起攻击。`xinetd` 提供了一种能力，通过其配置文件中的可选字段，或者在 `/etc/hosts.allow` 或 `/etc/hosts.deny` 中指定的配置，将对服务的访问限制到指定的主机或网络。红帽 Linux 通过一种名为 `tcp_wrappers` 的机制实现了这些基于主机或网络的限制，该机制是默认启用的。在启用 `tcp_wrappers` 的情况下，当 `xinetd` 接收到服务的网络请求时，它会将请求传递给 `tcp_wrappers`。`tcp_wrappers` 记录请求，然后检查其访问规则。如果请求来自允许访问你服务器的客户端，`tcp_wrappers` 将启动请求的服务器程序并退出。

`tcp_wrappers` 对客户端是不可见的。它是与应用程序无关的，只有在 `xinetd` 建立会话时活跃——它不会对运行中的应用程序产生任何开销。其他应用程序也可以使用 `tcp_wrappers` 库函数进行构建。对这些应用程序的网络访问随后可以通过 `tcp_wrappers` 配置文件进行控制。

你使用两个文件 `/etc/hosts.allow` 和 `/etc/hosts.deny` 来配置 `tcp_wrappers` 的访问规则。列在 `hosts.allow` 中的客户端被允许访问；列在 `hosts.deny` 中的客户端被拒绝访问。需要记住的一个重要点是，如果客户端在两个文件中都没有列出，则会自动授予该客户端访问权限。当 `tcp_wrappers` 搜索其访问文件时，一旦找到客户端的第一个匹配项就会停止搜索。如果任何一个文件缺失，将被视为空文件；你可以通过删除 `hosts.allow` 和 `hosts.deny` 来关闭访问控制。

搜索顺序如下：

1. `hosts.allow`
2. `hosts.deny`
3. 不匹配 = 允许访问

你在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中使用相同的访问控制语言来告诉 `tcp_wrappers` 允许或拒绝哪些客户端。这两个文件中中的行的基本格式为：

```
daemon_list : client_list
```

例如，这一行：

```
in.telnetd : 192.168.1.5
```

在 `/etc/hosts.allow` 文件中，这一行告诉 `tcp_wrappers` IP 地址为 `192.168.1.5` 的客户端允许 Telnet 登录到你的系统。`/etc/hosts.deny` 中的相同行告诉 `tcp_wrappers` 该客户端不允许 Telnet 登录到你的系统。你可以通过多种不同的方式指定客户端，如表 10-5 所示。

表中列出的 `ALL` 通配符可以代表任何客户端或服务。多个列表可以用逗号分隔。可以使用 `EXCEPT` 运算符对守护进程列表和客户端列表应用限制或例外。以下代码包含一个示例 `hosts.allow` 文件，以展示如何构建列表来控制访问。

| 表 10-5 | 在 /etc/hosts.allow 和 /etc/hosts.deny 中指定客户端的方法 | 备注 |
| :--- | :--- | :--- |
| | .xyz.com | 以点开头。匹配主机名最后部分包含 `xyz.com` 的任何客户端。同时匹配 `us.xyz.com` 和 `server1.engr.xyz.com`。 |
| | 172.16. | 以点结尾。匹配 IP 为 `172.16.x.y` 的任何客户端。 |
| | 172.16.72.0/255.255.254.0 | 带有子网掩码的 IP 网络。匹配 IP 为 `172.16.72` 到 `172.63.255` 的任何客户端。 |
| | ALL | 匹配任何客户端，匹配任何守护进程 |
| | LOCAL | 匹配任何不包含点的客户端主机名。 |

`hosts.allow` 文件中的第一行仅仅是注释。下一行指定任何与本系统处于同一域的客户端或来自 `.afe.dom.com` 的任何客户端都可以连接到任何服务。第三行指定 `192.168.25` 子网上的任何客户端（IP 为 `192.168.25.73` 的客户端除外）都可以 FTP 到此系统。最后一行指定 IP 为 `192.168.1.10` 的客户端可以对此主机进行 `finger` 查询或使用 FTP。随后的代码包含一个 `hosts.deny` 文件，以展示如何构建列表来控制访问。

```
#hosts.deny

ALL EXCEPT in.fingerd : .xyz.com

in.telnetd : ALL EXCEPT 192.168.1.10

ALL:ALL
```

`hosts.deny` 文件的第一行是注释。注释行以符号 (`#`) 开头，可以出现在任何一个文件的任何位置。第二行指定 `.xyz.com` 域的任何客户端不能执行除在主机上运行 `finger` 以外的任何操作。第三行指定 IP 为 `192.168.1.10` 的客户端允许 Telnet 登录到主机。最后一行指定任何不匹配单个规则的其它客户端将被拒绝访问由 `tcp_wrappers` 控制的所有服务。

`tcp_wrappers` 访问控制语言还允许你为给定的客户端列表指定要执行的 shell 命令。这些规则可以使用多种扩展模式。此类规则的格式如下：当你将这些内容作为 shell 命令的一部分包含时，它们将在命令运行之前被展开。这些中最有趣的是 `twist` 运算符。在 `hosts.deny` 中使用该运算符的示例所示：

```
in.telnetd : .hack.org : twist /bin/echo access denied
```
