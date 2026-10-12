
```bash
[student@localhost ~]$ more .forward
| /bin/procmail
```

为什么这比重新配置 `MTA` 更好？有几点需要考虑：

- 虽然我们可以创建一个全局的 `procmail` 配置（即 `/etc/procmailrc` 文件），但这通常只在你将 `procmail` 作为垃圾邮件过滤器时才会这样做。由于特定的垃圾邮件过滤器程序比 `procmail` 更健壮，因此 `procmail` 在此功能上并不常用（除非是个别情况）。如果没有有效的 `procmail` 配置文件，则只使用个人配置。
- 并不是所有用户都想使用 `procmail`。大多数用户认为创建规则的过程具有挑战性。如果 `MTA` 被配置为使用 `procmail` 且只有少数用户在创建规则，那么 `procmail` 将会在没有有效理由的情况下被反复调用。

**注意**：作为系统管理员，你可以将 `procmail` 规则放置在 `/etc/procmailrc` 文件中。然而，你应该避免放置任何执行外部命令的规则。这些命令将以 `root` 用户身份运行，可能会导致你的系统出现安全问题。

因此，除非大多数用户都在使用 `procmail` 规则，或者你正在使用全局配置文件，否则用户通过他们自己的 `.forward` 文件调用 `procmail` 是有意义的。你为用户提供了一种简单的方法，通过注释掉他们自己 `.forward` 文件中的那一行来临时禁用 `procmail`。

## `procmail` 规则

`procmail` 规则的语法为：

```
:0 [flags] [:lockfile]
* [conditions]
Action
```

`:0` 通知 `procmail` 这是一个新规则的开始。`[flags]` 用于修改规则匹配的工作。表 33-2 描述了这些标志。

### 表 33-2 `procmail` 标志

| 标志 | 说明 |
|---|---|
| `H` | 仅匹配消息的头部部分。这是默认值。 |
| `B` | 在消息正文中进行匹配。 |
| `D` | 区分大小写的匹配。（默认是不区分大小写的） |
| `c` | 在抄送 (cc) 上执行匹配。 |
| `w` | 等待操作完成。如果操作失败；`procmail` 将继续解析匹配规则。 |
| `W` | 作用类似于 `w`，但会抑制“程序失败”消息。 |

可以通过执行 `procmail -h` 命令查看额外的过滤器，如示例 33-1 所示。

### 示例 33-1 `procmail -h` 命令

```bash
[student@localhost ~]$ procmail -h 2>&1 | tail -12
Recipe quick flag reference:
 H egrep header             B egrep body
D distinguishing case
A also execute this recipe if the common condition matched same as ‘A’, but only if the previous recipe was successful
 E else execute this recipe, if the preceding recipe didn’t match
 e on error execute this recipe, if the previous recipe failed
h deliver header (default)     b deliver body (default)
f filter                 i ignore write errors
c carbon copy or clone message
w wait for a program      r raw mode, mail as as is
nW same as 'w', but suppress 'Program failure' messages
```

*注：原文中 `mail as as is` 似乎有笔误，通常应为 `mail as is`，但按要求保持代码原样。*

`[:lockfile]` 是一个文件名（或字符），它告诉 `procmail` 工具程序通知其他进程它正在处理一个文件。这防止了在同一条消息上发生重复操作。在大多数情况下，指定 `:` 为锁文件也是一样，这允许 `procmail` 工具程序选取它自己的文件名。

`[conditions]` 行用于执行模式匹配本身。`[condition]` 行必须以 `*` 字符开头才有效。

`procmail` 工具程序使用 `egrep` 命令来执行模式匹配。你应该根据之前的经验了解 `egrep` 命令；表 33-3 提要了 `egrep` 工具支持的一些更重要的模式匹配字符。

### 表 33-3 `egrep` 模式匹配字符

| 字符 | 说明 |
|---|---|
| `*` | 匹配零或多个前一个字符。 |
| `+` | 匹配一个或多个前一个字符。 |
| `{x;y}` | 匹配前一个字符 `x` 到 `y` 次。 |
| `.` | 匹配任何单个字符（换行符除外）。 |
| `[range]` | 匹配 "[]" 字符列出的单个字符。 |
| `^` | 匹配行首。 |
| `$` | 匹配行尾。 |
| `\|` | 选择（或操作）。 |
| `\n` | 匹配换行符。 |

## 表 33-4 `procmail` 动作

| 动作 | 说明 |
|---|---|
| `Filename` | 一个文件名（或字符），告诉 `procmail` 工具程序通知其他进程它正在处理一个文件。 |
| `Another program` | 可以用于将消息发送到另一个程序。 |
| `E-mail address` | 可以用于路由消息。 |
| `Nested block` | 用于将多个动作组合在一起。 |

`[:lockfile]` 是一个文件名（或字符），告诉 `procmail` 工具程序通知其他进程它正在处理一个文件。这防止了在同一条消息上发生重复操作。在大多数情况下，指定 `:` 为锁文件也是一样，允许 `procmail` 工具程序选取它自己的文件名。

`[conditions]` 行用于执行模式匹配本身。`[condition]` 行必须以 `*` 字符开头才有效。

`procmail` 工具程序使用 `egrep` 命令来执行模式匹配。你应该根据之前的经验了解 `egrep` 命令；表 33-3 提供了 `egrep` 工具支持的一些更重要的模式匹配字符。

作为系统管理员，你可以将 `procmail` 规则放置在 `/etc/procmailrc` 文件中。然而，你应该避免放置任何执行外部命令的规则。这些命令以 `root` 用户身份运行，可能会导致你的系统出现安全问题。

因此，除非大多数用户都在使用 `procmail` 规则，或者你正在使用全局配置文件，否则用户通过他们自己的 `.forward` 文件调用 `procmail` 是有意义的。你还为用户提供了一种简单的方法，通过注释掉他们自己 `.forward` 文件中的那一行来临时禁用 `procmail`。

## 第 3 章：管理本地邮件传递

## `procmail` 规则

`procmail` 规则的语法为：

```
:0 [flags] [:lockfile]
* [conditions]
Action
```

`:0` 通知 `procmail` 这是一个新规则的开始。`[flags]` 用于修改规则匹配的工作。表 33-2 描述了这些标志。

### 表 33-2 `procmail` 标志

| 标志 | 说明 |
|---|---|
| `H` | 仅匹配消息的头部部分。这是默认值。 |
| `B` | 在消息正文中进行匹配。 |
| `D` | 区分大小写的匹配。（默认是不区分大小写的） |
| `c` | 在抄送 (cc) 上执行匹配。 |
| `w` | 等待操作完成。如果操作失败；`procmail` 将继续解析匹配规则。 |
| `W` | 作用类似于 `w`，但会抑制“程序失败”消息。 |

可以通过执行 `procmail -h` 命令查看额外的过滤器，如示例 33-1 所示。

### 示例 33-1 `procmail -h` 命令
