
## 第 22 章：系统与网络安全

MD5 相比旧式密码加密的另一个优势是，旧密码被限制为最多八个字符；而新密码（使用 MD5 加密）可以长得多。长密码更难破解，即使 `/etc/shadow` 文件落入别有用之手也是如此。

在 `/etc/shadow` 文件中使用 MD5 加密的一个线索是下面示例中第二个字段的加密密码长度增加，以及 `$1$` 前缀：

```
root:$1$AAanYi/nYSHeHBuz2up9Gcfoo18rt50:11077:0:9999:7:-1:134540356
```

可插认证模块（PAM）执行实际的 MD5 加密。PAM 为 Linux 系统上的用户身份验证提供了一种灵活的方法。通过配置文件中的设置，你可以更改文件的身份验证方法，而无需实际修改验证用户身份的 `login` 和 `passwd` 程序。

Red Hat Linux 广泛使用 PAM，配置文件位于你系统的 `/etc/pam.d` 目录下。检查该目录的内容。以下是我我的 Red Hat Linux 系统上看到的内容：

```
/etc/pam.d
apacheconf    kbrdate      printconf-gui        samba
bindf        kde          reboot               serviceconf
chfn         kisndock     redhat-config-apache  smtp
chsh         kpppp         redhat-config-bound  sshd
kscreensaver su
firewall-config kuser       redhat-config-date    sudo
           wuftpd       redhat-config-printer-gui system-auth
def          local_conf redhat-config-time   up2date
gdmconf      login        redhat-config-users  up2date-config
gnome-lockit neat         rexec                 up2date-nox
pnormg-auth other        rhn-register         v41-config
halt         password     rlogin                xdm
hrowser      poweroff     rp3-config           xxcreensaver
internet-druid rsh                               xserver
```

如列表所示，各种身份验证用户的程序都有一个配置文件（每个都是一个文本文件）。例如，有 `login`、`passwd` 和 `su` 的条目。以下是我系统上 `/etc/pam.d/passwd` 文件的内容：

```
/etc/pam.d/passwd
#PAM-1.0
auth required      /lib/security/pam_stack.so service=system-auth
account required  /lib/security/pam_stack.so service=system-auth
password required  /lib/security/pam_stack.so service=system-auth
```

这些行表示，身份验证、账户管理和密码检查都应由 `pam_stack` 模块（`/lib/security/pam_stack.so`）带参数 `service=system-auth` 完成。本质上，`pam_stack` 模块指向 `/etc/pam.d` 目录下的另一个配置文件。在这里，配置文件是 `/etc/pam.d/system-auth`。以下是我 Red Hat Linux 电脑上 `/etc/pam.d/system-auth` 文件的内容：

```
cat /etc/pam.d/system-auth
#PAM-1.0
# This file is auto-generated.
# User changes will be destroyed by the next time authconfig is run.
auth required       /lib/security/pam_env.so
auth sufficient      /lib/security/pam_unix.so leaveauth nullock
account required       /lib/security/pam_deny.so
account required       /lib/security/pam_unix.so
password required      /lib/security/cracklib.so retry=3 type-
password sufficient    /lib/security/pam_unix.so nullock use_authtok md5
password required       /lib/security/pam_deny.so
session required       /lib/security/pam_limits.so
session required       /lib/security/pam_unix.so
```

虽然我已经过过了所有细节，但这里是对其中一些行的简要解释。第一行 `auth` 加载 PAM 模块 `/lib/security/pam_env.so`，它可以设置或取消环境变量。第二行 `auth` 指定了一个身份验证模块，通过使用 PAM 模块 `/lib/security/pam_unix.so` 并带上 `likeauth nullock` 等参数来检查用户身份。字符串中的选项含义如下：

- `likeauth`（无论模块是用于设置新凭据还是验证现有用户，都返回相同的值）
- `nullock`（`/etc/pam.d/system-auth` 中的行表示如果 `pam_unix.so` 模块身份验证失败，则拒绝访问系统。）
- `/etc/pam.d/system-auth` 中的 `account` 行检查以确保用户未过期，且用户被允许在特定时间登录等。

`/etc/pam.d/system-auth` 中的接下来两行 `password` 指定了如何设置密码。第一行 `password` 使用 `/lib/security/cracklib.so` 模块来破解密码（这正如 `cracklib.so` 模块名称所示）。`retry=3` 表示用户最多可以输入三次密码。第二行 `password` 表示使用 MD5 加密将密码存储在 `/etc/shadow` 文件中。`/etc/pam.d/passwd` 配置文件在使用 `passwd` 命令更改密码时生效。以下是我尝试更改密码的示例：

```
passwd
Changing password for user
(current) password: 
New password: 
Retype new password: 
Password updated successfully.
```
