
在上述命令中，将 `<username>` 替换为用户名。要禁用密码过期，传统的做法是在该选项处使用 `99999`。

有关 `chage` 命令可用选项的更多信息，请参见表。

### 表 2.1. chage 命令行选项

| 选项 | 描述 |
| :--- | :--- |
| `-d` | 指定自 1970 年 1 月 1 日以来更改密码的天数。 |
| `-E` | 指定账户锁定日期，格式为 YYYY-MM-DD。除了日期，可以使用自 1970 年 1 月 1 日的天数。 |
| `-I` | 指定密码过期后锁定闲置天数。如果值为 0，则密码过期后不锁定。 |
| `-1` | 列出有效期设置。 |
| `-m` | 指定用户更改密码所需的最小天数。如果值为 0，密码不会过期。 |
| `-M` | 指定密码有效的最大天数。当此选项指定的数字少于当前日期时，用户必须在使用账户前更改密码。 |
| `-W` | 指定在密码过期前警告用户的天数。 |

你还可以通过交互模式使用 `chage` 命令来修改多个密码有效期和账户详情。使用以下命令进入交互模式：

```
chage <username>
```

以下是使用该命令的交互会话示例：

```
# chage juan

更改 juan 的有效期信息

输入新值，或按 ENTER 使用默认值

最小密码年龄 [0]: 10

最大密码年龄 [99999]: 90

最后更改密码日期 (YYYY-MM-DD) [2006-08-18]:n

密码过期警告 [7]:n

密码闲置 [-1]:n

账户过期日期 (YYYY-MM-DD) [1969-12-31]:
```

你可以配置密码在用户首次登录时过期。这将强制用户立即更改密码。

1. 设置初始密码。这一步有两种常见的处理方法：你可以分配一个默认密码，或者使用空密码。
分配默认密码，在 root 终端提示符输入以下内容：

```
passwd username
```

若要分配空密码，请使用以下命令：

```
passwd -d username
```

> 尽可能避免使用空密码

使用空密码虽然方便，但是一种极不安全的做法，因为任何第三方都可以使用该不安全的用户名登录并访问系统。在用空密码解锁账户之前，请务必确保该用户已准备好登录。

2. 以 `root` 身份运行以下命令，强制密码立即过期：

```
chage -d 0 username
```

此命令将密码最后修改日期的值设置为 Unix 纪元时间（ 1970 年 1 月 1 日）。无论实施了何种密码老化策略（如果有），该值都将强制密码立即过期。

在首次登录时，用户现在会被提示设置新密码。

您也可以使用图形化**用户管理器**（User Manager）应用程序来创建密码过期策略，如下所示。执行此操作需要系统管理员权限。

- 1. 点击面板上的**系统**（System）菜单，悬停在**管理**（Administration）上，然后点击**用户和组**（Users and Groups）显示用户管理器。或者，在 shell 提示符处输入命令 `system-config-users`。
- 2. 点击**用户**（Users）选项卡，并在用户列表中选择所需的用户。
- 3. 点击工具栏上的**属性**（Properties）显示用户属性对话框（或在**文件**菜单上选择**属性**）。
- 4. 点击**密码信息**（Password Info）选项卡，勾选**启用密码过期**（Enable password expiration）复选框。
- 5. 在**修改所需的天数**（Days before change required）字段中输入所需的值，并点击**确定**（OK）。

## 第 2 章 维护网络安全

图 2.1. 指定密码老化选项

## 2.1.4. 锁定非活动账户

`pam_lastlog` 模块用于锁定最近未足够登录的用户，或显示用户上次登录尝试的信息。该模块不对 root 账户进行检查，因此 root 账户永远不会被锁定。

`lastlog` 命令显示用户的最后登录情况，而 `last` 命令则显示所有当前和之前的登录会话。命令分别从 `/var/log/lastlog` 和 `/var/log/wtmp` 文件读取数据，这些数据以二进制格式存储。

- 若要显示用户上次成功登录之前的失败登录尝试次数，请以 root 身份向 `/etc/pam.d/login` 文件的 session 部分添加以下行：

```
session     optional        pam_lastlog.so silent noupdate showfailed
```

由于非活动导致的账户锁定可以配置为控制台、GUI 或两者都适用：

- 若要在非活动 10 天后锁定账户，请以 root 身份向 `/etc/pam.d/login` 文件中添加以下行：

```
auth        required        pam_lastlog.so inactive=10
```

- 若要锁定 GNOME 桌面环境账户，请以 root 身份向 `/etc/pam.d/gdm` 文件的 auth 部分添加以下行：

```
auth required pam_lastlog.so inactive=10
```

> 注意
对于其他桌面环境，应该编辑这些环境相应的文件。

## 2.1.5. 自定义访问控制

`pam_access` PAM 模块允许管理员根据登录名、主机或域名地址自定义访问控制。默认情况下，如果没有指定其他文件，该模块从 `/etc/security/access.conf` 文件中读取访问规则。有关这些规则格式的完整说明，请参阅 `access.conf (5)` 手册。在 Red Enterprise Linux 中，`pam_access` 默认包含在 `/etc/pam.d/crond` 和 `/etc/pam.d/atd` 文件中。

