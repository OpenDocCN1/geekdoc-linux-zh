
```text
$ if3
word 1: apple
word 2: orange
word 3: pear
No match

$ if3
word 1: apple
word 2: orange
word 3: apple
Match: words 1 & 3

$ if3
word 1: apple
word 2: apple
word 3: apple
Match: words 1, 2, & 3
```

如果三个单词不相同，结构将控制权传递给第一个 `elif`，它开始一系列测试，以查看是否有任何一对单词相同。随着嵌套的继续，如果任何一个 `if` 语句得到满足，结构将控制权传递给下一个 `then` 语句，随后传递给 `fi` 语句之后的语句。每当一个 `elif` 语句没有得到满足时，结构将控制权传递给下一个 `elif` 语句。包含 `&` 符号的 `echo` 参数周围的双引号防止 shell 将 `&` 解释为特殊字符。

## `lnks` 脚本

下面这个名为 `lnks` 的脚本演示了 `if...then` 和 `if...then...elif` 控制结构。这个脚本查找指向其第一个参数（文件名）的硬链接。如果你提供目录名称作为第二个参数，`lnks` 将在该目录及其所有子目录中搜索链接。如果你没有指定目录，`lnks` 将搜索工作目录及其子目录。此脚本不会查找符号链接。

```bash
$ cat lnks
#!/bin/bash
# Identify links to a file
# Usage: lnks file [directory]

if [ $# -eq 0 -o $# -gt 2 ]; then
  echo "Usage: lnks file [directory]" 1>&2
  exit 1
fi
if [ -d "$1" ]; then
  echo "First argument cannot be a directory." 1>&2
  echo "Usage: lnks file [directory]" 1>&2
  exit 1
else
  file=$1
fi

if [ $# -eq 1 ]; then
  directory="."
elif [ -d "$2" ]; then
  directory="$2"
else
  echo "Optional second argument must be a directory." 1>&2
  echo "Usage: lnks file [directory]" 1>&2
  exit 1
fi
# Check that file exists and is an ordinary file:
if [ ! -f "$file" ]; then
  echo "lnks: $file not found or special file" 1>&2
  exit 1
fi
# Check link count on file
set -- $(ls -l "$file")
linkcnt=$2
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

Alex 在他的主目录中有一个名为 `letter` 的文件。他想查找该文件在他和其他用户的主目录文件树中的链接。在以下示例中，Alex 从他的主目录调用 `lnks` 来执行搜索。`lnks` 的第二个参数 `/home` 是他希望开始搜索的目录的路径名。`lnks` 脚本报告 `/home/alex/letter` 和 `/home/jenny/draft` 是同一个文件的链接：

```text
$ lnks letter /home
lnks: using find to search for links...
/home/alex/letter
/home/jenny/draft
```

除了 `if...then...elif` 控制结构外，`lnks` 还引入了 shell 程序中常用的其他特性。以下讨论将分节描述 `lnks`。

### 指定 shell

`lnks` 脚本的第一行使用 `#!`（第 288 页）来指定将执行该脚本的 shell：

```bash
#!/bin/bash
```

在本章中，`#!` 表示法仅出现在更复杂的示例中。它确保正确的 shell 执行脚本，即使用户正在运行不同的 shell 或脚本是从另一个 shell 脚本调用的。

### 注释

`lnks` 的第二行和第三行是注释；shell 会忽略井号后的文本，直到下一个 `NEWLINE` 字符为止。这些 `lnks` 中的注释简要说明了文件的作用以及如何使用它：

```bash
# Identify links to a file
# Usage: lnks file [directory]
```

### 用法消息

第一个 `if` 语句测试 `lnks` 是否以零个参数或超过两个参数调用：

```bash
if [ $# -eq 0 -o $# -gt 2 ]; then
    echo "Usage: lnks file [directory]" 1>&2
    exit 1
fi
```

如果这些条件中任何一个为 *true*，`lnks` 将向标准错误发送用法消息，并以状态 1 退出。用法消息周围的双引号防止 shell 将方括号解释为特殊字符。用法消息中的方括号表示 `directory` 参数是可选的。

第二个 `if` 语句测试第一个命令行参数 (`$1`) 是否是一个目录（`test` 的 `-d` 参数在文件存在且为目录时返回 *true* 值）：

```bash
if [ -d "$1" ]; then
    echo "First argument cannot be a directory." 1>&2
    echo "Usage: lnks file [directory]" 1>&2
    exit 1
else
    file=$1
fi
```

如果第一个参数是目录，`lnks` 显示用法消息并退出。如果它不是目录，`lnks` 将 `$1` 的值保存在 `file` 变量中，因为脚本后面 `set` 会重置命令行参数。如果在发出 `set` 命令之前未保存 `$1` 的值，该值将会丢失。

### 测试参数

`lnks` 的下一部分是 *if ... then ... elif* 语句：

```bash
if [ $# -eq 1 ]; then
    directory="."
elif [ -d "$2" ]; then
    directory="$2"
else
    echo "Optional second argument must be a directory." 1>&2
    echo "Usage: lnks file [directory]" 1>&2
    exit 1
fi
```

`test-command` 确定用户是否在命令行中指定了单个参数。如果 *test-command* 返回 *0 (true)*，用户创建的名为 `directory` 的变量被赋值为工作目录 (*.*). 如果 *test-command* 返回 *false*，*elif* 语句测试第二个参数是否为目录。如果是目录，`directory` 变量被设置为第二个命令行参数 `$2`。如果 `$2` 不是目录，`lnks` 向标准错误发送用法消息并以状态 1 退出。

`lnks` 中的下一个 `if` 语句测试 `$file` 是否不存在。这个测试使 `lnks` 不会浪费时间查找指向不存在文件的链接。

带有 `!`, `-f`, 和 `$file` 三个参数的 `test` 内置命令在文件 `$file` 不*存在* 时求值为 *true*：

```bash
[ ! -f "$file" ]
```

跟在 `test` 的 `-f` 参数前的 `!` 运算符否定了其结果，如果文件 `$file` *存在* 且是普通文件，则得出 *false*。

接下来 `lnks` 使用 `set` 和 `ls -l` 来检查 `$file` 的链接数：

```bash
# Check link count on file
set -- $(ls -l "$file")
linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
  echo "lnks: no other hard links to $file" 1>&2
  exit 0
fi
```
