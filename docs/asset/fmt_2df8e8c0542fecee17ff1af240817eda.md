
# GECOS 和登录 SHELL

当用户运行 `passwd`（第 712 页）时，此实用程序会与 `passwd` 守护进程交换信息以更新密码（以及主服务器上 `/etc/shadow`（可选的）文件中的其他信息）。更改请求会被发送到 `syslog`（第 608 页）。`NIS` 初始化脚本可以作为目录，更多信息请参阅 115 页。

# LDAP

## 概述

`LDAP`（轻量级访问协议）是旧的 `DAP` 的替代方案，它在 `TCP/IP` 上运行并感知网络，且适用于许多平台。`LDAP` 客户端查询服务器并指定其想要的数据。例如，查询可以询问住在旧金山的姓 `Smith` 的人的名字。

`LDAP`（目录访问协议）适用于不经常更改的数据，服务器持有 *目录*。`LDAP` 客户端查询并更新这个目录。除了名称和地址信息，`LDAP` 目录可以持有网络服务。或者，其他服务可以使用它进行认证。

将其按组成部分命名。以下行定义了包含域组件（`DC`）`sobell` 和 `DC` `com` 的 `DSE`：

```bash
$ sudo grep -r sobell /etc/ldap/*
/etc/ldap/slapd.d/cn-config={1}db.ldif:olcSuffix: dc=sobell,dc=com
```

## LDIF 和 DN

`LDIF` 和 `CN` 在 `LDAP` 数据格式（`LDIF`）中指定的 `LDAP` 目录，示例 `DSE` 可能包含以下条目，该条目由 `LDAP` 数据交换格式（`LDIF`）指定；更多信息请参见 `ldif` 手页：

```ldap
cn: cn=Samuel Smith,dc=sobell,dc=com
cn: Samuel Smith
cn: Sam
cn: SLS
givenName: Samuel
sn: Smith
mail: sls@sobell.com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
```

除了第一行外，每行都指定一个属性。每行中冒号之前的单词是属性名。冒号和空格之后是属性值。该条目的第一行指定了该条目的 `DN`（区分名）。`RDN` 中使用的属性值是 `CN`（通用名称），来自该条目：`Samuel Smith`。第二级是顶级条目的子级；因此，父条目的 `DN` 即为顶级条目的 `DN`（`dc=sobell,dc=com`）。你可以通过其 `DN` 唯一地标识此条目：`cn=Samuel Smith,dc=sobell,dc=com`。

由于此条目定义了三个 `CN`，因此对 `Samuel Smith`、`Sam` 或 `SLS` 的搜索将返回此条目。此条目还定义了名（`given name`）、姓（`sn`）和电子邮箱地址（`mail`）。

`objectClass` 属性从其父类继承对象类属性。此外，每个条目必须至少有一个 `objectClass` 属性（前述条目有四个）。`objectClass` 值必须是架构（`schema`）中定义的类。架构规定了对象类的强制性（必须）和可选（允许）的属性。例如，架构中的以下条目定义了名为 `person` 的对象类。`MUST` 和 `MAY` 行指定了 `person` 对象类需要的属性（`sn` 和 `cn`；属性之间用美元符号隔开）以及哪些属性是可选的（`userPassword`, `phoneNumber`, `seeAlso` 和 `description`）。

```bash
$ cat /etc/ldap/slapd/core.schema
```

```schema
objectclass ( 2.5.6.6 NAME 'person'
DESC 'RFC2256: a person'
SUP top STRUCTURAL
MUST ( sn $ cn )
MAY ( userPassword $ phoneNumber $ seeAlso $ description )
...
```

### 缩写

以下列表总结了本节提到的缩写。

- `CN` 通用名称
- `DC` 域组件
- `DN` 区分名 (Distinguished Name)
- `DSE` `DSA` 特有条目
- `LDIF` `LDAP` 数据交换格式
- `RDN` 相对区分名

### 更多信息

- 本地页面：`ldap.conf`, `ldapmodify`, `ldapsearch`, `ldif`, `slapd`, `slapd.conf`, `slapppasswd`
- Web `LDAP` 主页：`www.openldap.org`
- 管理员指南：`www.openldap.org/doc/admin24`
- OpenLDAP Faq-O-Matic：`www.openldap.org/faq`
- gq: `gq-project.org`
- HOWTO `LDAP` Linux HOWTO
- 书籍：`www.zytrax.com/books/ldap`

# 设置 LDAP 服务器

本节介绍了设置 `LDAP` 服务器所涉及的步骤。

