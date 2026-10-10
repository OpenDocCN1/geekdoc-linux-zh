
私有企业编号是作为 OID 存储的有用信息的示例。主要用于使用 SNMP 的公司的私有企业编号存储在 OID 编号 `1.3.6.1.4.1` 下。在该 OID 下表示的公司包括 IBM (`1.3.6.1.4.1.2`)、`Cisco Systems` (`1.3.6.1.4.1.9`) 和 Hewlett Packard (`1.3.6.1.4.1.11`)。

如果你将每个数字分解为其组成部分，你会看到它们以顶级 OID `1`（用于 ISO 分配的 OID）开头，然后是 `3`（ISO 识别的组织），然后是 `6`（美国国防部），然后是 `1`（互联网），然后是 `4`（私有），然后是 `1`（企业）。之后是代表每家公司的编号。

你可以在 `www.iana.org/assignments/enterprise-numbers` 的私有企业编号列表中查看完整的企业编号列表。在 `www.alevistrand.no/objectid/top.html` 搜索 OID 分配（从顶级节点开始）。你可以从互联网编号分配机构 (`www.iana.org/cgi-bin/enterprise.pl`) 请求你的 OID。

## 构建你的 LDAP 目录

虽然标准文档用于保持 LDAP 目录中的对象类、属性和其他元素唯一，但你可以自由地将这些元素组合到你自己的 LDAP 目录中，方式由你决定。你用于创建目录的结构是 LDAP 数据交换格式 (`LDIF`)。

你存储在 LDAP 目录中的每部分信息都必须位于基础可分辨名称（或*基础 dn*）之下。因为如今许多组织可以表示

通过唯一的互联网域名，域名是识别您的 LDAP 基础 DN 的流行方式。实际上，在本章的示例中，我使用的基础可识别名称是 `linuxtoss.net`。如果您正在为一个可以用域名表示的组织创建 LDAP 目录，您可以将 `linuxtoss.net` 替换为您的域名。

如果您正在为较大的组织创建 LDAP 目录结构（换句话说，不仅仅是像我在这里做的那样只创建一个地址簿），您需要仔细考虑希望目录如何组织。对于跨国公司，您可能希望在基础可识别名称下添加国家代码（`us`、`de`、`it` 等）。

## 设置 OpenLDAP 服务器

设置 OpenLDAP 服务器所需的所有软件包都包含在随 Fedora 和 RHEL 发行版提供的 DVD 中。或者，您可以轻松地通过 Internet 使用 `yum` 安装这些软件包。安装这些软件包后，您就可以开始配置 OpenLDAP 服务器了。

### 安装 OpenLDAP 软件包

要配置 OpenLDAP 服务器，首先应该从 Fedora 或 RHEL 发行版安装所有 `openldap` 软件包。首先，检查已安装了哪些 `openldap` 软件包：

```bash
# rpm -qa "openldap*"
openldap-2.3.27-4
openldap-servers-2.3.27-4
openldap-devel-2.3.27-4
openldap-clients-2.3.27-4
```

只有在开发 LDAP 应用程序时才需要 `openldap-devel` 软件包。否则，您可以从随本书提供的 DVD 上安装 `openldap`、`openldap-clients` 和 `openldap-servers` 软件包。

### 配置 OpenLDAP 服务器 (`slapd.conf`)

您可以在配置文件 `/etc/openldap/slapd.conf` 中配置对 OpenLDAP 数据库的访问和使用。

> **注意：** 关于可以在 `slapd.conf` 文件中使用的功能的更完整说明，请参阅 `slapd.conf` 手册页。

- **1. 编辑 `slapd.conf`。** 创建 `/etc/openldap/slapd.conf` 的备份副本，然后使用任何文本编辑器以 root 用户身份打开该文件。以下步骤告诉您一些可能想要更改的信息。

- **2. 查看架构。** 在 `slapd.conf` 文件中，通常用于创建 LDAP 目录的架构是从 `/etc/openldap/schema` 目录中包含进来的。

