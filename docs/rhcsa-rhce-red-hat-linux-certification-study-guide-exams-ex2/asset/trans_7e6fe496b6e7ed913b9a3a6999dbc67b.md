
> 如果你在考试期间必须配置 SELinux，则在安装过程中已无法再进行配置。SELinux 默认以 enforcing 和 targeted 模式实现。如果必须配置 SELinux 且需要重启，应用 SELinux 策略的过程可能需要几分钟。在考试期间你将无法登录或做其他任何事情。因此请提前规划！

> 如果你只是想尝试 SELinux，请将其配置为 permissive 模式。它会记录任何违规行为而不阻止任何操作。可以使用 SELinux 管理工具轻松设置，或在 /etc/sysconfig/selinux 中设置 SELINUX=permissive。如果 auditd 服务正在运行，违规行为会记录在 /var/log/audit 目录下的 audit.log 文件中。只要记住，Red Hat 很可能希望考生在考试期间将 SELinux 配置为 enforcing 模式。

## 命令行下配置 SELinux

虽然 SELinux 仍在积极开发中，但在 RHEL 6 发布后变得更加有用。尽管与 SELinux 相关存在恐惧，使用 SELinux 管理工具来配置 SELinux 设置可能更高效。而且它相比 Security Level Configuration 工具中的 GUI SELinux 功能有了很大改进。你甚至可以为单个目录设置 SELinux 上下文。

为此，以下各节展示了如何从命令行界面配置和管理 SELinux。然而，使用 GUI 工具演示 SELinux 的完整功能更容易，因此本章稍后将详细介绍此类功能。

## 配置基本 SELinux 设置

有一些基本命令可用于查看和配置基本 SELinux 设置。要查看 SELinux 的当前状态，运行 `getenforce` 命令；它返回三个不言自明的选项之一：`enforcing`、`permissive` 或 `disabled`。`sestatus` 命令提供更多信息，输出类似于以下内容：

```
SELinux status:		enabled
SELinuxfs mount:	/selinux
Current mode:		enforcing
Mode from config file:	enforcing
Policy version:		24
Policy from config file:	targeted
```

你可以使用 `setenforce` 命令更改当前的 SELinux 状态；选项很简单：

```
# setenforce enforcing
# setenforce permissive
```

这会更改 `/selinux/enforce` 布尔值。作为布尔值，你可以用 1 和 0 分别代替 `enforcing` 和 `permissive`。然而，详细 SELinux 布尔值的更改需要不同的命令。

> **考试提示**
> 如果 SELinux 被禁用，在将 SELinux 设置为 enforcing 模式后重启系统可能需要几分钟。然而，与 RHEL 5 相比，该过程花费的时间要少得多。

另外，如果由于某种原因 SELinux 被禁用，输出将为：

```
SELinux status:		disabled
```

在这种情况下，`setenforce` 命令将不起作用。相反，你必须在 `/etc/sysconfig/selinux` 文件中设置 `SELINUX=enforcing`。这需要进行“重新标记”，即 SELinux 标签会被应用到本地系统上的每个文件。这可能需要宝贵的时间。

## 为 SELinux 配置普通用户

与 RHEL 5 的一个变化是普通默认用户的 SELinux 状态。要查看当前用户的状态，运行 `semanage login -l` 命令。根据 RHEL 6 的默认安装，其输出如下：

```
__default__		unconfined_u		s0-s0:c0.c1023
root			unconfined_u		s0-s0:c0.c1023
system_u		system_u		s0-s0:c0.c1023
```

换句话说，普通的“默认”用户具有与 `root` 管理用户相同的 SELinux 权限。为确认这一点，以普通用户身份运行 `id -Z` 命令。未作更改时，其输出如下，这表明该用户不受任何 SELinux 设置限制。

