
防火墙是信息安全领域增长最快的技术工具之一。然而，防火墙的安全性仅取决于其所驻留的操作系统的安全性。

## TCP Wrappers

另一个问题是 TCP Wrappers。TCP Wrappers 是在 UNIX 系统上常用的一种工具，用于监控和过滤对网络服务的连接。虽然它不进行加密，但 TCP Wrappers 会记录日志并控制谁可以访问你的系统。它是一个二进制程序，会包裹在 inetd 服务周围，例如 telnet 或 ftp。使用 TCP Wrappers 时，系统会为 inetd 连接启动包装器，记录所有尝试，然后将尝试与 ACL 进行核对。如果连接被允许，TCP Wrappers 会将连接交给适当的二进制程序，例如 telnet。如果访问控制列表拒绝连接，则连接将被丢弃。

防火墙为什么需要 TCP Wrappers？防火墙难道不已经为你完成所有这些工作了吗？首先，以防防火墙被攻破或崩溃，TCP Wrappers 提供了一层额外的防御。没有防火墙是百分之百安全的。其次，TCP Wrappers 可防止防火墙配置错误，从而可能为黑客提供入口点。第三，TCP Wrappers 增加了一层日志记录——验证其他系统日志。

> NOTE
> 请务必使用防火墙以外的系统来检索和编译 TCP Wrappers。你不应在防火墙上保留编译器。

## The /etc/default/login File

通过 /etc/default/login 文件，无论系统是否在互联网上，都可以防止未经授权的访问的最后一种方法。确保以下行未被注释：

```
CONSOLE=/dev/console
```

有了此条目，root 只能从安全的系统控制台登录，而不能通过网络使用 telnet 或 rlogin 登录。但是，此条目并不会禁止用户在以普通用户身份登录后使用 su 命令切换到 root。

## Modems

调制解调器始终是入侵者的潜在入口点。任何发现电话号码的人都可以尝试登录。低成本计算机可以被改造成自动拨号设备，搜索调制解调器线路，然后无休止地尝试猜测密码并入侵。如果必须使用调制解调器，只能用于外拨呼叫。外拨调制解调器不会接听电话。如果允许来电，请实施回调系统。回调系统可保证只有授权的电话号码才能连接到系统。另一种选择是使用两个调制解调器，在两者之间建立安全密钥。这样，只有具有安全密钥的调制解调器才能与系统调制解调器连接并访问计算机。

## The Trusted Host

除了保护密码之外，你还需要保护系统免受来自网络另一端的 root 用户入侵。例如，systemA 是一个可信主机，用户可以从该主机登录而无需输入密码。请注意，如果 systemA 设置为 systemB 上的可信主机，则在 systemA 上具有 root 访问权限的用户只需通过网络登录即可访问 systemB 上的 root 登录。当 systemB 尝试从 systemA 对 root 进行身份验证时，它依赖于本地文件中的信息——具体来说是 /etc/hosts.equiv 和 ~/.rhosts。

## The /etc/hosts.equiv File

/etc/hosts.equiv 文件包含远程系统的可信主机列表，每行一个。/etc/hosts.equiv 文件的结构如下：

```
system1
system2 user_a
```

如果用户（root）尝试从此文件中列出的主机之一使用 rlogin 远程登录，并且如果远程系统可以访问用户的密码条目，则远程系统允许用户无需密码登录。

当在 /etc/hosts.equiv 中为主机创建条目时，例如 system1 的示例条目，这意味着该主机受信任，该机器上的任何用户也受信任。如果同时提及用户名，如同一文件中的第二个条目，则只有在指定用户尝试访问时主机才受信任。/etc/hosts.equiv 文件中单行 + 表示所有已知主机均受信任。

/etc/hosts.equiv 文件存在安全风险。如果你在系统上维护 /etc/hosts.equiv 文件，该文件应仅包含网络中的可信主机。该文件不应包含属于不同网络的任何主机或位于公共区域的任何机器。

## The .rhosts File

.rhosts 文件是 /etc/hosts.equiv 文件的用户等价物。它包含主机和用户的列表。如果此文件中列出了主机-用户组合，则指定用户将被授予权限，可从指定主机远程登录而无需提供密码。请注意，.rhosts 文件必须位于用户主目录的顶层，因为位于子目录中的 .rhosts 文件不会被查阅。用户可以在其主目录中创建 .rhosts 文件——这是允许在不同系统上其自己的账户之间进行可信访问的另一种方式，而无需使用 /etc/hosts.equiv 文件。

