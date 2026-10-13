
在`/etc/news`目录下可以找到各种 INN 配置文件，包括`inn.conf`、`storage.conf`、`readers.conf`和`incoming.conf`（见表 26-1）。`inn.conf`用于设置 INN 的选项，而`incoming.conf`文件则包含接收新闻源的计算机主机信息。在`readers.conf`文件中为远程主机添加条目，以允许其访问您的新闻服务器。实际新闻源在`/var/spool/news`目录下的各个目录中管理。在这里，您会看到诸如`article`（存放新闻组文章）、`outgoing`（存放用户发布到新闻组的文章）以及`overview`（存放文章摘要信息）等目录。正确配置 INN 可能是一个复杂且耗时的过程，因此请务必查阅参考手册和在线资源，例如文档。更改配置时，请务必重启 INN 服务器。`/etc/rc.d/init.d`目录下有一个`innd`脚本，其参数与 Web httpd 脚本类似。您可以使用`innd`脚本的`start`、`restart`和`stop`参数来启动、重启和停止 INN 服务器。

表 26-1：INN 配置文件

| 文件 | 描述 |
|------|-------------|
| `inn.conf` | 通用 INN 配置文件。 |
| `incoming.conf` | 指定接收新闻源的主机。 |
| `cycbuff.conf` | 配置 cnfs 存储格式中使用的缓冲区。 |
| `storage.conf` | 定义存储类。存储类由存储方法和使用它的新闻组组成。存储方法是存储格式：`tradspool`、`timehash`、`timecaf`和`cnfs`。另一种方法`trash`会丢弃文章。 |
| `expire.ctl` | 设置新闻服务器上文章的过期策略。 |
| `readers.conf` | 指定可以使用新闻阅读器访问新闻服务器的主机。 |
| `ovdb.conf` | 配置`ovdb`存储方法用于概览。 |
| `newsfeeds` | 定义您的新闻服务器如何将文章馈送到其他新闻服务器。 |
| `moderated` | 受控新闻组。 |
| `infeed.conf` | 配置`infeed`的新闻源处理进程。 |
| `innreport.conf` | 配置`innreport`工具以生成基于日志的报告。 |
| `buffindexed.conf` | 配置`buffindexed`方法的概览缓冲区。 |

**提示** INN 中每个配置文件都有一个人页（man page），提供了关于如何配置其功能的详细信息。

### inn.conf

在许多发行版中，已经为您设置了带有默认设置的基本`inn.conf`文件。有几个初始参数需要您自行设置，例如`domain`，它保存您服务器的域名；`pathhost`，在此指定您希望您的新闻阅读器在发布的新闻文章 Path 头部字段中显示的名称；以及`server`，在此指定您新闻阅读器的 IP 地址或完全限定域名，例如`mynews.mytrek.com`。已经为您设置了不同的 Path 选项，用于定义不同 INN 目录的位置，例如将`patharticles`设置为`/var/spool/news/articles`（存放您的新闻组文章），将`pathetc`设置为`/etc/news`（存放您的配置文件）。

### 存储格式

对于通常被下载和访问的海量新闻文章，存储格式是像 INN 这样全规模新闻服务器的核心关注点。INN 允许您在四种可能的存储格式中进行选择：`tradspool`、`timehash`、`timecaf`和`cnfs`。`tradspool`是一种传统方法，其中文章根据其所属新闻组安排在简单的目录结构中。这种方法在访问和存储时已知非常耗时。`timehash`将文章存储在按接收时间组织的目录中，这使得删除过期文章变得更容易。`timecaf`类似于`timehash`，但同一时间接收的文章被放在同一个文件中，从而大大加快访问速度。`cnfs`将文章存储到已经设置好的缓冲区文件中。当缓冲区文件变满时，新来的文章会覆盖较旧的文章。这是一种极快的方法，因为不会创建新文件。无需设置最大文章限制，但也没有控制文章保留时长的机制。在`storage.conf`文件中，存储格式作为存储方法分配给不同的新闻组。

### 概览

