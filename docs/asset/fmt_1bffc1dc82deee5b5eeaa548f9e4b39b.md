
列表 1-5 显示，用户 `david` 在更改密码后必须至少等待两天才能再次更改。在被强制更改密码之前，他可以停留的最大数为 90 天。他会提前七天收到警告。如果他在密码过期后的 14 天内没有登录（并成功更新密码），账户将变为非活动状态，他将无法更改密码（或登录）。

如果你请了暑期工，可以为他们设置一个账户过期日期。然后你可以将更改密码的最小天数设置得大于最大密码有效期。这将防止他们在拥有账户期间更改密码。将警告设置为 `0` 则不会让他们受到他们无能为力的警告的困扰。所以你可以看到，只要有一点想象力，就可以设置账户来处理密码有效期的许多不同情况。

![](img/af15a808e558ebd8fb82568163d30069_43_0.png)

你将在第 2 章学习更多关于为什么你应该实施密码有效期管理的知识。

![](img/af15a808e558ebd8fb82568163d30069_46_0.png)

## 理解模块控制

第二列是控制字段，指示当模块返回 `SUCCESS`（成功）、`IGNORE`（忽略）或 `FAILURE`（失败）时会发生什么。该字段可以包含以下之一：`requisite`（必须）、`sufficient`（足够）或 `optional`（可选）。控制字段中任意行使用的值会影响其他行。例如，一个标记为 `sufficient` 成功的行将终止 PAM 进程并记录用户。同样，一个标记为 `requisite` 失败的行将立即终止登录过程。无论在何种情况下，都不会有后续行被处理。通常情况下，所有行都会被处理。

- `requisite` 控制是终结性的。任何标记为 `requisite` 的行如果从模块接收到 `FAILURE`，将立即终止并向服务返回 `FAILURE`。其他模块将不会被评估。你通常不会希望使用这种控制；使用 `required`（见下一条目）更好。这是因为 `requisite` 是文件中的第一个控制，其下方的模块将不会被评估，包括用于记录尝试访问的模块。（参见“模块解释”）

- `required` 控制将与其他所有行结合使用。这意味着，无论状态（`SUCCESS`、`IGNORE` 或 `FAILURE`），其余模块都将通过评估。`required` 控制是最常用的，因为在从所有模块接收到最终状态之前，它的状态不会返回给服务，这意味着如果其中一个模块用于记录尝试（无论成功与否），你将获得一条日志条目。我们将更深入地观察它的工作原理。

- `sufficient` 控制在被遇到时，只要之前的 `required` 控制没有通过 `FAILURE`，它就会立即向服务返回 `SUCCESS`（从而成功终止登录过程）。如果之前的 `required` 控制字段通过了 `FAILURE`，则 `sufficient` 控制将返回 `IGNORE` 或 `FAILURE`，然后它被视为一个可选（`optional`）控制的 `IGNORE` 或 `FAILURE`（见下一段）。

- `optional` 控制仅当它是任何给定类型的唯一模块时才重要。否则，`FAILURE` 将被忽略。如果即使此控制失败也允许用户登录，则应该使用这种控制。

为了让用户被允许访问系统，任何一个 `requisite` 或 `required` 模块都不能返回 `FAILURE`。由于它们没有返回，用户被允许访问。请记住，如果 `optional` 控制是任何给定类型的唯一模块，则它将变为 `required`。

## 模块本身

第三列是要使用的模块的完整文件名。模块可以位于你希望放置的任何地方，但如果模块位于编译后的模块目录中，则只需要名称。否则，必须指定模块的完整路径。`OpenLinux` 的编译内置模块路径为 `/lib/security`。

第四列将包含你可能传递给模块的任何适用选项。并不是所有模块都有选项，且并不总是需要选项，但它们用于以某种方式修改模块的行为。你将结合下面的模块查看这些选项。

`OpenLinux` 提供的可用插拔认证模块包括列表 1-7 中的模块。

**列表 1-7：** `OpenLinux` 上可用的 PAM

