
在此示例中，本地当前目录现在是 `/home/james/demos`。

还有其他用于下载文件的重要命令——使用 `i` 指定文件以二进制方式传输；通常，传输设置为文本文件。当你想要传输程序、归档文件、压缩文件或任何其他非文本文件时，先将传输类型设置为 `i`。

近年来，大多数公用系统都增加了一项安全措施，禁止匿名用户上传到 `/incoming` 或 `/pub/incoming` 目录之外的任何位置。

`mput` 命令的工作方式与 `put` 类似，但允许你指定通配符。默认情况下，`mput` 会询问你是否上传每个文件；要关闭此文件提示，请在给出 `mput` 命令前输入 `prompt`。此命令是切换——再次输入 `prompt` 可在会话中重新打开文件提示。

### 33.2.2 Downloading a File

`get` 命令的工作方式与 `put` 类似，但方向相反——指定远程系统上的文件，`get` 会将其副本保存到本地系统的当前目录中。同样，在下载非文本文件时先使用 `i`。 （你也可以使用 `i` 下载文本文件，因此在传输文件前始终设置它是一个好习惯；大多数 Linux 系统在连接后立即将类型设置为 `i`）。

- 要下载远程系统当前目录中的文件 `INDEX.gz` 并将其保存到你的 `~/tmp` 目录，请输入：

```
ftp62; lcd ~/tmp RET
Local directory now /home/james/tmp
ftp get INDEX.gz RET
local: INDEX.gz remote: INDEX.gz
Transferred 10942767 bytes
ftp62;
```

> NOTE: `mget` 命令的工作方式与 `get` 类似，但允许使用通配符；与 `mput` 一样，除非你先使用 `prompt` 命令关闭它，否则每次都会提示你确认每个文件。

### 33.3 Reading Usenet

@sf(WWW): http://www.faqs.org/usenet/index.html

@sf(WWW): http://www.geocities.com/ResearchTriangle/tab/6892/

Usenet 是一个著名的、庞大的全球讨论版集合，称为新闻组，用户可以在其中阅读消息（称为文章）并公开回复。新闻组按层级命名和组织，每个分支由句点（'.'）分隔；例如，`comp.os.linux` 新闻组是 `comp.os` 分支的 `comp` 层级的一部分。

下表列出了 Usenet 的“八大”层级，并给出了每个层级中的一些新闻组示例。

| USENET HIERARCHY | DESCRIPTION |
|---|---|
| comp | 计算。 news:comp.os.linux.advocacy, news:comp.text.tex |
| humanities | 人文学科。 news:humanities.music.composers.wagner |
| misc | 杂项。 news:misc.consumers.frugal-living |
| news | 与 Usenet 本身相关的新闻组。 news:newusers.questions |
| rec | 娱乐。 news:rec.music.marketplace.vinyl, news:rec.food.cooking |
| sci | 科学。 news:sci.math, news:sci.cognitive |
| soc | 社会群体和文化。 news:soc.culture.usa, news:soc.college |
| talk | 谈天说地。 news:talk.environment, news:talk.politics.guns |

虽然还有许多其他层级，但这八个在技术上是被认为属于 Usenet 本身的唯一新闻组。虽然 netnews 是指包括 Usenet 在内的所有新闻组的集合这一术语，但这两个术语经常被互换使用。

“替代”层级 `alt.` 可能是最受欢迎的层级之一——几乎任何你想讨论的主题在这里都有合适的新闻组，包括不相干的内容。还有针对特定地理区域主题的层级；例如，`cols.` 层级用于哥伦布、俄亥俄州的主题，而 `seattle` 用于华盛顿州西雅图。因此，`cols.forsale` 涉及大哥伦布地区出售的物品，而 `seattle.forsale` 则是西雅图及其周边地区出售的物品。层级也可以存在于某些组织；例如，`gnu` 层级用于关于 GNU 项目的新闻组，而 `bit` 用于流行的 Bitnet LISTSERV 邮件列表的新闻组再分发。

# 《Linux 实用手册：日常使用的技巧与方法》：

