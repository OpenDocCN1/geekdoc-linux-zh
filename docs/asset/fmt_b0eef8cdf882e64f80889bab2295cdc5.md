
> 在部署任何关键应用程序之前，使用 Samba PDC 进行测试总是一个好主意。服务器应用程序（例如 Exchange 和 MS5 的 SQL Server）可能无法在所有环境中运行。这是因为这些应用程序可以使用新的 MS-RPC 调用，而 Samba 开发人员在常规 PDC 开发期间没有遇到过这些调用。如果你遇到由于 MS-RPC 而无法运行的服务器应用程序，最好的办法是向 samba-technical 邮件列表报告错误。准备好提供大量的日志文件，以帮助开发者获取实现缺失功能所需的信息。

![](img/e6dc042fe420c610acdd193e834a4772_393_0.png)

## Windows NT 4.0/2000 域控制

> Samba 2.2 只能作为 Windows NT PDC 功能，不能作为使用 Kerberos 5 和 Active Directory 的 Windows 2000 域控制器。

## 如何配置 Samba PDC

将 Samba 配置为 Windows NT/2000 客户端的域控制器，与将其配置为 Windows 9x/ME 客户端登录服务器的过程非常相似。因此，我们将使用上次定义的 `smb.conf` 作为起点。以下 `smb.conf` 重新打印自列表 21.1。

**列表 22.1** 来自第 21 小时的 `smb.conf` 文件

```
##
## Mon Aug 27 01:09:17 CDT 2001
## jerry carter <jerry@samba.org>

## 24 小时自学学 Samba
## 用于 Windows 9x 登录服务器的 smb.conf

[global]
netbios name = POGO
workgroup = STY
security = user
passwords = yes
domain = yes
logon = script
os level = 6
domain = yes
master = yes
[domain]
path = /
read only = no
public = yes
[homes]
comment = Home directories
user =
create mask = 0000
directory mask = 0700
browseable = no
valid users =
```

除了机器所需的设置（`security = user`, `logons = yes`）外，在担任 PDC 时有三个关键点需要注意：

- Samba 无法与另一个 Windows NT 4.0 风格的主域控制器建立信任关系。
- Samba 无法将 Windows NT 4.0 账户管理器 (`SAM`) 的用户和组数据库同步到 Windows NT 4.0 PDC 或备用域控制器 (`BDC`)。然而，目前可以配置具有多个 Samba BDC 的 Samba PDC。关于最后一点，将在本小时内进行更多详细介绍。
- Samba 未提供任何将 Unix 组映射到 Windows NT 全局或本地组的机制。
- Samba 允许通过 Windows NT 域用户管理器修改少数用户账户，如密码和“账户禁用”标记。

> 在部署任何关键应用程序之前，使用 Samba PDC 进行测试总是一个好主意。服务器应用程序（例如 Exchange 和 MS5 的 SQL Server）可能无法在所有环境中运行。这是因为这些应用程序可以使用新的 MS-RPC 调用，而 Samba 开发人员在常规 PDC 开发期间没有遇到过这些调用。如果你遇到由于 MS-RPC 而无法运行的服务器应用程序，最好的办法是向 samba-technical 邮件列表报告错误。准备好提供大量的日志文件，以帮助开发者获取实现缺失功能所需的信息。

![](img/e6dc042fe420c610acdd193e834a4772_393_0.png)

## 机器账户

描述机器的一种简单方法是将其称为信任账户。机器账户的用户名是带有字符的 NetBIOS 名称。每个域成员都有自己的信任账户，因此也有自己的密码。

![](img/e6dc042fe420c610acdd193e834a4772_.png)

将任何类型的客户端加入 Windows 域遵循相同的步骤：

1. 在域控制器上为客户端创建信任账户。
2. 将客户端加入域。
3. 重启客户端。

## 在 Samba PDC 上创建信任账户

在 Windows 域中创建机器账户有两种：

- 在尝试加入域之前手动创建机器账户。
- 在加入域时创建机器账户。

