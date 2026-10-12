
# 列表 25-5 ldapsearch 查询整个 LDAP 数据库的输出

```
bible:/etc/ldap/schema # ldapsearch -b o=Acme,c=UK
# extended LDIF
# LDAPv3
# base <=Acme,c=UK> with scope sub
# filter: (objectClass=)
# requesting: ALL
#
# Acme, UK
dn: o=Acme,c=UK
o: Acme
objectClass: top
objectClass: organization
# Sales, Acme, UK
dn: ou=Sales,o=Acme,c=UK
ou: Sales
objectClass: top
objectClass: organizationalUnit
# Marketing, Acme, UK
dn: ou=Marketing,o=Acme,c=UK
ou: Marketing
objectClass: top
objectClass: organizationalUnit
# IT, Acme, UK
dn: ou=IT,o=Acme,c=UK
ou: IT
objectClass: top
objectClass: organizationalUnit
# HR, Acme, UK
dn: ou=HR,o=Acme,c=UK
ou: HR
objectClass: top
objectClass: organizationalUnit
# Services, Acme, UK
```

dn: ou=Services,o=Acme,c=UK

ou: Services

objectClass: top

objectClass: organizationalUnit

# Helpdesk, IT, Acme, UK

dn: ou-Helpdesk,ou=IT,o=Acme,c=UK

ou: Helpdesk

objectClass: top

objectClass: organizationalUnit

# Architects, IT, Acme, UK

dn: ou-Architects,ou=IT,o=Acme,c=UK

ou: Architects

objectClass: top

objectClass: organizationalUnit

# Administrators, IT, Acme, UK

dn: ou-Administrators,ou=IT,o=Acme,c=UK

ou: Administrators

objectClass: top

objectClass: organizationalUnit

dn: ou=Administrators,ou=IT,o=Acme,c=UK

ou: Administrators

objectClass: top

objectClass: organizationalUnit

dn: uid=aimee,ou=Administrators,ou=IT,o=Acme,c=UK

uid: aimee

cn: Aimee Davies

givenName: Aimee

sn: Davies

objectClass: person

objectClass: organizationalPerson

objectClass: inetOrgPerson

objectClass: posixAccount

objectClass: top

objectClass: shadowAccount

userPassword: {crypt}IESLPbFVJwpVEE

shadowLastChange: 12572

shadowMax: 99999

shadowWarning: 7

loginShell: /bin/bash

uidNumber: 1000

gidNumber: 100

homeDirectory: /home/aimee

telephoneNumber: 555-1027

o: Acme UK

gecos: Aimee Davies

```

## 第四部分 在 SUSE Linux 中实现网络服务

第二个字段可以是以下之一：

- `required`（必须的）：如果模块遇到错误，将导致整个服务（`imap`）的失败。即使身份验证失败，服务配置中剩余定义的 PAM 系统执行仍会继续。
- `requisite`（要求的必选的）：如果发生错误，PAM 将立即返回失败并停止执行配置文件的剩余部分。
- `sufficient`（足够的）：如果此 PAM 模块从系统返回成功，即使之前的某个 PAM 模块返回了失败，它也会返回整体成功（通常与 `required` 操作配合使用）。
- `optional`（可选的）：如果身份验证成功或失败，只要该项是此类类型服务（账户、密码、认证或会话）的唯一条目，则将强制执行。

第三和第四字段是 PAM 模块在文件系统中的位置，以及你需要传递给模块的任何参数。例如，如果你想通过 MySQL 数据库验证用户（使用 `pam_mysql`），你需要传递数据库名、表名、用户名和密码列，以及可以连接到数据库的 MySQL 用户名和密码。

在 `imap` 服务的示例中，我们已经说明对于 `auth` 和 `account` 认证方法，身份验证必须在两个条目中都成功（这是合理的，因为用户名和密码错误或账户已被禁用，我们不希望用户登录）。这两个条目都使用 `pam-unix.so` 模块，该模块查询标准 Unix 数据库（`/etc/passwd` 和 `/etc/shadow`）。最后对于 `auth` 条目，我们告诉 `pam-unix` 模块，服务为我们提供空密码是可以的（例如如果用户有空密码——这是个坏主意！）。

## 在 Linux 中集成 LDAP

当你将用户帐户存储在 LDAP 中，你就可以针对这些账户进行身份验证。要实现这一点，需要发生三件事：

1. 当系统需要查找有关用户的信息（UID、主目录等）时，它会查询 `nss` 切换器。`NSS` 是一个核心组件，允许 `glibc` 从系统中查找信息。这包括用户、组和主机数据。

`NSS` 通过 `/etc/nsswitch.conf` 文件进行控制，你需要更改其默认的文件查找（显式检查 `/etc/passwd` 等），以查询位于 `/etc/ldap.conf` 中的 LDAP 服务器。

```
passwd: files ldap

group: files ldap
```

设置完成后，使用 `runscd restart` 重启名称缓存守护进程 (`NSCD`)。

## 网络信息与目录服务

![](img/e749d3c47634a5bbb94e11699efbe992_670_0.png)

`NSCD` 是 LDAP 用户的噩梦。`NSCD` 缓存了系统上的 NSS 查询，这样后续查询就不需要查询原始 NSS 源。如果你在使用 LDAP 用户时发生了某些奇怪的事情，请尝试重启 `NSCD` 缓存看看是否能解决问题。

2. 告诉你的 LDAP 系统使用特定的 LDAP 数据源来获取数据。要做到这一点，你需要编辑 `/etc/ldap.conf` 文件。该文件定义了 LDAP 客户端信息——最重要的是 LDAP 服务器和默认搜索基准（正如我们之前使用 `-b` 选项所示）。在在此环境中，`ldap.conf` 文件包含 `localhost` 的服务器规范，因为 LDAP 数据就在那里，以及一个 `o=Acme,c=UK` 的基准。

```
host 127.0.0.1

base=Acme,c=UK
```

3. 配置 PAM 使用 LDAP 服务器。最近通过使用 `/etc/security/pam_unix2.conf` 文件，这已经被大大简化。

```
auth: use_ldap nullok

account: use_ldap

password: use_ldap nullok
```