- `pam_access.so`
- `pam_cracklib.so`
- `pam_deny.so`
- `pam_dialup.so`
- `pam_env.so`
- `pam_ftp.so`
- `pam_group.so`
- `pam_lastlog.so`
- `pam_limits.so`
- `pam_listfile.so`
- `pam_mail.so`
- `pam_nologin.so`
- `pam_permit.so`
- `pam_pwdb.so`
- `pam_radius.so`
- `pam_rhosts_auth.so`
- `pam_rootok.so`
- `pam_securetty.so`
- `pam_shells.so`
- `pam_stress.so`
- `pam_tally.so`
- `pam_time.so`
- `pam_unix_acct.so`
- `pam_unix_auth.so`
- `pam_unix_passwd.so`
- `pam_unix_session.so`
- `pam_warn.so`
- `pam_wheel.so`

首先你将查看一些更常见的模块，然后查看它们如何使用的示例，以便理解模块堆叠，从登录服务开始。

## 模块解释

`pam_access.so` 模块指定使用 `/etc/security/access.conf` 文件来确定是否允许访问。访问根据该文件内的匹配项被允许（或拒绝）。该文件中的每行格式为：

`permission:user(s):origins`

- `permission` 将是 `+`（允许）或 `-`（拒绝）。
- `user(s)` 将是 `ALL` 之一。

`OpenLinux` 默认不包含示例文件，但上述内容允许你创建一个文件并测试此模块。此模块不接受任何选项。

`pam_cracklib.so` 模块根据字典单词检查密码。当用户尝试更改密码时，模块会对密码进行一些合理性检查，以查看其是否容易被猜，例如使用字典单词（或派生词）、重复字母、长度（太短）以及其他几个。选项不是必须的，但提供了：`debug`、`type` 和 `retry=`。`debug` 选项是详细的并会记录会话。`type=` 选项允许你更改默认的“New UNIX password:”提示符，将 `type=` 之后的字符串替换掉为 `UNIX`。而 `retry` 将在失败时返回错误之前提示用户指定的次数（默认为 `1`）。

**列表 1-8：** 另一个受限的服务文件

```
| auth | control | module |
| :--- | :--- | :--- |
| auth | required | pam_deny.so |
| auth | required | [empty] |
| account | required | pam_deny.so |
| account | required | [empty] |
| password | required | [empty] |
| session | required | [empty] |
```

如你所示，`auth`、`account`、`password` 和 `session` 都是 `required`。

# 第 1 章：用户、组和安全

## 第 1 节：用户、组和安全

请小心处理此项，因为登录服务中带有足够控制的第一条 `auth` 语句将允许 `root` 无密码登录，这可能不是您想要的——您已收到警告。它接受一个选项：`debug`。

`pam_permit.so` 模块补充了 `pam_deny.so` 模块，它始终返回 `SUCCESS`。此模块忽略所有选项。

`pam_pwdb.so` 模块提供了对 `passwd` 和 `shadow` 文件的接口。此模块接受多个选项，但在使用之前您应该了解它们。可用选项如下：

- `debug`–记录调试信息
- `audit`–记录任何用户需要的审计调试信息
- `use_first_pass`–从上一个模块获取密码；不提示密码
- `try_first_pass`–除非 `authtok` 未设置，否则不提示密码
- `use_authtok`–如果未检测到 `pam_authtok`，则返回 `FAILURE`；不提示密码（仅用于堆叠的密码模块）
- `not_set_pass`–不维护 `shadow` 密码系统
- `unix`–将密码存入 `/etc/passwd` 文件
- `md5`–在下次更改密码时使用 `md5` 哈希值
- `bigcrypt`–在下次更改密码时使用 `DES-C2` 算法
- `nodelay`–避免 `1` 秒的身份验证失败延迟

截至本文为止，`OpenLinux` 不支持使用 `md5` 或 `bigcrypt` 密码，因此不应使用它们。除非您已转换了 `shadow` 文件并恢复到旧式的 `UNIX` `passwd` 文件，否则不应使用 `UNIX` 选项。注意，某些选项包含了这些对比的使用。

`pam_hosts_auth.so` 模块允许或禁止使用 `.hosts` 和 `hosts.equiv` 文件。它还允许或禁止在文件中这些“危险”条目。选项包括：

