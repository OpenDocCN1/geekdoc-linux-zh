
在对简单组件的测试中（第 8 行的 `if` 语句），左侧是去除了后缀 `/` 后的参数（第 463 页）。如果没有这种字符（例如，如果 `$1` 是 `alex`），则没有字符被移除，两边相等。假设参数是一个后面带有斜杠的简单文件名，例如 `/usr`。在这种情况下，表达式 `${1%/*}` 的求值为空字符串。为了让函数在这种情况下工作，你必须采取两个预防措施：在这种情况下如所示所示将表达式放在引号内，并确保你的递归函数在将空字符串作为参数传递时表现正常。通常，程序是健壮的：它们已经为边界、无效或无意义的输入做好了准备，并表现出恰当的行为。

通过在函数开头放置以下命令，你可以开启跟踪（tracing）并观察递归的工作过程：

```
setopt xtrace

if [[ -o xtrace ]]; then print "makepath $*"; fi
```

由于 Z Shell 的跟踪不显示函数调用，上面的第二行显示了在跟踪开启时，每次执行函数时显示的函数名和参数。

```
zsh % makepath a/b/c

+ print makepath a/b/c

makepath a/b/c

+ setopt xtrace

+ print makepath a/b

makepath a/b

+ setopt xtrace

+ print makepath a

makepath a

+ mkdir a

+ return 0

+ mkdir a

+ makepath a/b
```

## Shell 程序 513

+ return 0
+ mkdir a/b/c
+ return 0

你可以看到函数沿着递归路径工作并再次向上返回。使用一个无效的路径调用 `makepath` 并观察发生了什么是很有启发意义的。下面的示例显示了尝试创建路径 `/a/b/c` 时会发生什么，这要求你在根目录下创建目录 `a`。除非你有权限，否则你被允许这样做。

```
zsh % makepath /a/b/c

+ print makepath /a/b/c

makepath /a/b/c

+ set xtrace

+ print makepath /a/b

makepath /a/b

+ set xtrace

+ print makepath /a

makepath /a

+ set xtrace

+ print makepath

makepath

+ return 0

+ mkdir /a

mkdir: cannot make directory '/a': Permission denied

+ return 1

+ return 1

+ return 1
```

只有当 `makepath` 传递一个空参数且错误一直传回时，递归才会停止，因此示例 `makepath` 以非零状态退出。

### 注意

示例忽略了你在使用递归函数时可能会遇到的潜在问题。该问题的原因是，默认情况下 Z Shell 变量是全局的。在递归函数的执行期间，该函数的多个实例可能同时激活。除一个外，它们都在等待其“子”调用完成。如果递归的 Z Shell 使用变量，除非你将变量设为局部的，否则这些函数将共享每个变量的副本。这可能会产生副作用，而通常这不是你想要的。按照规则，你应该使用 `typeset`（第 455 页）或 `local` 将所有递归函数的变量都设为局部的。

## 一个编程问题：makers

本节将一些 Z Shell 编程结构结合成一个完整的程序。示例使用了 `ci`，它是 Linux 版本控制系统 (RCS) 命令之一。如果你不熟悉 RCS，请参阅第 559 页的描述。示例还使用了 `find`（见第二部分第 730 页）。

编写一个名为 `makers` 的程序，接受两个目录名作为参数 `source` 和 `target`。程序应该在 `target` 中创建以 `source` 为根的层次结构的副本，但 `source` 下每个普通文件都应该使用 `ci` 签入对应的 RCS 文件。如果 `target` 不存在，应该创建它。程序应确保路径 `source` 不是路径 `target` 的前缀，反之亦然。它应该跳过 `source` 中任何不是目录或普通文件的文件（例如 FIFO 或套接字）。

下面的命令应该在 `resdir` 下创建一个与 `sdir` 下相同的层级结构，除非（例如）`resdir/functions/func1.sh` 是普通文件，此时该命令应该创建 `resdir/functions/func1.sh,v`：

```
makersrc resdir scdir
```

## 514 第 13 章：Z Shell 高级 Shell 编程

解决此类问题有很多方法。这里是解决该问题的算法：

- 检查命令行参数数量是否正确。如果无效，则说明并退出。
- 从一个目录开始。如果无效，则说明并退出。
- 目录二必须可用。如果它存在但是一个普通文件，则说明并退出。
- 确保两个目录都不在另一个的路径中。如果无效，则说明并退出。
- 使用 `find` 遍历源树以产生路径名。对于每个路径名：
    - 确定路径名是指目录、普通文件还是其他。
    - 构建以目标目录为根的对应的路径名。
    - 使用 `ci` 在该路径处创建 RCS 文件。

## Shell 程序 515

