
## 巴克斯-诺尔范式

巴克斯-诺尔范式是表示语句正确顺序和用法的标准。它最早由 John Backus 在 1959 年引入，后来由 Peter Naur 简化，因此有了现在的名称。John Backus 于 2007 年去世。请为 John 学习接下去的用例语句。

当发生错误时，脚本将执行 `usage` 函数并显示以下消息：

```
USAGE: mk_passwd.ksh [-m] [-n] [password_length]

Where:

    -m      Creates a password printout for Security

    -n      Loads the default keyboard data keys file

    password_length  Integer value that overrides
                         the default 8 character
                         password length.\n"
```

## 第二部分 - 程序员、测试人员和分析师的脚本

### `trap_exit` 描述

此函数 `trap_exit` 仅在捕获到退出信号时执行。你稍后将看到如何设置陷阱（`trap`）。此函数的作用是执行函数列表中列出的任何命令。在我们需要中，我们需要在退出壳脚本之前删除 `$OUTFILE`。此外，如果文件不存在，我们不希望向 `stderr` 发送任何消息。该语句如下所示：

```bash
function trap_exit
{
  rm -f $OUTFILE >/dev/null 2>&1
}
```

注意，我们将 `stderr` 输出重定向到 `stdout`（通过文件描述符 `2>&1` 指定），但在我们将所有内容发送到由 `>/dev/null` 指定的空桶之前。

接下来的章节将涵盖命令行参数所需的测试和解析。

## 测试和解析命令行参数

由于此壳脚本有控制执行的命令行选项，我们需要测试每个命令行参数的有效性，然后解析每个参数，以设置脚本的执行方式。我们需要执行四个测试来验证每个参数。

### 验证命令行参数的数量

第一步是确保命令行参数的数量在我们预期的参数限制范围内。对于此脚本，我们预期不少于三个参数。为了测试参数数量，我们使用 `$#` 壳变量来测试参数数量是否大于 3。此测试代码所示：

```bash
# Check command line arguments - $# > 3
if (( $# > 3 ));
then
  usage
  exit 1
fi
```

注意，我们使用了由双括号 `(( expression ))` 表示的数学测试。关于此测试语法的一个需要注意的点是，对于用户定义或脚本定义的变量，不需要在变量名前使用美元符号 (`$`)。对于壳变量，你在这里也必须使用壳的表示法。如果命令行上的参数数量超过 3，我们将显示 `usage` 函数并以返回代码 1 退出壳脚本。

### 有效命令行参数测试

我们实际上只有三个有效的命令行参数。因为 `-n` 和 `-m` 是小写字母，我们大可以为喜欢输入大写字母的人添加它们的大写对应项。现在我们只有五个有效的命令行参数：

- 整数
- `-n` 和 `-N` 表示创建一个新的 `$KEYBOARD_FILE`
- `-m` 和 `-M` 表示要打印管理器的密码报告

看起来使用 `case` 语句通过 `$0` 解析命令行参数来测试似乎是轻而易举的，其中 `$0` 是一个用单空格分隔的命令行参数列表。详细信息请看列表 12-7 中的代码块。

```bash
# Test for valid command line arguments
# Valid arguments are -n, -N, -m, -M, and any integer
if (( $# != 0 ))
then
    for CMD_ARG in $0
    do
        case $CMD_ARG in
            *([-0-9]))
                # The '+([-0-9])' test notation is looking for
                # an integer. Any integer is assigned to the
                # length of password variable, LENGTH
                LENGTH=$CMD_ARG
                ;;
            -n|-N)
                # The colon (:) is a no-op, which does nothing
                ;;
            -m|-M)
                # The colon (:) is a no-op, which does nothing
                ;;
            *)
                # Invalid argument
                ;;
        esac
done
```

列表 12-7 用于有效命令行参数的测试

## 第二部分 针对程序员、测试员和分析师的脚本

```bash
echo "\nPress ENTER when you are ready to continue: \c"
read REPLY
clear
;;

# 打印经理密码报告
PRINT_PASSWORD_MANAGER_REPORT=TRUE
;;

?\) # 显示用法
usage
exit 1
esac
done
```

列表 12-10（续）

在位于 `while` 循环所在行的 `getopts` 语句中，我们提供了四个命令行选项。这些选项包括用于执行 `load_default_keyboard` 函数的 `-n` 和 `-N` 选项。对于 `-m` 和 `-M` 选项，打印机变量设置为 `TRUE`。任何其他结果将导致脚本以返回代码 1 退出。请注意 `case` 语句中的 `\?`。这指定任何无效选项都将被赋值为问号（`?`）。我们没有在任何选项后加冒号，因此我们不期望为任何参数分配任何值。

## 主程序开始

现在我们已经定义了所有的变量并验证了所有的命令行参数，准备好开始 `mk_passwd.ksh` 脚本的主部分了。

### 设置陷阱

要做的第一件事是设置陷阱。如果捕获并定义了退出信号，陷阱允许我们在脚本或函数退出之前采取行动。我们永远无法捕获 `kill -9` 退出。这个 `kill` 选项不会执行任何优雅的退出；它只是将进程从系统进程表中移除，该进程不再存在。常见的退出信号有 1、2、3 和 15。有关退出信号的完整列表，请参阅第 1 章“脚本快速上手与回顾”，或在命令行上输入 `kill -l`（注意是小写的 L）。

我们的陷阱显示在此：

```bash
trap 'trap_exit; exit 2' 1 2 3 15
```

当检测到被捕获的退出信号时（在这种情况下为信号 1、2、3 或 15），陷阱会执行包含在单引号内的两个命令（`'commands'`）。这些命令包括运行 `trap_exit` 函数以删除 `$OUTFILE` 文件；然后脚本以返回代码 2 退出，该代码已定义为此 shell 脚本的陷阱退出。

### 检查键盘文件

如果没有键盘数据文件，此脚本将毫无用且无法执行任何操作。为了检查 `$KEYBOARD_FILE` 是否存在，我们执行 `check_for_and_create_keyboard_file` 函数。正如我们之前看到的，该函数会检查系统中是否存在键盘文件。如果没有找到文件，将提示用户自动加载默认键盘布局，即一个标准的 109 键 QWERTY 键盘。此功能允许新用户快速启动，并在文件被删除时能够轻松恢复。当我们想要加载自定义键盘布局时，只需要将默认键盘文件替换为新的键盘文件即可。

### 加载 KEYS 数组

一旦我们有了 `$KEYBOARD_FILE`，我们就准备好将键盘字符加载到 `KEYS` 数组中。这段脚本通过文件数据加载 `KEYS` 数组。实现此最简单的方法是使用 `while` 循环读取文件的每一行（在这种情况下是单个字符），从文件底部输入循环，如列表 12-1 所示。

```bash
X=0 # 初始化数组计数器为零
# 加载名为 'KEYS' 的数组，
# 包含 $KEYBOARD_FILE 中的键盘元素。
while read ARRAY_ELEMENT
do
    ((X = X + 1)) # 计数器加1
    # 加载数组中的一个元素
    KEYS[$X]=$ARRAY_ELEMENT
done < $KEYBOARD_FILE
```
