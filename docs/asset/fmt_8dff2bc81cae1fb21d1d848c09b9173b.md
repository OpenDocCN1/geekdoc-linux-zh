
此 `/etc/sudoers` 文件定义了两个用户别名，`SENIORADMIN` 和 `ASSISTANTS`，其中第一个只有一个用户（`kabir`），第二个有两个用户（`mike` 和 `john`）。用户权限规范规定如下：

用户别名 `SENIORADMIN` 列出的用户可以在所有主机上以 `root` 身份运行 `sudo`（默认），这些用户也可以运行所有命令。因为用户 `kabir` 是

现在你知道任何用户账户都可以转换为超级用户账户，你可能认为任何用户都可以很轻松地登录 Red Hat Linux 系统；事实并非如此。Red Hat Linux 系统默认使用可插认证模块（`PAM`）进行登录验证，这要求超级访问仅从认为安全的终端进行。默认情况下

用于登录的 `PAM` 配置文件 `/etc/pam.d/login` 包含如下所示的一行：

```
auth required /lib/security/pam_securetty.so
```

此行表示在允许登录之前，需要满足 `pam_securetty.so` 模块强制执行的安全限制。该特定模块仅当登录是从 `/etc/security` 文件中列出的 `TTY` 尝试时才认为超级用户登录尝试是的。但如果你决定将普通用户转换为超级用户并尝试通过 `Telnet`（将使用伪 `TTY` 设备）登录，你可以通过在 `/etc/security` 文件中添加伪 `TTY` 设备（通常为 `tty1` 到 `tty2`）来轻松更改它。不建议这样做，因为它创建了安全风险。相反，如果你必须由于某些管理和问责原因使用多个超级用户账户，你应该：

1. 创建多个用户账户。
2. 为每个超级用户创建一个普通用户账户。
3. 指示每个超级用户作为普通用户登录系统，并使用 `su` 命令（下文将讨论）切换到账户。

`su` 命令可以替代 `UID` 和 `GID`。例如，你可以作为普通用户登录并运行不带任何参数的 `su` 来进入 `root` 账户。你将被提示输入 `root` 密码；知道 `root` 密码将启动一个新的 `shell` 并以 `root` 用户登录。记住，超级用户（`UID = 0`, `GID = 0`）对所有内容都有完全访问权限，因此这些是非常敏感的账户。在后续章节中，我将向你展示如何在不将其转换为超级用户的情况下分配超级用户权限。

### 为普通用户分配权限

使用 `sudo` 命令，你可以允许普通用户执行由超级用户运行的命令。假设你是组织的首席系统管理员，刚刚获得了两个新的助理系统管理员。你想将你的日常管理任务分配给他们。你应该创建两个 `UID` 和 `GID` 设置为 `0` 的超级用户账户，以便这两个管理员对所有内容拥有完全访问权限。这取决于你对他们作为最终用户时像你一样细心的能力的信心。因为信心需要某些

可以在同一行中定义多个别名，例如：

```
UserAlias ASSISTANTS=mike,brian:INTERNS=monika,paula,jones
```

在这里，同一行内定义了两个别名（`ASSISTANTS` 和 `INTERNS`），别名定义之间用冒号分隔。同样的语法也适用于其他别名类型。

有两个特殊关键字：`ALL` 和 `NOPASSWD`。`ALL` 代表“所有”，`NOPASSWD` 用于表示不需要密码。列表 7-1 显示了 `/etc/sudoers` 文件的示例

# 列表 7-1：sudoers 文件 文件示例

```
# sudoers 文件。

#

# 此文件必须以 root 身份使用 'visudo' 命令进行编辑。

#

# 有如何编写 sudoers 文件的详情，请查看 man 页。

#
```

```
# 主机别名规范
```

```
# 用户别名规范
User_Alias SENIORADMIN=kabir

User_Alias ASSISTANTS=mike,john

# 用户权限规范
```

```
SENIORADMIN ALL-ALL

ASSISTANTS ALL-ALL
```

此 `/etc/sudoers` 文件定义了两个用户别名，`SENIORADMIN` 和 `ASSISTANTS`，其中第一个只有一个用户（`kabir`），第二个有两个用户（`mike` 和 `john`）。用户权限规范规定如下：

用户别名 `SENIORADMIN` 列出的用户可以在所有主机上以 `root` 身份运行 `sudo`（默认），这些用户也可以运行所有命令。因为用户 `kabir` 是

