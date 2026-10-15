
### PAM 模块列表

| 模块 | 可用性 | 说明 |
| :--- | :--- | :--- |
| `pam_opie` | 公开可用 | 仅支持 `auth` 模块类型。呈现 OPIE 挑战并要求 OPIE 一次性密码。可从 `http://www.openwall.com/pam-opie.html` 获取。此模块在第 143 页的“OPIE 和 PAM”中进行了讨论。 |
| `pam_permit` | Red Hat 5.2/6.0 | 支持所有模块类型。始终返回成功。 |
| `pam_pwdb` | Red Hat 5.2/6.0 | 支持所有模块类型。替代 `pam_unix.*` 模块。根据 `/etc/pwdb.conf` 文件收集认证数据库。 |
| `pam_pwfile` | 公开可用 | 此模块在本书最后阶段宣布。它是一个仅用于认证的模块，允许指定备用密码文件。这样，您可以为各种服务配置不同的密码。例如，您可以为 IMAP 拥有一套用户名和密码，而为其他所有服务拥有完全不同的另一套。您可以在 `http://espresso.ee.sun.ac.za/~cabotha/pam_pwfile.html` 找到此模块。 |
| `pam_radius` | Red Hat 5.2/6.0 | 仅支持 `session` 模块类型。为通过 RADIUS 认证的用户提供会话服务。 |
| `pam_rhosts_auth` | Red Hat 5.2/6.0 | 仅支持 `auth` 模块类型。提供通过 `~/.rhosts` 文件进行认证的功能。可以配置为允许或拒绝此类认证。 |
| `pam_roottok` | Red Hat 5.2/6.0 | 仅支持 `auth` 模块类型。允许 `root` 用户在不要求密码的情况下访问。仅当与 `sufficient` 控制标志一起使用时才有意义。 |
| `pam_securitty` | Red Hat 5.2/6.0 | 仅支持 `auth` 模块类型。仅适用于 `root`。检查 `root` 是否从 `/etc/securitty` 中列出的设备之一登录。如果是，返回成功；否则失败。 |
| `pam_shells` | Red Hat 5.2/6.0 | 仅支持 `auth` 模块类型。如果用户的默认 `shell` 列在 `/etc/shells` 中，则验证用户。 |
| `pam_stress` | Red Hat 5.2/6.0 | 此模块用于调试和对支持 PAM 的应用程序进行压力测试。 |
| `pam_tally` | Red Hat 5.2/6.0 | 仅支持 `auth` 模块类型。跟踪登录尝试次数，并可以基于指定数量的失败尝试拒绝访问。 |
| `pam_time` | Red Hat 5.2/6.0 | 仅支持 `account` 模块类型。根据 `/etc/security/time.conf` 中指定的用户、终端、服务和时间限制访问。 |
| `pam_tcpd` | 公开可用 | 仅支持 `auth` 模块类型。通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 实现 `TCP_wrappers` 风格的访问控制、日志记录和功能。`TCP_wrappers` 在第 10 章中讨论。该模块可从 `http://web.tis.caltech.edu/~cachasse/pam_tcpd.html` 获取。 |
| `pam_unix_acct`<br>`pam_unix_auth`<br>`pam_unix_passwd`<br>`pam_unix_session` | Red Hat 5.2/6.0 | 这些模块提供与 `pam_pwdb` 类似的功能，区别在于认证数据库是 `/etc/passwd` 或 NIS。 |
| `pam_unix-new` | 公开可用 | 将上述四个模块合为一体，并实现 `pam_pwdb` 的许多功能。可在 `ftp://hunter.minuet.edu.pl/pub/users/baggins/PAM/` 获取。 |
| `pam_warn` | Red Hat 5.2/6.0 | 仅支持 `auth` 和 `password` 模块类型。此模块通过 `syslog` 工具生成包含远程用户和远程主机（如果可用）的日志消息。 |
| `pam_wheel` | Red Hat 5.2/6.0 | 仅支持 `auth` 模块类型。提供一种方式，将 `root` 的访问权限限制为 `wheel` 组的成员。 |
| `pam_xauth` | Red Hat 6.0 或公开可用 | 仅支持带有 `optional` 控制标志的 `session` 模块类型。此会话自动将 X Window System 魔术 `cookie` 传递给其他用户（例如，通过 `su`），从而允许有效的 `UID` 打开 X 应用程序，而无需使用 `xhost` 命令。 |

## 支持 PAM 的应用程序

