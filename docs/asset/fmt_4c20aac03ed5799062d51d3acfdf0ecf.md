
## 设置后端

执行以下命令安装后端数据库：

```bash
$ sudo ldapadd -Y EXTERNAL -H ldap:/// -f backend.setup.ldif
```

输出应包含以下内容：

```
SASL/EXTERNAL authentication started
SASL username: gidnumber=0+uidnumber=0,cn=peercreed,cn=external,cn=auth
SASL SES:  0
adding new entry "cn=module,cn=config"
adding new entry "olcDatabase=hdb,cn=config"
```

## 设置前端

以下内容为示例数据库设置 `DSE`（`LDAP` 目录中的顶层条目；第 758 页）。请用您想要使用的域名替换 `dc=sobell,dc=com`。

```bash
$ cat t1.ldif

dn: dc=sobell,dc=com
changetype: add
objectClass: top
objectClass: dcObject
objectclass: organization
o: Sobell Associates
dc: Sobell
description: Sobell Example
```

执行以下命令将此信息添加到 `LDAP` 目录中：

```bash
$ ldapmodify -xD "cn=admin,dc=sobell,dc=com" -w porcupine -f t11.ldif

adding new entry "dc=sobell,dc=com"
```

接下来，设置一个管理员用户。请用您想要使用的密码替换示例中的 `porcupine`。

```bash
$ cat t12.ldif

dn: cn=admin,dc=sobell,dc=com
changetype: add
objectClass: simpleSecurityObject
objectClass: organizationalRole
cn: admin
description: LDAP administrator
userPassword: porcupine
```

执行修改命令：

```bash
$ ldapmodify -xD "cn=admin,dc=sobell,dc=com" -w porcupine -f t12.ldif

adding new entry "cn=admin,dc=sobell,dc=com"
```

## 测试服务器

在设置好数据库后端和前端后，使用以下查询测试服务器（您可能在执行此查询前需要重启）：

```bash
$ ldapsearch -x -s base namingContexts

# extended LDIF
# LDAPv3
# base <> (default) with scope baseObject
# filter: (objectClass=*)
# requesting: namingContexts
# dn:
namingContexts: dc=sobell,dc=com
# search result
search: 2
result: 0 Success
# numResponses: 2
# numEntries: 1
```

命令行上的 `-x` 指定简单身份验证，`-s base` 指定搜索范围为基准对象，而 `namingContexts` 是您正在搜索的属性。该命令的输出应与前面的示例所示类似。搜索返回的 `namingContexts` 应与您在设置前端时指定的 `DSE` 相同（第 762 页）。

`slapcat` 工具必须以特权用户（而非 `LDAP` 管理员）运行，它可以从 `slapd` 数据库检索信息并以 `LDIF` 格式显示（第 759 页）。尽管 `slapcat` 是一个非常有用的工具，但在用它备份数据库时请务必小心：在您进行备份时，其他用户可能会更改数据。`slapcat` 显示基础 `LDAP` 目录包含了本章前面章节设置的两个条目。

```bash
# sudo slapcat

dn:dc=sobell,dc=com
objectClass: top
objectClass: dcObject
objectClass: organization
o: Sobolev Associates
dc: Sobolev
description:U29iZlxswEVSYW1wbGg
structuralObjectClass: organization
entryUUID:42d495ba-0785-102f-8764-43c5bcc7e
creator:admin,dc=sobell,dc=com
startTimestamp:20100682007512
entryCSN:20100682007512.367377Z000000#000000
modifiersName:cn=admin,dc=sobell,dc=com
modifyTimestamp:20100682007512

dn:cn=admin,dc=sobell,dc=com
objectClass: simpleSecurityObject
objectClass: organizationalRole
cn: admin
description: LDAP administrator
userPassword::cc3yY3Waw51
```

每个条目的第一行指定了该条目的 `DN`。以 `dc` 开头的行指定 `DC`（域组件）。`objectClass` 行指定了该条目所属的对象类。以 `o`（`organizationName` 的缩写）开头的行指定了该条目所属组织的名称。

服务器会向条目添加更多信息，包括在条目生命周期内保持不变的 `UUID` 数字、时间戳以及创建和修改该条目的用户名称。

## 向目录添加条目

