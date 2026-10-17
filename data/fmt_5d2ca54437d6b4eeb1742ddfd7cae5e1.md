
`sudo systemctl restart squid`

# 第 35 章 代理、反向代理与虚拟专用网络 (VPN)

```
matthew@seymour:-$ sudo ./build-ca
```

```
matthew@seymour:-$ sudo cp -r /usr/share/doc/openvpn/examples/easy-rsa/2.0/* /etc/openvpn/easy-rsa/
```

为服务器生成证书和私钥，将 `yourusername` 替换为你的服务器名称：

```
matthew@seymour:-$ sudo ./build-key-server yourusername
```

构建 Diffie-Hellman 参数：

```
matthew@seymour:-$ sudo ./build-dh
```

复制证书和密钥，将 `yourusername` 替换为你的服务器名称：

```
matthew@seymour:-$ cd keys
matthew@seymour:-$ sudo cp yourusername.crt yourusername.key ca.crt dh1024.pem /etc/openvpn/
```

你必须使用此方法为每个客户端创建一个证书。这是因为较大的专有 VPN 供应商会在其客户端和软件中分发证书，而你正在自己创建。在服务器机器上为每个客户端执行此操作，将 `clientname` 替换为每个客户端的名称：

```
matthew@seymour:-$ cd /etc/openvpn/easy-rsa-/
matthew@seymour:-$ source vars
matthew@seymour:-$ ./build-key clientname
```

现在，将你生成的以下文件复制到对应的客户端。为每个客户端重复此操作，将 `clientname` 替换为每个客户端系统的名称：

```
/etc/openvpn/ca.crt
/etc/openvpn/easy-rsa/keys/clientname.crt
/etc/openvpn/easy-rsa/keys/clientname.key
```

在文件安装到客户端后，删除服务器上的这些文件。

OpenVPN 在 `/usr/share/doc/openvpn/examples/sample-config-files/` 中包含了许多配置文件。如果你有比此处的简单设置更复杂的需求，可以阅读它们。例如，你只需要最基础的配置文件。复制并解压这些：

```
matthew@seymour:-$ sudo cp /usr/share/doc/openvpn/examples/sample-config-files/
server.conf.gz /etc/openvpn
matthew@seymour:-$ sudo zip -d /etc/openvpn/server.conf .gz
```

编辑 `/etc/openvpn/server.conf`，通过更改或添加以下行指向并使用你之前创建的证书和密钥，将 `yourservername` 替换为你的服务器名称，并保持其他默认设置不变：

```
ca ca.crt
cert yourservername.crt
key yourservername.key
```

启动你的服务器：
```
matthew@semour~$ sudo systemctl start openvpn-server
```

OpenVPN 在你的电脑上创建一个名为 `tun0` 的新网络接口。要确保接口已创建，请输入：

```
matthew@semour~$ sudo ifconfig tun0
```

要使用上一节描述的客户端使用新 VPN 服务器，请选择 OpenVPN 作为 VPN 类型，使用本节中的 `yourservername` 作为网关，并将类型设置为证书 (TLS)。此外，将用户证书指向你创建并移动到客户端机器的客户端证书，CA 证书指向你创建并移动到客户端机器的凭据库，并将私钥指向你创建并移动到客户端机器的私钥。

# 参考

- **squid-cache.org—Squid Web 代理缓存首页**
- **https://github.com/oskarpearson/squid-users-guide—Squid：用户指南首页，一本关于 Squid 的免费在线书籍**
- **https://help.ubuntu.com/lets/serverguide/squid.html—设置 Squid 的 Ubuntu 社区文档**
- **Squid: The Definitive Guide by Duane Wessels—由 Squid 领先开发人员之一编写的一本深入介绍 Squid 服务器的实用指南**
- **Web Caching by Duane Wessels—一本讨论如何实现缓存的理论书籍**
- **http://help.ubuntu.com/lets/serverguide/openvpn.html—设置 OpenVPN 的官方 Ubuntu 服务器文档**

# 第 36 章

## 本章内容

# 轻量级目录访问协议 (LDAP)

- 配置服务器
- 配置客户端
- LDAP 管理
- 参考

轻量级目录访问协议 (LDAP，发音为 "ell-dap") 是技术之一，尽管它并不为人知，但它是许多企业计算核心基础设施的一部分。它的任务很简单：存储有关用户的信息。然而，它的强大源于它可以与几十种其他服务关联。LDAP 可以支持登录验证、公钥分发、邮件路由和地址验证。最近，它已成为单点登录 (SSO) 技术推动的核心。

