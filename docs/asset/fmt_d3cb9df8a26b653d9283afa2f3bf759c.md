
```
method <methodname> {
    class: <storage class number>
    newsgroup: <wildmat>
    size: <minsize> [,<maxsize>]
    expires: <mintime>[,<maxtime>]
    options: <options>
}
```

对于每个方法名称（`timehash`、`cnfs`、`timecaf`、`tradspool` 或 `trash`），定义适用于该方法的新闻组。本章前面“理解 Wildmat 字符”边栏中描述了可以使用的通配符字符（`*`、`?` 等）。可选的 `class` 值可以分配一个数字（`0`、`1` 等），该数字与存储文章过期时间的 `expire.ctl` 文件中的条目匹配。可选的 `size` 值确定文章的最小和最大尺寸。（`maxsize` 为 `0` 表示对文章大小没有限制。）可选的 `expires` 值根据文章中的 `Expires:` 头确定存储类。`options` 值（本身是可选的）可用于设置特定于方法选项。

## 使用 timehash 存储方法

`timehash` 存储方法根据新闻服务器接收新闻组文章的时间来存储它们。以下 `timehash` 方法条目示例包含在 `storage.conf` 文件本身中。您可以取消注释并修改这些条目来创建您自己的条目：

```
method timehash {
  newsgroups: *
  class: 0
}

method timehash {
  newsgroups: alt.binaries.*
  class: 1
  size: 2,32000
}

method timehash {
  newsgroups: alt.*
  class: 2
  size: 1
}
```

第一个 `timehash` 条目匹配所有传入的新闻组（`*`）。类号基本上标识了与使用该条目存储的新闻组的过期时间设置匹配的一个类。（请参阅本章后面“设置过期时间”中关于 `expire.ctl` 的说明，了解如何定义每个类。）第二个 `timehash` 条目为 `alt.binaries` 层级下的新闻组分配了一个类（`1`）和尺寸（`2` 字节到 `32,000` 字节的限制）。第三个 `timehash` 条目是一个示例，为 `alt` 新闻组层级下的所有组分配了一个类（`2`）和一个尺寸（`1` 到无限字符数）。

## 使用 cnfs 存储方法

`cnfs` 新闻组存储方法是一种高效的方式，用于根据收到的文章数量来轮换新闻组文章（而不仅仅是根据接收时间）。虽然这种方法配置起来更复杂，但它是管理传入新闻文章数据库大小的一种好方法。

> 提示：如果您拥有完整的新闻源，INN 安装说明建议使用 `cnfs` 方法来存储文章。对于处理当今必须处理的新闻量，这种方法比 `timehash` 存储方法效率高得多。

这里有一些来自 `storage.conf` 文件的 `cnfs` 方法条目示例。您可以取消注释并修改这些条目以适应您的配置：

```
method cnfs {
  newsgroups: *
  class: 1
  size: 0,3999
  expires: 4d
  options: FAQS
}

method cnfs {
  newsgroups: *
  class: 2
  size: 0,3999
  expires: 0s,4d
  options: SMALLAREA
}

method cnfs {
  newsgroups: *
  class: 3
  size: 4000,1000000
  options: BIGAREA
}
```

请注意，这些示例中的每个 `cnfs` 存储方法都适用于所有新闻组。文章根据其类和尺寸存储在缓冲器中。每个 `options` 字段中的值需要与 `cycbuff.conf` 文件中的条目匹配，如下节所示。

### 为 cnfs 存储分配缓冲区

对于适当的存储方法，新闻组文章会根据 `/etc/news/cycbuff.conf` 文件的内容从您的新闻服务器中轮换出来。以下是 `cycbuff.conf` 文件中定义前面所述方法所用缓冲区的一些条目：

```
# The order of lines in this file is not important among the same item.
# But all cycbuff items should be presented before any metacycbuff
# item.
# 1. Cyclic buffers
cycbuff:ONE:/export/cycbuffs/one:512000
cycbuff:TWO:/export/cycbuffs/two:512000
cycbuff:THREE:/export/cycbuffs/three:512000
# 2. Meta-cyclic buffers
metacycbuff:BIGAREA:ONE, TWO
metacycbuff:SMALLAREA:THREE
```

