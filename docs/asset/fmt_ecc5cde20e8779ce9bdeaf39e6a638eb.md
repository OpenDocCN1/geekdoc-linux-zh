
要安装远程（网络或远程主机连接）打印机，请在打印机的 `/etc/printcap` 文件条目中放置打印机主机和设备的远程条目。`:rm` 条目标识控制远程打印机的远程主机，而 `:rp` 条目指定远程打印机的设备名。在以下示例中，远程打印机位于 `rabbit.mytrek.com` 并称为 `lp1`：

```
:rm=rabbit.mytrek.com
:rp=lp1
```

## 配置 lpd

`LPRng` 允许你配置 `lpd` 服务器，设置全局默认值或控制打印机访问。只需管理两个配置文件，并且两者都 heavily 注释。你的发行版通常会为两者提供基本版本。提供了广泛的功能集，让你创建具有强大和复杂功能能力的服务器。

## lpd.conf

`LPRng` 的通用配置（包括 `lpd` 打印服务器）在 `/etc/lpd.conf` 文件中处理。在这里，你可以指定适用于所有打印机和打印管理的功能。你应该将这些功能视为默认功能，因为其中任何一项都可以在打印机的 `printcap` 条目中被覆盖。随 `LPRng` 安装的 `lpd.conf` 文件包含一份详尽的配置参数列表。这些参数全部被注释掉了，前缀为 `#` 号。每个参数前面都有一段描述该参数的注释。条目本身列出参数给出的默认值，并在条目前面加上 `default` 一词。`connect_timeout` 参数的条目如下所示：

```
# Purpose: connection timeout for remote printers
# default connect_timeout=10 (INTEGER)
```

要创建你自己的超时条目，最好在下方添加自己的条目，如下所示。注意，前面的 `#` 和 `default` 一词在新条目中都没有了。远程打印机的连接超时现在设置为 20。这可以被打印机的 `printcap` 文件条目覆盖。

```
# Purpose: connection timeout for remote printers
# default connect_timeout=10 (INTEGER)
connect_timeout=20
```

参数也可以是你可以打开或关闭的标志。关闭的标志用一个附加的 `@` 符号表示。在下面的示例中，`allow_user_logging` 参数是一个允许用户请求登录信息的标志。默认情况下，它是关闭的。下面的示例将其打开：

```
# Purpose: allow users to request logging info using lpr -mhost&port
# default allow_user_logging@ (FLAG off)
allow_user_logging
```

## LPRng 访问控制：lpd.perms

`LPRng` 提供访问控制规则，用于控制远程用户如何访问你的打印服务器，以及由此控制它所管理的打印机。这些规则放置在 `/etc/lpd.perms` 文件中，可用于拒绝向特定主机或用户提供打印服务。此类规则由一个动作和一组键（key）组成。键指定要满足的条件，如果条件满足，则执行其关联的动作。在每条规则中，你有一个动作和一个或多个键。如果有多个键，则必须满足所有条件才能执行该动作。键的一个示例是指定主机的 IP 地址。此外，你还必须指定所请求服务的种类，例如打印请求或连接请求。动作通常是 `ACCEPT` 或 `REJECT`。键作为标志或变量操作。要指定主机，你使用赋值运算符将地址赋给 `HOST` 键。对于用户，使用 `USER`；对于 IP 地址，使用 `IPIP`。服务种类由 `SERVICE` 键指定。对于打印请求，你赋的值是 `lpd` 代码 `P`。以下示例将主机指定为键，并将拒绝来自该地址的任何请求：

```
REJECT SERVICE=P HOST=192.168.0.57
```

`lpd.perms` 文件由一组规则组成，这些规则按顺序求值，直到找到匹配项。`DEFAULT` 动作规则应该是最后一条规则，通常用于接受任何请求。换句话说，任何未被前面规则匹配的请求都会被接受。通常，你会设置规则来拒绝某些请求，例如来自特定主机的请求。大多数请求不会匹配这些规则，而是会落到 `DEFAULT` 动作，即 `ACCEPT` 它们。

