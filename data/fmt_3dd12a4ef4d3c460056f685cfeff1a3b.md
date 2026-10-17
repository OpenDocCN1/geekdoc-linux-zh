
$ rpm -qai | less

Fedora Core 用户也可以使用 `yum` 命令仅查看已安装软件包的名称和信息，以及任何可用的更新软件包，例如：

```
$ yum info | less
```

如果你使用的是 Fedora 且只想查看已安装软件包的信息，`yum` 命令的列表选项如下：

```
$ yum info installed ; less
```

然而，Fedora 项目在 http://fedora.redhat.com/projects/package-list/ 提供了每个 Fedora 版本中每个软件包的列表和描述。Red Hat, Inc. 的免费 Linux 发行版 Red Hat Linux 9 包含的软件包列表（编写时）可以在 http://www.redhat.com/software/linux/technical/packages.html 找到。

## 认证

Linux 认证是快速增长的技术行业的一部分。数百不同的供应商提供 Linux 技能课程和测试。然而，由于 Linux 是开源软件，并没有正式的规则或强制要求。（此处原文存在大量重复，，已按翻译要求处理）。

## 通过 UPDATE 或 YUM 保持更新

了解错误修复、安全更新和其他勘误信息对于 Red Hat Linux 或 Fedora 系统的成功和健康至关重要。在使用商业版 Red Hat Linux 发行版时，为了掌握最重要的进展，请确保在 Red Hat 网络上注册，订阅 Red Hat 公告，或定期浏览 http://www.redhat.com/apps/support/errata/index.html。你还可以使用更新客户端来维护你的工作站或服务器——但你需要订阅 Red Hat 的商业支持。

Fedora 用户使用 `yum` 命令（root 权限）来跟进错误修复、新软件包或安全更新。

## 网站和搜索引擎

互联网上存在成千上万提供有关 Linux 和 Red Hat Linux 信息的网站。立即获取所需答案的关键在于使用最好的搜索引擎和技巧。在排除故障时，知道如何搜索意味着挫败与成功的区别。本节提供了一些 Internet 搜索提示，并按各种主题列出了与 Red Hat、Fedora 和 Linux 相关的网站。这些列表是全面的，在编写时已经过检查并可以访问。

## Web 搜索提示

通过 Web 排除 Linux故障是获取棘手问题答案高效且有效的方法。进行高效搜索的最基本规则之一是使用特定的搜索词来寻找特定的答案。例如，如果你只搜索“Red Hat Linux”，你会得到很多链接和过多的信息。但如果你搜索“Fedora Core sound”，你更有可能找到你需要的信息。如果你收到了错误消息，请使用它；否则，使用 Linux 内核诊断信息作为你的搜索标准。

其他技巧包括：

- 在搜索字符串中使用符号，例如使用加号 (`+`) 强制匹配包含两个字符串的页面（如果所使用的 Web 搜索网站的搜索引擎支持此类功能）
- 在返回的结果中进行搜索
- 对结果进行排序（通常按日期排序以获取最新信息）
- 搜索相关信息
- 词干提取搜索；例如，指定不仅返回 "link"，还返回 "linking" 和 "linked"

花些时间尝试你喜爱的搜索引擎的特性——你将获得更高效的搜索结果。除了提高搜索技能外，还要花时间根据你的需求选择最好的搜索引擎。

## Google 是你的朋友

Web 上一些最快、最全面的搜索引擎由 Linux 驱动，因此使用这些可用资源是有意义的。在海量的带有搜索引擎的网站中，http://google.com 脱颖而出，每月拥有超过 1000 万用户。你可以使用先进的硬件和软件为你的搜索带来速度和效率。如果你正在寻找特定的 Linux 答案，请利用 Google 位于 http://google.com/linux 的 Linux 页面。

为什么 Google（以一位数学家命名）如此强大？你可以从 http://www.google.com/technology/index.html 的 Google 团队那里获得快速了解。它的成功部分归功于出色的算法、良好的编程和简单的界面设计，但大多数用户似乎真正赞赏 Google 在搜索引擎结果的第一页就提供你所寻找内容的链接的神奇能力。Google 的早期成功还因为该网站在数千台运行 Red Linux 的 PC 集群上运行其搜索引擎！

Google 拥有互联网上规模最大的数据库，超过 10 亿个 Web 页面和 1 PB（1024TB）的存储空间。数据库的大小非常重要，因为空的搜索结果对用户是没用的，而返回生僻主题命中结果的能力可以在成功、满意与挫败之间产生区别。Google 的功能包括：在结果页面上的 GoogleScout 链接返回相似页面、查看返回给搜索引擎的 Web 页面的确切版本（称为“缓存”功能）、高级搜索，以及最近添加的通往活跃 Usenet 新闻的链接！

为了更好地了解 Google 能为你提供什么，请浏览 http://www.google.com/options/。你会发现指向两个两个不同服务和工具的链接，涵盖了专门搜索、数据库、信息链接、翻译器和其他实用的浏览工具。

## Red Hat 软件包列表

你可以通过 `rpm` 命令快速方便地查看 Red Hat Linux 或 Fedora Core 系统上安装的 RPM 软件包列表，并附带每个软件包的简短描述：

```
$ rpm -qai | less
```

Fedora Core 用户也可以使用 `yum` 命令仅查看已安装软件包的名称和信息，以及任何可用的更新软件包，例如：

```
$ yum info | less
```

如果你使用的是 Fedora 且只想查看已安装软件包的信息，`yum` 命令的列表选项如下：

```
$ yum info installed ; less
```
