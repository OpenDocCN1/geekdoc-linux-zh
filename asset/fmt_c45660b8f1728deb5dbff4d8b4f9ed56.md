
- `remote name=remote name` — 您可能需要此值用于 PAP 认证，但在 CHAP 认证时不应输入。（对于 CHAP，远程 PPP 服务器会向您发送其名称。）

- `require-chap`、`require-pap`、`auth`、`noauth` — 要求 Windows NT 服务器进行自我认证（即 `require-chap` 和 `require-pap` 在其各自协议中所做的）是一个好主意。`auth` 值要求服务器在可以发送或接收数据包之前进行自我认证。然而，据可靠消息，Windows NT 不允许执行这些操作。认证将失败，您无法建立连接。您可能需要明确输入 `noauth` 选项，以指示服务器不需要进行自我认证。

- `default-asyncmap` — PAP 可能因“链路透明性问题”而认证失败。如果认证失败且您确信认证信息正确，请尝试添加此值。

- `ipcp-accept-local`、`ipcp-accept-remote` — 有时服务器会请求您的本地 IP 地址，即使它想要自己分配一个。远程地址也是如此。请尝试将这些行添加到选项文件中：

```
192.168.0.1:192.168.0.2
ipcp-accept-local
ipcp-accept-remote
demand
```

这提供了临时的本地和远程地址，并告知远程服务器它可以替换这些值。您可以使用 `0.0.0.0` 代替此处显示的私有 IP 地址。

- `bsdcomp`、`deflate` — 某些类型的压缩不受 Windows NT PPP 服务器支持。因此，您不应请求 BSD 压缩（`bsdcomp`）或 Deflate 压缩（`deflate`）。在某些情况下，您可能希望明确禁止这些类型的压缩：`nobbsdcomp`、`nodeflate` 和 `noccp`（用于无压缩控制协议）。

如前所述，`pppd` 选项的最佳说明位置是 `pppd` 手册页。有关示例选项文件，请查看 `/usr/share/doc/ppp*/sample`。

### 运行调试

如果调制解调器工作正常，但您完全无法连接，首先要做的是开启 PPP 日志记录。这将帮助您定位问题。如果在查看日志输出后仍感到困惑，请将该日志文件交给专家进行审查。通过将在 `ifcfg-ppp0` 文件中设置 `DEBUG=yes` 来确保调试已开启。

> **提示：** 我建议将您的失败 PPP 输出发布到 `comp.protcol.ppp` 新闻组，那里有一些非常聪明的 PPP 专家可以回答您的问题。但在发布之前，请阅读该组几天内的消息。很可能有人已经遇到同样的问题并有解决方案。此外，仅发布日志文件中相关的部分。

要将调试定向到 PPP 的独立日志文件，请向 `/etc/syslog.conf` 文件添加以下行：

```
daemon.*                 /var/log/pppmsg
local2.*                /var/log/pppmsg
```

在此之后，按以下方式重启 syslog 守护进程：

```
# service syslog restart
```

最好从桌面进行此调试过程，因为打开几个终端窗口会有帮助（我建议至少三个）。从第一个窗口开始，启动一个命令，列出我们刚才定义的日志文件（`pppmsg`）的内容，以显示调试消息传入：

```
# tail -f /var/log/pppmsg
```

在下一个窗口中，启动 PPP 接口。假设是 `ppp0`，请以 root 用户身份使用以下命令：

```
# ifup ppp0
```

以下是输出的部分列表：

