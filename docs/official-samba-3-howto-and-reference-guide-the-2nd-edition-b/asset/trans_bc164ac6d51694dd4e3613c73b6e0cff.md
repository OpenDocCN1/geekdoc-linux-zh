
-s sid
使用 -s 将 SID 解析为名称。这是上述 -n 选项的反操作。SID 必须以传统的 Microsoft 格式的 ASCII 字符串形式指定。例如，S-1-5-21-1455342024-3071081365-2475485837-500。

-set-auth-user username%password
存储 winbindd 在与域控制器进行会话设置时使用的用户名和密码。这使得 winbindd 能够在一个禁用了“限制匿名”（也称为“仅与 Windows 2000 服务器兼容的权限”）的 Windows 2000 域中运行。

-sequence
显示所有已知域的序列号。

-S sid
将 SID 转换为 UNIX 用户 ID。如果该 SID 不对应于由 winbindd(8) 映射的 UNIX 用户，则操作将失败。

-t
验证在将 Samba 服务器添加到 Windows NT 域时创建的工作站信任账户是否正常工作。

-u
此选项将列出在 winbindd(8) 守护进程正在运行的 Windows NT 域中可用的所有用户。所有受信任域中的用户也会被列出。请注意，此操作不会为 winbindd(8) 尚未见过的任何用户分配用户 ID。

-U uid
尝试将 UNIX 用户 ID 转换为 Windows NT SID。如果指定的 uid 不属于 idmap uid 范围，则操作将失败。

-x user
删除现有的本地 winbind 用户。

-X group
删除现有的本地 winbindd 组。

-Y sid
将 SID 转换为 UNIX 组 ID。如果该 SID 不对应于由 winbindd(8) 映射的 UNIX 组，则操作将失败。

-V
打印程序版本号。

-h|-help
打印命令行选项摘要。

## 退出状态

**wbinfo** 程序在操作成功时返回 0，操作失败时返回 1。如果 winbindd(8) 守护进程未正常工作，**wbinfo** 将始终返回失败。

## 参见

winbindd(8) 和 ntlm_auth(1)

## 47.20 winbindd

### 概要

```
winbindd [-F] [-S] [-i] [-Y] [-d <debug_level>] [-s <smb_config_file>]
    [-n]
```

## 描述

此程序是 *samba*(7) 套件的一部分。

**winbindd** 是一个守护进程，它为大多数现代 C 库中的名称服务切换（Name Service Switch）功能、通过 PAM 和 **ntlm_auth** 向任意应用程序提供的一系列服务以及 Samba 本身提供服务。

即使 winbind 未用于 nsswitch，它仍然通过管理到域控制器的连接，为 **smbd**、**ntlm_auth** 和 **pam_winbind.so** PAM 模块提供服务。在此配置中，*idmap uid* 和 *idmap gid* 参数不是必需的。（这被称为“仅 netlogon 代理模式”。）

名称服务切换允许从不同的数据库服务（如 NIS 或 DNS）获取用户和系统信息。具体行为可以通过 */etc/nsswitch.conf* 文件进行配置。用户和组在解析为 Samba 系统管理员指定的用户和组 ID 范围时被分配。

**winbindd** 提供的服务称为“winbind”，可用于从 Windows NT 服务器解析用户和组信息。该服务还可通过相关的 PAM 模块提供身份验证服务。

pam_winbind 模块支持 *auth*、*account* 和 *password* 模块类型。需要注意的是，*account* 模块仅执行 *getpwnam*() 以验证系统能否为用户获取 uid，因为域控制器已经执行了访问控制。如果 *libnss_winbind* 库已正确安装，或配置了替代名称源，这应该总是成功的。

以下 nsswitch 数据库由 winbindd 服务实现：

- **hosts** 此功能仅在 IRIX 上可用。传统上存储在 *hosts*(5) 文件中并由 **gethostbyname**(3) 函数使用的用户信息。名称通过 WINS 服务器或广播进行解析。
- **passwd** 传统上存储在 *passwd*(5) 文件中并由 **getpwent**(3) 函数使用的用户信息。
- **group** 传统上存储在 *group*(5) 文件中并由 *getgrent*(3) 函数使用的组信息。

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

- **-F** 如果指定了此参数，主 **winbindd** 进程将不会守护化，即不会双重 fork 并与终端分离。子进程仍会正常创建以服务每个连接请求，但主进程不会退出。此操作模式适用于在 Daniel J. Bernstein 的 **daemontools** 包中的 **supervise** 和 **svscan** 等进程监控器下运行 **winbindd**，或适用于 AIX 进程监控器。
- **-S** 如果指定了此参数，**winbindd** 将记录到标准输出而不是文件。
- **-V** 打印程序版本号。
- **-s <配置文件>** 指定的文件包含服务器所需的配置详细信息。此文件中的信息包括服务器特定的信息，例如使用哪个主体文件，以及对服务器将提供的所有服务的描述。更多信息请参见 *smb.conf*。默认配置文件名在编译时确定。
- **-d**`-debug=debuglevel` *debuglevel* 是 0 到 10 之间的整数。如果未指定此参数，默认值为零。

此值越高，记录到日志文件中的关于服务器活动的详细信息就越多。在级别 0 时，仅记录严重错误和重大警告。级别 1 适合日常运行 - 它生成少量关于执行的操作的信息。

级别 1 以上将生成大量的日志数据，仅在调查问题时使用。级别 3 以上专为开发者设计，并生成 HUGE 数量的日志数据，其中大部分极其晦涩难懂。

请注意，在此处指定此参数将覆盖 smb.conf 文件中的参数。

- **-logfile** logdirectory 日志/调试文件的基础目录名称。将添加扩展名“ .program”（例如 log.smbclient, log.smbd, 等..）。客户端永远不会删除日志文件。
- **-h, -help** 打印命令行选项摘要。
- **-i** 告知 **winbindd** 不成为守护进程并与当前终端分离。此选项由开发者在需要对 **winbindd** 进行交互式调试时使用。**winbindd** 也会记录到标准输出，就好像给出了 -S 参数一样。
- **-n** 禁用缓存。这意味着 winbindd 在响应客户端之前必须始终等待域控制器的响应，从而使其变慢。然而，结果会更加准确，因为缓存中的结果可能不是最新的。如果 DC 没有响应，这也可能导致 winbindd 暂时挂起。
- **-Y** 单守护进程模式。这意味着 winbindd 将作为单个进程运行（Samba 2.2 中的操作模式）。Winbindd 的默认行为是启动一个负责更新过期缓存条目的子进程。

## 名称和 ID 解析

Windows NT 服务器上的用户和组在创建时被分配一个安全标识符（SID），该标识符是全局唯一的。要将 Windows NT 用户或组转换为 unix 用户或组，需要 SID 与 unix 用户和组 ID 之间的映射。这是 **winbindd** 执行的工作之一。

当 winbindd 从服务器解析用户和组时，用户和组 ID 从指定范围中分配。这是按先到先得的基础进行的，尽管一旦客户端执行用户或组枚举命令，所有现有的用户和组都会被映射。分配的 unix ID 存储在 Samba 锁定目录下的数据库文件中，并将被记住。

警告：SID 到 unix ID 的数据库是 winbindd 存储用户和组映射的唯一位置。如果此文件被删除或损坏，就没有办法

