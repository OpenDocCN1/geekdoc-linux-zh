
在上面的示例中，在 `Enter the value:` 提示符处输入的内容不会在输入时显示。然而，该值保留在变量中，并通过 `echo "You entered: $a"` 显示。

你可以更改特殊字符的值，例如 `kill` 和 `erase`。`stty` 实用影响连接到标准输入的终端。你可以通过将输入重定向到 `stty` 来查看或更改当前终端以外的终端特性。参考以下命令语法：

```bash
stty [arguments] < /dev/ttyxx
```

`tyxx` 是目标终端的文件名。只有当你拥有该设备文件或你是超级用户时，你才能更改终端的特性。

## 示例

第一个示例显示了不带任何参数的 `stty`，列出了几个终端操作参数。（你的系统可能会显示更多或不同的参数。）`erase =` 之后的字符是 `868` `stty` `erase` 键。字符前的 `^` 表示 `CONTROL` 键。该示例显示将 `erase` 键设置为 `CONTROL-H`。

如果 `stty` 不显示 `erase` 字符，则它被设置为默认值 `DELETE`。如果你看不到 `kill` 字符，它被设置为默认值 `^U`。

```bash
$ stty
speed 9600 baud; line = 0;
erase = ^H;
```

接下来，`ek` 参数将 `erase` 和 `line kill` 键恢复为默认值：

```bash
$ stty ek
```

下一个显示验证了更改。`stty` 实用不显示 `erase` 字符或 `line kill` 字符，表明它们都被设置为默认值。

```bash
$ stty
speed 9600 baud; line = 0;
```

下一个示例将 `erase` 键设置为 `CONTROL-H`：

```bash
$ stty erase CONTROL-V CONTROL-H
$ stty
speed 9600 baud; line = 0;
erase = ^H; kill = ^X;
```

下面，`stty` 将 `line kill` 键设置为 `CONTROL-X`。这次用户输入了一个脱字符 (`^`) 后跟一个 `x` 来表示 `CONTROL-X`。你可以使用小写或大写字母。

```bash
$ stty ^A
$ stty
speed 9600 baud; line = 0;
erase = ^H; kill = ^X;
```

下面，`stty` 转换 `TAB`，以便向终端发送相应数量的空格（`SPACE`）代替 `TAB`。如果终端不自动扩展 `TAB`，请使用此命令。

```bash
$ stty -tabs
```

如果你登录后终端上出现的所有内容都是大写字母，执行以下命令然后检查 `CAPS LOCK` 键。如果已设置，请将其关闭。

```bash
$ STTY -LCASE
```

如果你使用的终端无法显示小写字母，请开启 `ifcase`。

## tail 869

| 命令 | 描述 |
|---|---|
| tail | 显示文件的最后部分（尾） |

语法：`tail [options] [file-list]`

### 总结

`tail` 显示文件的最后部分或末尾。它从你在命令行上指定的一个或多个文件或从标准输入获取输入。

### 参数

`file-list` 包含 `tail` 显示的文件路径名。如果你指定了多个文件，`tail` 会在显示文件行之前先显示每个文件的文件名。如果你没有指定任何文件，`tail` 将从标准输入获取输入。

### 选项

- `--bytes=[+]n[u]]`: 按字节（字符）计数。`n` 是可选的非零整数。`u` 是可选的测量单位，可以是 `b`（512 字节块）、`k`（1024 字节或 1KB 块）或 `m`（1MB 块）。如果你包含了测量单位，`tail` 将按该单位的字节计数。你可以在 `n` 前加一个加号 (`+`) 让 `tail` 从文件开始计数而不是从末尾计数。`tail` 实用仍然计数到末尾，即使你从开始计数，因此 `+10` 会导致 `tail` 显示从第十行到文件的最后一行。
- `--follow`: 在复制文件的最后一行后，`tail` 进入无限循环。如果文件增大，它将等待并从文件中复制额外的行。这对于跟踪在后台运行并将输出到文件的进程进度有用。`tail` 将继续到末尾，即使你从开始计数，因此 `+10` 会导致 `tail` 显示从第十行到文件的最后一行。

## tar 872

| 命令 | 描述 |
|---|---|
| tar | 从存档中存储或检索文件 |

# 修饰符

你可以在选项后指定一个或多个修饰符。如果你使用修饰符的单字符形式，不需要前面的连字符。但是，除非你将修饰符与其他单字符修饰符结合，否则使用连字符是一个习惯。

如果修饰符带有参数，则该修饰符必须是组中的最后一个。例如，在 `tar` 命令中，参数的排列是合：

```bash
$ tar -cb 10 -f /dev/ftape
```

另一方面，以下命令 `-cbf` 会产生错误：

```bash
$ tar -cbf 10 /dev/ftape
Invalid value for blocksize
```

