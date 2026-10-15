
```
$ cat /etc/ldap/schema/core.schema
...
objectclass ( 2.5.6.6 NAME 'person'
 DESC 'RFC2256: a person'
 SUP top STRUCTURAL
 MUST ( sn $ cn )
 MAY ( userPassword $ telephoneNumber $ seeAlso $ description )
)
...
```

### 缩略语

以下列表总结了本节中提到的缩略语。

- `CN` 通用名称（Common Name）
- `DC` 域名组件（Domain Component）
- `DN` 可区分名称（Distinguished Name）
- `DSE` DSA 特定条目（DSA-Specific Entry）
- `LDIF` LDAP 数据交换格式（LDAP Data Interchange Format）
- `RDN` 相对可区分名称（Relative Distinguished Name）

#### 更多信息

本地手册页：`ldap.conf`、`ldapmodify`、`ldapsearch`、`ldif`、`slapd`、`slapd.conf`、`slapasswd`

- Web LDAP 主页：`www.openldap.org`
- 管理员指南：`www.openldap.org/doc/admin24`
- Ubuntu：`help.ubuntu.com/10.04/serverguide/C/openldap-server.html`
- OpenLDAP 常见问题解答生成器：`www.openldap.org/faq`
- 书籍：`www.zytrax.com/books/ldap`
- gg：`gg-project.org`

# 设置 LDAP 服务器

本节解释了设置 LDAP 服务器所涉及的步骤。

## 先决条件

安装以下软件包：

- `slapd`
- `ldap-utils`

**`slapd` 初始化脚本** 手动配置 `slapd` 后，调用 `slapd` 初始化脚本以重启 `slapd`：

```
$ sudo service slapd restart
Stopping OpenLDAP: slapd.
Starting OpenLDAP: slapd.
```

## 注意事项

**`DB_CONFIG`** 你可以修改 `/var/lib/ldap/DB_CONFIG` 文件中的参数以提高 LDAP 服务器的性能。请参阅 `http://www.openldap.org/faq/data/cache/1072.html` 网页以获取更多相关信息。还请参见本地系统中的 `/usr/share/doc/slapd/examples/DB_CONFIG` 和 `/usr/share/doc/slapd/README.DB_CONFIG.gz` 文件。

**防火墙** `slapd` LDAP 服务器通常监听 TCP 端口 389，该端口未加密。如果你使用 LDAP 进行身份验证，请使用端口 636 上的 LDAP over SSL。如果 LDAP 服务器系统正在运行防火墙，你需要打开其中一个端口。使用 `gufw`（第 876 页），通过添加允许客户端访问端口 389 或端口 636 服务的规则来打开其中一个端口。

## 设置服务器

**后端** OpenLDAP 使用目录信息树（DIT）层次结构，其根位于 `/etc/ldap/ldap.d/cn=config`（等号是目录名称的一部分），以配置 **`slapd`** 守护进程。此设置允许动态配置 **`slapd`** 守护进程（无需重启守护进程）。在你向 LDAP 数据库添加用户数据之前，必须配置此 DIT，即**后端**。

**前端** 数据库的前端也需要在添加用户数据之前进行配置。你必须将其设置为持有用户想要存储的数据类型。第 762 页的“设置前端”描述了如何设置与许多地址簿应用程序兼容的数据库。

一旦你设置了后端和前端，你就可以按照第 764 页的“向目录添加条目”一节中所述的方法添加用户数据。

本节列出了在 **`sobell.com`** 域中设置 LDAP 服务器所涉及的步骤。当你设置 LDAP 服务器时，在示例中将你正在设置的服务器域名替换为 **`sobell.com`**。

为了实验和学习 LDAP，请在本地设置并运行本节中描述的示例服务器。尽管示例使用的是 **`sobell.com`**，但当你从服务器系统工作时，可以将 LDAP 服务器称为 **`localhost`**。

## 设置后端

在向 LDAP 数据库的前端添加信息之前，你需要向后端添加三个模式文件和一个设置文件。安装 LDAP 时会安装这三个模式文件。输入以下命令将这些文件添加到 LDAP 目录：

```
$ sudo ldapadd -Y EXTERNAL -H ldap:///~ -f /etc/ldap/schema/cosine.ldif
SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
adding new entry "cn=cosine,cn=schema,cn=config"
...
$ sudo ldapadd -Y EXTERNAL -H ldap:///~ -f /etc/ldap/schema/nis.ldif
...
$ sudo ldapadd -Y EXTERNAL -H ldap:///~ -f /etc/ldap/schema/inetorgperson.ldif
...
```

