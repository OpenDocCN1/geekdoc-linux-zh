
- 内置整数运算和整数数据类型
- 扩展陷阱处理
- 输入（`read`）和输出（`print`）设施
- 针对任何文件描述符的文件控制和 I/O 重定向，包括文件描述符复制
- 数组变量和字符串操作符

本章之前的章节讨论了这些特性中的大部分，许多特性对于交互和 shell 编程都有用。本节开发了一个完整的 shell 程序，向你展示如何有效地结合这些特性。

# 程序结构

Z Shell 提供的结构并不是随机组合。它们经过仔细挑选，以提供像 C 或 Pascal 等其他过程化语言中的大多数结构化特征。过程化语言必须为你提供这些能力：

- 声明、赋值、操作变量和常量数据的能力。Z Shell 提供了字符串变量以及完整的算术运算符。
- 通过创建子程序将大程序拆分为小程序的能力。Z Shell 允许创建函数并调用脚本。Z 函数是可以递归调用的；即一个函数可以调用自己。你可能不需要递归，但有时它允许你轻松地解决困难问题。
- 条件执行语句的能力，使用如 Z Shell 的 `if` 等语句。
- 迭代执行语句的能力，使用如 `while` 和 `for` 等语句。
- 在程序内外传输数据的能力，与用户通信。

编程语言以不同的方式实现这些能力，但核心思想是相同的。当你想要用程序解决问题时，必须先想出一个解决方案的步骤。这种步骤被称为算法。通常，你可以在不同的语言中以相似的方式实现同一个算法。在本章之前，你已经看到了除递归以外的所有 Z Shell 编程结构。一个有效的递归 Z 函数示例将在下一节给出。

# 递归

递归结构是根据自身定义的。这听起来可能是循环的，但并不是。为了避免循环，递归定义必须包含一个非自引的特例。递归思想出现在生活中。例如，你可以将祖先定义为母亲、父亲或你的祖先之一。这个定义不是循环的；它明确指定了你的祖先是谁（你的母亲、你的父亲、你母亲的母亲、你父亲的母亲，以此类推）。

许多 Linux 工具递归运行。请参见第二部分中 `chmod`（第 676 页）和 `chown`（第 680 页）工具的示例。

使用递归函数解决以下问题：

```编写一个名为 makedath 的 shell 函数，给定一个路径名，将该路径中的所有组件创建为目录。例如，命令 makedath a/b/c/d 应该创建 a、a/b、a/b/c 和 a/b/c/d。mkdir 工具支持执行此操作的 -p 选项。在不使用 mkdir -p 的情况下解决该问题。```

递归解决方案的一种算法如下：

1. 检查此路径参数。如果是空字符串或已存在的目录，则什么都不做并返回。
2. 如果它是简单的路径组件，创建它（使用 `mkdir`）并返回。
3. 否则，使用原始参数的路径前缀调用 `makepath`。这（最终）会创建最后一个组件之前的所有目录，然后可以使用 `mkdir` 创建。

通常情况下，递归函数必须调用一个不需要再次调用自身的简单情况（base case）。它不断递归，直到最终遇到了问题的简单版本时才停止。

以下是基于该算法的一种可能解决方案：

```
makepath()
  if [[ ${1} -eq 0 || -d "$1" ]]
    then
      return 0 # 什么都不做
    fi
  # 检查参数是否为简单路径组件：
  if [[ "${1/*}" ]]
    then
      mkdir "$1"
      return $?
    fi
  makepath ${1/*} || return 1
  mkdir "$1"
  return $?
```

在对简单组件的测试（第八行的 `if` 语句）中，左侧表达式是剥离了 `/` 字符开头的最短后缀后的参数（第 463 页）。如果没有这样的字符（例如如果 `$1` 是 `alex`），则什么都没有被剥离，两边相等。假设参数是一个以斜杠开头的简单文件名，例如 `/usr`。在这种情况下，表达式 `${1/*}` 的求值为空字符串。为了让函数在这种情况下正常工作，你必须采取两项预防措施：如所示给左侧表达式加上引号，并确保你的递归函数在接收空字符串作为参数时行为正常。通常，良好的程序是健壮的：它们为边界、无效或无意义的输入做好了准备，并表现出恰当的行为。

通过在函数开头放置以下命令，你可以开启追踪并观察递归的运行。

```
setopt xtrace
  if [[ -o xtrace ]]; then print makepath "$"; fi
```

