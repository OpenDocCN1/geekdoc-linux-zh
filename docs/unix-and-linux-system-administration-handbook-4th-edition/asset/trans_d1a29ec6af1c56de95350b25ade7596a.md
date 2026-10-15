
# 版本确定

供应商似乎很少想到要记录他们随系统一起包含的外部软件包的版本，因此你可能需要做一些侦探工作才能弄清楚你到底在处理什么软件。有时你可以通过 dig 的一个巧妙查询来确定版本号，dig 是随 BIND 一起提供的命令。命令

```
$ dig @server version.bind txt chaos
```

会返回版本号，除非有人通过更改 BIND 的配置文件来有意隐瞒该信息。首先，使用以下命令确定所讨论域的域名服务器名称

```
$ dig domain ns
```

然后再执行 version.bind 查询。例如，该命令在 isc.org 上有效：

```
$ dig @ns-ext.isc.org version.bind txt chaos
version.bind.      0 CH TXT "9.5.1"
```

但在 cs.colorado.edu 上无效：

```
$ dig @mroe.cs.colorado.edu version.bind txt chaos
version.bind.      0 CH TXT "wouldn’t you like to know..."
```

一些站点将 BIND 配置为隐藏其版本号，其理论是这提供了某种程度的“通过模糊实现的安全”。我们并不真正推崇这种做法，但它可能有助于抵御一些脚本小子。有关此主题的更详细讨论，请参见第 603 页。

同样的查询也适用于其他一些 DNS 软件；例如，

```
$ dig @k.root-servers.net version.bind txt chaos
version.bind.      0 CH TXT "NSD 2.3.7"
```

显示 K 根名称服务器正在运行 NSD。

CHAOS 类中的另一条数据标识了被查询的服务器的名称。但等等——如果你刚刚查询了服务器，你必须知道它的名称，对吧？实际上，一些最繁忙的服务器，例如根名称服务器，实际上是分布在全球各地的多台机器，它们都具有相同的服务器名称和 IP 地址。这种复制方案称为“anycast 路由”。路由系统会将你引导到“最近”的实例。如果你是正在尝试调试问题的系统管理员，则区分你到达的是哪一台复制服务器可能很重要。例如，

```
$ dig @k.root-servers.net hostname.bind txt chaos
hostname.bind.    0 CH TXT "k2.nap.k.ripe.net"
```

或

```
$ dig @k.root-servers.net id.server txt chaos
id.server.              0 CH TXT "k2.nap.k.ripe.net"
```

IETF 试图将这些奇特的 CHAOS 类名称标准化为实现无关的形式，version.server 和 id.server，但只有 id.server 完成了整个流程；version.server 最终停留在从未成为 RFC 的 IETF 草案中。NSD 使用全部四种形式，BIND 仅使用三种已批准的形式。

作为管理员，你可以使用 -v 标志启动名称服务器 named 或 nsd，使其将版本打印到标准输出并退出。在 Linux 上，你可以询问你的包管理器安装了哪个版本。你通常也可以通过检查 /var/log 或系统等效位置中的日志文件来了解你拥有的 BIND 版本。BIND 名称服务器在启动时会将版本号记录到 syslog facility "daemon"。grep BIND 可得到如下行：

```
Jul 13 07:19:55 nubark named[757]: starting BIND 9.5.0-P2 -u named
```

如果一切都失败了，dig 的版本号通常与 named 的并行，并且即使 named 未安装，dig 也经常被安装。dig 的输出第一行包含版本号作为注释。

## 表 17.8 我们示例系统中随附的 BIND 版本

| System | OS vers | BIND vers | BIND release date |
|---|---|---|---|
| ISC | — | 9.6.1-P3 | January, 2010 |
| Ubuntu | 9.04 | 9.5.1-P2 | March, 2009 |
| SUSE | 10.2 | 9.4.2 | November, 2007 |
| RHEL | 5.3 | 9.3.4-P1 | July, 2007 |
| Solaris | 5.10 | 9.3.4-P1 | July, 2007 |
| OpenSolaris | 2009.06 | 9.6.1-P1 | July, 2009 |
| HP-UX | 11 | 9.3.2 | December, 2005 |
| AIX | 6.1 | 8.3.3+ or 9.2.1 | January, 2004 |

AIX 随附 BIND 8 和 BIND 9 两个二进制文件，分别称为 named8 和 named9。默认情况下，通用形式 named 链接到 named8。版本号中的 + 是 “+Fix_for_CERT_till_07_15_04” 的简写；并不算最新。

大多数供应商会将安全修复反向移植到其安装的旧版本发布版，而不是升级到 ISC 的最新发布版，因此版本号可能具有误导性。如你所见，我们的许多供应商都不是很及时，因此你的第一个 DNS 系统管理员任务可能是升级软件。

有关 syslog 的更多信息，请参见第 11 章。
