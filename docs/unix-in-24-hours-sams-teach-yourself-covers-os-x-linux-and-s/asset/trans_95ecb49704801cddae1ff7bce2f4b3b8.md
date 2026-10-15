

如果你手头有研讨会上的那份讲义文件，能否请把它发给我？

谢谢。

& _

这条消息来自我的朋友 Cheryl Butcher。消息中第一组行——每行都是一个单词、一个冒号以及一些其他信息——是消息的头部，即邮戳和信封的电子等价物。头部始终包含 From:、Subject: 和 To:，分别指定发件人的姓名和电子地址、消息的主题以及收件人列表。

3. 要回复这条消息，我输入 reply：

Click here to view code image

```
& reply
To: CBUTCHER
Subject: RE: Smartphone Based GRE's
-
```

我现在输入的任何内容都将发回给 Cheryl：

Click here to view code image

```
Hi. I am very interested in hearing about your reaction to the smartphone-based GRE test. I'm sure you're correct that there is a paper there, but wouldn't it be best to work with ETS on the project?

I'll dig around and find those handouts soonest.

Happy holidays!

Dave
```

要结束消息，我只需在单独一行按 ^d 或单独使用简写 .：

```
.
Cc: _
```

Berkeley Mail 现在要求我指定是否还有其他人希望收到此消息的抄送。在此输入一个或两个账号名称即可让指定人员看到发给 Cheryl 的此消息的副本。因为我不想让任何其他人阅读此消息，所以我按 Return，这会发送消息并将我返回到提示符：

```
& _
```

4. 我现在可以使用 headers 命令查看当前消息（即我刚刚阅读的那条）。它是 > 所指示的消息（参见图 20.1）：

Click here to view code image

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

## Tip

Berkeley Mail 中的大多数命令都可以缩写为首字母——正如上面 h 是 headers 的快捷方式所示——这减少了打字量。

## 7. 你可以通过在 save 命令和文件夹名称之间指定数字来将一组消息保存到文件中：

```
& save 6 8 harris
6: Inappropriate message
```

糟糕。我已删除了 6 和 8 号消息。在继续之前我必须先恢复它们：

Click here to view code image

```
& undelete 6 8
& save 6 8 harrismail
"harrismail" [New file] 268/13392
```

## 8. 现在我使用 quit 命令退出此程序：

Click here to view code image

```
& quit
Saved 1 message in mbox
Held 6 messages in /var/mail/taylor
$
```

我查看但未删除的消息会被移出我的收件箱到文件 mbox。我保存的消息和我标记为删除的消息会被静默移除，所有剩余消息保留在 /usr/spool/mail/taylor 中。

## Note

我对 Berkeley Mail 最大的抱怨是它对所有这些活动都保持沉默。我不喜欢已保存的消息在退出时会自动从收件箱中删除，更重要的是——我已阅读的消息会自动投入另一个文件夹。为了确保你在退出时已读消息不会被移入 mbox，你可以使用 preserve 命令，你可以用数字列表使用它，就像使用其他 Berkeley Mail 命令一样。你保留的任何消息都将保留在你的收件箱中。

你必须使用它才能熟练掌握，但它是值得的：Berkeley Mail 提供了相当多的功能，使你能够在命令行中轻松阅读电子邮件、保存邮件并根据需要回复，而无需离开命令行。该程序具有相当大的

