

你可以使用 `slapcat` 来验证更改。最后一个示例从 LDAP 目录中删除 Helen：

```
$ cat sa3bd.1dif
dn: cn=Helen Simpson,ou=employees,dc=sobel1,dc=com
changetype: delete
```

```
$ ldapmodify -X D "cn=ldapadmin,dc=sobel1,dc=com" -w porcupine -f sa3bd.1dif
deleting entry "cn=Helen Simpson,ou=employees,dc=sobel1,dc=com"
```

## 用于处理 LDAP 的其他工具

你可以使用多种工具来处理 LDAP。例如，大多数电子邮件客户端都能从 LDAP 数据库中检索数据。

## EVOLUTION MAIL

本节介绍如何使用 Evolution（Mail）从前面创建的示例 LDAP 数据库中检索数据。假设你已经在本地系统上配置了 Evolution。如果你正在运行 KDE，你可以使用集成在许多 KDE 工具（包括 Kontact）中的 KAddressBook。

通过选择主菜单：应用程序⇒互联网⇒ Evolution Mail，或通过在终端模拟器或运行应用程序窗口（Alt+F2）中输入命令 `evolution`，打开 Mail-Evolution 窗口。要查询 LDAP 数据库，请从菜单栏中选择 文件⇒新建⇒ 地址簿。Evolution 将显示“新建地址簿”窗口的“常规”选项卡（图 21-1）。

![](img/f28adb66a7398a382f0505e0ba74a872_760_0.png)

从标记为“类型”的下拉列表中选择“On LDAP Servers”。在标记为“名称：”的文本框中输入 Evolution Mail 用于引用此 LDAP 目录的名称：示例使用 **employees**。在标记为 **Server** 的文本框中输入 LDAP 服务器的 FQDN。如果你是在本地系统进行实验，在此框中输入 **localhost**。如果适用，请更改标记为 **Port** 的文本框中的值。为了遵循本章中的示例，请从标记为 **Use secure connection** 的下拉列表中选择 **No encryption**。

在标记为 **Authentication** 的部分中，从标记为 **Login method** 的下拉列表中选择 **Using distinguished name (DN)**。在标记为 **Login** 的文本框中输入 LDAP 管理员的 DN（示例使用 **cn=ldapadmin,dc=soxell,dc=com**）。

![](img/f28adb66a7398a382f0505e0ba74a872_761_0.png)

接下来，点击标记为 **Details** 的选项卡（图 21-2）。点击 **Find Possible Search Bases**。如果一切正常，Evolution 将显示“支持的搜索基础”窗口。突出显示你想使用的目录的 DN，然后点击 **OK**。Evolution 将在标记为 **Search base** 的文本框中显示所选的 DN。从标记为 **Search scope** 的下拉列表中选择 **Sub**，以启用在目录所有级别的搜索。点击 **OK**。

接下来，点击 Mail-Evolution 窗口左下角的 **Contacts** 按钮。**On this computer** 和 **On LDAP** 服务器将出现在窗口的左侧。如果你指定的地址簿名称（示例中为 **employees**）未出现在 **On LDAP** 服务器下方，请点击该标签左侧的三角形。然后点击你想要处理的地址簿的名称。Evolution 会提示输入 LDAP 管理员密码。输入密码并点击 **OK**。Evolution 会突出显示地址簿的名称；你现在可以搜索 LDAP 数据库了。

在窗口右上角的“搜索”文本框中输入条目的名称，然后按 **RETURN**。Evolution 将显示该条目。下一页的图 21-3 展示了遵循本章示例并在“搜索”文本框中输入 **Mark** 后的结果。

![](img/f28adb66a7398a382f0505e0ba74a872_761_1.png)

**图 21-2** 新建地址簿窗口，“详情”选项卡

![](img/f28adb66a7398a382f0505e0ba74a872_762_0.png)

图 21-3  联系人 - Evolution 窗口

## KONQUEROR

如果你正在运行 KDE，你可以使用 Konqueror 来查看 LDAP 目录的内容。在 Konqueror 的位置栏中输入以下字符串并按 RETURN：

```
ldap://server-name/DN
```

