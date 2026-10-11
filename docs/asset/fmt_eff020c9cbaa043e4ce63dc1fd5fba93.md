
```bash
#!/bin/sh
s -q -DBATCH -DNOPAUSE -dSAFER \
-sOutputFile=$ -sDEVICE=pnmraw $@
```

双引号中的 `"$@"` 会展开由空格分隔的参数。

### 7.3.4 `$0`

变量 `$0` 存储脚本名称，它用于生成诊断信息。假设你的脚本需要报告一个存储在 `BADPARM` 变量中的无效参数。你可以通过以下行打印诊断信息，这样错误消息中就会脚本名称：

```bash
echo $0: bad option $BADPARM
```

你应该将诊断错误信息发送到标准错误（stderr）。回想第 1.14.1 节，`2>1` 将标准错误重定向到标准输出（stdout）。要写入标准错误，可以使用 `1>2` 反转这一过程。对于前面的 `BADPARM` 示例，使用以下命令：

```bash
echo $0: bad option $BADPARM 1>&2
```

### 7.3.5 `$$`

变量 `$$` 存储 shell 的进程 ID（PID）。

### 7.3.6 `$?`

变量 `$?` 存储 shell 执行的最后一个命令的退出码。退出码是掌握 shell 脚本的关键，接下来将对其进行讨论。

## 7.4 退出码

当一个 Unix 程序结束执行时，它会为启动该程序的父进程留下一个退出码。退出码是一个数字，有时被称为错误代码。当退出码为 0 (`0`) 时，意味着程序运行没有问题。然而，如果程序出错，它通常以某个非 0 的数字退出。

最后一个命令的退出码存储在特殊变量 `$?` 中，因此你可以在 shell 提示符下自行检查：

```bash
$ ls / > /dev/null
$ echo $?
0
$ ls /asdfas > /dev/null
ls: /asdfas: No such file or directory
$ echo $?
1
```

你可以看到成功的命令返回了 0，而失败的命令返回了 1。

如果你打算使用某个命令的退出码，必须在运行命令后立即使用或存储该代码。例如，如果你在上述系列命令完成后紧接着运行第三次 `echo $?`，结果将是 0，因为两个 `echo` 命令中的第二个已经成功执行了。你应该使用类似 `exit 1` 的命令，将退出码 1 传给运行它的任何父进程。

在编写异常终止脚本的 shell 代码时，你不一定非使用 1；但例如，你可能想对不同的条件使用不同的数字。

> 注意：像 `diff` 和 `grep` 等某些程序使用非零退出码表示正常情况。例如，如果 `grep` 在输入中找到匹配模式的内容，它返回 1，否则返回 0。在这种情况下，非零退出码并不是错误。这些命令使用其他退出码表示错误：`grep` 和 `diff` 使用 2 表示真实问题。如果你正在编写使用非标准退出码的程序，请阅读其手册页。退出码通常在“DIAGNOSTICS”（诊断）部分进行解释。

## 7.5 条件判断

Bourne shell 拥有用于条件的特殊结构，例如 `if/then/else` 语句。这里有一个带有条件的简单脚本，检查脚本的第一个参数是否为 `hi`：

```bash
#!/bin/sh
if [ $1 = hi ]; then
    echo 'The first argument was "hi"'
else
    echo -n 'The first argument was not "hi" -- ' \
    echo It was "$1"'
fi
```

上述脚本中的 `if`、`then`、`else` 和 `fi` 是 shell 关键字。其他所有内容都是命令。这是一个极其重要的点，因为其中一个命令是 `$1 = "hi"`。`[` 字符是 Unix 系统上的一个实际程序；并不是特殊的 shell 语法。所有 Unix 系统都有一个名为 `[` 的命令，用于执行 shell 条件测试。该程序也称为 `test` ——仔细检查 `[` 会发现它们共享同一个索引节点（inode），或者其中一个是另一个的符号链接。

现在你可以明白为什么 7.4 节中的退出码如此重要了，因为整个过程是这样工作的：

- 1. shell 运行 `if` 关键字后面的命令，并收集该命令的退出码。
- 2. 如果退出码为 0，shell 执行 `then` 关键字之后的所有命令，直到遇到 `else` 或 `fi` 关键字停止。
- 3. 如果退出码不是 0 且存在 `else` 子句，shell 运行 `else` 关键字后面的命令。
- 4. 条件判断在 `fi` 处结束。

注意：上述示例中的条件存在一个小问题——这是一个常见的错误。它可能是空的，因为用户可能没有输入参数。如果没有参数，测试将读取 `[ = "hi" ]`，导致 `[` 命令报错并终止。你可以通过以下两种方式之一将参数括在引号中（两种都很常见）来修复它：

```bash
if [ "$1" = hi ]; then
if [ "$1" = x"hi" ]; then
```

值得重复的是，`if` 之后的内容始终是一个命令。你需要在测试命令后加一个分号（`;`）——如果你跳过了分号，shell 会将 `then` 作为参数传递给测试命令。（如果你不喜欢那样，可以将 `then` 放在新的一行）。

这是一个如何使用分号的示例：

```bash
if [ $1 = hi ]; then
    echo "The first argument was 'hi'"
else
    echo "The first argument was not 'hi'"
fi
```

这是一个在循环中使用测试的示例：

```bash
#!/bin/sh
for filename in *; do
    if [ -f $filename ]; then
        ls -l $filename
    else
        echo "$filename is not a regular file"
    fi
done
```

这是一个使用多个条件的示例：

```bash
#!/bin/sh
if [ -f file1 -a -f file2 ]; then
    echo "Both files are regular"
fi
```

这是一个使用 OR 运算符的示例：

```bash
#!/bin/sh
if [ -f file1 ] || [ -f file2 ]; then
    echo "At least one of the files is regular"
fi
```

这是一个使用 NOT 运算符的示例：

```bash
#!/bin/sh
if [ ! -f file1 ]; then
    echo "file is not a regular file"
fi
```

### 7.5.2 测试条件

你已经知道如何通过 `[ str1 = str2 ]` 测试字符串；测试成功时退出码为 0，失败时为非零。

然而，请记住，大多数测试操作非常适合处理文件。一个重要的原因是大多数测试涉及文件属性。例如，下一行检查文件是否为普通文件：

```bash
-f file
```

在脚本中，你可能会看到如下的 `-f` 测试，用于测试当前目录下的所有项：

```bash
for filename in *; do
    if [ -f $filename ]; then
        ls -l $filename
    else
        echo "$filename is not a regular file"
    fi
done
```
