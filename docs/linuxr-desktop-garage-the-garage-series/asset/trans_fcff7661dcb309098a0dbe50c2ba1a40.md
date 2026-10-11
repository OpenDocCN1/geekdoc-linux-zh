

最好直接从这里开始，并按照链接到最新发行版进行安装。安装过程就在您的浏览器中完成。根据您安装 Mozilla 或 Firefox 的方式，您可能需要以 root 用户身份运行浏览器才能安装 ChatZilla。如果您不确定，请以 root 身份运行该程序。

## 以 Root 身份运行

以 root 身份运行图形用户界面（GUI）程序最简单的方法是什么？当然是终端，例如：

```bash
$ su
Password:
# mozilla &
```

别忘了，命令末尾的 & 符号会在后台运行程序，让您的终端保持空闲以便执行更多命令。

当程序安装完成后，您需要重启浏览器。关闭并重新打开 Mozilla 或 Firefox，然后查看菜单。在 Mozilla 中，请转到 Window > IRC Chat。在 Firefox 中，请转到 Tools > ChatZilla。Firefox 还允许您选择将 ChatZilla 添加为工具栏按钮。

1.  打开 ChatZilla（见图 10.8）。
2.  您最初看到的屏幕充满了“[INFO]”信息。其中包含可用网络的列表。只需选择其中一个：点击 freenode 开始。
3.  系统会提示您输入昵称。输入一个并点击确定。选择一个日后不会让您感到尴尬的名字。
4.  更多的消息会不断滚动。如果您成功加入服务器，您应该能在所有其他信息的末尾看到类似以下内容：
    - `-- End of /MOTD`
    - `== User mode for [your user name] is now + i`
    - MOTD 是“今日消息”（Message of the Day）。之前滚动过去的许多文本就是它。只需在窗口中向上滚动即可阅读——其中一些相当有趣。
5.  现在您需要找到一个要加入的频道。频道就像一间充满交谈者的人的房间。要列出活动频道，请输入：
    - `/list`

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_272_0.png)

在 freenode.org 这样的大型服务器上返回的列表可能很长。您可以使用 `-min` 和 `-max` 选项来限制返回的频道数量：

```bash
/list -min 5
```

这将返回至少包含五个人的频道。您还可以访问 http://www.irchelp.org/irchelp/channelist 查看用于查找频道的搜索引擎。

### 图 10.8
ChatZilla。

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_273_0.png)

6.  在 Freenode.net 上，您可能可以进入 `#newirc` 和 `#newsr` 频道而不会惹上太多麻烦。您使用 `/join` 命令加入频道：

    ```bash
    /join #newsr
    ```

    如果您发现自己是频道中唯一的人，请不要感到惊讶。如果是这样，没关系；只需练习一些命令，也许还可以对自己表达一些诗意的动作。

7.  要说话，只需输入并点击回车。要表达动作，请使用 `/me` 命令，然后完成句子。*例如*：

    ```bash
    /me is a genius
    ```

    当我登录为

    ```
    ** susan is a genius
    ```

    时会显示出来。

8.  要离开，请使用 `/leave`。

## 几个基本的 IRC 命令

表 10.1：IRC 命令

| IRC 命令 | 结果 |
|---|---|
| /help | 显示来自该服务器的帮助信息，这可能是一个很长的列表 |
| /join #philosophy | 加入名为 philosophy 的频道 |
| /leave 或 /part | 离开频道，但保留在服务器上 |
| /list | 列出服务器上的频道 |
| /me dances like a cowboy | ** [您的用户名] dances like a cowboy |
| /msg josh | 向昵称为 josh 的用户发送私人消息 |
| /nick newnickname | 更改您的用户名——在此情况下改为 newnickname |
| /invite | 邀请另一位用户加入频道 |
| /quit see ya | 退出 IRC 并发送告别信息 "see ya" |

## XChat

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_274_0.png)

每组程序中都有稳定可靠的资深老将。对于 IRC 聊天来说，那个稳定的程序就是 XChat。如果您是 IRC 的新手，XChat 可能是您的最佳选择，因为它让新手的一切都变得简单。一旦启动 XChat，您会看到几个简单的字段，用于填写您的用户名（默认为您的 Linux 用户名）以及要加入的服务器列表。选择一个服务器，主要的 XChat 窗口就会弹出。

