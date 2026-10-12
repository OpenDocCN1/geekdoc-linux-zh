
| module-type | control-flag | module-path | arguments |
| :--- | :--- | :--- | :--- |
| | | | |

`control-flag` 字段指定根据 PAM 模块的结果采取的操作。可以为给定应用程序指定多个 PAM 模块（这称为`堆栈`）。`control-flag` 还决定了堆栈中模块的相对重要性。如我们将看到的，堆栈顺序和 `control-flags` 非常重要。该字段的四个可能值为 `required`、`requisite`、`optional` 和 `sufficient`。它们总结在表 5.2 中。

`module-path` 字段指示 PAM 模块的绝对路径名位置。Red Hat 5.2/6.0 将所有 PAM 模块放在 `/lib/security`。（第 110 页的表 5.15 提供了许多可用 PAM 模块的概览，包括 Red Hat 发行版和公共领域的模块。）

### 表 5.1 PAM 模块类型

| 模块类型 | 描述 |
| :--- | :--- |
| `auth` | `auth` 模块指示应用程序提示用户提供身份标识，如密码。它可以使用凭证，也可以授予权限。 |
| `account` | `account` 模块检查用户帐户的各种方面，如密码老化、限制对特定时间段或特定位置的访问。它也常用于基于系统资源限制系统访问。 |
| `session` | `session` 模块用于在会话建立前后提供功能。这包括设置环境、日志记录等。 |
| `password` | `password` 模块类型通常与 `auth` 模块堆叠。它负责更新用户身份验证令牌，通常是密码。 |

| 控制标志 | 描述 |
| :--- | :--- |
| `required` | 为了授予服务，此模块必须返回成功。如果此模块是一系列堆叠模块中的一个，其他所有模块仍会执行。应用程序不会被告知是哪个或哪些模块失败了。 |
| `requisite` | 同上，但在此处失败会终止所有模块的执行，并立即向应用程序返回失败状态。 |
| `optional` | 顾名思义，此模块并非必需。然而，如果它是唯一的模块，其返回给应用程序的状态可能会导致失败。 |
| `sufficient` | 如果此模块成功，堆栈中剩余的模块将被忽略，并成功返回给应用程序。具体来说，如果模块成功，这意味着堆栈中后续的模块都不会被执行，无论后续模块关联的控制标志如何。如果此模块失败，并不一定导致堆栈失败，除非它是堆栈中唯一的模块。 |

参数（`arguments`）字段用于指定传递给模块的标志或选项。指定参数是可选的。大多数模块都有一些通用的可用参数，列于表 5.3 中。其他参数则按模块提供，并将在讨论各个模块时详细说明。

简而言之，`/etc/pam.d` 中的每个文件都与其命名的服务或应用程序相关联，并且包含一系列记录列表，每条记录包含模块类型、控制标志、模块名称及位置，以及可选参数。如果模块属于同一类型，则被视为堆叠，并按照其出现的顺序执行，除非控制标志提前终止执行。整个堆栈，而不仅仅是单个模块，控制给定服务和模块类型的行为。可选地，使用参数可以进一步控制模块的行为。

现在让我们看看这种机制实际上是如何实现的。

# PAM 管理

使用免费软件的一个乐趣在于，它的文档往往很差、不正确，或者它运行得不完全正确（甚至根本无法运行！）。有各种新闻组可以发布查询（参见附录 A），一些供应商（如 Red Hat 和 S.U.S.E.）维护自己的邮件列表，有时会有所帮助。然而，通常你会发现你必须自己搞定一切。本节将超越当前可用的文档，希望能为使用 PAM 提供一个良好的起点。

## PAM 和密码

我们首先看看 PAM 如何用于控制密码选择和密码老化。示例 5-3 显示了 `/etc/pam.d/passwd` 配置文件。请注意，有两个条目使用 `passwd` 模块类型。这是一个堆叠条目的示例。让我们详细检查这些条目。这就有点复杂了，一旦我们弄清楚了，这一章的其余部分应该更容易理解。

### 示例 5-3 `/etc/pam.d/passwd` 配置文件

