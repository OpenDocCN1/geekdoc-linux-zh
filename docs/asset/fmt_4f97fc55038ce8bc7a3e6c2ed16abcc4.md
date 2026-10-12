
| 基础主题 | 本节题目 |
| :--- | :--- |
| `collectd` 守护进程 | 1, 2 |
| 监控解决方案 | 3, 4 |
| 现在如何？ | 5 |

1. 使用哪个工具来收集数据？
   a. `statd`
   b. `datad`
   c. `collected`
   d. `top`

2. 使用 ____ 来确定它收集的内容。
   a. 数组 (`array`)
   b. 插件 (`plugin`)
   c. 切换器 (`toggle`)
   d. 开关 (`switch`)

3. 下哪个项可以与 `collectd` 协同工作？
   a. `Nagios`
   b. `MRTG`
   c. `Cacti`
   d. `RRDtool`

4. 下哪个项是 `collectd` 的前端工具？
   a. `Nagios`
   b. `MRTG`
   c. `Cacti`
   d. `sar`

5. 真或否：你应该始终离开监控。

## `LPIC-2C` 认证指南

在大多数情况下，你不太可能会修改任何全局设置。最重要的配置更改通常是在插件上执行的。你在此文件中可能的操作是启用或禁用这些插件。例如，考虑来自 `/etc/collectd/collectd.conf` 文件的以下部分：

```
LoadPlugin df
LoadPlugin disk
#LoadPlugin dns
```

该文件的这部分用于告诉 `collectd` 监控哪些统计数据。在上一个示例中，`df` 和 `disk` 插件已启用，而 `dns` 插件未启用。你可能想知道这些不同的插件实际上是做什么作用的。在大多数情况下，你可能猜出来；然而，你不需要猜测，因为文档页面列出了所有这些插件：`https://collectd.org/wiki/index.php/Table_of_Plugins`。以下是根据文档描述对 `df`、`disk` 和 `dns` 插件的说明：

- `df`—D 插件收集文件使用信息，即基本上是挂载分区上使用了多少空间，以及剩余多少空间。它以长久以来存在的 `df(1)` UNIX 命令命名，且与其非常相似。(`https://collectd.org/wiki/index.php/Plugin:DF`)
- `disk`—Disk 插件收集硬盘的性能统计，在支持的情况下还收集分区的统计。(`https://collectd.org/wiki/index.php/Plugin:Disk`)
- `dns`—DNS 插件的功能与 `dnstop` 类似：它使用 `libcap` 获取所有发往 UDP/53 端口（DNS 端口）的流量副本，解析包并收集你的 DNS 流量统计数据。它监听的接口以及是否应该收集由主机自身发送的数据包，可以在配置文件中设置。(`https://collectd.org/wiki/index.php/Plugin:DNS`)

你不需要为了示例记住所有的插件，你应该检查配置文件并确定你真正想要收集什么数据。请记住，每个插件都需要额外的系统资源。为了节省系统资源，请对你不需要使用的插件进行注释（`comment out`）处理。

对于你启用的插件，每个插件都可以进行不同的配置。例如，要配置 `df` 插件，你需要修改示例 2-1 所示的 `/etc/collectd/collectd.conf` 文件中的以下部分。

### 示例 2-1 配置 `df` 插件

```
<Plugin>
# Device "/dev/sda1"
# Device "192.168.0.2:mnt/nfs"
# MountPoint "/home"
# FSType "ext3"

# 忽略 rootfs，根守护进程文件系统会出现两次，导致
# 其中一次更新失败并大量刷日志
FSType rootfs
# 忽略常见的虚拟 / 临时文件系统
FSType sysfs
FSType proc
FSType devtmpfs
FSType devpts
FSType tmmpfs
FSType fusectl
FSType cgroup
IgnoreSelected true
# ReportByDevice false
# ReportReserved false
# ReportInodes false

ValuesAbsolute true
# ValuesPercentage false
</Plugin>
```

`注意：` 对于考试来说，你不需要知道如何修改特定的插件，但如果你在实际情况中使用 `collectd`，你应该研究每个插件的文档并根据你的需求进行更改。

## 安装 `collectd`

