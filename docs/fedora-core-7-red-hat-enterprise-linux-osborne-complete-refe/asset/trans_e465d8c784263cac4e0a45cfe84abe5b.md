

dn: ou=users,dc=mytrek,dc=com
objectclass: organizationalUnit
ou: users

随后是各个个体记录，例如以下针对 **dylan** 的记录。这里的对象类是 organizationalPerson 和 inetOrgPerson。然后是属性，例如通用名称 (cn)、用户 ID (uid)、组织 (o)、姓氏 (sn) 和街道地址。

dn: cn=dylan,ou=users,dc=mytrek,dc=com
objectclass: organizationalPerson
objectclass: inetOrgPerson
cn: dylan
uid: dylan
o: MyTrek
sn: shark
street: 77777 saturn ave

这里展示了一个 LDIF 文件的示例。该组织是 mytrek.com。其中包含两条记录，一条是针对 **dylan** 的，另一条是针对 **chris** 的：

# mytrek.ldif

dn: dc=mytrek,dc=com
objectclass: dcobject
objectclass: organization
dc: mytrek
o: MyTrek

dn: cn=Manager,dc=mytrek,dc=com
cn: Manager
objectclass: organizationalRole

dn: ou=users,dc=mytrek,dc=com
objectclass: organizationalUnit
ou: users

dn: cn=dylan,ou=users,dc=mytrek,dc=com
objectclass: organizationalPerson
objectclass: inetOrgPerson
cn: dylan
uid: dylan
o: MyTrek
sn: shark
street: 77777 saturn ave

dn: cn=chris,ou=users,dc=mytrek,dc=com
objectclass: organizationalPerson
objectclass: inetOrgPerson
cn: chris
uid: chris
o: MyTrek
sn: dolphin
street: 99999 neptune way

## 添加记录

创建 LDIF 文件后，你可以使用 ldapadd 命令将记录添加到你的 LDAP 目录中。使用 -D 选项指定要添加记录的目录，使用 -f 选项指定要读取的 LDIF 文件。你甚至可以使用 ldapadd 直接输入字段。-x 选项表示使用简单密码访问，-W 会提示输入密码，-D 选项指定目录管理员。

# ldapadd -x -D "cn=Manager,dc=mytrek,dc=com" -W -f mytrek.ldif
Enter LDAP Password:
adding new entry "dc=mytrek,dc=com"
adding new entry "cn=Manager,dc=mytrek,dc=com"
adding new entry "ou=users,dc=mytrek,dc=com"
adding new entry "cn=dylan,ou=users,dc=mytrek,dc=com"
adding new entry "cn=chris,ou=users,dc=mytrek,dc=com"

请务必重启 LDAP 服务器，以使更改生效。

## 搜索 LDAP

添加记录后，你可以使用 ldapsearch 命令搜索你的 LDAP 目录。-x 和 -W 选项提供简单密码访问，-b 选项指定要使用的 LDAP 数据库。在选项之后是待搜索的属性，在本例中是 street（街道）属性。

# ldapsearch -x -W -D 'cn=Manager,dc=mytrek,dc=com' -b 'dc=mytrek,dc=com' street
Enter LDAP Password:
# extended LDIF
#
# LDAPv3
# base <dc=mytrek,dc=com> with scope sub
# filter: (objectclass=*)
# requesting: street

# dylan, users, mytrek.com
dn: cn=dylan,ou=users,dc=mytrek,dc=com
street: 77777 saturn ave

# chris, users, mytrek.com
dn: cn=chris,ou=users,dc=mytrek,dc=com
street: 99999 neptune way

# search result
search: 2
result: 0 Success

# numResponses: 6
# numEntries: 5

如果你希望查看数据库中列出的所有记录，你可以使用相同的搜索命令，但不指定任何属性。

## LDAP 工具

实际上要创建或更改 LDAP 数据库中的条目，你可以使用 `ldapadd` 和 `ldapmodify` 实用工具。使用 `ldapdelete` 可以删除条目。创建 LDAP 数据库后，你可以通过 LDAP 服务器使用 `ldapsearch` 对其进行查询。对于 LDAP 服务器，你可以使用 LDAP 数据交换格式（LDIF）创建包含 LDAP 条目的文本文件。然后，可以使用 `slapadd` 工具将这些文本文件一次性批量读取到 LDAP 数据库中。`slapcat` 工具从 LDAP 数据库中提取条目，并将它们保存在 LDIF 文件中。为了重新索引添加和修改的内容，你需要使用 `slapindex` 实用工具。有关使用和设置 LDAP 数据库（如地址簿）的详细信息，请参阅 Linux 文档项目中的 LDAP 指南（www.ldif.org）。

