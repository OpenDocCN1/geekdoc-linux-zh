
# 只有拉取文件时才有效

`read only = false`

# 执行传输时的 UID 和 gid

`uid = root`

`gid = root`

# 允许连接的主机列表

`hosts = distribution_master_hostname`

可以设置许多其他选项，默认值是合理的。此配置将操作限制在 `/etc` 目录并仅允许列出的主机访问。从用户或客户端的角度来看，你可以使用 `rsync` 将文件送到服务器，格式为 `目标主机名:模块`，这映射到上面的模块。如果你想在拉取模式下设置 `rsync`（从中央 `rsync` 服务器拉取文件），上面的行仍然有效，但你可能希望进一步收紧限制。

## LDAP 数据的结构

例如，这里有一个典型的（但简化的）`/etc/passwd` 行，它以 nLDAP 条目的形式暴露出来：

```
uid: shopper

cn: Grace Hopper

userPassword: [crypt]$1pZaGA2RL$MPDjoc0afuhHY6k8HQFP0

loginShell: /bin/bash

uidNumber: 1202

gidNumber: 1202

homeDirectory: /home/shopper
```

这种表示法是 LDIF（LDAP 数据交换格式）的一个简单示例，该格式被大多数与 LDAP 相关的工具和服务器实现。LDAP 数据可以轻松地在纯文本之间相互转换，这是其成功的原因之一。

条目通过使用“区分名称”（distinguished names，即属性名: dn）组织成层级结构，这些名称形成了某种搜索路径。例如，我们上述用户的 dn 为：

```
uid=shopper,ou=People,dc=navy,dc=mil
```

与 DNS 一样，“最高有效位”位于右侧。在这里，DNS 名称 `navy.mil` 被用于构建 LDAP 层级的顶层。它被拆分为两个域组件（dc）“navy”和“mil”，但这仅是几种常见约定之一。

每个条目恰好有一个区分名称。因此，条目层级结构看起来像一棵没有环的简单分支树。然而，也预留了条目之间的符号链接以及指向其他服务器的引用规定。

LDAP 条目通常通过对象类（objectClass）属性进行模式化，这些属性指定了条目可以包含的属性，其中某些属性可能是有效性必需的。模式还为每个属性分配了数据类型。对象类以传统的面向对象方式进行嵌套和组合。对象类树的顶层是名为 `top` 的类，它仅规定条目必须有一个 `objectClass` 属性。

表 19.2 显示了一些常见的 LDAP 属性，它们的含义可能并非一而易见。

### 表 19.2 LDAP 层级中常见的某些属性名

| 属性 | 缩写 | 含义 |
| --- | --- | --- |
| o | Organization (组织) | 通常标识站点的顶层条目 |
| ou | Organizational unit (组织单元) | 逻辑划分，例如“营销部” |
| cn | Common name (通用名称) | 表示条目最自然的名称 |
| dc | Domain component (域组件) | 用于基于 DNS 模型构建层级结构的站点 |
| objectClass | Object class (对象类) | 该条目属性遵循的模式 |

*a. 通常不用于根据 DNS 建立 LDAP 层级结构的站点*

## LDAP 的意义

在对它有一些经验之前，LDAP 可能是一个难以捉摸的概念。LDAP 本身并不解决任何特定的管理问题。没有某项是为 LDAP 量身定制的要处理的“首要任务”，而且不同人员部署 LDAP 服务器的原因也大不相同。因此，在进入安装和配置 OpenLDAP 的具体细节之前，回顾一下你可能想要在你的站点中调查并使用 LDAP 的某些原因，也许是值得的。

以下是它的优点：

