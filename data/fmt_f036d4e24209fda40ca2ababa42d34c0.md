
- **Bad Password**：静默地将任何输入错误密码的用户登录为**来宾**。如果用户密码错误并因此在不知情的情况下以**来宾**身份登录，她可能会看到比习惯中更少的共享，这可能会让用户感到困惑。

默认值：`never`

## passdb backend

指定 `Samba` 如何存储密码。对于 `LDAP` 设置为 `ldapsam`，对于 `Samba` 设置为 `smbpasswd`，对于 `TDB`（简单数据库）密码存储设置为 `tdbsam`。有关使用 `smbpasswd` 更改或添加 `Samba` 密码的说明，请参见第 831 页。

默认值：`tdbsam`

## passwd chat

`Samba` 用来与由 `passwd program` 定义的程序进行交互的聊天脚本。如果不遵循此脚本，`Samba` 不会更改密码。仅当 `unix passwd sync` 设置为 `YES` 时使用。

默认值：

```
%s\n
%s\n
%s
```

*(注：原文表明了一个特定的默认格式，通常是`<newpassword>`，但标准的`Samba`手册页通常显示提示符和响应。如果暗示了特定字符串，我将保留原文的具体默认值结构，但在此处`OCR`显示：)*

默认值：

`<newpassword> %\n`

`<newpassword> %\n`

`<changed>`

## passwd program

`Samba` 用于设置 `Linux` 密码的程序。`Samba` 用用户的用户名替换 `%u`。

默认值：无

## security

指定客户端是否以及如何向服务器传输用户名和密码信息。选择以下之一：

- `USER`：导致 `Samba` 要求 `Windows` 用户在登录到 `Samba` 服务器时提供用户名和密码。使用此设置您可以使用：

    - `username map` 将 `Samba` 用户名映射到 `Linux` 用户名

    - `encrypt passwords` 加密密码（推荐）

    - `guest account` 将用户映射到**来宾账户**

- `SHARE`：导致 `Samba` 不针对每个用户进行身份验证。相反，`Samba` 使用 `Windows 9x` 设置，其中每个共享可以为读取或完全访问权限设置单独的密码。此选项与较新版本的 `Windows` 不兼容。

- `SERVER`：导致 `Samba` 使用另一个 `SMB` 服务器来验证用户名和密码。如果远程验证失败，本地 `Samba` 服务器会尝试像 `security` 设置为 `USER` 那样验证用户名和密码。

- `DOMAIN`：`Samba` 将加密的密码传递给 `Windows NT` 域控制器进行验证。要使 `DOMAIN` 生效，必须正确设置 `smb.conf` 中的 `workgroup` 参数。

- `ADS`：指示 `Samba` 使用 `Active Directory` 服务器进行身份验证，允许 `Samba` 服务器作为原生 `Active Directory` 成员参与。（`Active Directory` 是 `Windows 2000` 及更高版本使用的集中信息系统。它取代了 `Windows NT` 及更早版本使用的 `Windows` 域。）

默认值：`USER`

## unix password sync

`YES` 导致 `Samba` 在关联用户更改加密的 `Samba` 密码时更改用户的 `Linux` 密码。

默认值：`NO`

## username map

指向一个将 `Windows` 用户名映射到 `Linux` 用户名的用户映射文件。更多信息请参见第 830 页的“User maps”。

默认值：无映射

# 日志参数

## log file

`Samba` 日志文件的名称。`Samba` 用客户端系统名称替换 `%m`，允许您为每个客户端生成单独的日志文件。

默认值：无

`Fedora/RHEL`：`/var/log/samba/log.%m`

## log level

设置日志级别，0（零）表示关闭，较高的数字表示更详细的日志。

默认值：`0`（关闭）

## max log size

指定日志文件最大大小（以千字节为单位）的整数。0（零）指定无限制。当文件达到此大小时，`Samba` 在文件名后追加 `.old` 并开始新的日志，删除旧的日志文件。

默认值：`5000`

`Fedora/RHEL`：`50`

# 浏览器参数

*域主浏览器* 是负责维护在浏览时使用的网络机器列表的系统。`SMB` 每 11–15 分钟使用加权选举来确定哪台机器是 **域主浏览器**。`Samba` 服务器是否赢得此选举取决于两个参数：

- 将 `domain master` 设置为 `YES` 指示 `Samba` 服务器参加选举。

- `os level` 决定 `Samba` 服务器的投票权重。`os level` 的最大设置为 `255`，尽管将其设置为 `65` 应可确保 `Samba` 服务器获胜。`NT Server` 系列域控制器——包括 `Windows 2000`、`XP` 和 `2003`——使用 `os level` 为 `32`。

## domain master

`YES` 导致 `nmbd` 尝试成为 `domain master` 浏览器。如果存在 `domain master` 浏览器，则本地主浏览器将向其转发其浏览列表的副本。如果没有 `domain master` 浏览器，则浏览查询可能无法跨越子网边界。`Windows PDC`（主域控制器）始终尝试成为 `domain master`，如果失败可能会表现异常。更多信息请参见前面的讨论。

