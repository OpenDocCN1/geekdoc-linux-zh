

# 理解 OID

如果你查看模式文件（`/etc/openldap/schema/*`），你会发现每个 LDAP 对象类和属性都映射为一个点分隔的数字。这个分层字符串被称为对象标识符（OID）。

由于 LDAP 旨在作为一个全局目录（所有条目均可唯一），如果你希望创建一个可全局访问的目录，在可能的情况下，应尽可能使用已分配有现有 OID 的项目。然而，如果你发现需要创建尚未定义的对象类或属性，请考虑为你的组织申请一个对象标识符（OID）。另一种选择是自行编造属性名称和 OID，在这种情况下，你不应该期望该数据能在全局范围内被访问，或者尽量避免与现有 OID 发生冲突。

就像域名一样，OID 分配允许你在需要时在该 OID 下创建分支。如果你的组织已被分配了专用 OID，那么可以保证你在此编号下创建的每个项目都是全局唯一的（前提是你自己妥善维护这些分配）。

私有企业号是作为 OID 存储的有用信息的一个例子。主要用于使用 SNMP 的公司私有企业号存储在 OID 编号 1.3.6.1.4.1 之下。在该 OID 下代表的公司包括 IBM（1.3.6.1.4.1.2）、思科系统（1.3.6.1.4.1.9）和惠普（1.3.6.1.4.1.11）。对于红帽软件（Red Hat Software）和 Fedora 项目，其 OID 编号分别为 1.3.6.1.4.1.2312 和 1.3.6.1.4.1.30401。

如果你将每个数字分解为其组成部分，你会发现它们以顶层 OID 1（用于 ISO 分配的 OID）开始，然后是 3（ISO 标识的组织），接着是 6（美国国防部），然后是 1（互联网），接着是 4（私有），最后是 1（企业）。之后就是代表每家公司的数字。

你可以在 <http://www.iana.org/assignments/enterprise-numbers> 上的私有企业号列表中查看完整的企业号列表。在 <http://www.alvestrand.no/objectid/top.html> 上搜索 OID 分配（从顶级节点开始）。你可以从互联网号码分配机构（<http://www.iana.org/cgi-bin/mediatypes.pl>）申请你的 OID。

misc.schema 文件包含一些杂项邮件相关的模式定义。

> **提示：** LDAP 模式查看器允许你查看常见 LDAP 模式中的对象类、属性、语法和匹配规则。这些定义也指向了更全面地定义每个对象类的 RFC（<http://www.andrew.cmu.edu/user/dd26/ldap.akb@home.com/index.html>）。

### 4. 添加后端数据库定义

在 `slapd.conf` 文件中，你需要定义一些后端数据库定义。每组后端定义适用于一组相同类型的数据库。

以下是后端数据库定义在一个名为 linuxtoys.net 的域中的计算机上出现的示例（当然，你需要将 linuxtoys 和 net 替换为你自己域中的相应信息）：

```
##################################################################
# ldbm and/or bdb database definitions
##################################################################
database              bdb
suffix                "dc=linuxtoys,dc=net"
directory             /var/lib/ldap
rootdn                "cn=Manager,dc=linuxtoys,dc=net"
cachesize             10000
searchstack           8
dbmsync
dbdirsync
```

该数据库的类型为 bdb（Berkeley DB 事务后端），它定义了此目录的数据存储方式。ldbm（轻量级目录访问协议代理后端）数据库是你可以使用的另一种类型。后缀指定对 linuxtoys.net 的此 slapd 服务器的查询应指向此数据库。directory 行将 /var/lib/ldap 目录标识为此 LDAP 目录的位置。

> **注意：** 有关数据库后端的更多信息，请访问 http://www.openldap.org/data/cache/893.html 上的 OpenLDAP.org 网站。

rootdn 行表明，可以授予 root 权限以修改与 linuxtoys.net 可区分子目录名称（distinguished name）关联的数据库中的数据（前提是在下一步中描述的那样，使用 rootpw 提供密码）。我添加了最后四个选项以提高 bdb 数据库的性能（有关详细信息，请查看 man slapd-bdb）。

### 5. 添加密码

在 `slapd.conf` 文件中，你需要输入修改 OpenLDAP 后端数据库所需的密码。默认情况下，rootpw 行定义了一个明文字符串作为你的密码。该密码将赋予你对后端数据库的完全控制权。其外观可能如下所示：

```
rootpw        mysecret
```

> **注意：** 如果你打算使用明文密码，请确保你的 `slapd.conf` 文件对全局用户的读取权限已关闭（chmod 640 /etc/openldap/slapd.conf）。有关创建用于访问 OpenLDAP 后端数据库的加密密码的信息，请参阅侧栏“创建加密密码”。