- LDAP 可以作为用户信息的中心存储库，包括从电话号码、家庭地址到用户名和密码的所有信息。
- 同样，你可以使用 LDAP 分发辅助应用程序的配置信息。大多数邮件系统——`sendmail`、`Exim` 和 `Postfix`——都可以从 LDAP 获取大部分路由信息，而这实际上是 LDAP 最流行的应用之一。`Apache` 服务器和 `autofs` 自动挂载器等各种工具也可以配置为关注 LDAP。随着时间的推移，LDAP 支持可能会变得越来越普遍。
- LDAP 让应用程序（即使是由其他团队和其他部门编写的）能够验证用户，而无需担心账户管理的具体细节。
- LDAP 数据的更改会立即生效，并对所有主机和客户端应用程序立可见。
- 通过 `ldapsearch` 等命令行工具可以轻松访问 LDAP 数据。此外，LDAP 受到 Perl 和 Python 等常用脚本语言的支持（通过使用库）。因此，LDAP 是分发本地脚本和管理实用程序配置信息的极佳方式。
- 有许多出色的 Web 工具用于管理 LDAP，例如 `phpLDAPadmin` (`phpldapadmin.sourceforge.net`) 和 Directory Administrator (`diradmin.open-it.org`)。这些工具非常易用，你完全可以拆开箱子开始玩，而无需阅读说明书。
- LDAP 作为公共目录服务得到了良好支持。大多数邮件客户端都支持使用 LDAP 访问用户目录。许多网络浏览器还通过 URL 类型支持简单的 LDAP 搜索。
- 微软的 Active Directory（活动目录）架构基于 LDAP，当前版本的 Windows Server 包含了扩展（最初称为“Services for UNIX”），然后是“Windows Security and Directory Services for UNIX”

## OpenLDAP：传统的开源 LDAP 服务器

“UNIX，”而现在是“Windows Server 2008 UNIX Interoperability Components”，这些组件促进了 UNIX 用户和组的映射。有关将你的 UNIX 系统与基于 Active Directory 的 LDAP 集成的更多信息，请参阅第 30 章“与 Windows 协作”。

### LDAP 文档与规范

关于 LDAP 的一个很好的通用介绍是《LDAP for Rocket Scientists》，它涵盖了 LDAP 架构和协议。你可以在 `zytrac.com/books/ldap` 在线找到它。另一个良好的信息来源是 LDAP 相关的 RFC，它们非常多且多样。作为一个整体，它们往往给人留一种极其复杂的印象，表 19.3 列出了其中的一些要点。

### 表 19.3 列出的一些要点

| RFC | 标题 |
| --- | --- |
| 2307 | 使用 LDAP 的方法 |
| 2820 | 访问控制要求 |
| 2849 | 数据交换格式 |
| 3112 | 模式 |
| 3672 | LDAP 中的条目 |
| 4511 | 目录模型 |
| 4512 | 身份验证方法 |
| 4513 | 条目的字符串表示 |
| 4514 | 过滤器表示 |
| 4515 | 定位符 |
| 4516 | 句法与匹配规则 |
| 4519 | 应用程序的模式 |

### 共享系统文件

这些是你需要的行：

```
database bdb

suffix "dc=mydomain,dc=com"

rootdn cn=admin,dc=mydomain,dc=com

rootpw [crypt]$...

directory /var/lib/ldap
```

数据库设置为 `bdb`，对于存储在内部的数据是可以的。可以使用其他后端，包括动态创建数据的方法。

`suffix` 是你的“LDAP 基准”。它是你的 LDAP 命名空间的根，类似于你的 DNS 名称。事实上，这个示例说明了使用 DNS 域名作为 LDAP 基准的常见做法。

`rootdn` 是管理员的名称，`rootpw` 是管理员的 UNIX 格式密码。注意，通往管理员名称的域组件也必须指定。你可以从 `/etc/shadow` 复制密码（如果你没有使用 MD5），或者使用简单的 Perl 单行命令生成它：

```
perl -e "print crypt('password',salt);"
```

其中 `passed` 是你想要的密码，`salt` 是任意的两个字符字符串。

`slapd.conf` 文件中的密码。由于存在此密码，请确保你的 `slapd.conf` 文件权限为 600，且文件归 `root` 所有。