产生错误的原因是 `-b` 修饰符带有参数，但它不是组中的最后一个修饰符。这与用于许多 UNIX 系统的原始 `tar` 版本不同，后者允许这种构造：

- `--absolute-paths (-P)` `tar` 的默认行为是通过剥离开头的斜杠强制将所有路径变为相对路径。此选项将禁用此功能，因此任何绝对路径将保持为绝对路径。
- `--block-compress` 通常一次性压缩（`gzip`）或解压缩（`gunzip`）整个归档。这种技术对于磁带设备上的归档无效。此选项与压缩或解压缩选项之一配合使用时会导致 `tar` 按块压缩归档，这对于磁带归档非常有效。
- `--block-size [n] (-b)` 使用 `n` 作为创建归档的块因子。仅当 `tar` 直接向磁带创建归档时使用此选项。（当 `tar` 读取归档时，会自动确定块因子）。`n` 的值是作为单个块写入磁带的字节块数量。如果不指定 `n`，默认值为 `20`。
- `--checkpoint` 显示它从归档中提取的目录名称。
- `--compress` or `uncompress (-Z)` 在创建归档时使用 `compress`，从归档中提取文件时使用 `uncompress`。
- `--dereference (-h)` 跟随符号链接，并将链接到的文件像普通文件和目录一样包含进来。
- `--directory directory (-C)` 在处理之前将工作目录更改到目录。
- `--exclude filename` 不处理名为 `filename` 文件。如果 `filename` 是一个目录，则不处理该目录内的任何文件或目录。

# 874 tar

- `--exclude-from filename (-X)` 与 `--exclude` 选项类似，不同之处 `filename` 标识一个文件，该文件包含要从处理中排除的文件列表。`filename` 中列出的每个文件必须单独占一行。
- `--file filename (-f)` 使用 `filename` 作为存储归档的文件（设备）名称。如果没有此选项，`tar` 从磁带设备 `/dev/rmt` 读取/写入归档。`filename` 可以是普通文件的名称，可以是设备（如磁带驱动器），也可以网络上另一台计算机的设备。要给出另一台计算机的名称，请在设备前加上另一台计算机的域名和冒号（:）。如果你的用户名与当前使用的不同，可以在域名前之前加上远程机器上的用户名，后跟 `@`。以下由 `Alex` 在 `kudos` 上提供的命令，导致 `tar` 使用 `bravo` 上的磁带设备 `/dev/st0` 来存储归档，并使用 `Scott` 的账户访问磁带设备：

```bash
tar -cf scott@bravo:/dev/st0 /
```

### 注意事项

为了 `tar` 命令能够工作，`Alex`（在 `kudos` 上操作）必须有权限在 `bravo` 上通过 `Scott` 使用 `Scott` 的账户，`Scott` 必须能够执行 `rmt` 实用程序（远程机器上的 `rmt` 接受 `tar` 输出并将其写入磁带），并且 `Scott` 必须对 `bravo` 上的 `/dev/st0` 写入权限。

你可以使用连字符 (`-`) 代替文件名，在创建归档时引用标准输入，从归档中提取文件时引用标准输出。这两个命令是创建 `/dev/st0` 上 `/home` 目录下文件归档的等效方法：

```bash
tar -zcf /dev/st0 /home
tar -cf /home | gzip > /dev/st0
```

- `--gzip`
- `--ungzip (-z)` 使 `tar` 在创建归档时自动使用 `gzip` 压缩归档，并在从中提取文件时解压缩归档。从归档读取时，此选项还会导致 `tar` 检测归档是否是用 `compress` 实用程序压缩的。使用了 `compress`，`tar` 在提取文件时将使用 `uncompress` 而不是 `gunzip`。
- `--ignore-failed-read` 在创建归档时，如果文件列表中的任何文件不可读，`tar` 通常会以非零退出状态退出。此选项导致 `tar` 继续处理，跳过不可读的文件。

# tar 875

- `--interactive` or `(-w)` 在读取或写入每个文件之前请求确认。如果你想让 `tar` 执行操作，请响应 `y`。任何其他响应均让 `tar` 不执行操作。
- `--modification-time (-m)` 将修改时间设置为提取时的时间。如果没有此选项，`tar` 尝试保持原始文件的修改时间。
- `--one-file-system (-l)` 当在为归档读取文件时，如果文件列表中出现目录，`tar` 会递归处理该命名目录下方的文件和目录。使用此选项后，`tar` 将留在命名目录所在的文件系统中，而不会读取其他文件文件系统上的文件和目录。
- `--sparse (-S)` Linux 允许你在磁盘上拥有稀疏文件。这些是为空的大文件。空块不占用磁盘空间。此选项告诉 `tar` 如果输入是稀疏的，则在归档创建稀疏文件。
- `--length (-L)` 询问从每个文件中读取的字节数。
- `--verbose (-v)` 列出正在处理的文件名。这对于查看操作进度很有用。

### 注意