您可能使用的其他架构通常依赖于包含这些架构。因此，除非您知道不需要它们，否则不要删除这些架构中的任何一个：

```text
include	/etc/openldap/schema/core.schema
include	/etc/openldap/schema/cosine.schema
include	/etc/openldap/schema/inetorgperson.schema
include	/etc/openldap/schema/nis.schema
include	/etc/openldap/schema/misc.schema
```

`core.schema` 文件是所有 LDAP 目录所必需的。`cosine.schema` 和 `inetorgperson.schema` 文件特别有用（并且此过程需要它们）。`nis.schema` 文件用于在 LDAP 目录中提供网络信息系统数据。`misc.schema` 文件包含一些杂项邮件相关架构定义。

> **提示：** LDAP 架构查看器 (`http://ldap.akbkhome.com`) 允许您查看常见 LDAP 架构的对象类、属性、语法和匹配规则。定义还指向更完整定义每个对象类的 RFC。

- **3. 添加后端数据库定义。** 在 `slapd.conf` 文件中，您需要定义一些后端数据库定义。每组后端定义适用于同一类型的数据库组。

以下是名为 `linuxtoys.net` 域名的计算机后端数据库定义出现示例（当然，您会将 `linuxtoys` 和 `net` 替换为您自己域名的相应部分）：

```text
############################################################
# ldbm and/or bdb database definitions
############################################################

database	bdb
suffix	"dc=linuxtoys,dc=net"
directory	"/var/lib/ldap"
rootdn	"cn=Manager,dc=linuxtoys,dc=net"
cachesize 10000
searchstack 8
dbnosync
dbdirread
```

此数据库类型为 `bdb`（Berkeley DB 事务后端），它定义了此目录的数据存储方式。`ldbm`（轻量级目录访问协议代理后端）数据库是您可以使用的另一种类型。`suffix` 指定发往此 `slapd` 服务器针对 `linuxtoys.net` 的查询将指向此数据库。`directory` 行标识 `/var/lib/ldap` 目录作为此 LDAP 目录的位置。

`rootdn` 行表示可以授予 root 访问权限以更改与 `linuxtoys.net` 可识别名称关联的数据库中的数据（前提是提供使用 `rootpw` 描述的密码）。我添加了最后四个选项以提高 `bdb` 数据库的性能（有关详细信息，请输入 `man slapd-bdb`）。

- **4. 添加密码。** 在 `slapd.conf` 文件中，您需要输入修改 OpenLDAP 后端数据库所需的密码。默认情况下，`rootpw` 行定义了作为您密码的明文字符串。密码将赋予您完全控制后端数据库的权限。它看起来像以下内容：

```text
rootpw    mysecret
```

> **注意：** 如果您打算使用明文密码，应确保 `slapd.conf` 文件的读取权限对世界关闭（`chmod 640 /etc/openldap/slapd.conf`）。有关创建加密密码以访问 OpenLDAP 后端数据库的信息，请参阅侧边栏“创建加密密码”。

#### 创建加密密码

要为 OpenLDAP 数据库的管理员创建加密密码，您可以使用 `slappasswd` 命令。您可以使用 Crypt、SSHA、SMD5、MD5 或 SSH 加密创建密码。以下是使用 MD5 加密为 OpenLDAP 创建密码的示例：

```bash
# slappasswd -h {md5} > /tmp/myslap
New password:  ******
Re-enter new password:  ******
# cat /tmp/myslap
{MD5}uBoM+LCQg5GHJ2Z4NLu9A==
```

输入密码（两次）以创建加密的 MD5 密码。此示例将加密密码定向到 `/tmp/myslap` 文件；您稍后可以将其读取到 `slapd.conf` 文件中。在此示例中，我让您 `cat` 文件，以便您可以看到加密密码的样子。您的密码将不同。使用加密而非明文密码时，`rootpw` 行看起来像这样：

```text
rootpw    {MD5}uBoM+LCQg5GHJ2Z4NLu9A==
```

- **5. 保存 `slapd.conf`。** 保存对 `slapd.conf` 文件的更改并关闭它。
