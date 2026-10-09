
# ssh

`ssh [option] |user@host [command-line]`

`ssh` 工具通过在远程系统上启动 shell 或在主机上登录你来运行命令行。`ssh` 工具可以替代 `rsh` 和 `login`，在不安全网络上的两个系统之间提供安全的加密通信。

## Arguments

`host` 是你想要登录或在其上面运行命令的系统。除非你建立了几种类型的身份验证，否则 `ssh` 会提示你输入远程系统的用户名和密码。当 `ssh` 能够自动登录时，它将以运行 `ssh` 命令的用户身份登录，或者像命令行上出现的 `user@` 一样登录。

命令行在远程系统上运行。如果没有命令行，`ssh` 将登录到远程系统。如果你没有通过本地 shell 扩展它们，则必须对命令行中的特殊字符加引号。

## Options

*   `-f (not foreground)` 在执行命令行之前询问密码后将 `ssh` 发到后台。此选项当你想在后台运行命令行但必须提供密码时有用。它的使用隐含 `-n`。
*   `-l user (login)` 尝试以 `user` 登录。此选项等同于在命令行上使用 `user@`。
*   `-n (null)` 将 `ssh` 的标准输入重定向自 `/dev/null`。
*   `-p port` 连接到远程主机上的端口 `port`。
*   `-q (quiet)` 抑制警告和诊断消息。
*   `-t (tty)` 为远程系统上的 `ssh` 进程分配一个伪终端。如果没有此选项，当你在后台运行命令行但必须提供密码时（无效）。它的使用隐含 `-n`。
*   `-v (verbose)` 显示调试消息。此选项当你想在后台运行命令行但必须提供密码时有用。它的使用隐含 `-n`。
*   `-x (off)` 关闭转发。

## Discussion

默认情况下，`split` 将文件分成每部分 1000 行的部分，命名为 `xaa`、`xab`、`xac` 等。带有 `-l` 选项的 `wc` 工具显示每个文件的行数。最后一个文件 `xar` 比其他文件都小。

## Examples

```bash
$ split /etc/termcap
$ wc -l *
 1000 xaa
1000 xab
1000 xac
...
1000 xap
1000 xaq
 103 xar
17103 total
```

下一个示例使用前缀参数指定文件名名前缀为 `SEC`，使用 `--suffix-length` 将文件名后缀的字母数量改为 3：

```bash
$ split --suffix-length=3 /etc/termcap SEC
$ ls
SEcaa SEcaac SEcaae SEcaag SEcaai SEcaak SEcaam SEcaao SEcaaq
SEabaab SEcaad SEcaaf SEcaah SEcaaj SEcaal SEcaan SEcaap SEcaar
```

## Notes

The ssh utility

`ssh` 工具通过在远程系统上启动 shell 或在主机上登录你来运行命令行。`ssh` 工具可以替代 `rsh` 和 `login`，在不安全网络上的两个系统之间提供安全的加密通信。

# 776 ssh

```bash
$ ssh watson@kudos
watson@kudos's password:
Last login: Sat Sep 17 06:51:59 from bravo
$ hostname
kudos
$ exit
```

Alex 现在决定更改他在 `kudos` 上 `watson` 登录的密码。

```bash
$ ssh watson@kudos dewd passwd
watson@kudos's password:
(current) UNIX password: por
```

当 Alex 看到 `passwd`（在 `kudos` 上运行）显示了他的密码时他停了下来：他知道有些不对劲。为了让 `passwd` 工作，它必须在 `tty`（终端）上运行，这样它可以关闭字符回显（`tty -echo`），从而在用户输入时不显示密码。`-t` 选项通过将伪终端与在远程系统上运行的 `passwd` 进程关联来解决这个问题：

```bash
$ ssh -t watson@kudos passwd
watson@kudos's password:
Changing password for watson
(current) UNIX password:
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully
Connection to kudos closed.
$
```

当你运行一个使用字符/伪图形界面的程序时，`-t` 选项同样有用。

以下示例使用 `tar`（第 786 页）创建工作目录层次内容的归档文件。`-f` 选项导致 `tar` 将其输出发送到标准输出。管道将在本地系统上运行的 `tar` 输出通过 `ssh` 发送给远程系统上运行的 `dd`（第 633 页）：

