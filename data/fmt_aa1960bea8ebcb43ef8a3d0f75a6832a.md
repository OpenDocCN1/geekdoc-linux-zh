
没有人想要增加维护密码服务的复杂性，或降低我们想要实施的安全性。遗憾的是，在密码方面，UNIX 和 Windows 遵循的并不是相同的规则。首先，它们采用单向算法来加密密码。LAN Manager 服务器使用未加密的密码，Windows 使用 Unicode 版本密码的 NT 和 MD4 哈希值，并使用修改后的 DES 算法通过随机盐值（`salt`）对密码进行加密（此处原文此处应为哈希处理）。为了让情况变得更加复杂，较旧的 Windows 系统在会话设置期间显示明文密码。幸运的是，Samba 许多选项来处理 UNIX 和 Windows 密码之间的差异。

## 明文密码

假设您的网络免受密码嗅探（谁的网络是绝对安全的呢？），在 SMB 设置时授权明文密码可能是在混合 UNIX 和 Windows 环境中管理密码最简单的方法。相反，在安全性方面，这是糟糕的方法。客户端呈现给 Samba 的密码将使用标准的 UNIX 身份验证方法根据 UNIX 密码文件进行验证：

```
encrypt passwords = false
security = <user or share>
```

除了网络传输中明文密码相关的安全问题外，您可能还会遇到如 Windows for Workgroups 等类客户端的问题，它们在将密码发送到服务器之前会对大写进行处理。与上一节关于加密用户名的部分类似，Samba 提供了一个密码级参数，如果大写密码检查失败，该参数将指导服务器尝试不同的大小写字母组合。该参数接受一个数值，表示在放弃之前尝试的组合数量。最大值决定了在验证密码时将尝试哪些组合。值 '0' 则指引服务器在拒绝访问之前检查密码的所有大写和全小写情况。

```
password level = <integer value>
```

Windows NT4 服务包 3：Windows 95 更新版本；Windows 98 以及 Windows 2000 均通过 SMB 会话设置协商加密密码。要恢复对明文密码的支持，请安装 Samba 分发版 `/docs` 目录下提供的适当注册表更新（表 7.1），或使用 `regedit` 直接编辑注册表（示例 7.3）。

### 表 7.1 Windows 明文密码注册表更新文件

| 路径 |
| :--- |
| `/.samba <version>/docs/NT4_PlainPassword.zip` |
| `/.samba <version>/docs/Win2000_PlainPassword.zip` |
| `/.samba <version>/docs/Win95_PlainPassword.zip` |
| `/.samba <version>/docs/Win98_PlainPassword.zip` |

### 示例 7.3 支持明文密码的注册表项

#### Windows NT

```
Find:HKEY_LOCAL_MACHINE\system\CurrentControlSet
\Services\rdr\parameters
Add: EnablePlainTextPassword, dword: 00000001
```

#### Windows 9x

```
Find:HKEY_LOCAL_MACHINE\System\CurrentControlSet
\Services\Vxd\VNETSUP
Rename: "New Value #1" to "EnablePlainTextPassword", dword:00000001
```

## 加密密码

通过在 Samba 中启用 NTLM 加密密码支持，可以在 SMB 会话设置期间消除明文密码选项。该功能通过消除在网络上窃听密码的可能性提高了整体网络安全性；然而，它增加了维护和同步 UNIX 和 NTLM 密码的复杂性。启用加密密码需要维护额外的密码文件，并且必须与标准的 UNIX 密码维护活动结合进行。

通过将 `encrypt password` 参数设置为 `true` 来启用 NTLM 加密密码选项，创建一个 Samba `smpasswd` 文件的实例，其中包含每个用户的条目。通常执行此操作简单的方法是将每个加密或 NIS 密码文件作为 Samba 分发版中提供的 `mkmpasswd.sh` 壳脚本的输入。该过程描述于示例 7.4。

```
encrypt passwords = <false>
```

### 示例 7.4 启用 Samba 加密密码

```
encrypt passwords = true
```

