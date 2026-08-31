
# 在 Ubuntu 20.04 上安装 vnStat 的教程

> 原文：<https://blog.eldernode.com/install-vnstat-on-ubuntu-20-04/>

![Tutorial Install vnStat on Ubuntu 20.04](img/ec95ea5167bbf75af0a6289c00606a39.png)

`vnStat`（**v**iew **n**etwork **Stat**istics）是一款用于网络流量监控的命令行工具。它使用简单的控制键，帮助您记录和查看不同时间段的网络统计数据。这个网络实用程序用于 Linux 操作系统，是一个基于控制台的网络流量监视器。由于流量信息是从 `/proc` 文件系统中分析的，因此可以在没有 root 权限的情况下使用`vnStat`。通过`vnStat`，您可以以详细表格或命令行统计视图的形式查看每小时、每天、每月的统计信息。请阅读本指南，了解在 Ubuntu 20.04 上安装`vnStat`的完整教程。如需购买全面管理且价格低廉的 [Ubuntu VPS](https://eldernode.com/ubuntu-vps/)，请选择一个软件包或通过 [Eldernode](https://eldernode.com/) 联系我们。

## 如何在 Ubuntu 20.04 上一步步安装 vnStat

作为开发人员或系统管理员，您需要监控网络流量或带宽使用情况，以监控共享互联网带宽的各种系统上的流量。`vnStat` 可以帮助您监控各种网络参数，如带宽消耗以及流入和流出的流量。本文将详细介绍`vnStat`，它是能够实现上述功能的工具之一，并将教授在 [Ubuntu](https://blog.eldernode.com/tag/ubuntu/) 20.04 上安装`vnStat` 的过程。

### vnStat 特性

以下是使用`vnStat` 的最重要优势：

- 同时监控多个网络接口
- 安装和运行快速且简单
- 收集的统计数据在系统重启后仍然存在
- 提供多种输出选项
- 数据保留期限完全由用户动态配置
- 可以将月份配置为遵循计费周期
- 轻量级，资源占用极少
- 无论流量如何，CPU 使用率都保持较低水平
- 无需 root 权限即可使用
- 支持在线颜色配置编辑器

## 在 Ubuntu 20.04 | Ubuntu 18.04 上安装并配置 vnStat

`vnStat` 在 Ubuntu 的默认软件源中可用，因此请使用以下命令进行安装。

```
sudo apt update
```

```
sudo apt install vnstat
```

现在，`vnStat` 已安装完毕，可以开始运行。要测试其是否安装成功，可以在终端中输入 `vnstat`。您不会看到类似“找不到 vnstat”的错误。此外，您可以使用以下命令获取所有网络接口的基本统计信息。

```
vnstat
```

### 如何在 Ubuntu 20.04 上启动并运行 vnStat

要确保`vnStat` 正在运行，请使用以下命令：

```
sudo systemctl status vnstat
```

确认`vnStat` 安装且运行正常后，您需要找到并设置希望监控的网络接口。为此，请运行以下命令查看系统上可用的网络接口及其名称列表：

```
ifconfig
```

现在，为了告诉`vnStat` 要监控的网络接口，我们以有线接口 `ens33` 和无线接口 `wlan0` 为例。在终端中输入以下命令：

```
vnstat -u -i ens33
```

通过运行上述命令，您已激活对该接口的监控。如果这是您首次运行，可能会遇到错误：`无法读取数据库"/var/lib/vnstat/ens33"`。您只需忽略该错误即可。

如果您使用 WLAN，请用以下命令设置无线网络接口：

```
vnstat -u -i wlan0
```

运行以下命令，查看系统中所有可用的网络接口：

```
vnstat --iflist
```

现在您已知道所有想要监控的接口。如果对该接口名称使用上述命令，就可以监控其流量。然后，使用以下命令启动`vnStat`守护进程：

```
sudo service vnstat start
```

您可以检查守护进程的状态。要从所有已注册的接口接收每月的总网络流量摘要，请运行以下命令：

```
ps -f | grep vnst
```

使用 `-i` 选项可以监控特定网络接口的基本使用情况。例如，对于`ens33`，命令如下：

```
vnstat -i ens33
```

**注意**：将上述命令中的 `ens33` 替换为任何其他接口名称（如 `eth0` 或 `wlan0`），即可获得该接口的统计信息。在每个表的末尾，`vnStat` 会提供该月的估计网络使用量。您可以将此功能作为`vnStat` 的众多实用特性之一，用于控制带宽使用。

### 如何在 Ubuntu Linux 上使用 vnStat

您可以使用`vnStat` 监控特定时间段和特定接口的流量。此处仍以 `ens33` 为例。

**每小时统计视图**

要以基于控制台的图形和表格形式查看最近 24 小时的使用情况，请运行：

```
vnstat -h -i ens33
```

要获得其他接口的结果，请将 `ens33` 替换为 `eth0` 或 `wlan0`。

**月度统计视图**

使用 `-m` 选项查看每月统计数据：

```
vnstat -m -i ens33
```

**每周统计视图**

使用 `-w` 选项查看接口的每周统计数据：

```
vnstat -w -i ens33
```

### 如何使用 vnStat 生成图形图像

使用`vnStat` 还可以生成以图形形式表示网络流量的图像。要从`vnStat` 创建图形并将其存储在指定位置，需要以下信息。

**单个接口的摘要输出**

使用 `vnStati` 的 `-s` 选项获取特定接口的输出。要获得输出并将其保存为主文件夹中名为 `summary.png` 的图像，请输入：

```
vnstati -s -i ens33 -o ~/summary.png
```

**每小时统计显示**

要获得每小时显示的输出，请使用 `-h` 选项，命令如下。**注意**：显示的内容始终为最近 24 小时的数据。

```
vnstati -h -i ens33 -o ~/summary2.png
```

**累计输出**

此外，结合多个接口的流量分析，可以得到总输出。请参见以下示例和命令。

例如，`eth0+eth1` 通过汇总 `eth0` 和 `eth1` 的统计数据得出流量输出。类似地，您可以添加任意数量的接口，如 `eth0+eth1+eth2` 或 `eth0+wlan0` 等。

```
vnstati -s -i wlan0+eth0 -o ~/summary3.png
```

## 结论

在本文中，您了解了如何在 Ubuntu 20.04 上安装`vnStat`。`vnStat` 为您提供了多种信息，您可以通过监控网络流量来记录、分析和生成准确的结果。如果您有兴趣了解更多信息，请参考我们关于 [Linux 服务器监控命令](https://blog.eldernode.com/linux-server-monitoring-commands/) 的文章。