- `no_hosts_equiv`–忽略 `/etc/hosts.equiv` 文件
- `no_hosts`–忽略 `/etc/hosts` 或 `~/.hosts` 文件
- `debug`–记录调试信息
- `now`–不打印警告
- `suppress`–抑制所有消息
- `promiscuous`–允许在任何字段中使用 `+` 通配符（这是一个非常糟糕的主意）

`pam_rootok.so` 模块对任何 `UID` 为 `0` (`root`) 的用户返回 `SUCCESS`。配合足够控制（`sufficient` control）使用时，它将允许无密码访问服务。

`pam_security.so` 模块仅允许 `root`。它读取文件 `/etc/security`，并仅允许 `root` (`UID` `0`) 从该文件中列出的控制台登录。如果您处于非常安全的环境中并希望 `root` 能够通过 `telnet`（伪终端，即 `tty` 设计）登录，则要么添加 `tty0-255` 的行，要么注释掉登录服务中的 `pam_security.so` 行。注意不建议禁用此模块。该模块会检查确保 `/etc/security` 不可写。

`pam_shells.so` 模块如果 `/etc/passwd` 中列出的用户 `shell` 也列在 `/etc/shells` 中，则返回 `SUCCESS`。如果 `/etc/passwd` 未列出 `shell`，则用户使用 `/bin/sh` 登录。`/etc/passwd` 中列出的任何未在 `/etc/shells` 中的 `shell` 都会对该用户返回 `FAILURE`。`/etc/passwd` 文件不能是可写的。

`pam_stress.so` 模块用于密码管理。此模块有大量选项，包括 `debug`，但在正常情况下，通常是以下之一：

- `rootok`—允许 `root` 修改用户密码而无需提示旧密码
- `expired`–告诉模块像用户密码已过期一样执行

其他选项将导致第一个或第二个（如果适用）函数失败，使用来自另一个模块的密码或将密码传递给另一个模块（或不），等。虽然 PAM 非常灵活，但如果您需要这些特殊功能，应该阅读关于该模块的 PAM 文档。

`pam_tally.so` 模块默认在 `OpenLinux` 的任何服务文件中均未使用。然而，它非常值得讨论。此模块将维护尝试访问的计数。计数可以通过成功登录重置，也可以在达到预定的失败次数后拒绝访问。默认计数文件为 `/var/log/faillog`（不可写）。全局选项有：

- `err=[successfail]`–如果发生错误（例如无法打开文件）该怎么做
- `file=/full/path/and/filename`–如果不使用默认值

以下选项仅适用于 `auth` 类型：
- `no_magic_root`–通常 `root` (`UID` `0`) 在失败时不会增加计数器，但此选项强制执行增加。如果您允许 `root` 使用 `telnet`/`r-commands`，这是一个好主意（尽管总而言，`telnet`/`r-commands` 是非常糟糕的主意）

## 第 1 部分：您的主机

以下选项仅适用于账户类型：

- `deny=n` – 在尝试登录 `n` 次后拒绝访问。当未指定 `no_magic_root` 时，除 `root` 用户 (`UID` `0`) 外，将默认的重置行为从不重置更改为重置
- `no_magic_root` – 不忽略 `root` 访问尝试的拒绝。当与上述 `deny=` 结合时，重置行为与普通用户一致
- `even_deny_root_account` – 与上述 `no_magic_root` 结合时，可以锁定 `root`。您已收到警告。只要不指定 `no_magic_root`，`root` 就可以绕过，但普通用户将被锁定
- `reset` – 所有用户（包括 `magic root`）成功登录时将计数器重置为 `0`
- `no_reset` – 不重置计数；除非设置了 `deny=`，否则默认如此

`pam_time.so` 模块允许根据时间限制访问。这在 `/etc/security/time` 中提供。`pam_time.so` 模块允许或禁止使用 `.time`。它还允许或禁止在文件中这些“危险”条目。

`pam_wheel.so` 模块允许或禁止 `wheel` 组的用户访问。`pam_wheel.so` 模块允许或禁止使用 `.wheel`。它还允许或禁止在文件中这些“危险”条目。

`pam_unix.so` 模块允许或禁止使用 `.unix`。`pam_unix.so` 模块允许或禁止在文件中这些“危险”条目。

