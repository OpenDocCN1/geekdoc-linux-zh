
将报警记录到远程服务器的选项通过第 37 行的 `logger` 命令实现。这是一个问题，因为 `logger` 只能记录到本地 syslog。没有直接记录到远程 syslogd 的客户端实用。不过，可以做的是记录到本地 syslog，并配置本地守护进程将其转发到远程机器。为了让你的报警脚本工作，我必须修改本地的 syslog 配置。注意到在报警脚本中我记录到了设施 `local6`，我需要在本地的 `/etc/syslog.conf` 中添加此行，假设远程监控器的主机名为 `watchdog`。

```
local6.info @watchdog
```

不要忘记在 `watchdog` 上配置 syslog 以接收输入。你需要在 syslog 启动脚本中添加 `-r` 标志，如第4 章“为了可靠性进行安装和配置”所示。

这种方式的远程日志很容易，但也有一些需要注意的地方。如果故障导致客户端无法解析主机名，那么你的客户端 syslog 将无法发送到 `watchdog`，因为它无法确定 `watchdog` 的地址。你可以将 IP 地址硬编码在 syslog 配置文件中，但这会降低可移植性。另一种替代方案是将 `watchdog` 的地址放在客户端的 `/etc/hosts` 中，允许本地名称解析。

同样的问题也适用于远程服务器。传入的日志消息仅携带发送者的 IP 地址，`watchdog` 上的 syslog 在将其写入本地日志时，会尝试将这些地址解析为主机名。

注意，过度记录或失控的日志机制可能会淹没日志并导致问题。如果你使用远程日志，这个问题可能会在网络上成倍增加。此外，远程 syslog 已配置为接受远程条目，它没有内部手段来判断是谁在发送消息。这可能成为一个安全漏洞，导致拒绝服务攻击的可能性。你可能希望考虑使用防火墙并过滤进入 syslog 端口 `514/UDP` 的输入来保护远程 syslog。

## 送至呼机机（Pager）

最后一种告警类型是呼机机。在一个完美的世界，应该有一种简单的方法来生成呼机消息。但我们生活在一个并不简单的世界里。有多种不同的方式可以呼叫，正如随附侧边栏“呼机机入门”讨论的那样。我的示例使用了 `snpp` 命令，它是侧边栏中提到的 `sendpage` 软件包的一部分。`-m` 标志允许从命令行包含发送到呼机机的文本，否则 `snpp` 将从标准输入读取。`snpp` 的最后一个参数 `admin` 是一个需要在 `send page` 文件中设置的标识符。它将指向呼机机的电话号码，并在必要时指向被呼叫者的 PIN 码。

现在你有了一个在监控检测到危险情况时响警的标准手段。接要做的事情是编写一些监控器。

## 呼机机入门（PAGING PRIMER）

呼机机的种类多样，从简单的“拨打我的呼机机并留下号码，我会稍后回电”到目前的字母数字、双向呼机机兼电子邮件客户端兼 Web 客户端模型。在服务器管理领域最有用的类型可能是字母数字呼机机，它允许发送字符字符串消息，为呼机机接收者描述问题。这些呼机机使用由个人通信行业协会（PCIA）发布的 Telocator 字母数字协议（TAP）。这是一种基于 ASCII 的协议，通常实现在发起呼叫的服务器与由呼机机供应商操作的呼机终端之间的串行通信线路上。通过使用 TAP 会话的服务器生成的呼叫，自动等同于你拨打呼机机号码并发送数字、字母数字或语音消息呼叫。一旦消息发出，它将通过他们的呼机机终端网络路由到离呼机机本身最近的一个，然后从那里最终广播到呼机机。

## 在生产环境中监控 Linux

为了让你的服务器能够自动创建呼叫，你需要一个 TAP 客户端。有几个开源 TAP 客户端，包括 Beepage、QuickPage 和 Sendpage。除了作为 TAP 客户端外，QuickPage 和 Sendpage 还实现了由 RFC1861 定义的简单网络呼叫协议（Simple Network Paging Protocol, SNPP）。SNPP 客户端使用 SNPP 通过本地网络将页面发送到 SNPP 服务器。该服务器拥有外接调器连接，并使用 TAP 将通过 SNPP 接收到的呼叫发送到呼机终端，从那里它穿过呼机机网络到达呼机机本身。在呼叫发起者和调制调器之间使用 SNPP 的优势在于，它允许从多个客户端收集呼叫，这些客户端可以分布在本地网络中，然后由单个模型排队传输。下一代呼叫将通常提供双向呼叫。下一代协议 Telocator 网络呼叫协议（TNPP）可以处理这种通信。请关注未来的 Linux TNPP 客户端。

