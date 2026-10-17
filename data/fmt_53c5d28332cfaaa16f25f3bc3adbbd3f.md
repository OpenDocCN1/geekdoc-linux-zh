
| `migrate` | 仅在“auth”上下文中有意义；用于使用成功身份验证使用的密码更新 `smbpasswd` 文件。 |

| `smbconf=` file | 指定 `smb.conf` 文件的替代路径。 |

### 27.2.5.2 密码迁移配置

以下 PAM 配置展示了如何使用 `pam_smbpass` 将 Samba 的明文密码迁移为加密密码。与其他方法不同，这可以用于从未连接过 Samba 共享的用户：当用户通过 `ftp` 登录、使用 `ssh` 登录、收取邮件时，就会发生密码迁移，等等。

```
#%PAM-1.0
# password-migration
#
auth requisite pam_nologin.so
# 如果 pam_unix 成功，则调用 pam_smbpass。
auth requisite pam_unix.so
auth optional pam_smbpass.so migrate
account required pam_unix.so
password requisite pam_cracklib.so retry=3
password requisite pam_unix.so shadow md5 use_authtok try_first_pass
password optional pam_smbpass.so nullok use_authtok try_first_pass
session required pam_unix.so
```

### 27.2.5.3 成熟密码配置

以下是一个成熟的 `smbpasswd` 安装的示例 PAM 配置。`private/smbpasswd` 已完全填充，我们认为如果 SMB 密码不存在或与 UNIX 密码不匹配，则视为错误。

```
#%PAM-1.0
# password-mature
#
auth requisite pam_nologin.so
auth required pam_unix.so
account required pam_unix.so
password requisite pam_cracklib.so retry=3
password requisite pam_unix.so shadow md5 use_authtok try_first_pass
password required pam_smbpass.so use_authtok use_first_pass
session required pam_unix.so
```

### 27.2.5.4 Kerberos 密码集成配置

以下是一个示例 PAM 配置，展示了 `pam_smbpass` 与 `pam_krb5` 一起使用的情况。这对于既是 Samba PDC 又是 Kerberos 领域成员的系统可能很有用。

```
#%PAM-1.0
# kdc-pdc
#
auth requisite pam_nologin.so
auth requisite pam_krb5.so
auth optional pam_smbpass.so migrate
account required pam_krb5.so
password requisite pam_cracklib.so retry=3
password optional pam_smbpass.so nullok use_authtok try_first_pass
password required pam_krb5.so use_authtok try_first_pass
session required pam_krb5.so
```

## 27.3 常见错误

PAM 可能很挑剔，对配置错误也很敏感。这里我们来看看 Samba 邮件列表中的几个案例。

### 27.3.1 pam_winbind 问题

*一名用户报告道：我有以下 PAM 配置：*

**注意**

PAM 允许堆叠身份验证机制。此外，还可以将在一个 PAM 模块中获取的信息传递给 PAM 堆栈中的下一个模块。有关此环境中 PAM 特定功能的详细信息，请参阅您特定系统实现的文档。某些 Linux 实现还提供 `pam_stack.so` 模块，允许在一个中央文件中配置所有身份验证。基于更易于管理的理由，`pam_stack.so` 方法有一些忠实的追随者。不过，就像生活中所有的问题一样，每个决定都有取舍，因此您可能需要查看 PAM 文档以获取更有用的信息。

在下面的示例中，决定即使在基本的 Samba 身份验证中也使用 `smbpasswd` 数据库。这样的决定也可以针对 `passwd` 程序做出，从而允许使用 `passwd` 程序更改 `smbpasswd` 密码：

```
#%PAM-1.0
# samba 服务的 PAM 配置文件
#
auth     required    pam_smbpass.so nodelay
account  required    pam_pwdb.so audit nodelay
session  required    pam_pwdb.so nodelay
password required    pam_smbpass.so nodelay smbconf=/etc/samba.d/smb.conf
```

以下是特定 Linux 系统的 PAM 配置文件。默认条件使用 `pam_pwdb.so`。

```
#%PAM-1.0
# samba 服务的 PAM 配置文件
#
auth     required    pam_pwdb.so nullok nodelay shadow audit
account  required    pam_pwdb.so audit nodelay
session  required    pam_pwdb.so nodelay
password required    pam_pwdb.so shadow md5
```

`pam_smbpass` 模块，请参阅 Samba 源代码分发中 `source/pam_smbpass` 目录中的文档。

```
#%PAM-1.0
# login 服务的 PAM 配置文件
#
auth     required    pam_smbpass.so nodelay
account  required    pam_smbpass.so nodelay
session  required    pam_smbpass.so nodelay
password required    pam_smbpass.so nodelay
```

`auth required /lib/security/pam_securly.so`

`auth sufficient /lib/security/pam_winbind.so`

`auth sufficient /lib/security/pam_unix.so use_first_pass nullok`

`auth required /lib/security/pam_stack.so service=system-auth`

`auth required /lib/security/pam_winbind.so`

`account required /lib/security/pam_stack.so service=system-auth`

`account required /lib/security/pam_winbind.so`

`password required /lib/security/pam_stack.so service=system-auth`

> 当我打开一个带有 [Ctrl][Alt][F1] 的新控制台时，我无法使用我的用户“pittie”登录。我也尝试使用用户“science/pittie”，但也没用。

问题可能在于包含了 `pam_stack.so service=system-auth`。该文件通常包含许多内容，可能会重复你已经在做的事情。尝试注释掉用于 auth 和 account 的 `pam_stack` 行，看看是否有效。如果有效，请查看 `/etc/pam.d/system-auth`，并只将其中你需要的内容复制到你的 `/etc/pam.d/login` 文件中。或者，如果你希望所有服务都使用 Winbind，你可以将 Winbind 相关的内容放入 `/etc/pam.d/system-auth`。

### 27.3.2 Winbind 无法解析用户和组

> “我的 `smb.conf` 文件配置正确。我指定了 `idmap uid = 12000` 和 `idmap gid = 3000-3500`，并且 winbind 正在运行。当我执行以下操作时，一切正常。”

```
root# wbinfo -u
MIDEARTH\maryo
MIDEARTH\jackb
MIDEARTH\ameds
...
MIDEARTH\root
```

```
root# wbinfo -g
MIDEARTH\Domain Users
MIDEARTH\Domain Admins
MIDEARTH\Domain Guests
...
MIDEARTH\Accounts
```

“但这个命令失败了：”
