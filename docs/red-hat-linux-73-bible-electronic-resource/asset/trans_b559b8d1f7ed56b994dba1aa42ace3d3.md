
# 按原样使用 PortSentry

与 **Logcheck** 一样，**PortSentry** 安装后无需任何额外操作即可正常工作。默认情况下，安装 *portsentry* 软件包时，**PortSentry** 的行为如下：

- */etc/init.d/portsentry* 启动脚本在系统启动至运行级别 3、4 或 5 时自动运行（级别 3 和 5 使用最为常见）。
- 在基本模式下，**PortSentry** 配置为监控以下端口号：
    - **TCP：** 1, 11, 15, 143, 540, 635, 1080, 1524, 2000, 5742, 6667, 12345, 12346, 20034, 31337, 32771, 32772, 32773, 32774, 40421, 49724, 54320
    - **UDP：** 1, 513, 635, 640, 641, 700, 32770, 32771, 32772, 32773, 32774, 31337, 54321
- 针对攻击（表现为对受监控端口的扫描），任何后续试图连接该协议（**TCP** 或 **UDP**）任何服务的尝试都将被阻止。

被阻止访问您系统的计算机将列在 *portsentry.blocked.tcp* 或 *portsentry.blocked.udp* 文件（位于 */var/portsentry* 目录）中，具体取决于被扫描的协议（**TCP** 或 **UDP**）。从这些文件中删除条目可以恢复被阻止计算机的访问权限。

# 配置 PortSentry

您可能需要修改 **PortSentry** 的运行方式。要更改 **PortSentry** 的行为，请修改 */etc/portsentry/portsentry.conf* 文件。在该文件中，您可以选择要监控的端口、监控模式以及检测到扫描时采取的措施。这些措施包括：

- 阻止远程计算机的访问
- 将来自远程计算机的消息重定向到一个无效主机
- 添加一条防火墙规则以丢弃来自远程计算机的数据包

您可能需要修改的另一个文件是 */etc/portsentry/portsentry.modes*。*portsentry.modes* 文件仅包含 **PortSentry** 可以运行的模式。

## 修改 portsentry.conf 文件

要编辑 portsentry.conf 文件，请以 root 用户身份使用任意文本编辑器打开 /etc/portsentry/portsentry.conf 文件。以下部分介绍了该文件中可以修改的信息。

## 选择端口

portsentry.conf 文件定义了基本模式和隐匿模式下监控哪些端口。默认情况下，只有基本的 TCP 和 UDP 模式处于激活状态，因此只监控这些端口（除非您切换到其中一种隐匿模式）。TCP_PORTS 和 UDP_PORTS 选项定义了要监控的端口。它们在 portsentry.conf 文件中的显示方式如下：

```
TCP_PORTS="1,11,15, 143,540,635,1080,1524,2000,5742,6667,12345,12346,20034, 31337, 32771,32772,32773,32774, 40421, 49724, 54320"
UDP_PORTS="1,513, 635, 640,641, 700, 32770,32771, 32772,32773,31337, 54321"
```

除非您是 TCP/IP 专家，否则您可能正在思考这些端口代表哪些服务。互联网号码分配机构（IANA）为 UDP 和 TCP 端口分配服务。您可以在以下网址查看这些分配：

`www.iana.org/assignments/port-numbers`

Red Hat Linux（以及其他 Linux/UNIX 系统）中的网络服务从 /etc/services 文件获取端口号分配。因此，通常只需检查 /etc/services 文件即可找到大多数被分配给被扫描端口的服务。

用于监控的端口是根据几个不同标准选择的。低端口号（1、11、15 等）被选中，以捕获从端口 1 开始扫描数百个端口的端口扫描器。如果扫描器在访问端口 1 后被阻止，它将无法获取有关计算机上可能开放的其他端口的信息。另一个标准是包含入侵者专门检查的端口，因为这些服务可能存在漏洞，易受攻击。其中包括 systat（端口 11）和 netstat（端口 15）服务。

如果您实际上正在运行分配给某个端口的服务，您可能需要从 portsentry.conf 文件中的列表中移除该端口。另一方面，如果您担心攻击并想要更多的覆盖范围，可能希望向列表中添加端口。portsentry.conf 文件包含一些示例，您可以取消注释（删除 # 符号）以监控更多的端口。

如果您从基本扫描更改为隐匿扫描（如本章稍后“修改 portsentry.modes 文件”部分所述），则监控的端口将由 ADVANCED_PORTS_TCP 和 ADVANCED_PORTS_UDP 选项定义。这两个选项的默认设置如下：

```
ADVANCED_PORTS_TCP="1023"
ADVANCED_PORTS_UDP="1023"
```

