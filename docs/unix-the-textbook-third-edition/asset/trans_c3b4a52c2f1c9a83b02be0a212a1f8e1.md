

## EXERCISE 12.6

复制 myname 变量的值到另一个变量 anyname。使 anyname 变量只读并 unset 掉 myname 和 anyname 变量。发生了什么？展示你的全部工作。

## 12.4 PASSING ARGUMENTS TO SHELL SCRIPTS

在本节中，我们描述了命令行参数如何传递给 shell 脚本以及如何被其操作。如我们在第 12.3 节中讨论的，你可以将命令行参数，或位置参数，传递给一个 shell 脚本。这些参数的值，从第一个参数开始，分别存储在变量 $1、$2、$3、$4 等中。变量名 $0 包含脚本文件名（即命令名）。在某些 UNIX 系统上，最多只有前九个参数存储在这些变量中。你可以使用这些变量的名称来引用这些参数的值。如果引用的位置参数未被传入参数，其值为 null。环境变量 $# 包含脚本执行时传入的参数总数。变量 $* 和 $@ 都包含所有参数的值，但 $@ 在用作 "$@" 时会为每个单独的参数加上引号。cmdargs_demo 文件中的 shell 脚本展示了如何使用这些变量。

```
$ cat cmdargs_demo
#!/bin/sh
echo "The command name is: $0."
echo "The number of command line arguments passed as parameters is $#."
echo "The values of the command line arguments are: $1 $2 $3 $4 $5 $6 $7 $8 $9 $10 $11"
echo "Another way to display the values of all of the arguments is: $@."
echo "Yet another way is: $*."
exit 0
$ ./cmdargs_demo a b c d e f g h i j k l m n
The command name is: cmdargs_demo.
The number of command line arguments passed as parameters is 9.
The values of the command line arguments are: a b c d e f g h i j k.
Another way to display the values of all of the arguments: a b c d e f g h i j k l m n.
Yet another way is: a b c d e f g h i j k l m n.
$ ./cmdargs_demo One Two 3 Four 5 6
The command name is: cmdargs_demo.
The number of command line arguments passed as parameters is 6.
The values of the command line arguments are: One Two 3 Four 5 6.
Another way to display the values of all of the arguments: One Two 3 Four 5 6.
Yet another way is: One Two 3 Four 5 6.
$
```

在 shell 仅在 shell 变量 $1–$9 中同时维护最多九个位置参数的系统上，你可以编写能够接受并处理超过九个参数的脚本。为此，使用 shift 命令。默认情况下，该命令将命令行参数向左移动一个位置，使 $2 变成 $1，$3 变成 $2，依此类推。第一个参数 $1 被移出。一旦移位，参数就无法恢复到原始值。移位的位数可以多于一个，并作为命令的参数指定。以下是该命令的简要说明。

### SYNTAX

```
shift [N]
```

Purpose: Shift the command line arguments N positions to the left

shift_demo 文件中的脚本展示了 shift 命令的语义。第一个 shift 命令将第一个参数移出并将剩余参数向左移动一个位置。第二个 shift 命令将当前参数向左移动三个位置。三个 echo 命令用于分别显示程序名 ($0) 的当前值、所有位置参数的值 ($@) 以及前三个位置参数的值。脚本执行的结果显而易见。

```
$ cat shift_demo
#!/bin/sh
echo "The program name is $0."
echo "The arguments are: $@"
echo "The first three arguments are: $1 $2 $3"
shift
echo "The program name is $0."
echo "The arguments are: $@"
echo "The first three arguments are: $1 $2 $3"
shift 3
echo "The program name is $0."
echo "The arguments are: $@"
echo "The first three arguments are: $1 $2 $3"
exit 0
$ ./shift_demo 1 2 3 4 5 6 7 8 9 10 11 12
The program name is shift_demo.
The arguments are: 1 2 3 4 5 6 7 8 9 10 11 12
The first three arguments are: 1 2 3
The program name is shift_demo.
The arguments are: 2 3 4 5 6 7 8 9 10 11 12
The first three arguments are: 2 3 4
The program name is shift_demo.
The arguments are: 5 6 7 8 9 10 11 12
The first three arguments are: 6 7 8
```

