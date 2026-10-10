
`restore -ivf /dev/tape`

| 命令 | 说明 |
| --- | --- |
| `add [arg]` | 将文件或目录添加到待提取文件列表中。被标记的文件在用 `*ls*` 列出时，其名称前会显示一个 `+` 号。被标记目录的所有子目录也会被提取。 |
| `cd arg` | 切换当前工作目录。 |
| `delete [arg]` | 从提取列表中删除文件或目录。被删除目录的所有子目录也将被移除。 |
| `extract` | 提取提取列表上的文件和目录。 |
| `help` | 显示可用命令列表。 |
| `ls [arg]` | 列出当前工作目录或指定目录的内容。 |
| `pwd` | 显示当前工作目录的完整路径。 |
| `quit` | 退出 `restore` 交互模式。即使提取列表中还有项，`quit` 命令也不会执行任何提取操作。 |
| `setmodes` | 设置提取中所有文件和目录的所有者、模式和时间。 |
| `verbose` | 在详细模式下，每个文件在提取时都会列出。此外，`ls` 命令会列出文件和目录的索引节点号（inode）。 |

表 18-5：`restore` 的交互模式 Shell 命令

此命令将生成一个包含备份整个目录结构的 shell。你将获得一个提示符，可以使用 `cd` 命令移动到不同目录，并使用 `ls` 列出文件和子目录。你使用 `add` 命令标记要提取的文件或目录。如果你以后决定不提取它，可以使用 `delete` 命令将其从标记列表中移除。一旦你选择了所有想要的项目，就可以输入 `extract` 命令从备份归档中检索。要退出恢复 shell，输入 `quit`。`help` 命令将列出 `restore` 命令。

如果你需要恢复整个文件系统，应使用带有 `-r` 选项的 `restore`。你可以将文件系统恢复到任何足够大小的空白格式化硬盘分区，包括文件系统的原始分区。如果可能，建议在另一个分区上恢复文件系统并检查结果。

恢复整个文件系统涉及设置一个格式化分区、将其挂载到你的系统，然后切换到其根目录以运行 `restore` 命令。首先，你应该使用 `-r` 选项来恢复文件系统。

```
restore -ivf /dev/tape
```

## 第三部分：设备与文件系统

## 19. Shell 配置

### Shell 初始化与配置
- 别名 `Aliases`
- 环境变量
- 子 shell `Subshells`

Linux 上通常使用四种主要的 shell：Bourne Again shell `BASH`、Korn shell、TCSH shell 和 Z shell。尽管它们各不相同，但 shell 共享许多相同特性。在 UNIX 中，Bourne shell 缺少许多功能。但在 Linux 中，BASH shell 包含了大部分功能。

| 特性 | 说明 |
| --- | --- |
| `bash` | BASH shell, `/bin/bash` |
| `bsh` | BASH shell, `/bin/bsh` |
| `sh` | BASH shell, `/bin/sh` |
| `tcsh` | TCSH shell, `/bin/sh` |
| `csh` | TCSH shell, `/bin/csh` |
| `ksh` | Korn shell, `/bin/ksh` |
| `zsh` | Z shell, `/bin/zsh` |

表 19-1：Shell 唤起命令

BASH shell 是大多数 Linux 发行版的默认 shell。如果你登录命令行界面，将被自动置于默认 shell，并获得一个 shell 提示符来输入命令。BASH shell 的 shell 提示符是美元符号 `$`。在 GUI 界面中（如 GNOME 或 KDE），你可以打开一个终端窗口，它将显示带有默认 shell `BASH` 提示符的命令行界面。虽然你登录的是默认 shell，但可以通过以下命令切换到其他 shell：`tcsh` TCSH shell、`bash` BASH shell、`ksh` Korn shell 和 `zsh` Z shell。你可以通过按下 `CTRL-d` 或使用 `exit` 命令退出。你的工作只需要一种 shell 即可完成。表 19-1 显示了调用不同 shell 的各种命令。某些 shell 提供了链接来调用 shell，例如 `sh` 和 `bsh`，它们链接到调用 BASH shell 的 `bash` 命令。

