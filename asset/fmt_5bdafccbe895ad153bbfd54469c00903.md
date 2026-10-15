
# OpenLDAP 数据库配置指南

## 目录
1. 创建 OpenLDAP 数据库
2. 为 OpenLDAP 用户创建加密密码
3. 编辑 `slapd.conf` 文件
4. 启动 LDAP 服务
5. 为 OpenLDAP 用户创建账户
6. 以 LDIF 格式提取用户详情和密码
7. 将 LDIF 文件导入 OpenLDAP 数据库
8. 验证 OpenLDAP 数据库中条目的添加

# 1. 创建 OpenLDAP 数据库

要创建 OpenLDAP 数据库，请执行以下步骤：

1. 输入以下命令在 `/var/lib/ldap` 目录下创建一个名为 `newmoon.com` 的目录：

```
# mkdir /var/lib/ldap/newmoon.com
```

2. 输入以下命令，将 `/var/lib/ldap/newmoon.com` 目录的所有权分配给 OpenLDAP 服务器：

```
# chown ldap:ldap /var/lib/ldap/newmoon.com
```

# 2. 为 OpenLDAP 用户创建加密密码

复制由 `slappasswd` 命令显示的加密密码。此密码将指定在 `slapd.conf` 文件的 `rootpw` 指令中。

# 3. 编辑 slapd.conf 文件

为了编辑 `/etc/openldap/slapd.conf` 文件以配置 OpenLDAP 服务器，请执行以下步骤：

1. 编辑 `suffix` 指令以指定 OpenLDAP 域的域名组件，如下所示：

```
suffix "dc=newmoon, dc=com"
```

2. 编辑 `rootdn` 指令以指定 OpenLDAP 根用户的通用名称和域组件，如下所示：

```
rootdn "cn=Manager, dc=newmoon, dc=com"
```

3. 在 `rootpw` 指令后粘贴加密密码，如下所示：

```
rootpw {SSHA}k/DSZn1Bm05Wbi6HZRSNpc3HpmI1Nzcgc
```

4. 编辑 `directory` 指令以指定 OpenLDAP 数据库的位置，如下所示：

```
directory /var/lib/ldap/newmoon.conf file.
```

5. 保存并退出 `/etc/openldap/slapd.conf` 文件。

# 4. 启动 LDAP 服务

执行以下命令启动 LDAP 服务：

```
# service ldap start
```

# 5. 为 OpenLDAP 用户创建账户

要为 OpenLDAP 用户创建账户，请执行以下步骤：

1. 输入以下命令在默认组 `users` 中添加一个名为 `ronald` 的用户：

```
# useradd -g users ronald
```

2. 输入以下命令为 `Ronald` 分配密码：

```
# passwd ronald
```

前述命令显示如下输出：

```
Changing password for user Ronald.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

当创建用户时，用户和密码详情将存储在 `/etc/passwd` 文件中。

# 6. 以 LDIF 格式提取用户详情和密码

要以 LDIF 格式从 `/etc/passwd` 文件中提取创建的用户和密码条目，请执行以下步骤：

1. 输入以下命令从 `/etc/passwd` 文件中提取用户 `ronald` 的条目，并追加到 `/etc/openldap/passwd.ronald` 文件：

```
# grep ronald /etc/passwd > /etc/openldap/passwd.ronald
```

2. 输入以下命令从 `/etc/passwd` 文件中提取根用户的条目，并追加到 `/etc/openldap/passwd.root` 文件：

```
# grep root /etc/passwd > /etc/openldap/passwd.root
```

`passwd.ronald` 和 `passwd.root` 文件需要转换为 LDIF 格式。要将文件转换为 LDIF 格式，请使用 `migrate_passwd.pl` Perl 脚本。

3. 输入以下命令在 OpenLDAP 服务器上定位 `migrate_passwd.pl` Perl 脚本：

```
# locate -u
# locate migrate_passwd.pl
```

前述命令显示如下输出：

```
/usr/share/openldap/migration/migrate_passwd.pl
```

4. 输入以下命令将 `passwd.ronald` 文件转换为 `ronald.ldif`：

```
# /usr/share/openldap/migration/migrate_passwd.pl /etc/openldap/passwd.ronald /etc/openldap/ldif
```

同样，输入以下命令将 `passwd.root` 文件转换为 `root.ldif`：

```
# /usr/share/openldap/migration/migrate_passwd.pl /etc/openldap/passwd.root /etc/openldap/root.ldif
```

5. 编辑 `/etc/openldap/ronald.ldif` 文件，将条目 `dn: uid=ronald,ou=People,dc=newmoon,dc=com` 替换为以下条目：

```
dn: uid=ronald,ou=People,dc=newmoon,dc=com
```

`ronald.ldif` 中的前述条目将把域名从 `padl.com` 更改为 `newmoon.com`。

同样，编辑 `/etc/openldap/root.ldif` 文件，并将域组件和通用名称更改为 `uid=root,ou=People,dc=newmoon,dc=com`，如下所示：

```
dn: uid=root,ou=People,dc=newmoon,dc=com
uid: root
cn: Manager
cn: root
objectClass: account
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword: {crypt}$1$9T11TUMV$rD8snEotzmLTLIdz19901
shadowLastChange: 12931
shadowMax: 99999
shadowWarning: 7
loginShell: /bin/bash
uidNumber: 0
gidNumber: 0
homeDirectory: /root
gecos: root

dn: uid=operator,ou=People,dc=newmoon,dc=com
uid: operator
cn: Manager
cn: operator
objectClass: account
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword: {crypt*}
shadowLastChange: 12931
shadowMax: 99999
shadowWarning: 7
loginShell: /sbin/nologin
uidNumber: 11
gidNumber: 0
homeDirectory: /root
gecos: operator
```

6. 输入以下命令创建一个名为 `newmoon.com` 的 ldif 文件：

```
# vi /etc/openldap/newmoon.com.ldif
```

7. 在 `newmoon.com.ldif` 文件中添加以下条目以指定域名 `newmoon.com` 和 `ou` 的属性：

```
dn: dc=newmoon,dc=com
dc: newmoon
description: Root entry for newmoon.com
objectClass: Object
objectClass: organizationalUnit
ou: root

dn: ou=People,dc=newmoon,dc=com
ou: People
description: All people
objectClass: organizationalUnit
```

# 7. 将 LDIF 文件导入 OpenLDAP 数据库

要将 ldif 文件导入 OpenLDAP 数据库，请执行以下步骤：

1. 输入以下命令将 `newmoon.com.ldif` 导入 OpenLDAP 数据库：
