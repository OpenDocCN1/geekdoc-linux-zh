

# 378 新闻公告

第一个 tin 障碍可能已经开始了。取决于程序的编译方式，它会在启动时显示几条错误信息（这些信息在 xterm 中可能不可见）并立即退出。在这种情况下，它期望在 `/var/spool/news/` 下有一个新闻存档，该存档应由服务器创建。

tin 可以在不联系服务器的情况下读取存档。然而，如果没有任何本地服务器，或者使用了不同的本地服务器（如 leafnode），这个相当特殊的功能就会失效。尝试使用选项 -r 启动 tin：

```
user$ tin -r
```

# 使用方法

在首次启动时，tin 会从服务器将所有已知新闻组的列表传输到本地的 .newsrc 中。如果到服务器的互联网连接仅通过调制解调器，这将需要几分钟时间。（等待时间仅发生在首次启动。）随后，tin 将显示已订阅新闻组的空列表。

按 Y 显示所有未订阅新闻组的详细列表。现在，你可以使用光标移动到所需的新闻组，并按 S 订阅单个组，或者使用 Shift+S 订阅所有匹配给定模式的组。例如，你可以输入 os.linux.* 来选择所有 Linux 组。再次按 Y —— 屏幕大致如下：

```
Group Selection (localhost)               h=help

32 comp.os.linux.hardware
92 comp.os.linux.misc
3 comp.os.linux.networking
2 comp.os.linux.x
```

```
<=set current to n, TABnext unread,/search pattern, clatchup,\goto, jline down, kline up, help, move, quit, toggle all/unread,
subscribe, job pattern, unsubscribe, Unsubscribe pattern, yank in out
```

第二列中的数字表示你有多少篇未读的文章。要阅读新闻组中的文章，只需将光标移动到该行并按 -。现在，屏幕结构将看起来像这样：

```
2zfck signals error. Disk defective? Joerg Mertin
2 + 2 MC in color? Kai Straube
4 + 3 - no daemon present Joachim Zob
6 + 2 Problems with kernel compilation Stefan Lange
```

第二列需要一些解释。如果它包含一个数字，表示我们有一个包含 n 未读文章的线程。使用光标键，你可以选择一篇文章或一个线程。使用回车可以阅读文章。它会带你进入下一篇文章，返回列表。一旦文章被阅读，加号或线程数字将被移除。当你退出列表并再次访问它时，已读的文章将不再显示。

# 新闻客户端 379

如果你想再次查看已读过的文章，必须使用 Z 将整个组标记为“未读”。

下表列总结了 tin 最重要的键盘快捷键。请注意，某些快捷键仅适用于某些窗口（例如）：

# tin 键盘快捷键

- + ↑ 上一个/下一篇文章或新闻组
- - → 阅读新闻组或文章
- ← 返回上一个层级结构
- Tab 跳到下一篇未读的文章
- / 搜索文本

# 处理新闻

- + F 向新闻组发送回复（跟进），将其作为新文章发送
- R 直接以邮件形式向作者发送文章的回复（在文章窗口中）
- W 写写新文章
- T 标记文章
- M 将（标记的）文章或线程作为邮件发送
- S 将（标记的）文章或整个线程存储在文件中
- C 将此组中的所有文章标记为“已读”
- Z 将组中的所有文章标记为“未读”

# 处理组

- + S 订阅该组
- Shift+S 订阅多个组（带模式）（组必须可见，预先按 Y）
- U 取消对某个组的订阅
- Shift+U 取消对多个组的订阅（带模式）
- Y 显示所有命令或仅显示已订阅的新闻组

丰富的 man 文本描述了许多额外命令。可以通过 H 调用在线帮助，但它仅显示快捷键列表。根据发行版的不同，可以在 /usr/doc/tin/ 中找到更多信息。

你可以使用选项 -nq 来加速 tin 的启动。在这种情况下，它只考虑已订阅的组。无法订阅额外的组，tin 也不会检查新闻组在服务器上可用。

# 配置

tin 可以进行广泛配置。你可以直接修改文件 `.tin/tinrc`，或者在程序内部通过 Shift+M 调用配置对话框。除了其他，这还允许你激活颜色和鼠标支持。

# 编辑器

tin 没有自己的编辑器，并将 vi 作为其默认编辑器。你可以通过恰善设置 EDITOR 或 VISUAL 环境变量来防止这一点。

# 发送者地址

tin 通常使用用户、主机名和域名来构建发送者地址。在离线配置中，这很少是一个良好的解决方案；应该使用互联网账户的电子邮件地址。为此，可以通过 Shift+M 设置修改后的发送者地址（tinrc 中的 mail_address 选项）。

> 注意：如你所知，修改后的发送者地址对新闻文章有效，对通过 REPLY 发送的邮件无效。你应该使用你的邮件程序直接回复新闻文章。

# 11.3 离线新闻配置 (leafnode)

leafnode 是一种专门为小型新闻存档（最多几十个组）优化的新闻服务器。因此，leafnode 特别适用于在个人计算机上管理新闻存档。

> 提示 你可以在网上找到最新的 leafnode 版本：http://www.wuerzburg.de/~krasel/leafnode.html

# 安装与配置

到目前，许多发行版已在 contrib 目录下作为预配置包提供了 leafnode。如果不是，你需要从 FTP 服务器下载这个相当小的包。本章中的信息指的是版本 1.8，但对 1.8 之后的版本也同样有效（Leafnode 1.7 有缺陷，不应使用！）

# config

leafnode 的配置在 config 文件中进行，通常位于 /usr/lib/tin/config 或 /etc/leafnode。该文件中最重要的设置涉及 leafnode 应该从哪个新闻服务器或新闻服务器读取新闻文章。对于 305 页的示例用户，这是 news.provider.de。expires 关键字表示未使用的新闻线程应在服务器上保留多少天。默认设置为 20。initialfetch 指定了在订阅新闻组后，第一次读取多少篇新闻文章。如果你不设置限制，leafnode 将传输所有可用文章——这可能会非常耗时！

maxfetch 对当前操作有效。每当 leafnode 搜索新文章时，最多传输此数量的文章。如果你偶尔传输（例如每周一次）像 comp.os.linux.misc 等流行报的文章，请选择一个高值——否则你的本地新闻存档将是不完整的。值过高也不是好主意——传输许多新闻文章需要很长的时间。根据经验，每秒传输两篇新闻是一个现实的值。Leafnode 提供的 config 文件有详细注释。检查二进制文件所在的位置。

# /etc/ntpserver

此文件指定了本地客户端应该联系哪个服务器。由于 leafnode 现在运行在你的计算机上，你需要输入 localhost。

# SNNTPSERVER

此环境变量由某些新闻客户端评估，因此必须设置为 localhost。（在 SuSE 中，你在文件 /etc/rc.config 中设置 NNTPSERVER）

