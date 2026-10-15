
`/remember/:14` 条目告诉 `expire` 程序在文章过期后保留历史记录 14 天。在一段时间内保留已过期文章记录的原因是处理以下情况：feed 源提供了先前已被接受并已过期的旧文章。在这种情况下，服务器将能够拒绝这些旧文章。如果没有保留记录，服务器将再次接受旧文章。

示例中的所有其他条目采用以下基本格式：

`<pattern>:<modification flag>:<keep>:<default>:<purge>`

每个条目包含五个以冒号分隔的字段：

- `pattern` 字段是一个通配符模式，指示该规则适用于哪些新闻组。
- `modification flag` 字段指示该规则适用于与 `pattern` 字段匹配的哪些类型的新闻组。`modification flag` 字段的可能值为：`A`（所有新闻组）、`M`（仅限受审核的新闻组）、`U`（仅限不受审核的新闻组）。

第四个特殊值是可能的（`x`），它表示应移除交叉张贴的文章，即使这些文章仍然列在尚未使其过期的新闻组中。

- `keep` 字段表示文章应保留在新闻组中的最短时间（以天为单位）。
- `default` 字段表示当文章未通过 `Expires` 头提供替代过期时间时，文章应保留在新闻组中的默认天数。
- `purge` 字段表示无论 `Expires` 头指定了任何替代过期时间，文章应保留在新闻组中的最长时间（以天为单位）。

请记住，当您使用 `CNFS` 存储方法时，过期时间实际上是自动的，因为新闻组的大小受到预先存在的缓冲文件大小的限制。在这种情况下，`expires.ctl` 文件中只有 `/remember/` 条目会被使用。实际上，`storage.conf` 文件中的条目控制着 `CNFS` 存储方法中文章的过期时间，如前文“为 CNFS 和 timehash 编辑 storage.conf”一节所述。

### 为 CNFS 存储创建文章池

如果您使用 `CNFS` 存储方法，可以按如下方式创建文章池：

1. 对于每个 `cycbuff`，您需要创建一个缓冲文件。这可以使用 `dd` 命令完成。例如，要创建我们在示例 `cycbuff.conf` 文件中提到的 `cycbuffs`，我们需要执行以下操作：

```
# dd if=/dev/zero of=/disk1/cycbuffs/one bs=1k count=2048000
# dd if=/dev/zero of=/disk1/cycbuffs/two bs=1k count=2048000
# dd if=/dev/zero of=/disk2/cycbuffs/three bs=1k count=2048000
# dd if=/dev/zero of=/disk2/cycbuffs/four bs=1k count=2048000
# dd if=/dev/zero of=/disk3/cycbuffs/five bs=1k count=2048000
# dd if=/dev/zero of=/disk3/cycbuffs/six bs=1k count=2048000
# chmod 0644 /disk1/cycbuffs/one
# chmod 0644 /disk1/cycbuffs/two
# chmod 0644 /disk2/cycbuffs/three
# chmod 0644 /disk2/cycbuffs/four
# chmod 0644 /disk3/cycbuffs/five
# chmod 0644 /disk3/cycbuffs/six
```

2. 每个 `dd` 命令都会创建一个文件，文件大小由 `count` 参数指定，并用零填充。`chmod` 命令确保 `cycbuffs` 具有必要的权限。

### 创建新闻历史数据库文件

要构建新闻历史数据库，您需要两个文件——`newsgroups` 文件和 `active` 文件。`makehistory` 命令使用这些文件来创建初始历史数据库。以下是创建历史数据库所涉及的各个步骤：

1. 获取 `newsgroup` 和 `active` 文件。如果您的 `INN` 发行版中没有这些文件，请从 `ftp.isc.org:/pub/usenet/CONFIG` 下载，并将它们保存到 `news` 用户主目录的 `db` 子目录（`~news/db`）中。
2. 使用命令 `su news` 切换为 `news` 用户。
3. 切换到 `db` 子目录：

