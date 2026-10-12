
| **SNMP 对象** | **对象信息** |
| :--- | :--- |
| ifOutDiscards | 即使未检测到错误，也被选择丢弃以防止其传输的出站数据包数量 |
| ifOutErrors | 因错误无法传输的出站数据包数量 |
| ifOutQLen | 输出数据包队列长度（以数据包为单位） |

MRTG 支持对 SNMP 对象或 OID 字符串进行数学运算。这些运算符可用于例如将一组接口的输入错误和输出错误总数进行分组，而不仅仅是单个接口。因此，

$$
\begin{array}{l}
\text{Target[monet] : ifInErrors.0:public@10.0.2.75+ifInErrors.1:public@10.0.2.75}\\
\&\text{ifOutErrors.0:public@10.0.2.75+ifOutErrors.1:public@10.0.2.75}
\end{array}
$$

计算在设备 10.0.2.75 上找到的第一个和第二个接口的接口错误总和。

## 监控磁盘空间

MRTG 还支持从自定义程序或脚本收集数据。例如，MRTG 可以显示磁盘空间使用信息。使用可在贡献软件目录中找到的 df2mrtg 脚本，MRTG 监控各个磁盘分区并提供磁盘使用和大小信息。以下命令显示此任务：

Target[monet] : `/usr/mrtg/bin/df2mrtg -u /dev/hdb2`

将此行和一些附加选项放在 MRTG 配置文件中会生成图 9.6 所示的图表。表 9.6 显示，具有从其他来源收集信息的能力是 MRTG 的一项非常强大的功能。如图所示，每日图表显示磁盘空间在大约 120 MB 左右运行；然后在大约下午 6:00（1800 小时）磁盘空间骤降至接近零。这持续了四个小时，直到当晚 10:00 后释放了额外的磁盘空间，超过 180 MB。月度图表记录了相同的事件，但实际数据被压缩到更小的比例。因此，磁盘空间为零的四小时窗口在此图表中只是短暂的下降。这些图表使得可以轻松地将磁盘消耗 pinpoint 到天和小时，并将极大地有助于确定事件发生的原因。

![](img/f265c9d1f2610aca197c430cbfcd51f5_524_0.png)

## 图 9.6 MRTG 磁盘空间报告。

如果你有兴趣开发自定义程序来监控非 SNMP 信息，程序返回的数据必须采用 MRTG 能够理解的格式。因此，程序必须返回四行输出，其中包括第一个变量的当前状态、第二个变量的当前状态、指示目标系统正常运行时间的字符串以及指示目标名称的字符串。

前两个变量可与例如每秒传入字节数和每秒传出字节数相比较。系统更新时间表示系统上次重新启动的时间（或网络管理组件——代理——上次重新启动的时间）。为确保脚本输出与目标匹配，会返回目标名称。

在 `df2mrtg` 脚本的情况下，第一个变量表示当前使用的磁盘空间（以千字节为单位，当使用 -u 选项时），第二个变量是第一个变量的重复。因为我们只对监控磁盘空间感兴趣，所以系统正常运行时间信息和表示目标的字符串是不需要的。此外，根据脚本返回的数据类型，你可能需要使用 Options 关键字并根据需要使用 gauge 或 absolute。此脚本还报告有关本地系统磁盘分区的其他信息。表 9.7 列出了命令行选项。

## **表 9.7** *df2mrtg* 脚本命令行选项

| Option | Description |
| :--- | :--- |
| -f | 报告分区中的空闲磁盘空间 |
| -s | 报告磁盘分区的总大小 |
| -p | 以百分比报告空闲磁盘空间 |
| -u | 报告已使用的磁盘空间 |

如果你希望 MRTG 对分区上的空闲磁盘空间进行图表绘制，请使用 -f 选项。-s 选项将报告分区总大小。因为 MRTG 用于监控网络接口，所以当它用于监控磁盘空间或其他系统信息时，应更改一些默认值和配置信息。以下是与使用 `df2mrtg` 脚本时最合适的配置非常接近的 MRTG 配置。

```
Title[monet]: Disk Space Monitor
PageTop[monet]: <H1> Disk Space Usage for System: Monet
```

```
Options[monet]: gauge,growright
MaxBytes[monet]: 314461
AbsMax[monet]: 400000
WithPeak[monet]: ymwD
YLegend[monet]: Available Space
ShortLegend[monet]: Bytes
Legend1[monet]: Current Disk Utilization.
```

![](img/f265c9d1f2610aca197c430cbfcd51f5_526_0.png)

图 9.7 MRTG 按百分比报告磁盘使用情况。

由于 MRTG 和 df2mrtg 脚本的灵活性，我们可以报告可用磁盘空间的百分比，而不是报告可用磁盘空间。这也许是一个更好的度量，因为通过显示百分比利用率，我们可以快速了解可用磁盘空间状况，而无需进行任何数学运算。图 9.7 显示了同一个分区，但使用脚本的 -p 选项报告磁盘百分比。如你所见，此图表显示的信息与图 9.6 相同，但以百分比显示此信息更有意义且更易于阅读。

## MRTG 的贡献组件

MRTG 包中包含了一些模块，以提供对 MRTG 的额外定制支持以及对额外服务和设备的监控。表 9.8 提供了在 `/usr/lib/mrtg/contrib` 目录中找到的这些模块的列表。

## 表 9.8 MRTG 的贡献模块

| Module Name | Description |
| --- | --- |
| `ascendget` | 提供来自 Ascend 远程访问设备的调制解调器信息 |
| `atmmaker` | 为 ATM 设备构建 MRTG 配置文件 |
| `cpumon` | 监控 UNIX 系统的 CPU 使用情况 |
| `distrib` | 根据 MRTG 日志文件构建网络流量分布图 |
| `get-active` | 生成 MRTG 监控的最活跃接口报告 |
| `get-multiserial` | 监控本地 UNIX 系统上的拨入调制解调器 |
| `GetSNMPlinesUP` | 查询 SNMP 设备以获取特定对象并将值返回给 MRTG |
| `ircstats` | 收集活动 IRC 客户端的信息 |
| `mrtg-archiver` | 根据设备目标列表归档 MRTG 报告 GIF |
| `mrtg-blast` | 在 MRTG 中整合 `tcp-blast` 输出 |
| `mrtg-dynip` | 使 MRTG 能够监控动态网络接口 |

## 表 9.8 MRTG 的贡献模块（续）

| Module Name | Description |
|---|---|
| mrtg-igpet | 使 MRTG 能够使用 IP 地址而不是实例来监控接口 |
| mrtg-mail | 监控邮件统计信息 |
| mrtgidfx | 生成受监控设备的 MRTG 索引 |
| mrtgidnex.cgi | 生成受监控设备的 MRTG 索引（改进的脚本） |
| ping-probe | 使用 ping 显示往返性能信息 |
| portmasters | 显示来自 Livingston Portmaster 设备的调制解调器信息 |
| rdlog2 | 生成 MRTG 监控设备的流量显示 |
| rumb-stat | 从 Apache 等 Web 服务器获取低级统计信息 |
| TCH | 监控 USR Total Control 调制解调器机架的调制解调器利用率 |
| xlsummary | 从 MRTG 日志文件提取摘要信息并生成 Excel 图表 |

这些工具的安装和操作可在与脚本名称相同（或相似）的目录中找到。

## 故障排除 MRTG 问题

由于 MRTG 配置文件由纯文本组成，因此在定制过程中相对容易在此文件中引入语法错误或其他错误。此外，在执行其他 MRTG 程序时可能存在产生错误的其它条件。以下是
