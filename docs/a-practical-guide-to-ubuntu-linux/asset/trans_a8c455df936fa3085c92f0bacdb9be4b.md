

```bash
if [ $# -eq 1 ]; then
  directory=""
elif [ -d "$2" ]; then
  directory="$2"
else
  echo "Optional second argument must be a directory." 1>&2
  echo "Usage: lnks [directory]" 1>&2
  exit 1
fi

# Check that file exists and is an ordinary file
if [ ! -f "$file" ]; then
  echo "lnks: file not found or special file" 1>&2
  exit 1
fi

# Check link count on file
set -- $(ls -l "$file")
linkcnt=$2
```

```bash
if [ "$linkcnt" -eq 1 ]; then
  echo "lnks: no other hard links to $file" 1>&2
  exit 0
fi

# Get the inode of the given file
set $(ls -i "$file")
inode=$1

# Find and print the files with that inode number
echo "lnks: using find to search for links..." 1>&2
find "$directory" -xdev -inum $inode -print
```

Max 在他的主目录下有一个名为 letter 的文件。他想找到该文件在其他用户主目录树中的链接。在下面的例子中，Max 从主目录下调用 `lnks` 来执行搜索。`lnks` 的第二个参数 `/home` 是他想要开始搜索的目录路径。`lnks` 脚本报告 `/home/max/letter` 和 `/home/zach/draft` 是指向同一个文件的链接：

```bash
$ .lnks letter /home
lnks: using find to search for links...
/home/max/letter
/home/zach/draft
```

除了 `if...then...elif` 控制结构外，`lnks` 还引入了 shell 程序中常用的其他特性。接下来的讨论将逐节介绍 `lnks`。

### 指定 shell `lnks` 脚本的第一行使用 `#!`（第 302 页）来指定执行脚本的 shell：

```bash
#!/bin/bash
```

在本章中，`#!` 符号仅出现在更复杂的示例中。它确保了即使用户运行的是不同的 shell，或者脚本是从运行不同 shell 的脚本中被调用的，也会由正确的 shell 来执行脚本。

### 注释 `lnks` 的第二和第三行是注释；shell 会忽略哈希标记（#）之后到下一个换行符之前的文本。`lnks` 中的这些注释简要地说明了该文件的功能并解释了如何使用它：

```bash
# Identify links to a file
# Usage: lnks file [directory]
```

### 用法消息第一个 `if` 语句测试调用 `lnks` 时参数是否为空或多于两个：

```bash
if [ $# -eq 0 -o $# -gt 2 ]; then
  echo "Usage: lnks file [directory]" 1>&2
  exit 1
fi
```

如果其中任一条件为真，`lnks` 会向标准错误发送一条用法消息并以状态 1 退出。用法消息周围的双引号防止 shell 将方括号解释为特殊字符。用法消息中的括号表示目录参数是可选的。

第二个 `if` 语句测试命令行参数（`$1`）是否为目录（`-d` 参数测试，如果文件存在且是目录则返回真）：

```bash
if [ -d "$1" ]; then
  echo "First argument cannot be a directory." 1>&2
  echo "Usage: lnks file [directory]" 1>&2
else
  file="$1"
fi
```

如果第一个参数是目录，`lnks` 会显示用法消息。如果它不是目录，`lnks` 将 `$1` 的值保存在 `file` 变量中，因为在脚本后面会设置命令行参数。如果在执行 `set` 命令之前没有保存 `$1` 的值，则它的值将会丢失。

### 测试参数 `lnks` 的下一部分是一个 `if...then...elif` 语句：

```bash
if [ $# -eq 1 ]; then
  directory=""
elif [ -d "$2" ]; then
  directory="$2"
else
  echo "Optional second argument must be a directory." 1>&2
  echo "Usage: lnks file [directory]" 1>&2
  exit 1
fi
```

## 控制结构 965

第一个测试命令确定用户是否在命令行上指定了单个参数。如果测试命令返回 0（真），则 `directory` 变量被赋值为工作目录的值（`.`）。如果测试命令返回假，`elif` 语句测试该参数是否为目录。如果是目录，则 `directory` 变量设置为第二个命令行参数 `$2`。如果 `$2` 不是目录，`lnks` 会向标准错误发送一条用法消息并以状态 1 退出。

