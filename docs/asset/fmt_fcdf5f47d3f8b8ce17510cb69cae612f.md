
与 NT 和 2000一样，访问共享上的某些数据不能仅通过文件共享软件的权限来实现；在 NT 和 2000 上，你需要 NTFS 文件和目录安全系统的配合，而在 Linux 和 Samba 中，情况也是如此。

正如你在第 6 章中所学的那样，你可以使用 `chmod` 命令在 Linux 中设置文件或目录的权限。如果你这样做，那么任何尝试访问 Samba 共享上数据的人都必须满足 Samba 权限（`write list` 或 `read list`）以及文件和目录权限的可能性。但请记住，Linux 并不提供丰富的文件和目录权限选项。这层额外的安全保障很棒，但如果你花费大量时间通过共享和文件/目录权限来精调安全性，请要小心，否则可能会产生支持性问题——如果你通过目录权限排除了某人并忘记了这样做，当你给那个人赋予 `write list` 权限但他仍然无法访问共享时，你会疯掉的！

# 关于 Windows 2000 的说明

到目前为止，我的示例都涉及 NT 4 域。你也可以对 Windows 2000 域执行相同的操作；你的 Samba 服务器可以轻松在 Windows2000 域上进行验证，就像任何 NT 4.0 系统都可以加入 Active Directory 一样。但在将 Samba 服务器连接到 Windows 2000 时，有几点需要。

首先，如果你设置了 Active Directory 的“不接受 NTLM 登录”设置，那么你的 NT 4.0 机器和 Samba 机器都无法成为该域的一部分。NT 4.0 无法使用 Kerberos，如果 Active Directory 只理解 Kerberos 登录，那么你就麻烦了。Samba 运行在 Linux 之上，Linux 确实理解 Kerberos，但方式并不是 Active Directory 所喜欢的程度。不过，你可以在互联网上阅读一篇有趣的文章，关于某人如何成功让他的 Linux 机器登录 Active Directory，地址为：http://acd.ucar.edu/~fredrick/linux/ad.html。

其次，当你使用“Active Directory 用户和计算机”为 Samba 服务器创建计算机帐户时，你会看到一个名为“允许 Windows 2000 计算机使用此账户”（Allow Pre-Windows 2000 Computers to Use This Account）的复选框。如果你是 Windows 2000 新手且不确定如何创建计算机账户，请遵循这些指令：

- 1. 登录到 W2K 域控制器。
- 2. 点击开始 > 管理工具 > Active Directory 用户和计算机。
- 3. 在代表域的左侧面板上，右键点击并选择新建 > 计算机。
- 4. 在弹出的面板中，勾选标记为“允许 Windows 2000 计算机使用此账户”的框并点击确定。

第三，当你引用 Windows 2000 域或域控制器时，请使用其旧式的 NetBIOS 名称进行引用。例如，如果你的 Windows 2000 域名为 `acme.com`，那么该域可能有一个名为 `ACME` 的“低级”名称。如果域控制器名为 `bigdog.acme.com`，那么它的低级名称就是 `\BIGDOG`。

# 使用 NT/2000 域验证 Linux 用户：winbind

随着 Samba 2.2 出现了一个非常有用的功能：使用 NT 4.0 或 Active Directory 域账户登录 Linux 机器的能力。你已经在第 6 章中读到，可以将 Linux 机器变成一个 NIS 服务器，在其中你可以存储一组集中的用户和组账户，使你无需为每台 Linux 机器上的每个用户重新构建用户账户。但这意味着你仍然需要维护两套集中的用户账户：NIS 账户和微软域。`winbind` 告诉 Linux，“当有人想要登录时，去某某域中的 Microsoft NT 或 AD 域控制器处验证该用户。”

`winbind` 需要几个部分：

