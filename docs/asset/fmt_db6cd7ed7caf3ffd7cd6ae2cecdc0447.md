
# 960 第 27 章 编写 BOURNE AGAIN SHELL 编程

在 `cat` 和 `less` 中使用可选的 `--` 参数可以告诉这些实用程序命令行之后不再有更多选项，并且不要将后续列表中开头的连字符 `-` 视为选项。因此，`--` 允许你查看一个以连字符开头命名的文件。虽然并不常见，但以连字符开头的文件名确实存在。`你可以使用命令 cat --fname 创建这样一个文件。` `---argument` 适用于所有使用 `getopts` 内置命令（第 1012 页）解析其选项的 Linux 工具；它不适用于更多和其他少数工具。该参数在配合 `rm` 删除文件名以连字符开头的文件时（`rm --fname`）特别有用，包括你在实验 `--argument` 时创建的任何文件。

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_1010_0.png)

图 27-3 if...then...elif 流程图

## if...then...elif

`if...then...elif` 控制结构（图 27-3）具有以下语法：

```
if if...test-command
  then
    commands
elif test-command
  then
    commands
  ...
  else
    commands
```

`elif` 语句将 `else` 语句和 `if` 语句结合在一起，并允许你构建一组嵌套的 `if...then...else` 结构（图 27-3）。`else` 语句和 `elif` 语句之间的区别是，每个 `else` 必须与一个 `fi` 语句配，而多个嵌套的 `elif` 语句只需要一个结束的 `fi` 语句。

下面的示例展示了一个 `if...then...elif` 控制结构。该 shell 脚本比较用户输入的三个单词。第一个语句使用布尔运算符 `-a` 作为参数进行测试。只有当第一个和第二个逻辑比较为真时（即 `word1` 匹配 `word2` 且 `word2` 匹配 `word3`），内置 `test` 才返回 true 状态。如果 `test` 返回 true 状态，脚本将执行下一个语句之后的命令，将控制传递给 `fi` 之后的语句，并终止：

```
$ cat if3
echo -n "word 1: "
word1
echo -n "word 2: "
word2
echo -n "word 3: "
word3
if ["$word1" = "$word2" -a "$word2" = "$word3"]
  then
    echo "Match: words 1, 2, & 3"
  elif ["$word1" = "$word2"]
  then
    echo "Match: words 1 & 2"
  elif ["$word1" = "$word3"]
  then
    echo "Match: words 1 & 3"
  elif ["$word2" = "$word3"]
  then
    echo "Match: words 2 & 3"
  else
    echo "No match"
fi
```

```
$ ./if3
word 1: apple
word 2: orange
word 3: pear
No match
$ ./if3
word 1: apple
word 2: orange
word 3: apple
Match: words 1 & 3
$ ./if3
word 1: apple
word 2: apple
word 3: apple
Match: words 1, 2 & 3
```

如果这三个单词不同，该结构会将控制传递给第一个 `if`，它将开始一系列测试，以检查任何一对单词是否相同。如果其中一个 `if` 满足条件，结构会将控制传递到下一个语句，随后传递到 `fi` 之后的语句。每当一个 `if` 语句不满足条件时，结构会将控制传递到下一个 `elif` 语句。参数周围的双引号防止了 shell 将其解释为特殊字符。

## 可选脚本

下面的名为 `Inks` 的脚本演示了 `if...then` 和 `if...then...elif` 控制。该脚本查找其第一个参数（一个文件名）的硬链接。如果你提供目录名作为第二个参数，`Inks` 将以该目录为根的层次结构中搜索链接。如果你不指定目录，`Inks` 将搜索工作目录及其子目录。该脚本不定位符号链接。

```
$ cat Inks
#!/bin/bash
# Identify links to a file
# Usage: Inks file [directory]
```

