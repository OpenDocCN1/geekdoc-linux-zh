
Connected to `nessl.server.net`

Escape character is "*"

`200` `nessl.server.net` DINERS Version 5.2c, posting OK

`HELP`

`500` command not recognized

`HELP`

`100` Legal commands:

`authinfo user Name:pass`

`article [MessageID][Number]`

`body [MessageID][Number]`

`check MessageID`

`date`

`group newsgroup`

`head [MessageID][Number]`

`help`

`have`

`last`

`List [active|inactive,times[newsgroups[subscriptions]]]`

`newsgroup`

`mode stream`

`mode reader`

`gnewsgroups yymmd hmmss [GMT] [<distributions>]`

`newness newsgroups yymmd hmmss [GMT] [<distributions>]`

`next`

`post`

`slave`

`stat [MessageID][Number]`

`takethis MessageID [group_pattern]`

`xtitle header [range]MessageID`

`xldr header [range]MessageID`

`over [range]`

`xpat header [range]MessageID pat [norepat...]`

提交了 `HELP` 命令，并返回了合法命令列表。注意，最初且刻意地提交的命令是 `HELP`。该命令是无效的，服务器做了相应的响应。

命令从客户端提交到 NNTP 服务器。如果服务器没有响应，可以重新发送命令。下一节将讨论服务器响应。

## NNTP 服务器响应

响应可以是两种类型之一：状态或文本。数字状态行标识与命令相关的响应。状态代码由三位数字组成。表 17.3 描述了第一位。

| 第一位代码 | 说明 |
|---|---|
| 1xx | 信息消息 |
| 2xx | 成功 |
| 3xx | 命令正常 |
| 4xx | 命令未执行 |
| 5xx | 发生了错误 |

表 17.3. NNTP 响应，第一位

| 状态代码 | 说明 |
|---|---|
| 100 | 返回帮助文本 |
| 190-199 | 调试输出 |
| 200 | 服务器就绪。 |
| 201 | 服务器就绪。允许发布。 |
| 400 | 服务正在终止 |
| 500 | 命令无法识别 |
| 501 | 提供的命令语法错误 |
| 502 | 访问限制或权限拒绝 |
| 503 | 程序故障；命令未执行 |

表 17.4. NNTP 响应，第二位

| 状态代码 | 说明 |
|---|---|
| 0x | 通用状态代码 |
| 1x | 标识选择 |
| 2x | 标识响应 |
| 3x | 标识功能 |
| 4x | 标识分布 |
| 8x | 标识消息 |
| 9x | 用于调试 |

第二种响应是文本响应。它在数字状态行之后发送，指示故障。文本格式本身以单独行的 CR/LF 对（`.`）结束。如果文本以点开头，该行将包含两个点（`..`）。客户端程序必须验证每一行，检查长点或双点，并做出相应。以下示例演示了：

```
stispy telnet nessl.att@local.net mnt

Trying 943.432.123...

Connected to nessl.server.net

Escape character is "*"

200 nessl.server.net DINERS Version 5.2c, posting OK

HELP

500 command not recognized

HELP

100 Legal commands:

authinfo user Name:pass

article [MessageID][Number]

body [MessageID][Number]

check MessageID

date

group newsgroup

head [MessageID][Number]

help

have

last

List [active|inactive,times[newsgroups[subscriptions]]]

newsgroup

mode stream

mode reader

gnewsgroups yymmd hmmss [GMT] [<distributions>]

newness newsgroups yymmd hmmss [GMT] [<distributions>]

next

post

slave

stat [MessageID][Number]

takethis MessageID [group_pattern]

xtitle header [range]MessageID

xldr header [range]MessageID

over [range]

xpat header [range]MessageID pat [norepat...]
```

注意，在提交 `HELP` 命令后，服务器返回了命令列表。列表以单独行的单点（`.`）结束。如果文本以点开头，该行将包含两个点（`..`）。

文本消息通常用于显示给用户。状态代码通常会被解释并对用户隐藏，因为代码本身并不具信息性。

# 命令响应详情

本节详细介绍了 NNTP 命令及其相关的响应。更多详细信息请参阅 RFC 977。

## ARTICLE 命令

`ARTICLE` 命令的语法如下：

```
ARTICLE message-id
```

接收到此命令后，服务器将显示所标识文章的头部、一个空行以及文章的正文（文本）。所标识的 `message-id` 是文章头文件中的消息 ID。内部维护的“当前文章指针”保持不变。

以下是 `ARTICLE` 命令的一种可选用法：

```
ARTICLE [nnn]
```

在上述 `ARTICLE` 命令的用法中，将显示当前或指定文章的头部、一个空行和正文（文本）。参数 `nnn` 是可选的，它是新闻组中文章的数字 ID。如果提供该参数，则显示当前文章。

如果使用了有效的文章编号，将设置当前文章指针。响应将指示当前文章编号。

`message-id` 字段可用于清除重复文章，因为该 ID 对于每个文章都是唯一的。

以下列表显示了与 `ARTICLE` 命令相关的响应。`n` 代表文章编号，`a` 代表文章的消息 ID。

+ * `220 n a.` 文章已检索，随后将显示头部和正文。
* `221 n a.` 文章已检索，随后将显示头部。
* `222 n a.` 文章已检索，随后将显示正文。
* `223 na.`
* `412.` 未选择新闻组。
* `420.` 未选择当前文章。
* `423.` 指定的文章编号在该组中不存在。
* `430.` 未找到所标识的文章。

## GROUP 命令

`GROUP` 命令的语法如下：

```
GROUP ggg
```

新闻组的名字作为参数 `ggg` 提供。这是要加入（或选择）的新闻组。使用 `LIST` 命令可以获取提供的新闻组列表。

如果命令执行成功，将返回所选新闻组的第一篇和最后篇文章。此外，还会给出所有可用文章的总计数，但该计数仅为估值。推导出该计数的方法取决于具体实现。

一旦使用此命令选择了新闻组，当前文章指针将设置为第一篇文章。如果执行失败，则保持上一个新闻组和当前文章指针。

以下列表显示了提交 `GROUP` 命令后可能看到的响应。`n` 是新闻组的文章计数。`f` 指定第一篇文章。`i` 指定新闻组中的最后篇文章。`s` 表示新闻组的。

+ * `211 f s.` 标识所选的新闻组。
* `411.` 指定的新闻组不存在。

## HELP 命令

`HELP` 命令的语法如下：

```
HELP
```

接收到此命令后，服务器将返回其支持的可用命令列表。单独占一行的句号 `.` 标识列表的结束。

以下响应适用于 `HELP` 命令：

+ * `100.` 随后将显示帮助文本。

## IHAVE 命令

`IHAVE` 命令的语法如下：

```
IHAVE <messageid>
```
