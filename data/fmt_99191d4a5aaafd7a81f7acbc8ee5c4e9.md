
## 第 26 章 firestarter 和 iptables：设置防火墙

![](img/556454b01d95450a92edff64b47580d6_938_0.png)

**图 26-7** 事件选项卡，右键菜单

如果这些事件可能是恶意用户尝试访问系统的行为，则被认为是严重的。例如，被拦截的使用 `ssh` 登录尝试是一个严重事件；被拦截的 `ping` 则不是。

“网络”（Network）框架显示了系统每个连接的活动情况。

当您点击“活动连接”（Active connections）左侧的小三角形时，`firestarter` 会显示一个可滚动的活动连接列表；拉伸窗口可以显示更多连接。点击此列表中的某行进行选择，然后右键点击并选择“查找主机名”（Lookup hostnames），将“源”（Source）和“目的”（Destination）列中的值从 IP 地址更改为主机名。“端口”（Port）列出了连接在目标主机上的端口。“服务”（Service）列指示了与指定端口关联的服务。“程序”（Program）列显示了运行的程序名称（如果它是本地的或是 `firestarter` 已知的）。

### 事件选项卡

`Firestarter` 事件选项卡（图 26-7）是修改默认防火墙策略的关键。它显示了被拦截的连接列表。该列表中的每一行都指定了防火墙根据规则拦截的一个事件。以黑色显示的事件是尝试连接随机端口的尝试，通常不引起关注。灰色的事件是无害的，主要由广播流量组成。红色的事件是尝试访问未向公众提供的服务，可能表明恶意用户正尝试访问防火墙主机或客户端系统。

您可以通过以下几种方法修改此列表：

- 要用主机名代替 IP 地址，请高亮您想要更改的条目，右键点击并选择“查找主机名”（Lookup Hostnames）（图 26-7）。
- 默认情况下，“被拦截连接”（Blocked Connections）列表不包含冗余项。要显示冗余条目，请取消 `Firestarter` 菜单中“编辑(Edit):偏好(Preferences):事件(Events):跳过冗余项(Skip redundant entries)”复选框的勾选。

### firestarter：维护防火墙

| | 事件 (Events) | 策略 (Policy) | 帮助 (Help) |
|---|---|---|---|
| 清除 (Clear) | | | `Ctrl+L` |
| 重载 (Reload) | | | |
| 保存列表 (Save List) | | | `F12` |
| 显示列 (Show Column) | 时间 (Time) | | `Ctrl+1` |
| | 方向 (Direction) | | `Ctrl+2` |
| | 端口 (Port) | 源 (Source) | `Ctrl+3` |
| | | 协议 (Prot) | `Ctrl+4` |
| | | 出 (Out) | `Ctrl+5` |
| | | | `Ctrl+6` |
| | | | `Ctrl+7` |
| | | | `Ctrl+8` |
| | | | `Ctrl+9` |
| | | | `Ctrl+10` |
| | | | `Ctrl+11` |
| | | | `Ctrl+12` |
| | | | `Ctrl+13` |
| | | | `Ctrl+14` |