由于 Z 追踪不显示函数调用，上面的第二行显示了在追踪开启时，每次执行的函数名和参数：

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
+ mkdir a/b
```

++ return 0

+ mkdir a/b

+ return 0

你可以看到函数沿着递归路径向下执行并再次向上返回。使用无效路径调用 `makepath` 并观察发生了什么是有启发性的。下面的示例展示了当你尝试创建路径 `/a/b/c` 时发生的情况，这需要在根目录下创建目录 `a`。除非你有权限，否则你是不允许这么做的。

```
zsh % makedpath /a/b/c
+ print makedpath /a/b/c
makepath /a/b/c
+ setopt xtrace
+ print makedpath /a/b
makedpath /a/b
+ setopt xtrace
+ print makedpath /a
makedpath /a
+ setopt xtrace
+ print makedpath
makedpath
+ return 0
+ mkdir /a
mkdir: cannot make directory '/a': Permission denied
+ return 1
+ return 1
+ return 1
```

只有当向 `makedpath` 传递空参数且错误返回一直传回时，递归才会停止，因此原始的 `makepath` 以非零状态退出。

## 注意

示例忽略了你在使用递归函数时可能会遇到的潜在问题。该问题源于：默认情况下，Z Shell 变量是全局的。在递归函数的执行期间，该函数的多个实例可能同时处于激活状态。但它们中的每一个都在等待它们的“子”调用完成。如果递归的 Z Shell 函数使用了变量，除非你将变量设为局部（`local`），否则这些函数将共享每个变量的副本。这可能会产生副作用，而这通常不是你想要的。按照原则，你应该使用 `typeset`（第 455 页）或 `local` 将所有递归函数的变量都设为局部。

## 一个编程问题：markers

本节将一些 Z Shell 结构组合成一个完整的程序。示例使用了 `ci`，它是 Linux 系统版本控制系统（RCS）命令之一。如果你不熟悉 RCS，请参阅第 559 页的描述。示例还使用了 `find`（见第二部分第 730 页）。

编写一个名为 `markers` 的程序，接受两个目录名作为参数：`source`（源）和 `target`（目标）。程序应该在 `target` 中创建以 `source` 为根的层次结构的副本，但 source 下的每个普通文件应该通过命令提交到 target 下对应的 RCS 文件。如果 `target` 不存在，则应该创建它。程序应确保路径 `source` 不是路径 `target` 的前缀，反亦然。它应该跳过 `source` 中任何不是目录或普通文件的文件（如 FIFO 或套接字）。

以下命令在 `srcdir` 下创建一个与 `srcdir` 相同的层次结构，但（例如）`srcdir/functions/func1.sh` 是普通文件，那么命令应该创建 `srcdir/functions/s.func1.sh`：

```
markers srcdir srcdir
```

解决此类问题的方法像程序员人数一样多。这里是解决该问题的算法：

1. 检查命令行参数的有效性。如果无效，则提示并退出。
2. 遍历 source，使用 `find` 生成路径。对于每个路径：
   a. 如果路径指向目录，则创建相应的目录。
   b. 如果路径指向普通文件，则构造相应的路径并使用 `ci` 在那里创建 RCS 文件。
   c. 如果路径指向其他类型的文件，则向报告文件写入消息并跳过它。
3. 在每个阶段，如果发生错误，将适当的消息写入错误文件。

因此，程序的主体可以采用如下结构：

```
coproc find &source <&
while read pathname <&
do
    commands
