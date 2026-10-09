

PAM 文件未正常工作。为了防止恶意用户查看有关 PAM 的信息，PAM 将错误消息发送到文件，而不是屏幕。

## 不要将自己锁定在系统之外

正确编辑 PAM 配置文件需要仔细小心。一个小小的错误就可能让你将自己锁定在系统之外。为了避免此问题，请保留你编辑的 PAM 配置文件的备份副本，彻底测试每一项更改，并确保更改安装后你仍能登录。在你完成测试之前，保持一个 root shell 打开（使用 `sudo -i`）。如果更改失败且无法登录，请使用 root shell 用备份副本替换新编辑的文件。

## 更多信息

- 本地：/usr/share/doc/libpam*
- 手册页：pam 手册页。输入命令 `apropos pam` 以列出 PAM 手册页。
- Web：*Linux-PAM 系统管理员指南*：www.kernel.org/pub/linux/libs/pam/Linux-PAM-html/Linux-PAM-SAG.html
- HOWTO：*用户认证 HOWTO*

## 配置文件、模块类型和控制标志

以下是一个 PAM 配置文件的示例。注释行（已省略）以井号（#）开头。

```
$ grep '^[^#]' /etc/pam.d/*
auth    requisite    pam_securtty.so
auth    requisite    pam_nologin.so
session required    pam_env.so readenv=1
session required    pam_env.so readenv=1 envfile=/etc/default/locale
@include common-auth
auth    optional    pam_group.so
session required    pam_limits.so
session optional    pam_lastlog.so
session optional    pam_motd.so
session optional    pam_mail.so standard
@include common-account
@include common-session
@include common-password
```

每一行都指示 PAM 在认证过程中执行某些操作。每行的第一个词是模块类型指示符：account、auth、password 或 session（表 11-4，见下页）。第二个词是控制标志（表 11-5，见下页），指示当认证失败时 PAM 应采取的操作。该行的其余部分包含 PAM 模块的名称（位于 /lib/security）以及该模块的任何参数。PAM 库本身使用 /etc/pam.d 文件来确定将工作委派给哪些模块。以 @include 开头的行包含指定名称的文件。

表 11-4 模块类型指示符

| 模块类型 | 描述 | 控制 |
| :--- | :--- | :--- |
| account | 账户管理 | 确定已认证用户是否允许使用其正在尝试使用的服务。（即，账户是否已过期？该用户此时是否允许使用此服务？） |
| auth | 认证 | 证明用户已获授权使用该服务；使用密码或其他机制。 |
| password | 密码修改 | 更新认证机制，如用户密码。 |
| session | 会话管理 | 在服务启动时（如用户登录时）设置相关内容，并在服务终止时（如用户注销时）拆除相关内容。 |

你可以使用表 11-5 中列出的控制标志关键字之一来设置控制标志。

表 11-5 控制标志关键字

| 关键字 | 标志功能 |
| :--- | :--- |
| required | 成功是认证成功的必要条件。在所有模块执行完毕后，才会返回控制权及失败结果。这种将报告延迟到所有模块执行完毕后再告知调用程序的技术，可能使攻击者无法准确知道其认证尝试失败的具体原因，并减少向攻击者透露的系统信息，使其更难入侵。 |
| requisite | 成功是认证成功的必要条件。在模块失败后立即中止进一步的模块处理，并立即返回控制权。这种技术可能会向攻击者暴露有关系统的信息。然而，如果它能阻止用户在不安全的连接上输入密码，则可能防止信息落入攻击者之手。 |
| sufficient | 成功表示该模块类型已认证成功，且后续同类型的 required 模块将不会执行。失败对于该模块类型的堆栈并非致命。这种技术通常用于当某种认证形式足够时：如果一种失败，PAM 会尝试另一种。例如，当你使用 rsh 连接到另一台计算机时，pam_rhosts_auth 首先检查你的连接是否可以在没有密码的情况下被信任。如果连接可被信任，pam_rhosts_auth 模块报告成功，PAM 立即向调用它的 rsh 守护进程报告成功。你不会被要求输入密码。如果你的连接不被认为是可信的，PAM 会重新开始认证并请求密码。如果第二次认证成功，PAM 会忽略 pam_rhosts_auth 模块报告失败的事实。如果两个模块都失败，你将无法登录。 |
| optional | 结果通常被忽略。可选模块仅在它是特定服务堆栈上唯一的模块时才相关。 |