> **提示** 你可以使用 system-config-authentication 工具启用并指定 LDAP 服务器（系统|管理|认证菜单；参见第 4 章）。你还可以使用 LDAP 浏览器/编辑器或 GNOME 目录管理员来管理和编辑 LDAP 目录。

## LDAP 与 PAM

借助 LDAP，你还可以更精确地控制信息泄漏的种类以及向谁泄漏。使用 PAM 模块（`pam_ldap`），LDAP 可以执行用户身份验证任务，为用户提供集中式身份验证。用户为不同服务（如 POP 邮件服务器登录、系统登录和 Samba 登录）执行的登录操作，都可以通过使用单一的受 PAM 保护的用户 ID 和密码通过 LDAP 完成。若要配置 PAM 使用 LDAP，请使用 system-config-authentication 工具（系统|管理|认证），并在“认证”面板上选择“启用 LDAP 支持”（参见第 4 章）。你还应确保正确指定了 LDAP 服务器。若要使用 LDAP 进行身份验证，你需要配置 PAM 以使用它，并将身份验证文件迁移到 LDAP 格式。`/usr/share/openldap/migration` 目录中包含可用于将旧文件转换为 LDAP 版本的脚本。

## LDAP 与名称服务切换服务

使用 `libnss_ldap` 模块，LDAP 还可以用于名称服务切换（NSS）服务，与 NIS 和系统文件一起提供诸如密码和组等系统数据库服务。客户端可以轻松启用 NSS 的 LDAP，方法是使用 system-config-authentication 工具（系统|管理|认证）并在“用户信息”面板中选择“启用 LDAP 支持”。你还需要确保指定了 LDAP 服务器。你也可以手动在 `/etc/nsswitch.conf` 文件中为条目添加 `ldap`。

> **提示** 为了更安全地保护对 LDAP 服务器的访问，你应该对 LDAP 管理员的密码进行加密。LDAP 管理员在 `rootdn` 条目中指定，其密码在 `rootpw` 条目中指定。要创建加密密码，请使用 `slappasswd` 命令。该命令会提示你输入密码并显示其加密版本。将该加密版本复制到 `rootpw` 条目中。

在 Thunderbird 中，打开地址簿，然后选择 **文件 | 新建**，并选择 **LDAPD** 目录。在此处，你可以输入 **LDAP** 服务器。这将显示一个面板，你可以在其中输入地址簿名称、**LDAP** 服务器的主机名、要搜索的基础 **DN** 以及端口号（在 Fedora 中为 389）。

# 可插拔认证模块

可插拔认证模块（PAM）是一项认证服务，它允许系统确定对用户的认证方法。在 Linux 系统中，传统上通过查找密码来进行身份验证。当用户登录时，登录过程会在密码文件中查找他们的密码。使用 PAM，用户的认证请求被转发给 PAM，PAM 进而使用指定的方法对用户进行认证。这可以是简单的密码查找，也可以是向 LDAP 服务器发起请求，但提供认证的是 PAM，而不是用户或应用程序直接进行密码查找。在这方面，认证变得集中化，并由特定服务（即 PAM）控制。实际的认证程序可以由系统管理员动态配置。认证由模块执行，这些模块可根据所需的认证类型而变化。管理员只需修改 PAM 配置文件即可添加或替换模块。更多 PAM 模块的信息和列表，请访问位于 www.kernel.org/pub/linux/libs/pam 的 PAM 网站。PAM 模块位于 /lib/security 目录中。

## PAM 配置文件

PAM 为请求认证的不同服务使用不同的配置文件。这些配置文件存储在 /etc/pam.d 目录中。例如，你有一个用于登录系统的配置文件（/etc/pam.d/login），一个用于图形化登录的配置文件（/etc/pam.d/gdm），以及一个用于访问 Samba 服务器的配置文件（/etc/pam.d/samba）。如果不存在服务文件，则调用默认 PAM 配置文件，即 /etc/pam.d/other。system-auth 文件包含由 system-config-authentication 生成的系统服务的标准认证模块，并在许多其他配置文件中被调用。此外，Fedora 为其配置工具（如 system-config-services 和 system-config-network）设置认证。

## PAM 模块

PAM 配置文件包含用于认证的模块列表。它们的格式如下：

module-type control-flag module-path module-args

module-path 是要运行的模块，module-args 是你想要传递给该模块的参数。虽然有一些通用参数，但大多数模块都有自己特有的参数。module-type 指代不同的认证管理组：账户（account）、认证（authentication）、会话（session）和口令（password）。账户管理执行账户验证，检查诸如用户是否拥有访问权限或密码是否过期等账户方面。认证（auth）验证用户是谁，通常通过密码确认。口令管理执行认证更新，例如

