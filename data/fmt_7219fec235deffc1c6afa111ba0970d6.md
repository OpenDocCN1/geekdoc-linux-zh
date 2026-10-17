
下面是一个定义配置简单示例。定义标签被括在括号中，后面跟着两个参数条目。`path` 参数指定允许访问的文件夹。`writeable` 参数指定用户是否对该文件夹具有写权限。

```
[folder]
path = /home/chris
writeable = true
```

打印服务具有相同的格式，但需要某些其他参数。`path` 参数指定打印程序文件夹（spooler folder）的位置。`read only` 和 `printable` 参数设置为 `true`，表示该服务是只读且可打印的。`guest` 选项表示任何人都可以访问。

```
[myprinter]
path = /var/spool/samba
read only = yes
printable = yes
guest ok = yes
```

参数条目通常是同义词，即不同的条目可能具有相同的含义。例如，`read only = no`、`writeable = yes` 和 `write ok = yes` 都意味着相同的内容，即为用户提供写权限。

提示：`writeable` 选项是 `read only` 选项的反向别名。`writeable = yes` 条目等于 `read only = no` 条目。

## 基本配置

在 `smb.conf` 文件中为 Samba 配置需要设置的所有只有 `workgroup` 和 `netbios` 条目，以及你想要访问的任何共享文件夹。`workgroup` 是你的 Windows 工作组名称，`netbios` 是运行 Linux 和 Samba 服务器的的主机名。这些条目位于 `smb.conf` 文件顶部的 `Globals` 定义下的 `Related Options` 标题下。默认值已经列出。删除前面的分号字符并将值更改为适用于你网络的值。在这里，`workgroup` 和 `netbios` 名称被设置为 `workgroup` 和 `rich4`。

```
workgroup = workgroup
netbios = rich4
```

在 `Shares` 部分中，你可以配置 Samba 共享文件夹。详情请参阅“共享定义”（Share Definitions）。

一旦你进行了更改，请在终端窗口中使用 `service` 命令对 `smb` 和 `nmb` 脚本重启 Samba 服务器（使用 `su` 命令以 root 用户身份登录），或使用 `system-config-services`（System | Administration | Services）。

```
su
service smb restart
service nmb restart
```

## 变量替换

对于分配给参数的字符串值，你可以结合替换运算符。这为指定可能取决于上下文的值提供了更大的灵活性，例如 `\%username`。例如，假设一个服务需要为每个登录的用户使用单独的文件夹。此类文件夹路径可以使用 `%` 变量指定，该变量会替换为当前用户名。字符串 `path = /tmp/%u` 对于 `justin` 用户将变为 `path = /tmp/justin`，对于 `dylan` 用户将变为 `path = /tmp/dylan`。表 13-1 列出了几个较常见的替换变量。

| 变量 | 描述 |
| --- | --- |
| %S | 当前服务的名称 |
| %P | 当前服务的根文件夹 |
| %u | 当前服务的用户名 |
| %H | 用户的主目录 |
| %h | 运行 Samba 的互联网主机 |
| %m | 客户端机器的 NetBIOS 名称 |
| %L | 服务器的本地名称 |
| %M | 客户端机器的 NetBIOS 名称 |
| %I | 客户端的 IP 地址 |

## 全局定义

全局定义（Global definition）决定了工作组名称以及文件夹设置。全局定义从 `[global]` 开始。这里讨论了几个更重要的条目。全局定义从 `[global]` 开始。

## 网络选项

网络选项组织成不同的部分。网络选项从 `[global]` 开始。`workgroup` 是 Samba 服务器的名称。在 Windows 客户端，这通常是 `WORKGROUP`。在本示例中，工作组名称为 `mygroup`。

## 独立服务器选项

```
# ---- Standalone Server Options -----
#
 security = Samba 运行的模式。可以设置为 user，
#（已弃用），或 server（已弃用）。
#
# passdb backend = 用于存储用户信息的后端。新的
# 安装程序应使用 tdbsam 或 ldaps。tdbsam 不需要
# 额外的配置。为了向后兼容，"smpassword" 
# 工具可用。

security = user
passdb backend = tdbsam
```

Samba 资源通常通过共享级（share）或用户级（user）安全设置进行访问。在用户级上，每个用户都可以访问资源，而无需登录服务器。在用户级上，每个用户必须使用密码登录。Windows 客户端在登录过程中使用加密密码。如前所述，密码默认是加密的，并由密码数据库管理。在接下来的条目中，`security` 设置为 `user`，且密码数据库文件使用 `tdbsam`。

```
security = user
passdb backend = tdbsam
```

如果你想使用共享级安全设置，请将 `share` 指定为安全选项。然而该选项已弃用。用户级安全通过以下标准进行配置：

## 域成员选项

如果你的网络通过域服务器集中处理认证，那么你的 Samba 服务器需要成为域成员。域成员身份通常由活动目录服务器（Active Directory Server）或特定的 PDC 服务器处理。需要配置 `smb.conf` 文件以支持域成员身份。安全选项设置为 `domain` 或 `ads`。如果你选择 `domain`，则 `workgroup` 选项设置为域名称。

```
security = domain
workgroup = mydomain
```

在 `smb.conf` 文件的 Domain Members Options（域成员选项）部分，你可以设置 `realm` 密码服务器选项。如果 `security` 设置为 `ads`，你可以设置 `realm` 选项（活动目录域）。如果你将 `security` 设置为 `domain`，则使用 `password server` 选项来指定你的网络使用的 Windows PDC 服务器。使用星号（`*`）代替 PDC 名称，Samba 将将自动检测 PDC 服务器。

```
; realm = MY_REALM
; password server = <NT-Server-Name>
```

## 域名解析

名称服务解析通常由 WINS 服务器（Windows NetBIOS 名称服务，`nmbd`）提供，该服务由 `nmb` init 脚本启动。如果你的本地网络有 WINS 服务器，你可以改为指定它。这里显示了注释掉的默认条目。将 `w.x.y.z` 替换为你网络的 WINS 服务器名称。

- `wins server = w.x.y.z`

你的 Samba `nmbd` 服务器对 WINS 的支持被注释掉以避免冲突，使你的 Samba 名称解析服务器变为纯客户端。这里显示了开启 WINS 支持的注释条目。

- `wins support = yes`

```
--- Name Resolution ---------------------
# 此部分详细说明了对 Windows Internet 名称 Service (WINS)的支持。

# 注意：Samba 既可以是 WINS 服务器也可以是 WINS 客户端，但不能两者兼得。
##
# wins server = 告诉 Samba 的 NMBD 组件作为 WINS 客户端。
##
# dns proxy = 当设置为 yes 时，Samba 尝试通过 DNS
# nslookups 解析 NetBIOS。
```

- `wins support = yes`

- `wins server = w.x.y.z`

- `dns proxy = yes`

如果你的网络也有它想要用于名称解析的 DNS 服务器，你可以改为启用它。默认情况下，它是如所示注释掉的。移除注释符号以允许你网络的 DNS 服务器进行 Windows 名称解析。此外，WINS 服务器支持必须关闭。

- `dns proxy = yes`

此外，还可以指示名称解析检查 `lmhosts` 和 `/etc/hosts` 文件。这里显示了注释掉的默认条目。

- `wins resolve order = lmhosts host wins`

## 打印选项
