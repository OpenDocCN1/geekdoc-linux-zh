
| | |
| --- | --- |
| *Monitor* | 通过接受来自 VantagePoint Performance 的警报来提供警报监控功能，并显示警报。 |
| *Planner* | 通过外推 VantagePoint Performance 数据进行预测，从而提供预测功能。 |
| *Analyzer* | 分析来自多个系统的 VantagePoint Performance 数据并显示数据。您可以同时查看来自多个系统的数据。 |

在我们的示例中，我们将针对单个系统进行操作。我们将获取在大约一周时间内收集的 VantagePoint Performance 数据，并展示其中的一部分。在这个示例中，我们不会从多个分布式系统获取数据，并且在该示例中仅使用一台服务器。

HP VantagePoint Performance 代理程序生成包含系统资源消耗信息的日志文件。HP VantagePoint Performance 代理程序运行时间越长，它在日志文件中记录的数据就越长。我经常被要求审查运行状况不佳的系统，并提出系统升级建议。我通常运行 HP VantagePoint Performance 代理程序至少一周，以便在足够长的时间段内获取日志信息，从而获得有用的数据。对于一些系统而言，这段时间可能是数月。对于负载规律的其他系统，一周可能已经足够。

在运行 VantagePoint Performance 一周后，我调用了 VantagePoint Performance Analyzer/UX 来查看这一周内发生的系统资源利用率水平。我们将查看的图表包括 CPU、内存和磁盘。图 12-11 显示了一周的全球 CPU 摘要：

![](img/eff8b9287a5f38c5adf538f24aacf29e_836_0.png)

图 12-11 全球 CPU 摘要界面

您可以使用 VantagePoint Performance Analyzer/UX 调整该图表的几乎所有可想象的特征。不幸的是，书中的这张图表丢失了颜色。所使用的颜色使您在计算机屏幕上查看图表时能够识别参数。总 CPU 利用率始终是图表中的最高点，它是系统模式和用户模式利用率的总和。

图 12-11 展示了经典的 CPU 利用率，主要时段反映了高 CPU 利用率，非主要时段反映了低 CPU 利用率。然而，在某些方面，这个图表可能会产生误导。由于每三个小时会出现一个数据点，因此每个 24 小时周期有八个小刻度，您无法看到在更短时间窗口内的实际 CPU 利用率。例如，我们无法准确看到 CPU 在早上何时变得负载严重。我们可以看到它是在第二个和第三个刻度之间，但这是一段很长的时间 - 在上午 6:00 到 9:00 之间。在一天结束时也存在同样的缺乏细粒度的问题。我们可以看到 CPU 利用率在第五和第七个刻度之间明显下降，但这并没有给我们一个清晰的视图。

图 12-12 显示了在更短时间窗口内的 CPU 利用率。

![](img/eff8b9287a5f38c5adf538f24aacf29e_837_0.png)

图 12-12 全球 CPU 摘要 - 短时间周期

图 12-12 显示了在更短时间窗口内更细粒度的 CPU 利用率。这种更细粒度的窗口使人们清楚地看到全天发生的活动高峰。例如，在上午 8:30 出现了一个明显的登录高峰。

内存利用率也可以在整周期间以图表形式显示，如图 12-13 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_838_0.png)

用户内存利用率是图表的底线，大致对应于前面显示的 CPU 利用率。在非主要时段，用户内存利用率较低，而在主要时段较高。

系统内存利用率是图表的中间线，在一周内保持相对稳定。

总内存利用率始终是图表的顶线，它是系统利用率和用户利用率的总和。由于系统内存利用率大致保持不变，它随用户利用率的升降而升降。

此图表上数据点之间三个小时的间隔可能无法提供我们所需的细粒度。图 12-14 显示了在更短时间窗口内的内存利用率。

![](img/eff8b9287a5f38c5adf538f24aacf29e_839_0.png)

图 12-14 全球内存摘要 - 短时间周期