您可以使用许多图形化和文本化的工具向 `LDAP` 目录添加信息并进行查询。本节解释了如何使用 `ldapmodify` 命令行工具设置员工 `LDAP` 目录。其他工具的描述请参见第 767 页。

当您在 `ldapmodify` 命令行上指定以下文件时，该命令将向目录添加条目。以下示例显示了如何添加一个 `organizationalUnit` 条目。

```ldif
dn: dc=sobell,dc=com
changetype: add
objectClass: top
objectClass: dcObject
objectclass: organization
o: Sobell Associates
dc: Sobolev
description: Sobell Example
```

（注：原文提供的文本在中间部分存在大量重复和乱码，译文已根据逻辑进行了清理和翻译。）

# 第 21 章 NIS 和 LDAP

## 使用 Evolution 邮件客户端管理 LDAP 地址录

![新建地址录窗口，通用选项卡](img/45ff4cd21497435daa35084a84b95d07_818_0.png)
**图 21-1 新建地址录窗口，通用选项卡**

**通用选项卡**：从标记为 `Type` 的下拉列表中选择 `On LDAP Servers`。`Evolution` 将使用标记为 `Name` 的文本框中的内容来指代此 `LDAP` 目录；示例使用了 `employees`。在标记为 `Server` 的文本框中输入 `LDAP` 服务器的 `FQDN`。如果你在本地系统上进行实验，请在此框中输入 `localhost`。如果适用，请更改 `Port` 框中的值。为了遵循本章的示例，请在用于建立 `secure connection` 的下拉列表中选择 `No encryption`。

**详情选项卡**：接下来点击标记为 `Details` 的选项卡（图 21-2）。找到“Possible Search Bases”（可能的搜索基）。如果一切运行正常，`Evolution` 将显示“Supported Search Bases”（支持的搜索基础 [注：原文为 "Windows"，根据上下文可能是 OCR 错误，应为 "Bases" 或 "Windows" 指代搜索范围]）。高亮你想要使用的目录 `DN` 并点击 `OK`。`Evolution` 将选定的 `DN` 显示在 `Search base` 文本框中。在 `Search scope` 下拉列表中选择 `Sub` 以启用对目录所有层级的搜索。点击 `OK`。

接下来点击 `Mail-Evolution` 窗口左下角的 `Contacts` 按钮。在窗口左侧会有 `CouchDB`、`On this Computer` 和 `On LDAP servers`。如果你指定的地址录名称（示例中的 `employees`）未出现在 `On LDAP servers` 下方，请点击该标签左侧的加号 (+)。然后点击你想要操作的地址录名称。`Evolution` 会提示 `LDAP` 管理员密码。输入 `OK`。`Evolution` 会高亮地址录名称；你现在可以搜索 `LDAP` 数据库了。

在窗口右上角标记为 `Search` 的文本框中输入条目名称并按回车。`Evolution` 将显示该条目。图 21-3 显示了本章后续示例的结果，并在 `Search` 文本框中输入 `Sam`。

![新建地址录窗口，详情选项卡](img/45ff4cd21497435daa35084a84b95d07_819_0.png)
**图 21-2 新建地址录窗口，详情选项卡**

![联系人 - Evolution 窗口](img/45ff4cd21497435daa35084a84b95d07_819_1.png)
**图 21-3 联系人 - Evolution 窗口**

## 使用 Konqueror 浏览 LDAP 目录

如果你正在运行 `KDE`，可以使用 `Konqueror` 检查 `LDAP` 目录的内容。在 `Konqueror` 的位置栏中输入以下字符串并按回车：

```text
ldap://server-name/DN
```

其中 `server-name` 是 `LDAP` 服务器的名称或 IP 地址（如果你在服务器系统上运行 `Konqueror`，则使用 `localhost`），`DN` 是你想要查看的条目的 `DN`。`Konqueror` 会显示你指定的 `DN` 下的所有条目。双击条目以显示它。例如，要操作之前创建的 `LDAP` 目录，请在位置栏中输入 `ldap://localhost/ou=employee,dc=ibold,dc=com`。作为响应，`Konqueror` 将显示带有其 `RDN` 的条目。然后你可以点击这些条目之一来显示其实体。

## 本章总结

