
## 第 31 章：轻量级目录访问协议 (LDAP)

555

必须做出安全选择，包括凭据级别和验证方法：

以下是支持的凭据级别：

- 1 匿名
- 2 代理
- 3 代理匿名

选择凭据级别 [help]: [1] 1

以下是支持的验证方法：

1 无
2 simple
3 sasl/DIGEST-MD5
4 tls:simple
5 tls:sasl/DIGEST-MD5

选择验证方法 (help): [1] 2

当前验证方法 authenticationMethod: simple

您还想添加另一个验证方法吗？N

在检查服务器配置后，您可能需要配置客户端。这包括设置代理和目录访问格式的超时时间，以及时间和大小限制：

- 您是否希望客户端跟随重定向 (y/n/h)? [n] n
- 您是否想修改服务器的大小限制 sizelimit 值 (y/n/h)? [n] n
- 您是否想以 'crypt' 格式存储密码 (y/n/h)? [y] n
- 您是否想设置服务验证方法 (y/n/h)? [n] n
- 搜索时间限制（秒）（help): [60]
- 配置文件生存时间 TTL（秒）（help): [3600]
- 绑定时间限制（秒）（help): [10] 2
- 您是否想设置服务搜索描述符 (y/n/h)? [n] n

最后，在 dconfconf 执行任何操作之前，将向您展示一个配置摘要：

### 配置摘要

| # | 字段 |
| :--- | :--- |
| 1 | 服务的域名 : sales.cassowary.net |
| 2 | 要设置的 BaseDN : dc-sales,dc-cassowary,dc-net |
| 3 | 要创建的配置文件名称 : default |
| 4 | 默认服务器列表 : 192.64.18.1 |
| 5 | 首选服务器列表 = |
| 6 | 默认搜索范围 : one (单个) |
| 7 | 凭据级别 : anonymous (匿名) |
| 8 | 验证方法 : simple |
| 9 | 启用跟随定向 : FALSE |
| 10 | 时间限制 : - |
| 11 | IDS 限制 : - |
| 12 | 启用 crypt密码存储 : 1 |
| 13 | 服务验证方法 pam_ldap |
| 14 | 服务验证方法 keyserv |
| 15 | 服务验证方法 passwd-cmd: |
| 16 | 搜索时间限制 : 30 |
| 17 | 配置文件生存时间 : 43200 |
| 18 | 绑定限制 : 2 |
| 19 | 服务搜索描述符 None (无) |

## 练习 31-3 idsconffig 配置

检查您的 `idsconffig` 配置。是否有任何选项需要与上一个示例不同的设置？

## 创建 LDAP 条目

`ldapadd` 命令用于在 LDAP 容器中创建条目，适用于存储在 `/etc` 目录下文件中所有标准系统数据库。通过此方法可以将以下 Solaris 数据库（带有相应的 ou）传输到 LDAP：

- `aliases` (ou=Aliases)
- `bootparams` (ou=Ethers)
- `ethers` (需要先安装 bootparams 数据库) (ou=Ethers)
- `group` (ou=Group)
- `hosts` (ou=Hosts)
- `netgroup` (ou=Netgroup)
- `netmasks` (需要先安装 networks 数据库) (ou=Networks)
- `networks` (ou=Networks)
- `passwd` (ou=People)
- `shadow` (需要先安装 passwd 数据库) (ou=People)
- `protocols` (ou=Protocols)
- `publickey` (ou=Hosts)
- `rpc` (ou=Rpc)
- `services` (ou=Services)

可以通过以下方式查询任何表：

- `auto_home`
- `auto_master`
- `bootparams`
- `client_info`
- `cred`
- `ethers`
- `group`
- `hosts`
- `mail_aliases`
- `netgroup`
- `netmasks`
- `networks`
- `passwd`
- `protocols`
- `rpc`
- `sendmailvars`
- `services`
- `timezone`

例如，要获取存储在 `hosts` 表中的主机（hosts）列表，我们应该使用以下命令：

```bash
# nisldmaptest -t hosts.org_dir
```

如果在表中发现了一个不再有效的主机，可以使用以下命令将其删除：

```bash
# nisldmapmaptest -d -t hosts.org_dir name=oldhost
```

## 使用 iDS

在本示例中，我们将演示如何通过控制台管理 iDS。一旦安装了 iDS 服务器，你就应该能够使用以下命令启动控制台：

```bash
# directoryserver startconsole
```

登录窗口将显示适当的管理员端口号和主机名，如图 31-2 所示。在这种情况下，14462 是安装期间指定的 LDAP 服务器的管理员端口。

![](img/0ce985fd07a5af27ed793d64cf4b977d_587_0.png)

**图 31-2** 管理服务器的身份验证

必须输入管理员 ID 和相应的密码以调出主管理窗口。

随后显示主 IDS 控制台，如图 31-3 所示。有两个标签用于区分控制台的两个主要功能：服务器与应用程序（Servers and Applications），以及用户与组（Users and Groups）。“服务器与应用程序”标签有两个窗格：已为网络配置。显示本地服务器组，以及本地管理服务器和实际目录服务器的条目。通过选择与 localhost 相关的图标，将显示主机名、描述、物理位置、操作系统和系统。

![](img/0ce985fd07a5af27ed793d64cf4b977d_587_1.png)

**图 31-3** 主控制台窗口

## 第 31 章：轻量级目录访问协议 (LDAP)

> 注意：选择服务器组图标会显示组名称、描述和安装路径。
