

**注意：** `pap-secrets` 和 `chap-secrets` 文件不应允许除 root 用户外的任何人访问。任何获取这些信息的人都可能利用它们访问您的互联网账户。默认情况下，权限对所有用户（除 root 用户外）都是关闭的。（若要关闭权限，请输入 `chmod 600 /etc/ppp/*secrets`。）

## 查看 ifcfg-ppp0 文件

`ifcfg-ppp0` 文件（`/etc/sysconfig/network-scripts/ifcfg-ppp0`）包含传递给 `pppd` 守护进程的选项，这些选项用于与远程 PPP 服务器协商的功能。PPP 连接中出现的许多问题都是由某些选项配置错误造成的（特别是请求服务器无法或不提供的功能）。

下面是一个用于连接到 Windows NT PPP 服务器的 `ifcfg-ppp0` 文件示例：

```
DEVICE=ppp0
NAME=Acme_Internet_Service
MODEMPORT=/dev/ttyS0
LINESPEED=115200
PAPNAME=guest
ONBOOT=yes
DEFROUTE=yes
DEMAND=yes
IDLETIMEOUT=600
```

设备名称为 `ppp0`（这与配置文件 `ifcfg-ppp0` 相关联）。`NAME` 是您分配给该连接的名称。`MODEMPORT` 是与调制解调器所连接端口相关联的设备名称（在本例中为 COM1）。`LINESPEED` 设置计算机与调制解调器之间的速度（单位为 bps，而非拨号速度，后者通常较慢）。假设您正在使用 PAP 身份验证，则 `PAPNAME` 是您登录时使用的用户名。

- **ONBOOT** 设置为 `yes`，以便在启动时启动 `pppd` 守护进程（但由于设置了 `DEMAND=yes`，此时尚不会进行拨号）。`DEFROUTE=yes` 将默认路由设置为此 PPP 连接。
- **DEMAND**=`yes` 确保仅在存在流量时才初始化链路。`IDLETIMEOUT=600` 会导致连接在空闲 600 秒后超时。

**提示：** 如果您想查看这些参数各自设置的确切选项，请查看 `/etc/sysconfig/network-scripts/ifup-ppp` 脚本的内容。例如，如果 `DEFROUTE=yes`，则向 `pppd` 守护进程发送 `defaultroute` 选项。有关每个选项的说明，请参阅 `pppd` 手册页（输入 `man pppd`）。

您可以添加一行 `PPOPTIONS` 以设置希望传递给 `pppd` 守护进程进程的任何其他选项。在某些情况下，ISP 可能会要求使用此处未包含的其他值。同样，连接某些类型的服务器时，您也不应将某些选项放入此文件中。以下是关于某些 Windows NT 服务器建议在此文件中不应包含或应包含的一些值。有关这些选项的说明，请参阅 `pppd` 手册页：

- **remotename=remotename** — 您可能需要此值用于 PAP 身份验证，但在 CHAP 身份验证中不应输入。（对于 CHAP，远程 PPP 服务器会将其名称发送给您。）
- **require-chap, require-pap, auth, noauth** — 要求 Windows NT 服务器进行自我身份验证是个不错的主意（这就是 *require-chap* 和 *require-pap* 在各自协议中执行的操作）。`auth` 值要求服务器在能够发送或接收数据包之前进行自我身份验证。然而，据可靠消息，Windows NT 不允许您执行这些操作。身份验证将失败，您将无法建立连接。您可能需要明确表明服务器无需进行自我身份验证，方法是输入 `noauth` 选项。
- **default-asyncmap** — 由于“链路透明度问题”，PAP 可能无法完成身份验证。如果身份验证失败，且您确定身份验证信息正确，请尝试添加此值。
- **ipcp-accept-local, ipcp-accept-remote** — 有时服务器会请求您的本地 IP 地址，即使它想自己分配一个。远程地址也是如此。尝试将以下行添加到选项文件中：

```
192.168.0.1:192.168.0.2
ipcp-accept-local
ipcp-accept-remote
demand
```

这提供了临时本地和远程地址，并告诉远程服务器它可以替换这些值。除了使用私有 IP 地址（如所示），您还可以使用 0.0.0.0。

- **bsdcomp, deflate** — 某些类型的压缩不受 Windows NT PPP 服务器支持。因此，您不应请求 BSD 压缩（*bsdcomp*）或 Deflate 压缩（*deflate*）。在某些情况下，您可能希望禁止这些类型的压缩：*nobdscmp*、*nodeflate* 和 *noaccp*（用于无压缩控制协议）。

如前所述，描述 *pppd* 选项的最佳位置是 *pppd* 手册页。要查看示例选项文件，请查看 /usr/share/doc/ppp/sample。

## 运行调试

如果您的调制解调器正在工作，但完全无法连接，首先要做的是开启 PPP 的日志记录。这将有助于您追踪问题。如果在查看日志输出后仍然不知所措，请让专家审查日志文件。通过在 *ifcfg-ppp0* 文件中将 *DEBUG* 设置为 *yes* 来确保已开启调试。

