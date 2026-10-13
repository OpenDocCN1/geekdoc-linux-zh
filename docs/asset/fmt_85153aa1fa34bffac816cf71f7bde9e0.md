
根据参数的不同，值可以是字符串、数字或真（`true`）/假（`false`）。与许多其他文件一样，注释以井号（`#`）开头。

# 第三部分：与 Red Hat Linux 联网

## 表 16：inn.conf 中的参数

| 参数 | 描述 |
| :--- | :--- |
| mta | 设置邮件代理。默认是 `sendmail`。 |
| organization | 设置你的组织名称。 |
| method | 设置你想要使用的方法。默认是 `deault`。 |
| pathhost | 设置你的服务器的主机名。 |
| domain | 设置域名。 |
| allnews | 如果你想接收匹配该模式的新闻组，将其设置为 `true`。星号（`*`）匹配所有新闻组。以感叹号（`!`）开头的模式表示不发送这些新闻组。 |
| storageapi | 如果你想使用历史缓存，将其设置为 `true`。默认是 `0`。 |
| hiscize | 设置 KB 大。默认是 `256`。 |
| innflags | 设置任何传递给 INN 的标志。 |

## 理解新闻提源

`newsfeeds` 文件指定如何将传入的文章分发到其他服务器。`newsfeeds` 文件包含一系列条目。每个提源具有如下格式：

```
site:pattern:distrib:flags:parameter
```