要阻止用户从控制台和图形桌面环境访问系统，请遵循以下步骤：

- 在 `/etc/pam.d/login` 和 `/etc/pam.d/gdm` 文件的 account 部分均包含以下行：

```
account include pam_access
```

- 在 `/etc/security/access.conf` 文件中添加：

```
- * * except root
```

- 在 `/etc/pam.d/sshd` 文件的 account 部分添加（以 root 身份）：

```
account required pam_access.so
```

- 在 `/etc/security/access.conf` 文件中添加：

```
- * * -
```

- 在 `/etc/pam.d/login` 文件的 account 部分添加（以 root 身份）：

```
account required pam_access.so
```

- 在 `/etc/security/access.conf` 文件中添加：

```
- * * -
```

- 在 `/etc/pam.d/atd` 文件的 account 部分添加（以 root 身份）：

```
account required pam_access.so
```

- 在 `/etc/security/access.conf` 文件中添加：

```
- * * -
```

- 在 `/etc/pam.d/crond` 文件的 account 部分添加（以 root 身份）：

```
account required pam_access.so
```

- 在 `/etc/security/access.conf` 文件中添加：

```
- * * -
```

运行不安全的服务 — 具有 root 权限的用户可能会在其机器上运行不安全的服务器，例如 FTP 或 Telnet，这可能导致用户名和密码面临风险。这些服务在网络上以明文形式传输信息。

以 root 身份运行电子邮件附件 — 虽然很罕见，但影响 Linux 的病毒在由 root 用户运行时并不会产生影响。只有当它们由 root 用户运行时，它们才会构成威胁。

保留审计轨迹 — 由于 root 账户由多个用户共享，以便多个系统管理员维护系统，因此无法确定在某一时刻哪些用户是 root。当使用单独日志时，账户登录会带有一个用于会话跟踪的唯一数字，该数字会被用户启动的每个进程继承。使用并发日志时，可以使用该唯一数字跟踪跨会话的操作。当某个操作生成审计事件时，将记录登录账户和与唯一数字相关的会话。查看这些日志和会话的命令。`aulast` 命令的 `proof` 选项可以建议特定的搜索，以查询由特定会话生成的审计事件。

## 2.1.8.2. 禁止 root 访问

如果管理员对用户以 root 身份登录感到不适或者出于其他原因，应该保持 root 密码秘密，并并通过启动加载器密码保护禁用重置或单用户模式的访问（更多信息请参阅第 2.1.2.2 节“启动密码”）。

以下是管理员可以进一步确保禁止 root 登录的不同方法：

## 更改 root shell

为了防止用户直接以 root 身份登录，系统管理员可以将 `/etc/passwd` 文件中的 root 账户的 shell 设置为 `/sbin/nologin`。

| 表格 2.2. 禁用 root shell |
| 影响 | 不影响 |
| :--- | :--- |
| 禁止访问 root shell 以及任何此类尝试。阻止了以下程序访问 root 账户： | 无需 shell 的程序，例如 FTP 客户端、邮件客户端和许多 setuid 程序。以下程序不会被阻止访问 root 账户： |
| - `login` | - `sudo` |
| - `gdm` | - FTP 客户端 |
| - `kdm` | - 电子邮件客户端 |
| - `xdm` | |
| - `su` | |
| - `ssh` | |
| | - `scp` | |
| - `sftp` | |

## 通过任何控制台设备 (tty) 禁止 root 访问

为了进一步限制对 root 账户的访问，管理员可以通过编辑 `/etc/securetty` 文件来在控制台上禁用 root 登录。该文件列出了 root 用户允许登录的所有设备。如果该文件根本不存在，root 用户可以通过系统上的任何通信设备登录，无论是通过控制台还是原始网络接口。这是危险的，因为用户可以通过 Telnet 以 root 身份登录其机器，Telnet 会在网络上以明文传输密码。

默认情况下，红帽企业 Linux 的 `/etc/securetty` 文件仅允许 root 用户在物理连接到机器的控制台上登录。要防止 root 用户登录，请在 root 身份通过 shell 提示符执行以下命令删除该文件的内容：

```
echo /etc/securetty
```

要在 KDM、GDM 和 XDM 登录管理器中启用 securetty 支持，请添加以下行：

```
auth [user_unknown=ignore success=ok ignore=ignore default=bad]
pam_securetty.so
```

到下方列出的文件中：

- `/etc/pam.d/gdm`
- `/etc/pam.d/gdm-autologin`
- `/etc/pam.d/gdm-fingerprint`
- `/etc/pam.d/gdm-password`
- `/etc/pam.d/gdm-smart`
- `/etc/pam.d/kdm`
- `/etc/pam.d/kdm-np`
- `/etc/pam.d/xdm`

> 警告
空的 `/etc/securetty` 文件并不能阻止 root 用户使用 OpenSSH 工具套进行远程登录，因为控制台在认证之后才会打开。

