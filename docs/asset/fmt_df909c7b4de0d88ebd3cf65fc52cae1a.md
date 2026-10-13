
## 充分利用可插身份模块 (PAM)

在许多较新的系统中，PAM 配置被分在存储于 `/etc/pam.d/` 目录下的多个文件中。每个文件以其处理的服务命名，因此文件内部的每个操作都省略了服务标识符。列表 5.4 的等效文件 `/etc/pam.d/login` 文件可能包含：

| auth required pam_securetty.so |
| auth required pam_pwdb.so |
| auth required pam_nologin.so |
| auth optional pam_mail.so |
| account required pam_pwdb.so |
| session required pam_pwdb.so |
| session optional pam_lastlog.so |
| password required pam_pwdb.so |

最终，结果是相同的。如果 `/etc/pam.d/` 目录存在，它将被专门使用，而 `/etc/pam.conf` 文件将被忽略。

由于这些规则中的每一个都属于 `login` 服务，每当用户尝试登录时，整个栈都会被处理。让我们逐条查看栈规则。请参考之前提到的 PAM 模块参考指南以获取每个模块及其属性的详细说明。操作将按此顺序进行：

- 1. `pam_security.so` 模块检查请求的用户是否允许在控制台登录，此操作通过与 `/etc/security` 文件比较用户的登录位置来实现（强制）。
- 2. `pam_pwdb.so` 模块被调用以检查用户是否有正确的密码。此操作也是强制的。
- 3. `pam_nologin.so` 模块被调用以检查 `/etc/nologin` 文件是否存在。如果是，则显示该文件并最终失败登录。此操作也是强制的。
- 4. `pam_mail.so` 模块被调用以检查用户是否有新邮件。此操作是可选的，根据是否有新邮件，用户将被允许登录。
- 5. `pam_pwdb.so` 模块再次被调用，此时在 `account` 上下文中，导致检查密码过期。如果账户过期或用户拒绝输入新密码，操作将失败。此操作对于 `login` 是强制的。
- 6. `pam_pwdb.so` 模块再次被调用，此时在 `session` 上下文中，导致在系统日志中记录登录尝试。如果系统无法记录，用户将不允许登录。此操作是强制的。
- 7. `pam_lastlog.so` 模块被调用以更新 `/var/log/lastlog` 中的登录历史。
- 8. `pam_pwdb.so` 模块最后一次调用，在 `/etc/shadow` 文件中替换密码，以防登录过程中（步骤5）已更新密码。此操作也是强制的，意味着如果系统无法完成，用户将不允许登录。

此操作栈代表了从开始到结束的用户登录整个验证过程。如果这一点看起来有些模糊，请尝试参考 PAM 系统管理员指南获取详细信息。然而，最好的方法是直接开始使用 PAM。

### 让 PAM 发挥作用：密码过期

现在你已经在某种程度上理解了 PAM 如何工作，我们将修改几个 PAM 服务栈。我们要修改的第一个是密码服务，它负责更新用户的登录密码。所有用户密码都经过良好的选择是重要的。它们应该长两个字符，并且避免使用字典单词。

大多数发行版现在默认都包含了良好的密码选择强制——但如果你发现你的发行版并非如此，我们将描述一个可能的 `/etc/pam.d/passwd` 文件。

首先，我们需要验证系统上是否存在 `pam_cracklib.so` 模块。假设你的文件数据库是完好的，你应该能够发现是否存在 `pam_cracklib.so` 以及所需的字典：

```
locate pam_cracklib.so dict | grep crack
```

如果通过此命令能够找到 `pam_cracklib.so` 以及 `crack` 字典文件或一组字典文件，那么理论上就可以启用密码强制。只需用井号 (`#`) 注释掉 `/etc/pam.d/passwd` 文件中的现有行，并替换为列表 9.2 中的内容即可。

#### 列表 9.2 强制 `/etc/pam.d/passwd` 文件

```
password required pam_cracklib.so type=user retry=3

password required pam_pwdb.so useauthtok
```

### 充分利用可插身份模块 (PAM)

如果你使用的是 `/etc/pam.conf` 文件而不是 `/etc/pam.d/` 目录，请在文件中搜索以 `passwd` 开头的行。将它们注释掉并替换为列表 9.3 所示的行。

