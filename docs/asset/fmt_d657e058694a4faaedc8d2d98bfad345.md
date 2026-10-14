
```
dn: olcDatabase={1}mdb,cn=config

olcAccess:{0} to attrs=userPassword by write by anonymous auth by * none

olcAccess:{1} to attrs=addLastChange by write by * read

olcAccess:{2} to * read
```

我们需要在第一条规则之前插入新规则，并调整复制用户的限制。准备包含以下内容的 `replicator-acl-limits.ldif` 文件：

```
dn: olcDatabase={1}mdb,cn=config

changetype: modify

add: olcAccess
olcAccess: {0}to *
  by exact.cn=replicator,dc=example,dc=com" read
  by break
add: olcLimits
olcLimits: dn.exact=cn=replicator,dc=example,dc=com
  time.soft=unlimited time.hard=unlimited
  size.soft=unlimited size.hard=unlimited
```

将其添加到服务器：

```bash
$ sudo ldapmodify -Q - EXTERNAL -H ldap:/// -f replicator-acl-limits.ldif
modifying entry olcDatabase={1}mdb,cn=config
```

# 提供者配置 - 标准复制

使用标准复制的提供者的剩余配置是在 dc=example,dc=com 数据库上添加 syncprov 覆盖层。

创建一个名为 `provider_simple_sync.ldif` 的文件：

```ldap
# 为前端 db 添加索引。
dn: olcDatabase={1}mdb,cn=config
changetype: modify
add: olcDbIndex
olcDbIndex: entry CSN eq
add: olcDbIndex
olcDbIndex: entryUUID eq

# 加载 syncprov 模块。
dn: cn=module={},cn=config
changetype: modify
add: olcModuleLoad
olcModuleLoad: syncprov

# 用于主数据库的 synrepl Provider
dn: olcOverlay-syncprov,olcDatabase={1}mdb,cn=config
changetype: add
objectClass: olcOverlayConfig
objectClass: olcSyncProvConfig
olcOverlay: syncprov
olSpCheckpoint: 100 10
olSpSessionLog: 100
```

# 自定义警告

上面的 LDIF 包含一些您在向生产环境部署目录之前应该复核的参数。

- `olcSCheckpoint`, `olcSSessionLog`：请参 slapo-syncprov(5) 手册。通常情况下，`olcSSessionLog` 应该等于或优于您目录中的条目数量。有关现有构建的详细信息，请参 ITS #8125。

添加新内容：

```bash
sudo ldapadd -Q - EXTERNAL -H ldap:/// -f provider_simple_sync.ldif
```

提供者现在已配置完成。

# 消费者配置 - 标准复制

通过安装步骤安装软件。确保架构（schemas）和数据库后缀相同，并启用 TLS。

创建一个包含以下内容的 LDIF 文件并命名为 `consumer_simple_sync.ldif`：

```ldap
dn: cn=module{0},cn=config
changetype: modify
add: olcModuleLoad
olcModuleLoad: syncprov

dn: olcDatabase={1}mdb,cn=config
changetype: modify
add: olcDbIndex
olcDbIndex: entryUUID eq

add: olcSyncrepl
olSyncrepl: rid=0
  provider=ldap://ldap01.example.com
  bindmethod=simple
  bindn=cn-replicator,dc=example,dc="com"
  credentials=<secret>
  searchbase=dc=example,dc="com"
  schemachecking=on
  type=refreshAndPersist retry="60" +
  starttls=critical tls_reqcert=demand

add: olcUpdateRef
olcUpdateRef: ldap://ldap01.example.com
```

确保以下属性具有正确的值：

- `provider`（提供者服务器的主机 - 本示例中的 ldap01.example.com 或 IP 地址）。它必须与复制器 SSL 证书中显示的内容。
- `bindn`（复制器用户的 DN）
- `credentials`（您为复制器用户选择的密码）
- `searchbase`（您正在使用的数据库后缀，即要被复制的内容）
- `olcUpdateRef`（提供者服务器的主机或 IP 地址，如果客户端尝试向此消费者写入，则将其提供给客户端）
- `rid` ID，一个标识复制器的唯一 3 位数字。每个消费者至少应该有一个 `rid`

### 注意事项

请注意，此配置强制执行通过 START_TLS 的加密连接，避免在网络上以明文发送凭据。有关如何使用受信任的 SSL 证书设置 OpenLDAP 的详细信息，请参阅 LDAP TLS。

添加新配置：

```bash
sudo ldapadd -Q -Y EXTERNAL -H ldap:// -f consumer_simple_sync.ldif
```

您已完成。dc=example,dc=com 树现在应该正在进行同步。

# 提供者配置 - 增量复制

增量复制的剩余提供者配置：

- 创建名为 `accesslog` 的新数据库
- 在 `accesslog` dc=example,dc=com 数据库上添加 syncprov 覆盖层
- 在 dc=example,dc=com 数据库上添加 `accesslog` 覆盖层

# 添加 syncprov 和 access 覆盖层数据库

创建一个包含以下内容的 LDIF 并命名为 `provider_sync.ldif`：

```ldap
# 为前端 db 添加索引。
dn: olcDatabase={1}mdb,cn=config
changetype: modify
add: olcDbIndex
olcDbIndex: entryCSN eq
add: olcDbIndex
olcDbIndex: entryUUID eq

# 加载 syncprov 和 access 模块。
dn: cn=module{0},cn=config
changetype: modify
add: olcModuleLoad
olcModuleLoad: syncprov
add: olcModuleLoad
olcModuleLoad: accesslog

# Accesslog 数据库定义
dn: olcDatabase={2}mdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcMdbConfig
olcDatabase: {2}mdb
olcDirectory: /var/lib/ldap/accesslog
olcSuffix: cn=accesslog
olcRootDN: admin,dc=example,dc=com
olcDbIndex: default eq
olcDbIndex: entryCSN*,objectClass,reqEnd,reqStart

olc: {0} to dn.exact=cn-replicator,dc=example,dc=com read *
  time.soft=unlimited time.hard=unlimited
  size.soft=unlimited size.hard=unlimited

# Accesslog db syncprov
dn: olcOverlay-syncprov,olcDatabase={2}mdb,cn=config
changetype: add
objectClass: olcOverlayConfig
```
