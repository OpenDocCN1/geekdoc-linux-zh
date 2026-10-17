
| `delete user script` | 删除用户脚本 |
| `dfree command` | dfree 命令 |
| `dns proxy` | DNS 代理 |
| `domain admin group` | 域管理员组 |
| `domain admin users` | 域管理员用户 |
| `domain controller` | 域控制器 |
| `domain groups` | 域组 |
| `domain guest group` | 访来组 |
| `domain guest users` | 访来用户 |
| `domain logons` | 域登录 |
| `domain master` | 域主 |
| `encrypt passwords` | 加密密码 |
| `getwd cache` | getwd 缓存 |
| `homedir map` | 家目录映射 |
| `hosts equiv` | hosts 等效性 |
| `interfaces` | 接口 |
| `keepalived` | 保持存 |
| `kernel oplocks` | 内核乐观锁 |
| `dap filter` | dAP 过滤器 |
| `ldap port` | LDAP 端口 |
| `ldap root` | LDAP 根节点 |
| `Ldap root passwd` | LDAP 根密码 |
| `Ldap server` | LDAP 服务器 |
| `Ldap suffix` | LDAP 后缀 |
| `lim announce` | lim 发布 |
| `im interval` | im 间隔 |
| `load printers` | 加载打印机 |
| `local master` | 本地主 |
| `lock dir` | 锁目录 |
| `lock directory` | 锁定 |
| `log file` | 日志文件 |
| `log level` | 日志级别 |
| `logon drive` | 登录驱动器 |
| `logon home` | 登录家目录 |
| `logon path` | 登录路径 |
| `logon script` | 登录脚本 |
| `lpq cache time` | lpq 缓存时间 |
| `machine password timeout` | 机器密码超时 |
| `mangled stack` | 处理栈 |
| `map to guest` | 映射到访客 |
| `max disk size` | 最大磁盘大小 |
| `max log size` | 最大日志大小 |
| `max mux` | 最大复用 |
| `max open files` | 最大打开文件数 |
| `max packet` | 最大数据包 |
| `max ttl` | 最大生存时间 |
| `max wins ttl` | 最大 wins 生存时间 |
| `max xmit` | 最大传输 |
| `message command` | 消息命令 |
| `min passwd length` | 最小密码长度 |
| `min wins ttl` | 最小 wins 生存时间 |
| `name resolve order` | 名称解析顺序 |
| `netbios aliases` | NetBIOS 别名 |
| `netbios name` | NetBIOS 名称 |
| `nis homedir` | NIS 家目录 |
| `nt acl support` | NT ACL 支持 |
| `nt pipe support` | NT 管道支持 |
| `nt smb support` | NT SMB 支持 |
| `null passwords` | 空密码 |
| `ole locking compatibility` | OLE 锁定兼容性 |
| `oplock break wait time` | 乐观锁中断等待时间 |
| `os level` | 级别 |
| `packet size` | 数据包大小 |
| `panic action` | 崩溃动作 |
| `passwd chat` | 密码聊天 |
| `passwd chat debug` | 密码聊天调试 |
| `passwd program` | 密码程序 |
| `password level` | 密码级别 |
| `password server` | 密码服务器 |
| `preferred master` | 首选主 |
| `preload` | 预加载 |
| `printcap` | printcap 文件 |
| `printcap name` | printcap 名称 |
| `printer driver file` | 打印机驱动文件 |
| `protocol` | 协议 |
| `read bmpx` | 读取 bmpx |
| `read prediction` | 读取预测 |
| `read raw` | 读取原始数据 |
| `read size` | 读取大小 |
| `remote announce` | 远程发布 |
| `remote browse sync` | 远程浏览同步 |
| `restrict anonymous` | 限制匿名 |
| `root` | 根 |
| `root dir` | 根目录 |
| `root directory` | 根目录 |
| `security` | 安全 |
| `server string` | 服务器字符串 |
| `shared mem size` | 共享内存 |
| `smb passwd file` | smb 密码文件 |
| `smbrun` |  |
| `socket address` | 套接地址 |
| `socket options` | 套接选项 |
| `ssl` | SSL |
| `ssl CA certDir` | SSL CA 证书目录 |
| `ssl CA certFile` | SSL CA 证书文件 |
| `ssl ciphers` | SSL 加密算法 |
| `ssl client cert` | SSL 客户端证书 |
| `ssl client key` | SSL 客户端密钥 |
| `ssl compatibility` | SSL 兼容性 |
| `ssl hosts` | SSL 主机 |
| `ssl hosts resign` | SSL 主机签名 |
| `ssl require clientcert` | SSL 要求客户端证书 |
| `ssl require servercert` | SSL 要求服务器证书 |
| `ssl server cert` | SSL 服务器证书 |
| `ssl server key` | SSL 服务器密钥 |
| `ssl version` | SSL 版本 |
| `stat cache` | stat 缓存 |
| `stat cache size` | stat 缓存大小 |
| `strip dot` | 去除点 |
| `syslog` | syslog |
| `syslog only` | 仅限 syslog |
| `time offset` | 时间偏移量 |
| `time server` | 时间服务器 |
| `timestamp logs` | 时间戳日志 |
| `unix password sync` | Unix 密码同步 |
| `unix realname` | Unix 真实名称 |
| `update encrypted` | 更新加密 |
| `use rohosts` | 使用 rohosts |
| `username level` | 用户名级别 |
| `username map` | 用户名映射 |
| `valid chars` | 有效字符 |
| `wins proxy` | wins 代理 |
| `wins server` | wins 服务器 |
| `wins support` | wins 支持 |
| `workgroup` | 工作组 |
| `write raw` | 原始数据 |

## 共享部分

共享定义了 Samba 将向工作组和域客户端提供的显式资源。系统提供了两个预定义的部分，分别为 `[homes]` 和 `[printers]`，用于允许用户访问其 UNIX `$HOME` 目录以及 UNIX 打印文件中列出的任何打印机。可以定义其他共享以授予或限制对单个目录和打印机的访问，或指定存储配置文件的位置。完整的共享参数列表见表 6.5。请参考 `smb.conf`(5) 消息获取每个共享的描述。

如果在 `smb.conf` 中定义了 `[homes]` 部分，当未找到匹配的请求共享名称时，它将成为默认目标。此时假设该名称为服务器上的有效用户账户。将扫描密码文件以寻找新的匹配项。如果提供了用户名，则会将提供的密码与服务器密码文件中的用户条目进行验证。一旦通过验证，将通过克隆 `[homes]` 部分中指定的默认参数创建一个新共享，并将其与用户的 `$HOME` 目录关联。有关共享目录的更多信息，请参阅第 11 章。
