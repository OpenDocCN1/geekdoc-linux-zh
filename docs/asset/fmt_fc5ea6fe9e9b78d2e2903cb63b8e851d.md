
你可以在 `newsfeeds` 文件中使用令人眼花缭乱的选项数量。如果有兴趣深入了解，请阅读 `newsfeeds` 文件中的注释并参考 `newsfeeds` 手册页（输入 `man newsfeeds`）。该手册页还将指向相关的手册页。

## 获取活动新闻组列表

Internet Software Consortium（www.isc.org）维护着所有官方活动新闻组的列表。ISC 将这些新闻组存储在两个文件中：`newsgroups` 和 `active`。`newsgroups` 文件包含每个新闻组名称及其简短描述。`active` 文件存储新闻组以指示你的新闻服务器提供哪些新闻组。

创建 `newsgroups` 和 `active` 文件有两种方法。对于最小的新闻服务器，你可以使用 `/var/lib/news` 中的默认 `newsgroups` 和 `active` 文件并添加所需信息。然后你可以使用 `ctlinnd newsgroup` 命令稍后添加新闻组。或者，你可以从 ISC 获取完整的 `active` 和 `newsgroups` 文件并对其进行编辑。

你可以从 ISC FTP 服务器下载最新的 `active` 和 `newsgroups` 文件：http://ftp.isc.org/pub/usetnet/CONFIG/。从该目录，你可以下载这些文件的未压缩版本（每个文件大小超过 1MB）或压缩版本。选择 `active.gz` 和 `newsgroups.gz` 文件，你可以在 Red Hat Linux 中使用 `gunzip` 命令将其解压缩（`gunzip active.gz newsgroups.gz`）。

你的 `/var/lib/news` 目录中有最小的默认 `active` 和 `newsgroups` 文件。将新版本的文件复制到 `/var/lib/news`，然后手动编辑 `active` 文件。`newsgroups` 文件提供新闻服务器向用户提供的新闻组的名称和描述。`active` 文件是 `innd` 守护进程读取的官方新闻组列表，以便它知道应接受文章的新闻组。

`active` 和 `newsgroups` 文件需要由 `news` 用户拥有。因此，你应该在以 `news` 用户登录时将这些文件复制到 `/var/lib/news` 目录，或在当前目录中输入以下命令更改其所有权：

```
# chown news.news active newsgroups
```

## 创建历史数据库

在启动 INN 服务器之前，你需要创建历史数据库。你可以从 `/var/lib/news` 目录中输入以下内容来完成此操作（以 `news` 用户登录）：

```
$ touch history

$ /usr/lib/news/bin/makedb -i

$ mv history.n.dir history.dir

$ mv history.n.hash history.hash

$ mv history.n.index history.index

$ chmod 644 history*
```

## 选择文章存储方式

传统上，新闻服务器以非常简单的方式存储新闻组文章。在新闻转储目录（例如 `/var/spool/news`）中，每篇文章都存储在以新闻组命名的子目录下。例如，`comp.os.linux.x` 新闻组的文章将存储在新闻转储目录的 `comp/os/linux/x` 中。每篇文章以其唯一的邮件编号命名并放置在该目录中。

不幸的是，鉴于如今新闻组文章的巨大数量，传统的新闻文章存储方式变得相当低效。除了传统方法外，INN 新闻服务器还提供以下其他存储新闻组文章的方法：

- `timehash`：文章根据到达时间存储在目录中。这种方法使控制文章保留时间更容易，并防止任何目录包含过多的文件。

在默认新闻目录（`/var/spool/news`）中，`timehash` 存储方法根据文章接收时间创建目录。`timehash` 目录的形式为 `time-xc/bb/cc/yyy-aaa`。这里，`xx` 是存储类的十六进制值，`yyyy` 是十六进制序列号。其他值表示到达时间。

- `cnfs`：文章存储在文章到达前配置的缓冲区文件中。在这种安排下，当新文章到达且缓冲区已满时，新文章会替换最旧的文章。这被称为 `cyclical storage`。

