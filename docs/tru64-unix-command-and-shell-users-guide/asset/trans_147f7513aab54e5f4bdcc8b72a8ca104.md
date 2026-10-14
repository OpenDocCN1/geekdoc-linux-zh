

# Export global variables
export PATH ENV EDITOR FCEDIT PS1

# Set mail variables
MAIL=/usr/spool/mail/$LOGNAME
MAILCHECK=300

## 表8-12：Korn或POSIX Shell的.profile脚本示例

| 命令 | 描述 |
|---|---|
| 设置环境变量 | |
| PATH=/usr/bin:/usr/local/bin | 指定搜索路径。在本例中，先搜索 /usr/bin，再搜索 /usr/local/bin。 |
| ENV=$HOME/.kshrc | 指定 $HOME/.kshrc 作为登录脚本。 |
| EDITOR=vi | 指定 vi 作为 shell 提示符下命令行编辑和文件名补全的默认编辑器。 |
| FCEDIT=vi | 指定 vi 作为 fc 命令的默认编辑器。 |
| PS1="'hostname' [!] $ " | PS1 变量指定 Korn 或 POSIX shell 的提示符。其默认值为 $。此变量赋值指定将提示符改为：hostname 命令的输出，后跟当前命令的命令编号，再后跟美元符号（$）。例如，如果您的系统名称为 boston，且当前命令编号为 30，则提示符将是：boston[30] $。 |
| 导出全局变量 | |
| export PATH ENV EDITOR FCEDIT PS1 | 指定将 PATH、ENV、EDITOR、FCEDIT 和 PS1 变量的值导出到所有子 shell。 |
| 设置邮件变量 | |
| MAIL=/usr/spool/mail/$LOGNAME | 指定邮件系统用来检测新邮件到达的文件的路径名。在本例中，邮件系统会在 /usr/spool/mail 目录下您的用户名子目录中查找。 |
| MAILCHECK=300 | 指定 shell 每 300 秒（5 分钟）检查一次邮件。 |
| a 关于 fc 命令的信息，请参见 8.4.4 节。 |

在下面的 .kshrc 登录脚本中，设置了 shell 变量、命令别名、命令历史变量以及文件创建权限。表 8-13 解释了脚本的每个部分。

```
# Set shell variables
set -o monitor
set -o trackall

# Set command aliases
alias rm='rm -i '
alias rename='mv '
alias l 'ls -l'
alias c clear

# Set history variables
HISTSIZE=40

# Set file creation permissions
umask 027
```

## 表8-13：.kshrc脚本示例

| 命令 | 描述 |
|---|---|
| Shell变量 | |
| set -o monitor | 指定 shell 监视所有后台进程，并在进程完成时显示完成消息。 |
| set -o trackall | 指定 shell 跟踪您执行的所有命令。命令被跟踪后，shell 会存储该命令的位置，并在您下次输入时更快地找到该命令。 |
| 命令别名 | |
| alias rm='rm -i' | 指定 rm 命令使用 -i 选项（该选项会提示您确认文件删除）。 |
| alias rename='mv' | 指定 rename 作为 mv 命令的新名称。 |
| alias l='ls -l' | 为 ls -l 命令定义一个短名称，该命令以长格式列出目录文件。 |
| alias c='clear' | 为 clear 命令定义一个短名称，该命令用于清空屏幕。 |
| 历史变量 | |
| HISTSIZE=40 | 指示 shell 将最近 40 条命令存储在历史缓冲区中。 |

**表8-13：.kshrc脚本示例（续）**

| 命令 | 描述 |
|---|---|
| 设置文件创建权限 | |
| `umask 027` | 指定所有新建文件的最大权限。此命令为所有者提供所有权限，为同组成员提供读和执行权限，而其他用户没有权限。umask 不会被子 shell 继承。 |

## 8.4.2 元字符

表8-14描述了Korn或POSIX shell元字符（对shell具有特殊含义的字符）。这些元字符的含义，根据它们出现在shell脚本中、文件名规范中、用于引用其他字符时、输入/输出规范中或用于指示变量替换时，按解释进行分组。

**表8-14：Korn或POSIX Shell元字符**

| 元字符 | 描述 |
|---|---|
| 语法 | |
| `|` | 分隔管道中的命令。 |
| `&&` | 如果当前命令成功，则运行下一条命令。 |
| `||` | 如果当前命令失败，则运行下一条命令。 |
| `;` | 分隔应按顺序执行的命令。 |
| `;;` | 分隔 case 构造的元素。 |
| `&` | 在后台运行命令。 |
| `()` | 在子 shell 中将命令分组为一个单独的进程。 |
| `{}` | 在不创建子 shell 的情况下对命令分组。 |
| 文件名 | |
| `/` | 分隔文件路径名的各个部分。 |
| `?` | 匹配除前导点（`.`）之外的任何单个字符。 |
| `*` | 匹配除前导点（`.`）之外的任何字符序列。 |

