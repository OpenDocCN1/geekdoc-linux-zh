
```
$ ls -l myenv
-rwxrwxr-x 1 winky winky 11 Aug 26 17:38 myenv
```

### 运行新的 Shell 程序

你可以通过多种方式运行新的 shell 程序。每种方法都会产生相同的结果，这证明了在 Linux 中使用 shell 的灵活性。运行 shell 程序的一种方法是像执行 Linux 命令一样从命令行运行文件 `myenv`：

```
$ ./myenv
```

在特定 shell（例如 `pdksh`）下执行 `myenv` 的第二种方法如下：

```
$ pdksh myenv
```

这会启动一个新的 `pdksh` shell，并将文件名 `myenv` 作为参数传递以执行该文件。第三种方法需要你在主目录中创建一个名为 `bin` 的目录，然后将新的 shell 程序复制到该目录中。然后你就可以在无需指定特定位置或使用 shell 的情况下运行该程序。你可以这样做：

```
$ mkdir bin
$ mv myenv bin
$ myenv
```

之所以可行，是因为 Ubuntu 默认设置会在你的 shell 环境中包含可执行路径 `$HOME/bin`。你可以通过将 `env` 命令的输出通过管道传递给 `grep` 来查看此环境变量 `PATH`，如下所示：

```
$ env | grep PATH
/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin: \
/usr/X11R6/bin:/sbin:/home/paul/bin
```

正如你所见，用户（本例中为 `paul`）可以使用新的 `bin` 目录来存放可执行文件。另一种查看环境变量的方法是使用 `echo` 命令并加上变量名（本例中为 `$PATH`）：

```
$ echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/bball/bin
```

#### CAUTION

切勿将 `.` 放入你的 `$PATH` 中以执行文件或当前目录中的命令——这会带来严重的安全风险，尤其是对于 `root` 操作员而言，如果 `.` 在你的 `$PATH` 搜索顺序中排在首位则风险更大。黑客放置在 `/tmp` 等目录中的特洛伊脚本可被用于恶意目的，如果当前工作目录是你的 `$PATH` 的一部分，则会立即被执行。

#### Storing Shell Scripts for Systemwide Access

执行命令 `myenv` 后，你应该能够从命令行使用 `ldir` 列出当前目录下的文件列表，并使用 `ll` 列出显示属性的文件列表。然而，将 `myenv` 中的新命令放入你的 shell 登录或配置文件中是使用这些新命令的最佳方式。对于 Ubuntu 以及几乎所有 Linux 用户，默认 shell 是 `bash`，因此你可以通过将它们放入 `/etc/bashrc` 文件中，使这些命令对系统上的每个人都可用。`tcsh` 的系统范围别名包含在 `/etc/profile.d` 目录下扩展名为 `.csh` 的文件中。`pdksh` shell 也可使用这些命令别名。

#### NOTE

要在登录后使用 `bash` 以外的 shell，请从命令行使用 `chsh` 命令或在 X 会话期间使用 `system-config-users` 客户端。你将被要求输入密码（如果使用 `system-config-users`，则为 `root` 密码），以及新 shell 的位置和名称（请参阅表 11.1）。新 shell 将成为你的默认 shell，但前提是其名称在 `/etc/shells` 中可接受的系统 shell 列表中。

#### Interpreting Shell Scripts Through Specific Shells

大多数 shell 脚本在开头使用 shebang 行（`#!`）来控制用于运行脚本的 shell 类型；此 bang 行调用的是 `bash` 的 `sh` 咒语：

```
#!/bin/sh
```

shebang 行（是 “sharp” 和 “bang” 的缩写，`#` 和 `!` 的两个名称）告诉 Linux 内核应使用特定命令（shell，或在其他脚本的情况下，可能是 `awk` 或 `Perl`）来解释文件的内容。使用 shebang 行是所有 shell 脚本编写的常见做法。例如，如果你使用 `bash` 编写 shell 脚本，但希望脚本像由 Bourne shell `sh` 运行一样执行，则脚本的第一行将包含 `#!/bin/sh`，它是 `bash` shell 的链接。以 `sh` 运行 `bash` 会使 `bash` 表现得像 Bourne shell。这就是符号链接 `sh` 指向 `bash` 的原因。

