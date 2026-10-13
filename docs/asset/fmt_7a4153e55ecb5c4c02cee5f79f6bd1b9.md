
<id>

dn:<distinguished name>

<attrype>:<attrvalue>

<attrype>:<attrvalue>

<attrype>:<attrvalue>

```
```

每个条目可以根据需要包含任意数量 `<attrype>:<attrvalue>` 对。空行表示条目的结束。

> 注意 所有的 `<attrype>` 和 `<attrvalue>` 对都必须在相应的架构文件中定义，才能使用这些信息。

任何包含在 `""` 和 `""` 之间的值都是变量，可以在创建新的 LDAP 条目时设置。然而，此规则不适用于 `<id>`。`<id>` 是由你使用的应用程序确定的数字。

## 第 13 章 轻量级目录访问协议 (LDAP) 187

### 13.3. OpenLDAP 守护进程与工具

Open LDAP 库和工具套分布在以下软件包中：

- `openldap` — 包含运行 OpenLDAP 服务器和客户端应用程序所需的库。
- `openldap-clients` — 包含用于查看和修改 LDAP 服务器上目录的命令行工具。
- `openldap-servers` — 包含配置和运行 LDAP 服务器所需的服务器和其他工具。

为了执行管理任务，`openldap-servers` 软件包会将以下工具安装到：

- `slapadd` — 将 LDIF 文件中的条目添加到 LDAP 目录。例如，命令 `/usr/sbin/slapadd -l ldif-output` 会写入一个名为 `ldif-output` 的 LDIF 文件，其中包含新的条目。
- `slapcat` — 以默认格式（Berkeley）从 LDAP 目录中提取条目，并将其保存到 LDIF 文件中。例如，命令 `/usr/sbin/slapcat -l ldif-output` 将输出一个名为 `ldif-output` 的 LDIF 文件，其中包含 LDAP 目录中的条目。
- `slapindex` — 根据当前内容重新索引 `slapd` 目录。
- `slappasswd` — 生成加密的用户密码值，用于 `ldapmodify` 或修改 `slapd` 配置文件 `/etc/openldap/ldap.conf` 中的根密码。执行 `/usr/sbin/slpasswd` 命令创建密码。

**警告**
在使用 `slapadd`、`slapcat` 或 `slapindex` 之前，务必通过执行 `/usr/sbin/service slapd stop` 停止 `slapd`。否则，LDAP 目录的完整性可能会受到威胁。

有关如何使用这些工具工具，请参考各自的手手册（man pages）。

`openldap-clients` 软件包将工具安装到 `/usr/bin/`，用于添加、修改和删除 LDAP 目录中的条目。这些工具包括：

- `ldapmodify` — 修改 LDAP 目录中的条目，接受通过文件或标准输入的输入；`ldapadd` — 通过接受文件或标准输入的输入向目录添加条目；`ldapadd` 实际上是 `ldapmodify -a` 的软链接。
- `ldapsearch` — 使用 shell 提示符搜索 LDAP 目录中的条目。
- `ldapdelete` — 通过终端的用户输入或文件输入，从 LDAP 目录中删除条目。

除 `ldapsearch` 外，这些工具中的每一个工具最常用的方式都是引用包含要进行更改的文件，而不是为 LDAP 目录中想要更改的每个条目手动输入命令。此类文件的格式在每个应用程序的手手册中有概述。

## 第 13 章 轻量级目录访问协议 (LDAP)

### 13.3.1. NSS、PAM 和 LDAP

除了 OpenLDAP 软件包外，Red Linux 包含包含一个名为 `nss_ldap` 的软件包，它增强了 LDAP 集成到 Linux 和 UNIX 环境的能力。

`nss_ldap` 软件包提供了以下模块：

- `/lib/libnss_ldap-<glibc-version>.so`
- `/lib/security/pam_ldap.so`

`libnss_ldap-<glibc-version>.so` 模块允许应用程序通过 glibc 的名称服务切换 (SSS) 接口在 LDAP 目录中查找用户、组、主机和其他信息。NSS 允许应用程序结合网络信息服务 (NIS) 名称服务和认证文件使用 LDAP 进行身份验证。

`pam_ldap` 模块允许 PAM 感知应用程序使用存储在 LDAP 目录中的信息来验证用户。PAM 感知应用程序包括控制台登录、POP 和 IMAP 邮件服务器以及 Samba。通过在网络上部署 LDAP 服务器，所有这些应用程序都可以使用相同的用户 ID 和密码组合进行身份验证，极大简化了管理工作。

### 13.3.2. PHP4、Apache HTTP 服务器与 LDAP

Red Linux 包含一个包含 PHP 服务器端脚本语言的 LDAP 模块的软件包。

`php-ldap` 软件包通过 `/usr/lib/php4/ldap.so` 模块为 PHP4 HTML 嵌入脚本语言添加 LDAP 支持。该模块允许 PHP4 脚本访问存储在 LDAP 目录中的信息。

![](img/31025704b51d5760c0228ff0f3db98bf_203_0.png)

> Red Linux 不再附带 `auth_ldap` 软件包。该软件包为版本 1.3 及更早的 Apache HTTP 服务器提供了 LDAP 支持。请访问 Apache 软件基金网站 http://www.apache.org/ 了解该模块状态详情。

### 13.3.3. LDAP 客户端应用程序

存在支持创建和修改目录的图形 LDAP 客户端，但它们没有随 Red Linux 发行。其中一个应用程序是 LDAP Browser/Editor —— 这是一个基于 Java 的工具，可在 http://www.iet.edu/~gawojar/ldap 获取。

其他 LDAP 客户端以只读方式访问目录，用于检索而非更改组织范围的信息。此类应用程序的示例包括基于 Mozilla 的 Web 浏览器、Sendmail、Balsa、Paine、Evolution 和 Gnome Meeting。

### 13.4. OpenLDAP 配置文件

OpenLDAP 配置文件安装在 `/etc/openldap/` 目录下。以下是突出的重要目录和文件简列表：

- `/etc/openldap/ldap.conf` — 这是所有使用 OpenLDAP 库（如 ldsearch、ldapsd、Sendmail、Pine、Balsa、Evolution 和 Gnome Meeting）的客户端应用程序的配置文件。
- `/etc/openldap/slapd.conf` — 这是 `slapd` 守护进程的配置文件。有关关于此文件的更多信息，请参见第 13.6 节“编辑 /etc/openldap/slapd.conf”。
- `/etc/openldap/schema/` — 此子目录包含 `slapd` 守护进程使用的架构（schema）。有关此目录的更多信息，请参见第 13.5 节“/etc/openldap/schema/ 目录”。

> 注意
> 如果安装了 `nss_ldap` 软件包，它将创建一个名为 `/etc/ldap.conf` 的文件。该文件由 `nss_ldap` 软件包提供的 PAM 和 NSS 模块使用。有关此配置的更多信息，请参见第 13.7 节“配置您的系统使用 OpenLDAP 进行认证”。

### 13.5. /etc/openldap/schema/ 目录

`/etc/openldap/schema/` 存储 LDAP 定义，这些定义位于 `slapd.at` 和 `slapd.conf` 文件中。所有的属性语法定义和对象类定义现在位于不同的架构文件中。`/etc/openldap/schema.conf` 使用 `include` 引用了各种架构文件：

```
include core.schema

include cosine.schema

include person.schema

include nis.schema

include inetd.schema

include kerberos.schema

include member.schema

include mail.schema

include device.schema

include posix.schema
```
