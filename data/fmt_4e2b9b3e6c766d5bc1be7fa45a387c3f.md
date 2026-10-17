
`rootdn` 行表明，可以授予 root 权限以修改与 `linuxtoys.net` 可区分子目录名称（distinguished name）关联的数据库中的数据（前提是在下一步中描述的那样，使用 `rootpw` 提供密码）。我添加了最后四个选项以提高 `bdb` 数据库的性能（有关详细信息，请查看 `man slapd-bdb`）。

### 5. 添加密码

在 `slapd.conf` 文件中，你需要输入修改 OpenLDAP 后端数据库所需的密码。默认情况下，`rootpw` 行定义了一个明文字符串作为你的密码。该密码将赋予你对后端数据库的完全控制权。其外观可能如下所示：

```
rootpw        mysecret
```

> **注意：** 如果你打算使用明文密码，请确保你的 `slapd.conf` 文件对全局用户的读取权限已关闭（`chmod 640 /etc/openldap/slapd.conf`）。有关创建用于访问 OpenLDAP 后端数据库的加密密码的信息，请参阅侧栏“创建加密密码”。

### 6. 保存 slapd.conf

保存你对 `slapd.conf` 文件的更改并关闭它。

### 7. 检查 slapd.conf

通过运行 `slappasswd` 命令来检查 `slapd.conf` 文件中的语法错误，方法如下：

```
# slappasswd -u
config file testing succeeded
```

如果文件语法有误（例如，如果省略了引号或逗号位置错误），消息将显示为 `slappasswd: bad configuration file`。尝试修正问题并再次检查文件。稍后，当数据库创建完成后，你可以再次运行 `slappasswd`（不带 `-u` 选项），以确保 `slapd.conf` 指向存在且配置正确的数据库。

此时，你可以尝试启动 OpenLDAP 服务。

#### 创建加密密码

要为 OpenLDAP 数据库的管理员创建加密密码，请使用 `slappasswd` 命令。你可以使用 `Crypt`、`SSHA`、`SMD5`、`MD5` 或 `SHA` 加密来创建密码。以下是使用 `MD5` 加密为 OpenLDAP 创建密码的示例：

```
# slappasswd -h {md5} > /tmp/myslap
New password: ********
Re-enter new password: ********
# cat /tmp/myslap
{MD5}uBoM+LOQg5GHJj2Z4NLu9a==
```

输入密码（两次）以创建加密的 `MD5` 密码。此示例将加密密码重定向到 `/tmp/myslap` 文件；你可以稍后将其读取到 `slapd.conf` 文件中。在此示例中，我让你 `cat` 该文件，以便你可以查看加密密码的外观。你的密码将有所不同。使用加密密码而非明文密码时，`rootpw` 行的外观如下：

```
rootpw {MD5}uBoM+LOQg5GHJj2Z4NLu9a==
```

#### 启动 OpenLDAP 服务

像在 Fedora 中启动大多数服务一样，使用 `service` 和 `chkconfig` 命令启动 OpenLDAP 服务。OpenLDAP 的服务名称为 `slapd`。若要立即启动服务，请输入以下内容：

```
# service slapd start
Starting slapd: [ OK ]
```

若要设置 `slapd` 服务在每次系统重启时自动启动，请输入以下内容：

```
# chkconfig slapd on
```

默认情况下，`slapd` 服务对所有人开放读取权限。

#### 设置地址簿

在设置地址簿数据库结构时，我基于组织名称（在本示例中为 `linuxtoys`）来确定数据库的可区分子目录名称（`dn`）。

在 `slapd.conf` 文件中将后缀设置为 `linuxtoys net`（`suffix "dc=linuxtoys,dc=net"`）（你的设置可能不同），后端数据库被设置为处理对 `linuxtoys net` 的可区分子目录名称（`dn`）的查询。接下来，你可以在此可区分子目录名称下为该组织创建地址簿结构。

