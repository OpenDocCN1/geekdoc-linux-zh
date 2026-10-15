
## 第 11 章 额外的命令行概念

环境变量是一个键值对。程序可以使用环境变量中的数据来决定在某些情况下的行为。例如，可以通过通过设置 `PAGER` 环境变量的值来更改用于显示帮助页（man pages）的默认命令。

环境变量是大小写敏感的；但按照惯例，它们使用大写字母。要查看已知环境变量的值，请运行 `echo $VAR_NAME` 或 `printenv VAR_NAME`。你可以不带参数地使用 `env` 或 `printenv` 命令来显示当前设置的所有环境变量。

```
$ echo $HOME

/home/jason

$ printenv HOME

/home/jason

$ printenv

SHELL=/bin/bash

TERM=xterm

USER=jason

MAIL=/var/mail/jason

PATH=/usr/local/bin:/usr/bin:/usr/local/games:/usr

PWD=/home/jason

LANG=en_US.UTF-8

PS1=$

SHLV=1

HOME=/home/jason

LOGNAME=jason

OLDPWD=/home/jason

$ env

SHELL=/bin/bash

TERM=xterm

USER=jason

MAIL=/var/mail/jason

PATH=/usr/local/bin:/usr/bin:/usr/local/games:/usr

PWD=/home/jason

LANG=en_US.UTF-8

PS1=$

SHLV=1

HOME=/home/jason

LOGNAME=jason

OLDPWD=/home/jason

$
```

当启动一个进程时，它会继承父进程导出的环境变量。仅设置的环境变量只会影响当前运行的进程，除非显式地导出（`export`）。在下面的示例中，`PAGER` 环境变量被设置为当前 shell 的 `less`。如果在没有导出该变量的情况下启动了子进程（例如另一个 Bash shell 实例），则该环境变量不会被继承。当导出了 `PAGER` 并启动新的 Bash shell 时，该变量对该进程可用。要删除一个环境变量，请使用 `unset` 命令。

```
$ echo $PAGER

$ PAGER=less

$ echo $PAGER

less

$ bash

$ echo $PAGER

$ exit

exit

$ export PAGER=less

$ bash

$ echo $PAGER

less

$ exit

exit

$ echo $PAGER

less

$ unset

$ echo $PAGER
```

| 变量 | 用途 |
| :--- | :--- |
| `EDITOR` | 用于编辑文件的程序。 |
| `HOME` | 用户的家目录。 |
| `LOGNAME` | 当前用户的 ID 或登录 ID。 |

表 36: 常用环境变量

| 变量 | 用途 |
| :--- | :--- |
| `MAIL` | 用户在本地系统上的邮箱位置。 |
| `OLDPWD` | 旧的或上一个工作目录。 |
| `PATH` | 命令的搜索路径。 |
| `PAGER` | 用于分页查看文件的程序。 |
| `PS1` | 主提示符字符串。 |
| `PWD` | 当前工作目录。 |
| `USER` | 当前用户的 ID 或登录 ID。 |

### 别名 (Aliases)

你可以在命令行中使用称为别名（aliases）的键盘快捷键。通过为经常重复使用、很长、难以输入或难以记忆的命令创建别名，你可以节省一些时间。你可以使用别名来修复常见的拼写错误。有些人使用别名让 Linux 的行为变得像他们熟悉的另一种操作系统一样。

`alias [alias_name=[value]]` 不带任何参数时，`alias` 命令会列出环境中的别名。因此使用 `alias alias_name=value` 来创建一个新的别名。

`unalias alias_name` 删除 `alias_name`。使用 `unalias -a` 删除所有别名。

```
$ alias ls='ls -l'

$ alias

alias ls='ls -l'

$ ls -l

total 32

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Desktop

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Documents

drwxr-xr-x 2 jason 4096 May 17 13:37 Downloads

-rw-rw-r-- 1 jason 274 Jun 28 14:52 goals.txt

drwxr-xr-x 3 jason 4096 Jun 21 22:05 Music

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Pictures

-rw-rw-r-- 1 jason 73 Jun 29 02:30 to-do.txt

$ ls -l

total 32

drwxr-xr-x 2 jason 4096 Jun 21 22:01 Desktop

drwx-xr-x 2 jason 4096 Jun 21 22:01 Documents

drwx-xr-x 2 jason 4096 May 17 13:37 Downloads

-rw-rw-r-- 1 jason 274 Jun 28 14:52 goals.txt

drwx-xr-x 3 jason 4096 Jun 21 22:05 Music

drwx-xr-x 2 jason 4096 Jun 21 22:01 Pictures

-rw-rw-r-- 1 jason 73 Jun 29 02:30 to-do.txt

$ alias=$usr/local/bin/backup-database.sh

$ $
```

