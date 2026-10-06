
$ `/etc/samba/` `cat` `/lmhosts`

# 此文件提供的功能与 lmhosts 文件为 Windows

# 提供的功能相同，它是将 netbios 名称映射到 ip 地址的另一种方法。

# 更多信息请参阅 smb.conf 手页中的

# 'resolve order' 章节。

127.0.0.1        localhost

`/etc/samba/` #

```

![](img/9a8db5c8d556a70e5a1096951da47eec_261_0.png)

在没有 DNS 服务器的情况下，可以使用 `lmhosts` 提供简单的 NetBIOS 名称解析。像 `/etc/hosts` 一样，我们通常不怎么频繁使用 `lmhosts`。与 `/etc/hosts` 文件相关的所有弱点都适用于 `/etc/samba/lmhosts` 文件。在你的 Linux 服务器上使用 `nmbd` 守护进程可以提供一个更健壮的 NetBIOS 名称解析系统。

## smbfstab

`/etc/samba/smbfstab` 文件用于在你的系统上配置 Samba 客户端。当仅将系统配置为 Samba 服务器时，不需要它。`smbfstab` 文件用于在系统启动时自动挂载远程系统上的共享目录。图 6.12 显示了一个示例 `smbfstab` 文件。

要实现这一点，你需要指定共享项、挂载点、类型（`cifs` 或 `smbfs`）以及各种选项，例如用于验证的用户名和密码。我们需要查看的下一个文件是 `smbpasswd`。

## smbpasswd

`/etc/samba/smbpasswd` 文件是在设置 Samba 服务器时必须注意的关键文件。除了 `smbpasswd` 之外，你可能不需要对前面的配置文件做什么。

## 图 6.12

`/etc/samba/smbfstab`

```
fstab:/etc/samba/ cat /smhosts

# 此文件用于在系统启动时自动挂载

# 系统的共享目录。你指定共享项、挂载

# 点、类型（cifs 或 smbfs）以及各种选项，

# 例如用于验证的用户名和密码。

fstab:/etc/samba/ #
```

## smbususers

`/etc/samba/smusers` 文件用于将用户名映射到服务器。例如，图 6.13 显示了一个 `smusers` 文件。

在 `smusers` 文件中，你使用以下语法：

`Samba服务器用户名 = 客户端用户名`

## 图 6.13

`/etc/samba/smusers`

```
fs:/etc/samba/ cat /smusers

# 此文件允许你将客户端用户名映射

# 到服务器。该用户名为 smuser。

root administrator admin

fs:/etc/samba/ #
```

## smb.conf

`/etc/samba/smb.conf` 是 Samba 配置的核心。你的大部分配置将在此文件中完成。它分为两个部分：全局选项和共享资源。`[global]` 部分用于定义全局范围的选项。共享资源部分用于定义 SMB 客户端可以的服务器资源。默认 `smb.conf` 文件的部分如图 6.14 所示。

## 图 6.14

`/etc/samba/smb.conf`

```
fs:/etc/samba/ cat /smb.conf

# smb.conf 是 Samba 的主配置文件。你可以在

# /usr/share/doc/packages/samba/examples/smb.conf

# 找到一个带注释的版本 SUSE

# 日期:2004-06-30

[global]

group = TUX-MEM

printing = cups

printname = cups

printname case = 750

caps options = none

printer admin = admin, root, administrator

username map = /etc/samba/smusers

may point to = local users

login path = \%s/%profile

login home = %s

[homes]

comment = Home Directories

valid users = @

browsable = No

read only = No

inherit permissions = Yes

[profiles]

