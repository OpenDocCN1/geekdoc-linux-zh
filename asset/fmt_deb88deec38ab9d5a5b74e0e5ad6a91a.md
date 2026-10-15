
第一条规则调用 `pam_unix.so` 来验证用户在 `/etc/shadow` 文件中有有效条目。`nullok_secure` 参数表示来自终端时时接受空密码。PAM 必须成功，但仅此点不足以允许用户登录。如果此规则失败，第二条规则将立即返回失败以防止身份验证。如果账户栈中已经存在用户，第三条规则将不会返回值，但应该被执行到。在安装了其他身份验证机制（如 LDAP 或指纹扫描）的 Ubuntu 系统上，此文件将调用 PAM 由这些服务的特定身份验证。

7. 调用 `pam_group.so` 模块，验证用户是否是一个或多个组的成员，并且用户的数字标识符确实存在。此 PAM 模块被执行但是是可选的——成功或失败并不重要，除非它是登录服务的唯一模块（它并非如此），且仅此点不足以允许用户登录。

8. 调用 `pam_limits.so` 模块在配置文件 `/etc/security/limits.conf` 中设置用户限制（该文件在 Ubuntu 系统上不包含任何提交的条目，某种程度上没有意义）。PAM 必须成功（即能够读取其配置文件），但仅此点不足以允许用户登录。

9. 调用 `pam_lastlog.so` 模块向用户 `/var/log/lastlog` 添加条目，打开会话并关闭该会话。此 PAM 模块被执行但是是可选的——成功或失败并不重要，除非它是登录服务的唯一模块（它并非如此），且仅此点不足以允许用户登录。

10. 调用 `pam_motd.so` 模块在控制台显示 `/etc/motd` 的内容。此 PAM 模块被执行但是是可选的——成功或失败并不重要，除非它是登录服务的唯一模块（它并非如此），且仅此点不足以允许用户登录。

11. 调用 `pam_mail.so` 模块检查用户的邮件目录，如果有挂起的邮件则显示。此 PAM 模块被执行但是是可选的——成功或失败并不重要，除非它是登录服务的唯一模块（它并非如此），因此仅此点不足以允许用户登录。

12. 包含 `/etc/pam.d/common-account` 文件的内容，它为验证用户拥有账户提供一组 PAM 规则。Ubuntu 和 Ubuntu 系统使用标准的 `/etc/password` 和 `/etc/shadow` 身份验证，此文件包含以下规则：

```
account [success=1 default=ignore] pam_unix.so

account requisite pam_deny.so

account required pam_permit.so
```

第一条规则调用 `pam_unix.so` 模块执行传统的 Linux 身份验证，检查用户账户在 `/etc/shadow` 文件中未被标记为过期。此 PAM 在成功时将账户栈值设置为 1，但不足以允许用户登录。如果此规则失败，第二条规则将立即返回以防止身份验证。如果账户栈中已经没有值，第三条规则将在账户栈上返回一个正值，但不应该被执行到。在安装了其他身份验证机制（如 LDAP、Kerberos 或指纹扫描）的 Ubuntu 系统上，这将调用由这些服务特定验证账户所需的 PAM。

13. 包含 `/etc/pam.d/common-session` 文件的内容，它为交互和非本地登录会话提供一组 PAM 规则。Ubuntu 和 Ubuntu 系统使用 `/etc/password` 和 `/etc/shadow` 身份验证，此文件包含以下规则：

```
session [default=-] pam_permit.so

session requisite pam_deny.so

session required pam_permit.so

session required pam_unix.so

session optional pam_ck_connector.so nox11
```