在 `cycbuff.conf` 文件中，所有循环缓冲区（`cycbuff`）条目都应出现在元循环缓冲区（`metacycbuff`）之前。`cycbuff` 条目的第二个字段标识缓冲区的名称。在本例中，这三个缓冲区条目分别命名为 `ONE`、`TWO` 和 `THREE`。（每个缓冲区名称后来都被分配给一个 *元循环* 缓冲区。）每个 `cycbuff` 条目中的第三个字段是标识缓冲区文件路径的文件名。最后一个字段是缓冲区的千字节大小（`1K` 等于 `1024` 字节）。

在 `metacycbuff` 条目中，第二个字段包含元循环缓冲区的符号名称（这些名称用于 `storage.conf` 文件中的 `options` 条目）。每个条目中的第三个字段然后将 `cycbuff` 条目分配给每个元循环类。

您还可以向此文件添加可选条目，例如以下条目，以影响缓冲的方式：

- `cycbuffupdate`：反映在头更新之间存储的文章数量。默认值为 `25`。
- `refreshinterval`：反映 `cycbuff` 头被读取和被重新读取之间的秒数。默认值为 `30`。

## 创建 cnfs 存储缓冲区

您可以使用 `dd` 命令在常规文件系统之上创建一个大文件。以下是使用 `dd` 命令创建缓冲区文件的示例：

```
dd if=/dev/zero of=/var/spool/news/articles/cycbuff bs=32k count=N
```

在此示例中，`N` 将替换为您想要的缓冲区大小除以 `32`。

必须将新闻用户和新闻组分配为您创建的缓冲区文件的所有者。权限模式应为 `0664` 或 `0660`。例如：

```
$ chown news /var/spool/news/articles/cycbuff
$ chgrp news /var/spool/news/articles/cycbuff
$ chmod 0664 /var/spool/news/articles/cycbuff
```

## 设置过期时间

新闻文章的过期时间在 `/etc/news/expire.ctl` 文件中设置。该文件中现有的条目可以用作您的默认过期时间。使用 `remember` 条目，文章（即使已过期）会被保留 `10` 天。这样，如果文章来自另一个新闻源，您可以接受它。以下是包含在 `expire.ctl` 中的 `remember` 条目：

```
/remember/:10
```

如果您希望 `Expires:` 头起作用，请在您的 `expire.ctl` 文件中保留以下条目：

```
!:A:1:10:never
```

某些组适合永久保留。以下是 `expire.ctl` 文件中的两行，这些行使以 `.answers` 结尾的所有新闻组以及以 `news.announce` 开始的所有新闻组的文章保留更长时间：

`expire.ctl` 文件中的条目存在三种不同的格式。第一种格式即前文所示的 `/remember/` 条目。第二种格式是用于定义与在 `storage.conf` 文件中设置的类相关联的过期时间的条目。第三种格式包含五个以冒号分隔的字段，用于将过期规则分配给特定的组。后两种格式的示例如下：

```
classnumber:keep:default:purge
newsgroups:modflag:keep:default:purge
```

以下是各字段的说明：

- `classnumber`：一个数字（`0`、`1` 等），对应于 `storage.conf` 文件中识别的一个类。
- `newsgroups`：第一个字段指定分配此过期规则的组。通常，你可以使用 `wildmat` 字符来匹配新闻组。（有关详细信息，请参阅“理解 Wildmat 字符”侧栏。）
- `modflag`：你可以使用此字段的值来进一步限制匹配哪些组。该字段应包含以下字母之一：`M`（仅限受审核的组）、`U`（仅限非受审核的组）、`A`（所有组）、`X`（删除文章）。使用 `X` 会导致所有匹配的文章从其分配的所有组中删除。
- `keep`：此字段标识文章应保留多少天。该字段应包含一个数字或单词 `never`（永不）。文章的过期时间不会早于 `keep` 设置的值。
