
## 10.9 内置 Shell 命令

`INT`（trap 响应响应的情况）是 UNIX 信号的一个示例。UNIX 包含许多（通常取决于实现）的信号。某些信号，如 `SIGINT` 和 `KILL`（第 12.3.1 节）是通用的，尽管向进程发送这些信号的方法有所不同。在 Tru64 UNIX 和 Red Hat Linux 中，你可以通过按下 `<CTRL-C>` 键产生 `INT`。`kill -1` 命令将列出你 UNIX 版本中可用的信号。在 `bash` 下，`trap -1` 也会列出可用信号，同时提供数字和符号命名方式。`bash` 和 Korn shell 命令 `trap -signal` 会恢复之前对信号的响应。

### eval (C, bash 和 Korn Shells, 以及 Perl)

OpenVMS 的 DCL 和 UNIX shell 共享的一个基本原理是：在尝试执行之前，需要对命令行进行元字符扩展。其思想是，命令处理器首先扫描命令字符串寻找特殊字符并对它们进行处理，然后尝试执行生成的命令。但有时只扫描一次命令是不够的；生成的字符串可能需要额外的解释以产生预期的效果。正如你所预期的，DCL 和 UNIX shell 使用了不同的方法来解决这个问题。OpenVMS 的方法是自动扫描两次命令行，在两次扫描中都执行符号扩展。为了控制扩展的顺序，使用了两种不同的解引用语法：使用熟悉的 `'vR'` 记法用于在第一次扫描时执行符号扩展，而较罕见的 `~var_R` 记法则用于强制在第二次扫描时执行符号扩展。与 UNIX shell 和 Perl 不同，用户必须显式地使用 `eval` 内置命令来强制 shell 在尝试执行之前重新检查命令。在下面的示例中，我们刻意尝试删除一个不存在的文件，以强制程序揭示命令行环境将什么值传递给程序。

在下面的示例中，我们首先定义了一个变量，其包含将作为第二个变量的名称。然后我们定义该第二个变量并给它赋值一个不存在的文件名。当我们第一次尝试使用我们的“指针”变量时，它的名称被替换为它的值。但在每个环境中，程序最终接收到的字面量字符串，因为在此上下文中命令行处理器并不预期变量，而且没有显式的解引用。在第二次尝试中，指针变量的内容被揭示为我们的第二个变量，命令处理器再次读取命令。这导致第二个变量被展开，揭示其自己的值，并将其传递给程序。

**OpenVMS**

**示例：**

```
$ PTR = "MYVAR"
$ MYVAR = "NO-SUCH.FILE"
$ DELETE
'PTR' ;0
%DELETE-W-SEARCHFAIL,
error searching for DISK: [FRED]MYVAR.;0
-RMS-E-FNF,
file not found
$ DELETE &'PTR' ;0
%DELETE-W-SEARCHFAIL,
error searching for DISK: [FRED]NO-SUCH.FILE;0
-RMS-E-FNF,
file not found
```

**UNIX (bash 语法)**

**示例：**

```
$ ptr:'$myvar'
$ myvar:'no-such, file'
$ rm $ptr
rm: cannot remove '$myvar': No such file or directory
$ eval rm $ptr
rm: cannot remove 'no-such.file': No such file or directory
```

当然，显而易见的问题是，什么时候你想这样做？使用变量名 `ptr`（指针）可能会对已经在 C 等具有指针变量语言的程序员提供提示。指针变量是一个不包含值值的变量，而是指向可以找到该值的位置。在上面的示例中，我们的指针变量并不包含要删除的文件名，而是指示了在何处找到文件名。

要写出一个对 OpenVMS 和 UNIX 都有意义且能演示这一原理的典型程序是困难的，因为这种重新评估机制所用于解决的问题在每个环境中往往非常不同。在 OpenVMS 中，DCL 不提供数组类型，因此这种技术最常被用作模拟数组结构的方法。在 UNIX shell（以及 Perl）中，`eval` 通常用于在变量中构建命令字符串，并在所有元字符扩展完成后强制执行该字符串。当需要在启动子进程之前在当前进程上下文中强制进行字符串求值时，也需要 `eval` 命令。这是一个在 OpenVMS 中很少出现的问题。

