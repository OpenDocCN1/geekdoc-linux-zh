
要配合上一节描述的客户端使用你的 VPN 服务器，选择 OpenVPN 类型，将本节中的 `yourusername` 作为网关，类型设置为证书 (TLS)，用户证书使用你创建并移动的客户端证书，CA 证书使用你创建并移动的证书，私钥使用你创建并移动的私钥文件。

## 参考文献

- www.squid-cache.org/—Squid Web 代理缓存主页。
- deckle.co.za/squid-users-guide/—Squid 用户指南主页，一本关于 Squid 的免费在线书籍。
- https://help.ubuntu.com/community/Squid—Ubuntu 关于设置 Squid 的社区文档。
- 关于网络缓存这一主题有两本优秀的书籍。第一本是由 Duane Wessels 编写《Squid: The Definitive Guide》(O'Reilly)，ISBN: 0-596-00162-2。第二本同样由 Duane Wessels 编写《Web Caching》(O'Reilly)，ISBN: 1-56592-536-X。在这两者中，前者更具实用性，深入涵盖了 Squid 服务器。后者则更具理论性，讨论了如何实现缓存。Wessels 是 Squid 的领先开发者之一，因此这两本书在技术准确性上都是无可完美的。
- https://help.ubuntu.com/14.04/serverguide/openvpn.html — 设置 OpenVPN 的 Ubuntu 官方服务器文档。

# 第 30 章 管理关系型数据库服务

## 本章内容

- 数据库基础简要回顾
- 选择数据库：MySQL 对比 PostgreSQL
- 配置 MySQL
- 配置 PostgreSQL
- 数据库客户端
- 参考文献

本章介绍了 MySQL 和 PostgreSQL，这是 Ubuntu 存储库中可用的两种数据库系统。在本章中，你将学习这些系统的功能、这两个程序之间的比较，以及如何权衡它们的优缺点。这些信息可以帮助你根据组织的数据库需求选择并部署其中一个系统。

## 类似于 MySQL

2009 年，Oracle 宣布将收购 Sun Microsystems。该交易于 2010 年 1 月完成。短期来看，这实际上并没有产生任何影响，但数据库世界正在关注 MySQL 会发生什么变化，至少有两个小组分叉了代码，以确保数据库在保持活跃开发的同时仍然保持免费和开源。这些小组发布并正在开发 MariaDB (https://www.mariadb.org/) 和 Percona Server (http://www.percona.com/software/percona-server)。虽然没有人真正知道会发生什么，但我们建议关注这些项目以及 MySQL 的其他潜在替代方案，以防最坏的担心变成——即 Oracle 认为免费的 MySQL 与其付费数据库产品竞争过于激烈，从而杀掉或削弱该项目。有趣的是，一些相当流行的 Linux 发行版和组织已经从 MySQL 切换，例如 Fedora、OpenSUSE 和 Wikipedia（它们现在都在使用 MariaDB）。好消息是，你在本章中学到的关于 MySQL 的任何知识可能都完美适用于提到的其他选项。

组织的数据库管理员 (DBA) 有几项职责，这些职责取决于组织的规模和运营情况、支持人员等。根据特定组织的结构，如果你是 DBA，你的职责可能包括以下内容：

- **安装和维护数据库服务器**——你可能安装并维护数据库软件。维护可能涉及安装补丁以及在适当的时间升级软件。作为 DBA，你需要对系统拥有 root 权限，并知道如何管理软件（参阅第 9 章“管理软件”）。你还需要意识到内核、文件系统和安全问题。

- **安装和维护数据库客户端**——数据库客户端是访问数据库的程序（你将在本章稍后的“数据库客户端”部分中学习更多内容），可以是本地的，也可以通过网络远程访问。你的职责可能包括在用户的系统中安装和维护这些客户端。本章讨论了如何从 Linux 命令行以及通过其图形界面数据库工具来安装和使用这些客户端。

- **管理账户和用户**——账户和用户管理包括从数据库中添加和删除用户、分配和管理密码等。在本章中，你将了解到如何为 MySQL 和 PostgreSQL 授予和撤销用户权限以及密码。

- **确保数据库安全**——为了确保数据库安全，你需要关注访问控制（确保只有获得授权的人才能访问数据库）和权限（确保能够访问数据库的人不能做不应该做的事）。在本章中，你将学习如何管理安全 Shell (SSH)、Web 和本地图形用户界面 (GUI) 客户端对数据库的访问。规划和监督组织的定期备份是另一个关键环节。

- **确保数据完整性**——在服务器磁盘存储的所有信息中，数据库的完整性至关重要。确保完整性涉及考虑多用户访问，并确保当多个用户对数据库进行更改时，更改不会丢失或重复。

## 数据库基础简要回顾

数据库服务基于客户端/服务器模型。数据库通常有两种形式：扁平和关系型。关系数据库的一个示例是`/etc/passwd`：

```
root:x:0:0:root:/bin/bash
daemon:x:1:daemon:/usr/sbin/
bin:x:2:bin:/bin/
sys:x:3:sys:/dev/
sync:x:4:sync:/dev/
games:x:5:60:games:/usr/games/
man:x:6:12:man:/var/cache/man/
lp:x:7:lp:/lp/
mail:x:8:mail:/var/mail/
news:x:9:news:/var/spool/news/
uu:x:38:38:uu:/var/uu/
proxy:x:33:proxy:/bin/
backup:x:34:backup:/var/backups/
list:x:36:38:list:/var/list/
irc:x:39:irc:/var/run/ircd
gnats:x:41:41:gnats:/var/lib/gnats/
data:x:60:60:data:/root/
backup:x:74:backup:/root/
list-data:x:87:87:list-data:/var/list/
ircp:x:83:83:ircp:/nonexistent/
system-system:x:199:199:system-system:/var/cache/systemd-/
apt:x:100:100:apt:/var/cache/apt/
messaged:x:101:103:messaged:/var/log/journal/
uids:x:110:113:uids:/var/lib/uids/
```