**提示：** 我建议将失败的 PPP 输出发布到 comp.protcol.ppp 新闻组，那里有一些非常聪明的 PPP 专家可以帮助回答您的问题。然而，在发布之前，请先阅读该组几天的消息。很可能已经有人遇到过相同的问题并有解决方案。此外，请只发布日志文件中相关的部分。您也可以向当地的 Linux 用户组寻求帮助。

要将调试信息定向到 PPP 的单独日志文件，请在 `/etc/syslog.conf` 文件中添加以下行：

```
daemon.*      /var/log/pppmsg
local2.*      /var/log/pppmsg
```

在此之后，按如下方式重启 syslog 守护进程：

```
# service syslog restart
```

最好尝试从桌面进行此调试过程，因为需要打开几个终端窗口（建议至少打开三个）。从第一个窗口中，启动一个命令，列出我们刚才定义的日志文件（pppmsg）的内容，以便调试消息传入时显示：

```
# tail -f /var/log/pppmsg
```

在下一个窗口中，启动 PPP 接口。假设它是 ppp0 接口，请使用以下命令作为 root 用户：

```
# ifup ppp0
```

以下是输出的一部分列表：

```
Sep  6 20:43:51 maple pppd[2077]: pppd 2.4.1 started by root, uid 0
Sep  6 20:43:51 maple ifup-ppp: pppd started for ppp0 on /dev/modem at 115200
Sep  6 20:43:52 maple chat[2079]: abort on (BUSY)
Sep  6 20:43:52 maple chat[2079]: abort on (ERROR)
Sep  6 20:43:52 maple chat[2079]: abort on (NO CARRIER)
Sep  6 20:43:52 maple chat[2079]: abort on (NO DIALTONE)
Sep  6 20:43:52 maple chat[2079]: abort on (Invalid Login)
Sep  6 20:43:52 maple chat[2079]: abort on (Login incorrect)
Sep  6 20:43:52 maple chat[2079]: send (ATE)
Sep  6 20:43:52 maple chat[2079]: expect (OK)
Sep  6 20:43:53 maple chat[2079]: AT:
Sep  6 20:43:53 maple chat[2079]: OK
Sep  6 20:43:53 maple chat[2079]: -- got it
Sep  6 20:43:53 maple chat[2079]: send (ATDT5551212")
Sep  6 20:44:10 maple chat[2079]: expect (CONNECT)
Sep  6 20:44:10 maple chat[2079]: "
Sep  6 20:44:10 maple chat[2079]: ATDT5551212"
Sep  6 20:44:10 maple chat[2079]: CONNECT
Sep  6 20:44:10 maple chat[2079]: -- got it
Sep  6 20:44:10 maple chat[2079]: send (\d)
Sep  6 20:44:14 maple pppd[2077]: Serial connection established.
Sep  6 20:44:14 maple pppd[2077]: Using interface ppp0
Sep  6 20:44:14 maple pppd[2077]: Connect: ppp0 <>--> /dev/modem
Sep  6 20:44:17 maple pppd[2077]: local IP address 222.62.137.121
Sep  6 20:44:17 maple pppd[2077]: remote IP address 222.62.1.105
Sep  6 20:44:17 maple pppd[2077]: primary   DNS address 222.62.111.253
Sep  6 20:44:17 maple pppd[2077]: secondary DNS address 111.222.111.254
```

此输出显示了在 `/dev/modem` 上启动 PPP 连接。验证调制解调器工作正常后，chat 脚本发送电话号码。连接建立，PPP 接口启动。经过一些参数协商后，服务器为通信双方分配 IP 地址，连接即可使用。

如果您成功连接，但您的应用程序（Web 浏览器、FTP 等）似乎都无法工作，请检查您的 PPP 接口是否被标记为默认路由（`/sbin/route -n`）。如果是，请检查您的 `/etc/resolv.conf` 文件中是否正确指定了 DNS 服务器。使用 `ping` 命令对那些 DNS 服务器的 IP 地址进行 ping，以确保您可以连通。

## 将您的 LAN 连接到互联网

您 LAN 上的用户很高兴您使他们能够相互共享文件和打印机。但是，如果他们想访问互联网，可能需要使用自己的调制解调器、电话线和互联网账户。既然您的用户已经通过 LAN 连接，您可以在 Linux 中设置一个供所有人共享的互联网连接。这样做的优点如下：

- **节省调制解调器** — 不必每台计算机都有调制解调器，您可以有一个高速设备（如 DSL 路由器或电缆调制解调器），它将所有流量路由到互联网。
- **节省电话线** — 不必为每个想要访问互联网的人使用一条电话线，您可以使用一条线连接到您的 ISP。（在 DSL 的情况下，电话公司甚至允许您使用同一条电话线进行模拟语音和高速数字数据传输。）
- **集中维护** — 如果与您的互联网连接相关的信息发生变化（如您的拨出号码或名称服务器地址），您可以在一个位置管理这些更改，而无需在每台计算机上进行更改。
- **集中安全** — 您可以更好地控制进出您网络的互联网流量。

本节的步骤假设您已经按照第 15 章的描述设置了 LAN。同时也假设您的 Fedora 系统有一个通往互联网的出站连接，LAN 上的计算机与互联网之间的所有流量都可以通过该连接传输。

