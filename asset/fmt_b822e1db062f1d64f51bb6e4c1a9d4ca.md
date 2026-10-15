
| `program` | 将日志管道到程序的标准输入 |

驱动程序还支持有限的变量。有日期变量，可以根据接收日志的日期命名日志文件；有包含源机器名称的主机名变量等等。

# 第 6 章 监控服务

这些变量最有用的实现之一是让 `syslog-ng` 将日志放入自动创建的以当前月份命名的目录中。使用这些目录就像拥有了一个自动日志归档系统；具体方法如下：

```
destination mail { file("/var/log/syslog-ng/$YEAR$MONTH/mail") group(wheel)
perm(0640); };
destination cron { file("/var/log/syslog-ng/$YEAR$MONTH/cron") group(wheel)
perm(0640); };
destination auth { file("/var/log/syslog-ng/$YEAR$MONTH/auth") group(wheel)
perm(0640); };
destination kernel { file("/var/log/syslog-ng/$YEAR$MONTH/kern") group(wheel)
perm(0640); };
destination daemon { file("/var/log/syslog-ng/$YEAR$MONTH/daemon") group(wheel)
perm(0640); };
destination firewall { file("/var/log/syslog-ng/$YEAR$MONTH/firewall") group(wheel)
perm(0640); };
```

## Log Paths

Log paths 从整个配置开始，将 sources、filters 和 destinations 连接成一个统一的日志系统。每个日志路径都指定了 `syslog-ng` 应从哪里记录消息、哪些过滤器以及哪些目的地。以下是这些日志路径的示例：

```
log { source(src); filter(f_mail); destination(mail); }
log { source(src); filter(f_cron); destination(cron); }
log { source(src); filter(f_auth); destination(auth); }
log { source(src); filter(f_kern); destination(kernel); }
log { source(src); filter(f_daemon); destination(daemon); }
log { source(src); filter(f_firewall); destination(firewall); }
```

## 适当使用 `syslog-ng`

`syslog-ng` 很容易安装，但请记住，尽管它可以安装在所有机器上，但它在中央日志服务器是最有用的。系统提供的 `syslog` 应该将所有日志重定向到你的新日志服务器。在 Solaris 上的配置如下：

```
log { source(src); filter(f_mail); destination(mail); }
log { source(src); filter(f_cron); destination(cron); }
log { source(src); filter(f_auth); destination(auth); }
log { source(src); filter(f_kern); destination(kernel); }
log { source(src); filter(f_daemon); destination(daemon); }
log { source(src); filter(f_firewall); destination(firewall); }
```

## 应用日志

并不是所有的工具和应用程序都使用 `syslog`。事实上，如果不在监控，`syslog` 会产生大量的日志。应用程序日志会变得失控。将日志放在常见的子目录（如 `/var/log`）下可以简化归档。

## 真实案例：日志失控

一家运行流行 Java 应用程序的公司刚刚发布了其 Web 应用程序的新版本。两天后，系统管理员收到报警，称其中一台服务器上的文件系统已满。其中一名管理员检查了网站以确保所有程序运行正常，事实也确实如此。然而，在其中一台服务器上，`/var` 文件系统已被应用程序服务器的错误日志填满了。事实上，日志的增长速度几乎达到了每秒近 1,000 条！管理员将产生问题的日志移动到另一个文件系统并重启了服务器，这暂时解决了问题。在整个波折期间的变故过程中，服务器和应用程序仍然在运行！由于 `/var` 文件系统中没有存储关键的应用程序数据，溢出的日志文件没有对应用程序产生任何不利影响，也没有发生停机。

## 文件大小

日志的大小会影响整个文件系统，但文件大小对日志的可用性也有直接影响。你会在一个 2MB 的系统日志中搜索信息，还是在一个 500MB 的系统日志中搜索？显然，在较小的日志中查找信息要容易得多，但尽可能拥有更多信息也是有：翻阅备份磁带来查找上周的日志对你来说可能是不可接受的。在决定对日志文件大小的容忍度时，应该考虑到这些因素，包括相关日志的增长率。