图 12-14 显示了在更短时间窗口内更细粒度的内存利用率。现在您可以精确地看到内存利用率在大约一天的时间内是如何变化的。

磁盘利用率也可以在整周期间以图表形式显示，如图 12-15 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_840_0.png)

图 12-15 全球磁盘摘要

与 CPU 和内存图表一样，这是一整周的磁盘使用情况。由于该图表上出现了许多峰值，我们肯定希望查看和分析更短的时间窗口。

图 12-16 显示了在更短时间窗口内的磁盘利用率。

![](img/eff8b9287a5f38c5adf538f24aacf29e_841_0.png)

图 12-16 全球磁盘摘要 - 短时间周期

这个大约三小时的更短时间窗口显示了更多的细节。在深夜出现了巨大的磁盘活动峰值。这些可能由多种原因引起，包括批处理作业处理或系统备份。

您不仅可以一次查看与单个系统资源相关的参数。您还可以同时查看许多系统资源的使用方式，如图 12-17 所示。

![](img/eff8b9287a5f38c5adf538f24aacf29e_842_0.png)

图 12-17 全球摘要历史界面

该图表包含许多系统资源，包括 CPU、磁盘和内存。当同时显示如此多的系统资源时，您肯定希望查看更短的时间段。

图 12-18 显示了在更短时间窗口内的相同参数。

![](img/eff8b9287a5f38c5adf538f24aacf29e_843_0.png)

图 12-18 全球摘要 - 短时间周期

图 12-18 显示了在更短时间窗口内许多系统资源利用率的更细粒度。现在您可以查看各种系统资源与其他系统资源之间的关系。

您可以通过一个名为 **perfstat** 的实用命令找到在您的系统上运行的 VantagePoint Performance Analyzer/UX 的状态。以下示例展示了使用“-?”选项发出 **perfstat** 命令以查看所有 **perfstat** 选项：

```
# perfstat -?

usage: perfstat [options]

Unix option Function
-? List all perfstat options.
-c Show system configuration information.
-e Search for warnings and errors from
   performance tool status files.
-f List size of performance tool status files.
-p List active performance tool processes.
-t Display last few lines of performance tool
status files.
-v List version strings for performance tool files.
-Z Dump perfstat info to a file and tar tape.
```

使用 `-c` 选项，您可以获取有关系统配置的信息，如下面的列表所示：

```
# perfstat -c

********************************************************************
** perfstat for rp ux6 on Fri May 15 12:20:06 EDT
********************************************************************

system configuration information:

uname -a: HP-UX ux6 B.11.00 E 9000/800 71763 8-user license

mounted file systems with disk space shown:
Filesystem          kbytes    used    avail %used Mounted on
/dev/vg00/lvol3     85016    27675  54736  34% /
/dev/vg00/lvol1     67733   44928  16031  74% /stand
/dev/vg00/lvol8    163840   56995  90927  42% /var
/dev/vg00/lvol7    497712  358775 132155  73% /usr
/dev/rp06vg tmp /tmp       4319777 1093927 3134084 26% /tmp
/dev/vg00/lvol6     270336  188902  76405  71% /opt
/dev/vg root1/ var   640691   15636  605834   3% /newvar
/dev/vgroot1/usr    486677  356866 115210  76% /newusr
/dev/vgroot1/stand  677733   45109  58580  74% /newstand
/dev/vgroot1/root    83733   21181  54178  28% /newroot
/dev/vgroot1/opt     263253  188109  67246  74% /newopt
/dev/vg00/lvol15     20480     119   8168   6% /home

LAN interfaces:
Name           Mtu        Network       Address       Ipkts     Opkts
lo0            4136      127.0.0.0     localhost     77442     77442
lan0           1500      192.60.11.0   rp-ux6       7847831   12939169

********************************************************************
           (end of perfstat -c output)  *************
```

使用 `-f` 选项显示性能工具状态文件的大小，如下面的列表所示：