如前所述，`collectd` 守护进程主要用于收集数据。如果你真的想使用这些数据，你还应该安装一个工具来查看数据图表。有很多此类工具；你可以在这里找到这些工具的列表：`https://collectd.org/wiki/index.php/List_of_front-ends`。

以下示例是在 `Ubuntu` 系统上执行的。安装并配置了五个工具：`collectd`、`lighttd`（一个 Web 服务器）、`PHP`、`git` 和 `CGP`（一个基于 `PHP` 的提供 `collectd` 数据图表的 Web 应用）。

- `第 1 步.` 安装 `collectd`、`lighttd` 和 `PHP`：
  `sudo apt-get install lighttd php5-cgit`

- `第 2 步.` 通过编辑 `/etc/php5/cgi/php.ini` 文件并取消以下行的注释（删除前面的分号），在 `lighttd` Web 服务器中启用 `PHP`：
  `cgi.fix_pathinfo=-1`

- `第 3 步.` 在 `lighttd` 中启用 `CGI` 并启动 `lighttd`（注意：只有在你已经运行了 `Apache` Web 服务器的情况下，才需要第一行）：
  `sudo service apache2`
  `sudo lighttd-enable-mod fastcgi`
  `sudo lighttd-enable-mod fastcgi-php`
  `sudo service lighttd start`

- `第 4 步.` 使用 `git` 工具下载 `CGP`：
  `cd /var/www`
  `git clone http://git.nethuis.nl/pub/cgp-git`

到此时，你应该已经正确安装并运行了一切。收集守护进程应该已经自动启动。你可以通过打开浏览器并输入 URL：`http://localhost/cgp/` 来查看图表。结果应该像图 2-1 所示。

![](img/a76ac3bb017d749781a228f025853f37_67_0.png)

`图 2-1` `collectd` 结果

## 监控解决方案

本章涵盖的考试目标之一是“对 `Nagios`、`MRTG` 和 `Cacti` 等监控解决方案的了解”。请记住，“了解”意味着你知道它们是做什么的。考虑到这一点，以下是你应该关于这些解决方案了解的内容。

### `Nagios`

这是一个自 1999 年以来就存在的项目。事实上它不是一个单一的产品，而是一个产品集合，包括：

- `Nagios XI`（监控包）
- `Nagios Server`
- `Nagios Network`
- `Nagios Manager`
- `Nagios Core`

### `MRTG`

`MRTG` 代表 `Multi Router Graph`，一种主要用于监控流量的工具。正如其名称所示，它从路由器读取流量并为未来记录这些信息。你可以通过网页查看这些数据。

### `Cacti`

另一个开源项目，`Cacti` 也专注于监控。它主要是是 `RRDtool`（轮询数据库）的前端工具。`Cacti` 提供了一个查看 `RRDtool` 提供数据的易用界面。

### `sar`

你忘记第一章的 `sar` 吗？请记住 `sar` 可以提供一段时间内的 CPU 和磁盘使用统计数据。与这些大多数工具相比，它还有一个优势，因为它是发行版的一部分。尽管它不提供华丽的图表，但在急需时它可以发挥作用。

## 进一步考虑

虽然考试目标只提到了三个工具，但实际上有几十种工具可用。对于考试，你应该了解本章提到的那三个。在现实生活中，在实施任何这些工具之前，你真的应该探索可用工具。在做决定之前，你应该考虑许多因素，包括但不限于：

- 该工具提供什么级别的支持？
- 它是完全开源的还是某些功能需要付费？
- 该工具的灵活性如何？
- 安装方便吗？配置方便吗？升级方便吗？
- 重要：它为你的系统增加了多少开销？
- 非常重要：它的安全性如何？

还有其他点需要考虑，但这些让你对实施系统监控解决方案应该投入多少精力有了良好的了解。这是一个关键决定……请明智选择！

## 好了，现在怎么办？

如果你想利用这些工具提供的功能，应该采取以下一些关键步骤：

- 确定你需要测量什么。如果你对这个问题的答案是“所有”，你真的需要重新考虑。思考一下对于这个系统来说什么是潜在问题。如果是一个邮件服务器，那么网络流量和 `/var` 分区的磁盘空间使用情况可能是关键的。CPU 和内存使用可能没那么关键。

## 第 2 章：预测未来资源需求