以下文件将使用包含 DC **`sobell`** 和 DC **`com`**（第 758 页）的 DSE 以及名为 **`admin`**、密码为 **`porcupine`** 的管理员用户来设置 LDAP 数据库的后端。根据你正在设置的数据库更改这些值。（注意倒数第四行很长，在以下显示中进行了换行。此文件可在 Web 上的 `www.sobell.com/UB3/code/chapter_21/backend.setup.ldif` 获取。）

```
$ cat backend.setup.ldif
dn: cn=module,cn=config
objectClass: olcModuleList
cn: module
olcModulePath: /usr/lib/ldap
olcModuleLoad: back_hdb

dn: olcDatabase=hdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcHdbConfig
olcDatabase: {1}hdb
olcSuffix: dc=sobell,dc=com
olcDbDirectory: /var/lib/ldap
olcRootDN: cn=admin,dc=sobell,dc=com
olcRootPW: porcupine
olcDbConfig: set_cachesize 0 2097152 0
olcDbConfig: set_lk_max_objects 1500
olcDbConfig: set_lk_max_locks 1500
olcDbConfig: set_lk_max_lockers 1500
olcDbIndex: objectClass eq
olcLastMod: TRUE
olcDbCheckpoint: 512 30
olcAccess: to attrs=userPassword by dn="cn=admin,dc=sobell,dc=com" 
       write by anonymous auth by self write by * none
olcAccess: to attrs=shadowLastChange by self write by * read
olcAccess: to dn.base="" by * read
olcAccess: to * by dn="cn=admin,dc=sobell,dc=com" write by * read
```

输入以下命令以加载此文件：

```
$ sudo ldapadd -Y EXTERNAL -h ldapi:/// -f backend.setup.ldif
SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
adding new entry "cn=module,cn=config"

adding new entry "olcDatabase=hdb,cn=config"
```

## 设置前端

以下文件为示例数据库设置 DSE（LDAP 目录中的顶级条目；第 758 页）。用你想使用的域名替换 `dc=sobell,dc=com`。

```
$ cat t11.ldif
dn: dc=sobell,dc=com
changetype: add
objectClass: top
objectClass: dcObject
objectClass: organization
dc: Sobell Associates
dc: Sobell
description: Sobell Example
```

## 测试服务器

在配置好数据库的后端和前端之后，使用以下查询来测试服务器（在此查询生效之前可能需要重启）：

```
$ ldapsearch -x -s base namingContexts
# extended LDIF
#
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectClass=*)
# requesting: namingContexts
#

dn: namingContexts: dc=sobell,dc=com

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1
```

命令行中的 `-x` 指定简单认证，`-s base` 将搜索范围指定为基对象，**`namingContexts`** 是您要搜索的属性。该命令的输出应与前面示例中显示的内容相似。搜索返回的 **`namingContexts`** 应与您在前端设置时指定的 DSE 相同（第 762 页）。

`slapcat` 实用程序必须以特权用户（而非 LDAP 管理员）身份运行，它从 `slapd` 数据库中检索信息并以 LDIF 格式显示（第 759 页）。虽然 `slappacl` 是一个有用的工具，但如果您使用它来备份数据库，请谨慎操作：当您在备份时，其他用户可能正在更改数据。接下来，`slappacl` 显示基本 LDAP 目录包含本章前面几节中设置的两个条目。

```
$ sudo slappacl
  dn: dc=sobell,dc=com
  objectClass: top
  objectClass: dcObject
  objectClass: organization
  o: Sobell Associates
  dc: Sobell
  description:: U29IZWxsIEV4YW1wbGU 
  structuralObjectClass: organization
  entryUUID: 42d495ba-0785-102f-8764-434c55dbcc7e
  creatorsName: cn=admin,dc=sobell,dc=com
  createTimeStamp: 20100608200751Z
  entryCSN: 20100608200751.367377? #00000000#000000000 
  modifiersName: cn=admin,dc=sobell,dc=com
  modifyTimeStamp: 20100608200751Z

  dn: cn=admin,dc=sobell,dc=com
  objectClass: simpleSecurityObject
  objectClass: organizationalRole
  cn: admin
  description: LDAP administrator
  userPassword: cG9y3VwAW5l
  ...
```

