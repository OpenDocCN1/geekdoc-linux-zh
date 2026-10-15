
不幸的是，使用无线波作为媒介是极度不安全的。任何拥有无线以太网设备的人，即使是像 Sharp Zaurus 这样的小设备，都可以坐在你的网络附近。为了实现这一点，你可以购买一个无线基站将无线网络桥接（或连接）到有线网络——这几乎就像通过向一个端口插入另一个集线器或交换机，为集线器或交换机提供了更多端口。无线基站同时包含有线和无线网络硬件；它物理上接入网络，并能与无线网络设备进行无线通信。（你可以让普通电脑承担无线基站的工作，但并不值得）

Linux 还有一个名为 `ifconfig` 的额外工具，用于设置无线网络的的一些技术细节。例如，如果隔邻有人有一个无线网络，你需要用扩展服务标识符 (`ESSID`) 字符串标识符将你的网络与他们的区分开。

要启用 `ifconfig`，你的内核需要无线局域网扩展，你可以在内核配置的网络支持选项中找到它们（见第 10 章）。运行不带参数的 `ifconfig` 会产生如下输出：

```
lo no wireless extensions.
```

```
eth0 no wireless extensions.
```

```
eth1 802.11-DS ESSID:"some net" Nickname:HERMES
Mode:Managed Frequency:2.437GHz Access Point:00:04:5A:CE:BF:17
Bit Rate:11Mbps/s Tx-Power:15dB Sensitivity:1/3
RTS thr:off Fragment thr:off
Power Management:off
Link Quality:44/92 Signal level:-49 dB Noise level:-93 dB
Rx invalid nwid:0 invalid crypt:0 invalid misc:7255
```

如你所见，无线设置是绑定在网络接口上的。最重要的设置如下：

- **ESSID**：网络的字符串标识符。你的无线接入点应该有此设置。

- **Mode (模式)**：定义网络类型以及网络接口在网络中角色的设置。大多数无线网络是管理网络（managed networks），这意味着至少有一个节点作为接入点并监控网络上的节点。你的接口可以作为客户端、主接入点、辅助接入点或中继。然而，也存在没有接入点的自形成网络（ad hoc networks）。

- **Access point (接入点)**：你当前无线接入点的无线接口的 MAC 地址（如果你处于管理网络）。

- **Encryption key (加密密钥)**：无线网卡当前的等效无线隐私 (`WEP`) 密钥。

你可以像使用 `ifconfig` 一样手动设置这些参数：

```
ifconfig eth1 myynet mode managed
```

在前面的示例中，`ifconfig` 配置了 `eth1` 接口，`ESSID` 为 `myynet`，网络拓扑为 `managed`。重要的 `ifconfig` 参数列在表 5-5 中。请查看 `ifconfig(8)` 手页以获取完整的参数列表。

### 表 5-5: ifconfig 参数

| 参数 | 值 |
| --- | --- |
| essid | `ESSID` 字符串，或 `any`。 |
| ap | 接入点的 MAC 地址，或 `any`。 |
| mode | `Managed`（管理）, `Master`（主）, `Repeater`（中继）, `Secondary`（辅助）或 `Auto`（自动）。 |
| channel | 通道号（每个通道都有预定的频率）；运行 `iwlist channel` 获取可用通道列表。 |
| freq | 直接频率规格（例如，2.412 GHz 使用 `2.412G`）。 |
| key | 通常是 `WEP` 密钥的十六进制值，或禁用 `WEP`。 |

对于无线插入的 PC 卡，大多数发行版支持 `/etc/pcmia/wireless.opts` 中的 PC 卡工具。当你将无线卡插入机器时，运行第 11.6 节中来自 `/etc/pcmia/wireless` 的 PC 卡服务守护进程。无线网络根据 `wireless.opts` 中的参数运行 `ifconfig`，这是一个 Bourne case 语句，主要根据你的无线卡的 MAC 地址做出决策。`wireless.opts` 配置文件有许多你应该检查的示例条目。

为 MAC 地址为 `00:02:2D:B0:EE:E4` 的无线卡创建一个条目，可以使用以下内容：

