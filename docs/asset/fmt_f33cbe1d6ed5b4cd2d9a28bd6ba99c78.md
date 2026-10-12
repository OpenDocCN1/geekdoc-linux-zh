
根据你的 LDAP 目录的使用方式，你可能需要编辑 `slapd.oc.conf` 中的对象类定义。例如，如果你正在为你的组织创建一个员工 LDAP 目录，你可能会为某些对象类设置特定的必需属性，这些属性可能不会在组织外部使用（例如，你组织内部的员工 ID 号可能是 `person` 对象类的一个必需属性）。

### 8.6 OpenLDAP 守护进程和实用程序

OpenLDAP 包包含两个守护进程：`slapd` 和 `slurpd`。`slapd` 守护进程是独立的 LDAP 守护进程，支持 LDAP 需要运行它。

`slurpd` 守护进程控制 LDAP 目录在网络上的复制。`Slurpd` 将变更从主 LDAP 目录发送到从 LDAP 目录。除非你的网络上有一个以上的 LDAP 服务器，否则你不需要运行 `slurpd`。如果你有多个 LDAP 服务器，你需要运行 `slurpd` 以保持 LDAP 目录同步。

OpenLDAP 还包括一些用于添加、修改和删除 LDAP 目录中条目的实用程序。`ldapmodify` 工具用于修改 LDAP 数据库中的条目。`ldapadd` 实用程序用于向目录添加条目（`ldapadd` 实际上是到 `ldapmodify -a` 的硬链接）。`Ldapsearch` 用于搜索条目，`ldapdelete` 用于删除条目。`ldif2ldbm` 工具将 LDIF 文件转换为 LDBM 后端数据库。

有关所有这些实用程序的更多信息，请参见它们的手册页。

### 8.7 为 LDAP 添加额外功能的模块

Red Hat Linux 包含以下为 LDAP 添加功能的软件包：

`nss_ldap` 模块是 **Solaris 名称服务切换（NSS）** 的 LDAP 模块。NSS 是一组 C 库扩展，用于访问 LDAP 目录信息，而不是或除了 **网络信息服务**（NIS 名称服务和/或平面文件）之外。需要使用 `nss_ldap` 模块才能将 LDAP 用作本地名称服务。

`pam_ldap` 模块用于将 LDAP 认证集成到可插拔认证模块（PAM）API 中。如果使用 `pam_ldap`，用户可以通过 LDAP 目录进行认证和更改密码。`nss_ldap` 和 `pam_ldap` 模块包含在 `nss_ldap` 软件包中。

Red Hat Linux 还包括 Apache Web 服务器的 LDAP 模块。`auth_ldap` 模块用于将 HTTP 客户端与 LDAP 目录中的用户条目进行认证。`php-ldap` 模块为 PHP3 HTML 嵌入式脚本语言添加了 LDAP 支持。`auth_ldap` 和 `php-ldap` 模块需要作为**动态共享对象**（DSO）编译到 Apache 中。

### 8.8 LDAP 操作指南：快速概述

本节提供了启用 LDAP 目录所需步骤的快速概述。

1. 确保安装了 `openldap` RPM 以及其他所需的任何 LDAP 相关 RPM。
2. 查看 OpenLDAP 网站上的快速入门指南（http://www.opendap.org/faq/data/cache/172.html；从“创建 slapd 配置文件”开始，因为 LDAP 文件已经安装），或者查看 Linux-LDAP HOWTO（http://www.linuxdoc.org/HOWTO/LDAP-HOWTO-HOWTO.html）以获取在你的系统上使用 LDAP 的说明。两者都涵盖了其余步骤。
3. 编辑 `slapd.conf` 文件以使其适合你的系统。
4. 启动 `slapd`。
5. 创建您的 LDAP 目录（PADL Software 网站在 http://www.padl.com/ldap_examples.html 提供了 LDAP 条目的示例）。
6. 使用 `ldapadd` 或脚本向您的 LDAP 目录中添加条目。
7. 使用 `ldapsearch` 查看 `slapd` 是否正在运行。
8. 此时，您的 LDAP 目录应该已经存在。下一步是配置支持 LDAP 的应用程序，使它们能够使用 LDAP 目录。

### 8.9 配置系统以使用 OpenLDAP 进行身份验证

