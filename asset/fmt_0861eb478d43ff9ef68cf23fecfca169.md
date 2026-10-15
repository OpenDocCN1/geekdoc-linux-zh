
### 描述

本工具是 `samba(7)` 套件的一部分。

`wbinfo` 程序查询并返回由 `winbindd(8)` 守护进程创建和使用的信息。

必须配置并运行 `winbindd(8)` 守护进程，`wbinfo` 程序才能返回信息。

### 选项

- `-a username%password` 尝试通过 `winbindd` 验证用户。这会检查两种验证方法并报告其结果。

  > 注意
  >
  > 不要尝试在第三方应用程序中使用此功能进行身份验证。请改用 `ntlm_auth(1)`。

- `-c user` 创建一个本地 winbind 用户。

- `-C group` 创建一个本地 winbindd 组。

- `domain name` 此参数设置执行指定操作的域。如果使用特殊域名 "." 来表示 winbindd 所属的当前域。目前只有 `--sequence`、`-u` 和 `-g` 选项遵循此参数。

- `-g` 此选项将列出 Windows NT 域中可用的所有组，该域是 `samba(7)` 守护进程正在运行的目标域。所有受信任域中的组也会被列出。请注意，此操作不会为 `winbindd(8)` 尚未看到的组分配组 ID。

- `-get-auth-user` 将 `winbindd` 在与域控制器建立会话期间使用的用户名和密码打印出来。用户名和密码可以使用 `-A` 设置。仅对 root 可用。

- `-G gid` 尝试将 UNIX 组 ID 转换为 Windows NT SID。如果指定的 gid 不属于 idmap gid 范围内，则操作将失败。

- `-I ip` `-I` 选项查询 `winbindd(8)` 发送节点状态请求，以获取与 `ip` 参数指定的 IP 地址关联的 NetBIOS 名称。

- `-m` 生成 `winbindd(8)` 在解析名称时联系的那些 Windows NT 服务器信任的域列表。此列表不包括该服务器作为主域控制器的 Windows NT 域。

- `-n name` `-n` 选项查询 `winbindd(8)` 获取与指定名称关联的 SID。可以使用 winbind 分隔符字符在用户名前指定域名。例如，`CWDOM1/Administrator` 指的是 `CWDOM1` 域中的 `Administrator` 用户。如果未指定域，则使用 `smb.conf(5)` 中 `workgroup` 参数指定的域。

- `-N name` `-N` 选项查询 `winbindd(8)` 查询 WINS 服务器，以获取与 `name` 参数指定的 NetBIOS 名称关联的 IP 地址。

- `-o user:group` 将 winbind 本地组添加为指定的 winbindd 本地用户的辅助组。

- `-O user:group` 将 winbind 本地组从指定的 winbindd 本地用户的辅助组中移除。

- `-p` 检查 `winbindd` 是否仍然存活。打印 'succeeded' 或 'failed'。

- `-r username` 尝试获取用户所属的 UNIX 组 ID 列表。这只适用于域控制器上定义的用户。

- `-s sid`
使用 `-s` 将 SID 解析为名称。这是上述 `-n` 选项的反操作。SID 必须以传统的 Microsoft 格式的 ASCII 字符串形式指定。例如，`S-1-5-21-1455342024-3071081365-2475485837-500`。

- `-set-auth-user username%password`
存储 `winbindd` 在与域控制器进行会话设置时使用的用户名和密码。这使得 `winbindd` 能够在一个禁用了“限制匿名”（也称为“仅与 Windows 2000 服务器兼容的权限”）的 Windows 2000 域中运行。

- `-sequence`
显示所有已知域的序列号。

- `-S sid`
将 SID 转换为 UNIX 用户 ID。如果该 SID 不对应于由 `winbindd(8)` 映射的 UNIX 用户，则操作将失败。

- `-t`
验证在将 Samba 服务器添加到 Windows NT 域时创建的工作站信任账户是否正常工作。