#### The Shebang Line

shebang 行是一种魔数，如 `/usr/share/magic` 中所定义——Linux `file` 命令的魔数文本数据库。魔数被许多不同的 Linux 命令用于快速识别文件类型，其数据库格式在名为 `magic` 的第五节手册页中有文档记录（使用 `man 5 magic` 阅读）。例如，魔数可被 Linux `file` 命令用来显示脚本的身份（无论使用什么文件名）为使用特定 shell 或其他解释器（如 `awk` 或 `Perl`）的 shell 脚本。

你还可能通过使用不同的 shell 在脚本中发现不同的或新的环境变量。例如，如果你从 `bash` 命令行启动 `csh`，你会发现几个新的变量或定义略有不同的变量，例如

```
$ env
...
VENDOR=intel
MACHTYPE=i386
HOSTTYPE=i386-linux
HOST=thinkpad.home.org
```

另一方面，`bash` 可能提供这些变量或同名但定义略有不同的变量，例如

```
$ env
...
HOSTTYPE=i386
HOSTNAME=thinkpad.home.org
```

尽管 shebang 行的行为并未由 POSIX 定义，但其用法的变体在你编写 shell 脚本时可能很有帮助。例如，如 `wish` 手册页所述，你可以使用 shell 来帮助执行 shell 脚本中调用的程序，而无需硬编码程序的路径名。`wish` 命令是一个窗口化 Tool Control Language（`tcl`）解释器，可用于编写图形客户端。避免使用程序的具体路径名可提高 shell 脚本的可移植性，因为并非每个 Unix 或 Linux 系统都将程序放在相同的位置。

例如，如果你想使用 `wish` 命令，你的第一反应可能是写

```
#!/usr/local/bin/wish
```

尽管这在许多其他操作系统上都能工作，但在 Linux 下脚本会失败，因为 `wish` 位于 `/usr/bin` 目录下。然而，如果你这样写命令行，

```sh
#!/bin/sh
exec wish "$@"
```

你可以使用 `wish` 命令（作为二进制文件或 shell 脚本本身）；你的第一反应可能是要在 Linux 中写 `wish`。

#### 在 Shell 脚本中使用变量

在为 Linux 编写 shell 脚本时，你会使用三种类型的变量：

- **环境变量**——属于系统环境，你可以在 shell 程序中使用它们。可以定义新变量，其中一些变量，如 `PATH`，也可在 shell 程序中进行修改。

- **内置变量**——这些是变量，例如在命令上使用的选项（由 shell 解析为 *位置参数*）由 Linux 提供。与环境变量不同，你无法修改它们。

- **用户变量**——由你在编写 shell 脚本时定义。你可以在 shell 程序中随意使用和修改它们。

shell 编程与其他编程语言的一个主要区别是，在 shell 编程中，变量不是 *类型化* 的——也就是说，你不必指定变量是数字还是字符串，等等。

#### 为变量赋值

假设你想使用一个名为 `lcount` 的变量来计算 shell 程序中循环的迭代次数。你可以按如下方式声明并初始化此变量：

| Command | Environment |
|---|---|
| `lcount=0` | `pdksh` and `bash` |
| `set lcount=0` | `tcsh` |

> **NOTE**
>
> 在 `pdksh` 和 `bash` 下，你必须确保等号 (`=`) 前后没有空格。

要将字符串存储在变量中，你可以使用以下方法：

| Command | Environment |
|---|---|
| `myname=Sanjiv` | `pdksh` and `bash` |
| `set myname=Sanjiv` | `tcsh` |

如果字符串中没有嵌入空格，请使用前面的变量形式。如果字符串包含嵌入空格，你可以按如下方式进行赋值：

| Command | Environment |
|---|---|
| `myname="Sanjiv Guha"` | `pdksh` and `bash` |
| `set myname="Sanjiv Guha"` | `tcsh` |

#### 访问变量值

你可以通过在变量名前加上 `$`（美元符号）来访问变量的值。也就是说，如果变量名为 `var`，你可以通过使用 `$var` 来访问其值。