编辑 `/etc/ldap.conf` 以设置 LDAP 客户端请求的默认服务器和基准。这非常简单——只需 `host` 参数设置为你的服务器，并将 `base` 设置为与 `slapd.conf` 中的 `suffix` 相同的值。（确保这两行都已取消注释。）

到此，你应该能够通过简单无参数运行来启动 `slapd`。

## 389 Directory Server：替代开源 LDAP 服务器

与 OpenLDAP 一样，389 Directory Server (`port389.org`) 是密歇大学工作的扩展。然而，它在商业领域（在 Netscape）度过了几年时间，然后作为一个开源项目回归。

考虑将 389 Directory Server 作为 OpenLDAP 的替代方案有很多理由，但其卓越的文档是一个明确的优势。389 Directory Server 提供了多份专业级管理和使用指南，包括详细的安装和部署说明。

389 Directory Server 的其他一些功能包括

- 多主复制，以实现容错能力和高写入性能
- Active Directory 用户和组同步

## 使用 LDAP 代替 /etc/passwd 和 /etc/group

- 适用于用户、组和服务器管理所有方面的图形化控制台
- 基于 LDAP 的在线、零停机、架构、配置、管理以及树内访问控制信息 (ACI) 的更新

截至本文编写时，389 Directory Server 的开发社区似乎比 OpenLDAP 更活跃。对于新安装的系统，我们通常推荐使用它替代 OpenLDAP。

从管理的角度来看，这两个开源服务器的结构和操作非常相似。这可能并不令人意外，因为这两个软件包都是基于同一段原始代码库构建的。

## 使用 LDAP 代替 /etc/passwd 和 /etc/group

添加客户端 LDAP 支持相对容易。某些系统默认安装了必要的 LDAP 软件包，但如果没有安装，它们通常会将该包作为一个选项提供。该软件包包含一个 PAM 模块，允许我们在使用名称服务之外，通过可插拔认证模块使用 LDAP。（有关将 UNIX 和 Linux 系统与基于目录的 LDAP 集成的更多信息，请参阅第 30 章“与 Windows 协作”）。

`nss_ldap` 的客户端默认设置在 `/etc/ldap.conf` 中，其格式与 `/etc/open/ldap.conf`（见第 732 页）相同，但为名称服务和 PAM 上下包含了额外的选项。你还必须编辑每个客户端上的 `/etc/nsswitch.conf` 文件，将 LDAP 添加为你想要进行 LDAP 化的每类型数据的源。（`nsswitch conf` 更改了 C 库请求以使用 `libnss_ldap` 库……参见第 739 页的“优先考虑管理信息的源”）。

`RFC2307` 定义了从传统 UNIX 数据集（如密码和组文件）到 LDAP 命名空间的标准映射。对于我们在 UNIX 环境中使用 LDAP 的系统管理员来说，这至少在理论上是一份非常有用的参考文档。在实践中，这些规范对计算机来说比对人类要容易得多；你最好查看示例。

Padl Software 提供了一组免费的 Perl 脚本，可以将平面文件或 NIS 映射迁移到 LDAP。你可以在 `padl.com/OSS/MigrationTools.html` 获取，这些脚本运行非常简单。它们可以作为过滤器生成 LDIF，也可以在活动服务器上运行以直接上传数据。例如，`migrate_group` 脚本将 `/etc/group` 中的此行转换为以下 LDAP：

```
dn: cn=csstaff,ou=Group,dc=domainname,dc=com

cn=csstaff

objectClass: posixGroup

objectClass: top
```

# 第 19 章 共享系统文件

```
userPassword: {crypt}x

gidNumber: 2033

memberuid: evi

memberuid: matthew

memberuid: trent
```

（注意对象类和区分名规范，这些在第 729 页的密码示例中被省略了。）

一旦导入了数据库，你可以通过运行 `slapcat` 工具来验证传输是否正确，该工具会显示整个数据库。

## LDAP 查询

