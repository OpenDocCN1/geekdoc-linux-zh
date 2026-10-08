

## 最佳实践：用户权限与许可

本章及后续章节中的“最佳实践”部分旨在作为该章节的“教训总结”回顾。如果你已经了解某个特定主题的基础知识，本节的笔记可能就是你需要的全部。

首先，保护影子密码套件（shadow password suite）的文件非常重要。因为 `/etc/passwd` 和 `/etc/group` 是全局可读的，因此 `/etc/shadow` 和 `/etc/group` 应该只允许 root 管理员读取。作为 Linux 管理员，你需要了解如何从命令行创建并管理用户账户。

你可以赋予两种特权。一种是与硬件组件（如 CD、电话媒体和音频设备）相关的特权。此外，还有与系统配置、文件共享和打印管理相关的管理权限。

通过 Linux 用户私有组方案，用户是他们自己的特殊组的成员。作为管理员，你可以创建一个特殊组。在 SGID 位的帮助下，该组可以由这些用户共享，并防止他人查阅。SUID 和粘滞位（sticky bits）是支持普通用户不同操作的特殊权限。

Linux 提供了层级的管理权限。通过 `su`、`sg` 和 `sudo` 命令可以访问此类权限。某些管理权限与特定 Linux 组的成员身份绑定。`sudo` 命令尤为重要，因为它支持根据 `/etc/sudoers` 配置为普通用户提供特权。

Linux 日志包含系统日志和内核日志。可记录的身份验证事件基于相关配置文件中的 `auth` 和 `authpriv` 选项。此类日志存储在 `/var/log` 目录中，并每周记录一次。黑客客尝试登录你的系统的记录可以在上述目录下的 `auth.log` 和 `secure` 等文件中找到。

PAM 模块用于进一步规范对管理命令的访问。PAM 可能位于 `/etc/pam/` 目录，使用存储在 `/lib/security/` 中的模块。四种模块类型为 `auth`、`account`、`password` 和 `session`。PAM 模块的成功或失败取决于所应用的控制标志，这些标志可能是要求的（required）、足够的（sufficient）或可选的（optional）。

对于 GUI 工具，由 PolicyKit 进行管理。它调节你可能在 GUI 中控制的 dbus 系统组件之间的访问。它可以根据用户调节各种工具的访问。它可以根据用户是本地还是远程来调节访问。正如 PolicyKit 正在为 GNOME 开发一样，KAuth 正在为 KDE 开发。

如果你有网络身份验证数据库，同样存在安全问题。两个基于 Linux 的身份验证数据库是 NIS 和 LDAP。NIS更容易设置，因为它几乎可以直接使用影子密码套件。在默认配置中，这两个服务都以明文形式发送密码。LDAP 可以使用第三方证书机构（如 VeriSign 或 GoDaddy）或使用 `openssl` 命令创建的自签名证书进行保护。NIS 没有加密选项。

## 章节总结

本章的重点是用户安全。它从影子密码套件的文件开始。在该结构中，Linux 管理员可以根据组成员身份分配标准和管理权限。你可以根据 `/etc/sudoers` 文件进一步自定义管理权限。SUID、SGID 和粘滞位可用于可执行文件和共享目录设置特殊权限。可以通过 `/var/log/` 目录中的日志跟踪登录访问。PAM 模块可以进一步自定义用户对关键管理工具的访问。PolicyKit 可以更进一步自定义 GNOME 桌面环境内的用户访问。对于网络身份验证提供了两种基于 Linux 的选项：NIS 和 LDAP。

## 核心概念与术语

| account | required | Group ID (GID) |
| :--- | :--- | :--- |
| auth | requisite | 轻量级目录访问协议 (LDAP) |
| chage | session | |
| dbus | sg | 网络信息服务 (NIS) |
| --frequent | su | Ping 风暴攻击 (Ping storm) |
| groupadd | sudo | 设置组 ID (SGID) 位 |
| groupdel | sufficient | 设置用户 ID (SUID) 位 |
| groupmod | useradd | 影子密码套件 |
| --last | userdel | 粘滞位 (Sticky bit) |
| optional | userm | 用户 ID (UID) |
| password | | 用户私有组方案 |

## 第 4 章评估

- 1. 下列哪个文件通常不被所有用户读取？

- 9. 下列哪种特殊权限与共享目录相关？该目录对于非目录所有组成员的人无法访问。

  - A. /etc/passwd
  - B. /etc/shadow
  - C. /etc/group
  - D. /etc/login.defs

  - A. SUID
  - B. SGID
  - C. Sticky bit
  - D. Executable bit

- 2. 下列哪个文件包含关于密码时间限制的信息？

- 10. 配置文件中的下列哪个选项收集了登录尝试和失败的信息？

  - A. /etc/passwd
  - B. /etc/shadow
  - C. /etc/group
  - D. /etc/gshadow

  - A. auth
  - B. sys
  - C. log
  - D. user

- 3. 下列哪个命令可以用于修改用户密码的过期信息？

- 11. 下列哪个 PAM 模块与登录信息的关系最小？

  - A. useradd
  - B. passwd
  - C. groupmod
  - D. chage

  - A. auth
  - B. account
  - C. password
  - D. session

- 4. 该命令搜索所有组名为 `uid=10` 的文件。假设你已登录 root 管理员账户。

- 12. 输入 PAM 模块所在的目录。

- 5. 关于用户权限组方案，下列哪种陈述是正确的？

- 13. 下列哪个 PolicyKit 概念与配置规则以用户使用桌面工具相关？

  - A. Linux 中没有私有组。
  - B. 组中的用户信息是私有的。
  - C. 用户的主 UID 是用户的主 GID。
  - D. 用户是同一个私有组的成员。

  - A. 隐式授权 (Implicit authorizations)
  - B. 显式授权 (Explicit authorizations)
  - C. 管理授权 (Administrative authorizations)
  - D. PolicyKit 授权 (PolicyKit authorizations)

- 6. 下列哪些组的成员经常被设置为管理员？（选两个）

- 14. 下列哪些 PolicyKit 命令可以用于通过会话识别用户登录？（选两个）

  - A. admin
  - B. adm
  - C. ipadmin
  - D. sys

  - A. ck-history
  - B. ck-list-sessions
  - C. ck-launch-session
  - D. ck-logins

- 7. 下列哪个命令仅需要已配置用户的密码？

  - A. sudoers
  - B. sudo
  - C. su
  - D. sg

- 15. 下列哪个命令可以识别 NIS 使用的网络端口？

- 8. 输入在命令行控制台中中打开并编辑 /etc/sudoers 文件的命令。

  - A. nmap -p
  - B. ypbind -p
  - C. rpcinfo -p
  - D. portmap -p