.rhosts 文件存在重大的安全问题。虽然 /etc/hosts.equiv 文件由系统管理员控制，可以有效管理，但任何用户都可以创建 .rhosts 文件授予其选择的任何人访问权限——而系统管理员并不知情。

当所有用户的主目录都在一台服务器上，并且只有某些人拥有该服务器的超级用户访问权限时，防止用户使用 .rhosts 文件的一个好方法是（以超级用户身份）在用户主目录中创建一个空的 .rhosts 文件。然后，将此文件的权限更改为 000，以便即使以超级用户身份更改它也很困难。这将有效地防止用户通过不负责任地使用 .rhosts 文件而危及系统安全。

> TIP
> 将 root 登录更改为“root”以外的名称，并且永远不要在 /etc/hosts.equiv 文件中仅放置系统名称而不跟用户名或多个名称。

管理 .rhosts 文件的唯一安全方法是完全禁止它们。此策略的一个可能例外是 root 账户，该账户可能需要 .rhosts 文件来执行网络备份和其他远程服务。

## Restricting FTP

Solaris 8 的文件传输协议（FTP）是跨网络传输文件的常用工具。虽然大多数站点都保留 FTP 启用状态，但你需要限制谁可以使用它。Solaris 8 包含一个名为 /etc/ftpusers 的文件，用于限制通过 FTP 的访问。/etc/ftpusers 文件包含禁止在系统上运行 FTP 登录的登录名列表。以下是默认 /etc/ftpusers 文件的示例：

```
# more /etc/ftpusers
root
daemon
bin
sys
adm
lp
uucp
nuucp
listen
nobody
noaccess
nobody4
```

> NOTE
> Solaris 8 的默认设置是不允许 root 通过 FTP 登录。如果你选择允许 root 通过 FTP 登录，请从 /etc/ftpusers 文件中删除“root”。此外，请确保 /etc/default/login 文件允许远程 root 登录权限。此过程在后面标题为“Restricting Root Access”的部分中进行了描述。

此文件中的名称必须与你的 /etc/passwd 文件中的登录名匹配。

名为 in.ftpd 的 FTP 服务器守护进程在每次调用 FTP 会话时都会读取 /etc/ftpusers 文件。如果尝试获得访问权限的用户的登录名与 /etc/ftpusers 文件中的名称匹配，则访问将被拒绝。

另一个名为 /etc/shells 的文件包含系统上的 shell 列表。而 /etc/ftpusers 文件包含不允许使用 FTP 的用户列表，/etc/shells 文件将只允许运行在此文件中定义的 shell 的用户进行 FTP 连接。如果此文件存在，并且 shell 的条目不存在于此文件中，则运行未定义 shell 的任何用户都不会被允许连接到此系统的 FTP。

/etc/shells 文件默认不存在。如果文件不存在，系统将使用系统默认 shell。系统默认 shell 如下：

|  |  |
|---|---|
| /bin/bash | /sbin/sh |
| /bin/csh | /usr/bin/bash |
| /bin/jsh | /usr/bin/csh |
| /bin/ksh | /usr/bin/jsh |
| /bin/pfcsh | /usr/bin/ksh |
| /bin/pfksh | /usr/bin/pfcsh |
| /bin/pfsh | /usr/bin/pfksh |
| /bin/sh | /usr/bin/pfsh |
| /bin/tcsh | /usr/bin/sh |
| /bin/zsh | /usr/bin/tcsh |
| /sbin/jsh | /usr/bin/zsh |

你可以使用 vi 编辑器创建此文件并列出你希望系统识别的每个 shell。以下是 /etc/shells 文件的示例：

```
# more /etc/shells
    /sbin/sh
    /bin/sh
    /bin/ksh
```

> NOTE
> 如果你没有在 /etc/shells 文件中列出所有默认 shell，如我在前一个示例中所做的那样，使用这些 shell 的用户将不被允许访问。

## Securing Superuser Access

UNIX 超级用户身份不受对系统其他用户施加的限制的约束。任何 UID 为零（0）的 UNIX 账户都是超级用户。所有 UNIX 系统都有一个名为 root 的默认超级用户登录。此账户的用户可以访问任何文件并运行任何命令。此登录很有价值，因为任何可能因删除访问权限、忘记密码或只是需要从其无权访问的区域获取文件而陷入困境的用户都可以由 root 帮助。
