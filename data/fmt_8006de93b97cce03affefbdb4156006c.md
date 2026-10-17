
# Web 托管与互联网服务器

连接到虚拟主机 `128.138.243.150` 的客户端将获得来自 `/var/www/htdocs/company` 目录的文档，该目录应该是此网站特有的。

## 22.5 缓存与代理服务器

互联网及其上的信息正在快速增长。因此，支持这些增长所需的带宽和计算资源也在快速增长。这种局面如何持续下去呢？

处理这种增长的唯一方法是使用复制（`replication`）。无论是在国家、区域还是站点级别，随着互联网的增长，互联网内容需要从更近的源更方便地获取。每天从澳大利亚通过一条极其昂贵的链路向北美传输数百万次同一个热门网页是毫无意义的。当这些信息一旦跨越链路传输一次后，应该有一种方法将其存储起来。幸运的是，确实有这种方法。

一个答案是免费提供的 Squid Object Cache：这是一种运行在 Linux 下的缓存和代理服务器，支持 HTTP、FTP 和 SSL 等多种协议。

其工作原理如下：客户端浏览器（如 Netscape 和 Internet Explorer）连接 Squid 服务器请求互联网对象。Squid 服务器代表客户端请求（或如后文所述从缓存中提供对象），并将结果返回给客户端。此类代理服务器通常用于增强安全性或过滤内容。

在基于代理的系统中，一台机器需要通过组织的防火墙访问互联网。在学校等机构中，代理服务器还可以过滤内容，防止不当材料落入他人手中。有很多商业和免费的代理服务器（有些基于 Squid，有些不是）。

代理服务很不错，但 Squid 的缓存功能非常值得尝试。Squid 不仅缓存本地用户的信息，还允许构建 Squid 服务器分级。Squid 服务器使用 Internet Cache Protocol (`ICP`) 来通信缓存中的内容。此功能允许管理员构建这样一个系统：本地用户连接缓存服务器获取互联网内容。如果站点的另一个用户已经请求过相同的内容，则以局域网速度（通常为 `100 Mb/s`）返回。如果没有，则向区域缓存服务器请求，如果有则立即提供。

研究表明，运行缓存服务器可以减少高达 `40%` 的带宽需求。这种效率提供了经济效益。为什么“使用 Squid”？
- 1. 遗憾的是，某些网站将所有页面标记为不可缓存，这阻止了 Squid 工作。
- 2. 遗憾的是，Squid 无法缓存动态生成的页面。（参考《Linux 管理手册》可以获得更多信息等）。

## 设置 Squid

Squid 易于安装和配置。由于 Squid 需要空间来存储缓存，请将其运行在具有可用内存和磁盘空间的机器上。一个合理的配置是拥有 `256MB RAM` 和 `20GB` 磁盘的机器。我们可以从发行版通过 `RPM` 或 `apt-get` 获取 Squid 包，你也可以从 `www.squid-cache.org` 下载 Squid 的免费版本。如果你选择自己的路径，需要在解压发行版后运行配置脚本。该脚本假设将包安装在 `/usr/local/squid`。如果你喜欢其他位置，请使用 `--prefix=` 参数进行配置。

一旦安装了 Squid，你必须本地化 `squid.conf` 文件。查看发行目录中的 QUICK START 文件以获取对 `squid.conf` 需要进行的更改列表。你必须运行 `squid -z` 来构建并清空目录结构。最后，你可以手动通过脚本启动服务器；你最终需要在系统文件中调用此脚本，以便在机器启动时启动 Squid 服务器。测试 Squid，配置你的浏览器使用 Squid 服务器作为代理。此选项通常位于浏览器设置中。

## 22.6 匿名 FTP 服务器设置

FTP 是互联网上最老、最基本的服务之一，但仍在广泛使用。尽管 FTP 有多种内部用途，但互联网上常见的是“匿名 FTP”，它允许在站点没有账户的用户下载你提供的文件。

FTP 对于分发文件、文档草稿等非常有用。与 HTTP 相比，它的优势在于允许用户自行检查材料树并查看文件的大小和修改日期。你不需要编写任何 HTML 来指向新文件——只需将它们丢入目标区域即可。

