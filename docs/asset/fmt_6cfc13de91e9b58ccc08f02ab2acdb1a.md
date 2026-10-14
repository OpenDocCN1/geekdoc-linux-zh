
| `$attr(name),%s` | sysfs 属性 |
| `$env(key), %E` | 环境变量 |
| `$major, %M` | 主设备号 |
| `$minor, %m` | 次设备号 |
| `$result, %c` | 程序输出 |
| `$parent, %P` | 父级设备名称 |
| `$sys, %S` | sysfs 中的挂载点 |
| `$$` | '$' 符号 |
| `%%` | '%' 符号 |

查看文档获取更多变量。

唯一强大的 udev 管理命令是 `udevadm`。通过此命令，你可以调试规则并查看系统状态。例如，以下命令将从 udev 视角提供 sda 设备的所有信息：

```
udevadm info -a -p /sys/block/sda
```

## PAM 模块

稍后我会经常提到 PAM 模块，所以 PAM 代表“可插拔认证模块”，它是一个广泛用于许多需要验证程序的库。该库提供了一个标准 API 并加载模块——实现验证方法的和其他其他内容，并在需要时加载。注意，它是一个库，而不是服务！

## 第 8 章 UNIX 与 LINUX – 操作技巧

通过模块实现的功能被分为四大类：

- Auth - 身份验证/凭据获取
- Account - 账户管理
- Password - 认证令牌（如密码）更新
- Session - 会话管理

`Auth` 识别用户并设置凭据（UID/GID），还会更新某些信息，如最后登录时间、设置的限制等。`Account` 检查此账户是否可用/已启用，`password` 允许更改密码（或其他认证令牌），`session`（此处应为“会话”）在用户会话开始或结束时执行任何操作。一个模块可以实现这些组的任何子集。每个 PAM 服务都有其自己的模块列表、组及其选项。

PAM 配置文件可能是“BSD 风格”的——一个包含所有服务的大文件，其中每行的第一个单词是服务名，或者一组以服务名命名的文件。在 Linux 中，主要使用第二种方法，我将采用这种方法。PAM 配置文件中行的格式为“`group flag module [options]`”，其中 `group` 是 `auth`、`account`、`password` 或 `session`；`flag` 是 `required`、`requisite`、`optional` 或条件列表；`module` 是模块；`options` 是模块选项。行按同组内的顺序进行扫描，因此顺序至关重要。

对于每一行，都会调用指定的模块，并根据结果（OK 或 FAIL）和 `flag` 采取相应的操作：

| Flag | Action |
|---|---|
| Required | OK=继续，FAIL=继续处理，但在最后拒绝请求 |
| Requisite | OK=继续，FAIL=停止处理并拒绝请求 |
| Sufficient | OK=停止处理并接受请求，FAIL=继续处理 |
| Optional | 忽略结果 |

`Flag` 也可以是格式为“`[value=action, ...]`”的列表，其中 `value` 是模块调用返回的值，`action` 是要执行的操作。可能的值如下：

| Value | 含义 |
|---|---|
| Success | 模块表示正常 = OK |
| Ignore | 模块信号希望其返回值被忽略 |
| Abort | 模块表示现在停止 |
| Default | |

“此集合中未显式提到的所有返回值”通常用于捕获所有错误/失败（因为有很多种），这会迫使你提到 `ignore=ignore`（有时是其他如 `= some obvious`），它们在默认操作下会失败。

FAIL – 列表中的所有值：`open_err`, `symbol_err`, `service_err`, `system_err`, `buf_err`, `auth_err`, `session_err`, `cred_err`, `conv_err`, `authtok_err`, `authtok_recover_err`, `user_unknown`, `perm_denied`, `cred_insufficient`, `authtinfo_unavailable`, `new_authtok_reqd`, `authtok_lock_busy`, `authtok_disable_aging`, `authtok_expired`, `acct_expired`, `maxtries`, `cred_unknown`, `cred_expired`, `try_again`, `module_unknown`, `bad_item`, `conv_again`, `incomplete`, `no_module_data`

操作可以是：

- `ok` - 模块的返回码应被视为（……如果没有错误）。
- `bad` - 将自身标记为失败（不终止）。
- `die` - 失败 + 终止。
- `done` - OK 并终止。
- `ignore` - 模块的状态不会影响栈的返回码。
- `n`（一个 >0 的整数）- OK 并跳过后续 n 条规则。
- `reset` - 清除模块状态。

在这种“列表表示法”中，我们可以定义普通 `flag` 为：

`required = [success=ok new_authtok_reqd=ok ignore=ignore default=bad]`

`requisite = [success=ok new_authtok_reqd=ok ignore=ignore default=die]`

`sufficient = [success=done new_authtok_reqd=done default=ignore]`

`optional = [success=ok new_authtok_reqd=ok default=ignore]`

这是一个简单的认证描述示例，使用了 `unix`、`permit` 和 `deny` 模块。`unix` 模块通过 `/etc/passwd` 和 `/etc/shadow` 检查密码，`pam` 允许访问，`deny` 拒绝访问：

```
auth [success=1 default=ignore] pam.so nullock_secure
auth requisite pam_deny.so
auth required pam_permit.so
```

对于规则链的调试，`debug` 模块非常有用；它会返回参数中指定的值，例如：

```
auth optional pam_debug.so auth=perm cred=denied
auth sufficient pam.debug.so auth=success cred=success
```

配置文件中的特殊指令是 `@include`，它允许包含另一个文件中的文本——通常用于公共部分。以 `#` 开头的行是注释。有很多不同的模块，但我建议至少阅读关于 `pam limits`、`pam_exec`、`pam_env`、`pam_list` 和 `access` 内容。

## Shell 技巧

命令行仍然是管理员的主要工具。原因在于它的多功能性。了解如何操作 shell 意味着能够快速解决任务当你当你同时执行几十甚至上百条命令（或者更糟，按顺序执行）时，这些技术变得尤为相关。例如，在命令行中执行至少十条命令不到一分钟。但打开浏览器并设置所需时间、选择所需菜单要花费长得多，执行这些操作的人将浪费窗口中已有的所有时间。如果你需要 100 或 1000 条命令呢？让我们分享一些在 `bash`（或 `zsh`）中工作以提高效率的技巧。

大括号指定枚举，为每个元素将创建一个不同的参数。让我们使用它：