```

## 516 第 13 章：Z Shell 与高级 Shell 编程

```bash
if [[ ${#} -eq 0 || -d "$1" ]]; then
    return 0;
fi
if [[ "${1%/*}" = "$1" ]]; then
    mkdir "$1"
    return $?
fi
makepath ${${1%%/*}} || return 1
mkdir "$1"
    return $?
}
```

```bash
rcname() {
    echo ${1},v
}
checkargs() {
    if [[ $# -ne 2 ]]; then
        print -u2 "usage: makers source dest"
        exit 1
    fi
    if [[ ! -d "$1" ]]; then
        print -u2 "$1: Not a directory"
        exit 1
    fi
    if [[ -a "$2" && -d "$2" ]]; then
        print -u2 "$2: Not a directory"
        exit 1
    fi
    if [[ "$1" = "$2" || "$2" = "$1" ]]; then
        print -u2 "Cannot make one directory above or below the other."
        exit 1
    fi
    return 0
}
```

```bash
checkargs "$@"

# 打开错误和报告文件
exec 3>ERRS
exec 4>REPORT

source="$1"
dest="$2"
coproc "$source" -print find pathname <&; do
    while read pathname; do
        target=$dest${pathname$source}
        if [[ -d "$pathname" ]]; then
            makepath "$target" || return -u3 "Cannot create directory $target"
        elif [[ -f "$pathname" ]]; then
            target=$(rcname "$target")
            ci -l -q "-t$pathname" "$pathname" "$target" >2&3
            print -u3 "Cannot create $target"
        else
            print -u4 "$pathname is not a directory or regular file: skipped"
        fi
    done
done
exec 3<&-
exec 4<&-
# 如果错误和报告文件为空，则删除它们！
if [[ ! -s $ERRS ]]; then /bin/rm -f $ERRS; fi
if [[ ! -s $REPORT ]]; then /bin/rm -f $REPORT; fi

exit 0
```

有许多方法可以改进此程序。例如，它的退出状态并不总是反映实际发生的情况。本章末的练习要求你以各种方式修改该程序。

## 另一个编程问题：测验 (quiz)

另一个你可以用 Z Shell 程序解决的。。这个问题要求与用户进行交互，因此解决方案需要不同的 Shell 编程特性。

> 编写一个名为 `quiz` 的通用选择程序。该程序应该从数据文件中获取问题并将其展示给用户。它应该记录正确答案和错误答案的数量。用户必须能够随时退出程序，并显示结果摘要。

该程序的详细设计，甚至对问题的详细描述，都取决于许多选择。程序将如何知道哪些主题可以用于测验？用户将如何选择主题？程序如何知道测验何时结束？程序应该每次以相同的顺序展示（对于给定的主题）相同的问题，还是应该对它们进行随机乱序？

当然，在定义问题时，你可以做出许多非常好的选择。以下细节使问题具体化：

- 每个主题对应于主测验目录的一个子目录。该目录将由环境变量 `QUIZDIR` 命名，其默认值为 `/usr/games/lib`。
- 特定主题中的每个问题对应于主题目录中的一个文件。
- 问题的表示如下：文件的第一行是问题的文本。如果超过一行，则必须用反斜杠转义换行符（NEWLINE）（这种选择使得使用 `read` 内置函数读取单个问题变得简单）。第二行是一个整数，代表选项的数量。接下来的行是选项本身。最后一行是正确答案。以下是一个示例文件。

```text
Who discovered the principle of the lever?
Euclid
Archimedes
Thomas Edison
The Lever Brothers
Archimedes
```

- 程序展示主题目录中的所有问题。用户在任何时候都可以通过 `CONTROL-C` 中断测验，此时程序将总结到为止的结果并退出。如果用户没有中断，那么当程序问完所有问题后，它将总结结果并退出。
- 程序在展示主题中的问题之前，应该对它们进行随机乱序。

以下是该程序的顶层设计：

1. 初始化。这涉及许多步骤，例如将目前为止已问的问题数量以及正确和错误答案的数量设置为零。
2. 向用户提供主题选择，并获取用户的响应。
3. 切换到相应的主题目录。
4. 确定要问的问题（即该目录中的文件名）。以随机顺序重新排列。
5. 重复展示问题并询问答案，直到测验结束或被用户中断。
6. 展示结果并退出。

显然，这些步骤中的某些（例如步骤 3）是简单的，而另一些（例如步骤 4）是复杂的。这是程序的骨架：

```bash
initialize() {
  num_ques=0
  cd ${QUIZDIR:-/usr/games/lib} || exit 2
}

choose_subj() {
  set -A subjects $(command ls)
  PS3="choose a subject for the quiz: "
  select Subject in "${subjects[@]}"; do
    if [[ -z "$Subject" ]]; then
      print -u2 "No subject chosen. Bye."
      exit 0
    fi
    print $Subject
    return 0
  done
}

scramble() {
  typeset -i index quescount
  set -A questions $(command ls)
  quescount=${#questions}
  ((index = quescount))
  while ((index > 1)); do
    ((target = $RANDOM % index + 1))
    # exchange logic
    tmp=${questions[$target]}
    questions[$target]=${questions[$index]}
    questions[$index]=$tmp
    ((index -= 1))
  done
}

ask() {
  # Implementation for asking a question
}

summarize() {
  # Implementation for showing results
}

# 主程序
trap 'summarize; exit' INT
initialize
subject=$(choose_subj)
cd "$subject" || exit 2
scramble
for ques in "${questions[@]}"; do
  ask "$ques"
done
summarize
```

# Shell 程序 521

此函数将数组变量 `questions` 初始化为目录中的文件名（问题）列表。变量 `quescount` 被设置为文件数量。然后使用以下算法：循环索引 `count` 取自 `quescount`（数组变量中最后一个项的索引）。对于 `index` 的每一个值，函数会在 1 到 `index`（包含边界值）之间选择一个随机目标值。命令

```bash
(( target = $RANDOM % $index + 1 ))
```

通过取 `RANDOM` 除以 `index` 的余数（`%` 运算符），产生一个 0 到 `index` 之间的随机值。然后，函数会交换 `questions` 中位置 `target` 和 `index` 处的元素，以确保相同问题不重复。在另一个名为 `exchange` 的函数中执行此操作非常方便。

```bash
exchange() {
  local temp_value
  temp_value=$questions[$1]
  questions[$1]=$questions[$2]
  questions[$2]=$temp_value
}
```