要启用匿名 FTP，你需要为虚拟用户 `ftp` 创建账户，配置其家目录，并设置 FTP 服务器守护进程 `ftpd`。由于匿名 FTP 的性质，正确配置它非常重要，以免敏感文件意外泄露给全世界。

`ftpd` 由 `inetd` 管理，因此在 `/etc/inetd.conf` 和 `/etc/services` 文件中有条目。（如果你的系统使用 `xinetd` 而不是 `inetd`，你需要在 `/etc/xinetd.d` 中为 `ftpd` 创建文件，而不是使用 `/etc/inetd.conf`。）当 FTP 用户匿名登录时，`ftpd` 执行 `chroot` 调用，使 `~ftp` 目录之外的文件不可见且不可访问。这种保护提供的增强安全性非常重要，因为 `ftpd` 必须以 root 身份运行以操作套接字端口。

要允许来自匿名 `ftp`，请采取以下步骤：
- 将用户 `~ftp` 添加到你的普通密码文件中。
- 在 `~ftp` 下创建子目录 `bin`、`etc`、`lib` 和 `pub`。
- 将 `ls` 程序以及 `ls` 所需的共享库拷贝到 `~ftp/lib`。
- 将 `etc/passwd` 和 `/etc/group` 拷贝或硬链接到 `~ftp/etc`。
- 按下文描述编辑 `passwd` 和 `group` 文件。
- 将 `~ftp/etc/passwd` 中的所有密码替换为星号。
- 为 `~ftp` 下的文件和目录设置正确的权限。

没有人需要登录 ftp 账户，因此使用星号作为 ftp 的密码。指定 `/bin/false` 作为 ftp 的登录 shell 也是个好主意。由于匿名 ftp 会话限制在 `~ftp` 中，`bin` 和 `etc` 子目录必须提供 `ftpd` 需要的所有命令和配置信息。在 `chroot` 后，`~ftp/bin` 和 `~ftp/etc` 将伪装成 `/bin` 和 `/etc`。

在大多数情况下，`ftpd` 只使用 `~ftp/etc` 中的 `passwd` 和 `group` 命令副本。`~ftp` 下的 `passwd` 文件应该只包含 root、daemon 和 ftp 用户。你必须将密码替换为星号，因为这个 `passwd` 副本将供使用你 ftp 服务器的人使用。

### 表 22.4 ~ftp 下的推荐权限

| 文件/目录 | 所有者 | 模式 | 文件/目录 | 所有者 | 模式 |
| --- | --- | --- | --- | --- | --- |
| `~ftp` | root | 555 | `~ftp/etc/passwd` | root | 444 |
| `~ftp/bin` | root | 555 | `~ftp/etc/group` | root | 444 |
| `~ftp/bin/ls` | root | 111 | `~ftp/pub` | root | 755 |
| `~ftp/etc` | root | 555 | `~ftp/lib` | root | 755 |

请注意，在 Red Hat 和 SuSE 发行版中，匿名 FTP 是默认开启的。虽然默认配置使得匿名 FTP 的设置非常简单，但它对于不知其情的系统管理员构成了风险。如果您不想提供匿名 FTP 服务，请从 `passwd` 文件中删除 `ftp` 用户。

匿名 FTP 最大的安全风险之一是允许用户在 FTP 目录中存放文件。世界可写目录无论多么隐蔽，都会迅速变成“巢穴”，黑客和寻找交换盗版软件（`warez`）的青少年会在那里存储文件，耗尽你所有的带宽，并让你置身于一系列可能不尽人意、甚至是完全违法的活动链条的中心。不要成为问题的一部分；永远不要在你的系统上允许可写入的匿名 FTP 目录。

## 22.7 练习题

- **E22.1** 在你的工作站上配置一个虚拟接口。在操作前后运行 `ifconfig` 查看发生了什么变化。你能从同一子网的另一台机器 ping 通该虚拟接口吗？从不同的网络呢？为什么可以或不可以？（需要 root 权限。）

- **E22.2** 使用数据包嗅探器（`tcpdump`）捕获一个上传信息的双向 HTTP 会话（例如填写表单或搜索字段）。对会话进行注释，显示你的浏览器如何向 Web 服务器传递信息。（需要 root 权限。）

