
利用这些替换和其他 `smb.conf` 选项，可以做许多极具创造性的事情。

## 名称混淆

Samba 支持名称混淆，以便 DOS 和 Windows 客户端可以使用不符合 8.3 格式的文件。它也可以设置为调整 8.3 格式文件名的字母大小写。

有几个选项控制混淆执行的方式，它们在此分组列出，而不是单独列出。关于默认值，请查看 `testparm` 程序的输出。

所有这些选项都可以为每个服务单独设置（当然也可以全局设置）。

选项包括：

- `case sensitive` = yes/no/auto 控制文件名是否区分大小写。如果不区分，Samba 必须执行文件名搜索并匹配传入的名称。默认设置 `auto` 允许支持区分大小写文件名的客户端（目前是 Linux CIFSVFS 和 3.0.5 及更高版本的 `smbclient`）以逐数据包的方式告知 Samba 服务器，它们希望以区分大小写的方式访问文件系统（以支持 UNIX 区分大小写的语义）。没有 Windows 或 DOS 系统支持区分大小写的文件名，因此为它们将此选项设置为 `auto` 等同于设置为 `no`。默认为 `auto`。

- `default case` = upper/lower 控制新文件名的默认大小写。默认为小写。

- `preserve case` = yes/no 控制新文件是否按客户端传递的大小写创建，还是强制为默认大小写。默认为 `yes`。

- `short preserve case` = yes/no 控制符合 8.3 语法的新文件（即全大写且长度合适）是否以大写创建，还是强制为默认大小写。此选项可与 `preserve case = yes` 一起使用，允许长文件名保留其大小写，而将短文件名转为小写。默认为 `yes`。

默认情况下，Samba 3.0 具有与 Windows NT 服务器相同的语义，即不区分大小写但保留大小写。

## 关于用户名/密码验证的说明

用户连接服务有多种方式。服务器使用以下步骤来确定是否允许连接到指定服务。如果所有步骤都失败，连接请求将被拒绝。然而，如果其中一个步骤成功，后续步骤将不再检查。

如果服务被标记为 `guest only = yes` 且服务器以共享级安全性运行（`security = share`），则跳过步骤 1 到 5。

- 1. 如果客户端传递了用户名/密码对，且该用户名/密码对由 UNIX 系统的密码程序验证，则以此用户名建立连接。这包括使用 `\server\service%username` 方法传递用户名的情况。

- 2. 如果客户端此前已向系统注册过用户名，现在提供了该用户名的正确密码，则允许连接。

- 3. 客户端的 NetBIOS 名称和任何先前使用的用户名将与提供的密码进行检查。如果匹配，则以对应用户身份允许连接。

- 4. 如果客户端此前已验证了用户名/密码对，且客户端传递了验证令牌，则使用该用户名。

- 5. 如果 `smb.conf` 文件中为服务提供了 `user =` 字段，且客户端提供了密码，并且该密码与 `user =` 字段中的某个用户名匹配（根据 UNIX 系统的密码检查），则以 `user =` 行中的用户名建立连接。如果 `user =` 列表中的某个用户名以 `@` 开头，则该名称扩展为同名组中的名称列表。

- 6. 如果服务是来宾服务，则无论提供的密码如何，都以服务中指定的 `guest account =` 中给出的用户名建立连接。

## 每个参数的解释

### `abort shutdown script` (G)

默认值：*无默认值*

*示例：* `abort shutdown script = /sbin/shutdown -c`

这是一个完整路径名称，指向由 `smbd(8)` 调用的脚本，该脚本应停止由 `shutdown script` 发起的关机过程。

如果连接的用户拥有 `SeRemoteShutdownPrivilege` 权限，此命令将作为用户运行。

### `acl compatibility` (S)

默认值：*`acl compatibility = Autowin2k`*

*示例：* `acl compatibility = win2k`

此参数指定应与哪个操作系统 ACL 语义兼容。可能的值包括用于 Windows NT 4 的 `nt4`、用于 Windows 2000 及更高版本的 `win2k` 以及 `auto`。如果你指定 `auto`，此参数的值将基于客户端的版本。没有理由将此参数从默认值更改。