本章描述了 BASH shell 的常用特性（如别名），以及如何使用 shell 变量和初始化文件根据需求配置 shell。其他 shell 共享许多相同特性并使用类似的变量和初始化文件。

虽然这里展示了基础的 shell 特性和配置，但你应该参考每个 shell 相应的在线文档和 FAQ 以获取更详细的示例和解释。

### 初始化配置文件

每种类型的 shell 都有自己的一套初始化和配置文件。TCSH shell 使用 `.login`、`.tcshrc` 和 `.logout` 文件。`.profile`、`.bashrc` 和 `.bash_logout`。Z shell 具有几个初始化文件：`.zshen`, `.login`, `.profile`, `.zshrc`, `.logout`。列表请参见表 19-2。检查每个 shell 的 Man页（帮助手册）以查看它们通常是如何配置的。当你安装一个 shell 时，这些文件的默认版本会自动放置在用户的家目录中。除了 TCSH shell 外，所有 shell 在变量定义和赋值方面都使用非常相似的语法（TCSH 使用的语法略有不同，详见其 Man 页描述）。

| 文件名 | 功能 |
|---|---|
| BASH Shell | |
| `.bash_profile` | 登录初始化文件 |
| `.bashrc` | BASH shell 配置文件 |
| `.bash_logout` | 退出重名 |
| `.bash_history` | 历史文件 |
| `/etc/profile` | 系统登录初始化文件 |
| `/etc/bashrc` | 系统 BASH shell 配置文件 |
| `/etc/profile.d` | 专用 BASH shell 配置文件的目录 |
| `/etc/bash_completion` | 应用程序的补全选项 |
| TCSH Shell | |
| `.login` | 登录初始化文件 |
| `.tcshrc` | TCSH shell 配置文件 |
| `.logout` | 退出文件 |
| Z Shell | |
| `.zhenv` | Shell 登录文件（首次读取） |
| `.zprofile` | 登录初始化文件 |
| `.zlogin` | Shell 登录文件 |
| `.zshrc` | Z shell 配置文件 |
| `.logout` | 退出文件 |
| Korn Shell | |
| `.profile` | 登录初始化文件 |
| `.kshrc` | KORN shell 配置文件 |

表 19-2：Shell 配置文件

## 配置目录与文件

应用程序通常在用户的家目录中安装配置文件，这些文件包含特定的配置信息，用于根据该特定用户的需求定制应用程序。这可能表现为一个以点开头的单个配置文件，或者是一个包含多个配置文件的目录。该目录名称也将以点开头。例如，

Mozilla 在用户的家目录中安装了一个名为 `mozilla` 的目录，其中包含配置文件。另一方面，许多应用程序使用一个名为 `mailrc` 的单文件来存储用户设置的别名和功能设置，其他像 Evolution 这样的程序也有它们自己的 `evolution`。大多数单配置文件以字母 `rc` 结尾。FTP 使用名为 `netrc` 的文件。大多数读取使用名为 `newsrc` 的文件。配置文件中的条目通常由应用程序设置，尽管你通常可以通过编辑文件来创建条目。应用程序有自己的特殊变量，你可以在其中定义并分配值。你可以使用 `ls -a` 命令列出家目录中的配置文件。

## 别名 `Aliases`

你使用 `alias` 命令为命令创建另一个名称。`alias` 命令的操作类似于一个宏，会展开为它所代表的内容。别名并没有在字面上替换命令的名字；它只是给该命令起了另一个名字。`alias` 命令以关键字 `alias` 和命令的新名称开头，后面紧跟一个等号和该别名将引用的命令。

注意：`alias` 命令中使用的等号周围不能有空格。

在下一个示例中，`list` 变成 `ls` 命令的另一个名称：

```
$ alias list=ls

$ ls

mydata today

$ list

mydata today

$
```

如果你想让别名自动定义，必须在 shell 配置文件中输入 `alias` 操作。在 Fedora 上，别名定义在用户的 `bashrc` 文件或 `bash_aliases` 文件中。要使用 `bash_aliases` 文件，你必须首先取消 `bashrc` 文件中读取 `.bash_aliases` 的命令注释。只需编辑 `bashrc` 文件并删除前面的 `#`，使其出现如下所示的内容：

```bash