> **注意：** `dc=` 代表域组件（Domain Component）。当你将域名包含在你的可区分子目录名称中时，放置该域名各部分的顺序应将最接近 DNS 根的部分放在最后。在此示例中，`dc=linuxtoys` 位于 `dc=net` 之前。如果你对将域名包含在 LDAP 目录中的规范感兴趣，请参阅 `RFC 2247`。

你需要以一种可以加载到 OpenLDAP 数据库中的格式创建地址簿文件。所需的格式称为 LDAP 数据交换格式（`LDIF`）。以此格式输入的信息可用于构建数据库，并一次性从文件向目录中加载大量数据。

以下步骤说明了如何创建一个包含 `linuxtoys.net` LDAP 目录（可区分子目录名称）地址簿定义的 `LDIF` 文件，并将该文件加载到你的 LDAP 服务器中。

- **1. 创建 ldif 文件。** 作为 `root` 用户，使用任意文本编辑器创建一个用于保存 LDAP 目录条目的文件。在我的示例中，我使用了 `/etc/openldap/toypeople.ldif` 文件。

> **注意：** 创建 `ldif` 文件时，务必在每个新的可区分子目录名称（`dn:`）行之前保留一个空白行。空白行告诉 `ldapadd` 开始一个新条目。如果没有空白行，LDAP 将不知道你要开始一个新的可区分子目录名称。此外，删除每行前的所有空格，确保所有新行都从第 1 列开始。（行首的空格表示新行实际上是前一行的一部分。）

- **2. 定义组织。** 你需要定义要加载到 LDAP 服务器中的目录。在我的示例中，我添加了将组织定义为 Linux Toys 的信息，位于可区分子目录名称 `linuxtoys net`（`dc=linuxtoys,dc=net`）之下，方法是将以下信息添加到我的 `toypeople.ldif` 文件中。

```
dn:                      dc=linuxtoys,dc=net
objectClass:              dcObject
objectClass:              organization
dc:                      linuxtoys
o:                      Linux Toys
```

- **3. 添加一个组织角色。** 我通过在 `toypeople.ldif` 文件中添加以下行，确定了通讯录管理员的角色。

```
dn: cn=Manager,dc=linuxtoys,dc=net
objectClass: organizationalRole
cn: Manager
description: LinuxToys Address Book Administrator
```

- **4. 添加一个组织单元。** 由于在本例中，通讯录基本上由组织成员的名字和地址组成，因此我将该组织单元（`ou`）命名为 `members`（成员）。

```
dn: ou=members,dc=linuxtoys,dc=net
objectClass: top
objectClass: organizationalUnit
ou: members
```

> **注意：** 尽管在我的示例中，我创建的是一个位于目录结构顶部的通讯录，但如果你身处一家大型公司，你很可能会想要一个更复杂的目录结构。例如，与其在目录结构的顶部放置一个通讯录，你可以为国家、地点或部门创建额外的组织单元。然后，每个单元可能都有自己的通讯录。你可能还希望支持每个单元下的多个目录。例如，可能有一个单独的目录用于跟踪计算机设备或公司车辆。

- **5. 添加人员。** 在目录结构就位，且 `linuxtoys.net` 可区分名称下拥有 `members` 单元后，我可以开始向目录中添加人员。我将每个人定义为 `organizationalPerson` 和 `inetOrgPerson` 对象类。我可以为每个人的信息添加许多不同的属性。然而，我选择的大多数属性都是 Thunderbird 邮件客户端（将在本章稍后展示）将要读取的属性。以下是这两个条目：

```
dn: cn=John Jones,dc=linuxtoys,dc=net
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: John Jones
mail: jjwones@linuxtoys.net
givenname: John
sn: Jones
uid: jjwones
o: Linux Toys
telephoneNumber: 800-555-1212
homePhone: 800-555-1313
mobile: 800-555-1414
pager: 800-555-1515
facsimileTelephoneNumber: 800-555-1414
title: Account Executive
homePostalAddress: 1515 Broadway$New York NY 99999
```
