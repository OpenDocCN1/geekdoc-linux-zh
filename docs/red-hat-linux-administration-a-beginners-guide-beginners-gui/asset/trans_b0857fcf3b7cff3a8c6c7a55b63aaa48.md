
## 表 5-3 PAM 配置文件位置

| 文件位置 | 定义 |
| :--- | :--- |
| /sbin/pam_filter | 有机会检查用户和正在运行的应用程序的所有输入和输出的过滤器。这是一种非常隐蔽的设置日志和陷阱的方法，但很少被使用。 |
| /sbin | 可能被库函数调用的辅助工具。 |
| /lib | 管理认证过程的实际 PAM 库。根据应用程序的配置，它调用 /lib/security 目录中相应的模块。 |
| /lib/security | 由实际的 PAM 库调用的动态加载认证模块。 |
| /usr/include/security | 针对开发者的特殊头文件。 |
| /etc/security | 位于 /lib/security 中的模块的配置文件。 |
| /etc/pam.d | 每个使用 PAM 的应用程序的配置文件。如果使用 PAM 的应用程序没有特定的配置文件，则自动使用默认配置。 |

也许并非如此。PAM 允许这样做的原因是并非所有应用程序都是一样的。例如，使用 Qpopop 邮件服务器的 POP 邮件服务器可能希望允许网站的所有用户获取邮件，但登录程序可能只希望允许某些用户登录到控制台。为了适应这种情况，PAM 需要一个不同于登录程序配置的 POP 邮件配置文件。

## 配置 PAM

此处描述的配置文件是位于 /etc/pam.d 目录中的那些。如果你想更改适用于 /etc/security 目录中特定模块的配置文件，应参考随模块提供的文档。（请记住，PAM 只是一个框架。具体的模块可以由任何人编写。）

由于 PAM 配置文件的“可堆叠”特性，其本质非常有趣。也就是说，配置文件的每一行都会在认证过程中进行评估（下文提到的例外情况除外）。每一行指定了一个执行某些认证任务并返回成功或失败标志的模块。结果摘要返回给调用 PAM 的应用程序。

> **注意** 我所说的“失败”并不意味着程序没有正常工作。而是指当执行某些过程来验证用户是否可以执行某事时，返回值是“否”。PAM 使用“成功”和“失败”这两个术语来表示传回给调用应用程序的信息。

每个文件由以下格式的行组成：

```
module_type control_flag module_path arguments
```

其中 `module_type` 代表四种模块类型之一：**auth**（认证）、**account**（账户）、**session**（会话）或 **password**（密码）。注释必须以井号（#）字符开头。表 5-4 列出了这些模块类型及其功能。

### 表 5-4 PAM 模块类型描述

| 模块类型 | 功能 |
| :--- | :--- |
| **auth** | 指示应用程序向用户提示输入密码，然后授予用户和组权限。 |
| **account** | 不执行认证，但根据其他因素（如时间或用户位置）来确定访问权限。例如，通过这种方式，**root** 登录只能被授予控制台访问权限。 |
| **session** | 指定在用户登录前后需要执行的操作（如果有的话）（例如记录连接）。 |
| **password** | 指定允许用户更改其密码的模块（如果适用）。 |

`control_flag` 允许你指定如何处理特定认证模块的成功或失败。控制标志在表 5-5 中描述。

### 表 5-5 PAM 认证模块控制标志

| 控制标志 | 描述 |
| :--- | :--- |
| required | 如果指定此标志，该模块必须成功认证个人。如果失败，返回的摘要值必须是失败。 |
| requisite | 此标志类似于 **required**；但是，如果 **requisite** 认证失败，配置文件中列出的后续模块将不会被调用，并且立即向应用程序返回失败。这允许你要求在接受登录尝试之前必须满足某些条件（例如，用户在局域网中且不能来自互联网）。 |
| sufficient | 如果 **sufficient** 模块返回成功，并且配置文件中没有更多的 **required** 或 **sufficient** 控制标志，PAM 将向调用应用程序返回成功。 |
| optional | 此标志允许 PAM 继续检查其他模块，即使此模块已失败。当你希望在特定模块失败时仍允许用户登录时，应使用此选项。 |

`module_path` 指定执行认证任务的模块的实际目录路径。有关模块的完整列表，请访问 PAM 的网站（http://www.kernel.org/pub/linux/libs/pam）。

