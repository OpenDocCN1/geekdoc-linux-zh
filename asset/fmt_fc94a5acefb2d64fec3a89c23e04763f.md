
此命令列出 `/etc/password` 文件的内容，并将输出管道传给 `sort` 命令。`sort` 命令获取 `/etc/password` 文件每行开头的用户名，按字母顺序排序，并将输出传给 `cut`。`cut` 命令提取第 1 和第 5 个字段（以冒号 `:` 为字段分隔符），然后将输出传给 `less`。

## 顺序命令

有时你想在单行上运行多个命令。你可以使用分号 (`;`) 实现这一点。当第二个命令依赖于第一个命令的输出时，这非常有用。示例：

```
$ date; ls
```

在此示例中，`date` 命令首先运行，然后运行 `ls` 命令。

## 后台命令

某些命令可以通过在命令末尾添加安符 (`&`) 在后台运行。这允许你在命令执行时继续使用 Shell。示例：

```
$ sleep 10 &
```

`sleep` 命令在后台运行 10 秒。

## 扩展命令

通过命令替换，你可以将一个命令的输出作为另一个命令的参数。通过这种方式，Shell 在执行命令之前会先解释该命令的输出。命令替换的两种形式是 `$(command)` 或 `` `command` ``。（第一种情况是首选方法。）

示例：

```bash
$ vi $(find /home -name xxyzy)
```

在此示例中，`find` 命令首先运行并查找 `/home` 下所有名为 `xxyzy` 的文件。然后将其输出作为参数传递给 `vi` 命令。

## 扩展算术表达式

有时你想将算术结果传递给命令。你可以使用两种形式来扩展算术表达式并传递给 Shell：`$[expression]` 或 `$((expression))`。示例：

```
$ echo "I am $((2008 - 1957)) years old."
I am 51 years old.
```

在此示例中，Shell 先解释算术表达式（2008 - 1957），然后将信息传递给 `echo` 命令。

## 扩展变量

存储在 Shell 中的信息的环境变量可以使用美元符号 (`$`) 元字符进行扩展。当你在命令行上扩展环境变量时，打印的是变量的值而不是变量名本身，如下：

```
$ ls -1 $BASH
-rwxr-xr-x 2 root      625516 Dec 5 11:13 /bin/bash
```

将 `$BASH` 作为 `ls -1` 的参数会导致打印 bash 命令的详细列表。有关 Shell 环境变量的更多信息，请参阅下一节。

# 使用 shell 环境变量

每个活跃的 shell 都会存储它需要使用的信息，这些信息被称为环境变量。环境变量可以存储诸如配置文件的位置、邮箱和路径目录等信息。它还可以存储你的 shell 提示符值、历史列表的大小以及操作系统的类型。

要查看当前分配给你的 shell 的环境变量，请输入 `declare` 命令。（输出内容可能超过一个屏幕，请输入 `declare | more`）。你可以通过在任何这些变量前加上美元符号 (`$`) 并将其放置在命令行中来引用该变量的值。例如：

```bash
$ echo USER
chris
```

此命令打印 `USER` 变量的值，该变量保存了你的用户名 (`chris`)。将 `USER` 替换为任何其他变量名即可打印其值。

# 常见的 shell 环境变量

当你启动 shell（通过登录或打开终端窗口）时，很多环境变量已经准备就绪。以下是在使用 `bash` shell 时设置的或你可以通过不同功能设置的变量：

- `BASH` — `bash` 命令的完整路径。这通常是 `/bin/bash`。
- `BASH_VERSION` — `bash` 命令当前版本号。
- `UID` — 这是当前用户的有效用户 ID。它在 shell 启动时根据用户在 `/etc/passwd` 文件中的记录进行分配。
- `FCEDIT` — 如果设置了，此变量表示 `fc` 命令编辑历史命令时使用的编辑器。如果未设置此变量，则使用 `vi`。
- `HISTFILE` — 你的历史文件的位置。它通常位于 `$HOME/.bash_history`。
- `HISTSIZE` — 可以存储的历史条目数量。达到此数字后，旧的命令会被丢弃。默认值为 1000。
- `HISTCMD` — 返回当前命令在历史列表中的编号。
- `HOME` — 这是你的家目录。每次你登录或带选项输入 `cd` 命令时，它都是你的工作目录。
- `HOSTTYPE` — 描述运行 Linux 系统的计算机架构的值。对于兼容 Intel 的 PC，其值为 `i386`、`i486`、`i586`、`i686` 或类似 `i386-linux` 的值。对于 AMD 64 位和 Intel EM64T 机器，值为 `x86_64`。还有 `ppc` 和 `ppc64`，用于 32 位和 64 位的 Apple 电脑。

