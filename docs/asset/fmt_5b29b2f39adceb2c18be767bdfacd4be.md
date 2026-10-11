
进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在表达式 `cvar = avar + bvar` 中，加法运算符（`+`）将 `avar` 与 `bvar` 相加，得到它们的和 `cvar`

在 `List.of(arg0, arg1, arg2)` 中，`List` 接口的工厂方法 `of()` 接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用 `cmd` 命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

## 3. 在 Fedora、RHEL 和 Centos 发行版中，使用 `service` 命令启动 `winbindd` 守护进程。输入

## 使用 `net` 命令将 Samba 服务器加入 Windows 域。假设 Windows 员账户密码已知，输入
```
[root@serverA -]# rpc join -U root% windows_administrator
```
已加入域 `WINDOWS-DOMAIN`

其中 Microsoft Windows 域中具有权限加入系统的账户的密码为 `windows_administrator.password`。

## 使用 `winfo` 工具列出 Windows 域中所有可用用户，以确保一切运行正常。输入
```
[root@serverA -]# winfo -u
```

## SAMBA 故障排除

以下是在使用 Samba 时可能会遇到的一些简单问题的典型解决方案：

- 重启 Samba：这可能是必要的，因为 Samba 进入了未定义状态，或者（更有可能）你对配置进行了更改但忘记重新加载 Samba 以使更改生效。
- 确保配置选项正确：`smb.conf` 文件中的错误通常出现在目录名、用户名、网络号和主机名中。一种常见的错误是当新客户端添加到对服务器具有特殊访问权限的组时，但 Samba 未被告知所添加客户端的名称。不要忘记语法类型错误，`testpalm` 工具是你的助手。
- 监控加密密码：这些密码可能不匹配——服务器配置为使用加密密码而客户端也是如此，或者（更有可能）客户端正在使用加密密码，而 Samba 未配置为使用它们。如果你急于让客户端运行，可以使用 Samba 源码中附带的 `regedit` 脚本禁用客户端加密（参见 `docs` 子目录）。

## 总结

在本章中，我们讨论了编译、安装和配置 Samba 的过程，以便您的 Linux 服务器能够与基于 Windows 网络集成。Samba 是一个强大的工具，具有替代专用文件和打印机的 Microsoft Windows 服务器的潜力。

阅读大量的文档可能不是你度过时光的最喜欢的方式，但你会发现 Samba 文档是完整、有帮助且易于阅读的。

# Linux 管理：入门指南

至少浏览一下这些文件看看里面有什么，这样当你需要时，就知道该去哪里获取额外信息。有了今天可用的所有 Samba 文本（有些免费，有些不免费），你应该拥有配置即使是最复杂的设置所需的一切。立刻就会想到两本关于 Samba 所有内容的优秀书籍：John Terpstra 写的《Samba-3 by Example》，以及 John Terpstra 和 Jelmer Vernooij 写的《The Official Samba-3 HOWTO and Reference Guide》，由 Prentice Hall 出版（2004年3月）。这些书有印刷版和电子版。书籍的在线版本可以在 `www.samba.org` 找到。

## 第 25 章

## LDAP

# Linux 管理：入门指南

轻量级目录访问协议（LDAP）被称为过许多事物，包括“切片面包以来最好的发明”。但它实际上是一组开放协议，用于通过网络访问和修改中央存储的信息。LDAP 基于 X.500 标准（X.500 是一个国际标准组织 [ISO] 标准，定义了目录服务的整体模型），但它是原始标准的更轻量级版本。RFC 2251 解释了它。

LDAP 由密歇根大学于 1992 年开发，作为 X.500 的轻量级替代方案。LDAP 是可扩展的，相对容易实现，并且基于开放标准。

## LDAP 基础

LDAP 是一项全局目录服务。它特别适用于读取、搜索和浏览操作。以下是一些流行的实现：

- OpenLDAP，一种开放 LDAP
- Novell 的 NetWare Directory Service (`eDirectory`)
- Microsoft 的 Active Directory
- iPlanet Directory Server（这曾在 Sun 和 Netscape 之间拆分。Netscape Directory 被 Red Hat 收购，随后将其向开放社区。）
- IBM 的 SecureWay Directory

## LDAP 目录

与流行的域名命名系统 (DNS) 一样，LDAP 中的目录条目按分级树排列。在大多数分级结构中，树越深，存储的内容就越精确。LDAP 的分级结构被称为目录信息树 (`DIT`)。目录的顶部是根元素。标识结构中任何节点的完整路径被称为该节点的区别名 (`DN`)。

再次，就像 DNS 一样，LDAP 目录的结构通常反映地理和/或组织边界。地理边界可以是国界、州界、市界等。组织边界可以沿着职能线、部门线或组织单元。

例如，名为 Example, Inc. 的公司可能决定使用基于域的命名结构来构建其目录树。该公司内部可能有不同的划分（组织单元，OU），例如工程部、销售部和研发部。此类公司的 LDAP 目录树如图 25-1 所示。

图中示例对象的 DN 为“`dn: uid=yyang,ou=sales,dc=example,dc=org.`”

## 客户端/服务器模型

与其他服务一样，LDAP 遵循典型的客户端/服务器模式。客户端与服务器之间的典型交互如下：

