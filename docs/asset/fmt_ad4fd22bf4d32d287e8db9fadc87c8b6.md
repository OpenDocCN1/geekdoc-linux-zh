
`rlogin` `[-l username] host`

```
rlogin 命令允许您远程登录到主机。例如，要登录名为 shell.myhost.com 的主机，请运行
```

```
rlogin shell.myhost.com
```

由于 `rlogin` 不被认为安全，我建议您仅在封闭的局域网环境中使用它。`-l` 选项允许您指定用于身份验证的用户名。如果您想在不输入密码的情况下远程登录主机，请在用户主目录中创建 `.rhosts` 文件。添加您将用于发出 `rlogin` 请求的计算机的主机名或 IP 地址。再次强调，由于许多人认为这是一种安全风险，我不建议广泛使用 `rlogin`。

### talk

语法：

```
talk username tty
```

如果您需要向另一用户发送消息，电子邮件效果很好。但是，如果您需要与另一用户实时通信，类似于电话交谈，请使用 `talk` 命令。要与已登录的另一用户交谈，请使用以下命令：`talk ronak@csus.edu` 您请求的 user 必须接受您的 `talk` 请求。用户接受您的 `talk` 请求后，您可以开始互相交谈（输入）。`talk` 程序在任一方执行 Ctrl+C（intr 键）时终止。

### telnet

语法：

```
telnet hostname or IP address [port]
```

这是默认的 Telnet 客户端程序。您可以使用此程序连接到 Telnet 服务器。例如，如果指定主机运行 Telnet 服务器，以下命令将打开到 shell.myportal.com 系统的 Telnet 连接：

```
telnet shell.myportal.com
```

连接打开后，您将被提示输入用户名和密码。登录成功后，您可以访问 Telnet 服务器上的本地用户账户。

### wall

语法：

```
wall
```

`wall` 命令允许您向所有用户的终端发送文本消息，只要他们未通过 `mesg` 命令禁用其 tty 的写访问权限。输入 `wall` 后，您可以输入单行或多行消息，然后按 Ctrl+D 发送。

## 网络管理员命令

本节讨论的命令使您能够收集有关网络服务和网络本身的信息。

### host

语法：

```
host [-a] host IP address
```

默认情况下，`host` 程序允许您快速检查主机 IP 地址。如果使用 `-a` 选项，`host` 会返回有关指定主机或 IP 地址的各种 DNS 信息。

### hostname

语法：

```
hostname
```

此程序显示系统的主机名。

### ifconfig

语法：

```
ifconfig [interface] [up | down] [netmask mask]
```

`ifconfig` 程序允许您配置网络接口。您也可以使用此程序查看接口的状态。例如，如果您之前已为 Red Hat Linux 系统配置了网络，并且有一个预配置的网络接口设备 `eth0`，您可以运行以下命令：

```
ifconfig eth0
```

您应该会看到类似以下内容的输出：

```
eth0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37

inet addr:206.171.50.50 Bcast:206.171.50.63

Mask:255.255.255.240

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:9470 errors:0 dropped:0 overruns:0 frame:0

TX packets:7578 errors:0 overruns:0 carrier:0

collisions:0

Interrupt:5 Base address:0x340
```

这里，`ifconfig` 报告网络接口设备 `eth0` 具有 Internet 地址（inet addr）206.171.50.50、广播地址（Bcast）206.171.50.63 和网络掩码（255.255.255.240）。其余信息显示该接口迄今为止接收了多少数据包（RX packets）、发送了多少数据包（TX packets）、迄今为止发生了多少种不同类型的错误、该设备使用什么中断地址线、使用什么 I/O 地址基址等等。

你可以在不带任何参数的情况下运行 `ifconfig`，以获取所有已启动的网络设备的完整列表。

你可以使用 `ifconfig` 启动接口。例如，以下命令使用 IP 地址 206.171.50.50 启动 `eth0`：

```
ifconfig eth0 206.171.50.50 netmask 255.255.255.240 \ broadcast 206.171.50.63
```

你也可以使用 `ifconfig` 命令快速关闭接口。例如，以下命令关闭 `eth0` 接口：

```
ifconfig eth0 down
```

## netcfg

请参阅第 7 章中关于使用 `netcfg` 配置网络接口卡的部分。

## netstat

语法：

```
netstat [-r] [-a] [-c] [-i] [-n]
```

`netstat` 程序显示本地系统进出网络连接的状态。例如，以下命令显示本地系统上的所有网络连接：

```
netstat -a
```

要显示路由表，请使用 `-r` 选项。要持续显示网络连接状态，请使用 `-c` 选项。要显示所有网络接口的信息，请使用 `-i` 选项。要显示数字 IP 地址，请使用 `-n` 选项。

## nslookup

语法：

```
nslookup [-query=DNS record type] [hostname or IP] [name server]
```

`nslookup` 命令使你能够执行 DNS 查询。你可以选择以交互方式查询 DNS 服务器，或立即查找信息。例如，

```
nslookup -query=mx integrationlogic.com
```

立即返回 `integrationlogic.com` 域的 MX 记录。

以下命令执行相同的操作，但不是使用 `/etc/resolv.conf` 文件中指定的默认名称服务器，而是使用 `ns.nitec.com` 作为名称服务器：

```
nslookup -query=mx integrationlogic.com ns.nitec.com
```

你也可以使用 `-q` 代替 `-query`。例如，以下命令返回命名主机名的 IP 地址（地址记录）：

```
nslookup -q=a www.formtrack.com
```

你也可以以交互模式运行 `nslookup`。只需不带任何参数运行命令，即可看到 `nslookup` 提示符。在 `nslookup` 提示符下，输入 `?` 可获取帮助。如果你计划同时执行多个 DNS 查询，交互模式会非常有帮助。例如，要查询多个域（如 `ad-engine.com` 和 `classifiedworks.com`）的 NS 记录，只需输入以下命令：

```
set query=ns
```

设置查询类型为 `ns` 后，输入 `ad-engine.com` 并等待回复；收到回复后，尝试下一个域名；以此类推。如果你想在 `nslookup` 提示符下更改名称服务器，请使用 `server` 命令。例如，

```
server ns.ad-engine.com
```

使 `nslookup` 使用 `ns.ad-engine.com` 作为名称服务器。要退出交互模式并返回 shell 提示符，请在 `nslookup` 提示符下输入 `exit`。

## ping

语法：

```
ping [-c count] [-s packet size] [-I interface]
```

这是网络管理员最广泛使用的程序之一，`ping` 用于检查远程计算机是否可以通过 TCP/IP 协议访问。技术上，该程序向远程主机发送 Internet 控制消息协议（ICMP）回显请求。由于协议要求对回显请求作出响应，远程主机必须发送回显响应。这使 `ping` 程序能够计算将数据包发送到远程主机所需的时间。例如，

```
ping blackhole.nitec.com
```

会持续向 `blackhole.nitec.com` 主机发送 ping 消息。要停止 `ping` 程序，请按 Ctrl+C，这会导致程序显示一组统计信息。以下是前述命令生成的 ping 请求输出示例：

```
PING blackhole.nitec.com (209.63.178.15): 56 data bytes

64 bytes from 209.63.178.15: icmp_seq=0 ttl=53 time=141.5 ms

64 bytes from 209.63.178.15: icmp_seq=1 ttl=53 time=162.6 ms

64 bytes from 209.63.178.15: icmp_seq=2 ttl=53 time=121.4 ms
```
