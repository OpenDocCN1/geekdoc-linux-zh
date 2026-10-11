
## 示例 5-25 对管理员友好的 /etc/pam.d/other 文件（续）

account required /lib/security/pam_deny.so
password required /lib/security/pam_warn.so
password required /lib/security/pam_deny.so
session required /lib/security/pam_deny.so

pam_warn 的这种额外日志记录功能具有明显的调试优势，但从安全角度来看也有其优势。例如，如果您发现了一些可疑活动，您可能希望在周围服务的环境中，在认证堆栈中添加 pam_warn。对于支持该功能的模块，您也可能希望使用 debug 参数来获取更详细的审计信息。执行此操作时请务必密切关注，因为您的日志文件会迅速变得庞大。而且，如果坏人已经潜入，他们也在阅读这些日志文件！

此类别中还有另一个模块。它是 pam_deny 的对立面。它被称为 pam_permit——您猜对了——它绝对允许访问。它适用于所有模块类型，即使使用也需要极其谨慎。

## 附加 PAM 选项

还有许多其他的 PAM 模块，其中一些在本书中都有讨论。在第 109 页的“可用的 PAM 模块”中，列出了许多模块，包括当前可用的和正在开发中的；在第 112 页的“支持 PAM 的应用程序”中，描述了许多可用的应用程序。

## PAM 日志

PAM 模块会在 syslog 中记录到 auth 设施。这意味着，在您的日志中，消息最终会出现在 syslog 中 auth 设施条目指定的文件中。在 Red Hat 5.2/6.0 中，默认位置是 /var/log/messages。我们在第 8 章中讨论了 syslog。

## 可用的 PAM 模块

表 5.15 提供了许多可用 PAM 模块的列表和简要说明。一些模块随 Red Hat（或其他）发行版一起提供，而另一些则需要下载。随 Red Hat 5.2/6.0 提供的模块会加以注明（可以在 http://www.redhat.com/ 上找到）；对于其他所有模块，会指定网站，如果已知，则提供作者信息。如果您的系统已经支持这些模块，它们将位于 /lib/security 或 /usr/lib/security 中。如果您下载并添加一个模块，请确保将其放在正确的目录中。

### 表 5.15 PAM 模块概述

