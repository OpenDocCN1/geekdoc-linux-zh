
![](img/243613168ac865b539f12460d966088e_532_0.png)

`/etc/pam.d` 中的文件列出了每个应用程序执行每项任务所使用的模块集。每个这样的模块集称为认证堆栈或简称为堆栈。`PAM` 按顺序一次调用一个模块，从堆栈的顶部（配置文件中列出的第一个模块）到底部。每个模块向 `PAM` 报告成功或失败。当配置文件中的所有模块堆栈（有一些例外）都被调用后，`PAM` 库向应用程序报告成功或失败。

`PAM` 提供共享库，将认证代码与应用代码分离，而不是将认证代码构建到每个应用程序中。用户认证技术在应用程序之间保持一致。通过这种方式，`PAM` 使系统管理员能够在不修改应用程序的情况下更改特定应用程序的认证机制。

`PAM` 为多种系统入口服务（如 `login`、`ftp`、`su` 和 `sudo`）提供认证。你可以利用其堆栈认证模块的能力，将系统入口服务与不同的认证机制（如 `RSA`、`DCE`、`Kerberos` 和智能卡）集成。

从登录到使用 `su` 或 `sudo`，再到系统关机，每当你需要输入密码（或者因为系统信任你所说的身份而不被要求输入密码）时，`PAM` 使系统管理员能够配置认证过程。它还使所有使用 `PAM` 进行认证的应用程序的配置过程基本上保持一致。

# 不要创建 /etc/pam.conf

> **注意** 你可能在其他系统中遇到过 `PAM`，那里所有配置都安排在单个文件（`/etc/pam.conf`）中。此文件在 `Fedora/RHEL` 系统中不存在。相反，`/etc/pam.d` 目录包含单独的配置文件，每个使用 `PAM` 的应用程序一个。这种设置使得安装和卸载使用 `PAM` 的应用程序变得容易，因为你不需要每次都修改 `/etc/pam.conf` 文件。如果在未使用此文件的系统上创建 `/etc/pam.conf` 文件，`PAM` 配置可能会变得混乱。不要使用来自不同系统的 `PAM` 文档。此外，某些支持 `PAM` 的系统上不可用 `requisite` 控制标志。

**错误消息** `PAM` 会警告你遇到的错误，并将其记录到 `/var/log/messages` 或 `/var/log/secure`。如果你正在尝试弄清楚为什么修改后的 `PAM` 文件未正常工作，请查看这些文件。为了防止恶意用户看到有关 `PAM` 的信息，`PAM` 将错误消息发送到文件而不是屏幕。

## 更多信息

- `Linux-PAM` 系统管理员指南：`/usr/share/doc/pam-1.1.6/html/Linux-PAM_SAG.html`
- `PAM` 模块：`pam` 手册页，`apropos pam` 列出描述 `PAM` 模块的手册页
- 网页描述：`www.netbsd.org/docs/guide/en/chap-pam.html`
- 用户认证 `HOWTO`

# 配置文件、模块类型和控制标志

**登录模块** 以下是一个 `PAM` 配置文件的示例。注释行以井号（`#`）开头。

```text
$ cat /etc/pam.d/login
#PAM-1.0
auth  [user_unknown=ignore success=ok ignore=ignore default=bad] pam_security.so
auth      substack      system-auth
auth      include       postlogin
account   required      pam_nologin.so
account   include       system-auth
password  include       system-auth
# pam_selinux.so close should be the first session rule
session   required      pam_selinux.so close
session   required      pam_logind.so
session   optional      pam_console.so
# pam_selinux.so open should only be followed by sessions to be executed in the user context
session   required      pam_selinux.so open
session   required      pam_namespace.so
session   optional      pam_keyinit.so force revoke
session   include       system-auth
session   include       postlogin
-session  optional      pam_ck_connector.so
```

第一行是特殊注释；只有当发布另一种 `PAM` 格式时，它才会有意义。除了前面示例的第一行外，请勿使用 `#`。