仅在使用 Windows NT 域管理工具进行安装时才有用。脚本可以自由地创建一个任意名称的组，以绕过 unix 组名称限制。在这种情况下，脚本必须将创建的组的数字 gid 打印到标准输出（stdout）。

### `add machine script` (G)

默认值：无默认值

示例：`add machine script = /usr/sbin/adduser -n -g machines -c Machine -d /var/lib/nobody -s /bin/false %u`

这是脚本的完整路径名，当使用管理员用户名和密码方法将机器添加到其域时，将由 `smbd(8)` 执行。

仅当使用与 Unix uid 方法关联的用户 sam 后端来计算 RID（例如 `smbpasswd`）时才需要此选项。此选项仅在 Samba 3.0 中可用。

### `addprinter command` (G)

默认值：无默认值

示例：`addprinter command = /usr/bin/addprinter`

随着 Samba 2.2 引入了基于 MS-RPC 的 Windows NT/2000 客户端打印支持，“添加打印机向导”（APW）图标现在也显示在分享列表中的“Printers...”文件夹里。APW 允许远程向 Samba 或 Windows NT/2000 打印服务器添加打印机。

对于 Samba 主机而言，这意味着必须将打印机物理添加到底层打印系统中。`add printer command` 定义了一个将要运行的脚本，该脚本将执行将打印机添加到打印系统以及将相应的服务定义添加到 `smb.conf` 文件以使其能被 `smbd(8)` 共享所必需的操作。

`addprinter command` 会自动按以下顺序接收参数：

- 打印机名称
- 共享名称
- 端口名称
- 驱动程序名称
- 位置
- Windows 9x 驱动程序位置

所有参数都来自 Windows NT/2000 客户端发送的 `PRINTER_INFO 2` 结构，但有一个例外。“Windows 9x 驱动程序位置”参数仅出于向后兼容性的目的而包含在内。结构中的其余字段是根据对 APW 问题的回答生成的。

一旦执行了 `addprinter command`，`smbd` 将重新解析 `smb.conf` 文件，以确定由 APW 定义的共享是否存在。如果共享名称仍然无效，则 `smbd` 将向客户端返回 `ACCESS_DENIED` 错误。“add printer command”程序可以输出一行文本，Samba 会将此文本设置为新打印机连接的端口。如果未输出此行，Samba 不会重新加载其打印机共享。

### `add share command` (G)

默认值：无默认值

示例：`add_share_command = /usr/local/bin/addshare`

Samba 2.2.0 引入了通过 Windows NT 4.0 服务器管理器动态添加和删除共享的功能。`add_share_command` 用于定义一个外部程序或脚本，该程序或脚本将向 `smb.conf` 添加新的服务定义。为了成功执行 `add_share_command`，`smbd` 要求管理员必须使用 root 账户（即 `uid == 0`）连接。

执行时，`smbd` 会自动调用 `add_share_command` 并传递四个参数。

- `configFile` - 全局 `smb.conf` 文件的位置。
- `shareName` - 新共享的名称。
- `pathName` - 磁盘上现有目录的路径。
- `comment` - 与新共享关联的注释字符串。

此参数仅用于添加文件共享。若要添加打印机共享，请参阅 `addprinter command`。

### `add user script` (G)

默认值：无默认值

示例：`add user script = /usr/local/samba/bin/add_user %u`

这是脚本的完整路径名，将在下文描述的特殊情况下由 `smbd(8)` 以 ROOT 身份运行。

通常，Samba 服务器要求为访问此服务器上文件的所有用户创建 UNIX 用户。对于使用 Windows NT 账户数据库作为其主要用户数据库的网站来说，创建这些用户并保持用户列表与 Windows NT PDC 同步是一项艰巨的任务。此选项允许 `smbd` 在用户访问 Samba 服务器时按需创建所需的 UNIX 用户。

要使用此选项，`smbd(8)` 不能设置为 `security = share`，且必须将 `add user script` 设置为脚本的完整路径名，该脚本将在给定一个扩展为要创建的 UNIX 用户名的 `%u` 参数的情况下创建 UNIX 用户。