首先，我们考虑机器账户的通用前提：每个信任账户本质上都是由机器使用的用户账户，并且每个账户都必须关联一个相对 ID (`RID`)（如果你需要复习 RID 和 SID，请参见第 14 章）。在 Windows 域中，所有用户账户、信任账户和组都存在相同的数值空间 (`1000 – (2³ – 11)`) 这意味着无法既有一个 RID 为 1000 的组，又有一个 RID 为 1000 的用户。许多 Unix 系统有一种通用做法（在某些 Linux 发行版中是标准），使用相同的名称、`uid` 和 `gid` 创建用户和组。之所以这是可能的，是因为 `uid` 从一个池中分配，而 `gid` 从另一个池中分配，两者独立且无关。

Samba PDC 必须具备某种机制来确保每个信任账户都有唯一的 RID。显而易见的解决方案是对机器账户使用与用户账户相同的方法，并根据 `uid` 生成 RID。

这种解决方案的缺点是 Unix 不支持机器登录账户的概念，除非使用 NIS+ 等目录服务。最具可移植性的解决方案是要求 Samba 域中的每个信任账户在本地系统密码文件（即 `/etc/passwd`）中都有条目，因此具有唯一的 `uid`。尽管这并不是最优雅的解决方案，但 Samba 开发人员希望很快就会修复，该需求从版本 1.9.18 的 alpha 版本开始的域控制（Domain Control）实现一直延续了下来。

由于许多网络管理员实施了自定义系统来创建用户账户，因此很难描述一种向 `/etc/passwd` 添加账户的通用方法。然而，以下命令通常对于 Linux 发行版来说就足够了。主目录 (`-d`) 和 shell (`-s`) 已禁用，并且主组被设置为用于机器信任账户的指定 Unix 组。“`machineaccount$`”的值是新域成员的 NetBIOS 名称，后跟一个“`$`”。

```
root# useradd -d /dev/null -g ntmach -s /bin/false machine name$
```

下一个命令将防止通过 `/etc/passwd` 成功验证。请记住，`smbd` 只需要该条目来获取机器账户的 `uid`。

```
root# passwd -l "machine name$"
```

结果是一个类似于 `nt-client:x:790:200::dev/null:/bin/false` 的条目。

此账户除了 Samba 之外，任何任何 Unix 服务器都永远不需要使用。通过禁用 shell、主目录和密码，我们保护了账户免受未经授权的使用。

![](img/e6dc042fe420c610acdd193e834a4772_397_0.png)

关于 `/etc/passwd` 文件格式的更多信息，请参见 `passwd(5)` 页。参考以下书籍也可能有所帮助：Robin Burk 的《Unix Unleashed》、《Bill Ball 的《Linux Unleashed》、《Aeleen Frisch 的《Essential System Administration》或 Eve Nemeth 的《Unix Administration Handbook》。

我们现在回到关于如何创建一个主机尝试加入域时使用的机器账户的原始讨论。第一个选项是在客户端加入域之前手动创建账户。除了普通用户账户外，`smbpasswd` 工具还能创建机器账户。

以下命令将在 `smbpasswd` 文件中创建一个机器信任账户条目，主机在加入域时可以使用该账户。

```
root# smbpasswd -a -m "machine name$"
```

此初始条目将有一个已知密码，它是机器小写字母 NetBIOS 名称的 NT 哈希值。例如，如果机器账户的用户名是 `nt-client`，则初始密码将设置为字符串 `nt-client` 的 NT 哈希值。

### Windows NT 4.0/2000 域控制

最好在创建账户后立即将客户端主机加入域，因为在更改密码之前，任何声称是新主机的客户端都可以通过成功猜出密码加入域。

加入 Windows（或 Samba）域的更安全的方法是使用管理账户并在需要时创建机器账户。事实上，Windows 2000 要求使用这种方法。图 22.1 显示了在使用管理账户保护与 PDC 的会话时加入 Windows NT 客户端时使用的对话框（开始 -> 设置 -> 控制面板 -> 网络）。

图 22.1 通过指定管理账户加入域，以保护客户端与 PDC 的会话。

![](img/e6dc042fe420c610acdd193e834a4772_398_0.png)
