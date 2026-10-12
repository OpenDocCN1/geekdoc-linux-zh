
当 Windows 用户尝试访问 Samba 服务器时，在登录（SMB 协议中的会话设置）时，`smbd(8)` 会联系密码服务器并尝试用给定的密码验证给定的用户。如果身份验证成功，`smbd` 会尝试在 UNIX 密码数据库中查找一个 UNIX 用户以映射该 Windows 用户。如果此查找失败，且已设置 `add user script`，则 `smbd` 将以 `ROOT` 身份调用指定的脚本，将任何 `%u` 参数扩展为要创建的用户名。

如果此脚本成功创建了用户，则 `smbd` 将继续操作，就好像该 UNIX 用户已经存在一样。通过这种方式，动态创建 UNIX 用户以匹配现有的 Windows NT 账户。

另请参阅 `security`、`password server`、`delete user script`。

## add user to group script (G) 默认值：无默认值

示例：`add user to group script = /usr/sbin/adduser %u %g`

这是当用户使用 Windows NT 域管理工具将用户添加到组时将调用的脚本的完整路径。它将由 `smbd(8)` 以 `ROOT` 身份运行。任何 `%g` 将被替换为组名，任何 `%u` 将被替换为用户名。

请注意，下面示例中使用的 `adduser` 命令并非在所有系统上都支持所使用的语法。

## admin users (S) 默认值：无默认值

示例：`admin users = jason`

这是一个将被授予共享管理特权的用户列表。这意味着他们将作为超级用户（`root`）执行所有文件操作。

您应该非常谨慎地使用此选项，因为在此列表中的任何用户都将能够在共享上执行任何他们喜欢的操作，而不管文件权限如何。

在 Samba 3.0 中，此参数将无法与 `security = share` 一起工作。这是设计使然。

## afs share (S) 默认值：`afs share = no`

此参数控制是否为此共享启用特殊的 AFS 功能。如果启用，它假定通过 `path` 参数导出的目录是一个本地 AFS 导入。特殊的 AFS 功能包括尝试手工制造一个 AFS token，如果在 `configure` 中启用了 `--with-fake-kaserver`。

映射的用户名必须包含要登录的 `cell` 名称，因此如果不设置此参数，将不会有 `token`。

## algorithmic rid base (G) 默认值：`algorithmic rid base = 1000100000`

示例：`algorithmic rid base = 100000`

这决定了 Samba 如何使用其算法映射，将 `uid/gid` 映射到构建 NT 安全标识符（SID）所需的 `RID`。

将此选项设置为较大的值可能对从 WinNT 和 Win2k 过渡的网站有用，否则现有的用户和组 `rid` 将与系统用户等发生冲突。

所有 UID 和 GID 必须能够解析为 SID，以便服务器上的 ACL 正确运行。因此，算法映射无法“关闭”，但将其“挪开”应该能解决这些问题。然后可以在支持 `arbitrary-rid` 的后端中为用户和组分配“低”RID。

## allocation roundup size (S) 默认值：`allocation roundup size = 10485760`（以禁用向上取整）

示例：`allocation roundup size = 0`（以禁用向上取整）

此参数允许管理员调整报告给 Windows 客户端的分配大小。默认的 1MB 大小通常会导致 Windows 客户端性能提高。然而，分配大小向上取整可能会给某些应用程序带来困难，例如 MS Visual Studio。如果 MS Visual Studio 编译器开始因内部错误而崩溃，请为此共享将此参数设置为零。

整数参数指定以字节为单位的向上取整大小。

## allow trusted domains (G) 默认值：`allow trusted domains = yes`

此选项仅在 `security` 选项设置为 `server`、`domain` 或 `ads` 时生效。如果设置为 `no`，则试图从 `smbd` 所在的域或工作组以外的域或工作组连接到资源将失败，即使该域被执行身份验证的远程服务器信任。

如果您只想让 Samba 服务器向其所属域中的用户提供资源，这将非常有用。举个例子，假设有两个域 `DOMA` 和 `DOMB`。`DOMB` 被 `DOMA` 信任，且 Samba 服务器位于 `DOMA` 中。在正常情况下，在 `DOMB` 中有账户的用户可以访问 Samba 服务器上具有相同账户名的 UNIX 账户的资源，即使他们在 `DOMA` 中没有账户。这使得实施安全边界变得困难。

