
## 图 10-10

PAM 配置文件位于 /etc/pam.d 目录

```
[root@server1 ~]# ls /etc/pam.d/
atd                halt                smartcard-auth-ac
authconfig         ksu                 sftp
authconfig-gtk     login               smtp.postfix
authconfig-tui     newrole             sshd
chfn               other               su
chsh               passwd              sudo
config-util        password-auth       sudo-i
crond              password-auth-ac    su-l
cups               polkit-1            system-auth
cvs                poweroff            system-auth-ac
eject              reboot              system-config-authentication
fingerprint-auth   remote              system-config-date
fingerprint-auth-ac rhn_register        system-config-kdump
gdm                run_init            system-config-keyboard
gdm-autologin      runuser             system-config-network
gdm-fingerprint    runuser-l           system-config-network-cmd
gdm-password       setup               system-config-users
gdm-smartcard      smartcard-auth      xserver
[root@server1 ~]#
```

## 控制标志

PAM 系统将用户验证过程分为四个独立任务。 这是四种不同的 PAM 标志类型：

-   **身份验证管理 (auth)** 建立用户的身份。 例如，PAM auth 命令决定是否提示输入用户名和/或密码。 相关选项甚至可以授予组成员资格。
-   **账户管理 (account)** 根据账户策略允许或拒绝访问。 例如，PAM account 命令可能根据时间、密码过期或特定受限用户列表来拒绝访问。
-   **密码管理 (password)** 管理其他密码策略。 例如，PAM password 命令可能限制用户在控制台重置前尝试登录的次数。
-   **会话管理 (session)** 为应用程序应用设置。 例如，PAM session 命令可能为登录控制台设置默认设置。

图 10-11 所示的代码来自示例 PAM 配置文件 /etc/pam.d/login。 所有 PAM 配置文件中的每一行都采用以下格式书写：

```
module_type  control_flag  module_path  [arguments]
```

## 图 10-11

PAM /etc/pam.d/login 配置文件

```
#PAM-1.0
auth [user_unknown=ignore success=ok ignore=ignore default=bad] pam_securetty.so
auth include system-auth
account required pam_nologin.so
account include system-auth
password include system-auth
# pam_selinux.so close should be the first session rule
session required pam_selinux.so close
session required pam_loginuid.so
session optional pam_console.so
# pam_selinux.so open should only be followed by sessions to be executed in the
user context
session required pam_selinux.so open
session required pam_namespace.so
session optional pam_keyinit.so force revoke
session include system-auth
-session optional pam_ck_connector.so
~
~
"/etc/pam.d/login" 16L, 728C
```

module_type 如前所述，可以是 auth、account、password 或 session。 control_flag 决定 PAM 在模块成功或失败时执行的操作。 module_path 指定实际 PAM 模块文件的位置。 最后，与常规 shell 命令一样，您可以为每个模块指定参数。

control_flag 字段需要进一步解释。 它决定配置文件在模块标记成功或失败时如何反应。 五种不同的控制标志在表 10-5 中描述。

## 表 10-5

PAM 控制标志

| control_flag | 描述 |
|---|---|
| required | 如果模块工作正常，命令继续执行。 如果失败，PAM 将继续执行配置文件中的下一个命令——但由 PAM 控制的命令仍将失败。 |
| requisite | 如果模块失败，则停止进程。 |
| sufficient | 如果模块工作正常，则登录或其他身份验证继续进行。 无需处理其他命令。 |
| optional | 除非未使用其他模块，否则 PAM 忽略此模块的成功或失败。 |
| include | 包含所注配置文件中的所有 module_type 指令；例如，如果指令为 password include system-auth，则包含 PAM system-auth 文件中的所有 password 指令。 |

要了解控制标志的工作方式，请查看 /etc/pam.d/reboot 配置文件中的命令：

```
auth sufficient pam_rootok.so
```

第一个 auth 命令检查 pam_rootok.so 模块。 换句话说，如果 root 用户运行 reboot 命令，control_flag 为 sufficient，则此文件中的其他 auth 命令将被忽略。 Linux 运行 reboot 命令。 这在 /usr/share/doc/pam-versionnumber/txts 目录中的 README.pam_rootok 文件中有说明。

```
auth required pam_console.so
```

鉴于第一行的目的，此第二个 auth 命令仅针对非 root 用户运行，以管理控制台内的权限。 在这种情况下，它只是确认登录到该控制台的任何用户的控制台所有权。

```
#auth include system-auth
```

