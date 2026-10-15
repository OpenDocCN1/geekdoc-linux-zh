
此时，你应该只需不带任何参数地运行 `slapd`，就可以将其启动。

### 389 目录服务器：另一款开源 LDAP 服务器

与 OpenLDAP 一样，389 目录服务器（port389.org）也是密歇根大学所做工作的延伸。不过，在重新以开源项目形式回归之前，它曾在商业领域（Netscape）发展数年。

有很多理由让你考虑将 389 目录服务器作为 OpenLDAP 的替代品，但其出色的文档是一个明显的优势。389 目录服务器附带多份专业级的管理和使用指南，包括详细的安装和部署说明。

389 目录服务器的其他几个关键特性包括：

- 多主复制（Multimaster replication），用于容错和高写入性能
- Active Directory 用户和组同步
- 用于用户、组和服务器管理各个方面的图形控制台
- 在线、零停机、基于 LDAP 的架构、配置、管理和树内访问控制信息（ACIs）更新

截至撰写本文时，389 目录服务器似乎比 OpenLDAP 拥有更活跃的开发社区。对于新安装，我们通常建议选择它而非 OpenLDAP。

从管理角度来看，这两款开源服务器的结构和操作惊人地相似。这或许并不太令人意外，因为这两个软件包都构建在相同的原始代码基础之上。

### 用 LDAP 替代 /etc/passwd 和 /etc/group

客户端的 LDAP 支持相对容易添加。有些系统默认安装了必要的 `nss_ldap` 包，但如果没有，通常也会以可选方式提供该包。这个包中包含一个 PAM 模块，除了名称服务切换（name service switch）之外，你还可以将 LDAP 与可插拔认证模块（PAM）一起使用。（关于如何将 UNIX 和 Linux 系统与基于 Active Directory 的 LDAP 集成，请参阅第 30 章“与 Windows 协作”。）

`nss_ldap` 的客户端 LDAP 默认值设置在 `/etc/ldap.conf` 中，该文件与 `/etc/openldap/ldap.conf`（在第 732 页描述）共享格式，但包含针对名称服务和 PAM 上下文的额外选项。你还必须编辑每个客户端上的 `/etc/nsswitch.conf` 文件，为你要 LDAP 化的每种数据类型添加 `ldap` 作为来源。（`nsswitch.conf` 的改动会让 C 库将请求传递给 `libnss_ldap` 库，然后该库利用 `/etc/ldap.conf` 中的信息来确定如何执行 LDAP 查询。详细信息请参见第 739 页的“为管理信息源排序”。）

RFC2307 定义了从传统 UNIX 数据集（如 `passwd` 和 `group` 文件）到 LDAP 命名空间的标准映射。对于在 UNIX 环境中使用 LDAP 的系统管理员来说，它至少在理论上是一份有用的参考文档。但实际上，这些规范对计算机来说比对人类更容易阅读；你最好还是看看示例。

Padl Software 提供了一套免费的 Perl 脚本，用于将现有的平面文件或 NIS 映射迁移到 LDAP。你可以从 padl.com/OSS/MigrationTools.html 获取，这些脚本运行起来很简单。它们既可以用作过滤器来生成 LDIF，也可以直接针对在线服务器运行以直接上传数据。例如，`migrate_group` 脚本会将 `/etc/group` 中的这一行：

```
csstaff:x:2033:evi,matthew,trent
```

转换为以下 LDIF：

```
dn: cn=csstaff,ou=Group,dc=domainname,dc=com
cn: csstaff
objectClass: posixGroup
objectClass: top
```

```
memberOf: CN=Enterprise Admins,CN=Users,DC=boulder,DC=atrust,DC=com
name: ned
sAMAccountName: ned
userPrincipalName: ned@boulder.atrust.com
lastLogonTimestamp: 129086952498943974
mail: ned@atrust.com
```

`ldapsearch` 的 `-h` 和 `-p` 选项分别指定你要查询的 LDAP 服务器的主机名和端口。

你通常需要向 LDAP 服务器进行身份验证。在这种情况下，`-x` 选项请求简单认证（相对于 SASL）。`-D` 选项标识具有执行查询所需权限的用户帐户的可分辨名称，`-W` 选项使 `ldapsearch` 提示你输入相应的密码。

`-b` 选项告诉 `ldapsearch` 在 LDAP 层级结构中的哪个位置开始搜索。这个参数称为 `baseDN`；因此用 `b` 表示。默认情况下，`ldapsearch` 会返回 `baseDN` 以下所有匹配的条目；你可以通过 `-s` 选项来调整此行为。

