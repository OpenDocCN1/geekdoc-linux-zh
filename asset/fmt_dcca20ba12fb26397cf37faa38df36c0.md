
```
newsgroups: *

class: 1

size: 0,3999

expires: 4d

options: FAQs
```

method cnfs {

newsgroups: *

class: 2

size: 0,3999

expires: 0s,4d

options: SMALLAREA
}

```
```

method cnfs {

newsgroups: *

class: 3

size: 4000,1000000

options: BIGAREA
}
```

请注意，这些示例中的每个 `cnfs` 存储方法都适用于所有新闻组。文章根据类别和大小存储在不同的缓冲区中。每个 `options` 字段中的值需要与以下部分所示的 `cycbuff.conf` 文件中的条目相匹配。

### 为 cnfs 存储分配缓冲区

新闻组文章根据 `/etc/news/cycbuff.conf` 文件的内容，从您的新闻服务器中循环删除，适用于适当的存储方法。以下是 `cycbuff.conf` 文件中的一些条目，定义了前面描述的方法所使用的缓冲区：

```
# The order of lines in this file is not important among the same item.
# But all cycbuff items should be presented before any metacycbuff item.
# 1. Cyclic buffers
cycbuff:ONE:/export/cycbufs/one:512000
cycbuff:TWO:/export/cycbufs/two:512000
cycbuff:THREE:/export/cycbufs/three:512000
# 2. Meta-cyclic buffers
metacycbuff:BIGAREA:ONE, TWO
metacycbuff:SMALLAREA:THREE
```

在 `cycbuff.conf` 文件中，所有循环缓冲区 `cycbuff` 条目应出现在元循环缓冲区 `metacycbuff` 条目之前。`cycbuff` 条目的第二个字段标识缓冲区的名称。在此示例中，三个缓冲区条目分别命名为 `ONE`、`TWO` 和 `THREE`。每个缓冲区名称稍后会被分配给一个元循环缓冲区。每个 `cycbuff` 字段中的第三个字段是标识缓冲区文件路径的文件名。最后一个字段是缓冲区的大小，以千字节为单位 `1K` 等于 `1024` 字节。

在 `metacycbuff` 条目中，第二个字段包含元循环缓冲区的符号名称在 `storage.conf` 文件的 `options` 条目中使用。每个条目中的第三个字段还将 `cycbuff` 条目分配给每个元循环类别。

您还可以向此文件添加可选条目，例如以下内容，以影响缓冲：

- `cycbuffupdate`: 反映在标头更新之间存储的文章数量。默认值是 `25`。
- `refreshinterval`: 反映 `cycbuff` 标头被读取和重新读取之间的秒数。默认值是 `30`。

## 为 cnfs 存储创建缓冲区

您可以使用 `dd` 命令创建存在于常规文件系统之上的大文件。以下是用于创建缓冲区文件的 `dd` 命令示例：

```
$ dd if=/dev/zero of=/var/spool/news/articles/cycbuff bs=32k count=N
```

在此示例中，`$N$` 将被替换为您想要的缓冲区的大小除以 `32`。`news` 用户和新闻组必须被分配您创建的缓冲区文件的拥有权。权限模式应为 `0664` 或 `0660`。例如：

```
$ chown news /var/spool/news/articles/cycbuff
$ chgrp news /var/spool/news/articles/cycbuff
$ chmod 0664 /var/spool/news/articles/cycbuff
```

## 设置过期时间

新闻文章的过期时间在 `/etc/news/expire.ctl` 文件中设置。该文件中的现有条目可作为您的默认过期时间。使用 `remember` 条目，文章即使已过期会被记住 `10` 天。这样，如果文章从另一个新闻源提供，您可以接受它。以下是包含在 `expire.ctl` 中的 `remember` 条目：

```
/remember/:10
```

如果您希望 `Expires:` 标头生效，请在 `expire.ctl` 文件中保留以下条目：

```
*:A:1:10:never
```

有些组最好永久保留。`expire.ctl` 中的这些行使所有以 `.answers` 结尾的新闻组以及所有以 `news.announce` 开头的新闻组的文章保留时间更长：

```
*.answers:M:1:35:90
news.announce.*:M:1:35:90
```

`expire.ctl` 文件中的条目存在三种不同的格式。第一种格式由前面所示的 `/remember/` 条目表示。下一个是用于定义与 `storage.conf` 文件中设置的类别相关联的过期时间的条目。另一种格式包含五个以冒号分隔的字段，用于为特定组分配过期时间。以下是后两种格式的示例：

```
classnumber:keep:default:purge
newsgroups:modflag:keep:default:purge
```

以下是每个字段的描述：

- `classnumber:` 一个数字 `0`、`1` 等，对应于在 `storage.conf` 文件中标识的类。
- `newsgroups:` 第一个字段指定分配给此过期规则的新闻组。通常，您可以使用通配符来匹配新闻组。请参阅“理解 Wildmat 字符”侧边栏了解详情。
- `modflag:` 您可以使用此字段中的值进一步限制匹配的组。该字段应包含以下字母之一：`M` 仅限经过审核的组、`U` 仅限未经过审核的组、`A` 所有组、`X` 删除文章。`X` 会导致每篇匹配的文章从其分配到的每个组中删除。
- `keep:` 此字段设置应保留文章的天数。该字段包含一个数字或单词 `never`。文章不会早于 `keep` 设置的值过期。
- `default:` 此字段指定默认值以天为单位。如果 `Expires:` 值小于默认值，则使用默认值。如果 `Expires:` 值大于默认值，则 `Expires:` 值也将被 hon... hon... 采用。
- `purge:` 此字段标识文章应被保留的天数的外部边界。此边界允许接受带有 `Expires:` 标头的文章。如果文章的 `Expires:` 值长于此清除值，则文章将在 `purge` 指定的时间被丢弃。

> **提示:** 首先添加默认新闻组。使用的 `expire` 规则是最后匹配到的那个。

此文件的 contents 对 `cnfs` 存储方法来说价值较低，因为当缓冲区满时文章会被循环淘汰。因此，`cnfs` 存储方法使得精确控制文章何时被清除变得困难。

## 允许用户访问您的服务器

按照 INN 软件的交付方式，您的服务器将允许任何拥有本地主机登录的用户访问或读取新闻服务器。来自所有其他主机计算机的请求将被拒绝。为实现此目的，`/etc/news/readers.conf` 文件的内容设置如下：

```
auth "localhost" {
    hosts: "localhost, 127.0.0.1, stdin"
    default: "<localhost>"
}

access "localhost" {
    users: "<localhost>"
    newsgroups: "*"
    access: RPA
}
```

在上面的行中，`auth` 定义将本地主机身份定义为包括来自本地计算机不同接口的读取器连接。授予本地主机身份用户对所有新闻组的访问权限包括读取文章 `R`、发布文章 `P` 以及发布经过审核新闻组的文章 `A` 的能力。

您可以添加访问定义以允许从其他主机计算机访问您的 INN 服务器。例如，如果您想允许 `handsonhistory.com` 域中计算机的所有用户访问您的 INN 服务器，您可以使用以下代码：

```
auth handson {
   hosts: "*.handsonhistory.com, handsonhistory.com"
   default: "<LOCAL>"
}

access handson {
   newsgroups: "*"
   access: RPA
}
```
