
**代码列表 11.6** `.forward` 文件应该引用 `vacation` 文件。

- 3. 保存文本并退出编辑器。
  第 4 章详细介绍了在 `pico` 和 `vi` 中保存和退出的详尽细节。

- 4. `vacation -I`
  在提示符处输入 `vacation -I` 来启动 `vacation` 并告诉它响应所有传入的消息。你仍然会在收件箱中收到这些邮件，而且事实上，它们会堆积在你的收件箱等待返回。

- 5. `~/.forward`
  查看家目录下的 `.forward` 文件，验证它是否包含对 `vacation` 程序的引用。你的 `.forward` 文件指定了在收到邮件时应该发生什么。在示例中，它应该由 `vacation` 处理。对 `vacation` 的引用通常由 `vacation` 程序自动插入，但如果那里没有，你需要添加 `\your, "vacation yourid"`。当然，请将上面的占位符替换为你真实的用户 ID，并可能包含 `vacation` 的完整路径（在我们系统上是 `/usr/bin/vacation`）。（参见**代码列表 11.6**。）

![](img/30f4227f5df2c6cea63896bef2fc574f_263_0.png)

## 提示

- 在开始休假之前，记得从所有邮件列表中取消订阅。如果你这样做，你可能会向一整群不在乎的人发送休假通知（不要骚扰邮件列表管理员！）。更糟糕的是，你可能会导致邮件循环！（在那种情况下，发送给列表的消息会被服务器确认，而确认信息又启动了 `vacation` 通知），导致成百上千条消息堆积在你的账户中。这不应该发生，但有时会发生。

- `mv .forward vacation-forward`
  在提示符处，将引用 `vacation` 程序的 `.forward` 文件重命名为另一个名称（在此情况下为 `vacation-forward`）。你也可以直接删除它或移除对 `vacation` 的引用，但将其保存起来更方便，这样你下次休假就可以重复使用它。

## 配置 procmail

让我们看看……来自老板的 2 条消息……来自收藏家讨论组的 17 条消息……噢，嘿，妈妈发来的一条消息……还有……

管理 Unix 生活的最佳方法之一就是使用 `procmail`（一个邮件过滤程序）自动处理你的某些电子邮件。

在本节中，我们将展示如何配置传入的消息。如图 11.16 和 11.17 所示，你需要完成两件事来设置系统管理 `procmail`：

- 为 `procmail` 指定设置（图 11.16）。例如，邮件通常直接进入你的收件箱；然而，`procmail` 在邮件到达收件箱之前对其进行过滤，你需要告诉 `procmail` 你的邮件文件夹在哪里，以及其他。

- 告诉 `procmail` 执行它的工作（图 11.17）。本质上，你创建一个 `.forward` 文件，将你的邮件发送给 `procmail` 处理。

![](img/30f4227f5df2c6cea63896bef2fc574f_264_0.png)

### 为 procmail 指定设置

- 1. `pico ~/.mailrc`
  首先，访问家目录下的 `procmailrc`。

- 2. `LOGFILE=$HOME/.mailog`
  为 `procmail` 提供一个记录活动的地方。

- 3. `PATH=/usr/bin:/local/bin`
  指定程序的路径。

- 4. `DEFAULT=$HOME/mail`
  指定邮件的去向。

- 5. `MAILDIR=$HOME/FriGolBuddies`
  指定过滤后的邮件去向。

- 6. `~/forward`
  使用你喜欢的编辑器创建。

### 使用 procmail 响应邮件

`procmail` 可以帮助你自动或选择性地响应邮件。编写一个配方：

- 1. `vi ~/.procmail`
  在 `vi` 中访问你的 `.procmail` 文件。

- 2. 移动到文件末尾，设置信息下方。

- 3. `::`
  使用 `:0:` 开始一个新的配方，如图 11.18 所示。

- 4. `* ^TGFuddies`
  设置 `procmail` 过滤的标准。在这里，`* ^T` 告诉 `procmail` 检查所有传入消息的收 行（实际上也 CC 行）。`GolBuddies` 是行中匹配的文本。

- 5. `MAILDIR/FriGolBuddies`
  指定过滤后的邮件去向。

- 6. 保存并关闭文件。

```
Activate Vacation Program

:0

| /usr/bin/vacation jdoe

:0

| *TGFuddies

|MAILDIR/FriGolBuddies
```

![](img/30f4227f5df2c6cea63896bef2fc574f_265_0.png)

# 发送和读取邮件

## 使用 procmail 转发邮件：

- 1. `pico ~/.procmailrc`
  首先，启动你的编辑器并编辑你之前在主目录中创建的 `.procmailrc` 文件。

- 2. `:0;`
  在文件的末尾新起的一行添加 `:0;`，这会启动一个 procmail 配方（recipe）。这基本上是告诉 procmail 在处理邮件时“锁定”你的邮件目录。

- 3. `! myotheremail@example.com`
  提供一个感叹号 `!` 以及以及要将邮件发送到的地址。

- 4. 保存并关闭文件。

现在，你所收到的所有邮件都将自动转发到 `myother-email@example.com`。

## 使用 procmail 丢弃垃圾邮件

以下是配方：

```
:0:
* !TAO.*aw@.*raycomm
$MAILDIR/spam
```

该配方使用正则表达式来过滤那些并非明确发送给以 `@` 开头且以 `raycomm` 结尾的用户 ID 的消息，并将它们放入一个名为 `spam` 的特殊文件夹。将垃圾邮件过滤器放在规则列表的末尾，这样所有来自你的邮件列表和其他消息都会首先被分类。在测试此功能并确保你喜欢它且它不会漏掉重要邮件后，你可以将最后一行改为 `/dev/null` 以直接丢弃垃圾信息。

对于更复杂、高级的垃圾邮件解决方案，请在 Google 上搜索“procmail spam filter”访问 `http://www.google.com/` 查看相关选项。

## 使用 procmail 调用 vacation（自动回复功能）：

- 1. `pico ~/.procmailrc`
  首先，访问你的编辑器并编辑你之前在主目录中创建的 `.procmailrc` 文件。

- 2. `:0 c`
  `| /usr/bin/jdoe`
  在文件的末尾新起的一行添加该配方，用于发送一份副本（`c` 代表 copy）给 `vacation` 程序（注意：此处应在第一行末尾添加 `c`）。关于 `vacation` 程序的更多信息请参见本章节。

- 3. 保存并关闭文件。

现在，你收到的所有邮件都将被存储并交给 `vacation` 程序进行处理。

## 提示

字体 你的 `.procmailrc` 文件按顺序处理。一旦匹配到入站邮件配方，它就会执行。所以如果没有匹配到任何配方，邮件将投递到指定的默认位置（之前）。

- 在配置好 `procmail` 后，请保持耐心。有时 `procmail` 会按特定的时间处理邮件（例如每小时），所以测试它可能需要一些时间。

# procmail 配方示例

以下带有注释的配方将帮助你开始使用 `procmail`。

```
# 根据 To;, Cc: 等类似的头部过滤

:0:
* ^TO.*awr@.*raycom.com
$MAILDIR/interesting

# 根据主题过滤

:0:
* ^Subject:.*Status
$MAILDIR/reports

# 根据发送者过滤

:0:
*^From:.*spammer@example.com
$MAILDIR/DELETE

# 根据发送者直接丢弃垃圾

:0:
*^From:.*spammer@example.com
/dev/null

# 根据大小过滤（大于1000 字节）

:0:
* >1000
$MAILDIR/longish
```
