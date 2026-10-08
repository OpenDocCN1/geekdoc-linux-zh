
远程加入的客户端支持实现在 `net` 命令中，这些命令有：

- `dom join` - 将远程计算机加入域。
- `dom unjoin` - 将远程计算机退出域。
- `dom renamecomputer` - 重命名已加入域的远程计算机。

### `DOM JOIN domain=DOMAIN ou=OU=ACCOUNT password=PASSWORD reboot`

将计算机加入域。此命令支持以下额外参数：

- `DOMAIN` 可以是 NetBIOS 域名（也称为短域名）或 Active Directory 域的 DNS 域名。在 Windows 中，还可以控制使用哪个域控制器。这可以通过使用 `\` 分隔符附加 DC 名称来实现。例如：`MYDOM\MYDC`。`DOMAIN` 参数不能为 NULL。
- `OU` 可以是一个 RFC 1779 LDAP DN，例如 `ou=mymachine,cn=Users,dc=example,dc=com`，以便在非默认 LDAP 容器中创建机器帐户。此可选参数仅在加入活动域（Active Domains）时支持。
- `ACCOUNT` 定义了用于将机器加入域的域账户。该域账户需要足够的权限来加入机器。
- `PASSWORD` 定义了由 `ACCOUNT` 指定域账户的密码。
- `REBOOT` 是可选参数，可以设置为在成功加入域后重启远程机器。

注意，你还需要使用标准参数来连接并验证你想要加入的远程机器。这些额外参数包括：`-S computer` 和 `-U user`。

示例：`net dom join -S xp -U XP,administrator*secret domain=MYDOM account=MYDOM\administrator password=topsecret reboot`。

此示例将使用密码 `secret` 以本地管理员身份连接到名为 `XP` 的计算机，并将该计算机加入名为 `MYDOM` 的域，管理员账户和密码为 `secret`。加入成功后，计算机将重启。

### `DOM UNJOIN account=ACCOUNT password=PASSWORD reboot`

将计算机退出域。此命令支持以下额外参数：

- `ACCOUNT` 定义了用于将机器退出域的域账户。该域账户需要足够的权限来加入机器。
- `PASSWORD` 定义了由 `ACCOUNT` 指定域账户的密码。
- `REBOOT` 是可选参数，可以设置为在成功退出域后重启远程机器。

注意，你还需要使用标准参数来连接并验证你想要退出的远程机器。这些额外参数包括：`-S computer` 和 `-U user`。

示例：`net dom unjoin -S xp -U XP,administrator*secret domain=MYDOM account=MYDOM\administrator password=topsecret reboot`。

这将使用密码 `secret` 以本地管理员身份连接到名为 `XP` 的计算机，并使用 `MYDOM` 管理员账户和密码 `secret` 将计算机退出域。退出成功后，计算机将重启。

### `DOM RENAMECOMPUTER newname=NEWNAME ACCOUNT=PASSWORD reboot`

重命名已加入域的计算机。此命令支持以下额外参数：

- `NEWNAME` 定义机器的新名称。
- `ACCOUNT` 定义了用于将机器加入域的域账户。该域账户需要足够的权限来加入机器。
- `PASSWORD` 定义了由 `ACCOUNT` 指定域账户的密码。
- `REBOOT` 是可选参数，可以设置为在成功加入域后重启远程机器。

注意，你还需要使用标准参数来连接并验证你想要加入域的远程机器。这些额外参数包括：`-S computer` 和 `-U user`。

示例：`net dom join -S xp -U XP,administrator*secret domain=MYDOM account=MYDOM\administrator password=topsecret reboot`。

这将使用密码 `secret` 以本地管理员身份连接到名为 `XP` 的计算机，并将该计算机加入名为 `MYDOM` 的域，管理员账户和密码为 `secret`。加入成功后，计算机将重启。

## `G_LOCK`

管理全局锁。

### `G_LOCK timeout command`

在全局锁下执行 shell 命令。这可能用于定义 shell 命令的执行顺序。锁定信息存储在 `g_lock.tdb` 文件。在运行 CTDB 的设置中，锁定信息将在所有节点可用。

- `LOCKNAME` 定义全局锁的名称。
- `TIMEOUT` 定义超时时间。
- `COMMAND` 定义要执行的 shell 命令。

### `G_LOCK LOCKS`

列出所有现有 `lockname` 的列表。

### `G_LOCK DUMP lockname`

转储特定全局锁的锁定表。

## `HELP [COMMAND]`

提供指定命令的使用信息。

## `VERSION`

本手页对于 Samba 套件版本 3 是完整的。

### AUTHOR

原始 Samba 及相关工具由 Andrew Tridjell 创建。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

`net` 手由 Jelmer Vernooij 编写。