```
if [ $# -eq 0 -o $# -gt 2 ]; then
    echo "Usage: Inks file [directory]" 1>&2
    exit 1
fi
if [ -d "$1" ]; then
    echo "First argument cannot be a directory." 1>&2
    echo "Usage: Inks file [directory]" 1>&2
    exit 1
else
    file="$1"
fi

if [ $# -eq 1 ]; then
  directory=""
elif [ -d "$2" ]; then
  directory="$2"
else
  echo "Optional second argument must be a directory." 1>&2
  echo "Usage: Inks file [directory]" 1>&2
  exit 1
fi

# 检查文件是否存在并是普通文件
if [ -f "$file" ]; then
  echo "Inks: file not found or special file" 1>&2
  exit 1
fi

# 检查文件的链接数
set --=$(ls -l "$file")
if [ $# -eq 1 ]; then
  echo "Inks: no other hard links to $file" 1>&2
  exit 0
fi

# 获取给定文件的 inode
set --=$(ls -i "$file")
inode=$1

# 查找并打印 inode 相同的文件
echo "Inks: using find to search for links..." 1>&2
find "$directory" -xdev -inode $inode -print
```

`Max` 在家目录下有一个名为 `letter` 的文件。他想在其他用户的目录树中找到该文件的链接。在下面的示例中，`Max` 从他的家目录调用 `Inks` 来执行搜索。`Inks` 的第二个参数 (`/home`) 是他想要开始搜索的目录路径。`Inks` 脚本报告 `/home/max/letter` 和 `/home/zach/draft` 是该文件的链接。

```
$ ./inks letter /home
Inks: using find to search for links...
/home/max/letter
/home/zach/draft
```

在 `if...then...elif` 控制结构，`Inks` 引入了 shell 程序中常用的其他功能。下面的讨论将逐节介绍 `Inks`。

指定 shell

`Inks` 脚本的第一行使用 `#!` (page 302) 指定执行脚本的 shell：

```
#!/bin/bash
```

# 964 第 27 章 编写 BOURNE AGAIN SHELL 编程

在本章中，`#` 符号只出现在复杂的示例中。它确保即使用户运行不同的 shell 或脚本从不同的 shell 调用，正确的 shell 也会执行脚本。

注释

`Inks` 的第二和第三行是注释；shell 会忽略井号 (`#`) 之后到换行符之间的文本。这些注释简要说明了文件的功能以及如何使用它：

```
# Identify links to a file
# Usage: Inks file [directory]
```

用法消息

第一个 `if` 语句测试 `Inks` 是否带有零个参数或两个两个参数：

```
if [ $# -eq 0 -o $# -gt 2 ]; then
    echo "Usage: Inks file [directory]" 1>&2
    exit 1
fi
```

如果其中任一条件的状态为 1，`Inks` 将向标准错误发送用法消息并退出。用法消息周围的双引号防止 shell 将中括号解释为特殊字符。用法消息中的中括号表示目录是可选的。

第二个 `if` 语句测试第一个命令行参数 (`$1`) 是否为目录（`-d` 参数用于测试文件是否存在且是目录则为真）：

```
if [ -d "$1" ]; then
    echo "First argument cannot be a directory." 1>&2
    echo "Usage: Inks file [directory]" 1>&2
    exit 1
else
    file="$1"
fi
```

如果第一个参数是目录，`Inks` 将显示用法消息并退出。如果不是目录，`Inks` 将在脚本后面将 `$1` 的值保存到 `file` 变量中。`set` 会重置命令行参数。如果在发布 `set` 命令之前保存 `$1` 的值，其值将会丢失。

# 控制结构

第一个测试命令确定用户是否在命令行上指定了单个参数。如果测试命令返回 0（真），则将目录变量赋值为工作目录的值（`.`）。如果测试命令返回假，则 `elif` 语句将测试第二个参数是否为目录。如果是目录，则将目录变量设置为第二个命令行参数 `$2`。如果 `$2` 不是目录，`Inks` 将向标准错误输出一条用法信息并以状态 1 退出。