## 前提条件

安装以下软件包。当安装 `slapd` 软件包时，`dpkg postinst` 脚本会配置基础 `LDAP` 目录，询问管理员密码并启动 `slapd` 守护进程。

- `slapd`
- `ldap-utils`

`slapd init` 脚本。在你手动配置 `slapd` 后，调用 `slapd init` 脚本来重启 `slapd`：

```bash
$ sudo /etc/init.d/slapd restart
Stopping OpenLDAP: slapd.
Starting OpenLDAP: slapd.
```

## 注意事项

`slapcat` 工具必须以特权用户（而非 `LDAP` 管理员）身份运行，它从 `slapd` 数据库检索信息并以 `LDIF` 格式显示（723页）。虽然 `slapcat` 是非常有用的工具，但如果你使用它备份数据库，请小心：在你进行备份时，其他用户可能正在更改数据。接下来，`slapcat` 显示 `dpkg postinst` 脚本包含的基础 `LDAP` 目录包含两个条目：

# 设置 LDAP 服务器 725

```bash
$ sudo slapcat
dn: dc=nodomain
objectClass: top
objectClass: dcObject
objectClass: organization
o: nodomain
dc: nodomain
...
dn: cn=admin,dc=nodomain
objectClass: simpleSecurityObject
objectClass: organizationalRole
cn: admin
description: LDAP administrator
```

第一个条目的 `DN` 为 `nodomain`，它本身包含一个 `nodomain` 的 `DC`。

第二个条目设置了一个名为 `admin` 的管理员，其 `cn` 为 `cn=admin,dc=nodomain`。虽然这种设置是一个功能性的 `LDAP` 目录，但可能不是你想要的。下一节将解释如何重新配置此目录以满足你的需求。

`DB_CONFIG` 你可以修改文件中的参数来提高 `LDAP` 服务器的性能。更多信息请参见网页 `www://www.openldap.org/faq/data/cache/1072.html` 以及本地系统上的 `/usr/share/doc/slapd/README.DB_CONFIG.gz` 文件。

防火墙。`LDAP` 服务器通常监听在 `TCP` 端口 `389`，该端口未加密。你使用 `LDAP` 进行身份验证，在 `636` 端口使用 `LDAP over SSL`。

## 逐步设置

本节列出了设置 `LDAP` 服务器所涉及的步骤。示例使用了 `sobell`。对于本地系统进行实验，你可以将此名称设置为你喜欢的任何名称，并将服务器系统称为 `localhost`。

### 配置服务器

在完成这些说明后，执行命令 `sudo dpkg-reconfigure slapd`。该实用呈现出一个伪图形（30页）显示（图 21-1），询问你想要如何配置 `slapd`。通常，你可以接受默认答案，但以下例外：

```bash
$ sudo dpkg-reconfigure slapd

跳过 OpenLDAP 服务器配置？ [否]

DNS 域名: sobell.com

组织名称: Sobell Associates Inc.

要使用的数据库后端: [HDB]

是否在卸载 slapd 时删除数据库？ [否]

管理员密码: purcupine

确认密码: purcupine

允许 LDAPv2 协议吗？ [否]

在 /etc/ldap/slapd.d/ 未找到 slapd 的配置目录。

如果你有 slapd 配置目录，请修改

/etc/default/slapd 以反映此设置。如果你在安装期间选择

不

配置 slapd，则你需要在启动 slapd 之前

进行配置。

正在创建初始 slapd 配置... 完成。

正在创建初始 LDAP 目录... 完成。

重新加载 AppArmor 配置文件 ... 完成。

正在启动 OpenLDAP: slapd。
```

### 测试服务器

在运行 `dpkg-reconfigure` 后，使用以下查询测试服务器（你可能需要在执行此查询前重启系统）：

```bash
$ ldapsearch -x -s base namingContexts
# extended LDIF
#
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectclass=*)
# requesting: namingContexts
#
#
d:
namingContexts: dc=sobell,dc=com

# 搜索结果
search: 2
result: 0 Success
# numResponses: 2
# numEntries: 1
```

命令行上的 `-x` 指定简单身份验证，`-s base` 指定搜索范围为基准对象，而 `namingContexts` 是你正在搜索的属性。此命令的输出应该与前面的示例所示类似。搜索返回的 `namingContexts` 应该与你在回答 `dpkg-reconfigure` DNS 域名问题时（DNS domain name）指定的 `DSE`（第 726 页）相同。

# 第 21 章 NIS 和 LDAP