本节简要概述了如何配置您的 Red Hat Linux 系统以使用 OpenLDAP 进行身份验证。除非您是 OpenLDAP 专家，否则您可能需要比这里提供的更多文档。请参阅第 8.10 节“网络上的 LDAP 资源”中提供的参考以获取更多信息。

#### 8.9.1 安装必要的 LDAP 软件包

首先，您需要确保 LDAP 服务器和 LDAP 客户端机器上都安装了相应的软件包。LDAP 服务器需要 `openldap` 软件包。

LDAP 客户端机器需要安装以下软件包：`openldap`、`auth_ldap`、`nss_ldap` 和 `pam_ldap`。

#### 8.9.2 编辑配置文件

##### 编辑 `/etc/openldap/slapd.conf`

位于 `/etc/openldap` 中的 `slapd.conf` 文件包含了您的 `slapd` LDAP 服务器所需的配置信息。您需要编辑此文件，使其针对您的域和服务器进行具体设置。

`suffix` 行指定了 LDAP 服务器将提供信息的域。`suffix` 行应从以下内容更改为：

```
suffix "dc=acmewidgets, dc=com"
```

或

```
suffix "dc=acmeuniversity, dc=org"
```

`rootdn` 条目是某个用户的 DN，该用户不受针对 LDAP 目录操作设置的访问控制或管理限制参数约束。`rootdn` 用户可以被视为 LDAP 目录的 root 用户。`rootdn` 行需要从以下内容更改为：

```
rootdn "cn=root, dc=your-domain, dc=com"
```

类似以下内容：

```
rootdn "cn=root, dc=redhat, dc=com"
```

或

```
rootdn "cn=ldapmanager, dc=my_organization, dc=org"
```

将 `rootpw` 行从以下内容更改为：

```
rootpw secret
```

类似以下内容：

```
rootpw {crypt}$4l9sOIJo4kBM
```

在上面的示例中，您使用的是加密的 root 密码，这是一个比在 `slapd.conf` 文件中留下明文 root 密码好得多的主意。要生成此加密字符串，您应该从 `passwd` 文件中复制出来，或者使用 Perl：

```
perl -e "print crypt('passwd','a_salt_string');"
```

在上面的 Perl 行中，`salt_string` 是一个两字符的盐，而 `passwd` 是密码的明文版本。

您也可以从 `/etc/passwd` 中复制 `passwd` 条目，但如果 `passwd` 条目是 MD5 密码（Red Hat Linux 6.2 的默认设置），则此方法无效。

##### 编辑 `ldap.conf`

编辑 LDAP 服务器和客户端上 `/etc` 和 `/etc/openldap` 中的 `ldap.conf` 文件。

编辑 `/etc/ldap.conf`（`nss_ldap` 和 `pam_ldap` 的配置文件），以反映您的组织和搜索基础。`/etc/openldap/ldap.conf` 文件是像 `ldapsearch`、`ldapadd` 等命令行工具的配置文件，它也需要根据您的 LDAP 设置进行编辑。客户端机器需要为系统修改这两个文件。

##### 编辑 `/etc/nsswitch.conf`

要使用 `nss_ldap`，您需要将 `ldap` 添加到 `/etc/nsswitch.conf` 的相应字段中。（编辑此文件时要非常小心；确保您知道自己在做什么。）例如：

```
passwd: files ldap
shadow: files ldap
group: files ldap
```

##### 复制 PAM 配置文件

要使用 `pam_ldap`，您需要将 PAM 配置文件从 `/usr/doc/nss_ldap>version>/pam.d/` 复制到您的 `/etc/pam.d/` 目录。这是一组允许所有标准 PAM 支持的应用程序使用 LDAP 进行身份验证的 PAM 配置文件。（PAM 超出了本 LDAP 概述的范围，因此如果您需要帮助，请查阅第 2.6 节“使用 PAM 进行用户身份验证”和/或 PAM man 手册页。）

#### 8.9.3 将旧的认证信息迁移到 LDAP 格式

`/usr/share/openldap/migration` 目录包含一组 shell 和 Perl 脚本，用于将您的旧认证信息迁移到 LDAP 格式。（是的，使用这些脚本需要在系统上安装 Perl。）

首先，您需要修改 `migrate_common.ph` 文件，使其反映您的域。默认的 DNS 域应从以下内容更改为：

```
$DEFAULT_MAIL_DOMAIN = "padi.com";
```

类似以下内容：

```
$DEFAULT_MAIL_DOMAIN = "your_company.com";
```
