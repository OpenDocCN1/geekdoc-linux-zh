

```
tty      pts/0
uid      508
user     test
version tcsh 6.10.00 (Astron) 2000-11-19 (i386-intel-linux) options
nb,nl,dl,rh,color
$
```

注意，`tcsh set` 命令的输出与在 `bash` shell 中列出变量的输出有所不同。`tcsh` shell 版本将变量显示在左侧，将当前值显示在右侧。

你应该通过它们在 `bash` shell 中对应的项来识别许多 shell 变量。以下是你需要注意的几点区别：

- `tcsh` shell 使用 `prompt` 变量（以及 `prompt2` 和 `prompt3`），而不是 `PS1`、`PS2` 和 `PS3` 环境变量。
- `path` 变量包含一个目录索引列表，而不是一个由冒号分隔的单个字符串。

要显示或使用 变量的当前值，必须在它前面加上美元符号 `$`：

```
$ echo $path
/usr/local/bin /bin /usr/bin /usr/X1R6/bin
```

索引字符串使用数组格式来访问 shell 变量的各个值。你可以使用数组格式来访问单个元素：

```
$ echo $path[1]
/usr/local/bin
$ echo $path[2]
/bin
$ echo $path[3]
/usr/bin
$
```

注意，数组从索引位置 1 开始。

记住，shell 变量使用全小写字母，而环境变量使用全大写字母。将它们混淆可能会导致问题。

## 环境变量

`tcsh` shell 同样维护一组环境变量，与 `Bourne shell` 类似。表 21-3 列出了这些环境变量。

## 表 21-3

| 变量 | 描述 |
| --- | --- |
| AFSUSER | 等于 `fsuser` shell 变量。 |
| COLUMNS | 终端可用的列数。 |
| DISPLAY | 指向图形窗口 X Windows 服务器的指针。 |
| EDITOR | 默认编辑器的路径名。 |
| GROUP | 等于 `group` shell 变量。 |
| HOME | 等于 `home` shell 变量。 |
| HOST |  shell 进程的系统名称。 |
| HOSTTYPE | 运行 shell 进程的机器类型。 |
| HPATH | 冒号分隔的目录列表，`run-help` 编辑器会在其中查找命令文档。 |
| LANG | 指定首选字符环境。 |
| LC_CTYPE | 如果设置，则仅更改 `ctype` 字符处理。 |
| LINES | 终端的行数。 |
| LS_COLORS | 用于 `ls` 命令的文件类型和颜色分配的冒号分隔列表。 |
| MACHTYPE | 系统的微处理器类别或机器模型。 |
| OSTYPE | 系统的操作系统。 |
| PATH | 用于定位可执行文件的目录的冒号分隔列表。 |
| PWD | 等于 `cwd` shell 变量，但仅在实际更改目录后更新。 |
| REMOTEHOST | 如果当前用户已远程登录，则远程主机的 IP 地址。 |
| SHLV | 嵌套 shell 的数量（等于 `shvl` shell 变量）。 |
| SYSTYPE | 当前系统类型。 |
| TERM | 终端类型（等于 `term` shell 变量）。 |
| TERCAP | 终端能力字符串。 |
| USER | 等于 `user` shell 变量。 |
| VENDOR | 系统处理器的供应商。 |
| VISUAL | 全屏编辑器的路径名。 |

## tcsh Shell

许多 `tcsh` 环境变量是同名 shell 变量的重复。这是为了提供与 `Bourne shell` 环境的某些兼容性（注意包含 `PATH` 环境变量，其格式与 `Bourne shell` 的 `PATH` 环境变量相同）。

然而，两者之间没有建立关联。如果你更改了其中一个，另一个不会改变。在设置 shell 变量（如 `path`）的同时不设置相应的环境变量（`PATH`），可能会引发各种问题。

要显示当前环境变量，你必须使用 `setenv` 命令：

```
$ setenv
USER=test
LOGNAME=test
HOME=/home/test
PATH=/usr/local/bin:bin:/usr/X11R6/bin:/usr/X11R6/bin
MAIL=/var/mail/test
SHELL=/bin/tcsh
TERM=xterm
HOSTTYPE=i386-linux
VENDOR=intel
ostYPE=linux
MACHYPE=1386
SHLV=1
PWD=/home/test
GROUP=test
HOST=testbox
INPUTRC=/etc/inputrc
LESS=MM
LESSKEY=/etc/.less
BSUNUM=14
HOSTNAME=testbox
LSCOLS=00:00-fi=00:d1=01:34:
```

