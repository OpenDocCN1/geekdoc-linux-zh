

## 提示

- 请向你的系统管理员确认是否真的需要一个 .forward 文件。许多 Linux 和 Unix 系统会自动检查 .procmailrc 文件，即使没有 .forward 文件。
- 设置好 procmail 处理后，请耐心等待。有时 procmail 会按特定时间表处理邮件（例如每小时），因此测试可能需要花费一些时间。
- 使用 tail -f .maillog 来实时监控日志。这会告诉 tail 不断显示文件的末尾，即使文件正在被添加内容。使用 Ctrl+C 停止。

## 3. PATH=/usr/bin:/usr/local/bin:/bin

指定你的可执行程序的路径。现在就这样做是个好主意，以防你最终使用 procmail 更广泛地过滤或自动回复消息。

## 4. DEFAULT=/var/spool/mail/yourid

指定你的传入邮件的位置。请记住，过滤器在邮件到达收件箱之前就会获取邮件，因此你需要告诉 procmail 你的收件箱在哪里。请向系统管理员确认 DEFAULT。 (/var/spool/mail/yourid 通常是位置，但并非总是如此，当然要使用你的真实用户 ID，而不是 yourid。)

## 5. MAILDIR=$HOME/mail

指定 procmail 应该找到你的邮件程序以及它创建的所有文件夹和信息的位置。如果你使用 pine，你可能会完全按照所示输入这一行。如果你使用 mutt，你可能需要使用 Mail 而不是 mail。

## 要启用 procmail 过滤：

- 1. pico ~/.forward
  使用你喜欢的编辑器在你的主目录中创建 .forward 文件。
- 2. "!IFS= '' && exec /usr/bin/procmail -- -f - || exit 75 #yourid"
  完全按照所示输入文本，但将上面的 yourid 替换为你的用户 ID（图 11.17）。如果 procmail 不在 /usr/bin，请输入实际位置。/usr/local/bin 也是另一个可能的目录。
- 3. 保存并关闭文件。
  就这样！现在你只需等待传入消息，看看它们是否按你的预期被过滤（你将在下一节中设置）。

## 使用 procmail 回复邮件

procmail 可以帮助你自动或有选择地回复邮件。正如你将看到的，procmail 与转发邮件和使用 vacation 程序非常相似，但你可能会发现 procmail 更灵活。

## 要指定消息应如何被过滤（“编写配方”）：

- 1. vi ~/.procmailrc
  在 vi 中访问你的 .procmailrc 文件。
- 2. 移到文件的末尾，设置信息下方。
- 3. :0:
  使用 :0: 开始一个新配方，如图 11.18 所示。（不要问为什么使用 :0:。这就是它的方式。）
- 4. * ^TOGolfBuddies
  设置 procmail 用于过滤的标准。这里。
  ▲ * ^TO 告诉 procmail 检查所有传入消息的 TO 行（实际上也包括 CC 行）。
  ▲ GolfBuddies 是要在 TO 行中匹配的文本（如 TO: GolfBuddies@nowhere.nowhen.com）。当然，你应该输入要查找的列表的实际名称（或你的邮件列表的别名，或其他内容），而不是 GolfBuddies。
- 5. $MAILDIR/FriGolfBuddies
  指定过滤后的邮件应去往的位置。在这种情况下，过滤后的邮件将进入 FriGolfBuddies 文件夹，但你可能会将邮件列表的消息过滤到 listmail 文件夹。
- 6. 保存并关闭文件。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_260_0.png)

## 要使用 procmail 转发邮件：

- 1. `pico ~/.procmailrc`
  首先，访问你的编辑器并编辑你在主目录中之前创建的 `.procmailrc` 文件。
- 2. `:0:`
  在文件底部的空行添加 `:0:`，以启动 procmail 配方。这基本上告诉 procmail 在处理邮件时“锁定”你的邮件目录。
- 3. `! myotheremail@example.com`
  提供管道 (!) 和要发送邮件到的地址。
- 4. 保存并关闭文件。
  现在你收到的所有邮件都将自动转发到 myotheremail@example.com。

## 使用 procmail 丢弃垃圾邮件

以下配方。

```
:0:
* !TO. *cwr@*. *raycomm.com
$MAILDIR/spam
```

过滤未明确发送给用户 ID 为 @ 前的 cwr 且末尾为 raycomm.com 的消息，并将它们放入名为 spam 的特殊文件夹。将垃圾邮件过滤器放在规则列表的末尾，以便所有来自你的邮件列表和其他重要消息都被先归档。测试此设置并确保你喜欢它且不会丢弃有价值的消息后，你可以将最后一行更改为 /dev/null 以直接丢弃垃圾。

有关更复杂和更复杂的垃圾邮件解决方案，请查看 http://directory.google.com/Top/Computers/Software/Internet/Clients/Mail/Unix/Procmail/Filtering_Spam/ 上的选项。

