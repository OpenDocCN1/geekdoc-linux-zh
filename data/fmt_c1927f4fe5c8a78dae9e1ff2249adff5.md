
# UNIX 无界：入门方法

## 第 9 章 UNIX 通信

```
$ /etc/wall [Return]
Alert ... [Return]
Lab will be closed in 5 minutes. Time to log out. [Return]
[Ctrl-d]
$
Broadcast message from david
Alert ...
Lab will be closed in 5 minutes. Time to log out.
```

而底部屏幕显示对方输入的内容。例如，如果你输入 `talk daniel` 并按 `[Return]` 键，你的屏幕会分成两部分，你的屏幕上会出现以下消息：

```
[waiting for your party to respond]
```

以及以下消息出现在 `Talk_daemon@xyz at 111:22`：

```
talk: Connection requested by david@xyz
talk: Respond with: talk david@xyz
```

Daniel 通过输入 `talk david@xyz` 来响应。

现在，Daniel 的屏幕被分为两个部分，对话开始。要结束会话，参与的任何一方都可以按 `[Ctrl-c]`，并在两个终端上都会显示以下消息。

```
[Connection closing. Exiting]
```

如果 Daniel 使用了 `talk` 命令来阻止消息，你的终端上将显示以下消息：

```
[Your party is refusing]
```

### 图 9–6

对话：上方屏幕是 David 的；下方屏幕是 Daniel 的。

```
[Connection established]          david's screen
Hi Dan!
Is today's meeting still on?
Hi Dave
Yes. Be there!
Bye.
```

```
[Connection established]          daniel's screen
Hi Dave!
Yes. Be there!
Bye.
Hi Dan
Is today's meeting still on?
```

### 电子邮箱

电子邮箱（e-mail）是现代环境中不可或缺的一部分。电子邮件让你能够在用户之间发送和接收消息、备忘录和其他文档。使用电子邮件发送邮件与使用 `write` 命令之间的主要区别在于，使用 `write` 命令时，只有在你登录时才能看到发送给你的消息；而对于电子邮件，你的邮件会自动保存直到你阅读它。电子邮件服务比传统邮件更方便、更快速，且不会通过电话打扰接收方。

在 UNIX 下，可以使用 `mail` 或 `talk` 命令。...（注：原文后续部分似乎存在乱码或重复的文本，已根据指令对有效内容进行翻译和处理）

要向 Daniel（登录名 `daniel`）发送消息，请执行以下操作：

- `mailx daniel [Return]` ... 向 `daniel` 发送消息。
- `Subject: meeting [Return]` ... 输入主题。

```
Hi, Dan [Return]
请告诉我明天的会议是否仍然举行。 [Return]
Dave [Return]
[Ctrl-d] ................. 信号指示消息结束。
EOT ............................ 传输结束。
$ _ ............................ 回到提示符。
```

1. 主题（`Subject`）字段是可选的。只需按 `[Return]` 即可跳过主题提示。
2. 在空行开头按 `[Ctrl-d]` 发送消息的结束信号。
3. 无论对方用户是否登录，邮件都会投递到该用户的邮箱中。
4. 收件者一登录，就会收到有邮件的通知。以下消息将出现在他们的终端上：

`You have mail`（你有邮件）

#### 9.2.3 阅读邮件

为了阅读邮件，你输入 `mailx` 而不带任何参数。如果你的邮箱中有邮件，`mailx` 会显示两行信息，随后是邮箱中邮件头部的编号列表，然后是 `mailx` 提示符（默认是一个问号）。此时，邮件处于命令模式，你可以使用命令来删除、保存或回复消息等。在 `?` 提示符处按 `[q]` 即可退出 `mailx`。

头部列表由邮箱中的每个邮件项一行组成。格式如下：

```
> status message # sender date lines/characters subject
```

头部行中的每个字段都传了有关你邮件的某些信息：

