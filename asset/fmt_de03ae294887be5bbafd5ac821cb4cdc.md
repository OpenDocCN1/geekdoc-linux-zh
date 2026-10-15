
如你所示，使用该程序时可以实现不同的功能和操作。`root` 或普通用户都可以使用它。当作为普通用户运行时，它允许用户更改存储了 SMB 密码的任何机器上用于 SMB 会话的密码。

在命令行提示符不带任何选项运行时，程序将尝试更改本地机器上当前登录用户的 SMB 密码。程序将响应更改密码的提示，首先要求输入当前密码。要更改密码，`smbpasswd` 将要求输入两次新值。如果条目匹配，则将更改 `smbpasswd` 文件。`smbpasswd` 程序的运行方式与 Unix 密码程序类似。然而，`smbpasswd` 作为客户端应用程序运行并期望与本地运行的 `smbd` 守护进程通信，而 `smbpasswd` 以 `setuid` 身份运行。`smbpasswd` 文件包含加密的 SMB 密码，通常位于 `/usr/local/samba/lib`。如果你想在提示时输入“no password”来创建一个空密码，则该用户的 `smbpasswd` 条目将在 `smbpasswd` 文件中包含字符串“NO PASSWORD”。非 `root` 用户也可以使用 `smbpasswd` 更改其他机器上的 SMB 密码。

最后，当作为 `root` 运行时，`smbpasswd` 程序将向 `smbpasswd` 文件添加、删除或修改用户条目。与普通用户运行 `smbpasswd` 相对比，当超级用户（通常是 `root`）运行它时，不需要运行 `smbd` 守护进程，可以直接对 `smbpasswd` 文件进行更改。

表 11.2 包含了主要 `smbpasswd` 选项的描述。

非 `root` 用户要使用 `smbpasswd` 程序，`smbd` 守护进程必须运行。只有当 Samba 已配置为使用加密密码时，`smbpasswd` 命令才有用。

## 表 11.2 smbpassword 选项

| 选项 | 描述 |
| - | - |
| `-a` | 遵循此选项的用户名将被添加到本地 `smbpassword` 文件中。将创建用户并提示输入新密码。如果是新用户，旧密码将为空，在旧密码处按回车即可。如果用户已存在，可以使用此方法更改密码。在 `smbpassword` 中创建用户时，用户必须存在。 |
| `-d` | 遵循此选项的用户名将在 `smbpasswd` 文件中被禁用。此选项涉及写入 `smbpassword` 文件。如果禁用，通过此用户名进行身份验证的尝试将失败。只有在以 `root` 身份运行时才有效。 |
| `-e` | 遵循此选项的用户名将在 `smbpasswd` 文件中启用。使用此选项可以修改 `smbpassword` 文件中的账户。如果账户已禁用，该选项将不起作用。启用账户后，用户将能够通过 SMB 进行身份验证。只有在以 `root` 身份运行时才有效。 |
| `-O debuglevel` | `debuglevel` 是 0 到 10 的整数；值越大，日志的信息越多。默认值为 0。大于 1 的级别产生错误和严重警告。大于 3 的级别产生开发者有用的信息。 |
| `-n` | 遵循此选项的用户名将在 `smbpasswd` 文件中设置为空。为了允许用户使用空密码登录，Samba 服务器应设置为 `yes`。只有在以 `root` 身份运行时才有效。 |
| `-r remote_machine` | 使用 `-r` 选项时，远程机器名位于选项之后。允许你更改远程服务器上的密码。远程机器必须可以通过网络访问。 |
| `-R name resolve order` | 使用 `-R` 选项时，`R` 选项将指定名称解析服务以及查找 NetBIOS 名称时的使用顺序。选项有 `imhosts`, `hosts`, `wins` 和 `bcast`。它们导致名称解析如下：`Imhosts` 使用 `Imhosts` 文件查找 IP 地址。`hosts` 使用系统 `/etc/hosts` 执行标准的主机到 IP 地址解析。`wins` 使用指定的 WINS 服务器执行名称查询。`bcast` 在 `samba.conf` 参数列出的接口的每个本地子网上执行网络广播。当配合 `smpasswd` 时未定义此参数，将使用 `samba.conf` 文件中定义的名称解析顺序。在没有任何条目的情况下，默认为 `Imhosts`, `hosts` 和 `bcast`。 |
| `-m` | 此选项指定涉及机器账户，并在 Samba 服务器充当 PDC 时使用。只有在以 `root` 身份运行时才有效。 |
| `-j DOMAIN` | 使用此选项时，Samba 服务器将作为域成员加入 Windows 域。随后，该 Samba 服务器将能够向域内的任何域控制器验证用户账户。该 Samba 服务器必须已经在域中创建了机器账户。只有在以 `root` 身份运行运行时才有效。 |
| `-U username` | 当当前登录用户需要远程服务器上的备用用户名时，此选项允许更改远程用户名账户。 |
| `-h` | 与许多 Unix 程序一样，此选项将返回 `smbpasswd` 程序的帮助文本。 |
| `-s` | 此选项允许 `smpasswd` 以静默模式运行而不显示提示。它通常用于包含 `smpasswd` 且不需要用户干预的脚本中。 |

