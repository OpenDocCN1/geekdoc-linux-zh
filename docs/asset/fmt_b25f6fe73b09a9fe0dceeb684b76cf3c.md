
当软件包的新版本发布时，安装它到系统中非常容易。从可用软件包窗口中选择软件包的方式与您选择要安装的软件包的方式相同。工具栏上的升级按钮以及菜单中操作 => 升级都将开始该过程。您只需以安装新软件包相同的方式添加软件包。

在升级期间，您会看到类似于安装软件包时的进度指示器。完成后，旧版本的软件包将被移除，除非您另行指定（更多信息请参见第 7.4 节 配置）。

使用升级选项比卸载旧版本的软件包然后安装新版本要好得多。使用升级可以确保您对软件包配置文件所做的更改得到妥善保留，而卸载然后重新安装新软件包可能会导致这些更改丢失。

如果在安装过程中磁盘空间不足，安装将失败。但是，发生错误时正在安装的软件包可能会留下一些文件。为了清理此错误后的残留，请在腾出更多磁盘空间后重新安装该软件包。

## 8 轻量级目录访问协议（LDAP）

### 8.1 什么是 LDAP？

`LDAP`（轻量级目录访问协议）是一个用于网络上的全局或本地目录服务和/或互联网上的建议开放标准。目录在此意义上非常像电话簿。`LDAP` 可以处理其他信息，但目前通常用于将姓名与电话号码和电子邮件地址相关联。目录被设计用于支持大量查询，但目录中的数据并不经常更改。

`LDAP` 比纸质电话簿更有用得多，因为 `LDAP` 的设计旨在支持在 Internet 范围内的 `LDAP` 服务器之间的传播，就像域名服务（`DNS`）一样。`DNS` 系统充当互联网的地址簿，通过跟踪域名/IP 地址对来工作。`DNS` 服务器告诉联网的机器数据包需要去往哪里。在未来，`LDAP` 可以为许多类型的目录信息提供相同类型的全球访问；目前，`LDAP` 更常用于单个大型组织，如大学或公司，用于目录服务。

`LDAP` 是一个客户端-服务器系统。`LDAP` 客户端连接到 `LDAP` 服务器，并查询信息或提供需要输入到目录中的信息。服务器要么回答查询，将查询转交给另一个 `LDAP` 服务器，要么接受信息以整合到目录中。

`LDAP` 有时被称为 `X.500 Lite`。`X.500` 是目录的国际标准。`X.500` 功能齐全，但复杂且需要大量的计算资源和完整的 `OSI` 堆栈。相比之下，`LDAP` 可以轻松地运行在 `PC` 上并通过 `TCP/IP`。`LDAP` 可以访问 `X.500` 目录，但它不支持 `X.500` 的所有功能。

本章将讨论 `OpenLDAP` 的配置和使用，`OpenLDAP` 是 `LDAP` 的一个开源实现。`OpenLDAP` 包括 `slapd`，一个独立的 `LDAP` 服务器；

`slurpd`，一个独立的 `LDAP` 复制服务器；实现 `LDAP` 协议的库；实用程序；工具；以及示例客户端。

### 8.2 LDAP 的优缺点

使用 `LDAP` 的主要好处是将组织内某些类型的信息整合在一起。例如，组织内所有不同的用户列表可以合并到一个 `LDAP` 目录中。任何需要此信息的 `LDAP` 启用应用程序都可以查询该目录。用户也可以使用目录来获取目录信息。

`LDAP` 的其他优势包括其实现的简便性（与 `X.500` 相比），以及其定义良好的应用程序编程接口（`API`），这意味着拥有 `LDAP` 功能的应用程序和 `LDAP` 网关的数量在未来应该会增加。

从负面角度看，如果你想使用 `LDAP`，你需要支持 `LDAP` 的应用程序或者需要使用 `LDAP` 网关。如前所述，`LDAP` 的使用量将会增加，但目前，并没有大量支持 `LDAP` 的应用程序可用于 Linux 系统。此外，虽然 `LDAP` 支持一些访问控制，但它不支持像 `X.500` 那样多的安全特性。

### 8.3 LDAP 的用途