PAM 按照应用程序的要求使用每种模块类型。也就是说，应用程序单独要求 PAM 进行认证、检查账户状态、管理会话和更改密码。PAM 使用 /lib/security 目录中的一个或多个模块来完成这些任务中的每一项。

/etc/pam.d 中的配置文件列出了用于每个应用程序执行每项任务的模块集合。每组相同模块类型的集合称为堆栈。PAM 按顺序一次调用一个模块，从堆栈顶部（配置文件中列出的第一个模块）到堆栈底部。每个模块向 PAM 报告成功或失败。当一个配置文件内的所有模块堆栈（有一些例外）都被调用后，PAM 库向应用程序报告成功或失败。

## 示例

以下是登录服务认证堆栈的一部分：

```
$ cat /etc/pam.d/login
auth required pam_security.so
@include common-auth
auth requisite pam_nologin.so
...
```

登录实用程序首先请求用户名，然后要求 PAM 运行此堆栈以认证用户。请参阅表 11-4 和表 11-5。

1. PAM 首先调用 pam_security（安全 tty）模块，以确保 root 用户仅从允许的终端登录。（默认情况下，root 不允许通过网络运行 login；此策略有助于防止安全漏洞。）如果认证堆栈要成功，pam_security 模块必须成功。只有当有人试图从未授权的终端以 root 身份登录时，pam_security 模块才报告失败。否则（如果正在认证的用户名不是 root，或者用户名是 root 且登录尝试来自安全终端），pam_security 模块报告成功。
2. PAM 内部的成功和失败是不透明的概念，仅适用于 PAM。它们等同于操作系统其他地方使用的“true”和“false”是不等同的。
3. 包含的 common-auth 文件包含检查正在登录的用户是否已获授权的模块。作为完成此任务的一部分，这些模块验证用户名和密码。
4. pam_nologin 模块确保如果 /etc/nologin.txt 文件存在，则只允许 root 用户登录。（即，只有当 /etc/nologin.txt 不存在或 root 用户正在登录时，pam_nologin 模块才报告成功。）因此，当已安排不久后关机时，系统阻止用户登录，以免系统在登录后的几分钟后关机。

account 模块类型的工作原理与 auth 模块类型类似，但在用户认证后被调用；它充当用户访问系统前必须满足的额外安全检查或要求。例如，**account** 模块可能强制实施一项政策，规定用户只能在工作时间登录，或检查密码是否已过期。

**session** 模块类型用于设置和拆除会话（也许是挂载和卸载用户的家目录）。在 Ubuntu 系统中常见的一个 **session** 模块是 **pam_mail**，它在用户登录到文本环境时通告**你有新邮件**。

**password** 模块类型有点特别：堆栈中的所有模块都被调用一次，并被指示获取将其密码存储到持久内存（如磁盘）所需的所有信息，但并非实际存储。如果确定无法或不应存储密码，模块将报告失败。如果堆栈中的所有 **password** 模块都报告成功，它们会被第二次调用，并被告知将第一次获取的密码存储到持久内存中。**password** 模块负责更新认证信息（即更改用户密码）。

任何一个模块可以充当一种以上的模块类型；许多模块可以充当所有四种模块类型。

# 修改 PAM 配置

## 修改 PAM 文件时要谨慎

> 注意 | 除非你了解如何配置 **PAM**，否则不要更改 `/etc/pam.d` 中的文件。**PAM** 配置中的错误会使系统不可用。

某些 UNIX 系统要求用户必须是 **wheel** 组的成员才能使用 **su** 命令。虽然 Ubuntu Linux 默认未如此配置，但 **PAM** 允许你通过编辑 `/etc/pam.d/su` 文件来更改此行为：

```
$ cat /etc/pam.d/su
.
.
# Uncomment this to force users to be a member of group root before they can use 'su'
# auth    required    pam_wheel.so

# Uncomment this if you want wheel members to be able to su without a password.
# auth    sufficient    pam_wheel.so trust
...
```

此 **su** 模块的行包含注释，其中包括允许仅 **wheel** 组用户使用 **su**（required）以及允许 **wheel** 组成员在未提供密码的情况下运行 **su**（sufficient）所需的行。当你希望系统遵循这些规则之一时，取消其中一行的注释。

