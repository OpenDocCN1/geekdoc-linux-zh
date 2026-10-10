

其功能与 `--signature` 完全相同，只不过签名是从文件中读取的。

## `--suffix=.<sfx>`

在为生成的文件名添加后缀时，使用指定的后缀而不是 `.patch`。一种常见的替代方式是使用 `--suffix=.txt`。如果将此值留空，将会移除 `.patch` 后缀。

请注意，前导字符不一定要是点号；例如，你可以使用 `--suffix=-patch` 来生成类似 `0001-description-of-my-change-patch` 的文件名。

## `-q, --quiet`

不将生成的文件名打印到标准输出。

## `--no-binary`

不输出二进制文件中变更的内容，而是显示一个提示，说明这些文件已更改。使用此选项生成的补丁无法正确应用，但对于代码审查仍有用。

## `--root`

即使修订参数只是一个单独的提交（通常会被视为 `<since>`），也将其视为 `<revision range>`。请注意，包含在指定范围内的根提交始终被格式化为创建补丁，与该标志无关。

## 配置

你可以使用配置变量指定要添加到每条消息中的额外邮件头行、主题前缀和文件后缀的默认值、在输出多个补丁时对补丁进行编号、添加 "To" 或 "Cc:" 头、配置附件，以及签署补丁。

```
[format]
    headers = "Organization: git-foo\n"
    subjectPrefix = CHANGE
    suffix = .txt
    numbered = auto
    to = <email>
    cc = <email>
    attach [ = mime-boundary-string ]
    signOff = true
    coverletter = auto
```

## 讨论

`git format-patch` 生成的补丁采用 UNIX 邮箱格式，其中包含一个固定的“魔法”时间戳，用于表明该文件是 format-patch 的输出而非真正的邮箱，例如：

```
From 8f72bad1abf19a534559661343e21d6491c3908d3 Mon Sep 17 00:00:00 2001
From: Tony Luck <>
Date: Tue, 13 Jul 2010 11:42:54 -0700
Subject: [PATCH] =?UTF-8?q?|[IA64] Put ia64 config files on the ?
=?UTF-8?q?We Kleine-König diet?=
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 8bit
arch/arm config files were slimmed down using a python script (See
commit c2330e286f68f1c408b4aa6515ba49d57f05beae comment)
Do the same for ia64 so we can have sleek & trim looking...
```

通常，它会放在 MUA（邮件用户代理）的草稿文件夹中，在三个短划线之后编辑以添加应及时的评论（这些评论不应放入变更日志中），然后作为一条消息发送，在我们示例中，该消息的主体以“arch/arm config files were…”开头。在接收端，读者可以将有趣的补丁保存在 UNIX 邮箱中，并使用 `git am` 应用它们。

当一个补丁是 ongoing discussion（正在进行中的讨论）的一部分时，可以对 `git format-patch` 生成的补丁进行微调，以利用 `git am --scissors` 功能。在你对讨论的回复之后，会有一行仅由 “--- --->”（剪刀和穿孔线）组成，随后是移除了不必要头字段的补丁：

```
... > So we should do such-and-such. Makes sense to me. How about this patch?
--- --->
Subject: [IA64] Put ia64 config files on the Uwe Kleine-König diet
arch/arm config files were slimmed down using a python script...
```

以这种方式发送补丁时，通常你发送的是你自己的补丁，因此除了 “From $SHA1 $magic_timestamp” 标记外，你还应从补丁文件中省略 `From:` 和 `Date:` 行。补丁标题可能与该补丁所回复的讨论主题不同，因此你很可能需要保留 `Subject:` 行，如上例所示。

### 检查补丁损坏

许多邮件客户端如果没有正确设置，会破坏空白符。以下是两种常见的损坏类型：

- 没有任何空白字符的空上下文行。
- 开头多了一个空白字符的非空上下文行。

测试你的 MUA 是否设置正确的一种方法是：

- 按照你的常规方式将补丁发送给你自己，只是 `To:` 和 `Cc:` 行中不包含列表和维护者地址。
- 将该补丁保存为 UNIX Mailbox 格式的文件。例如，将其命名为 `a.patch`。
- 应用它：

```
git fetch <project> master:test-apply
$ git checkout test-apply
$ git reset --hard
$ git am a.patch
```

如果它没有正确应用，可能有各种各样的原因。

补丁本身没有干净利落地应用。这是*糟糕*的情况，但与你 MUA 的关系不大。在这种情况下，你可能需要在重新生成补丁之前使用 `git rebase` 对该补丁进行 rebase（变基）。

