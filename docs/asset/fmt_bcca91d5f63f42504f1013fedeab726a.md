
请注意第 86 页示例 5-3 中指定了 `use_authtok` 参数。这意味着 `pam_pwhd` 将使用从 `pam_cracklib` 接收的新密码。本质上，`pam_cracklib` 控制新密码的选择，但 `pam_pwhd` 实际上执行更新。

### 注意

> 强烈建议使用 `md5`（MD5 在第 3 章中讨论）或 `bigcrypt`（一种修改过的 `crypt(3)`，允许最多 16 个字符的密码）参数，而不是默认的、传统的 UNIX `crypt(3)` 散列。它允许更长的密码，可能更难被诸如 `Crack`（在第 12 章中讨论）等程序猜测。在 Red Hat 6.0 中，选择 MD5 是安装时的选项。

| 标准参数 | 描述 |
| :--- | :--- |
| `debug` | 生成额外的输出到 `syslog` 实用程序。大多数 PAM 模块支持此参数。其确切定义取决于提供此参数的模块。 |
| `no_warn` | 不向应用程序传递警告消息。 |
| `use_first_pass` | 此模块将使用上一个模块的密码。如果失败，则不尝试从用户获取另一个条目。此参数仅适用于 `auth` 和 `password` 模块。 |
| `try_first_pass` | 同上，但不同之处在于，如果密码失败，它将提示用户输入另一个条目。此参数仅适用于 `auth` 和 `password` 模块。 |

> `syslog` 实用程序在第 8 章中详细讨论。

| 参数 | 描述 |
| :--- | :--- |
| `nullok` | 允许更改空（不存在）密码。鉴于前面所述原因，不建议使用此参数。 |
| `not_set_pass` | 导致此模块忽略来自前一个模块的密码，并禁止此模块将新密码传递给后续模块。 |
| `use_authtok` | 此参数强制模块将新密码设置为从前一个堆叠模块接收到的密码。 |
| `md5`, `bigcrypt` | 除了使用传统的 UNIX 密码散列算法（通过 `crypt` 函数调用实现），你可以选择其中一种。 |
| `shadow`, `radius`, `unix` | 允许通过 `pwhd` 库在数据库之间传输密码。 |

1. 有关 `NIS` 的更多详细信息，请参见第 3 章。`NIS` 以前被称为 Yellow Pages (`YP`)。

2. RSA Data Security, Inc., MD5 Message-Digest Algorithm.

模块类型 `account`（账户）。当使用 `pam_pwdb` 作为账户模块类型时，其目的是验证用户的账户信息。这包括验证用户是否拥有账户、用户是否关联了密码老化参数（如果有），以及用户是否需要关于即将过期的密码警告或关于选择新密码的建议。作为此模块类型，`pam_pwdb` 仅识别 `debug` 参数。

模块类型 `session`（会话）。当使用 `pam_pwdb` 作为会话模块类型时，其唯一目的是将用户名和服务类型记录到 `syslog` 中，分别在登录时和随后的注销时进行。它不识别任何参数。

## pam_cracklib 模块

`pam_cracklib` 模块仅旨在与密码模块类型配合使用。其目的是检查密码的强度和长度，这两个元素都可以通过下文描述的参数进行配置。该模块仅能在堆栈中工作，因为它没有更新功能。它需要 `libc` `crack` 库和 `cracklib_dict` `Crack` 字典，两者都位于 Red Hat 5.2/6.0 发行版的 `/usr/lib` 目录下。正如你可以看到的，该模块严重依赖于 `Crack` 实用程序中的元素，这些内容在第 12 章中有详细讨论。