- **E22.3** 使用数据包嗅探器捕获打开一个繁忙网页（如 amazon.com 或 cnn.com 的首页）时的流量。开启了多少个独立的 TCP 连接？是由谁发起的？这是使用 TCP 协议最高效的方式吗？（需要 root 权限。）

- **E22.4** 找到一个互联网可访问的 Web 服务器的日志文件，也许是你自己网站的主服务器。检查日志文件。对于过去几小时内的访问模式，你能说明什么？在此期间出现了哪些错误？日志文件的内容说明了哪些隐私问题？（可能需要 root 权限。）

- **E22.5** 在你的系统上安装 Apache 并创建几个内容页面。从其他机器验证你的 Web 服务器是否正在运行。找到 Apache 日志文件，让你看到哪些浏览器正在访问你的服务器。配置 Apache，向 E22.1 中创建的虚拟接口提供其内容页面。（需要 root 权限。）

- **E22.6** 使用 `tcpdump` 捕获主动和被动 FTP 会话的 FTP 。支持匿名 FTP 服务器的需求如何影响站的防火墙策略？防火墙规则需要允许什么？（需要 root 权限。）

# 第三章
各种杂项

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_746_0.png)

# 23 软件安装与本地化

Linux 并不是魔法变出现在计算机上的；需要有人把它放进去。尽管现在有越来越多的供应商提供预配置的 Linux 系统，但在某些时刻，你不可避免地需要自己安装 Linux。同样，你几乎总是需要进行一些更改，以处理本地环境的特殊需求。管理员通常必须执行以下所有任务：

- 安装 Linux
- 自动化批量安装
- 系统本地化
- 保持系统更新
- 软件包管理

本章将探索一些帮助减少软件安装痛苦并使这些任务能够有效扩展的技术和应用。

## 23.1 基础 Linux 安装

在大多数情况下，Linux 盒的基础安装是简单的。你从 CD-ROM 或软盘启动它，回答几个问题，它就会软件包拷贝到你的硬盘上。

Red Hat 和 SuSE 发行版中，匿名 FTP 是默认开启的。虽然默认配置使得匿名 FTP 的设置非常简单，但它对于不知其情的系统管理员构成了风险。如果您不想提供匿名 FTP 服务，请从 `passwd` 文件中删除 `ftp` 用户。

匿名 FTP 最大的安全风险之一是允许用户在 FTP 目录中存放文件。世界可写目录无论多么隐蔽，都会迅速变成“巢穴”，黑客和寻找交换盗版软件（`warez`）的青少年会在那里存储文件，耗尽你所有的带宽，并让你置身于一系列可能不尽人意、甚至是完全违法的活动链的中心。不要成为问题的一部分；永远不要在你的系统上允许可写入的匿名 FTP 目录。

ISC（互联网软件联盟）DHCP 服务器随我们的发行版一起发布，支持 PXE。如果你使用不同的 DHCP 服务器，安装 Intel 的 PXE 包。

Debian 项目的标准正在改进。 ... 一个名为 FAI 的项目：

http://informatik.uni-ko/fai

Debian 项目的标准正在改进。 ...
http://debian.org/stable/

Debian 项目的标准正在改进。 ...
http://redhat.com/manual

Debian 项目的标准正在改进。 ...
http://debian.org/manuals

Debian 项目的标准正在改进。 ...
http://debian.org/install/

Debian 项目的标准正在改进。 ...
http://debian.org/network/

Debian 项目的标准正在改进。 ...
http://debian.org/docs/

Debian 项目的标准正在改进。 ...
http://debian.org/security/

Debian 项目的标准正在改进。 ...
http://debian.org/ports/

Debian 项目的标准正在改进。 ...
http://debian.org/support/

Debian 项目的标准正在改进。 ...
http://debian.org/archive/

Debian 项目的标准正在改进。 ...
http://debian.org/help/

Debian 项目的标准正在改进。 ...
http://debian.org/news/

Debian 项目的标准正在改进。 ...
http://debian.org/faq/

Debian 项目的标准正在改进。 ...
http://debian.org/media/

Debian 项目的标准正在改进。 ...
http://debian.org/wiki/

Debian 项目的标准正在改进。 ...
http://debian.org/community/

Debian 项目的标准正在改进。 ...
http://debian.org/events/

