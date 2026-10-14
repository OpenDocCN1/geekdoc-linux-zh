
# 列表25-2：Acme 的 LDIF 文件

```text
dn=oAcme,c=UK
o: Acme
objectClass: top
objectClass: organization

d=ou=Sales,o=Acme,c=UK
ou: Sales
objectClass: top
objectClass: organizationalUnit

d=ou=Marketing,o=Acme,c=UK
ou: Marketing
objectClass: top
objectClass: organizationalUnit

d=ou=IT,o=Acme,c=UK
ou: IT
objectClass: top
objectClass: organizationalUnit

d=ou=HR,o=Acme,c=UK
ou: HR
objectClass: top
objectClass: organizationalUnit

d=ou=Services,o=Acme,c=UK
ou: Services
objectClass: top
objectClass: organizationalUnit
```

# 第25 章 在 SUSE 中使用 LDAP

## 643

```text
dn: ou=Helpdesk,ou=IT,o=Acme,c=UK
ou: Helpdesk
objectClass: top
objectClass: organizationalUnit
```

```text
dn: ou=Architects,ou=IT,o=Acme,c=UK
ou: Architects
objectClass: top
objectClass: organizationalUnit
```

```text
dn: ou=Administrators,ou=IT,o=Acme,c=UK
ou: Administrators
objectClass: top
objectClass: organizationalUnit
```

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_687_0.png)

在创建 LDIF 文件时，确保记录数据后面没有尾随空格是非常重要的。人们在创建 LDAP 条目时一个常见的错误是留了尾随空格，在 LDAP 条目的情况下，这会在将其插入 LDAP 服务器时产生错误。LDAP 文件中看起来正确的数据与 LDAP 服务器中的数据并不相同。此外，LDAP 条目的顺序也是重要的。

除了 `ou`（组织单位）外，大多数条目都是相同的。我们通过这个文件理解这些条目意味着什么。

每个条目都有一个唯一的 DN，它们位于 LDAP 树中的各个组织单位。例如，这些 LDAP 目录说明了了 LDAP 服务器中的组织单位。我们希望通过这个看到它反映了 Acme 图表。每个条目定义了你向 LDAP 服务器的填充内容。

## 剖析对象

一个条目由 DN、被创建的对象（在本例中）以及类定义组成。`top` 类非常特殊，因为它所有的对象都应该属于它。这听起来很奇怪，但这意味着 LDAP 结构是完全模块化的，而不是硬编码的。

## 644 第四部分 在 SUSE Linux 中实现网络服务

`organizationalUnit` 类定义了作为组织单位的对象。许多其他的 `objectClass` 用于描述进入 LDAP 的各种对象。我们将在本章中遇到它们。

## 插入 LDIF 文件

当 LDIF 文件包含组织结构创建完成后，你需要将这些信息输入 LDAP 服务器。首先，确保你的 LDAP 服务器正在运行：

```bash
ldap:- # rcdldap status
Checking for ldap running
```

当 LDAP 服务器运行时，你需要添加条目（参见列表 25-3）。

> 25-3：向 LDAP 插入 LDIF 条目

```bash
# ldapadd -D "cn=admin,o=Acme,c=UK" -x -f /tmp/top.ldif
Enter LDAP Password:
adding new entry "ou=Acme,c=UK"

adding new entry "ou=Sales,o=Acme,c=UK"

adding new entry "ou=Marketing,o=Acme,c=UK"

adding new entry "ou=IT,o=Acme,c=UK"

adding new entry "ou=HR,o=Acme,c=UK"

adding new entry "ou=Services,o=Acme,c=UK"

adding new entry "ou=Helpdesk,ou=IT,o=Acme,c=UK"

adding new entry "ou=Architects,ou=IT,o=Acme,c=UK"

adding new entry "ou=Administrators,ou=IT,o=Acme,c=UK"
```

`ldapadd` 命令的使用方法与 `ldapsearch` 命令相似。你需要以管理员身份（`-D`）绑定，并使用简单验证（`-x`）让 `ldapadd` 运行。

用于密码的 `-w`。唯一的区别是使用 `-f` 参数来指定我们已经创建的 LDIF 文件的位置。如果一切顺利，LDIF 文件中的条目将被添加到 LDAP 服务器中。

现在你已经已经在 LDAP 服务器中拥有了组织结构，接下来需要向其中填充一些对象。

### 向 LDAP 服务器中添加用户数据

在创建 LDIF 文件之前，你需要定义你关于用户持有的哪些信息。由于你将使用这些信息来存储用户账户以及用户信息，因此你将使用 `inetOrgPerson`、`person`、`posixAccount`、`shadowAccount` 和 `organizationalPerson` 对象类。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_689_0.png)

你可以在 OpenLDAP schema 中找到更多关于可以在 LDIF 文件和 LDAP 服务器中使用的数据信息。这些架构文件位于 `/etc/openldap/schema`。

参考 `/etc/openldap/schema` 中的架构，你可以看到 `person` 对象类可以包含表 25-1 所示的信息。

### 表 25-1

person 对象类

| 元素 | 描述 |
|---|---|
| sn | 姓* |
| cn | 通用名* |
| UserPassword | 密码 |
| Telephone | 联系电话 |
| SeeAlso | 自由格式引用条目 |
| Description | 用户描述 |

*必须在对象类中

每个对象类都定义了每个对象可以包含的内容，这些信息定义在 LDAP 架构文件中。要需关于对象类中包含内容的更多信息，请查看 `/etc/openldap/schema` 中的架构文件。

现在你为为用户构建一个 LDIF 文件。在列表 25-4 中，我们详细列出了其中一个用户，以便你可以看到她的档案在该组织中看起来应该是什么样。

### 列表 25-4：Aimee Davies 的 LDIF 列表

```
dn: aimee,ou=Administrators,ou=IT,o=Acme,c=UK
uid: aimee
cn: Aimee Davies
givenName: Aimee
sn: Davies
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword: [crypt]ESlp8fJpWVEE
shadowLastChange: 12572
shadowMax: 99999
shadowWarning: 7
loginShell:/bin/bash
uidNumber: 1000
gidNumber: 100
homeDirectory:/home/aimee
telephoneNumber: 555-1027
o: UK
gecos: Aimee Davies
```

我们为管理员 Aimee Davies 构建了一个 LDIF 文件，其中包含了账户信息，允许她将 LDAP 数据作为 Unix 认证源。

为了构建初始 LDIF 文件，我们使用了 PWED 迁移工具将标准用户账户从 `/etc/passwd` 传输到 LDIF 的文件，并编辑该文件以添加关于组织和她电话号码的额外信息。

你可以将组织中的每个用户添加到反映组织架构图的特定组织单元。使用 `ldapsearch` 命令，你现在可以查看 LDAP 服务器中的数据（参见列表 25-5）。你使用 `-b` 选项告诉 `ldapsearch` 从 LDAP 树的 `o=Acme,c=UK` 基准开始搜索。这允许你搜索 LDAP 树的特定部分，而不是整个树。