# 使用旧版本的 smbpasswd 文件

2.0.0 之前的旧版本 Samba 使用了不同的 `smbpasswd` 文件格式，该格式不包含账户标志（Account Flags）或最后更改时间（Last Change Time）字段。当前的 Samba 2.0 代码能够使用旧的 `smbpasswd` 文件并添加新用户条目，但可能无法修改旧的条目。随着时间的推移，不同的用户名条目包含了新条目，而有些则没有。旧式的 `smbpasswd` 账户可以通过运行 Samba 发行版中 `/bin` 目录下的脚本 `convert_smbpasswd` 将旧文件转换为新版本。该命令的语法所示：

```bash
cat_old_smbpasswd_file | convert_smbpasswd > new_smbpasswd_file
```

请仔细注意语法，因为 `convert_smbpasswd` 脚本从 `stdin` 读取并输出到 `stdout`。使用前请备份任何 `smbpasswd` 文件。

运行 `convert_smbpasswd` 脚本后，新的 `smbpasswd` 文件将包含新条目。如果条目完整无误，此时应将 `new_smbpasswd_file` 复制并覆盖旧文件。

# 加密密码

`LanManager` 和 Windows NT 宿机的密码加密与 Unix 密码加密类似。在任何情况下，服务器都使用一个包含用户密码哈希值的文件。对用户明文进行操作会创建哈希值。

对于 `LanManager` 主机，这涉及获取用户的明文密码、将其转换为大写，并对该值进行加密。这 16 字节的加密值被称为哈希密码。

Windows NT 加密涉及更高质量的加密，同样产生不可逆的 16 字节加密值。

在操作过程中，对于任何想要使用了加密密码 Samba 服务器并尝试挂载 Samba 驱动器（或使用 Samba 资源）的客户端，任务任务是请求连接并协商客户端和服务器使用的协议。在服务器与客户端之间的交换期间，Samba 服务器生成一个随机值回复客户端，并在发送后存储该值。该值被称为挑战（`challenge`）。每个独立客户端连接的挑战值都是不同的。

在客户端，使用来自 `smbpasswd` 文件的哈希密码对挑战进行加密。产生的值被称为响应（`response`）。

在客户端，在调用 `SMBsessionupX`（用于用户级安全）或 `SMBtconX`（用于共享级安全）的 SMB 调用期间，客户端会将响应值返回给 Samba 服务器。当涉及 NT 协议级别时，上述计算将对用户密码的两个哈希同时进行。

收到响应后，Samba 服务器将挑战值与从哈希密码生成的值进行比较。如果它们匹配，则允许客户端访问。如果不匹配，则拒绝客户端访问。

# 设置密码

要为 Samba 配置加密，请遵循以下步骤：

- 编译并安装 Samba。
- 如果你的系统支持，在 `smb.conf` 的 `[global]` 部分添加 `encrypt=yes` 行。
- 使用 `hostspasswd` 文件定义用户密码。

# 使用 hosts 控制访问

Samba 具有使用 `hosts` 参数控制访问的能力。以下是 `hosts allow` 值的示例：

- `*` 192.168.1.*
- 192.168.1.0/24
- testpc1, laptop

允许来自 NIS 组 "sambabook" 的主机，但拒绝来自路由器的访问：

```text
hosts allow = @sambabook
hosts deny = router1
```

允许来自 `sambabook.com` 域的主机：

```text
hosts allow = @sambabook.com
```
