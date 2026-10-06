
命令行目前最出色的功能可以使用 `<TAB>` 键补全目录或文件名的一部分，或者如果命令在路径中，则补全命令。

例如，当你尝试查找 `/usr/bin` 目录中哪些以字母 `ls` 开头的命令时，你可以使用以下操作：

点击此处查看图像-`/bin/ls<TAB>`

```
lsattr lsb_release lsdev lsdiff lskat lskkatproc lsppgpot
```

在不同目录之间切换时，它的效果非常好。你只需要插入下一个元素具有识别性的唯一部分，并按下 `Tab` 键即可补全目录名：

点击此处查看代码图像

```
cd /home/rb <TAB>
cd /home/rbrunson/Des <TAB>
cd /home/rbrunson/Desktop/Se <TAB>
cd /home/rbrunson/Desktop/Settings <Enter>
```

在 `rb` 字符后立即使用 `<TAB>` 会补全 `/home/rbrunson` 目录。在此添加斜杠（`/`）并输入 `Des` 然后按 `<TAB>` 会补全 `Desktop` 目录。最后，在末尾添加 `/Se` 然后按两次 `<TAB> <TAB>` 即可补全目标目录的完整路径。

> 注意
> `Tab` 补全不仅是为了速度，也是为了准确性。许多系统管理员都没有在配合 `rm` 命令使用 `Tab` 补全时删除了整个文件系统。

## Shell 中的特殊字符

许多字符对 `Shell` 具有特殊意义；其中一些定义在表 4-4 中。

### 核心话题

| 字符 | 用途 | 示例 |
|---|---|---|
| `~` | 当前用户主目录的简写 | `vi ~/.bashrc` |
| `\` | 忽略下一个字符（转义字符） | `echo SPRD is \$` |
| `/` | 目录分隔符 | `cd /home/rbrunson` |
| `$` | 变量，位于任何变量之前 | `echo VAR` |
| `?` | 单字符通配符 | `ls *.t` |
| `'` | 单（绝对） | `echo 'Cost: $100'` |
| `` ` `` | 反引号，用于替换 | `echo `date`` |
| `"` | 双引号 | `echo "Cost: $VAR"` |
| `*` | 零到多个通配符 | `ls dar*` |
| `&` | 在 shell 中后台运行作业 | `mozilla &` |
| `&&` | 如果 `cmd1` 退出 0（成功），则执行 `cmd2` | `cmd1 && cmd2` |
| `|` | 将输出管道到文件 | `ls -l pr` |
| `||` | 如果 `cmd1` 退出 1（失败），则执行 `cmd2` | `cmd1 || cmd2` |
| `;` | 执行多个命令 | `cmd1 ; cmd2` |
| `[]` | 字母/数字范围 | `ls file[0-9]` |
| `>` | 将输出重定向到文件 | `prog1 > file` |
| `<` | 将输入重定向到程序 | `prog1 < file` |

表4-4 常见特殊字符

### 控制命令执行

执行命令时总是会返回退出状态，但不总是显示。要显示退出状态，你必须使用 `echo` 命令和字符串 `$?`。

### 核心话题

#### 可能的退出状态

以下执行一个保证运行的命令，显示当前用户主目录下的所有文件：

点击此处查看代码图像

```
ls -a ~ 
.acrobat .adobe .bash_history .bashrc .dvipsrc
```

接下来，再次运行命令并使用特殊字符和特殊变量来返回退出状态：

点击此处查看代码图像

```
ls -a ; echo $ 
.acrobat .adobe .bash_history .bashrc .dvipsrc 
0
```

`0` 是命令的状态，由 `$` 变量回显。

现在，运行一个虚假的命令，或者你不知道运行了什么（我最喜欢的 `farg`）。你必须在之前的代码后面加上 `$` 变量；退出状态类似于 `1` 或 `127` —— 任何非 `0` 的值：

点击此处查看代码图像

```
farg ; echo $ 
-bash: farg: command not found 
127
```

总结来说，程序要么执行时无错误（成功）并返回退出状态 `0`，要么发生故障并返回非零退出状态（通常为 `1` 或 `127`）。

> 注意
> `Tab` 补全不仅是为了速度，也是为了准确性。许多系统管理员都没有在配合 `rm` 命令使用 `Tab` 补全时删除了整个文件系统。

