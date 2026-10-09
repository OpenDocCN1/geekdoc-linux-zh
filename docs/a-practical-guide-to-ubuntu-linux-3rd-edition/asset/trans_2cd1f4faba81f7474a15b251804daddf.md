

其名称是根据其组件部分命名的。以下行定义了由域名组件（DC）**soBell** 和 DC **com** 组成的 DSE：

```
$ sudo grep -r soBell /etc/ldap/
/etc/ldap/slapd.d/cn=config/olcDatabase={1}hdb.ldif:olcSuffix: dc=soBell,dc=com
...
```

**LDIF 和 CN** 示例 DSE 指定的 LDAP 目录可能包含以下条目，该条目以 LDAP 数据交换格式（LDIF；有关更多信息，请参阅 *Ldif* 手册页）指定：

```
dn: cn=Samuel Smith,dc=soBell,dc=com
cn: Samuel Smith
cn: Sam
cn: SLS
givenName: Samuel
sn: Smith
mail: sls@example.com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
```

除第一行外，每一行都指定一个属性。每行中冒号前面的单词是属性名称。冒号后面跟随一个**空格**，然后是属性值。本示例中的第一行指定了该条目的 DN。在 RDN 中使用的属性值是该条目中的一个 CN（**通用名称**）：**Samuel Smith**。这个二级条目是顶级条目的子条目；因此，父条目的 DN 是顶级条目的 DN（**dc=soBell,dc=com**）。你可以通过其 DN 唯一地标识此条目：**cn=Samuel Smith,dc=soBell,dc=com**。

由于该条目定义了三个 CN，搜索**Samuel Smith**、**Sam** 或 **SLS** 将返回此条目。此条目还定义了名字（given name）、姓氏（sn）和电子邮件地址（mail）。

**objectClass 属性** 条目从其父级继承对象类属性。此外，每个条目必须至少有一个 **objectClass** 属性（前面的条目有四个）。每个 **objectClass** 值必须是模式（schema）中定义的类。模式定义了对象类的必需和可选（允许）属性。例如，模式中的以下条目定义了名为 **person** 的对象类。MUST 和 MAY 行指定了 **person** 对象类需要哪些属性（**sn** [姓氏] 和 **cn**；属性名称由美元符号分隔）以及哪些属性是可选的（**userPassword**、**telephoneNumber**、**seeAlso** 和 **description**）。

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

- **CN** 通用名称（Common Name）
- **DC** 域名组件（Domain Component）
- **DN** 可区分名称（Distinguished Name）
- **DSE** DSA 特定条目（DSA-Specific Entry）
- **LDIF** LDAP 数据交换格式（LDAP Data Interchange Format）
- **RDN** 相对可区分名称（Relative Distinguished Name）

# 更多信息

本地手册页：ldap.conf, ldapmodify, ldapsearch, ldif, slapd, slapd.conf, slapasswd

- Web LDAP 主页：www.openldap.org
- 管理员指南：www.openldap.org/doc/admin24
- Ubuntu：help.ubuntu.com/10.04/serverguide/C/openldap-server.html
- OpenLDAP 常见问题解答生成器：www.openldap.org/faq
- 书籍：www.zytrax.com/books/ldap
- gg：gg-project.org

# 设置 LDAP 服务器

本节解释了设置 LDAP 服务器所涉及的步骤。

## 先决条件

安装以下软件包：

- slapd
- ldap-utils

**slapd 初始化脚本** 手动配置 slapd 后，调用 slapd 初始化脚本以重启 slapd：

```
$ sudo service slapd restart
Stopping OpenLDAP: slapd.
Starting OpenLDAP: slapd.
```

## 注意事项

**DB_CONFIG** 你可以修改 /var/lib/ldap/DB_CONFIG 文件中的参数以提高 LDAP 服务器的性能。请参阅 http://www.openldap.org/faq/data/cache/1072.html 网页以获取更多相关信息。还请参见本地系统中的 /usr/share/doc/slapd/examples/DB_CONFIG 和 /usr/share/doc/slapd/README.DB_CONFIG.gz 文件。

**防火墙** slapd LDAP 服务器通常监听 TCP 端口 389，该端口未加密。如果你使用 LDAP 进行身份验证，请使用端口 636 上的 LDAP over SSL。如果 LDAP 服务器系统正在运行防火墙，你需要打开其中一个端口。使用 gufw（第 876 页），通过添加允许客户端访问端口 389 或端口 636 服务的规则来打开其中一个端口。

## 设置服务器

**后端** OpenLDAP 使用目录信息树（DIT）层次结构，其根位于 `/etc/ldap/ldap.d/cn=config`（等号是目录名称的一部分），以配置 **slapd** 守护进程。此设置允许动态配置 **slapd** 守护进程（无需重启守护进程）。在你向 LDAP 数据库添加用户数据之前，必须配置此 DIT，即**后端**。

**前端** 数据库的前端也需要在添加用户数据之前进行配置。你必须将其设置为持有用户想要存储的数据类型。第 762 页的“设置前端”描述了如何设置与许多地址簿应用程序兼容的数据库。

一旦你设置了后端和前端，你就可以按照第 764 页的“向目录添加条目”一节中所述的方法添加用户数据。

本节列出了在 **sobell.com** 域中设置 LDAP 服务器所涉及的步骤。当你设置 LDAP 服务器时，在示例中将你正在设置的服务器域名替换为 **sobell.com**。

为了实验和学习 LDAP，请在本地设置并运行本节中描述的示例服务器。尽管示例使用的是 **sobell.com**，但当你从服务器系统工作时，可以将 LDAP 服务器称为 **localhost**。

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

以下文件将使用包含 DC **sobell** 和 DC **com**（第 758 页）的 DSE 以及名为 **admin**、密码为 **porcupine** 的管理员用户来设置 LDAP 数据库的后端。根据你正在设置的数据库更改这些值。（注意倒数第四行很长，在以下显示中进行了换行。此文件可在 Web 上的 www.sobell.com/UB3/code/chapter_21/backend.setup.ldif 获取。）

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

以下文件为示例数据库设置 DSE（LDAP 目录中的顶级条目；第 758 页）。用你想使用的域名替换 dc=sobell,dc=com。

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