NTLM 加密密码选项通过将 `encrypt password` 参数设置为 `true` 来启用，创建一个 Samba `smpasswd` 文件的实例，其中包含每个用户的条目。通常执行此操作简单的方法是将每个加密或 NIS 密码文件作为 Samba 分发版中提供的 `mkmpasswd.sh` 壳脚本的输入。该过程描述于示例 7.4（此处原文重复且逻辑混乱，已根据语境调整）。

（注：原文在示例 7.4 之后存在大量重复和逻辑循环，翻译时已根据技术核心逻辑进行了整合）

```
security = user
encrypt passwords = no
update encrypted = yes
```

在会话期间，Samba 使用 UNIX 认证过程根据 `/etc/passwd` 验证客户端的明文密码。验证成功后，Samba 将明文密码加密为 LAN Manager 和 NT 哈希格式，并将其存储在 `smbpasswd` 文件中。注意，用户必须在 `smbpasswd` 文件中已存在条目。`smbpasswd` 文件中的任何额外密码信息将被新密码覆盖。一旦完成加密加密密码的过程，请关闭 `update encrypted` 参数并开启 `encrypt passwords` 参数：

```
encrypt passwords = yes
update encrypted = no
```

# 密码同步

此时，你已经完成了服务器上 Samba 加密密码支持的设置，包括 UNIX 的 `/etc/passwd` 和 Samba 的 `/usr/local/samba/private/smbpasswd`。你可能更喜欢一种自动方法来保持这两个文件的同步。对其中一个密码的更新会自动反映在另一个文件中。Samba 可以为你处理该问题的任何一方。通过使用 `unix` 附加认证程序，Samba 每当接收到 `smbpasswd` 更改命令时就会更新 UNIX 的 `/etc/passwd`，并且密码聊天文本需要根据你特定的 UNIX 操作系统进行定制。对于 UNIX 老手来说，这类似于为 UUOCP 连接设置登录聊天。在正常运行期间请不要开启此选项，因为这会让密码以明文形式显示。

```
passwd chat = <true, false>
```

如果你想在调用 UNIX 命令时更新 `smbpasswd`，则需要构建一些内容。这可能是复杂的。你可能会在密码和 `smbpasswd` 之间导致一个更新循环。如果你愿意跳过这个编程练习，Stephen Langevin 已经通过 `pam_samba` 模块完成了部分工作。Samba 通过名为可插拔认证模块 (`PAM`) 的定义良好的 API 和共享库接口添加附加认证方法。我们将在“认证方法”部分详细详细介绍 PAM。`pam_smbpass` 允许 UNIX 用户针对 LM 服务进行身份验证，并在用户更改账户 LM 时更新两个密码文件。注意，此密码将仅在本地 Samba 服务器上有效，因此它不用于维护分布式环境中的远程文件。Stephen 的 `pam_smbpass` 可从 `ftp://ftp.netplex.net/pub/` 获取。

### 示例 7.7 同步 Samba smbpasswd 和 UNIX 密码更新

```
encrypt passwords = yes
security = user
unix password sync = yes
```

```
passwd program = /usr/bin/passwd %u
passwd chat = *password* %n\n *password* %n\n *successful*
```

你可能对定期将你的 NT SAM 数据库与 `smpasswd` 程序同步感兴趣。Samba 团队的 Jeremy Alison 创建了一项名为 `pwdump.exe` 的工具，它可以将 SAM 账户的副本导出为 `smpasswd` 格式。该程序必须在 NT 的管理员帐户上运行。`pwdump.exe` 工具可在 Samba 发行存储中获取。

```
pwdump > smpasswd
```

# 域认证

与其让 Samba 执行维护密码空间的工作，你可以将其交给远程服务器。使用 `password server` 参数识别远程服务器。与远程服务器的交互可以是用户级认证或域级认证模式，分别由 `server` 或 `domain` 的 `security` 值指定。域级认证提供了一些你在选择远程认证方法时可能需要考虑的额外功能。在域级认证下，不需要复制 NTLM 和 UNIX 账户。Samba 服务器还可以参与域信任关系。