`pam_time.so` 模块允许在 `/etc/passwd` 中限制访问。`pam_unix.so`, `pam_wheel.so`, `pam_time.so`, `pam_warn.so`, `pam_secure.so`。

`pam_security.so` 模块仅允许 `root`。它读取文件 `/etc/security` 并仅允许 `root` (`UID` `0`) 从该文件中列出的控制台登录。如果您处于非常安全的环境中并希望 `root` 能够通过 `telnet`（伪终端，即 `tty` 设计）登录，要么添加 `tty0-255` 的行，要么注释掉登录服务中的 `pam_security.so` 行。注意不建议禁用此模块。该模块会检查确保 `/etc/security` 不可写。

`pam_shells.so` 模块如果 `/etc/passwd` 中列出的用户 `shell` 也列在 `/etc/shells` 中，则返回 `SUCCESS`。如果 `/etc/passwd` 未列出 `shell`，则用户使用 `/bin/sh` 登录。`/etc/passwd` 中列出的任何未在 `/etc/shells` 中的 `shell` 都会对该用户返回 `FAILURE`。`/etc/passwd` 文件不能是可写的。

`pam_stress.so` 模块用于密码管理。此模块有大量选项，包括 `debug`，但在正常情况下，通常是以下之一：

- `rootok`—允许 `root` 修改用户密码而无需提示旧密码
- `expired`–告诉模块像用户密码已过期一样执行

其他选项将导致第一个或第二个（如果适用）函数失败，使用来自另一个模块的密码或将密码传递给另一个模块（或不），等。虽然 PAM 非常灵活，但如果您需要这些特殊功能，应该阅读关于该模块的 PAM 文档。

`pam_tally.so` 模块默认在 `OpenLinux` 的任何服务文件中均未使用。然而，它非常值得讨论。此模块将维护尝试访问的计数。计数可以通过成功登录重置，也可以在达到预定的失败次数后拒绝访问。默认计数文件为 `/var/log/faillog`（不可写）。全局选项有：

- `err=[successfail]`–如果发生错误（例如无法打开文件）该怎么做
- `file=/full/path/and/filename`–如果不使用默认值

以下选项仅适用于 `auth` 类型：
- `no_magic_root`–通常 `root` (`UID` `0`) 在失败时不会增加计数器，但此选项强制执行增加。如果您允许 `root` 使用 `telnet`/`r-commands`，这是一个好主意（尽管总而言，`telnet`/`r-commands` 是非常糟糕的主意）

## 示例

现在你已经看到了这些模块的作用，请回看列表 1-6，登录服务。首先，你看到一个带有强制控制的 `auth` 类型调用了安全模块。这只允许从安全终端访问 `root`。第二行检查 `/etc/passwd` 文件以验证用户和 `UID`。第三条 `auth` 语句将查找一个 `/etc/nologin` 文件。如果它不存在，则返回 `SUCCESS`。第四条 `auth` 语句被注释掉了，但如果你想根据 `/etc/security` `tty.dialog` 和 `passwd.passwd` 中定义的密码和授权进行检查，可以轻松更改，但这并不是允许拨号。最后一条 `auth` 语句是可选的，但如果系统仅用于电子邮件账户，则可能需要。

账户类型检查 `shadow` 文件中包含的用户密码。如果它与用户输入的匹配，则返回 `SUCCESS`。

密码类型是强制的，并将用于更新密码所需的令牌。

`/etc/passwd` 中的某些文件将是原始的。例如，`chfn` 使用 `pam_passwd.so` 模块，并且它对于 `auth`、账户和密码类型是强制的。

登录文件可能还需要一些解释。第一行检查 `root` (`UID` `0`) 是否仅从安全终端登录，通常是本地系统上的终端（我们不希望在不可信的网络上通过明文传输密码）。请检查 `/etc/security`。接下来的行表示，如果 `/etc/hosts.env` 或 `~/hosts` 文件存在，则允许访问（当然，该文件对该用户是只读的）。如果这些文件不存在，你必须成功通过后续的所有模块。注意，默认情况下，包含 `cracklib.so` 模块的行是被注释掉的（行开头有一个 `#`）。你可能想要取消 `cracklib.so` 行的注释，以便用户能够更改不安全的密码。

你想要注意的最后一个服务是 `su` 服务。第一行：
