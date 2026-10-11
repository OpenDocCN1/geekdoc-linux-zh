
# Linux 世界中一种不太流行的替代性 shell 是 C shell

正如你可能猜的那样，C shell 在某种程度上尝试将 C 编程语言中的功能整合到 shell 脚本中。开源实现中最流行的 C shell 版本是 `tcsh` shell。本章将讨论 `tcsh` shell，描述如何为它编写 shell 脚本。

- 本章内容
- `tcsh` shell 的历史
- `tcsh` 的组成
- 使用 `tcsh` shell

## 什么是 tcsh shell？

C shell 是由 Bill Joy 在加州大学伯克利分校开发的，用于替代 AT&T 实验室创建的 Unix shell（Bourne shell 之前）。伯克利的开发人员当时拥有并构建了一个 Unix 系统来与 AT&T Unix 竞争，而 C shell 是他们的默认选择。20 世纪 70 年代后期，Ken Greer 创建了 C shell 的扩展，添加了 TENEX 操作系统中包含编辑功能。这就是 `tcsh` 名字的由来。`tcsh` shell 已经成为许多 Unix 系统的流行 shell（包括早期的 macOS）。

虽然 `bash` shell 已成为大多数 Linux 发行版的默认 shell，但 `tcsh` shell 是可选的，并且可以根据需要直接从源代码安装。如果你将 shell 脚本从 BSD 环境迁移到 Linux 环境，使用 `tcsh` shell 会非常有帮助。

由于 C shell 创建于 Bourne shell 之前，两者之间存在显著差异。由于 `bash` 基于 Bourne shell，`tcsh` 和 `bash` shell 之间也存在显著差异。对于所有非简单的应用程序，编写可以在两个环境中运行的脚本几乎是不可能的。

第四部分 替代性 Linux Shell

## tcsh Shell 组件

与 `bash` shell 一样，`tcsh` shell 使用命令行参数、默认文件、环境变量和内置命令来定义 shell 运行环境。本节将描述 `tcsh` shell 的这些特性。

### tcsh 命令行参数

`tcsh` shell 提供了若干命令行参数，允许你自定义 shell 的运行方式。这些命令行参数定义了哪些 shell 功能以及 shell 在交互环境中的行为。表 21-1 列出了 `tcsh` shell 可用的命令行参数。

`tcsh` shell 使用了一些与 `bash` 相同的命令行参数，但也有一些自己的。

`-v` 和 `-V` 参数在 `tcsh` shell 中进行故障排除时非常有用。它们会在 shell 执行命令时显示命令。

`-V` 参数从 shell 启动就开始显示命令，包括登录和启动 shell 文件（见“`tcsh` 文件”章节）。`-v` 参数在启动和登录完成后才开始显示命令。

这对于命令行没有用，但在处理 shell 脚本时非常酷：

```
$ cat test1
#!/bin/tcsh -v
# run a script
set testing=10
echo "This is a test"
echo "The value of testing is $testing"
./test1
```

```
set testing=10
echo "This is a test"
This is a test
echo "The value of testing is $testing"
The value of testing is 10
$
```

#### tcsh Shell 命令行参数

| 参数 | 说明 |
| :--- | :--- |
| `-b` | 退出选项参数，强制将所有剩余参数被视为非选项参数。 |
| `-c` | 命令从指定的参数读取。 |
| `-d` | shell 从 `$HOME/.cshdirs` 文件加载目录栈。 |
| `-e` | 如果命令非正常终止或以非零退出状态退出，shell 将退出。 |
| `-f` | shell 不处理 `$HOME/.tcshrc` 文件。 |
| `-i` | 强制开启交互式 shell 会话。 |
| `-l` | 指定将 shell 作为登录 shell 使用。 |
| `-m` | 强制 shell 执行 `$HOME/.tcshrc` 文件，即使它不属于有效用户。 |
| `-n` | shell 解析命令但不执行它们。 |
| `-q` | shell 接受 SIGOUT 信号，并禁用作业控制。 |
| `-s` | Shell 命令从 STDIN 获取。 |
| `-t` | shell 读取并执行单行输入。 |
| `-v` | 设置 verbose shell 变量，使得在使用历史记录替换时命令会进行回显。 |
| `-V` | 在执行 `$HOME/.tcshrc` 文件之前设置 verbose shell 变量。 |
| `-x` | 设置 echo shell 变量，使得命令在执行前会立即进行回显。 |
| `-X` | 在执行 `$HOME/.tcshrc` 文件之前设置 echo shell 变量。 |
| `--help` | 在 STDOUT 上显示帮助信息并退出。 |
| `--version` | 显示 `tcsh` shell 的版本信息。 |