每个提目的字段由冒号（`:`）分隔。通常，条目跨多行，行尾的反斜杠（`\`）用于延续。以下是每个条目的四个字段：

1. 第一字段 `site` 是提源的名称。每个名称必须唯一。
2. 第二字段由逗号分隔的新闻组模式组成，后跟一个可选的发行列表。
3. 第三个字段是逗号分隔的标志列表。
4. 第四个字段用于参数，其值取决于第三个字段。

现在你已经了解 `/etc/news/newsfeeds` 文件的布局，可以学习该文件作为示例。默认文件包含许多示例提源条目，但前两个都被注释掉了：

- `ME` 是一个始终需要的特殊提源条目。它有两个用途：首先，此条目中列出的新闻组模式会被加到所有其他条目中所有新闻组模式之前。其次，`ME` 条目的发行列表决定了你的服务器从远程站点接收的内容。

# 第 16 章：新闻服务器

`controlchan` 馈送条目用于设置 INN，以便使用外部程序处理删除控制消息（这些消息用于创建新闻组和删除组）。例如，以下 `controlchan` 指定了使用外部程序 `/usr/bin/controlchan` 来处理所有控制消息，但除了 `cancel`（用于取消文章）：

```
controlchan!
:!*,control.*,!control.cancel\
:Tm.Wnsm:/usr/lib/news/bin/controlchan
```

除了这些馈送，你还需要为你的新闻服务器提供新闻服务的任何实际站点添加条目。此类条目的格式如下

```
feedme.domain.com\
:!junk,!control/!foo\
:Tm:innfeed!
```

其中 `feedme.domain.com` 是向你的系统发送新闻文章的站点的完全域名。

## 理解 incoming.conf

`incoming.conf` 文件描述了哪些主机允许连接到你的主机馈送文章（在 INN 2.2.3 之前的版本中，使用名为 `hosts.ntp` 的文件来指定允许将文章传输到本地站点的远程主机）。对于单个馈送，你可以添加如下条目：

```
peer myfeed |
hostname: myfeedsite.com
```

其中 `myfeed` 是对端的标签，`myfeedsite.com` 标识该对端——即向你的站点提供服务的站点。

请记住，仅仅在 `incoming.conf` 文件中添加站点名称并导致该远程站点开始向你的站点提供服务——只是让你的服务器能够接受来自远程站点的新闻文章。在远程，必须配置服务器向你的站点发送文章。

## 理解 readers.conf

此文件指定了读取客户端（如 Mozilla）可以从你的服务器检索新闻组的主机名或 IP 地址。例如，以下 `.conf` 文件允许来自 `localhost` 和网络 `192.168.0.0` 中任何主机的读取访问和发布访问（这意味着你可以提交文章）：

```
auth "localhost" |
hosts: "localhost, 127.0.0.1, stdin"
default: "<localhost>"
|
access "localhost" |
users: "<localhost>"
newsgroups: "**"
```

# 486 第三部分：使用 Red Hat Linux 进行联网

```
access: RPA
auth "localnet" (
hosts: 192.168.0.0/24
default: "<localnet>"
)
access "localnet" (
users: "<localnet>"
newsgroups: **
access: RPA
)
```

## 启动 INN

除了配置文件外，你还需要启动执行新闻服务器维护的 `cron` 任务。在 Red Hat Linux 中，这些 `cron` 任务已经设置好。因此，你现在已经准备好启动 INN 服务器——`inn`。

在启动 `inn` 之前，你必须运行 `makehistory` 和 `madebz` 来初始化并重建 `inn` 历史数据库。输入 `makehistory` 和 `man madebz` 了解更多关于这些命令的信息。你可以使用以下命令创建初始历史数据库和关联索引：

```
/usr/lib/news/bin/makehistory -b f history -0 -1 30000 -I
/var/lib/news
/usr/lib/news/bin/madebz -s wc -1 < history -f history
chown news.news *
own news.news /var/spool/news/overview/group.index
chmod 664 /var/spool/news/overview/group.index
```

对于 Red Hat Linux 中的任何其他不在 `xinetd` 下运行的独立服务器，你可以通过输入以下命令设置 `inn` 在开机时启动：

```
chkconfig --level 35 innd on
```

要启动 `inn`，以 `root` 身份登录并输入以下命令：

```
service inn start
```

如果你更改了任何配置文件（如 `inn.conf` 或 `newsfeeds`），请使用以下命令重启 `inn` 服务器：

```
service inn restart
```

你可以输入 `ps ax` 来查看 `inn` 进程是否正在运行。如果一切顺利，可以在 `ps ax` 命令的输出中看到如下两个进程：

```
23789 ? S 0:00 /usr/lib/news/bin/innd -p4
23794 ? S 0:00 /usr/lib/bin/perl /usr/lib/news/bin/controlchan
```

# 第 16 章：新闻服务器 487

内部洞察 `/var/log/spooler` 文件包含 `innd` 的所有状态和错误消息。输入以下命令查看该文件中的最后几条消息：`tail /var/log/spooler`

## 设置本地新闻组

如果你想将新闻组作为公司内部共享信息的方式，可以建立本地新闻组的层级。然后，你可以使用这些新闻组在公司内部创建虚拟社区，有共同兴趣的人可以在那里非正式地讨论问题并交换知识。

## 定义新闻组层级

第一个任务是定义新闻组的层级，并决定每个新闻组将讨论的内容。例如，如果你的公司名称是 XYZ Corporation，这里是你可能定义的局部新闻组层级：

- `xyz.general`—关于 XYZ 公司的通用条目
- `xyz.weekly-news`—每周新闻
- `xyz.weekly.menu`—每周食堂菜单以及所有关于该菜单的讨论
- `xyz.iyorsale`—出售物品
- `xyz.jobs`—XYZ 公司的招聘职位
- `xyz.wanted`—想要购买
- `xyz.technical`—技术讨论
- `xyz.technical.hardware`—关于硬件的技术
- `xyz.technical.software`—关于软件的技术

## 更新配置文件

```
control               各种消息。
control.cancel       取消文章。
control.check         检查组。
control.newgroup     创建新闻组。
control.rmgroup      删除组。
junk                 填充文章。
```

在 `newsfeeds` 文件中为每个新闻组添加条目，后面跟上简要描述。你还必须为本地新闻组添加使用的存储方法。例如，你可以在 `etc/news/storage.conf` 中添加以下行来定义存储方法：

```
method: trad
```
