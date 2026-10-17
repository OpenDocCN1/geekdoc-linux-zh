
默认情况下，`yppasswd` 不允许用户更改其登录 shell 或 GECOS（第 1251 页）信息。您可以在启动 `yppasswd` 时通过命令行选项更改这些设置，或者更方便地通过修改 `/etc/sysconfig/yppasswd` 配置文件来更改。`yppasswd` 的 `--chfn` 选项允许用户更改其 GECOS 信息；`--e chfn` 允许用户更改其登录 shell。当您在 `/etc/sysconfig/yppasswd` 中设置这些选项时，每次运行 `yppasswd` 时这些值都会自动设置。以下示例使 `yppasswd` 接受端口 112 上的调用，并允许用户同时更改其 GECOS 信息和登录 shell：

```
# cat /etc/sysconfig/yppasswd
YPPASSWD_ARGS='--port 112 -e chfn -e chsh'
```

## LDAP

`LDAP`（轻量级目录访问协议）是较旧的 `X.500` `DAP`（目录访问协议）的替代方案。它运行在 `TCP/IP` 之上，具备网络感知能力，基于标准，并且可在许多平台上使用。客户端向 `LDAP` 服务器查询，并指定其所需的数据。例如，查询可以请求所有居住在旧金山且姓 `Smith` 的人的名和电子邮件地址。

由于 `LDAP` 旨在处理不频繁变化的数据，服务器保存了一个针对搜索和读取优化的数据库，称为*目录*。`LDAP` 客户端会查询并更新此目录。

除了姓名和地址信息外，`LDAP` 目录还可以存储网络服务列表。或者，其他服务可以将其用于身份验证。`LDAP` 适用于任何需要快速查找的相对静态的结构化信息。许多类型的客户端被配置为与 `LDAP` 服务器通信，包括专门的 `LDAP` 客户端（第 795 页）、电子邮件客户端和身份验证服务器。

`Fedora/RHEL` 提供 `LDAP` 的 `OpenLDAP` (`www.openldap.org`) 实现。`OpenLDAP` 使用 `Sleepycat` `Berkeley` `Database`（`Berkeley` `DB`，或 `BDB`，现归 `Oracle` 所有），它满足 `LDAP` 数据库的需求。它支持分布式架构、复制和加密。`BDB` 与关系型数据库 (`RDBMS`) 的不同之处在于，`BDB` 不将信息存储在行和列中，而是将 `LDAP` 目录实现为一种分层数据结构，将具有相似属性的信息分组在一起。本章描述 `OpenLDAP`。

除了 `BDB`，`Fedora/RHEL` 还提供 `HDB`（哈希数据库），它基于 `BDB`，但以真正的分层方式组织数据。`HDB` 比 `BDB` 提供更快的写入速度。它还支持子树重命名，允许在数据库内高效移动子树。

### 动态配置

在 `2.3` 版本发布之前，`OpenLDAP` 必须静态配置。这种设置对于拥有大型数据库的用户来说存在问题：每次修改配置时，都必须重启 `LDAP` 守护进程，这需要很长时间。`OpenLDAP` `2.3` 版本引入了运行时（动态或在线）配置。这种设置允许在不重启 `LDAP` 守护进程的情况下修改配置。虽然当前版本（`2.4`）仍允许静态配置，但未来趋势指向动态配置，这也是本章所描述的内容。

### Fedora/RHEL 目录服务器

除了 `OpenLDAP`，`Fedora` 提供 `389` 目录服务器（`389-ds` 软件包），`RHEL` 提供 `Red` `Hat` 目录服务器，两者都是 `LDAP` 服务器。更多信息请参见下一页的参考资料。

### 条目和属性

*条目*（`LDAP` 目录层次结构中的一个节点或容器）是 `LDAP` 目录中信息的基本单位。每个条目保存一个或多个*属性*。每个属性都有一个名称（属性类型或描述）和一个或多个*值*。属性名称来自一个标准模式，该模式存储在 `/etc/openldap/schema` 目录的文件中。此模式在多种 `LDAP` 实现中是标准的，使 `LDAP` 客户端能够从许多 `LDAP` 服务器获取数据。虽然通常没有必要也不建议这样做，但您可以增强或修改标准模式。

### DN 和 RDN

`DN`（可分辨名称）唯一标识 `LDAP` 目录中的每个条目。`DN` 由 `RDN`（相对可分辨名称）组成，`RDN` 由条目中的一个或多个属性构建而成，后跟父条目的 `DN`。由于 `DN` 可能会改变（例如，一位女性可能更改她的姓氏），且有时需要一致且唯一的标识符，服务器会为每个条目分配一个 *UUID*（第 1280 页）。

### DSE 和 DC

`DSE`（`DSA` 特定条目）是 `LDAP` 目录的根条目（也称为基、后缀或顶级条目）。（`DSA` 代表目录系统代理。）`DSE` 在名为 `/etc/openldap/slap.d/cn=config/olcDatabase={3}hdb.ldif` 的文件中定义。通常，`DSE` 和域名是相同的。`LDAP` 定义域名的组成部分。以下行定义了由 `DC` *brillserve* 和 `DC` *com* 组成的 `DSE`：

