
# tin

`tin` 是一个实用的程序，初看可能会给你留下并不不错的印象，但实际上它的处理效率比某些其他程序（如 `Netscape`）高得多。当你想要使用该程序读取本地新闻文章时，只需启动 `tin` 即可。

如果文章仅在远程服务器上（在线操作），你必须在 `/etc/nntpserver` 文件或环境变量 `NNTPSERVER` 中指定其地址。在本章的提供商示例中，地址为 `news.provider`——见第 427 页。此外，在阅读之前，必须与提供商建立 `PPP/SL` 连接。随后，使用 `tin -r` 启动新闻程序。如果你已经有一个 `.newrc` 文件，可以节省时间并执行 `-r -n`。现在，只考虑已订阅的新闻组。第一次启动 `tin` 时这显然是不可能的。

当你使用它时，`tin` 会显示所有已知新闻组的列表（无论是否存在）。如果使用本地新闻服务器，该列表源自 `/var/lib/news/active`——见第 488 页。

默认情况下，`tin` 会订阅所有新闻组。因此，第一步是取消所有订阅：首先，按 `Y [Shift-U], [x]`，然后按 `[x]`。取消订阅需要一些时间。随后，你可以使用 `Y` 来检查操作是否正确。`Y` 可在所有新闻组视图和已订阅组之间切换。

按 `Y` 切换到显示所有新闻组的模式。现在，你可以使用光标移动到所需的新闻组并使用 `$` 订阅单个组，或者使用 `[Shift-$]` 订阅所有符合给定的组。例如，你可以输入 `comp.linux.*` 来选择所有 `LINUX` 组。再次按一次 `Y`——屏幕应该看起来如下所示：

# 组选择 (4)

| 计数 | 组 |
| :--- | :--- |
| 32 | `comp.linux.hardware` |
| 92 | `comp.linux.misc` |
| 3 | `comp.linux.networking` |
| 2 | `comp.linux.x` |

```
<set current to n, TAB=next unread /=search pattern, c=catch,
goto, j=line down, k=line up, h=help, m=ove, q=quit, r=toggle all/unread,
subscribe, $subscribe pattern, uUnsub pattern, y yank in/out
```

# USENET 新闻 479

第二列中的数字表示你有多少篇文章未阅读。若要阅读 `de.comp.os.linux.misc` 中的文章，只需将光标移动到该行并按 `[/ 或 -]`。现在，屏幕结构将看起来像这样：

- `1 e2fsck 信号错误。磁盘损坏？Joerg Mertin`

- `2 +2 MC 颜色？Kai Straube`

- `3 +2 * Linux 2.0 到了！Dirk Bernhardt`

- `4 +3 lpd - 无守护进程Joachim Zobel`

- `5 + tin = sloowoo :) Urs=?8859-185?`

- `6 +2 内核编译问题Stefan Jane`

第二列需要解释。如果它包含数字，说明我们有一个包含 `n` 个未读文章的线程。通过按键选择文章或线程。进入文章。`[-]` 返回列表。

# 482 使用 LINUX 访问互联网

在作者许可（非常感谢！）的基础上经过了细微改动。更新和修订可以在互联网上找到：

```
http://www.uni-koeln.de/~acp66/linux
Markus Dickebehm <d.dickebehm@uni-koeln.de>
```

# 引言

决定在线时间长短的关键因素是阅读新闻，而时间因素由电脑前的人决定。数据量通常相对较小；阅读和挑选文章占据了时间。当新闻组中的所有新文章通过调制解调器请求获取并“离线”时，这种时间可以显著减少。离线阅读新闻的前提条件：

- 良好的网络连接（本说明假设使用 `PPP` 连接，参见第 426 页）。
- 安装和配置本地新闻服务器（第 482 页）。
- 安装和配置阅读和发布新闻文章的程序（第 491 页和 494 页）。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_507_0.png)

# 新闻服务器配置 (INN)

`Linux` 有两个竞争的新闻服务器：`cNews` 和 `INN` 包。`INN` 包的规模稍大，主要用于较大的新闻服务器。`cnews` 包是早期为带有 `UUcp` 的较小机器开发的。与其他软件包不同，这两个同时安装这两个包是不可能的（而且这样做也没有意义）。

