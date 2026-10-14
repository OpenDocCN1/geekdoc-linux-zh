
```bash
#!/bin/sh
alias 11='ls -L'
alias 1dir='ls -aF'
alias copy='cp'
```

这个简单的脚本为 `ls` 和 `cp` 命令创建了别名（aliases），即命令的方便快捷形式。`11` 别名提供长目录列表：`1dir` 别名是命令，但在列表中显示指示符（用于目录或可执行文件）。`copy` 别名与 `cp` 命令相同。你可以尝试并添加自己的选项，或者为你经常使用的选项的其他命令创建别名。

在 Linux 下，你可以通过多种方式执行 `myenv`。例如所示，你可以使用 `chmod` 命令让 `myenv` 可执行，并像执行任何其他 Linux 命令一样执行它：

```bash
matthew@semour:-$ chmod +x myenv
```

这实际上是 `myenv` 的权限，可以使用 `ls` 命令及其 `-l` 选项进行检查：

```bash
matthew@semour:-$ ls -l myenv
-rwxr-xr-x  1 matthew 2010-07-08 18:19 myenv
```

# 运行新的 Shell 程序

你可以通过几种方式运行你的 Shell 程序。每种方法产生相同的结果，这证明了在 Linux 中使用 Shell 的灵活性。运行 Shell 程序的一种方法是从命令行执行文件 `myenv`，就像执行一个 Linux 命令一样：

```bash
matthew@semour:-$ ./myenv
```

在特定 Shell（如 `pdksh`）下执行 `myenv` 的另一种方法如下：

```bash
matthew@semour:-$ pdksh myenv
```

第三种方法需要在家目录下创建一个名为 `bin` 的目录，然后将新的 Shell 程序复制到该目录中。你就可以在不需要指定位置或使用 Shell 的情况下运行该程序了。操作如下：

```bash
matthew@semour:-$ mkdir bin
matthew@semour:-$ mv myenv bin
matthew@semour:-$ myenv
```

这之所以有效，是因为 Ubuntu 默认将执行路径 `$HOME/bin` 包含在你的 Shell 环境中。你可以通过将 `env` 命令的输出通过给 `grep` 来定义名为 `PATH` 的环境变量：

```bash
matthew@semour:-$ env | grep PATH
/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin:/n/X11R6/bin:sbin:/home/matthew/bin
```

你可以看到，用户（在本例中）可以使用新的 bin 目录来存放可执行文件。另一种引入环境变量的方法是使用 `echo` 命令配合变量（在这种情况下为 `$PATH`）：

```bash
matthew@semour:-$ echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:/usr/X11R6:/home/bball
```

## 注意

在你的 `$PATH` 中放入某些内容会带来安全风险，特别是对于 root 操作员，如果它位于你 `$PATH` 搜索顺序的第一位，更是如此。放置在 `/tmp` 等目录中的木马脚本可能被恶意利用，如果当前工作目录是 `$PATH` 的一部分，它们将被立即执行。

# 系统级 Shell 脚本

创建命令 `myenv` 后，你应该能够从命令行使用 `ldir` 获取当前目录下的文件列表，并使用 `11` 获取 `myenv` 下的文件列表。使用 `myenv` 中新命令的最佳方法是将它们放入 Shell 的登录文件或配置文件中。对于 Ubuntu 以及几乎所有的 Linux 用户来说，Shell 是 `bash`，因此你可以通过将它们放入 `/etc/bashrc` 文件来让系统上的所有人使用这些命令。每个系统级别名包含在 `/etc/profile.d` 目录下扩展名为 `.csh` 的文件中。`pdksh` Shell 也可以使用这些别名。

## 注意

登录后要使用 bash 以外的 Shell，请从命令行使用 `chsh system-config users` 或使用 X 会话。系统会要求你输入密码（如果使用 system-config-users 则输入 root 密码）以及新 Shell 的位置和名称（见表 13.1）。新 Shell 将成为你的默认 Shell，但前提是它的名称在 `/etc/shells` 可接受的系统 Shell 列表中。

# 通过特定 Shell 解释 Shell 脚本

