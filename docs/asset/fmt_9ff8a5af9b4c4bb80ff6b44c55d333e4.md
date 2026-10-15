
如果这些条件为真，`lnks` 会向标准错误发送一条消息并以状态 `1` 退出。括号周围的双引号防止了 shell 将括号解释为特殊字符。用法消息中的括号向用户指示目录参数是可选的。

第二个语句测试 `$1` 是否为目录（`-d` 参数），如果文件存在且是一个目录，则该测试返回真：

```bash
if [ -d "$1" ]; then
  echo "First argument cannot be a directory." 1>&2
  echo "Usage: lnks file [directory]" 1>&2
  exit 1
else
  file="$1"
```
如果是目录，`lnks` 将显示用法信息并退出。如果不是目录，`lnks` 将将 `$1` 的值保存到脚本稍后部分的 `file` 变量中，随后该部分会设置命令行参数。如果在执行命令之前没有保存 `$1` 的值，则其值将丢失。

`lnks` 的下一部分是 `if...then...elif` 语句：

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

第一个测试命令确定用户是否在命令行上指定了单个参数。如果测试命令返回 `0`（真），则用户创建的变量 `directory` 被赋值为工作目录（`.`）。如果测试命令返回假值，则 `elif` 语句测试第二个参数是否为目录。如果是目录，则 `directory` 变量将被设置为第二个命令行参数 `$2`。如果 `$2` 不是目录，`lnks` 会向标准错误发送一条消息并以状态 `1` 退出。

`Inks` 中的下一个 `if` 语句检查 `$file` 是否存在。这是一个重要的查询，因为让 `Inks` 花费时间寻找一个不存在的文件的链接是没有意义的。

带有三个参数 `!`、`-f` 和 `$file` 的内置命令 `test` 在文件 `$file` 不存在时结果为真：

```bash
[ -f "$file" ]
```

测试参数 `-f` 之前的 `!` 运算符对其结果取反，如果文件 `$file` 存在且是一个普通文件，则结果为假。

接下来，`Inks` 使用 `set` 和 `-l` 来检查 `$file` 有多少个链接：

```bash
# 检查文件的链接数
set -- $(ls -l "$file")
linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
  echo "Inks: no other links to $file" 1>&2
  exit 0
fi
```

内置命令 `test` 使用命令替换（第 575 页）将位置参数设置为 `-l` 的输出。在 `ls -l` 的输出中，第二个字段是链接数，用户创建的变量 `linkcnt` 等于 `$2`。与 `set` 配合 `--` 防止了 `set` 将第一个参数解释为选项（`-` 产生的第一个参数是文件的访问权限，且可能以 `-` 开头）。`if` 语句检查 `linkcnt` 是否等于 `1`；如果是，则向标准错误发送消息。如果 `linkcnt` 等于 `1`，`Inks` 会向标准错误发送一条消息并以状态 `0` 退出。

```bash
# 检查文件是否存在并为普通文件：
if [ -e "file" ]; then
  echo "Inks: file not found or special file" 1>&2
  exit 1
fi
```

```bash
# 检查文件的链接数
set -- $(ls -l "file")
```

```bash
linkcnt=$2
if [ "$linkcnt" -eq 1 ]; then
  echo "Inks: no other links to "file" 1>&2
  exit 0
fi
```

```bash
# 查找给定文件的 inode 
set $(ls -i "file")
```

`inode=$1`

```bash
# 查找并打印具有该 inode 的文件
echo "Inks: using find to search for links..." 1>&2
find "directory" -xdev -inum "$inode" -print
```

在接下来的示例中，Alex 在其主目录下使用 `Inks` 搜索工作目录中名为 `letter` 的文件。`Inks` 脚本报告 `/home/alex/letter` 和 `/home/jenny/draft` 是指向同一个文件的链接：

```bash
# Inks letter /home
Inks: using find to search for links...
```