## announce as (G) 默认值：`announce as = NT Server Win95`

示例：`announce as = Win95`

此参数指定 `nmbd(8)` 在网络邻居浏览列表中声明自己为何种类型的服务器。默认值设置为 Windows NT。有效选项为：`"NT Server"`（也可写作 `"NT"`）、`"NT Workstation"`、`"Win95"` 或 `"WfW"`，分别代表 Windows NT Server、Windows NT Workstation、Windows 95 和 Windows for Workgroups。除非你有特定需求希望停止 Samba 以 NT 服务器身份出现（否则这可能会阻止 Samba 服务器正确参与浏览器服务器角色），否则请勿更改此参数。

## announce version (G)

默认值：`announce version = 4.9.0`

示例：`announce version = 2.0`

此参数指定 `nmbd` 在宣布自身为服务器时所使用的重大版本和次要版本号。默认值为 4.9。除非你有特定需求将 Samba 服务器设置为低版本服务器，否则请勿更改此参数。

## auth methods (G)

默认值：*无默认值*

示例：`auth methods = guest sam winbind`

此选项允许管理员选择 `smbd` 在验证用户时使用的认证方法。此选项会根据 `security`（安全性设置）取合理的默认值。这应被视为开发者选项，仅在极少数情况下使用。在大多数（如果不是全部）生产服务器中，默认设置应该就足够了。

列表中的每一项将依次尝试对用户进行身份验证，直到用户成功认证。实际上，通常只有其中一种方法能够完成认证。

可能的选项包括：

- `guest`（匿名访问）
- `sam`（基于 NetBIOS 名称或域名称在本地账户列表中查找）
- `winbind`（通过 `winbindd` 将认证请求转发给远程用户）
- `ntdomain`（针对远程域用户的 pre-winbind 认证方法；已被弃用，建议改用 `winbind` 方法）
- `trusteddom`（通过 `smbd` 直接联系远程域控制器来认证受信用户；已被弃用，建议改用 `winbind` 方法）

## available (S)

默认值：`available = yes`

此参数允许你“关闭”一个服务。如果 `available = no`，则*所有*尝试连接该服务的操作都将失败。此类失败会被记录日志。

## bind interfaces only (G)

默认值：`bind interfaces only = no`

此全局参数允许 Samba 管理员限制机器上的哪些接口可以处理 SMB 请求。它对文件服务 `smbd(8)` 和名称服务 `nmbd(8)` 的影响略有不同。

对于名称服务，它会促使 `nmbd` 绑定到 `interfaces` 参数中列出的接口上的 137 和 138 端口。`nmbd` 还会绑定到“所有地址”接口（`0.0.0.0`）的 137 和 138 端口，以读取广播消息。如果未设置此选项，`nmbd` 将在所有这些套接字上提供名称请求服务。如果设置了 `bind interfaces only`，则 `nmbd` 将检查通过广播套接字传入的数据包的源地址，并丢弃那些不匹配 `interfaces` 参数列表中接口广播地址的数据包。由于单播数据包是在其他套接字上接收的，这允许 `nmbd` 拒绝为通过任何未列在 `interfaces` 列表中的接口发送数据包的主机提供名称服务。然而，IP 源地址欺骗可以击败这种简单的检查，因此不应将其作为 `nmbd` 的安全功能严肃使用。

对于文件服务，它促使 `smbd(8)` 仅绑定到 `interfaces` 参数中给出的接口列表。这将 `smbd` 服务的网络限制为通过那些接口传入的数据包。请注意，不要将此参数用于提供 `PPP` 或其他间歇性或非广播网络接口的机器，因为它无法应对非永久性接口。

如果设置了 `bind interfaces only`，除非将网络地址 `127.0.0.1` 添加到 `interfaces` 参数列表中，否则由于以下原因，`smbd(8)` 和 `nmbd(8)` 可能无法按预期工作。
