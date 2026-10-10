
```
/isa/fdc1,3f0/fd0,0
Aug 19 17:17 chmod2 isa: [ID 202937 kern.info] ISAdevice: asyo0
Aug 19 17:19 chmod2 genuix: [ID 37669 kern.info] asyo0 is
/isa/asy1,3f8
Aug 19 17:22 chmod2 pseudo: [ID 129642 kern.info] pseudo-device: xvc0
Aug 19 17:22 chmod2 genuix: [ID 37669 kern.info] xsvc0
/pseudo/xsvc0
Aug 19 17:24 chmod2 i8042: [ID 526150 kern.info] 8042 device: mouse#1,mouse
0
Aug 19 17:24 chmod2 genuix: [ID 37669 kern.info] mouse8042 is
/isa/i8042,1,60/mouse@1
Aug 19 17:25 chmod2 pseudo: [ID 129642 kern.info] pseudo-device: pm0
Aug 19 17:25 chmod2 genuix: [ID 37669 kern.info] pm0 is
/pseudo/pm0
```

默认情况下，`/var/adm/messages` 属于 `root`，组具有读写权限，所有人具有只读权限。

## /var/adm/last 文件

此文件包含 `last` 命令使用的信息。通过 `/var/adm/wtmp` 文件，它提供了最近登录系统的用户信息。此文件应属于 `root` 并允许所有人读取权限。`last` 命令是安全监控的一个重要工具。我们将在创建报告的部分详细介绍其使用方法。

## /etc 文件

自然，除了日志文件外，你还应该关注 `/etc` 目录下的系统配置文件。`/etc/default/login` 文件包含重要的登录信息，例如 root 用户是否可以远程登录。监控 `/etc/passwd` 查看任何未识别账户，监控 `/etc/hosts` 查看主机名的更改。另一个重要文件是 `/etc/inet/services`，用于配置系统如何解析名称。另一个重要文件是 `/etc/switch.conf`。此外，黑客经常操控的目录是 `/etc/rc.d`。由于这些目录包含每个运行级别的启动和停止脚本，黑客经常插入代码以便在系统重启后运行未经授权的程序。此列表并不完整。你选择监控的文件取决于系统的使用方式以及你希望安全强度有多大。Tripwire 的默认设置涵盖了大部分重要的系统文件。确保你理解你的策略并知道哪些文件正在被监控。了解你的系统及其特定配置是阻止对这些文件进行未经授权更改的第一步。

许多优秀方法可以自动化检查日志文件的过程。一种流行的应用程序叫做 `swatch`。该应用程序的名字来源于“simple watcher and filter”（简单观察和过滤器）。由 Todd Addkins 用 Perl 编写，可以在 www.stanford.edu/~atkins/swatch 找到。`Swatch` 易于安装和配置，对于监控日志文件并在潜在问题非常有帮助。正如我们之前讨论的，Tripwire 是监控文件和目录的一种流行且可靠的方法。另一种方法是创建自己的 shell 脚本来自定义你想要查看的信息。让我们看看如何创建一个每天早上发送系统状态报告的脚本。

## 系统状态报告

每天早上 7:00，我会从我负责的每个系统接收电子邮件。这些消息为我提供了快速的状态报告，让我了解系统的整体状况，并提供查看任何潜在系统或安全问题的机会。让我们创建一个提供系统状态报告的脚本。首先，让我们决定想看什么。就像我的当地报纸一样，我们想看头条新闻、体育比分、商业新闻以及关于当地人物和事件的文章。

### 头条

首先，我想看到所有需要我关注的近期事件。一种方法是查看 `/var/adm/messages` 文件的最后 10 行。为了做到这一点，我将对 `dmesg` 命令使用 `tail`：

```
dmesg | tail
```

脚本的第一部分如下：

```
SYS_LOG=$(dmesg | tail | awk -F: '{print $1 $2}')
UP_TIME=$(uptime) > /export/home/scripts/report
echo "Good morning, here's the news from $(uname -n)" >> /export/home/scripts/report
echo "for $(date)" >> /export/home/scripts/report
echo "\n" >> /export/home/scripts/report
echo "The last entries in the syslog are:\n$SYS_LOG" >> /export/home/scripts/report
```

此脚本将 `dmesg | tail` 命令字符串赋值给变量 `SYS_LOG`。然后创建报告。为了演示，我们在 `/export/home/scripts` 创建了脚本并命名。它首先告诉我们报告生成的地点和时间；然后显示 `/var/adm/messages` 中的最新条目。

### 体育页

下一部分提供了相当于体育比分的内容。我们想要查看当前的 CPU 负载以及系统持续运行的时间。如果 CPU 负载异常高，或者系统在在我们不知情的情况下重启了，我们将立即进行调查。

脚本如下：

```
CPU_ACT=$(uptime | awk -F: '{print $4}')
RE_BOOT=$(who -b)
```

```
echo "\n\n" >> /export/home/scripts/report
echo "The current CPU load over the last 1, 5 and 15 mins is: $CPU_ACT" >> /export/home/scripts/report
```

```
echo "The system was last rebooted":"$RE_BOOT >> /export/home/scripts/report
```

### 本地事件

此部分用于汇总使用系统的用户。我们想查看当前谁登录了系统，以及谁使用了 `su` 命令。该部分的内容如下：

```
CURRENT_USERS='who'
WHO_SU='tail /var/adm/sulog'
```

```
echo "\n*****" >> /export/home/scripts/report
echo "The users currently logged in:\n$CURRENT_USERS" | cat >>/export/home/scripts/report
echo "\n*****" >> /export/home/scripts/report
echo "The last 10 users of the su command were:\n$WHO_SU" | cat >>/export/home/scripts/report
echo "\n*****" >> /export/home/scripts/report
echo "If you were a Hacker, how would you break into this system?" >>/export/home/scripts/report
echo "\n\n" >> /export/home/scripts/report
```

通过此部分中的信息，我们寻找不处于处于状态的账户。例如，如果我们看到用户 `janeill` 在早上 7:00 登录，而我们知道该用户很少在早上 9:00 之前出现，我们就有理由怀疑。要么是 `janeill` 起早了，要么她昨晚忘记注出了——要么是其他人正在使用该账户。无论什么情况下，都需要进行调查。

此外，这还能告诉我们谁在使用 `su` 命令。如果我们看到用户 `janeill` 成功切换到了 `root` 账户，而我们知道该用户不应该这样做，我们就有了麻烦。

脚本的最后一行将报告发送到 root 电子邮件地址。通过使用 Sendmail 别名，我们可以将报告发送到任何电子邮件地址：

```
cat /export/home/scripts/report | mailx -s "Daily Report from `uname -n`" root
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_376_0.png)

# 检测与拒绝黑客攻击 • 第 11 章 353

## 开始行动！

以下是完整的脚本：
