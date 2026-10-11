
- 描述 Shell 的构建模块
- 讨论 Bash 初始化文件
- 查看 Shell 如何执行命令
- 了解一些简单的脚本示例

## 1.1 常见的 shell 程序

UNIX shell 程序用于解释用户命令，这些命令可以由用户输入，也可以从一个名为 shell 或 shell 程序的文件中读取。shell 脚本是被解释执行的，而不是编译的。shell 会逐行从脚本中读取命令，并在系统中搜索这些命令（见第 1.2 节），而编译器则将程序转换为机器可读的格式，即一个可执行文件——该文件随后后可以在 shell 脚本中使用。

除了向内核传递命令外，shell 的主要任务是提供用户环境，该环境可以使用特定的 shell 资源配置文件进行单独配置。

### 1.1.1 Shell 类型

就像人们了解不同的语言和方言一样，你的 UNIX 系统通常提供多种类型的 shell：

- `sh` 或 Bourne shell：在 UNIX 系统和与 UNIX 环境中仍在使用的原始 shell。这是基础 shell，一个功能较少的小程序。虽然它不是标准 shell，但为了兼容 UNIX 程序，它在每个 Linux 系统上都是可用的。
- `bash` 或 Bourne Again shell：标准的 GNU shell，直观且灵活。对于初学者来说可能是理想选择，同时对于高级和专业用户来说也是一个强大的工具。在 Linux 上，`bash` 是普通用户的标准 shell。这种 shell 被称为 Bourne shell 的*超集*，包含了一系列附加和插件。这意味着 Bourne Again 兼容 Bourne shell：在 `sh` 中运行的命令在本书中同样有效。然而，反过来则并不总是如此。书中的所有示例和练习都使用 `bash`。
- `csh` 或 C shell：该 shell 的语法类似于 C 语言语言。有时会被程序员所青睐。
- `tcsh` 或 Turbo C shell：常用 C shell 的超集，增强了用户友好性和速度。
- `ksh` 或 Korn shell：有时受到具有 UNIX 背景的人的青睐。它是 Bourne shell 的超集；在标准配置下对初学者来说是一场噩梦。

文件 `/etc/shells` 提供了 Linux 系统上已知 shell 的概览：

## 1.2 Bourne Shell 的优点

```bash
mia:> cat /etc/shells
/bin/bash
/bin/sh
/bin/tcsh
/bin/csh
```

你的默认 shell 设置在 `/etc/passwd` 文件中，如下所示的用户 mia 的行：

```bash
mia:L2NOfqdPrHWE:504:504:mia Maya:/home/mia:/bin/bash
```

要从一个 shell 切换到另一个 shell，只需在活动终端中输入新 shell 的名称。系统通过 `PATH` 设置找到该名称所在的目录，由于 shell 是一个可执行文件（程序），当前 shell 会激活并执行它。通常会显示一个新的提示符，因为每个 shell 都有其典型的外观：

```bash
mia:> tcsh
[mia@post21 ~]$
```

## 1.2 Bourne Again Shell 的优点

GNU 项目（GNU 的 UNIX）提供了用于类 Unix 系统管理的工具，这些工具是自由软件并符合 UNIX 标准。

`Bash` 是一种兼容 `sh` 的 shell，它结合了 Korn shell (`ksh`) 和 C shell (`csh`) 的有用功能。它旨在符合 IEEE POSIX P1003.2/ISO 9945.2 Shell 和工具标准。在编程和交互式使用方面，它相比 `sh` 提供了功能性改进；这些包括命令行编辑、无限制大小的命令历史、作业控制、shell 函数和别名、无限制大小的索引数组以及从二到六十四任何基数的整数运算。`Bash` 可以在不修改的情况下运行大多数 `sh` 脚本。

与其他 GNU 项目一样，`bash` 倡议是为了保留、保护和促进使用、学习、复制、修改和重新发布软件的自由。众所周知，这种条件能激发创造力。`bash` 程序也是如此，它有很多其他 shell 无法提供的额外功能。

### 1.2.1 调用

除了可以使用 `set` shell 内置命令配置的单字符 shell 命令行选项外，还有几种你可以使用的多字符选项。我们将在本章及接后的章节中遇到几个最流行的选项；完整列表可以在 Bash info 页面找到：Bash features → Invoking Bash。