More = =
```

让我们先来看 `[global]` 节中的参数。

## smb.conf 的 [GLOBAL] 节
在 `smb.conf` 的 `[global]` 节中实际上有很多可以使用的参数，但其中大多数你可能永远用不到。如果你想查看所有可能的参数的列表，请参阅 `smb.conf` 页面。对于 CLE 认证，你只需要熟悉少数几个参数。这些包括：

- `workgroup`—此参数定义了 Samba 服务器将参与的工作组或域的名称。
- `netbios name`—此参数用于手动设置 Samba 服务器的 NetBIOS 名称。如果你没有在 `smb.conf` 中包含此参数，则 NetBIOS 名称将默认为服务器的主机名。
- `server string`—此参数用于为 Samba 服务器提供描述，该描述将在 Windows 客户端的“我的网络位置”中显示。此文本字符串可以包含你想要的任何值。如果你没有在 `smb.conf` 中包含此参数，`smbd` 将默为 `Samba samba_version_number`，如图 6.15 所示。

图 6.15
`server string` 参数的默认值。
![](img/9a8db5c8d556a70e5a1096951da47eec_264_0.png)

- `os level`—此参数用于配置 Samba 服务器在选举为主主浏览器（master browser）时的表现。如果你不包含此参数，Samba 服务器将被分配为 20 的 `os level`，并将胜过工作组或域中除 PDC 或 BDC 以外的任何 Windows 系统。如果你想确保 Samba 服务器在浏览器选举中胜过任何其他系统，请包含此参数并将其设置为 65。
- `encrypt passwords`—此参数用于配置 `smbd` 使用加密密码。这应该始终设置为 `on`，因为自 Windows 98 以来每个版本的 Windows 都需要加密密码。
- `domain logons`—此参数用于将 Samba 配置为域控制器。当设置为 `yes` 时，Samba 服务器运行 `logeton` 服务，允许用户对域进行身份验证。

# 第 6 章：为 SLES 9 上的 Windows 客户端配置文件和服务

- `domain master`—在配置 PDC 时将此参数设置为 `yes`；在配置服务器作为 BDC 时将其设置为 `no`。
- `preferred master`—此参数将 Samba 服务器配置为工作组或域的首选主浏览器。如果设置为 `yes`，则在服务启动时将强制选举。如果 `domain master` 设置为 `yes`，则 Samba 服务器将赢得选举。
- `passdb backend`—此参数用于识别 Samba 用户账户的存储位置。
- `wins server`—如果你的网络上已经运行了 WINS 服务器，请在你的 `smb.conf` 文件中包含此参数，并将其值设置为 WINS 服务器的 IP 地址。
- `wins support`—如果你的网络中已经没有 WINS 服务器，请使用此参数通过将其值设置为 `yes` 来将 `nmbd` 运行为 WINS 服务器。此参数的默认值为 `no`。
- `loads printers`—这是一个非常有用的参数。如果你在 `smb.conf` 文件中包含此参数，则 `/etc/printcap` 中定义的所有打印机将自动共享给 SMB 客户端使用。

### 注意
还记得第 5 章中我们说 Windows 桌面系统不支持 CUPS 打印机吗？这里是我们的答案！通过使用 Samba，我们可以将 CUPS 打印机共享给 Windows SMB 客户端。Samba 太棒了！

- `security`—这是一个经常被新 Samba 管理员忽略的关键参数。此参数决定了 `smbd` 如何验证用户身份。有五种可能的值：

- `user`—身份验证按用户处理。此值通常用于网络中的工作组。当 `security` 参数设置为 `user` 时，SMB 客户端必须先使用有效的用户名和密码向 Samba 服务器进行身份验证验证，然后才允许访问服务器上的共享资源。如果 `smb.conf` 中没有包含 `security` 参数，则这是默认行为。
- `share`—身份验证按共享项处理。此值通常用于网络中的工作组。当 `security` 参数设置为 `share` 时，系统中的每个共享项都分配了其独立的密码。客户端系统可以通过提供共享项的密码来访问该共享。系统不会检查用户名。
- `domain`—此值通常用于网络中的域。当设置为 `domain` 时，所有的身份验证过程都由远程 PDC 或 BDC 处理。
- `server`—此值通常用于工作组。当设置为 `server` 时，所有的身份验证请求都将转发到另一个 SMB 服务器。这可能是另一个 Samba 服务器，也可能是一个 Windows 系统。
- `ads`—当 Samba 服务器是 Active Directory（活动目录）域的成员时使用此值。当设置为 `ads` 时，所有的身份验证过程将由 AD 域控制器处理。
- `printing`—此参数定义了 Samba 管理的服务器打印系统类型。可能的值有 `CUPS`, `LPRNG`, `PLP`, `SYSV`, `AIX`, `HPUX`, `QNX`, `SOFTQ` 和 `BSD`。大多数情况下，你可能会使用 `CUPS` 进行打印。
- `username map`—此参数允许你指定用于将 SMB 客户端用户名映射到本地系统用户名的文件。用于此目的的默认文件是 `/etc/samba/smbus`。

你需要了解的下一个部分是 `[homes]`。让我们来看看它。

## smb.conf 的 [HOMES] 节
如果你参考图 6.15，你会看到 `smb.conf` 中有一个名为 `[homes]` 的节。该节设计用于自动共享用户的家目录。当用户验证到 Samba 服务器时，家目录将被共享，如图 6.16 所示。

图 6.16
共享的家目录。
![](img/9a8db5c8d556a70e5a1096951da47eec_264_0.png)

除了这些共享目录外，你还可以使用 `smb.conf` 定义你自己的共享目录。我们将看看如何操作。

# 第 6 章：为 SLES 9 上的 Windows 客户端配置文件和服务

## 创建共享目录
你可以共享文件系统中的任何目录。要实现这一点，你需要在 `smb.conf` 文件中添加一个节，语法如下：

```
[share_name]

  comment = share_description

  path = path to shared directory

  other smb_options