下一个 `if` 语句测试 `$file` 是否存在。此测试可以防止 `Inks` 浪费时间去寻找不存在的文件链接。当内置命令 `test` 被带上三个参数 `!`、`-f` 和 `$file` 时，如果 `$file` 不存在，则评估结果为真：

```
[ ! -f "file" ]
```

`!` 运算符对 `-f` 参数进行解码以取反其结果，如果 `$file` 存在且是一个普通文件，则结果为假。

`Inks` 使用 `set` 和 `-l` 来检查 `$file` 拥有的链接数量：

```bash
# 检查文件的链接计数
set --$(ls -l "file")
linkcount=$2
if [ "$linkcount" -eq 1 ]; then
  echo "Inks: no other hard links to $file" 2>&1
  exit 0
fi
```

内置命令 `set` 使用命令替换（见第 362 页）将位置参数设置为 `-l` 的输出。该输出的第二个字段是链接计数，因此用户创建的变量 `linkcount` 等于 `$2`。在 `set` 中使用的 `--` 可以防止 `set` 将 `ls -l` 产生的第一个参数解释为选项（第一个参数是文件的访问权限，通常以 `-` 开头）。`if` 语句检查 `linkcount` 是否等于 1；如果是，`Inks` 将显示消息并退出。尽管这条消息不是真正的错误消息，但它被重定向到了标准错误。正如“为什么”部分所，所有的信息性消息都发送到标准错误。只有 `Inks` 的最终输出——指向指定文件的链接路径会被发送到标准输出，因此你可以随所欲地重定向输出。

如果链接计数大于 1，`Inks` 将去识别 `$file` 的 inode (1153)。正如第 229 页所解释的，比较与文件名相关的 inode 是判断文件名是否指向同一个文件链接的良好方法。`Inks` 脚本使用 `set` 将位置参数设置为 `ls -i` 的输出。`set` 的第一个参数是文件的 inode 号，因此用户创建的变量 `inode` 被赋值为 `$1` 的值：

```bash
# 获取给定文件的 inode
set --$(ls -i "file")
inode=$1
```

# 第 27 章 编写 BOURNE AGAIN SHELL (BASH)

最后，`Inks` 使用该工具搜索 inode 号与 `$inode` 匹配的文件：

```bash
# 正在查找 Inks：使用 find 搜索链接...
echo "$directory" -xdev -inum $inode -print
```

该工具在以第一个参数（`Directory`）指定的目录为根的目录中，搜索符合剩余参数指定标准的文件。在本例中，剩余参数是 inode 与当前 `$inode$` 匹配的文件名，并将其它们输出到标准输出。由于不同系统中的文件可能具有相同的 inode 号但并没有链接，`find` 必须只搜索与 `$directory` 位于同一文件系统中的目录。`-xdev`（跨设备）参数防止 `find` 搜索其他文件系统上的目录。有关文件系统和链接的更多信息请参阅第 226 页。

`Inks` 中命令前的 `echo` 命令告诉用户 `find` 正在运行，这是因为 `find` 运行可能需要长时间。由于 `Inks` 不包含最终的退出语句，`Inks` 的退出状态取决于它运行的最后一个命令 `find` 的退出状态。

# 调试 shell 脚本

当你使用 `bash` 编写脚本时，很容易出错。你可以使用 shell 的 `-x` 选项来帮助调试脚本。此选项会导致 shell 在运行每个命令之前先显示该命令。通过这种方式跟踪脚本的执行可以让你获得关于问题所在的信息。

你可以运行上一个示例中的 `Inks` 并让 shell 在执行每个命令前显示。你可以为当前 shell 设置 `-x` 选项（`set -x`），以便所有脚本在运行时显示命令；或者使用 `-x` 选项仅影响通过命令运行脚本的 shell。