- 当然，需要 Samba 程序（`smbd` 必须运行）。
- `nmbd` 必须在运行。
- 需要一个名为 `winbind` 的守护进程在运行。
- 你必须通过 `netjoin` 命令让 Linux 加入域。
- 你必须使用 PAM（可插拔模块）来实现。

为了让 Samba 工作，我们将一个一个地设置。我们将假设在 Linux 机器上。

# 设置 `smb.conf` 的具体示例

为了简单起见，让我们假设我们仍在旧的 REALM 域示例中工作。这是该域的 `smb.conf` 可能的如下：

```
[global]
wins server = 130.10.20.5
workgroup = REALM
server string = Test Samba Server
netbios name = LINUXBOX
security = domain
password server = *
encrypt passwords = yes
username map = /etc/linixtont
[public]
path = /publicstuff
guest ok = yes
writeable = no
write list = gerry
[private]
path = /privatestuff
guest ok = no
valid users = @managers
write list = @managers
```

`/etc/linixtont` 文件将有一条记录：

```
managers = @managers
```

在第一个共享中，我使用了 `guest ok` 而没有使用 `valid users` 语句，因为我并不在乎谁访问它，但 `writeable = no` 确保了没有人可以修改它——除了 `gerry` 之外。在第二个共享中，禁用访客并显式地仅将 `managers` 组的成员设为 `valid users`，可以将其他人全部排除在外。

# Linux 文件和目录权限 Samba

与 NT 和 2000一样，访问共享上的某些数据不能仅通过文件共享软件的权限来实现；在 NT 和 2000 上，你需要 NTFS 文件和目录安全系统的配合，而在 Linux 和 Samba 中，情况也是如此。

正如你在第 6 章中所学的那样，你可以使用 `chmod` 命令在 Linux 中设置文件或目录的权限。如果你这样做，那么任何尝试访问 Samba 共享上数据的人都必须满足 Samba 权限（`write list` 或 `read list`）以及文件和目录权限的可能性。但请记住，Linux 并不提供丰富的文件和目录权限选项。这层额外的安全保障很棒，但如果你花费大量时间通过共享和文件/目录权限来精调安全性，请要小心，否则可能会产生支持性问题——如果你通过目录权限排除了某人并忘记了这样做，当你给那个人赋予 `write list` 权限但他仍然无法访问共享时，你会疯掉的！

# 关于 Windows 2000 的说明

到目前为止，我的示例都涉及 NT 4 域。你也可以对 Windows 2000 域执行相同的操作；你的 Samba 服务器可以轻松在 Windows2000 域上进行验证，就像任何 NT 4.0 系统都可以加入 Active Directory 一样。但在将 Samba 服务器连接到 Windows 2000 时，有几点需要注意。

首先，如果你设置了 Active Directory 的“不接受 NTLM 登录”设置，那么你的 NT 4.0 机器和 Samba 机器都无法成为该域的一部分。NT 4.0 无法使用 Kerberos，如果 Active Directory 只理解 Kerberos 登录，那么你就麻烦了。Samba 运行在 Linux 之上，Linux 确实理解 Kerberos，但方式并不是 Active Directory 所喜欢的程度。不过，你可以在互联网上阅读一篇有趣的文章，关于某人如何成功让他的 Linux 机器登录 Active Directory，地址为：http://acd.ucar.edu/~fredrick/linux/ad.html。

其次，当你使用“Active Directory 用户和计算机”为 Samba 服务器创建计算机帐户时，你会看到一个名为“允许 Windows 2000 计算机使用此账户”（Allow Pre-Windows 2000 Computers to Use This Account）的复选框。如果你是 Windows 2000 新手且不确定如何创建计算机账户，请遵循这些指令：

- 1. 登录到 W2K 域控制器。
- 2. 点击开始 > 管理工具 > Active Directory 用户和计算机。
- 3. 在代表域的左侧面板上，右键点击并选择新建 > 计算机。
- 4. 在弹出的面板中，勾选标记为“允许 Windows 2000 计算机使用此账户”的框并点击确定。