```
Jun  6 20:43:51 maple pppd[2077]: pppd 2.4.1 started by root, uid 0
Jun  6 20:43:51 maple ifup-ppp: pppd started for ppp0 on /dev/modem at 115200
Jun  6 20:43:52 maple chat[2079]: abort on (BUSY)
Jun  6 20:43:52 maple chat[2079]: abort on (ERROR)
Jun  6 20:43:52 maple chat[2079]: abort on (NO CARRIER)
Jun  6 20:43:52 maple chat[2079]: abort on (NO DIALTONE)
Jun  6 20:43:52 maple chat[2079]: abort on (Invalid Login)
Jun  6 20:43:52 maple chat[2079]: abort on (Login incorrect)
Jun  6 20:43:52 maple chat[2079]: send (ATZ^M)
Jun  6 20:43:52 maple chat[2079]: expect (OK)
Jun 6 20:43:53 maple chat[2079]: ATZ^MM
Jun 6 20:43:53 maple chat[2079]: OK
Jun 6 20:43:53 maple chat[2079]: -- got it
Jun 6 20:43:53 maple chat[2079]: send (ATDT5551212^MM)
Jun 6 20:43:53 maple chat[2079]: expect (CONNECT)
Jun 6 20:43:53 maple chat[2079]: ^M
Jun 6 20:44:10 maple chat[2079]: ATDT5551212^MM
Jun 6 20:44:10 maple chat[2079]: CONNECT
Jun 6 20:44:10 maple chat[2079]: -- got it
Jun 6 20:44:10 maple chat[2079]: send (^D)
Jun 6 20:44:14 maple pppd[2077]: Serial connection established.
Jun 6 20:44:14 maple pppd[2077]: Using interface ppp0
Jun 6 20:44:14 maple pppd[2077]: Connect: ppp0 <--> /dev/modem
...
Jun 6 20:44:17 maple pppd[2077]: local IP address 222.62.137.121
Jun 6 20:44:17 maple pppd[2077]: remote IP address 222.62.1.105
```

此输出显示在 `/dev/modem` 上启动 **PPP** 连接。在验证调制解调器工作正常后，`chat` 脚本发送电话号码。连接建立，**PPP** 接口启动。在进行一些参数协商后，服务器为通信双方的 IP 地址进行分配，连接即可使用。

如果您能够连接，但您的任何应用程序（Web 浏览器、**FTP** 等）似乎都不起作用，请检查您的 **PPP** 接口是否被标记为默认路由（`/sbin/route -n`）。如果是，请检查您的 `/etc/resolv.conf` 文件中的 **DNS** 服务器是否指定正确。使用 `ping` 命令向这些 **DNS** 服务器 IP 地址发起请求，以确保您可以访问它们。

### 将您的 LAN 连接到 Internet

您 **LAN** 上的用户对能够共享文件和打印机感到满意。但是，如果他们想访问 **Internet**，可能需要使用自己的调制解调器、电话线和 **Internet** 账户才能到达那里。在您的用户已经通过 **LAN** 连接的情况下，您可以设置一个所有人都可以共享的 **Internet** 连接。这样做的优点如下：

- **节省调制解调器** — 不需要每台计算机都有自己的调制解调器，您可以拥有一个高速调制解调器（例如 **DSL** 调制解调器），它可以将所有消息路由到 **Internet**。

- **节省电话线** — 不需要每个想访问 **Internet** 的人使用一条电话线，您可以使用一条到 **ISP** 的线路。（在 **DSL** 的情况下，电话公司甚至允许您使用同一条电话线进行模拟语音和高速数字数据传输。）

- **集中维护** — 如果您的 **Internet** 连接相关信息发生变更（例如拨出号码或名称服务器地址），您可以在一个位置管理这些变更，而无需在每台计算机上进行修改。

## 中央安全管理

- **中央安全管理** — 您可以更好地控制进出您网络的互联网流量。

本部分的步骤假设您已按照第 15 章所述设置了局域网（LAN）。同时假设您的 Red Hat Linux 系统拥有一条通往互联网的出站连接，局域网内计算机与互联网之间的所有流量都可以通过该连接传递。该出站连接可以是拨号连接，也可能是通过另一张连接到 DSL 调制解调器或其他局域网的局域网卡。本节介绍了设置 Red Hat Linux 计算机的两种方法，以便局域网上的客户端可以访问互联网：
