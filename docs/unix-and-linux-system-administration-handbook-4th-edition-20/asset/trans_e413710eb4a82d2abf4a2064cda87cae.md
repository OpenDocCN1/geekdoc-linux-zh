

# 第17章 DNS：域名系统

## 版本确定

厂商往往并不会在文档中记录他们在系统中包含了哪个版本的软件包包，因此你可能需要进行一些“侦探”工作才能准确找到你正在处理的软件到底是什么。你有时可以通过一个巧妙的挖掘——即一个与 BIND 附带的命令——来确定版本号。

```
$ dig @server version.bind txt chao
```

这将返回版本号，除非有人决定通过更改 BIND 配置文件中的设置来隐瞒信息。首先，通过以下命令确定相关域名的名称服务器的名称：

```
$ domain ns
```

然后查询 `version.bind` 查询。例如，该命令在 isrc 处可以工作：

```
$ dig @ns-ext.isc.org version.bind txt chao
version.bind 0 CH TXT "9.5.1"
```

但在 cs.colorado.edu 上却不起作用：

```
$ dig @mroe.cs.colorado.edu version.bind txt chao
version.bind 0 CH TXT "wouldn't you like to know..."
```

一些站点配置了 BIND 以隐藏其版本号，其理论是这可以提供某种程度的“模糊性安全性”。我们并不支持这种做法，但它可能有助于抵御一些脚本小子（script kiddies）。关于此主题的更详细描述请参见第603页。

此示例查询适用于其他 DNS 软件；例如，

```
$ dig @root-servers.net version.bind txt chao
version.bind 0 CH TXT "NSD 2.3.7"
```

显示 K 根名称服务器正在运行。

CHAOS 类中的另一部分数据标识了被查询的服务器名称。但是——如果你刚刚查询了服务器，你应该知道它的名字，对吧？实际上，最繁忙的服务器（例如根名称服务器）实际上是分布在全球各地的多台机器，具有相同的服务器名称和 IP 地址。这种复制方案被称为“任播路由（anycast routing）”。路由系统将你带到“最近”的实例。然而，如果你是试图调试问题的系统管理员，那么区分你访问的是复制服务器中的哪一个可能非常重要。例如，

```
$ dig @root-servers.net hostname.bind txt chao
hostname.bind 0 CH TXT "k2.nap.k.ripe.net"
```

> 17. 答案中的 0 是数据值。我们的一个报告员注意到，此查询的结果显示为“Name as Bind, James Bind!”

或者

```
$ dig @k.root-servers.net id.server txt chaos
id.server.    0 CH TXT "k2.nap.k.ripe.net"
```

IETF 试图将这些奇怪的 CHAOS 类名称标准化为独立的密集形式 `version.server` 和 `id.server`，但只有 `id.server` 通过了该过程；`version.server` 最终出现在了一个变成 RFC 的 IETF 草案中。NSD 使用所有四形式，但仅使用三个批准的形式。

作为管理员，你可以使用 `-v` 标志启动服务器（名为 nsd），将其版本打印到标准输出并退出。在 Linux 上，你可以询问你的包管理器安装了哪个版本。你也可以通过检查 `/var/log` 或其系统对应的日志文件来确定 BIND 版本。BIND 服务器在启动时会将版本记录到 syslog (daemon)。使用 `grep` 搜索 BIND 可以获取如下行：

```
Jul 13 07:19:55 nubark named[757]: starting BIND 9.5.0-P2 -u named
```

如果其他方法都失败，`dig` 的版本号通常与 `named` Parallel，而且即使没有安装 `named`，通常也会安装 `dig`。`dig` 输出的第一行包含注释的版本号。

表 17.8 显示了示例系统中包含的 BIND 版本。使用当前版本总是安全的。

## 17.8 示例系统中自带的 BIND 版本

| 系统 | OS 版本 | BIND 版本 | BIND 发布日期 |
| :--- | :--- | :--- | :--- |
| ISC | | 9.6.1-P3 | 2010年1月 |
| Ubuntu | 9.04 | 9.5.1-P2 | 2009年3月 |
| SUSE | 10.2 | 9.4.2 | 2007年11月 |
| RHEL | 5.3 | 9.3.4-P1 | 2007年7月 |
| Solaris | 5.10 | 9.3.4-P1 | 2007年7月 |
| OpenSolar | 2009.06 | 9.6.1-P1 | 2007年7月 |
| HP-UX | 11 | 9.3.2 | 2005年12月 |
| AIX | 6.1 | 8.3.3 或 9.2.1 | 2004年1月 |

AIX 向其安装的旧版本回传（back-port）安全修复，而不是升级到 ISC 的最新发布版本，因此版本号可能是误骗性的。如你所见，许多厂商并不是最新的，因此你的系统管理员可能需要升级软件。AIX 分提供 BIND 8 和 BIND 9。通用形式链接到 `named`。版本号中的 `+` 表示不完全。

每个配置语句以关键字开始，可以告诉我们关于选项的更多信息。有些语句可以以以下的方式开始，有些几乎值得单独写一个章节。

现在，来看看这些语句！有些短小精悍，有些几乎需要一个章节。

## include 语句

为了拆分或组织大型配置，你可以将配置的不同放在单独的文件。子文件通过 `include` 语句引入：

```
include "path";
```

如果路径是相对的，它相对于 `directory` 选项指定的目录进行解释。`include` 语句的一个常见用途是引入不受全局读取的密钥。与其对整个 `named.conf` 文件关闭访问，某些站点会将密钥放在受限权限。这些文件被引入 `named.conf`。

许多站点将区域语句放在单独的文件中并通过 `include` 语句将它们引入。这种配置有助于将相对静态的部分与可能变化的部分分开。

## options 语句

`options` 语句指定全局选项，某些选项可以针对特定区域或服务器进行覆盖。通用格式为

```
options {
  option;
  option;
  ...
```

如果 `named.conf` 中不存在 `options` 语句，将使用默认值。

BIND 有许多选项——实际上是太多了。9.7 版本拥有150多个选项，这对于系统管理员来说很难理解。不幸的是，每当 BIND 认为删除某些选项是个坏主意或不再需要时，就会受到使用并需要这些晦涩选项的点的反对。我们在这里没有涵盖所有的 BIND 选项；我们偏向了覆盖范围，只讨论我们推荐的。我们还询问了 BIND 开发者关于建议覆盖选项的意见，并遵循了他们的建议。

有关选项更全面的覆盖，请参见本章末列出的关于 DNS 和 BIND 的书籍。你也可以参考与 BIND 附带的文档。发行版目录下的 ARM 文档。