- `-u`
此选项将列出在 `winbindd(8)` 守护进程正在运行的 Windows NT 域中可用的所有用户。所有受信任域中的用户也会被列出。请注意，此操作不会为 `winbindd(8)` 尚未见过的任何用户分配用户 ID。

- `-U uid`
尝试将 UNIX 用户 ID 转换为 Windows NT SID。如果指定的 uid 不属于 idmap uid 范围，则操作将失败。

- `-x user`
删除现有的本地 winbind 用户。

- `-X group`
删除现有的本地 winbindd 组。

- `-Y sid`
将 SID 转换为 UNIX 组 ID。如果该 SID 不对应于由 `winbindd` 映射的 UNIX 组，则操作将失败。

- `-V`
打印程序版本号。

- `-h|-help`
打印命令行选项摘要。

## 退出状态

`wbinfo` 程序在操作成功时返回 0，操作失败时返回 1。如果 `winbindd(8)` 守护进程未正常工作，`wbinfo` 将始终返回失败。

## 参见

`winbindd(8)` 和 `ntlm_auth(1)`

## 47.20 winbindd

### 概要

```
winbindd [-F] [-S] [-i] [-Y] [-d <debug_level>] [-s <smb_config_file>]
    [-n]
```

## 描述

此程序是 `samba(7)` 套件的一部分。

`winbindd` 是一个守护进程，它为大多数现代 C 库中的名称服务切换（Name Service Switch）功能、通过 PAM 和 `ntlm_auth` 向任意应用程序提供的一系列服务以及 Samba 本身提供服务。

即使 winbind 未用于 nsswitch，它仍然通过管理到域控制器的连接，为 `smbd`、`ntlm_auth` 和 `pam_winbind.so` PAM 模块提供服务。在此配置中，`idmap uid` 和 `idmap gid` 参数不是必需的。（这被称为“仅 netlogon 代理模式”。）

名称服务切换允许从不同的数据库服务（如 NIS 或 DNS）获取用户和系统信息。具体行为可以通过 `/etc/nsswitch.conf` 文件进行配置。用户和组在解析为 Samba 系统管理员指定的用户和组 ID 范围时被分配。

`winbindd` 提供的服务称为“winbind”，可用于从 Windows NT 服务器解析用户和组信息。该服务还可通过相关的 PAM 模块提供身份验证服务。

`pam_winbind` 模块支持 `auth`、`account` 和 `password` 模块类型。需要注意的是，`account` 模块仅执行 `getpwnam()` 以验证系统能否为用户获取 uid，因为域控制器已经执行了访问控制。如果 `libnss_winbind` 库已正确安装，或配置了替代名称源，这应该总是成功的。

以下 nsswitch 数据库由 `winbindd` 服务实现：

- `hosts` 此功能仅在 IRIX 上可用。传统上存储在 `hosts(5)` 文件中并由 `gethostbyname(3)` 函数使用的用户信息。名称通过 WINS 服务器或广播进行解析。

- `passwd` 传统上存储在 `passwd(5)` 文件中并由 `getpwent(3)` 函数使用的用户信息。

- `group` 传统上存储在 `group(5)` 文件中并由 `getgrent(3)` 函数使用的组信息。

例如，可以在 `/etc/nsswitch.conf` 文件中使用以下简单配置，最初从 `/etc/passwd` 和 `/etc/group` 解析用户和组信息，然后从 Windows NT 服务器解析。

```
passwd:		files winbind
group:		files winbind
# only available on IRIX; Linux users should use libnss_wins.so
hosts:		files dns winbind
```

可以在 `/etc/nsswitch.conf` 文件中使用以下简单配置，最初从 `/etc/hosts` 解析主机名，然后从 WINS 服务器解析。

```
hosts:		files wins
```

## 选项

- `-F` 如果指定了此参数，主 `winbindd` 进程将不会守护化，即不会双重 fork 并与终端分离。子进程仍会正常创建以服务每个连接请求，但主进程不会退出。此操作模式适用于在 Daniel J. Bernstein 的 `daemontools` 包中的 `supervise` 和 `svscan` 等进程监控器下运行 `winbindd`，或适用于 AIX 进程监控器。