```
$ grep brillserve /etc/openldap/slap.d/cn=config/olcDatabase={3}hdb.ldif
olcSuffix: dc=brillserve,dc=com
```

### LDIF 和 CN

示例 `DSE` 指定的 `LDAP` 目录可能包含以下条目，该条目以 `LDIF`（`LDAP` 数据交换格式；有关更多信息，请参见 `ldif` 手册页）指定：

```
dn: cn=Sam the Great,dc=brillserve,dc=com
cn: Sam the Great
cn: the great
objectClass: inetOrgPerson
mail: sam@brillserve.com
givenName: Sam
sn: the Great
displayName: Sam the Great
telephoneNumber: 888 888 8888
homePhone: 111 111 1111
initials: SLS
```

除第一行外，每一行都指定一个属性。每行中冒号前的单词是属性名称。冒号和空格之后是属性值。本示例中的第一行指定了条目的 `DN`。`RDN` 中使用的属性值是条目中的一个 `CN`（通用名称）：`Sam the Great`。这个二级条目是顶级条目的子条目；因此，父条目的 `DN` 就是顶级条目的 `DN`（`dc=brillserve,dc=com`）。您可以使用其 `DN` 唯一标识此条目：`cn=Sam the Great,dc=brillserve,dc=com`。由于此条目定义了两个 `CN`，搜索 `Sam the Great` 或 `The Great` 都会返回此条目。此条目还定义了名字（`givenName`）、姓氏（`sn`）、电子邮件地址（`mail`）和其他属性。

- `objectClass` 属性：条目继承其父条目的对象类属性。此外，每个条目必须至少具有一个 `objectClass` 属性。每个 `objectClass` 值必须是模式中定义的类。模式指定了对象类的强制和可选 [允许] 属性。例如，模式中的以下条目定义了名为 `person` 的对象类。`MUST` 和 `MAY` 行指定了 `person` 对象类要求的属性（`sn` [姓氏] 和 `cn`；属性名称由美元符号分隔）以及可选属性（`userPassword`、`telephoneNumber`、`seeAlso` 和 `description`）。

```
$ cat /etc/openldap/schema/core.schema
...
objectClass ( 2 . 5 . 6 . 6  NAME 'person'
	DESC 'RFC2256: a person'
	SUP top STRUCTURAL
	MUST ( sn $ cn )
	MAY ( userPassword $ telephoneNumber $ seeAlso $ description ) )
...
```

- **缩写**：以下列表总结了本节中涵盖的缩写。
  - `CN` 通用名称
  - `DC` 域组件
  - `DN` 可分辨名称
  - `DSE` `DSA` 特定条目
  - `LDIF` `LDAP` 数据交换格式
  - `RDN` 相对可分辨名称

## 更多信息

- 本地手册页：`ldap.conf`、`ldapmodify`、`ldapsearch`、`ldif`、`slapd`、`slapd.conf`、`slappassword`
- `Web` `LDAP` 主页：`www.openldap.org`
- 管理员指南：`www.openldap.org/doc/admin24`
- `389` 目录服务器主页：`directory.fedoraproject.org`
- `Red` `Hat` 目录服务器手册：`access.redhat.com/site/documentation/`
- `Red_Hat_Directory_Server`（这些手册适用于 `Fedora` 和 `Red` `Hat` 目录服务器）
- `OpenLDAP` `Faq-O-Matic`：`www.openldap.org/faq`
- 书籍：`www.zytrax.com/books/ldap`
- `gq`：`sourceforge.net/projects/gqclient`
- `HOWTO` `LDAP` `Linux` `HOWTO`

## 配置 LDAP 服务器

本节说明如何配置 `LDAP` 服务器。

### 先决条件

安装以下软件包：

- `openldap-clients`
- `openldap-servers`

运行 `systemctl` 以启用 `LDAP` 守护程序 `slapd`（独立 `LDAP` 守护程序——这个缩写其实并不完全贴切），使系统在每次进入多用户模式时都启动 `slapd` 服务，然后启动 `slapd` 服务。使用 `systemctl status` 命令确保服务正在运行。在工具、服务和脚本的名称中，不要混淆 `ldap` 和 `slapd`。

```
# systemctl enable slapd.service
# systemctl start slapd.service
```

修改 `slapd` 配置文件后，再次运行第二条命令，但将 `start` 替换为 `restart`，以便 `slapd` 重新读取这些文件。

`Fedora/RHEL` 在安装 `openldap-servers` 软件包时不会加载内部 `LDAP` 模式。在创建数据库之前，必须手动执行此任务。使用 `root` 权限，运行以下命令以加载模式。该命令使用 `ldapadd` 处理 `/etc/openldap/schema` 目录中扩展名为 `.ldif` 的每个文件。它使用交互式 `for...in` 控制结构（第 995 页）。

```
# for file in /etc/openldap/schema/*.ldif
> do
> ldapadd -Y EXTERNAL -H ldapi:/// -f $file
> done
SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
adding new entry "cn=collective,cn=schema,cn=config"

SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
adding new entry "cn=corba,cn=schema,cn=config"
...
```