# 第三部分：管理用户、进程和网络

在该组中只有一个用户，这实际上意味着 `kabir` 可以通过 `sudo` 运行所有命令。换句话说，用户 `kabir` 可以执行 `root` 用户可以做的任何事情。

第二个用户规范规定，列在用户别名 `ASSISTANTS` 中的用户将允许与第一种规范中的用户具有完全相同的权限。

现在让我们回到第一个示例场景，即你有两个不需要完全超级用户权限的助手。假设你（用户 ID = `yourid`）希望这两个助手（`sysad1`, `sysad2`）仅在特定情况下拥有运行某些命令的权限，那么你的 `/etc/sudoers` 文件可能看起来如下所示：

```
# 用户别名规范
User_Alias SENIORADMIN=yourid

User_Alias ASSISTANTS=sysad1,sysad2
```

```
# 用户权限规范
SENIORADMIN ALL=ALL

ASSISTANTS ALL=ALL=/sbin/shutdown
```

现在假设过了一段时间，你确信这两个用户可以负责任地处理其他超级权限，因此你想给他们完全访问权限，但排除运行 `su` 命令的权限。现在的 `/etc/sudoers` 如下所示：

```
# 用户别名规范
User_Alias SENIORADMIN=yourid

User_Alias ASSISTANTS=sysad1,sysad2
```

```
# 用户权限规范
SENIORADMIN ALL=ALL

ASSISTANTS ALL=ALL,!/bin/su
```

从 `ASSISTANTS` 的用户规范中可以看出，他们被允许通过 `sudo` 运行除 `/bin/su` 命令之外的所有 `ALL` 命令。如你所见，`sudo` 命令在创建具有部分超级用户权限的用户时非常有用。现在你已经非常了解关于如何创建和管理超级用户账户了，请考虑一下与普通用户相关的管理问题。

在创建、修改和删除用户账户时，你有两种选择：使用命令行工具管理用户或使用 Linux 工具。由于第一种方法是传统的，而第二种方法是新兴的方法，我将向你展示这两种方法。

# 第7章：用户管理 185

### 使用命令行工具管理用户

随着 Linux 变得比任何时候都要流行，红帽公司和整个 Linux 社区都在让 Linux 变得易用。`linuxconf` 项目就是一个很好的例子。然而，管理 UNIX 盒的传统方法仍然必要的，以便熟悉其他 UNIX 操作系统的人也能轻松管理 Linux 系统。在本节中，我将向你展示使用各种命令行工具进行用户管理的传统方法。

> 注意：后续章节中讨论的命令也适用于影子密码（`shadow passwords`）。你将在第 18 章中学习影子密码。

# 创建新用户账户

创建新用户账户非常简单。要在命令行创建用户，你可以运行 `useradd` 命令。例如，要创建一个名为 `newuser` 的用户，你可以如下所示运行此命令：

```
useradd newuser
```

这将使用系统默认值在 `/etc/passwd` 中添加一个新条目（如果你使用影子密码，则在 `/etc/shadow` 中添加：详情请参见第 18 章）。例如，当我在我的红帽系统上运行上述命令时，`/etc/passwd` 显示了如下的新用户：

```
newuser:::506:::/home/newuser:/bin/bash
```

如果你还记得之前讨论过的 `/etc/passwd` 字段，你会发现密码字段（第二个字段）被设置为 `!!`。这意味着尚未设置密码，用户还无法登录。因此，你需要通过运行如下的 `passwd` 命令为该用户创建一个密码：

```
passwd newuser
```

你会被要求输入两次密码，一旦密码被接受，它将被加密并添加到 `/etc/passwd` 文件中该用户的条目中。

`UID` 和 `GID` 的值将由 `useradd` 自动选择。基本上，它会将 `/etc/passwd` 中的最后一个用户 `UID` 增加 1，并将 `/etc/group` 中的最后一个 `GID` 增加 1，分别为新用户创建 `UID` 和 `GID`。主目录会在默认的顶层主目录中创建。同样，登录 `shell` 也是从系统默认中选择的。你将在稍后的章节中学习如何设置这些默认值。如果你想覆盖默认值，可以指定命令行选项。要覆盖默认主目录，请使用 `-d newdirectory` 选项（其中 `newdirectory` 是你的目录名称）。例如：

```
useradd newuser -d /www/newuser
```
