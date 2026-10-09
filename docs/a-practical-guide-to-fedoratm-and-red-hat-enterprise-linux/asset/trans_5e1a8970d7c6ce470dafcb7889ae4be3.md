
gmake[1]: 正在离开目录 '/var/yp/mg'  
plum 已被设置为 NIS 主服务器。  
现在您可以在所有从服务器上运行 `ypcd -s plum`。  
运行 `ypinit` 后，必须重启服务器（第 779 页）。

## 服务器故障排除

本节介绍了一些 NIS 服务器故障排除的方法。有关排查 NIS 客户端故障的技术，请参见第 776 页的“客户端故障排除”。

从服务器端检查 `ypserv` 是否已连接到 `rpcbind`：

```
$ rpcinfo -p | grep ypserv
100004  2  udp   114  ypserv
100004  1  udp   114  ypserv
100004  2  tcp   114  ypserv
100004  1  tcp   114  ypserv
```

再次从服务器系统确认 NIS 服务器已启动并正在运行：

```
$ rpcinfo -u localhost ypserv
program 100004 version 1 ready and waiting
program 100004 version 2 ready and waiting
```

如果服务器未正常工作，请使用 `systemctl` 停止 NIS 服务器。然后手动在后台启动 `ypserv` 并开启调试模式：

```
# systemctl stop ypserv.service
# ypserv --debug
[ypserv (ypserv) 2.31]

WARNING: no securenets file found!
ypserv.conf: files: 30
ypserv.conf: xfr_check_port: 1
ypserv.conf: 0.0.0.0/0.0.0.0::shadow.byname:2
ypserv.conf: 0.0.0.0/0.0.0.0::passwd.adjunct.byname:2
...
```

`--debug` 选项会使 `ypserv` 保持在前景运行，并将其错误消息和调试输出发送到标准错误流。当 `ypserv` 在前景运行时，按下 CTRL-C 即可停止它。

## yppasswd：NIS 密码更新守护进程

NIS 密码更新守护进程 `yppasswd` 仅在主服务器上运行；没有必要在从服务器上运行它。如果主服务器宕机且您尝试从客户端更改密码，`yppasswd` 将显示错误消息。当用户在客户端运行 `yppasswd`（第 777 页）时，该实用程序会与 `yppasswd` 守护进程交换信息，以更新 NIS shadow（可选包括 passwd）映射中以及 NIS 主服务器上的 `/etc/shadow`（可选包括 `/etc/passwd`）文件中用户的密码（以及其他可选信息）。密码更改请求会被发送到 `syslogd`（第 620 页）。

如果服务器系统正在运行防火墙，请为 `yppasswd` 开放一个端口。请参见第 780 页的“防火墙”。

### 启动 yppasswd

按照第 779 页的说明启动 `yppasswd`。

### 允许修改 GECOS 和登录 Shell

默认情况下，`yppasswd` 不允许用户更改其登录 shell 或 GECOS（第 1251 页）信息。您可以在启动 `yppasswd` 时通过命令行选项更改这些设置，或者更方便地通过修改 `/etc/sysconfig/yppasswd` 配置文件来更改。`yppasswd` 的 `--chfn` 选项允许用户更改其 GECOS 信息；`--e chfn` 允许用户更改其登录 shell。当您在 `/etc/sysconfig/yppasswd` 中设置这些选项时，每次运行 `yppasswd` 时这些值都会自动设置。以下示例使 `yppasswd` 接受端口 112 上的调用，并允许用户同时更改其 GECOS 信息和登录 shell：

```
# cat /etc/sysconfig/yppasswd
YPPASSWD_ARGS='--port 112 -e chfn -e chsh'
```

## LDAP

LDAP（轻量级目录访问协议）是较旧的 X.500 DAP（目录访问协议）的替代方案。它运行在 TCP/IP 之上，具备网络感知能力，基于标准，并且可在许多平台上使用。客户端向 LDAP 服务器查询，并指定其所需的数据。例如，查询可以请求所有居住在旧金山且姓 Smith 的人的名和电子邮件地址。

由于 LDAP 旨在处理不频繁变化的数据，服务器保存了一个针对搜索和读取优化的数据库，称为*目录*。LDAP 客户端会查询并更新此目录。

除了姓名和地址信息外，LDAP 目录还可以存储网络服务列表。或者，其他服务可以将其用于身份验证。LDAP 适用于任何需要快速查找的相对静态的结构化信息。许多类型的客户端被配置为与 LDAP 服务器通信，包括专门的 LDAP 客户端（第 795 页）、电子邮件客户端和身份验证服务器。

Fedora/RHEL 提供 LDAP 的 OpenLDAP (www.openldap.org) 实现。OpenLDAP 使用 Sleepycat Berkeley Database（Berkeley DB，或 BDB，现归 Oracle 所有），它满足 LDAP 数据库的需求。它支持分布式架构、复制和加密。BDB 与关系型数据库 (RDBMS) 的不同之处在于，BDB 不将信息存储在行和列中，而是将 LDAP 目录实现为一种分层数据结构，将具有相似属性的信息分组在一起。本章描述 OpenLDAP。

