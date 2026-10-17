
`objectclass`: `person`

`objectclass`: `organizationalPerson`

`objectclass`: `posixAccount`

`cn`: `icuser1`

`sn`: `icuser1`

`uid`: `icuser1`

`userPassword`: `icuser1x`

`uuidnumber`: `50001`

`gidnumber`: `500`

`homedirectory`:`/home/icuser1`

`logshell`:`/bin/bash`

LDAP 服务器 DS 文件中的 `adminDN` 条目为 `cn=ldapadm4,o=ibm`。
并没有特殊理由导致管理员 DN 在目录中仅有两个层级，而添加的 `icuser1` DN 有三层，这看起来像是一个逻辑合理的组织结构。目录层级也是通过 CMS `LDAPADD` `EXEC` 创建的。

使用 CMS 命令从目录中检索条目：

```
ldapsr -h 9.12.4.92 -D "cn=ldapadm4,o=ibm" -w ldapmx -b "cn=icuser1,ou=icc,o=ibm" "objectclass=*"
```

如预期的输出如下：

```
cn=icuser1, ou=icc, o=ibm
objectclass=top
objectclass=person
objectclass=organizationalPerson
objectclass=posixAccount
cn=icuser1
sn=icuser1
uid=icuser1
userpassword=icuser1x
uuidnumber=50001
gidnumber=500
homedirectory=/home/icuser1
loginshell=/bin/bash
```

`userPassword` 以明文形式输入，除非 DS CONF 文件中的密码加密选项 `pwEncryption` 设置为加密 `userPassword` 属性，否则它在目录中将保持明文。当 `pwEncryption` 参数设置从 `none` 为 `SHA` 时，`userPassword` 将通过 SHA 算法加密。对于已经未加密的情况下输入到目录的条目，有一个工具 `db2passwd` 可用于加密明文密码。对加密的 `userPassword` 进行简单的 `ldapsch` 搜索结果将不会显示 `userpassword=NOT`。实际返回的是一个标记为 SHA 和加密密码的标签，这在 CMS 中是不可打印的。此加密仅适用于 LDBM 数据库。

上述 CMS `LDAPSEARCH` 上的选项 `-Dcn=idldapm4;o=ibm` 和 `-w idldapm` 是必须的，因为 DS CONF 文件参数 `allowAnonymousBinds` 被设置为 `off`，因此不允许匿名绑定。使用密码 `idldapm` 的名称 `idldapm4` 用于显式绑定到 LDAP 服务器。如果将 `allowAnonymousBinds` 参数设置为 `on` 且允许匿名绑定，则 `LDAPSRCH` 将可以使用指定的 `-D` 和 `-w` 选项工作。

LDBM 后端在 z/VM LDAP 服务器中使用以下设置：
DS CONF:

```
database LDBM GLDBLD31
suffix="o=ibm"
```

## 11.2.2 z/VM LDBM 和本地认证

z/VM LDAP 服务器允许客户端在使用 RACF 验证所提供的密码时，绑定到 LDBM 后端的条目。Oracle 用户名的条目（密码除外）维护在 LDBM 中，这与 `icuser1` 的 LDBM 情况一样。在 LDBM 目录条目和 z/VM LDAP 服务器配置文件中均有几处不同。`icuser2` 是用于使用 z/VM LDAP 这种身份验证方法的 Oracle 用户名。显示了 `icuser2` 的目录条目。

```
cn=icuser2,ou=icc,o=ibm
objectclass=top
objectclass=person
objectclass=organizationalPerson
objectclass=ibm-nativeAuthentication
objectclass=posixAccount
cn=icuser2
sn=icuser2
ibm-nativeid=ICCUSER2
uid=icuser2
uidnumber=50002
gidnumber=500
homedirectory=/home/iccuser2
loginshell=/bin/bash
```

注意，LDBM 目录条目中没有密码属性和值对。指定了 `objectclass=ibm-nativeAuthentication`，其定义包含了 `ibm-native` 属性。该 `objectclass` 允许使用 `ibm-native` 属性，这就是与 z/VM LDAP 本地认证的连接。RACF ID 必须以大写添加到目录条目中；否则本地认证将失败。

通过来自 CMS 的以下 RACF 命令将 `iccuser2` 添加到 z/VM RACF：

```
rac au (iccuser2) pass(password)
rac al (iccuser2) noexpired password(ldap22)
```

运行了 `alteruser` 命令，以防止 `iccuser2` 在首次访问 RACF 时需要更改密码。

在 z/VM LDAP DS CONF 文件中使用以下三个参数设置进行本地认证：

```
useNativeAuthchecked
nativeUpdateAllowed on
nativeAuthSubtree "ou=icc,o=ibm"
```

## 11.2.3 z/VM SDBM

z/VM LDAP 服务器提供了对存储在 RACF SDBM 中的 RACF 用户信息的访问。RACF 组和连接信息也是可用的，但本文未进行讨论。SDBM 也被称为 LDAP 服务器的 RACF 后端。DBM 数据库允许使用 RACF ID 和密码进行目录认证。z/VM RACF 必须对 LDAP 服务器可用以便与 RACF 通信，且 LDAP 服务器必须配置为使用 SDBM。SDBM 限制了 DN 的格式，因为 DN 必须匹配底层 RACF 架构。中 Oracle 用户的完整 DN 包含两个必需属性：`racfid` 和 `profiletype`。在讨论中，`profiletype` 的属性值始终为 `user`。在其他上下文中，`group` 对于 `profiletype` 也是有效的。此处使用的 SDBM 后缀是 `cn=racfvm, o=ibm, c=us`。z/VM LDAP 服务器可以配置为同时支持 LDBM 和 SDBM，但此处讨论仅在 DS CONF 文件配置了 SDBM。

所有。关于 Oracle 用户 `icuser1` 的一切都存在于 RACF SDBM 数据库中。以下是 SDBM 的 DS CONF 设置：

```
database LDBM GLDBLD31
suffix="o=ibm"
```

z/VM LDAP 服务器管理员 `ldap2` 在 LDAP 服务器首次启动时，通过 `addUser` 命令添加到 RACF。用户 `icuser1` 通过以下命令添加到 z/VM RACF SDBM：

```
ldapadd -h 9.12.4.92 -D "cn=ldapadm4,o=ibm" -w ldapmx -b "cn=icuser1,ou=icc,o=ibm"
```

此 RACF 文件的内容为：

```
dn=icuser1,profiletype=user,cn=racfvm,o=ibm,c=us
objectclass=user
racfid=icuser1
```

使用 `rac al (icuser1) noexpired password(ldap22)` 命令为 `icuser1` 设置密码。通过 `ldapsch`：

```
ldapsr -h 9.12.4.92 -D "cn=ldapadm4,o=ibm" -w ldapmx -b "cn=icuser1,ou=icc,o=ibm"
```

返回关于 `rac1` 的如下信息：

```
racfid=rac1,profiletype=user,cn=racfvm,o=ibm,c=us
racfid=RAC1
racauthordate=12/18/07
racowner=RACFID-LDAPDM2,PROFILETYPE=USER,CN=RACFVM,O=IBM,C=US
passwordinterval=30
racpasswordchanged=12/18/07
racdefaultgroup=RACFID-SYS1,PROFILETYPE=GROUP,CN=RACFVM,O=IBM,C=US
raclastaccess=01/08/12:52:57
raclogondays=SUNDAY
raclogondays=MONDAY
raclogondays=TUESDAY
```