## 注意事项

您可以从 `www.sobell.com/RH7/code/chapter_21` 下载设置和运行本节描述的 `LDAP` 服务器所需的文件。

`slapd` `LDAP` 服务器通常使用未加密的 `TCP` 端口 `389`。如果将 `LDAP` 用于身份验证，请在端口 `636` 上使用 `SSL` over `LDAP`。如果服务器运行防火墙或位于防火墙之后，您需要打开其中一个端口。

运行以下命令以在系统每次启动时（永久地）以及在当前运行的系统上打开端口 `389`；有关 `firewall-cmd` 的信息请参见第 906 页。将 `389` 替换为 `636` 即可打开端口 `636` 而不是 `389`。

```
$ su -c 'firewall-cmd --add-port=389/tcp'
$ su -c 'firewall-cmd --permanent --add-port=389/tcp'
```

### 分步设置

本节列出了在 `brillserve.com` 域中设置 `LDAP` 服务器的步骤。当您设置 `LDAP` 服务器时，请在示例中用您要设置的服务器域名替换 `brillserve.com`。本节中的示例非常简单；您可能需要在使用目录设置不同的条目。

为了实验和学习 `LDAP`，请在本地设置并运行本节中描述的示例服务器。尽管示例使用了 `brillserve.com`，但在服务器系统上工作时，您可以将 `LDAP` 服务器称为 `localhost`。

### 配置服务器

按照上一页中的说明加载内部 `LDAP` 模式。

接下来，设置 `LDAP` 数据库、`brillserve` `DC`（域组件）以及 `ldadmin` `CN`（通用名称）。您可以按照“下载示例文件”（上一页）中的说明下载 `db.ldif` 文件。

```
$ cat db.ldif
dn: olcDatabase=hdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcHdbConfig
olcDatabase: hdb
olcDbDirectory: /var/lib/ldap
olcAccess: {0}to attrs=userPassword,shadowLastChange by self write by anonymous auth by dn="cn=ldadmin,dc=brillserve,dc=com" write by $ none
olcAccess: {1}to dn.base="" by $ read
olcAccess: {2}to $ by self write by dn="cn=ldadmin,dc=brillserve,dc=com" write by $ read olcLastMod: TRUE
olcDbCheckpoint: 512 30
olcDbConfig: {0}set_cachesize 0 2097152 0
olcDbConfig: {1}set_K_max_objects 1500
olcDbConfig: {2}set_LK_max_lockers 1500
olcDbConfig: {3}set_LK_max_lockers 1500
olcDbIndex: objectClass eq
#
#
# Set up brillserve admin with password
olcSuffix: dc=brillserve,dc=com
olcRootDN: cn=ldadmin,dc=brillserve,dc=com
olcRootPW: porcupine
```

`db.ldif` 文件的第一部分用于设置 `LDAP` 数据库。`olcSuffix` 行（`db.ldif` 中倒数第三行）定义了 `DSE`（可搜索目录树）[第 787 页]。`olcRootDN` 行确定了可以从 `LDAP` 目录中读取任何信息并向其中写入任何信息的用户（`LDAP` 管理员）。这一行的值是用户的 `DN`（可区分名称）。`RDN`（相对可区分名称）是 `LDAP` 管理员的名称；`DN` 包括父节点（在 `olcSuffix` 行中指定的 `DSE`）的 `DN`。在本例中，该用户的名称是 `ldadmin`（在 `db.ldif` 的倒数第二行中指定）。该用户是 `LDAP` 用户，不需要作为系统用户存在（即该用户无需列在 `/etc/passwd` 中）。`olcRootPW`（最后一行）为 `LDAP` 管理员设置密码。本例将 `porcupine` 设置为明文密码；在实际环境中，使用加密密码更安全（稍后将进行说明）。

以下命令使用 `root` 权限运行，使用 `ldapadd` 将 `db.ldif` 中的条目添加到数据库。

```
$ su -c 'ldapadd -Y EXTERNAL -H ldapi:/// -f db.ldif'
Password:
SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0, cn=peercred, cn=external, cn=auth
SASL SSF: 0
adding new entry "olcDatabase=hdb, cn=config"
```

如果您将通过网络管理 `LDAP`，请使用加密密码。首先使用 `slappasswd` 加密密码：

```
# slappasswd
New password:
Re-enter new password:
{{{SHA512}}7h060/qgeUrXl/Tsqy80lTbGYBOXdc/+
```

然后将 `slappasswd` 的输出复制到 `db.ldif` 中的新 `olcRootPW` 行：

```
olcRootPW: {{{SHA512}}7h060/qgeUrXl/Tsqy80lTbGYBOXdc/+
```

## 启动和测试服务器

按照第 789 页中的说明启动 `slapd` 守护程序。然后使用以下查询测试服务器：

```
$ ldapsearch -X -s base namingContexts
# extended LDIF
#
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectclass=*)
# requesting: namingContexts
#
#
dn:
namingContexts: dc=my-domain,dc=com
namingContexts: dc=brillserve,dc=com

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1
```
