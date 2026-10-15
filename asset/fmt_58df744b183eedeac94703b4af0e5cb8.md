
`dpkg-reconfigure` 实用程序用于重新配置已安装的软件包配置，它会在任何基于字符的设备（包括终端模拟器）下显示图形化窗口。以下命令允许你交互式地重新配置 exim4：

```
$ dpkg-reconfigure exim4-config
```

第一个窗口显示拆分配置与非拆分配置（第 721 页）之间的差异，告诉你可以在哪里找到此主题的更多信息，并询问你是否要设置拆分配置（图 20-1）。如果你选择使用拆分配置，`dpkg-reconfigure` 会为 `dc_use_split_config` 赋值 `true`。

# SPAMASSIN

垃圾邮件工具是一个过滤器。也就是说，它从标准输入读取每封邮件，将其发送到 spam 处理，并将修改后的邮件写入标准输出。守护进程使用多种技术识别垃圾邮件：

- 标头分析：检查发送垃圾邮件的人使用的为了让邮件看起来合法的技巧。
- 正文分析：检查邮件正文的垃圾邮件特征。
- 黑名单：检查列表以查看发送者是否已知会发送垃圾邮件。
- 数据库：对比 Vipul's Razor（razor.sourceforge.net，垃圾邮件跟踪数据库）检查邮件签名。

## SpamAssassin 如何工作

在 spam 运行时，你可以通过设置一个字符串来查看垃圾邮件如何工作：

+   - spam

## SPAMASSIN 729

当然，SpamAssassin 报错是因为你提供的字符串不包含此处的报告的核心内容。逻辑行以 X-Status contains Yes 开头（它认为该消息是电子邮件）。SpamAssassin 使用一种评分系统，为每封邮件分配若干个命中（hits）。如果邮件收到的命中数达到（默认为 5.0），SpamAssassin 就会将其标记为垃圾邮件。该状态中列出的原因详细列见下方的 **内容分析详情：** 部分。

以下是经 SpamAssassin 处理的一封真实垃圾邮件。它收到了 24.5 次命中，这几乎肯定是一个失误。

```
X-Spam-Status: Yes, hits=24.5-received=6
tests_IN_FUTURE,06.12,INVALID_DATE, TZ_ABSURD,
MISC,ON_SPAM_KEY,OVERLOOK,TIME
MISC,SPAM_ZEROS,ZERODD,RCVD_IN_DSBL,RBL_IN_NJABL
RCVD_IN_UNCONFMED,DSBL_REMOVE_PAGE,VACATION_SAMPLE,
NJABL_OPEN_PROX
************************************
X-Spam-Checker: SpamAssassin v5.3.6 (1.7.2.1-2023-05-10-exp)
X-Spam-Report: 这封邮件看起来像垃圾邮件。原始邮件始终附在邮件中。在此报告中，你可以报告或清除类似的模糊细节。
内容分析详情：热带三周假期
在那些地方有大量的**女性、性、酒精、每件事等等！**等
邮件垃圾邮件通过各种类型的短语出现。
内容分析详情：（24.5 次命中，需要 5 次）
INVALID_DATE,TZ_ABSURD (4.5 分) 无效日期：（匹配器不存在）
MISC,SPAM_ZEROS,4 (4.0 分) 被垃圾工具检测到（4零变体）
VACATION_SAMPLE (1.9 分) 正文：假期
RCVD_IN_DSBL (6.8 分) 名为 "report" 的页面 URL
MISC,OUTLOOK_TIME (6.0 分) 位于 Outlook（Outlook 格式）
DATE_IN_FUTURE,06_12 (1.3 分) 于接收日期之后 6 天
RCVD_IN_NJABL (2.6 分) 通过 njabl.org 的中继接收
RCVD_IN_UNCONFMED (2.5 分) 通过 unconfirmed.dsbl.org 的中继接收。
RBL 检查：找到 94.99.198.200.unconfirmed.dsbl.org。
NJABL,OPEN_PROX (2.6 分) 这是一个代理/中继/正式/垃圾源
RCVD_IN_DSBL (2.6 分) 通过 list.dsbl.org 的中继接收。
RBL 检查：找到 211.157.63.200.list.dsbl.org。
X-Spam-Flag: YES
Subject: [Spam] re: statement
```