```
*,*,00:02:2D:B0:EE:E4)
INFO="my Home Network"
ESSID="my network"
MODE="Managed"
RATE="auto"
KEY="2688645297";
```

你必须将此条目放在 `wireless.opts` 的 case 语句中，以下行之前：

# NOTE : 删除以下四行以激活下面的示例 ...

# START SECTION TO REMOVE own*,*,*);

# END SECTION TO REMOVE

## 6.1 服务的基础

TCP 服务是最容易理解的服务之一，因为它们是简单的、不间断的数据流。例如，你可以直接与 TCP 端口 80 上的 Web 服务器通信，以了解数据是如何跨越连接的。运行以下命令连接到 Web 服务器：

```
telnet www.nytimes.com 80
```

你应该会得到如下的响应：

```
Trying some address...
Connected to www.nytimes.com.
Escape character is '^'.
```

现在输入以下内容：

```
GET /
```

按两次回车键。服务器将发送一组 HTML 文本作为响应，然后终止连接。

这里有两个重要的教训：

- 远程主机有一个监听在 TCP 端口 80 上的 Web 服务器。

- `telnet` 为发起连接的客户端提供服务。

> 注意：`telnet` 是一个最初设计用于允许登录远程主机的程序。虽然非 Kerberos 的 `telnet` 远程登录是完全不安全的（你稍后会学），但 `telnet` 客户端对于调试远程服务非常有用。`Telnet` 不支持 UDP 或 TCP 以外的任何传输层。有关 `netcat`（一个强大的通用网络客户端）的信息，请参见第 6.5.3 节。

## 6.2 独立服务器

独立网络服务器与系统上的任何其他服务器守护进程（如 `cron`）没有区别，它们它们监听网络端口。事实上，你已经在第 4 章中见过了 `syslog`，如果使用 `-f` 选项启动它，它会在端口 514 上接收 UDP 数据包。

以下是一些你可能在系统中发现运行的其他常见网络服务器：

- `http` Web 服务器

- `lpd` 打印服务器（参见第 12 章）

- `postfix`, `qmail`, `sendmail` 邮件服务器

- `sshd` 安全外壳守护进程（参见第 6.4 节）

- `nfsd`, 挂载的网络文件系统守护进程

- `smbd`, `nmbd` Windows 文件共享守护进程（参见第 14 节）

- `portmap` 远程过程调用 (`RPC`) 端口映射服务守护进程

## 6.3 inetd 守护进程

为每个服务实现独立服务器是非常低效的，因为每个服务器必须完全熟悉网络接口 API，拥有自己的端口配置系统等。在许多方面，与 TCP 通信的 API 与标准 I/O 系统没有太大。TCP 服务器从网络端口读取数据并将输出返回这些端口——这与第 1.2 节中不带参数的 `cat` 命令的行为相似。

`inetd` 守护进程是一个管理器，它规范了网络端口访问，并在程序与网络端口之间建立了接口。启动 `inetd` 后，它会读取 `inetd.conf` 文件并监听该文件中定义的网络端口，为每个传入的连接附加新启动的进程。

`inetd.conf` 中的每一行看起来都像这样：

```
ident stream tcp nowait nobody /usr/sbin/inetd ident -i
```

这里有七个字段：

- **服务名**：来自 `/etc/services` 的服务名（第 5.12 节）。

- **Socket 类型**：对于 TCP 和 UDP 通常是 `stream` 和 `gram`。

- **协议**：传输协议，如 `tcp` 或 `udp`。

- **数据报服务器行为**：对于 UDP，为 `wait` 或 `nowait`。使用任何其他协议的服务应使用 `nowait`。

- **用户**：应该运行该服务的用户名。如果你想设置组，请添加 `.group`。

- **可执行文件**：`inetd` 应该连接到服务的程序。

- **参数**：前一个字段中可执行文件的参数。第一个参数应该是程序名称。

`inetd.conf` 中的 `#` 表示注释。要禁用某个 `inetd` 服务，请在 `/etc/inetd.conf` 中的该条目前放置一个 `#`，然后运行以下命令使其重新读取配置文件：

```
kill -HUP `cat /var/run/inetd.pid`
```
