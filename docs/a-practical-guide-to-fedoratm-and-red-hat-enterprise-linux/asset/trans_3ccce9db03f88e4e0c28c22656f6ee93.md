

`o` 属性名是 `organizationName` 的缩写。

下一个文件向 LDAP 目录中添加了名为 `employees` 的对象类 `organizationalUnit`。其 DN 为 `ou=employees`，后接 DSE：

```
$ cat BB.ldif
dn: ou=employees,dc=brillserv,dc=com
changetype: add
objectClass: organizationalUnit
ou: employees
```

```
$ ldapmodify -x "cn=ldapadmin,dc=brillserv,dc=com" -w porcshine -f BB.ldif
adding new entry "ou=employees,dc=brillserv,dc=com"
```

在此对象类就位后，你可以向 LDAP 目录中添加员工。以下文件添加了一名员工：

```
$ cat CC.ldif
dn: cn=Zach Brill,ou=employees,dc=brillserv,dc=com
changetype: add
cn: Zach Brill
cn: brillserv
objectClass: inetOrgPerson
mail: zbrill@brillserv.com
givenName: Zach
surname: Brill
displayName: Zach Brill
telephoneNumber: 999 999 9999
homePhone: 000 000 0000
initials: ZCB
```

```
$ ldapmodify -x "cn=ldapadmin,dc=brillserv,dc=com" -w porcshine -f CC.ldif
adding new entry "cn=Zach Brill,ou=employees,dc=brillserv,dc=com"
```

现在 `ldapsearch` 显示了你刚刚添加的员工：

```
$ ldapsearch -x -LLL -b dc=brillserv,dc=com
dn: dc=brillserv,dc=com
objectClass: dcObject
...
dn: cn=Zach Brill,ou=employees,dc=brillserv,dc=com
cn: Zach Brill
cn: brillserv
objectClass: inetOrgPerson
mail: zbrill@brillserv.com
givenName: Zach
sn: Brill
displayName: Zach Brill
telephoneNumber: 999 999 9999
homePhone: 000 000 0000
initials: ZCB
```

DN 显示该新员工位于目录结构的第三级：第一级是 `dc=brillserv,dc=com`；`ou=employees,dc=brillserv,dc=com` 位于第二级；而员工 `cn=Zach Brill,ou=employees,dc=brillserv,dc=com` 位于第三级。

以下示例在第三级添加了另一名员工：

```
$ cat DD.ldif
dn: cn=Sam the Great,ou=employees,dc=brillserv,dc=com
changetype: add
cn: Sam the Great
objectClass: inetOrgPerson
mail: sam@brillserv.com
givenName: Sam
surname: the Great
displayName: Sam the Great
telephoneNumber: 888 888 8888
homePhone: 111 111 1111
initials: SLS
```

```
$ ldapmodify -x "cn=ldapadmin,dc=brillserv,dc=com" -w porcshine -f DD.ldif
adding new entry "cn=Sam the Great,ou=employees,dc=brillserv,dc=com"
```

下一个示例使用 `ldapmodify` 的 modify 指令来替换名为 Sam the Great 的员工的 `mail` 属性值，并为其添加一个 `title` 属性。单独的一行连字符用于分隔单个文件中的多个修改。由于文件指定了 Sam 的 DN，服务器知道要修改哪一条目。

```
$ cat EE.ldif
dn: cn=Sam the Great,ou=employees,dc=brillserv,dc=com
changetype: modify
replace: mail
mail: sls@brillserv.com
-
add: title
title: CTO
```

```
$ ldapmodify -x "cn=ldapadmin,dc=brillserv,dc=com" -w porcshine -f EE.ldif
modifying entry "cn=Sam the Great,ou=employees,dc=brillserv,dc=com"
```

你可以使用 `ldapsearch` 来验证该更改。最后一个示例从 LDAP 目录中删除了 Sam：

```
$ cat FF.ldif
dn: cn=Sam the Great,ou=employees,dc=brillserv,dc=com
changetype: delete
```

```
$ ldapmodify -x "cn=ldapadmin,dc=brillserv,dc=com" -w porcshine -f FF.ldif
deleting entry "cn=Sam the Great,ou=employees,dc=brillserv,dc=com"
```

## 用于处理 LDAP 的工具

你可以使用多种工具来处理 LDAP。例如，大多数电子邮件客户端都可以从 LDAP 数据库中检索数据。

### Evolution 邮件

本节介绍如何使用 Evolution（Mail）从前面创建的示例 LDAP 数据库中检索数据。在跟随本节示例之前，必须在本地系统上配置 Evolution。如果你只是想尝试使用 Evolution，可以使用如 `user@localhost` 这样的电子邮件地址进行设置。如果你正在运行 KDE，可以使用 KAddressBook，它集成在许多 KDE 工具中，包括 Kontact。

