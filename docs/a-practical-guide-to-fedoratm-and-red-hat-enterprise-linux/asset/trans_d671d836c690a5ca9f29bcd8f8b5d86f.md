

```bash
echo " c. Name of the working directory"
echo -e " d. Contents of the working directory\n"
read -P "Enter a, b, c, or d: " answer
echo
#
case "$answer" in
a)
date
;;
b)
who
;;
c)
pwd
;;
d)
ls
;;
*)
echo "There is no selection: $answer"
;;
esac
```

$ ./command_menu

命令菜单

a. 当前日期和时间
b. 当前登录的用户
c. 工作目录的名称
d. 工作目录的内容

输入 a、b、c 或 d: a

Sun Jan 6 12:31:12 PST 2013

`-e` 选项使 `echo` 将 `\n` 解释为换行符。如果不包含此选项，`echo` 不会输出那些使菜单易于阅读的额外空行，而是输出（字面意义的）两个字符序列 `\n`。`-e` 选项使 `echo` 解释其他几个反斜杠引用的字符（表 27-3）。请记住对反斜杠引用的字符进行引用（即在该字符串周围加上双引号），以便 shell 不会解释它，而是将反斜杠和字符传递给 `echo`。有关避免使用 `-e` 选项的方法，请参阅 `xpg_echo`（第 403 页）。

**表 27-3** `echo` 中的特殊字符（必须使用 `-e`）

| 引用字符 | `echo` 显示 |
| :--- | :--- |
| `\a` | 警报（铃） |
| `\b` | 退格 |
| `\c` | 抑制末尾换行 |
| `\f` | 换页 |
| `\n` | 换行 |
| `\r` | 回车 |
| `\t` | 水平制表符 |
| `\v` | 垂直制表符 |
| `\\` | 反斜杠 |
| `\nnn` | ASCII 八进制代码为 `nnn` 的字符；如果 `nnn` 无效，`echo` 按字面意思显示该字符串 |

你还可以使用 `case` 控制结构在脚本中执行各种操作，具体取决于调用脚本时提供的参数数量。以下名为 `safedit` 的脚本使用基于命令行参数数量（`$#`）进行分支的 `case` 结构。它调用 `vim` 并保存正在编辑的文件的备份副本。

```bash
$ cat safedit
#!/bin/bash

PATH=/bin:/usr/bin
script=$(basename $0)
case $# in

    0)
        vim
        exit 0
        ;;

    1)
        if [ ! -f "$1" ]
        then
            vim "$1"
            exit 0
        fi
        if [ ! -r "$1" -o ! -w "$1" ]
        then
            echo "$script: check permissions on $1" 1>&2
            exit 1
        else
            editfile=$1
        fi
        if [ ! -w "." ]
        then
            echo "$script: backup cannot be \
        created in the working directory" 1>&2
            exit 1
        fi
        ;;

    *)
    echo "Usage: $script [file-to-edit]" 1>&2
    exit 1
;;
esac
tmpfile=/tmp/$$.$script
cp $editfile $tmpfile
if vim $editfile
then
    mv $tmpfile bak.$(basename $editfile)
    echo "$script: backup file created"
else
    mv $tmpfile editerr
    echo "$script: edit error---copy of " \
        "original file is in editerr" 1>&2
fi
```

如果你不带任何参数调用 `safedit`，`case` 结构执行其第一个分支，并不带文件名参数调用 `vim`。因为并没有正在编辑现有文件，所以 `safedit` 不会创建备份文件。如果你带一个参数调用 `safedit`，它会运行 `case` 结构第二个分支中的命令，并验证 `$1` 指定的文件尚不存在，或者是用户拥有读写权限的文件。`safedit` 脚本还验证用户对工作目录具有写权限。如果用户带多个参数调用 `safedit`，`case` 结构的第三个分支将显示用法信息并以状态 1 退出。

- **设置 PATH**
  在脚本开头，`PATH` 变量被设置为搜索 `/bin` 和 `/usr/bin`。以这种方式设置 `PATH` 可以确保脚本执行的命令是标准实用工具，这些工具位于这些目录中。通过在脚本内部设置此变量，你可以避免可能遇到的问题，例如用户设置了 `PATH` 以优先搜索他们自己的目录，并且拥有与脚本调用的实用工具同名的脚本或程序。你还可以在脚本中包含绝对路径名来实现这一目的，尽管这种做法会降低脚本的可移植性。

- **程序名称**
  下一行声明了一个名为 `script` 的变量，并用脚本的简单文件名对其进行初始化：

```bash
script=$(basename $0)
```

`basename` 实用工具将其参数的简单文件名组件发送到标准输出，并使用命令替换将其赋值给 `script` 变量。`$0` 保存脚本被调用时使用的命令（第 1022 页）。无论用户使用以下哪个命令调用该脚本，`basename` 的输出都是简单文件名 `safedit`：

```bash
$ /home/max/bin/safedit memo
$ ./safedit memo
$ safedit memo
```

设置 `script` 变量后，它会在用法和错误消息中替换脚本的文件名。通过使用派生自调用脚本的命令的变量，而不是硬编码到脚本中的文件名，你可以为脚本创建链接或重命名它，而用法和错误消息仍然可以提供准确的信息。

- **临时文件命名**
  `safedit` 的另一个特性与在临时文件名称中使用 `$S` 参数有关。`esac` 语句后面的语句创建并赋值给 `tempfile` 变量。该变量包含一个存储在 `/tmp` 目录中的临时文件的名称，许多临时文件都存储在这里。临时文件名以 shell 的 PID 号开头，以脚本名称结尾。使用 PID 号确保文件名是唯一的。因此，即使两个人同时使用 `safedit`，`safedit` 也不会尝试覆盖现有文件。附加脚本名称是为了万一文件因某种原因遗留在 `/tmp` 中，你可以弄清楚它是从哪里来的。

文件名中 PID 号位于 `$script` 之前而不是之后，是因为某些旧版本的 UNIX 对文件名有 14 个字符的限制。Linux 系统没有这种限制。由于 PID 号确保了文件名的唯一性，将其放在首位可以防止其被截断。（如果 `$script` 部分被截断，文件名仍然是唯一的。）出于同样的原因，在脚本下方几行处的 `if` 控制结构中创建备份文件时，文件名由字符串 `bak.` 加上正在编辑的文件名组成。在旧系统上，如果 `bak` 用作后缀而不是前缀，且原始文件名为 14 个字符长，`bak` 可能会丢失，从而导致原始文件被覆盖。`basename` 实用工具在添加 `bak.` 前缀之前提取 `$editfile` 的简单文件名。

`safedit` 脚本在 `if` 结构中使用了一个不寻常的*测试命令*：`vim $editfile`。*测试命令*调用 `vim` 编辑 `$editfile`。当你完成编辑文件并从 `vim` 退出时，`vim` 返回一个退出代码。如果控制结构使用该退出代码来决定采取哪个分支。如果编辑会话成功完成，`vim` 返回 0，并执行 `then` 语句后面的语句。如果 `vim` 没有正常终止（例如用户*杀掉* [第 465 页]了 `vim` 进程），`vim` 返回非零退出状态，脚本执行 `else` 后面的语句。

## select

`select` 控制结构基于 Korn Shell 中发现的结构。它显示一个菜单，根据用户对项目的选择为变量赋值，并执行一系列命令。`select` 控制结构的语法如下：

```bash
select varname [in arg . . . ]

do

commands

done
```

`select` 结构显示*arg* 项目的菜单。如果你省略关键字 `in` 和参数列表，`select` 使用位置参数代替 *arg* 项目。