PAM 配置行中的最后一个条目是 `arguments`。这些是传递给认证模块的参数。虽然参数因模块而异，但有一些适用于所有模块的通用选项。这些参数在表 5-6 中描述。

### 表 5-6 PAM 认证模块参数

| 参数 | 描述 |
| :--- | :--- |
| debug | 将调试信息发送到系统日志。 |
| no_warn | 不向调用应用程序发出警告消息。 |
| use_first_pass | 不第二次提示用户输入密码。相反，他们第一次输入的密码决定了他们进入系统的资格。（这适用于两个不同模块都需要密码才能继续的配置。） |
| try_first_pass | 此选项类似于 **use_first_pass**，用户第二次不会被提示输入密码。但是，如果现有密码导致模块返回失败，则会要求用户输入第二个密码，并再次尝试该模块。 |
| use_mapped_pass | 将来自前一个模块的密码传递到当前模块，很像 **use_first_pass**。但是，该密码随后用于生成加密或解密密钥。 |

## 一个 PAM 配置文件示例

让我们来看看一个示例 PAM 配置文件，`/etc/pam.d/login`：

```
#%PAM-1.0
auth		required	/lib/security/pam_security.so
auth		required	/lib/security/pam_pwdb.so shadow nullok
auth		required	/lib/security/pam_nologin.so
account	required	/lib/security/pam_pwdb.so
password	required	/lib/security/pam_cracklib.so
password	required	/lib/security/pam_pwdb.so shadow nullok use_authtok
session	required	/lib/security/pam_pwdb.so
```

你可以看到，第一行以井号符号开头，因此是注释。因此，你可以忽略它。让我们继续看第 2 行：

```
auth required /lib/security/pam_security.so
```

由于 **module_type** 是 **auth**，PAM 将要求输入密码。**control_flag** 设置为 **required**，因此该模块必须返回成功，否则登录将失败。该模块本身，**pam_security.so**，验证在 /etc/security 文件中提到的终端上只有 **root** 账户才能登录。此行没有参数。

```
auth required /lib/security/pam_pwdb.so shadow nullok
```

类似于第一个 **auth** 行，第 3 行要求输入密码进行认证，如果密码失败，认证过程将向调用应用程序返回失败标志。

```
auth required /lib/security/pam_nologin.so
```

在第 4 行中，`pam_nologin.so` 模块检查 `/etc/nologin` 文件。如果该文件存在，只有 **root** 允许登录；其他人会被拒绝并显示错误消息。如果文件不存在，它总是返回成功。

```
account required /lib/security/pam_pwdb.so
```

在第 5 行中，由于 **module_type** 是 **account**，`pam_pwdb.so` 模块的行为有所不同。它会静默检查用户是否甚至被允许登录（例如，“他们的密码是否已过期？”）。如果所有参数检查正常，它将返回成功。

```
password required /lib/security/pam_cracklib.so
```

第 6 行中 **module_type** 为 **password** 意味着该模块仅在更改密码时应用。`pam_cracklib.so` 模块执行各种检查，以查看密码是否“太容易”被潜在入侵者破解。

```
password required /lib/security/pam_pwdb.so shadow nullok use_authtok
```

第 7 行展示了 `pam_pwdb.so` 模块的多功能性。当 **module_type** 设置为 **password** 时，它将执行 `/etc/passwd` 文件的实际更新。**shadow** 参数告诉它检查 `/etc/shadow` 文件是否存在，如果存在则更新该文件。**nullok** 参数允许用户将密码从空条目更改为实际密码。最后一个选项，**use_authtok**，强制 `pam_pwdb.so` 使用从先前 **module_type** 条目为 **password** 处获取的密码。

```
session required /lib/security/pam_pwdb.so
```

`pam_pwdb.so` 模块的最后一种用途是 **module_type session**。此时，它将登录成功和失败发送到系统日志。

## "Other" 文件

如前所述，如果 PAM 无法找到特定于某个应用程序的配置文件，它将使用通用的配置文件代替。这个通用的配置文件被称为 `/etc/pam.d/other`。默认情况下，“other”配置文件设置为偏执的设置，使得所有认证尝试都被记录并立即拒绝。建议你保持这种设置。