```
checkargs() {

    # 只允许两个参数。

    if [[ $# != 2 ]]; then

        print -u2 "usage: rcname source dest"

        exit 1

    fi

    # 必须从目录开始

    if [[ ! -d "$1" ]]; then

        print -u2 "$1: 不是目录"

        exit 1

    fi

    # 目录二必须可用

    if [[ -a "$2" && ! -d "$2" ]]; then

        print -u2 "$2: 不是目录"

        exit 1

    fi

    # 确保两个目录都不在另一个的路径中

    if [[ "$1" = "$2" || "$2" = "$1" ]]; then

        print -u2 "无法在上方或对方创建。"

        exit 1

    fi

    return 0

}
```

你可以通过命令 `checkargs "$@"` 调用此函数，将命令行参数传递给 `checkargs`。

程序的主部分使用 `find` 查找文件和目录。`findSource` 命令将以 source 为根的层次结构中的每个文件的路径每行输出到标准输出。如果 shell 将 `find` 放入协进程并在循环中从协进程读取，它可以如下所示处理路径名：

```
coproc find &source

while read pathname <&p

do

    commands

done
```

程序必须妥善处理错误和特殊情况。它打开两个文件，一个读取错误，另一个记录被跳过的文件名。

将各个部分结合并填充缺失部分，这里是解决该问题的完整程序：

```
#!/bin/zsh

ERRS=./err_file

REPORT=./report
```

```
rcname() {

    echo ${1},v

}
```

`rcname` 函数在文件名末尾附加 .v。答案被写入标准输出，以便你能够在命令替换中使用 `rcname`，例如

```
newname=$(rcname oldname)
```

# 516 第 13 章：Z Shell 与高级 Shell 编程

```bash

if [[ ${#} -eq 0 || -d "1" ]]; then

    return 0;

fi

if [[ "${1%*}\
```

# 打开错误日志和报告文件
exec 3>$ERRS
exec 4>$REPORT

```bash

source="$1"

dest="$2"

copro find "$source" -print

while read pathname; do

    target=$dest/${pathname#$source}

    if [[ ! -d "$pathname" ]]; then

        makepath "$target" || print -u3 "Cannot create directory $target"

    elif [[ -f "$pathname" ]]; then

        target=$(rcname "$pathname")

        ci -l -q "-t-$pathname" "$target" >4 2>&3 ||

```

# Shell 程序 517

```bash

print -u3 "Cannot create target"

else

    print -u4 "$pathname is not a directory or regular file: skipped"

fi

done

exec 3<&-

exec 4&-

# 如果错误和报告文件为空则删除它们！

if [ ! -s $SERRS ]; then /bin/rm -f $SERRS; fi

if [ ! -s $REPORT ]; then /bin/rm -f $REPORT; fi

exit 0

```

有许多方法可以改进这个程序。例如，它的状态并不总是反映实际发生的情况。本章末尾的练习将要求你以各种方式修改该程序。

# 另一个编程问题：测验 (quiz)

这里有另一个可以用 Z Shell 解决的这个问题。这个问题需要与用户进行交互，因此解决方案需要不同的 Shell 编程特性。

> 编写一个名为 quiz 的通用选择程序。该程序应该从数据文件中获取问题，并将其展示给用户。它应该记录正确答案和错误答案的数量。用户必须能够随时编辑程序，并获得到目前为止的结果总结。

该程序的详细设计，甚至对问题的详细描述，都取决于许多选择：程序如何知道哪些科目可以进行测验？用户如何选择科目？程序如何知道测验何时结束？程序应该每次都以相同的顺序展示（给定科目）问题，还是应该打乱它们的顺序？

当然，在具体化问题说明时，你可以做出许多完美的选择：

- 每个科目对应于主测验目录的一个子目录。该目录由环境变量 `QUIZDIR` 命名，默认值为 `/usr/games/lib`。
- 特定科目中的每个问题对应于该科目目录中的一个文件。
- 问题的表示形式如下：文件的第一行是问题的文本。如果超过一行，则必须用反斜杠转义 NEWLINE（这种选择使得使用 read 内置函数读取单个问题变得容易）。）。文件的第二行是一个整数，表示选项的数量。接下来的几行是选项本身。最后一行是正确答案。以下是一个示例问题文件。

# 518 第 13 章：Z Shell 与高级 Shell 编程

谁发现了杠杆原理？
4
欧几里得
阿基米德
托马斯·迪森
杠杆兄弟
阿基米德

- 程序展示科目目录中的所有问题。用户可以在任何时候通过 CONTROL-C 中断测验，此时程序将总结结果并退出。如果用户没有中断，那么当程序问完所有问题后，它将总结结果并退出。
- 程序在展示科目中的问题之前对其进行打乱顺序。