PAM 的灵活性体现在事实：这并不是唯一的密码强度检查 PAM 模块。另一个是 `pam_passwd`，可以在 [http://www.us.kernel.org/pub/linux/libs/pam/modules.html](http://www.kernel.org/pub/linux/libs/pam/modules.html) 上获取。

`pam_cracklib` 可用的参数描述见表 5.5。

### 表 5.5 pam_cracklib 的参数

| 参数 | 描述 |
| :--- | :--- |
| `debug` | 该参数会将额外的模块行为信息写入 `syslog`，但不会记录密码。 |
| `type=字符串` | 该参数将在其生成的消息中用 字符串 替换 UNIX 字符串，例如 New UNIX password（新的 UNIX 密码）。 |
| `retry=n` | 这是该模块允许用户在更改密码时重试的次数。默认值为 1。 |
| `difok=n` | 这表示新密码中必须与旧密码不同的字符数。默认值为 10。然而，无论此限制如何，如果新密码中至少有一半的字符与旧密码不同，将被接受。 |
| `minlen=n` | 该参数指定最小密码长度 + 1。默认设置为 9，这意味着实际最小密码长度为 10。为了进一步混淆问题，根据下面列出的 `\*credit` 参数指定的值，此最小长度实际上可能会缩短。 |
| `lcredit=n` | 此处指定的值表示由于新密码中至少包含一个小写字符，`minlen` 值被减少的字符数。默认值为 1。可以设置为 0 以消除信用。 |
| `ucredit=n` | 此处指定的值表示由于新密码中至少包含一个大写字母，`minlen` 值被减少的字符数。默认值为 1。可以设置为 0 以消除信用。 |
| `dcredit=n` | 此处指定的值表示由于新密码中至少包含一个数字字符，`minlen` 值被减少的字符数。默认值为 1。可以设置为 0 以消除信用。 |
| `ocredit=n` | 此处指定的值表示由于新密码中至少包含一个非字母数字字符，`minlen` 值被减少的字符数。默认值为 1。可以设置为 0 以消除信用。 |

除了表 5.5 中可配置选项外，`pam_cracklib` 还通过以下方式检查新密码的强度：

1. 验证新密码不是旧密码的逆序。
2. 验证新密码不是旧密码某些字符的简单大小写变化。
3. 检查新密码是否在 `cracklib.dict` 中。如果在其中，它会警告用户，但不会强制选择另一个密码。

## 在密码模块类型中叠加 pam_pwdb 和 pam_cracklib 的影响

在本节中，我们将看看 `pam_cracklib` 如何在第 86 页示例 5-3 所示的堆栈中与 `pam_pwdb` 相互作用。

回想一下，在示例 5-3 中，这两个叠加条目出现在 `/etc/pam.d/password` 中。

```
password    required    /lib/security/pam_cracklib.so retry=3
password    required    /lib/security/pam_pwdb.so use_authtok
```

第一个条目调用 `pam_cracklib` 并提示用户输入其新密码（请记住，身份验证模块类型的 `pam_cracklib` 条目负责提示用户输入其旧密码以进行身份验证）。在用户提供新密码后，`pam_cracklib` 请求重复输入以进行验证。完成后，`pam_cracklib` 执行其检查，以确定密码是否可接受。如果是，它将新密码传递给带有 `use_authtok` 参数的 `pam_pwdb`，这意味着它将接受此新密码并要求 `pwdb` 库更新相应的数据库。

让我们通过考虑一个示例来看看这些模块的力量和灵活性。假设我们要使用 `md5` 而不是标准的 UNIX `crypt(3)` 机制来进行哈希处理。这是一个好主意，因为像 `Crack` 这样的流行密码猜测工具需要消耗更多的 CPU 资源来猜测密码（参见第 337 页上的 Crack 的白帽用途）。使用 `md5` 的主要好处是你可以要求更长的密码---20、30 甚至更多字符。让我们看一下一个要求 20 字符密码的示例。我们还将设置 `type` 参数，看看我们的用户是否注意到了变化。示例 5-5 展示了如果在 `/etc/pam.d/passwd` 中强制实施这些更改，堆栈可能是什么样子。

### 示例 5-5 在 /etc/pam.d/passwd 中使用 md5 和 minlen

```
password	required	/lib/security/pam_cracklib.so minlen=20\
			retry=3 type=SECRET
password	required	/lib/security/pam_pwb.so md5 use_authtok
```

**警告**

如果你做出类似于示例 5-5 所示的更改，你还必须更改使用密码模块类型的所有等效 `pam_pwb` 和 `pam_cracklib` 实例。在 Red Hat 5.2 中，这至少包括 `/etc/pam.d` 中的 `chfn`、`chsh`、`login`、`rlogin`、`su` 和 `xdm` 文件。