```bash
$ cat buwd
# /bin/bash
# back up the working directory to the user's
# home directory on the remote system specified
# by $machine
```

```bash
# remote system:
machine=speedy
```

```bash
dir=$(basename $(pwd))
filename=$dir.tar
```

```bash
echo Backing up $(pwd) to your home directory on $machine
tar -cf - | ssh $machine "dd obs=256k of=$filename"
echo done. Name of file on $machine is $filename
```

# strings

显示可打印字符字符串

`strings [options] file-list`

`strings` 工具从对象和其他非文本文件中显示可打印字符的字符串。

### 参数

`file-list` 是 `strings` 处理的文件列表。

### 选项

*   `-all -a` 处理整个文件。如果不使用此选项，`strings` 只处理对象文件中已初始化和加载的部分。
*   `-bytes=min -min` 显示长度至少为 `min` 个字符的字符字符串（默认值为 4）。
*   `-print-file-name -f` 在每个字符串前显示该字符串来源文件名。

### 讨论

`strings` 工具可以帮助你确定非文本文件的内容。`strings` 的一个应用是确定 `lost+found` 目录中文件的所有者。

### 示例

以下示例显示了 `man` 工具可执行文件中四个或更多可打印字符的字符串。如果你不知道这个文件是什么，这些字符串可以帮助你判断它是 `man` 可执行文件。

```bash
$ strings /usr/bin/man
man: internal error - cannot find message %d
/unsafe/
my_xprintf called with %s
Error parsing config file
No manual entry for %s
using %s as pager
%, version %s
found man directory %s
found manpath map %s --> %s
corresponding catdir is %s
Line too long in config file
section: %s
......
```

# stty

显示或设置终端参数

`stty [options] [[arguments]]`

在没有任何任何参数的情况下，`stty` 显示影响终端/终端模拟器操作的某些参数。有关这些某些参数的列表以及每个参数的解释，请参见“参数”。

参数用于建立或更改设置。

### 选项

*   `--all -a` 接受第 587 页描述的常用选项。
*   `--file=/dev/device -F` 报告所有参数。此选项不接受参数。
*   `-affects device`。如果不使用此选项，`stty` 将影响连接到标准输入的设备。只有在你拥有该设备或你是超级用户（Superuser）时，你才能更改设备的特性。
*   `--save -g` 生成当前设置的报告，该格式可以作为另一个 `stty` 命令的参数。此选项不接受参数。

### 参数

指定 `stty` 作用哪些终端参数。通过指定不带可选连字符（在下列表中指示为 `[-]`）的参数来开启每个参数。使用连字符将其关闭。除非另有说明，否则本节描述的是参数的默认状态。

### 特殊按键和特性

*   `columns n` 设置行宽为 `n` 列。
*   `ek (erase)` 将删除键和行删除键设为默认值。许多系统使用 `DELETE` 和 `CONTROL-U` 作为默认值。
*   `erase x` 将删除键设置为 `x`。要指定控制字符，请在 `x` 之前加上 `CONTROL-V`（例如，使用 `CONTROL-V CONTROL-H` 来表示 `CONTROL-H`）或使用符号 `^h`，其中 `^` 是脱字符符号（在大多数键盘上是 `SHIFT 6`）。
*   `intr x` 将中断键设置为 `x`。参见 `erase x` 的惯例。
*   `kill x` 将行删除键设置为 `x`。参见 `erase x` 的惯例。
*   `rows n` 将屏幕行数设置为 `n`。
*   `sane` 将终端参数设置为通常可以接受的值。当多个 `stty` 参数发生变化，导致终端难以运行 `stty` 来纠正设置时，`sane` 参数非常有用。如果 `sane` 不起作用，则输入该命令。

# 示例

第一个示例显示了不带任何参数的 `stty` 命令列出的几个终端操作参数。（您的系统可能会显示更多或不同的参数。）`erase =` 之后的字符是 `erase` 键。字符前的 `^` 表示一个 CONTROL KEY（控制键）。在示例中，`erase` 键被设置为 `CONTROL-H`。如果 `stty` 没有显示 `erase` 字符，它被设置为默认值 `DELETE`。如果你没有看到 `kill` 字符，它被设置为默认的 `^`。

```bash
$ stty
speed 38400 baud; line = 0;
erase = ^H;
```

