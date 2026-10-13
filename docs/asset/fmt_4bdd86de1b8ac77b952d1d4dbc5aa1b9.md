
在 8.4 中，第 7 行显示了与 ppp 示例中使用的相同的参数。第 8 行是为了不打扰朋友和家人而使用的 chat 程序，让它在三分钟内完成 ppp 会话。第 17 行是指定启动和停止 ppp 的场景。第 18 行是用于监控 PPP 会话的特殊图形化程序。`dial` 在后台运行。你必须以 root 用户身份启动它。在 `dial` 设置完成后，你可以测试它们。当 `dial` 检测到需要连接 PPP 服务器的网络条件时，它会启动 `chat` 程序建立 PPP 会话。你可以创建一个启动脚本将其放入 Linux 的 `/etc/rc.d` 区域，以便在启动时自动运行。每当程序需要通过 IP 访问远程主机（例如 `fetchmail`），`dial` 就会介入并启动 PPP 会话。

## kppp 程序

如果你使用的是带有 KDE 桌面环境（KDE）窗口器的 Linux，你可以使用另一种方法来简化 PPP 连接。`kppp` 程序是一个帮助你配置和启动 `pppp` 程序的图形化界面。图 8.8 显示了启动程序时出现的主界面。

![](img/4af9afea53463095baf6057b1f7b908_238_0.png)

图 8.8 kppp 程序主界面

从主界面，你可以选择配置好的 PPP 主机，通过输入密码并点击 Connect 按钮启动 ppp 连接。点击主界面上的 Setup 按钮会启动 kppp 配置界面。可以通过使用配置界面上的 Accounts 标签卡预配置多个账户。图 8.9 显示了 Accounts 标签卡。

![](img/4af9afea53463095baf6057b1f7b908_239_0.png)

图 8.9 kppp Accounts 配置标签卡

可以通过点击 New 按钮配置单个账户，如图 8.10 所示。

![](img/4af9afea53463095baf6057b1f7b908_239_1.png)

图 8.10 kppp 账户设置界面。新账户的每个属性都可以在 Edit Account 界面配置。你可以输入启动 PPP 会话所需的电话号码和身份验证方法。

已为账户配置好。说到账户，还有一个实用的计费功能，它可以记录你的总会话时间并生成一份格式良好的报告，显示特定月份内的所有连接时间。

![](img/4af9afea53463095bafc6057b1f7b908_241_0.png)

**图 8.12**
ppp Modem 配置页。

## Linux 服务器 PPP 实现

用于作为客户端连接到 PPP 服务器的相同 `pppd` 程序也可以用作 `pppd` 服务器。参考列表 8.2 中的第 10 行；客户端在 PPP 服务器上运行 `pppd` 命令来启动 PPP 会话。除了手动运行 `pppd` 之外，还创建了程序允许 Linux 服务器在拨号线上检测到 PPP 请求时自动运行 `pppd`。本节还讨论了配合 `ppd` 使用 `mget+sendfax` 程序的好处。

## pppd 服务器参数

某些 `pppd` 选项允许 `pppd` 程序以服务器模式运行。尽管 PPP 是点对点协议，但连接端之一充当服务器，等待从客户端计算机建立 PPP 连接。接下来的段落将讨论服务器端使用的一些选项。

`passive` 和 `silent` 选项用于允许 `pppd` 程序等待 LCP Configure-Request 数据包以启动 PPP 会话。

`proxy` 选项允许 PPP 主机代表 PPP 客户端响应本地网络上的 ARP 请求。这允许其他计算机连接到 PPP 客户端。

## 邮件服务与 Linux Linux

> 注意

`proxyarp` 选项允许其他计算机连接到 PPP 客户端。当你与 ISP 建立 PPP 连接时，你的 Linux 服务器将成为 ISP 网络上的一个网络设备，面临同样的危险。我强烈建议使用防火墙软件控制外部客户端对 Linux 服务器的访问。如果 PPP 连接上没有使用防火墙软件，应极其小心。请留意系统日志中无效的访问尝试。