`tar` 命令是归档和压缩文件的强大工具。它在 Unix 类系统中被广泛用于软件的备份和分发。提供的许多可用选项允许对创建和提取归档的方式进行细粒度的控制。

## tee 将标准输入复制到标准输出和更多文件

语法：`tee [options] file-list`

### 摘要

`tee` 工具将标准输入复制到标准输出*并且*复制到你在命令行上指定的一个或多个文件中。

### 参数

`file-list` 包含接收 `tee` 输出的文件路径。

### 选项

在不使用任何选项的情况下，如果输出文件已存在，`tee` 将覆盖它们并响应中断信号。如果 `file-list` 中的文件不存在，`tee` 将创建它。

- `-a` 将输出追加到现有文件而不是覆盖它们。
- `--ignore-interrupts (-i)` 让 `tee` 不响应中断。

### 示例

在下面的示例中，管道将 `make` 的输出发送给 `tee`，`tee` 将其复制到标准输出和 `accounts.out` 文件。发送到标准输出的副本显示在屏幕上。`cat` 命令显示发送到文件的副本。

```bash
$ make accounts | tee accounts.out
cc -C trans.c
cc -C reports.c
```

```bash
$ cat accounts.out
cc -C trans.c
cc -C reports.c
```

请参考第 871 页查看使用 `tail -f` 而不是 `tee` 的类似示例。

## 878 telnet

## telnet 通过网络连接到远程计算机

语法：`telnet [options] [remote-computer]`

### 摘要

`telnet` 工具使用标准 `telnet` 协议通过网络连接到远程系统。`remote-computer` 是远程系统的名称或网络地址。`telnet` 工具通常用于在远程系统上建立登录会话，前提是你在该系统上有一个账户。

### 参数

如果你没有在命令行上指定 `remote-computer`，`telnet` 将尝试建立到该系统的连接。如果你没有指定远程计算机的名称，`telnet` 将以交互模式运行，提示你输入下面描述的命令之一。

### 选项

- `-` escape 将转义字符从 `CONTROL-]` 改为字符 `c`。
- `login-name` 尝试使用 `login-name` 自动登录到远程计算机。如果远程计算机理解如何通过 `telnet` 处理自动登录，系统会提示你输入该用户的密码。

### 讨论

连接到远程计算机后，你可以通过输入转义字符进入 `telnet` 的命令模式。在 Linux 系统上，转义字符通常是 `CONTROL-`。当你连接到远程系统时，它应该报告它所识别的转义字符。要退出命令模式，请单独行输入一个 `RETURN`。

在响应 `telnet>` 提示符时，可以使用以下命令：

- `help` 显示本地系统 `telnet` 工具识别的命令列表。
- `close` 关闭与远程系统的连接。如果你在启动 `telnet` 时在命令行上指定了系统名称，`close` 的效果与 `quit` 相同——`telnet` 程序退出并返回到 `shell`。如果你使用 `open` 命令而不是在命令行上指定远程系统，`close` 则将 `telnet` 返回到命令模式。
- `remote-computer` 如果你没有在命令行上指定远程系统，或者连接系统的尝试失败，你可以使用 `open` 命令交互式地指定远程系统的名称。

## telnet 879

## quit

退出 `telnet` 会话。

## z

如果你在启动 `telnet` 时使用的是支持作业控制的 `shell`，你可以使用 `z` 命令挂起与远程系统的会话。当你挂起会话时，你将返回本地系统上的登录 `shell`。要恢复与远程系统的 `telnet` 会话，请在 `shell` 提示符处输入 `fg`。

### 注意事项

许多计算机（包括非 Linux 系统）都支持 `telnet` 协议。`telnet` 命令是该协议在 Linux 系统上的实现，允许你连接到许多不同系统。虽然你通常使用 `telnet` 登录，但远程计算机可能通过 `telnet` 提供其他服务，例如访问特殊数据库。

### 示例

在下面的示例中，用户连接到名为 `bravo` 的远程系统。运行几个命令后，用户逃逸到命令模式并使用 `z` 命令挂起 `telnet` 会话，以便在本地系统上运行几个命令。用户使用 Z Shell 的 `fg` 命令恢复 `telnet`。最后，远程系统上的 Z Shell `logout` 结束了 `telnet` 会话。显示了本地系统的提示符。

```bash
kudos% telnet bravo
Trying 130.128.52.2 ...
Connected to bravo.
Escape character is '^]'.
```

```bash
Linux 2.0.18 (bravo.sro.com) (ttyp2)
bravo login: watson
Password:
Last login: Wed Jul 31 10:37:16 from kudos
Linux 2.0.18 (Posix).
```

```bash
bravo%
.
bravo%
telnet> z
zsh: suspended telnet bravo
kudos%
.
kudos% fg
[1] + continued telnet bravo
```

```bash
bravo$ logout
Connection closed by foreign host.
kudos%
```