包括 Netscape Roaming Access 在内的多个 Netscape 应用程序都支持 `LDAP`。`Sendmail 8.9.x` 可以使用 `LDAP` 查找地址。你的组织可以使用 `LDAP` 作为全组织范围的目录和/或名称服务（替代 `NIS` 或平面文件）。你甚至可以使用个人 `LDAP` 服务器来管理自己的电子邮件地址簿（参见第 8.10 节，网络上的 LDAP 资源）。

可以通过 `pam_ldap` 模块将 `LDAP` 用作认证服务。`LDAP` 通常用作中央认证服务器，以便用户拥有一个统一的登录，涵盖控制台登录、`POP` 服务器、`IMAP` 服务器、使用 `Samba` 连接到网络的机器，甚至 `Windows NT` 机器。使用 `LDAP`，所有这些登录情况都可以依赖相同的用户 ID 和密码组合。

### 8.4 LDAP 术语

条目是 `LDAP` 目录中的一个单元。条目通过其唯一的**可分辨名称**（`DN`）进行标识或引用。

条目具有属性；属性是与条目直接相关的信息片段。例如，一个组织可以是 `LDAP` 条目。与该组织相关的属性可能包括其传真号码、地址等。人员也可以是 `LDAP` 目录中的条目。人员的常见属性包括他们的电话号码和电子邮件地址。

某些属性是必需的，而其他属性是可选的。对象类（`objectclass`）设置了哪些属性是必需的，哪些是可选的。对象类定义可以在 `slapd.oc.conf` 文件中找到。

`LDAP` 数据交换格式（`LDIF`）是一种用于 `LDAP` 条目的 ASCII 文本格式。向 `LDAP` 服务器导入或导出数据文件必须采用 `LDIF` 格式。`LDIF` 条目的外观如下：

```
[<id>]
dn: <distinguished name>
<attrtype>: <attrvalue>
<attrtype>: <attrvalue>
<attrtype>: <attrvalue>
```

一个条目可以包含尽可能多的 `<attrtype>: <attrvalue>` 对。空行表示该条目已结束，另一个条目即将开始。

`< >` 内部包含的一切都是变量，在添加 `LDAP` 条目时你可以设置它们，除了 `<id>`。`<id>` 是一个数字，通常由 `LDAP` 工具在添加条目时设置，你很可能永远不需要手动设置它。

### 8.5 OpenLDAP 文件

`OpenLDAP` 配置文件安装在 `/etc/openldap` 目录中。如果在 `/etc/openldap` 中执行 `ls`，你会看到类似以下内容：

```
$ ls
ldap.conf              ldapsearchprefs.conf    slapd.at.conf      slapd.oc.conf
ldappfilter.conf       ldaptemplates.conf      slapd.conf
```

你需要了解的 `slapd.conf`、`slapd.at.conf` 和 `slapd.oc.conf` 文件。`slapd.conf` 文件包含 `slapd` 守护进程和所有数据库后端 的配置信息。在启动 `slapd` 守护进程之前，你需要对 `slapd.conf` 进行一些修改。

`slapd.at.conf` 文件保存 `LDAP` 目录的属性语法定义。属性语法描述属性提供的信息类型。你有五个选择：

- `bin` -- 二进制信息
- `ces` -- 大小写精确字符串（大小写敏感的字符串）
- `cis` -- 大小写忽略字符串（大小写不敏感的字符串）
- `tel` -- 电话号码（忽略空格和连字符）
- `dn` -- 可分辨名称

例如，以下是典型 `slapd.at.conf` 中的属性语法定义：

```
attribute      photo                 bin
attribute      personalsignature     bin
attribute      jpegphoto             bin
attribute      audio                 bin
attribute       labeledurl           ces
attribute       ref                 ces
attribute       userpassword         ces
attribute       telephonenumber      tel
```

某些支持 `LDAP` 的应用程序可能需要你编辑 `slapd.at.conf` 文件，通常是为了添加特定的属性语法定义。

`slapd.oc.conf` 文件包含 `LDAP` 目录的对象类定义。对象类定义说明了特定对象类中哪些属性是必需的，哪些属性是可选的。

以下摘自典型的 `slapd.oc.conf` 文件，包含了 `top`、`alias` 和 `referral` 对象类的定义：

```
objectclass top
    requires     top

objectClass alias
    requires
        aliasedObjectName,
        objectClass

objectClass referral
    requires
        ref,
        objectClass
```