## 环境变量与设置

许多字符对 `Shell` 具有特殊意义；其中一些定义在表 4-4 中。

### 路径

路径是一个由冒号分隔的目录列表，用于搜索可执行文件。它通常用于定位不在当前目录的命令。你可以通过两种方法引用当前目录中的文件：

- 绝对路径——`/home/`
- 相对路径——`./`

路径通常设置在所有用户的 `/etc/profile` 或单个用户的 `~/.bashprofile` 中。可以修改路径并添加目录。以下示例显示了操作：

1. 编辑 `/etc/profile` 或 `.bashprofile`。
2. 使用 `G` 跳到文件末尾。
3. 使用 `o` 打开新行进行编辑。
4. 添加以下行，将 `yourpath` 替换为系统的路径：

```
export PATH=$PATH:yourpath
```

### 获取 HOME

某些简写和变量指向用户的主目录，可以使用工具快速到达那里。

`HOME` 变量从 `/etc/passwd` 文件中的用户主目录条目读取。该变量值为当前用户主目录的完整路径：

点击此处查看代码图像

```
cd HOME — 进入 /home/username
```

另一种方法是直接使用 `cd` 命令。这将最快地返回主目录。

最后，你可以使用波浪号（`~`）字符引用用户的主目录，输入 `cd ~` 也能进入主目录。

> 注意
> 考试测试你是否理解如何进入主目录以及某些字符对你的作用。最容易被忽略和理解错误的错误是使用 `~username` 组合。示例：
> 你的系统有一个用户 `tarfoo`，你以 `root` 用户身份登录。系统上有一个 `/root/tarfoo` 的目录。运行命令 `cd ~tarfoo` 会进入 `tarfoo` 用户的主目录，而运行 `cd ~/tarfoo` 会进入 `/root/tarfoo` 目录。

## bash 历史功能

`history` 命令显示以前执行过的命令栈。

`bash_history` 函数依赖于一个名为 `HISTFILE` 的变量，该变量通常被设置为当前用户的 `.bash_history` 文件（位于用户的家目录）。当使用 `echo` 输出其内容时，它会返回用户历史文件的完整路径和名称，如下：

点击此处查看代码图片

```
echo $HISTFILE
/home/rbrunson/.bash_history
```

当用户使用登录 shell 或交互式/非登录 shell 登录时，会打开用户的 `.bash_history` 文件。通常情况下，在用户退出该 shell 会话之前，历史栈不会写入 `.bash_history` 文件。在用户登录并在登录 shell 中执行 `bash` 子 shell（subshell）的情况下，子 shell 会读取父 shell 的历史文件并在退出时将其写入其中。你可以通过执行以下操作看到这一过程：

1. 以用户身份登录到机器。
2. 执行以下命令：
3. 然后启动一个新 shell：
4. 在新 shell 中，执行以下操作：
5. 执行这些命令：
6. 使用以下命令退出子 shell：
7. 使用以下命令查看你的历史栈：
8. 使用以下命令查看现有 `.bash_history` 文件的最后 10 行：

点击此处查看代码图片

```
echo "this is the main shell history"
```

```
bash
```

点击此处查看代码图片

```
echo "this is the subshell history"
```

```
history
```

```
exit
```

```
history
```

`tail $HISTFILE`

![](img/16cd7204aa58beaaf530d67f50f15fc5_168_0.png)

### 重要历史变量

变量用于控制 `bash` 对历史文件的使用。以下是 shell 启动时化的常用历史变量：

- `HISTFILE`—默认值为 `~/.bash_history`，并在登录时设置在环境变量中。
- `HISTCDMD`—当前命令的历史记录或索引号，因此 `echo $HISTCDMD` 会显示该命令的编号。
- `HISTCONTROL`—如果设置为 `ignorespace`，以空格开头的行将不会添加到历史文件中。如果设置为 `ignoredups`，无论时间是否重复，与前一行内容重复的行都被忽略。
- `HISTFILESIZE`—历史栈在写入历史文件时使用的行数。如果生成的栈大于指定的大小，它将从文件开头截断以匹配正确的大小。默认值为 500。

### 在 bash 中设置选项

`bash` 使用内置命令 `set` 来开启或关闭选项。`bash 2.0` 及更高版本中新增了 `shift` 命令，它涵盖了 `set` 命令的功能。`LPI` 考试重点是 `set` 命令：

