
设置 OpenLDAP 服务器所需的所有软件包都包含在 Fedora 中。作为替代方案，您可以轻松地使用 `yum` 通过互联网安装这些软件包。安装这些软件包后，您可以开始配置 OpenLDAP 服务器。

## 安装 OpenLDAP 软件包

要配置 OpenLDAP 服务器，请首先从 Fedora 安装所有 `openldap` 软件包。首先，检查安装了哪些 `openldap` 软件包：

```bash
# rpm -qa "openldap*"
```

只有在开发 LDAP 应用程序时才需要 `openldap-devel` 软件包。否则，您可以从随本书提供的 DVD 或通过网络输入以下命令安装 `openldap`、`openldap-clients` 和 `openldap-servers` 软件包：

```bash
# yum install openldap openldap-clients openldap-servers
```

## 配置 OpenLDAP 服务器 (slapd.conf)

您在配置文件 `/etc/openldap/slapd.conf` 中配置 OpenLDAP 数据库的访问和使用。作为替代方案，您也可以将您的 `slapd.conf` 添加到 `/etc/openldap/slapd.d` 目录中的信息数据库。此过程使用旧版的 `slapd.conf` 方法。

> 注意：有关在 `slapd.conf` 文件中可以使用的功能的更完整描述，请参阅 `slapd.conf` 手册页。

1. **删除 slapd.d 目录。** 如果您愿意，可以将 `slapd.conf` 文件转换为存储在 `/etc/openldap/slapd.d` 目录中（有关将该文件转换为较新格式的信息，请参阅 `slaptest` 手册页）。要使用旧式的 `slapd.conf` 文件，请删除 `slapd.d` 目录，方法如下：

```bash
# rm -rf /etc/openldap/slapd.d
```

2. **编辑 slapd.conf。** 备份 `/etc/openldap/slapd.conf` 文件，然后使用任何文本编辑器以 root 用户身份打开该文件。以下步骤告诉您一些您可能想要更改的信息。

3. **审查模式。** 在 `slapd.conf` 文件中，通常用于创建 LDAP 目录的模式是从 `/etc/openldap/schema` 目录包含的。您可能使用的其他模式通常依赖于包含这些模式。因此，除非您确定不需要它们，否则不要删除这些模式中的任何一个：

```text
include /etc/openldap/schema/corba.schema
include /etc/openldap/schema/core.schema
include /etc/openldap/schema/cosine.schema
include /etc/openldap/schema/duconf.schema
include /etc/openldap/schema/dyngroup.schema
include /etc/openldap/schema/inetorgperson.schema
include /etc/openldap/schema/java.schema
include /etc/openldap/schema/misc.schema
include /etc/openldap/schema/nis.schema
include /etc/openldap/schema/openssl.schema
include /etc/openldap/schema/policy.schema
include /etc/openldap/schema/collective.schema
```

由于模式是纯文本文件，您可以使用任何文本编辑器打开它们。模式的几个部分对我们感兴趣。`corba.schema` 文件是所有 LDAP 目录必需的。`cosine.schema` 和 `inetorgperson.schema` 文件特别有用（且此过程需要）。`nis.schema` 文件用于在 LDAP 目录中提供网络信息服务 (NIS) 数据。

### 理解 OID

如果你查看模式文件（`/etc/openldap/schema/*`），你会发现每个 LDAP 对象类和属性都映射为一个点分隔的数字。这个分层字符串被称为对象标识符（OID）。

由于 LDAP 旨在作为一个全局目录（所有条目均可唯一），如果你希望创建一个可全局访问的目录，在可能的情况下，应尽可能使用已分配有现有 OID 的项目。然而，如果你发现需要创建尚未定义的对象类或属性，请考虑为你的组织申请一个对象标识符（OID）。另一种选择是自行编造属性名称和 OID，在这种情况下，你不应该期望该数据能在全局范围内被访问，或者尽量避免与现有 OID 发生冲突。

就像域名一样，OID 分配允许你在需要时在该 OID 下创建分支。如果你的组织已被分配了专用 OID，那么可以保证你在此编号下创建的每个项目都是全局唯一的（前提是你自己妥善维护这些分配）。

私有企业号是作为 OID 存储的有用信息的一个例子。主要用于使用 SNMP 的公司私有企业号存储在 OID 编号 `1.3.6.1.4.1` 之下。在该 OID 下代表的公司包括 IBM（`1.3.6.1.4.1.2`）、思科系统（`1.3.6.1.4.1.9`）和惠普（`1.3.6.1.4.1.11`）。对于红帽软件（Red Hat Software）和 Fedora 项目，其 OID 编号分别为 `1.3.6.1.4.1.2312` 和 `1.3.6.1.4.1.30401`。

如果你将每个数字分解为其组成部分，你会发现它们以顶层 OID `1`（用于 ISO 分配的 OID）开始，然后是 `3`（ISO 标识的组织），接着是 `6`（美国国防部），然后是 `1`（互联网），接着是 `4`（私有），最后是 `1`（企业）。之后就是代表每家公司的数字。

你可以在 <http://www.iana.org/assignments/enterprise-numbers> 上的私有企业号列表中查看完整的企业号列表。在 <http://www.alvestrand.no/objectid/top.html> 上搜索 OID 分配（从顶级节点开始）。你可以从互联网号码分配机构（<http://www.iana.org/cgi-bin/mediatypes.pl>）申请你的 OID。

`misc.schema` 文件包含一些杂项邮件相关的模式定义。

> **提示：** LDAP 模式查看器允许你查看常见 LDAP 模式中的对象类、属性、语法和匹配规则。这些定义也指向了更全面地定义每个对象类的 RFC（<http://www.andrew.cmu.edu/user/dd26/ldap.akb@home.com/index.html>）。

## 4. 添加后端数据库定义

在 `slapd.conf` 文件中，你需要定义一些后端数据库定义。每组后端定义适用于一组相同类型的数据库。

以下是后端数据库定义在一个名为 `linuxtoys.net` 的域中的计算机上出现的示例（当然，你需要将 `linuxtoys` 和 `net` 替换为你自己域中的相应信息）：

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

该数据库的类型为 `bdb`（Berkeley DB 事务后端），它定义了此目录的数据存储方式。`ldbm`（轻量级目录访问协议代理后端）数据库是你可以使用的另一种类型。后缀指定对 `linuxtoys.net` 的此 `slapd` 服务器的查询应指向此数据库。`directory` 行将 `/var/lib/ldap` 目录标识为此 LDAP 目录的位置。

> **注意：** 有关数据库后端的更多信息，请访问 http://www.openldap.org/data/cache/893.html 上的 OpenLDAP.org 网站。