默认值：`AUTO`

## local master

`YES` 导致 `nmbd` 参加子网上本地主浏览器的选举。本地主浏览器存储本地子网上实体 *NetBIOS* 名称的缓存，允许浏览。`Windows` 机器自动参加选举；为了使浏览正常工作，网络必须至少有一台 `Windows` 机器或一台将 `local master` 设置为 `YES` 的 `Samba` 服务器。将 `local master` 设置为 `NO` 是不好的做法。如果您不想让计算机充当本地主，请将其 `os level` 设置为较低的数字，以便在所有其他方法失败时可以将其用作本地主。

默认值：`YES`

## os level

控制 `Samba` 如何为其工作组广播自身以进行浏览器选举，以及 `nmbd` 成为本地主浏览器可能性的整数。较高的数字增加了本地服务器成为本地主浏览器的机会。更多信息请参见本部分开头的讨论。

默认值：`20`

## preferred master

`YES` 强制 `nmbd` 持有本地主选举，并以轻微的优势进入本地系统。将 `domain master` 设置为 `YES` 时，此参数有助于确保本地 `Samba` 服务器成为 `domain master`。在多台服务器上将此参数设置为 `YES` 会导致这些服务器竞争成为主服务器，产生大量网络流量，有时导致不可预测的结果。`Windows PDC` 自动表现为此参数设置为 `YES`。

默认值：`AUTO`

# 通信参数

## dns proxy

在作为 *WINS服务器* 运行时，`YES` 导致 `nmbd` 在 *NetBIOS* 解析失败时使用 `DNS`。

默认值：`YES`

## socket options

调整与客户端交换数据时使用的网络参数。

默认值：`TCP_NODELAY`

## wins server

`nmbd` 应注册的 `WINS` 服务器的 `IP` 地址。

默认值：未启用

## wins support

`YES` 指定 `nmbd` 将作为 `WINS` 服务器运行。

默认值：`NO`

# 共享参数

以下每个参数都可以在 `smb.conf` 中出现多次，在每个共享定义中出现一次。

## available

`YES` 指定该共享为活跃状态。将此参数设置为 `NO` 以禁用共享，但继续记录其请求。

默认值：`YES`

## browsable

确定是否可以在例如 `Windows`“网上邻居”中浏览该共享。

默认值：`YES`

`Fedora/RHEL`：各不相同

## comment

共享的描述，在从 `Windows` 浏览网络时显示。

默认值：无

`Fedora/RHEL`：各不相同

## guest ok

允许以 `guest` 身份登录的用户访问此共享。

默认值：`NO`

`Fedora/RHEL`：各不相同

## path

被共享目录的路径。

默认值：无

`Fedora/RHEL`：各不相同

## read only

不允许写入访问。使用 `writable` 允许读写访问。

默认值：`YES`

`Fedora/RHEL`：各不相同

## 故障排除

`Samba` 和 `Windows` 提供了可用于排查连接问题的工具。本节将讨论这些工具，并建议在 `Samba` 无法工作时用于缩小问题范围的技巧。

1. 重启 `Samba` 守护进程。通常，在修改 `smb.conf` 文件后无需重启这些守护进程。请确保 `smbd` 和 `nmbd` 正在运行。

   ```bash
   # systemctl reload smb
   # systemctl reload nmb
   # systemctl status smb
   ...
   # systemctl status nmb
   ...
   ```

2. 运行 `testparm` 以确认 `smb.conf` 文件语法正确：

   ```bash
   $ testparm
   Load smb config files from /etc/samba/smb.conf
   Processing section "[homes]"
   Processing section "[printers]"
   Processing section "[tmp]"
   Loaded services file OK.
   Server role: ROLE_STANDALONE
   Press enter to see a dump of your service definitions
   ...
   ```

   您可以忽略有关 `rlimit_max` 的错误信息。如果在 `smb.conf` 中拼写错误关键字，您将获得如下错误：

   ```bash
   $ testparm
   Load smb config files from /etc/samba/smb.conf
   Unknown parameter encountered: "workgroup"
     Ignoring unknown parameter "workgroup"
   ...
   ```

3. 检查 `/var/log/samba` 中的日志文件（第 843 页）。

4. 使用 `ping`（第 305 页）从连接的两端进行操作，以确保网络正常运行。

5. 确认服务器上的防火墙没有阻止服务器或客户端上的 `Samba` 连接（第 836 页）。命令 `firewall-cmd --list-ports` 会显示本地系统上的开放端口。

6. 确保尝试登录的用户作为 `Samba` 用户存在。参见第 831 页的 `pdbedit`。

7. 确保您已为尝试登录的 `Samba` 用户设置了密码。参见第 831 页的 `smbpasswd`。

8. 您可能需要修改 `SELinux` 策略。参见第 836 页和第 840 页。

9. 如果您指定了 `hosts deny` 的值，请务必指定 `hosts allow` 的值，包括 `127.0.0.1`，以便您可以从本地系统访问 `Samba`。更多信息请参见第 842 页。