> 提示：大多数人发现将 LDAP 视为一种高度专业的数据服务器时，更容易理解这个概念。在后台，Ubuntu 使用数据库存储其所有的 LDAP 信息；然而，LDAP并不提供像 SQL 那样直接的数据操作方法。

OpenLDAP 使用 Sleepcat Software 的 Berkeley DB (BDB)，强烈建议保留该默认设置。不过，如果你有特定需求，也存在更适合你的替代方案。

本章介绍了 LDAP 服务器的相对基础的安装，包括如何托管包含员工姓名和电子邮件地址的市级目录服务。LDAP 是一个客户端/服务器系统，这意味着 LDAP 服务器托管数据，而 LDAP 客户端对其查询。Ubuntu 自带了 OpenLDAP，以及 Evolution 和 Mozilla Thunderbird 等支持 LDAP 的客户端。

Telegram Channel

由于 LDAP 数据通常通过互联网可用——或者至少在你的局域网内——因此务必努力确保服务器的安全。本章提供了关于 OpenLDAP 密码配置的具体说明。

# 配置服务器

如果你已经使用了多年 LDAP，你会意识到它的巨大力量和灵活性。但如果你是第一次使用 LDAP，它看起来像是你能想象的最复杂的组件。LDAP 有特定的配置要求，这些要求在图形工具中非常缺乏，并且有很多数字需要记忆。从好的一方面来看，所有的努力都是的，LDAP 大大地提升了你的网络体验。在继续之前，你应该阅读全章。在开始配置服务器之前，阅读 `/etc/ldap/schema` 中的 README 文件。

配置服务器的第一步是安装客户端和服务应用程序。当你从 Ubuntu 仓库安装 `ldap` 和 `ldap-utils` 包时，还会安装 `libldap2` 包。

默认情况下，Ubuntu 以运行所需的最少选项配置 slap。

现在你需要知道服务器的完全限定域名 (FQDN)。稍后你将开始编写/修改配置文件，这将该过程的一个部分。示例使用了 `matthewhelmke.com`。在需要时，将其更改为你的 FQDN。

从 FQDN 中获取域组件，它是存储在 DNS 中的域名。LDAP 将域名的每个部分（用点分隔）视为一个域组件。在 `matthewhelmke.com` 中有两个 DC 项：dc=matthewhelmke dc=com。

OpenLDAP 使用一个独立的目录 `cn=config` 目录信息树来配置 slap 守护进程。这允许你动态修改架构定义、索引，而无需停止并重启服务，这在之前的版本中是需要的。这种配置需要两个文件：一个只有最小配置的后端和一个与外部程序兼容的传统格式的前端。

## 创建你的架构

通过加载某些文件启动你的架构。通过预加载某些设置，配置变得更快更快更容易。如果你正在构建企业级服务器，请阅读官方 OpenLDAP 文档并从零开始，以便确切了解服务器正在执行的一切。对于此示例，使用以下命令加载这三个文件：

```
matrix@semour:-$ sudo ldap -Y EXTERNAL -H ld:/// -f /etc/ldap/schema/
```

```
matthew@semour:-$ sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/
-:-$ sudo ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/
```

接下来，创建一个名为 `backend.matthewhelmke.com.ldif` 的文件，内容如下：

```
# 加动态后端模块
d: cn=module,cn=config
objectClass: olcModuleList
cn: module
olcModulepath:/usr/lib/ldap
olcModuleload: back_hdb
# 数据库设置
d: olcDatabase=hdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcHDbConfig
olcDatabase:{1}hdb
olcSuffix: dc=matthewhelmke,dc=com
olcDirectory: /var/lib/ldap
olcRootDN: cn=admin,dc=matthewhelmke,dc=com
olcRootPW: changeToSOMETHINGBetter
olcDbConfig: set_caches=0 2097152 0
olcDbConfig: set_lk_max_objects 1500
olcDbConfig: set_lk_max_locks 1500
olcDbConfig: set_lk_max_lockers 1500
olcDbIndex: objectClass:eq
olcLastMod: TRUE
olcCheckpoint: to attrs=userPassword by dn="cn=admin,dc=matthewhelmke,dc=com" write by
anonymous auth by self write by *
olcAccess: to attrs=shadowLastChange by self write by * read
olcAccess: to dn.base="* by read
olcAccess: to by dn="cn=admin,dc=matthewhelmke,dc=com" write by *
```

