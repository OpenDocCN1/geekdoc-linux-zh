
接下来，点击 Mozilla 浏览器本身的 `Window`（窗口）菜单，并选择 `Mail & Newsgroups`（邮件与新闻组）。第一次执行此操作时，会显示 `Account Wizard`（账户向导）；你可以在此设置电子邮件和新闻账户。如果你需要更改信息，可以在 `Mail and News` 窗口中打开 `Edit` 菜单并选择 `Mail & Newsgroup Account Settings`（邮件与新闻组账户设置）。此外，如果你点击 `Mail and News` 窗口左侧面板显示的邮件或新闻账户，右侧面板会出现可点击的链接，允许你检查设置或创建新账户。

完成这些信息的输入后，你可以点击 `OK` 进入新闻阅读器窗口，如图 20.7 所示。你可以点击左侧面板中的新闻服务器名称，并在右侧选择 `Subscribe to Newsgroups`（订阅新闻组），以开始从你的新闻服务器下载新闻组列表。你随时可以通过点击该窗口中的 `Refresh`（刷新）按钮来更新新闻组列表。

![](img/446debe023486a07fde575245cf7a3ff_714_0.png)

**20.7** 从数千个新闻组列表中选择进行阅读。

## 与 TWIKI 协作

尽管 Usenet 是一个实用的交互协作工具，但在某些情况下，基于 Web 的工具更符合你的需求。`TWIKI` (`http://TWIKI.org`) 是一个基于 Web 的交互协作工具，也可以作为公告板、知识库、Bug 跟踪器和软件存档。

> **提示**
>
> 你可以查看公司首页上的 `TWIKI Success Stories`（成功案例）来获取探索 `TWIKI` 的动力。你也可以探索这个 Linux 相关的公共 `TWIKI` 站点：
>
> `http://TWIKI.org/cgi-bin/view/Wikilearn/WebIndex`

`Red Hat` 不提供 `TWIKI`，你必须在完成简单的注册后从 `TWIKI` 网站下载它。然后你会收到一封电子邮件指令，说明如何从该网站下载 `.zip` 文件。（使用 `unzip` 解压文件。）该程序根据 `GPL` 协议许可。

你可能想先阅读位于 `http://TWIKI.org/cgi-bin/view/TWIKI/TWikiDocumentation` 的安装说明。以下是关于在 `Red Hat Linux 8.0` 系统上顺利完成安装过程的简短建议（此列表假设你正以 `root` 用户执行安装）：

- 你需要创建目录 `/home/twiki`。

- 安装说明提到了文件 `/etc/httpd/httpd.conf`。对于 `Red Hat 8.0`，该文件位于 `/etc/httpd/httpd.conf`。你只需复制并粘贴下载说明提供的示例中所示的条目。

- `Red Hat 8.0` 的 `Perl` 路径为 `/usr/bin/perl`。

- `Red Hat 8.0` 以 `apache` 用户身份运行 `CGI` 脚本，而不是默认 `TWIKI` 安装中假设的 `root` 用户。你可以浏览到 `http://localhost/twiki/bin/testenv` 并阅读屏幕上显示的警告。这是一个运行在你的本地机器上的特殊脚本，帮助你诊断安装中的任何问题。这些信息应针对你的安装，任何警告都应附带关于如何解决问题的建议。

`TWIKI` 安装指南建议设置权限并更改所有权。对于 `Red Hat 8.0`，权限设置是正确的，但所有权错了。要更改所有权，请按照以下步骤操作（每一步完成后，都应重新加载 `http://localhost/twiki/bin/testenv` 页面以检查进度）：

1. `apache` 的所有权，但将 `/home/twiki/templates` 的所有权改 `root`：

```bash
chgrp -r apache /home/httpd
chgrp -r root /home/twiki/templates
```

2. 修改 `/home/httpd/twiki/lib/TWiki.cfg` 以反映你自己的域名，而不是 `http://your.domain.com`。

3. 将 `RCS` 仓库文件的所有权更改为用户 `apache`：

```bash
# cd /home/twiki/data
# perl -pi -e 's/:noby:apache/:*V'
```

完成安装后，你应该拥有一个“原始”的 `TWIKI` 安装，你可以在 `http://localhost/twiki/bin/view` 查看它。对于任何应用程序，你都需要进一步配置此文件以使其符合你的需求。`TWIKI` 文档解释了你可以使用的许多配置选项和过程。该文档包含在你刚刚完成的 `TWIKI` 安装中。

## 互联网中继聊天 (IRC)