点击此处查看代码图片

```
set -o option (将选项开启)
set +o option (将选项关闭)
```

`set` 命令在开启选项时使用 `-o` 选项；反之，它使用 `+o` 规格符来关闭选项。

### 重要 bash 选项

`Bash` 有一组你在考试和现实生活中应该了解的选项。下列表列出了最常用的选项：

- `emacs` `vi`—这些用于设置编辑命令行时的键位映射样式。
- `history`—此选项默认开启。读取变量 `HISTFILE` 的值来确定历史文件。
- `hashall`—默认开启，此选项为请求的命令及其位置启用哈希表，以便重复使用命令。
- `monitor`—此选项导致作业控制使后台进程在单独组中运行，并在它们结束或完成时通知控制。
- `noclobber`—此选项默认关闭；开启时，不允许通过重定向符号 (`>`) 覆盖现有文件。如果尝试此类操作，将发生语法错误。建议使用双重定向（追加文件内容）。
- `noexec`—开启时对脚本文件进行干拟运行。交互式 shell 会忽略它，但脚本会检查所有命令的语法而不执行它们。
- `notify`—立即向控制报告已终止的作业，而不是等到下一次执行 `jobs` 命令。
- `verbose`—此选项在执行任何命令之前都会将其回显或打印到屏幕上。这对于视障用户以及作为执行字符串的检查非常有用。

预计会看到关于如何使用 `set` 和 `unset` 命令切换选项的问题。请记住，设置选项是通过 `set -o` 选项语法完成的，而取消或移除选项则需要 `set +o` 选项语法。预计看到如 `noclobber`、`history`、`vi` 和 `emacs` 等选项。

## 考试准备任务

正如引言中“如何使用本书”部分提到的，你有几种准备考试的选择：此处的练习题、第 21 章“最终准备”以及 DVD 上的模拟考试。

## 复习所有关键主题

本章中最重要的主题在页外边缘处用“关键主题”图标标记出。表 4-5 列出了这些关键主题的参考以及它们各自所在的页码。

![](img/16cd7204aa58beaaf530d67f50f15fc5_170_0.png)

| 关键主题元素 | 描述 | 页码 |
|---|---|---|
| 段落 | a 的定义 | 93 |
| 章节 | 登录 shell | 94 |
| 章节 | 一个 shell | 95 |
| 章节 | 命令结构 | 98 |
| 章节 | 命令补全 | 99 |
| 表 4-5 | 常用字符 | 100 |
| 章节 | 可能的状态 | 100 |
| 章节 | 历史文件 | 102 |
| 章节 | 路径 | 104 |
| 章节 | 重要变量 | |

## 关键术语

定义以下术语：

- 参数 (`argument`)
- 导出 (`export`)
- 历史 (`history`)
- 特殊 (`special`)

## 复习题

这些题目的答案在附录中。

1. 什么 shell 不支持内联编辑？
   a. `Bash`
   b. `Bash`
   c. `ksh`
   d. `csh`
2. 阅读以下短语：________ 是读取环境的过程。哪个单词可以正确完成上述陈述？
   a. 替换
   b. 翻译
   c. 加载
   d. 解析
   e. 源
3. 在尝试执行一个长名称命令时，你不记得最后几个字符。接下来输入哪个字符可以找到命令剩余部分？
   a. `ESC`
   b. `Ctrl-Enter`
   c. `Tab`
4. 执行命令后，你没有看到错误信息，但命令的行为和输出有所不同。你可以在随后的行输入什么来查看是否存在错误？
   a. `echo $`
   b. `echo?`
   c. `echo`
5. 在行上执行以下哪些命令可以返回你的家目录？（选择所有适用项）
   a. `cd $HOME`
   b. `cd`
   c. `cd ~`
   d. `cd`
   e. `cd /home`
6. 哪个命令可以用于显示历史文件的最后 10 行？
   a. `tail -f /var/history`
   b. `history | tail`
   c. `cat +10 $HISTFILE`
   d. `last`
- 1. 经常变化的文件应该放在：
  a. `/usr`
  b. `/proc`
  c. `/root`
  d. `/var`