#### 列表 9.3 `/etc/pam.conf` 的强制密码行

```
passwd required pam_cracklib.so type=user retry=3

passwd required pam_pwdb.so useauthtok
```

注意，如果你有 MD5 密码，在任何情况下可能都需要第二行的末尾添加空格和 `md5` 单词。

这些更改将导致 PAM 系统要求用户提供更好的密码，而不是毫无抱怨地接受坏密码。这个小型 `passwd` 栈背后的理论如下：

- 当用户输入所需的密码时，将密码与常用词字典进行检查。此任务由 `pam_cracklib.so` 模块执行，并且为了继续执行栈是强制的。
- 在放弃之前最多请求三次良好的密码（`retry=3` 参数）。
- 如果用户输入了良好的密码（`pam_cracklib.so` 模块成功完成），使用 `pam_pwdb.so` 模块（负责管理密码数据库）更新身份令牌（密码）。

这个简单的更改允许系统管理员要求用户选择良好的密码，而无需知道密码是什么，或安装第三方软件或后市密码工具。

### 强制 wheel 组

在 Unix 类系统中，传统做法是只有当相关用户是 `wheel` 组的成员时才允许某些操作发生，该组按照习惯保留给具有系统管理类型访问的用户。在实际限制于 `wheel` 组的操作中，包含了 `su` 命令，它允许一个用户接管另一个用户的 UID，通常是 `root` 用户。

许多用户惊讶地发现，Linux 系统默认并不强制执行 `wheel` 组，这意味着只要知道密码，任何用户都可以执行 `su` 命令并使用它以 `root` 身份登录。显然，能够完全执行 `su` 这种操作的能力对于普通用户来说是一个安全风险。让我们纠正这种局面。

## 第 9 小时

如果你不了解 `wheel` 组（`wheel group`），不用担心——它的实现并不困难。`wheel` 组简单来说就是限制某些敏感服务（如 `su`）的访问权限给被授予了管理员权限的一组用户。你可能在 `/etc/group` 文件中已经有一个 `wheel` 组了。如果没有，只需使用 `groupadd` 添加一个该组，并根据需要将用户添加到 `wheel` 组中，以创建你的管理员类别。例如，如果你想让 `frank`、`mary` 和 `joe` 成为管理员，那么你的 `/etc/group` 文件中的 `wheel` 条目可能如下所示：

```
wheel::1:frank,joe
```

这一行使得 `frank`、`mary` 和 `joe` 成为 `wheel` 组的成员。然后，使用本节中记录的简单技术，你可以仅向这些用户授予对 `su` 服务的访问权限。

我们将修改 `/etc/pam.d/su` 文件，该文件控制 `su` 命令的身份验证行为，将其改为以下行为：

- 仅允许 `wheel` 组的用户使用 `su`。
- 要求所有用户（包括 `root`）在尝试使用 `su` 获取 `root` 级权限时输入密码。
- 记录所有的 `su` 使用情况。

更新后的 `/etc/pam.d/su` 文件如列表 9.4 所示。

#### 列表 9.4 更新后的 `/etc/pam.d/su`

```
auth       required pam_warn.so

auth       requisite pam_wheel.so group=wheel

auth       required pam_pwdb.so

account    required pam_pwdb.so

password   required pam_pwdb.so use_authtok

session    required pam_pwdb.so
```

在这个 `/etc/pam.d/su` 文件中，`pam_pwdb.so` 模块显而易见，该模块在 PAM 用户指南中有详尽文档，并在其他 PAM 配置文件中经常被使用。这里新引入的是 `pam_wheel.so` 模块，它仅仅是检查用户是否为 `wheel` 组的成员。因为它被标记为 `requisite`（强制性），如果栈失败（当用户不是 `wheel` 组成员时），栈将立即以失败退出而不会继续执行。因此，只有 `wheel` 组成员会被要求输入密码。所有其他人从一开始就会被拒绝。

## 充分利用可插身份验证模块 (PAM)

如果你想实现 `wheel` 机制并保护 `su` 免受非 `wheel` 成员的访问，你应该应该采取一步：将 `su` 二进制文件的所有者改为 `wheel` 组，并移除公共执行权限，如下：
