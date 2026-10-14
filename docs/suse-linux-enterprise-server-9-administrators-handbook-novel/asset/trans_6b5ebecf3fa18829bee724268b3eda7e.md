
## 设置默认用户账户属性

如前一节所述，用户账户的默认值存储在 `/etc/default/useradd` 中。useradd 和 YaST 都使用此文件。其他设置，例如密码老化策略，则存储在 `/etc/login.defs` 中。然而，这两个文件仅管理本地用户——即在 `/etc/passwd` 中定义的用户。当创建 LDAP 或其他非本地用户时，这些文件不起作用，因为这些用户的设置存储在其各自的数据库中。

> **注意**
> 
> 请参阅第 8 章，了解有关设置和配置 LDAP 和 NIS 等服务的信息。

在列表 4.1 中显示了默认的 `/etc/default/useradd` 文件。新建用户的默认设置如下：

- 用户的主 GID 为 100（组 users）。
- 用户将被设为 dialout、uucp、video 和 audio 组的成员。
- 用户的主目录将在 `/home` 下创建。
- 用户可以使用已过期的密码无限期登录。
- 没有预设的账户过期日期。
- 用户的默认 shell 为 `/bin/bash`。
- `/etc/skel` 中的文件和子目录将在主目录创建后复制到用户的主目录。

### 列表 4.1
默认的 /etc/default/useradd 文件

```
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=dialout,uucp,video,audio
```

您可以根据特定需求自定义此文件。例如，如果需要新用户成为 video、audio、helpdesk 和 support 组的成员，请将 GROUPS= 行更改为：

```
GROUPS=video,audio,helpdesk,support
```

如果某些站点特定配置文件（例如包含 SQL 数据库服务器名称的配置文件）需要放置在用户主目录中，只需将它们放在 `/etc/skel` 中，它们将在主目录创建时被复制。

### 提示

`/etc/default/useradd` 中的设置可以使用 YaST 编辑。从“用户和组管理”屏幕中，选择“专家选项”，“新用户的默认值”。

默认用户账户、组和密码老化策略设置，例如密码的生命周期，均可在 `/etc/login.defs` 文件中找到。该文件还包含登录过程中使用的设置（例如登录失败后允许再次尝试前的延迟时间）。列表 4.2 中显示了与用户账户和组相关的指令。

### 列表 4.2
/etc/login.defs 中的用户和组相关指令

```
#
# Password aging controls (used by useradd):
#
# PASS_MAX_DAYS
# - Maximum number of days a password may be used.
# PASS_MIN_DAYS
# - Minimum number of days allowed between password changes.
# PASS_WARN_AGE
# - Number of days warning given before a password expires.
PASS_MAX_DAYS    99999
PASS_MIN_DAYS    0
PASS_WARN_AGE    7


#
# Min/max values for automatic uid selection in useradd
#
# SYSTEM_UID_MIN to SYSTEM_UID_MAX inclusive is the range for
# UIDs for dynamically allocated administrative and system
# accounts.
# UID_MIN to UID_MAX inclusive is the range of UIDs of
# dynamically allocated user accounts.
#
SYSTEM_UID_MIN        100
SYSTEM_UID_MAX        499
UID_MIN              1000
UID_MAX             60000
```

### 列表 4.2
/etc/login.defs 中的用户和组相关指令（续）

```
#
# Min/max values for automatic gid selection in groupadd
#
# SYSTEM_GID_MIN to SYSTEM_GID_MAX inclusive is the range for
# GIDs for dynamically allocated administrative and system
# groups.
# GID_MIN to GID_MAX inclusive is the range of GIDs of
# dynamically allocated groups.
SYSTEM_GID_MIN        100
SYSTEM_GID_MAX        499
GID_MIN               1000
GID_MAX               60000

#
# User/group names must match the following regex expression.
# The default is [A-Za-z_][A-Za-z0-9_.$-]*[A-Za-z0-9_.$-]\?
#
CHARACTER_CLASS      [A-Za-z_][A-Za-z0-9_.$-]*[A-Za-z0-9_.$-]\?

#
# Umask which is used by useradd and newusers for creating
# new home directories.
UMASK                 022

#
# If defined, this command is run when adding a user.
# It should rebuild any NIS database etc. to add the
# new created account.
#
USERADD_CMD           /usr/sbin/useradd.local

#
# If defined, this command is run before removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed.
#
USERDEL_PRECMD        /usr/sbin/userdel-pre.local

#
# If defined, this command is run after removing a user.
# It should rebuild any NIS database etc. to remove the
# account from removed.
#
USERDEL_POSTCMD       /usr/sbin/userdel-post.local
```

### 警告

