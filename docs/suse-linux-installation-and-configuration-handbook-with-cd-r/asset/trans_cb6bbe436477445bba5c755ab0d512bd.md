

| 选项 | 含义 |
| --- | --- |
| -S | 文件存在且为套接字。 |
| -t | 文件存在且在终端上打开。 |
| -u | 文件存在且设置了 set uid 位。 |
| -w | 文件存在且可写。 |
| -x | 文件存在且可执行。 |
| -O | 文件存在且由当前用户拥有。 |
| -G | 文件存在且由当前组拥有。 |
| -z | 文件存在且长度为零字节。 |
| -n | 文件存在且长度不为零字节。 |

这是一次关于 shell 脚本编写的简短速成课程。Shell 脚本是 Linux 最强大的方面之一。如何完全掌握它们超出了本书的范围，但这是你绝对应该追求的。通过 shell 脚本可以完成很多事情，你会感到惊讶。获取更多信息的良好起点是 SuSE Linux 中可用的脚本。阅读 /etc/profile 并查看 /sbin/init.d 中的 init 脚本以获取更多脚本——这些都是艺术品！

## TCSH 特性

TCSH 是你可以在 SuSE Linux 中使用的另一个 shell。它在许多方面与 bash 相似，因为 bash 继承了 TCSH 的一部分。TCSH 是对旧的 C shell 的改进，并且对程序员特别有吸引力，因为它使用与 C 语言相似的语法。你不必是程序员就会知道如何使用 shell，但如果你是，你会更喜欢它。作为交互式 shell，TCSH 几乎与 bash 完全相同，但在脚本方面，两者差异很大。

## 初始化文件

TCSH 有三个配置文件，.login、.tcshrc 和 .logout。这些文件在 TCSH 中的工作方式与在 bash shell 中相同。

.login 文件在每次以登录 shell 运行 TCSH 时执行。此文件对应于 bash shell 使用的 .profile 文件。.login 文件应包含你希望在登录时声明的任何环境变量。SuSE 团队没有为你提供 .login 文件，因为 bash 是 SuSE Linux 的默认 shell。因此，你不必像使用 bash 的 .profile 那样从此文件开始。

.tcshrc 文件在每次运行 shell 时执行，无论它是登录 shell 还是子 shell。此文件与 bash 中的 .bashrc 文件相同。在此文件中输入你希望在所有 TCSH 实例中使用的所有环境变量。如果你想遵循 SuSE 的方法，你可以在 .tcshrc 文件中输入你想要的所有环境变量，然后从 .login 文件调用此文件。

最后一个配置文件是 .logout。这与 bash 中的 .bash_logout 文件类似。在此文件中输入你希望在退出 shell 时执行的任何命令。

## 环境变量

TCSH 使用环境变量进行配置，就像 bash 一样。但，与 bash 中使用 export 命令不同，你在 TCSH 中使用 set 命令来配置变量。要取消一个变量，你使用 unset 命令。以下段落讨论了你可以为 TCSH 配置的选项。

如果你希望 TCSH 在执行命令之前回显你输入的命令，你可以设置 echo 变量。要这样做，你输入以下命令：

```
> set echo
```

TCSH 的默认行为是允许用户通过按 Ctrl+D 键组合退出 shell。要禁用此功能，你输入以下内容：

```
> set ignoreeof
```

如果你希望 TCSH 在重定向命令输出时避免覆盖文件，你输入此命令：

```
> set noclobber
```

前一个命令会导致 shell 检查你要重定向输出到的文件是否已存在。如果存在，它会给出错误而不是覆盖它。

如果你希望 shell 在后台作业终止时通知你，设置 notify 变量：

```
> set notify
```

以下是重要的 TCSH 环境变量列表：

- home—这是由 shell 声明的，其值为你的主目录的路径。
- user—这是由 shell 声明的，其值为当前用户的名称。
- cwd—这是由 shell 声明的，其值为当前工作目录。
- path—这是 shell 将搜索二进制文件的目录列表。
- shell—这是当前 shell 二进制文件的路径。
- prompt—这是主 shell 提示符。
- cdpath—这是 cd 命令将搜索目录的路径列表。

## TCSH 中的脚本编写

脚本是一个包含 TCSH 要执行的命令的文本文件。它类似于编写程序。TCSH 脚本的功能与 MS-DOS 中的批处理文件相同，例如。

要编写 shell 脚本，你必须在文本文件中编写要执行的命令，然后运行该文件。让我们看一个简单 shell 脚本的示例，看看它是如何构建的。使用你喜欢的编辑器，在一个新文本文件中输入以下内容：

```
#
ls
```

将文件保存为 myls 并退出。你有两种选择来运行此 shell 脚本，要么将其提供给 TCSH，要么使其可执行。以下是第一种方法的示例：

```
>tcsh myls
```

前一个命令启动一个新的 TCSH，它将读取你的脚本并执行它。你也可以使脚本可执行，以便像普通程序一样运行它。要做到这一点，你必须更改文件的权限使其可执行：

```
> chmod u+x myls
> myls
```

shell 脚本现在将像普通程序一样运行。当你运行它时，文件中的第一个字符 # 表示此文件是 TCSH shell 脚本。因此，你应该将此字符作为脚本中的第一个字符输入。实际脚本非常简单；它只是运行 ls 命令。

你可以添加内容使 shell 脚本更复杂，如下所示：

```
#
clear
ls
```

现在，脚本首先清除屏幕，然后执行 ls 命令。你也可以添加更多命令并使用管道和重定向运算符，如果你愿意。你甚至可以使 shell 脚本从命令行读取参数。以下是一个示例：

```
#
clear
ls $1 | less
```

前一个脚本以目录路径作为其参数。然后，它列出该目录的内容并将其通过管道传输到 less 命令以分页显示。在命令
> myls /usr/
中，$1 被替换为你提供的第一个命令行参数。命令行参数从 $0 开始，$0 是实际 shell 脚本的名称。在我们的示例中，myls 是 shell 脚本的名称，$1 是第一个参数，$2 是第二个参数，以此类推。

你可以在 shell 脚本中使用环境变量来读取用户输入。例如，修改脚本如下：

```
#
clear
echo "Which directory do you want to view?"
set DIR = $<
ls $DIR | less
```

与 bash 不同，TCSH 没有 read 命令，而是使用 $< 特殊字符将标准输入重定向到变量。它从用户读取输入并将其分配给名为 DIR 的环境变量。ls 命令以 DIR 中的值为参数。

脚本使用控制结构使你能够根据某个值的不同执行 shell 的某些部分。例如，让我们扩展我们的简单脚本以提供一个漂亮的菜单：

```
#
clear
echo "Simple Script"
echo "1- Normal ls"
echo "2- Paged ls"
echo "3- Exit"
echo "Please make your choice"
set CHOICE = $<
switch ($CHOICE)
case 1:
    ls $1
    breaksw
case 2:
    ls $1 | less
    breaksw
case 3:
    exit
    breaksw
default:
    echo "Unknown choice...Aborting"
    exit
endsw
```

此脚本将显示一个包含三个选项的菜单。它使用标准输入重定向来读取用户的输入，然后使用 switch 构造根据该选择确定执行哪一部分。正如你所见，它与在 C 语言中编程非常相似。

在 TCSH 中编写脚本是一项相当高级的任务，甚至比在 bash shell 中编写脚本更高级，因为它使用编程语言语法和结构。对于程序员来说，这不应该是个问题。

