

- `-d|--debug=debuglevel` `debuglevel` 是 0 到 10 之间的整数。如果未指定此参数，默认值为零。

该值越高，日志文件中记录的服务器活动详细信息就越多。在级别 0 时，仅记录关键错误和严重警告。级别 1 是日常运行的合理级别——它会产生少量关于所执行操作的信息。

高于 1 的级别将产生大量日志数据，仅应在调查问题时使用。高于 3 的级别专为开发人员设计，会产生**巨量**日志数据，其中大部分内容极其晦涩难懂。

请注意，在此处指定该参数将覆盖 smb.conf 文件中的参数。

- `-l|--logfile=logdirectory` 日志/调试文件的基础目录名称。将追加扩展名“.programname”（例如 log.smbclient, log.smbd 等...）。客户端从不删除日志文件。

- `-h|--help` 打印命令行选项摘要。

- `-b` 打印有关 Samba 构建方式的信息。

- `-p <port number(s)>` port number(s) 是 smbd 应监听的 TCP 端口的空格或逗号分隔列表。默认值取自 smb.conf 中的 ports 参数。

默认端口为 139（用于基于 NetBIOS over TCP 的 SMB）和端口 445（用于基于 TCP 的纯 SMB）。

## 文件

- `/etc/inetd.conf` 如果服务器由 inetd 元守护进程运行，此文件必须包含适合元守护进程的启动信息。

- `/etc/rc` 或您的系统使用的任何初始化脚本。

如果在启动时作为守护进程运行服务器，此文件将需要包含服务器的适当启动序列。

- `/etc/services` 如果通过元守护进程 inetd 运行服务器，此文件必须包含服务名称（例如，netbios-ssn）到服务端口（例如，139）和协议类型（例如，tcp）的映射。

- `/usr/local/samba/lib/smb.conf` 这是 smb.conf(5) 服务器配置文件的默认位置。系统安装此文件的其他常见位置包括 `/usr/samba/lib/smb.conf` 和 `/etc/samba/smb.conf`。

此文件描述了服务器向客户端提供的所有服务。更多信息请参阅 smb.conf(5)。

### 限制

在某些系统上，**smbd** 在 setuid() 调用后无法将 uid 变回 root。这类系统被称为“陷阱门 uid 系统”。如果您拥有这样的系统，您将无法让两个不同用户同时从客户端（如 PC）连接。尝试连接第二个用户将导致访问被拒绝或类似错误。

### 环境变量

- **PRINTER** 如果未为可打印服务指定打印机名称，大多数系统将使用此变量的值（如果未定义此变量，则使用 **lp**）作为要使用的打印机名称。但这并非服务器特有的功能。

### PAM 交互

Samba 使用 PAM 进行身份验证（当提供明文密码时）、账户检查（此账户是否被禁用？）以及会话管理。Samba 对 PAM 的支持程度受限于 SMB 协议的限制以及 *obey pam restrictions* smb.conf(5) 参数。当此参数被设置时，将应用以下限制：

- **账户验证：** 所有对 samba 服务器的访问都会针对 PAM 进行检查，以确认账户是否有效、未被禁用且允许在此时登录。这也适用于加密登录。
- **会话管理：** 当不使用共享级别安全性时，用户必须在授予访问权限之前通过 PAM 的会话检查。然而，在共享级别安全性中这会旁路处理。另外请注意，一些较旧的 pam 配置文件可能需要添加一行以支持会话。

### 诊断

服务器发出的大多数诊断信息都会记录在指定的日志文件中。日志文件名在编译时指定，但可在命令行上覆盖。

…… [思维中省略了文本，但在输出中存在] …… 每一个诊断信息。在这个阶段，你最好的选择仍然是 grep 源代码并检查导致你所看到的诊断信息的条件。

## TDB 文件

Samba 将数据存储在许多 TDB（Trivial Database）文件中，通常位于 `/var/lib/samba`。

