
| Table A.13 | 处理编码和压缩文件 |

| Table A.14 | 安装软件 |

| Table A.15 | 使用便捷实用程序 |

在本附录中，您将找到关于 Unix 命令和标志的相当全面的参考，以及每个命令的示例和描述。我们组织本附录以与本书大致平行，以便您可以轻松查阅关键命令和相关标志，而不必被一长串命令淹没。

表 A.a 总结了本附录中的内容。

表 A.1–A.15 包含与编号相同的章节所涵盖主题相关的命令和标志（第 16 章和第 17 章没有引入太多新命令，因此这些章节的命令包含在其他附录中的类似命令中）。除了各章节中讨论的命令和标志之外，您还会发现一些相关的命令和选项，它们可能在您的 Unix 冒险中有用、能唤起您记忆的参考信息，以及帮助您开始并进行其他项目的想法。如果您在寻找一份全面的命令标志参考，请查看附录 C。

## 表 A.1

### 快速入门 Unix：生存技能

| Command | Description |

|---|---|

| `apropos` keyword | 查找 keyword 的适当手册页。 |

| `cat` file | 在屏幕上显示文件内容或将文件内容提供给标准输出。 |

| `cat` file1 file2 | 显示 file1 和 file2。 |

| `cd` | 从 Unix 系统中的任何位置返回到你的主目录。 |

| `cd` .. | 在目录树中向上移动一级。 |

| `cd` `/etc` | 更改为相对于系统根目录的 `/etc` 目录。 |

| `cd` `~/subdir` | 使用波浪号 (`~`) 作为主目录的便捷快捷方式。 |

| `cd` Projects | 相对于当前目录移动到 Projects 目录。 |

| `col` -b | 过滤输入中的退格和反向换行。用于使手册页可编辑且不带奇怪格式。 |

| `Ctrl D` | 关闭当前进程（通常是 shell）以及如果你关闭登录 shell 则关闭你的 Unix 会话。 |

| `exit` | 关闭当前 shell，如果你在登录 shell 中则关闭你的 Unix 会话。 |

| `less` file | 用于逐屏查看文件。 |

| `logout` | 关闭你的 Unix 会话。 |

| `ls` | 列出文件和目录。 |

| `ls` `/` | 列出根目录中的文件和目录。 |

| `ls` `/directory` | 列出 directory 中的文件和目录。 |

| `ls` -a | 列出所有文件和目录，包括隐藏文件。 |

| `ls` -c | 按修改日期列出文件和目录。 |

| `ls` -l | 以长格式列出文件和目录，并提供额外信息。 |

| `ls` -lh | 以长格式列出文件和目录，并提供额外信息和可读的尺寸。 |

| `man` 5 command | 查看 command 手册页的指定章节（5）。有时用作 `man` -s 5 command。 |

| `man` command | 查看 command 的手册（帮助）页。 |

| `man` -k keyword | 查找 keyword 的适当手册页。 |

| `more` file | 更改你的密码。 |

| `passwd` | 显示你当前所在的目录的路径和名称。 |

| `pwd` | 重置 shell 以修复显示问题。 |

| `reset` | 尝试修复意外、突然且奇怪的显示问题。 |

| `stty` sane | 无需注销即可重新登录。 |

| `su` - yourid | 成为 root 用户。 |

| `su` | 以 root 用户的权限运行命令。 |

| `sudo` command |  |

## 使用目录和文件

| COMMAND | DESCRIPTION |

|---|---|

| `cp` existingfile newfile | 将 existingfile 复制到名为 newfile 的文件。 |

| `cp` -i existingfile oldfile | 将 existingfile 复制到名为 newfile 的文件，在覆盖现有文件前提示你。 |

| `cp` -r `/Projects` `/shared/Projects` | 将目录 `/Projects` 复制到新名称 `/shared/Projects`，指定递归复制。 |

| `find` . -name lostfile -print | 在当前目录或子目录中查找名为 lostfile 的文件。 |

| `find` `/home` -name `"pending*"` -print | 在主目录或子目录中查找所有名称以 `"pending"` 开头的文件。 |

| `find` `/home/shared` -mtime -3 -print | 查找在过去三天内被修改的 shared 目录中的所有文件。 |

| `find` ~ -name `"*.backup"` -exec compress {} \; | 压缩当前目录中名称包含 `"backup"` 的所有文件，无需确认。 |

| `find` ~ -name `"*.backup"` -ok rm {} \; | 查找并在确认后删除当前目录中所有名称以 `".backup"` 结尾的文件。 |

| `ln` `/home/a/*` `/home/b/*` | 将 a 目录中的所有文件硬链接到 b 目录中的文件。 |

| `ln` afile alink | 链接 afile 和 alink，使同一文件本质上存在于两个不同的目录中。 |

| `ln` -s `/home/deb/Projects` `/home/helper/Project` | 从 `/home/deb/Projects` 创建到 `/home/helper/Project` 的软链接。 |

| `locate` string | 查找名称中包含 string 的文件。 |

| `mkdir` Newdirectory | 创建一个名为 Newdirectory 的新目录。 |

| `mv` existingfile newfile | 将 existingfile 重命名为 newfile。 |

| `mv` -i oldfile newfile | 将 oldfile 重命名为 newfile，要求系统在覆盖（销毁）现有文件前提示你。 |

| `rm` badfile | 删除 badfile。 |

| `rm` -i * | 交互式删除，在删除前提示。适用于 Unix 认为其为命令标志的有问题名称的文件。 |

| `rm` -i badfile | 交互式删除 badfile。 |

| `rm` -ir dan* | 交互式删除当前目录中以 `"dan"` 开头的所有目录或文件，以及以 `"dan"` 开头的子目录中的所有文件和子目录。 |

| `rmdir` Yourdirectory | 删除空目录 Yourdirectory。 |

| `touch` newfile | 创建一个名为 newfile 且无内容的文件。 |

| `touch` -t 200112312359 oldfile | 将 oldfile 的文件日期更新为 2001 年 12 月 31 日 23 小时 59 分钟。 |

| `which` command | 找出 command 的完整路径。这对于查看具有相同名称的多个命令中将执行哪一个很有价值。 |

| `whereis` file | 找出 file 的完整路径以及相关文件。 |

## Table A.3

### Working with Your Shell

| COMMAND | DESCRIPTION |

|---|---|

| `!10` | Rerun command 10 from the history list in `csh` or `zsh`. |

| `bash` | Start a `bash` subshell or run a `bash` script. |

| `chsh` | Change your shell. |

| `csh` | Start a `csh` (C) subshell or run a `csh` shell script. |

| `echo` `$SHELL` | Display the value of the `$SHELL` environment variable. |

| `exit` | Leave the current shell and return to the previous one, or log out of the log-in shell. |

| `history` | View a numbered list of previous commands. |

| `ksh` | Start a `ksh` (Korn) subshell or run a `ksh` shell script. |

| `r` 2 | Repeat a specific command in `ksh` from the history output (in this case command 2). |

| `set` -o emacs | Enable command completion with emacs commands in the `ksh` shell. |
