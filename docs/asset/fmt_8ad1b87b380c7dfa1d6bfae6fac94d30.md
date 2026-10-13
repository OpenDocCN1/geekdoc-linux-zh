
# `wc` 命令

`wc` (word count) 命令显示文本文件或输入的行、单词和字符（或字节）。例如，在 `/etc/profile` 文件上运行此命令时，你会看到类似下面的输出：

```
$ wc /etc/profile
54 146 937 /etc/profile
```

其中：

- 第一列表示行数 (`54`)
- 第二列表示单词数 (`146`)
- 第三列表示字符数（或字节）（`937`）
- 第四列表示文件名 (`/etc/profile`)

你可以使用表 1-2 中列出的选项来获取所需的输出。

| 选项 | 操作 |
|---|---|
| `-l` | 输出行数。 |
| `-w` | 输出单词数。 |
| `-c` | 输出字节数。 |
| `-m` | 输出字符数。 |

表 1-2 `wc` 选项

以下示例显示 `/etc/profile` 中的行数：

```
$ wc -l /etc/profile
54 /etc/profile
```

尝试带其他选项运行 `wc` 查看结果。

## `wall` 命令

`wall` 命令用于向系统中所有登录用户广播消息。输入 `wall` 命令并按回车。开始输入消息，完成后按 `Ctrl+d` 进行广播。

```
# wall
```

## 在线帮助

在使用系统时，你需要获取有关命令、用法和可用选项的信息。RHEL 通过 `man`（手册）页提供在线帮助。手册页作为 RHEL 安装的一部分安装，提供了命令和配置文件的详细信息，包括简短描述、用法、选项、缺陷、额外引用和作者。

使用 `man` 命令查看命令的帮助。以下示例显示了如何检查 `passwd` 命令的手页：

```
$ man passwd
PASSWD(1)           User utilities           PASSWD(1)
```

NAME

`passwd` - 更新用户的身份令牌(s)

SYNOPSIS

`passwd [-k] [-u -f] [-d] [-x maxdays] [-w warmdays]`

`[-i inactivated] [-S] [--stdin] [username]`

DESCRIPTION

`passwd` 用于更新用户的身份令牌。

...

## 在更新之前建议一个密码。

当你在手册页中时，表 1-3 列出的一些常用键可以帮助你高效导航。

| 键 | 操作 |
|---|---|
| Enter / 下箭头 | 向前移动一行。 |
| 上箭头 | 向后移动一行。 |
| f / 空格 / 翻页 | 向前翻页。 |
| b / 翻页 | 向后翻页。 |
| d / u | 向下/上移动半页。 |
| g / G | 移动到手册页的开头/结尾。 |
| `:f` | 显示正在查看的行号和字节。 |
| q | 退出手册页。 |
| `/pattern` | forward搜索指定的模式。 |
| `?pattern` | 向后搜索指定的模式。 |
| n / N | 找到模式的下一个/上一个出现处。 |
| h | 提供导航键的帮助。 |

表 1-3 在手册页中导航

### 节

手册页有几个节。例如，第1节节用户命令，第4 节包含特殊文件，第5 节描述系统配置文件，第8 节包括系统管理命令等。

若要查找配置文件 `/etc/passwd` 的信息，请执行以下操作：

```
$ man 5 passwd
PASSWD(5) Linux Programmer's Manual PASSWD(5)
```

NAME

`passwd` - 密码文件

DESCRIPTION

`passwd` 是一个文本文件，包含了系统账户列表，为每个账户提供了一些 ...

无论是否使用影子密码，许多系统管理员使用一个

### 按关键字搜索

有时你需要使用某个命令但不知道它的名称。Linux 允许你使用 `man` 命令的 `-k` 选项或 `apropos` 命令对所有可用手册页进行关键字搜索。搜索是在 `whatis` 数据库中进行的，该数据库包含命令和文件的详细信息，并列出了包含指定关键字的所有手册页。`whatis` 数据库由 `/etc/cron.daily/makewis.cron` 脚本每天更新一次。你可以使用 `makewis` 命令手动更新它。

```
$ man -k password
$ apropos password
```

`(1) - 修改用户密码过期信息`
`2 chpasswd (8) - 批模式更新密码`
`3 cracklib (rpm) - 密码检查库。`
`4 crypt (3) - 密码和数据加密`
`5 endpasswd [getpasswd] ............ (3) - 获取密码文件条`

另一种快速确定可用选项及其简要描述的方法是在执行命令时使用 `--help` 或 `-h/?` 选项。例如，要获取 `passwd` 命令的帮助，可以执行以下任一操作：

```
passwd --help
```

```
passwd -?
```

用法: `passwd [OPTION...] <accountName>`

`-k, --keep-tokens` 保留未过期的身份令牌

`-d, --delete` 删除指定账户的密码（仅限 root）

`-l, --lock` 锁定指定账户（仅限 root）

`-u, --unlock` 解锁指定账户（仅限 root）

`-f, --force` 强制操作

```
-x, --maximum=DAYS 密码最大生存期（仅限 root）
-n, --minimum=DAYS 密码最小生存期（仅限 root）
-w, --warning=DAYS 密码过期前用户接收警告的天数（仅限 root）
-i, --inactive=DAYS 密码过期后账户被禁用的天数（仅限 root）
-S, --status 报告指定账户的密码状态（仅限 root）
-stdin 从标准输入读取新令牌（仅限 root）
```

```
帮助选项:
?, --help 显示此帮助消息
-?, --usage 显示简要的用法消息
```

### 显示简短描述

`whatis` 提供了一种在 `whatis` 数据库中快速搜索指定命令或文件的简短描述的方法。例如，以下内容显示了在 `yum.conf` 和 `passwd` 文件上运行命令时的输出：

```
whatis yum.conf
```

`yum.conf [yum] (5) - yum(8) 的配置文件`

```
whatis passwd
```

`Passwd (1) - 更新用户的身份令牌`

`Passwd (5) - 密码文件`

`Passwd (rpm) - 使用 PAM 设置/更改密码的 passwd 实用`

`passwd [passwd] (1ssl) - 计算密码哈希值`

| Linux 概览 |

第一条输出表示指定的文件是与 `yum` 命令相关的配置文件，第二个输出指向了 `passwd` 文件的四个条目。

`whatis` 命令的替代方案是使用带有 `-f` 选项的 `man` 命令产生相同的结果：

```
man -f yum.conf
```

```
man -f passwd
```
