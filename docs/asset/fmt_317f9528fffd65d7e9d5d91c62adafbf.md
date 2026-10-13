
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual processing.

Let's produce correct output.

[content]
- 通过 `maxartsize` 参数，您可以限制您的服务器接受的文章大小。默认情况下，该值为 `10000`。示例：
  `maxartsize: 5000`

- `localmaxsize` 参数限制您的服务器存储的文章大小。默认情况下，该值为 `50000`。示例：
  `localmaxsize: 50000`

- 通过 `pathias` 参数，可以在新闻文章 `Path-` 行的 `pathhost` 值前添加一个名称。不需要任何值。

- `modermailer` 参数设置包含受控新闻组别名的默认杂志文件。默认情况下，使用 `/etc/inn/moderators` 文件中的值来识别来自 `moderators.isc.org` 提供的所有可用受控新闻组列表，其中新闻组名称格式化为 `(.*@moderators.isc.org)`。

- `domain` 参数决定用于您的新闻服务器的域名。通常情况下，此参数为空，系统会自动获取您计算机的域名。如果您的计算机在其他服务中不使用 FQDN，您可以手动设置此选项。

- `fromhost` 参数用于设置从新闻服务器上的用户发送的新闻文章中，`From:` 行所使用的主机名称。此信息将与用户的电子邮件地址一起添加到 `From:` 行中。如果留空，新闻服务器将使用计算机的 FQDN。（您可以通过设置 `FROMHOST` 环境变量来覆盖此值）。

# 第 22 章 设置新闻服务器 777

## 非传统存储参数

如果您在使用传统的新闻服务器存储方法，则需要在 `inn.conf` 文件中进行特殊配置以便该方法生效。然而，如果您想使用 `timehash` 或 `cnfs` 方法来存储新闻文章，则需要设置一些参数并进行进一步的配置（后文所述）。以下列表讨论了您可能想要设置的一些值：

- 如果您希望使用 Storage Manager API 存储新闻文章，则需要将 `storageapi` 参数设置为 `yes`。这在 `timehash` 和 `cnfs` 存储方法上是强制要求的。该参数默认是关闭的，因此默认将使用传统的新闻文章存储方法（如前所述）。您可以通过以下方式开启此参数：

- 如果您使用 Storage Manager API 存储新闻文章，但没有配置标记哈希（tagged hash），则应该将 `extendeddbz` 的值设置为 `true`。该值默认认为 `false`，且如果 `storageapi` 关闭，则会被忽略。将其设置为 `true` 会为您的哈希文件消耗四倍的空间，但会显著提高性能。以下是默认设置该值以关闭该功能的方式：

  `extendeddbz: false`

- 如果让 Storage Manager API 根据 Xref 头部中的新闻组名称存储文章，则 `storeonxref` 参数应为 `true`（默认即如此），如下所示。如果该值为 `false`，则新闻组文章将通过 `Newsgroups` 头部中的新闻组名称存储。

  `storeonxref: true`

- 如果将 Newsgroup-ID 存储在历史文件中，而不是仅以哈希格式存储，请将 `storemsgid` 设置为 `true`。只有当 `storageapi` 为 `false` 时，该值才能为 `true`。该值的默认显示如下：

  `storemsgid: true`

有关使用不同方法存储新闻文章的信息，请参阅本章节后面关于选择文章存储方式的章节。

## 新闻目录参数

`inn.conf` 文件设置了包含新闻组信息的目录位置。虽然您可能不需要更改这些位置，但知道它们在哪里是有帮助的。以下内容摘自 `inn.conf` 文件，用于展示不同新闻目录的位置：

```
#
#
  指向新闻系统各个部分的路径
#
```

```
pathnews: /usr
path: /usr/bin
pathfilter: /usr/bin/filter
pathcontrol: /usr/bin/control
pathdb: /var/lib/news
patetc: /etc/news
pathrun: /var/run/news
pathlog: /var/log/news
pathttp: /var/log/news
pathtmp: /usr/tmp
pathpool: /var/spool
patharticles: /var/spool/news/articles
pathoverview: /var/spool/news/overview
pathgoing: /var/spool/news/outgoing
pathincoming: /var/spool/news/incoming
patharchive: /var/spool/archive
pathunover: /var/spool/unover
overview: .overview
```

## 设置新闻源 (News Feeds)

为了让新闻文章能够流动，新闻服务器需要相互了解并愿意交换文章。`/etc/news/incoming.conf` 文件列出了允许连接并为您提供新闻的计算机。您使用 `/etc/news/newsfeeds` 文件来设置新闻文章应该发送到哪里。您必须设置这两个文件。

## 配置为您提供源的主机

要配置向您的新闻服务器提供文章的主机，您需要配置 `/etc/news/incoming.conf` 文件。在此文件中，您可以设置各种影响这些新闻源行为的键值参数。其他条目是对等（peers）或组（group）条目。

键值条目设置了分配给每个对等实体和组的值。可以通过在对等实体和组条目内添加新的键值条目来覆盖特定对象的值。对等实体识别可以向您的服务器提供新闻的计算机完全限定域名（FQDN），以及任何键值条目。组条目是将一组对等实体分配特定键值条目的方法。

当您定义主机如何向您发送新闻以及它们被允许如何这样做时，整个过程似乎有点复杂。以下是其手册页中 `incoming.conf` 文件内容的示例：

```
# 全局值，适用于所有没有
# 自己的对等实体。
max-connections: 5
```

```
# 一个对等定义。
peer uunet (
  hostname: usenet1.uu
)
peer vixie (
  hostname: gw.home.uix.com
  max-connections: 10 # 覆盖全局值。
)
# 一个包含两个对等的组，它们可以开启
# 更多的连接
group fast-sites (
  max-connections: 15
)
# 另一个对等实体。使用了来自
# fast-sites 组范围的 max-connections 值。hostname 值
# 默认为该对等实体的名称。
peer data.ramona.uix.com (
)
peer bb.home.uix.com (
  hostname: bb.home.uix.com
  max-connections: 20 # 它真的很厉害。
)
```
