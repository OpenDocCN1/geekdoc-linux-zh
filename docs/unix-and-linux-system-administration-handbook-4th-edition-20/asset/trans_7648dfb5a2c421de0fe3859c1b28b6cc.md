

# Rootly 条目

## 907

在 Linux 系统上，`chage` 程序用于控制密码有效期。通过 `chage`，管理员可以强制执行密码更改之间的最小和最大时间、密码过期日期、在密码过期前提醒用户的天数、账户被自动锁定前允许的未活动天数等。以下命令将密码更改之间的天数设置为 2 天，最大天数设置为 90 天，过期日期设为 2010 年 7 月 31 日，并在过期前 14 天提醒用户：

![](img/579efec8c67772f31ecf34844bbb71a2_955_0.png)

```
$ sudo chage -m 2 -M 90 -E 2010-07-31 -W 14 ben
```

有关用户账户设置的更多详细信息，请参阅第 7 章。

其他系统实现密码有效期的方式有所不同，通常粒度较低。在 Solaris 下，您可以在 `/etc/default/password` 中设置密码有效期偏好。HP-UX 系统的密码有效期通过 `smc` 控制台控制，而 AIX 则在 `/etc/security/user` 文件中配置。

# 组登录与共享登录

任何被多个人使用的登录账户都是坏事。组登录（例如“guest”或“demo”）是黑客可以藏身立足的，在许多场景下，联邦法规（如 HIPAA）中是被禁止的。不要在您的站点允许此类登录。然而，技术控制无法阻止用户共享密码，因此强制执行是最佳策略。

# 用户 shell

从理论上讲，您可以将用户账户的 shell 设置为任何程序，包括自定义脚本。在实践中，使用 `bash` 和 `tsch` 等标准以外的 shell 是一种危险的做法，对于以脚本作为 shell 的无密码登录，风险更大。如果您产生了创建此类登录的冲动，可以考虑使用无密码的 SSH 密钥对。

# Rootly 条目

root 登录的唯一特征是其 UID 为 0。由于 `/etc/passwd` 文件中存在存在使用该 UID 的条目，因此可能有多种方法登录 root。

黑客在获取 root shell 后，安装后门的常用方法是将 root 登录编辑到 `/etc/passwd` 中。`who` 等程序引用的是 `utmp` 中存储的名称而非拥有登录 shell 的 UID，因此它们无法暴露那些看似是无辜用户但实际上以 UID 0 登录的黑客。

不要允许 root 远程登录，即使是通过标准的 root 账户。在 OpenSSH，您可以在 `/etc/ssh/sshd_config` 文件中将 `PermitRootLogin` 配置选项设置为 `No` 以强制执行此限制。

在 Solaris 上，您可以使用 `/etc/default/login` 中的 `CONSOLE=/dev/console` 来禁止控制台以外位置的 root 登录。

![](img/579efec8c67772f31ecf34844bbb71a2_955_1.png)

![](img/579efec8c67772f31ecf34844bbb71a2_955_2.png)

不要允许 root 远程登录，即使是通过标准的 root 账户。在 OpenSSH 下，您可以在 `/etc/ssh/sshd_config` 文件中将 `PermitRootLogin` 配置选项设置为 `No` 以强制执行此限制。

在 Solaris 上，您可以使用 `/etc/default/login` 中的 `CONSOLE=/dev/console` 来禁止控制台以外位置的 root 登录。

![](img/579efec8c67772f31ecf34844bbb71a2_955_1.png)

![](img/579efec8c67772f31ecf34844bbb71a2_955_2.png)

（注：此处原文存在内容重复）

在 OpenSSH 下，您可以在 `/etc/ssh/sshd_config` 文件中将 `PermitRootLogin` 配置选项设置为 `No` 以强制执行此限制。

在 Solaris 上，您可以使用 `/etc/default/login` 中的 `CONSOLE=/dev/console` 来禁止控制台以外位置的 root 登录。

![](img/579efec8c67772f31ecf34844bbb71a2_955_1.png)

![](img/579efec8c67772f31ecf34844bbb71a2_955_2.png)

# 安全

不要允许 root 远程登录，即使是通过标准的 root 账户。在 OpenSSH 下，您可以在 `/etc/ssh/sshd_config` 文件中将 `PermitRootLogin` 配置选项设置为 `No` 以强制执行此限制。

在 Solaris 上，您可以使用 `/etc/default/login` 中的 `CONSOLE=/dev/console` 来禁止控制台以外位置的 root 登录。

![](img/579efec8c67772f31ecf34844bbb71a2_955_1.png)

![](img/579efec8c67772f31ecf34844bbb71a2_955_2.png)

## 22.5 PAM

PAM 代表“可插认证模块”（Pluggable Authentication Modules）。PAM  own决定了认证模块如何交互。

- **required**：如果模块失败，整个栈将失败。如果成功，则继续执行。
- **sufficient**：如果模块成功，整个栈将立即成功。如果失败，则继续执行。
- **requisite**：如果模块失败，整个栈立即失败。如果成功，则继续执行。
- **optional**：如果模块失败，只有在没有其他 `sufficient` 模块成功的情况下栈才会失败。
- **include**：包含另一个 PAM 配置文件。

模块在文件中的顺序至关重要。例如，`required` 模块应该放在 `sufficient` 模块之前，以确保执行检查。

# 表 22.1 PAM 控制标志

| 标志 | 失败时停止 | 成功时停止 | 注释 |
| :--- | :--- | :--- | :--- |
| binding | 否 | 是 | 类似于 sufficient，但不会导致栈失败 |
| include | | 否 | 在此处包含另一个配置 |
| optional | 否 | 否 | 仅当该模块是唯一模块时显著 |
| required | 否 | 否 | 失败会导致栈失败 |
| requisite | 是 | 否 | 类似于 required，但会失败栈 |
| sufficient | 否 | 是 | 名称有点误导；请参见注释 |

这些不同控制标志之间的交互可能非常复杂，但在大多数情况下，遵循标准规则就足够了。Linux 在处理密码方面使用的一组略有不同的标志，但逻辑仍然是相同的。如果您要修改系统的安全设置，请确保您彻底了解该系统并双重核对细节。

例如，这里有一段典型的 PAM 配置片段：

```
# login service

login auth requisite pam_authtok_get.so.1
login auth required pam_dhkeys.so.1
login auth required pam_unix_cred.so.1
login auth required pam_unix_auth.so.1
login auth required pam_dial_auth.so.1
```

