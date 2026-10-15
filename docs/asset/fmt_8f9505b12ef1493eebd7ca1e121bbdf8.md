
`$ mailx`

Mail version 5.0. Type `?` for help.

`"/var/mail/taylor"`: 9 messages 5 new

1 disserli Mon Nov 22 19:40 54/2749 "Re: Are you out there"

>N 2 Laura.Ramsey Tue Nov 30 16:47 46/1705 "I've got an idea..."

N 3 ljw Fri Dec 3 22:57 130/2712 "Re: Attachments"

N 4 sartin Sun Dec 5 15:15 15/341 "I need your address"

N 5 rustle Tue Dec 7 15:43 29/955 "flash cards"

6 harrism Tue Dec 7 16:13 58/2756 "Re: Writing Lab OWL proj"

7 CBUTCHER Tue Dec 7 17:00 19/575 "Smartphone Based GRE's"

8 harrism Tue Dec 7 21:46 210/10636 "writing environments"

N 9 v892127 Wed Dec 8 07:09 38/1558 "Re: Have you picked up"

& _

这里有很多信息。第一行，程序标识自己为 Mail version 5.0。在顶部角落稍显隐蔽地提醒我，随时可以输入 `?` 获取命令帮助。

第二行告诉我正在读取哪个邮箱。在这个例子中，我查看的是收件邮件的默认邮箱，即 `/var/mail/taylor`。在你的系统上，你可能会在这个目录中找到你的邮箱，也可能在类似的目录 `/usr/mail` 中找到。无论如何，你都不必担心它的位置，因为 Berkeley Mail 可以自动找到它。

第 3 到 11 行列出了我从不同人那里收到的邮件消息。格式是：如果之前未看过该邮件，第一列为 `N`；一个唯一的索引号（每个列表中的第一项是 1）；发送消息的账户；消息发送的日期和时间；消息的行数和字符数；以及消息的主题（如果已知）。图 20.1 更清楚地说明了这一点。

![](img/036fe100817eada43c999b050270081b_365_0.png)

**图 20.1：理解 mailx 中的消息显示。**

### 2. 要阅读特定消息，我只需输入该消息的索引号：

```
& 7

Message 7:

From: CBUTCHER Sun Dec 7 17:00:28 2014

From: Cheryl <CBUTCHER>

Subject: Smartphone Based GRE's

To: Dave Taylor <TAYLOR>

I've scheduled to take the smartphone-based GRE's in Indy.

Call me crazy but someone's got to do it. I'll let you know how it goes.

Do you know anyone else that has taken the GRE's this way? I figure there's a paper in it somewhere......

```

如果你手头有研讨会上的那份讲义文件，能否请把它发给我？

谢谢。

& _

这条消息来自我的朋友 Cheryl Butcher。消息中第一组行——每行都是一个单词、一个冒号以及一些其他信息——是消息的头部，即邮戳和信封的电子等价物。头部始终包含 `From:`、`Subject:` 和 `To:`，分别指定发件人的姓名和电子地址、消息的主题以及收件人列表。

### 3. 要回复这条消息，我输入 `reply`：

```
& reply

To: CBUTCHER

Subject: RE: Smartphone Based GRE's

-
```

我现在输入的任何内容都将发回给 Cheryl：

```
Hi. I am very interested in hearing about your reaction to the smartphone-based GRE test. I'm sure you're correct that there is a paper there, but wouldn't it be best to work with ETS on the project?

I'll dig around and find those handouts soonest.

Happy holidays!

Dave
```

要结束消息，我只需在单独一行按 `^d` 或单独使用简写 `.`：

```
.
Cc: _
```

Berkeley Mail 现在要求我指定是否还有其他人希望收到此消息的抄送。在此输入一个或两个账号名称即可让指定人员看到发给 Cheryl 的此消息的副本。因为我不想让任何其他人阅读此消息，所以我按 Return，这会发送消息并将我返回到提示符：

```
& _
```

### 4. 我现在可以使用 `headers` 命令查看当前消息（即我刚刚阅读的那条）。它是 `>` 所指示的消息（参见图 20.1）：

```
& headers

  1 disserli Mon Nov 22 19:40  54/2749 "Re: Are you out there"

  2 Laura.Ramsey Tue Nov 30 16:47  46/1705 "I've got an idea..."

N  3 ljw      Fri Dec   3 22:57 130/2712 "Re: Attachments"

N  4 sartin   Sun Dec   5 15:15  15/341 "I need your address"
```

```
1 disserli Mon Nov 22 19:40 54/2749 "Re: Are you out there"

2 Laura.Ramsey Tue Nov 30 16:47 46/1705 "I've got an idea..."

N 3 ljw Fri Dec 3 22:57 130/2712 "Re: Attachments"

N 4 sartin Sun Dec 5 15:15 15/341 "I need your address"

N 5 rustle Tue Dec 7 15:43 29/955 "flash cards"

>N 9 v892127 Wed Dec 8 07:09 38/1558 "Re: Have you picked up"

&
```

#### Tip

Berkeley Mail 中的大多数命令都可以缩写为首字母——正如上面 `h` 是 `headers` 的快捷方式所示——这减少了打字量。

### 7. 你可以通过在 `save` 命令和文件夹名称之间指定数字来将一组消息保存到文件中：

```
& save 6 8 harris

6: Inappropriate message
```

糟糕。我已删除了 6 和 8 号消息。在继续之前我必须先恢复它们：

```
& undelete 6 8

& save 6 8 harrismail

"harrismail" [New file] 268/13392
```

### 8. 现在我使用 `quit` 命令退出此程序：

```
& quit

Saved 1 message in mbox

Held 6 messages in /var/mail/taylor

$
```
