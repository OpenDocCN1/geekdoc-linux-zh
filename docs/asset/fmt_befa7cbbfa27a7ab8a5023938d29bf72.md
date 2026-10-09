
## 服务器安全：SSL

服务器安全涉及两个不同方面：保护你的 Web 服务器免受未经授权的访问，以及为浏览器和服务器之间的交易提供安全性。为了防止服务器受到未经授权的访问，你使用 `Squid` 等代理服务器。`Squid` 是 Linux 系统上经常使用的 GNU 代理。（参见第 29 章关于 SSL 密钥的说明。）`Apache` 本身有几个保护安全能力的模块。这些包括用于强制控制的 `mod_access`；`mod_auth`，

`mod_auth_db`、`mod_auth_digest`、`mod_auth_dbm` 以及用于匿名 FTP 类摘要的 `mod_auth_anon` 提供认证支持（请参前文关于访问控制和认证的章节）。

为了确保传输的安全，你需要完成三个任务：你必须验证身份、检查数据的完整性并确保传输的私密性。为了验证参与传输的主机身份，你执行身份验证程序。为了检查数据的完整性，你添加一个包含数据值的数字签名。摘要值是一个唯一表示数据的数值。最后，为了确保传输的私密性，你对其进行加密。这样，浏览器与服务器之间的事务就可以被加密，且只有浏览器和服务器可以解密传输内容。用于 Linux Apache 服务器实现安全传输最常用的协议是套接字层（SSL）协议，它最初由 Netscape 为网络安全交易开发。

与安全外壳（SSH）和 GNU 隐私守护（GPG）一样，SSL 使用公私钥加密的形式进行身份验证。数据使用公钥加密，但只能使用私钥解密。一旦数据通过身份验证，就会使用约定的加密算法对其进行加密。数字签名通过加密 MDS 摘要值来确保完整性。身份验证通过使用证书颁机构的证书完成。证书识别安全传输中的不同方，验证它们确实是其所声明的身份。服务器将有一个验证其身份的证书，证明它就是它声称的服务器。连接服务器的浏览器也将有一个识别其身份的证书。这些证书反过来由证书颁机构签名，证明它们是有效证书。证书颁机构是双方都信任的独立实体。

证书包含特定服务器的公钥，或者带有证书颁机构的数字签名以及身份信息（如运行服务器或浏览器的用户或公司名称）提供。证书的有效性直接取决于其可靠性。要在互联网上运行 Web 服务器，你应该从像 VeriSign 这样知名的证书颁机构获取证书。像 `stronghold` 这样的商业供应商可以完成此工作。许多知名公司维护自己的证书颁机构，以确保公司内部交易的安全。SSL 会话通过握手建立，在握手过程中，服务器和浏览器通过交换证书进行身份验证，协商用于加密传输的加密算法，并选择摘要完整性密钥的类型。用于身份验证的公钥加密类型也有可选，即 RSA 或 DSA。对于每个会话，浏览器和服务器会建立一个唯一的密钥供使用。

有一个名为 `OpenSSL` 的 SSL 免费开源版本可用。它基于 Eric A. Young 和 Tim J Hudson 的 SSL。然而，美国政府的限制阻止了 Apache Web 服务器在内置 SSL 能力的情况下自由分发。你必须单独获取 OpenSSL 并更新你的 Apache 服务器以包含此功能。

美国政府对超过 40 位的加密技术维持出口限制。SSL 支持多种加密算法，包括 168 位、128 位和 40 位的密钥（128 位被认为是安全的，相比之下，其他都是没用的）。这意味着如果 Apache 包含了 SSL，它将无法在美国境外进行分发。然而，在美国境外，有项目通过使用 OpenSSL 为 Apache 分发 SSL。这些项目在美国境的非商业用途中是免费的，但受出口限制影响。Apache-SSL 项目

