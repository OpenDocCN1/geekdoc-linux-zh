
## 10 监控与性能调优

在本章中，我们将探讨以下主题：

- 调优系统性能
- 设置 PCP – Performance Co-Pilot（性能辅助）
- 监控基础系统性能
- 监控 CPU 性能
- 监控 RAM 性能
- 监控存储性能
- 监控网络性能

### 引言

监控基础设施是环境的一个重要方面，它可以让你了解它的运行行为。它会告诉你瓶颈在哪里，以及有哪些改进空间。在本章中，我们将监控性能，并在某些指标超过特定值时创建触发器。

## 调优系统性能

公司购买他们能获得的最好的硬件，并希望优化地使用一切。然而，让应用程序运行得快的不仅仅是硬件。你的操作系统在特定情况下表现也会不同。

`Tuned` 是一套工具和一个守护进程，它可以根据使用情况自动调优系统设置。它通过插件定期从组件收集数据，并根据当前用法更改系统设置。

### 如何操作...

在本教程中，我们将询问要使用哪个配置文件，并通过以下步骤进行应用：

1. 运行以下命令安装所需的包：
   `yum install -y tuned`
2. 通过执行以下命令启用并启动 `tuned`：
   `systemctl enable tuned`
   `systemctl restart tuned`
3. 通过以下操作让 `tuned` 猜测要使用的配置：
   `tuned-adm recommend virtual-guest`
4. 最后，按照如下方式将推荐的配置应用于 `tuned`：
   `tuned-adm profile virtual-guest`

### 更多...

你可以在 `/lib/tuned/` 中找到系统的 `tuned` 配置文件。当你创建自己的时，按照 `/lib/tuned` 中的组织方式在 `/etc/tuned/` 中创建。我不建议在 `/etc/tuned` 中创建与 `/lib/tuned` 同名的新配置，但如果你这样做，将使用 `/etc/tuned` 中的那个。最好创建一个不同名称的新配置，包括你想修改的。每个配置都有一个目录，包含一组控制系统行为的文件。如果你查看这些目录下的 `tuned.conf` 文件，你会发现这些文件定义了其他工具（如 `cpufreq`）所需的设置。例如，如果你为笔记本创建配置，应用 `powersave` CPU 调优器会好一点，你可以在 `/etc/tuned/` 创建新文件，内容如下：

```
# laptop tuned configuration

#

[main]

include=desktop

[cpu]

replace=1

governor=powersave
```

当你知道系统的瓶颈时，可以通过特定方式配置你的系统来缓解它们。使用 `tuned` 创建并应用基于组件监控的配置非常方便。

### 另请参见

有关调优系统的更多信息，请参考[红帽性能调优指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Performance_Tuning_Guide/index.html)。

查看 `tuned (8)`、`tuned-adm (8)`、`tuned-main.conf (5)` 和 `tuned-conf (5)`。

## 设置 PCP – Performance CoPilot

多年来，创建了许多工具来排查系统性能问题，例如 `top`、`sar`、`iotop`、`vmstat`、`dstat` 等。然而，这些工具中没有相互集成，有些是扩展。

`PCP` 似乎有几个功能：监控系统的各个方面，允许集中存储（性能）数据，并允许不仅使用实时数据，还使用保存的数据。

### 如何操作...

在本教程中，我们将查看“默认”设置和“收集器”配置，允许你获取所需的所有性能数据。

#### 默认安装

这是 `PCP` 的基础设置：

1. 安装必要的包；运行以下命令：
   `yum install -y pcp`
2. 现在，按照如下方式启用并启动守护进程：
   `systemctl enable pmcd`
   `systemctl enable pmlogger`
   `systemctl start pmcd`
   `systemctl start pmlogger`
3. 如果你想让中央收集器监控系统，执行：
   `firewall-cmd --add-service pmcd --permanent`

#### 中央收集器

每个作为收集器的主机都需要额外的配置。方法如下：

1. 在 `/etc/pcp/pmlog/control` 中为每个系统添加一行来收集数据：
   `<hostname> PCP_LOG_DIR/pmlog/<hostname> -r T24h10m -c config.<hostname>`

在这里，`<hostname>` 是主机的完全域名 (FQDN)。参考以下示例：
`guest.example.com PCP_LOG_DIR/pmlog/guest.example.com -r T24h10m -c config.example.com`

2. 添加后，你需要重启 `pmlogger`：
   `systemctl restart pmlogger`

### 更多...

默认情况下，`PCP` 每 60 秒记录一次。如果你想将统计频率增加到 30 秒，你需要更改 `/etc/pcp/pmlog/control` 中的配置。修改统计数据有点困难。如果你想可视化数据，需要安装 `pcp-gui`：

```bash
yum install -y pcp-gui
```

该包带有一个名为 `pmchart` 的工具，允许创建图形。有关 `PCP` 及其组件的更多信息，请参考它们的在线手册。

## 监控系统性能

我们需要关注全局系统值。特别重要的有：

- `kernel.all.pswitch`
- `kernel.all.nprocs`
- `kernel.all.load`

### 另请参见

更多信息请参考[红帽性能调优指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Performance_Tuning_Guide/index.html)。

### 如何操作...

我将向你展示一种显示文本和图形输出的方法。

1. 通过执行以下命令以 1 秒为间隔显示指标的实时数据：
   `pmstat -c 1`

2. 为 `pmchart` 创建一个显示实时数据的配置文件 `system.conf`，内容如下：

```
#pmchart
version 1

chart style plot antialiasing off

plot color #ffff00 metric kernel.all.pswitch

chart style plot antialiasing off

plot color #ffff00 metric kernel.all.nprocs

chart style plot antialiasing off

plot color #ffff00 metric kernel.all.load instance *1

plot color #ff924a metric kernel.all.load instance *5

plot color #ff0000 metric kernel.all.load instance *15
```

3. 下一步，使用以下命令通过 `pmchart` 为 `guest.example.com` 绘制实时图表：

```bash
pmchart -h guest.example.com -c system.conf
```

![](img/a6dbf7df749be83c0faae2334e970c0b_961_0.png)

### 更多内容...

之前的示例是基于“实时”数据的；然而，你并不局限于实时数据。你可以通过增加 `pmlogger` 的间隔来获取更多关于故障系统的数据，之后查看生成的数据。使用其他工具时，你必须通过 cronjob 等方式使用额外的工具，而 `PCP` 允许你同时完成这两种操作。

### 补充操作示例

以下是操作方法：

1. 通过以下命令显示 `guest.example.com` 在 2015 年 11 月 1 日 15:30 到 16:30 之间、间隔为 5 分钟的数据：

```bash
pmdumptext -H -t -m -1 -S @15:30 -T @16:30 kernel.all.pswitch kernel.all.nprocs kernel.all.load -a /var/log/pcp/pmlogger/guest.example.com/20151101
```