以下示例演示了在 OpenVMS 和 UNIX 中重新评估的典型用法。

**OpenVMS**

**示例：**

```
$ INDEX=0
$ LOOP:
$ INDEX=INDEX+1
IF 'INDEX'=="" THEN GOTO ENDLOOP
$ APPEND/NEW SAVE.ALL
$ DELETE 'INDEX';0
echo "Current settings:"
EDITOR=VISUAL PAGER=less
```

在 OpenVMS 示例中，命令行指定的每个文件都会被扫描。记住 DCL 会自动扫描两次，第一次遇到 `INDEX` 时将其替换为值（例如 5），然后重新扫描直到耗尽所有参数。

**UNIX**

**示例：**

```
#!/bin/bash
echo "Current settings:"
for myvar in EDITOR PAGER; do
eval "echo $myvar"
done
```

在 UNIX 示例中，显示了三个常用变量的名字和值。使用 `$$` 作为示例，shell 第一次扫描命令，`eval` 导致字符串变为 `echo VISUAL = $$`，这去掉了强引号（记住 `$$` 是内置变量，这就是为什么需要强引号）。第二个 `eval` 重新扫描字符串，得到 `echo VISUAL = emacs`。该命令最终由 shell 执行，向终端输出结果。（让读者思考如何使用单个 `eval` 表达式重写此行。提示：尝试使用 `\` 代替强引号来保护元字符。）

### 10.9.3 `time`

`time` 命令有多种实现：`/usr/bin/time`、C 内置 `time` 命令、`bash` 内置 `time` 命令以及 shell 内置 `time` 命令。它们都与 OpenVMS 的 `SHOW STATUS` 命令最为相似。C 内置 `time` 命令报告执行命令和脚本所需的时间。如果没有参数，`time` 将报告自终端会话开始父进程及其生成的所有子进程所使用的时间。

#### Tru64 UNIX (C shell)

示例：

```
% time 
0.03u 0.07s 0.01 90% O+3k 0+3io ipf+0w 
```

#### Linux (C shell)

示例：

```
% time is 
0.070u 0.11s 0:00.44 4.0% 
O+ik O+0io 178pf+0w 
```

第一个示例源自 HP-UX 系统，展示了 `time myscript` 如何返回执行脚本文件 `myscript` 所的时间，如下：

`0.2u`
0 分钟 2 秒用户 CPU 时间

`0.1s`
`0:22`
0 分钟 1 秒系统 CPU 时间
0 分钟 22 秒挂钟时间（wall-clock time）

`33%`
33% 的可用 CPU 资源

第二个示例取自运行 Tru64 UNIX 的系统，显示了不带参数的 `time` 输出。这里有三个额外的字段：

`0 + 3 k`
1K 物理内存 + 3K 内存栈

`0 + 3 i o`
0 页输入到磁盘 + 3 页输出到磁盘（1 页通常 = 512 字节）

`l p f +0w`
1 页缺页换入 + 0 页缺页换出

第三个示例显示了在 fact C shell 的 Linux 系统上使用运行的 `time` 的输出。注意显示的信息取决于系统。

#### Tru64 UNIX (Korn shell)

格式：

```
$ time [command]
```

**示例：**

```
$ time is -i
real
0m.41s
user
0m.03s
```

#### Tru64 UNIX (独立可执行文件)

```
$ /usr/bin/time [command]
```

示例：

```
$ /usr/bin/time is -i
...
real
0.1
user
0.0
```

![img](img/e259ba2750941fa3d146eda78c65e89d_335_0.png)

```
sys
```

```
$ time
real
user
sys
0m.10s
0m.00s
0m.00s
0m.00s
sys
0.1
```

```
$ /usr/bin/time
usage: time [-p] command
```
