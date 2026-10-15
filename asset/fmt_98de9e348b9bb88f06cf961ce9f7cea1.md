
我们需要以能够加载到 OpenLDAP 数据库中的格式来创建地址簿文件。我们所需的格式被称为 LDAP 数据交换格式（`LDIF`）。在此格式中输入的信息可用于构建数据库，也可用于从文件一次性向目录加载大量数据。

以下步骤解释了如何创建一个包含 `linuxtoys.net` 目录（区分名）地址簿定义的 `LDIF` 文件，然后将该文件加载到 LDAP 服务器中。

## 1. 创建 ldif 文件
作为 `root` 用户，使用任何文本编辑器，创建一个文件来容纳您的 LDAP 目录条目。在我的示例中，我使用了文件 `/etc/openldap/toypeople.ldif`。

> **注意：** 创建 `ldif` 文件时，务必在每个新的区分名（`dn:`）行之前保留一个空白行。空白行告知 `ldapadd` 开始一个新条目。如果没有空白行，LDAP 将不会认为您正在开始一个新的区分名。

## 2. 定义组织
您需要定义将加载到 LDAP 服务器中的目录。因此，在我的示例中，我在区分名 `linuxtoys.net` (`dc=linuxtoys,dc=net`) 下添加了定义组织为 Linux Toys 的信息，通过向我的 `toypeople.ldif` 文件中添加以下信息：

```
dn:                dc=linuxtoys,dc=net
objectClass: top
objectClass: dcObject
objectClass:	organization
dc:	linuxtoys
o:	Linux Toys
```

## 3. 添加组织角色
我通过向 `toypeople.ldif` 文件中添加以下行来识别地址簿管理员的角色。

```
dn:	cn=manager,dc=linuxtoys,dc=net
objectClass:	organizationalRole
cn:	Manager
description:	LinuxToys Address Book Administrator
```

## 4. 添加组织单元
由于在本例中，地址簿基本上由组织成员的名字和地址组成，我将组织单元（`ou`）命名为 `members`。

```
dn:	ou=members,dc=linuxtoys,dc=net
objectClass:	top
objectClass:	organizationalUnit
ou:	members
```

> **注意：** 虽然在我的示例中我创建的地址簿位于目录结构的顶部，但如果您在大型公司工作，很可能会想要更复杂的目录结构。例如，您可以在目录结构顶部只有一个地址簿，或者可以为国家、地点或部门创建额外的组织单元。然后，每个单元可能有自己的地址簿。您可能还希望支持每个单元下的多个目录。例如，可能会有一个单独的目录来跟踪计算机设备或公司车辆。

## 5. 添加人员
有了目录结构，并且在 `linuxtoys.net` 区分名下有了 `members` 单元，我就可以开始向目录中添加人员了。我将每个人定义为 `organizationalPerson` 和 `inetOrgPerson` 对象类。我可以为每个人的信息添加许多不同的属性。然而，我选择的大多数属性都是 Mozilla Mail 客户端（我将在本章稍后展示）将要读取的属性。以下是这两个条目：

```
dn:	cn=John Jones,ou=members,dc=linuxtoys,dc=net
objectClass:	organizationalPerson
objectClass:	inetOrgPerson
cn:	John Jones
mail:	jwjones@linuxtoys.net
givenname:	John
sn:	Jones
uid:	jwjones
o:	Linux Toys
telephoneNumber:	800-555-1212
homePhone:	800-555-1313
mobile:	800-555-1414
pager:	800-555-1515
facsimileTelephoneNumber: 800-555-1414
title: Account Executive
homePostalAddress: 1515 Broadway New York NY 99999

dn: cn=Sheree Glass,ou=members,dc=linuxtoys,dc=net
objectClass: top
objectClass: organizationalPerson
objectClass: inetOrgPerson
ou: members
cn: Sheree Glass
mail: sheree@linuxtoys.net
givenname: Sheree
sn: Glass
uid: siglass
o: Linux Toys
telephoneNumber: 800-555-2893
homePhone: 800-555-4329
mobile: 800-555-8459
pager: 800-555-4955
facsimileTelephoneNumber: 800-555-3838
title: Interior Decorator
homePostalAddress: 167 E Street Salt Lake UT 99999
```

如您在此所见，列在地址簿目录（称为 `members`）中的两个人各自与一个通用名称（`cn`）相关联。John Jones 和 Sheree Glass，它们位于 `linuxtoys.net` 域组件之下。您可以通过重复此结构向此文件中添加任意数量的人员。

> **注意：** 您可能会发现不需要这里显示的所有属性，或者希望添加其他属性。请参考架构文件，查看 `organizationalPerson`、`inetOrgPerson` 以及您可能希望在地址簿中使用的其他对象类所支持的属性列表。

## 6. 保存 ldif 文件
保存对 `ldif` 文件的更改（在我的情况下，文件名为 `/etc/openldap/toypeople.ldif`。）

## 7. 将信息添加到 LDAP 服务器
您可以使用 `ldapadd` 命令将您创建的 `ldif` 文件的全部内容添加到您的 LDAP 目录中。以下是我用于将我的 `ldif` 文件（名为 `toypeople.ldif`）的内容添加到我的 LDAP 目录的命令：

```
# ldapadd -x -D "cn=manager,dc=linuxtoys,dc=net" -W -f toypeople.ldif
Enter LDAP Password: mysecret
adding new entry "dc=linuxtoys,dc=net"

adding new entry "cn=manager,dc=linuxtoys,dc=net"

adding new entry "ou=members,dc=linuxtoys,dc=net"

adding new entry "cn=John Jones,ou=members,dc=linuxtoys,dc=net"
```

## 8. 重启服务器
此时，您可以通过输入以下内容来重启服务器：

```
/etc/init.d/ldap restart
```

## 9. 搜索目录
为了确保所有内容都已正确插入目录，您可以运行以下搜索命令：
