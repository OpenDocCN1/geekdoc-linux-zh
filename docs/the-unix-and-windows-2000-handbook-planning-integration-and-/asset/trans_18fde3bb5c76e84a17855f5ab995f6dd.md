

| Variable | Value | Description |
|---|---|---|
| `security` | `Share` \| `User` \| `Server` \| `domain` | 指定 SAMBA 服务器采用的安全级别。 这些值对应于 Windows 中的对应项。 Share 级别安全为每个服务/资源提供一个密码。 User 级别安全要求连接的用户通过 `passwd` 文件进行身份验证。 Server 级和 domain 级安全都使用 Windows NT 服务器来验证用户连接。 Domain 级安全允许来自受信任域的用户进行身份验证，而 server 级安全则不允许。 |
| `password server` | `NetBIOS name` | 指定用作身份验证服务器的服务器名称（通常为 PDC）。 |
| `username map` | `Pathname` | 指定将 UNIX 用户名映射到 NT 用户名的文件。 这对于 root 和 administrator 等用户很有用，因为这些用户在各自的系统上没有同名用户。 |
| `domain group map` | `Pathname` | 这与 `username map` 变量相同，只是它提供组映射。 |
| `encrypt passwords` | `yes/no` | 指定密码是否将被加密或以明文形式传递。 使用 server 级或 domain 级安全时，应始终指定 `yes`。 |
| `socket options` |  | 对此参数使用默认值，它们有效！ |
| `local master` | `yes/no` | 指定 SAMBA 服务器是否将在 NetBIOS 网络上作为本地主浏览器。 除非本地子网中没有 NT 服务器，否则应始终将此参数指定为 `no`。 |
| `domain master` | `yes/no` | 指定 SAMBA 服务器是否将在 NetBIOS 网络上作为域主浏览器。 除非域/工作组中没有 NT 服务器，否则应始终将此参数指定为 `no`。 |
| `preferred master` | `yes/no` | 指定 SAMBA 服务器是否将在 NetBIOS 网络上作为首选主浏览器。 除非任何地方都没有 NT 服务器，否则应始终将此参数指定为 `no`。 |

| Variable | Value | Description |
|---|---|---|
| os level | Number | 指定 SAMBA 服务器在赢得浏览主选举中的优先级。 你设置此数字越高（最大 33），SAMBA 服务器赢得选举的可能性就越大。 我们建议将此参数设置为 0，除非没有可用的 NT 服务器。 |
| name resolve order | String | 指定 SAMBA 服务器将解析 NetBIOS 名称的顺序。 最常见的解析顺序是 wins lmhosts host。 |
| wins support | yes/no | 指定 SAMBA 服务器是否还提供 NetBIOS 名称解析功能。 除非没有可用的 NT 服务器，否则不要在 Windows NT 网络上启用此功能。 |
| wins server | IP address | 指定用于查询 WINS 请求的服务器。 |
| wins proxy | yes/no | 指定 SAMBA 服务器是否将作为非 WINS 启用客户端的 WINS 代理，例如未运行 SAMBA 的 UNIX 工作站。 |
| lm announce | yes/no | 指定 SAMBA 服务器是否将向网络发出 LanManager  announcements。 除非你的网络上有旧的 LanManager 客户端，否则将此参数设置为 no。 |
| dns proxy | yes/no | 指定 SAMBA 服务器是否将作为 DNS 代理。 |

你也可以在 [<sharename>] 部分下显式创建任何共享并按需配置。 你可以使用 SAMBA 文档中指定的任何允许变量。 以下是前面讨论的 smb.conf 文件的更完整版本，包括共享和打印机定义：

## Table 8.11 SAMBA [homes] Section Variables

| Variable | Value | Description |
|---|---|---|
| comment | Text | 用于描述所提供的服务。 在 [homes] 部分使用时，应指定一个通用短语。 |
| browseable | yes/no | 指定此服务是否可在 NetBIOS 网络上浏览。 |
| guest ok | yes/no | 指定是否允许访客访问此共享。 在 homes 部分使用时，我们建议将其设置为 no。 |
| writeable | yes/no | 指定是否可以写入此共享。 除非你只希望用户查看其主目录而不使用它，否则应将此参数指定为 yes。 |

## Table 8.12 SAMBA [printers] Section Variables

| Variable | Value | Description |
|---|---|---|
| comment | Text | 用于描述所提供的服务。 在 [printers] 部分使用时，应指定一个通用短语。 |
| browseable | yes/no | 指定此服务是否可在 NetBIOS 网络上浏览。 |
| path | pathname | 指定将文档 spool 到的路径。 这通常位于 /var/spool 目录中的某个位置。 |
| printable | yes/no | 指定是否可以向打印机打印。 为什么要创建共享然后说，“不，你不能打印，哈，哈。” 应始终将此参数设置为 yes。 |

```
# -------------------- Global Settings --------------------
[global]
netbios name = LILDIPPER
workgroup = COSMOS
server string = Samba %v Server

browseable = yes

hosts allow = 192.168.
hosts deny = 192.168.224.

load printers = yes
printcap name = /etc/printcap
printing = bsd
```

