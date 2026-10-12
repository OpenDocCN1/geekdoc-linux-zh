
- 3. **使用以下命令安装所有更新：**
  `rpm -F *`
- 4. **使用以下命令删除更新文件：**
  `rm -fr /usr/local/updates`

## 保护密码

历史上，UNIX 密码存储在 /etc/passwd 文件中，任何用户都可以读取。例如，root 用户在典型的旧式 /etc/passwd 文件中的条目如下所示：

```
root:t6Z7NWDK1K8Su:0:0:root:/root:/bin/bash
```

字段由冒号 (:) 分隔，第二字段包含加密形式的密码。为了检查密码是否有效，login 程序会加密用户输入的明文密码，并将其与 /etc/passwd 文件的内容进行比较。如果匹配，则允许用户登录。

密码破解程序的工作方式与 login 程序类似，只是这些程序一次从字典中选取一个词，加密该词，并将其与 /etc/passwd 文件中的加密密码进行比较以寻找匹配项。要破解密码，入侵者需要 /etc/passwd 文件。通常，破解者利用各种 Internet 服务器（如邮件和 FTP）的弱点来获取 /etc/passwd 文件的副本。

近年来，Red Hat Linux 中对密码的安全性进行了多项改进。其中包括影子密码和可插拔认证模块，并且在安装 Red Hat Linux 时可以轻松安装这些功能。在 Red Hat Linux 安装过程中，有一步涉及在身份验证配置屏幕中进行选择。如果接受默认选择——启用 MD5 密码和启用影子密码——您将自动在 Red Hat Linux 中启用更安全的密码。

### 影子密码

显然，将密码随意放置让任何人都能获取——即使它们是加密的——也是糟糕的安全做法。因此，Red Hat Linux 不再将密码存储在 /etc/passwd 文件中（任何用户都可以读取），而是将其存储在影子密码文件 /etc/shadow 中。只有超级用户（root）可以读取此文件。例如，以下是新式 /etc/passwd 文件中 root 的条目：

```
root:x:0:0:root:/root:/bin/bash
```

在这种情况下，请注意第二字段包含 x 而不是加密密码。x 是影子密码；实际的加密密码现在存储在 /etc/shadow 文件中，其中 root 的条目如下：

```
root:$1$AAAn/yNuESHbZupy9cGfoo1Bf0tS0:1107:0:99999:7:-1:-1:134540356
```

/etc/shadow 条目的格式使用冒号分隔字段，与 /etc/passwd 文件中的条目相似，但大多数字段的含义不同。第一个字段仍然是用户名，第二个字段是加密密码。

/etc/shadow 条目中的剩余字段控制密码何时过期。您无需解释或更改 /etc/shadow 文件中的这些条目。相反，使用 chage 命令来更改密码过期信息。首先，您可以使用 chage 命令配合 -l 选项来检查用户的密码过期信息，如下所示（在这种情况下，您必须以 root 身份登录）：

```
chage -l root
```

此命令显示过期信息，包括密码的有效时长以及可以更改密码的频率。

如果您希望确保用户每 90 天强制更改一次密码，可以使用 -M 选项设置密码保持有效的最大天数。例如，为了确保用户 naba 在 90 天内被提示更改密码，我以 root 身份登录并输入以下命令：

```
chage -M 90 naba
```

您可以对每个用户账户执行此操作，以确保所有密码在适当时过期，并且所有用户都必须选择新密码。

### 可插拔认证模块 (PAMs)

除了通过使用影子密码提高密码文件的安全性外，Red Hat Linux 还使用 RFC 1321 中描述的 MD5 消息摘要算法（www.faqs.org/rfcs/rfc1321.html 或 www.cis.ohio-state.edu/cgi-bin/rfc/rfc1321.html）改进了存储在 /etc/shadow 文件中的密码的实际加密方式。MD5 将任意长度的消息缩减为文档的 128 位消息摘要（或指纹），以便您可以使用私钥对其进行加密以进行数字签名。MD5 对于密码加密也很有效。

