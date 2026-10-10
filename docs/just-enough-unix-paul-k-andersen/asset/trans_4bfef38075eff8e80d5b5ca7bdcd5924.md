

## 22.11 复习（续）

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

4. **通过输入命令行的首字母来重复命令。** 因此，要重复以字母 $s$ 开头的命令行，请输入：

   `/home/you > !s` 按回车键

   以 $s$ 开头的最近一条命令是 *source* 命令：

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

2. 上一个练习中需要反引号是为了告诉 shell 将 date 解释为命令，而不是单词。如果省略反引号会发生什么？试一试。打开你的 `.login` 并移除 `date` 周围的反引号：

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

参数 `u+x` 告诉 `chmod`，你要为用户 (u) 添加 (+) 执行 (x) 文件中 shell 脚本的权限。现在你只需要输入文件名：

```
$ commands
```

shell 就会运行文件中的命令。

当你告诉 shell 运行像 `commands` 文件这样的脚本时，你的登录 shell 实际上会调用另一个 shell 进程来运行该脚本。（**请记住，** shell 只是另一个程序，而 UNIX 可以同时运行多个程序。）父 shell 会等待其子进程完成，然后接管并给你一个提示符：

```
$
```

顺便提一下，子 shell 可以与其父 shell 不同。例如，你可以将 `csh` 或 `ksh` 作为你的登录 shell，但使用 `sh` 来运行你的 shell 脚本。许多用户实际上就是这样做的。当到了运行脚本的时候，`csh` 或 `ksh` 只是调用 `sh` 作为子 shell 来完成任务。

我们将始终使用 `sh` 来运行 shell 脚本。为了确保使用 `sh`，我们将在每个 shell 脚本文件的顶部包含以下行：

```
#!/bin/sh
```

因此，我们的 `commands` 文件看起来会像这样：

```shell
#!/bin/sh
# A simple shell script
cal
date
who
```

### 23.3 Shell 作为编程语言

示例脚本 `commands` 几乎微不足道——它所做的不过是执行三条简单的命令，这些命令你也可以轻松地输入到标准输入中。实际上 shell 可以做更多。事实上，它是一种成熟的编程语言，具有与其他编程语言相同的许多特性，包括：

- 变量
- 输入/输出函数
- 算术运算
- 条件表达式
- 选择结构
- 循环结构

我们将按顺序讨论这些特性。

### 23.4 变量

在 Bourne Shell 脚本中，通常使用三种类型的变量：

- *环境变量*。有时也被称为特殊 shell 变量、关键字变量、预定义 shell 变量或标准 shell 变量，它们用于定制运行环境以适合你的需求。示例包括 `TERM`、`HOME` 和 `MAIL`。
- *用户创建的变量*。这些是你自己创建的变量。
- *位置参数*。这些由 shell 用于存储命令行参数的值。

其中，环境变量和用户创建的变量已经介绍过了。然而，位置参数是新的，由于它们在 shell 编程中非常有用，我们现在将详细研究它们。

位置参数也被称为*只读变量*或*自动变量*，因为 shell 为你自动设置了它们。它们“捕获”将被 shell 脚本使用的命令行参数的值。位置参数编号为 0, 1, 2, 3,... , 9。为了说明我们的用法，请考虑以下 shell 脚本，并假设它包含在一个名为 `echo_args` 的可执行文件中：

```shell
#!/bin/sh
# Illustrate the use of positional parameters
echo $0 $1 $2 $3 $4 $5 $6 $7 $8 $9
```