其余的行告诉 `PAM` 在认证过程中执行某些操作。每行的第一个单词是模块类型指示器：`account`、`auth`、`password` 或 `session`（表 10-3）。第二个是控制标志（表 10-4），指示如果认证失败，`PAM` 应采取的操作。该行的其余部分包含 `PAM` 模块（位于 `/lib64/security` 或 `/lib/security` 中）的名称以及该模块的任何参数。`PAM` 库本身使用 `/etc/pam.d` 文件来确定将工作委托给哪些模块。控制标志为 `include` 的行包含第三个字段中指定的文件。

### 表 10-3 模块类型指示器

| 模块类型 | 描述 | 控制 |
| :--- | :--- | :--- |
| `account` | 账户管理 | 确定已认证的用户是否允许使用其试图使用的服务。（即，账户是否已过期？该用户在此时间段是否允许使用此服务？） |
| `auth` | 认证 | 证明用户有权使用该服务；使用密码或另一种机制。 |
| `password` | 密码修改 | 更新认证机制，如用户密码。 |
| `session` | 会话管理 | 在服务启动时（如用户登录时）设置内容，并在服务终止时（如用户注销时）清理内容。 |

你可以使用表 10-4 中列出的控制标志关键字之一来设置控制标志。

### 表 10-4 控制标志关键字

| 关键字 | 标志功能 |
| :--- | :--- |
| `required` | 认证成功需要成功。在所有模块执行完毕后，返回控制和失败结果。延迟向调用程序报告直到所有模块都执行完毕的技术可能使攻击者无法确切知道导致其认证尝试失败的原因，并告知他们更少的系统信息，从而增加他们入侵的难度。 |
| `requisite` | 认证成功需要成功。进一步的模块处理被中止，并在模块失败后立即返回控制。该技术可能会向攻击者暴露有关系统的信息。然而，如果它防止用户在不可靠连接上提供密码，它可能会阻止信息落入攻击者手中。 |

## 表 10-4 控制标志关键字（续）

| 关键字 | 标志功能 |
| :--- | :--- |
| `sufficient` | 成功表示此类型的模块已成功；此类型的后续 `required`（必需）模块将不再执行。失败对于此类型的模块栈并不致命。这种技术通常用于当某种身份验证方式已经足够好的情况：如果一个失败了，`PAM` 会尝试另一种。例如，当你使用 `su` 提升权限时，`/etc/pam.d/su` 首先使用 `pam_rootok` 检查你是否以 UID 为 0（`root` 权限）运行。由于 `su` 调用 `pam_rootok` 时使用的控制标志为 `sufficient`，如果你以 UID 为 0 运行，`pam_rootok` 模块将报告成功，并且 `PAM` 会立即向调用它的 `su` 实用程序报告成功。如果你没有以 `root` 权限运行，`PAM` 将重新进行身份验证并要求输入密码。如果第二次身份验证成功，`PAM` 将忽略 `pam_rootok` 模块报告失败的事实。如果两个模块都失败，`PAM` 将向调用它的 `su` 实用程序报告失败。 |
| `optional` | 结果通常被忽略。可选模块仅当它是特定服务的模块栈上唯一的模块时才相关。 |

`PAM` 根据应用程序的请求使用每种模块类型。也就是说，应用程序分别要求 `PAM` 进行身份验证、检查账户状态、管理会话以及更改密码。`PAM` 使用 `/lib64/security` 或 `/lib/security` 目录中的一个或多个模块来完成这些任务。

## 示例

登录服务的身份验证栈的一部分如下所示：

```bash
$ cat /etc/pam.d/login
auth [user_unknown=ignore success=ok ignore=ignore default=bad] pam_security.so
auth include system-auth
account required pam_nologin.so
...
```

`login` 实用程序首先要求输入用户名，然后调用 `PAM` 运行此栈来对用户进行身份验证。请参阅表 10-3 和表 10-4。