确保将所有的 `matthewhelmke.com` 实例都替换为你的完全限定域名（FQDN），并将 `olcRootPW` 条目更改为你选择的更安全的密码。然后，将新文件添加到目录中，按照以下步骤操作，以确保你是在创建文件的目录下执行此命令：

```
matthew@semour:-$ sudo ldapadd -Y EXTERNAL -H ldapi:/// -f backend.example.com.ldif
```

## 填充目录

后端已准备绪。现在，你需要填充前端目录以使其可用。创建另一个名为 `frontend.matthewhelmke.com.ldif` 的文件，内容如下：

```
# 域名中的顶层对象
dn: dc=matthewhelmke,dc=com
objectClass: top
objectClass: dcObject
objectclass: organization
o: Example Organization
dc: Example
description: LDAP Example
# 管理用户。
dn: cn=admin,dc=matthewhelmke,dc=com
objectClass: simpleSecurityObject
objectClass: organizationalRole
cn: admin
description: LDAP administrator
userPassword: changeToSOMETHINGbetter
ou=people,dc=example,dc=com
objectClass: organizationalUnit
ou: people
ou=groups,dc=matthewhelmke,dc=com
objectClass: organizationalUnit
ou: groups
uid=john,ou=people,dc=matthewhelmke,dc=com
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: matthew
sn: Helmke
givenName: Matthew
cn: Matthew Helmke
displayName: Matthew Helmke
uidNumber: 1000
gidNumber: 10000
userPassword: changeMeSOMETHINGbetter
gecos: Matthew Helmke
loginShell: /bin/bash
homeDirectory: /home/matthew
shadowExpire: -1
```

```
shadowFlag: 0
shadowWarning: 7
shadowMin: 8
shadowMax: 999999
shadowLastChange: 10877
mail: matthew@matthewhelmke.com
postalCode: 85711
l: Tucson
o: Example
mobile: +1 (520) xxx-xxxx
homePhone: +1 (520) xxx-xxxx
title: System Administrator
postalAddress: I'm not putting it in the book.
initials: MH
```

```
dn: cn=example,ou=groups,dc=example,dc=com
objectClass: posixGroup
cn: example
gidNumber: 10000
```

记得更改细节以符合你的信息。然后将此文件添加到 LDAP 目录：
`matthew@seymour:-$ sudo ldapadd -x -D cn=admin,dc=example,dc=com -W -f frontend.example.com.ldif`

要检查你的内容是否已添加到 LDAP 目录，你可以使用 `ldsearch`，如下：
`matthew@:-$ ldsearch -xLLL -b "dc=example,dc=com" uid=john sn givenName cn-uid=matthew,ou=people,dc=matthewhelmke,dc=com
cn: Matthew Helmke
sn: Helmke
givenName: Matthew`

在这个示例中，dn 代表区分名称（distinguished name），uid 指用户标识，ou 是组织单元（organizational unit），dc 代表域名组件（domain component），cn 是通用名称（common name），sn 是姓氏（family or surname），许多文化都知道 givenName。

使用 LDAP 时，你可以以多种方式组织数据。你可以使用现有的架构（如前面的示例中使用开始时加载的 LDIF 文件），也可以创建自己的架构。

## 配置客户端

在这个示例中，dn 代表区分名称，uid 指用户标识，ou 是组织单元，dc 代表域名组件，cn 是通用名称，sn 是姓氏，许多文化都知道 givenName。

使用 LDAP 时，你可以以多种方式组织数据。你可以使用像开始时加载的 LDIF 文件那现有架构，也可以创建自己的。

在这个示例中，dn 代表区分名称，uid 指用户标识，ou 是组织单元，dc 代表域名组件，cn 是通用名称，sn 是姓氏，许多文化都知道 givenName。

## 配置客户端

`olcLastMod: TRUE`
`olcCheckpoint: to attrs=userPassword by dn="cn=admin,dc=matthewhelmke,dc=com" write by`
`anonymous auth by self write by *`
`olcAccess: to attrs=shadowLastChange by self write by * read`
`olcAccess: to dn.base="* by read`
`olcAccess: to by dn="cn=admin,dc=matthewhelmke,dc=com" write by *`

确保将所有的 `matthewhelmke.com` 实例都替换为你的完全限定域名（FQDN），并将 `olcRootPW` 条目更改为你选择的更安全的密码。然后，将新文件添加到目录中，按照以下步骤操作，以确保你是在创建文件的目录下执行此命令：

```
matthew@semour:-$ sudo ldapadd -Y EXTERNAL -H ldapi:/// -f backend.example.com.ldif
```
