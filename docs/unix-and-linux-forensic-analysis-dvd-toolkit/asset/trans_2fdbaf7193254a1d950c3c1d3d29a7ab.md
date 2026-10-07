

## 第 4 章 • 初步分类与现场响应：数据分析

……有记录日志，但并没有这样做。他们一直希望被放入入侵检测系统（IDS）或入侵预防系统（IPS）中，但一直缺乏资源。你需要弄清楚他们拥有什么、这些数据位于网络的什么位置，以及它们是否记录日志。确保索要他们拥有的任何日志。

- **受影响系统的状态** 这是另一个客户可能并不真正了解的项之一。我参与过几个案例，在这些案例中你被告知了某事，例如某个系统没有重启；但一旦你到达现场，就会发现事实恰恰相反。因此，如果你在到达之前问了这些问题，你必须再次提问，并在可能的情况下进行核实。这些信息可能会影响你调查的方向。

- **维持正常业务运行** 在尽可能可能的情况下，你需要理解对客户来说什么是“正常”。在响应安全事件时，你很可能是第一次查看客户的基础设施。你完全不知道他们的 ID 命名规范是什么，平均每天经历什么种的流量，哪些系统之间在相互通信，或者构成他们典型一天的数以百计的变量任何变量。为了进行任何形式的初步分析，你必须尽可能地理解这些。

虽然你需要就这个主题提出尽可能多的问题，但要理解，随着调查的进行，无疑会有更多问题出现。确保让客户知道你会有更多问题，并且你需要一个可靠的联系人（POC），该联系人需要对他们的技术和业务流程有足够的了解，以便明智地回答这些问题。

一旦你收集了你认为相关的所有信息（这无疑会发生变化），你就可以开始初步分析。在调查的阶段，最重要的事情是对事件保持中立。尽量不要对数据的走向下达过早的结论。简单地让数据来决定你所采取的路径。

## 日志分析

在我拙看来，你调查的起点应该是对客户能够提供的任何日志文件进行分析。这可能什么都没有，如果是这样，你现在可能该吃片阿司匹林了，因为头痛很快就会到来；也可能是数级的数据，如果是这样，你可能还是得阿司匹林，因为同样的头痛很快就会到来。

从头开始。一个简单的概念是，在任何事件中，入侵者必须从某个地方进入客户网络，所以从那里开始。它可能是一个虚拟专用网络（VPN）集中器，可能是一个卫星办事处，也可能来自特定的工作站或服务器。无论情况如何，从那里开始。

Linux 系统上的日志文件是极好的东西。它们具有高度的可配置性、高效且详细。如果运气好，你正在收集和或分析日志的系统至少已经有了默认的日志配置。Linux 日志是纯文本，因此你不需要使用任何第三方软件或工具来执行有效的搜索。此外，你可以编写自定义脚本，根据日志的内容和你所需的输出执行自动操作。

Linux 日志位于 /var/log 目录。这些是由系统维护的日志文件，极可能（通常是默认如此）来自任何安装到系统中的第三方软件。你还会在目录中看到以某些名称结尾的文件，如图 4.1 所示。

### 图 4.1 结尾的文件

```
log_type       syslog          var.log         dmes.log         kern.log         mail           couple.log,1  udev           postgresql
auth.log       auth.log.1      boot.log        dbw.0          dpkg.dplog.1     messages       syslog           user.log        updated-apt-grades   kern.log.0
acpid.log      acpid.log.1     btmp.0          btmp.0          dpkg.dplog.1     kern.log.1      messages.1       syslog           user.log.1
auth62.log     auth62.log.1    wtmp.0          wtmp.0          dpkg.dplog.2     kern.log.2      messages.2       syslog           user.log.2
auth64.log     auth64.log.1    lastlog.0       lastlog.0       dpkg.dplog.3     kern.log.3      messages.3       syslog           user.log.3
cron.log       cron.log.1      creds.0          creds.0          dpkg.dplog.4     kern.log.4      messages.4       syslog           user.log.4
fail.log       fail.log.1      fpc.0           fpc.0           dpkg.dplog.5     kern.log.5      messages.5       syslog           user.log.5
ufw.log        ufw.log.1       gmmp.0          gmmp.0          dpkg.dplog.6     kern.log.6      messages.6       syslog           user.log.6
hhold.log       hhold.log.1      hd.0            hd.0            dpkg.dplog.7     kern.log.7      messages.7       syslog           user.log.7
ndmp.log       ndmp.log.1      info.0          info.0           dpkg.dplog.8     kern.log.8      messages.8       syslog           user.log.8
nscd.log       nscd.log.1      journal.0       journal.0        kern.log.9      messages.9       syslog           user.log.8
kern.log.log.d...................................................................................................................journal.0.kern.log.9      messages.9.syslog           user.log.9
ac.log.auth.log.1...log..w.0.......1.......log.1...1.syslog.user.log.1
acpid.log      acpid.log.1     btmp.0          btmp.0          dpkg.dplog.1     kern.log.1      messages.1       syslog           user.log.1
auth62.log     auth62.log.1    wtmp.0          wtmp.0          dpkg.dplog.2     kern.log.2      messages.2       syslog           user.log.2
auth64.log     auth64.log.1    lastlog.0       lastlog.0       dpkg.dplog.3     kern.log.3      messages.3       syslog           user.log.3
cron.log       cron.log.1      creds.0          creds.0          dpkg.dplog.4     kern.log.4      messages.4       syslog           user.log.4
fail.log       fail.log.1      fpc.0           fpc.0           dpkg.dplog.5     kern.log.5      messages.5       syslog           user.log.5
ufw.log        ufw.log.1       gmmp.0          gmmp.0          dpkg.dplog.6     kern.log.6      messages.6       syslog           user.log.6
hhold.log       hhold.log.1      hd.0            hd.0            dpkg.dplog.7     kern.log.7      messages.7       syslog           user.log.7
ndmp.log       ndmp.log.1      info.0          info.0           dpkg.dplog.8     kern.log.8      messages.8       syslog           user.log.8
nscd.log       nscd.log.1      journal.0       journal.0        kern.log.9      messages.9       syslog           user.log.9
```
*(注：由于示例中代码块存在大量重复和乱码，此处已按原始格式结构处理)*

这些被称为轮转存档。根据日志设置的粒度不同，日志会变得庞大且繁琐。Linux 提供了一个 `logrotate` 命令，它的作用正如你认为的那样：通过在文件末尾添加数字后缀来轮转日志文件。例如，在图 4.1 中，你可以看到没有数字后缀的 `syslog`。存档中的第一个文件是 `syslog.0.gz`，它是之前活跃的日志文件。接下来你会看到 `syslog.1.gz` 到 `syslog.6.gz`。这些是 gzip 格式的剩余存档日志。当 `logrotate` 运行时（通常每天运行一次，默认可以在 /etc/cron.daily 中找到），它会获取当前文件，在文件末尾添加 “.0”，并重新以该文件的标准名称“syslog”开始记录。

