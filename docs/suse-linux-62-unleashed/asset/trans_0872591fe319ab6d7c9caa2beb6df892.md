

# 网络与互联网服务
第二部分

2. 如果你允许本地局域网或其他机器或通过机器上的远程访问服务器连接的机器读取由系统收集的新闻，你需要将它们的名称添加到 `/etc/news/nnrp.access` 文件中。当每个人调用新闻阅读器时，nnrp 守护进程启动时会读取此文件。`nnrp.access` 文件包含了允许从你的服务器读取新闻的所有机器列表，并遵循以下语法：

```
name:perms:password:newsgroup
```

name 是你允许读取新闻的机器地址。你可以使用通配符来允许整个子集。perms 是权限，取值可以是以下值之一：Read（只读访问）、Post（允许发布消息）或 Read Post（同时允许读取和发布）。用户在允许发布前需要通过用户名进行身份验证，password 则完成相同任务。为了防止用户通过你的服务器发布消息，请将 user 和 password 留空，以便它们无法被匹配。

newsgroup 是新闻组名称的模式，取决于你如何设置内容，可以读取或不读取。新闻组的访问使用通配符，`comp*` 允许访问所有以 `comp` 开的新闻组，而 `sex` 则禁用访问任何以单词 `sex` 开头的组组。`nnrp.access` 文件的默认设置为阻止所有访问。要允许 `tpci.com` 域内的所有用户在无需身份验证的情况下读取和发布新闻，请在文件中添加行：

```
*tpci.com:Read Post::*
```

要忽略域名名向你系统上的所有人开放新闻系统，请在域名中使用星号。

3. `inn.conf` 文件应该位于你的 `/etc/news` 目录。你可能应该将包含 organization 的行更改为：

```
organization: 你的公司名称
```

这指定了当用户访问你服务器上的新闻组时的默认组织标头信息。

当然，如果你正在设置 INN 从你 ISP 的新闻服务器获取新闻，那么 ISP 必须在其端设置好你希望用户访问的新闻组。记住，新闻会占用大量带宽，因此请尽量减少新闻下载量。

在设置 `incoming.conf`、`nnrp.access` 和 `inn.conf` 文件并通知你的 ISP 你想使用 NNTP 服务后，你就应该能够使用 INN 下载新闻并使用新闻阅读器访问它。（这假设你已经在 `nnrp.access` 文件中授予了自己权限）。INN 的配置文件中可以引入许多复杂性，但保持简单往往是最好的方法。随着经验的增长，你可以修改新闻源的行为；但是，你应该从简单的访问方法开始，以便先测试新闻系统。设置好 INN 后，下一步是为用户提供一个新闻阅读器。

# NNTPCache 简介

如前所述，许多公司和个人运行 NNTPCache 而不是获取完整的新源。这是因为 NNTPCache 可以节省费用。本章描述的 NNTPCache 可能是最流行的。编写时，NNTPCache 并没有随 SuSE Linux 发布，但可以从 http://www.nntpcache.org 轻松下载。需要注意的是，NNTPCache 对个人和非营利组织免费，但在商业环境中应获得许可。请查看目录下的 `LICENSING` 文件获取更多信息。

# NNTPCache 如何工作

NNTPCache 的设计看起来像一个基于 NNRP 的普通服务器，任何新闻阅读器都可以连接到它——但有一个不同之处。如果你正在配置 NNTPCache 获取文章的默认新闻服务器；这通常是你 ISP 的新闻服务器。例如，如果你正在读取 `comp..linux.advocacy` 新闻组，你选择读取的每篇文章都从你的默认新闻服务器检索，并将副本保留在你的 NNTPCache 服务器上——这个过程被称为缓存文章。

不仅文章被缓存，新闻服务器的活动列表（active lists）也是。活动列表是该特定新闻服务器的当前新闻组列表。这很有用，因为不需要每次打开新闻阅读器时都刷新列表。