10. 在 `Windows` 命令提示符中，使用 `net view` 显示服务器（本例中为 `plum`）提供的共享列表：

    ```text
    C:\>net view \\plum

    Shared resources at \\plum

    Samba Server Version 4.0.6

    Share name   Type   Used as Comment

    sam          Disk   Home Directories
    tmp          Disk   Temporary Directory

    The command completed successfully.
    ```

11. 尝试从 `Windows` 命令提示符映射（挂载）驱动器。以下命令尝试将 `plum` 上名为 `sam` 的共享映射为驱动器 `X:`

    ```text
    C:\>net use x: \\plum\sam

    Enter the user name for 'plum': sam
    Enter the password for plum:

    The command completed successfully.
    ```

12. 在 `Samba` 服务器上，使用 `nmblookup`（`samba-client` 包）查询 `nmbd` 服务器，使用特殊名称 `__SAMBA__` 作为服务器的 `NetBIOS` 名称。`-d 2` 选项在第 2 级打开调试器，生成中等数量的输出。`-B` 选项指定要查询的服务器。

    ```bash
    $ nmblookup -d 2 -B 127.0.0.1 __SAMBA__
    ...
    Querying __SAMBA__ on 127.0.0.1
    Got a positive name query response from 127.0.0.1 ( 192.168.206.181 )
    192.168.206.181 __SAMBA__<00>
    ```

下一个示例使用 `nmblookup`，不设置调试级别，查询本地系统的所有 `NetBIOS` 名称。

```bash
$ nmblookup -B 127.0.0.1 \
querying * on 127.0.0.1 <00>
192.168.206.181 *<00>
```

要从本地服务器查询主浏览器，请运行 `nmblookup`，并加上 `-A` 选项，后跟 `localhost` 或服务器名称：

```bash
$ nmblookup -A 127.0.0.1
Looking up status of 127.0.0.1
PLUM <00> - B <ACTIVE>
PLUM <03> - B <ACTIVE>
PLUM <20> - B <ACTIVE>
MCS <00> - <GROUP> B <ACTIVE>
MCS <1e> - <GROUP> B <ACTIVE>

MAC Address = 00-00-00-00-00-00
```

13. 在 `Samba` 服务器上，使用 `smbclient`（`samba-client` 包）加上 `-L` 选项后跟服务器名称，以生成服务器提供的共享列表。当您未输入密码时，`smbclient` 会显示匿名用户可用的共享。当您输入密码时，它还显示受限共享，包括该用户的 `[homes]` 共享。

    ```bash
    $ smclient -L localhost
    Enter sam's password: RETURN (do not enter a password)
    Anonymous login successful
    Domain=[MGS] OS=[Unix] Server=[Samba 4.0.6]

    Sharename          Type          Comment
    ---------          ---------     -----------------
    tmp                Disk          Temporary Directory
    IPC$               IPC           IPC Service (Samba Server Version 4.0.6)

    Anonymous login successful
    Domain=[MGS] OS=[Unix] Server=[Samba 4.0.6]

    Server            Comment
    ----------------  -----------------
    PEACH
    PLUM              Samba Server Version 4.0.6
    Workgroup         Master
    MGS               PEACH
    ```

## 本章小结

`Samba` 是一套程序，可让服务器向客户端共享目录层次结构和打印机。通常，服务器是 `Linux` 系统，客户端是 `Windows` 机器。`Samba` 在服务器和客户端系统之间共享的目录层次结构或打印机称为 *share*（共享）。要访问 `Linux` 系统上的共享，`Windows` 用户必须提供用户名和密码。用户名必须直接对应于 `Linux` 用户名，或由 `smb.conf` 中 `username map` 参数指向的文件（通常是 `/etc/samba/smbusers`）映射对应。`Samba` 密码由 `smbpasswd` 生成，并保存在名为 `tdbsam` 的 trivial Database 中。`Samba` 的主要配置文件是 `/etc/samba/smb.conf`，您可以使用 `system-config-samba`（仅限 `Fedora`）或文本编辑器进行编辑。

从 `Windows` 机器，您可以通过打开目录或资源管理器窗口，并在窗口顶部附近的地址文本框中输入 `\\` 后跟服务器名称来访问 `Samba` 服务器上的共享。响应地，`Windows` 会显示服务器上的共享。您可以像处理 `Windows` 文件一样处理这些共享。

从 `Linux` 系统，您可以使用几种 `Samba` 工具来访问共享。这些工具包括 `smbtree`（显示共享）、`smbclient`（类似于 `ftp`）以及带有 `-t cifs` 选项的 `mount`（挂载共享）。此外，您可以从终端模拟器或 Enter a Command 窗口（`ALT-F2`）输入 `nautilus` 来浏览共享。

## 练习题

1. 哪两个守护进程是 `Samba` 套件的一部分？每个做什么？

2. 将 `Windows` 用户映射到 `Linux` 用户需要哪些步骤？

3. 系统管理员如何为新用户添加 `Samba` 密码？

4. `[homes]` 共享的用途是什么？此共享是否应该可浏览？为什么？

## 高级练习题