## 第一部分：在 Fedora RHEL 中入门

- `MAIL` — 你的邮箱文件的位置。该文件通常是 `/var/spool/mail` 目录下的你的用户名。
- `OLDPWD` — 在你切换到当前工作目录之前的工作目录。
- `OSTYPE` — 标识操作系统的名称。对于 Fedora 和 RHEL，`OSTYPE` 的值为 `linux-` 或 `linux-gnu`，取决于你正在使用的 shell 类型。（Bash 也可以运行在其他操作系统上。）
- `PATH` — 用于查找你输入的命令的目录列表，用冒号分隔。普通用户的默认值：`/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/home/chris/bin`

对于 root 用户，该值还包括 `/sbin`、`/usr/sbin` 和 `/usr/local/sbin`。
- `PPID` — 启动当前 shell 的命令的进程 ID（例如它的父进程）。
- `PROMPT_COMMAND` — 可以设置一个在 shell 显示之前运行的命令。设置 `PROMPT_COMMAND=date` 会提示符出现之前列出当前日期和时间。
- `PS1` — 你的 shell 提示符的值。你可以将许多项目读入提示符中（日期、用户、名称等）。有时命令需要额外的提示符，你可以通过变量 `PS2`、`PS3` 等进行设置。（设置提示符将在在本章稍后的部分描述。）
- `PWD` — 被分配为当前目录的目录。每当你通过 `cd` 命令更改目录时，此值就会更改。
- `RANDOM` — 访问此变量会生成一个随机数。数字在 0 到 32767 之间。
- `SECONDS` — 自 shell 启动以来的秒数。
- `SHLVL` — 与当前 shell 会话相关的 shell 数量。当你登录 shell 时，`SHLVL` 为 1。每当你启动一个新的 `bash` 命令（例如使用 `su` 变成新用户，或简单地输入 `bash`），该数字就会递增。
- `TEOUT` — 可以设置一个数字，代表 shell 在未接收输入的情况下可以空闲秒数。达到该秒数后，shell 将退出。这是一个安全特性，降低了无人值守的 shell 被未经授权的人访问的概率。（这必须在登录 shell 中设置才能实际导致 shell 登销用户。你可以在任何终端会话中使用它，以便在几秒钟后关闭当前 shell，例如 `TETOUT=30`）
- `UID` — 分配给你的用户名的用户 ID。用户 ID 数字存储在 `/etc/password` 文件中。

# 第4章：使用 Linux 命令 165

# 设置你自己的环境变量

环境变量可以提供一种方便的方法，用于存储你在 shell 中频繁使用的部分信息。你可以创建任何需要的变量（避免使用那些已使用的变量），以便你可以读取这些值。

要设置环境变量，请使用赋值运算符。例如：

```bash
$ MYVAR="hello world"
```

要让变量对子进程可用，请使用 `export` 命令：

```bash
$ export MYVAR
```

要移除变量，请使用 `unset` 命令：

```bash
$ unset MYVAR
```

你还可以通过将它们添加到 shell 配置文件（如 `.bashrc`）来设置环境变量。这确保了每次你启动新 shell 时变量都会被设置。

# 第 4 章：使用 Linux 命令 167

```
$ jobs
[1] Stopped (tty output) vi /tmp/myfile
[2] Running find /usr/-print > /tmp/allusrflies & 
[3] Running nroff -man /usr/man2/* */tmp/man2 & 
[4] Running nroff -man /usr/man3/* */tmp/man3 & 
[5]+ Stopped nroff -man /usr/man4/* */tmp/man4
```
