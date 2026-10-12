
为了将认证与应用程序分离，Linux 开发社区参考了 Solaris 系统并创建了自己的 PAM 实现：可插认证模块（Pluggable Authentication Modules）。通过分离认证与应用程序，系统管理员可以实现自己的技术。本节介绍了关键组件、安装方法以及 Red Hat 自带的一些模块。

# 安装 PAM

如果你选择 Red Hat 的标准安装程序，你可能已经安装了 PAM。如果没有，你也可以从 Red Hat 网站 `http://www.redhat.com` 下载。我们本节使用的版本是 `0.57`，配置文件为 `0.51`。我们将使用以下命令安装 RPM：

```
[root@insocoxygen /root]# rpm -i pam-0.57-2.1386.rpm
[root@insocoxygen /root]# rpm -i pamconfig-0.51-2.1386.rpm
```

如果你已经安装了这些包，`rpm` 应该会提示。如果是旧版本，请确保在 `rpm` 中指定 `-u` 而不是 `-option`，以便它可以正确地升级文件。

# 高级概念：密码认证模块 第 24 章

## 第五部分 系统管理

### 第24 章 管理用户和组

...续上

- `sufficient`（足够）：如果模块返回成功，且配置文件中没有更多需要或充分的 `control_flags`（控制标志），则 PAM 向调用它的应用程序返回成功。
- `optional`（可选）：此标志允许 PAM 在当前模块失败时继续检查其他模块。当您在某个特定模块失败时仍允许用户登录时，将需要使用此标志。

`module_path` 指定了执行身份验证任务的 PAM 的实际目录路径。要查看 PAM 自带的模块完整列表，请使用您喜欢的 Web 浏览器查看 `/usr/doc/pam-5.9/html/pam.html` 文件。文档的文本版本也可以 `/usr/doc/pam-59` 目录下找到。

`arguments` 是传递给认证模块的参数。虽然参数取决于特定模块，但某些通用选项也适用于所有模块。它们是：

- `debug`：将调试信息发送到系统日志。（通常位于 `/var/log`——详细信息请检查 `/etc/syslog.conf`。）
- `no_warn`：不向调用应用程序发送消息。
- `use_first_pass`：不再向用户提示输入密码。相反，使用第一次输入的密码来确定用户是否有进入系统的资格。
- `try_first_pass`：与 `use_first_pass` 类似，用户不会被提示第二次密码；然而，如果现有的密码导致模块返回失败，则会要求输入第二个密码。
- `use_mapped_pass`：将密码从上一个模块传递给当前模块，用法类似于 `use_first_pass`；但随后该密码将用于生成加密或解密密钥。

PAM 的一个特性是它的“可堆叠性”（stackable）。这意味着在身份验证过程中，配置文件中的每一行都会被评估（后文所示例外除外）。每行指定一个执行某些身份验证任务的模块，并返回成功或失败标志。结果摘要将返回给调用 PAM 的应用程序。

让我们检查一个 PAM 配置文件示例：`/etc/pam.d/login`。

```
## PAM-1.0
auth      required      /lib/security/pam_security.so
auth      required      /lib/security/pam_pwdb.so shadow nullock
auth      required      /lib/security/pam_nologin.so
account   required      /lib/security/pam_pwdb.so
password  required      /lib/security/pam_cracklib.so
password  required      /lib/security/pam_pwdb.so shadow nullock use_authtok
session   required      /lib/security/pam_pwdb.so
```

你可以看到第一行以井号开头，因此是一条注释。你可以忽略它。

现在逐行查看文件的其余部分：

```
auth      required      /lib/security/pam_security.so
```

指定 `module_type` 为 `auth`（认证），这意味着它将返回一个密码。`control_flag` 设置为 `required`（必须），因此该模块必须返回成功否则登录将失败。模块本身是 `pam_security.so` 模块，它验证 root 账户的登录只能在 `/etc/security` 中提到的终端上发生。

```
auth      required      /lib/security/pam_pwdb.so shadow nullock
```

与上一行类似，这一行想要使用密码进行身份验证，如果密码失败，身份验证过程将向调用应用程序返回失败标志。`pam_pwdb.so` 模块的行为取决于 `module_type`。在这种情况下，`auth` 类型允许 `pam_pwdb.so` 对 `/etc/passwd` 文件进行基础密码检查。`shadow` 参数告诉它如果为真，则检查 `/etc/shadow` 文件，`nullock` 参数允许用户将密码从空更改为某些内容。（通常情况下，它将空密码视为一种账户锁定机制。）

```
auth      required      /lib/security/pam_nologin.so
```

`pam_nologin.so` 模块检查 `/etc/nologin` 文件。如果该文件存在，则只允许 root 登录，其他人将被错误消息拒绝。如果文件不存在，它始终返回成功。

```
account   required      /lib/security/pam_pwdb.so
```

`module_type` 为 `account`（账户），`pam_pwdb.so` 模块将静默检查用户是否被允许登录（例如，他的密码是否已了？）。如果所有参数检查均通过，它将返回成功。

```
password  required      /lib/security/pam_cracklib.so
```

密码 `module_type` 为 `account` 意味着我们在更改密码期间将使用 `pam_cracklib.so` 模块。`pam_cracklib.so` 模块执行各种检查，以查看密码是否容易被潜在入侵者破解。

```
password required /lib/security/pam_pwdb.so nullock use_authtok
```

这是 `pam_pwdb.so` 模块多功能的另一个例子。当 `module_type` 设置为 `password` 时，它将执行 `/etc/passwd` 文件的实际更新。`shadow` 参数告诉它检查 `/etc/shadow` 文件是否存在，如果存在则更新该文件。`nullock` 允许用户将空条更改真实密码。最后一个选项 `use_authtok` 强制 `pam_pwdb.so` 使用从上一个 `password` 类型 `module_type` 条目检索到的密码。

```
session required /lib/security/pam_pwdb.so
```

这是 `pam_pwdb.so` 模块的第四次也是最后的用法。这次它将登录成功发送到系统日志，因为 `module_type` 设置为 `session`（会话）。

# other 文件

当我们需要为某个服务进行身份验证，但没有该服务的配置文件时会发生什么？简单使用 `/etc/pam.d/other`——一种通用类型的设置。

在这种情况下，如果用户尝试使用感知 PAM 的应用程序（例如 FTP 服务器）进行身份验证，但缺少配置文件（例如 FTP 文件意外删除），PAM 将默认使用 `/etc/pam.d/other` 配置。

默认情况下，other 配置设置为谨慎的设置，所有身份验证尝试都会被记录并拒绝。建议保持如此。

# 噢不！我无法登录

用道格拉斯·亚当斯的名言来说：“不要慌。”像 Linux 下发生的许多配置错误一样，此错误可以通过进入单用户模式或使用软盘启动来修复。（详情参见第23章“使用启动管理器”进入单用户模式。）

# 高级概念：密码认证 第24 章

当你以单用户模式进入系统后，只需编辑 `/etc/pam.d/login` 文件，使其仅包含以下行：

```
auth required /lib/security/pam_unix_auth.so
account required /lib/security/pam_unix_acct.so
password required /lib/security/pam_unix_passwd.so
session required /lib/security/pam_unix_session.so
```