上述两项条目表示监控从 1 到 1023 的所有端口。监控较高的端口号可能导致更多的误报，因此不建议这样做。如果您发现 PortSentry 经常被意外触发，您可能希望使用 `ADVANCED_EXCLUDE_TCP` 和 `ADVANCED_EXCLUDE_UDP` 选项来排除被触发的端口。以下示例展示了这两个值的默认设置：

```
ADVANCED_EXCLUDE_TCP="111,113,139"
ADVANCED_EXCLUDE_UDP="520,138,137,67"
```

默认情况下，TCP 的 `ident` 和 NetBIOS 服务（端口 111、113 和 139）以及 UDP 的路由、NetBIOS 和 Bootp 广播（端口 520、138、137 和 67）被排除在高级扫描之外。（排除的原因是远程计算机可能会访问这些端口，而不代表任何误用。）如果您正在运行隐匿模式，也应该通过将这些服务的端口号添加到列表中，来排除您在系统上运行的任何服务。

## 识别配置文件

除了 `portsentry.conf` 文件外，PortSentry 还使用几个其他配置文件。您可以在 `portsentry.conf` 文件中找到这些文件的位置。这些文件的定义方式如下：

```
# Hosts to ignore
IGNORE_FILE="/etc/portsentry/portsentry.ignore"
# Hosts that have been denied (running history)
HISTORY_FILE="/var/portsentry/portsentry.history"
# Hosts that have been denied this session only (temporary until next restart)
BLOCKED_FILE="/var/portsentry/portsentry.blocked"
```

您可能不想移动这些配置文件的位置。以下是这些文件用途的一些说明：

- `portsentry.ignore` 文件包含您不希望被阻止的所有 IP 地址列表（即使它们试图不当访问您计算机上的端口）。默认情况下，分配给本地计算机的所有 IP 地址都会添加到该文件中。如有需要，您可以添加受信任计算机的 IP 地址。
- `portsentry.history` 文件包含已被阻止访问您计算机的计算机的 IP 地址列表。
- `portsentry.blocked.*` 文件包含在当前会话期间已被阻止访问您计算机的计算机列表。`portsentry.blocked.tcp` 文件包含不当扫描您计算机 TCP 端口的计算机的 IP 地址。扫描 UDP 端口后被阻止的计算机的地址包含在 `portsentry.blocked.udp` 文件中。

对您计算机端口的访问仅在当前会话期间被阻止（即，直到下次重启或重启 PortSentry 为止）。因此，为了更永久地排除远程计算机，您应该施加其他限制（例如使用 /etc/hosts.deny 文件、防火墙命令或重定向到无效主机）。这些方法将在本章稍后描述。

## 选择响应措施

扫描端口的人就像检查您家中的门是否锁好一样。在大多数情况下，这表明有人在检查您的系统是否存在弱点。因此，当另一台计算机扫描您的端口时，PortSentry 的默认响应是阻止该计算机在当前会话期间进一步访问您的计算机。不会采取永久阻止该计算机访问的措施。portsentry.conf 文件中的 BLOCK_UDP 和 BLOCK_TCP 选项设置端口被扫描时采取的自动响应类型。这些选项的默认设置如下：

```
BLOCK_UDP="2"
BLOCK_TCP="2"
```

引号内的值决定了 PortSentry 如何反应另一台计算机对您的端口的扫描。以下列表描述了这些值的含义。

- 值为 "2"（默认值）会导致对已扫描协议（TCP 或 UDP）的服务的访问被临时阻止，并且该操作会被记录日志。此外，如果定义了由 KILL_RUN_CMD 选项运行的命令，则随后将运行该命令。（此选项默认未配置。）
- 值为 "0" 会导致记录端口扫描日志，但不会阻止。
- 值为 "1" 会导致运行 KILL_ROUTE 和 KILL_HOSTS_DENY 选项。（有关这些选项的说明，请参阅以下列表。）默认情况下，来自远程计算机的后续请求将被重定向到无效主机，并且远程主机的 IP 地址将被添加到 /etc/hosts.deny 文件中，从而拒绝访问网络服务。

以下是关于您可以使用哪些选项来更改对端口扫描的响应的一些建议：

- **KILL_ROUTE**：此选项运行 /sbin/route 命令，将来自远程计算机的请求重定向到无效主机。默认情况下，此选项设置为以下值，有效地丢弃来自远程计算机的请求：

```
KILL_ROUTE="/sbin/route add -host $TARGETS gw 127.0.0.1"
```

> **注意：** 除了重定向来自远程主机的 IP 数据包外，您还可以使用防火墙规则来拒绝访问。如果您使用 ipchains 防火墙，请取消注释以下行以拒绝来自远程主机的访问：
>
> ```
> KILL_ROUTE="/sbin/ipchains -I input -s $TARGETS -j DENY -i"
> ```

