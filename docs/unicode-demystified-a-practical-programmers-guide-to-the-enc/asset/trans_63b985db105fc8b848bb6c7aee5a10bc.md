
用户验证技术在不同的应用程序之间保持一致。PAM 允许系统管理员在不触动应用程序的情况下更改特定应用程序的验证机制。

PAM 为各种系统登录服务（登录、ftp 等）提供验证。你可以利用 PAM 使用不同验证机制对系统登录服务进行验证的能力，例如 RSA、DCE、Kerberos 和智能卡。

从使用 `su` 登录到关闭系统，每当系统要求你输入密码（或因为系统信任你的身份而未要求密码）时，PAM 都让系统管理员能够配置验证过程成为可能，并让所有使用 PAM 进行验证的应用程序都拥有完全相同的配置过程。

存储在 `/etc/pam.d/` 中的配置文件描述了每个应用程序的验证程序。这些文件的名称通常与其所配置的应用程序名称相同或相似。例如，登录的验证是在 `/etc/pam.d/login` 中配置的。文件名就是该文件所配置的 PAM 服务名称。偶尔，一个文件可能为两个程序服务。

# 不要让自己锁在系统之外

正确编辑 PAM 配置文件需要细心和注意。一个小错误就可能让你被锁在电脑之外。为了避免此类问题，请务必始终保留你编辑的 PAM 文件的备份，彻底测试每次更改，并确保在安装更改后仍然可以登录。在完成之前，保持超级用户（Superuser）会话开启。当更改失败且无法登录时，使用超级用户将新编辑的文件替换为备份副本。

PAM 会对它遇到的任何错误发出警告，将其记录在 `/var/log/messages` 或 `/var/log/secure` 文件中。如果你试图弄清楚为什么更改后的 PAM 文件无法正常工作，请查看这些文件。为了防止向恶意用户提供不必要的信息，PAM 将错误消息发送到文件而不是屏幕。

PAM 服务与 `/etc/services` 文件之间没有关系。PAM 服务名称是每个应用程序赋予 PAM 的任意字符串；PAM 随后查找具有该名称的配置文件并使用它来控制如何进行验证。PAM 服务没有中央注册表。

# 配置文件、模块类型和控制标志位

以下是一个 PAM 配置文件的示例。注释行以井号 (`#`) 开头：

```
$ cat /etc/pam.d/login
#%PAM-1.0
auth      required      /lib/security/pam_securetty.so
auth      required      /lib/security/pam_stack.so service=system-auth
auth      required      /lib/security/pam_nologin.so
account   required      /lib/security/pam_stack.so service=system-auth
password  required      /lib/security/pam_stack.so service=system-auth
session   required      /lib/security/pam_stack.so service=system-auth
session   optional      /lib/security/pam_console.so
```

第一行是特殊注释；只有当发布了其他 PAM 格式时，它才有意义。在上述示例的第一行中，不要使用此以外的 `#`。

其余行告诉 PAM 作为验证过程的一部分执行某些操作：account、auth、password 或 session（表 17-19）。第二个是控制标志位（表 17-20），它指示行的其余部分包含 PAM 模块的路径以及该模块的任何参数。PAM 库本身使用 `/etc/pam.d` 文件来决定哪些模块处理工作。

| 模块类型 | 描述 | 控制 |
|---|---|---|
| auth | 验证 | 证明用户有权使用该服务。这可以使用密码或其他机制完成。 |
| account | 账户管理 | 确定已验证的用户是否被允许使用其尝试使用的的服务。（也就是说，账户是否过期？用户是否被允许在此时段使用此服务？） |
| password | 更改密码 | 更新验证机制，例如用户密码。 |
| session | 会话管理 | 在服务启动时进行设置（例如，用户登录时），并在服务结束时取消设置（例如，用户注销时）。 |

# 控制标志位

你可以使用表 17-20 列出的控制标志位关键字之一来选择控制标志位。

| required | |

验证成功需要成功。在栈中的所有模块执行后，将返回控制和失败结果。这种延迟在所有模块执行后才向调用程序报告结果的技术可以防止攻击者知道其验证失败的原因，并向他们提供更少的信息，使他们更难入侵。 |

| requisite | |

验证成功需要成功。当模块失败后，将中止后续模块处理并立即返回控制。这种技术可能会向攻击者暴露有关系统的信息。另一方面，如果它能防止用户在不安全的连接上提供密码，它可能会防止信息落入攻击者手中。 |

| sufficient | |

成功表示此模块类型已成功，并执行该类型的后续必需的模块。失败对于该模块类型的栈来说不是致命的。这种技术通常用于某种形式的验证已经足够好的情况：如果一种失败了，PAM 会尝试另一种。例如，当使用 `rsh` 连接到另一台计算机时，`pam_hosts` 首先检查你的连接是否可以在没有密码的情况下被信任。如果连接可以信任，`pam_hosts` 模块将报告成功。 |

| optional | |

结果通常被忽略。可选模块仅在当它是栈中唯一的模块时才相关。PAM 根据应用程序的要求使用每种模块类型。 |

# 示例

登录服务的验证栈部分示例如下：

```
$ cat /etc/pam.d/login
#%PAM-1.0
auth      required      /lib/security/pam_securetty.so
auth      required      /lib/security/pam_stack.so service=system-auth
auth      required      /lib/security/pam_nlogin.so
```

登录程序首先请求用户名，然后要求 PAM 运行此栈以验证用户。请参阅第 105 页的表 17-19 和第 106 页的表 17-20。