### 1.2.2 Bash 启动文件

`Bash` 根据你调用它的方式读取不同的启动文件。

**作为交互式登录 shell 调用，或带有‘login’ 参数**

交互式意味着你可以输入命令。shell 并不是因为脚本被激活而运行。登录 shell 意味着你在通过系统身份验证（通常通过提供用户名和密码）后获得了 shell。

读取的文件：

- `/etc/profile`
- `~/.bash_profile`、`~/.bash_login` 或 `~/.profile`：第一个存在的可读文件
- 退出登录时读取 `~/.bash_logout`。

如果配置文件存在但不可读，则会打印错误信息。如果文件不存在，`bash` 将搜索下一个。

**作为交互式非登录 shell 调用**

非登录 shell 意味着你不需要对系统进行身份验证。例如，当你使用图标或菜单项打开终端时，这就是非登录 shell。

读取的文件：

- `~/.bashrc`

此文件通常在 `~/.bash_profile` 中被引用。

**非交互式调用**

所有脚本都使用非交互式 shell。它们被设计为执行某些任务，不能被指令执行除其编写任务之外的其他工作。

读取的文件：

- 由 `BASH_ENV` 定义

如果你想使用此文件，`PATH` 不用于搜索该文件。

**通过 sh 命令调用**

`Bash` 尝试以符合 POSIX 标准的方式运行，即使是交互式的。

读取的文件：

- `/etc/profile`
- `~/.profile`

在交互式调用时，`ENV` 变量可以指向额外的启动信息。

### POSIX 模式

此选项通过 `set` 内置命令启用：

```bash
set -o posix
```

或者通过带有 `--posix` 选项调用 `bash`。此时 `bash` 将尽可能遵循 POSIX 标准的行为。

读取的文件：

- 由 `ENV` 变量定义。

**远程调用**

通过 `rsh` 调用时读取的文件：

- `~/.bashrc`

### 避免使用 r-

注意使用 `rlogin`、`telnet`、`rsh` 和 `rcp` 等工具的危险性，因为这些数据在网络上传输是不安全的。如果你需要远程执行、文件传输等工具，请使用通常被称为 `SSH` 的安全 Shell，从 <http://www.openssh.org> 获取。

### 当 UID 不等于 EUID 时调用

当 Bash 进程的有效用户 ID (`EUID`) 与调用脚本的用户 ID 不同时，`Bash` 不读取任何启动文件。这种情况通常出现在 `setuid` 脚本中；更多信息请参见 `setuid` 手页。

## 交互式 shell

交互式 shell 通常从终端读取并写入用户的终端：输入和输出都连接到终端。当 `bash` 命令作为非选项参数调用时，会启动交互式行为，这允许设置位置参数（见第三章“Bash 环境”）。

此 shell 是交互式的？通过查看特殊参数 `$-` 的内容进行测试，当 shell 是交互式的，它包含 'i'：

```bash
eddy:$ echo $-
i
```

在非交互式 shell 中，提示符 `PS1` 未设置。

交互式 shell 行为的区别：

- `Bash` 读取启动文件。
- 默认启用作业控制。
- 设置了提示符，多行命令启用 `PS2`，它通常设置为“>>”。当 shell 认为你输入了未完成的命令（例如忘记引号、命令结构等）时，也会得到这个提示符。
- 默认使用 `readline` 从命令行读取命令。
- `Bash` 解释 shell 选项 `ignoreeof` 而在接收到 EOF（文件结束）时立即退出。
- 默认启用命令历史和历史扩展。历史在 shell 时保存到 `HISTFILE` 指向的文件。默认情况下，`HISTFILE` 指向 `"$HOME/.bash_history"`。
- 启用别名。
- 在没有捕获器的情况下，`SIGTERM` 信号被忽略。
- 在没有捕获器的情况下，`SIGINT` 被捕获并处理。因此，例如输入 Ctrl+C 不会退出交互式 shell。
- 退出时向所有作业发送 `SIGHUP` 信号是通过 `hunuponxit` 选项配置的。

## 1.2 Bourne Again Shell 的优势

- 命令在读取时立即执行。
- `Bash` 会定期检查邮件。
- `Bash` 可以配置为在遇到未被引用的变量时退出。在交互模式下，此行为被禁用。
