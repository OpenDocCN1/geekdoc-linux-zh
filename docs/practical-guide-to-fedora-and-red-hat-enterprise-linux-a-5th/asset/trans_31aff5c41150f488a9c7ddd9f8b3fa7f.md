
## 在递归函数中使用局部变量

函数沿着递归路径向下执行，然后又返回上来。调用 `makepath` 并使用无效路径来观察会发生什么，这是很有教育意义的。以下示例在开启调试运行的情况下，试图创建路径 `/a/b`，这需要你在根目录中创建目录 `a`。除非你有权限写入根目录，否则不允许创建此目录。

```bash
$ makepath /a/b
+ makepath /a/b
+ [[ 4 -eq 0 ]]
+ [[ -d /a/b ]]
+ [[ /a = \a ]]
+ makepath /a
+ [[ 2 -eq 0 ]]
+ [[ -d /a ]]
+ [[ '' = \^A ]]
+ [[ 0 -eq 0 ]]
+ return 0
+ mkdir /a
mkdir: cannot create directory '/a': Permission denied
+ return 1
+ return 1
```

当 `makepath` 被拒绝创建 `/a` 目录的权限时，递归停止。错误返回值一路传回，因此原始的 `makepath` 以非零状态退出。

> **提示** 上述示例忽略了使用递归函数时可能遇到的一个潜在问题。在递归函数的执行过程中，该函数的许多独立实例可能同时处于活动状态。除了其中一个实例外，其他所有实例都在等待其子调用完成。
>
> 由于函数在调用它们的 shell 的相同环境中运行，shell 及其调用的函数隐式共享变量，使得函数的所有实例共享每个变量的单一副本。共享变量可能会产生副作用，而这些都是你很少想要的。原则上，你应该使用 `typeset` 使递归函数的所有变量成为局部变量。有关更多信息，请参见第 928 页。

## 测验 shell 脚本

使用 *bash* 脚本解决以下问题：

> 编写一个通用的多项选择测验程序。程序应从数据文件中获取问题，向用户展示问题，并记录正确和错误答案的数量。用户必须能够在任何时候退出程序，并显示到该点为止的结果摘要。

该程序的详细设计，甚至问题的详细描述，取决于多种选择：程序如何知道哪些科目可供测验？用户如何选择科目？程序如何知道测验何时结束？程序是否应以相同的顺序（对于给定科目）每次呈现相同的问题，还是应该随机打乱它们？

当然，你可以做出许多完美的选择来实现问题的规范。以下细节缩小了问题规范的范围：

- 每个科目对应主测验目录的一个子目录。该目录将在环境变量 `QUIZDIR` 中命名，其默认值为 `~/quiz`。例如，你可以拥有以下目录，分别对应工程、艺术和政治科目：`~/quiz/engineering`、`~/quiz/art` 和 `~/quiz/politics`。如果你希望所有用户都能访问它，请将测验目录放在 `/usr/games` 中（需要 root 权限）。
- 每个科目可以有几个问题。每个问题由其科目目录中的一个文件表示。
- 每个表示问题的文件的第一行是问题的文本。如果它需要多于一行，你必须用反斜杠转义换行符。（这种设置使得使用 `read` 内建函数读取单个问题变得很容易。）文件的第二行是一个整数，指定选项的数量。接下来的行是选项本身。最后一行是正确答案。以下是一个示例问题文件：

```
who discovered the principle of the lever?
4
Eucuid
Archimedes
Thomas Edison
The Lever Brothers
Archimedes
```

- 程序呈现主题目录中的所有问题。在任何时候，用户都可以通过 CONTROL-C 中断测验，此时程序将总结迄今为止的结果并退出。如果用户没有中断，程序在问完所选科目的所有问题后，将总结结果并退出。
- 程序在呈现主题目录中的问题之前会对它们进行打乱。

### 顶层设计

以下是该程序的顶层设计：

1. 初始化。这涉及一些步骤，例如将已问问题的数量、正确和错误答案的数量设置为零。设置用于捕获 CONTROL-C 的陷阱。
2. 向用户呈现科目选择，并获取用户的响应。
3. 切换到相应的科目目录。
4. 确定要问的问题（即该目录中的文件名）。将它们按随机顺序排列。
5. 反复提出问题并要求答案，直到测验结束或被用户中断。
6. 呈现结果并退出。

显然，其中一些步骤（如步骤 3）很简单，而另一些步骤（如步骤 4）很复杂，值得单独分析。对于任何复杂的步骤，使用 shell 函数，并使用 `trap` 内建函数处理用户中断。

