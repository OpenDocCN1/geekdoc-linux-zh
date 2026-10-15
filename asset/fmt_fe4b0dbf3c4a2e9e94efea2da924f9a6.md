
查看表 5-3 中的文件位置列表，你可能会问为什么 PAM 需要这么多不同的配置文件。“每个应用程序一个配置文件？这听起来太疯狂了！” 吧，也许并不是。PAM 允许此的原因是并不是所有应用程序都是平等的。例如，一个使用 Dovecot 邮件服务器的邮局协议（POP）邮件服务器可能允许该站点的所有用户获取邮件，但登录程序可能只想允许某些用户登录控制台。为了适应这一点，PAM 需要一个与登录程序配置文件不同的 POP 配置文件。

| 文件位置 | 定义 |
| --- | --- |
| `/lib64/security` 或 `/lib/security` (32 位) | 由实际 PAM 库调用的动态加载认证模块。 |
| `/etc/` | 位于 `/lib64/security`（或 `/lib/security`）中的模块的配置文件。 |
| `/etc/pam.d` | 每个使用 PAM 的应用程序的配置文件。如果使用 PAM 的应用程序没有特定的配置文件，则自动使用默认配置。 |

**表 5-3** 重要的 PAM 目录

## 配置 PAM

我们在这里讨论的配置文件位于 `/etc/pam.d` 目录。如果你想更改适用于 `/etc/security` 目录中特定模块的配置文件，你应该咨询该模块随附的文档。（记住 PAM 只是一个框架。特定模块可以由任何人编写）。

PAM 配置文件的性质很有趣，因为它具有“可堆叠性”（stackable）的特性。这意味着配置文件的每一行都会被认证过程评估（以及下文显示的会）。

`/etc/pam.d` 中的每个 PAM 配置文件由具有以下语法的行组成：

```
module_type      control_flag      module_path      arguments
```

其中 `module_type` 代表四种类型：`auth`（认证）、`account`（账户）、`session`（会）或 `password`（密码）。注释必须以 `#` 字符开头。表 5-4 列出了这些类型。

| 模块类型 | 功能 |
| --- | --- |
| `auth` | 指示应用程序提示用户输入密码并授予用户和组权限。用于认证。 |
| `account` | 不执行认证，但确定其他访问因素，如时间。用于授权。 |
| `session` | 指定在用户登录前后需要执行的任何操作（例如，记录连接）。 |
| `password` | 指定允许用户更改密码的模块（如果适用）。 |

表 5-4 PAM 模块类型

### 第 5 章 管理用户和组

`control_flag`（控制标志）允许你指定如何处理特定模块的成功或失败。常见的控制标志描述在表 5-5 中。

`module_path`（模块路径）指定执行认证任务的模块文件名或完整路径。模块通常存储在 `/lib64/security/`（或 `/lib/security/`）目录下。

| 控制标志 | 描述 |
| --- | --- |
| `required` | 如果指定了此标志，模块必须成功认证个人。如果它失败，返回的摘要值必须为失败。 |
| `requisite` | 此标志类似于 `required`；但如果 `requisite` 认证失败，配置文件中列出的模块将不再被调用，并立即向应用程序返回失败。这允许你要求在接受登录之前满足某些条件（例如用户必须在局域网内而不是尝试通过互联网登录）。 |
| `sufficient` | 如果 `sufficient` 模块返回成功，且配置文件中没有更多的 `required` 或 `sufficient` 控制标志，PAM 将向应用程序返回成功。 |
| `optional` | 此标志允许 PAM 继续检查其他模块，即使其中一个已经失败。换句话说，该模块的结果将被忽略。例如，当某个特定模块失败时仍允许用户登录，可以使用此标志。 |
| `include` | 此标志用于包含作为参数指定的另一个配置文件中的所有行或指令。这是链链或堆叠不同 PAM 文件中指令的方法。 |
| `substack` | 这用于从指定的 PAM 配置文件中包含给定类型的所有行（栈）。它与 `include` 控制标志的区别在于，指定的 `substack` 失败并不意味着会自动跳过对剩余模块栈的检查。当前模块栈的评估将继续。 |

