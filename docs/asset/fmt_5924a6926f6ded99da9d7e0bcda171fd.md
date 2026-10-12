
```bash
# .../etc/openldap/cacerts
```

我们在本章之前在配置跨 realm 信任（图 26-2）时通过访问 Active Directory 控制台执行了相同的操作。

我们可以在复制数据之前对 Active Directory DC 进行查询。为了检查一切运行正常，我们将从普通的 LDAP 连接开始。

```bash
[root@uniform ~]# ldapsearch -x D "CN=Administrator,CN=Users,DC=ventanas,DC=local" -b dc=ventanas,dc=local "(cn=Administrator)" -H ldaps://yankee.ventanas.local -w P@ssword
ldap_sasl_bind(SIMPLE): Can't contact LDAP server (-1)
```

```bash
[root@uniform ~]# ldapsearch -x D "CN=Administrator,CN=Users,DC=ventanas,DC=local" -b dc=ventanas,dc=local "(cn=Administrator)" -H ldap://yankee.ventanas.local -w P@ssword
```

# Administrator, Users, ventanas.local

dn: CN=Administrator,CN=Users,DC=ventanas,DC=local

objectClass: top

objectClass: person

objectClass: organizationalPerson

objectClass: user

cn: Administrator

description: Built-in account for administering the computer/domain

distinguishedName: CN=Administrator,CN=Users,DC=ventanas,DC=local

instanceType: 4

```

接下来，我们将检查安全连接是否可用。

```bash

[root@uniform ~]# ldapsearch -x D "CN=Administrator,CN=Users,DC=ventanas,DC=local" -b dc=ventanas,dc=local "cn=Administrator)" -H ldaps://yankee.ventanas.local -w P@ssw

```

# Administrator, Users, ventanas.local

dn: CN=Administrator,CN=Users,DC=ventanas,DC=local
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: user
cn: Administrator

description: Built-in account for administering the computer/domain
distinguishedName: CN=Administrator,CN=Users,DC=ventanas,DC=local
instanceType:4
```

我们准备好启动复制，但首先我们需要销毁可能关联的 Kerberos 票据。

```bash
[root@uniform certs]# kdestroy
[root@uniform certs]# klist
klist: No credentials found (ticket cache KEYRING:persistent:0)
```

现在创建副本，使用 Windows 服务器（`--winsync`），以及连接的用户（`--binddn`）及其密码（`--bindpw`）。我们还需要传递 Active Directory CA 证书的位置（`--cacert`）以及我们要连接的服务器的 FQDN（`yankee.ventanas.local`）。在使用 `passync` Windows 插件同步密码时，还需要指定密码的值（`--passync`）。

```bash
[root@uniform ~]# ipa-replica-manage connect --winsync --binddn CN=Administrator,CN=Users,DC=ventanas,DC=local --bindpw=P@ssword --passync=P@ssword --cert=/etc/openldap/certs/AD-CA.cert yankee.ventanas.local -v
```

Added CA certificate /etc/openldap/certs/AD-CA.cert to certificate database for uniform.apres.local

ipa: INFO: AD Suffix is: DC=ventanas,DC=localnThe user for the Windows PassSync service is uid=passysync,cn=sysaccounts,cn-etc,dc=apres,dc=local

ipa: INFO: Added new sync agreement, waiting for it to become ready . . .

: INFO: Replication Update in progress: FALSE: status: 0 Replica acquired successfully: Incremental update started: start: 0: end: 0

: INFO: Agreement is ready, starting replication . . .

Starting replication, please wait until this has completed.

Update succeeded

Connected 'uniform.apres.local' to 'yankee.ventanas.local'

副本创建正确完成，我们可以随时列出副本。

```bash
[root@uniform ~] ipa-replica-manage list
Directory Manager password:
```

yankee.ventanas.local: winsync

uniform.apres.local: master

现在，如果我们创建一个新的 Active Directory 用户，例如 John Windows，我们在 FreeIPA 服务器上也能看到该用户。

```bash
[root@uniform ~]# ipa user-find
.User login: jwindows
First name: John
Last name: Windows
Home directory: /home/jwindows
Login shell: /bin/sh
UID: 643400005
GID: 643400005
Account disabled: False
Password: False
Kerberos keys available: False
```

### 总结

在本章中，我们学习了如何成功地集成 FreeIPA 和 Active Directory。作为首选的集成方法，我们在两个域之间建立了信任关系。我们还查看了集成的替代方法，例如复制信息。我们还进一步学习了关于 POSIX 和非 POSIX 组的知识，以及 ID 范围以及在必要时手动创建它们的方法。最后，我们研究了微软实现 Kerberos 协议的某些特殊之处，特别是 MS PAC 的使用。

## 第 27 章

## 网络文件系统 (NFS)

NFS 是由 Sun 公司最初开发的分布式文件系统。在本章中，我们将涵盖以下概念：

- 了解 NFSv4 的主要功能。
- 配置和管理 NFSv4 服务器和客户端。
- 了解和使用 NFSv4 伪文件系统。
- 了解和使用 NFSv4 ACL。
- 使用 Kerberos 进行 NFSv4 认证。

我们还将学习以下术语和工具：`exportfs`、`/etc/exports`、`/etc/idmapd.conf`、`nfs4_editfacl`、`nfs4_getfacl`、`nfs4_setfacl`、`mount` 以及 `/etc/fstab`。

### NFS 主要特性

Sun 最初在 20 世纪 80 年代后期发布了 NFS 协议。与其他许多许多协议一样，它经历了多次更新。

它允许我们将数据保留在中央主机上，客户端连接到该主机。客户端通过挂载目录（就像本地目录一样）连接到中央主机。该主机通常被用于在中央位置存储用户的家目录，用户可以通过修改 `/etc/fstab` 文件或使用 `mount` 命令来挂载这些目录。