开始数据库备份。
...
Database backup complete.

```
$ alias

alias bu=$usr/local/bin/backup-database.sh

alias ll='ls -l'
```

别名仅对你的当前会话有效。因此，如果你创建了一个别名、注销并重新登录，该别名将不可用。要让它们在会话之间持久化，需要将其放入初始化文件。

### 实例化文件 (Initialization Files)

为了在会话之间持久化别名，需要将它们保存在初始化文件中。要保存这些命令，需要将它们保存在 `.bashprofile`。通常 Bash 会使用 `source` 命令读取并执行文件 `.bashrc`。如果你想在执行之前检查它，可以使用 `if` 语句检查文件是否存在。

```
$ cat ~/.bashprofile

if -f ~/.bashrc ]; then

  source ~/.bashrc

fi

# source11 
```
```bash
$ echo "alias11='ls -l'" >> ~/.bashrc
# 以 # 号开头的行是注释。
# 将自定义内容放入文件。
```
```bash

$ cat ~/.bashrc

# 以 # 号开头的行是注释。

# 将自定义内容放入文件。

alias11='ls -l'

$ source11

$ alias11

ls -l

$
```

### Shell 历史 (Shell History)

你在命令行执行的命令保存在 shell 历史中。你的历史保留内存中，直到会话结束。此时，历史会被保存到 `.bash_history`。不同的 shell 使用不同的文件，但它们通常包含命令。你可以设置 `HISTSIZE` 环境变量来控制保存到历史中的命令数量。默认值为 500。当 `history` 命令不带参数执行时，它会显示历史命令列表。

`!N` 重复第 N 行命令。

`!!` 重复上一条命令。

`!pattern` 重复以 pattern 开头的最近一次命令。

```
$ history

1 ls

2 diff random-states random-states.bak

3 history

$ !

1 ls

2 diff random-states random-states.bak

$ echo $SHELL

/bin/bash

$ !!

echo $SHELL

/bin/bash

$ id

id=jason
```

你可以通过输入 Ctrl-r 来搜索 shell 历史。这会启动一个反向搜索，用 (reverse-i-search) ':' 表示，并允许你输入历史命令的一部分来检索。通过遍历历史中匹配搜索内容的其他命令，继续按 Ctrl-r。当你找到想要执行的命令时，按回车。如果你想在执行之前更改命令行，请按 Esc。要完全放弃反向搜索，输入 Ctrl-c。

```
$ diff random-states random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah

(reverse-i-search)'di': diff random-states random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah $
```

### Tab 补全 (Tab Completion)

要调用补全功能，只需输入命令并按 Tab 键。补全尝试完成部分输入的命令。如果有多种可能性，按两次 Tab 可以显示这些选项。你可以随时继续输入并按 Tab 。

除了补全命令外，你可以使用 Tab 补全来完成文件名和目录名。当文件或目录作为 `ls`, `cat`, `rm` 等命令的参数使用时，这非常有用。

```
### 输入 jo[Tab][Tab] 结果为：

$ jo

jobs join
```

```
[1]+ Running      ./db-backup.sh &
$ ls r*

random-states random-states.bak

### 输入 cat[Space][Tab][Enter] 导致：

$ cat random-states

Tennessee Nashville

Wyoming Cheyenne

Indiana Indianapolis

Indiana Indianapolis

Arizona Phoenix

Colorado Denver

Indiana Indianapolis

Georgia Atlanta

$
```

### 续行 (Line Continuation)

如果你想创建一个视觉上跨越多行但作为单个命令的命令行，请在每个需要延续的行末尾使用反斜杠 `\`。当反斜杠出现在命令行的末尾时，它充当续行符。如果你在命令提示符处使用它，延续的行将以大于符号 `>` 前缀。你在阅读文档或检查 shell 脚本时可能会遇到这种情况。

```
$ diff \\
> random-states \\
> random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah

$ diff random-states random-states.bak

3c3

< Georgia Atlanta

---

> Georgia Savannah

$ 
```

## 第 12 章 进程与作业 (Processes and Jobs)

`ps` 命令用于列出 Linux 系统上当前运行的进程。如果你在不带任何参数的情况下运行 `ps`，它将显示以你身份运行并与你的终端相关的进程。如果你两次连接到 Linux 服务器，你将看到 `ps` 命令的不同输出。对于第一个会话，可能会看到以下内容，它使用的是 `pts/0`（伪终端 0）。

```
$ ps

PID TTY         TIME CMD

1309 pts/0     00:00:00 bash