1. `PAM` 首先调用 `pam_security`（安全 tty；`pam_security` man 页）作为身份验证（`auth`）模块，以确保 `root` 用户仅从允许的终端登录。此模块查看 `/etc/security` 文件中列出的允许名为 `root` 的用户登录的终端列表。因此，`PAM` 实现了长期以来 UNIX 不允许 `root` 使用 `telnet` 登录系统的做法（`telnet` 使用 `login` 进行身份验证）。这项技术未被使用，但可以添加到 `sshd`、`vsftpd` 和其他 `PAM` 配置文件中。
   控制标志字段中的括号（`[ ]`）内是*值*=*动作*对。当模块返回*值*时，`PAM` 评估*动作*。在示例中，当模块返回 `user_unknown` 时，运行该模块的结果被忽略，而当模块返回 `success` 时，用户被允许继续身份验证。有关详细信息，请参见 `pam_security` 的 `man` 页。
   如果身份验证栈要成功，`pam_security` 模块必须成功。只有当有人试图从未经身份验证的终端以 `root` 身份登录时，`pam_security` 模块才会报告失败。否则（如果正在验证的用户名不是 `root`，或者用户名是 `root` 但登录尝试是从安全终端进行的），`pam_security` 模块报告成功。
   `PAM` 内部的成功和失败是仅适用于 `PAM` 的抽象概念。它们不等于操作系统其他地方使用的“true”和“false”。
2. 接下来，`PAM` 包含 `/etc/pam.d/system-auth` 文件（`system-auth` `man` 页）。此文件提供了调用 `PAM` 的通用接口。
3. `pam_nologin` 模块（`pam_nologin` `man` 页）确保如果 `/etc/nologin` 文件存在，则仅允许 `root` 用户登录。（也就是说，只有当 `/etc/nologin` 不存在或 `root` 用户正在登录时，`pam_nologin` 模块才报告成功。）因此，当系统计划在未来不久关机时，系统会阻止用户登录，以免他们在系统关机前一刻才登录进来。

`account` 模块类型的工作方式类似于 `auth` 模块类型，但它在用户经过身份验证后调用；它作为额外的安全检查或要求，用户必须满足这些要求才能访问系统。例如，`account` 模块可能强制执行用户仅在工作时间内登录的策略，或检查密码是否已过期。

`session` 模块类型设置并拆除会话（例如挂载和卸载用户的主目录）。一个常见的 `session` 模块是 `pam_console` 模块，它专门针对在物理控制台而非远程登录的用户进行系统设置。本地用户可以访问闪存驱动器、DVD 驱动器、声卡，有时还可以访问系统管理员定义的其他设备。

`password` 模块类型有点不寻常：栈中的所有模块都会被调用一次，并被告知获取存储密码所需的所有信息到持久内存（如磁盘），但实际并不存储它。如果确定无法或不应存储密码，模块将报告失败。如果栈中的所有 `password` 模块都报告成功，它们会被第二次调用，并被告知将第一次通过时获得的密码存储到持久内存中。`password` 模块负责更新认证信息（即更改用户的密码）。

任何单个模块都可以充当多种模块类型；许多模块可以充当所有四种模块类型。例如，`pam_unix` 可以作为 `auth` 模块调用，以对照 `passwd` 和 `shadow` 文件检查用户名和密码；作为 `account` 模块检查密码过期；作为 `password` 模块更新密码（即如果 `login` 提示 *your password has expired, enter a new password*）；或者作为 `session` 模块记录登录和注销时间戳用于 `wtmp`（供 `last` 实用程序使用）。

## 修改 PAM 配置

### 不要将自己锁在系统之外

> **注意** 正确编辑 `PAM` 配置文件需要仔细注意。很容易因错误而将自己锁在系统之外。为避免此问题，请保留你所编辑的 `PAM` 配置文件的备份副本，彻底测试每一个更改，并确保在更改安装后你仍能登录。直到测试完成之前，请保持一个 `root` shell 开启（使用 `su` 或 `sudo -1`）。如果更改失败且你无法登录，请使用 `root` shell 用备份副本替换新编辑的文件。