接下来，使用 `-ek` 参数将 `erase` 和 line kill 键恢复为默认值：

```bash
$ stty --ek
speed 38400 baud; line = 0;
```

接下来的显示验证了更改。`stty` 工具既没有显示 `erase` 字符也没有显示 line kill 字符，这表明它们都设置为了默认值：

```bash
$ stty erase CONTROL-V CONTROL-H
$ stty
speed 38400 baud; line = 0;
erase = ^H;
```

接下来，`stty` 将 line kill 键设置为 `CONTROL-X`。这次用户输入了一个脱字符（`^`）后跟一个 `x` 来表示 `CONTROL-X`。你可以使用小写或大写字母。

```bash
$ stty kill ^X
$ stty
speed 38400 baud; line = 0;
erase = ^H;
```

现在 `stty` 将 interrupt（中断）键设置为 `CONTROL-C`：

```bash
$ stty intr CONTROL-V CONTROL-C
```

在下面的示例中，`stty` 关闭了 `Tabs` 功能，以便向终端发送相应数量的 `SPACES`（空格）而不是 `TAB`。如果终端没有自动扩展 `Tabs`，请使用此命令。

```bash
$ stty -tabs
```

如果你登录后发现终端上所有内容都是大写字母，请执行以下命令并检查 `CAPS LOCK` 键。如果已开启，请将其关闭：

```bash
$ stty -lcase
```

如果你使用的是无法显示小写字母的旧终端，请开启 `lcase`。

虽然通常没有人更改 suspend（挂起）键的默认值 `CONTROL-Z`，但你可以这样做。执行以下命令将 suspend 键更改为 `CONTROL-T`：

```bash
$ stty susp ^T
```

# tail

显示文件的最后部分（尾）

`tail [options] [file-list]`

`tail` 工具显示文件的最后部分或末尾。

参数：`file-list` 是 `tail` 要显示的文件路径列表。当你指定多个文件时，`tail` 在显示文件的行内容之前会先显示每个文件的文件名。如果你没有指定参数，或者用连字符（`-`）代替文件名，`tail` 将从标准输入读取。

# 选项

接受第 587 页中的常用选项。

*   `--bytes=[+][n/u] -c[+][n/u]`

    按字节（字符）而不是行进行计数。`n` 是一个指定字节数的整数。因此，命令 `tail -c 5` 显示文件的最后五个字节。`u` 是一个可选的计量单位，可以是 `b`（512 字节块）、`k`（千字节或 1,024 字节块）或 `m`（1,048,576 字节块）。如果你包含了计量单位，`tail` 将按该单位而不是字节计数。

    如果你在 `n` 前加加号（`+`），`tail` 将从文件开始计数而不是从末尾。`tail` 工具将显示到文件结束，尽管它是从开头开始计数的。因此 `tail -c+5` 会导致 `tail` 从第五行一直到文件结束。

*   `--follow -f`

    在复制文件的最后一行后，`tail` 会进入无限循环，如果文件增长，则等待并复制文件中额外的行。如果你在 `file-list` 中使用此选项指定多个文件，`tail` 每次显示不同文件的输出时都会包含一个新的页头，以便你知道正在添加哪个文件。此选项对于跟踪在后台运行并将输出发送到文件的进程有用。`tail` 工具将无限期等待，因此你必须使用中断键来终止。另见 `-s` 选项。

*   `--lines=[+][n/u] -n[+][n/u]`

    按行计数（默认值）。`n` 是一个指定行数的整数。`u` 是可选的计量单位；其用法请参见 `--bytes` 选项。虽然文档未说明，但你可以使用 `±` 在不使用此选项的情况下指定行数。

    如果你在 `n` 前加加号（`+`），`tail` 将从文件开始计数而不是从末尾。`tail` 工具将显示到文件结束，尽管它是从开头开始计数的。因此 `tail -n +5` 会导致 `tail` 从第五行显示到文件的最后一行。

*   `--quiet -q`

    当在 `file-list` 中指定多个文件时抑制页头信息。

*   `--sleep-interval=n -s n`

    配合 `-f` 使用，导致 `tail` 在检查额外输出之间睡眠 `n` 秒。

# 注意

`tail` 工具默认显示输入的最后十行。

# 示例