在脚本中定义 `tcsh` shell 时使用 `-v` 参数，会导致 shell 在执行每条语句之前显示该语句。

## tcsh 文件

`tcsh` shell 会自动查找几个默认文件，用于设置环境变量和执行命令。如果存在任何默认文件，`tcsh` shell 就会会在特定实例执行它们。`tcsh` shell 可以处理三种不同类型的默认文件：

- 登录文件 `Login files`
- Shell 启动文件 `Shell startup files`
- 退出文件 `Logout files`

本节将检查你可以用于 `tcsh` shell 的众多文件。

### tcsh 登录文件

如果你将 `tcsh` 作为登录 shell 使用，它首先查找并执行以下文件：

- `/etc/csh.login`
- `/etc/csh/login`

你会注意到所有这些文件的文件名中都包含 `csh`。由于 `tcsh` shell 被设计为原始 C shell 的替代品，它被设计为可以处理 C shell 能处理的任何默认文件。这使得从 C shell 环境迁移到 `tcsh` shell 环境变得轻而易举。

这些文件适用于所有使用 `tcsh` 作为登录 shell 的用户。这些文件应该包含为所有用户设置的系统级环境变量，以及所有用户都应该使用的可执行程序（例如设置默认文件和目录权限的 `umask` 命令）。如果你正在使用支持 `tcsh` shell 的 Linux 发行版，很可能这些文件中的某一个已经存在并用于在登录时设置系统环境变量了。

在执行完这两个文件中的任意一个后，`tcsh` shell 会在每个用户的 `$HOME` 目录下查找一个文件：

```
$HOME/.login
```

该文件可以包含用户特定的环境变量设置，以及单个用户在登录系统时、命令行界面提示符出现之前想要运行的可执行命令。

你在 `$HOME/.login` shell 中做的任何环境变量设置将覆盖 `/etc/csh.login` 文件中设置的系统级设置。你可以通过在每个文件中添加一个简单的 `echo` 语句并登录，来测试 `tcsh` shell 执行这些文件的顺序：

```
$ telnet localhost
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^'\nWelcome to testbox
login: test
Password:
Last login: Fri Jan 11 18:54:41 from localhost.localdomain
This is the /etc/csh.login file
This is the .login file
$
```

如示例所示，`tcsh` shell 首先执行了 `/etc/csh.login` 文件。

### Shell 启动文件

如果你不将 `tcsh` shell 作为登录 shell 使用，而仅作为交互式 shell 使用，那么在 shell 启动时必须处理一组不同的文件。

默认的系统级启动文件是：

- `/etc/csh.csh`

在执行此文件（如果存在）后，`tcsh` shell 会进入用户的 `$HOME` 目录，并查找以下文件之一：

- `$HOME/.cshrc`
- `$HOME/.tcshrc`

如果两个都存在，它将只会执行 `.tcshrc` 文件。你可以通过使用 `echo` 语句进行简单测试，来测试 `tcsh` shell 执行这些文件的顺序：

```
$ tcsh
This is the /etc/csh.tcshrc file
This is the /home/test/.tcshrc file
$
```

当启动一个新的 `tcsh` shell 时，它首先执行了 `/etc/csh.tcshrc` 文件，然后是 `$HOME` 目录下的 `.tcshrc` 文件。

当你使用 `tcsh` shell 运行脚本时，也会执行 shell 启动文件：