自由分发内置 SSL 的 Apache，即 `apache-ssl`。你可以从他们的网站 `www.apache-ssl.org` 下载该程序（尽管对加密技术的出口有限制，但对进口/进口没有限制）。此外，`mod_ssl` 项目提供了一个带有补丁的 SSL 模块，你可以用它更新 Apache 服务器以包含 SSL（`www.modssl.org`）。在 Apache 风格的许可下，SSL 对商业和非商业用途均免费。Red Hat 和 Fedora 包含了 `mod_ssl` 模块。SSL 会话通过握手建立，在握手过程中，服务器和浏览器通过交换证书进行身份验证，协商用于加密传输的加密算法，并选择摘要完整性密钥的类型。用于身份验证的公钥加密类型也有可选，即 RSA 或 DSA。对于每个会话，浏览器和服务器会建立一个唯一的密钥供使用。

# 第 4 部分：网络服务

新闻组服务器用于为本地网络设置新闻组或支持互联网 Usenet 新闻的服务已日益少见。数据库服务器在管理本地网络海量数据集以及互联网服务方面变得越来越常见。

## 新闻服务器

新闻服务器为互联网用户提供 Usenet 新闻服务。它们有自己的 TCP/IP 协议，即网络新闻传输协议（NNTP）。在大多数 Linux 系统上，InterNetNews (`INN`) 新闻服务器提供服务（`www.isc.org`）。此外，还存在提供更佳互联网资源访问的服务器。

InterNetNews (`INN`) 新闻服务器访问 Usenet 馈送，为你网络上的新闻客户端提供完整的新闻组及其文章。新闻组文章通过 NNTP 传输，支持该协议的服务器被称为 NNTP 服务器。`INN` 由 Rich Salt 编写，目前由互联网软件协会 (`ISC`) 维护和支持。你可以从其网站 `www.isc.org` 下载当前版本。大多数 Linux 发行版也都包含了 `INN`。`/usr/share/doc` 下的 `INN` 文档目录包含示例。`INN` 的主程序是 `inn` 守护进程。

`INN` 有两个版本：一个较小的 `INN` 用于本地网络，另一个更复杂的 `INN` 用于大型网络。`INN` 还包含了几个支持程序，用于维护、崩溃恢复以及对服务器性能和使用的统计分析。`INN` 实现了基于日志的保护。`INN` 还具有一个强大的过滤系统来筛选不需要的文章。

> 注意：Leafnode 是为可能连接互联网的小型网络设计的 NNTP 服务器。你可以从网站 `www.leafnode.org` 获取软件包。

## 数据库服务器：MySQL 和 PostgreSQL

大多数 Linux 发行版都包含了两个功能完整的数据库服务器：MySQL 和 PostgreSQL。两者中 MySQL 更流行，尽管 PostgreSQL 以功能著称。本章将介绍如何设置和管理 MySQL 数据库，并对 PostgreSQL 进行简单介绍。你可以通过表 23-1 了解更多关于这些产品的信息。

| 数据库 | 资源 |
|---|---|
| MySQL | `www.mysql.com` |
| PostgreSQL | `www.postgresql.org` |

## 关系型数据库数据库结构

MySQL 和 PostgreSQL 都使用关系型数据库结构。本质上，这意味着数据被放在表中，使用字段与其他表关联。表中的每行都是一条记录，每个有一个唯一标识符。表之间的连接通过特殊表实现。关系型数据库理论和实现超出了本章的范围。

简单的单表数据库不需要唯一标识符。列出名称和地址是单表数据库的一个示例。然而，大多数数据库通过将数据划分为不同的表，每个表持有数据的唯一实例。这种方式，数据是不重复的；然后根据需要进行引用。关系型组织可以存储大量信息。有许多实现关系数据库的方法，简单的规则是将数据组织到表中，每个记录给出一个唯一标识符。

SQL 查询语言是大多数关系数据库管理系统（RDBMS）包括 MySQL 和 PostgreSQL 所使用的语言。尽管许多 RDBMS 使用管理工具管理数据库，在 Linux MySQL 和 PostgreSQL 上，你仍然需要直接使用 SQL 命令。以下命令将创建一个数据库：

```
CREATE DATABASE myphotos
```

在对数据库执行任何操作之前，首先使用 `USE` 命令访问它：

```
USE myphotos
```

使用 `CREATE TABLE` 命令创建表；表的字段列在括号内。对于每个字段，你需要指定名称、数据类型和其他选项，例如是否可以为值（null）。