`Local_IP:Remote_IP` 选项允许 `pppp` 为远程设备分配 IP 地址。`Local_IP` 是 PPP 主机的地址，而 `Remote_IP` 地址是将将分配给远程 PPP 客户端的地址。

与其为 `pppp` 使用命令行选项，你也可以将选项放在配置文件中。默认情况下，`pppd` 会检查 `/etc/ppp/options` 以获取使用的选项列表。另一个实用的功能是，`pppd` 程序还会根据其初始化的 tty 线路检查其他选项。如果你在 tty 线路 `tty0`、`tty1` 和 `tty2` 上有三种模式，请使用 `/etc/ppp/options.ttyS1` 和 `/etc/ppp/options.ttyS2`。每个选项文件将指定一个不同的 `Local_IP:Remote_IP` 对。这样，多个 PPP 客户端就不会被意外分配重复的 IP 地址。

## mget+sendfax 程序

如果你想让 Linux 服务器充当 PPP 服务器并能够监听客户端连接，`mget+sendfax` 程序是一个非常棒的工具。大多数 Linux 发行版都带了此程序的二进制包。如果你的 Linux 发行版没有包含它，你可以在 `sunite.unc` 的 `/pub/Linux/system/serial` 目录下找到它。`mget+sendfax` 由 Gert Doering 编写。

通常，Linux 使用 `getty` 程序处理串口线的登录尝试。当串口线检测到连接时，它使用 `login` 程序来验证输入的用户名。`mget+sendfax` 程序包含一个新程序 `mget`，它取代了串口的标准 `getty` 程序。`mget` 通过自动检测入电类型和使用锁文件，比 `getty` 更具灵活性。

`mget` 程序同时使用命令行选项和配置文件来控制其运行方式。控制串口程序的 Linux 文件是 `/etc/inittab` 文件。Linux 服务器的每一行在 `/etc/inittab` 文件中都有其自己的终端行。允许 `mgetty` 监控串口的 `inittab` 文件条目所示：

```
# 为调制调器设置串口线

s:12345:respawn:/sbin/mgetty -D -s 38400 -n 4 ttyS
```

使用冒号分隔不同的参数。第一个参数是终端线的唯一标识符。第二个参数表示哪个 init 级别将处于激活。这允许线路在 init 级别 1 到 5 处于激活状态。第三个参数用于指示 init 程序如何处理该线路。`respawn` 关键字告诉它在指定的级别启动程序，并在每次程序终止时重启它。这允许调制调器在客户端断开连接后循环使用。第四个参数是它将产生监控终端线的程序。`mgetty` 命令的格式为：

```
mgetty [options] ttydevice
```

其中 `[options]` 是控制调制调器线路行为的 `mgetty` 选项，`ttydevice` 是 `mgetty` 将监控的 Linux 行。表 8.6 显示了 `mgetty` 可用的选项。

## 表 8.6 mgetty 命令行选项

| 选项 | 说明 |
| - | - |
| -x LEVEL | 将调试级别设置为 LEVEL |
| -s SPEED | 将线路速率设置为 SPEED |
| -a | 尝试自动检测调制调器 |
| -k SPACE | 设置千字节数 |
| -m 'issue' | 指定登录信息 |
| -r | 设置铃声次数 |
| -p PROMPT | 指定提示符 |
| -D | 锁定调制调器 |
| -F | 启用传真 |
| -R | 设置铃声次数 |
| -i 'issue' | 指定问题信息 |
| -S 'DOC' | 指定文档 |

## 邮件服务与 Linux

如 `inittab` 所示，调制调器将接听。可能会误骗你的是 `mgetty` 不接听。

除了命令行选项，`mgetty` 使用配置文件定义其操作。`/etc/ppp/options` 文件用于

```
/AutoPPP

- pap

- crtsck
```
