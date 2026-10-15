

The modules perform the following tasks (not all are included in the above configuration):

- **auth required pam_securetty.so**
  该模块检查文件 /etc/securetty 中有效登录终端的列表。如果终端未列在该文件中，则从该终端拒绝登录。这仅涉及 root 用户。
- **auth required pam_env.so**
  该模块可用于设置额外的环境变量。变量可在文件 /etc/security/pam_env.conf 中配置。
- **auth required pam_unix2.so nullok**
  模块 pam_unix2.so 在身份验证过程中用于验证用户提供的登录名和密码。
- **auth required pam_nologin.so**
  该模块检查是否存在文件 /etc/nologin。如果找到此类文件，其内容会在用户尝试登录时显示。除了 root 用户外，其他用户均被拒绝登录。
- **account required pam_unix2.so**
  在此条目中再次使用 pam_unix2.so 模块，但在此情况下它检查用户的密码是否仍然有效或用户是否需要创建新密码。
- **password required pam_pwcheck.so nullok**
  这是类型为 password 的模块的条目。当用户尝试更改密码时使用。在此情况下，使用模块 pam_pwcheck.so 检查新密码是否足够安全。
  **nullok** 参数允许用户更改空密码，否则空密码将被视为锁定账户。
- **password required pam_unix2.so nullok use_first_pass use_authtok**

  更改密码时也需要 pam_unix2.so 模块。它对新密码进行加密（更准确地说是哈希），并将其写入身份验证数据库。

  **nullok** 的意义与上面对 pam_pwcheck.so 的描述相同。使用参数 **use_first_pass**，pam_unix2 使用来自之前模块的密码，例如 pam_pwcheck.so，如果没有来自之前模块的身份验证令牌则报错终止。参数 **use_authtok** 用于强制此模块将新密码设置为由之前堆叠的密码模块提供的密码。
- **session required pam_unix2.so**

  在此使用 pam_unix2.so 模块的 session 组件。不带参数时该模块无效果，带参数 **trace** 时它使用 syslog 守护进程记录用户的登录。
- **session required pam_limits.so**

  pam_limits.so 为用户设置资源限制，可在文件 /etc/security/limits.conf 中配置。
- **session required pam_mail.so**

  该模块在用户邮箱中有新邮件时会显示消息。它还会设置一个指向用户邮件目录的环境变量。

## Secure Password Guidelines

即使系统的最佳安全设置也可能被攻破，如果用户选择容易猜测的密码。凭借当今的计算能力，简单的密码可在几分钟内被破解。

这些攻击也称为 *字典攻击*，因为密码破解程序只是从字典文件中一个接一个地尝试单词，包括这些单词的一些常见变体。

因此，密码绝不应该是可以在字典中找到的单词。好的、安全密码应始终包含数字和大写字符。

要检查用户密码是否满足此要求，您可以在用户设置密码之前启用一个特殊的 PAM 模块来先测试密码。PAM 模块称为 pam_pwcheck.so 并使用 cracklib 库来测试密码的安全性。

默认情况下，此 PAM 模块在 SLES 10 上已启用。

如果用户输入的密码不够安全，则会显示以下消息：

```
Bad password: too simple
```

然后提示用户输入其他密码。

还有专用的密码检查程序可供使用，例如 **John the Ripper** (http://www.openwall.com/john/)。

