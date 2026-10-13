
## 答案

- 1. crontab 文件将 `minute hour` 指定为时间说明符的前两个字段。
- 2. 命令 `crontab -r` 会永久删除 crontab 文件。
- 3. 当然会，尽管很复杂。它匹配以下枚举列表：0,3,6,7,8,9,11,13,15,17,19。
- 4. 问题在于 cron 程序使用的 PATH 很可能与你的登录 shell 不同。为规避此问题，请始终为 crontab 行中引用的命令以及 cron 代表你调用的任何 shell 脚本中指定的命令指定完整路径名。
- 5. 正如我父母肯定会确认的那样，所有文明国家的茶点时间都是下午 4 点。精确地说。

在接下来的一个小时里，我们将通过分析和管理 Unix 中众多日志文件的增长来了解 cron 的一些实际用途。我们还将学习 Linux 中一个名为 logrotate 的巧妙新实用程序，以及如何在其他 Unix 系统中模拟它。

![](img/5ced0c78d748bd190e9027e5549a3622_315_0.png)

![](img/5ced0c78d748bd190e9027e5549a3622_317_0.png)

## 第 16 小时

### 管理你的日志文件

系统管理员最重要的任务之一是关注系统和磁盘空间。之前我们花了一些时间探索 df、du 和 find，并学习了它们如何用于更好地了解系统上磁盘空间的分配。

在本小时中，我们将深入研究不同 Unix 服务使用的特定日志文件，学习如何分析它们以标记任何潜在问题，以及如何防止它们耗尽磁盘空间。

本小时你将学习

- 探索日志文件的内容
- 通过日志事件追踪黑客
- 打开 httpd 日志文件
- 使用 logrotate 修剪日志文件
- 构建自己的日志轮转工具

## 理解日志文件

无论是启动过程本身、FTP 服务器、邮件服务器，还是计算机上运行的任何其他服务，如果它执行了某些操作或有人与其交互，该事件就会被记录。一些服务有自己的日志文件，但许多服务使用名为 syslog 的共享集中式日志机制。syslog 将所有消息写入通常称为 messages 或 syslog 的日志文件。

Unix 变体在日志文件放置位置上有所不同，但通常你会在 /var/log 中找到它们，默认情况下。

### 任务 16.1：在日志文件中翻找

不同系统具有不同数量的日志文件，这取决于运行的服务数量以及每个服务的日志配置方式。

- 1. 首先，查看 /var/log 目录：

```
# ls -s
total 1836
0 boot.log      63 ksyms.2      0 pgsql      0 spooler.3
0 boot.log.1    63 ksyms.3      18 rpmpkgs   0 spooler.4
5 boot.log.2    63 ksyms.4      18 rpmpkgs.1  1 squid
0 boot.log.3    63 ksyms.5      18 rpmpkgs.2  1 vbox
0 boot.log.4    63 ksyms.6      18 rpmpkgs.3  42 wtmp
51 cron         20 lastlog      18 rpmpkgs.4  40 wtmp.1
257 cron.1      2 mailog        1 sa          0 xferlog
253 cron.2      5 mailog.1      1 samba       0 xferlog.1
254 cron.3      4 mailog.2      1 secure      0 xferlog.2
252 cron.4      3 mailog.3      5 secure.1    0 xferlog.3
11 dmesg        3 mailog.4      4 secure.2    0 xferlog.4
1 fax           1 messages     2 secure.3    23 XFree86.0.log
1 gdm           6 messages.1   1 secure.4    24 XFree86.9.log
1 httpd         26 messages.2  0 spooler
63 ksyms.0      2 messages.3   0 spooler.1
63 ksyms.1      1 messages.4   0 spooler.2
```

请注意，文件具有版本号后缀。正如你将在本小时后面学到的那样，这表明它们正在被轮转——数字越高，文件越旧。没有版本号标识的版本是当前日志文件。

- 2. 最基本的日志文件是 syslog 的文件，在 Linux 机器上，它被称为 /var/log/messages。

```
# grep "Mar 11" messages
Mar 11 00:13:23 staging su(pam_unix)[12835]: session closed for user root
Mar 11 00:14:14 staging sshd(pam_unix)[12796]: session closed for user taylor
Mar 11 00:02:18 staging syslogd 1.4.1: restart.
Mar 11 11:19:32 staging sshd(pam_unix)[14687]: session opened for user taylor
  by (uid=0)
Mar 11 14:09:06 staging su(pam_unix)[14539]: session opened for user root by
  taylor(uid=502)
```

```
Mar 11 16:02:05 staging sshd(pam_unix)[14716]: session opened for user taylor by (uid=0)
Mar 11 16:28:10 staging sshd(pam_unix)[14716]: session closed for user taylor
Mar 11 16:28:19 staging su(pam_unix)[14593]: session closed for user root
Mar 11 16:28:21 staging sshd(pam_unix)[14368]: session closed for user taylor
```

这是 2002 年 3 月 11 日所有已记录消息的列表。没什么令人兴奋的，但你可以看出 su 记录事件，而 sshd（ssh 守护进程）记录用户连接和断开的情况。

