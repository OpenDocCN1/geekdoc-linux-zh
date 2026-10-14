
# usermod -D 1

`Local = 1`

`Distributed = 0`

`Minimum User ID = 12`

`Next User ID = 200`

`Maximum User ID = 4294967293`

`Duplicate User ID = 0`

`Used Hashed Database = 0`

`Max Groups Per User = 32`

`Base Home Directory = /usr/user 2`

`Administrative Lock = 1`

`Primary Group = users`

`Skeleton Directory = /usr/skel`

`Shell = /bin/sh`

`Synchronized UNIX/PC Accts = 0`

`PC Minimum Password Length = 0`

`PC Minimum Password Age = 0`

`PC Maximum Password Age = 42`

`PC Password Uniqueness = 0`

`PC Force Logout After = Never`

```
```

# usermod -D pc_synchronize=1 pc_password_uniqueness=1 \
pc_max_password_age=60 3

# usermod -D

```

# 示例 7–1：使用 usermod 更改默认环境变量（续）

```

`Synchronized UNIX/PC Accts = 1`

`PC Minimum Password Demand = 0`

`PC Minimum Password Age = 4`

`PC Maximum Password Age = 60`

`PC Password Uniqueness = 1`

`PC Force Logoff After = Never`

```

- 1 此命令显示当前的默认环境变量。
- 2 `usermod` 命令的输出是环境变量的默认值列表。当您创建账户时，这些值将分配给新账户。例如，所有新账户都创建在 `/user` 的基础主目录下。
- 3 此命令为三个仅适用于 Windows NT 账户的环境变量指定了新的默认值。
- 4 此（截断的）列表显示了环境变量的新默认值，如下：

`pc_synchronize=1`

当 ASU 运行时，会创建关联的 Windows NT 域和 UNIX 账户

```
pc_passwd_uniqueness=1
```

强制对密码进行唯一性验证

```
pc_max_passwd_age=60
```

指定用户在必须更改密码之前可以经过的最大天数

使用 `groupmod -D` 命令来设置创建新组的默认环境变量。当您创建新账户时，您可以为环境变量指定备选值以覆盖默认值。更多信息请参阅 `useradd(8)`、`usermod(8)` 和 `userdel(8)`。

在命令提示符处，您可以在每个命令后输入 `-h` 以显示显示命令选项的帮助屏幕。在 ASU 域用户管理器中，当您编辑默认策略时，会执行类似的任务，该策略为新创建的账户建立了类似的默认环境变量。

您无法仅使用 ASU 账户管理工具对 UNIX 账户执行操作，无法使用 UNIX 工具对仅存在于 Windows NT 域的账户执行操作。以下章节提供了当 ASU 运行以及您管理同步账户时，UNIX 和 ASU 账户管理工具的行为信息。

## 7.6.1 管理同步账户

如果您已设置了 ASU 并配置了同步账户区域，账户管理工具中的功能将自动启用。以下章节描述了这些功能在不同账户管理工具中的显示方式。

锁文件可防止您使用两个工具（或同一工具的两个实例）。这种情况在具有许多管理员管理许多账户的大型安装中很容易发生。该锁文件位于 `/.AM_is_running`。如果锁文件存在，则只有一个进程可以访问与用户组数据相关的系统文件。如果您尝试调用任何 UNIX 账户管理工具的第二个实例，错误消息将通知您文件已被锁定。

当使用 ASU 工具时，ASU 会检测到锁文件的存在且无法创建关联的 UNIX 账户。它仅创建 Windows NT 域账户。不会显示锁文件错误消息，您也不会收到关联账户已创建的确认。使用 ASU 工具时，请验证 `/etc/password` 文件的内容。

### 7.6.1.1 使用 SysMan 账户和组选项

SysMan 账户的用户界面在 ASU 运行时不会显示任何视觉差异。如果启用了同步账户，窗口和屏幕将没有区别。但应注意以下行为变化：

- 添加用户
在作为账户创建的一部分将账户持有人分配给某个组时（主组），您可以从几个 DOS----- 组中进行选择。

如果如示例 7–1 描述所示启用了关联的 Windows NT 账户创建，则关联账户将自动创建，您无法覆盖其创建。

- 删除用户
关联的 Windows NT 域账户将自动删除。您无法覆盖此删除 7–38 管理用户账户

如果您想保留 Windows NT 账户，请执行此操作。修改一个组

有关信息请参阅第 7 章。

### 7.6.1.2 使用账户管理器 (dxaccounts)

账户工具 `dxaccounts` 是一个原生的 X 应用程序，可以使用窗口环境的功能，例如绘图

271

以及拖放和粘贴图标来轻松地克隆账户和组。然而，与便携的 SysMan 账户工具不同，它仅在 XDE 中运行。

管理器不支持 LDAP 组。

### 7.6.1.3 使用命令行工具

用于管理用户组账户的命令行工具用于配置默认账户特性，如示例 7-1 所示。这些特性应用于所有新创建的账户并在 ASU 工具中被称为账户策略。与图形化工具不同，在运行命令时，您可以选择覆盖环境变量并为新账户指定自定义值。

安装 ASU 后，将可以使用以下账户和组创建选项：

- `useradd`, `usermod`-提供了以下选项使用 `-D` 设置默认的 Windows 账户特性。同时也显示了默认值：
- `pc_synchronize=(value: 1, on)`
使用此选项确定在 Windows NT 域或 UNIX 系统上创建新账户时是否默认创建同步账户。如果此值为零，则不创建同步账户。
- `pc_min_password_age=(value: 0, off)`
此选项指定更改密码之前必须经过的天数。不允许用户比此更频繁地更改密码。
- `pc_max_password_age=(value: 42 days)`
使用此选项指定在必须更改密码之前可以经过的最大天数。用户必须至少定期更改密码。
- `pc_passwd_uniqueness=(value: 0, off)`
使用此选项强制对用户提供的密码进行唯一性验证，确保他们不重复密码。

`pc_force_logoff=(value: Never, off)`

使用此选项设置临时账户，当账户过期后，账户持有人将被自动注销。

你可以如示例 7-1 所示，通过 `-D -x` 选项调用这些扩展选项。要覆盖默认特性，你可以在执行账户管理操作（例如创建账户）期间，使用 `x` 标志位指定扩展选项：

```
# useradd -x pc_passwd_uniqueness=1 guest9
```