每个条目的第一行指定该条目的 `DN`。以 `dc` 开头的行指定 `DC`（域组件）。`objectClass` 行指定该条目所属的对象类。以 `o`（`organizationName` 的缩写）开头的行指定该条目所属组织的名称。

服务器向条目中添加更多信息，包括一个在条目生命周期内保持不变的 UUID 编号、时间戳以及创建和修改该条目的用户名称。

## 向目录中添加条目

您可以使用许多工具（包括图形化工具和文本工具）来向 LDAP 目录添加信息并进行查询。本节介绍如何使用 `ldapmodify` 命令行实用程序来设置员工 LDAP 目录。其他工具的描述请参见第 767 页。

当您在 `ldapmodify` 命令行中指定以下文件时，`ldapmodify` 会向 LDAP 目录添加一个二级条目（位于 DSE 条目下方一级）。该文件添加了一个名为 `employees`（`ou=employees`）的 `organizationalUnit` 对象类。`DN` 是 `ou=employees` 后接 DSE。

```
$ cat sal.ldif
dn: ou=employees,dc=sobell,dc=com
changetype: add
objectClass: organizationalUnit
ou: employees
```

`sal.ldif` 的第一行指定要添加的条目的 `DN`。`changetype` 指令告诉 `ldapmodify` 将该条目添加到目录中。如果您在 `ldapmodify` 命令行上使用 `-a` 选项，或者使用 `ldapadd` 实用程序代替 `ldapmodify`，则可以省略此指令。`objectClass` 行指定该条目所属的对象类。`ou`（`organizationalUnitName` 的缩写）指定该条目所属组织单元的名称。

以下命令基于 `sal.ldif` 文件修改 LDAP 目录。`ldif` 文件扩展名通常用于存储 LDIF 条目的文件，但并非必需。

```
$ ldapmodify -D "cn=admin,dc=sobell,dc=com" -w porcupine -f sal.ldif
adding new entry "ou=employees,sobell,dc=com"
```

`-x` 选项使服务器使用简单认证。`-D` 后面的参数指定命令要处理的目录中 LDAP 管理员的 `DN`。通过指定此用户，该参数同时也指定了 LDAP 目录的 DSE。（LDAP 管理员条目的父项的 `DN` 指定了 DSE。）`-w` 后面的参数是 LDAP 管理员的密码。输入文件的名称位于 `-f` 选项之后。`ldapmodify` 实用程序报告新条目的 `DN`。

有了这个对象类，您就可以向 LDAP 目录中添加员工。以下文件添加了一名员工：

```
$ cat sa2.ldif
dn: cn=Samuel Smith,ou=employees,dc=sobell,dc=com
changetype: add
cn: Samuel Smith
cn: smith
objectClass: inetOrgPerson
mail: sls@example.com
givenName: Samuel
surname: Smith
displayName: Samuel L Smith
telephoneNumber: 999 999 9999
homePhone: 000 000 0000
initials: SLS
```

以下命令使用 `-W` 使 `ldapmodify` 提示输入 LDAP 管理员密码。在提示处指定密码而不是在命令行上指定，可以避免运行 `ps` 的用户看到密码，从而提高安全性。

```
$ ldapmodify -XD "cn=admin,dc=sobell,dc=com" -W -f sa2.ldif
Enter LDAP Password:
adding new entry "cn=Samuel Smith,ou=employees,dc=sobell,dc=com"
```

现在 `slapcat` 显示您刚刚添加的员工：

```
$ sudo slapcat
dn: dc=sobell,dc=com
---

dn: cn=Samuel Smith,ou=employees,dc=sobell,dc=com
cn: Samuel Smith
cn: smith
objectClass: inetOrgPerson
mail: sls@example.com
givenName: Samuel
sn: Smith
displayName: Samuel L Smith
telephoneNumber: 999 999 9999
homePhone: 000 000 0000
initials: SLS
---
```

`DN` 表明新员工位于目录结构的第三级：第一级是 `dc=sobell,dc=com`；`ou=employees,dc=sobell,dc=com` 位于第二级；而员工 `cn=Samuel Smith,ou=employees,dc=sobell,dc=com` 位于第三级。

您可以将任意数量的条目放入一个文件中，但每个条目必须与下一个条目用空行隔开。为了清晰起见，本节的示例每个文件显示一个条目。以下示例在第三级添加了另一名员工：
