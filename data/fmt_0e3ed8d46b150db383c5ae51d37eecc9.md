
# private_which `[bool]` (no) `<majordomo>`

如果设置为 `yes`，则请求者必须在邮件列表中才能获取该列表的 `which` 信息。

`private_which` = `no`

# private_who `[bool]` (no) `<majordomo>`

如果设置为 `yes`，则请求者必须在邮件列表中才能使用 `who` 命令。

`private_who` = `yes`

# purge_received `[bool]` (no) `<resend>`

在转发消息之前删除所有已接收行。

`purge_received` = `no`

任何后续帖子都应发送到主列表，而不是摘要列表。只有发送到主列表的消息才会被传递到摘要脚本。尽管我们设置别名的方式，任何直接发送到摘要的内容都会自动重新路由回主列表。

# reply_to `[word]` (digestonly-sample) `<resend,digest>`

将带有值 `<value>` 的 `reply-to` 头部放入外发消息中。如果使用令牌 `$SENDER`，则发送者的地址将用作 `reply-to` 头部的值这是 `reply-to` 头部的值，用于摘要列表。

`reply_to` = `Digestonly-sample@majordomo-host.mydomain.com`

```
# resend_host    [word] (undef) <resend>
# The host name that is appended to all address strings
# specified for resend.
resend_host      =
```

设置 `restrict_post` 为 `/dev/null` 可阻止任何人直接向摘要发布。

```
# restrict_post  [restrict_post] (undef) <resend>
# If defined only address listed in one of the files (colon
# or space separated) can post to the mailing list. This is
# less useful than it seems it should be since there is no
# way to create these files if you do not have access to
# the machine running resend. This mechanism will be
# replaced in a future version of majordomo/resend.
restrict_post    = /dev/null
```

```
# sender         [word] (owner-digestonly-sample-digest) <majord>
# The envelope and sender address for the resent mail. This
# string has "@" and the value of resend_host appended to
# it to make a complete address. For majordomo, it provides
# the sender address for the welcome mail message generated
# as part of the subscribe command.
sender           = owner-digestonly-sample
```

```
# strip          [bool] (yes) <majordomo>
# When adding address to the list, strip off all comments
# etc, and put just the raw address in the list file. In
# addition to the keyword, if the file <listname>.strip
# exists, it is the same as specifying a yes value. That
# yes value is overridden by the value of this keyword.
strip            = yes
```

```
# subject_prefix [word] (undef) <resend>
# This word will be prefixed to the subject line, if it is
# not already in the subject. The text is expanded before
# being used. The following expansion tokens are defined:
# $LIST - the name of the current list, $SENDER - the
# sender as taken from the from line, $VERSION, the version
# of majordomo.
subject_prefix   =
```

通常，摘要列表可能采用开放的订阅策略。然而，对于仅摘要列表，应将其关闭。

```
# subscribe_policy [enum] (open) <majordomo> /open;closed;auto/
# One of 3 possible values: open, closed, auto. Open
# allows people to subscribe themselves to the list. Auto
# allows anybody to subscribe anybody to the list without
# maintainer approval. The existence of the file
# <listname>.auto is the same as specifying the value
# auto. Closed requires maintainer approval for all
# subscribe requests to the list. In addition to the
# keyword, if the file <listname>.closed exists, it is the
# same as specifying the value closed. The value of
# this keyword overrides the value supplied by any existent
# files.
subscribe_policy = closed
```

每当创建摘要时，它都会存储在 `~majordomo/archives/digestonly-sample/`（即在主列表名称下），并发送给主列表的所有订阅者。

## 参考文献

《蝙蝠书》：Costales B 和 Allman E，《Sendmail》；O'Reilly。请查阅最新版本。

RFC 可从许多 FTP 档案库中获取。例如，对 RFC822 进行 Web 或档案搜索，应能提供许多获取位置。

1523 Borenstein, N. 文本/enriched MIME 内容类型。1993 年 9 月；15 页。 (Format: TXT=32692 bytes)

1522 Moore, K. MIME（多用途互联网邮件扩展）第二部分：非 ASCII 文本的消息头扩展。1993 年 9 月；10 页。 (Format: TXT=22503 bytes) (Obsoletes 1342)

1521 Borenstein, N.; Freed, N. MIME（多用途互联网邮件扩展）第一部分：指定和描述互联网消息正文格式的机制。1993 年 9 月；81 页。 (Format: TXT=187425 PS=393670 bytes) (Obsoletes RFC 1341)

1176 Crispin, M. 交互式邮件访问协议：版本 2。1990 年 8 月；30 页。 (Format: TXT=67330 bytes) (Obsoletes RFC 1064)

1056 Lambert, M. PCMail：个人计算机的分布式邮件系统。1988 年 6 月；38 页。 (Format: TXT=85368 bytes) (Obsoletes RFC 993)

822 Crocker, D. ARPA 互联网文本消息格式标准。1982 年 8 月 13 日；47 页。 (Format: TXT=109200 bytes) (Obsoletes RFC 733; Updated by RFC 1327, RFC 1148, RFC 1138)