- `account_policy.tdb*` NT 账户策略设置，如密码过期时间等...
- `broleck.tdb` 字节范围锁
- `browse.dat` 浏览列表
- `connections.tdb` 共享连接（用于强制最大连接数等...）
- `gencache.tdb` 通用缓存数据库
- `group_mapping.tdb*` 组映射信息
- `locking.tdb` 共享模式与 oplocks
- `login_cache.tdb*` 错误的密码尝试
- `messages.tdb` Samba 消息系统
- `netsamlogon.cache.tdb*` 来自 net_samlogon() 请求的用户 net_info.3 结构缓存（作为域成员时）
- `ntdrivers.tdb*` 已安装的打印机驱动
- `ntforms.tdb*` 已安装的打印机表单
- `ntprinters.tdb*` 已安装的打印机信息
- `printing/` 包含每个打印队列的 lpq 输出缓存的 tdb 目录
- `registry.tdb` Windows 注册表骨架（通过 regedit.exe 连接）
- `sessionid.tdb` 会话信息（例如支持 `utmp = yes`）
- `share_info.tdb*` 共享 ACL
- `winbindd_cache.tdb` winbindd 的用户列表等缓存
- `winbindd_idmap.tdb*` winbindd 的本地 idmap 数据库
- `wins.dat*` 当 `wins support = yes` 时的 wins 数据库

(*) 信息在重启后持久存在（但不一定需要备份）。

## 信号

向 **smbd** 发送 SIGHUP 信号将使其在短时间内重新加载其 **smb.conf** 配置文件。

建议**不要**使用 **SIGKILL (-9)** 来终止用户的 **smbd** 进程，除非作为最后手段，因为这可能导致共享内存区域处于不一致状态。安全终止 **smbd** 的方法是发送 SIGTERM (-15) 信号并等待其自行终止。

**smbd** 的调试日志级别可以使用 *smbcontrol(1)* 程序（SIGUSR1[2] 信号自 Samba 2.2 起*不再*使用）调高或调低。这是为了在保持正常低日志级别的同时诊断瞬态问题。

请注意，由于信号处理程序会发送调试写入，它们在 **smbd** 中是不可重入的。因此，您应在 **smbd** 处于等待传入 SMB 的状态时再发出它们。可以通过在 select 调用之前解除阻塞信号，并在之后重新阻塞信号来使信号处理程序安全，但这会影响性能。

## 另请参阅

hosts_access(5), inetd(8), nmbd(8), smb.conf(5), smbclient(1), testparm(1), testprns(1). 以及互联网 RFC *rfc1001.txt*, *rfc1002.txt*. 此外，CIFS（前身为 SMB）规范可通过网页 http://samba.org/cifs/⁷ 获取。

![](img/86d74c6cc862465e3a42e6dc3c90935a_862_0.png)

## 47.12 smbpasswd

### 概要

smbpasswd

### 描述

此工具是 samba(7) 套件的一部分。

smbpasswd 是 Samba 加密密码文件。它包含用户名、Unix 用户 ID 以及用户的 SMB 哈希密码，还包括账户标志信息和密码最后修改的时间。此文件格式随着 Samba 的演进而变化，过去曾有几种不同的格式。

### 文件格式

Samba 2.2 使用的 smbpasswd 文件格式与熟悉的 Unix *passwd*(5) 文件非常相似。它是一个 ASCII 文件，每个用户占一行。每行内的每个字段由冒号分隔。以 '#' 开头的任何条目都会被忽略。smbpasswd 文件包含每个用户的以下信息：

- **name** 这是用户名。它必须是标准 UNIX 密码文件中已经存在的名称。
- **uid** 这是 UNIX uid。它必须与标准 UNIX passwd 文件中同一用户条目的 uid 字段匹配。如果不匹配，Samba 将拒绝承认此 smbpasswd 文件条目对该用户有效。
- **Lanman Password Hash** 这是用户密码的 LANMAN 哈希值，编码为 32 个十六进制数字。LANMAN 哈希是通过使用用户密码作为 DES 密钥来 DES 加密一个众所周知的字符串生成的。这是 Windows 95/98 机器使用的相同密码。请注意，此密码哈希值被认为非常薄弱，因为它易受字典攻击，且如果两个用户选择相同的密码，此条目将完全相同（即密码不像 UNIX 密码那样进行“加盐”）。如果用户有 null 密码，此字段将以十六进制字符串的开头包含字符 'NO PASSWORD'。如果十六进制字符串等于 32 个 'X' 字符，则用户的账户被标记为*已禁用*，用户将无法登录到 Samba 服务器。

> **警告 ！！** 请注意，由于 SMB/CIFS 身份验证协议采用质询-响应机制，任何知道此密码哈希值的人都能够模拟该用户进行网络身份验证。因此，这些哈希值被称为*明文等价物*，且必须*不要*向根用户以外的任何人开放。为了保护这些密码，smbpasswd 文件被放置在一个具有读取权限的目录中，且