- 2. 你的 shell 位于 `/usr/local`。你输入 `cd ../bin`。当你输入 `pwd` 时，显示哪个目录？
  a. `/bin`
  b. `/usr/bin`
  c. `/usr/local/bin`
  d. 无，此命令返回错误。
- 3. 下列哪个目录应该与根目录 (`/`) 位于同一个分区？
  a. `/boot`
  b. `/usr`
  c. `/home`
  d. `/sbin`
- 4. 你在一个名为 `foo` 的目录中发现了一个文件。找出该文件是什么或做什么的好方法是：
  a. `file foo`
  b. `/foo`
  c. `cat foo`
  d. `which foo`
- 5. 使用什么命令可以更新文件的日期？
  a. `tar`
  b. `file`
  c. `date`
  d. `touch`
- 6. 你正尝试创建一个新的嵌套目录：`/a/b/c/d/`。创建这个嵌套目录集最快的方法是：
  a. `mkdir /a; mkdir /a/b; mkdir /a/b/c; mkdir /a/b/c/d`
  b. `mkdir /a/b/c`
  c. `mkdir -p /a/b/c`
  d. `md /a/b/c`
- 7. 你知道系统中有多个 `doit` 命令副本。你如何找到在命令行输入 `doit` 时运行的是哪一个？
  a. `whereis doit`
  b. `locate doit`
  c. `find doit`
  d. `which doit`
- 8. 你知道你今天早上下载了一个名为 `backup.tar.gz` 的文件，但不记得把它存放在哪里了。找到该文件的最合适命令是：
  a. `find / -name backup.tar.gz`
  b. `find backup.tar.gz`
  c. `locate backup.tar.gz`
  d. `whereis backup.tar.gz`
- 9. 你想把 Fred 的家目录打包到 U 盘中，在他离开公司时随身带走。哪个命令最好？快点，有蛋糕吃！
  a. `/home/fred | tar -czf /media/removable/fred.tar.gz`
  b. `tar -czf /home/fred > /media/removable/fred.tar.gz`
  c. `cd /home/; tar -cjf /media/removable/fred.tar.bz2 fred`
  d. `cd /home/fred tar -cjf /media/removable/fred.tar.bz2 *`
- 10. 包含 `/etc/pine.cone` 的命令 `-tf archive.tar` 作用是什么？
  a. 创建一个包含 `/etc/pine.cone` 的新存档 `archive.tar`
  b. 将 `etc/pine.cone` 添加到存档
  c. 检查 `etc/pine.cone` 是否在存档内部
  d. 从 `archive.tar` 中提取 `etc/pine.cone`
- 11. 哪种压缩工具提供了最高压缩率？
  a. `bzip2`
  b. `gzip`
  c. `compress`
  d. `cpio`

## 基础主题 (Foundation Topics)

## 文件系统概述 (Filesystem Overview)

文件系统的结构从文件系统的根开始，用斜杠字符 (`/`) 表示。文件系统上的每个项目都可以从系统根通过唯一的路径访问，无论它存储在哪个设备上，例如 `/usr/local/bin/foobar`。

`Unix` 在某些文件的存放位置演化出了自己的传统。商业和学术版 `Unix` 的碎片化导致了根据你使用的 `Unix` 版本而产生不同的惯例差异。

`Linux` 借鉴了许多 `Unix` 的实践，并以不同发行版的形式拥有其自身的碎片化。社区开始着制定一种名为“文件系统层次结构标准”（`FHS`）的文件系统布局标准，以便人们和软件更容易知道文件可以在哪里找到。

最新的 `FHS` 可以在 `http://www.pathname.com/fhs/` 找到。

`LPI` 根据 `FHS 2.3` 编写了关于目录结构的考试题。`FHS` 并不是一个真正的标准，而是一套明确的建议，大多数（并非所有）发行版厂商都遵守。考试中的许多题目引用了 `FHS`。

## 东西该归哪里 (What Belongs Where)

考试对于 `Linux` 文件的正确目录和位置看得很非常重，但没有什么比问什么绝对应该放在根目录 (`/`) 中，或者什么可以被放在其他地方更让人头疼的。

## 系统根目录 (The Root of the System)

从根目录 (`/`) 开始，表 5-2 列出了常见的顶层目录，并对每个目录进行了简短说明：

| 目录 | 说明 |
|---|---|
| `bin` | 所有用户的二进制执行文件 |