1635 pts/0     00:00:00 ps
```

以下是第二次连接时 `ps` 的输出，它使用的是 `pts/1`。

```
$ ps

PID TTY         TIME CMD

1721 pts/1     00:00:00 bash

1821 pts/1     00:00:00 ps
```

如果你想显示所有运行的进程，无论关联的终端或锁，请使用命令 `ps -u username`。

```
$ ps -u jason

PID TTY         TIME CMD

1308 ?           00:00:00 sshd

1309 pts/0     00:00:00 bash

1720 ?           00:00:00 sshd

1721 pts/1     00:00:00 bash
```

要查看系统上运行的每一个进程，使用命令 `ps -e`。

```
$ ps -e | head

PID TTY         TIME CMD

1 ?             00:00:00 init

2 ?             00:00:00 kthread

3 ?             00:00:00 ksoftirqd/0

6 ?             00:00:00 migration/0

7 00:00:00 watchdog/0

8 00:00:00 cuset

9 00:00:00 khelper

10 00:00:00 kdevmpfs

11 00:00:00 netns
```

默认情况下，`ps` 提供的信息相当稀疏。通常在在使用 `ps` 时，你会提供额外的参数来显示更详细的信息。以下是与 `ps` 配合使用的一些常用选项。

### 表 37：常用的 PS 选项

| 选项 | 说明 |
|---|---|
| `-e` | 显示所有进程。 |
| `-f` | 使用完整格式列表。 |
| `-u <username>` | 显示用户的进程。 |
| `-p <PID>` | 显示进程 ID (PID) 的进程信息。 |
| `-H` | 以层级结构（树形）显示进程。 |
| `--forest` | 使用 ASCII 艺术以层级结构显示进程。 |

下表说明了组合上述选项的一些实用方法。

### 表 38：常用的 PS 命令

| 命令 | 说明 |
|---|---|
| `ps -e` | 显示所有进程。 |
| `ps -ef` | 使用完整格式列表显示所有进程。 |
| `ps -EH` | 以树形格式显示所有进程。 |
| `ps -e -forest` | 使用 ASCII 艺术以树形格式显示进程。 |
| `ps -u <username>` | 显示用户运行的进程。 |
| `ps -fp <PID>` | 为进程 ID (PID) 显示完整格式列表。 |

以下演示了各种 `ps` 命令的输出。

```
$ ps

PID TTY TIME CMD

1309 pts/0 00:00:00 bash

2096 pts/0 00:00:00 ps

$ ps -f

UID PID PPID C TIME TTY TIME CMD

jason 1309 1308 0 15:15 pts/0 00:00:00 -bash

jason 2102 1309 0 15:45 pts/0 00:00:00 ps -f

$ ps -1309

PID TTY TIME CMD

1309 pts/0 00:00:00 bash

$ ps -fp 1309

UID PID PPID C TIME TTY TIME CMD

jason 1309 1308 0 15:15 pts/0 00:00:00 -bash

$ ps -e | head

PID TTY TIME CMD

1 ? 00:00:00 init

2 ? 00:00:00 kthread

3 ? 00:00:00 ksoftirqd/0

6 ? 00:00:00 migration/

7 ? 00:00:00 watchdog/0

8 ? 00:00:00 cuset

9 ? 00:00:00 khelper

10 ? 00:00:00 kdevmps

11 ? 00:00:00 netns

$ ps -11 | head

UID PID PPID C TIME TTY TIME CMD

root 1 0 0 15:14 ? 00:00:00 /sbin/init

root 2 0 0 15:14 ? 00:00:00 [kthread]

root 3 2 0 15:14 ? 00:00:00 [ksoftirqd/0]

root 6 2 0 15:14 ? 00:00:00 [migration/0]

root 7 2 0 15:14 ? 00:00:00 [watchdog/0]

root 8 2 0 15:14 ? 00:00:00 [cuset]

root 9 2 0 15:14 ? 00:00:00 [khelper]

root 10 2 0 15:14 ? 00:00:00 [kdevtmpfs]

root 11 2 0 15:14 ? 00:00:00 [netns]

$ ps -fu www-data

UID PID PPID C TIME TTY TIME CMD

www-data 1060 1057 0 15:15 ? 00:00:00 /usr/sbin/apache2 -k start

www-data 1061 1057 0 15:15 ? 00:00:00 
```

```bash

$ ps

PID TTY TIME CMD

1309 pts/0 00:00:00 bash

2096 pts/0 00:00:00 ps

$ ps -f

UID PID PPID C TIME TTY TIME CMD

jason 1309 1308 0 15:15 pts/0 00:00:00 -bash
```