| 模块 | 可用性 | 描述 |
| :--- | :--- | :--- |
| pam_access | Red Hat 5.2/6.0 | 读取 /etc/security/access.conf 文件以确定用户/终端或用户/主机对是授予还是拒绝访问。 |
| pam_console | Red Hat 6.0 或公开可用 | 在物理控制台设备登录时设置权限和设备所有权。期望 /etc/security/console.console 文件提供权限和所有权参数；期望 /etc/security/console.apps/ 目录提供服务。支持 auth、account 和 session 可选：模块类型/控制标志对。 |
| pam_cracklib | Red Hat 5.2/6.0 | 仅支持 password 模块类型。用于对照 cracklib 检查密码选择，并禁止其中找到的任何选择。 |
| pam_deny | Red Hat 5.2/6.0 | 支持所有模块类型。始终返回失败。 |
| pam_env | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。使用 /etc/security/pam_env.conf 文件设置 shell 环境变量。 |
| pam_filter | Red Hat 5.2/6.0 | 支持所有模块类型。此模块提供捕获会话中几乎所有按键输入的能力。需要一个过滤器程序，未包含在内。 |
| pam_ftp | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。实现匿名 ftp。 |
| pam_group | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。根据 /etc/security/group.conf 文件设置 GID（语法几乎与第 96 页讨论的 /etc/security/time.conf 相同）。 |
| pam_if | 公开可用 | 支持所有模块类型。一种用于管理堆栈执行行为的简单条件语句。可从 http://www.dcit.cz/~jan/pam/ 获取。此模块在第 143 页的“OPIE 和 PAM”中进行了讨论。 |
| pam_lastlog | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。用于控制最后登录信息的显示。 |
| pam_limits | Red Hat 5.2/6.0 | 仅支持 session 模块类型。使用 /etc/security/limits.conf 文件根据可用的系统资源确定用户是否可以登录。 |
| pam_listfile | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。允许基于用户、终端、远程主机、组和 shell 的使用访问控制列表。 |
| pam_mail | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。提供“您有新邮件”服务。 |
| pam_nologin | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。提供检查 /etc/nologin 文件是否存在的功能，如果该文件存在，将显示文件内容并导致认证失败。 |
| pam_opie | 公开可用 | 仅支持 auth 模块类型。呈现 OPIE 挑战并要求 OPIE 一次性密码。可从 http://www.openwall.com/pam-opie.html 获取。此模块在第 143 页的“OPIE 和 PAM”中进行了讨论。 |
| pam_permit | Red Hat 5.2/6.0 | 支持所有模块类型。始终返回成功。 |
| pam_pwdb | Red Hat 5.2/6.0 | 支持所有模块类型。替代 pam_unix.* 模块。根据 /etc/pwdb.conf 文件收集认证数据库。 |
| pam_pwfile | 公开可用 | 此模块在本书最后阶段宣布。它是一个仅用于认证的模块，允许指定备用密码文件。这样，您可以为各种服务配置不同的密码。例如，您可以为 IMAP 拥有一套用户名和密码，而为其他所有服务拥有完全不同的另一套。您可以在 http://espresso.ee.sun.ac.za/~cabotha/pam_pwfile.html 找到此模块。 |
| pam_radius | Red Hat 5.2/6.0 | 仅支持 session 模块类型。为通过 RADIUS 认证的用户提供会话服务。 |
| pam_rhosts_auth | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。提供通过 ~/.rhosts 文件进行认证的功能。可以配置为允许或拒绝此类认证。 |
| pam_roottok | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。允许 root 用户在不要求密码的情况下访问。仅当与 sufficient 控制标志一起使用时才有意义。 |
| pam_securitty | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。仅适用于 root。检查 root 是否从 /etc/securitty 中列出的设备之一登录。如果是，返回成功；否则失败。 |
| pam_shells | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。如果用户的默认 shell 列在 /etc/shells 中，则验证用户。 |
| pam_stress | Red Hat 5.2/6.0 | 此模块用于调试和对支持 PAM 的应用程序进行压力测试。 |
| pam_tally | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。跟踪登录尝试次数，并可以基于指定数量的失败尝试拒绝访问。 |
| pam_time | Red Hat 5.2/6.0 | 仅支持 account 模块类型。根据 /etc/security/time.conf 中指定的用户、终端、服务和时间限制访问。 |
| pam_tcpd | 公开可用 | 仅支持 auth 模块类型。通过 /etc/hosts.allow 和 /etc/hosts.deny 实现 TCP_wrappers 风格的访问控制、日志记录和功能。TCP_wrappers 在第 10 章中讨论。该模块可从 http://web.tis.caltech.edu/~cachasse/pam_tcpd.html 获取。 |
| pam_unix_acct<br>pam_unix_auth<br>pam_unix_passwd<br>pam_unix_session | Red Hat 5.2/6.0 | 这些模块提供与 pam_pwdb 类似的功能，区别在于认证数据库是 /etc/passwd 或 NIS。 |
| pam_unix-new | 公开可用 | 将上述四个模块合为一体，并实现 pam_pwdb 的许多功能。可在 ftp://hunter.minuet.edu.pl/pub/users/baggins/PAM/ 获取。 |
| pam_warn | Red Hat 5.2/6.0 | 仅支持 auth 和 password 模块类型。此模块通过 syslog 工具生成包含远程用户和远程主机（如果可用）的日志消息。 |
| pam_wheel | Red Hat 5.2/6.0 | 仅支持 auth 模块类型。提供一种方式，将 root 的访问权限限制为 wheel 组的成员。 |
| pam_xauth | Red Hat 6.0 或公开可用 | 仅支持带有 optional 控制标志的 session 模块类型。此会话自动将 X Window System 魔术 cookie 传递给其他用户（例如，通过 su），从而允许有效的 UID 打开 X 应用程序，而无需使用 xhost 命令。 |

## 支持 PAM 的应用程序

表 5.16 列出了许多支持 PAM 的应用程序，这意味着该应用程序包含调用 PAM 所必需的调用。与表 5.15 一样，Red Hat 5.2/6.0 发行版中可用的应用程序会加以注明。

## 关于配置 PAM 的重要说明

本章对 PAM 进行了入门级介绍。文中描述了许多示例，并提供了一些使用技巧。然而，毫无疑问，你们中的许多人会有自己的配置想法。本节提供了一些简单但重要的关于为您的环境配置 PAM 的说明。

