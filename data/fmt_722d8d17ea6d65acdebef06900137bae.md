
每个条目有四个由冒号（`:`）分隔的字段。通常，条目跨越多行，并且行尾的反斜杠（`\`）用于将行继续到下一行。以下是四个字段的含义：

- 第一个字段 `site` 是馈送的名称。每个名称必须唯一，对于发送到其他新闻服务器的馈送，名称设置为远程服务器的主机名。名称后面是一个可选的斜杠和一个排除列表（`/exclude,exclude...`），由一系列名称组成。如果文章的 `Path` 行中出现此列表中的任何名称，则该文章不会被转发到该馈送。如果您不希望接收来自特定来源的文章，可以使用排除列表。
- 第二个字段由一组以逗号分隔的新闻组模式组成，例如 `*@alt.binaries.warez.*,!control*,!local*`，后面跟一个可选的分发列表。分发列表是一组以逗号分隔的关键字，每个关键字指定文章将被分发的特定站点集。新闻组模式本质上定义了接收此新闻馈送的站点的订阅列表。星号匹配所有新闻组。以 `@` 开头的模式会导致匹配该模式的新闻组被丢弃。以感叹号（`!`）开头的模式表示匹配的新闻组不发送。顺便说一下，INN 配置文件中使用的一种简单的模式匹配语法称为 `wildmat` 模式。
- 第三个字段是以逗号分隔的标志列表 — 这些字段确定馈送条目类型并为条目设置某些参数。有许多标志；输入 `man newsfeeds` 并阅读手册页以了解有关标志的更多信息。
- 第四个字段用于参数，其值取决于第三个字段中的设置。通常，此字段包含 INN 服务器使用的文件名或外部程序的名称。您可以在 `newsfeeds` 手册页中了解有关此字段的更多信息。

现在您知道了 `/etc/news/newsfeeds` 文件的布局，您可以将其作为示例进行研究。默认文件包含许多示例馈送条目，但只有两个被注释掉了：

- `ME` 是一个始终必需的特殊馈送条目。它有两个用途。首先，此条目中列出的新闻组模式会被添加到所有其他条目中的新闻组模式。第二，`ME` 条目的分发列表决定了你的服务器从远程站点接受的分发内容。
- `controlchan` feed 条目用于设置 INN，使其使用外部程序来处理控制消息（这些消息用于创建新的新闻组和删除组）。例如，以下 `controlchan` 条目指定外部程序 `/usr/lib/news/bin/controlchan` 来处理所有控制消息，除了取消消息（用于取消文章）：

```
controlchan!

:!*!,control.control.*,!control.cancel\
:Tc,WnSm:/usr/lib/news/bin/controlchan
```

除这些 feed 条目外，你还要为新闻服务器提供新闻馈送的任何实际站点添加条目。此类条目的格式为

```
feedme.domain.com
:ljunk,!control/!foo\
:Tm:innfeed!
```

其中 `feedme.domain.com` 是你的系统向其发送新闻文章的站点的完全限定域名。

## The incoming.conf file

`incoming.conf` 文件描述哪些主机被允许连接到你的主机以馈送文章。对于单个馈送，你可以添加如下条目

```
peer mybuddy {
  hostname: a-feed-site.domain.com
}
```

其中 `mybuddy` 是对等体的标签，`a-feed-site.domain.com` 标识馈送你的站点的站点。

请记住，仅仅在 `incoming.conf` 文件中添加站点的名称并不会导致该远程站点开始向你的站点馈送新闻——它只是使你的服务器能够从远程站点接受新闻文章。在远程站点，你的朋友必须配置他的或她的服务器以向你的站点发送文章。

## The readers.conf file

此文件指定新闻阅读器客户端（如 Mozilla）可以从中检索新闻组的的主机名或 IP 地址。例如，以下 `readers.conf` 文件允许从 `localhost` 以及网络 `192.168.0.0` 中的任何主机进行读取访问和发布访问（意味着你可以提交文章）：

```
auth "localhost" {
  hosts: "localhost, 127.0.0.1, stdin"
  default: "<localhost>"
}

access "localhost" {
  users: "<localhost>"
  newsgroups: "**"
  access: RPA
}

auth "localnet" {
  hosts: 192.168.0.0/24
  default: "<localnet>"
}

access "localnet" {
  users: "<localnet>"
  newsgroups: "**"
  access: RPA
}
```

## InterNetNews startup

除了配置文件之外，你还必须启动执行新闻服务器定期维护的 cron 作业。在 Red Hat Linux 中，这些 cron 作业已经设置好。因此，你现在可以启动 INN 服务器——`innd`。

在启动 `innd` 之前，你必须运行 `makehistory` 和 `makedbz` 以初始化并重建 INN 历史数据库。输入 `man makehistory` 和 `man makedbz` 以了解有关这些命令的更多信息。输入以下命令以创建初始历史数据库、相关索引，并设置某些文件的属主和权限：

```
/usr/lib/news/bin/makehistory -b -f history -0 -l 30000 -I
cd /var/lib/news
/usr/lib/news/bin/makedbz -s 'wc -l < history' -f history
chown news.news *
chown news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index
```

与 Red Hat Linux 中的其他服务器一样，要启动 `innd`，请以 root 身份登录并输入以下命令：

```
service innd start
```

要确保 inn 在启动时启动，输入以下命令：

```
chkconfig --level 35 inn on
```

如果更改任何配置文件（如 `inn.conf` 或 `newsfeeds`），请使用以下命令重新启动 inn 服务器：

```
service inn restart
```

输入 `ps ax` 以查看 inn 进程是否正在运行。如果一切顺利，你应该在 `ps ax` 命令的输出中看到两个类似以下的过程：

```
23789 ? S 0:00 /usr/lib/news/bin/inn -p4
23794 ? S 0:00 /usr/bin/perl /usr/lib/news/bin/controlchan
```

`/var/log/spooler` 文件包含来自 inn 的所有状态和错误消息。输入以下命令以查看该文件中的最后几条消息：

```
tail /var/log/spooler
```

## Setting Up Local Newsgroups

如果你想使用新闻组作为在公司内部共享信息的一种方式，可以设置本地新闻组层次结构。然后你可以使用这些新闻组在公司内部创建虚拟社区，让有共同兴趣的人可以非正式地讨论问题并交流知识。

### Defining a newsgroup hierarchy

第一步是定义新闻组层次结构并决定每个新闻组将讨论什么内容。例如，如果你的公司名称是 XYZ Corporation，以下是你可以定义的新闻组层次结构的局部内容：

- `xyz.general` — 关于 XYZ Corporation 的一般事项
- `xyz.weekly.news` — 每周新闻
- `xyz.weekly.menu` — 每周食堂菜单及相关讨论
- `xyz.forsale` — 员工出售物品的清单
- `xyz.jobs` — XYZ Corporation 的职位空缺
- `xyz.wanted` — 员工发布的求助、求购等信息
- `xyz.technical.hardware` — 关于硬件的技术讨论
- `xyz.technical.software` — 关于软件的技术讨论

### Updating configuration files

以下是更新本地新闻组的配置文件然后重新启动新闻服务器的步骤：

1. 向 `/var/lib/news/newsgroups` 文件中为每个新闻组添加描述性条目。

以下是默认 `/var/lib/news/newsgroups` 文件中的条目：

```
control          Various control messages (no posting).
```
