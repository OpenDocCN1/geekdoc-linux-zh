
文件包含两个主要指令：

- `ignore` 使 Swatch 忽略匹配正则表达式的日志项。
- `watch` 在日志匹配正则表达式时执行一系列操作。

表 13-2 总结了 Swatch 支持的动作。请查看 man 页获取语法。

| 动作 | 描述 |
| --- | --- |
| bell | 终端响铃。 |
| continue | 执行当前块的操作后，使 Swatch 尝试匹配后续模式。 |
| echo | 将匹配行打印到 stdout。该指令支持多种颜色和模式。 |
| exec | 使用提取的字段执行 shell 命令。 |
| mail | 发送包含匹配行的电子邮件。 |
| pipe | 将匹配行通过到一个命令。 |
| quit | 使 Swatch 终止。 |
| throttle | 限制关联模式匹配的频率。 |
| write | 使用 write 命令向指定用户发送匹配行。 |

默认情况下，Swatch 监控 `/var/log/messages` 文件。然而，你可以使用 `-t` 标记指示 Swatch 监控另一个文件。详情请参 man 页面。要监控多个日志文件，请同时运行多个 Swatch 实例。只需适当调整 SysVinit 文件即可。

## 使用 SWATCH

启动 Swatch 后，以 root 身份登录，或执行另一个触发 Swatch 配置文件中规则的操作。几秒钟后，Swatch 应该会执行与规则相关的操作。

如果 Swatch 工作不正常，请停止服务。然后，通过执行如下命令交互式运行 Swatch：

```
/usr/bin/swatch -c /etc/swatch.conf -f filename
```

其中 `filename` 是你想要分析的日志文件名。Swatch 对文件进行一次扫描，而不是持续运行。你可以反复调整 Swatch 配置并执行此命令，直到配置正确。

## 网络监控

除了监控系统日志外，你应该更广泛地监控网络状态。主机被入侵的迹象可能是网络流量意外激增，或者主机或服务不可用。在本节中，我将描述两个用于网络监控的工具。

### NetSaint

NetSaint 是一个用于监控主机和网络的灵活工具，能够监控服务的可用性和资源使用情况（如处理器负载和磁盘使用率）。通过 NetSaint 的 Web 界面，你可以查看系统状态，如图 13-1 所示。NetSaint 还可以生成实时警报，可以通过电子邮件、传真机或用户定义的方法递送。NetSaint 的监控和通知是可以自定义的，因此你可以根据任何需求对其进行调整。

从 NetSaint 菜单中，你可以选择大约五个六个显示和报告中的任何一个。“概述”`Overview`显示显示了每个可能的状态类别中的主机和服务的数量。它还显示了哪些标记、通知、事件处理程序检查处于激活状态。最后，在“网络健康”`Network Health`部分，彩色条可以一目看出主机和服务的整体状态。

## 第 13 章：管理防火墙

![](img/0f69b2a8749a24b957044e9f26f2d5b4_418_0.png)

图 13-1：NetSaint 主屏幕和菜单

![](img/0f69b2a8749a24b957044e9f26f2d5b4_418_1.png)

图 13-2：策略概述显示

NetSaint 可以显示详细的状态信息，也可以显示摘要状态信息。图 13-3 显示了“状态详情”`Status Detail`视图，它呈现了每个主机和服务的当前状态。显示显示了最后检查服务可用性的时间以及服务可用的时间段。主机和服务的名称是链接，让你能够深入查看更详细的信息。

### 390 第三部分：防火墙操作

![](img/0f69b2a8749a24b957044e9f26f2d5b4_419_0.png)

图 13-3 显示了“主机趋势”`Host Trends`显示，这是一个显示影响主机的事件时间和持续时间的条形图。显示可以配置为显示特定感兴趣的时间段。显示还报告了主机处于在线、宕机、不可达或不确定状态的时间百分比。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_419_1.png)

图 13-4：主机趋势细分