**表 5-5** PAM 控制标志

#### 144 Linux 系统管理：入门指南

| 参数 | 说明 |
| --- | --- |
| `debug` | 将调试信息发送到系统日志。 |
| `no_warn` | 不向调用应用程序发送警告消息。不再向用户提示第二次输入密码。 |
| `use_first_pass` | 而是，应该重复在上一个认证（`auth`）模块中输入的密码用于用户身份验证。（这仅适用于 `auth` 和 `password` 模块。） |
| `try_first_pass` | 此选项与 `use_first_pass` 类似，因为用户不会被再次提示输入密码。然而，如果现有密码导致模块返回失败，将再次提示用户输入密码。 |
| `use_mapped_pass` | 此参数指示模块获取上一个模块输入的明文令牌（token），并生成一个加密/解密密钥，用该密钥安全地存储或检索此模块所需的认证令牌。 |
| `expose_account` | 此参数允许模块对账户信息采取不那么谨慎的态度——取决于系统管理员的认为。 |
| `nullok` | 此参数允许被调用的 PAM 模块允许空（null）密码 |

表 5-6 PAM 配置参数

PAM 配置行的最后一项是参数，它代表传递给认证模块的参数。虽然参数特定于每个模块，但某些通用选项可以适用于所有模块。这些参数在表 5-6 中描述。

## PAM 配置文件示例

让我们查看一个示例 PAM 配置文件 `/etc/pam.d/login`：

```
1. ##PAM-1.0
2. auth        substack system-auth
3. auth        include postlogin
4. account    required pam_nlogin.so
5. account    include system-auth
6. password  include system-auth
```

### 第 5 章 管理用户和组

```
7. # pam_selinux.so close 应该是第一条会话规则
8. session required pam_selinux.so close
9. session required pam_loginuid.so
```

请注意，已添加行号以帮助文件的可读性。

第一行以哈希符号开头，因此是一条注释。因此，我们可以忽略它。

```
##PAM-1.0
```

让我们继续看第 2 行：

```
auth substack system-auth
```

`module_type`（模块类型）是 `auth`，这意味着它处理验证用户的凭据（例如，用户名和密码）。

`control_flag`（控制标志）设置为 `substack`，因此这一行将导致跳转到指定的配置文件 `/etc/pam.d/system-auth`。评估将按照 `system-auth` 文件中指定的方式继续，并将控制权返回给 PAM 模块。这一行没有参数。

文件中的其余行在解释之前给出，从第 3 行开始：

```
auth include postlogin
```

与第 2 行类似，第 3 行通过认证验证用户。

`control_flag` 设置为 `include`。这将包含来自 `/etc/pam.d/required` 配置文件中所有类型为该类型的行。这一行没有参数。

```
account required pam_loginuid.so
```

在第 4 行中，`module_type` 是 `account`，这意味着它用于根据各种因素限制账户对系统服务的访问。`control_flag` 是 `required`。这意味着如果此模块失败，PAM 将向调用应用程序返回失败，但将继续对堆栈中下一个模块进行评估。

`pam_loginuid.so` (`/lib64/security/pam_loginuid.so`) 是要调用的实际 PAM 模块名称。`pam_loginuid.so` 模块检查 `/etc/pam.d` 文件。如果存在，则允许 root 登录；其他用户会被错误消息拒绝。如果文件不存在，它始终返回成功。

```
account include system-auth
```

在第 5 行中，`module_type` 是 `account`。`control_flag` 设置为 `include`。这将包含来自 `/etc/pam.d/system-auth` 配置文件中所有类型为 `account` 的行。这一行没有参数。

```
auth include system-auth
```

在第 6 行中，`module_type` 是 `password`。`control_flag` 设置为 `include`。这将包含 `/etc/pam.d/system-auth` 配置文件中所有类型为 `password` 的行。这一行没有参数。

```
# pam_selinux.so close 应该是第一条会话规则
```