以下是该程序的骨架版本，包含空的 shell 函数：

```bash
function initialize
{
    # Initializes variables.
}

function choose_subj
{
    # Writes choice to standard output.
}

function scramble
{
    # Stores names of question files, scrambled,
    # in an array variable named questions.
}

function ask
{
    # Reads a question file, asks the question, and checks the
    # answer. Returns 1 if the answer was correct, 0 otherwise. If it
    # encounters an invalid question file, exit with status 2.
}

function summarize
{
    # Presents the user's score.
}

# Main program
initialize                # Step 1 in top-level design

subject=$(choose_subj)   # Step 2
[[ $? -eq 0 ]] || exit 2  # If no valid choice, exit

cd $subject || exit 2     # Step 3
echo # Skip a line

scramble

for ques in ${questions[*]}; do # Step 5
    ask $ques
    result=$?
    (( num_ques=num_ques+1 ))
    if [[ $result == 1 ]]; then
        (( num_correct += 1 ))
    fi
    echo # Skip a line between questions
    sleep ${QUIZDELAY:=1}
done

summarize # Step 6
exit 0
```

为了让用户更容易阅读结果，在问题循环中出现了 **sleep** 调用。它在问题之间延迟 `$QUIZDELAY` 秒（默认为 1 秒）。现在的任务是填补程序的缺失部分。从某种意义上说，这个程序是反向编写的。细节（shell 函数）在文件中先出现，但在开发过程中最后出现。这种常见的编程实践被称为自顶向下设计。在自顶向下设计中，你首先填写程序的粗略轮廓，稍后提供细节。这样，你将问题分解为更小的问题，每个问题都可以独立工作。Shell 函数在使用自顶向下方法时非常有帮助。

编写 **initialize** 函数的一种方法如下。**cd** 命令使 `QUIZDIR` 成为脚本其余部分的工作目录，如果未设置 `QUIZDIR`，则默认为 `~/quiz`。

```bash
function initialize ()
{
    trap 'summarize; exit 0' INT # Handle user interrupts
    num_ques=0 # Number of questions asked so far
    num_correct=0 # Number answered correctly so far
    first_time=true # true until first question is asked
    cd ${QUIZDIR:=~/quiz} || exit 2
}
```

准备好应对 `cd` 命令失败。目录可能无法搜索，或者另一个用户可能已将其删除。如果 `cd` 失败，前面的函数将以状态码 2 退出。

下一个函数 **choose_subj** 稍复杂一些。它使用 **select** 语句显示菜单：

```bash
function choose_subj ()
{
    subjects=(ls)
    PS3="Choose a subject for the quiz from the preceding list: "
    select subject in ${subjects[*]}; do
        if [[ -z "${subject}" ]]; then
            echo "No subject chosen. Bye." >&2
            exit 1
        fi
        echo $subject
        return 0
    done
}
```

该函数首先使用 `ls` 命令和命令替换将主题目录列表放入 `subjects` 数组。接下来，`select` 结构（第 917 页）向用户展示主题列表（由 `ls` 找到的目录），并将所选目录名称分配给 `subject` 变量。最后，函数将主题目录的名称写入标准输出。主程序使用命令替换将此值分配给 `subject` 变量 `[subject=$(choose_subj)]`。

`scramble` 函数提出了许多困难。在此解决方案中，它使用数组变量（`questions`）来存储问题名称。它使用 `RANDOM` 变量打乱数组中的条目（每次引用 `RANDOM` 时，它都有一个[随机]整数值，介于 0 和 32767 之间）：

```bash
function scramble ()
{
    typeset -i index quescount
    questions=(ls)
    quescount=${#questions[*]} # Number of elements
    ((index=quescount-1))
    while [[ $index > 0 ]]; do
        ((target=RANDOM % index))
        exchange $target $index
        ((index -= 1))
    done
}
```

此函数将数组变量 `questions` 初始化为工作目录中的文件名（问题）列表。变量 `quescount` 被设置为这些文件的数量。然后使用以下算法：让变量 `index` 从 `quescount - 1`（数组变量中最后一个条目的索引）倒数。对于 `index` 的每个值，函数在 0 和 `index` 之间（包括两端）选择一个随机值 `target`。命令

```bash
((target=RANDOM % index))
```

通过取 `$RANDOM` 除以 `index` 的余数（`%` 运算符），生成 0 到 `index - 1` 之间的随机值。然后函数交换 `questions` 中位置 `target` 和 `index` 处的元素。在名为 `exchange` 的另一个函数中执行此操作是很方便的。

