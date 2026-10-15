
`HOME` 变量被那些需要当前用户主目录路径名来存储或搜索文件的程序使用，因此不应更改它。如果 `root` 用户登录到系统，`HOME` 变量设置为 `/root`；或者，如果名为 `user1` 的用户登录到系统，`HOME` 变量设置为 `/home/user1`。请记住，波浪号 `~` 元字符表示当前用户的主目录；如下所示，此元字符是 `HOME` 变量的指针：

```
[root@server1 root]# echo $HOME
/root
[root@server1 root]# echo ~
/root
[root@server1 root]# HOME=/etc
[root@server1 root]# echo $HOME
/etc
[root@server1 root]# echo ~
/etc
[root@server1 root]# _
```

与 `HOME` 变量一样，`PWD`（打印工作目录）变量对用户环境至关重要，也不应更改。`PWD` 存储用户在目录树中的当前位置。它受 `cd` 命令的影响，并在需要识别当前目录时由 `pwd` 等其他命令使用。下面的输出演示了该变量如何工作：

```
[root@server1 root]# pwd
/root
[root@server1 root]# echo $PWD
/root
[root@server1 root]# cd /etc
[root@server1 etc]# pwd
/etc
[root@server1 root]# echo $PWD
/etc
[root@server1 root]#
```

`PATH` 变量是 `BASH` shell 中最重要的变量之一，因为它允许用户仅通过输入命令名称来执行命令。请记住，大多数命令由硬盘上可执行文件表示，这些文件通常组织在名为 `bin` 或 `sbin` 的目录中，遍布整个 Linux 目录树。要执行 `ls` 命令，您可以输入该文件的绝对或相对路径名（即 `/bin/ls` 或 `../bin/ls`），或者简单地输入字母 "ls"，让系统搜索 `PATH` 变量中列出的目录以查找名为 `ls` 的命令。`PATH` 变量的示例内容显示在下面的输出中：

```
[root@server1 root]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:
/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin:/root/bin
[root@server1 root]#
```

从上述输出中，如果用户仅在命令提示符处输入命令 `ls` 并按下 `Enter`，`shell` 会注意到路径名中没有 `/` 字符，并继续在 `/usr/kerberos/sbin` 目录中查找文件 `ls`，然后是 `/usr/kerberos/bin` 目录、`/usr/local/sbin` 目录、`/usr/local/bin` 目录、`/sbin` 目录，最后是 `/bin` 目录，以找到 `ls` 可执行文件。如果在 `PATH` 变量中的任何目录中都没有找到 `ls` 文件，`shell` 会返回一条错误消息，如下所示，其中使用了拼写错误的命令：

```
[root@server1 root]# lss
bash: lss: command not found
[root@server1 root]#
```

因此，如果某个命令位于 `PATH` 变量中列出的目录内，您可以简单地在命令行输入该命令的名称来执行它，因为 `shell` 将能够找到文件系统中相应的可执行文件。直到本节为止，本书中使用的所有命令都位于 `PATH` 变量中列出的目录中。然而，如果可执行文件不在 `PATH` 变量中列出的目录中，用户必须指定该可执行文件的绝对或相对路径名。下面使用 `/root` 目录（一个未列在 `PATH` 变量中的目录）中的 `myprogram` 文件对此进行了示例说明：

```
[root@server1 root]# pwd
/root
[root@server1 root]# ls -F
Desktop/ myprogram*
[root@server1 root]# myprogram
bash: myprogram: command not found
[root@server1 root]# /root/myprogram
This is a sample program.
[root@server1 root]# ./myprogram
This is a sample program.
[root@server1 root]# cp myprogram /bin
[root@server1 root]# myprogram
This is a sample program.
[root@server1 root]# _
```

在上面的输出中，当 `myprogram` 可执行文件被复制到 `/bin` 目录后，用户只需输入其名称即可执行它，因为 `/bin` 目录列在 `PATH` 变量中。

