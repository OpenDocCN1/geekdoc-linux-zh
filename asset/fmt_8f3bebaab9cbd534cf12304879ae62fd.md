
```
dn: cn=Sam the Great,dc=brillserve,dc=com
cn: Sam the Great
cn: the Great
objectClass: inetPerson
mail: sam@brillserve.com
givenName: Sam
sn: The Great
displayName: Sam the Great
telephoneNumber: 888 888 888
homePhone: 111 111 1111
initials: SLS
```

除了第一行外，每行指定一个属性。每行冒号之前的单词是属性名称。冒号和空格之后是属性值。此示例中的第一行指定了该条目的 DN。RDN 中使用的属性值是该条目的 CN（通用名称）：Sam the Great。此二级条目是顶层条目的子级；因此，该条目的 DN 是顶层条目的 DN（`dc=brillserve,dc=com`）。你可以通过其 DN 唯一标识它：`cn=Sam the Great,dc=brillserve,dc=com`。

由于此条目定义了两个 CN，搜索 Sam the Great 或 Great 将返回此条目。该条目还定义了给定名、姓氏（`sn`）和电子邮件地址（`mail`）以及其他属性。

`objectClass` 从其父类继承对象类。此外，每个条目必须至少有一个 `objectClass`。每个 `objectClass` 必须是架构中定义的类。架构定义了对象类的强制性属性和可选（允许）属性。例如，架构中的条目定义了名为 `person` 的对象类。`MUST` 和 `MAY` 行指定了对象类所需的属性（`[sn]` 和 `cn`；属性之间用美元符号 `$` 分隔）以及哪些属性是可选的（`password, phoneNumber, seeAlso` 和 `description`）。

```
$ cat /etc/ldap/schema/core.schema
objectClass ( 2.5.6.6 NAME 'person' 
  DESC 'RFC2256: a person' 
  SUP TOP STRUURAL 
  MUST ( sn cn ) 
  MAY ( userPassword phoneNumber seeAlso description ) )
```

以下列表总结了本节提到的缩写词。

- `CN` 通用名称（Common Name）
- `DC` 域组件（Domain Component）
- `DN` 区分名（Distinguished Name）
- `DSE` DSA 特有条目（DSA-Specific Entry）
- `LDIF` LDAP 数据交换格式（LDAP Data Interchange Format）
- `RDN` 相对区分名（Relative Distinguished Name）

## 更多信息

本地页面：`ldap.conf`, `ldmapify`, `ldapsearch`, `ldif`, `slapd`, `slappasswd`

Web LDAP 主页：`www.openldap.org`

管理员指南：`www.openldap.org/doc/admin24`

389 Directory Server 主页：`directory.redhataproject`

Red Hat Directory Server 手册：`docs.redhat.com/docs/en-US/Red_Hat_Directory_Server/7.1/html/Administrators_Guide/TOC.htm`（这些手册适用于 Fedora 和 Red Hat Directory Servers）

OpenLDAP FAQ-O-Matic：`www.openldap.org/faq`

缩写词

778 第 21 章 NIS 和 LDAP

设置 LDAP 服务器 779

`book`：`www.zytrax.com/books/ldap`

`q`：`sourceforge.net/projects/ldap`

HOWTO

# 设置 LDAP 服务器

本节解释了如何设置服务器。

## 前决条件

安装以下软件包：

- `openldap-clients`
- `openldap-servers`

按照第 769 页“前决条件”下的说明启动 `slapd` 守护进程。使用以下查询测试服务器：

```bash
$ ldapsearch -x -s base namingContexts
# extended LDIF
#
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectclass*=)
# requesting: namingContexts
#
#
dn:amingContexts: dc=brillserve,dc=com

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1
```

命令行中的 `-x` 指定简单身份验证，`-s base` 指定搜索范围为基对象（base object），而 `namingContexts` 是你正在查找的属性。此命令的输出应与前一个示例所示类似。搜索返回的 `namingContexts` 应与你在配置服务器时指定的 DSE 相同。

### 向目录添加条目 (ADD ENTRIES TO THE DIRECTORY)

你可以使用许多图形化和文本工具向 LDAP 目录添加信息和进行查询。本节介绍了如何使用 `ldapmodify` 命令行工具设置员工 LDAP 目录。其他工具的描述请参阅第 784 页。

当你在 `ldapmodify` 命令中指定以下文件时，`ldapmodify` 会向目录添加一个二级条目（DSE 条目下方的）：

```bash
$ cat one.ldif
d=brillserve,dc=com
changetype: add
c=brillserve
objectClass: dcobject
objectClass: organization
organizationName: ZBr Associates Inc.
```

`ldif` 文件的第一行指定了要添加条目的根 DN。`changetype` 指令告诉 `ldapmodify` 将该条目添加到目录。如果你在 `ldapmodify` 命令行中使用 `-a` 选项，或者使用 `ldapadd` 工具代替 `ldapmodify`，则可以省略此行。以 `dc` 开头的行指定 DC（域组件）。`ObjectClass` 行指定了该条目所属的对象类。`organizationName` 指定了该条目**所属的组织名称**。

以下命令根据 `one.ldif` 文件修改 LDAP 目录。`.ldif` 文件扩展名很常见，但对于持有 LDAP 条目的文件来说并非必须的。

```bash
$ ldapmodify -Xd "cn=ldapadmin,dc=brillserve,dc=com" -w popcupine -f one.ldif
adding new entry: cn=brillserve,dc=com-
```

`-x` 选项允许服务器使用简单身份验证。`-D` 之后的参数指定了要操作的目录 LDAP 管理员的 DN（第 780 页步骤 b）。通过指定此用户，该参数也指定了 LDAP 目录的 DSE。LDAP 管理员条目父节点的 DN 指定了 DSE。`-w` 之后的参数是 LDAP 管理员的密码。为了更高的安全性，你可以使用 `-W` 让 `ldapmodify` 提示输入密码。`-f` 选项之后是输入文件的名称。`LDAPutil` 输出新条目的 DN。

`slapcat` 工具必须以系统 root 用户（而非 LDAP 目录管理员）身份运行，它以 LDIF 格式显示 LDAP 目录中的所有条目。执行完上述命令后，有一个条目：

```bash
$ su -c slapcat
dn: dc=brillserve,dc=com
dc: brillserve
objectClass: dcObject
objectClass: organization
o: Brill Associates Inc.
structuralobjectClass: organization
entryUID:34143f4-e4a9-102f-9480-97daa3d0714e
creatorName: cn=ldapadmin,dc=brillserve,dc=com
createTimestamp: 201103168502
entryCSN: 201103168502.7811962+0000000#000#00000
modifierName: cn=ldapadmin,dc=brillserve,dc=com
modifyTimestamp: 201103168502
```

`o` 属性名称是 `organizationName` 的缩写。服务器向条目添加了额外信息：在条目生存期间保持不变的 UUID 数字、时间戳以及创建和修改该条目的用户名。在本例中，他们是同一个人。
