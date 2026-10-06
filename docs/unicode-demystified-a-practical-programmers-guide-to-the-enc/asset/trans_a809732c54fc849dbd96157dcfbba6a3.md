

```bash
function mycp
{
  case $# in
    0)    exec 3<&4 &&1 ;;
    1)    exec 3<$ $1 &&4 ;;
    2)    exec 3<$ $4 >$2 ;;
    *)   print "Usage: mycp [source] [dest]"
        exit 1;
  esac
}
```

该函数的实际工作是在以 `cat` 开头的行完成的。脚本的其他部分安排了文件描述符 3 和 4（它们是 cat 命令的输入和输出）与正确的文件关联。

下一个程序接受命令行上的两个文件名并将它们都排序到临时文件中。程序将排序后的文件合并到标准输出，并在每个文件前加上一个指示其来源哪个文件的数字。

Z Shell 没有用于“小于等于”或“大于等于”的字符串比较运算符。你不能像这个示例那样使用大于（例如在 if 语句中使用 `[[ "$Line1" > "$Line2" ]]`）作为小于等于的等价物：

```zsh
zsh % cat sortmerge
#!/bin/zsh
usage()
{
if [[ $# -ne 2 ]];
then
print -u2 "Usage: $0 file1 file2"
exit 1
fi
# 默认临时目录
: ${TMPDIR:=/tmp}
# 检查参数数量
usage "$@"
# 设置排序的临时文件
file1=$TMPDIR/file1.$
file2=$TMPDIR/file2.$
# 排序
sort $1 > $file1
sort $2 > $file2
# 读取文件 $file1 和 $file2。使用 FD 3 和 4。
exec 3<$file1
exec 4<$file2
# 读取每个文件的第一行以确定如何开始
read -u3 Line1
Status1=$?
read -u4 Line2
Status2=$?
```

# 第 15 章 Z Shell 与高级 Shell 编程

```zsh
# 策略：当两个文件中都有剩余输入时：
# 输出较小的行。
# 从该行来源的文件读取新行。
while [[ $Status1 -eq 0 && $Status2 -eq 0 ]]
do
  if [[ "$Line1" > "$Line2" ]];
    then
      print "1.\t$Line1"
      read -u3 Line1
      Status1=$?
  else
    print "2.\t$Line2"
    read -u4 Line2
    Status2=$?
  fi
done
# 现在其中一个文件已到达末尾。
# 从每个文件读取到结束。
# 第文件：
while [[ $Status1 -eq 0 ]]
do
  print "1.\t$Line1"
  read -u3 Line1
  Status1=$?
done
# 下一个文件2：
while [[ $Status2 -eq 0 ]]
do
  print "2.\t$Line2"
  read -u4 Line2
  Status2=$?
done
# 关闭并删除两个输入文件
rm -f $file1 $file2
exit 0
```

# 函数

Shell 函数的语法有两种格式（zsh 接受这两种格式，bash 仅接受第一种）：

```bash
func_name()
{
  commands
}
```

或者

```bash
function func_name
{
  commands()
}
```

