
### timestamp logs (G)

Samba2.0 默认会对所有日志目添加时间戳。如果你正在调试某个问题，这可能会分散注意力。此参数允许关闭时间戳。

```
默认值：timestamp logs = True
```

```
示例：timestamp logs = False
```

### unix password sync (G)

此布尔参数控制当加密的 `smpasswd` 文件更改时，Samba 是否尝试将 UNIX 密码与 SMB 密码同步。如果设置为 `true`，则 `password program` 参数中指定的密码——允许设置新的 UNIX 密码而无需访问旧 UNIX 密码（因为 SMB 密码已更改，对旧密码的访问已清除，只有新的）。默认情况下设置为 `false`。

另见 `password program`，`password chat`。

```
默认值：unix password sync = False
```

```
示例：unix password sync = True
```

### realmname (G)

此布尔参数在设置时会导致 Samba 提供域名（realm name）。这对于用户具有不同的用户名到用户名的情况有用。

```
默认值：realmname = no
```

```
示例：realmname = yes
```

### update encrypted (G)

此布尔参数在设置时允许用户更新加密后的密码。这对于迁移用户非常有用。

```
默认值：update encrypted = no
```

示例：`update encrypted = yes`

### use hosts (G)

如果此全局参数为真，它指定将读取用户家目录下的 UNIX `.hosts` 文件，以找到允许无密码访问的主机。

注意：使用 `hosts` 可能会导致严重的安全漏洞。因为你正在信任 PC 提供用户名。PC 很容易提供虚假的用户名。我建议只有在你确切知道做什么时才使用 `hosts` 选项。

```
默认值：use hosts = no
```

```
示例：use hosts = yes
```

### user (S)

`username` 的同义词。

### users (S)

`username` 的同义词。

### username (S)

可以在逗号分隔的列表中指定多个用户，在这种情况下，提供的密码将逐个对用户名进行测试（从左到右）。

`username` 行仅在 PC 无法提供自己的用户名时需要。这用于 COREPLUS 协议或你的用户名与 UNIX 用户名不同的情况。在这两种情况下，你可能也可以使用 `server\user` 语法。

在许多情况下，提供的行并不是一个很好的解决方案，因为 Samba 会尝试逐个对 `username` 行中的用户名验证密码。对于密码重复的用户来说，这很慢且是个坏主意。明智地使用此参数可能会导致超时或安全漏洞。

Samba 依赖于底 UNIX 安全。此参数并不限制谁可以登录，它只是向 Samba 服务器提示哪些用户可能同意提供的密码。守护以登录的用户身份运行，因此他们无法做用户启动 telnet 会话时无法做的事情。

要限制特定的用户组，可以使用 `valid users=` 参数。如果任何用户名以 `@` 开头，则首先在 netgroups 列表中查找该名称（如果 Samba 编译了长期支持功能），随后在 UNIX 组数据库中查找并扩展为该组名的用户列表。

如果任何用户名以 `+` 开头，则该名称仅在 UNIX 组数据库中查找，并展开为该名称组中所有用户的列表。

如果任何用户名以 `&` 开头，则该名称仅在 yp netgroups 数据库中查找（如果 Samba 编译时带有 netgroup 支持），并展开为该名称网络组中所有用户的列表。

请注意，搜索组数据库可能需要一些时间，某些客户端可能会在搜索期间超时。

有关此参数如何决定对服务的访问的更多信息，请参阅 `关于用户名/密码验证的注意事项` 章节。

默认：如果是访客服务则使用访客账户，否则使用服务名称。

示例：

```
username = fred
```

```
username = fred, mary, jack, jane, @users, @pcgroup
```

### username level (G)

此选项允许 Samba 尝试 `猜测` 真实的 UNIX 用户名，因为许多 DOS 客户端发送的是大写用户名。Samba 会尝试小写用户名、以及首字母大写的用户名，如果在该 UNIX 机器上未找到该用户名，则失败。

如果将此参数设置为非零，行为将发生变化。该参数是一个数字，指定了在确定 UNIX 用户名时尝试的大写组合数量。数字越大，尝试的组合越多，发现用户名的速度就越慢。当你的 UNIX 机器上有奇怪的用户名（例如 `AstrangeUser`）时，使用此参数。

默认：`username level = 0`
示例：`username level = 5`

### username map (G)

此选项允许你指定一个包含从客户端到服务器用户名映射的文件。这可以用于多个目的。最常见的是是将在 DOS 或 Windows 机器上使用的用户名映射到 UNIX 机器使用的用户名。多个映射可以映射到单个服务器，以便它们更方便地共享文件。

因此，此选项的使用涉及 UNIX 用户名，而不是 Windows（特别是 NT 域）用户名。换句话说，一旦使用此选项映射了名称，Samba 服务器将为内部和外部目的提供该映射后的名称。

此选项与 `domain map` 参数不同，后者维护 UNIX 用户名和 NT 域之间的一一对应映射：具体来说，Samba 服务器会同时映射两个用户名，将 NT 用户名呈现给外部 NT 世界，并在内部使用 UNIX 用户名。

映射文件按行解析。每行左侧应包含单个 UNIX 用户名，后面跟着 `=`，右侧是用户名列表。右侧用户名列表可能包含 `@group` 形式的名称，以便匹配该组中的任何 UNIX 用户名。特殊客户端 `*` 是通配符，匹配任何名称。映射文件的每行长度最多可达 1023 个字符。

文件每行被处理时，会将提供的用户名与 `=` 右侧的每个用户名进行比较。如果提供的名称匹配右侧的任何名称，则将其替换为左侧的名称。然后继续处理下一行。

如果任何行以 `#` 或 `;` 开头，则将其忽略。

如果任何行以 `!` 开头，则如果该行执行了映射，处理将在该行后停止。否则，映射继续并处理每一行。当文件后面有通配符映射行时，使用 `!` 最有用。

例如，将名称 `admin` 或 `administrator` 映射到 UNIX 名称 `root`，您可以使用：

```
root = admin administrator
```

或将 UNIX 组 `system` 中的任何人映射到 UNIX 名称 `sys`，您可以使用：

```
sys = @system
```

您可以在用户名映射文件中拥有尽可能数量的映射。

如果您的系统支持 NIS NETGROUP 选项，会在检查 `/etc/group` 数据库之前检查网络组数据库。

您可以通过名称周围的双引号来映射带有空格的 Windows 用户名。例如：

```
tridge = "Andrew Tridgell"
```

这将 windows 用户名 `Andrew Tridgell` 映射到 unix 用户名 `tridge`。

以下示例将 `mary` 和 `fred` 映射到 unix 用户 `sys`，并将其余部分映射到 `guest`。注意使用 `!` 告诉 Samba 如果在该行找到匹配项时停止处理。

```
!sys = mary fred
```

```
guest = *
```
