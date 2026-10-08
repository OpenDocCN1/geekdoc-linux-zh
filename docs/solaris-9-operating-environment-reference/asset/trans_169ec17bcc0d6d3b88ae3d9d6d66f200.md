

# 1508

# uux

```
castle% uux "!diff sys!/home/dan/filenames2!/a4/dan/filename2 \
!/filename.diff"
```

PUBDIR 是 uucp 源码中定义的公共目录。默认情况下，该目录为 `/var/spool/uucpublic`。

uux 尝试将所有适当的文件发送到指定的系统，并在那里进行处理。对于输出文件，请使用括号对文件名进行转义。例如，以下命令从系统 b 获取 `/usr/filename` 并将其发送到系统 a，对该文件执行 `cut` 命令，并将 `cut` 命令的结果发送到系统 c。

```
castle% uux "a:cut -f1 b!/usr/filename <c!/usr/filename"
```

如果远程系统上的请求命令被禁用，uux 会发出通知。你可以使用 `-n` 选项关闭此通知。响应将通过远程系统的邮件返回。

以下限制适用于处理 uux 的 shell 管道进程：

- 通过引用命令字符串或将特殊字符作为单独参数，来对任何特殊的 shell 字符（如 `<`, `>`, `;`, `|`）进行引用。
- 在从不同系统收集文件时，uux 不执行路径名扩展。因此，如 `uux ^c9 remsys!~*.c` 的请求将尝试将字面上名为 `*.c` 的文件复制到本地系统。
- shell 管道中的第一个命令可以带有系统名。所有其他命令都在第一个命令所在的系统上执行。
- 使用 shell 元字符 `<<` 和 `>>` 可能无法实现你预期的功能。
- shell 对重定向运算符 `>>`、`<<`、`|` 或 `&` 进行分词。
- 你不能在管道开头使用保留字 `!` 来修改状态。
- 不执行别名（alias）替换。

# 注意事项

在远程系统上执行命令发生在 uucp 系统知的目录中。

执行所需的所有文件都会放在此目录中，除非它们位于同一系统。因此，简单的文件名（不带路径或系统引用）在 uux 请求中必须是唯一的。以下命令不起：

```
castle% uux "a:diff b!/home/dan/dyz c!/home/dan/xyz >!/xyz.diff"
```

但如果 `diff` 是允许的命令，则以下命令有效：

```
castle% uux "a:diff a!/home/dan/dyz c!/home/dan/xyz >!/xyz.diff"
```

受保护的文件和位于受保护目录的文件可以通过 uux 命令在命令中发送。然而，如果请求者是 root 且该目录对其他人不可搜索，则请求将失败。

# 选项

- 指定命令字符串来自标准输入。
- `-aname` 使用名称作为用户作业标识，替换发起者的用户 ID。（将通知返回给用户 ID。）
- `-b` 如果退出状态为非零，则返回提供给 uux 命令的任何标准输入。
- `-c` 不将本地文件复制到池化目录以传输到远程系统（默认）。
- `-C` 强制将本地文件复制到池化目录以传输。
- `-grade` 指定等级为单个字母、数字或字母数字字符串，用于定义服务等级。参考 `uuglist(1C)` 来确定是否可以使用单个字母、数字或字母数字字符串作为服务等级。`uuglist` 命令的输出是可用服务等级列表，或提示使用单个字母或数字作为服务等级的消息。
- `-j` 在标准输出上输出作业 ID，即作业标识。`ustat(1C)` 可以使用此作业标识来获取状态或终止作业。
- `-n` 如果命令失败，不通知用户。
- `-p` 与 `-` 相同。指定命令字符串来自标准输入。
- `-r` 将作业排队但不启动文件传输。
- `-filename` 在 `filename` 中报告传输状态。接受此选项是为了兼容性，但因为不安全会被忽略。
- `-xdebug-level` 在标准输出上产生调试输出。指定调试级别为 0 到 9 之间的数字；随着数字增加到 9，显示更详细的信息。
- `-z` 向用户发送成功通知。

# 环境变量

参见 `environ(5)` 以获取影响 uux 执行的以下环境变量描述：`LC_TYPE`、`LC_MESSAGES` 和 `NLPATH`。

# 退出状态

- 0 成功完成。
- >0 发生了错误。

# 文件

- `/etc/uucp/*`

其他数据和程序。

# 1510

```
/etc/uucp/Permissions
远程执行权限。
/usr/lib/uucp/*
其他程序。
/var/spool/uucp
池化目录。
```

# 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWmbu |

# 另见

参见以下命令的描述：`cut(1)`、`mail(1)`、`uucp(1)`、`uuglist(1C)`、`ustat(1C)`、`attributes(5)`

# vacation 自动回复

# 语法

```
/usr/bin/vacation [-I]
/usr/bin/vacation [-a]
/usr/bin/vacation [username]
```

# 描述

vacation 自动回复邮件。它使用家目录下的 `.forward` 文件来转发邮件。当 vacation 程序激活时，它使用 `.vacation.pag` 和 `.vacation.dir` 文件存储发送者列表。

在以下情况下发送回复：

- 当邮件头包含 `To:` 或 `Cc:` 行时，vacation 会向发送者回复。
- 当邮件包含 `Precedence: bulk` 或 `junk` 字符串时。
- 当邮件来自 `postmaster` 时。
- 当邮件来自 `Mailer-Daemon` 时。

# 设置 vacation

vacation 提供了一个交互式程序，你可以用它来配置 vacation。程序会自动在你的家目录下创建以下文件：

~/.vacation.msg 包含在响应传入邮件时发送的消息。

~/.forward 包含用于转发邮件的行，格式取决于 vacation 运行。

~/.vacation.pag

要设置 vacation，输入不带参数的命令。如果家目录下没有 `.vacation.msg` 文件，vacation 将创建一个默认消息并启动一个允许你修改的编辑器。如果有 `.vacation.msg` 文件，vacation 使用 `VISUAL` 或 `EDITOR` 环境变量来确定调用何种编辑器。如果家目录下已存在 `.vacation.msg` 文件，vacation 会询问你是否要编辑它。如果未设置任何环境变量，vacation 将使用 `vi` 作为编辑器。以下示例使用家目录下已存在的 `.vacation.msg` 文件设置了 vacation。

```
castle%
```

该程序可以在你休假时自动回答你的邮件。
你有一个 `/export/home/winsor/.vacation.msg` 文件。
你想看它吗？y
From: winsor (通过 vacation 程序)
Subject: away from my mail

我将一段时间不查看邮件。
关于 "SUBJECT" 的邮件将在我回来后阅读。
你想编辑它吗？n
启用 vacation 功能将创建一个 ".forward" 文件。
你想启用 vacation 功能吗？y
Vacation 功能已启用。请记住在度假回来将其关闭。旅途愉快。

当 vacation 启用时，邮件会将会将副本发送给 username，并将另一个副本交给 vacation。

# 禁用 vacation

.forward 文件的存在决定 vacation 是否启用。要禁用 vacation，请删除 .forward 文件或将其重命名。

你可以使用 vacation 程序来禁用 vacation。如果家目录下存在 .forward 文件，将询问你是否要删除它以禁用 vacation 并结束安装。现有的 `.vacation.msg`、`.vacation.pag` 和 `.vacation.dir` 文件不受影响。以下示例使用 vacation 命令来禁用 vacation。

```
castle%
```

该程序可以在你休假时自动回答你的邮件。下一步 *