查看此文件的内容，我们可以确定用户 taylor 在 00:14 sshd 会话结束时仍处于登录状态，并且在时钟转到 3 月 11 日时，还有一个 su 会话（作为 root）处于活动状态。凌晨 4:02，syslogd 重启，用户 taylor 当天登录了两次，一次在上午 11:19，第二次在下午 4:02（16:02）。在此期间，taylor 切换到 root 并让 root shell 从上午 11:19 运行到下午 4:28（16:28）。

通过在旧日志文件中搜索 Mar 10 快速查看，可以识别初始 su，以查看是否也是 taylor 发起的：

```
# grep "Mar 10" messages.1 | grep 'su'
Mar 10 23:39:49 staging su(pam_unix)[12835]: session opened for user root by taylor(uid=502)
```

果然如此，在晚上 11:39，taylor 使用 su 命令成为 root。

- 3. 也许比梳理某一天的登录更重要的是扫描任何潜在的安全问题。一个明显的问题是：是否有人尝试使用 su 功能但登录失败？

```
# grep "su" messages* | grep -vE '(session opened|session closed)'
messages:Mar 18 12:52:14 staging su(pam_unix)[5330]: authentication failure; logname=taylor uid=502 euid=0 tty= ruser= rhost= user=root
messages.1:Mar 12 20:56:09 staging su(pam_unix)[17297]: authentication failure; logname=taylor uid=502 euid=0 tty= ruser= rhost= user=root
messages.3:Feb 23 21:09:16 staging su(pam_unix)[15552]: authentication failure; logname=taylor uid=502 euid=0 tty= ruser= rhost= user=taylorsu
```

你可以看到，在包含所有记录事件的时间窗口内，有三次 su 失败尝试，分别发生在 2 月 23 日、3 月 12 日和 3 月 18 日，全部由用户 taylor 发起。其中两次是尝试成为 root，一次是尝试成为 taylorsu。

你也可以通过构建一个快速摘要并使用有用的 uniq 实用程序来查看差异，从而验证所有成功的 su 是否都来自已知用户：

```
# grep 'session opened' messages* | awk '{print $12 " became " $10 }' | \
sort | uniq -c
2 taylor(uid=0) became taylor
15 taylor(uid=502) became root
2 taylor(uid=502) became taylorsu
4 (uid=0) became judi
35 (uid=0) became taylor
```

有点复杂，但我们提取所有“session opened”消息，剥离 From 和 To 账户信息，并输出一个简单的三词值。然后 sort 确保它们有序，uniq -c 统计每个字符串的唯一出现次数并为每个唯一字符串输出一行，以重复计数为前缀。例如，第二行显示 taylor 使用 su 实用程序成为 root 15 次。

- 4. 相比之下，在 Mac OS X 系统上，syslog 文件被称为 system.log，其中包含各种有趣的信息。例如，想知道系统进入睡眠并再次唤醒时会发生什么？

```
Mar 18 11:35:02 dsl-132 mach_kernel: UniNenet::
putToSleep: turning off cell clock!!!
Mar 18 11:35:02 dsl-132 mach_kernel: System Sleep
Mar 18 11:35:02 dsl-132 mach_kernel: System Wake
Mar 18 11:35:02 dsl-132 mach_kernel: Wake event 0020
```

更有用的是，su 和 sudo 都在这里记录：

```
# grep "su:" system.log
Mar 15 09:42:38 dsl-132 su: taylor to root on /dev/ttyp1
# grep "sudo:" system.log
Mar 11 22:02:45 dsl-132 sudo: taylor : TTY=ttyp1 ; PWD=/Users/taylor/bin ; USER=root ; COMMAND=/docron weekly
Mar 11 22:05:14 dsl-132 sudo: taylor : TTY=ttyp2 ; PWD=/Users/taylor ; USER=root ; COMMAND=/bin/ls /
```

在此日志文件中，没有证据表明除 taylor 之外的任何用户运行 su 或 sudo。

![](img/5ced0c78d748bd190e9027e5549a3622_320_0.png)

> 你可以通过查看日志文件的第一行和最后一行轻松确定记录的时间段：
>
> ```
> # head -1 system.log ; tail -1 system.log
> Mar 11 22:02:28 dsl-132 syslogd: restart
> Mar 18 12:20:58 dsl-132 WindowServer[65]: CGGetWindowLevel:
> Invalid window 623
> ```
> 在这里你可以看到这大约代表一周：从 3 月 11 日晚上 10:02 到 3 月 18 日下午 12:20。

- 5. 下一个要检查的日志文件是 boot.log，它显示了启动时屏幕输出的所有消息。由于大多数 Unix 系统不会每天启动（希望如此！），因此这通常会为空，正如你在步骤 1 的 ls 列表中看到的那样。

```
# head -20 boot.log.2
Feb 25 22:44:42 staging atd: atd shutdown succeeded
Feb 25 22:44:44 staging httpd: httpd shutdown succeeded
Feb 25 22:44:44 staging sshd: sshd -TERM succeeded
```