通过在终端模拟器或命令输入窗口（ALT+F2）中输入命令 `evolution` 来打开“邮件-Evolution”窗口。要查询 LDAP 数据库，请选择菜单栏：文件->新建->地址簿。Evolution 将显示一个新的“新建地址簿”小窗口。在标记为“类型”的下拉列表中选择“在 LDAP 服务器上”。Evolution 将显示“新建地址簿”窗口的“连接到 LDAP”选项卡（图 21-1）。

![](img/243613168ac865b539f12460d966088e_851_0.png)

**图 21-1** 新建地址簿窗口，连接到 LDAP 选项卡

![](img/243613168ac865b539f12460d966088e_852_0.png)

**图 21-2** 新建地址簿窗口，使用 LDAP 选项卡

在标记为“类型”的下拉列表中会出现“在 LDAP 服务器上”。在标记为“名称”的文本框中输入 Evolution 邮件将用于指代此 LDAP 目录的名称；本例使用 `employees`。在标记为“服务器”的文本框中输入 LDAP 服务器的 FQDN。如果你正在本地系统上进行实验，请在此框中输入 `localhost`。如果合适，请更改标记为“端口”的文本框中的值。要跟随本章的示例，请在标记为“加密”的下拉列表中选择“无”。

在标记为“身份验证”的部分中，从标记为“方法”的下拉列表中选择“使用特定名称（DN）”。在标记为“用户名”的文本框中输入 LDAP 管理员的 DN（本例使用 `cn=ldapadmin,dc=brillserv,dc=com`）。

接下来，点击标记为“使用 LDAP”的选项卡（图 21-2）。点击“查找可能的搜索基数”。如果一切正常，Evolution 将在标记为“搜索基数”的下拉列表中显示一个条目。选择你要使用的目录的 DN（本例使用 `dc=brillserv,dc=com`）。在标记为“搜索范围”的下拉列表中选择“子树”，以启用对目录所有层级的搜索。点击“确定”。

接下来点击“邮件-Evolution”窗口左下角的“联系人”按钮。“在 LDAP 服务器上”出现在窗口的左侧。如果你指定的地址簿名称（本例中为 `employees`）没有出现在“在 LDAP 服务器上”下方，请点击该标签左侧的三角形。然后点击你要使用的地址簿名称。Evolution 会提示输入 LDAP 管理员密码。输入密码（本例中为 `porcupine`）并点击“确定”。Evolution 会高亮显示地址簿的名称；现在你可以搜索 LDAP 数据库了。

![](img/243613168ac865b539f12460d966088e_853_0.png)

**图 21-3** 联系人，Evolution 窗口

在窗口右上角标记为“搜索”的文本框中输入条目的名称，然后按 RETURN 键。Evolution 将显示该条目。图 21-3 显示了跟随本章示例并在搜索文本框中输入 `Zach` 的结果。

### GQ：LDAP 客户端 (Fedora)

`gq` 实用工具（sourceforge.net/projects/gqclient；`gq` 包）是一个图形化（基于 GTK+）的 LDAP 客户端，你可以用它来显示和修改条目。通过在终端模拟器或命令输入窗口（ALT+F2）中输入命令 `gq` 来打开 GQ 窗口。在使用 `gq` 之前，你必须指定管理员的 DN。选择菜单栏：文件►首选项，点击“服务器”选项卡，高亮显示服务器 [本例中为 `localhost`]，点击“编辑”，点击“连接”选项卡，并在标记为“Bind DN”的文本框中输入管理员的 DN（本例中为 `cn=ldapadmin,dc=brillserv,dc=com`）。点击两次“关闭”。

点击“浏览”选项卡，并点击条目左侧的加号 (+) 以显示后续层级。点击 CN 条目以显示有关该 CN 的信息。图 21-4（下一页）显示了 `gq` 显示示例 LDAP 目录中条目的情况。

你还可以使用 `gq` 浏览架构：点击“架构”选项卡，并从窗口左侧选择服务器（图 21-5，下一页中的 `localhost`）。点击 `objectClasses` 左侧的加号 (+)，然后点击一个对象类以查看有关该对象类的信息，包括必需和可选属性的列表。

![](img/243613168ac865b539f12460d966088e_854_0.png)

**图 21-4** 使用 gq 浏览 LDAP 目录

## 章节摘要

NIS（网络信息服务）通过在一个中央数据库中维护通用管理文件，并让客户端联系数据库服务器以从数据库中检索信息，从而简化了这些文件的管理。NIS 所服务的网络称为 NIS 域。每个 NIS 域有一个主服务器；较大的网络可能有从服务器。

NIS 提供的信息源自本地配置文件，例如 `/etc/passwd` 和 `/etc/hosts`。这些文件称为源文件或主文件。在 NIS 能够存储源文件包含的信息之前，必须将其转换为 dbm 格式的文件，称为映射。`ypcat` 和 `ypmatch` 实用工具显示来自 NIS 映射的信息。

![](img/243613168ac865b539f12460d966088e_854_1.png)

**图 21-5** gq 的架构选项卡

