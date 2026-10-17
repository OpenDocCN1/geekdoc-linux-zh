
9. `logrotate` 程序查询以下哪个配置文件来获取设置？

A. `/etc/logrotate.conf`

B. `/usr/bin/logrotate/logrotate.conf`

C. `/usr/src/logrotate/logrotate.conf`

D. `/etc/logrotate/.conf`

E. `~/.logrotate`

10. 你想创建一个日志条目，说明你正在手动关闭系统以添加新网卡。在使用 `shutdown` 之前，你可能会如何创建此日志条目？

A. `dmesg -1 "shutting down to add network card"`

B. `syslog shutting down to add network card`

C. `rsyslogd "shutting down to add network card"`

D. `logger shutting down to add network card`

E. `wall "shutting down to add network card"`

11. 你的经理要求你配置 `logrotate` 以定期、无人值守的方式运行。你应该配置什么实用程序/功能来实现这一目标？

A. `at`

B. `/etc/logrotate.d`

C. `cron`

D. `initabb`

E. `ntpd`

12. 你已将 Linux 计算机上的系统（软件）时钟设置为正确时间，并想将硬件时钟设置为与之匹配。你可能会输入什么命令来实现这一目标？

A. `date --sethwclock`

B. `ntpdate`

C. `sysclock --tohc`

D. `time --set -hw`

E. `hwclock --systohc`。效果是什么？

13. 作为 root 用户，你输入 `date 12110710`。

+ A. 软时钟将被设置为今年 12 月 11 日早上 7:10。
+ B. 软时钟将被设置为今年 10 月 7 日下午 12:11。
+ C. 软时钟将被设置为今年 11 月 12 日早上 7:10。
+ D. 软时钟将被设置为今年 7 月 10 日下午 12:11。
+ E. 软时钟将被设置为 1211 年 7 月 10 日。

14. 计算机在 `/etc/ntp.conf` 中具有以下两行会导致什么效果？

```
server pool.ntp.org
server tardis.example.org
```

+ A. 本地计算机的 NTP 服务器将轮询公共 NTP 池中的服务器；第一个服务器选项将覆盖后续的服务器选项。
+ B. 本地计算机的 NTP 服务器将轮询 `tardis.example.org` 时间服务器；最后一个服务器选项将覆盖之前的服务器选项。
+ C. 本地计算机的 NTP 服务器将同时轮询公共 NTP 池中的服务器和 `tardis.example.org` 的服务器，并使用提供最清洁数据的站点。
+ D. 本地计算机的 NTP 服务器将因为 `/etc/ntp.conf` 中格式错误的服务器规范而拒绝运行。
+ E. 本地计算机的 NTP 服务器将轮询公共服务器池中的计算机，当且仅当公共池服务器宕机时回退到 `tardis.example.org`。

15. 你在五台计算机的网络中将一台（`gateway.pangaea.edu`）配置为 NTP 服务器，它从 `ntp.example.com` 获取时间信号。你网络中的其他计算机应该使用哪个作为它们的时间源？

+ A. 你应该咨询公共 NTP 服务器列表以找到最适合你的服务器。
+ B. `gateway.pangaea.edu` 和 `ntp.example.com` 均是
+ C. 仅 `ntp.example.com`
+ D. 仅 `gateway.pangaea.edu`
+ E. 无。NTP 应该在互联网上使用，而不是小型本地网络上。

16. 下列任务最可能由 `cron` 任务处理？（选择两项）

+ A. 计算机启动时启动重要的服务器
+ B. 查找并删除旧临时文件
+ C. 脚本化受监督账户创建
+ D. 监控磁盘分区空间状态并发送邮件报告
+ E. 按顺序向打印机发送文件

17. 下列哪行如果用于用户 cron 任务，将每天运行两次 `/usr/local/bin/cleanup`？

+ A. `15 7,19 * * baker /usr/local/bin/cleanup`
+ B. `15 7,19 * /usr/local/bin/cleanup`
+ C. `*/2* * * baker /usr/local/bin/cleanup`
+ D. `15 */2 * * /usr/local/bin/cleanup`
+ E. `2 /usr/local/bin/cleanup`

