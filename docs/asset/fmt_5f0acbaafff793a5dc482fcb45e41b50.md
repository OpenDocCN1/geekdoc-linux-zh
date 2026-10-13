
```
# ldapadd -x -D "cn=Manager,dc=newmoon,dc=com" -W -f /etc/ldap/newmoon.com.ldif
```

前述命令显示如下输出，验证了 `newmoon.com.ldif` 文件已导入到 OpenLDAP 数据库。

```
adding new entry "dc=newmoon,dc=com"
adding new entry "ou=People,dc=newmoon,dc=com"
```

### 2. 输入以下命令将 `root.ldif` 导入 OpenLDAP 数据库：

```
# ldapadd -x -D "cn=Manager,dc=newmoon,dc=com" -W -f /etc/ldap/root.ldif
```

前述命令显示如下输出，验证了 `root.ldif` 文件已导入到 OpenLDAP 数据库：

```
adding new entry "uid=root,ou=People,dc=newmoon,dc=com"
adding new entry "ou=operator,dc=newmoon,dc=com"
```

### 3. 输入以下命令将 `ronald.ldif` 导入 OpenLDAP 数据库：

```
# ldapadd -x -D "cn=Manager,dc=newmoon,dc=com" -W -f /etc/ldap/ronald.ldif
```

前述命令显示如下输出，验证了 `ronald.ldif` 已导入到 OpenLDAP 数据库。

```
adding new entry "dc=newmoon,dc=com"
```

## 8. 验证 OpenLDAP 数据库中的条目

要验证 OpenLDAP 数据库中已添加的条目，请执行以下步骤：

### 1. 输入以下命令验证 OpenLDAP 数据库中已添加的条目：

要从 `/etc/passwd` 文件中以 LDIF 格式提取创建的用户和密码条目，并追加到 `/etc/openldap/passwd.ronald` 文件：

```
# grep ronald /etc/passwd > /etc/openldap/passwd.ronald
```

输入以下命令从 `/etc/passwd` 文件中提取根用户的条目，并追加到 `/etc/openldap/passwd.root` 文件：

```
# grep root /etc/passwd > /etc/openldap/passwd.root
```

`passwd.ronald` 和 `passwd.root` 文件需要转换为 LDIF 格式。要将文件转换为 LDIF 格式，请使用 `migrate_passwd.pl` Perl 脚本。

输入以下命令在 OpenLDAP 服务器上定位 `migrate_passwd.pl` Perl 脚本：

```
# locate -u
# locate migrate_passwd.pl
```

前述命令显示如下输出：

```
/usr/share/openldap/migration/migrate_passwd.pl
```

输入以下命令将 `passwd.ronald` 文件转换为 `ronald.ldif`：

```
# /usr/share/openldap/migration/migrate_passwd.ronald /etc/openldap/passwd.ronald /etc/openldap/ldif
```

同样，输入以下命令将 `passwd.root` 文件转换为 `root.ldif`。

```
# /usr/share/openldap/migration/migrate_passwd.pl /etc/openldap/passwd.root /etc/openldap/root.ldif
```

编辑 `/etc/openldap/ronald.ldif` 文件，将条目 `dn: uid=ronald,ou=People,dc=newmoon,dc=com` 替换为以下条目：

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

### 6. 输入以下命令创建一个名为 `newmoon.com` 的 ldif 文件：

```
# vi /etc/openldap/newmoon.com.ldif
```

### 7. 在 `newmoon.com.ldif` 文件中添加以下条目以指定域名 `newmoon.com` 和 `ou` 的属性：

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

# 498 Red Hat Linux 学习指南

```
pidfile /var/run/slapd.pid
argsfile /var/run/slapd.args
```

```
# 在 /var/lib/ldap 中创建一个用于 slurpd 的复制日志
replogfile /var/lib/ldap/master-slapd.replog
access to attr=userPassword
  by self write
  by anonymous auth
  by dn="cn=Manager,dc=newmoon,dc=com" write
  by dn="cn=replica,dc=newmoon,dc=com" write
  by read
access to *
  by peername=127.0.0.1 read
  by self write
  by peername=master.newmoon.com read
  by dn="cn=Manager,dc=newmoon,dc=com" write
  by dn="cn=replica,dc=newmoon,dc=com" write
  by read
```
