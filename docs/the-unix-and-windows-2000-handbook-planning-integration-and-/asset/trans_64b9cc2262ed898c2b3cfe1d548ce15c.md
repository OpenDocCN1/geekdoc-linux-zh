

## Listing 9.5 Ruleset Output for Remote User

```
> 3,0 dsw@anyxyz.com
rewrite: ruleset 3 input: dsw @ anyxyz . com
rewrite: ruleset 96 input: dsw < @ anyxyz . com >
rewrite: ruleset 96 returns: dsw < @ anyxyz . com >
rewrite: ruleset 3 returns: dsw @ anyxyz . com
rewrite: ruleset 0 input: dsw @ anyxyz . com
rewrite: ruleset 199 input: dsw @ anyxyz . com
rewrite: ruleset 199 returns: dsw @ anyxyz . com
rewrite: ruleset 98 input: dsw @ anyxyz . com
rewrite: ruleset 98 returns: dsw @ anyxyz . com
rewrite: ruleset 198 input: dsw @ anyxyz . com
rewrite: ruleset 95 input: < > dsw @ anyxyz . com >
rewrite: ruleset 95 returns: dsw < @ anyxyz . com >
rewrite: ruleset 198 returns: $# esmtp $@ anyxyz . com $: dsw < @ anyxyz . com >
rewrite: ruleset 0 returns: $# esmtp $@ anyxyz . com $: dsw < @ anyxyz . com >
>
```

Ruleset 3 的返回将地址重写为 Sendmail 可以在内部处理的格式。Ruleset 0 返回一个元组，其中包含 ESMTP（扩展 SMTP）的投递代理、anyxyz.com 的主机以及用户 dsw。这表明 Sendmail 将连接到机器 anyxyz.com 的邮件服务器以投递此消息。此结果表明你的 sendmail.cf 将处理向远程用户发送电子邮件。一旦你测试了代表性的远程和本地地址样本，你需要将配置文件（在我们的示例中为 sniglets.com.cf）复制到 /etc/sendmail.cf。接下来，编辑启动脚本（在第 3 章“系统启动和关闭”中介绍），以自动启动 Sendmail 守护进程。

> 客户端 sendmail.cf 配置文件应导致所有电子邮件都被转发到主配置文件中指定的邮件服务器。

## STARTING SENDMAIL

邮件服务器应作为守护进程在后台运行 Sendmail。这允许 Sendmail 监听来自其他邮件服务器的传入连接。还必须指示 Sendmail 在一定时间间隔内处理待处理队列。如果 Sendmail 守护进程无法联系收件人的邮件服务器，消息将被放入队列。队列需要定期处理以尝试投递所有排队的消息。这可通过以下命令实现：

```sh
#!/usr/sbin/sendmail -bd -q30m
```

-bd 选项使 Sendmail 以守护进程方式运行，而 -q30m 要求 Sendmail 每 30 分钟处理一次待处理队列。其他选项包括用于调试的 -d 和用于详细模式的 -v。

客户端 UNIX 工作站（非邮件服务器）不需要在后台以守护进程方式运行 Sendmail。来自客户端工作站的电子邮件会立即投递到邮件服务器。如果邮件服务器不可用，消息将被排队。

## QUEUE

Sendmail 会尝试立即投递邮件。当无法立即投递时，Sendmail 会保留消息并在稍后尝试投递（-q60m 选项）。排队的邮件被放置在保留目录（/var/spool/mqueue）中，并称为已排队。消息在队列目录中被拆分为单独的文件。每个文件名以单个字符标识符（表 9.4）开头，其后是字母 F，然后是每个单独消息的唯一标识符。Sendmail 接受命令行选项来处理队列。在“启动 Sendmail”部分中的示例中，我们使用了 -q30m。该选项指示 Sendmail 每 30 分钟尝试投递队列中的所有消息。

客户端 UNIX 工作站上的排队电子邮件也必须进行处理。客户端上的排队电子邮件是由于客户端无法联系邮件服务器所致。由于客户端未运行 Sendmail 守护进程，因此必须使用另一种方法来处理队列。在客户端 UNIX 工作站上，将以下行添加到 root 的 crontab 中：

```
0 * * * * /usr/sbin/sendmail -q
```

此命令可确保邮件队列每小时处理一次，并且当邮件服务器可用时，已排队的电子邮件将被投递到邮件服务器。

mailq 命令（/usr/sbin/sendmail -bp）会打印出邮件队列的摘要。其输出示例如下所示：

```
Mail Queue (2 requests)
--Q-ID--  --Size--  --Q-Time--  --Sender/Recipient---------
0AA14869     843 Tue Dec 28 14:57 <webb@sniglets.com>
                 (Deferred: Connection timed out with mail.nowhere.net.)
                 george@nowhere.net
0AA14794    1780 Tue Dec 28 14:53 <ox@sniglets.com>
                 (Deferred: Connection timed out with mail.somewhere.com.)
                 user@somewhere.com
```

第一行提供队列中电子邮件消息的总数量。剩余的行提供队列中每条消息的信息。每条消息的第一行包含标识符（ID）、消息大小、消息进入队列的日期/时间以及发件人的