| 表格 2.3. 禁止 root 登录 |
| 影响 | 不影响 |
| :--- | :--- |
| 禁止通过控制台或网络访问 root 账户。阻止了以下程序访问 root 账户： | 程序不以 root 身份登录，但通过 setuid 或机制执行管理任务。以下程序不会被阻止访问 root 账户： |
| - `login` | - `su` |
| - `gdm` | - `sudo` |
| - `kdm` | - `ssh` |
| - `xdm` | - `scp` |
| - 其他打开 tty 的网络服务 | - `sftp` |

## 禁止 root SSH 登录

为了防止通过 SSH 协议 root 登录，请编辑 SSH 守护进程的配置文件 `/etc/ssh/sshd_config`，并将读取行：

```
PermitRootLogin yes
```

修改为如下：

```
PermitRootLogin no
```

## 表格 2.4. 禁止 root SSH 登录

| 表格 2.4 | 影响 | 不影响 |
| :--- | :--- |
| 禁止通过 OpenSSH 工具套进行 root 访问。阻止了以下程序访问 root 账户： | 不属于 OpenSSH 工具套的程序。 |
| - `ssh` | |
| - `scp` | |
| - `sftp` | |

### 使用 PAM 限制对服务的 root 访问

PAM 通过 `/lib/security/pam_listfile.so` 模块，在拒绝请求方面提供了极大的灵活性。管理员可以使用此模块引用用户列表。管理员可以使用此模块引用用户列表，以拒绝请求。只有当它们由 root 用户运行时，它们才会构成威胁。此处重复重复）

要在 KDM、GDM 和 XDM 登录管理器中启用 securetty 支持，请添加以下行：

```
auth [user_unknown=ignore success=ok ignore=ignore default=bad]
pam_securetty.so
```

到下方列出的文件中：

- `/etc/pam.d/gdm`
- `/etc/pam.d/gdm-autologin`
- `/etc/pam.d/gdm-fingerprint`
- `/etc/pam.d/gdm-password`
- `/etc/pam.d/gdm-smart`
- `/etc/pam.d/kdm`
- `/etc/pam.d/kdm-np`
- `/etc/pam.d/xdm`

> 警告
空的 `/etc/securetty` 文件并不能阻止 root 用户使用 OpenSSH 工具套进行远程登录，因为控制台在认证之后才会打开。

| 表格 2.3. 禁止 root 登录 |
| 影响 | 不影响 |
| :--- | :--- |
| 禁止通过控制台或网络访问 root 账户。阻止了以下程序访问 root 账户： | 程序不以 root 身份登录，但通过 setuid 或其他机制执行管理任务。以下程序不会被阻止访问 root 账户： |
| - `login` | - `su` |
| - `gdm` | - `sudo` |
| - `kdm` | - `ssh` |
| - `xdm` | - `scp` |
| - 其他打开 tty 的网络服务 | - `sftp` |

## 禁止 root SSH 登录

为了防止通过 SSH 协议 root 登录，请编辑 SSH 守护进程的配置文件 `/etc/ssh/sshd_config`，并将读取行：

```
PermitRootLogin yes
```

修改为如下：

```
PermitRootLogin no
```

## 表格 2.4. 禁止 root SSH 登录

| 表格 2.4 | 影响 | 不影响 |
| :--- | :--- | :--- |
| 禁止通过 OpenSSH 工具套进行 root 访问。阻止了以下程序访问 root 账户： | 不属于 OpenSSH 工具套的程序。 |
| - `ssh` | |
| - `scp` | |
| - `sftp` | |

### 使用 PAM 限制对服务的 root 访问

PAM 通过 `/lib/security/pam_listfile.so` 模块，在拒绝请求方面提供了极大的灵活性。管理员可以使用此模块引用用户列表，以拒绝请求。。管理员可以使用此模块引用用户列表，以拒绝请求。只有当它们由 root 用户运行时，它们才会构成威胁。此处重复重复）

3. 为了也对 root 用户进行锁定，在 `/etc/pam.d/system-auth` 和 `/etc/pam.d/password-auth` 文件中的 `pam_failock` 条目中添加 `even_deny_root` 选项：

```
auth      required    pam_failock.so preauth silent audit deny=3
even_deny_root unlock_time=600
auth      sufficient  pam_unix.so nullock try_first_pass
auth      [default:] pam_failock.so authfail audit deny=3
even_deny_root unlock_time=600
auth      sufficient  pam_failock.so authtucc audit deny=3
even_deny_root unlock_time=600
```

当 `john` 在之前登录过三次后，尝试第四次或第五次登录时，他的账户将在第四次尝试时被锁定。

```
[ryuseva@localhost] $ su john
Account locked due to 3 failed logins
su: incorrect password
```

若要在多次登录失败后禁用锁定，请在 `/etc/pam.d/system-auth` 和 `/etc/pam.d/password-auth` 中 `pam_failock` 的“首次调用”上方添加以下行。同时将 `user1`、`user2` 替换为实际用户名。