INN 还支持概览。这些是文章的摘要，读者可以查看它们，而无需下载整篇文章来了解其内容。概览有自己独立的存储方法：`tradindexed`、`buffindexed`和`ovdb`。您在`inn.conf`的`ovmethod`功能中指定想要使用的方法。`tradindexed`对读者来说速度快，但对服务器来说生成难度大。`buffindexed`对新闻服务器来说速度快，但对读者来说速度慢。`ovdb`使用 Berkeley DB 数据库文件，对双方都非常快，但占用更多磁盘空间。如果您选择`ovdb`，可以在`ovdb.conf`中为其设置配置参数。

### INN 实施

在许多发行版中，已经创建了一个新闻用户和一个供 INN 守护进程使用的新闻组，并设置了`/var/spool/news`中的新闻目录。INN 软件还安装了一些 cron 脚本，用于更新您的新闻服务器，即删除旧文章并获取新文章。这些脚本通常放置在`/etc/cron.daily`目录中，尽管它们也可以位于任何位置。`inn-cron-expire`用于删除旧文章，而`inn-cron-rnews`用于检索新文章。`inn-cron-nntpsend`将从您的系统发布的文章发送到其他新闻服务器。

INN 还包括多个支持程序，用于提供维护和崩溃恢复，以及对服务器性能和用法进行统计分析。`cleanfeed`实现垃圾邮件保护，而`innreport`根据日志生成 INN 报告。INN 还具备一个非常强大的过滤系统，用于筛选不需要的文章。

**注意** `Leafnode`是为可能拥有较慢互联网连接的小型网络设计的 NNTP 服务器。您可以获取`Leafnode`软件包以及

![](img/32a48d8db4c23e6e2eb70d1e5034c976_598_0.png)

### Dig 服务器

`Dig`，官方名称为`ht://Dig`，是一种专为小型网络或内网设计的 Web 索引和搜索系统。`Dig`并不被视为全规模互联网搜索系统（如 Lycos、Infoseek 或 AltaVista）的替代品。与基于 Web 服务器的搜索引擎不同，`Dig`可以跨越站点中的多个 Web 服务器。`Dig`由圣地亚哥州立大学开发，并以 GNU 通用公共许可证免费分发。您可以在`www.htdig.org`获取相关信息、文档和软件包。

### Dig 搜索

`Dig`支持简单和复杂搜索，包括复杂的布尔搜索和模糊搜索方法。*模糊搜索*支持多种搜索算法，包括精确匹配、`Soundex`和同义词。搜索可以针对文本和 HTML 文档进行。HTML 文档可以包含关键词以提高检索准确性，您还可以使用 HTML 模板来控制结果的显示方式。

搜索可以根据认证要求、位置和搜索深度进行限制。为了保护受限目录中的文档，可以通知`Dig`要求输入特定的用户名和密码。您还可以限制搜索以检索特定 URL 中的文档，搜索数据库的子部分，或仅检索距离指定链接数之内的文档。

### Dig 配置

所有`ht://Dig`程序使用相同的配置文件`htdig.conf`，它位于`/etc/htdig`目录中。配置文件由属性项组成，每项以属性行开头，后跟冒号后的值。每个程序只使用它需要的属性：

```
max_head_length: 10000
```

您可以指定诸如`allow_virtual_hosts`（将虚拟主机作为独立服务器进行索引）和`search_algorithm`（指定用于搜索的算法）等属性。

### Dig 工具

`Dig`由五个程序组成：`htdig`、`htmerge`、`htfuzzy`、`htnotify`和`htsearch`。`htdig`、`htmerge`和`htfuzzy`生成索引，而`htsearch`执行实际搜索。首先，`htdig`收集数据库信息，搜索您域中的所有 URL 连接，并将网页与术语关联。`htmerge`程序使用此信息创建可搜索的数据库，并将之前生成的数据库中的信息合并进来。`htfuzzy`创建索引，允许使用模糊算法（如`Soundex`和同义词）进行搜索。数据库创建完成后，用户可以使用调用`htsearch`的网页来搜索此索引。结果会列在一个网页上。您可以在 HTML 文档中使用 META 标签来输入特定的`htdig`关键词、将文档排除在索引之外，或提供通知信息（如电子邮件地址和过期日期）。`htnotify`使用电子邮件和过期日期，在网页作者的内容过时时通知他们。