18. 你正在一个关键业务系统上安装 Linux。你可能想要添加以下哪个程序以确保每日备份任务被正确处理？

+ A. `temp-up`
+ B. `anacron`
+ C. `crontab`
+ D. `ntpd`
+ E. `syslog-ng`

19. 以下命令实现了什么？（管理员在输入第二个命令后按下 Ctrl+D。）

```
# at teatime
at> /usr/local/bin/system-maintenance
```

+ A. 无；这些命令无效。
+ B. 无；`teatime` 不是 `at` 的有效选项。
+ C. 无；你只能在 `at>` 提示符处输入有效的 `bash` 内建命令。
+ D. 无；`at` 需要你传递脚本名称，而 `teatime` 不是。
+ E. `/usr/local/bin/system-maintenance` 程序或脚本将在下午 4:00 运行。

20. 你可能会让脚本在 Linux 计算机上每天运行？（选择两项）

+ A. 将脚本或其链接放在 `/etc/cron.daily`。
+ B. 使用 `at` 命令在指定的时刻每天轮询指定的脚本。
+ C. 创建一个在指定的时刻每天运行一次的用户 `cron` 任务，并使用 `crontab` 安装该 `cron` 任务。
+ D. 使用 `run-parts` 让指定的脚本每天运行。
+ E. 输入 `crontab -d scriptname`，其中 `scriptname` 是你的脚本名称。

# 第 8 章 配置基础网络

本章涵盖了考试目标：

* 109.1 协议基础
* 109.2 基础网络配置
* 109.3 基础网络排错
* 109.4 配置客户端端 DNS

大多数 Linux 系统都连接到网络，无论是客户端还是服务器（通常两者都是）。即使是家用电脑和智能手机等专用设备也连接互联网。因此，设置 Linux 的基础网络工具对于完整配置 Linux 是必要的。在开始此任务之前，你必须理解现代网络的基础，例如网络地址的性质以及网络上常用的工具类型。从那里，你可以转向 Linux 网络配置，包括设置计算机地址、路由和名称解析等任务。遗憾的是，网络配置有时会出错；理解用于诊断和修复网络问题的工具和技术是网络配置中不可或缺的一部分。因此，本章涵盖了网络排错的基础。

# 理解 TCP/IP 网络

网络涉及许多构建在其他组件之上的组件。这些包括网络硬件、数据包以及用于数据交换的协议。这些组件共同组成了协议栈。今天最常见的协议栈是传输控制协议/网协议 (`TCP/IP`) 协议栈，但这并非唯一可用的选择。尽管如此，理解 `TCP/IP` 理论的基础知识将帮助你配置和管理网络。

# 了解网络硬件的基本功能

网络硬件的设计是为了允许两或更多计算机相互进行通信。现代计算机的主板上已经集成了网络接口，但也可以使用内部（`PCI`、`PCIe` 或类似）网卡和外部（`USB`、`PC` 卡及类似）网络接口。许多网络依赖电线或电缆以电脉冲的形式在机器之间传输数据，但使用无线电甚至光执行此工作的网络协议正变得越来越流行。

有时网络硬件与外围接口端口之间的界限是模糊的。例如，并行端口通常不被视为网络端口，但当它与并行线接口协议 (`PLIP`) [`http://tldp.org/HOWTO/PLIP.html`](http://tldp.org/HOWTO/PLIP.html) 使用时，并行端口就变成了一个网络设备。在这种情况下，当 `USB` 或 `RS-232` 串口端口与点点协议 (`PPP`) 使用时（通常连接电话调制解调器），它变成了网络接口。此类连接在今天很少见，但仍然可能。如果你需要知道如何配置 `PPP` 连接，请参考你所在发行版的文档或位于 [`http://tldp.org/HOWTO/PPP-HOWTO/`](http://tldp.org/HOWTO/PPP-HOWTO/) 的 `PPP` HOW TO。
