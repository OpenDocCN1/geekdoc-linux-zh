
编写 `initialize` 函数的一种方法如下。`cd` 命令使 `QUIZDIR` 成为脚本其余部分的工作目录，如果未设置 `QUIZDIR`，则默认为 `~/quiz`。

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

下一个函数 `choose_subj` 稍复杂一些。它使用 `select` 语句显示菜单：

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

```bash
function exchange ()
{
    temp_value=${questions[$1]}
    questions[$1]=${questions[$2]}
    questions[$2]=$temp_value
}
```

`ask` 函数也使用了 `select` 结构。它读取参数中指定的问题文件，并使用该文件的内容来呈现问题、接受答案以及判断答案是否正确。（见下文代码。）

`ask` 函数使用文件描述符 3 从问题文件中逐行读取数据，该文件名作为参数传入，在函数中由 `$1` 表示。它将问题读取到 `ques` 变量中，将问题数量读取到 `num_opts` 中。该函数通过初始化为空字符串并依次追加下一个选项来构建 `choices` 变量。然后，它将 `PS3` 设置为 `ques` 的值，并使用 `select` 结构以 `ques` 提示用户。`select` 结构将用户的答案存储在 `answer` 中，然后函数将其与文件中的正确答案进行比对。

`choices` 变量的构建方式旨在避免潜在问题。假设某个答案中包含空白字符。那么它在 `choices` 中可能会表现为两个或多个参数。为避免此问题，请确保 `choices` 是一个数组变量。`select` 语句会完成其余的工作：

```bash
$ cat quiz

#!/bin/bash

# 移除下一行前面的 # 以开启调试功能

# set -o xtrace

#=====================

function initialize()
{
    trap 'summarize ; exit 0' INT     # 处理用户中断
    num_ques=0                        # 迄今为止提出的问题数量
    num_correct=0                     # 迄今为止答对的题目数量
    first_time=true                   # 直到提出第一个问题前都为 true
    cd ${QUIZDIR:-~/quiz} || exit 2
}

#=====================

function choose_subj ()
{
    subjects=$( (ls) )
    PS3="从上述列表中为测验选择一个主题："
    select Subject in ${subjects[@]}; do
        if [[ -z "$Subject " ]]; then
            echo "未选择主题。再见。">&2
            exit 1
        fi
        echo $Subject
        return 0
    done
}

###############

function exchange ()
{
temp_value=${questions[$1]}
questions[$1]=${questions[$2]}
questions[$2]=$temp_value
}

###############

function scramble ()
{
typeset -i index quescount
questions=$( $! )
quescount=${#questions[*]}      # 元素数量
((index=quescount-1))
while [[ $index > 0 % ]]; do
   ((target=RANDOM % index))
   exchange $target $index
   ((index -= 1))
done
}

###############

function ask ()
{
exec 3<$1
read -u3 ques || exit 2
read -u3 num_opts || exit 2
index=0
choices=()
while (( index < num_opts )); do
    read -u3 next_choice || exit 2
    choices="${choices[$]}" "$next_choice"
    ((index += 1))
done
read -u3 correct_answer || exit 2
exec 3<&-
if [[ $first_time = true ]]; then
first_time=false
echo -e "您可以随时按下中断键退出。\n"
fi
PS3="$ques"    # 使 $ques 成为 select 的提示符
                                   # 并添加一些空格以提高可读性。
```