```

`share_name` 参数指定共享的名称。然后可以使用以下参数配置共享项：

- `comment`—此参数用于提供共享描述。
- `path`—此参数指定共享目录的完整路径。确保你配置了目录权限。

注意
`path` 参数是必须的。列出的是可选的。

- `browseable`—此参数指定该共享项是否可以在“我的网络位置”中被浏览。如果你不包含此参数，则假设默认值为 `yes`。
- `read only`—如果设置为 `yes`（默认值），则不允许用户在共享目录中创建或编辑文件。
- `writeable`—此参数基本上与 `read-only` 相同，只是方向相反。如果设置为 `yes`，则允许用户在共享目录中创建或编辑文件（假设文件系统权限允许）。
- `public`—当设置为 `yes` 时，此参数允许用户在不提供密码的情况下连接共享目录。因此，用户将以 `nobody` 系统账户身份连接。这仅用于共享级安全。此参数的默认值为 `no`。
- `valid users`—此参数指定允许访问共享项的用户。你可以用逗号分隔多个用户。你也可以通过输入 `@group_name` 来指定组。如果你没有在 `smb.conf` 中包含此参数，则任何人都可以访问该共享项。
- `guest ok`—当设置为 `yes` 时，此参数指定不需要密码即可访问共享资源的用户。默认值为 `no`。
- `printable`—当设置为 `yes` 时，该参数允许客户端系统在共享目录中创建打印缓存文件。默认值为 `no`。

与 `smb.conf` 文件的 `[global]` 部分一样，在配置共享时，还有数以万计的其它参数可以使用——比我们在这里能涵盖的要多得多。再次，其中大多数都是你可能永远不会用到的参数。之前列出的是 Linux 系统文件。要执行操作，你需要使用你日常可能用到的参数向 `smb.conf` 文件中添加一个节（section）。

配置好 `smb.conf` 文件后，你需要完成的下一个任务是为你的用户启用 Samba 账户。

## 启用 Samba 用户账户

如前所述，samba 不使用 `/etc/samba/passwd` 文件来存储用户账户。相反，它使用 `/etc/samba/smbpasswd` 文件。默认情况下，`smbpasswd` 是空的，如 6.17 所示。

图 6.17

一个空的 `smbpasswd` 文件。

```
fsl/etc/samba # cat .../smbpasswd

# This file is the authentication source for Samba if 'passdb backend' is set

# to 'smbpasswd' and encrypt passwords' is 'Yes' in the [global] section of

# /etc/samba/smb.conf

# See section 'passdb backend' and 'encrypt passwords' in the manual page of

# smb conf for more information.

fsl/etc/samba #█
```

提示

除了 `smbpasswd` 文件外，Samba 服务器还可以使用 LDAP 目录或 MySQL 数据库作为用户存储器。对于 CLE，你不需要知道如何这样做，因此我们在这里不介绍它。但是，如果你想尝试一下，可以在 YaST 的“身份”（Identity）选项卡中进行。选择“高级设置”（Advanced Settings）、“用户身份验证源”（User Authentication Sources）、“添加”（Add）。在弹出的对话框中，你可以选择用于 Samba 用户账户的数据库。

如何填充 `smbpasswd` 文件？你使用 `smbpasswd` 工具。要执行此操作，请完成以下步骤：

- 1. 打开终端会话。
- 2. 在 shell 提示符处切换到 root。

# 第 6 章：为 SLES 9  Windows 客户端配置文件和打印服务

提示

如果你以 root以外的任何用户运行 `smbpasswd`，它将仅对当前登录的用户账户执行操作。如果你想管理除你自己以外的账户，必须拥有 root 权限。

- 3. 在 shell 提示符处，输入 `smbpasswd -a username`。示例如图 6.18 所示。

图 6.18

启用 Samba 用户账户。

![](img/9a8db5c8d556a70e5a1096951da47eec_269_0.png)

- 4. 提示时，为 SMB 用户账户输入密码。

提示

关于是否应该为 SMB 用户账户和系统账户使用相同的密码，存在一些争议。我喜欢使用相同的密码，这样我就不需要维护两套独立的密码。然而，那些比我稍微有点安全偏执症的人坚持要求使用不同的密码。我让你由自己决定。

- 5. 提示时，重新输入密码。系统会提示用户账户已添加，如图 6.19 所示。

图 6.19

一个已启用的 Samba 账户。

![](img/9a8db5c8d556a70e5a1096951da47eec_269_1.png)

该用户账户现在位于 `/etc/samba/smbpasswd` 文件中，如图 6.20 所示。

## 图 6.20

`smbpass.sw` 中的 Samba 用户账户。

```
fslet:/etc/samba # passpasswd -a dcoughan

New SMB password

Bridges one SMB password:

Hidden user dcoughan

fslet:/etc/samba # passdb backend for Samba if 'passdb backend' is set

# This file is the authentication source for passdb backend

# to 'passdb' and encrypt passwords' is 'Yes' (in the global) section of

# /etc/samba/smb.conf

# See section 'passdb backend' and 'encrypt passwords' in the manual page of

# smb.conf for more information.

dcoughan 1086:5D2512B808D3B4B851404EE:19931CE5B8FCBDA84551A9FFB84947

SB(i)

fslet:/etc/samba # 1LCT-42AWN65