`dpkg-reconfigure` 工具向目录添加了一个二级条目（位于 `DSE` 条目下方）和一个三级条目。

在运行 `dpkg-reconfigure` 后，`slapcat` 显示了这两个条目：

```bash
$ sudo slapcat
dn: dc=sobell,dc=com
objectClass: top
objectClass: dCObject
objectClass: organization
o: Sobell Associates Inc.
o: so
structuralObjectClass: organization
entryUUID: 00a9404c-2037-102d-8186-89cfe750b5e8
creatorsName:
timeStamp: 2008092615106Z
entryCSN: 2008092615106.823966Z#000000####000000
modifiersName:
modifyTimestamp: 2008092615106Z

dn: dc=admin,dc=sobell,dc=com
objectClass: simpleSecurityObject
objectClass: organizationalRole
cn: admin
description: LDAP administrator
userPassword: dNeyX8fTU1INZBTketynVb0k=
```

每个内容的第一行指定了该条目的 `DN`（目录名称）。以 `dc` 开头的行指定 `DC`（域组件）。`ObjectClass` 指定了该条目所属的类。以 `o`（`organization-Name` 的缩写）开头的行指定了该条目所属组织的名称。

服务器会在条目中添加更多信息，包括在条目整个生命周期内保持不变的 `UUID` 数字、时间戳以及创建和修改该条目的用户名。在这种情况下，`dpkg-reconfigure` 设置了条目，但未指定任何用户。

## 向目录添加条目

你可以使用许多图形化和文本工具来向 `LDAP` 目录添加信息和进行查询。本节解释了如何使用 `ldmodify` 命令行工具来设置员工 `LDAP` 目录。其他工具的说明请参阅第 731 页。

当你在 `ldmodify` 命令中指定以下文件时，`ldmodify` 会向 `LDAP` 目录添加一个二级条目（位于 `DSE` 条目下方一级）。此文件添加了名为 `employees` (`ou=employees`) 的组织单元对象类。`DN` 由 `DSE` 指定为 `ou=employees`。

```bash
$ cat sal.ldif
dn: ou=employees,dc=sobell,dc=com
changetype: add
```

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_779_0.png)

`objectClass: organizationalUnit`

`ou: employees`

`sa1.ldap` 的第一行标识了你正在添加的条目的 `DN`。`change-type` 指令告诉 `ldapmodify` 将条目添加到目录中。如果你在 `ldapmodify` 命令行上使用 `-a` 选项，或者使用 `ldadd` 工具代替 `ldapmodify`，则可以省略此项。`ObjectClass` 指定了该条目所属的对象类。`ou`（`organizationalUnitName` 的缩写）指定了它所属的组织单元名称。

以下命令根据 `sa1.ldif` 文件修改 `LDAP` 目录。`.ldif` 文件扩展常用，但对于持有 `LDIF` 的文件并非必须。

```bash
$ ldapmodify -xD "cn=admin,dc=sobell,dc=com" -w - -f sa1.ldif
adding entry "ou=employees,dc=sobell,dc=com"
```

`-x` 选项允许服务器使用简单身份验证。参数 `-f` 指定了要操作的 `LDAP` 管理员的 `DN`（在安装时由 `dpkg-configure` 指定）。通过指定此用户，该参数也指定了 `LDAP` 目录的 `DSE`。参数 `-w` 是 `LDAP` 管理员的密码。`ldapmodify` 工具会报告新条目的 `DN`。

有了这个对象类，你就可以向 `LDAP` 目录中添加员工了。以下文件提供了一个示例：

```bash
$ cat sa2.ldif
dn: ou=employees,dc=sobell,dc=com
changetype: add
cn: Samuel Smith
cn: Samuel Smith
objectClass: inetOrgPerson
mail: samuel@sobell.com
givenName: Samuel
surname: Smith
displayName: Samuel Smith
telephoneNumber: 999 999 999
homePhone: 000 000 000
initials: SLS
```

以下命令使用 `-W` 导致 `ldapmodify` 提示 `LDAP` 密码。在提示中指定密码而不是在命令行中指定，可以通过避免密码对用户可见来提高安全性。

```bash
$ ldapmodify -xD "cn=admin,dc=sobell,dc=com" -W
adding entry "ou=employees,dc=sobell,dc=com"
```

（注：此处原文命令似乎漏掉了 -f sa2.ldif，根据上下文推断逻辑如下）

```bash
$ ldapmodify -xD "cn=admin,dc=sobell,dc=com" -W -f sa2.ldif
adding entry "ou=employees,dc=sobell,dc=com"
```