`INN` 凭借其更加灵活、速度更快的新闻系统，已在很大程度上确立了自身的地位。关于 `INN` 不太适合内存有限的机器（因为服务器始终保留在内存中）的说法在 `Linux` 上是不成立的，因为服务器及其配置文件在不需要时会被交换到硬盘磁盘上，从而不会进一步影响计算机的性能。

本说明集描述了 `INN` `1.4` 新闻服务器的配置。起点是一个二进制发行版，类似于在所有主流发行版（`RedHat`, `Debian`, `Slack`）中包含的那些。安装后，系统将包含两个新目录 `/usr/lib/news` 和 `/etc/news`，它们之后会被修改（较旧的发行版中，`/etc/news` 目录尚不存在，相应的文件位于 `/usr/lib/news`）。

# USENET 新 483

在安装 `INN` 之前，你应该意识到以下一点：你需要一些磁盘空间。取决于新闻文章在系统中留存多长时间，达到几 `Mbytes` 的大小并没有问题。在一个包含 28 个新闻组的示例配置中，平均文章数量和所谓的五天“过期”时间（进入进入的文章后被删除的时间），你必须预留 5–10 `Mbytes` 的空间。

在较小的分区中，问题不仅在于可用空间，还在可用的 `I-nodes` 数量：新闻文章很短，但每几篇——无论形式如何——都会占用一个 `I-node`。然而，`I-nodes` 的数量是有限的，可用空间也是如此。如果你为 `/var/spool/news` 创建了独立分区，请记住指定较高的 `I` 密度（参见第 106 页）。

当我们本文中谈到 `INN` 时，我们实际上是指带有所有配置文件的 `innd` 守护进程。在完成本节讨论的准备工作后，就可以首次启动 `innd` 了。随后，该守护进程将在每次系统设置时自动启动。

# 注册用户新闻

为了让 `INN` 无故障运行，必须满足某些前提条件：系统中必须存在用户 `news` 和组 `news`。在许多发行版中，情况已经如此；然而，必须在 `/etc/passwd` 和 `/etc/groups` 中进行检查以万万无一。

这里描述的所有后续命令和修改都应以用户 `news` 身份执行（`su news`）。如果需要由 `root` 执行单个命令，将会有明确说明。

此外，`INN` 会定期（每天一次）向 `/etc/aliases` 文件中建立的所谓“别名”（`alias`）发送邮件。为了使此条目生效，`root`（或新闻管理员）必须执行 `newnewaliases` 命令（前提是使用 `sendmail` 作为邮件传输代理）。

```
# 向 /etc/aliases 添加内容
bin: root
news: root
usenet: root
newsmaster: root
```

`INN` 使用 `/bin/mail` 程序发送其电子邮件。如果你正在使用 `RedHat`，请确保该程序已安装。（它包含在 `mailx` 软件包中。）

为了避免以后出现复杂情况，此时你应该检查 `/etc/inetd.conf` 中是否存在 `news` 条目：如果是的话（取决于发行版），必须用 `#` 注释掉该条目。

```
# /etc/inetd.conf
# 注释掉新闻条目
nntp stream tcp nowait root /usr/sbin/tcp /usr/sbin/in.nntpd
```

# INN 配置文件

### inn.conf

`INN` 的主配置位于 `/etc/news/inn.conf` 文件中（或 `/usr/lib/news/inn.conf`，取决于发行版）。其中，定义了计算机在 `Usenet` 上登录的主机名。这通常是任何情况下 `LINUX` 计算机使用的名称，但指定 `localhost` 也不会产生问题。

根据配置/发行版，除了条目 `127.0.1` 外，可以在 `/etc/hosts` 文件中指定另一个主机名。

```
# /etc/hosts
127.0.0.1 localhost
```

此外，你可以在文件中指定一个指定域的行。`organization` 属性指定了头文件中出现的行。

```
## /etc/news/inn.conf -- inn 配置
## $Revision: 1.5 $
## 格式:
##   <parameter>:<value>
server: localhost
organization: University of Cologne
```

### hosts.nntp

该文件的配置非常简单。

```
## /etc/news/hosts.nntp - 我们的信息的名称和地址
## $Revision: 1.4 $
## 格式
##   <host>:
##   <host>:<password>
localhost:
```
