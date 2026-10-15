
**表 11.14 typeset 命令的其他用途**

| 命令 | 作用 |
|---|---|
| `typeset` | 显示所有变量 |
| `typeset -i num` | 仅接受 num 的整数值 |
| `typeset -x` | 显示已导出的变量 |
| `typeset a b c` | 如果在函数中定义，会将 a、b 和 c 创建为局部变量 |
| `typeset -r x=foo` | 将 x 设置为 foo，然后使其只读 |

## 11.9.10 位置参数

通常，这些特殊的內建变量（常被称为位置参数）在 shell 脚本中用于从命令行传递参数，或在函数中用于保存传递给函数的参数值。这些变量之所以称为位置参数，是因为它们通过数字 1、2、3 等来引用，这些数字代表了它们在参数列表中各自的位置。参见表 11.15。

shell 脚本的名称存储在 $0 变量中。位置参数可以通过 set 命令进行设置和重置。

**表 11.15 位置参数**

| 表达式 | 功能 |
|---|---|
| `$0` | 引用当前 shell 脚本的名称 |
| `$1-$9` | 位置参数 1-9 |
| `${10}` | 位置参数 10 |
| `$#` | 求值为位置参数的个数 |
| `$*` | 求值为所有位置参数 |
| `$@` | 与 `$*` 相同，但被双引号括起时除外 |
| `"$*"` | 求值为 "$1 $2 $3" 等 |
| `"$@"` | 求值为 "$1" "$2" "$3" 等 |

### 示例 11.32

```sh
1  $ set tim bill ann fred
    $ print $*        # prints all the positional parameters.
    tim bill ann fred

2  $ print $1        # Prints the first position.
    tim

3  $ print $2 $3     # Prints the second and third position.
    bill ann

4  $ print $#        # Prints the total number of positional parameters.
    4

5  $ set a b c d e f g h i j k l m
    $ print $10      # Prints the first positional parameter followed by a 0.
    a0
    $ print ${10} ${11} # Prints the 10th and 11th positions.
    j k

6  $ print $#
    13

7  $ print $*
    a b c d e f g h i j k l m

8  $ set file1 file2 file3
    $ print \$$#
    $3

9  $ eval print \$$#
    file3
```

### 说明

- **1.** set 命令将值赋给位置参数。$* 特殊变量包含所有已设置的参数。
- **2.** 显示第一个位置参数 tim 的值。
- **3.** 显示第二个和第三个参数 bill 和 ann 的值。
- **4.** $# 特殊变量包含当前设置的位置参数个数。
- **5.** set 命令重置所有位置参数，原有的参数列表被清空。要打印第 9 个之后的位置参数，需要使用花括号将两位数字组合在一起。否则，将会打印第一个位置参数的值，并在其后附加该数字。
- **6.** 此时位置参数的个数为 13。
- **7.** 打印所有位置参数的值。
- **8.** 美元符号被转义；$# 是参数的个数。print 命令显示 $3，即一个美元符号后跟位置参数的个数。
- **9.** eval 命令在执行命令之前会对命令行进行第二次解析。第一次由 shell 解析时，print 会显示 $3；第二次在 eval 之后，print 会显示 $3 的值，即 file3。

## 11.9.11 其他特殊变量

Korn shell 有一些特殊的內建变量，如表 11.16 所示。

**表 11.16 特殊变量**

| 变量 | 含义 |
|---|---|
| `$$` | shell 的 PID |
| `$-` | 当前设置的 ksh 选项 |
| `$?` | 最后执行命令的退出值 |
| `$!` | 放入后台的最后一个作业的 PID |

### 示例 11.33

```sh
1 $ print The pid of this shell is $$
The pid of this shell is 4725
2 $ print The options for this korn shell are $-
The options for this korn shell are ism
3 $ grep dodo /etc/passwd
$ print $?
1
4 $ sleep 25 &
[1] 400
$ print $!
400
```

### 说明

- **1.** $$ 变量保存此进程的 PID 值。
- **2.** $- 变量列出此交互式 Korn shell 的所有选项。
- **3.** grep 命令在 /etc/passwd 文件中搜索字符串 dodo。`$?` 变量保存最后执行命令的退出状态。由于 grep 返回的值为 1，因此可以认为 grep 搜索失败。退出状态为 0 表示成功退出。
- **4.** 在 sleep 命令后附加的 & 会使该命令在后台执行。$! 变量保存最后放入后台的命令的 PID。

