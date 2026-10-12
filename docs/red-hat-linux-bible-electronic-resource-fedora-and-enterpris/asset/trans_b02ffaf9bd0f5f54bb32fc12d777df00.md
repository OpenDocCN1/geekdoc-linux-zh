
- **tradspool:** 这是 INN 的原始存储方法，其中每篇文章都作为单独的文件存储在以其新闻组命名的目录结构中。虽然这种方法使在新闻服务器上访问文章变得容易，但对于当今新闻服务器需要处理的新闻量而言，它已变得无效。
- **trash:** 此方法仅用于测试以及根据您的特定存储方法丢弃文章。已分配给垃圾存储方法的文章无法检索。

## 激活不同的存储方法

用于您的 INN 服务器的存储方法在 /etc/news/storage.conf 文件中设置。您可以通过在 storage.conf 文件中创建方法条目来激活 timehash、cnfs、timecaf、tradspool 或 trash 存储方法。您还可以将不同的新闻组和其他属性分配给不同的方法。（配置此文件后，timehash 方法不需要额外的配置文件设置；然而，cnfs 方法要求您设置一个 cycbuff.conf 文件。）

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

对于每个方法名称（timehash、cnfs、timecaf、tradspool 或 trash），定义适用于该方法的新闻组（s）。可使用的通配符（*、? 等）描述在“Understanding Wildmat Characters”侧边栏中，本章前面已介绍。可选的 class 值可以分配一个数字（0、1 等），该数字与存储文章过期时间的 expire.ctl 文件中的条目相匹配。可选的 size 值决定文章的最小和最大大小。（maxsize 为 0 则不对文章大小设限。）可选的 expires 值根据文章中的 Expires: 标头确定存储类别。options 值（本身也是可选的）可用于设置特定于方法的操作。

## 使用 timehash 存储方法

timehash 存储方法根据新闻服务器接收文章的时间来存储新闻组文章。以下 timehash 方法条目示例包含在 storage.conf 文件本身中。您可以取消注释并修改这些条目以创建自己的条目：

```
method timehash {
newsgroups: *
}
```
```
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

第一个 `timehash` 条目匹配所有传入的新闻组（*）。类号基本上标识一个与使用该条目存储的新闻组的过期时间设置相匹配的类别。（请参阅本章后面“Setting Up Expiration Times”中对 `expire.ctl` 的描述，了解每个类别是如何定义的。）第二个 `timehash` 条目为 `alt` 二进制层次结构下的新闻组分配一个类别（1）和大小（2 字节到 32,000 字节限制）。第三个 `timehash` 条目是为 `alt` 新闻组层次结构下的所有组分配一个类别（2）和一个大小（1）到无限数量的字符的示例。

## 使用 cnfs 存储方法

`cnfs` 新闻组存储方法是一种高效的方式，可根据接收到的文章数量（而不仅仅是接收时间）轮换新闻组文章。尽管此方法配置起来更复杂，但它是管理传入新闻文章数据库大小的好方法。

> TIP: INN 安装说明建议如果您拥有完整的新闻源，则使用 `cnfs` 方法存储文章。此方法比 `timehash` 存储方法更有效地管理当今必须处理的新闻量。

以下是来自 `storage.conf` 文件的 `cnfs` 方法条目的一些示例。您可以取消注释并修改这些条目以适应您的配置：

```
method cnfs {
        newsgroups: *
                class: 1
                size: 0,3999
                expires: 4d
                options: FAQs
}
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

请注意，这些示例中的每个 cnfs 存储方法都适用于所有新闻组。文章根据类别和大小存储在不同的缓冲区中。每个 options 字段中的值需要与以下部分所示的 `cycbuff.conf` 文件中的条目相匹配。

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

在 `cycbuff.conf` 文件中，所有循环缓冲区（cycbuff）条目应出现在元循环缓冲区（metacycbuff）条目之前。cycbuff 条目的第二个字段标识缓冲区的名称。在此示例中，三个缓冲区条目分别命名为 ONE、TWO 和 THREE。（每个缓冲区名称稍后会被分配给一个元循环缓冲区。）每个 cycbuff 字段中的第三个字段是标识缓冲区文件路径的文件名。最后一个字段是缓冲区的大小，以千字节为单位（1K 等于 1024 字节）。

在 metacycbuff 条目中，第二个字段包含元循环缓冲区的符号名称（在 `storage.conf` 文件的 options 条目中使用）。每个条目中的第三个字段还将 cycbuff 条目分配给每个元循环类别。

您还可以向此文件添加可选条目，例如以下内容，以影响缓冲：

- `cycbuffupdate`: 反映在标头更新之间存储的文章数量。默认值是 25。
- `refreshinterval`: 反映 cycbuff 标头被读取和重新读取之间的秒数。默认值是 30。

## 为 cnfs 存储创建缓冲区

您可以使用 dd 命令创建存在于常规文件系统之上的大文件。以下是用于创建缓冲区文件的 dd 命令示例：

```
$ dd if=/dev/zero of=/var/spool/news/articles/cycbuff bs=32k count=N
```

在此示例中，$N$ 将被替换为您想要的缓冲区的大小除以 32。news 用户和新闻组必须被分配您创建的缓冲区文件的拥有权。权限模式应为 0664 或 0660。例如：

```
$ chown news /var/spool/news/articles/cycbuff
$ chgrp news /var/spool/news/articles/cycbuff
$ chmod 0664 /var/spool/news/articles/cycbuff
```

## 设置过期时间

新闻文章的过期时间在 /etc/news/expire.ctl 文件中设置。该文件中的现有条目可作为您的默认过期时间。使用 remember 条目，文章（即使已过期）会被记住 10 天。这样，如果文章从另一个新闻源提供，您可以接受它。以下是包含在 expire.ctl 中的 remember 条目：

/remember/:10

如果您希望 Expires: 标头生效，请在 expire.ctl 文件中保留以下条目：

```
*:A:1:10:never
```

有些组最好永久保留。expire.ctl 中的这些行使所有以 .answers 结尾的新闻组以及所有以 news.announce 开头的新闻组的文章保留时间更长：

```
*.answers:M:1:35:90
news.announce.*:M:1:35:90
```

expire.ctl 文件中的条目存在三种不同的格式。第一种格式由前面所示的 /remember/ 条目表示。下一个是用于定义与 storage.conf 文件中设置的类别相关联的过期时间的条目。另一种格式包含五个以冒号分隔的字段，用于为特定组分配过期时间。以下是后两种格式的示例：

```
classnumber:keep:default:purge
newsgroups:modflag:keep:default:purge
```

以下是每个字段的描述：
