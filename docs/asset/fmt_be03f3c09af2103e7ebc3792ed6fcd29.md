
![](img/6ffd6bb320ccf354f5a4d57c9d95190d_253_0.png)

图 11.13 你的签名文件可以包含你想要的任何信息。发挥创意，但保持简洁！

如果你使用电子邮件有一段时间了，你肯定已经注意到签名文件，它们出现在消息底部，包含联系信息、公司名称，也许还有一句简短的搞笑引言或格言。你可以通过创建 `.signature` 文件（图 11.13）为你的外发消息添加签名。

### 创建签名文件：

1. `pico ~/.signature`
在 shell 提示符下，输入编辑器的名称（这里我们使用 `pico`，但你可以使用你选择的编辑器），指定主目录（使用 `~/`），然后指定 `.signature` 文件名。请注意文件名中的前导点，这会使文件隐藏。

2. `Eric J. Ray ejray@raycomm.com`
`My thoughts are my own ... is that OK, honey?`
继续输入你的签名信息（图 11.13）。我们建议你的 `.signature` 文件至少包含你的姓名和电子邮件地址。你还可以添加搞笑的说法（“你知道你是个极客，当你把去洗手间称为‘下载’时。”）或免责声明（“我的观点是我的，不是我的公司的。”）。你想要什么都可以。尽量让你的签名尽可能简短；过长的签名很难阅读。

3. 保存并退出文件。
如果你使用 `pico` 或 `vi`，你可以在第 4 章中获得快速提醒。

## ✓ 提示

- 如果你想让你的签名更华丽，使用 `figlet`，它是对字母的文本表示，如代码清单 11.5 所示。查看 www.yahoo.com 或你最喜欢的互联网搜索引擎并搜索 “figlet” 或 “figlet generator” 以获取有关创建自己的 figlet 的更多信息。
- 许多电子邮件纯粹主义者认为四行是最长的签名长度。如果你创建更长的签名，期望有些人会因此责骂你。
- `mutt` 和 `pine` 都会自动在外发邮件中包含 `.signature` 文件。

```
[ejr@hobbes ejr]$ more figlet

    ____       ____
   / __ \     / __ \
  / /_/ /____/ /_/ /____
 / ____/_____/ _, _/ ___/
/_/     /_/|_| |_|\___/

    ...figlet ASCII art...
```

代码清单 11.5 Figlets 很有趣也很花哨。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_255_0.png)

图 11.14 你所要做的就是告诉 Unix 你希望将你的消息转发到哪里。

## 提示

- 请咨询你的系统管理员，看看 `.forward` 文件是否真的能实现你想要的功能。许多较新的 Linux 和 Unix 系统会自动将邮件发送到 `procmail`（并忽略 `.forward` 文件），因此你可能需要使用 `procmail` 配方来转发你的邮件。它同样有效，只是不同。请参阅本章后面关于 `procmail` 的部分了解详情。
- 如果你愿意，你可以保留所有传入消息的副本（在你的收件箱中，就在它们通常所在的位置）并将其转发给不知情的收件人。只需输入 `yourid, otheraddress.com`（用当前系统上的你的用户 ID 替换 `yourid`，用要转发邮件的地址替换另一个）。
- 转发消息在你更换 ISP 时也很方便。你可以将发送到旧地址的所有消息转发到新地址，这有助于确保你在朋友和同事更新地址簿的同时仍能收到所有重要消息。

## 转发传入消息

假设你是某个大项目的老板，每个人都向你发送所有重要的相关电子邮件消息。你可以告诉 Unix 自动将这些传入消息转发给真正会采取行动的人。嘿，你是老板，对吧？或者也许你只是获得了不同的电子邮件帐户，并且希望将发送到旧地址的所有传入邮件转发到新地址。如图 11.14 所示，你所要做的就是创建一个 `.forward` 文件。

### 转发传入电子邮件消息：

1. `vi ~/.forward`
开始时，在 shell 提示符下输入 `vi`（或你使用的编辑器的相应命令），指示你的主目录（使用 `~/`），然后将 `.forward` 作为文件名。