其中 *server-name* 是 LDAP 服务器的名称或 IP 地址（如果你是在服务器系统上运行 Konqueror，则为 **localhost**），而 *DN* 是你想查看的条目的 DN。Konqueror 将显示你指定的 DN 下方的所有条目。双击一个条目以显示它。例如，为了处理前面创建的 LDAP 目录，请在位置栏中输入 `ldap://localhost/ou=employee,dc=sobell,dc=com`。作为响应，Konqueror 将显示具有此 RDN 的条目。然后你可以点击其中一个条目以完整显示该条目。

## GQ：一个 LDAP 客户端

gq 实用程序（gq-project.org）是一个图形化（基于 GTK+）的 LDAP 客户端，你可以使用它来显示、编辑和删除条目。它是 gq 包的一部分。在使用 gq 之前，你必须指定管理员的 DN。选择 **菜单栏: 文件→首选项**，点击“服务器”选项卡，突出显示服务器（示例中为 **localhost**），点击 **编辑**，点击 **连接** 选项卡，并将 **Bind DN** 设置为管理员的 DN（示例中为 **cn=ldapadmin,dc=sobell,dc=com**）。图 21-4 展示了 gq 显示示例 LDAP 目录中一个条目的情况。

你还可以使用 **gq** 来浏览模式：点击 **Schema** 选项卡，并从窗口左侧选择服务器（图 21-5 中为 **localhost**）。选择 **object-Classes**，然后选择一个对象类，以查看关于该对象类的信息，包括必需和可选属性的列表。

![](img/f28adb66a7398a382f0505e0ba74a872_763_0.png)

图 21-4 使用 gq 浏览 LDAP 目录

![](img/f28adb66a7398a382f0505e0ba74a872_763_1.png)

图 21-5 gq 的模式选项卡

## 本章摘要

NIS（网络信息服务）通过在中央数据库中维护通用管理文件，并让客户机联系数据库服务器以从数据库中检索信息，从而简化了这些文件的管理。NIS 服务的网络称为 NIS 域。每个 NIS 域都有一个主服务器；较大的网络可能有从服务器。

NIS 提供的信息源自本地配置文件，例如 /etc/passwd 和 /etc/hosts。这些文件被称为源文件或主文件。在 NIS 可以存储源文件中包含的信息之前，必须将其转换为 dbm 格式的文件，称为映射（maps）。ypcat 和 ypwhich 实用程序显示来自 NIS 映射的信息。

当你使用 NIS 来认证密码时，yppasswd 实用程序在客户机上取代了 passwd 的功能。保存 NIS 服务器配置信息的 /etc/ypserv.conf 文件指定了 NIS 服务器的选项和访问规则。为了增强系统安全性，你可以创建一个 /var/yp/securenets 文件，以防止未经授权的系统向 NIS 服务器发送 RPC 请求并检索 NIS 映射。

LDAP（轻量级目录访问协议）服务器持有一个为搜索和读取优化的数据库，称为目录。LDAP 客户端，如电子邮件客户端，会查询和更新此目录。此外，认证服务器可以使用 LDAP 目录来认证用户。

Fedora 和 RHEL 提供 OpenLDAP 的 LDAP 实现。OpenLDAP 使用 Sleepycat Berkeley 数据库，支持分布式架构、复制和加密。

## 练习

- 1. **passwd** 和 **yppasswd** 实用程序之间有什么区别？
- 2. 你如何防止 NIS 将 **root** 用户和其他系统用户导出到客户机？
- 3. 你如何让 NIS 用户信息覆盖客户机系统上的本地用户信息？
- 4. 为什么 /etc/passwd 文件需要两个 NIS 映射？
- 5. LDAP 目录与关系数据库系统有何不同？
- 6. LDAP 目录中信息的基本单位是什么？属性的结构是怎样的？

## 高级练习

- 7. 如何使用 NIS 为小型网络镜像私有 DNS 服务器的功能？为什么不应该在大型网络上以这种方式使用 NIS？
- 8. 如何确定工作目录是否是某个 NIS 用户的家目录？
- 9. 当你将 NIS 与 NFS 一起使用时，它提供了什么优势？
- 10. 建议一种实现 NIS 映射的方法，使其可以按多个字段进行索引。
- 11. LDAP 设备对象类在哪里定义？它的哪些属性是必需的，哪些是可选的？
- 12. 你如何确定小写“l”的 1 LDAP 对象类的较长名称？