大多数 Shell 脚本在开头使用 `shebang` (`#!`) 来控制用于运行脚本的 Shell 类型；这一 行调用了 bash 的 sh 咒语：

```bash
#!/bin/sh
```

`shebang` 行（它是为了“sharp”和“bang”，即 `#` 和 `!` 的两个名称）告诉 Linux 内核，需要使用特定的命令（Shell，或者在其他脚本的情况下，为 `awk` 或 `Perl`）来解释文件的内容。使用 shebang 行是所有 Shell 脚本编写的常见做法。例如，如果你使用 bash 编写脚本，但希望脚本像由 Bourne shell 一样执行，那么你脚本的第一行将包含 `#!/bin/sh`。

# Shebang 行

大多数 Shell 脚本在开头使用 `shebang` (`#!`) 来控制用于运行脚本的 Shell 类型；这一 bang 行调用了 bash 的 sh 咒语：

```bash
#!/bin/sh
```

`shebang` 行（它是为了“sharp”和“bang”，即 `#` 和 `!` 的两个名称）告诉 Linux 内核，需要使用特定的命令（Shell，或者在其他脚本的情况下，为 `awk` 或 `Perl`）来解释文件的内容。使用 shebang 行是所有 Shell 脚本编写的常见做法。例如，如果你使用 bash 编写脚本，但希望脚本像由 Bourne shell 一样执行，那么你脚本的第一行将包含 `#!/bin/sh`。

`wish` 命令是一个窗口工具控制语言 (`tcl`) 解释器，用于编写图形客户端。避免使用特定路径可以增加脚本的可移植性，因为并不是每个 UNIX 或 Linux 系统都有相同位置程序。例如，如果你想使用 wish 命令，你的直觉可能是写：

```bash
!/usr/local/bin/wish
```

这在许多操作系统上可行，但在 Linux 下会失败，因为 wish 位于 `/bin` 目录。但如果你这样写命令行：

```bash
#!/bin/sh
exec wish "$@"
```

就可以使用 wish 命令（作为二进制文件或脚本本身）。

# 在 Shell 脚本中使用变量

在 Linux 中编写 Shell 脚本时，你会处理三种变量：

- **环境变量**——系统环境的一部分，可以定义新变量，某些变量（如 `PATH`）也可以在 Shell 程序内部修改。
- **内置变量**——由 Linux 提供的命令行选项（被 Shell 解释为位置参数）。与环境变量不同，你无法修改它们。
- **用户变量**——在编写 Shell 脚本时定义的变量。你可以在脚本内部使用并修改它们，但在外部不可用。

Shell 编程与其他编程语言的主要区别在于，在 Shell 编程中变量没有类型——即你不需要指定变量是数字还是字符串等。

# 为变量赋值

假设你想在 Shell 程序中中使用变量 `lcount` 来计算循环的次数。你可以如下方式声明并初始化该变量：

| 命令 | 环境 |
|---|---|
| `lcount=0` | `pdksh` 和 `bash` |
| `set lcount=0` | `tcsh` |

## 编写和执行 Shell脚本 247

> 注意

在 `pdksh` 和 `bash` 中，你必须确保等号 (`=`) 前后没有空格。

要将字符串存储在变量中，可以使用以下方法：

| 命令 | 环境 |
| --- | --- |
| `myname=Sedona` | `pdksh and bash` |
| `set myname=Sedona` | `tcsh` |

如果字符串不包含嵌入空格，可以使用上述的变量形式。如果字符串包含嵌入空格，可以按照以下方式进行赋值：

| 命令 | 环境 |
| --- | --- |
| `myname="Saralyn"` | `pdksh and bash` |
| `set myname="Saralyn"` | `tcsh` |

# 访问变量值

你可以通过在变量名前前加上美元符号 (`$`) 来访问变量的值。也就是说，如果变量名为 `var`，你可以使用 `$var` 来访问该变量。

如果你想将 `var` 的值赋值给变量 `count1`，可以如下操作：

| 命令 | 环境 |
| --- | --- |
| `count1=$var` | `pdksh and bash` |
| `set` | `tcsh` |
| `count1=$var` | |

# 位置参数