MD5 相对于旧式密码加密的另一个优势是，旧密码最多限制为八个字符；而新密码（使用 MD5 加密）可以长得多。即使 /etc/shadow 文件落入错误的人手中，更长的密码也更难猜测。

您可以通过 /etc/shadow 文件判断 MD5 加密是否生效；加密后的密码更长，并且都带有 $1$ 前缀，如以下示例条目的第二字段所示：

```
root:$1$AAAAn1/yNuEShBzUpy9CgfooIBf0fSO:1107:0:99999:7::1::134540356
```

一个名为可插拔认证模块（PAM）的附加程序模块执行实际的 MD5 加密。Red Hat Linux 的 PAM 提供了一种灵活的用户认证方法。通过设置 PAM 的配置文件，您可以在不实际修改验证用户身份的重要程序（如 login 和 passwd）的情况下即时更改认证方法。

Red Hat Linux 大量使用 PAM 功能。PAM 驻留在许多不同的模块中（稍后会详细介绍）；其配置文件位于系统的 /etc/pam.d 目录中。通过输入以下命令查看系统上此目录的内容：

```
ls /etc/pam.d
```

此目录中的每个配置文件都指定了特定实用程序的用户认证方式。例如，有用于 login、passwd 和 su 的文件。在我的系统上输入 cat /etc/pam.d/passwd 文件时，我看到的内容如下：

```
#%PAM-1.0
auth       required     pam_stack.so service=system-auth
account    required     pam_stack.so service=system-auth
password   required     pam_stack.so service=system-auth
```

这些行表示认证、账户管理和密码检查都应使用 pam_stack 模块（/lib/security/pam_stack.so）并使用参数 service=system-auth 来完成。本质上，pam_stack 模块引用了 /etc/pam.d 目录中的另一个配置文件。在这种情况下，配置文件是 /etc/pam.d/system-auth。以下是我的 Red Hat Linux PC 上 /etc/pam.d/system-auth 文件的内容：

```
#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth required /lib/security/$ISA/pam_env.so
auth sufficient /lib/security/$ISA/pam_unix.so likeauth nullok
auth required /lib/security/$ISA/pam_deny.so
account required /lib/security/$ISA/pam_unix.so
password required /lib/security/$ISA/pam_cracklib.so retry=3 type=
password sufficient /lib/security/$ISA/pam_unix.so nullok use_authtok md5 shadow
password required /lib/security/$ISA/pam_deny.so
session required /lib/security/$ISA/pam_limits.so
session required /lib/security/$ISA/pam_unix.so
```

以下是配置文件中这些行的简要说明：

- 第一行 `auth` 加载 PAM 模块 `/lib/security/pam_env.so`。该模块可以设置或取消设置环境变量（`/lib/security/$ISA/pam_env.so` 中的 `$ISA` 指的是通常未定义的环境变量，因此 PAM 模块的有效路径名为 `/lib/security/pam_env.so`）。
- 第二行 `auth` 指定了一个认证模块，该模块使用 PAM 模块 `/lib/security/pam_unix.so` 并使用参数字符串 `likeauth nullok` 来检查用户身份。参数字符串中的选项含义如下：
  - `likeauth` — 无论模块用于设置新凭据还是认证现有用户名，都返回相同的值。
  - `nullok` — 允许空白密码。
- `/etc/pam.d/system-auth` 文件中的第三行 `auth` 如果 `pam_unix.so` 模块的认证不成功，则拒绝系统访问。
- `/etc/pam.d/system-auth` 文件中的 `account` 行检查用户账户是否未过期、用户是否允许在一天中的特定时间登录等。
- `/etc/pam.d/system-auth` 文件中的接下来两行 `password` 指定了密码的设置方式：
  - 第一行 password 使用 `/lib/security/pam_cracklib.so` 模块尝试破解新密码（模块名称中的 `cracklib` 即表示此含义）。