## 选择日志文件大小限制

选择日志文件的合适大小限制只能通过经验来实现。大小应该足够大，以保留你所需的历史数据；也要足够小，以便你可以搜索和传输文件而不会产生太大的延迟。你还应该在文件系统中留出足够的空间保留旧日志文件的在线副本（轮转）。随着时间的推移观察你的日志，看看它们如何增长，然后你可以为每个文件设定合适的限制。

## 轮转

日志轮转在管理文件大小的同时保持日志信息的可用性。你需要旧日志能够随时可用，以便研究当前问题并审计你的系统。根据你组织的性质，你可能被法律要求保留一段时间的日志。你最终可以将这些日志写入 CD-ROM 或磁带等长期存储设备，但让它们保持在线可以方便随时使用。

日志不会永远存在；尽管它们最终会变得巨大而无法使用，文件也会变得过时而失去价值。日志轮转将活动日志移动到单独的位置，这样它们就不会失控增长，也不会因为过时而其信息不再具有相关性。

## UNIX 系统管理入门进阶

大多数操作系统都内置了日志轮转功能，但如果有需要，很容易编写你自己的程序。Red Linux 每周轮转一次 `/var/log` 中的日志，每每周重命名每个文件：

```
$ls -l messages* root 95505 Jan 12 15:14 messages
-rw-r--r-- 1 root 118162 Jan 06 04:02 messages.1
-rw-r--r-- 1 root 91290 Dec 30 04:02 messages.2
-rw-r--r-- 1 root 91736 Dec 23 04:02 messages.3
-rw-r--r-- 1 root 121928 Dec 16 04:02 messages.4
```

这种轮转方案是可自定义的。Red Hat Linux 使用 `logrotate` 程序来自动化日志文件的轮转。你可以在第 12 章中找到 `logrotate` 的详细描述。

OpenBSD 采用了一种轮转方案，但它也习惯在轮转后对文件进行压缩。除了轮转文件，你还应该考虑你的日志保留策略，或者你希望在磁盘上保留每个日志多久。如从前面的示例所示，Red Linux 有一个为期四周的日志保留策略；四周后，轮转后的日志将从系统中永久删除。

保留取决于所有可用的磁盘空间；你愿意为旧日志投入多少磁盘空间？日志的大小会严重干扰新日志可用空间吗？尝试并观察什么方案对你的系统有效。

![](img/894492738e879267320b8d6f9a044180_181_0.png)

## 日志轮转步骤

`syslog` 打开日志并在整个进程生命周期内保持打开状态。如果你移动或重命名了日志文件，它们仍将保持打开状态并被写入。轮转这些文件的正确方法是重命名日志并重启 `syslog` 守护进程。或者，你可以停止守护进程、移动日志并重启，但你可能会在此过程中丢失一些日志。

## 归档存储

当轮转中最旧的日志被删除时，它就永远消失了。日志对于问题诊断、性能监控至关重要，甚至可能有法律影响，因此将它们归档到某种长期存储中是非常重要的。这种存储通常是某种磁带备份，但由于寿命更长，归档到 CD-ROM 正变得流行。

## 让归档随时可用

无论你使用何种介质存储日志，它都应该是随时可用且方便访问的，因为日志可能在任何时候被需要。CD-ROM 或磁带库可以只需按一下即可获取旧的归档。

你应该安排日志在轮转过程发生之前的某个时间写入归档介质，这样你就能拥有即将从在线存储中删除的文件的归档副本。你可以使用 `tar` 和 `dump` 等工具手动归档文件，或者让你的备份软件来管理。

作为一个简单的示例，以下 `crontab` 条目会在每周日 11:00 将所有日志写入设备 `/dev/0`：

```
0 11 * * ( cd /var/adm; tar cf /dev/0 messages*)
```

## 日志监控
