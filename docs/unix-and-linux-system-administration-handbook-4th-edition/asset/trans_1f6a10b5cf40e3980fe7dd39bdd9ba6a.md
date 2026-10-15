

大量 Exim 文档可在网上获取，作者也出版了几本相关书籍。

通过 Google 搜索 Exim 问题时，往往会找到陈旧、无日期且有时不合适的资料，因此请先查阅官方文档。发行版中包含一份 400 多页的规范和配置文档（doc/spec.txt）。该文档也可从 exim.org 以 PDF 文件形式获取。它是 Exim 的权威参考资料，并在每次新版本发布时都严格更新。

就 Exim 配置而言，存在两种文化：Debian 的和世界其他地方的。Debian 添加了 m4 预处理并运行自己的邮件列表来支持用户。我们不涵盖 Debian 特定的配置扩展。

Exim 4.70 及之后的版本已放弃对 DomainKeys（DKIM 的前身）的支持，并默认包含内部 DKIM 支持。两种系统在现实世界中可以共存，但 DKIM 已进入 IETF 标准轨道，并最终将取代 DomainKeys。

Exim 与 sendmail 相似之处在于它被实现为一个单一进程来执行所有邮件任务。然而，它没有继承 sendmail 的全部历史包袱（对古老地址格式的支持、需要将邮件发送到非互联网主机等）。编译时启用内容扫描，它可与 SpamAssassin 和 ClamAV 等常见的垃圾邮件和病毒扫描器接口。策略控制通过 ACL（访问控制列表）实现，可接受或拒绝消息，或将其传递给外部扫描软件。每个用户的过滤器可通过用户 .forward 文件中的一种特殊条目来实现。Exim 的许多行为在编译时指定，主要例子是 Exim 的数据库和消息存储格式。

Exim 系统中的主力组件称为路由器和传输。两者都属于“驱动程序”的总类。路由器决定消息应如何投递，而传输决定投递的机制。路由器是一系列有序的尝试项，而传输是一组无序的投递方法。

## Exim 安装

你可以从 exim.org 下载最新发行版，或如果你的站点是 Linux，则从你喜欢的软件包仓库获取。参考顶层的 README 文件和文件 src/EDITME，在其中你必须设置安装位置、用户 ID 和其他参数。EDITME 长达 1,000 多行，但大部分是注释，引导你完成编译过程；所需更改都有明确标注。编辑完成后，在运行 make 之前，将文件保存为 ../Local/Makefile 或 ../Local/Makefile-osname（如果你从同一个发行版目录为多个不同的操作系统构建配置）。

以下是 EDITME 文件中一些重要的变量（我们的看法）和建议值（Exim 开发者的看法）。前五个是必需的，其余是推荐的。

```
BIN_DIRECTORY=/usr/exim/bin          # Where the exim binary should live
SPOOL_DIRECTORY=/var/spool/exim      # Mail spool directory
CONFIGURE_FILE=/usr/exim/configure    # Exim's configuration file
SYSTEM_ALIASES_FILE=/etc/aliases     # Location of aliases file
EXIM_USER=exim                       # User to run as after rootly chores

ROUTER_ACCEPT=yes                    # Router drivers to include
ROUTER_DNSLOOKUP=yes
ROUTER_IPLITERAL=yes
ROUTER_MANUALROUTE=yes
ROUTER_QUERYPROGRAM=yes
ROUTER_REDIRECT=yes

TRANSPORT_APPENDFILE=yes             # Transport drivers to include
TRANSPORT_AUTOREPLY=yes
TRANSPORT_PIPE=yes
TRANSPORT_SMTP=yes

SUPPORT_MAILDIR=yes                  # Mailbox formats to understand
SUPPORT_MAILSTORE=yes
SUPPORT_MBX=yes

LOOKUP_DBM=yes                       # Database lookup methods to include
LOOKUP_LSEARCH=yes                   # Linear search lookup
LOOKUP_DNSDB=yes                     # Allow almost arbitrary DNS lookups
LOOKUP_CDB=yes                       # Dan Bernstein's constant DB lookups
USE_DB=yes                           # Use Berkeley DB (from README)
DBMLIB=-ldb                          # (from README)
WITH_CONTENT_SCAN=yes                # Include content scanning via ACLs

EXPERIMENTAL_SPF=yes                 # Include SPF support, needs libspf2
CFLAGS += -I/usr/local/include       # From www.libspf2.org
LDFLAGS += -lspf2

LOG_FILE_PATH=/var/log/exim_%slog    # Log files: file, syslog, or both
LOG_FILE_PATH=syslog
LOG_FILE_PATH=/var/log/exim_%slog
EXIM_LOG_MAX=10                      # Compress/cycle log files, keep 10
```

如果打算使用路由器和传输，则必须将它们编译到代码中。在内存充足的今天，你不妨全部保留。一些默认路径显然是非标准的：例如，二进制文件位于 /usr/exim/bin，PID 文件位于 /var/spool/exim。你可能希望调整这些值以匹配你其他已安装的软件。

大约有十种数据库查找方法可用，包括 MySQL、Oracle、CDB 和 LDAP。如果包含 LDAP，你必须指定 LDAP_LIB_TYPE 变量以告诉 Exim 你使用的是哪个 LDAP 库（选项为 Netscape、Solaris 以及几个版本的 OpenLDAP）。你可能还需要指定 LDAP 包含文件和库的路径。