```
CREATE TABLE names (
personid INT (5) UNSIGNED NOT NULL,
name VARCHAR (20) NOT NULL,
street VARCHAR (30) NOT NULL,
phone CHAR (8)
);
```

## MySQL

MySQL 构建在客户端/服务器模型之上，通过服务器守护进程（`mysql`）处理来自客户端程序的请求。MySQL 设计旨在提供速度、可靠性和易用性，是一个适用于密集使用的快速数据库管理系统。创建数据库使用标准 SQL 语言。用户访问可以通过分配权限来控制。

在 Fedora 上，你可以安装 MySQL 服务器客户端包，以及针对 Postfix、Exim 和 Apache 等服务的 MySQL 配置包。要安装的包有 `mysql-client`、`mysql-common` 和 `mysql-server`。文档包含在 `mysql-doc` 包中，并安装在 `/usr/share/doc/mysql-doc`。

## MySQL 配置

MySQL 支持三个不同的配置文件：一个用于全局设置，另一个用于服务器特定设置，还有一个可选的用于自定义设置。

- `/etc/my.cnf` 配置文件用于应用于客户端和服务器的全局设置。`/etc/my.cnf` 文件提供此类信息，如数据目录 (`/var/lib/mysql`) 和日志文件 (`/var/lib/mysql`)。

- `/etc/my.cnf` 文件用于全局设置（注：此处原文描述略有重复）。

- `/etc/my.cnf` 文件仅用于服务器设置。

- `.my.cnf` 文件允许用户自定义对 MySQL 的访问。它位于用户的目录下。注意这是一个隐藏文件（点文件）。

在 `/usr/share/doc/mysql-server` 目录下可以找到示例 `my.cnf` 文件。`/usr/share/doc` 目录列出了小型、中型、大型和巨大的实现配置。管理员手册位于 `/usr/share/doc/mysql` 目录。它是 info 格式的。输入 `info mysql` 启动它并使用回车键浏览菜单。在这里你可以找到更多关于不同选项的信息。

### 全局配置：/etc/my.cnf

MySQL 根据组（通常是服务器工具名称）指定选项。选项排列在组分区。组名放在括号内，随后是所应用的选项。默认的 `/etc/my.cnf` 文件所示：

```
[mysql]
user=mysql
datadir=/var/run/mysql/mysqld.pid
pid-file = /var/run/mysql/mysqld.pid
socket = /var/run/mysql/mysqld.sock
port = 3306
baseir = /usr
dadir = /var/lib/mysql
tmpdir = /tmp
language = /usr/share/English
```

MySQL 全局选项列在 `/etc/my.cnf` 文件中。它们被设置为组以控制 MySQL 服务器的不同行为：`mysqld` 用于守护进程，`safe-mysql` 用于 MySQL 启动脚本。`datadir /var/lib/mysql` 是你数据库文件放置的地方。服务器工具和守护进程位于 `basedir` 目录 `/usr` 下，MySQL 运行的用户由 `user` 选项指定。

`client` 组将设置发送给客户端的选项，例如使用 MySQL 数据库的端口和套。

```
[client]
port=3306
socket=/var/lib/mysql/mysqld.sock
```

## 第 23 章：新闻与数据库服务器

```
/usr/libexec/mysqld --help
```

## 用户配置：.my.cnf

访问数据库服务器的用户在自己的主目录下会有自己的配置文件：`.my.cnf`。在这里，用户可以指定连接选项，例如用于访问数据库的密码和连接超时时间。

```
[client]
password=mypassword

[mysql]
no-auto-rehash
set-auto-variable = connect_timeout=2

[mysql-hotcopy]
interactive-timeout
```

## MySQL 工具

MySQL 提供了多种工具（如表 23-2 所示），包括服务器、客户端和管理工具。可以使用 `mysqldump` 命令处理备份，`mysqlshow` 会显示数据库（这正于执行 SQL 命令 `SELECT *.*`），而 `mysqlimport` 可以导入文本文件（就像 `LOAD INFILE` 一样）。

| 命令 | 说明 |
| --- | --- |
| mysql | MySQL 服务器 |
| mysql | MySQL 客户端 |