`lnks` 中的下一个 `if` 语句测试 `$file` 是否存在。这可以防止 `lnks` 浪费时间去寻找不存在的文件的链接。通过带有 `!`、`-f` 和 `$file` 三个参数的内置命令 `test` 在 `$file` 不存在时结果为真：

```bash
[ ! -f "$file" ]
```

测试 `-f` 参数前的运算符反转其结果，如果 `$file` 存在且是一个普通文件，则结果为假。接下来 `lnks` 使用 `ls -l` 来检查 `$file` 拥有的链接数量：

```bash
# Check link count on file
set -- $(ls -l "$file")
linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
  echo "lnks: no other hard links to $file" 2>&2
  exit 0
fi
```

使用 `set` 内置替换（第 362 页）将位置参数设置为 `ls -l` 的输出。该输出的第二个字段是链接计数，因此用户创建的变量 `linkcnt` 被设置为 `$2`。在 `set` 中使用的 `--` 可以防止其将文件产生的第一个参数（通常以 `-` 开头）解释为选项。`if` 语句检查 `linkcnt` 是否等于 1；如果是的话，`lnks` 会显示一条消息并退出。虽然这条消息不是真正的错误消息，但根据 `lnks` 的编写方式，所有信息性消息都被发送到了标准错误。`lnks` 的最终产物——指向指定文件的链接文件名——被发送到标准输出，因此你可以随心愿地重定向输出。

如果链接计数大于 1，`lnks` 将识别 `$file` 的 inode（第 1153 页）。正如第 229 页解释，将 inode 与文件名进行比较是判断文件名是否指向同一个文件链接的好方法。`lnks` 脚本使用 `set` 将位置参数设置为 `ls -i` 的输出。`set` 的第一个参数是文件的 inode 号，因此用户创建的变量 `inode` 被赋予该值。

```bash
# Get the inode of the given file
set $(ls -i "$file")
inode=$1
```

### Find and print the files with that inode number

echo "lnks: using find to search for links..." 1>&2
find "$directory" -xdev -inum $inode -print
```

最后，`find` 工具在其第一个参数指定的根目录中搜索符合剩余参数标准的文件。在本例中，剩余参数是匹配 inode。`-xdev`（跨设备）参数防止 `find` 搜索其他文件系统。有关文件系统的更多信息请参阅第 226 页。

`lnks` 中命令之前的 `echo` 命令告诉用户正在运行 find，因为 find 运行可能需要时间。由于 `lnks` 不包含最终的 `exit` 语句，它的退出状态是最后一个执行的命令的状态。

## 调试 shell 脚本

当你编写像 `lnks` 这样的脚本时很容易出错。你可以使用 shell 的 `-x` 选项来调试脚本。该选项会导致 shell 在执行每个命令之前显示该命令。以这种方式跟踪脚本的执行可以让你获得问题所在的信息。

你可以像上一个例子一样运行 `lnks` 并让 shell 在执行每个命令之前显示。为当前 shell 设置 `-x` 选项（`set -x`）可以让所有脚本都显示命令，或者使用 `-x` 选项仅影响由命令行调用的脚本 shell。

```bash
$ bash -x lnks letter /home
+ [ $# -eq 0 -o $# -gt 2 ]
+ [ -d letter ]
+ file=letter
+ [ $# -eq 1 ]
+ [ -d /home ]
+ directory=/home
+ [ ! -f letter ]
```

PS4 脚本执行的每个命令之前都有 `PS4` 变量的值——默认为 (+)，因此你可以区分调试输出和脚本产生的输出。如果你在调用脚本的 shell 中设置了 `PS4`，则必须将其导出。如果你在调用脚本的 shell 中设置了 PS4，则必须将其导出。接下来的命令将 `PS4` 发送为 `>>>` 后加一个空格并将其导出：

```bash
$ export PS4='>>> '
```

