
以下示例展示了一个 `if...then...elif` 控制结构。该 shell 脚本比较用户输入的三个单词。第一个 `if` 语句使用布尔 AND 运算符（`-a`）作为 `test` 的参数。如果第一个和第二个逻辑比较均为 `true`（即 `word1` 与 `word2` 匹配，且 `word2` 与 `word3` 匹配），`test` 内建命令将返回 `true` 状态。如果 `test` 返回 `true` 状态，脚本将执行紧随其后的 `then` 语句的命令，将控制权传递给 `fi` 之后的语句，并终止。

```bash
$ cat if3
  read -p "word 1: " word1
  read -p "word 2: " word2
  read -p "word 3: " word3
  if [ "$word1" = "$word2" -a "$word2" = "$word3" ]
  then
    echo "Match: words 1, 2, & 3"
  elif [ "$word1" = "$word2" ]
  then
    echo "Match: words 1 & 2"
  elif [ "$word2" = "$word3" ]
  then
    echo "Match: words 2 & 3"
  elif [ "$word2" = "$word1" ]
  then
    echo "Match: words 2 & 3"
  else
    echo "No match"
  fi

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
Match: words 1, 2, & 3
```

如果这三个单词不完全相同，该结构将控制权传递给第一个 `elif`，从而开始一系列测试，以检查是否有任何一对单词相同。随着嵌套的继续，如果任何一个 `elif` 语句得到满足，结构将控制权传递给下一个 `then` 语句，随后传递给 `fi` 之后的语句。每当一个 `elif` 语句未得到满足时，结构将控制权传递给下一个 `elif` 语句。围绕包含 `echo` 参数且带有 `&`（与号）的双引号可防止 shell 将 `&` 解释为特殊字符。

## 可选的 `lnks` 脚本

以下名为 `lnks` 的脚本演示了 `if...then` 和 `if...then...elif` 控制结构。该脚本查找指向其第一个参数（文件名）的硬链接。如果提供目录名称作为第二个参数，`lnks` 将在以该目录为根目录的目录层次结构中搜索链接。如果不指定目录，`lnks` 将搜索工作目录及其子目录。此脚本不会定位符号链接。

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
    file="$1"
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

# Check that file exists and is an ordinary file
if [ ! -f "$file" ]; then
    echo "lnks: $file not found or is a special file" 1>&2
    exit 1
fi
# Check link count on file
set -- $(ls -l "$file")

linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
    echo 'lnks: no other hard links to $file' 1>&2
    exit 0
fi

# Get the inode of the given file
set $(ls -i "$file")

inode=$1

# Find and print the files with that inode number
echo 'lnks: using find to search for links...'
find "$directory" -xdev -inum $inode -print
```

Max 在他的主目录中有一个名为 `letter` 的文件。他想在 Max 和其他用户的主目录文件层次结构中查找该文件的链接。在以下示例中，Max 从他的主目录调用 `lnks` 来执行搜索。`lnks` 的第二个参数 `/home` 是 Max 想要开始搜索的目录的路径名。`lnks` 脚本报告 `/home/max/letter` 和 `/home/zach/draft` 是指向同一文件的链接：

```bash
$ ./lnks letter /home
lnks: using find to search for links...
/home/max/letter
/home/zach/draft
```

除了 `if...then...elif` 控制结构外，`lnks` 还介绍了 shell 程序中常用的其他功能。以下讨论逐段描述 `lnks`。

### 指定 shell

`lnks` 脚本的第一行使用 `#!`（第 338 页）来指定执行该脚本的 shell：

```bash
#!/bin/bash
```

在本章中，`#!` 表示法仅出现在更复杂的示例中。它确保正确的 shell 执行该脚本，即使用户正在运行不同的 shell，或者该脚本是从运行不同 shell 的脚本中调用的。

### 注释

`lnks` 的第二行和第三行是注释；shell 会忽略 `#` 号之后的文本，直到下一个换行符。`lnks` 中的这些注释简要说明了该文件的作用以及如何使用它：

```bash
# Identify links to a file
# Usage: lnks file [directory]
```

### 用法消息

第一个 `if` 语句测试 `lnks` 是否被调用时带有零个参数或超过两个参数：

```bash
if [ $# -eq 0 -o $# -gt 2 ]; then
    echo "Usage: lnks file [directory]" 1>&2
    exit 1
fi
```

如果这些条件中任一个为 `true`，`lnks` 会将用法消息发送到标准错误，并以状态 1 退出。围绕用法消息的双引号可防止 shell 将括号解释为特殊字符。用法消息中的括号表示目录参数是可选的。

第二个 `if` 语句测试第一个命令行参数（`$1`）是否为目录（如果文件存在且是目录，`test` 的 `-d` 参数将返回 `true`）：

```bash
if [ -d "$1" ]; then
    echo "First argument cannot be a directory." 1>&2
    echo "Usage: lnks file [directory]" 1>&2
    exit 1
else
    file="$1"
fi
```

如果第一个参数是目录，`lnks` 将显示用法消息并退出。如果它不是目录，`lnks` 会将 `$1` 的值保存在 `file` 变量中，因为在脚本后面 `set` 会重置命令行参数。如果在发出 `set` 命令之前未保存 `$1` 的值，其值将会丢失。

`lnks` 的下一部分是一个 `if...then...else` 语句：

```bash
if [ $# -eq 1 ]; then
    directory="."
elif [ -d "$2" ]; then
    directory="$2"
else
    echo "Optional second argument must be a directory."
    echo "Usage: lnks file [directory]" 1>&2
    exit 1
fi
```

第一个 *test-command* 确定用户是否在命令行上指定了单个参数。如果 *test-command* 返回 0（*true*），则 `directory` 变量被赋值为工作目录（`.`）的值。如果 *test-command* 返回非零值（*false*），`elif` 语句测试第二个参数是否为目录。如果是目录，`directory` 变量被设置为等于第二个命令行参数 `$2`。如果 `$2` 不是目录，`lnks` 将用法消息发送到标准错误，并以状态 1 退出。

`lnks` 中的下一个 `if` 语句测试 `$file` 是否存在。此测试可防止 `lnks` 浪费时间查找指向不存在文件的链接。当 `test` 内建命令使用 `!`、`-f` 和 `$file` 这三个参数调用时，如果文件 `$file` 不存在，其评估结果为 *true*：

```bash
[ ! -f "$file" ]
```

`test` 的 `-f` 参数前面的 `!` 运算符会否定其结果，如果文件 `$file` *存在* 并且是普通文件，则产生 *false*。

接下来 `lnks` 使用 `set` 和 `ls -l` 来检查 `$file` 的链接数量：

```bash
# Check link count on file
set -- $(ls -l "$file")

linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
    echo "lnks: no other hard links to $file" 1>&2
    exit 0
fi
```

`set` 内建命令使用命令替换（第 410 页）将位置参数设置为 `ls -l` 的输出。此输出的第二个字段是链接计数，因此用户创建的变量 `linkcnt` 被设置为等于 `$2`。与 `set` 一起使用的 `--` 可防止 `set` 将选项解释为 `ls -l` 生成的第一个参数（*第一个* 参数是文件的访问权限，通常以 `-` 开头）。`if` 语句检查 `$linkcnt` 是否等于 1；如果是，`lnks` 将显示一条消息并退出。虽然这条消息并非真正的错误消息，但它被重定向到标准错误。以 `lnks` 编写的方式，所有信息消息都发送到标准错误。只有 `lnks` 的最终产物，即指向指定文件的链接的路径名，会被发送到标准输出，因此您可以重定向输出。