最后一个参数是一个“过滤器”，用于描述你要搜索的内容。它不需要选项标志。这个过滤器 `cn=ned*` 返回所有通用名称以 “ned” 开头的 LDAP 条目。过滤器被引号括起来，以防止星号被 shell 的通配符扩展。

如果你想提取给定 `baseDN` 以下的所有条目，只需使用 `objectClass=*` 作为搜索过滤器——或者省略过滤器，因为这是默认行为。

过滤器之后的任何参数都用于选择要返回的特定属性。例如，如果你在上面的命令行中添加了 `mail givenName`，`ldapsearch` 将只返回匹配条目的这些属性。

### LDAP 与安全

传统上，LDAP 更多地是像电话簿一样使用，而不仅仅如此，因此在不加密的情况下发送数据通常是可以接受的。结果，“标准” LDAP 实现通过 TCP 端口 `389` 提供未加密的访问。然而，我们强烈建议不要使用未加密的 LDAP 来传输身份验证信息，即使密码是单独进行哈希或加密的。

作为替代方案，在大多数情况下（包括 Microsoft 环境），客户端和服务器端都提供了 LDAP-over-SSL（称为 LDAPS，通常在 TCP 端口 `636` 上运行）。这种访问方式更受青睐，因为它保护了查询和响应中包含的信息。尽可能使用 LDAPS。

像 LDAP 这样复杂的系统不可避免地存在被错误配置从而削弱安全性的可能。当然，它也可能包含一些普通的老式安全漏洞。管理员需自行注意。

NIS 目录中一个以 NIS 域命名的子目录。映射文件的确切名称和数量取决于所使用的哈希库。文件可以按每个键进行搜索，每个键对应一个映射（文件）。例如，在域 cssuns 中，`/etc/passwd` 映射的 DB 文件可能是：

```
/var/yp/cssuns/passwd.byname
/var/yp/cssuns/passwd.byuid
```

`makedbm` 命令从平面文件生成 NIS 映射。但是，你不需要直接调用此命令；`/var/yp` 中的 Makefile 会生成所有常见的 NIS 映射。修改系统文件后，`cd` 到 `/var/yp` 并运行 `make`。`make` 命令会检查每个文件的修改时间，与由其派生的映射的修改时间进行比较，并为每个需要重建的映射运行 `makedbm`。

在 HP-UX 系统上，使用名为 `ypmake` 的命令来代替 `make`。

`ypxfr` 命令将映射从主服务器复制到从服务器。`ypxfr` 是一个拉取命令；必须在每个从服务器上运行它，以使该服务器导入映射。从服务器通常会定期执行 `ypxfr`，只是为了确认它们拥有最新的映射；你可以使用 `cron` 来控制执行频率。

映射复制的默认实现效率有些低下。在大多数系统上，可以在主服务器上运行一个名为 `ypxfrd`（或 `rpc.ypxfrd`）的守护进程，以加快对 `ypxfr` 请求的响应。`ypxfrd` 绕过了正常的 NIS 协议，直接分发映射文件的副本。不幸的是，不同系统上映射文件以不同的数据库格式和字节顺序存储，因此使用 `ypxfrd` 会引入一些潜在的不兼容问题。

`yppush` 是一个在主服务器上使用的“推送”命令。它实际上并不传输任何数据，而是指示每个从服务器执行一次 `ypxfr`。NIS 目录中的 Makefile 使用 `yppush` 命令来确保新更新的映射被传播到从服务器。

名为 `ypservers` 的特殊映射不对应任何平面文件。此映射包含域中所有服务器的列表。当使用 `ypinit` 设置域时，它会自动构建。当主服务器需要将映射分发给从服务器时，会检查其内容。

后期的 `ypbind` 版本会定期检查，以确保它们正在处理对 NIS 域响应最快的服务器。这比传统实现有所改进，后者会固定在一个特定服务器上。

NIS 包含一些用于检查映射、查找每个服务器使用的映射版本以及控制客户端与服务器之间绑定的次要命令。NIS 命令和守护进程的完整列表见表 19.4。

### 表 19.4 NIS 命令和守护进程

| 程序 | 描述 |
|---|---|
| `ypserv` | 是 NIS 服务器守护进程，在启动时启动 |
| `ypbind` | 是 NIS 客户端守护进程，在启动时启动 |
| `domainname` | 设置机器的 NIS 域（在启动时运行） |
| `ypxfr` | 从主服务器下载映射的当前版本 |