### 6. 保存 slapd.conf

保存你对 `slapd.conf` 文件的更改并关闭它。

### 7. 检查 slapd.conf

通过运行 slappasswd 命令来检查 `slapd.conf` 文件中的语法错误，方法如下：

```
# slappasswd -u
config file testing succeeded
```

如果文件语法有误（例如，如果省略了引号或逗号位置错误），消息将显示为 `slappasswd: bad configuration file`。尝试修正问题并再次检查文件。稍后，当数据库创建完成后，你可以再次运行 slappasswd（不带 -u 选项），以确保 `slapd.conf` 指向存在且配置正确的数据库。

此时，你可以尝试启动 OpenLDAP 服务。

### 创建加密密码

要为 OpenLDAP 数据库的管理员创建加密密码，请使用 slappasswd 命令。你可以使用 Crypt、SSHA、SMD5、MD5 或 SHA 加密来创建密码。以下是使用 MD5 加密为 OpenLDAP 创建密码的示例：

```
# slappasswd -h {md5} > /tmp/myslap
New password: ********
Re-enter new password: ********
# cat /tmp/myslap
{MD5}uBoM+LOQg5GHJj2Z4NLu9a==
```

输入密码（两次）以创建加密的 MD5 密码。此示例将加密密码重定向到 /tmp/myslap 文件；你可以稍后将其读取到 `slapd.conf` 文件中。在此示例中，我让你 cat 该文件，以便你可以查看加密密码的外观。你的密码将有所不同。使用加密密码而非明文密码时，rootpw 行的外观如下：

```
rootpw {MD5}uBoM+LOQg5GHJj2Z4NLu9a==
```

### 启动 OpenLDAP 服务

像在 Fedora 中启动大多数服务一样，使用 `service` 和 `chkconfig` 命令启动 OpenLDAP 服务。OpenLDAP 的服务名称为 `slapd`。若要立即启动服务，请输入以下内容：

```
# service slapd start
Starting slapd: [ OK ]
```

若要设置 `slapd` 服务在每次系统重启时自动启动，请输入以下内容：

```
# chkconfig slapd on
```

默认情况下，`slapd` 服务对所有人开放读取权限。

### 设置地址簿

在设置地址簿数据库结构时，我基于组织名称（在本示例中为 linuxtoys）来确定数据库的可区分子目录名称（dn）。

在 `slapd.conf` 文件中将后缀设置为 linuxtoys net（suffix "dc=linuxtoys,dc=net"）（你的设置可能不同），后端数据库被设置为处理对 linuxtoys net 的可区分子目录名称（dn）的查询。接下来，你可以在此可区分子目录名称下为该组织创建地址簿结构。

> **注意：** `dc=` 代表域组件（Domain Component）。当你将域名包含在你的可区分子目录名称中时，放置该域名各部分的顺序应将最接近 DNS 根的部分放在最后。在此示例中，`dc=linuxtoys` 位于 `dc=net` 之前。如果你对将域名包含在 LDAP 目录中的规范感兴趣，请参阅 RFC 2247。

你需要以一种可以加载到 OpenLDAP 数据库中的格式创建地址簿文件。所需的格式称为 LDAP 数据交换格式（LDIF）。以此格式输入的信息可用于构建数据库，并一次性从文件向目录中加载大量数据。

以下步骤说明了如何创建一个包含 linuxtoys.net LDAP 目录（可区分子目录名称）地址簿定义的 LDIF 文件，并将该文件加载到你的 LDAP 服务器中。

- **1. 创建 ldif 文件。** 作为 root 用户，使用任意文本编辑器创建一个用于保存 LDAP 目录条目的文件。在我的示例中，我使用了 /etc/openldap/toypeople.ldif 文件。

> **注意：** 创建 ldif 文件时，务必在每个新的可区分子目录名称（dn:）行之前保留一个空白行。空白行告诉 ldapadd 开始一个新条目。如果没有空白行，LDAP 将不知道你要开始一个新的可区分子目录名称。此外，删除每行前的所有空格，确保所有新行都从第 1 列开始。（行首的空格表示新行实际上是前一行的一部分。）

- **2. 定义组织。** 你需要定义要加载到 LDAP 服务器中的目录。在我的示例中，我添加了将组织定义为 Linux Toys 的信息，位于可区分子目录名称 linuxtoys net（dc=linuxtoys,dc=net）之下，方法是将以下信息添加到我的 toypeople.ldif 文件中。

```
dn:                      dc=linuxtoys,dc=net
objectClass:              dcObject
objectClass:              organization
dc:                      linuxtoys
o:                      Linux Toys
```