通过查看“可用性”`Availability`显示你可以快速查看网络上所有主机的运行记录，如图 13-5 所示。此显示了每个主机在在线、宕机、不可达和不确定状态类别中花费的时间。报告周期是用户可选的，就像“主机”显示一样。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_420_0.png)

图 13-5：可用性显示

“警报历史”`Alert History`显示如图 13-6 所示，记录了 NetSaint 发出的警报。你可以使用该显示来验证你是否收到了 NetSaint 发出的所有警报。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_420_1.png)

图 13-6：警报历史显示

### 第三部分：防火墙操作

> **提示：如所述，NetSaint 除了提供的之外，还有几个额外的显示和选项。请访问 NetSaint 网站 http://www.netsaint.org/ 查看其他显示的示例。**

#### 安装 NetSaint

你可以通过 NetSaint 网站获取 NetSaint RPM 文件，该网站包含指向 FTP 服务器的链接，你可以从那里下载它们。你需要这些包：

- `netsaint`
- `netsaint-plugins`
- `netsaint-www`

除了 NetSaint 之外，你通常还应该安装以下包：

- `apache`
- `gd`
- `gd-devel`

如果你不想查看基于 NetSaint 的显示，可以忽略 `netsaint-www`。然而，取决于你的配置，你可能需要额外的包。

#### 配置 NetSaint

NetSaint 使用三个配置文件：

- 主配置文件，`/etc/netsaint/netsaint.cfg`
- 主机配置文件，`/etc/netsaint/hosts.cfg`
- CGI 配置文件，`/etc/netsaint/ncgi.cfg`

主配置文件和 CGI 文件通常不需要任何更改。如果需要，请参阅 NetSaint 网站上的文档。

## 第 13 章：管理防火墙

在主机配置文件中，你必须指定你想让 NetSaint 监控的主机和服务。遵循以下通用步骤：

1. 配置一个或多个主机组。
2. 为每个主机组配置一个或多个主机。
3. 配置一个或多个联系人组，每个组代表一组接收警报的人员。
4. 为每个联系人组配置一个或多个联系人。
5. 为每个主机配置一个或多个服务。

在你修订配置文件后，执行命令检查配置：

```
/usr/sbin/netsaint -v /etc/netsaint/netsaint.cfg
```

#### 运行 NetSaint

要启动 NetSaint，首先确保 http 服务正在运行，如有必要请启动它。然后，执行命令：

```
service netsaint start
```

你应该能够通过 URL `http://host.domain/netsaint/` 访问 NetSaint，其中 `host.domain` 是运行 NetSaint 的主机主机名和域名。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_422_0.png)

因为 NetSaint 是一个 CGI 程序，它可能——而且很——存在安全漏洞。你应该配置你的 Web 服务器，阻止不可信主机访问 NetSaint 目录。你还应该使用 `htpasswd` 限制授权用户访问 NetSaint。

### MRTG

多路由器流量图表 `MRTG` 是 Red Hat Linux 发行版的一部分，它可以让你通过 浏览器方便地可视化穿越交换机和路由器的流量。图 13-7 显示了典型的 MRTG Web 页面顶部。除了日图外，MRTG 还提供了几个额外的图表：

- 周
- 月 月
- 年度

使用 MRTG，你可以轻松发现流量的意外激增。此类激增可能指示入站或出站扫描活动或其他与网络安全的情况。

### 394 第三部分：防火墙操作

![](img/0f69b2a8749a24b957044e9f26f2d5b4_423_0.png)

图 13-7：MRTG Web 页面

#### 配置 MRTG

配置 MRTG 最简单的方法是使用 `cfgmaker` 程序。执行此操作，执行命令：

```
/usr/bin/cfgmaker --global WorkDir: '/var/www/html/mrtg/' \
  --global 'Options[_]: bits.growright' \
  --output /etc/mrtg/conf \
  community@router.domain
```