`NIS`（网络信息服务）通过将常用管理文件维护在中央数据库中，并让客户端连接数据库服务器检索信息，从而简化管理。`NIS` 服务的网络称为 `NIS` 域。每个 `NIS` 域有一个主服务器；网络则有从服务器。

`NIS` 提供的信息源自本地配置文件，例如 `/etc/passwd` 和 `/etc/hosts`。这些文件被称为源文件或主文件。`NIS` 可以存储源文件中包含的信息，但这些信息必须转换为 `dbm` 格式的文件，称为映射（`maps`）。`ypcat` 和 `ypmatch` 工具用于显示来自 `NIS` 映射的信息。

当你使用 `NIS` 进行密码身份验证时，`passwd` 工具（在客户端）替换了客户端上 `passwd` 的功能。`/etc/ypserv.conf` 文件存储了 `NIS` 服务器配置信息，指定了 `NIS` 服务器的选项和访问规则。为了增强安全性，你可以创建一个 `/var/yp/securenets` 文件，防止未经授权的系统检索 `NIS` 映射。

`LDAP`（轻量级目录访问协议）服务器持有一个针对搜索和读取优化的数据库，称为目录。`LDAP` 客户端（如电子邮件客户端）查询并更新此目录。此外，身份验证可以使用 `LDAP` 目录来验证用户。

`Ubuntu` 提供了 `LDAP` 的 `OpenLDAP` 实现。`OpenLDAP` 使用 `SQLite Berkeley Database`，它支持分布式架构、复制和加密。

## 练习题

1. `passwd` 和 `yppasswd` 工具之间的区别是什么？
2. 你如何防止 `NIS` 将 `root` 用户和其他系统用户导出到客户端？
3. 你如何让 `NIS` 用户信息覆盖客户端系统的本地用户信息？
4. 为什么 `/etc/passwd` 文件需要两个 `NIS` 映射？
5. `LDAP` 目录与关系型数据库系统有何不同？
6. `LDAP` 目录中的信息单位是什么？属性的结构是什么？

## 进阶练习题

7. 如何使用 `NIS` 镜像小型网络中私有 `DNS` 服务器的功能？为什么在大网络中不应这样使用 `NIS`？
8. 如何确定工作目录是否为 `NIS` 用户的家目录？
9. a. 使用 `NIS` 时提供了什么优势？b. 建议一种实现 `NIS` 的方法以便它们可以被索引。
10. `LDAP` 目录与关系型数据库系统有何不同？对象在哪里定义？
11. `LDAP` 目录中的信息单位是什么？属性的结构是什么？

# NFS 属性缓存与挂载选项

内核使用文件的修改时间来确定其缓存何时过期。如果属性缓存保存的时间晚于文件本身的修改时间，则缓存中的数据是新的。服务器必须定期刷新 `NFS` 挂载文件的属性缓存，用于判断另一个进程是否修改了该文件。对于普通文件和目录，此期间被指定为最小和最大秒数。以下是影响属性缓存的选项列表。

*   `ac` (`noac`) (**属性缓存**)：允许属性缓存（默认值）。`noac` 选项禁用属性缓存。虽然 `noac` 会减慢服务器速度，但它可以避免两个 `NFS` 客户端写入公共目录层级结构时出现过时属性。
*   `acdirmax=n` (**目录文件最大属性时间**)：`n` 是 `NFS` 在刷新目录属性之前等待的最长秒数（默认值为 60 秒）。
*   `acdirmin=n` (**目录文件最小属性时间**)：`n` 是 `NFS` 在刷新目录属性之前等待的最少秒数（默认值为 30 秒）。
*   `acremax=n` (**文件缓存最大属性时间**)：`n` 是 `NFS` 在刷新普通文件属性之前等待的最长秒数（默认值为 60 秒）。
*   `acremin=n` (**文件缓存最小属性时间**)：`n` 是 `NFS` 在刷新普通文件属性之前等待的最少秒数（默认值为 3 秒）。
*   `timeout=n` (**属性缓存超时**)：`n` 秒（如果没有此选项，`acregmax`、`acdirmin` 和 `acdirmax` 等单独选项将采用其分配的值或默认值）。

## 错误处理

以下选项控制当服务器未响应或发生 I/O 错误时 `NFS` 的处理行为。为了允许位于已挂载设备上的挂载点，缺失的挂载点被视为超时。

