
### 配置文件示例

```
fifo /etc/diald/diald.ctl

mode ppp

connect /sh /etc/ppp/connect

device /dev/modem

speed 38400

lock

crcts

local 192.168.1.45

remote 192.168.1.249

defaultroute

pppd-options asyncmap 0

include /usr/lib/diald/standard.filter
```

以上一章节“使用动态地址连接”中描述相同的方式运行 `dial` 命令。当你运行 `netstat` 或 `route` 时，将看到静态 IP 地址。

## 使用网络接口建立 PPP 连接

Red Hat 网络配置器简化了建立 PPP 连接的任务。以 `root` 身份登录并启动系统。打开控制面板并打开图 8-5 所示的网络配置器。

![](img/29df11d9c5c608ff7bfa65d0c78e37_354_0) 图 8-5：配置器窗口

点击网络配置器窗口顶部的 `Interfaces`（接口）按钮。激活 `Interfaces` 窗口，如图 8-6 所示。

![](img/29df11d9c5c608ff7bfa65d0c78e37_355_0) 图 8-6：接口窗口

点击 `PPP` 按钮，出现 `Create Interface`（创建接口）窗口。

![](img/29df11d9c5c608ff7bfa65d0c78e37_355_1) 图 8-7：创建接口窗口

输入你的 `ISP` 账户信息，如图 8-7 所示。

如果你需要调整硬件、通信接口（即串口端口）或网络设置，点击 `Customize`（自定义）按钮，进入图 8-8 所示的 `Edit Interface`（编辑接口）窗口。否则，点击 `Done` 完成接口设置。如果你没有设置从串口设备到调制调器的符号链接（手动使用 `/bin/ln` 命令或通过控制面板的 `Modem` 配置器），你应该在 `Customization` 窗口中将端口设置为 `/dev/tty1`。如果你将调制调器连接到 `/dev/tty0`（在 `MS-DOS` 中），你的系统可能会不同。如果你只是在实验，调制调器在握手时计算机填充了缓冲区并需要时间处理它。接下来点击 `Networking`（网络）按钮，出现图 8-9 所示的窗口。这是你可能更改默认路由的窗口。

![](img/29df11d9c5c608ff7bfa65d0c78e37_356_1) 最后，点击 `Communication`（通信）按钮，出现图 8-10 所示的窗口。

![](img/29df11d9c5c608ff7bfa65d0c78e37_357_0) 图 8-10：通信设置的自定义窗口

点击 `Done` 按钮，出现另一个窗口让你保存或取消所做的编辑。点击 `Save` 返回网络配置器。你已经配置了 `PPP` 连接，可以通过点击 `Activate` 激活它。如果调制调器已连接并打开，将启动 `pppd` 守护进程并运行脚本。这与 `dialup` 示例非常相似。列表 8-9 显示运行脚本 `/etc/sysconfig/network-scripts/ifup-ppp` 是根据你在网络配置器中的选择创建的。

列表 8-9：串口端口的自定义窗口

```
714 1 S     0:00 /etc/sysconfig/network-scripts/ifup-ppp /etc/sysconfig
716 1 S     0:00 /usr/bin/pppd -detach lock crcts defaultroute /dev
718 ? D     0:00 modprobe -k ppp0
```

注意内核进程通过 `modprobe` 将 `pppd` 插入内核。接下来运行拨号 `ISP` 的脚本，如图 8-10 所示。

列表 8-10：脚本启动了 `pppd` 守护进程

```
636 1 S 0:00 /usr/sbin/pppd -detach lock crcts defaultroute /dev
641 1 S 0:00 /usr/sbin/chat -f /etc/sysconfig/network-scripts/chat-ppp0
```

`chat` 进程结束，留下 `pppd` 守护进程控制连接。列表 8-11 显示 `pppd` 守护进程控制连接。

列表 8-11：控制连接的原始 `pppd`（注意：列表 8-11 的 `OCR` 文本在源文件中损坏）

你再次拥有完整的 `TCP/IP` 连接。你是一个互联网节点。要断开连接，只需点击网络配置器中的 `Deactivate`（禁用）按钮

## 监控你的连接

几个常用的网络监控和配置工具是 `ifconfig`、`route` 和 `netstat`。你使用 `ifconfig` 配置网络接口（物理和逻辑）。`route` 添加、删除和编辑静态路由。`netstat` 显示网络统计信息。如果你不带任何参数输入 `ifconfig`，将获得有关接口的信息，如列表 8-12 所示：

```
ifconfig
```

列表 8-12：`ifconfig` 显示接口信息

```
lo Link encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.255.255.0
UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1
RX packets:175 errors:0 dropped:0 overruns:0
TX packets:175 errors:0 dropped:0 overruns:0
eth0 Link encap:10Mbps Ethernet Hwaddr00:A0:24:2F:30:69
inet addr:192.168.1.254 Bcast:192.168.1.255 Mask:255.255.255.0
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:8809 errors:0 dropped:0 overruns:0
TX packets:6418 errors:0 dropped:0 overruns:0
s10 Link encap:Serial Line IP
inet addr:127.0.0.2 P-T:127.0.0.3 Mask:255.255.255.0
UP POINTPOINT RUNNING MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:1 errors:0 dropped:0 overruns:0
```

## 第三部分：重要的客户端-服务器网络

要显示系统可用的静态路由，请带有 `-n` 参数输入 `route` 命令：

```bash
/sbin/route -n
```

此命令显示了列表 8-13 所示的信息。注意，您需要配置 `/etc/hosts` 文件以显示接口名称。否则，`route` 命令将花费很长时间才能确定无法通过名称服务器解析 `IP` 地址。如果您配置了 `/etc/hosts`，可以移除数字选项 `-n`，并以助记符显示 `IP` 地址。

列表 8-13：`route` 命令显示静态路由

| 目的 | 网关 | 子网掩码 | 标志 | 标量 引用 | 使用接口 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 127.0.0.3 | * | 255.255.255 | UH | 1 | 0 slo |
| 192.168.1.0 | * | 255.255.255.0 | U | 0 | 46 eth0 |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 8 lo |
| default | * | 0.0.0.0 | U | 1 | 1 slo |

使用如下行所示参数的 `netstat` 命令，显示所有网络接口的统计信息：

```bash
/bin/netstat -r -n
```