2. `mynew@raycomm.com`
将文件第一行添加为你希望转发电子邮件的地址（图 11.14）。除了转发到单个地址外，你还可以使用包含多行多个地址的 `.forward` 文件，一次将传入邮件发送到多个地址。

3. 保存并关闭文件。
请参阅第 4 章，了解使用 `pico` 或 `vi` 保存和关闭文件的详细信息。

## 使用 vacation 宣布缺席

如果你计划休假并且将有一段时间无法查看邮件，让 Unix 帮你宣布缺席（图 11.15）。使用 `vacation` 程序，你可以让 Unix 向给你发邮件的每个人发送回复，说明你已不在办公室。

请记住，`vacation` 在不同的 Unix 系统和 ISP 之间差异很大。你拥有的可能与此处使用的“标准”形式不同。如果遇到任何问题，请务必向系统管理员咨询具体说明，同时也查看本章的 `procmail` 部分，因为许多较新的 Linux 和 Unix 系统使用 `procmail` 而不是 `.forward` 文件来告诉 `vacation` 回复你的邮件。

### 使用 vacation 发送“我正在休假”邮件：

1. `vi ~/vacation.msg`
在 shell 提示符下，输入 `vi ~/vacation.msg`。你需要编辑一条消息（实际上是一个模板），作为人们给你发邮件时应收到的休假通知，如图 11.15 所示。

2. `Subject: away from my mail!`
Thanks for emailing me about `$SUBJECT`. Fortunately for me, I’m taking a fabulous vacation mowing my lawn, doing laundry, and catching up on other things I can’t do because I usually work so much. If you would like me to stay on vacation, please email my boss (boss@example.com) and let her know. Thanks!
创建并编辑文本，说出你想要的内容。
文本中的 `$SUBJECT` 术语将被替换为发送给你的邮件的实际主题。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_256_0.png)

3. 保存文本并退出编辑器。
第 4 章详细介绍了在 `pico` 和 `vi` 中保存和退出的操作。

4. `vacation -I`
在 shell 提示符下输入 `vacation -I` 以启动 `vacation` 并告诉它回复所有传入邮件。你仍然会在收件箱中收到传入邮件。事实上，它们会堆积在你的收件箱中，等待你回来。

5. `cat ~/.forward`
查看主目录中的 `.forward` 文件，以验证其中包含对 `vacation` 程序的引用。你的 `.forward` 文件指定了邮件收到后应如何处理。在此示例中，它应由 `vacation` 处理。对 `vacation` 的引用通常由 `vacation` 程序自动插入，但如果没有，你需要编辑 `.forward` 文件并添加类似 `yourid, "|vacation yourid"` 的文本。当然，将上面的占位符替换为你的真实用户 ID，并可能包含 `vacation` 的完整路径（在我们的系统上为 `/usr/bin/vacation`）。（参见代码清单 11.6。）

代码清单 11.6 你的 `.forward` 文件应引用 `vacation` 文件。

```
[ejr@hobbes ejr]$ cat ~/.forward
ejr, "|vacation ejr"
[ejr@hobbes ejr]$
```

### 提示

- 在开始 `vacation` 之前，请记得取消订阅所有邮件列表。如果你不这样做，你会向一大群可能不在乎的人发送休假通知（更不用说你会真的惹恼列表管理员！）。或者更糟，你可能会导致邮件循环（你的列表邮件会被服务器确认，而确认邮件又会被发送休假通知），导致数百或数千条邮件积压在你的账户中。理论上不应该发生，但有时确实会发生。

### 停止 vacation 邮件：

- `mv .forward vacation-forward`
在 shell 提示符下，将引用 `vacation` 程序的 `.forward` 文件移动到不同的名称（在本例中为 `vacation-forward`）。你可以简单地删除它或移除对 `vacation` 的引用，但保存它以便下次休假时重复使用会更方便。

## 配置 procmail