正如 `RC 2812` 和 `RFC 2813` 所示，`IRC` 协议用于文本会议。像邮件和新闻一样，`IRC` 使用客户端/服务器模型。虽然个人很少建立 `IRC` 服务器，但这是可以。大多数人使用公共 `IRC` 服务器并通过 `IRC` 客户端访问它们。

`Red Hat` 提供了许多图形化 `IRC` 客户端，包括 `X-Chat`、`kirc`、`licq` 和 `Mozilla-chat`，但没有默认的聊天客户端。`Red Linux` 还为那些避开图形界面的用户提供了控制台客户端 `epic` 和 `1q`。如果你还没有喜欢的，应该尝试所有的客户端。

> **警告**
>
> 当你以 `root` 用户身份操作时，绝不要使用 `IRC` 客户端。由于潜在的安全问题，为 `IRC` 创建一个特殊用户更好。要这样使用 `X-Chat`，你只需打开一个终端窗口，使用 `su` 切换你的 `IRC` 客户端并启动 `xchat` 客户端。

`X-Chat` 是流行的 `IRC` 客户端，也是本章示例中使用的客户端。`X-Chat` 的 `HTML` 文档位于 `/usr/share/docs/xchat-1.8.10`。在开始之前阅读它们是一个好主意，因为它们包含了 `IRC` 的介绍和基础知识。要启动 `X-Chat` 客户端，可以在 `Extras` 菜单下的 `Internet` 菜单中选择 `IRC Client` 项，或者你可以从命令行启动它，如下：

```
$ xchat
```

`X-Chat` 允许你为自己分配最多三个昵称。你还可以指定你的姓名和用户名。由于许多人选择不在 `IRC` 聊天中使用真实姓名，你可以自由地在提供的任何空间中输入你想要的任何名称。你可以选择多个昵称；你可能在一个名称下被某个 `IRC` 频道封禁，然后你可以用另一个名称重新加入。

当你打开 `X-Chat` 主界面时，会出现 `IRC` 服务器列表，如图 20.8 所示。

当你双击选择一个服务器后，可以通过 `Window, List Window` 查看该服务器上的可用通道列表。`X-Chat` 通道列表出现。在该窗口中，你可以加入感兴趣主题的通道。要加入通道，只需双击即可。

# 682 第20章 新闻与其他协作通信

![](img/446debe023486a07fde575245cf7a3ff_717_0.png)

**图 20.8** 主 `X-Chat` 界面显示了可用的公共服务器列表，从中从中选择。

> 提示
>
> 不要对 `IRC` 公共服务器上大量的俚语和语言主题感到惊讶。欲欲关于 `IRC` 咒骂主题的幽默视角，请访问 `http://www.org/fun_docs/nocuss.html`。该网站还提供了维护 `IRC` 礼仪的技巧，如果你不想成为那些脏话的攻击对象，这至关重要！以下是一些最重要的 `IRC` 规则：
>
> * 不要使用彩色文本、全大写文本、闪烁文本或蜂铃（通过向终端发送“G”引起的“哔哔”声）。
>
> * 尊重他人。
>
> * 忽略行为不当的人。

选择频道后，你就可以加入对话，对话将以屏幕文本的形式出现。随着新消息的出现，消息会在屏幕上滚动。

**你自己的 IRC 服务器**

尽管 `Red Hat` 不提供 `IRC` 服务器，你也可以建立自己的 `IRC` 服务器。对于不熟悉 `Linux` 或 `IRC` 的人来说，设置服务器并不是一项任务。

一个流行的服务器是 `IRCd`，你可以从 `ftp://ftp.ircdhelp.org/pub/ircd/` 获取。在下载 `IRCd` 之前，你应该查看 `README` 文件以确定你需要哪些文件，相关信息请见 `http://www.irchelp.org/irchelp/ircd/`

# 在 Red Hat Linux 中通过 KIT 和 GAIM 使用 IM

`IM`（即时消息）也由美国在线（`AOL`）推广，以便 `AOL` 用户可以直接聊天，而不是在聊天室中发言。只要 `IM` 客户端正在运行，它们就会提醒你任何收到的消息。它们还会向服务器宣布你处于活跃状态并监听消息，这样你的朋友就能知道你有空与他们聊天。

如果需要，可以使用 `IM` 代替 `IRC` 进行办公室内协作。`Red Hat` 提供了两个 `IM` 客户端 `KIT` 和 `GAIM` 供你使用。要使用它们，你需要与一组活跃的 `IM` 用户（“好友”）保持通信。

`GAIM` 是 `Red Hat 8.0` 的默认 `IM` 客户端。它是一个 `GNOME`（基于 `GTK`）的 `IM` 客户端，支持广泛的协议。`GAIM` 是一个功能丰富的消息客户端，并支持通过插件来扩展应用程序的功能。

> 注意
