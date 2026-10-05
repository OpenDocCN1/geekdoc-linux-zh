

# 新闻客户端 373

仅在第一次运行时发生。Netscape 将列表存储在 `.netscape/xover-cache/server/hostinfo.dat`。

随后，将在对话框中显示所有可用新闻组的层级列表。此列表通常非常大（20,000 个新闻组或更多）。可以通过 SEARCH（搜索）对话表页来帮助查找所需的新闻组，例如你可以过滤出所有名称中包含“linux”的新闻组。（但是，不允许使用包含 * 的搜索模式）。当你找到所需的群组后，只需点击 SUBSCRIBE（订阅）按钮或激活勾选标记即可。

![](![](img/b30873dd3d753687a59253fb9ad26a0b_400_0.png)

图 11.1 使用 Netscape 订阅新闻组。

![](img/b30873dd3d753687a59253fb9ad26a0b_400_1.png)

图 11.2 使用 Netscape 阅读新闻。

为了能够使用 FILE/GET NEW MESSAGES（文件/获取新消息）命令更新新闻文章列表，你需要将 Netscape 配置为邮件客户端。这相当烦人，因为这使得无法在不将其作为电子邮件客户端的情况下仅将其作为新闻客户端使用。

# slrn

根据 RedHat 软件包描述，slrn 是地球上最好的新闻阅读器！在你分享这一观点之前，你必须花一点时间来习惯它。强大的功能被隐藏在顽固的界面之后，即使在 KDE Gnome 失去了图标的时代也是如此。这对于初学者来说足够了。

关于 slrn 的最新信息，包括一个非常有用的 FAQ 集合，可以在互联网上找到：
http://space.mit.edu/~davis/slrn

# 

无论该程序是用于访问本地服务器还是通过互联网访问远程服务器，都必须在环境变量 `NNTPSERVER` 中设置服务器名称。或者，也可以通过 `-h` 指定名称。（第 305 页示例用户的服务器名称为 news.provider.de。如果你使用 leafnode（见第 380 页）作为你的本地新闻服务器，则服务器框简单为 local.）

为了启动 slrn，主目录下必须位于 `.newsrc` 或 `.newsrc`。如果两者都没有（因为到为止没有其他新闻客户端使用过），slrn 会发出错误信息。

```
hofer slrn
rn 0.9.5.2 (Dec 11 1998 21:07:03)
Reading startup file /var/lib/slrn/slrn.rc.
Unable to open /home/hofer/.jnewsrc. I will try .newsrc.
slrn fatal error: Unable to open /home/hofer/.jnewsrc.
```

这个问题很容易解决。重试，这次你使用以下选项：

```
hofer slrn -f ~/.newsrc-create
srn 0.9.5.2 (Dec 11 1998 21:07:03)
Reading startup file /var/lib/slrn/slrn.rc.
Connecting to host localhost...
Connected to host. Posting Ok.
--如果 NNTP 连接较慢，下一步可能需要一段时间时间---
Creating /home/hofer/.newsrc........
```

读取所有存储的新闻组列表可能需要一些时间——但这只在第一次启动时需要。

slrn 现在显示了（仍然为空）的所有已订阅新闻组列表。要显示群组——包括你尚未订阅的群组——输入 Shift+*。除了 * 之外，你可以输入任何模式，例如 `*.os.` 以显示所有涉及操作系统的新闻组。

取决于你使用哪个服务器或互联网提供商，Shift+L 可能不起作用：未显示任何群组。如果你使用 leafnode 作为新闻服务器，这种情况很容易发生。用 Q 退出 strn，并使用编辑器将以下行插入配置文件 `.strnrc`：

```
set read.active 1
```

当你看到群组列表时，可以使用 S 订阅所需的组，使用 U 取消订阅。如果现在执行 Shift+L，将显示已订阅的组。

# 使用

要阅读群组的新闻，你用光标选择群组并按 `->`。现在 strn 显示所有文章列表，你可以再次使用光标和 `<-` 选择文章。在屏幕上出现的文本窗口中，可以使用空格键滚动，并使用 H 和 Z 显示/隐藏文本或新闻列表。

# strn 快捷键

- Q 退出当前视图
- ? 帮助
- C 将所有文章标记为“已读”
- Esc, U 将所有文章标记为“未读”
- 空格键向前滚动新闻
- H 显示/隐藏文本
- Z 显示/隐藏新闻列表
- F 将文章作为文本回复到新闻组
- R 将文章作为邮件直接回复给作者
- Shift+P 编写新文章

# 群组列表

- S 订阅群组
- U 取消对群组的订阅
- Shift+L 显示所有群组或仅显示已订阅的群组

# 376 NEWS

```
Wait Catch Nextart Post Reply Help
      D 41:[H:]...
      51: [H:]...
      20: News Group:de.comp.os,linux,hardware 2/24 (Top)
      disk 8, 3 Jun
```

```
`&` 是主数字，3,4,5 是次数字。
或者查看你是否在 /dev 下有 MRADEV。这应该会显示。

> 如果我换成你的位置，我不会放弃的，我会尝试保存，如果有数据的话，也可以

```
SPT: Re: 
```

图 11.3 使用 strn 阅读新闻。

# 配置

strn 的外观、操作和功能范围可以通过配置文件 `.strnrc` 进行大量修改。设置选项和语法在附带的示例文件 strnrc（通常位于 var/lib/strrn）中记录。

发送者地址

strn 通常使用用户名、主机名和域名来构建发送者地址。在离线配置中，这很少是一个良好的解决方案：相反，应该使用互联网账户的电子邮件地址`.strnrc` 中的以下行设置发送者地址：hofer@provider.de（对于示例用户 Hofer）。

```
username "hofer"
hostname "provider.de"
realname "sample user Hofer"
```

发送者地址将正确输入所有新闻文章中，但对于向新闻文章作者发送邮件的 REPLY 命令无效。在 strn 的当前版本中，似乎无法影响发送者地址。按照 Unix 的习惯，电子邮件地址由登录名、主机名和域名组成。只有 sendmail 配置可能解决此问题。

# 注意

# 编辑器

strn 没有自己的编辑器，并将 vi 作为默认编辑器。你可以通过适当设置 `EDITOR` 或 `VISUAL` 环境变量来防止此。

# 颜色

strn 的预设颜色有时无法阅读文本。轻微的修改效果极佳：将以下标题（包括帮助文本中的）在白色背景上显示为蓝色。

color blue

# 鼠标控制

通过以下行，可以使用鼠标控制 strn 的许多功能：

```
set mouse 1
```

除了菜单控制和群组或单个新闻文章的选择，还有许多不明显的鼠标快捷键。

# strn 鼠标快捷键

在“新闻组”状态行中：

- 左键向前滚动列表
- 右键向后滚动列表
- 中键关闭列表视图

在文章状态行中：

- 左键跳转到下一个未读新闻文章
- 右键跳转到上一个未读新闻文章
- 中键显示/隐藏引用文本 (> text)

在文章文中：

- 左键向前滚动文本
- 右键向后滚动文本
- 中键关闭文本视图

# tin

tin 是一个方便的程序，可能会给你留下相当浅薄的第一印象，但在处理上比某些其他程序（如 Netscape）要高效得多。对于 strn：不要被非常简单的界面所震慑！

# 启动

和 strn一样，tin 也会评估环境变量 `NNTPSERVER` 的内容或 `/etc/ntpserver` 文件，其中必须指定新闻服务器的名称（例如 localhost 或 news.provider.de）。