730 第 20 章 exim4: 设置邮件服务器、客户端及其他

# 配置 SPAMASSASSIN

SpamAssassin 在许多位置查找配置文件；详细信息请参阅 spamassassin 手页。最易操作的配置文件是 `/etc/mail/spamassassin/local.cf`。你可以编辑此文件来全局配置 SpamAssassin。用户可以覆盖这些全局选项，并在 `~/.spamassassin/user_prefs` 文件中添加自己的选项。你可以将本节讨论的选项放在这两个文件中的任何一个。

例如，你可以配置 SpamAssassin 重写被其评为垃圾邮件的邮件主题（Subject）。配置文件中的 `rewrite_header` 关键字控制此行为。该关键字后面的单词 `Subject` 告诉 SpamAssassin 重写主题行。删除下行行前面的 `#` 即可开启此行为：

```
# rewrite_header Subject ********
```

`required_score` 关键字指定了邮件在被 SpamAssassin 视为垃圾邮件之前必须收到的最低分数。默认值为 5.00。将此关键字的值设置为更高的数字，可以使 SpamAssassin 标记较少的邮件。

```
required_score 5.00
```

有时，本应标记为垃圾邮件的地址没有标记，或者不应标记为垃圾邮件的地址被标记了。使用 `whitelist_from` 关键字指定永远不应标记为垃圾邮件的地址，使用 `blacklist_from` 指定永远不应标记为垃圾邮件的地址：

```
whitelist_from =sans@example.com
blacklist_from =@spammer.net
```

你可以在 `whitelist_from` 和 `blacklist_from` 行上指定多个由空格分隔的地址。每个地址都可以通配符。要将所有从 example.com 域名发送邮件的人加入白名单，使用 `whitelist_from *=@example.com`。你可以使用多行 `whitelist_from` 和 `blacklist_from`。

# 在邮件服务器上运行 SPAMASSASSIN

本节介绍了如何在邮件服务器上设置 SpamAssassin，以便其在所有投递到本地系统的邮件发送之前对其进行处理。它展示了如何使用 `procmail` 作为 MDA，并让 `procmail` 通过垃圾过滤器发送邮件。

同时，请确保服务器系统上安装了 `procmail` 软件包。接下来，如果 `/etc/procmail` 配置文件不存在，请创建它，确保该文件所有者为 root，权限为 644 并包含以下内容。如果已存在：

```
# /etc/procmail
: | /usr/bin/procmail
```

770

`/etc/procmail` 的第一行是到 `procmail` 的管道。下一行是运行 `procmail` 的命令，而 `/etc/procmail` 的最后一行是运行邮件过滤器的命令。

```
:0 | /usr/bin/procmail
```

你也可以创建自己的 `procmail` 脚本。例如，你可以创建一个将所有邮件转发到特定地址的脚本：

```
:0 | mail -v user@example.com
```

你也可以用 `procmail` 过滤掉垃圾邮件。例如，你可以创建一个删除具有特定主题邮件的脚本：

```
:0 /Spam/ /dev/null
```

你还可以用 `procmail` 将邮件移动到特定文件夹。例如，你可以创建一个将具有特定主题的邮件移动到文件夹的脚本：

```
:0 /Spam/ deliver -d /home/user/Mail/spam
```

你还可以用 `procmail` 修改某些邮件的优先级。例如，你可以创建一个设置紧急邮件优先级的脚本：

```
:0 /Urgent/ mail -v -p 5 user@example.com
```

你还可以用 `procmail` 为某些邮件添加头信息。例如，你可以创建一个为所有工作邮件添加头的脚本：

```
:0 /Work/ mail -v -H "X-Priority: High"
```

你还可以用 `procmail` 删除某些邮件。例如，你可以创建一个删除来自特定发件者的所有邮件的脚本：

```
:0 @spammer.example.com /dev/null
```

你还可以用 `procmail` 转发某些邮件。例如，你可以创建一个转发所有关于特定项目的邮件的脚本：

```
:0 /Project/ mail -v project@example.com
```