- LDAP 客户端应用程序连接到 LDAP 服务器。这被称为“绑定服务器”。
- 根据服务器上配置的访问限制，LDAP 服务器接受或拒绝绑定/连接请求。假设它接受了……
- 客户端可以选择查询目录服务器、浏览存储在服务器上的信息，或尝试修改/更新 LDAP 服务器上的信息。
- 同样，在访问限制方面，服务器可以允许或拒绝客户端尝试的任何操作。如果服务器无法回答请求，它可能会将客户端转发或引用到另一个上游 LDAP 服务器，该服务器可能对该请求有更具权威性的响应。

## LDAP 的用途

LDAP 是一种分布式目录服务，可以作为各种类型信息的存储器。LDAP 目录可以存储几乎任何类型的信息——其性质非常多样，如纯文本信息、图像、二进制数据或公钥证书。

多年来，人们创建了各种 LDAP 架构（schemas），以便在 LDAP 目录中存储不同的数据源。以下是 LDAP 的用途示例：

- LDAP 可以作为组织的完整身份管理解决方案。它可以为用户提供身份验证和授权服务。事实上，网络信息服务（NIS）提供的服务完全被 LDAP 代替了。
- DNS 记录中的存储的信息可以存储在 LDAP 中。
- LDAP 可为组织（实例）提供“黄页”服务。
- 邮件路由信息可以存储在 LDAP 中。
- 存在一种 Samba 架构允许 Samba 服务器在 LDAP 中存储扩展属性。这使得 Samba 在需要冗余和复制的环境中可以作为 Microsoft Windows NT 域控制器的稳健替代方案。

## LDAP 术语

如果你打算精通 LDAP 术语，那么最好了解基本的 LDAP 技术术语。在本节中，我们尝试定义一些你在处理 LDAP 时经常会遇到的术语：

- Entry（条目，或对象）：这是 LDAP 目录中的一个单元。每个条目都由其特异性名称（DN）来限定，例如“`dn: uid=yyang,ou=sales,dc=example.`”。
- Attributes（属性）：这些是与条目关联的信息，例如组织的地址或人员的电话号码。

## 第 25 章：LDAP

- `objectClass`：这是一种特殊类型的属性。LDAP 中的所有对象都必须有一个 `objectClass` 属性。`objectClass` 定义规定了每个 LDAP 对象所需的属性。它指定了条目的对象类。该属性的值可以被客户端修改，但 `objectClass` 属性本身不能被删除。

`objectClass` 定义本身存储在架构文件（`schema files`）中。

- Schema（架构）：架构是规则的集合，决定了目录的结构和内容。架构包含属性类型定义、对象类定义等。

架构列出了每个对象类型的属性以及这些属性是必选还是可选的。架构通常存储在文本文件中。

架构的示例：

- `core.schema`：定义了基本的 LDAPv3 属性和对象。它是 OpenLDAP 实现中强制的核心架构。
- `inetOrgPerson.schema`：定义了 `inetOrg` 对象类及其关联属性。该对象用于存储人员的联系信息。

- `LDIF` 代表 LDAP 数据交换格式（LDAP Data Interchange Format）。它是用于 LDAP 条目的纯文本文件。向 LDAP 服务器导入或导出数据的文件必须是这种格式。用于 LDAP 服务器之间复制的数据也采用这种格式。

# OPENLDAP

OpenLDAP 是运行在 Linux/UNIX 系统上的 LDAP 的开源实现版本。OpenLDAP 是一套由以下组件组成的程序包：`slapd`、`slurpd` 和库，它们实现了 LDAP 协议，以及各种客户端和服务器端实用程序。

## 服务端守护进程

服务端由两个主要的守护进程组成：

- `slapd`：这是一个独立的 LDAP 守护进程。它监听来自客户端的 LDAP 连接，并响应通过这些连接收到的 LDAP 操作。
- `slurpd`：这是一个独立的 LDAP 复制守护进程。它用于将更改从一个数据库传播到另一个。它是用于将更改从一个 LDAP 服务器同步到另一个 LDAP 服务器的守护进程。只有在使用多个 LDAP 服务器时才需要它。

## OpenLDAP 实用程序

OpenLDAP 实用程序是一组命令行工具，用于查询、查看、更新和修改存储在 OpenLDAP 目录中的数据。在 Fedora Core 系统和 Red Hat Enterprise Linux (RHEL) 上，这套程序由 `openldap-clients*.rpm` 软件包提供，其中一些由 `openldap-server*.rpm` 软件包提供。程序列如表 25-1 所示。

## 安装 OPENLDAP

为了让 OpenLDAP 服务器和客户端组件运行起来，在 Fedora、RHEL 和 Centos 系统上需要这些包：

- `openldap-*.rpm`：为 Open-LDAP 提供配置文件和库。
- `openldap-clients*.rpm`：提供访问和修改 OpenLDAP 目录所需的客户端程序。
- `openldap-servers*.rpm`：提供配置和运行 LDAP 所需的服务器（`slapd`，`slurpd`）和其他实用程序。

> 提示：如果你只配置客户端，则不需要 `openldap-servers*.rpm` 包。

我们使用 `yum` 程序在示例系统中自动下载并安装 `open-ldap-servers` 包。步骤如下：

1. 以 root 身份登录时，首先通过查询红帽包管理器（RPM）数据库确认你已经安装了哪些包。
```bash