要管理 LDAP，你需要能够查看并操作数据库的内容。之前提到的 `phpLDAPAdmin` 工具是实现此目的的较好的工具之一——它为你提供了一个直观的点点界面。如果 `phpLDAPAdmin` 不是选项，`ldapsearch`（随 LDAP 和 389 Directory Server 一起分发）是一个类似的命令行工具，它以 LDIF 格式产生输出。`ldapsearch` 特别适用于从脚本调用以及在 Active Directory 充当 LDAP 服务器的环境中进行调试。

下面的示例查询使用 `ldapsearch` 查找 `cn` 以 "ned" 开头的每个用户的目录信息。（在这种情况下，只有一个结果）。讨论了各种标志的含义。

```bash
$ldapsearch -h atlantic.com -p 389
-x -D "cn=trent,cn=users,dc=boulder,dc=atrust,dc=com" -W
-b "CN=users,DC=boulder,DC=atrust,DC=com" "cn=ned"
```

```ld
# Enter LDAP Password: password

# LDAPv3

# base <CN=users,DC=boulder,DC=atrust,DC=com> with scope
# filter: cn=ned
# requesting: All
# ned, Users, boulder.atrust.com

dn: cn=ned,CN=Users,DC=boulder,DC=atrust,DC=com
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: user
cn: ned
sn: McCain
telephoneNumber: 303 245 4505
givenName: Ned
distinguishedName: Ned=cn,CN=Users,DC=atrust,DC=com
displayName: Ned. McCain
memberOf: CN=Users,CN=Builtin,DC=boulder,DC=atrust,DC=com
```

## LDAP 安全

memberOf: CN=Enterprise Admins,CN=Users,DC=boulder,DC=astrust,DC=com
name: ned
sAMAccountName: ned
userPrincipalName: ned@boulder.astrust.com
lastLoginTimestamp: 12086952489943974
mail: ned@astrust.com

`ldapsearch -h -p` flags 分别指定你想要查询的 LDAP 服务器的主机和端口。

你通常需要向 LDAP 服务器进行验证。在这种情况下，`-x` 标志请求简单认证（相对于 SASL）。`-b` 标志指定搜索的基 DN。`-W` 标志提示输入密码。LDAP 服务器的安全取决于几个因素。第一个是传输层的安全。如果在开放网络上使用 LDAP，数据可能会被拦截。因此，你应该使用 TLS/SSL 加密流量。第二个因素是 LDAP 服务器本身的安全。LDAP 支持访问控制指令 (ACI)，用于定义谁可以访问或修改什么数据。第三个因素是存储在 LDAP 目录中的数据。如果你存储密码，应该使用强哈希算法如 `bcrypt`。

## 19.4 NIS：网络信息服务

NIS 由 Sun 在 80 年代发布，是第一个网络目录。它最初被称为 Sun Yellow Pages，但后来由于法律原因必须更名。NIS 命令以 `yp` 开头。NIS 被 UNIX 发行版广泛采用。

然而，现在 NIS 老了。在新部署中不应使用 NIS。我们这样做主要是考虑到与 Windows 集成的需求，也是因为 NIS 的各种安全性和扩展性缺陷。尽管如此，考虑到许多站点在使用 NIS，我们仍然对它进行了简要介绍。

## NIS 模型

NIS 的共享单元是记录，而不是文件。一个记录通常对应于文件的一行。主服务器维护系统文件的权威副本，这些文件保留在原始位置和格式，并使用文本编辑器编辑。服务器进程映射网络可用内容。服务器及其客户端构成一个 NIS 域。

## 理解 NIS 如何工作

NIS 的数据存储在一个目录中，通常为 `/var/yp`。此后，我们称之为“NIS 目录”。每个 NIS 映射以哈希数据库格式存储在

# 理解 NIS 的工作原理

NIS 目录下的有一个子目录，以 NIS 域命名。映射文件的确切名称和数量取决于所使用的哈希库。对于每一个可以用于搜索文件的文件的键，都对应一个映射（文件）。例如，在 `ssuns` 域中，对应 `/etc/passwd` 映射的 DB 文件可能是：

```
/var/yp/ssuns/passwd.byname

/var/yp/ssuns/passwd.byuid
```