在主窗口中（见图 10.9），您会看到左侧是聊天区，底部是命令区，右侧是用户列表。菜单中充满了选项，如果您不知道对应于这些操作的 IRC 命令，或者只是不想输入它们，这些选项将为您提供帮助。服务器菜单中包括“加入频道”和“离开频道”等选项。在“设置”菜单下，您甚至可以通过浏览“设置 > 列表 > 用户命令”中的列表来学习一些新的 IRC 用户命令。

### 图 10.9
XChat 的主窗口。

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_275_0.png)

连接到服务器后，使用 /list 查找频道，或者在线搜索一个，然后使用 /join #channelName 加入。使用 XChat 时，您可能不会遇到任何技术问题——只可能会遇到一些人际关系问题。请保持礼貌，与其他人友好相处，并确保您能按时回家吃晚饭。

## 简评

| 程序 | 易用性 | 界面 | 评论 |
| :--- | :--- | :--- | :--- |
| Gaim | 很好 | 良好 | Gaim 功能齐全。与许多 GNOME/GTK 程序一样，它缺乏其 KDE 对应程序在设计和功能上的一些花哨之处，但在功能上有所创新。Gaim 开发人员有定期发布，并且在修复报告的错误方面反应最快。拥有平行的 Windows 版本意味着，即使您因某种原因必须使用 Windows，也可以保留相同的程序和界面。此外，该程序是自包含的，在 KDE 和 GNOME 中都能同样出色地运行 |
| Kopete | 良好 | 很好 | Kopete 起步较慢，但在大多数方面已赶上 Gaim，同时添加了一些独特的功能。如果您是 KDE 桌面的常规用户，Kopete 与 KAddressBook、系统托盘和 KNotify 集成的功能将非常棒 |
| Yahoo! Messenger | 良好 | 公平/较差 | 使用他们的客户端时，您永远不用担心无法连接到 Yahoo 不断变化的协议，但您的功能也不会那么多。值得钦佩的是，Yahoo! 关心到为他们自己的即时通讯程序制作了一个 Linux 版本，但如果他们能保持更新就好了。不仅与其他 Linux 程序相比，其界面看起来很旧，而且它甚至没有跟上 Yahoo 的 Windows 客户端的功能。保留此程序作为备用是个好主意。 |
| ChatZilla | 公平 | 公平 | ChatZilla 是一个相当新的程序，Mozilla 将其列为尚未完成。该程序是那些运行正常但没有有趣小工具可供玩耍的程序之一。您可以直接从浏览器启动它，这很方便。 |
| XChat | 良好 | 良好 | XChat 专为 IRC 聊天设计，而这正是它做得好的地方。内置的服务器列表和精心设计的菜单选项使其成为最直观、最易用的 IRC 客户端。 |

## 链接

- Jabber: http://www.jabber.org/
- Jabber 服务器列表: http://www.jabber.org/user/publicservers.php
- Gaim: http://gaim.sourceforge.org
- Gaim 的 SourceForge 论坛: https://sourceforge.net/forum/?group_id=235
- Gaim-festival (Gaim 的语音插件): http://festival-gaim.sourceforge.net/
- Gaim 的插件: http://gaim.sourceforge.net/plugins.php
- Kopete: http://www.kopete.org/
- Yahoo! Messenger: http://messenger.yahoo.com/
- Mozilla.org 上的 ChatZilla: http://www.mozilla.org/projects/ir-messaging/chatzilla/
- ChatZilla 用户指南: http://www.mozilla.org/projects/ir-messaging/chatzilla/user-guide.html
- XChat: http://www.xchat.org/
- IRC 帮助页面: http://www.irchelp.org/

![](img/f2b5f4073f00f9ec5546d9acb9cc6448_278_0.png)

# 音乐和电影

有些人确实很忙。大部分其他的忙碌者可以分为两类。有一类人喜欢说自己很忙，因为这让他们觉得自己很重要。这些忙碌的人经常告诉你他们睡得有多少，他们要跑多少腿，他们手头上有多少项目。他们夸耀这一切，好让你认为这些忙碌的人是特别的人，他们如此不可或缺，连一分钟都坐不下来。还有一类忙碌的人说自己很忙，是为了逃避他们本该做的事情。这些忙碌的人只有在被要求做一些令人不快的任务或参加不想要的社交活动时才会开口。突然之间，他们变得很忙。

“亲爱的，你准备好帮我洗车了吗？”我丈夫在一个下午喊道。

我环顾房间寻找脱身的借口，寻找出路。我当时只是在电脑上看电影并整理我的 MP3 收藏。

“苏珊？”他重复道。

我需要回应。“对不起，我不行。我现在真的很忙。”猜猜我是哪种忙碌的人。

“你在做什么？”他问。

