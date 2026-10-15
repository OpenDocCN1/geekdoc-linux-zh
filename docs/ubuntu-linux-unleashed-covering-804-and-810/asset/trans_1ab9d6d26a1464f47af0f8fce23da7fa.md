

## 相关 Ubuntu 和数据库命令

以下命令对于在 Ubuntu 中创建和操作数据库很有用：

- `createdb`—创建新的 PostgreSQL 数据库
- `createuser`—创建新的 PostgreSQL 用户账户
- `dropdb`—删除 PostgreSQL 数据库
- `dropuser`—删除 PostgreSQL 用户账户
- `mysql`—交互式查询 MySQL 服务器
- `mysqladmin`—管理 `mysqld` 服务器
- `mysqldump`—转储或备份 MySQL 数据或表
- `pgaccess`—访问 PostgreSQL 数据库服务器
- `pg_ctl`—控制 PostgreSQL 服务器或查询其状态
- `psql`—通过交互式终端访问 PostgreSQL

## 参考

以下是本章提及的数据库的参考资料：

- http://www.mysql.com—这是 MySQL 数据库服务器的官方网站。在这里您可以找到最新版本以及 MySQL 的最新信息和在线文档。您也可以在此处购买支持合同。如果您将在企业环境中使用 MySQL，可能需要考虑这一点。（许多公司不愿使用没有支持合同的软件。）
- http://www.postgresql.org—这是 PostgreSQL 数据库服务器的官方网站。您到达该网站时会被要求选择一个镜像。选择镜像后，您将被带到主站点。从那里，您可以找到有关 PostgreSQL 最新版本的信息并阅读在线文档。
- http://www.postgresql.org/docs/index.php?tutorial-start.html—这个交互式 HTML 文档树是开始学习如何使用 PostgreSQL 的绝佳场所。
- http://www.pgsql.com—这是一家提供 PostgreSQL 数据库付费支持合同的商业公司。

## 第 22 章

## LDAP

### 本章内容

- 配置服务器
- 配置客户端
- 管理
- 参考

轻量级目录访问协议（LDAP，发音为 ell-dap）是那些技术之一，虽然隐藏，但构成了企业计算核心基础设施的一部分。它的工作很简单：存储有关用户的信息。然而，它的强大之处在于它可以链接到数十种其他服务。LDAP 可以提供登录身份验证、公钥分发、电子邮件路由和地址验证，并且最近已成为推动单点登录技术发展的核心。

### 提示

大多数人将 LDAP 视为一种高度专业化的数据库服务器形式时，更容易理解其概念。在幕后，Ubuntu 使用数据库来存储所有 LDAP 信息；然而，LDAP 并没有提供像 SQL 那样简单直接的数据操作方式！

OpenLDAP 使用 Sleepycat Software 的 Berkeley DB（BDB），坚持使用该默认值是强烈推荐的。话虽如此，如果您有特定需求，也有替代方案。

本章介绍的是一个相对基础的 LDAP 服务器安装，包括如何托管一个包含员工姓名和电子邮件地址的公司范围目录服务。LDAP 是一个客户端/服务器系统，这意味着 LDAP 服务器托管数据，而 LDAP 客户端查询它。Ubuntu 将 OpenLDAP 作为其 LDAP 服务器提供，同时还提供多个 LDAP 启用的电子邮件客户端，包括 Evolution 和 Mozilla Thunderbird。我们在本章中涵盖了这三种应用程序。

由于 LDAP 数据通常可通过互联网访问——或至少是本地网络——因此确保服务器安全至关重要。本章提供了有关 OpenLDAP 密码配置的具体说明，我们建议您严格遵循我们的说明。

## 配置服务器

如果您使用 LDAP 已有多年，您会意识到其巨大的功能和灵活性。另一方面，如果您只是第一次尝试 LDAP，它看起来会像您能想象到的最糟糕的组件。LDAP 有特定的配置要求，图形工具极度缺乏，并且有大量需要记住的缩写。好消息是，您投入的所有辛苦工作都是值得的，因为一旦它正常工作，LDAP 将极大地改善您的网络体验。

配置 LDAP 服务器的第一步是安装客户端和服务器应用程序。启动 Synaptic 并安装 `slapd` 和 `ldap-utils` 包。系统会要求您为 `slapd` 输入管理员密码。

现在，使用 sudo 在您选择的文本编辑器中编辑 `/etc/ldap/slapd.conf`。这是 `slapd`，即 OpenLDAP 服务器守护进程的主要配置文件。向下滚动直到看到 `database`、`suffix` 和 `rootdn` 行。

这是 LDAP 系统最基本的配置。您的服务器名称是什么？`dc` 代表域名组件，即存储在 DNS 中的域名称——例如 example.com。对于我们的示例，我们使用了 hudzilla.org。LDAP 将域名的每个部分（以句点分隔）视为一个域名组件，因此域名 hudzilla.org 由域名组件 hudzilla 和域名组件 org 组成。

将 suffix 行更改为与您的域名组件匹配，以逗号分隔。例如：

```
suffix "dc=hudzilla,dc=org"
```

下一行定义根 DN，即另一个 LDAP 缩写，意为可区别名称。DN 是您目录中某人的完整描述：她的姓名以及她所在的域。例如

```
rootdn "cn=root,dc=hudzilla,dc=org"
```

CN 是另一个 LDAP 缩写，这次意为通用名称。通用名称就是其字面意思——一个人通常被称呼的名字。有些人有几个通用名称。Andrew Hudson 是一个通用名称，但同一用户也可能有通用名称 Andy Hudson。在我们的 `rootdn` 行中，我们定义了一个完整用户：通用名称为 root，位于域 hudzilla.org。这些行本质上是反向读取的。LDAP 首先访问 org，搜索 org 中的 hudzilla，然后在 hudzilla 中搜索 root。