除了 BDB，Fedora/RHEL 还提供 HDB（哈希数据库），它基于 BDB，但以真正的分层方式组织数据。HDB 比 BDB 提供更快的写入速度。它还支持子树重命名，允许在数据库内高效移动子树。

**动态配置**
在 2.3 版本发布之前，OpenLDAP 必须静态配置。这种设置对于拥有大型数据库的用户来说存在问题：每次修改配置时，都必须重启 LDAP 守护进程，这需要很长时间。OpenLDAP 2.3 版本引入了运行时（动态或在线）配置。这种设置允许在不重启 LDAP 守护进程的情况下修改配置。虽然当前版本（2.4）仍允许静态配置，但未来趋势指向动态配置，这也是本章所描述的内容。

**Fedora/RHEL 目录服务器**
除了 OpenLDAP，Fedora 提供 389 目录服务器（389-ds 软件包），RHEL 提供 Red Hat 目录服务器，两者都是 LDAP 服务器。更多信息请参见下一页的参考资料。

**条目和属性**
*条目*（LDAP 目录层次结构中的一个节点或容器）是 LDAP 目录中信息的基本单位。每个条目保存一个或多个*属性*。每个属性都有一个名称（属性类型或描述）和一个或多个*值*。属性名称来自一个标准模式，该模式存储在 /etc/openldap/schema 目录的文件中。此模式在多种 LDAP 实现中是标准的，使 LDAP 客户端能够从许多 LDAP 服务器获取数据。虽然通常没有必要也不建议这样做，但您可以增强或修改标准模式。

**DN 和 RDN**
DN（可分辨名称）唯一标识 LDAP 目录中的每个条目。DN 由 RDN（相对可分辨名称）组成，RDN 由条目中的一个或多个属性构建而成，后跟父条目的 DN。由于 DN 可能会改变（例如，一位女性可能更改她的姓氏），且有时需要一致且唯一的标识符，服务器会为每个条目分配一个 *UUID*（第 1280 页）。

**DSE 和 DC**
DSE（DSA 特定条目）是 LDAP 目录的根条目（也称为基、后缀或顶级条目）。（DSA 代表目录系统代理。）DSE 在名为 `olcDatabase={3}hdb.ldif` 的文件中定义。通常，DSE 和域名是相同的。LDAP 定义域名的组成部分。以下行定义了由 DC *brillserve* 和 DC *com* 组成的 DSE：

```
$ grep brillserve /etc/openldap/slap.d/cn=config/olcDatabase={3}hdb.ldif
olcSuffix: dc=brillserve,dc=com
```

**LDIF 和 CN**
示例 DSE 指定的 LDAP 目录可能包含以下条目，该条目以 LDIF（LDAP 数据交换格式；有关更多信息，请参见 *ldif* 手册页）指定：

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

除第一行外，每一行都指定一个属性。每行中冒号前的单词是属性名称。冒号和空格之后是属性值。本示例中的第一行指定了条目的 DN。RDN 中使用的属性值是条目中的一个 CN（通用名称）：**Sam the Great**。这个二级条目是顶级条目的子条目；因此，父条目的 DN 就是顶级条目的 DN（**dc=brillserve,dc=com**）。您可以使用其 DN 唯一标识此条目：**cn=Sam the Great,dc=brillserve,dc=com**。由于此条目定义了两个 CN，搜索 *Sam the Great* 或 *The Great* 都会返回此条目。此条目还定义了名字（given name）、姓氏（sn）、电子邮件地址（mail）和其他属性。

- **objectClass 属性**：条目继承其父条目的对象类属性。此外，每个条目必须至少具有一个 **objectClass** 属性。每个 **objectClass** 值必须是模式中定义的类。模式指定了对象类的强制和可选 [允许] 属性。例如，模式中的以下条目定义了名为 *person* 的对象类。**MUST** 和 **MAY** 行指定了 *person* 对象类要求的属性（sn [姓氏] 和 cn；属性名称由美元符号分隔）以及可选属性（userPassword、*telephoneNumber*、*seeAlso* 和 *description*）。

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
  - **CN** 通用名称
  - **DC** 域组件
  - **DN** 可分辨名称
  - **DSE** DSA 特定条目
  - **LDIF** LDAP 数据交换格式
  - **RDN** 相对可分辨名称

## 更多信息

- 本地手册页：ldap.conf, *ldapmodify*, *ldapsearch*, ldif, slapd, slapd.conf, *slappassword*
- Web LDAP 主页：www.openldap.org
- 管理员指南：www.openldap.org/doc/admin24
- 389 目录服务器主页：directory.fedoraproject.org
- Red Hat 目录服务器手册：access.redhat.com/site/documentation/
- Red_Hat_Directory_Server（这些手册适用于 Fedora 和 Red Hat 目录服务器）
- OpenLDAP Faq-O-Matic：www.openldap.org/faq
- 书籍：www.zytrax.com/books/ldap
- gq：sourceforge.net/projects/gqclient
- HOWTO LDAP *Linux HOWTO*

