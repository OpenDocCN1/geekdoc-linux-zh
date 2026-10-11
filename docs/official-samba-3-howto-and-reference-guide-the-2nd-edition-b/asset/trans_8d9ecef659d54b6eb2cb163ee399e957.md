
并且，与 MS Windows 2000 和 Active Directory 不同，Samba-3 不支持嵌套组。

### 10.4.4.7 安全性与 sambaSamAccount

在讨论目录中 sambaSamAccount 条目的安全性时，有两点重要事项需谨记。

- *切勿*在未加密的 LDAP 会话中检索 SambaLMPassword 或 SambaNTPassword 属性值。
- *切勿*允许非管理员用户查看 SambaLMPassword 或 SambaNTPassword 属性值。

这些密码哈希值是明文等价物，可被用于冒充用户而无需推导出原始的明文字符串。有关 LM/NT 密码哈希值详细信息的更多内容，请参见第 10 章，“账户信息数据库”。

为了解决第一个安全问题，*ldap ssl* smb.conf 参数默认要求在联系目录服务器时使用加密会话（*ldap ssl=on*），并使用**636**作为默认端口。当使用 OpenLDAP 服务器时，可以使用 StartTLS LDAP 扩展操作来替代 LDAPS。在这两种情况下，我们都强烈建议使用安全的通信协议（因此不要设置 *ldap ssl=off*）。

请注意，LDAPS 协议已不再推荐，取而代之的是 LDAPv3 StartTLS 扩展操作。然而，OpenLDAP 库仍然支持这种较旧的方法来保护客户端和服务器之间的通信。

第二个安全预防措施是防止非管理用户从目录中收集密码哈希值。这可以通过在 *slapd.conf* 中使用以下 ACL 来完成：

```
## 允许 "ldap admin dn" 访问，但拒绝其他人
access to attr=SambaLMPassword,SambaNTPassword
by dn="cn=Samba Admin,ou=People,dc=quena,dc=org" write
by * none
```

### 10.4.4.8 sambaSamAccounts 的 LDAP 特殊属性

sambaSamObject ObjectClass 由下表所示的属性组成：表 10.2 和表 10.3。

这些参数中的大多数仅在 Samba 作为域的 PDC 时起作用（有关如何配置 Samba 作为 PDC 的详细信息，请参见第 4 章，“域控制”）。以下四个属性仅在值是非默认值时才会与 sambaSamAccount 条目一起存储：

- sambaProfilePath
- sambaHomeDrive

这些属性仅在值是非默认值时才会与 sambaSamAccount 条目一起存储。例如，假设 MORIA 已被配置为 PDC，并且在其 smb.conf 文件中定义了 logon home = \\%L\%u。当名为 "becky" 的用户登录到域时，登录主目录字符串将扩展为 \\MORIA\becky。如果在条目 "uid=becky,ou=People,dc=samba,dc=org" 中存在 sambaHome 属性，则使用此值。但是，如果此属性不存在，则使用 logon home 参数的值来代替。仅当值是非默认值（例如，\\MOBY\becky）时，Samba 才会将属性值写入目录条目。

### 10.4.4.9 sambaSamAccount 的 LDIF 条目示例

以下是一个可用的 LDIF，演示了 SambaSamAccount ObjectClass 的使用：

```
dn: uid=guest2, ou=People,dc=quenha,dc=org
sambaLMPassword: 878D8014606CDA29677A44EFA1353FC7
sambaPwdMustChange: 2147483647
sambaPrimaryGroupSID: S-1-5-21-2447931902-1787058256-3961074038-513
sambaNTPassword: 552902031BEDE9EFAAD3B435B51404EE
sambaPwdLastSet: 1010179124
sambaLogonTime: 0
objectClass: sambaSamAccount
uid: guest2
sambaKickoffTime: 2147483647
sambaAcctFlags: [UX     ]
sambaLogoffTime: 2147483647
sambaSID: S-1-5-21-2447931902-1787058256-3961074038-5006
sambaPwdCanChange: 0
```

以下是同时使用 sambaSamAccount 和 posixAccount ObjectClasses 的 LDIF 条目：

