
```bash
[root@alpha ldap]# slaptest -u
58fe67c ldif_read_file: checksum error on "/etc/ldap/slapd.d/
cn=config/olcDatabase={2}hdb/olcOverlay={accesslog.ldif"
58fe67c UNKNOWN attributeDescription "STRUCTURALOBJECTCLASSSSS" inserted.
config file testing succeeded
```

# 第1章：从 OpenLDAP 开始

## 添加对象

现在我们必须在 LDAP 服务器中手动为 `dc=linuxolics,dc=com` 创建一个条目。此的最简单的方法是为该条目创建一个 LDIF 文件并将其传递给 `ldapadd` 命令。

因此，我们在常规位置 `/root/ldap/` 下创建一个名为 `linuxolics.ldif` 的文件，内容如下：

```
dn=linuxolics,dc=com
objectClass: dcObject
objectClass: organization
dc: linuxolics
o: linuxolics
```

我们指定了一系列属性，例如区分名称 `dn`、域组件 `dc` 和组织名称 `o`。我们还将新条目定义为 `dcObject` 和 `organization` 类型的对象。

根据我们创建的对象类型，有一系列属性可以是可选的或强制的。我们可以通过查询架构 `schema` 来检查这一点。例如，如果我们想知道在添加 `organization` 类型的对象时必须定义哪些属性，可以在架构中检查。我们应该去 `/etc/ldap/schema`，该目录下包含了定义 openLDap 架构的所有文件。如果我们不确定某个对象是在哪里定义的，可以使用 `grep` 命令。对于我们的示例来说，`organization` 对象定义在 `core.schema` 文件中，我们可以在其中找到如下的条目：

```
objectclass ( 2.5.6.4 NAME 'organization'
DESC 'RFC2256: an organization'
SUP top STRUCTURAL MUST o
MAY ( userSearchGuide $ seeAlso $ businessCategory $
x121Address $ registeredAddress $ destinationIndicator $
preferredDeliveryMethod $ telexNumber $ texasTerminalIdentifier $
telephoneNumber $ internationalDSNNNumber $
facsimileTelephoneNumber $ street $ postOfficeBox $ postalCode $
postalAddress $ physicalDeliveryName $ st $ 1 $ description )
```

如所示，在这种情况下，唯一的强制属性是 `o`。

现在执行 `ldapadd` 并将 `linuxaholics.ldif` 文件作为参数传递。我们指定了文件名 `-f`、管理员用户 `-D` 以及我们为该管理员定义的密码 `-w`。

```bash
[root@alpha ldap]# ldapadd -f linuxaxholics.ldif -D
cn=admin,dc=linuxaholics,dc=com -w pass
adding new entry "dc=linuxaholics,dc=com"
```

我们使用 `ldapsearch` 命令检查条目是否创建成功。

```bash
axholics,dc=com
# extended LDIF
#
# LDAPv3
# base <dc=linuxaholics,dc=com> with scope subtree
# filter: (objectclass=*)
# requesting: ALL
#
# linuxaholics.com
dn: dc=linuxaholics,dc=com
objectClass: dcObject
objectClass: organization
dc: linuxolics
o: linuxolics

# 搜索结果
search: 2
result: 0 Success

# numResponses: 3
# numEntries: 2
```

*(注：此处原文逻辑似乎存在重复或错乱，已根据上下文语义翻译)*

如我们所示，值已经根据我们在 LDIF 文件中指定的内容进行了更改。

另一个我们可以用来检查配置的有用工具是 `slaptest` 命令。

...

我们刚刚学习了如何将 `dc=linuxaholics,dc=com` 添加到我们的 LDAP 服务器中。现在我们将查看如何添加组织单元 `OU` 和组。

### 添加组织单元

我们可能想在 LDAP 中有一个名为 `users` 的组织单元 `OU` 来存储用户。为此，我们将创建一个名为 `users` 的 LDIF 文件，内容如下：

```
ou=users,dc=linuxaholics,dc=com
objectClass: organizational
```

我们执行 `ldapadd` 来创建该 OU。

```bash
[root@alpha ldap]# ldapadd -Y EXTERNAL -H ldapi:/// -f users.ldif -D cn=admin,dc=linuxaholics,dc=com -w pass
adding new entry "ou=users,dc=linuxaholics,dc=com"
```

### 添加用户

我们现在可以在 OU 内部添加用户。此过程与之前看到的非常相似。首先，创建一个名为 `tux.ldif` 文件，内容如下：

```
cn=Tux,ou=users,dc=linuxaholics,dc=com
objectClass: inetOrgPerson
objectClass: person
cn: Tux
sn: Tux
uid: tux
```

然后再次执行 `ldapadd`。

```bash
[root@alpha ldap]# ldap -Y EXTERNAL -H ldapi:/// -f tux.ldif -D cn=admin,dc=linuxaholics,dc=com -w pass
adding new entry "cn=Tux,ou=users,dc=linuxaholics,dc=com"
```

我们可能会收到此错误：

```
ldap_add: Invalid syntax
additional info: objectClass:(21)
```

这条消息意味着 `inetOrgPerson` 没有在架构中加载，因此我们必须包含它。在 `/etc/ldap/schema/` 文件夹中有许多 LDIF 文件可以扩展架构。我们将修改配置数据，以 root 用户身份进行验证。

```bash
[root@alpha ldap]# ldap -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/inetorgperson.ldif
```

如我们所示，我们得到了错误是因为属性类型未定义。因此我们也必须在架构中包含该定义。如果我们对 `/etc/ldap/schema/` 下的文件搜索字符串 `"audio"`，我们将看到该属性定义在 `cosine.ldif` 文件中。因此我们首先使用 LDIF 文件扩展架构。

```bash
[root@alpha ldap]# ldap -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/cosine.ldif
```

现在我们对 `inetorgperson.ldif` 执行同样的操作。

```bash
[root@alpha ldap]# ldap -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/inetorgperson.ldif
```

最后，我们添加之前创建的 `tux.ldif` 文件中的用户。

```bash
[root@alpha ldap]# ldap -f tux.ldif -x -D cn=admin,dc=linuxaholics,dc=com -w pass
adding new entry "cn=Tux,ou=users,dc=linuxaholics,dc=com"
```

## 第一章 启动 OPENLDAP

`olcTLSCertificateKeyFile`: `/etc/ldap/certs/password`

`structuralObjectClass`: `olcGlobal`

`entryUUID`: `bb3b82ec-4f85-1034-8587-e9dda2aed256`
