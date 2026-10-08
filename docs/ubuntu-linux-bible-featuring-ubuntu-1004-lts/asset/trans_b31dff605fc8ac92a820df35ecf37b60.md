

# 第三部分：Ubuntu 系统管理员

忽略空行和注释，该文件在 Ubuntu 系统上有意义的部分如下所示：

1: auth requisite pam_security.so
2: auth requisite pam_nologin.so
3: session required pam_selinux.so close
4: session required pam_env.so readenv=1
5: session required pam_env.so readenv-1 file=/etc/default/locale
6: @include common-auth
7: auth optional pam_group.so
8: session required pam_limits.so
9: session optional pam_lastlog.so
10: session optional pam_motd.so
11: session optional pam_mail.so standard
12: @include common-account
13: @include common-session
14: @include common-password
15: session required pam_selinux.so open

# 注意

实际的 /etc/pam/login 文件不包含行号（无法包含）。我添加了行号，以便将 PAM 条目与后续说明进行匹配。■

这一系列 PAM 序列中的相应行执行以下操作：

- 1. 调用 pam  pam_security.so 来检查用户是否登录在 /etc/security 文件中定义的安全终端上。此检查必须成功，但仅此还不足以允许用户登录。

- 2. 调用 pam_nologin.so PAM 模块检查当前系统是否允许登录，这通常通过检查 /etc/login 文件来实现。如果该文件存在，则系统处于维护状态或正在关机过程中，登录将用禁用。此检查必须成功（即该文件必须不存在），但仅此还不足以允许用户登录。

- 3. 调用 pam_selinux.so PAM 模块来翻译任何可能激活的 SELinux 安全上下文。如果未安装 SELinux，此模块将直接返回成功。

- 4. 调用 pam_env.so 模块，该模块从 /etc/security/pam.conf 文件中读取环境变量列表，以设置或取消设置这些变量（在 Ubuntu 系统上，该文件不包含任何非注释条目，因此是没有意义的）。此 PAM 必须成功（即能够读取其配置文件），但仅此还不足以允许用户登录。

- 5. 再次调用 pam_env.so 模块，在这种情况下它从 /etc/default/locale 文件读取环境变量列表以设置或取消设置，这在 Ubuntu 系统上设置了 LANG 环境变量。此 PAM 必须成功（即能够读取其配置文件），但仅此还不足以允许用户登录。

- 6. 包含 /etc/pam.d/common-auth 文件的内容，该文件为系统认证提供了一系列 PAM 规则。在某些标准 /etc/passwd 和 /etc/shadow 密码认证的 Ubuntu 系统上，该文件包含以下 PAM 规则：

```
auth [success=1 default-ignore] pam_unix.so
auth requisite pam_deny.so
auth required pam_permit.so
```
第一规则调用 pam_unix.so 来检查用户在 /etc/shadow 文件中是否被标记为过期。pam_secure 参数表示当来自 security 列出的终端时，空是可以接受的。此 PAM 必须成功，但仅此还不足以允许用户登录。如果第一规则失败，第二规则将立即返回失败。第三规则在 auth 栈中没有值时会放置一个正值，但通常不应到达该规则。

在某些安装了 LDAP、指纹识别等其他认证机制的 Ubuntu 系统上，该文件将调用特定于这些服务的 PAM 规则

- 7. 调用 pam_group.so 模块，验证用户是否属于 /etc/group 文件中定义的某个组。此 PAM 必须成功，但仅此还不足以允许用户登录。

- 8. 调用 pam_limits.so 模块在 /etc/security.conf 文件中设置用户限制。此 PAM 必须成功（即能够读取其配置文件），但仅此还不足以允许用户登录。

- 9. 调用 pam_lastlog.so 模块在打开会话时为用户在 /var/log/lastlog 中添加条目，关闭会话时。此 PAM 是可选的，其成功或失败并不重要，除非它是登录服务的唯一模块（它不是），因此仅此还不足以允许用户登录。

- 10. 调用 pam_motd.so 模块在登录控制台显示 /etc/motd 文件的内容。此 PAM 是可选的，其成功或失败并不重要，除非它是登录服务的唯一模块（它不是），因此仅此还不足以允许用户登录。

- 11. 调用 pam_mail.so 模块检查用户的邮件目录，如果有待处理邮件则显示消息。此 PAM 是可选的，其成功或失败并不重要，除非它是登录服务的唯一模块（它不是），因此仅此还不足以允许用户登录。

- 12. 包含 /etc/pam.d/common-account 文件的内容，该文件为验证用户在系统中是否有有效账户提供了一系列 PAM 规则。在标准 /etc/passwd 和 /etc/shadow 密码认证的 Ubuntu 系统上，该文件包含以下 PAM 规则：

```
account [success=1 default-ignore] pam_unix.so
account requisite pam_deny.so
account required pam_permit.so
```
第一规则调用 pam_unix.so 执行传统的 Linux 检查，验证账户在 /etc/shadow 文件中没有过期。此 PAM 在成功后会将 account 栈值设置为 1，但仅此还不足以允许用户登录。如果成功，文件中的其他规则将不再被调用。如果第一规则失败，第二规则将立即返回失败以阻止认证。第三规则在 auth 栈中没有值时会放置一个正值，但通常不应到达该规则。

在某些安装了 LDAP、Kerberos 或指纹扫描等其他认证机制的 Ubuntu 系统上，该文件将调用特定于这些服务的 PAM 规则

- 13. 包含 /etc/pam.d/common-session 文件的内容，该文件为交互性和非交互式登录会话提供了一系列 PAM 规则。在使用 /etc/passwd 和 /etc/shadow 认证的 Ubuntu 系统上，该文件包含以下 PAM 规则：

```
session [default=1] pam_permit.so
session requisite pam_deny.so
session required pam_permit.so
session required pam_unix.so
session optional pam_ck_connector.so noxill
```
第一规则调用 pam_permit.so 模块允许访问系统，如果没有设置值则将其设置为 1。如果第一规则失败，第二规则将立即返回失败以阻止会话认证。如果此规则由于原因失败，第三规则在 auth 栈中没有值时会放置一个正值，但通常不应到达该规则。第四规则调用 pam_unix.so 模块向 syslog 服务创建一个日志条目，标识用户在当前系统上登录会话的开始。此 PAM 成功了，但仅此还不足以允许用户登录。最后规则调用 pam_ck_connector.so 模块向 ConsoleKit 守护进程注册一个非 X11 登录会话，这意味着守护进程识别到物理控制台已发生了登录。

- 14. 包含 /etc/pam.d/common-password 文件的内容，该文件为实际检查密码提供了一系列 PAM 规则。在 Ubuntu 系统上