表 5.16 列出了许多支持 PAM 的应用程序，这意味着该应用程序包含调用 PAM 所必需的调用。与表 5.15 一样，Red Hat 5.2/6.0 发行版中可用的应用程序会加以注明。

### PAM 感知应用概览

| **应用程序** | **可用性** |
| :--- | :--- |
| `chfn` | Red Hat 5.2/6.0 |
| `chsh` | Red Hat 5.2/6.0 |
| `ftp` | Red Hat 5.2/6.0 |
| `imap` | Red Hat 5.2/6.0 |
| `linuxconf` | Red Hat 5.2/6.0 |
| `linuxconf-pair` | Red Hat 5.2/6.0 |
| `login` | Red Hat 5.2/6.0 |
| `mcserver` | Red Hat 5.2/6.0 |
| `other` | Red Hat 5.2/6.0 |
| `passwd` | Red Hat 5.2/6.0 |
| `ppp` | Red Hat 5.2/6.0 |
| `rexec` | Red Hat 5.2/6.0 |
| `rlogin` | Red Hat 5.2/6.0 |
| `rsh` | Red Hat 5.2/6.0 |
| `samba` | Red Hat 5.2/6.0 |
| `su` | Red Hat 5.2/6.0 |
| `sudo`* | 公开可用 |
| `vlock` | Red Hat 5.2/6.0 |
| `xdm` | Red Hat 5.2/6.0 |
| `xlock` | Red Hat 5.2/6.0 |

*在第 9 章中讨论。

## 关于配置 PAM 的重要说明

本章对 PAM 进行了入门级介绍。文中描述了许多示例，并提供了一些使用技巧。然而，毫无疑问，你们中的许多人会有自己的配置想法。本节提供了一些简单但重要的关于为您的环境配置 PAM 的说明。

首先，也是最重要的，务必在做出任何更改之前复制现有的、能正常工作的 `/etc/pam.d` 配置文件。通过 PAM 配置错误，完全有可能导致所有用户（包括 `root` 用户）被锁定。通过保留可工作的副本，你将始终能够启动到单用户模式（有关启动到单用户模式的信息，请参阅第 3 章第 22 页关于 `LILLO` 的说明），更正配置，并恢复系统运行。

其次，配置你的 `/etc/pam.d` 目录，使其权限仅限 `root` 用户读取/写入/执行，并配置其内容仅限 `root` 用户读取/写入。其他任何人都不需要读取该目录的内容。你可以通过以下方式实现：

```bash
# chmod u=rwx /etc/pam.d
# cd /etc/pam.d
# chmod u=rw *
```

第三，在安全的、最好是非生产环境中测试你的配置想法。在上线之前，尽可能多地尝试你能想到的变体。请记住，PAM 模块堆栈中的顺序至关重要。不同的顺序会产生不同的行为。通常，你希望 `pam_pwdb` 位于认证堆栈的末尾。也不要忘记控制标志的设置。使用不同的控制标志在许多情况下会导致截然不同的行为。对于与不同模块相关的参数也是如此。请记住，同一 PAM 模块的不同模块类型支持不同的参数。

第四，也是最后一点，Linux 是公开可用的软件。PAM 模块也是如此。在发布和分发之前，没有严格的质保程序。事实上，你经常就是质量保证机制！简而言之，你使用 PAM 的成功程度将取决于你获取的版本、你运行的 Linux 版本、你的硬件平台，以及可能的其他因素。请使用附录 A 中的资源以及你可用的任何其他支持机制。

## PAM 的未来

从本章的内容来看，希望已经清楚表明，针对 PAM 已经做了大量的工作。未来实际上是非常光明的。开放软件基金会（OSF）在 1995 年 10 月专门针对 PAM 发布了 `RFC 86.0`（`RFC` 的定义见第 3 章第 40 页的 Request for Comment）。正在进行额外的工作以增强控制标志选项，使系统管理员能够根据每个模块的返回代码指定操作。第 5.15 表（第 110 页）中提到的许多模块正在开发中，第 5.16 表（第 113 页）中列出的许多应用程序也是如此。鉴于其固有的灵活性，毫无疑问，PAM 将在我们身边存在一段时间。

## 摘要

本章描述了可插拔认证模块（PAM）。我们查看了一些配置和使用 PAM 的示例。我们还复习了许多可用的 PAM 模块和应用程序。我们指出了 PAM 提供的灵活性和安全特性。

## 延伸阅读

PAM 最好的文档是 Linux-PAM 系统管理员指南，可以在以下地址找到：
