
LDAP 代表轻量级目录访问协议（Lightweight Directory Access Protocol）。LDAP 已成为运行在 TCP/IP 之上的目录服务的标准。LDAP 是一种访问目录服务的客户端/服务器协议。它最初设计作为 X.500 数据库的前端，现在通常作为独立实体使用。IBM、Netscape、Sun、Novell、Microsoft 以及许多公司正在将 LDAP 整合到它们的目录结构中。

## 13.1.1 目录服务

目录服务是软件、硬件、进程、策略和管理程序的集合，涉及使目录中的信息对目录的用户可用。

目录类似于数据库。然而，目录和数据库的区别在于搜索和更新的次数。目录针对搜索进行了优化，而关系型数据库则侧重于维护具有频繁更新次数的数据。

目录的示例包括黄页、卡片索引或地址簿。信息按照定义的层级结构进行组织，并赋予属性。

当我们将目录上线时，数据就变成了动态的，这意味着它们可以很容易地更新和交叉引用。与纸质材料不同，任何发生的更新对所有用户来说都是即时的。

你可以对目录应用安全措施，使得只有预期的用户才能查看、修改或创建数据。这种安全性可以基于组、个人用户或其他任何认证方案。数据可以被加密。

目录服务通常涉及数据分发。目录服务的优势是性能和可用性。

## 13.1.2 目录服务

20 世纪80 年代中期，国际电信联盟（ITU）和国际标准组织（ISO）合并了它们在目录服务方面的努力。作为 LDAP 的前身，互联网工程任务组（IETF）开始了 LDAP 的工作。第一份描述 LDAP 的征求意见（RFC 1487）于 1993 年 7 月发布。

## 13.2 我如何使用 LDAP？

LDAP 允许系统和网络管理员集中管理用户、组、设备和其他数据。为了避免让自己受困于单一供应商，LDAP 的一些实际应用包括：

- 企业地址簿
- 用户身份验证
- 域名系统

## 13.3 LDAP 基础

LDAP 信息模型基于对象。对象可以是人、打印机、服务器或你能到的任何东西。LDAP 最基本的单元是条目（`entry`）。一个条目是信息的集合。每个条目属于一个对象类，该类决定了必需和可选的属性。每个属性都有类型和一个或多个值。

248 xSeries 和 Netfinity SuSE Linux 集成指南

LDIF 是以文本格式表示目录数据的标准方法。以下是一个用于加载目录并添加供我们测试用户的 LDIF 文件。

```
dn: ou=people, dc=ibm, dc=com
objectclass: top
objectclass: organizationalUnit
description: users who authenticate via the ldap server

dn: uid=ldaptest, ou=people, dc=ibm, dc=com
uid: ldaptest
cn: ldaptest
objectclass: account
objectclass: posixAccount
objectclass: top
objectclass: shadowAccount
userpassword: test123
shadowLastChange:11263
shadowMax:99999
shadowWarning:7
loginShell: /bin/bash
uidNumber: 500
gidNumber: 500
homeDirectory: /home/test
```

每个 LDAP 条目都必须有一个区分名（DN）。区分名是一个特指该条目的唯一键。

第一组条目用于在目录中创建根或基条目。在这种情况下，我们使用了 `com`、`ibm` 和 `people`（组织单元）。

在组织单元 `people` 内部，我们将存储用户及其对应的身份验证信息。第二组条目用于添加用户 `ldaptest` 以及进行身份验证所需的属性。

## 13.4 在 Linux 上的实现

你可以从以下处下载最新稳定版本的 OpenLDAP：

`ftp.openldap.org/pub/ldap`

然而，我们将使用 SuSE Linux 发行版自带的软件包。安装或验证以下 RPM 的安装：

`openldap`

`nss_ldap`

`pam_ldap`

### 13.4.1 Slapd.conf

现在编辑 `/etc/ldap/slapd.conf` 文件。将 `ibm` `ib` 和 `com` 替换为您的组织名称。

```
# 关于配置选项请参见 slapd(5)。
# 此文件不应允许全用户可读。
include /etc/ldap/slapd.conf
include /etc/ldap/slapd.cc.conf
schemack off
#referral /root.openldap.org/
pidfile /var/run/slapd.pid
argsfile /var/run/slapd.args
##################################################################
# ibm 数据库定义

database ibm
suffix "=oupeple,dc=ibm,dc=com*"
rootdn "cn=oupeple,dc=ibm,dc=com*"
rootdn "cn=Manager,dc=my Organization Name,c=US"
# 应该清除密码，特别是对于 rootdn，
# 详情请参见 slapd(5)。
rootpw insert_your_PASSWORD
# 数据库目录
# 此目录在运行 slapd 之前必须存在，
# 并且仅允许 slapd/tools 访问，推荐模式 700。
directory /var/lib/ldap
```

图 207. `slapd.conf` 文件

### 13.4.2 Ldap.conf

编辑 `/etc/ldap/ldap.conf` 文件。修改 `host` 和 `base` 条目。在这种情况下，我们将进行认证的 LDAP 服务器是本地。将 `paidl` 替换为您的组织名称。在我们的示例中，使用了 `ibm`。所有其他条目可以保持默认值。

250 SuSE Linux 集成指南 xSeries Netfinity

```
#
# LDAP 默认值
#
# 详情请参见 ldap.conf(5)
# 此文件应允许全用户读取。

BASE ou=people, dc=lhm, dc=com
HOST 127.0.0.1

#HOST ldap.opensldap.org ldap-master.opensldap.org:666
#PORT 389

#SIZELIMIT 12
#TIMELIMIT 15
#SDEF never
```

图 208. `ldap.conf` 文件

### 13.4.3 nsswitch.conf

`nsswitch.conf` 文件控制您的主机使用何种类型的名称服务来查找各种类型的条目。使用 LDAP，你可以轻松地设置域名系统和主机查找表。在这个示例中，我们需要修改 `passwd` 条目。编辑 `/etc/nsswitch.conf` 文件，并在 `passwd` 和 `group` 查找条目中添加 `ldap`：

- `passwd`: `files`, `ldap`
- `group`: `file`, `ldap`

### 13.4.4 /etc/pam.d/login

PAM 是一个处理系统上服务认证任务的库系统。PAM 将认证任务分为四个独立的管理组：`account`（账户）、`authentication`（认证）、`password`（密码）和 `session`（会话）。

- `account`：提供账户验证。例如：检查密码是否过期或验证用户是否有权限访问请求的服务。
- `authentication`：建立用户是其所称的身份，通常通过提示密码来实现。
- `password`：认证更新机制。例如：当当前密码过期时，提示用户输入新密码。
- `session`：在提供服务之前和撤销服务之后应该执行的任务。例如：审计日志维护和用户主目录的挂载。

要启用访问 LDAP 目录的 PAM 模块，编辑 `/etc/pam.d/login` 文件：
