

+   MAX_RUNNERS_PER_QUEUE 选项设置每个队列的默认运行器限制，如果在队列组定义中未使用 Runners=（或 R=）参数显式设置值。

## 负载平均值控制

sendmail 一直能够在系统负载平均值过高时拒绝连接或将消息排队而不是投递它们。 不幸的是，负载平均值只有一分钟的粒度，因此它并不是一个非常精细的工具来平滑 sendmail 消耗的资源。 DELAY_LA 原语让你设置一个负载平均值，在该值下 sendmail 应该减速；它将在当前连接的 SMTP 命令之间以及在接受新连接之前每隔一秒休眠一次。 默认值为 0，这会关闭该机制。

## 队列中无法投递的消息

邮件队列中无法投递的消息会严重影响繁忙邮件服务器的性能。 sendmail 有几个功能可以帮助解决无法投递消息的问题。 最有效的是 FALLBACK_MX 选项，如果第一次尝试无法投递，它会将消息交给另一台机器。 你的主机器将消息发送给有效地址，并将问题儿童分流到第二台备用机器。 另一个帮助是主机状态目录，它在队列运行之间存储远程主机的状态。

对于拥有大量邮件列表且不可避免包含暂时或永久无法投递地址的站点，FALLBACK_MX 选项是一个巨大的性能提升。 要使用它，你需要指定处理延迟邮件的主机。 例如，

```
define(`confFALLBACK_MX', `mailbackup.atrust.com')
```

会将首次投递尝试失败的消息转发到 mailbackup.atrust.com 进行进一步处理。 如果指定主机在 DNS 中有多个 MX 记录，则可以有多个备用机器。

TO_ICONNECT 选项为初始连接和发送消息设置超时。 如果你将其设置得很短，更多工作将被分流到备用 MTA。 然而，它确实让主服务器能够在创纪录的时间内完成对大型邮件列表的第一次传递。

在备用机器上，你可以使用 HOST_STATUS_DIRECTORY 选项来帮助处理多次失败。 该选项指示 sendmail 为发送邮件的每个主机维护一个状态文件，并在每次运行队列时使用该状态信息来优先处理主机。 该状态信息有效地实现了负缓存，并允许在队列运行之间共享信息。 对于处理大量坏地址的邮件列表的服务器来说，这是一个性能提升，但在文件 I/O 方面可能代价高昂。

下面是一个使用目录 /var/spool/mqueue/.hoststat 的示例。 （你必须先创建该目录。）

```
define('confHOST_STATUS_DIRECTORY', '/var/spool/mqueue/.hoststat')
```

如果使用相对路径指定 .hoststat 目录，它将存储在队列目录下。 sendmail 会根据目标主机名创建自己的内部子目录层次结构。

例如，如果发往 evi@anchor.cs.colorado.edu 的邮件失败，状态信息将保存在 /var/spool/mqueue/.hoststat/edu/colorado/cs 目录中的名为 anchor 的文件中。 这是因为主机 anchor 具有以自身为最高优先级的 MX 记录。 如果 DNS MX 记录将 anchor 的邮件指向主机 foo，则文件名将为 foo，而不是 anchor。

第三个繁忙机器的性能增强涉及设置最小队列年龄，以便任何在初始尝试中无法投递的消息在下一次投递尝试之间在队列中停留最短时间。 该技术通常与运行队列更频繁的命令行标志结合使用（例如，-q5m）。 如果一个队列运行器在坏消息上挂起，另一个将在 5 分钟后启动，从而提高可以投递的消息的性能。 整个队列按达到所需最短时间的消息进行批处理。 使用标志 -bd -q5m 运行 sendmail 并在配置文件中包含

```
define('confMIN_QUEUE_AGE', '27m')
```

可能会导致系统响应更快。

## 内核调优

如果你计划使用 UNIX 或 Linux 机器作为高容量邮件服务器，你应该修改内核的几个网络配置参数。 表 20.16 显示了在高容量邮件服务器上在 Linux 上需要更改的参数及其建议值和默认值。 类似的参数也存在于 UNIX 中，可能名称略有不同。

表 20.16 高容量邮件服务器上需要更改的内核参数

| Variable (relative to /proc/sys) | Default | Suggested |
|---|---|---|
| net/ipv4/tcp_fin_timeout | 180 | 30 |
| net/ipv4/tcp_keepalive_time | 7200 | 1800 |
| net/core/netdev_max_backlog | 300 | 1024 |
| fs/file_max | 4096 | 16384 |
| fs/inode_max | 16384 | 65536 |

![](img/14d78e3cecac4581d37024baf1e94cca_852_0.png)

要重置 Linux 机器上网络栈的参数，请使用 shell 的 echo 命令重定向到 /proc 文件系统中的正确变量。 第 14 章 TCP/IP Networking 从

