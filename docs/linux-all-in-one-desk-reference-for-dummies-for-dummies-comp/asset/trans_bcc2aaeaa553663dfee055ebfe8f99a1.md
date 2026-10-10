

## 配置并启动 INN 服务器

每个条目由冒号 (:) 分隔的四个字段组成。通常，条目跨越多行，并在行末使用反斜杠 (\) 将行延续到下一行。这四个字段的含义如下：

- ◆ 第一个字段，site，是源（feed）的名称。每个名称必须是唯一的，对于指向其他新闻服务器的源，该名称设置为远程服务器的主机名。名称后面跟随一个可选的斜杠 (/) 和一个排除列表（*exclude_*、*exclude_*…）的名称。如果该列表中的任何名称出现在文章的路径行中，则该文章不会被转发到该源。如果您不想从特定来源接收文章，可以使用排除列表。

- ◆ 第二个字段是用逗号分隔的新闻组模式列表，例如 `*@alt.barnries.warez.*,!control*,!local*`，后面跟随一个可选的发行列表（distribution list）。发行列表是一个由逗号分隔的关键字列表，每个关键字指定文章分发到的特定站点集合。新闻组模式实际上定义了接收此新闻源的站点订阅列表。星号 (*) 匹配所有新闻组。以 ! 开头的模式会导致匹配该模式的新闻组被丢弃。以感叹号 (!) 开头的模式意味着匹配的新闻组不会被发送。顺便一提，INN 配置文件中使用的简单模式匹配语法被称为 wildmat 模式。

- ◆ 第三个字段是用逗号分隔的标志列表——这些字段确定源条目类型并为条目设置某些参数。您会看到许多标志；输入 `man newsfeeds` 并阅读 man 页面以获取有关标志的更多信息。

- ◆ 第四个字段用于值取决于第三个字段设置的参数。通常，此字段包含 INN 服务器使用的文件或外部程序的名称。您可以从 newsfeeds 的 man 页面中找到有关此字段的更多信息。

既然您知道了 `/etc/news/newsfeeds` 文件的布局，就可以将其作为一个示例来研究了。默认文件包含许多示例源条目，但只有两个被注释掉了：

- ◆ `ME` 是一个特殊的源条目，始终需要存在。它有两个用途。首先，在此条目中列出的新闻组模式用作所有其他条目中所有新闻组模式的前缀。其次，`ME` 条目的发行列表决定了您的服务器接受来自远程站点的哪些发行。

- ◆ `controlchan` 源条目用于配置 INN，以便使用外部程序处理控制消息。（这些消息用于创建新新闻组和移除组。）例如，

![](img/11709a8f88c8cd03868a929dc94c0e2b_658_0.png)

以下 `controlchan` 条目指定外部程序 `/usr/lib/news/bin/controlchan` 来处理所有控制消息，除了 `cancel` 消息（用于取消文章）：

```
controlchan	:!* ,control,control.*,!control, cancel	:Tc,Wnsm: /usr/lib/news/bin/controlchan
```

除了这些源条室外，您还需要为您的新闻服务器提供新闻源的任何实际站点添加条目。此类条目的格式如下：

```
feedme.domain.com	:!junk,!control,!foo	:Tm: innfeed!
```

其中 *feedme.domain.com* 是您的系统发送新闻文章的站点的完全限定域名。

## incoming.conf 文件

*incoming.conf* 文件描述了哪些主机被允许连接到您的主机以发送文章。对于单个源，您可以添加像这样的条目：

```
peer mybuddy {
	hostname: a-feed-site.domain.com
}
```

其中 *mybuddy* 是对等方的标签，而 *a-feed-site.domain.com* 标识了为您站点提供源的站点。

![](img/11709a8f88c8cd03868a929dc94c0e2b_659_0.png)

请记住，仅仅在 *incoming.conf* 文件中添加站点名称并不会导致远程站点开始向您的站点发送新闻——它只是使您的服务器能够接受来自远程站点的新闻文章。在远程站点，您的伙伴必须配置其服务器以将文章发送到您的站点。

## readers.conf 文件

此文件指定新闻阅读器客户端（如 Mozilla）可以从您的服务器检索新闻组的主机名或 IP 地址。例如，以下 *readers.conf* 文件允许 *localhost* 和 192.168.0.0 网络中任何主机的 *读访问* 和 *发帖访问*（意味着您可以提交文章）：

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

## InterNetNews 启动

除了配置文件，您还必须启动执行新闻服务器定期维护的 cron 任务。在 Fedora Core 中，这些 cron 任务已经设置好。因此，您现在准备启动 INN 服务器——innd。

在启动 innd 之前，必须运行 makehistory 和 makedbz 来初始化并重建 INN 历史数据库。输入 man makehistory 和 man makedbz 以了解有关这些命令的更多信息。要创建初始历史数据库、关联索引并设置某些文件的所有权和权限，输入以下命令：

```
/usr/lib/news/bin/makehistory -b -f history -O -l 30000 -I cd /var/lib/news
/usr/lib/news/bin/makedbz -s `wc -l < history` -f history chown news.news *
chown news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index
```

在 Fedora Core 中，要启动 innd，请以 root 身份登录并输入 /etc/init.d/innd start。（或者，您可以输入 service innd start。）在 Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中，输入 /etc/init.d/inn start。为确保 innd 在启动时运行，在 Fedora Core 中输入 chkconfig --level 35 innd on，在 SUSE 中输入 chkconfig --level 35 inn on。在 Debian 和 Xandros 中，输入 update-rc.d inn defaults。

如果您对 INN 配置文件进行了任何更改，请记住通过调用 /etc/init.d 脚本并将 restart 作为参数来重新启动服务器。

![](img/11709a8f88c8cd03868a929dc94c0e2b_660_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_660_1.png)

## 设置本地新闻组

如果您想使用新闻组作为在公司内共享信息的方式，您可以设置一个本地新闻组层次结构。然后，您可以使用这些新闻组在公司内创建虚拟社区，具有共同兴趣的人可以非正式地讨论问题并交换知识。

## 定义新闻组层次结构

第一项任务是定义新闻组层次结构，决定每个新闻组讨论什么。例如，如果您的公司名称是 XYZ Corporation，以下是您可能定义的局部新闻组层次结构：

- ◇ `xyz.general`：关于 XYZ Corporation 的一般事务
- ◇ `xyz.weekly.news`：每周新闻
- ◇ `xyz.weekly.menu`：每周食堂菜单及相关的讨论
- ◇ `xyz.forsale`：员工出售物品的列表
- ◇ `xyz.jobs`：XYZ Corporation 的职位空缺
- ◇ `xyz.wanted`：员工发布的招聘需求（帮助、要购买的物品等）
- ◇ `xyz.technical.hardware`：关于硬件的技术讨论
- ◇ `xyz.technical.software`：关于软件的技术讨论

## 更新配置文件

以下是更新本地新闻组的配置文件并重新启动新闻服务器的步骤：

1. **为每个这些新闻组在 `/var/lib/news/newsgroups` 文件中添加描述性条目。**
   为此文件中的每个本地新闻组添加一行——输入其名称，后跟简要描述。例如，以下是您为 `xyz.general` 新闻组可能添加的内容：
   ```
   xyz.general		关于 XYZ Corporation 的一般事务
   ```

2. **编辑 `/etc/news/newsfeeds` 文件中的 ME 条目，并在逗号分隔的新闻组模式列表中添加短语 `*\*xyz.*`。**
   此步骤确保您的本地新闻组不会分发到您的站点外部。

