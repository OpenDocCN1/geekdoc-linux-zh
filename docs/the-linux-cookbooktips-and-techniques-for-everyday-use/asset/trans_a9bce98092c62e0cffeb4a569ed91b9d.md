

remote system.

公用系统在 FTP 主机上设置 `/pub` 目录是标准做法，该目录包含所有供公众使用的文件和资源。

- 要切换到远程系统的 `/pub` 目录并查看其中的文件，请输入：

```
ftp62; cd /pub RET
250 Directory changed to /pub.
ftp62; ls RET
ftp62; ls
200 PORT command successful.
150 Opening ASCII connection for file (918 bytes)
total 30258
-rw-rw-r-- 1 ftpadmin ftpadmin 10942767 Sep 28 06:18 INDEX.gz
drwxr-xr-x 5 ftpadmin ftpadmin 512 Sep 17 18:22 comp
-rw-rw-r-- 1 ftpadmin ftpadmin 9512498 Sep 28 06:40 ls-lR.gz
drwxr-xr-x 2 ftpadmin ftpadmin 512 Sep 17 18:22 rec
drwxr-xr-x 3 ftpadmin ftpadmin 512 Sep 17 18:22 science
226 Transfer completed with 918 Bytes/s.
ftp62;
```

在此示例中，`/pub` 目录包含三个子目录（`comp`、`rec` 和 `science`）和两个文件 `INDEX.gz` 和 `ls-lR.gz`；许多公用系统在其 `/pub` 目录中都有类似的文件——`INDEX.gz` 是其 ftp 站点上所有文件的列表，并附有说明，而 `ls-lR.gz` 是在其 ftp 服务器目录树上运行 `ls -lR` 命令的输出。

以下小节描述如何上传和下载文件。使用 quit 命令退出 ftp 并结束与远程系统的连接。

33.2.1 Uploading a File    上传文件。
33.2.2 Downloading a File    下载文件。

### 33.2.1 Uploading a File

使用 put 命令上传文件；将文件名作为参数给出。put 会在本地系统的当前目录中获取该文件，并将其副本放到远程系统的当前目录中。

- 要将本地系统当前目录中的文件 `thyme.rcp` 的副本放到远程系统的当前目录中，请输入：

```
ftp62; put thyme.rcp RET
```

本地系统的当前目录默认为你运行 ftp 命令的目录。要更改本地系统的目录，请使用 lcd；它与 cd 命令类似，但更改的是本地目录。

- 要切换到本地系统当前目录的父目录，请输入：

```
ftp62; lcd .. RET
Local directory now /home/james/demos
ftp62;
```

在此示例中，本地当前目录现在是 `/home/james/demos`。

还有其他用于下载文件的重要命令——使用 `i` 指定文件以二进制方式传输；通常，传输设置为文本文件。当你想要传输程序、归档文件、压缩文件或任何其他非文本文件时，先将传输类型设置为 `i`。

近年来，大多数公用系统都增加了一项安全措施，禁止匿名用户上传到 `/incoming` 或 `/pub/incoming` 目录之外的任何位置。

mput 命令的工作方式与 put 类似，但允许你指定通配符。默认情况下，mput 会询问你是否上传每个文件；要关闭此文件提示，请在给出 mput 命令前输入 prompt。此命令是切换——再次输入 prompt 可在会话中重新打开文件提示。

### 33.2.2 Downloading a File

get 命令的工作方式与 put 类似，但方向相反——指定远程系统上的文件，get 会将其副本保存到本地系统的当前目录中。同样，在下载非文本文件时先使用 i。 （你也可以使用 i 下载文本文件，因此在传输文件前始终设置它是一个好习惯；大多数 Linux 系统在连接后立即将类型设置为 `i`）。

- 要下载远程系统当前目录中的文件 `INDEX.gz` 并将其保存到你的 `~/tmp` 目录，请输入：

```
ftp62; lcd ~/tmp RET
Local directory now /home/james/tmp
ftp get INDEX.gz RET
local: INDEX.gz remote: INDEX.gz
Transferred 10942767 bytes
ftp62;
```

> NOTE: mget 命令的工作方式与 get 类似，但允许使用通配符；与 mput 一样，除非你先使用 prompt 命令关闭它，否则每次都会提示你确认每个文件。

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

