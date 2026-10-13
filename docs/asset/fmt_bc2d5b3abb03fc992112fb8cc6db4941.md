
| ldpasswd | listgetopm | longsurfer | lynx |
| ldsearch | listalias | look | lynx-color |
| ldd | listec | lookbib | lyx |
| ddlibc4 | lib | lpost | |
| ddlibc5 | kbib | 1pq | |
| less | 11 | 1pr | |

`bash` shell 通过列出所有以字母 "I" 开头的命令（或当前目录中的任何可执行文件）作为响应。如果你无法记住复杂的命令名称，这会非常有用。

`bash` shell 还有内置帮助功能，并列出所有内置命令，以及每个命令的帮助信息。

# help

GNU bash, version 2.0.3(1)-release (i686-pc-linux-gnu)

这些命令是在内部定义的。输入 `help` 查看此列表。

输入 `help name` 可以了解更多关于函数 'name' 的信息。

使用 `info bash` 可以了解更多关于 shell 的通用信息。

![](img/cbf420b293bae713df92ae05ab020555_162_0.png)

名称旁星号 (*) 表示该命令已禁用。

```
%[DIGITS | WORD] [&] . filename
alias [-p] [name=value] ... [ arg...] ] bg [job_spec]
bind [-l-lPSVS] [-m keymap] -f fi break
builtin [builtin-shell] [arg ...] case WORD in [PATTERN | PATTERN.
co [-p] [dir] command [-pV] arg ...]
continue [-n] declare [-affRxi] [-p] name=value
dirs [-cluv] [+N] [-N] display [-h] [-ar] [jobspec]
echo [-neE] [arg ...] enable [-pnds] [-a] [-f filename
eval [arg ...] exec [-cl] [-a name] file [redirc
exit export [-nf] [...] or export
```

要获取特定命令的帮助，请在 `help` 命令后输入命令名称。例如，要获取帮助，请在 `help` 命令后输入命令：

# help

`help`: 打印内置命令的帮助。

`help name`: 查找更多关于函数 'name' 的信息。

`info bash`: 查找更多关于 shell 的通用信息。

`help`: 打印内置命令的帮助。

...帮助。

### 理解命令行

当你使用 shell 在命令行处启动程序时，shell 会解释你的命令，而程序将其输出回到你的屏幕上。通过 shell，你可以让程序的输出发送到其他地方，例如文件。事实上，SuSE Linux 下的一切都是文件；这包括终端、打印机等设备以及许多从其他文件接受输入的程序。shell 还可以将一个程序的输出作为另一个程序的输入，甚至可以告诉程序从文件中读取输入。你可以将 `ls` 命令的标准输出重定向到文件：

```
# touch /tmp/trash/file1 /tmp/trash/file2 /tmp/trash/file3
# ls -w 1 /tmp/trash/* >trashfiles.txt
```

## 使用 Shell

本节后续部分使用的示例均采用 `bash` shell。如果你想尝试这些命令行，但当前没有使用该 shell，可以在命令行中输入 `bash` 并按回车键以使用 `bash` shell。完成后，输入 `exit` 并按回车键，即可返回你原始的 shell。

![](img/cbf420b293bae713df92ae05ab020555_166_0.png)

举一个简单的例子，你可以使用 `cpio` 命令处理包含文件名的文件。你可以通过使用标准输入将文件名传递给 `cpio` 命令来实现这一点：

```bash
# cpio -o <trashfiles.txt >trash.cpio
1 block
```

此命令行导致 `cpio` 命令从标准的 `trashfiles.txt` 文件中读取文件列表，然后通过标准输出将其输出发送到名为 `trash.cpio` 的文件中，从而创建一个归档。

> `cpio` 命令与 `tar` 和 `dump` 命令一样，用于归档或备份 SuSE Linux 文件。请参第 23 节“备份和恢复你的系统”以学习如何使用备份程序。

![](img/cbf420b293bae713df92ae05ab020555_166_1.png)