MUA 损坏了你的补丁；“am” 会抱怨补丁无法应用。查看 `.git/rebase-apply/` 子目录，查看 *patch* 文件包含的内容，并检查上述提到的常见损坏模式。

与此同时，也要检查 *info* 和 *final-commit* 文件。如果 *final-commit* 中的内容与你在提交日志消息中想要看到的内容不完全一致，那么接收者在应用你的补丁时很可能会手动编辑日志消息。补丁电子邮件中类似 “Hi, this is my first patch.\n” 的内容应该放在表示提交消息结束的三个短划线行之后。

## MUA 特定提示

这里有一些提示，介绍如何使用各种邮件客户端在线成功提交补丁。

### GMail

GMail 的 Web 界面没有关闭自动换行的方法，因此它会破坏你发送的任何电子邮件。不过，你可以使用 `git send-email` 并通过 GMail SMTP 服务器发送补丁，或者使用任何 IMAP 邮件客户端连接到 google IMAP 服务器，并通过该服务器转发电子邮件。

有关使用 *git send-email* 通过 GMail SMTP 服务器发送补丁的提示，请参阅 `git send-email` 的 EXAMPLE（示例）部分。

有关使用 IMAP 接口提交的提示，请参阅 `git imap-send` 的 EXAMPLE（示例）部分。

### Thunderbird

默认情况下，Thunderbird 不仅会自动换行，还会将电子邮件标记为 *format=flowed*（流动格式），这两者都会使生成的电子邮件无法被 Git 使用。

有三种不同的方法：使用附加组件关闭自动换行，配置 Thunderbird 不破坏补丁，或者使用外部编辑器以防止 Thunderbird 破坏补丁。

#### 方法 #1（附加组件）

安装可从 `<link>` 获取的 Toggle Word Wrap 附加组件。它会在编写器的“选项”菜单中添加一个“Enable Word Wrap”（启用自动换行）菜单项，你可以将其取消勾选。现在你可以像往常一样编写消息（复制 + 粘贴，`git format-patch` | `git imap-send` 等），但你需要手动为你输入的任何文本插入换行符。

#### 方法 #2（配置）

三个步骤：

1.  将你的邮件服务器配置为纯文本格式：编辑…账户设置…组成与寻址，取消勾选“以 HTML 格式编写消息”。
2.  配置你的常规组成窗口不换行。
    在 Thunderbird 2 中：编辑..首选项..组成，将纯文本消息换行设置为 0。
    在 Thunderbird 3 中：编辑..首选项..高级..配置编辑器。搜索 “mail.wrap_long_lines”。切换它以确保它设置为 false。另外，搜索 “mailnews.wraplength” 并将其值设置为 0。
3.  禁用 *format=flowed* 的使用：编辑..首选项..高级..配置编辑器。搜索 “mailnews.send_plaintext_flowed”。切换它以确保它设置为 false。

完成后，你应该能够像往常一样编写电子邮件（复制 + 粘贴，`git format-patch` | `git imap-send` 等），并且补丁不会被破坏。

#### 方法 #3（外部编辑器）

需要以下 Thunderbird 扩展：AboutConfig 和 External Editor。

1.  使用你选择的方法将补丁准备为文本文件。
2.  在打开编写窗口之前，使用 Edit à 账户设置取消勾选用于发送补丁的账户的“组成与寻址”面板中的“以 HTML 格式编写消息”设置。
3.  在 Thunderbird 主窗口中，*在你为补丁打开编写窗口之前*，使用 Tools à about:config 将以下项设置为指定值：
    ```text
    mailnews.send_plaintext_flowed => false
    mailnews.wraplength => 0
    ```
4.  打开编写窗口并点击外部编辑器图标。
5.  在外部编辑器窗口中，读取补丁文件并正常退出编辑器。

旁注：可能可以通过 about:config 和以下设置完成步骤 2，但尚无人尝试过。

```
mail.html_compose => false
mail.identity.default.compose_html => false
mail.identity.id?.compose_html => false
```

**contrib/thunderbird-patch-inline** 中有一个脚本，可以帮助你轻松地使用 Thunderbird 包含补丁。要使用它，请执行上述步骤，然后使用外部编辑器作为该脚本。

### KMail

这可以帮助你使用 KMail 以内联方式提交补丁。

1.  将补丁准备为文本文件。
2.  点击“新邮件”。
3.  在编写窗口中，进入“选项”并确保未设置“自动换行”。
4.  使用 Message à 插入文件… 并插入补丁。
5.  回到编写窗口：在消息中添加你希望的任何其他文本，完成地址和主题字段，然后按发送。

