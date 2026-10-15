
- **使用文本编辑器定义一个别名。** 将以下行添加到 `.cshrc` 文件中，为 `history` 命令创建别名：

```
alias h history
```

- **将更改写入文件并退出编辑器。**

- **使用 `source` 命令运行 `.cshrc` 文件。**

```
/home/you > source .cshrc <Return>
```

此时，别名应该已经设置好。在下一节中，您将看到如何使用该别名来运行 `history` 命令。

### 22.11 使用历史机制

历史机制保存您最近使用的命令列表，并允许您查看和重复该列表中的命令。

- **使用其别名运行 `history` 命令。** 输入 `h` 后跟 `Return` 以运行 `history` 命令：

```
/home/you > h <Return>
```

如果您正确设置了 `history` 的别名，您应该看到一个最近执行的命令的编号列表。请注意，`history` 命令本身将作为列表中的最后一项出现：

```
1  set history = 100
2  echo $history
3  cd
4  ls -a
5  cp .login .login.BAK
6  cp .cshrc .cshrc.BAK
7  echo "Your wish is my command, Oh Great One."
8  vi .login
9  source .login
10 set prompt = #
11 set prompt = 'Your Majesty? '
```

### 22.11 复习（续）

12. `vi .login`

13. `source .login`

14. `vi .login`

15. `source .login`

16. `vi calendar`

17. `source .login`

18. `vi .cshrc`

19. `. .cshrc`

20. `h`

2. **重复列表中的最近一条命令。** 这是在提示符后输入两个感叹号来实现的。试一试：

`/home/you > !!` 按回车键

你应该会看到和之前一样的另一份命令列表。

3. **通过编号重复命令。** 例如，要重复列表中的第七条命令，请输入：

`/home/you > !7` 按回车键

命令行将显示在屏幕上，并且该命令将被执行。

`echo "Your wish is my command, Oh Great One."`

`Your wish is my command, Oh Great One.`

4. **通过输入命令行的首字母来重复命令。** 因此，要重复以字母 `$s$` 开头的命令行，请输入：

`/home/you > !s` 按回车键

以 `$s$` 开头的最近一条命令是 *source* 命令：

`source .login`

### 22.12 命令摘要

**查看变量的值**

| 命令 | 描述 |
| :--- | :--- |
| `setenv` | 列出环境变量的值 |
| `set` | 列出特殊 `csh` 变量的值 |
| `echo $var` | 打印变量 `var` 的值 |

**设置变量的值**

| 命令 | 描述 |
| :--- | :--- |
| `set var = value` | 将变量 `var` 设置为 `value` |
| `set var = "A word"` | 将字符串 `A word` 存储在变量 `var` 中 |
| `setenv VAR value` | 将环境变量 `VAR` 设置为 `value` |

**执行启动文件**

| 命令 | 描述 |
| :--- | :--- |
| `source .login` | 执行 `.login` |

**更改提示符**

| 命令 | 描述 |
| :--- | :--- |
| `set prompt = "Prompt string"` | 将提示符设置为 `Prompt string` |

**创建命令别名 (csh)**

| 命令 | 描述 |
| :--- | :--- |
| `alias c command` | 将 `c` 设置为 `command` 的别名 |
| `unalias c` | 移除 `c` 作为 `command` 的别名 |

**使用历史机制 (csh)**

| 命令 | 描述 |
| :--- | :--- |
| `history` | 打印 `history` 列表 |
| `!!` | 重复 `history` 列表中最近的事件 |
| `!n` | 重复 `history` 列表中的第 `n` 个事件 |
| `!abc` | 重复以字母 `abc` 开头的最近事件 |

### 22.13 练习

1. `date` 命令打印日期和当前时间。将以下一行添加到你的 `.login` 中，并确保在 `date` 周围使用反引号：

```
`echo "The date and time are `date`."`
```

退出编辑器，并使用 `source` 命令运行 `.login`。会发生什么？

2. 上一个练习中需要反引号是为了告诉 shell 将 `date` 解释为命令，而不是单词。如果省略反引号会发生什么？试一试。打开你的 `.login` 并移除 `date` 周围的反引号：

```
echo "The date and time are date"
```

退出编辑器，并使用 `source` 命令运行 `.login`。会发生什么？（现在打开该文件并替换回反引号。）

3. 你的搜索路径是什么？

4. 你的 shell 的完整路径名是什么？

5. 更改你的提示符，使其始终显示当前工作目录。

6. `rm`、`cp` 和 `mv` 命令是危险的，因为它们可能覆盖或删除现有文件。`-i`（“交互”）选项会询问你是否确认这是你想要的操作。如果 `-i` 选项对你可用，请在你的 `.cshrc` 文件中放入以下行：

```
alias rm "rm -i"
alias cp "cp -i"
alias mv "mv -i"
```

7. 解释如果将以下行放在你的 `.cshrc` 文件中会发生什么：

```
alias m more
alias f finger
alias ls 'ls -R'
```

8. 为了防止文件被重定向操作覆盖，请在你的 `.cshrc` 中放入以下行：

```
set noclobber
```

它是否按预期工作？

# 第七部分：SHELL 脚本

## 23 SHELL 脚本

到目前为止，你一直通过键盘向 UNIX shell 输入命令。在这种使用方式下，shell 被称为命令解释器。shell 也可以作为高级编程语言使用。你不必在响应 shell 提示符时逐条输入命令，而是可以将多条命令放入一个文件中，由 shell 一次性执行。由 shell 命令组成的程序称为 *shell 脚本*。本章将向你介绍 Bourne Shell 的 shell 脚本。

### 23.1 简单的 Shell 脚本

假设你创建了一个名为 `commands` 的文件，包含以下内容：

```shell
# A simple shell script
cal
date
who
```

该文件的第一行以 `#` 符号开头，这表示*注释行*。`#` 后面的任何内容都会被 shell 忽略。其余三行是 shell 命令：第一行产生当前月份的日历，第二行显示当前日期和时间，第三行列出当前登录到你的系统的用户。

让 Bourne Shell (`sh`) 执行这些命令的一种方法是输入：

```
$ sh < commands
```

重定向运算符 `<` 告诉 shell 从文件 `commands` 读取，而不是从标准输入读取。然而，事实证明，在这种情况下，重定向符号并不是必需的。因此，你也可以通过输入以下内容来运行该命令文件：

```
$ sh commands
```

### 23.2 子 Shell

有没有办法设置 `commands`，使得你可以运行它而不必显式地调用 shell？换句话说，你能否在不先输入 `sh`、`csh` 或 `ksh` 的情况下运行 `commands`？答案是肯定的，但你首先必须使该文件*可执行*。`chmod` 实用程序可以做到这一点：

```
$ chmod u+x commands
```

参数 `u+x` 告诉 `chmod`，你要为用户 (`u`) 添加 (`+`) 执行 (`x`) 文件中 shell 脚本的权限。现在你只需要输入文件名：

```
$ commands
```

shell 就会运行文件中的命令。
