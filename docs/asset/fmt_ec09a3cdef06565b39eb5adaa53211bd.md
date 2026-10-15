
- `mysqldump`—转储或备份 MySQL 数据或表
- `pgaccess`—访问 PostgreSQL 数据库服务器
- `pg_ctl`—控制 PostgreSQL 服务器或查询其状态
- `psql`—通过交互式终端访问 PostgreSQL

### 参考

以下是本章提及的数据库的参考资料：
- http://www.mysql.com—这是 MySQL 数据库服务器的官方网站。在这里您可以找到最新版本以及 MySQL 的最新信息和在线文档。您也可以在此处购买支持合同。如果您将在企业环境中使用 MySQL，可能需要考虑这一点。（许多公司不愿使用没有支持合同的软件。）
- http://www.postgresql.org—这是 PostgreSQL 数据库服务器的官方网站。您到达该网站时会被要求选择一个镜像。选择镜像后，您将被带到主站点。从那里，您可以找到有关 PostgreSQL 最新版本的信息并阅读在线文档。
- http://www.postgresql.org/docs/index.php?tutorial-start.html—这个交互式 HTML 文档树是开始学习如何使用 PostgreSQL 的绝佳场所。
- http://www.pgsql.com—这是一家提供 PostgreSQL 数据库付费支持合同的商业公司。

# 第 22 章 LDAP

### 本章内容
- 配置服务器
- 配置客户端
- 管理
- 参考

轻量级目录访问协议（LDAP，发音为 ell-dap）是那些技术之一，虽然隐藏，但构成了企业计算核心基础设施的一部分。它的工作很简单：存储有关用户的信息。然而，它的强大之处在于它可以链接到数十种其他服务。LDAP 可以提供登录身份验证、公钥分发、电子邮件路由和地址验证，并且最近已成为推动单点登录技术发展的核心。

#### 提示
大多数人将 LDAP 视为一种高度专业化的数据库服务器形式时，更容易理解其概念。在幕后，Ubuntu 使用数据库来存储所有 LDAP 信息；然而，LDAP 并没有提供像 SQL 那样简单直接的数据操作方式！

OpenLDAP 使用 Sleepycat Software 的 Berkeley DB（BDB），坚持使用该默认值是强烈推荐的。话虽如此，如果您有特定需求，也有替代方案。

本章介绍的是一个相对基础的 LDAP 服务器安装，包括如何托管一个包含员工姓名和电子邮件地址的公司范围目录服务。LDAP 是一个客户端/服务器系统，这意味着 LDAP 服务器托管数据，而 LDAP 客户端查询它。Ubuntu 将 OpenLDAP 作为其 LDAP 服务器提供，同时还提供多个 LDAP 启用的电子邮件客户端，包括 Evolution 和 Mozilla Thunderbird。我们在本章中涵盖了这三种应用程序。

由于 LDAP 数据通常可通过互联网访问——或至少是本地网络——因此确保服务器安全至关重要。本章提供了有关 OpenLDAP 密码配置的具体说明，我们建议您严格遵循我们的说明。

## 配置服务器

如果您使用 LDAP 已有多年，您会意识到其巨大的功能和灵活性。另一方面，如果您只是第一次尝试 LDAP，它看起来会像您能想象到的最糟糕的组件。LDAP 有特定的配置要求，图形工具极度缺乏，并且有大量需要记住的缩写。好消息是，您投入的所有辛苦工作都是值得的，因为一旦它正常工作，LDAP 将极大地改善您的网络体验。

配置 LDAP 服务器的第一步是安装客户端和服务器应用程序。启动 Synaptic 并安装 `slapd` 和 `ldap-utils` 包。系统会要求您为 `slapd` 输入管理员密码。

现在，使用 `sudo` 在您选择的文本编辑器中编辑 `/etc/ldap/slapd.conf`。这是 `slapd`，即 OpenLDAP 服务器守护进程的主要配置文件。向下滚动直到看到 `database`、`suffix` 和 `rootdn` 行。

这是 LDAP 系统最基本的配置。您的服务器名称是什么？`dc` 代表域名组件，即存储在 DNS 中的域名称——例如 example.com。对于我们的示例，我们使用了 hudzilla.org。LDAP 将域名的每个部分（以句点分隔）视为一个域名组件，因此域名 hudzilla.org 由域名组件 hudzilla 和域名组件 org 组成。

将 `suffix` 行更改为与您的域名组件匹配，以逗号分隔。例如：

```
suffix "dc=hudzilla,dc=org"
```