```
dn: uid=gcarter, ou=People,dc=quenha,dc=org
sambaLogonTime: 0
displayName: Gerald Carter
sambaLMPassword: 552902031BEDE9EFAAD3B435B51404EE
sambaPrimaryGroupSID: S-1-5-21-2447931902-1787058256-3961074038-1201
objectClass: posixAccount
objectClass: sambaSamAccount
sambaAcctFlags: [UX     ]
userPassword: {crypt}$pM2e]8jRkzqgo
uid: gcarter
uidNumber: 9000
cn: Gerald Carter
loginShell: /bin/bash
logoffTime: 2147483647
gidNumber: 100
sambaKickoffTime: 2147483647
sambaPwdLastSet: 1010179230
sambaSID: S-1-5-21-2447931902-1787058256-3961074038-5004
homeDirectory: /home/soria/gcarter
sambaPwdCanChange: 0
sambaPwdMustChange: 2147483647
sambaNTPassword: 878D8014606CDA29677444EFA1353FC7
```

### 10.4.4.10 密码同步

Samba-3 及更高版本可以更新与账户一起存储的非 Samba (LDAP) 密码。使用 pam_ldap 时，允许一次更改 UNIX 和 Windows 密码。ldap passwd sync 选项可以具有表 10.4 中显示的值。更多详细信息可在 smb.conf 手册页中找到。

### 10.4.4.11 使用 OpenLDAP Overlay 进行密码同步

Howard Chu 编写了一个名为 smbK5pwd 的特殊 overlay。当执行 LDAP_EXOP_X_MODIFY_PASSWORD 操作时，该工具会修改 OpenLDAP 条目中的 SambaNTPassword、SambaLMPassword 和 Heimdal 哈希值。

该 overlay 随 OpenLDAP-2.3 一起提供，可在 contrib/slapd-modules/smbK5pwd 子目录中找到。此模块也可用于 OpenLDAP-2.2。

## 10.4.5 MySQL

时不时地，会出现一些看似（对他们而言）很棒的新想法。将用户账户存储在 SQL 后端中就是其中之一。希望这样做的人最适合了解这对他们有什么好处。这听起来可能像是在推卸责任，但事实上，我们无法记录有关为什么对大多数 Samba 用户而言效用有限的某些事情可能对其他人有意义的每个小细节。无论如何，以下说明应该能帮助坚定的 SQL 用户实现一个可用的系统。Samba 团队不积极维护这些账户存储方法。

### 10.4.5.1 创建数据库

你可以设置自己的表并指定字段名给 pdb_mysql（参见表 10.6 中的列名），或者使用默认表。文件 examples/pdb/mysql/mysql.dump 包含创建所需表的正确查询。使用命令：

```
root# mysql -uusername -hhostname -ppassword \
    database_name < /path/to/samba/examples/pdb/mysql/mysql.dump
```

### 10.4.5.2 配置

此插件缺乏良好的文档，但这里有一些简要信息。在 smb.conf 的 passdb backend 变量中添加以下内容：

```
passdb backend = [other-plugins] mysql:identifier [other-plugins]
```

标识符可以是任何字符串，只要它不与其他插件的标识符或 pdb_mysql 的其他实例冲突。如果你在 passdb backend 中指定了多个 pdb_mysql.so 条目，则还需要使用不同的标识符。

可以通过 [global] 部分的 smb.conf 文件提供额外选项。参见表 10.5。

![](img/86d74c6cc862465e3a42e6dc3c90935a_228_0.png)

由于 MySQL 用户的密码存储在 smb.conf 文件中，因此 smb.conf 文件应设置为仅运行 Samba 的用户可读。这被视为一个安全漏洞，很快将会修复。

列的名称在表 10.6 中给出。默认列名可在示例表转储中找到。

你可以在每个列的名称后面加一个冒号 (:)，以指定更新表格时要更新的列。你也可以在冒号后面什么都不指定，在这种情况下，字段数据将不会更新。将列名称设置为 NULL 表示不应使用该字段。

示例 10.4.2 显示在示例 10.4.2 中。

### 10.4.5.3 使用明文密码或加密密码

我强烈反对使用明文密码；然而，你可以使用它们。

如果你想使用明文密码，请将 ‘identifier:lanman pass column’ 和 ‘identifier plain pass column’ 设置为 ‘NULL’（不带引号），并将 ‘identifier:plain pass column’ 设置为包含明文密码的列的名称。

如果你使用加密密码，请将 ‘identifier:plain pass column’ 设置为 ‘NULL’（不带引号）。这是默认设置。