```
$ cd ~/news
```

4. 使用以下命令为您的新闻存储池创建新的历史文件：

```
$ makehistory -I
```

5. 此命令会创建两个文件：`history.n.dir` 和 `history.n.pag`。
6. 将 `history.n.dir` 重命名为 `history.dir`：

```
$ mv history.n.dir history.dir
```

7. 将 `history.n.pag` 重命名为 `history.pag`：

```
$ mv history.n.pag history.pag
```

8. 设置 `db` 目录中所有文件的权限：

```
$ chmod 644 *
```

### 使用 nntpsend.ctl 文件指定要馈送的站点

`nntpsend.ctl` 文件指定从您的服务器接收馈送的站点。该文件由 `nntpsend` 进程读取，由一系列条目组成，每行一个。每个条目由四个冒号分隔的字段组成：

```
<site>:<domain name>:<maximum size>:<arguments>
```

字段的使用方式如下：

- `site` 字段指示 `newsfeeds` 文件中用于此站点的名称。该名称用于为馈送创建批处理文件。
- `domain name` 字段是接收馈送站点的完全限定域名，该名称将作为参数传递给 `innxmit` 进程。
- `maximum size` 指示批处理文件的大小限制。文件将在此大小处截断。
- `arguments` 是传递给 `innxmit` 进程的其他可选参数。

例如，考虑以下来自 `nntpsend.ctl` 文件的条目：

```
news-feed.netvision.net.il:news.netvision.net.il:4m:T800 :t300
```

此条目表示文章应发送到主机 `news-feed.netvision.net.il`，并且批处理文件应命名为 `news-feed.netvision.net.il`。站点的完全限定域名在下一个字段（`news.netvision.net.il`）中指定。`maximum size` 字段指示最大批处理文件大小为四兆字节。最后一个字段指示传递给 `innxmit` 的参数。

为了确保有序、定期地将文章发送给馈送接收者，您必须从 `cron` 守护进程调用 `nntpsend`。为此，请按照第 7 章中的说明，在 `news` 用户的 `crontab` 文件中创建一个类似于以下内容的 `cron` 条目：

```
0,10,20,30,40,50 * * * * /usr/local/news/bin/nntpsend
```

此 `crontab` 条目使 `nntpsend` 每 10 分钟运行一次，并发送已排队等待传输的已发布文章。

#### 使用 `news.daily` 脚本控制日常维护

`INN` 需要执行每日服务器维护任务，例如使旧文章过期和轮转日志文件。为此，您需要为 `news.daily` 创建一个 `cron` 条目，如下所示：

```
0 3 * * * /usr/local/news/bin/news.daily expireover lowmark
```

在 `news` 用户的 `crontab` 文件中创建此条目。该条目将使 `news.daily` 每天凌晨 3 点运行，以执行日常维护任务，例如文章的过期处理。文章过期处理可能是一项繁重的过程，因此应在使用率较低的非高峰时段运行。

`news.daily` 脚本在运行时创建摘要报告，并通过邮件发送给新闻管理员。该报告包括磁盘使用信息、日志文件大小、日志条目数、传入文章和新闻组统计信息、文章过期数据以及过期后数据。

#### 使用 `rc.news` 在启动时启动 INN

通常，您会希望在启动时启动 `INN`。一些包含 `INN` 的 Linux 发行版已经配置为这样做。如果没有，您可以通过将以下命令添加到 `/etc/rc.d/rc.local` 文件的末尾来配置您的系统：

```
su news -c /usr/local/news/bin/rc.news
```

#### 了解 INN 日志文件

`INN` 将其活动记录在 `/usr/local/news/log/news` 文件中。文件中的条目采用以下格式：

```
<date> <time> +<feed> <message ID> <site>
```

根据 `inn.conf` 文件中的配置，可选地，在 `message ID` 字段之后可能会出现两个字段：