以下是该程序的顶层设计：

1. 初始化。这涉及许多步骤，例如将目前为止的问题数量以及正确和错误数量设为零。
2. 向用户提供科目选择，并获取用户的响应。
3. 切换到相应的科目目录。
4. 确定要问的问题（即该目录下的文件名）。以随机顺序重新排列它们。
5. 重复展示问题并询问答案，直到测验结束或被用户中断。
6. 展示结果并退出。

显然，这些步骤中的某些（如步骤 3）是简单的，而另一些（如步骤 4）是复杂的，值得单独分析。对任何复杂步骤使用 Shell 函数，并使用 trap 处理中断。

这里是程序的骨架版本，带有空的 Shell 函数：

```bash

function initialize

{

# 待填充。

}

function choose_subj

{

# 待填充。将选择写入标准输出。

}

function scramble

{

# 待填充。将打乱后的文件名存储

# 在名为 questions 的数组变量中。

```

# Shell 程序 519

```bash

function ask

{

# 待填充。读取问题文件，提问并检查

# 答案。如果答案正确则返回 0，否则返回 1。如果

# 无效的问题文件，则以状态 2 退出。

}

```

```bash

function summarize

{

# 待填充。向用户展示分数。

}

```

```bash

# 主程序

# 顶层设计中的步骤 1

initialize

# 处理用户中断

trap 'summarize; exit 0'

choose_subj

# 步骤 2

[[ $? -eq 0 ]] || exit 2

# 步骤 3

cd $subject || exit 2

# 步骤 4

scramble

# 步骤 5

for question in "${questions[@]}"; do

  ask

  if [[ $? -eq 0 ]]; then

    ((num_correct++))

  else

    ((num_ques++))

  fi

done

# 步骤 6

summarize

exit 0

```

有许多方法可以改进这个程序。例如，它的状态并不总是反映实际发生的情况。本章末尾的练习将要求你以各种方式修改该程序。一种初始化函数的方法是

# 520 第 13 章：Z Shell 与高级 Shell 编程

```bash

initialize() {

  num_ques=0

  num_correct=0

  cd $QUIZDIR:/usr/games/lib || exit 2

}

```

虽然它是初始化的一部分，但 trap 语句属于主程序。在 Z Shell 中，函数内部的 trap 是局部的（参见第 493 页）。下一个函数 choose_subj 复杂一些，使用 select 语句实现。

```bash

choose_subj() {

  set -A subjects $(command ls)

  PS3="选择一个测验科目: "

  select Subject in "${subjects[@]}"; then

    if [[ -z $Subject ]]; then

      print -u "未选择科目。再见。"

      exit 0

    fi

    print $Subject

    return 0

done

}

```

该函数首先使用 ls 命令获取科目目录列表。调用 ls 之前使用了保留字 command，以确保即使有名为 ls 的别名或函数也不会使用它们。select 向用户展示科目列表（通过 ls 找到的目录），并将选定的目录放入 Subject 中。参见第 477 页的 select。最后，函数将科目目录写入标准输出（如骨架程序所示）被存储在变量中。你必须为 cd 内置做好准备。目录可能是不可用的，或者另一个用户在 ls 和 cd 命令之间移动了目录。
scramble 函数面临许多困难。它使用数组存储问题名称。你需要一种能够随机打乱数组项并利用 RANDOM 变量算法。以下是 scramble 函数的实现：

```bash

scramble() {

  typeset -i index quescount

  set -A questions $(command ls)

  quescount=${#questions[@]}

  ((index = quescount))

  while ((index > 1)); do

    ((target = RANDOM % index + 1))

    exchange $target $index

    ((index -= 1))

  done

}

exchange() {

  typeset temp=${questions[$1]}

  questions[$1]=${questions[$2]}

  questions[$2]=$temp

}
```




# Shell 程序 521

此部分将数组变量 `questions` 初始化为工作目录下文件名（questions）的列表。变量 `quescount` 被设置为文件数量。然后使用以下算法：让变量 `index` 从 `quescount`（数组变量最后一个项的索引）递减。对于 `index` 的每一个值，函数会在 1 到 `index` 之间（包含边界值）随机计数一个值。

```bash

(( target = RANDOM % $index + 1 ))
```

上述代码通过取 `RANDOM` 除以 `index` 的余数（`%` 运算符），产生 0 到 `index` 之间的随机值。该函数交换 `questions` 数组中位置 `target` 和 `index` 的元素，以确保同一个问题不会重复。在另一个名为 `exchange` 的函数中执行此操作非常方便。

```bash

exchange() {

  local temp_value

  temp_value=$questions[$1]

  questions[$1]=${questions[$2]}

  questions[$2]=$temp_value

}
```