当使用缓冲区而不是文件系统时，文章可以更快地存储和提供。此方法的缺点是，由于文章在达到缓冲区限制后会自动被覆盖，因此更难执行保留文章一段设定期限的策略。此方法也需要更多配置。

- `timecaf`：使用此存储方法，大量文章存储在单个文件中。此方法比 `timehash` 方法快约四倍，但你对文章转储的控制较少。由于此方法相对较新，因此尚未像其他方法那样经过充分测试。与 `timehash` 类似，到达时间用于命名存储文章的文件。

- `tradspool`：这是 INN 的原始存储方法，其中每篇文章都作为单独的文件存储在以其新闻组命名的目录结构中。虽然这种方法使在新闻服务器上访问文章变得容易，但对于当今新闻服务器需要处理的新闻量而言，它已变得无效。
- `trash`：此方法仅用于测试以及根据您的特定存储方法丢弃文章。已分配给垃圾存储方法的文章无法检索。

## 激活不同的存储方法

用于您的 INN 服务器的存储方法在 `/etc/news/storage.conf` 文件中设置。您可以通过在 `storage.conf` 文件中创建方法条目来激活 `timehash`、`cnfs`、`timecaf`、`tradspool` 或 `trash` 存储方法。您还可以将不同的新闻组和其他属性分配给不同的方法。（配置此文件后，`timehash` 方法不需要额外的配置文件设置；然而，`cnfs` 方法要求您设置一个 `cycbuff.conf` 文件。）

The format of a storage.conf file entry is as follows:

```
method <methodname> {

newsgroups: <wildmat>

class: <storage class number>

size: <minsize> [, <maxsize>]

expires: <mintime> [, <maxtime>]

options: <options>

}
```

对于每个方法名称（`timehash`、`cnfs`、`timecaf`、`tradspool` 或 `trash`），定义适用于该方法的新闻组（s）。可使用的通配符（`*`、`?` 等）描述在“Understanding Wildmat Characters”侧边栏中，本章前面已介绍。可选的 `class` 值可以分配一个数字（0、1 等），该数字与存储文章过期时间的 `expire.ctl` 文件中的条目相匹配。可选的 `size` 值决定文章的最小和最大大小。（`maxsize` 为 0 则不对文章大小设限。）可选的 `expires` 值根据文章中的 `Expires:` 标头确定存储类别。`options` 值（本身也是可选的）可用于设置特定于方法的操作。

## 使用 timehash 存储方法

`timehash` 存储方法根据新闻服务器接收文章的时间来存储新闻组文章。以下 `timehash` 方法条目示例包含在 `storage.conf` 文件本身中。您可以取消注释并修改这些条目以创建自己的条目：

```
method timehash {

newsgroups: *

}
```

```
method timehash {

        newsgroups: alt.binaries.*

                class: 1

                size: 2,32000

}
```

```
method timehash {

        newsgroups: alt.*

                class: 2

                size: 1

}
```

第一个 `timehash` 条目匹配所有传入的新闻组（`*`）。类号基本上标识一个与使用该条目存储的新闻组的过期时间设置相匹配的类别。（请参阅本章后面“Setting Up Expiration Times”中对 `expire.ctl` 的描述，了解每个类别是如何定义的。）第二个 `timehash` 条目为 `alt` 二进制层次结构下的新闻组分配一个类别（1）和大小（2 字节到 32,000 字节限制）。第三个 `timehash` 条目是为 `alt` 新闻组层次结构下的所有组分配一个类别（2）和一个大小（1）到无限数量的字符的示例。

## 使用 cnfs 存储方法

`cnfs` 新闻组存储方法是一种高效的方式，可根据接收到的文章数量（而不仅仅是接收时间）轮换新闻组文章。尽管此方法配置起来更复杂，但它是管理传入新闻文章数据库大小的好方法。

> TIP: INN 安装说明建议如果您拥有完整的新闻源，则使用 `cnfs` 方法存储文章。此方法比 `timehash` 存储方法更有效地管理当今必须处理的新闻量。

以下是来自 `storage.conf` 文件的 `cnfs` 方法条目的一些示例。您可以取消注释并修改这些条目以适应您的配置：

```
method cnfs {
```