*   `fg` (`bg`) (**前台**)：在前台重试失败的 `NFS` 挂载尝试（默认值）。`bg`（后台）选项在后台重试失败的挂载尝试。
*   `hard` (`soft`)：在发生主超时时向控制台显示 `NFS` 服务器未响应并持续重试（默认值）。`soft` 选项在发生主超时时向调用程序报告 I/O 错误。通常，不建议使用 `soft`。正如挂载页所述，“它通常只会引起很多麻烦。” 更多信息请参阅第 780 页的“提高性能”。
*   `nointr` (`intr`) (**不中断**)：当发生主超时（`retrans`）时，不允许信号中断硬挂载目录层级结构上的文件操作（默认值）。`intr` 选项允许此类中断。
*   `retrans=n` (**重传值**)：`n` 分钟后，`NFS` 会产生主超时（默认值为 3）。主超时将中止操作或在控制台上显示服务器未响应，取决于设置的是 `hard` 还是 `soft`。
*   `retry=n` (**重试值**)：`NFS` 在放弃之前重试挂载操作的分钟（默认值为 10,000）。
*   `timeout=n` (**超时值**)：`n` 是 `NFS` 在发送后续 `RPC` 后重传（或发生次要超时）之前等待的十分之一秒（默认值为 7）。该值在每次超时时都会增加，最大为 60 秒，或直到发生主超时为止（见 `retrans`）。在网络繁忙、服务器较慢或请求通过多个路由器时，增加此值可能会提高性能。更多信息请参阅“超时”。

## 杂项选项

以下是其他一些有用的选项：

*   `lock` (`nolock`)：允许 `NFS` 锁定（默认值）。`nolock` 选项禁用 `NFS` 锁定（不启动锁定守护），对于不支持 `NFS` 锁定的旧版服务器有用。
*   `nodev` (**无设备**)：导致挂载的文件不作为设备运行（见第 777 页）。
*   `port=`：连接到 `NFS` 服务器时使用的端口（如果 `NFS` 守护进程未向 `portmap` 注册，默认为 2049）。当 `n` 设置为 0（默认值）时，`NFS` 查询服务器上的 `portmap` 以确定端口。
*   `rsize` (**读取块大小**)：从 `NFS` 服务器一次读取的字节数。默认块大小为 4096。参阅“提高性能”。
*   `wsize` (**写入块大小**)：一次向 `NFS` 服务器写入的字节数。默认块大小为 4096。参阅“提高性能”。
*   `tcp`：在 `NFS` 挂载中使用 `TCP` 协议代替 `UDP` 协议。此选项可能会提高拥塞网络上的性能；然而，某些 `NFS` 服务器仅支持 `UDP`。
*   `udp`：`NFS` 挂载使用默认的 `UDP` 协议。

## 提高性能

*   **hard/soft**：有几个参数会影响 `NFS` 的性能，特别是在慢速连接上，例如流量很多的线路或由调制解调器控制的线路。如果你有慢连接，请确保设置为 `hard`（见第 779 页，这是默认设置），以便超时不会中止程序执行。
*   **块大小**：提高 `NFS` 性能简单的方法之一是增加块大小——即每次传输的字节数。对于使用现代硬件的快速连接，4096 的默认值太低了。将 `rsize` 和 `wsize`（上述两者）增加到 8192 或更高。通过实验找到最佳块大小。每次更改选项时，请卸载并重新挂载目录层级。更多信息请参阅 `Linux-HOWTO`。
*   **超时**：`NFS` 等待 `timeout` 选项（见第 779 页）指定的时间以响应。如果没有及时收到响应，`NFS` 将再次发送传输。第二次传输使用的带宽在慢速连接上可能会导致速度更慢。你可以将 `timeout` 增加到最大 60 秒。记住，超时值是以十分之一秒为单位的（100 毫秒 = 十分之一）。

## /etc/fstab：自动挂载目录层级结构

`/etc/fstab`（见第 510 页）列出了系统在启动时自动挂载的目录层级结构。你可以在命令行或 `fstab` 文件中使用前面章节讨论的选项。

下行显示了 `fstab` 将来自 `dog` 的 `/grape/gc1` 文件系统挂载到 `/grape/gc1` 挂载点：

```text
dog:/grape/gc1 /grape/gc1 nfs 0 0
```