```
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

虽然这可能不是考试要求，但普通用户应由 SELinux 进行限制。当用户账户被入侵，而它们终将被入侵时，你希望 SELinux 规则能将可能造成的任何损害限制在最小范围。以下示例通过添加 (-a) 普通用户 `michael`，指定 (-s) `user_u` 角色进行限制：

```
# semanage login -a -s user_u michael
```

`user_u` 角色不应具有运行第 8 章所述的 `su` 或 `sudo` 命令的能力。如有需要，你可以使用 `semanage -d michael` 命令逆转此过程。由于用户角色仍在开发中，你应重点关注最新 Red Hat 文档中列出的可用用户角色，如表 4-8 所示。

另一个常见“用户”角色是 `system_u`，它通常不适用于普通用户。它是 `ls -Z` 命令对系统和配置文件输出中常见的用户。

当用户角色更改后，直到下次登录才会生效。例如，如果我在基于 GUI 的命令行中将用户 `michael` 的角色更改为 `user_u`，更改要到我注销并重新登录 GUI 后才会生效。当我在我的系统上尝试时，我不再能够启动任何管理配置工具，并且无法访问 `sudo` 和 `su` 命令。

在某些网络中，你可能希望将未来用户的角色更改为 `user_u`。如果不希望普通用户摆弄管理工具，你可以使用以下命令为未来的默认用户进行更改：

```
# semanage login -m -S targeted -s "user_u" -r s0 __default__
```

此命令修改 (-m) targeted 策略存储 (-S)，使用 SELinux 用户 (-s) `user_u`，使用 MLS s0 范围 (-r) 用于默认用户。`__default__` 在单词两侧各包含两个下划线字符。只要默认 SELinux 用户生效为 `user_u`，普通用户就无法访问管理工具或 `su` 和 `sudo` 等命令。以下命令可逆转此过程：

```
# semanage login -m -S targeted -s "unconfined_u" \
-r s0-s0:c0.c1023 __default__
```

> 考试提示 MLS 模式增加了 SELinux 的复杂性。具有适当布尔值和文件上下文的 Targeted 模式通常能提供充足的安全性。

需要完整的 MLS 范围 (`s0-s0:c0.c1023`)，因为 `unconfined_u` 用户通常不受 MLS 限制的限制。

**表 4-8**
SELinux 用户角色选项

| 用户角色 | 功能 |
|---|---|
| guest_u | 无 GUI，无网络，无 su 或 sudo 命令访问权限 |
| xguest_u | GUI，仅通过 Firefox 网络浏览器进行网络连接 |
| user_u | GUI 和网络可用 |
| staff_u | GUI、网络和 sudo 命令可用 |
| unconfined_u | 完全系统访问 |

## 管理 SELinux 布尔设置

大多数 SELinux 设置都是布尔值——换句话说，它们通过设置为 1 或 0 来激活和停用。设置后，布尔值存储在 `/selinux/booleans` 目录中。一个简单的例子是 `user_ping`，它通常设置为 1，允许用户运行 `ping` 命令。这些 SELinux 设置中的许多与特定的 RHCE 服务相关，将在本书记述的后半部分介绍。

这些设置可使用 `getsebool` 读取并使用 `setsebool` 命令修改。例如，`getsebool allow_user_exec_content` 命令的以下输出确认 SELinux 允许用户在主目录或 `/tmp` 目录中执行脚本：

```
allow_user_exec_content --> on
```

此默认值适用于 SELinux `user_u` 用户。换句话说，有了此布尔值，这类用户可以在所述目录中创建和执行脚本。该布尔值可以临时禁用，或以在重启后仍然有效的方式禁用。一种方法是使用 `setsebool` 命令。例如，以下命令在系统重启前禁用所述布尔值：

```
# setsebool allow_user_exec_content off
```

你可以在命令中用 `=0` 代替 `off`。由于这是一个布尔设置，效果相同；标志被关闭。然而，需要 `-P` 才能使布尔设置更改在系统重启后仍然有效。请注意，更改要到受影响用户实际登录相关系统时才会生效。

`getsebool -a` 命令的输出中提供了可用布尔值的完整列表。