某些 UNIX 系统要求用户必须是 `wheel` 组的成员才能使用 `su` 命令。虽然 `Fedora/RHEL` 默认未配置为此方式，但 `PAM` 允许你通过编辑 `/etc/pam.d/su` 文件来更改此行为：

```bash
$ cat /etc/pam.d/su
...
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth		sufficient			pam_wheel.so trust use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
#auth		required		pam_wheel.so use_uid
```

`su` 模块的行中包含注释，这些注释包含了允许仅 `wheel` 组中的用户使用 `su`（`required`）以及允许 `wheel` 组成员不提供密码即可运行 `su`（`sufficient`）所需的行。当希望系统遵循其中一条规则时，取消其中一行的注释。

## 设置服务器

本节讨论在设置服务器时你可能需要处理的问题：如何编写配置文件；如何指定主机和子网；如何使用 `rpcbind`、`rpcinfo` 和 TCP 包装器（`hosts.allow` 和 `hosts.deny`）；以及如何设置 `chroot` 监狱。第 13 章和第 18–26 章涵盖设置特定服务器；第 16 章讨论设置局域网（`LAN`）。

## 配置文件中的标准规则

大多数配置文件通常命名为 `.conf`，依赖于以下约定：

- 空行被忽略。
- 一行中任何位置的 `#` 开始一个注释，该注释持续到行尾。注释被忽略。
  - 如果名称中包含空格，你必须通过在其前面添加反斜杠（`\）` 或使用单引号或双引号将整个名称括起来来引用该空格。
  - 为了使长行更易于阅读和编辑，您可以将它们拆分为几行较短的行。要拆分一行，请立即在反斜杠（`\）` 后插入一个新行（在文本编辑器中按 `RETURN` 键）。如果您在空格之前或之后插入新行，可以缩进后续行以便于阅读。请勿在 Windows 机器上以这种方式拆分行，因为新行可能无法正确转义（Windows 使用 `RETURN-LINEFEED` 组合来结束行）。

不符合这些约定的配置文件将在文本中注明。

## 指定客户端

表 10-5 展示了指定主机或子网的一些常见方法。在大多数情况下，您可以通过用空格分隔它们的规格来指定多个主机或子网。

### 表 10-5 指定客户端

| 客户端名称模式 | 匹配内容 |
| :--- | :--- |
| `n.n.n.n` | 一个 IP 地址。 |
| 名称 | 一个主机名，可以是本地的或远程的。 |
| 以 `.` 开头的名称 | 匹配以指定字符串结尾的主机名。例如，`example.com` 匹配名为 `kudos.example.com` 和 `speedy.example.com` 的系统（以及其他名称）。 |
| 以 `.` 结尾的 IP 地址 | 匹配以指定数字开头的主机地址。例如，`192.168.0.` 匹配 `192.168.0.0–192.168.0.255`。如果省略末尾的句点，此格式不起作用。 |
| `n.n.n.n/m.m.m.m` 或 `n.n.n.n/mm` | 指定子网的 IP 地址和网络掩码。 |
| 以 `/` 开头 | 包含一个或多个如本表中指定的名称或地址的文件绝对路径名。 |

| 通配符 | 匹配内容 |
| :--- | :--- |
| `*` 和 `?` | 匹配简单主机名或 IP 地址中的一个（`?`）或多个（`*`）字符。这些通配符不匹配域名中的句点。 |
| `ALL` | 始终匹配。 |
| `LOCAL` | 匹配不包含句点的任何主机名。 |

| 运算符 | 匹配内容 |
| :--- | :--- |
| `EXCEPT` | 匹配前列表中不在后列表中的任何内容。例如，`a b c d EXCEPT c` 匹配 `a`、`b` 和 `d`。因此，您可以使用 `192.168. EXCEPT 192.168.0.1` 来匹配所有以 `192.168.` 开头的 IP 地址，但 `192.168.0.1` 除外。 |
  - 以下每个示例指定了一个或多个系统：
    - `10.10.` 匹配所有 IP 地址以 `10.10.` 开头的系统
