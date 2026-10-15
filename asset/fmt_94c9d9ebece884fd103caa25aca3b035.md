
```
/u0/yves/perl5/bin/timedexec /u0/yves/mrtg-2.2/mem postpaid
yves
MaxBytes[mail-mem]: 500000
AbsMax[mail-mem]: 500000
Unscaled[mail-mem]: dymy
```

# 第 24 章 ✦ 信息的消化与总结 497

## 编写用于 MRTG 的自定义脚本

默认情况下，`MRTG` 使用 SNMP 网络请求来收集数据。然而，在列表 24-1 中，我们运行了一个不同的程序，并以 `Target` 关键字命名：一个由我们生成的脚本。这就是 `MRTG` 如此实用的原因之一：你可以编写任何需要的程序或脚本，只要这些程序或脚本符合 `MRTG` 预期约定。与 `MRTG` 使用的脚本必须打印四行输出：

- 1. 第一个变量的当前状态
- 2. 第二个变量的当前状态
- 3. 字符串，告知目标的运行时间（uptime）
- 4. 目标名称

列表 24-2 中的脚本是 `mem`，用于监控系统的空闲内存和空闲交换分区（swap）。该脚本根据列表 24-1 中提供的配置文件了图 24-2 中的图表。我们使用 `vmstat` 作为在远程系统执行的命令，而不是 `sar`，因为对于实时监控，`vmstat` 更适合这项任务。`Sar` 每小时更新一次输出，而 `vmstat` 为我们提供了机器当前状态的快照。

### 列表 24-2：用于 MRTG 的示例 mem 脚本

```sh
#!/bin/sh

#Usage: mem target user

rsh $1 -l $2 vmstat 5 2 | tail -1 | awk '{print $5 "\n" $4}'
rsh $1 -l $2 uptime | awk '{print $3 " " $4}' | cut -f1 -d","
echo $1
```

在图 24-2 中，你可以看到两个不同变量相互绘图的结果。请注意空闲内存和空闲交换分区之间存在的关系。我们使用了来自主路由器的值，因为该交换分区相当繁忙。在这种情况下，曲线越高，表示可用内存越。。灰色曲线代表机器上的空闲内存，黑色曲线代表空闲交换分区。

![](img/c0f2cd6655e598a6e6ffb6a15368bc67_533_0.png)

图 24-2：同一 MRTG 图表上的空闲内存和空闲交换分区

正如你所看到的，这两个变量之间存在巨大的相关性；当空闲内存数量增加时，空闲交换分区数量也随之增加，且两者同时减少。这意味着在该机器上运行的大部分程序启动、完成它们需要做的事，然后消失。许多此类程序被交换出，要么是因为它们处于睡眠状态，要么是因为它们正在等待 I/O 请求完成，我们会看到空闲交换分区曲线下降，而空闲内存曲线没有相应的下降。这意味着我们的机器正在被高效地使用；程序在完成后会迅速消失，而不会随着时间的推移而累积。

图 24-2 中另一个明显的一点是，有时（特别是在白天），我们的空闲内存非常低。作为对此的反应，我们将把运行在这台机器上的 IRC 服务器移动到它自己的机器上。考虑到 IRC 服务器进程占据了约 35MB 内存，其中 26MB 是驻留的（其余的已交换出），这次移动应该让这台机器得到喘息。14:00 显示的空闲内存突然增加，是因为我们重启了机器。这种空闲内存的突然增加可能表明系统运行的某个程序存在内存泄漏。我们在这台机器上只运行了程序：邮件服务器程序（`sendmail`）和 IRC 服务器。如果我们将 IRC 服务器移走后没有看到空闲内存的逐渐下降，那么我们就找到了罪魁祸首。

列表 24-3 显示了另一个用于 `MRTG` 的脚本。该脚本命名为 `cpu`，绘制负载平均图；我们使用它创建了之前所示的图 24-1。

### 列表 24-3：用于 MRTG 的示例 cpu 脚本

```csh
#!/bin/csh

Usage: cpu target user

rsh $1 -l $2 uptime | awk '{
    print $NF, "\n" $(NF-2);
    print $3 " " $4
} | cut -f1 -d

echo $1
```

在列表 24-3 中，我们使用了特殊变量 `NF`。你永远无法假设 `uptime` 命令的输出是恒定的，有时机器是 82 天，有时是 82 分钟；`NF` 是输出的字段数量。为了让脚本更具可读性，我们增加了反斜杠来拆分多个 Unix 风格的输出。该脚本的好处是能够解析 1 分钟和 15 分钟的负载平均值。脚本接受两个参数：主机名（更多细节请见第 23 章）和一个用于登录的用户名。如果我们将 IRC 服务器移走后没有看到空闲内存的逐渐下降，那么我们就找到了罪魁祸首。

## 关于 MRTG 的更多信息

`MRTG` 还允许你自定义生成的 Web 页面。它带有一个小型 Perl 程序，通过它可以轻松构建所有机器的索引页。`MRTG` 安装简单且非常有用。该包将其所有数据存储在文件中。我们建议使用某些东西生成文本值。

```
echo $variable >> /dir/logfile
```

在这种情况下，`$variable` 是你想的值，`dir` 是你想保留的目录，`logfile` 是你想要的日志文件名。你还可以添加一个命令（如 `logger`）将值写入设施和优先级。出于同样的原因，我们建议这样做。

## 将数据转换为统计

除了绘图，你有其他方法来总结数据。其中一种是提取统计数据。例如，`sendmail` 日志可能很大。通过对它们进行总结，我们可以获取机器的邮件流量，或找出谁是站点最大的邮件用户。`SSL` 脚本（sendmail log analyzer）负责这项工作。`SSL` 读取 `sendmail` 日志文件（`/var/log/syslog`）并按用户排序。结果类似于列表 24-4，显示该机器在白天总共接收了 6198 条消息，并按用户排序。`SSL` 还提供了发送邮件的统计数据。

> 你可以在 `http://reference.perl.com` 找到 `SSL`。

### 列表 24：SSL 脚本的部分输出

```
To: 6198
151 messages 530706 bytes user56@pop.mcgill.ca
95 messages 295149 bytes user567@pop.mcgill.ca
84 messages 282963 bytes user4213@pop.mcgill.ca
70 messages 404877 bytes user13@pop.mcgill.ca
70 messages 208799 bytes user9344@pop.mcgill.ca
66 messages 495505 bytes user7985@pop.mcgill.ca
63 messages 164140 bytes user431@pop.mcgill.ca
57 messages 140381 bytes user9387@pop.mcgill.ca
52 messages 138510 bytes user40632@pop.mcgill.ca
50 messages 263088 bytes user45@pop.mcgill.ca
50 messages 146122 bytes user23847@pop.mcgill.ca
```

其他工具也可以总结 `sendmail` 日志。`SSL` 可以为你提供清晰的统计数据，但它们提供的信息不足以满足我们的需求。名为 `sm_logger` 的工具在总结 `sendmail` 日志方面更进了一，如列表 24-5 所示。`sm_logger` 脚本提供了更详细的每个用户和每个主机邮件统计，例如发送或来自某个用户或主机的邮件占总收发邮件的百分比。

### 列表 24-5：`sm.logger` 脚本的部分输出

```
Sendmail activity report

Starting: Jul 5 04:10:00

Ending: Jul 6 16:35:01

Message Status    Total   Size

Received          932     5336692

Delivered         1811    6440199

Deferred           0       0
```