最好不要更改 `SYSTEM_UID_*` 和 `SYSTEM_GID_*` 指令设置，因为这可能导致某些应用程序无法正常运行。

`/etc/login.defs` 中的 `UMASK` 指令由 useradd 和 YaST 用于设置主目录的正确文件权限。请参阅第 6 章，了解有关文件所有权和权限的信息。`USERDEL_PRECMD` 和 `USERDEL_POSTCMD` 指令指向两个可根据特定需求自定义的模板。例如，您可能希望在删除用户 ID 之前将用户主目录复制到其他位置。`USERDEL_PRECMD` 指令的默认脚本会删除用户拥有的任何 cron 作业，而默认的 `USERDEL_POSTCMD` 不执行任何操作。

### 提示

`/etc/login.defs` 中的设置可以使用 YaST 编辑，从 YaST 控制中心选择“安全和用户”，“安全设置”。如果当前安全设置是 1 级至 3 级之一，请单击“详细信息”。如果选择的是“自定义设置”，请单击“下一步”。然后会显示一系列屏幕，每个屏幕处理 `/etc/login.defs` 中找到的不同指令集。

`/etc/login.defs` 与 `/etc/default/useradd` 之间存在冗余时，`/etc/login.defs` 中的设置优先。

## 创建和编辑组

管理组的过程与管理用户类似。为了避免重复列出许多相同的步骤，我们在此列出了主要差异：

- 从 YaST 控制中心，选择“安全和用户”，“编辑和创建组”以启动“用户和组管理”模块。如果您已在“用户和组管理”模块中，请单击屏幕顶部附近的“组”单选按钮；您可以使用“用户”和“组”单选按钮在管理用户和组之间切换。
- 从终端会话启动 YaST 时，您可以使用 `yast groups` 或 `yast2 groups` 跳过 YaST 控制中心，直接进入“用户和组管理”模块。
- 图 4.3 显示了添加新本地组的屏幕。您需要提供组名，并可选择一个或多个将成为该组成员的用户。

### 图 4.3
添加新的本地组。

![](img/ae8469257d2662b469f2360b3bbbe322_128_0.png)

### 注意

“添加新本地组”屏幕中可用的用户列表包括所有已知用户，其中包括本地、LDAP、NIS 等用户。然而，如果您添加的是例如新的 LDAP 组，则仅显示 LDAP 用户以供选择。

- GID 会自动分配，使用最低的未使用 GID。如果您愿意，可以将其更改为其他值。如果新指定的值已在使用中，YaST 会发出警告。
- 组密码是可选的。它们允许非组成员的用户使用 `newgrp` 将其活动 GID 切换到该组——如果他们知道组的密码。
- 编辑现有组时，您还会看到此组为其默认组的用户的列表。您无法在 YaST 中修改此列表。要从此列表中删除用户，您需要为该用户分配不同的主 GID。

有三个常用的命令行实用程序用于管理组：

- **groupadd**—此应用程序通过向 `/etc/group` 添加新条目来创建新组。常见用法 simply `groupadd groupname`，其中将分配下一个可用的 GID。如果您希望为新组使用特定的 GID，请包含 `-g gid_number` 开关；对于系统组（即 GID 在 `/etc/login.defs` 中定义的 SYSTEM_GID_MIN 和 SYSTEM_GID_MAX 范围内的组），请包含 `-r` 开关。您可以使用 `-p password` 开关分配组密码；或者您可以使用 `passwd -g groupname`、`gpasswd groupname` 或 `groupmod -p password groupname` 稍后添加。一般建议您使用 `passwd -g` 或 `gpasswd` 设置密码，因为这样密码不会出现在命令行中。
- **groupmod**—此实用程序允许您修改组的名称、GID、成员列表及其密码。请记住，如果您更改 GID，则需要使用 `chgrp` 手动更改旧 GID 拥有的任何文件上的组所有权；更改名称对组所有权没有影响。您可以使用“创建和编辑用户账户”中之前讨论过的 `find` 命令。
- **groupdel**—使用此实用程序从 `/etc/group` 中删除组：`groupdel groupname`。请注意，只有当没有用户将此组作为其主组时，才能删除组。

在 SLES 9 及更高版本系统上您找不到 `/etc/gshadow` 文件，因为它不再使用。

## 安全考虑

保护任何操作系统的第一步是保护用户和组账户。这包括但不限于以下内容：

- 强制执行强密码选择
- 将用户访问限制为绝对必要的那些文件、目录和 shell
- 保护系统账户（尤其是 root）
- 关闭任何潜在的后门，例如禁用未使用或休眠的账户

这些步骤将在以下各节中讨论。其他预防措施，例如保护用户的工作环境、处理文件系统安全、防止
