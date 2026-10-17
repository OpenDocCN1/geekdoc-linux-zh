
# 图 3.1 接收、阅读和存储邮件

桑丘在 `tty6` 上工作时，收到了以下系统消息：

`You have mail in /var/spool/mail/panzasan.`（你有新邮件在 `/var/spool/mail/panzasan`。）

请注意，这里，用户名文件是 `panzasan`。

桑丘的系统配置为每 10 分钟检查一次邮件。显然它已经执行了该操作，并向他发送了新邮件通知。为了检查邮件，桑丘输入：

```
$ mail<Enter>
Mail version 8.1.6/6/93 Type ? for help
"/var/spool/mail/panzasan" 2 messages 1 new
U 1 quixote@hostname.local Tue Jul 17 10:50 10/267 "Meeting at El
Toboso"
N 2 nicholas@hostname.local Tue Jul 17 11:05 16/311 "Meeting Postponed?"
&
```

请注意示例 3.12 中列出的每条消息开头的 `U` 和 `N` 标记。`U` 表示未读（这是从以前用户查看其邮件但未阅读该特定消息时遗留下来的状态）。`N` 标记表示新邮件。

当出现 `&` 提示符时，桑丘知道只需按 Enter 键即可立即检查未读消息。他这样做是为了阅读第一条消息，这是他上次检查邮件时未读的消息。

```
&<Enter>
Message 1:
From quixoted Tue Jul 17 10:15:47 2001
Date: Tue Jul 17 2001 10:15:47 -600
To: panzasan@hostname.localdomain
Subject: Meeting at El Toboso<Enter>
Sancho! Don't forget the meeting tonight at Lady Dulcinéa's!
Signed, Quixote de La Mancha
```

然后，桑丘通过输入以下命令阅读新消息 2：

```
& 2<Enter>
```

（因为我已经读完消息 1，所以我也可以在这里直接按 Enter。）

```
Message 2:
From nicholas Tue Jul 17 10:50:32 2001
Date: Tue, Jul 17 2001 10:50:32 -600
From: nicholass@hostname.localdomain
To: panzasan@hostname.localdomain
Subject: Meeting Postponed?
Sancho, Perez just dropped by my office. Please call us regarding the status of the meeting Don Quixote scheduled for tonight at Lady Dulcinéa's. The Don told us yesterday that he thought the meeting was a 'go' but that he had not received confirmation from the Lady yet. Is it still on? Meanwhile, are you keeping a close watch over him? We don't need another 'windmill' episode.

Nicholas and Perez
```

以下是几个子命令选项——也被称为子命令，因为它们调用各自的功能——用于阅读邮件：

- 要阅读列表中的第一条消息，按 Enter 或输入 `1` 然后按 Enter。
- 要跳过第一条消息并阅读第二条消息，输入 `2` 并按 Enter。
- 要阅读任何列表中的第一条新消息，输入 `t` 并按 Enter。
- 要按顺序阅读消息，只需从你选择的第一条消息开始，然后在阅读完每条消息后依次按 Enter。

在 `&` 提示符处，你也可以输入以下字母（以及其他）来查看消息：

| 命令 | 描述 |
| :--- | :--- |
| `f` | 列出邮箱中消息的标题 |
| `d` | 删除消息 |
| `m` | 转发消息 |
| `r` | 发送回复 |
| `q` | 退出 `mail`，并将未读消息保留在队列中 |
| `s` | 将消息附加到文件中 |

要在 `mail` 中获取可用子命令的完整列表，请在 `&` 提示符处输入 `?`。

那么，如果桑丘想要查看他过去收到并阅读过的消息怎么办？`mail -f` 命令显示其个人邮箱（即 `/home/panzasan/mbox` 文件）中消息的列表。通常，当他退出 `mail` 程序时，未送达（但已阅读）的消息会写回该 `mbox` 文件，而不是写回所有新消息都来自的（incoming）`/var/spool/mail/panzasan` 文件。通过启动 `mail` 的 `mail -f` 部分，他可以以处理 `/var/spool/mail/panzasan` 中通过 `mail` 使用的新或未读消息的方式，来查看和处理这些消息。图 3.1 展示了典型的邮件接收和存储过程。

## 向屏幕发送消息：`write` 和 `wall` 命令

本节讨论的两个命令都提供了联系系统上其他用户的功能：

- `write` 允许你联系一个或多个特定用户
- `wall` 允许你联系系统上的所有用户

让我们依次讨论每一个。

### `write` 命令

`mail` 命令向我们展示了如何向他人的邮箱发送消息，以及如何接收和操作我们邮箱中的消息。相比之下，`write` 命令立即在指定用户的屏幕上显示消息。你可以向本地系统或网络中其他系统上的用户发送消息（只需将 `username` 替换为 `username@hostname`）。如果使用 `who` 或 `finger` 确定目标用户登录了不止一个终端，除非你只想指定要将消息发送到的终端，否则你可以在所有终端上显示你的消息，如下所示：

```
$ write username ttyname/number<Enter>
```

否则，要在任何终端和所有终端上到达目标用户，语法仅为：

```
$ write username<Enter>
```

然而，要让特定用户接收消息，该用户必须在当时已登录，并且必须没有拒绝消息出现在其终端的权限。默认情况下，Linux 不会关闭 `write` 权限；该任务由用户通过 `msg` 命令完成（本章后面将涵盖）。

#### 注意

您无法关闭来自 `root` 用户的消息。

在写会话中，每个用户交替发送和接收消息。长消息可以放在文件中，并定向或重定向给其他用户。其语法是

```
$ write username < filename.ext<Enter>
```

示例 3.13 说明了两个用户如何使用 `write`。接收用户使用相同的语法回复发起用户。

#### 示例 3.13 `write`

唐吉诃德需要通知桑丘，杜尔西内娅女士（真名：阿尔东莎·洛伦索，但她早已放弃说服这位高尚的老绅士他搞错了。此外，人力资源协调员拥有她的正确姓名）已确认会议，因此他冒险打断桑丘，发送以下内容：

```
$ write panzasan tty4<Enter>
Sancho, Lady Dulcinea has confirmed that we can meet at El Toboso at 6!
BYO nachos y salsa!<Enter>
signed, Quixote de La Mancha<Enter>
<Ctrl>-d
```

桑丘立即在他的屏幕上收到以下内容：

```
Message from quixoted@hostname on tty2 at 13:13
Sancho, Lady Dulcinea has confirmed that we can meet at El Toboso at 6!
BYO nachos y salsa!
signed, Quixote de La Mancha
EOF
```

要返回他们自己的提示符，消息接收者必须按 Enter 键。

### `wall` 命令

`wall` 命令向所有已登录系统的用户发送公共消息。其语法是

```
$ wall textofmessage<Enter>
```

默认情况下，所有用户都可以使用 `wall` 命令。示例 3.14 展示了 `root` 用户使用 `wall` 命令的情况。

#### 示例 3.14 `wall`

周二上午早些时候，Freston 必须发送以下紧急消息（请记住，`root` 用户使用的是 `#` 提示符而不是 `$`）：

```bash
#### wall Warning!! System Going Down in 15 Seconds! Please Log Off Now!
Sorry, colleagues!<Enter>
```

每个已登录用户立即收到以下消息：