第三行默认被注释掉。 如果您使此行生效，它将包含 system-auth 配置文件中的命令，该文件需要 root 用户权限。 使用 root 权限连接的远程用户仍被允许重新启动系统。

```
account required pam_permit.so
```

与 account 命令关联的模块 (pam_permit.so) 接受所有用户，即使是远程登录的用户。 换句话说，除非被之前的指令拒绝，否则此配置文件将允许任何 root 用户（本地或远程）重新启动 Linux 系统。

## PAM 文件的格式

本节有点复杂。 它从图 10-12 所示的 /etc/pam.d/login 配置文件开始。 此外，由于该文件包含对 /etc/pam.d/system-auth 配置文件的引用，您需要在这两个文件之间来回切换以跟上本节内容。

当用户打开文本控制台并登录时，Linux 会逐行处理此配置文件。 如前所述，/etc/pam.d/login 中的第一行将 root 用户访问限制为 /etc/securetty 文件中定义的受保护终端：

```
auth [user_unknown=ignore success=ok ignore=ignore default=bad] \
 pam_securetty.so
```

## 图 10-12 PAM /etc/pam.d/system-auth 配置文件

```
#PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth required pam_env.so
auth sufficient pam_fprintd.so
auth sufficient pam_unix.so nullok try_first_pass
auth requisite pam_succeed_if.so uid >= 500 quiet
auth required pam_deny.so

account required pam_unix.so
account sufficient pam_localuser.so
account sufficient pam_succeed_if.so uid < 500 quiet
account required pam_permit.so

password requisite pam_cracklib.so try_first_pass retry=3 type=
password sufficient pam_unix.so sha512 shadow nullok try_first_pass use_authtok
password required pam_deny.so

session optional pam_keyinit.so revoke
session required pam_limits.so
session [success=1 default=ignore] pam_succeed_if.so service in crond quiet
use_uid
session required pam_unix.so
~
"/etc/pam.d/system-auth" 22L, 937C
```

下一行包含来自 system-auth PAM 配置文件的 auth 命令：

```
auth include system-auth
```

图 10-12 所示的 system-auth 配置文件包含五个 auth 指令：

```
auth required pam_env.so
auth sufficient pam_fprintd.so
auth sufficient pam_unix.so nullok try_first_pass
auth requisite pam_succeed_if.so uid >= 500 quiet
auth required pam_deny.so
```

按顺序，它们设置环境变量，如果可用则通过指纹读取器 (pam_fprintd.so) 检查身份验证，并检查密码 (pam_unix.so)。 与这些模块关联的 sufficient 标志意味着如果输入了有效的指纹或密码，则身份验证有效。 账户的用户 ID 必须为 500 及以上。 如果未满足这些条件，用户将被锁定 (pam_deny.so)。

> **考试提示**
> 
> *如果 /etc/nologin 文件存在，则普通用户不允许登录到本地控制台。 任何尝试登录的普通用户都将把 /etc/nologin 的内容作为消息读取。*

现在返回 /etc/pam.d/login 文件。 下一行查找 account 模块类型，检查 /etc/nologin 文件中列出的不允许登录的账户：

```
account required pam_nologin.so
```

以下 account 模块包含来自 /etc/pam.d/system-auth 配置文件的 account 模块：

```
account include system-auth
```

这些是来自 /etc/pam.d/system-auth 的 account 模块类型行：

```
account required pam_unix.so
account sufficient pam_localuser.so
account sufficient pam_succeed_if.so uid < 500 quiet
account required pam_permit.so
```

第一行引用 /lib/security 目录中的 pam_unix.so 模块，该模块会弹出正常的用户名和密码提示。 根据 pam_localuser.so 模块，在 /etc/passwd 中找到的用户会自动接受。 根据 pam_succeed_if.so 模块，服务用户（用户 ID 小于 500）会自动登录，且不显示消息（quiet）。 pam_permit.so 模块始终返回成功。

现在返回 /etc/pam.d/login 文件。 下一行是 password 模块，它包含来自 /etc/pam.d/system-auth 文件的其他 password 模块类型行：

```
password include system-auth
```

这些是来自 /etc/pam.d/system-auth 的 password 模块类型行：

```
password requisite pam_cracklib.so try_first_pass retry=3
password sufficient pam_unix.so sha512 shadow nullok try_first_pass \
use_authtok
password required pam_deny.so
```

此列表中的第一个命令允许使用先前成功的密码 (try_first_pass)，然后将最大重试次数设置为三次。 下一个命令使用 SHA512 哈希加密密码，支持 Shadow Password Suite
