
该行表示，用户的 shell 必须列在`/etc/shells`中，用户才能成功通过`csh`认证。让我们它是如何实现的。每行配置都有三个字段：函数类型、控制参数和一个模块，顺序如下。以下是它们在该示例中的含义：

函数类型 用户应用程序请求 PAM 执行的函数。在这里，是`auth`，即验证用户的任务。

控制参数 该设置控制了 PAM 在当前行操作成功或失败后会做什么（在本示例中为`requisite`）。我们稍后会讨论这一点。

模块为该行运行的认证，决定了该行的实际作用。在这里，`pam_shells.so`模块检查用户的当前 shell 是否列在`/etc/shells`中。

PAM 配置的详情见`pam.conf(5)`手册页。让我们来看一些要点。

# 函数类型

用户应用程序可以请求 PAM 执行以下四个函数之一：

- `auth` 验证用户（检查用户是否如其所言）。
- `account` 检查用户账户状态（例如，用户是否有权执行某些操作）。
- `session` 执行仅针对用户当前会话的操作（例如显示今日消息）。
- `password` 更改用户的密码或其他凭据。

对于任何配置行，模块和函数决定了 PAM 的行为。一个模块可以有多个函数类型，因此在确定配置行的目的时，务必记住将函数和模块视为一个整体。例如，`pam_unix.so`模块在执行`auth`函数时会检查密码，但在执行`password`函数时会设置密码。

# 控制参数和堆叠规则

PAM 的一个重要特性是其配置行指定的规则是`stack`（堆叠），这意味着在执行函数时可以应用许多规则。这就是为什么控制参数如此重要：某一行中操作的成功或失败会影响后续行，或导致整个函数的成功或失败。

控制参数有两种：简单语法和更高级的语法。以下是你在规则中看到的三种简单语法控制参数：

- `sufficient`：如果此规则成功，则验证成功，PAM 不需要再查看任何其他规则。如果规则失败，PAM 将继续处理后续规则。
- `requisite`：如果此规则成功，PAM 将继续处理后续规则。如果验证失败，PAM 无需再查看任何其他规则。
- `required`：如果此规则成功，PAM 将继续处理后续规则。如果规则失败，PAM 将继续处理后续规则，但无论后续规则的最终结果如何，始终将返回验证失败。

接上文的示例，以下是一个用于`csh`验证函数的堆栈示例：

```
auth sufficient pam_rootok.so

auth requisite pam_shells.so

auth sufficient pam_unix.so

auth required pam_deny.so
```

《How Linux Works (Early Access) © 2021 by Brian Ward

通过此配置，当`csh`命令请求 PAM 执行验证函数时，PAM 将执行以下操作（流程图见图 7-4）：

1. `pam_rootok.so`模块检查`root`是否为尝试身份验证的用户。如果是，它将立即成功且不再尝试进一步验证。这是因为控制参数被设置为`sufficient`，所以 PAM 向`csh`返回成功。否则，进入第 2 步。

`(img/048936fa219_0.png)` 图 7-4：PAM 执行流程

2. `pam_shells.so`模块检查用户的 shell 是否列在`/etc/shells`中。如果不在，PAM 向`csh`返回失败。否则。

系统配置：日志、系统时间、批处理作业和用户 195

《How Linux Works (Early Access) © 2021 by Brian Ward

3. `pam_unix.so`模块向用户询问密码。控制参数设置为`sufficient`，因此 PAM 向`csh`返回成功。否则，继续执行。

4. `pam_deny.so`模块失败，因为控制参数设置为`required`，PAM 向`csh`返回失败。在这种情况下，`/etc/login.defs`中的加密算法应该在遇到不支持 PAM 的极少数情况下与 PAM 配置中的算法保持匹配。

# 注意

不要混淆函数和操作。PAM 与密码交互有两种方式：`auth`函数（用于验证密码）和`password`函数（用于设置密码）。追踪密码参数是最简单的。最好的方法是直接使用`grep`：

```bash
$ password.*unix /etc/pam.d/*
```

# 模块参数

PAM 模块可以在模块名后带有参数。你经常会遇到这种情况：

```
password pam_unix.so obscure sha512
```

参数`obscure`和`sha512`告诉 PAM 在设置密码时该做什么。首先，PAM 检查密码是否足够“`obscure`”（即密码与`shadow`密码等其他内容不太相似），然后 PAM 使用 SHA512 算法加密新密码。

# 7.10.2 关于 PAM 配置的提示

由于多年来密码验证的演变，许多密码配置遗留可能会引起困惑。首先需要注意的是文件`/etc/login.defs`。这是原始`shadow`密码套件的配置文件。它包含了关于`/etc/shadow`密码文件使用的加密算法的信息，但在安装了 PAM 的系统上它很少被使用，因为 PAM 配置已经包含了这些信息。在这种情况下，`/etc/login.defs`中的加密算法应该在遇到不支持 PAM 的极少数情况下与 PAM 配置中的算法保持匹配。

PAM 从哪里获取密码加密方案的信息？记住 PAM 与密码交互有两种方式：`auth`函数（用于验证密码）和`password`函数（用于设置密码）。追踪密码参数是最简单的。最好的方法是直接使用`grep`：

```bash
$ grep password.*unix /etc/pam.d/*
```