NNTPCache 的另一个功能是它可以连接到多个新闻服务器。有许多公共新闻服务器通常与特定主题相关。例如，微软提供了一个名为 `msnews.microsoft.com` 的新闻服务器，并拥有与微软相关主题的特定新闻组（新闻组命名为 `microsoft.*`）。SuSE 有一个新闻服务器，但无法公开访问。为了充分利用这一奇妙的功能，请配置 NNTPCache 与特定服务器通信并将新闻组与这些服务器关联。当你使用阅读器时，它让浏览所有不同的新闻服务器变得透明化，并为你你缓存所有内容。

显然，要充分利用 NNTPCache 的缓存能力，你需要一个相对稳定的互联网连接以及许多人使用你的 NNTPCache。即使你使用普通的普通的拨号连接，它仍然很有用。然而，你可能想为 NNTPCache 配置较小的磁盘空间作为缓存，或者将其完全关闭。

![](img/cbac72550c7126a22162e94d91a0c360_460_0.png)

# 下载和配置 NNTPCache

NNTPCache 不是标准 SuSE 6.2set的一部分，你必须下载它。这是一个非常简单的过程，因为可以从 NNTPCache 网站下载。访问 http://www.nntpcache.org/source.html 并向下滚动到提到 2.3.3 版本源码的地方；将其下载到你的机器上。RPM 包不适用，因为它是为 Red Hat 设计而非 SuSE。

一旦你下载了 NNTPCache RPM，你需要使用以下命令进行安装：

```
tar zf nntpcache-2.3.3.tar.gz
cd nntpcache-2.3.3
./configure ; make
```

以 root 身份执行以下操作：

```
make install
```

这会将配置文件安装在 `/etc/nntpcache` 下，将一些文档安装在 `/usr/doc/nntpcache-1.0.7.1-1`，并将执行所有工作的 NNTPCache 服务器安装在 `/usr/bin`。当然，适当的启动文件安装在 `/sbin/init.d` 树中。

之后，你可以删除源码：

```
rm -r nntpcache-2.3.3*
```

启动并运行不应该很长时间。进入 `/etc/nntpcache` 目录并输入 `ls` 命令：

```
root@nntpcache]# ls -l
total 26
-rw-r--r-- 1 root root 3584 Apr 27 23:05 access
-rw-r--r-- 1 root root 9315 Apr 27 23:04 config
-rw-r--r-- 1 root root 862 Apr 30 22:11 servers
-rw-r--r-- 1 root root 998 Jan 21 spam.filter
```

三个主要的配置文件：access、config 和 servers。还有一个文件 `spam.filter`，它包含过滤垃圾信息的字符串。第一个要配置的文件是 `access` 文件。允许使用 NNTPCache 的主机在此指定。你可以为指定的主机指定权限。现在，插入一个项允许你的局域网机器访问 NNTPCache：下一个要配置的文件是 `config`。此文件在 NNTPCache 启动时读取。你可能应该将组织字段更改为：

```
Organization MyCompany Ltd
```

当新闻阅读器未指定组织时，它会填充该字段。你可能会发现还有其他需要调整的参数，但目前足够了。

最后一个你需要编辑的文件是 `servers`。这是你指定想要配合 NNTPCache 使用的所有新闻源的地方。随 NNTPCache 发布的 servers 文件包含许多可能参考的示例，建议将现有文件重命名为 `servers.old` 并创建一个包含以下内容的新文件：

```
# timeouts
# host:port Interface Active.tim Newsgrp
- Group Xover
news.mysisp.net:119 DEFAULT 10m 12h 12h
- 10m 60d
msnews.microsoft.com:119 DEFAULT 24h 4d 4d
- 60m 60d
```

%BeginInGroups
# Group pattern Host
* news.mysisp.net:119
microsoft.* msnews.microsoft.com:119

确保此新的 servers 文件由用户和新闻组所有。前三个项指定了要使用的服务器。将 `news.mysisp.net` 替换为你的 ISP 提供的新闻服务器名称。注意我包含了微软的新闻服务器。

互联网新闻
第12 章

可以从互联网访问你维护的特定产品。