```bash
$ bash -x inks 1 letter /home
+ '[' 2 -eq 0 ]
+ '[' -d letter ]
+ file=letter
+ '[' 2 -eq 1 ]
+ '[' -d /home ]
+ directory=/home
+ '[' '!' -f letter ]
...
```

每个脚本执行的每个命令前面都有 `PS4` 变量的值——默认情况下是一个加号（`+`），这样你可以区分调试输出和脚本产生的输出。如果你在调用脚本的 shell 中设置了 `PS4`，则必须将其导出（export）。接下来的命令将 `PS4` 设置为 `>>>>` 后跟一个空格并将其导出：

```bash
$ export PS4='>>>> '
```

你也可以通过在脚本开头放置以下 `set` 命令来设置运行脚本的 shell 的 `-x` 选项：

```bash
set -x
```

在脚本中任何你想开启调试的地方放置 `set -x`。使用加号关闭调试选项：

```bash
set +x
```

`set -o xtrace` 和 `set +o xtrace` 命令分别与 `set -x` 相同的功能。

`for` 循环结构的语法如下：

```bash
for index in list
do
    commands
done
```

使用 "@"：该脚本使用 `for` 语句循环遍历命令行参数。

在在该脚本中，`for` 循环中隐式使用 `"@"` 特别有益，因为它会导致 `for` 循环将包含**空格**的参数视为单个参数。这包含了带引号的 `Marilou Smith`，这使得 shell 将其作为单个参数传递给脚本。`for` 语句中隐式的 `"@"` 导致 shell 重新生成带引号的参数 `Marilou Smith`，使其被视为单个参数。

`awk`：对于每个命令行文件，它从 `/etc/passwd` 的每行中提取第一个 (`$1`) 和第五个 (`$5`) 字段。`-F` 选项允许 `awk` 在读取 `/etc/passwd` 时使用冒号（:）作为字段分隔符，使其能够将每行拆分为多个字段。`awk` 命令设置并使用了 `$1` 和 `$5` 参数；它们包含在单问号内，且不会被 shell 解释。不要将这些参数与对应于命令行参数的位置参数混淆。第一个和第五个字段通过管道发送到 `grep` 页面。`grep` 工具在它的输入中搜索具有命令行参数值的 `Sid`。`-i` 选项允许 `grep` 在搜索时忽略大小写；`grep` 显示其输入中包含 `Sid` 的每一行。

一个有趣的语法异常，使得管道符号 `( | )` 出现在带有 `awk` 命令的行上：你不需要在管道符号后立即输入一个**换行符**（即管道符号是行的最后一个字符）就可以保持换行符并执行命令。尝试输入命令并按回车键。shell 会显示一个次级提示符。如果你接着输入 `sort` 然后按另一个回车，你将看到一个排序后的列表。即使管道符号后跟着一个换行符，管道仍然正常工作。

# while

`while` 控制结构具有以下语法：

```
while test-command
  do
    commands
  done
```

只要 `test-command`（图 27-5）返回真的退出状态，`while` 结构就会继续执行一系列的命令和 `done` 语句。在每次循环执行命令之前，该结构都会执行 `test-command`。当 `test-command` 的退出状态为假时，该结构将控制传递给 `done` 语句之后的语句。

以下 shell 脚本将数字变量初始化为零。然后 `test` 内置命令判断 `number` 是否小于 10。脚本使用 `-lt` 来执行数值测试。对于数值比较，你必须使用 `-ne`（不相等）、`-eq`（相等）、`-gt`（大于）、`-ge`（大于等于）、`-lt`（小于）或 `-le`（小于等于）。在处理 `test` 时进行字符串比较时，请使用 `=`（相等）或 `!=`（不相等）。在本示例中，只要 `number` 小于 10，`test` 的退出状态为 0（真）。只要 `test` 返回，该结构就会执行 `do` 和 `done` 语句之间的命令。

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_1021_0.png)

图 27-5 一个 while 流程图

关于 `test` 内置命令的详情，请参见第 955 页。