有关呼机机的更多信息可以在 `www.pcia.com` 和 `www.refreq.com` 找到。你可以在 `www.qpage.org` 找到 QuickPage，在 `sendpage.cpoint.net` 找到 Sendpage。

### 监控磁盘使用

列表 6.2 中的示例脚本按文件系统监控磁盘使用，并在超过阈值时生成告警：

```bash
#!/bin/ksh

# 监控系统的脚本
# 此脚本设计为从 /etc/cron.hourly 每小时运行一次

# 语法: monitor_filesystems

alarm_threshold=70
page_threshold=90
typeset -RZ4 usage_with_percent_sign
```

列表 6.2 `monitor_filesystems`

```bash
11
12 df -P | tail +2 while foo
13 do
14     usage_with_percent_sign=$(echo foo | awk '{print $5}')
15     usage=${usage_with_percent_sign%%}
16     fs=$(echo foo | awk '{print $1}')
17     mount=$(echo foo | awk '{print $6}')
18     if [[ $usage -ge $alarm_threshold ]];] then
19         /usr/local/bin/sound_alarm broadcast \
20         echo "File system $fs mounted at $Mount is $usage % full"
21     fi
22     if [[ $usage -ge $page_threshold ]];] then
23         /usr/local/bin/sound_alarm pager \
24         echo "File system $fs mounted at $Mount is $usage % full"
25     fi
26 done
27 monitor_filesystems
```

列表 6.2 `monitor_filesystems`（续）

如第 4 行所示，此脚本可以很容易地从 `/etc/cron.hourly` 运行，或者根据需要从 crontab 更频繁地运行。该脚本不接受任何参数，并扫描所有本地挂载的文件系统。第 8 行定义了告警阈值，为 70。第 10 行定义了呼叫阈值，为 90。第 12 行将 `df` 命令管道到循环中。第 14 行提取百分比。第 15 行删除百分号。第 16 行提取文件系统名称。第 17 行提取挂载点。第 18 行检查使用率是否超过告警阈值。第 20 行发送广播告警。第 22 行检查使用率是否超过呼叫阈值。第 23 行发送呼机告警。第 27 行调用函数。

此脚本的监控类型对于告知磁盘使用情况非常重要。遗憾的是，虽然它可以提醒你磁盘正在填充，但它无法采取任何措施阻止磁盘填充。理想的情况是一个在请求空间时自动控制存储空间的主动监控器。这种系统被称为磁盘配额。我们接下来将介绍。

# 构建可靠的服务器

## 配置 ext2 文件配额

磁盘配额可以在部分所有本地文件系统上启用。磁盘配额是 ext2 文件系统的标准功能，但默认未配置。如果你想使用磁盘配额，以下是配置步骤：

- 1. 通过在 `/etc/fstab` 中添加配额标志将文件系统标记为激活，如下：

```
/dev/hda6      /home      ext2 defaults,usrquota  1 
```

`usrquota` 标志允许按用户进行配额检查。你也可以使用 `grpquota` 按组进行检查，或者两者都使用。每个你想要执行配额的文件系统都必须标记。一旦 `/etc/fstab` 被编辑，你必须重新挂载每个启用了配额的文件系统，如下：

```
mount -o remount /home
```

- 2. 接下来你需要使用 `quotacheck` 命令创建配额数据文件，如下：

```
quotacheck /home
```

- 3. 你现在需要使用 `quotaon` 命令开启配额检查，如下：

```
quotaon /home
```

## 232 构建可靠的服务器

设置好配额后，你现在可能认为这会自动发生。但这样做有充分的必要理由。如果有 `quotaon` 命令，那么就必须有一个 `quotaoff` 命令，对吧？是的，有的，而且它非常重要，因为某些你可能想要执行的操作会受到配额的影响。为了适应这些情况，有必要临时禁用文件系统的配额检查。