- 状态（`status`）指示这是当前的消息。
- 如果消息是新的，状态为 `N`。这意味着你还没有读过这封邮件。
- 如果消息不是新的，状态为 `U`（未读）。这意味着你以前看过该邮件头部，但尚未阅读邮件本身。
- 消息编号（`message #`）表示邮件在邮箱中的序号。
- 发送者（`sender`）是给你发邮件的人的登录名。
- 日期（`Date`）显示邮件到达邮箱的日期和时间。
- 行/字符（`line/characters`）通过行数和字符数显示邮件的大小。

假设你是 Daniel，你刚刚登录并想要阅读你的邮件。

![](img/9bc78cf6fd0dc9f28ed030a3704f5a4d_275_0.png)

- 系统通知你你有邮件：

`You have mail`

- 要阅读邮件，输入 `mailx` 并按 `[Return]`；UNIX 响应如下：

```
mailx version 4.0 Type ? for help.
"/usr/students/mail/daniel": 1 message 1 new
> N 1 david ... Thu Nov 28 14:14 8:126 meeting
```

1. 第一行头部显示你的 `mailx` 版本号，并告知你你可以按 `[?]` 获取帮助。
2. 第二行头部显示 `/usr/mail/daniel`（即你的系统邮箱），后面接着是消息的数量和状态。在这种情况下，你有一封邮件，`N` 表示这是你第一次阅读它。

`?` 提示符表示 `mailx` 处于命令模式。你通过输入相关的消息编号来指定邮件。你也可以按 `[Return]` 从当前邮件（由头部上的 `>` 符号指示）开始阅读，并在 `?` 后按 `[Return]` 继续顺序阅读邮件。

> ? mailx in command mode.

```
? 1 [Return] 显示消息 1，即你邮箱中唯一的邮件。
Message 1
From: david, Thu, 28 Nov 01 14:14 EDT 2001
To: daniel
Subject: meeting
Status: R
Hi, Dan
请告诉我明天的会议是否仍然举行。
Dave
> ? Ready for the next command.
? q [Return] 退出 mailx。
Saved 1 message in /usr/students/david
$ 回到 shell。
```

当你使用 `q` 退出 `mailx` 时，它会将你读过的邮件保存到主目录下的私有邮箱中（因此，此时你的系统邮箱是空的）。

假设你想再次阅读邮件。输入 `mailx` 并按 `[Return]`；UNIX 响应：

```
No mail for daniel
```

查看你邮箱中的内容。

```
$ cat mbox [Return] . . . . . . 查看你邮箱中的内容。
From: david, Thu, 28 Nov 14:14 EDT 2001
To: daniel
Subject: meeting
Status: RO
Hi, Dan
请告诉我明天的会议是否仍然举行。
Dave
```

如你所料，`mbox` 包含了你的邮件。

#### 9.2.4 退出 mailx：q 和 x 命令

你可以在 `?` 提示符处输入 `q`（quit）或 `x`（exit）来退出 `mailx`。这两个命令以不同的方式退出 `mailx`。`q` 命令会导致删除你从系统邮箱读过的邮件。默认情况下，被删除的邮件副本保留在私有邮箱中（赋值给变量 `MAIL`）。`x` 命令不会删除你从系统邮箱读过的邮件。事实上，当你使用 `x` 时，邮箱中的内容保持不变。

##### mailx 选项

这些选项在调用 `mailx` 读取或发送邮件时在命令行中使用。以下序列显示了 `mailx` 选项的使用：

```
$ mailx -H [Return] . . . . . . 显示邮件头部。
N1 daniel Sep 30 12
N2 susan Sep 30 30
N3 marie Sep 30 13
```

| 选项 | 操作 |
| --- | --- |
| `-f [filename]` | 从指定文件而不是系统邮箱读取邮件。如果没有指定文件，则从 `mbox` 读取。 |
| `-H` | 显示头部列表。 |
| `-s subject` | 将主题字段设置为字符串。 |

输入 `mailx -f mymail` 并按 `[Return]` 从指定文件而不是系统邮箱读取；UNIX 响应：