```
auth      required    /lib/security/pam_pwdb.so
account   required    /lib/security/pam_pwdg.so
password  required    /lib/security/pam_cracklib.so retries=3
password  required    /lib/security/pam_pwdg.so use_authtok
```

### 注意

> 在这一章中，我们经常会引用不带尾部 `.so` 的 PAM 模块。例如，在文本中我们会将 `/lib/security/pam_pwdg.so` 简称为 `pam_pwdg`，但在所有示例中，按要求会使用 `/lib/security/pam_pwdg.so`。

`/lib/security/pam_pwdg` 模块与密码数据库库（`pwdg` 库，`libpwdg`，位于 `/lib` 中）交互并依赖该库。`pwdg` 库的目的是提供用户和组关联信息的集中式数据库查找。具体来说，它为 `pam_pwdg` 提供密码源。

`pwdg` 库需要一个 `/etc/pwdg.conf` 配置文件。示例 5-4 显示了一个示例文件。该文件包含两个不同的部分——第一部分，由 `user:` 关键字引导，涉及与用户相关的信息。第二部分，由 `group:` 关键字引导，涉及与组相关的信息。在部分标题之后，你会看到由 + 号连接的关键字，称为**列表**。每个列表代表合并用于形成每个用户或组记录的一组数据库。例如，`user:` 部分下的 `unix+shadow` 列表是由 `/etc/passwd` 和 `/etc/shadow` 文件的内容组成的列表。`nis+unix+shadow` 条目指定包含 NIS（前身为 `yp`）记录以及 `/etc/passwd` 和 `/etc/shadow` 文件内容的列表。组项完全类似。

### 示例 5-4 `/etc/pwdb.conf` 文件

```
# This is the configuration file for the pwdb library
#
user:
   unix+shadow
   nis+unix+shadow
group:
   unix+shadow
   nis+unix+shadow
```

当调用 `pam_pwdb` 模块时，它反过来会调用 `pwdb` 库。`pwdb` 库将基于 `/etc/pwdb.conf` 中的条目，找到与 `pam_pwdb` 传入的用户或组匹配的第一个条目。因此，该文件中的顺序很重要。首先出现的列表先被搜索，`pwdb` 会在第一个匹配处停止。

`pam_pwdb` 模块能够支持所有四种模块类型的操作。

**`auth` 模块类型。** 当指定 `auth` 类型时，它通过提示用户输入密码并查询 `pwdb` 的用户名/密码对来执行用户认证功能。它可以接受以下参数：`debug`、`use_first_pass`、`try_first_pass`、`nullok` 和 `nodelay`。所有 `pam_pwdb` 支持但 `auth` 模块类型不支持的其他参数将被静默忽略。其他任何参数都会通过 `syslog` 记录为错误，但不会影响模块的功能。前三个参数在 85 页的表 5.3 中有描述。

`nullok` 参数允许没有密码的账户。当然，你永远不会指定这个参数，对吧？因此，默认行为是，该模块将没有密码的账户视为锁定的账户。这很好！

`nodelay` 参数导致该模块在失败时立即返回。通常，该模块在报告认证失败之前会进行延迟，这使得攻击者更难猜测密码。

那么，第 86 页示例 5-3 中这一行的目的是什么：

```
auth            required       /lib/security/pam_pwdb.so
```

它使用户在被（`pam_cracklib`）提示输入新密码之前，先被提示输入旧密码！很酷，不是吗？`root` 用户例外于此要求。

**`password` 模块类型** 当 `pam_pwhd` 模块作为 `password` 模块类型使用时，它执行更新密码的任务。这意味着，当用户调用 `passwd` 命令时，在成功输入新密码（由 `pam_cracklib` 确定）后，`pam_pwhd` 将使用 `pwhd` 库更新新密码。可接受的参数类型包括 `debug`、`nullok`; `not_set_pass`; `use_authtok`; `try_first_pass`; `use_first_pass`; `md5`, `bigcrypt`; `shadow`; `radius`; `unix`。那些尚未讨论的参数在表 5.4 中进行了总结。
