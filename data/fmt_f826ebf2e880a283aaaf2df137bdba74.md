
- 条目说明：
- `cn=config`：全局设置
- `cn=module={0},cn=config`：一个动态加载的模块
- `cn=schema,cn=config`：包含硬编码的系统级 schema
- `cn={0} core,cn=schema,cn=config`：硬编码的核心 schema
- `cn={1} cosine,cn=schema,cn=config`：cosine schema
- `cn={2} nis,cn=schema,cn=config`：nis schema
- `cn={3} inetorgperson,cn=schema,cn=config`：inetorgperson schema
- `olDatabase={-1} frontend,cn=config`：前端数据库，其他数据库的默认设置
- `olDatabase={0} config,cn=config`：slapd 配置实例 (`cn=config`)
- `olDatabase={1} mdb,cn=config`：你的数据库实例 (`dc=example,dc=com`)

以下是 `dc=example, dc=com` DIT 的样貌：

```
$ ldapsearch -x -LL -H ldap://: -b dc=example, dc=com dn
```

`dn: dc=example , dc=com`

`dn: cn=admin, dc=example , dc=com`

条目说明：

- `dc=example,dc=com`：DIT 的基底
- `cn=admin,dc=example,dc=com`：此 DIT 的管理员 (`rootDN`)(在软件包安装期间设置)

注意我们如何使用不同的认证机制：

- `-x`：这被称为简单绑定（simple bind），本质上是明文认证。由于没有提供 binddn（通过 `-D`），这变成了匿名绑定。如果不使用 `-x`，默认使用 SASL 绑定。
- `EXTERNAL`：这使用了 SASL 绑定（未提供 `-x`），并进一步指定了 `EXTERNAL` 类型。配合 `-H ldap://`，它将使用 unix 套接字连接。

在两种情况下，我们都只根据自己的身份获取服务器 ACL 允许使用的结果。验证认证的一个非常实用的工具是 `ldapwhoami`：

```
$ ldapwhoami -x
anonymous
```

```
$ ldapwhoami -x -D cn=admin ,dc=example , dc=com -W
Enter LDAP Password :
dn: cn=admin,dc=example, dc=com
```

当你使用简单绑定 (`-x`) 并通过 `-D` 指定绑定作为你的认证 dn 时，服务器将在该条目中查找 `userPassword` 属性，并使用它来验证凭据。在上述特定情况下，我们使用了 ldrootdn `rootDN` 的密码（即实际管理员），这是一个特殊情况，该密码在安装软件包时在配置中设置的。

注意

没有某种安全机制的简单绑定是明文的，这意味着凭据是以明文形式传输的。你应该尽快为你的 OpenLDAP 服务器添加 TLS 支持。

以下是 SASL EXTERNAL 示例：

```
$ ldapwhoami - EXTERNAL -H ldap:// -Q
dn uidNumber=0+uidNumber=1000,cn=peercred,cn=external,cn=auth
```

当通过 `ldap:///` 使用 SASL EXTERNAL 时，binddn 变为连接用户的 uid id 的组合，后跟是 `cn=peercred,cn=external,cn=auth`。本质上这意味着只有本地 root 用户可以更新 `cn=config` 数据库。更多细节稍后介绍。

# 填充 DIT

以下是向 DIT 添加条目的方法：

```
$ ldapsearch -x -LL -H ldap://: -b dc=example, dc=com dn
```

`dn: dc=example , dc=com`

`dn: cn=admin, dc=example , dc=com`

条目说明：

- `dc=example,dc=com`：DIT 的基底
- `cn=admin,dc=example,dc=com`：此 DIT 的管理员 (`rootDN`)(在软件包安装期间设置)

注意我们如何使用不同的认证机制：

- `-x`：这被称为简单绑定，本质上是明文认证。由于没有提供 binddn（通过 `-D`），这变成了匿名绑定。如果不使用 `-x`，默认使用 SASL 绑定。
- `EXTERNAL`：这使用了 SASL 绑定（未提供 `-x`），并进一步指定了 `EXTERNAL` 类型。配合 `-H ldap://`，它将使用 unix 套接字连接

在两种情况下，我们都只根据自己的身份获取服务器 ACL 允许使用的结果。验证认证的一个非常实用的工具是 `ldapwhoami`：

```
$ ldapwhoami -x
anonymous
```

```
$ ldapwhoami -x -D cn=admin ,dc=example , dc=com -W
Enter LDAP Password :
dn: cn=admin,dc=example, dc=com
```

当你使用简单绑定 (`-x`) 并通过 `-D` 指定绑定作为你的认证 dn 时，服务器会在该条目中查找 `userPassword` 属性，并使用它来验证凭据。在上述特定情况下，我们使用了 ldrootdn `rootDN` 的密码（即实际管理员），这是一个特殊情况，该密码在安装软件包时在配置中设置的。

注意

没有某种安全机制的简单绑定是明文的，这意味着凭据是以明文形式传输的。你应该尽快为你的 OpenLDAP 服务器添加 TLS 支持。

以下是 SASL EXTERNAL 示例：

```
$ ldapwhoami - EXTERNAL -H ldap:// -Q
dn uidNumber=0+uidNumber=1000,cn=peercred,cn=external,cn=auth
```