Debian 项目的标准正在改进。 ...
http://debian.org/blog/

Debian 项目的标准正在改进。 ...
http://debian.org/conference/

Debian 项目的标准正在改进。 ...
http://debian.org/press-release/

Debian 项目的标准正在改进。 ...
http://debian.org/announcements/

Debian 项目的标准正在改进。 ...
http://debian.org/security-team/

Debian 项目的标准正在改进。 ...
http://debian.org/securityreport/

Debian 项目的标准正在改进。 ...
http://debian.org/securitytracker/

Debian 项目的标准正在改进。 ...
http://debian.org/downloads/

Debian 项目的标准正在改进。 ...
http://debian.org/dist/

Debian 项目的标准正在改进。 ...
http://debian.org/cdimage/

Debian 项目的标准正在改进。 ...
http://debian.org/ports/

Debian 项目的标准正在改进。 ...
http://debian.org/archive/

Debian 项目的标准正在改进。 ...
http://debian.org/devel/

Debian 项目的标准正在改进。 ...
http://debian.org/devel-info/

Debian 项目的标准正在改进。 ...
http://debian.org/mirrors/

Debian 项目的标准正在改进。 ...
http://debian.org/security-tracker/

Debian 项目的标准正在改进。 ...
http://debian.org/security-data/

Debian 项目的标准正在改进。 ...
http://debian.org/legal/

Debian 项目的标准正在改进。 ...
http://debian.org/copyright/

Debian 项目的标准正在改进。 ...
http://debian.org/copyright-policy/

Debian 项目的标准正在改进。 ...
http://debian.org/licenses/

Debian 项目的标准正在改进。 ...
http://debian.org/trademarks/

Debian 项目的标准正在改进。 ...
http://debian.org/social-guidelines/

Debian 项目的标准正在改进。 ...
http://debian.org/codebase/

Debian 项目的标准正在改进。 ...
http://debian.org/bugs/

Debian 项目的标准正在改进。 ...
http://debian.org/changelog/

Debian 项目的标准正在改进。 ...
http://debian.org/releases/

Debian 项目的标准正在改进。 ...
http://debian.org/supported-os/

Debian 项目的标准正在改进。 ...
http://debian.org/documentation/

Debian 项目的标准正在改进。 ...
http://debian.org/packages/

Debian 项目的标准正在改进。 ...
http://debian.org/users/

Debian 项目的标准正在改进。 ...
http://debian.org/about/

Debian 项目的标准正在改进。 ...
http://debian.org/contact/

Debian 项目的标准正在改进。 ...
http://debian.org/donate/

Debian 项目的标准正在改进。 ...
http://debian.org/jobs/

Debian 项目的标准正在改进。 ...
http://debian.org/meet/

Debian 项目的标准正在改进。 ...
http://debian.org/forum/

Debian 项目的标准正在改进。 ...
http://debian.org/irc/

Debian 项目的标准正在改进。 ...
http://debian.org/list/

Debian 项目的标准正在改进。 ...
http://debian.org/news/

Debian 项目的标准正在改进。 ...
http://debian.org/search/

Debian 项目的标准正在改进。 ...
http://debian.org/random/

Debian 项目的标准正在改进。 ...
http://debian.org/help/

Debian 项目的标准正在改进。 ...
http://debian.org/sitemap/

Debian 项目的标准正在改进。 ...
http://debian.org/rss.xml/

Debian 项目的标准正在改进。 ...
http://debian.org/feed.xml/

Debian 项目的标准正在改进。 ...
http://debian.org/atom.xml/

Debian 项目的标准正在改进。 ...
http://debian.org/robots.txt/

Debian 项目的标准正在改进。 ...
http://debian.org/security.txt/

Debian 项目的标准正在改进。 ...
http://debian.org/privacy.txt/

Debian 项目的标准正在改进。 ...
http://debian.org/

Debian 项目的标准正在改进。 ...
http://www.debian.org

# Linux 系统管理手册

尽管 Red Hat 的团队尚未正式支持 PXE，但他们确实提供了一些可用的 PXE 相关功能，并将 Intel PXE 软件作为其发行版的一部分共享。Kickstart 可以配置为在 PXE 上运行；参见：

```
```