第一个大括号（{）可以与函数名出现在同一行。如果函数定义中包含了别名的名称，它们会在函数被读取时（执行时）被展开。你可以在函数内部使用内置命令 `break` 来终止其执行。内置命令 `functions` 列出所有已定义的函数。

Shell 函数也可以作为定义特殊命令的简写。以下函数在后台启动一个命名的进程，其输出通常由保存到 `.process.out` 的进程显示：

```bash
start_process() {
  process > .process.out 2>&1 &
}
```

zsh 中没有 `setenv` 内置命令。以下函数模拟了该命令的行为（该命令在 bash 中可用）：

```zsh
zsh % setenv() {
if [ $ -eq 2 ]; then
  export $1=$2
else
  echo "Usage: setenv NAME VALUE" >&2
fi
```

如果有两个参数，`setenv` 函数将第二个参数的值赋值给第一个参数并导出第一个参数。Shell 内置命令与 bash 的相同（见第 571 页）。如果没有两个参数，函数将显示用法信息。内置命令 `unset` 用于删除函数定义：

```bash
unset func_name
```

Shell 将函数存储在内存中，因此它们的运行比 Shell 脚本更高效。如果你定义了过多的函数，在运行脚本时 Shell 的开销将变得无法接受。你也可以将函数存储在文件中，以便它们在第一次被调用时加载到内存中。内置命令 `autoload` 通知 zsh 函数函数存储在文件中。当执行 `autoload` 时（通常在启动新 shell 时），shell 不会将函数加载到内存，而是跟踪其名称（将其声明为未定义）。当脚本调用 `autoload` 时，zsh 会在 `FPATH` 列出的目录中搜索同名文件（`autoload` 的语法与 `PATH` 相同，见第 577 页）。你有责任确保函数定义和文件存储具有相同的名称。通常你有一个包含许多小文件的目录，当你处理多个使用不同函数的项目时，这种方式非常有用。

| 特殊函数 | 描述 |
| :--- | :--- |
| chpwd | 在切换目录时运行。以下示例显示了：
```zsh
zsh % chpwd() {
if [[ "$PWD" != "$OLDPWD" ]]; then
  echo "Changed directory to $PWD"
}
``` |
| periodic | 在显示提示符前运行。以下示例：
```zsh
zsh % periodic() {
  echo "Prompt updated"
}
``` |
| TRAP | 当接收信号时运行。以下示例：
```zsh
zsh % TRAP()
trap 'echo "Caught signal $1"' EXIT
``` |
| TRAPERR | 当命令返回非零状态时运行。以下示例：
```zsh
zsh % TRAPERR
trap 'echo "Error occurred"' ERR
``` |
| TRAPDEBUG | 在调试时运行。以下示例：
```zsh
zsh % TRAPDEBUG
trap 'echo "Debugging..."' DEBUG
``` |
| TRAPEXIT | 在退出时运行。以下示例：
```zsh
zsh % TRAPEXIT
trap 'echo "Exiting"' EXIT
``` |

# 内置命令

Z Shell 有许多内置命令（见第 161 页）。

### 别名：命令的快捷方式

`alias` 别名用于定义特殊命令。以下函数在后台启动一个命名的进程，其输出通常由保存到 `.process.out` 的进程显示：

```bash
start_process() {
  process > .process.out 2>&1 &
}
```

zsh 中没有 `setenv` 内置命令。以下函数模拟了该命令的行为（该命令在 bash 中可用）：

```zsh
zsh % setenv() {
if [ $ -eq 2 ]; then
  export $1=$2
else
  echo "Usage: setenv NAME VALUE" >&2
fi
```

如果有两个参数，`setenv` 函数将第二个参数的值赋值给第一个参数并导出第一个参数。Shell 内置命令与 bash 的相同（见第 571 页）。如果没有两个参数，函数将显示用法信息。内置命令 `unset` 用于删除函数定义：

```bash
unset func_name
```

Shell 将函数存储在内存中，因此它们的运行比 Shell 脚本更高效。如果你定义了过多的函数，在运行脚本时 Shell 的开销将变得无法接受。你也可以将函数存储在文件中，以便它们在第一次被调用时加载到内存中。内置命令 `autoload` 通知 zsh 函数存储在文件中。当执行 `autoload` 时（通常在启动新 shell 时），shell 不会将函数加载到内存，而是跟踪其名称（将其声明为未定义）。当脚本调用 `autoload` 时，zsh 会在 `FPATH` 列出的目录中搜索同名文件（`autoload` 的语法与 `PATH` 相同，见第 577 页）。你有责任确保函数定义和文件存储具有相同的名称。通常你有一个包含许多小文件的目录，当你处理多个使用不同函数的项目时，这种方式非常有用。

# 别名：命令的快捷方式

`alias` 别名用于定义特殊命令。以下函数在后台启动一个命名的进程，其输出通常由保存到 `.process.out` 的进程显示：

`alias` 别名用于定义特殊命令。

`alias` 不带参数显示所有别名：

```zsh
alias ls='ls -G'
```

以下示例创建并使用全局别名：

```zsh
alias ll='ls -la'
```

要删除别名，使用 `unset` 配合别名名称。以下示例删除别名：

```zsh
unset ll
```

有关更多信息请参阅第 801 页的“别名替换”。

# kill：终止进程

`kill` 内置命令向进程或作业发送信号，其语法与 bash 相同。如果不指定信号，`kill` 发送 `TERM`（软件终止，15）信号。有关信号名称和数字的更多信息，请参见第 667 页的表 13-5。在以下格式中，`n` 是信号数字，`PID` 是接收信号的进程标识：

```
kill -n PID
```

Shell 还支持命名信号。向作业发送信号时，可以使用名称：

```zsh
zsh % kill -TERM %1
```

此命令向作业 1 发送 TERM 信号。因为 `TERM` 是 `kill` 的默认信号，你也可以使用 `kill %1`。使用 `-l` 参数列出所有信号：

```bash
kill -l
```

# kill：终止进程

`kill` 内置命令向进程或作业发送信号，其语法与 bash 相同。如果不指定信号，`kill` 发送 `TERM`（软件终止，15）信号。有关信号名称和数字的更多信息，请参见第 667 页的表 13-5。在以下格式中，`n` 是信号数字，`PID` 是接收信号的进程标识：

```
kill -n PID
```

Shell 还支持命名信号。向作业发送信号时，可以使用名称：

```zsh
zsh % kill -TERM %1
```

此命令向作业 1 发送 TERM 信号。因为 `TERM` 是 `kill` 的默认信号，你也可以使用 `kill %1`。使用 `-l` 参数列出所有信号：

```bash
kill -l
```

# 作业控制

zsh 下的作业控制与 bash（第 554 页）和 tesh（第 690 页）非常相似。Shell 在显示多进程后台作业的所有 PID 编号方面遵循 tesh。