以下食谱描述了用于阅读和发布新闻组文章的工具。

## 33.3.1 选择新闻阅读器

选择新闻阅读器。

## 33.3.2 为主题查找新闻组

为主题查找新闻组。

### 33.3.1 选择新闻阅读器

一种让你阅读和发布新闻组文章的应用程序称为新闻阅读器。以下是 Linux 系统可用的最佳新闻阅读器。

| NEWSREADER | DESCRIPTION |
|---|---|
| gnus | Gnus 是一个功能非常强大且功能齐全的用于 Emacs 的新闻阅读器。你也可以用它来阅读邮件。 Debian: `gnus` WWW: http://www.gnus.org/ |
| knews | 一个用于 X 的图形化新闻阅读器。其功能包括以图形树形式显示文章线程，以及为通过慢速连接阅读新闻的人提供的选项。 Debian: `knews` WWW: http://www.matematik.su.se/~kij/ |
| mozilla | 历史上，商业 Web 浏览器也内置了邮件和新闻阅读器，并且该功能保留在 Mozilla 浏览器中。 Debian: `mozilla` WWW: http://www.mozilla.org/ |
| nn | nn 的座右铭是“无新闻是好事，但 nn 更好”；它是一款较老且非常流行的新闻阅读器，旨在以最少的时间阅读最多的新闻。 Debian: `nn` WWW: http://www.math.fu-berlin.de/~guckes/nn/ |
| pan | “Pimp A** Newsreader”是一款新一代图形化新闻阅读器，旨在追求速度。它旨在让初学者易于使用，并且在安装了 GNOME 的 X 中运行。 Debian: `pan` WWW: http://www.superpimp.org/ |
| peruser | News Peruser 是一套用于 X 的小型工具套件，便于在离线时阅读和撰写新闻文章——在系统在线时下载新闻批次。 Debian: `peruser` WWW: http://www.ibiblio.org/pub/Linux/system/news/readers/ |
| slrn | 基于 rn——其中一个最古老的新闻阅读器——slrn 针对通过家用调制解调器拨号等慢速连接的使用进行了优化。 Debian: `slrn` WWW: http://www.slrn.org/ |

### 33.3.2 为主题查找新闻组

Debian: `nn`

WWW: ftp://ftp.uwa.edu.au/pub/nn/beta/

使用 `nngrep` 查找与模式匹配的新闻组名称。这对于查找特定主题的组很有用。

- 要输出与模式 `society` 匹配的所有新闻组的列表，请输入：

```
$ nngrep society RET
```

使用 `-u` 选项仅搜索未订阅的组。如果您已订阅了多个组，并且只想查找尚未订阅的组，这很有用。

- 要输出与模式 `society` 匹配的所有未订阅新闻组的列表，请输入：

```
$ nngrep -u society RET
```

在前一个示例中，如果您已经订阅了组 `alt.society.neutopia`，则该组将不会显示；但您未订阅的其他与模式 `society` 匹配的组将被列出。

## 33.4 列出在线系统和用户活动

以下工具用于列出互联网上其他用户和系统的活动——显示他们是否当前在线，并可能显示更多关于他们的信息。

- 33.4.1 检查系统是否在线
- 该系统在线吗？
- 33.4.2 检查用户是否在线
- 该用户在线吗？
- 33.4.3 列出登录到系统的用户
- 谁在该系统上？
- 33.4.4 查找主机名的 IP 地址
- 该系统的 IP 地址是什么？
- 33.4.5 查找 IP 地址的主机名
- 该 IP 地址的名称是什么？
- 33.4.6 列出域名所有者
- 谁在该域名背后？

如果他们使用的系统启用了 `finger` 大多数基于 Unix 的系统都应启用，命令将告诉你以下信息：他们上次登录的日期和时间；他们是否当前已登录；他们的全名；他们的办公室房间和电话号码；他们的主目录；他们使用的 shell；他们是否有待处理的邮件；他们上次阅读邮件的时间；最后是他们的“计划”，如下所述。

- 要 `finger` 用户 `bradley@ap.spl.org`，请输入：