`SERVICE` 键的值根据提交的请求类型而不同。这些值可以从远程服务器的简单连接请求到打印作业的移除。诸如 `lpr`、`lpq`、`lprm` 和 `lpc` 等打印客户端会发出不同类型的服务请求。`lpq` 发出队列信息请求，其 `SERVICE` 键值为 `Q`。`lprm` 发出移除请求，键值为 `M`。

## LPRng 打印客户端

`LPRng` 使用与 `CUPS` 相同的命令行打印客户端。这些包括 `lpr`、`lpc`、`lpq` 和 `lprm` 命令。请查阅每个命令的手册页以了解详细选项。某些功能（如加密）仅 `CUPS` 版本可用。

## 新闻和搜索服务器

新闻服务器为 Internet 用户提供 Usenet 新闻服务。它们拥有自己的 TCP/IP 协议，即网络新闻传输协议（`NNTP`）。在大多数 Linux 系统中，包括 Red Hat，InterNetNews（`INN`）新闻服务器提供新闻服务（www.isc.org）。此外，还存在提供更好 Internet 资源访问的服务器。搜索和索引服务器 `ht://Dig` 能够对 Web 和 FTP 站点进行文档搜索（www.htdig.org）。借助它，您可以索引文档并执行复杂的搜索请求。

### 新闻服务器：INN

InterNetNews（`INN`）新闻服务器访问 Usenet 新闻源，为您网络上的新闻客户端提供完整的新闻组及其文章。新闻组文章使用 `NNTP` 传输，支持该协议的服务器被称为 `NNTP` 服务器。`INN` 由 Rich Salz 编写，目前由 Internet 软件联盟（`ISC`）维护和支持。您可以从其网站 www.isc.org 下载当前版本。`INN` 也包含在大多数 Linux 发行版中。`INN` 在 `/usr/share/doc` 中的文档目录包含大量示例。`INN` 的主要程序是 `innd` 守护进程。

### INN 配置文件

各种 `INN` 配置文件可以在 `/etc/news` 中找到，包括 `inn.conf`、`storage.conf`、`readers.conf` 和 `incoming.conf`（参见表 26-1）。`inn.conf` 设置 `INN` 的选项，而 `incoming.conf` 文件保存您接收新闻源的主机。将在 `readers.conf` 文件中为远程主机放置条目以允许它们访问您的新闻服务器。实际新闻源在 `/var/spool/news` 目录中的目录中管理。在这里您会找到诸如 `article` 的目录，其中保存新闻组文章；`outgoing` 用于您的用户发布到新闻组的文章；以及 `overview`，其中保存有关文章的摘要信息。`INN` 的正确配置可能是一个复杂且耗时的过程，因此请务必查阅参考资料和在线资源，例如文档。当您更改配置时，请务必重新启动 `INN` 服务器。`/etc/rc.d/init.d` 目录中有一个 `innd` 脚本，其参数与 Web `httpd` 脚本类似。您可以使用 `start`、`restart` 和 `stop` 参数与 `innd` 脚本来启动、重新启动和停止 `INN` 服务器。

**表 26-1 INN 配置文件**

| 文件 | 描述 |
|---|---|
| `inn.conf` | 通用 INN 配置文件。 |
| `incoming.conf` | 指定接收新闻源的主机。 |
| `cycbuff.conf` | 配置 cnfs 存储格式中使用的缓冲区。 |
| `storage.conf` | 定义存储类。这些由存储方法和使用它的新闻组组成。存储方法为存储格式：tradspool、timehash、timecaf 和 cnfs。额外的方法 trash 会丢弃文章。 |
| `expire.ctl` | 设置新闻服务器上文章的过期策略。 |
| `readers.conf` | 指定其用户可以使用新闻阅读器访问新闻服务器的主机。 |
| `ovdb.conf` | 配置 overviews 的 ovdb 存储方法。 |
| `newsfeeds` | 定义您的新闻服务器如何将文章馈送到其他新闻服务器。 |
| `moderated` | 受控新闻组。 |
| `innfeed.conf` | 配置 innfeed 的新闻源进程。 |
| `innreport.conf` | 配置 innreport 实用程序以生成基于日志的报告。 |
| `buffindexed.conf` | 配置 buffindexed 方法的概览缓冲区。 |

> 提示：`INN` 中每个配置文件都有一个 man 手册，提供有关如何配置其功能的详细信息。

#### inn.conf