##### 表 8-3 常见的 BASH 环境变量

| 变量 | 描述 |
| :--- | :--- |
| `BASH` | `BASH` shell 的完整路径 |
| `BASH_VERSION` | 当前 `BASH` shell 的版本 |
| `DISPLAY` | 用于将 `X` `Windows` 输出重定向到另一台计算机或设备的变量 |
| `ENV` | `BASH` 运行时配置文件的位置（通常为 `~/.bashrc`） |
| `EUID` | 当前用户的有效 `UID`（用户 ID） |
| `HISTFILE` | 用于在 `BASH` shell 中存储之前输入命令的文件名（通常为 `~/.bash_history`） |
| `HISTFILESIZE` | 注销时可以在 `HISTFILE` 中存储并在下次登录时使用的之前输入命令的数量；通常是 1000 条命令 |

#### 环境变量

| 变量 | 描述 |
| --- | --- |
| `HISTSIZE` | 在当前登录会话期间将存储在内存中的先前输入命令的数量；通常为 1000 个命令 |
| `HOME` | 当前用户主目录的绝对路径名 |
| `HOSTNAME` | `Linux` 系统的主机名 |
| `LOGNAME` | 登录到 `shell` 时使用的当前用户名称 |
| `MAIL` | 邮箱文件的位置（电子邮件存储位置） |
| `OLDPWD` | 最近的先前工作目录 |
| `OSTYPE` | 当前操作系统 |
| `PATH` | 在不存在包含 `/` 字符的绝对路径或相对路径时，用于搜索可执行程序文件的目录 |
| `PS1` | 当前 `shell` 提示符 |
| `PWD` | 当前工作目录 |
| `RANDOM` | 访问时会生成随机数的变量 |
| `SHELL` | 当前 `shell` 的绝对路径名 |
| `TERM` | 用于确定终端设置的变量；在新版 `Linux` 系统中通常设置为“linux”或“xterm”，在旧版 `Linux` 系统中设置为“console” |
| `TERMCAP` | 用于确定使用 `TERMCAP` 数据库 (`//etc/termcap`) 的旧系统中终端设置的变量 |

#### 用户定义变量

你可以使用前面讨论过的更改现有环境变量内容的相同方法来自定义变量。为此，只需指定变量的名称（称为 `变量标识符`），紧随其后的是等号 (`=`) 和新的内容。在创建新变量时，注意变量标识符具有以下特性：

- 它们可以包含字母数字字符（0–9, A–Z, a–z）、破折号 (`-`) 或下划线 (`_`) 字符。

- 它们不能以数字开头。

- 它们通常大写以遵循惯例（例如，`HOME`, `PATH` 等）。

要创建一个名为 `MYVAR` 且内容为“This is a sample variable”的变量并显示其内容，可以使用以下命令：

```
[root@server1 root]# MYVAR="This is a sample variable"
[root@server1 root]# echo $MYVAR
This is a sample variable
[root@server1 root]# _
```

上述命令创建了一个在当前 `shell` 中可用的变量。由 `shell` 运行的大多数命令都在一个单独的 `子 shell` 中运行，该子 `shell` 由当前 `shell` 创建。在当前 `shell` 中创建的变量在这些子 `shell` 及其内部运行的命令中不可用。因此，如果用户创建了一个要在某个程序（如数据库编辑器）中使用的变量，应使用 `export` 命令将该变量导出到所有子 `shell`，以确保由当前 `shell` 启动的所有程序都能访问该变量。

回想一下前面提到的内容，可以使用 `set` 命令列出 `BASH` shell 中的所有环境变量；用户定义的变量也显示在此列表中。类似地，要查看 `shell` 中所有导出的环境变量和用户定义变量的列表，可以使用 `env` 命令。由于 `set` 和 `env` 的输出通常很大，通常会将这些命令的标准输出重定向到 `grep` 命令，以仅显示特定行。
