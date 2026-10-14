

[molar]
# /usr/bin/crontab -l | grep memberUP
00 00,12 * * 1,3,5 /usr/sbin/caa_balance memberUP  #clustercronData

有关如何创建自己的集群范围 cron 解决方案的信息，请参阅最佳实践，“Using cron in a TruCluster Server Cluster”，可在以下位置获得：

http://www.tru64unix.compaq.com/docs/best_practices.

## 23.4.18 资源可用性统计

在 V5.1B 中，可以使用 caa_report 命令获取资源的可用性。您可以通过不使用任何开关来使用该命令查看每个资源的统计信息，或者，通过使用“-a”开关，可以选择要返回统计信息的资源。

```
# caa_report -a "memberUP powerUP"
Time report for period from earliest known begin-date to Wed Jul 3 00:02:10 2002

Application Availability Report for babylon5
Applications          starting/ending      uptime
------------------------------------------------
memberUP              Tue Jul 2 23:40:44 2002   99.61 %
                      Wed Jul 3 00:02:10 2002
powerUP                Tue Jul 2 23:41:06 2002   99.05 %
                      Wed Jul 3 00:02:10 2002
```

caa_report 命令可以通过使用“-o”开关仅返回具有非零统计信息的资源。此外，使用 caa_report 命令并使用“-s”开关将返回存在统计信息的所有资源。

特定时间段内应用程序的可用性可以通过“-b time”和“-e time”开关分别用于开始和结束时间范围来获取，其中 time 的形式为 mm/dd/yy:hh:mm。

要查看 memberUP 从 2002 年 6 月 15 日午夜到现在的可用性，您可以使用以下命令：

```
# caa_report -a memberUP -s 6/15/02:00:00
```

有关更多信息，请参阅 caa_report(1) 参考页。

## 23.4.19 资源状态

正如您现在可能已经注意到的那样，可以使用 caa_stat 命令确定资源的状态。caa_stat 命令生成的输出主要有两种形式：列表输出（每个资源多行）和表格输出（每个资源一行）。

列表输出是默认值，而表格输出是通过使用“-t”开关实现的。请注意，caa_stat 命令有一个“-l”（小写“L”）开关可用于列表输出，尽管它是隐含的。

本章中您看到的大部分输出都是表格形式，主要是因为输出更紧凑。

以下是显示 caa_stat 命令以下输出形式的列表输出示例：

- 默认输出。
- 详细输出（“-v”开关）。
- 使用“-p”开关获得的内存中配置文件（或当前注册的属性值）。
- 使用“-f”开关获得的完整输出（“-p”和“-v”开关的组合）。

| 默认 | 详细 | 当前注册的属性值 | 完整（详细 + CRAV） |
|---|---|---|---|
| # caa_stat ARes<br>NAME=ARes<br>TYPE=application<br>RESTART_ATTEMPTS=1<br>RESTART_COUNT=0<br>REBALANCE=t::1:0<br>FAILURE_THRESHOLD=0<br>FAILURE_COUNT=0<br>TARGET=ONLINE<br>STATE=ONLINE on molari | # caa_stat -v ARes<br>NAME=ARes<br>TYPE=application<br>ACTION_SCRIPT=ARes.scr<br>RESTART_ATTEMPTS=1<br>RESTART_COUNT=0<br>REBALANCE=t::1:0<br>FAILURE_THRESHOLD=0<br>FAILURE_COUNT=0<br>TARGET=ONLINE<br>STATE=ONLINE on molari | # caa_stat -p ARes<br>NAME=ARes<br>TYPE=application<br>ACTION_SCRIPT=ARes.scr<br>ACTIVE_PLACEMENT=0<br>AUTO_START=0<br>CHECK_INTERVAL=60<br>DESCRIPTION=ARes<br>FAILOVER_DELAY=0<br>FAILURE_INTERVAL=0<br>FAILURE_THRESHOLD=0<br>HOSTING_MEMBERS=<br>OPTIONAL_RESOURCES=<br>PLACEMENT=balanced<br>REBALANCE=t::1:0<br>REQUIRED_RESOURCES=<br>RESTART_ATTEMPTS=1<br>SCRIPT_TIMEOUT=60 | # caa_stat -f ARes<br>NAME=ARes<br>TYPE=application<br>ACTION_SCRIPT=ARes.scr<br>ACTIVE_PLACEMENT=0<br>AUTO_START=0<br>CHECK_INTERVAL=60<br>RESTART_ATTEMPTS=1<br>RESTART_COUNT=0<br>DESCRIPTION=ARes<br>FAILOVER_DELAY=0<br>FAILURE_INTERVAL=0<br>HOSTING_MEMBERS=<br>OPTIONAL_RESOURCES=<br>PLACEMENT=balanced<br>REBALANCE=t::1:0<br>REQUIRED_RESOURCES=<br>RESTART_ATTEMPTS=1<br>SCRIPT_TIMEOUT=60<br>FAILURE_THRESHOLD=0<br>FAILURE_COUNT=0<br>TARGET=ONLINE<br>STATE=ONLINE on molari |

表 23-13：caa_stat 输出

