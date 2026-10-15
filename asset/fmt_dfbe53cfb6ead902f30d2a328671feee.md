
```
# 将所有内核消息写入控制台。
# 其他日志会弄乱屏幕。
/kern.* /dev/console

# 记录任何（邮件外）级别为 info 或更高的内容。
# 不要记录私有的认证消息！
*.info:mail:news:news:authpriv.none:cron.none /var/log/messages

# authpriv 文件有限制访问。
authpriv.* /var/log/secure

# 将所有邮件消息存在一个地方。
mail.* /var/log/maillog

# 记录 cron 内容
cron.* /var/log/cron
```

# 所有人接收紧急消息

* .emerg

# 将级别为 crit及以上的新错误保存到特殊文件中。

uucp,news.crit

/var/log/spooler

# 将启动消息也保存到 boot.log

local.*

n/var/log/boot.log

#

# INN

#

news.=crit

news.=err

news.=notice

/var/log/news/news.crit

/var/log/news/news.err

/var/log/news/news.notice

以 `#` 字符开头的行是注释。其他行包含两列信息。左字段是分号分隔的列表（空格无效）的消息和消息优先级。右字段是这些消息应该写入的日志文件。

要将消息发送到另一台计算机（本地主机）而不是文件，首先将日志文件名替换为 `@` 后跟日志名称。例如，要将输出输出重定向到 `messages`、`secure` 和 `mailog` 日志文件，意味着在前面的文件中添加这些更改：

```
+   # 记录任何（邮件外）级别为 info 或更高的内容。
# 不要记录私有的认证消息！
*.info:mail.none;news.none;authpriv.none;cron.none @localhost

#  authpriv 文件有限制访问。
authpriv.*
@localhost

+   # 将所有邮件消息存在一个地方。
mail.*
@localhost
```

现在，消息将发送到 `localhost` 计算机上的 `syslogd`。主机名（`namehost`）的选择并不是随机的。惯例是创建一个主机名并将其作为作为 `localhost` 的系统别名。如果你以后需要将日志职责切换到不同的机器，你只需要更改日志别名：因此你不需要在每台计算机上重新编辑 `syslog.conf` 文件。

在 `localhost` 侧，必须带 `-r` 选项运行 `syslog`，这样它才会在网络上监听来自其他机器的日志消息。在 Fedora 中，这意味着在 `/etc/sysconfig/syslog` 文件的 `SYSLOG_OPTIONS` 变量中添加 `-r` 选项并重启 `syslog` 服务（`service syslog restart`）。`localhost` 必须能够访问 UDP 端口 `514` 以供 `syslog` 使用（检查 `/etc/services` 文件），因此你可能需要添加防火墙规则来允许。

## 第二部分 演示

### 理解 messages 日志文件

由于有许多程序和服务向 `messages` 日志文件记录信息，因此理解此文件的格式非常重要。你可以通过检查此文件来获取系统问题的早期预警。文件中的每一行都是某些程序或服务记录的一条消息。以下是实际 `messages` 日志文件的片段：

```
Feb 25 11:04:32 network: Bringing up loopback
Feb 25 11:04:32 network: Bringing up eth0
Feb 25 11:04:32 sshd: session opened for user root (pts/0)
Feb 25 11:04:32 sshd: session opened for user root (pts/1)
Feb 25 11:04:32 sshd: session opened for user root (pts/2)
Feb 25 11:04:32 sshd: session opened for user root (pts/3)
Feb 25 11:04:32 sshd: session opened for user root (pts/4)
Feb 25 11:04:32 sshd: session opened for user root (pts/5)
Feb 25 11:04:32 sshd: session opened for user root (pts/6)
Feb 25 11:04:32 sshd: session opened for user root (pts/7)
Feb 25 11:04:32 sshd: session opened for user root (pts/8)
Feb 25 11:04:32 sshd: session opened for user root (pts/9)
Feb 25 11:04:32 sshd: session opened for user root (pts/10)
Feb 25 11:04:32 sshd: session opened for user root (pts/11)
Feb 25 11:04:32 sshd: session opened for user root (pts/12)
Feb 25 11:04:32 sshd: session opened for user root (pts/13)
Feb 25 11:04:32 sshd: session opened for user root (pts/14)
Feb 25 11:04:32 sshd: session opened for user root (pts/15)
Feb 25 11:04:32 sshd: session opened for user root (pts/16)
Feb 25 11:04:32 sshd: session opened for user root (pts/17)
Feb 25 11:04:32 sshd: session opened for user root (pts/18)
Feb 25 11:04:32 sshd: session opened for user root (pts/19)
Feb 25 11:04:32 sshd: session opened for user root (pts/20)
Feb 25 11:04:32 sshd: session opened for user root (pts/21)
Feb 25 11:04:32 sshd: session opened for user root (pts/22)
Feb 25 11:04:32 sshd: session opened for user root (pts/23)
Feb 25 11:04:32 sshd: session opened for user root (pts/24)
```

文件中的每一行都是某些程序或服务记录的一条消息。以下是实际 `messages` 日志文件的片段：

- session opened for user root (pts/0)

- session opened for user root (pts/1)

- session opened for user root (pts/2)

- session opened for user root (pts/3)

- session opened for user root (pts/4)

- session opened for user root (pts/5)

- session opened for user root (pts/6)

- session opened for user root (pts/7)

- session opened for user root (pts/8)

- session opened for user root (pts/9)

- session opened for user root (pts/10)

- session opened for user root (pts/11)

- session opened for user root (pts/12)

- session opened for user root (pts/13)

- session opened for user root (pts/14)

- session opened for user root (pts/15)

- session opened for user root (pts/16)

- session opened for user root (pts/17)

- session opened for user root (pts/18)

- session opened for user root (pts/19)

- session opened for user root (pts/20)