下一行定义根 DN，即另一个 LDAP 缩写，意为可区别名称。DN 是您目录中某人的完整描述：她的姓名以及她所在的域。例如

```
rootdn "cn=root,dc=hudzilla,dc=org"
```

`CN` 是另一个 LDAP 缩写，这次意为通用名称。通用名称就是其字面意思——一个人通常被称呼的名字。有些人有几个通用名称。Andrew Hudson 是一个通用名称，但同一用户也可能有通用名称 Andy Hudson。在我们的 `rootdn` 行中，我们定义了一个完整用户：通用名称为 root，位于域 hudzilla.org。这些行本质上是反向读取的。LDAP 首先访问 org，搜索 org 中的 hudzilla，然后在 hudzilla 中搜索 root。

`rootdn` 很重要，因为它不仅仅是目录中的另一个用户。LDAP root 用户就像 Linux 中的 root 用户一样。它是拥有对系统完全控制权的人，可以随意进行任何更改。

接下来是一个稍微复杂一点的部分：我们需要为 LDAP root 用户设置密码。最简单的方法是打开一个新终端窗口，与现有的终端并行使用。在新终端中切换到 root，然后输入 `slappasswd`。该工具使用 SHA1 哈希算法为 OpenLDAP 生成密码哈希。提示时输入一个密码。输入并确认密码后，你应该会看到类似这样的输出：

```
{SSHA}qMVxFT2K1UUmrA89Gd7z6EK3gRLD1o2W
```

这就是从你的密码生成的密码哈希。你的与此处显示的不同，但重要的是它以 `{SSHA}` 开头，表示使用 SHA1。现在你需要切换回另一个终端（正在编辑 `slapd.conf` 的那个），并在 `rootdn` 行下方添加这一行：

```
rootpw <your password hash>
```

你应该用 `slappasswd` 的完整输出替换 `<your password hash>`，如下所示：

```
rootpw {SSHA}qMVxFT2K1UUmrA89Gd7z6EK3gRLD1o2W
```

这样就将 LDAP root 密码设置为刚刚用 `slappasswd` 生成的密码。这是你在 `slapd.conf` 文件中需要做的最后一次更改，因此保存更改并关闭编辑器。

回到终端，运行 `slaptest` 命令。这会检查你的 `slapd.conf` 文件是否存在错误，并确保你正确编辑了它。假设没有错误，运行 `/etc/init.d/slapd` 以启动 OpenLDAP。

Ubuntu 在每次启动时都会自动启动 OpenLDAP，但该命令会立即启动它。

最后的配置步骤是告诉 Ubuntu 如果未指定则应使用哪个 DN。你可以通过进入系统设置并选择身份验证来完成此操作。在出现的对话框中，在“用户信息”选项卡和“身份验证”选项卡中均勾选启用 LDAP 支持。接下来，单击配置 LDAP 按钮，输入你的 DC（例如，`dc=hudzilla,dc=org`）作为 LDAP 搜索基本 DN，并输入 `127.0.0.1` 作为 LDAP 服务器。单击确定，然后再次单击确定。

#### TIP
勾选启用 LDAP 支持并不会真正改变你的用户登录方式。在幕后，这会强制 Ubuntu 在 `/etc/ldap` 中设置 `ldap.conf` 文件，以便未指定基本搜索起始点的 LDAP 搜索被定向到你的 DC。

## 填充你的目录

LDAP 安装、配置并运行后，你现在可以开始填充目录中的人员。这涉及更多 LDAP 缩写，绝非易事，因此如果你需要多次重读才能理解，请不要担心。

首先，创建文件 `base.ldif`。你将使用它来定义系统的基本组件：域和地址簿。LDIF 是 LDAP 数据交换格式的缩写，它是记录用户数据以插入 LDAP 目录的标准方式。以下是我们示例中使用的内容：

```
dn: dc=hudzilla,dc=org
objectClass: top
objectClass: dcObject
objectClass: organization
dc: hudzilla
o: Hudzilla Dot Org

dn: ou=People,dc=hudzilla,dc=org
ou: People
objectClass: top
objectClass: organizationalUnit
```

该文件包含两个独立的实体，由空行分隔。第一个是我们的组织 hudzilla.org。`dn` 行你已经知道了，因为它们在目录范围内唯一定义每个对象。`objectClass` 指令指定允许此实体使用哪些属性以及需要哪些属性。在本例中，我们用它将 DC 设置为 hudzilla，并将 o（组织名称）设置为 Hudzilla Dot Org。
