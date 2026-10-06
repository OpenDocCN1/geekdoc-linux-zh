

# 144 Linux 系统管理：入门指南

| 参数 | 说明 |
| --- | --- |
| debug | 将调试信息发送到系统日志。 |
| no_warn | 不向调用应用程序发送警告消息。不再向用户提示第二次输入密码。 |
| use_first_pass | 而是，应该重复在上一个认证（auth）模块中输入的密码用于用户身份验证。（这仅适用于 auth 和 password 模块。） |
| try_first_pass | 此选项与 use_first_pass 类似，因为用户不会被再次提示输入密码。然而，如果现有密码导致模块返回失败，将再次提示用户输入密码。 |
| use_mapped_pass | 此参数指示模块获取上一个模块输入的明文令牌（token），并生成一个加密/解密密钥，用该密钥安全地存储或检索此模块所需的认证令牌。 |
| expose_account | 此参数允许模块对账户信息采取不那么谨慎的态度——取决于系统管理员的认为。 |
| nullok | 此参数允许被调用的 PAM 模块允许空（null）密码 |

表 5-6 PAM 配置参数

PAM 配置行的最后一项是参数，它代表传递给认证模块的参数。虽然参数特定于每个模块，但某些通用选项可以适用于所有模块。这些参数在表 5-6 中描述。

# PAM 配置文件示例

让我们查看一个示例 PAM 配置文件 `/etc/pam.d/login`：

```
1. ##PAM-1.0
2. auth        substack system-auth
3. auth        include postlogin
4. account    required pam_nlogin.so
5. account    include system-auth
6. password  include system-auth
```

# 第 5 章 管理用户和组

7. # pam_selinux.so close 应该是第一条会话规则
8. session required pam_selinux.so close
9. session required pam_loginuid.so

请注意，已添加行号以帮助文件的可读性。
第一行以哈希符号开头，因此是一条注释。因此，我们可以忽略它。

```
##PAM-1.0
```

让我们继续看第 2 行：

```
auth substack system-auth
```

module_type（模块类型）是 `auth`，这意味着它处理验证用户的凭据（例如，用户名和密码）。
control_flag（控制标志）设置为 `substack`，因此这一行将导致跳转到指定的配置文件 `/etc/pam.d/system-auth`。评估将按照 `system-auth` 文件中指定的方式继续，并将控制权返回给 PAM 模块。这一行没有参数。
文件中的其余行在解释之前给出，从第 3 行开始：

```
auth include postlogin
```

与第 2 行类似，第 3 行通过认证验证用户。
control_flag 设置为 `include`。这将包含来自 `/etc/pam.d/required` 配置文件中所有类型为该类型的行。这一行没有参数。

```
account required pam_loginuid.so
```

在第 4 行中，module_type 是 `account`，这意味着它用于根据各种因素限制账户对系统服务的访问。control_flag 是 `required`。这意味着如果此模块失败，PAM 将向调用应用程序返回失败，但将继续对堆栈中下一个模块进行评估。
`pam_loginuid.so` (`/lib64/security/pam_loginuid.so`) 是要调用的实际 PAM 模块名称。`pam_loginuid.so` 模块检查 `/etc/pam.d` 文件。如果存在，则允许 root 登录；其他用户会被错误消息拒绝。如果文件不存在，它始终返回成功。

```
account include system-auth
```

在第 5 行中，module_type 是 `account`。control_flag 设置为 `include`。这将包含来自 `/etc/pam.d/system-auth` 配置文件中所有类型为 `account` 的行。这一行没有参数。

```
auth include system-auth
```

在第 6 行中，module_type 是 `password`。control_flag 设置为 `include`。这将包含 `/etc/pam.d/system-auth` 配置文件中所有类型为 `password` 的行。这一行没有参数。

```
# pam_selinux.so close 应该是第一条会话规则
```

第 7 行被注释了。因此我们可以忽略它。

```
session required pam_selinux.so
```

在第 8 行中，module_type 是 `session`，用于指定在用户登录后是否需要执行某些操作。control_flag 设置为 `required`。`pam_selinux.so` (`/lib64/security/pam_selinux.so`) 是要调用的实际 PAM 模块名称。`pam_selinux.so` 用于设置默认的安全上下文。如果参数传递给 `pam_selinux.so` 模块，它在基于 Red Hat 的发行版中非常流行。

```
session required pam_loginuid.so
```

在第 9 行中，module_type 是 `session`。control_flag 设置为 `required`。`pam_loginuid.so` 是要调用的实际 PAM 模块名称。相同的概念适用于 `/etc/pam.d` 目录下的其他配置文件。如果你需要更多关于特定模块作用或其参数的信息，可以查阅该模块的帮助文档。

