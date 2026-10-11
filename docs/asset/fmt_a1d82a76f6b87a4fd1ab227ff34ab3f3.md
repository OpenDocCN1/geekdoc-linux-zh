
接下来你需要设置 `source` 变量。该选项告诉 Kismet 你正在使用什么类型的驱动和网卡，以及你的网卡配置在什么界面上。下面的例子告诉 Kismet 使用 Host 接入点驱动，并且你的网卡被配置为 `wlan0`。第三个选项 `wlan` 可以设置为任何值。

```
source=hostap,wlan0,wlan
```

以下是一些针对不同网卡和驱动的较常见的 `source` 选项：

```
# Source line for Intel Pro Wireless 2100 
source=ipx2100,eth0,ipx2100source 
# Source line for wlan-ng Prism2 driver 
source=prism2,wlan0,prism 
# Source line for Cisco (dependent on Cisco driver used) 
source=cisco,eth0,cisco 
# Alternate Source line for Cisco (dependent on Cisco driver used) 
source=cisco_cvs,eth1,wifi0,ciscoxfs 
# Source line for Hermes based cards (Orinoco) 
source=orinoco,eth0,orinocosource
```

除非你计划启用多个源，否则无需更改 `enable-sources` 变量，除非更改，否则该变量被注释掉。

默认情况下，Kismet 会跳频（hops channels）。这使得 Kismet 能够检测在 2.4GHz 频段不同信道上工作的接入点。除非你只想检测特定信道上的接入点，否则应保持此设置不变：

```
# Do we channelhop 
channelhop=true
```

如果你想识别特定信道上的接入点，请禁用跳频并在 `source` 变量中设置初始信道。例如，仅识别信道 8 上的接入点：

```
source=hostap,wlan0,wlan,8 
channelhop=false
```

下一个需要调整选项是信道速度（channel velocity）。它控制 Kismet 每秒应循环多少个信道。默认设置为每秒三个信道。这是一个可接受的，尽管保守的选项。要增加 Kismet 跳频的速度，请增加此数字。要降低速度，请减少此数字：

```
# How many channels per second do we hop? (1-10)
# The following option scans each channel for 1/5 of a second
channelvelocity=5
# The following option scans each channel for 1/2 of a second
channelvelocity=2
```

跳频和 GPS 配置之间的选项默认设置正确，通常不需要编辑。如果你使用 GPS 单元来捕获报告坐标，则应设置 GPS 配置选项。除非更改端口，否则 GPSD 监听端口 2947；因此，`kismet.conf` 中 GPS 的选项应设置为反映此情况：

```
# Do we have a GPS?
gps=true
# Host:port that GPSD is running on. This can be localhost OR remote!
gpshost=localhost:2947
```

下一个需要查看的选项是日志文件的写入间隔。默认设置是每 5 分钟写入一次日志。对于随意的驱动漫游，这可能是可以接受的；但是，对于专业人士，在系统或程序崩溃的情况下定期写入日志是个好主意（每分钟是一个安全的选择）：

```
# How often (in seconds) do we write all our data files (0 to disable)
writeinterval=60
```

Kismet 生成非常全面的日志文件集，如表 1.1 所示。

## 表 1.1 Kismet 日志文件类型

| 文件类型 | 描述 |

|---|---|

| Dump | 原始数据包转储，可以在 Ethereal 或其他数据包分析器中打开。 |

| Network | 列出已检测到的网络的文本文件。 |

| CSV | 检测到的网络的逗号分隔列表 |

| XML | 检测到的网络的可扩展标记语言（XML）格式日志。这对于导入其他应用程序很有用。 |

| Weak | 以 AirSnort 格式检测到的弱初始化向量（IV）数据包。 |

| Cisco | Cisco 设备产生的 Cisco 发现协议（CDP）广播日志。 |

| GPS | 检测到的接入点的 GPS 坐标日志。 |

`logtypes` 变量告诉 Kismet 您希望它生成哪些类型的日志文件。默认选项是可接受的（`dump`、`network`、`csv`、`xmll`、`weak`、`cisco` 和 `gps`）；但是，您可能并不需要所有这些。您应该确保生成的最少日志类型是 `dump`、`network` 和 `gps` 日志：

```
logtypes=dump,network,gps
```

`logdefault` 变量指定应在日志文件名前添加什么文本。Kismet 以 `[logdefault]-[date]-[sequence-number].[filetype]` 的格式写入文件。例如，如果 `logdefault` 设置为 Roamer，那么当天第三次漫游（wardriving）会话的 `gps` 日志将被命名为 Roamer-Oct-14-2006-3.gps。如果您在同一天内漫游多个区域，此选项有助于对结果进行排序：

```
# Default log title
logdefault=MyCustomer
```

您可能想要修改 `kismet.conf` 文件中的最后一个选项是 `logtemplate`。此选项控制日志的创建和存储位置以及日志文件的格式。如果未对此变量进行任何修改，日志将以默认格式、默认标题创建在启动 Kismet 的目录中。然而，将所有日志存储在一个位置，或者将不同类型的日志存储在不同的目录中可能更有益。与 `logtemplate` 相关，有七个可以设置的变量：

- `%t` 是 `logdefault` 中设置的标题
- `%d` 是当前日期，格式为 月-日-年 (Mon-DD-YYYY)
- `%D` 是当前日期，格式为 YYYYMMDD
- `%f` 是日志开始的时间
- `%i` 是日志的增量编号（即当天的第一个日志为 1，第二个为 2，等等）
- `%l` 是日志类型
- `%h` 是主目录

例如，如果您希望日志按文件类型生成在不同的目录中，并且创建在 wardrives 目录中，您应有如下 `logtemplate`：

```
logtemplate=WarDrives/$1/%n-%id
```

假设您将 `logtypes` 变量设置为 `dump`、`network` 和 `gps`，您将需要创建一个 `wardrives` 目录，其中包含三个子目录：`dump`、`network` 和 `gps`。

在进行任何更改后，保存文件，您就可以使用 Kismet 进行漫游了。

### 使用 Linux 和 Kismet 进行漫游

使用 Kismet 进行漫游有很多理由。您可以生成的日志文件范围非常广泛，这使得它极具吸引力。与其他一些漫游软件不同，Kismet 不仅检测访问点，还保存其所看到的所有数据包的完整日志。这些转储可以用其他数据包分析器打开，也可以馈入渗透测试程序。监听模式允许您识别隐藏的访问点（未通过 SSID 广播的）。此外，由于客户端通过网络进行身份验证时 SSID 是以明文形式发送的，Kismet 通常可以确定这些隐藏网络的 SSID。

现在，我们已经根据喜好调整了 Kismet 配置文件，准备好使用 Kismet 开始漫游了。在本节中，您将学习如何启动 Kismet，以及运行后如何使用 Kismet 界面。我们来看看 Kismet 提供的不同选项，以及如何为 Kismet 使用图形前端。

#### 启动 Kismet

启动 Kismet 相对简单。假设 Kismet 在您的路径中，在命令行中输入 `kismet`，如图 1.5 所示。

### 图 1.5 启动 Kismet……这里有个问题

![](img/d6ac176c353d2b7687c1186a140180a1_39_0.png)

进程 ID 文件（`pidfile`）无法设置。这是因为您没有权限写入 `/var/run`。有两种方法可以修复此问题。您可以更改 `kismet.conf` 中 `pidfile` 写入的位置：

```
# Where do we store the pid file of the server?
piddir=/home/roamer
```
